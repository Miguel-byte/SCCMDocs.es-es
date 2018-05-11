---
title: Planeamiento de MDM local
titleSuffix: Configuration Manager
description: Planee la administración de dispositivos móviles local para administrar dispositivos en System Center Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 02979fb8-ea7e-4ec6-b7e0-ecbfda73e52d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 10cddac80b9a7ea4bd912e2f52585cdcef7e70da
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="plan-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>Planear la administración de dispositivos móviles (MDM) local con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Tenga en cuenta los siguientes requisitos antes de preparar la infraestructura de Configuration Manager para tratar la administración de dispositivos móviles local.

##  <a name="bkmk_devices"></a> Dispositivos compatibles  
 La administración de dispositivos móviles local le permite administrar dispositivos móviles mediante las funciones de administración integradas en los sistemas operativos de los dispositivos.  La función de administración se basa en el estándar de administración de dispositivos (DM) Open Mobile Alliance (OMA) y muchas plataformas de dispositivo usan este estándar para permitir que se administren los dispositivos.  Los denominamos **dispositivos modernos** (en la documentación y en la interfaz de usuario de la consola de Configuration Manager) para distinguirlos de otros dispositivos que requieren el cliente de Configuration Manager para administrarlos.  

 > [!NOTE]  
>  La rama actual de Configuration Manager admite la inscripción en la administración local de dispositivos móviles para dispositivos con los sistemas operativos siguientes:  
>   
> -  Windows 10 Enterprise  
> -   Windows 10 Pro  
> -   Windows 10 Team \(a partir de la versión 1602 de Configuration Manager\)  
> -   Windows 10 Mobile  
> -   Windows 10 Mobile Enterprise
> -   Windows 10 IoT Enterprise   

##  <a name="bkmk_intune"></a> Uso de la suscripción a Microsoft Intune  
 Necesitará una suscripción a Microsoft Intune para empezar a usar la administración de dispositivos móviles local. La suscripción solo es necesaria para realizar el seguimiento de las licencias de los dispositivos y no se usa para administrar ni almacenar la información de administración de los dispositivos. La totalidad de la administración se controla en la empresa de la organización a través de la infraestructura local de Configuration Manager.  

 > [!NOTE]  
 > A partir de la versión 1610, Configuration Manager admite la administración de dispositivos móviles mediante el uso de Microsoft Intune y la infraestructura de Configuration Manager local al mismo tiempo.   

 Si el sitio tiene dispositivos con conectividad a Internet, el servicio de Intune puede usarse para notificar a los dispositivos que busquen actualizaciones de directivas en el punto de administración de dispositivos. Este uso de Intune está estrictamente destinado para la notificación de dispositivos que solo son accesibles a través de Internet. Los dispositivos sin conexión a Internet (y con los que Intune no puede establecer una comunicación) se basan en el intervalo de sondeo configurado para conectarse con roles de sistema de sitio para las funciones de administración.  

> [!TIP]  
>  Se recomienda configurar Intune antes de instalar los roles de sistema de sitio requeridos con el fin de minimizar el tiempo necesario para que tales roles puedan funcionar.  

 Para obtener información sobre cómo configurar la suscripción a Intune, consulte [Configurar una suscripción de Microsoft Intune para la administración de dispositivos móviles local en System Center Configuration Manager](../../mdm/get-started/set-up-intune-subscription-on-premises-mdm.md).  

##  <a name="bkmk_roles"></a> Agregar los roles de sistema de sitio requeridos  
 La administración de dispositivos móviles local requiere, como mínimo, uno de cada uno de los siguientes roles de sistema de sitio:  

-   **Punto de proxy de inscripción** para admitir las solicitudes de inscripción.  

-   **Punto de inscripción** para admitir la inscripción de dispositivos.  

-   **Punto de administración de dispositivos** para la entrega de directivas. Este rol de sistema de sitio es una variación del rol de punto de administración que se ha configurado para permitir la administración de dispositivos móviles.  

-   **Punto de distribución** para la entrega de contenido.  

