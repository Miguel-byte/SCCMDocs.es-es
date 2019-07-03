---
title: Protección de los datos con borrado, bloqueo o restablecimiento de contraseña de forma remota
titleSuffix: Configuration Manager
description: Proteja los datos del dispositivo mediante borrado completo, borrado selectivo, bloqueo remoto o restablecimiento del código de acceso con Configuration Manager.
ms.date: 08/14/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 770da7bd-02dd-474a-9604-93ff1ea0c1e4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0a50dd4df66292837cd7a3667a0790c04ebddb9a
ms.sourcegitcommit: 4981a796e7886befb7bdeeb346dba32be82aefd6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2019
ms.locfileid: "67516027"
---
# <a name="protect-data-with-remote-wipe-lock-or-passcode-reset-by-using-configuration-manager"></a>Protección de datos mediante borrado remoto, bloqueo o restablecimiento de código de acceso con Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Configuration Manager proporciona capacidades de eliminación selectiva, eliminación completa, bloqueo remoto y restablecimiento de código de acceso. Los dispositivos móviles pueden almacenar datos confidenciales y proporcionar acceso a muchos recursos corporativos. Para proteger dispositivos, puede emitir:  

- Una eliminación de datos completa para restaurar el dispositivo a su configuración de fábrica.  

- Una eliminación de datos selectiva para quitar solo los datos de empresa.  

- Un bloqueo remoto para ayudar a proteger un dispositivo que puede haberse perdido.  

- Un restablecimiento del código de acceso del dispositivo.  

> [!Important]  
> Desde el 14 de agosto de 2018, la administración híbrida de dispositivos móviles es una [característica en desuso](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). Para más información, vea [¿Qué es la Administración híbrida de dispositivos móviles (MDM)?](/sccm/mdm/understand/hybrid-mobile-device-management).<!--Intune feature 2683117-->  



## <a name="full-wipe"></a>Eliminación completa  

Podría emitir un comando de eliminación de datos del dispositivo cuando necesita proteger un dispositivo perdido o retirar un dispositivo del uso activo.  

Emitir una **eliminación de datos completa** a un dispositivo para restaurar el dispositivo a sus valores predeterminados de fábrica. Esto quita todos los datos de empresa y de usuario así como la configuración. Puede realizar una eliminación completa en dispositivos Windows Phone, iOS, Android y Windows 10.  

> [!NOTE]
> Solo puede realizar un borrado completo en dispositivos propiedad de la empresa.

