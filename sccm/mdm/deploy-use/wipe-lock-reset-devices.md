---
title: "Protección de datos mediante eliminación remota, bloqueo o restablecimiento de código de acceso mediante System Center Configuration Manager"
description: "Proteja los datos de su dispositivo mediante eliminación completa, eliminación selectiva, bloqueo remoto o restablecimiento del código de acceso mediante System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 770da7bd-02dd-474a-9604-93ff1ea0c1e4
caps.latest.revision: 18
caps.handback.revision: 0
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 49a2220616bb6c6734643885bf969245e4c67c77

---
# <a name="protect-data-with-remote-wipe-lock-or-passcode-reset-using-system-center-configuration-manager"></a>Protección de datos mediante eliminación remota, bloqueo o restablecimiento de código de acceso mediante System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Configuration Manager proporciona capacidades de eliminación selectiva, eliminación completa, bloqueo remoto y restablecimiento de código de acceso. Los dispositivos móviles pueden almacenar datos confidenciales y proporcionar acceso a muchos recursos corporativos. Para proteger dispositivos, puede emitir:  

-   Una eliminación de datos completa para restaurar el dispositivo a su configuración de fábrica.  

-   Una eliminación de datos selectiva para quitar solo los datos de empresa.  

-   Un bloqueo remoto para ayudar a proteger un dispositivo que puede haberse perdido.  

-   Restablecer la contraseña del dispositivo.  

##  <a name="full-wipe"></a>eliminación de datos completa  
 Podría emitir un comando de eliminación de datos del dispositivo cuando necesita proteger un dispositivo perdido o retirar un dispositivo del uso activo.  

 Emitir una **eliminación de datos completa** a un dispositivo para restaurar el dispositivo a sus valores predeterminados de fábrica. Esto quita todos los datos de empresa y de usuario así como la configuración.  Puede realizar una eliminación completa en dispositivos Windows Phone, iOS, Android y Windows 10.  

