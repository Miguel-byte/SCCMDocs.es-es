---
title: Inscripción masiva de dispositivos en MDM local
titleSuffix: Configuration Manager
description: Inscriba dispositivos en masa de forma automática con la administración local de dispositivos móviles en System Center Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: b36f5e4a-2b57-4d18-83f6-197081ac2a0a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 437f6e6068fb56f1a906cbb8bea24cd3c707f0e3
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="how-to-bulk-enroll-devices-with-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>Cómo inscribir dispositivos en masa con la administración local de dispositivos móviles en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*


La inscripción en masa de la administración local de dispositivos móviles de System Center Configuration Manager es una forma más automatizada de inscribir dispositivos si se compara con la inscripción de usuario, que exige que los usuarios escriban sus credenciales para inscribir el dispositivo.  La inscripción masiva usa un paquete de inscripción para autenticar el dispositivo durante la inscripción. El paquete (un archivo .ppkg) contiene un perfil de certificado y, opcionalmente, un perfil de Wi-Fi si el dispositivo necesita conectividad de la intranet para admitir la inscripción.  

> [!NOTE]  
>  La rama actual de Configuration Manager admite la inscripción en la administración local de dispositivos móviles para dispositivos con los sistemas operativos siguientes:  
>   
> -  Windows 10 Enterprise  
> -   Windows 10 Pro  
> -   Windows 10 Team  
> -   Windows 10 Mobile  
> -   Windows 10 Mobile Enterprise
> -   Windows 10 IoT Enterprise   

En las tareas siguientes se explica cómo inscribir equipos y dispositivos en masa para la administración local de dispositivos móviles:  