> [!NOTE]
> La eliminación en dispositivos de Windows 10 en versiones anteriores a la versión 1511 con menos de 4 GB de RAM puede provocar que el dispositivo no responda. [Obtenga más información](https://technet.microsoft.com/library/mt592024.aspx#full-wipe-disables-windows-10-devices-with-less-than-4-gb-ram).

#### <a name="to-initiate-a-remote-wipe-from-the-configuration-manager-console"></a>Para iniciar un borrado remoto desde la consola de Configuration Manager  

1. En la consola de Configuration Manager, seleccione **Activos y compatibilidad** y elija **Dispositivos**. Como alternativa, puede elegir **Colecciones de dispositivos** y seleccionar una colección.  

2. Seleccione el dispositivo que desea retirar/borrar.  

3. Elija **Acciones de dispositivo remoto** en **Grupo de dispositivos** y, a continuación, **Retirar/borrar**.  



## <a name="selective-wipe"></a>Borrado selectivo  

Emitir una **eliminación selectiva** a un dispositivo para quitar solo los datos de la compañía. En la tabla siguiente se describen los datos que se eliminan para cada plataforma y el efecto en los datos que permanecen en el dispositivo después de un borrado selectivo.  

**iOS**  

|Contenido borrado al retirar un dispositivo|iOS|  
|--------------------------------------------|---------|  
|Aplicaciones y datos asociados de la empresa que se instalaron mediante Configuration Manager e Intune|Las aplicaciones se desinstalarán. Se quitarán los datos de la aplicación de empresa.|  
|Perfiles de VPN y Wi-Fi|Quitado.|  
|Certificados|Quitado y revocado.|  
|Configuración|Quitado, excepto: **Permitir itinerancia de voz**, **Permitir itinerancia de datos**, y **permitir la sincronización automática durante la itinerancia**.|  
|Agente de administración|Se quitará el perfil de administración.|  
|Perfiles de correo electrónico|Para los perfiles de correo electrónico configurados mediante Intune, se quitan la cuenta de correo electrónico y el correo electrónico.|  

**Android y Android Samsung KNOX Standard**  

|Contenido borrado al retirar un dispositivo|Android|Samsung KNOX Standard|  
|--------------------------------------------|-------------|------------------|  
|Aplicaciones y datos asociados de la empresa que se instalaron mediante Configuration Manager e Intune|Se mantendrán instalados los datos y las aplicaciones.|Las aplicaciones se desinstalarán.|  
|Perfiles de VPN y Wi-Fi|Quitado.|Quitado.|  
|Certificados|Revocado.|Revocado.|  
|Configuración|Se quitan los requisitos.|Se quitan los requisitos.|  
|Agente de administración|Se revocarán los privilegios del administrador de dispositivos.|Se revocarán los privilegios del administrador de dispositivos.|  
|Perfiles de correo electrónico|No aplicable.|Para los perfiles de correo electrónico configurados mediante Intune, se quitan la cuenta de correo electrónico y el correo electrónico.|  

**Android for Work**

Al realizar un borrado selectivo en un dispositivo Android for Work, se quita el perfil de trabajo junto con todos los datos, las aplicaciones y la configuración del perfil de trabajo de dicho dispositivo. De esta forma, se retira el dispositivo de la administración con Intune y Configuration Manager. No se admite la eliminación completa para Android for Work.

 **Windows 10, Windows 8.1, Windows RT 8.1 y Windows RT**  

|Contenido borrado al retirar un dispositivo|Windows 10, Windows 8.1 y Windows RT 8.1|  
|---------------------------------|-------------|
|Aplicaciones y datos asociados de la empresa que se instalaron mediante Configuration Manager e Intune|Se desinstalan las aplicaciones y se quitan las claves de instalación de prueba. Se revocará la clave de cifrado de las aplicaciones que usan el borrado selectivo de Windows y no se podrá acceder a los datos.|  
|Perfiles de VPN y Wi-Fi|Quitado.|  
|Certificados|Quitado y revocado.|  
|Configuración|Se quitan los requisitos.|
|Agente de administración|No aplicable. El agente de administración está integrado.|  
|Perfiles de correo electrónico|Se quita el correo electrónico habilitado para EFS, lo que incluye la aplicación Correo para el correo electrónico y los datos adjuntos de Windows.|  

 **Windows 10 Mobile, Windows Phone 8.0 y Windows Phone 8.1**

|Contenido borrado al retirar un dispositivo|Windows 10 Mobile, Windows Phone 8 y Windows Phone 8.1|  
|-|-|
|Aplicaciones y datos asociados de la empresa que se instalaron mediante Configuration Manager e Intune|Las aplicaciones se desinstalarán. Se quitarán los datos de la aplicación de empresa.|  
|Perfiles de VPN y Wi-Fi|Quitados en Windows 10 Mobile y Windows Phone 8.1.|  
|Certificados|Quitado en Windows Phone 8.1.|  
|Agente de administración|No aplicable. El agente de administración está integrado.|  
|Perfiles de correo electrónico|Quitados (excepto Windows Phone 8.0).|  

La siguiente configuración también se quita de los dispositivos Windows 10 Mobile y Windows Phone 8.1:  

- **Requerir una contraseña para desbloquear dispositivos móviles**  
- **Permitir contraseñas sencillas**  
- **Longitud mínima de la contraseña**  
- **Tipo de contraseña requerida**
- **Expiración de la contraseña (días)**  
- **Recordar el historial de contraseñas**  
- **Número de errores de inicio de sesión consecutivos permitidos antes de que se borre el dispositivo**  
- **Minutos de inactividad antes de que se requiera la contraseña**  
- **Tipo de contraseña necesaria: Número mínimo de conjuntos de caracteres**  
- **Permitir cámara**
- **Requerir cifrado en el dispositivo móvil**  
- **Permitir almacenamiento extraíble**  
- **Permitir explorador web**  
- **Permitir almacén de aplicaciones**  
- **Permitir captura de pantalla**  
- **Permitir geolocalización**  
- **Permitir cuenta de Microsoft**  
- **Permitir copiar y pegar**  
- **Permitir tethering Wi-Fi**  
- **Permitir conexión automática a zonas Wi-Fi gratuitas**  
- **Permitir informes de zonas Wi-Fi**  
- **Permitir el restablecimiento de fábrica**
- **Permitir Bluetooth**  
- **Permitir NFC**
- **Permitir Wi-Fi**

#### <a name="to-initiate-a-remote-wipe-from-the-configuration-manager-console"></a>Para iniciar un borrado remoto desde la consola de Configuration Manager  

1. En la consola de Configuration Manager, seleccione **Activos y compatibilidad** y elija **Dispositivos**. Como alternativa, puede elegir **Colecciones de dispositivos** y seleccionar una colección.  

2. Seleccione el dispositivo que desea retirar/borrar.  

3. Elija **Acciones de dispositivo remoto** en **Grupo de dispositivos** y, a continuación, **Retirar/borrar**.  



## <a name="wiping-efs-enabled-content"></a>Eliminación de contenido habilitado para EFS  

Windows 8.1 y Windows RT 8.1 admiten el borrado selectivo de contenido cifrado con Sistema de cifrado de archivos (EFS). La información siguiente es aplicable a un borrado selectivo de contenido habilitado para EFS:  

- Solo se borran de forma selectiva las aplicaciones y los datos protegidos con EFS que usen el mismo dominio de Internet que la cuenta de Intune. Para obtener más información, consulte [Borrado selectivo de Windows para la administración de datos del dispositivo](https://technet.microsoft.com/library/dn486874.aspx).  

- Si se producen cambios en el dominio asociado con EFS, se pueden necesitar hasta 48 horas después de los cambios para que las aplicaciones y los datos que usen el nuevo dominio se puedan borrar de forma selectiva.  

- Los dominios que estén registrados con Intune serán los dominios de los que se eliminarán los datos.  

Los datos y las aplicaciones que son compatibles actualmente con el borrado selectivo de EFS son:  

- Aplicación Correo para Windows.  

- Carpetas de trabajo.

- Archivos y carpetas cifrados con EFS. Para obtener más información, consulte las [prácticas recomendadas para el sistema de cifrado de archivos](http://support.microsoft.com/kb/223316).  


### <a name="best-practices-for-selective-wipe"></a>Procedimientos recomendados para el borrado selectivo  

- Para lograr un borrado correcto de correo electrónico, configure los perfiles de correo electrónico en dispositivos iOS y Windows Phone 8.1.  

- Para lograr un borrado correcto de aplicaciones, asegúrese de que estas se distribuyen a través de la administración de aplicaciones de dispositivos móviles.  

- Para iOS, configure la opción **Permitir copia de seguridad en iCloud** en **No permitir**, de modo que los usuarios no puedan restaurar el contenido con iCloud.  

- Si se ha desactivado una cuenta, transcurrido un año, Intune retirará la cuenta y se realizará un borrado selectivo.  



##  <a name="passcode-reset"></a>Restablecimiento de la contraseña  

Si un usuario olvida su contraseña, puede ayudarle quitando la contraseña de un dispositivo o forzar el uso de una nueva contraseña temporal en un dispositivo. En la tabla siguiente se muestra cómo funciona el restablecimiento del código de acceso en distintas plataformas móviles.  

| Plataforma                              | Restablecimiento de la contraseña                                                                               |
|---------------------------------------|----------------------------------------------------------------------------------------------|
| iOS                                   | Permite borrar la contraseña de un dispositivo. No admite la creación de una nueva contraseña temporal. |
| macOS                                 | No compatible.                                                                               |
| Android                               | Compatible con versiones anteriores a Android 7.0. Crea un código de acceso temporal.                |
| Android for Work                      | No compatible.                                                                               |
| PC Windows 10                        | No compatible.                                                                               |
| Windows 10 Mobile                     | Compatible (excepto los dispositivos unidos a Azure AD).  |
| Windows Phone 8 y Windows Phone 8.1 | Compatible.                                                                                   |
| Windows RT 8.1                        | No compatible.                                                                               |
| PC Windows 8.1                       | No compatible.                                                                               |

> [!Note]    
> Debe llevar a cabo la acción de restablecimiento de contraseña desde el sitio de nivel superior de su entorno. Por ejemplo, si usa un sitio de administración central, solo puede llevar a cabo la acción en ese sitio. Si usa un sitio principal independiente, solo puede llevar a cabo la acción en ese sitio.

#### <a name="to-reset-the-passcode-on-a-mobile-device-remotely-in-configuration-manager"></a>Para restablecer el código de acceso de un dispositivo móvil de forma remota en Configuration Manager  

1. En la consola de Configuration Manager, seleccione **Activos y compatibilidad** y elija **Dispositivos**. Como alternativa, puede elegir **Colecciones de dispositivos** y seleccionar una colección.  

2. Seleccione el dispositivo o los dispositivos en los que se va a restablecer el código de acceso.  

3. Elija **Acciones de dispositivo remoto** en **Grupo de dispositivos** y, a continuación, **Restablecimiento de código de acceso**.  

#### <a name="to-show-the-state-of-the-passcode-reset"></a>Para mostrar el estado de restablecimiento del código de acceso  

1. En la consola de Configuration Manager, seleccione **Activos y compatibilidad** y elija **Dispositivos**. Como alternativa, puede elegir **Colecciones de dispositivos** y seleccionar una colección.  

2. Seleccione el dispositivo o los dispositivos en los que se va a mostrar el estado de restablecimiento de código de acceso.  

3. Elija **Acciones de dispositivo remoto** en **Grupo de dispositivos** y, a continuación, **Show Passcode State** (Mostrar estado del código de acceso).  



## <a name="remote-lock"></a>Bloqueo remoto  

Si un usuario pierde su dispositivo, es posible bloquearlo de forma remota. La tabla siguiente muestra el modo en que se puede usar el bloqueo remoto en distintas plataformas móviles.  

|Plataforma|Bloqueo remoto|  
|--------------|-----------------|  
|iOS|Compatible.|  
|Android|Compatible.|  
|Windows 10|No se admite en este momento.|  
|Windows Phone 8 y Windows Phone 8.1|Compatible.|  
|Windows RT 8.1 |Compatible si el usuario actual del dispositivo es el mismo usuario que inscribió el dispositivo.|  
|Windows 8.1|Compatible si el usuario actual del dispositivo es el mismo usuario que inscribió el dispositivo.|  

> [!Note]    
> Debe llevar a cabo la acción de bloqueo remoto desde el sitio de nivel superior de su entorno. Por ejemplo, si usa un sitio de administración central, solo puede llevar a cabo la acción en ese sitio. Si usa un sitio principal independiente, solo puede llevar a cabo la acción en ese sitio.

#### <a name="to-lock-a-mobile-device-remotely-through-the-configuration-manager-console"></a>Para bloquear un dispositivo móvil de forma remota a través de la consola de Configuration Manager  

1. En la consola de Configuration Manager, seleccione **Activos y compatibilidad** y elija **Dispositivos**. Como alternativa, puede elegir **Colecciones de dispositivos** y seleccionar una colección.  

2. Seleccione el dispositivo o los dispositivos para bloquear.  

3. Elija **Acciones de dispositivo remoto** en **Grupo de dispositivos** y, a continuación, elija **Bloqueo remoto**.  

#### <a name="to-show-the-state-of-the-remote-lock"></a>Para mostrar el estado del bloqueo remoto  

1. En la consola de Configuration Manager, seleccione **Activos y compatibilidad** y elija **Dispositivos**. Como alternativa, puede elegir **Colecciones de dispositivos** y seleccionar una colección.  

2. Seleccione el dispositivo en el que se va a mostrar el estado del bloqueo remoto.  

3. Elija **Acciones de dispositivo remoto** en **Grupo de dispositivos** y, a continuación, elija **Show Remote Lock State** (Mostrar estado de bloqueo remoto).  



## <a name="see-also"></a>Consulte también  

[Borrado selectivo de Windows para la administración de datos del dispositivo](https://technet.microsoft.com/library/dn486874.aspx)   