> [!NOTE]
> La eliminación en dispositivos de Windows 10 en versiones anteriores a la versión 1511 con menos de 4 GB de RAM puede provocar que el dispositivo no responda. [Obtenga más información](https://technet.microsoft.com/library/mt592024.aspx#full-wipe-disables-windows-10-devices-with-less-than-4-gb-ram).

### <a name="to-initiate-a-remote-wipe-from-the-configuration-manager-console"></a>Para iniciar un borrado remoto desde la consola de Configuration Manager  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad** y en **Dispositivos**. Como alternativa, puede hacer clic en **Recopilaciones de dispositivos** y seleccionar una recopilación.  

2.  Seleccione el dispositivo que desea retirar/borrar.  

3.  Haga clic en **Acciones de dispositivo remoto** en **Grupo de dispositivos**y, a continuación, seleccione **Retirar/borrar**.  

## <a name="selective-wipe"></a>eliminación selectiva  
 Emitir una **eliminación selectiva** a un dispositivo para quitar solo los datos de la compañía. La tabla siguiente describe para cada plataforma los datos que se eliminan y el efecto en los datos que permanece en el dispositivo después de una eliminación selectiva.  

 **iOS**  

|Contenido borrado al retirar un dispositivo|iOS|  
|--------------------------------------------|---------|  
|Aplicaciones y datos asociados de la compañía que se instalaron mediante Configuration Manager y Intune.|Las aplicaciones se desinstalarán. Se quitarán los datos de la aplicación de empresa.|  
|Perfiles de VPN y Wi-Fi|Quitado.|  
|Certificados|Quitado y revocado.|  
|Configuración|Quitado, excepto: **Permitir itinerancia de voz**, **Permitir itinerancia de datos** y **Permitir la sincronización automática durante la itinerancia**.|  
|Agente de administración|Se quitará el perfil de administración.|  
|Perfiles de correo electrónico|Para los perfiles de correo electrónico aprovisionados por Intune, se quitan la cuenta de correo electrónico y el correo electrónico.|  

 **Android y Android Samsung KNOX**  

|Contenido borrado al retirar un dispositivo|Android|Samsung KNOX|  
|--------------------------------------------|-------------|------------------|  
|Aplicaciones y datos asociados de la compañía que se instalaron mediante Configuration Manager y Intune.|Se mantendrán instalados los datos y las aplicaciones.|Las aplicaciones se desinstalarán.|  
|Perfiles de VPN y Wi-Fi|Quitado.|Quitado.|  
|Certificados|Revocado.|Revocado.|  
|Configuración|Requisitos quitados.|Requisitos quitados.|  
|Agente de administración|Se revocarán los privilegios del administrador de dispositivos.|Se revocarán los privilegios del administrador de dispositivos.|  
|Perfiles de correo electrónico|No aplicable.|Para los perfiles de correo electrónico aprovisionados por Intune, se quitan la cuenta de correo electrónico y el correo electrónico.|  

 **Windows 10, Windows 8.1, Windows RT 8.1 y Windows RT**  

|Contenido borrado al retirar un dispositivo|Windows 10, Windows 8.1 y Windows RT 8.1|Windows RT|  
|---------------------------------|-------------|-----------|
|Aplicaciones y datos asociados de la compañía que se instalaron mediante Configuration Manager y Intune.|Se desinstalan las aplicaciones y se quitan las claves de instalación de prueba. Se revocará la clave de cifrado de las aplicaciones que usan Windows Selective Wipe, y no se podrá tener acceso a los datos.|Se eliminan las claves de instalación de prueba pero las aplicaciones permanecen instaladas.|  
|Perfiles de VPN y Wi-Fi|Quitado.|No aplicable.|  
|Certificados|Quitado y revocado.|No aplicable.|  
|Configuración|Requisitos quitados.||  
|Agente de administración|No aplicable. El agente de administración está integrado.|No aplicable. El agente de administración está integrado.|  
|Perfiles de correo electrónico|Quita el correo electrónico habilitado para EFS que incluye la aplicación Correo para el correo electrónico y los datos adjuntos de Windows.|No aplicable.|  

 **Windows 10 Mobile, Windows Phone 8.0 y Windows Phone 8.1**  


 |Contenido borrado al retirar un dispositivo|Windows 10 Mobile, Windows Phone 8 y Windows Phone 8.1|  
|-|-|
|Aplicaciones y datos asociados de la compañía que se instalaron mediante Configuration Manager y Intune.|Las aplicaciones se desinstalarán. Se quitarán los datos de la aplicación de empresa.|  
|Perfiles de VPN y Wi-Fi|Quitado de Windows 10 Mobile y Windows Phone 8.1|  
|Certificados|Quitado en Windows Phone 8.1.|  
|Agente de administración|No aplicable. El agente de administración está integrado|  
|Perfiles de correo electrónico|Quitado (excepto Windows Phone 8.0)|  

 La siguiente configuración también se quita de los dispositivos Windows 10 Mobile y Windows Phone 8.1:  

-   Requerir una contraseña para desbloquear dispositivos móviles  

-   Permitir contraseñas sencillas  

-   Longitud mínima de contraseña  

-   Tipo de contraseña obligatoria  

-   Expiración de contraseña (días)  

-   Recordar el historial de contraseñas  

-   Número de errores de inicio de sesión repetidos que se permiten antes de que se borre el dispositivo  

-   Minutos de inactividad antes de que se pida la contraseña  

-   Tipo de contraseña requerida: número mínimo de conjuntos de caracteres  

-   Permitir cámara  

-   Requerir cifrado en dispositivo móvil  

-   Permitir almacenamiento extraíble  

-   Permitir explorador web  

-   Permitir almacén de aplicaciones  

-   Permitir captura de pantalla  

-   Permitir geolocalización  

-   Permitir cuenta de Microsoft  

-   Permitir copiar y pegar  

-   Permitir Wi-Fi Tethering  

-   Permitir la conexión automática a zonas Wi-Fi gratuitas  

-   Permitir informar de zonas Wi-Fi  

-   Permitir el restablecimiento de la configuración de fábrica  

-   Permitir Bluetooth  

-   Permitir NFC  

-   Permitir Wi-Fi  

### <a name="to-initiate-a-remote-wipe-from-the-configuration-manager-console"></a>Para iniciar un borrado remoto desde la consola de Configuration Manager  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad** y en **Dispositivos**. Como alternativa, puede hacer clic en **Recopilaciones de dispositivos** y seleccionar una recopilación.  

2.  Seleccione el dispositivo que desea retirar/borrar.  

3.  Haga clic en **Acciones de dispositivo remoto** en **Grupo de dispositivos**y, a continuación, seleccione **Retirar/borrar**.  

## <a name="wiping-encrypting-file-system-efs-enabled-content"></a>Eliminación de contenido habilitado para el sistema de archivos de cifrado (EFS)  
 El borrado selectivo de contenido cifrado de EFS es compatible con Windows 8.1 y Windows RT 8.1. La información siguiente es aplicable a un borrado selectivo de contenido habilitado para EFS:  

-   Solo se borran de forma selectiva las aplicaciones y los datos protegidos por EFS que usen el mismo dominio de Internet que la cuenta de Intune. Para obtener más información, consulte [Borrado selectivo de Windows para la administración de datos del dispositivo](http://technet.microsoft.com/library/dn486874.aspx).  

-   Si se producen cambios en el dominio asociado con EFS, esos cambios pueden tardar hasta 48 horas antes de que las aplicaciones y los datos que usen el nuevo dominio se puedan borrar de forma selectiva.  

-   Los dominios que estén registrados con Intune serán los dominios de los que se eliminarán los datos.  

 Los datos y las aplicaciones que son compatibles actualmente con el borrado selectivo de EFS son:  

-   Aplicación de correo para Windows  

-   Carpetas de trabajo  

-   Archivos y carpetas cifrados con EFS. Para obtener más información, consulte las [prácticas recomendadas para el sistema de cifrado de archivos](http://support.microsoft.com/kb/223316).  

### <a name="best-practices-for-selective-wipe"></a>Prácticas recomendadas para el borrado selectivo  

-   Para lograr un borrado correcto de correo electrónico, aprovisione los perfiles de correo electrónico a dispositivos iOS y Windows Phone 8.1.  

-   Para lograr un borrado correcto de aplicaciones, asegúrese de que estas se distribuyen a través de la administración de aplicaciones de dispositivos móviles.  

-   Para iOS, configure la opción “Permitir copia de seguridad en iCloud” en “No permitir” de modo que los usuarios no puedan restaurar el contenido con iCloud.  

-   Si se ha desactivado una cuenta, transcurrido un año Intune retirará la cuenta y se realizará un borrado selectivo.  

##  <a name="passcode-reset"></a>Restablecimiento de la contraseña  
 Si un usuario olvida su contraseña, puede ayudarle quitando la contraseña de un dispositivo o forzar el uso de una nueva contraseña temporal en un dispositivo. La tabla siguiente muestra el modo en que se puede restablecer la contraseña en distintas plataformas móviles.  

|Plataforma|Restablecimiento de la contraseña|  
|--------------|--------------------|  
|iOS|Permite borrar la contraseña de un dispositivo. No admite la creación de una nueva contraseña temporal.|  
|Android|Permite restablecer y crear una contraseña temporal.|  
|Windows 10|No se admite en este momento.|  
|Windows Phone 8 y Windows Phone 8.1|Compatible.|  
|Windows RT 8.1 y Windows RT|No compatible.|  
|Windows 8.1|No compatible.|  

### <a name="to-reset-the-passcode-on-a-mobile-device-remotely-in-configuration-manager"></a>Para restablecer el código de acceso de un dispositivo móvil de forma remota en Configuration Manager  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad** y en **Dispositivos**. Como alternativa, puede hacer clic en **Recopilaciones de dispositivos** y seleccionar una recopilación.  

2.  Seleccione el dispositivo o los dispositivos en los que se va a restablecer el código de acceso.  

3.  Haga clic en **Acciones de dispositivo remoto** en **Grupo de dispositivos**y, a continuación, seleccione **Restablecimiento de código de acceso**.  

### <a name="to-show-the-state-of-the-passcode-reset"></a>Para mostrar el estado de restablecimiento del código de acceso  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad** y en **Dispositivos**. Como alternativa, puede hacer clic en **Recopilaciones de dispositivos** y seleccionar una recopilación.  

2.  Seleccione el dispositivo o los dispositivos en los que se va a mostrar el estado de restablecimiento de código de acceso.  

3.  Haga clic en **Acciones de dispositivo remoto** en **Grupo de dispositivos**y, a continuación, seleccione **Mostrar estado del código de acceso**.  

##  <a name="remote-lock"></a>Bloqueo remoto  
 Si un usuario pierde su dispositivo, es posible bloquear el dispositivo de forma remota. La tabla siguiente muestra el modo en que se puede usar el bloqueo remoto en distintas plataformas móviles.  

|Plataforma|Bloqueo remoto|  
|--------------|-----------------|  
|iOS|Compatible.|  
|Android|Compatible.|  
|Windows 10|No se admite en este momento.|  
|Windows Phone 8 y Windows Phone 8.1|Compatible.|  
|Windows RT 8.1 y Windows RT|Compatible si el usuario actual del dispositivo es el mismo usuario que inscribió el dispositivo.|  
|Windows 8.1|Compatible si el usuario actual del dispositivo es el mismo usuario que inscribió el dispositivo.|  

### <a name="to-lock-a-mobile-device-remotely-through-the-configuration-manager-console"></a>Para bloquear un dispositivo móvil de forma remota a través de la consola de Configuration Manager  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad** y en **Dispositivos**. Como alternativa, puede hacer clic en **Recopilaciones de dispositivos** y seleccionar una recopilación.  

2.  Seleccione el dispositivo o los dispositivos para bloquear.  

3.  Haga clic en **Acciones de dispositivo remoto** en **Grupo de dispositivos**y, a continuación, seleccione **Bloqueo remoto**.  

### <a name="to-show-the-state-of-the-remote-lock"></a>Para mostrar el estado del bloqueo remoto  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad** y en **Dispositivos**. Como alternativa, puede hacer clic en **Recopilaciones de dispositivos** y seleccionar una recopilación.  

2.  Seleccione el dispositivo en el que se va a mostrar el estado del bloqueo remoto.  

3.  Haga clic en **Acciones de dispositivo remoto** en **Grupo de dispositivos**y, a continuación, seleccione **Mostrar estado de bloqueo remoto**.  

## <a name="see-also"></a>Véase también  
 [Borrado selectivo de Windows para la administración de datos del dispositivo](http://technet.microsoft.com/library/dn486874.aspx)   
 [Hybrid mobile device management (MDM) with System Center Configuration Manager and Microsoft Intune](../../mdm/plan-design/hybrid-mobile-device-management.md) (Administración híbrida de dispositivos móviles [MDM] con System Center Configuration Manager y Microsoft Intune)



<!--HONumber=Nov16_HO1-->