-   [Crear un perfil de certificado](#bkmk_createCert)  

-   [Crear un perfil de Wi-Fi](#CreateWifi)  

-   [Crear un perfil de inscripción](#bkmk_createEnroll)  

-   [Crear un archivo de paquete de inscripción (.ppkg)](#bkmk_createPpkg)  

-   [Use el paquete para la inscripción masiva de un dispositivo](#bkmk_getPpkg)  

-   [Comprobar la inscripción del dispositivo](#bkmk_verifyEnroll)  

##  <a name="bkmk_createCert"></a> Crear un perfil de certificado  
 El componente principal del paquete de inscripción es un perfil de certificado, que se usa para aprovisionar automáticamente un certificado raíz de confianza para el dispositivo que se está inscribiendo.  Este certificado raíz es necesario para la comunicación de confianza entre los dispositivos y los roles de sistema de sitio necesarios para la administración local de dispositivos móviles. Sin el certificado raíz, el dispositivo no sería de confianza en las conexiones HTTPS entre este y los servidores que hospedan los roles de sistema de sitio del punto de administración de dispositivos, el punto de inscripción, el punto de proxy de inscripción y el punto de distribución.  

 Como parte de la preparación del sistema para la administración local de dispositivos móviles, debe exportar un certificado raíz que pueda usar en el perfil de certificado del paquete de inscripción. Para obtener instrucciones sobre cómo obtener el certificado raíz de confianza, vea [Export the certificate with the same root as the web server certificate (Exportar el certificado con la misma raíz que el certificado de servidor web)](../../mdm/get-started/set-up-certificates-on-premises-mdm.md#bkmk_exportCert).  

 Use el certificado raíz exportado para crear un perfil de certificado. Para obtener instrucciones, vea [Creación de perfiles de certificado en Configuration Manager](../../protect/deploy-use/create-certificate-profiles.md).  

##  <a name="CreateWifi"></a> Crear un perfil de Wi-Fi  
 El otro componente del paquete usado para la inscripción masiva es un perfil de Wi-Fi. Es posible que algunos dispositivos no tengan la conectividad de red necesaria para admitir la inscripción hasta que se aprovisione una configuración de red. La inclusión de un perfil de Wi-Fi en el paquete de inscripción proporciona un medio para establecer la conectividad de red para el dispositivo.  

 Para crear un perfil de Wi-Fi en Configuration Manager, siga las instrucciones de [Creación de perfiles de Wi-Fi en Configuration Manager](../../protect/deploy-use/create-wifi-profiles.md).  

> [!IMPORTANT]  
>Al crear un perfil de Wi-Fi para la inscripción en masa, tenga en cuenta las dos cuestiones siguientes:
>
> - La rama actual de Configuration Manager solo admite las siguientes configuraciones de seguridad de Wi-Fi para la administración local de dispositivos móviles:  
>   
>   - Tipos de seguridad: **WPA2 Enterprise** o **WPA2 Personal**  
>   - Tipos de cifrado: **AES** o **TKIP**  
>   - Tipos de EAP: **tarjeta inteligente u otro certificado** o **PEAP**  
>
>
> - Aunque Configuration Manager tiene un valor para la información del servidor proxy en el perfil de Wi-Fi, no configura el proxy al inscribir el dispositivo. Si necesita configurar un servidor proxy con los dispositivos inscritos, puede implementar la configuración mediante elementos de configuración una vez que los dispositivos estén inscritos o crear el segundo paquete mediante el Diseñador de imágenes y configuraciones de Windows (ICD) para implementarlo junto con el paquete de inscripción en masa.

##  <a name="bkmk_createEnroll"></a> Crear un perfil de inscripción  
 El perfil de inscripción permite especificar los parámetros necesarios para la inscripción de dispositivos, incluido un perfil de certificado que proporcionará de forma dinámica un certificado raíz de confianza al dispositivo y un perfil de Wi-Fi que proporcionará la configuración de red si es necesario.  

 Antes de crear un perfil de inscripción, asegúrese de que tiene un perfil de certificado y un perfil de Wi-Fi (si es necesario) creados. Para obtener más información, vea [Crear un perfil de certificado](#bkmk_createCert) y [Crear un perfil de Wi-Fi](#CreateWifi).  

#### <a name="to-create-an-enrollment-profile"></a>Para crear un perfil de inscripción:  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad** >**Información general** >**Todos los dispositivos corporativos** >**Windows** >**Perfiles de inscripción**.  

2.  Haga clic con el botón derecho en **Perfil de inscripción** y, después, haga clic en **Crear perfil**.  

3.  En el Asistente para crear perfil de inscripción, escriba un nombre para el perfil, asegúrese de que **Local** sea la opción seleccionada en **Entidad de administración**y, después, haga clic en **Siguiente**.  

4.  Seleccione el código de sitio y haga clic en **Siguiente**.  

5.  Seleccione **Solo intranet**, elija los puntos de proxy de inscripción que el dispositivo usará para iniciar el proceso de inscripción y, después, haga clic en **Siguiente**.  

6.  Seleccione el perfil de certificado que contiene el certificado raíz de confianza (el perfil que creó en [Create a certificate profile](#bkmk_createCert)) y haga clic en **Siguiente**.  

7.  Seleccione el perfil de W-Fi que contiene la configuración de red necesaria para que los dispositivos se conecten a la intranet (perfil que creó en [Create a Wi-Fi profile](#CreateWifi)) y haga clic en **Siguiente**.  

    > [!NOTE]  
    >  Si no usa un perfil de Wi-Fi para el paquete de inscripción, omita esta etapa.  

8.  Confirme la configuración del perfil de inscripción y haga clic en **Siguiente**. Haga clic en **Cerrar** para salir del asistente.  

##  <a name="bkmk_createPpkg"></a> Crear un archivo de paquete de inscripción (.ppkg)  
 El paquete de inscripción es el archivo que se usa para la inscripción en masa en la administración local de dispositivos móviles.  Este archivo debe crearse con Configuration Manager. Puede crear tipos similares de paquetes con el Diseñador de imágenes y configuraciones de Windows (ICD), pero solo los paquetes que se creen en Configuration Manager podrán usarse para inscribir dispositivos en la administración local de dispositivos móviles de principio a fin. Los paquetes creados con Windows ICD solo pueden proporcionar el nombre principal de usuario (UPN) necesario para la inscripción, pero no ejecutar el proceso de inscripción real.  

 El proceso para crear el paquete de inscripción requiere Windows Assessment and Deployment Kit (ADK) para Windows 10.  En el servidor que ejecuta la consola de Configuration Manager, asegúrese de tener instalada la versión 1511 de Windows ADK. Para más información, consulte la sección sobre ADK de la página de [descarga de kits y herramientas para Windows 10](https://msdn.microsoft.com/windows/hardware/dn913721.aspx)  

> [!TIP]  
>  Si quita un paquete de inscripción de la consola de Configuration Manager, este no podrá usarse para inscribir dispositivos. Puede usar la eliminación de paquetes como una manera de administrar paquetes que ya no desea usar para la inscripción masiva de dispositivos.  

#### <a name="to-create-an-enrollment-package-ppkg-file"></a>Para crear un archivo de paquete de inscripción (.ppkg):  

1.  Haga doble clic en el perfil que acaba de crear (en [Crear un perfil de inscripción](#bkmk_createEnroll)y haga clic en **Exportar**.  

2.  Haga clic en **Examinar**, busque una ubicación para guardar el archivo .ppkg, escriba un nombre para el paquete y, después, haga clic en **Guardar**.  

3.  Si quiere proteger con contraseña el paquete, haga clic en la casilla junto a **Cifrar paquete**; luego, haga clic en **Exportar** y espere unos 10 segundos hasta que finalice la exportación.  

    > [!NOTE]  
    >  Si se cifra el paquete, Configuration Manager proporciona un mensaje con la contraseña descifrada. Asegúrese de que guardar la información de contraseña, porque lo necesitará al aprovisionar el paquete en los dispositivos.  

4.  Haga clic en **Aceptar**.  

##  <a name="bkmk_getPpkg"></a> Use el paquete para la inscripción masiva de un dispositivo  
 Puede usar el paquete para inscribir dispositivos antes o después de aprovisionar el dispositivo a través del proceso de experiencia inmediata (OOBE).   El paquete de inscripción también se puede incluir como parte del paquete de aprovisionamiento de un fabricante de equipos originales (OEM).  

 El paquete debe entregarse físicamente al dispositivo para usarlo para la inscripción masiva. Puede entregar el paquete de inscripción al dispositivo de varias maneras según sus necesidades, incluidas las siguientes:  

-   Copia desde el sistema de archivos  

-   Archivo adjunto a correo electrónico  

-   Copia a través de la conexión NFC (transmisión de datos en proximidad)  

-   Copia desde la tarjeta de memoria  

-   Digitalización de código de barras  

-   Copia desde un dispositivo anclado a red  

-   Inclusión en el paquete de aprovisionamiento de OEM  

#### <a name="to-bulk-enroll-a-device"></a>Para inscribir un dispositivo de forma masiva:  

1.  En el dispositivo que quiere inscribir, busque el paquete de inscripción (mediante el Explorador de archivos) y haga doble clic en el archivo .ppkg.  

2.  En el mensaje Control de cuentas de usuario, haga clic en **Sí** .  

3.  En el cuadro de diálogo que pregunta si el paquete procede de un origen de confianza, haga clic en **Sí, agregarlo**.  

     El proceso de inscripción se inicia y tarda aproximadamente 5 minutos.  

4.  Abra **Configuración**.  

5.  Haga clic en  **Cuentas** > **Acceso al trabajo**. Si la inscripción se realiza correctamente, verá una cuenta en **Aplicaciones de empresa**  

6.  Haga clic en la cuenta y luego en **Sincronizar** para iniciar la administración con Configuration Manager.  

##  <a name="bkmk_verifyEnroll"></a> Comprobar la inscripción del dispositivo  
 Puede comprobar que los dispositivos están inscritos correctamente en la consola de Configuration Manager.  

-   Inicie la consola de Configuration Manager.  

-   Haga clic en **Activos y compatibilidad** > **Introducción** > **Dispositivos**. El dispositivo inscrito aparece en la lista.  
