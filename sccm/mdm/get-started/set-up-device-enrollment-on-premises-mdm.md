---
title: 'Configurar la inscripción de dispositivos '
titleSuffix: Configuration Manager
description: Conceda permiso a los usuarios para que inscriban sus dispositivos para la administración local de dispositivos móviles en System Center Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 9ffaea91-1379-4b86-9953-b25e152f56a9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7d0424b662df4baba7374685dd7631347501352c
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32349089"
---
# <a name="set-up-device-enrollment-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>Configure la inscripción del dispositivo para Administración de dispositivos móviles local en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Para que los usuarios puedan inscribir sus dispositivos en la administración local de dispositivos móviles de System Center Configuration Manager, tiene que concederles el permiso para llevarlo a cabo. Para conceder permiso a los usuarios para inscribir dispositivos, realice las siguientes tareas.

-   [Crear un perfil de inscripción que permita a los usuarios inscribir dispositivos modernos](#bkmk_createProf)  

-   [Definición de configuración de cliente adicional para dispositivos inscritos](#bkmk_addClient)  

-   [Permitir a los usuarios recibir el perfil de inscripción de dispositivos modernos](#bkmk_enableUsers)  

-   [Almacenar el certificado raíz en dispositivos que se van a inscribir](#bkmk_storeCert)  

##  <a name="bkmk_createProf"></a> Crear un perfil de inscripción que permita a los usuarios inscribir dispositivos modernos  
 Para insertar la configuración necesaria para permitir a los usuarios inscribir dispositivos modernos, puede agregar un nuevo perfil de inscripción a la configuración de cliente predeterminada, que se aplica a todos los usuarios detectados en el sitio de Configuration Manager.  

1.  En la consola de Configuration Manager, haga clic en **Administración** > **Introducción** > **Configuración de cliente**, abra **Configuración de cliente predeterminada** y seleccione **Inscripción**.  

2.  En Configuración del dispositivo, especifique el intervalo de sondeo para los dispositivos modernos.  

3.  En Configuración de usuario, seleccione **Sí** para **Permitir a los usuarios inscribir dispositivos modernos**.  

4.  Junto a **Perfil de inscripción de dispositivo moderno**, haga clic en **Establecer perfil...** y luego haga clic en **Crear...**  

5.  En Crear perfil de inscripción, escriba un nombre para el perfil de inscripción y elija el código de sitio de administración que quiere que usen los usuarios con el perfil de inscripción. Haga clic en **Aceptar** varias veces para salir de la página Configuración predeterminada.  

> [!NOTE]  
>  Si quiere implementar el perfil de inscripción en un subconjunto de usuarios detectados, puede usar una recopilación de usuarios y crear la configuración de cliente personalizada para implementar en esa recopilación. Para obtener información sobre cómo crear configuraciones de cliente personalizadas, consulte [How to configure client settings in System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md) (Cómo configurar el cliente en System Center Configuration Manager)  

##  <a name="bkmk_addClient"></a> Definición de configuración de cliente adicional para dispositivos inscritos  
 Además de configurar el perfil de inscripción para los dispositivos modernos, también puede establecer otra configuración de cliente adicional para definir los ajustes de los dispositivos cuando están inscritos.  Para obtener información sobre cómo configurar clientes, consulte [How to configure client settings in System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md) (Cómo configurar el cliente en System Center Configuration Manager).  

 No todas las configuraciones de cliente están disponibles en la administración local de dispositivos móviles. La rama actual de Configuration Manager admite las siguientes configuraciones de cliente en la administración local de dispositivos móviles:  

-   Inscripción: esta configuración especifica el perfil de inscripción de dispositivos administrados. Para más información acerca de cómo configurar un perfil de inscripción, consulte [Crear un perfil de inscripción que permita a los usuarios inscribir dispositivos modernos](#bkmk_createProf).  

-   Directiva de cliente: esta configuración especifica la frecuencia de descarga de la directiva de cliente en el dispositivo. También puede habilitar la configuración para dirigirse a usuarios con el sondeo de directiva. Para obtener más información sobre la configuración de la directiva de cliente, consulte la sección Directiva de cliente en [Acerca de la configuración de cliente en System Center Configuration Manager](../../core/clients/deploy/about-client-settings.md).  

-   Implementación de software: esta opción establece el intervalo para evaluar los dispositivos cliente para implementaciones de software. Para obtener más información sobre la configuración de la implementación de software, consulte la sección Implementación de software en [Acerca de la configuración de cliente en System Center Configuration Manager](../../core/clients/deploy/about-client-settings.md)  

    > [!NOTE]  
    >  En la administración local de dispositivos móviles, la configuración de implementación de software solo puede usarse como configuración predeterminada del cliente. No se puede usar la configuración de implementación de software con la configuración de cliente personalizada en la rama actual de Configuration Manager.  

##  <a name="bkmk_enableUsers"></a> Permitir a los usuarios recibir el perfil de inscripción de dispositivos modernos  
 Para que los usuarios reciban la configuración de cliente modificada con el perfil de inscripción para la administración local de dispositivos móviles, debe detectarse mediante el método de detección de Active Directory. Para asegurarse de que todos los usuarios que necesiten el perfil de inscripción lo obtengan, ejecute la detección para usuarios de Active Directory. Para obtener instrucciones sobre cómo detectar usuarios, consulte [Run discovery for System Center Configuration Manager](../../core/servers/deploy/configure/run-discovery.md) (Ejecutar la detección en System Center Configuration Manager).  

##  <a name="bkmk_storeCert"></a> Almacenar el certificado raíz en dispositivos que se van a inscribir  
 Los usuarios con dispositivos unidos a un dominio ya tendrán probablemente el certificado raíz necesario para la comunicación de confianza con los servidores que hospedan los roles de sistema de sitio porque la raíz se emitió como parte del proceso de unión al dominio con Active Directory. Ningún equipo o dispositivo móvil unido al dominio necesitará tener instalado el certificado raíz de forma manual en el dispositivo para permitir que la inscripción tenga lugar. Estos dispositivos no tendrán el certificado raíz necesario de forma automática.  

 El archivo de certificado exportado debe proporcionarse en el dispositivo para la instalación manual. Esto puede hacerse mediante correo electrónico, OneDrive, tarjeta SD, unidad de memoria USB o cualquier método que se adapte mejor a sus necesidades.  

 El certificado raíz que quiere usar en los dispositivos es el que exportó en [Exportar el certificado con la misma raíz que el certificado de servidor web](../../mdm/get-started/set-up-certificates-on-premises-mdm.md#bkmk_exportCert).  

1.  En el dispositivo que se va a inscribir, ubique el archivo de certificado raíz y haga doble clic en él.  

2.  En la ventana Certificado, haga clic en **Instalar certificado…**  

3.  En el Asistente para importación de certificados, seleccione **Equipo local**y haga clic en **Siguiente**.  

4.  En la ventana Control de cuentas de usuario, haga clic en **Sí**.  

5.  Seleccione **Colocar todos los certificados en el siguiente almacén**y haga clic en **Examinar**.  

6.  Haga clic en **Entidades de certificación raíz de confianza**, haga clic en **Aceptar**y, luego, en **Siguiente**.  

7.  Haga clic en **Finalizar**.  