-   **Punto de conexión de servicio** para conectarse a Intune para notificar a los dispositivos que están fuera del firewall.  

 Estos roles de sistema de sitio se pueden instalar en el servidor de sistema de sitio único o pueden ejecutarse por separado en servidores diferentes, según las necesidades de la organización. Cada servidor de sistema de sitio que se usa para la administración de dispositivos móviles local debe estar configurado como un extremo HTTPS para comunicarse con dispositivos de confianza. Para obtener más información, vea [Comunicaciones de confianza requeridas](#bkmk_trustedComs).  

 Para obtener más información sobre el planeamiento para roles de sistema de sitio, consulte [Planificar los roles de sistema de sitio y los servidores de sistema de sitio en System Center Configuration Manager](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md).  

 Para obtener más información sobre cómo agregar los roles de sistema de sitio requeridos, consulte [Instalar los roles para la administración de dispositivos móviles local en System Center Configuration Manager](../../mdm/get-started/install-site-system-roles-for-on-premises-mdm.md).  

##  <a name="bkmk_trustedComs"></a> Comunicaciones de confianza requeridas  
 La administración de dispositivos móviles local requiere que los roles de sistema de sitio se habiliten para comunicaciones HTTPS. Según sus necesidades, puede usar la entidad de certificación (CA) de la empresa para establecer las conexiones de confianza entre servidores y dispositivos o podría usar una entidad de certificación disponible públicamente para que sea la autoridad de confianza.  De cualquier modo, necesitará un certificado de servidor web configurado con IIS en los servidores de sistema de sitio que hospedan los roles de sistema de sitio requeridos. También necesitará que el certificado raíz de esa entidad de certificación esté instalado en los dispositivos que deben conectarse a esos servidores.  

 Si usa la entidad de certificación de su empresa para establecer comunicaciones de confianza, debe realizar las tareas siguientes:  

-   Crear y emitir la plantilla de certificado de servidor web en la entidad de certificación.  

-   Solicitar un certificado de servidor web por cada servidor de sistema de sitio que hospede un rol de sistema de sitio.  

-   Configurar IIS en el servidor de sistema de sitio para que use el certificado de servidor web solicitado.  

 Para dispositivos unidos al dominio de Active Directory corporativo, el certificado raíz de la entidad de certificación de la empresa ya está disponible en el dispositivo para las conexiones de confianza. Esto significa que los dispositivos unidos a un dominio (por ejemplo, los equipos de escritorio) automáticamente serán de confianza para las conexiones HTTPS con los servidores de sistema de sitio. Sin embargo, los dispositivos no unidos a un dominio (normalmente los dispositivos móviles) no tendrán instalado el certificado raíz requerido. En estos dispositivos, será necesario instalar manualmente el certificado raíz para que puedan comunicarse correctamente con los servidores de sistema de sitio que admiten la administración de dispositivos móviles local.  

 Debe exportar el certificado raíz de la entidad de certificación emisora para su uso por parte de dispositivos individuales. Para obtener el archivo del certificado raíz, puede exportarlo mediante la entidad de certificación o, como alternativa más sencilla, puede usar el certificado de servidor web emitido por la entidad de certificación para extraer la raíz y crear un archivo de certificado raíz.   A continuación, se debe enviar el certificado raíz al dispositivo.  Ejemplos de métodos de entrega:  

-   Sistema de archivos  

-   Datos adjuntos de correo electrónico  

-   Tarjeta de memoria  

-   Dispositivo anclado a red  

-   Almacenamiento en la nube (por ejemplo, OneDrive)  

-   Conexión NFC (transmisión de datos en proximidad)  

-   Escáner de códigos de barras  

-   Paquete de aprovisionamiento de configuración rápida (OOBE)  

 Para obtener más información, consulte [Configurar certificados de comunicaciones de confianza para la administración de dispositivos móviles local en System Center Configuration Manager](../../mdm/get-started/set-up-certificates-on-premises-mdm.md).  

##  <a name="bkmk_enrollment"></a> Consideraciones de inscripción  
 Para habilitar la inscripción de dispositivos para la administración de dispositivos móviles local, se debe conceder a los usuarios permiso de inscripción y, además, sus dispositivos deben ser capaces de establecer comunicaciones de confianza con los servidores de sistema de sitio que hospedan los roles de sistema de sitio necesarios.  

 La concesión de permiso de inscripción a los usuarios puede realizarse a través de la configuración de un perfil de inscripción en la configuración del cliente de Configuration Manager. Puede usar la configuración de cliente predeterminada para insertar el perfil de inscripción en todos los usuarios detectados, o bien puede configurar dicho perfil en la configuración de cliente personalizada e insertar esa configuración en una o varias recopilaciones de usuarios.  

 Una vez concedido el permiso de inscripción, los usuarios pueden inscribir sus dispositivos. Para realizar la inscripción, el dispositivo del usuario debe tener el certificado raíz de la entidad de certificación (CA) que emitió el certificado de servidor web. Este certificado de servidor web se usa en los servidores de sistema de sitio que hospedan los roles de sistema de sitio necesarios.  

 Como alternativa a la inscripción iniciada por el usuario, puede configurar un paquete de inscripción masiva que permita que el dispositivo se inscriba sin intervención del usuario. Este paquete se puede entregar al dispositivo antes del aprovisionamiento inicial para su uso o cuando el dispositivo pasa a través de su proceso de OOBE.  

 Para obtener más información sobre cómo configurar e inscribir dispositivos, vea:  

-   [Configurar la inscripción del dispositivo para la administración de dispositivos móviles local en System Center Configuration Manager](../../mdm/get-started/set-up-device-enrollment-on-premises-mdm.md)  

-   [Inscribir dispositivos para la administración local de dispositivos móviles en System Center Configuration Manager](../../mdm/deploy-use/enroll-devices-on-premises-mdm.md)  
