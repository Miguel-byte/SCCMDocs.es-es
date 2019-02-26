---
title: Acciones remotas con la administración conjunta
titleSuffix: Configuration Manager
description: Ejecutar acciones remotas de Intune para dispositivos administrados conjuntamente
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4a877bed-f6c4-4048-9421-507dc848af5c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4439aa280edaffbb59f8d49ece58e067a729ec91
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56755604"
---
# <a name="remote-actions-with-co-management"></a>Acciones remotas con la administración conjunta

Deberá asegurarse de que todos los dispositivos que administra estarán accesible, sea cual sea su, cada vez que se conecta. También deberá proporcionar a cada usuario con todo lo que necesitan para ser productivo, al tiempo que protege las aplicaciones y los datos. Con las acciones de dispositivo compatibles con Intune, puede solucionar estas funciones esenciales de forma remota.

En el siguiente vídeo, director de programas principal Heidi Cheng y Administrador de programas senior Danny Guillory discutan y acciones remotas con la administración conjunta de demostración:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Using-Co-Management-to-Execute-Remote-Actions/player]



## <a name="benefits"></a>Ventajas

Acciones de dispositivo remoto ofrecen controles de administración en el dispositivo sin interferir con los datos personales. Estas acciones de dispositivo remoto le permiten: 
- Eliminar datos de la empresa en dispositivos perdidos o robados  
- Cambiar el nombre de un dispositivo  
- Reiniciar un dispositivo  
- Inventario de dispositivos de revisión  
- Controlar de forma remota un dispositivo  
- Limpiar por completo las aplicaciones preinstaladas de OEM con un reinicio empezar de cero  
- Realice una restablecimiento de fábrica en cualquier dispositivo Windows 10  

Estas funciones son una manera simple e importante para proteger los datos corporativos almacenados en estos dispositivos, ya sea en el correo electrónico o OneDrive.

Para obtener más información sobre estas acciones, consulte [acciones remotas disponibles](#available-remote-actions). 



## <a name="case-studies"></a>Casos prácticos

La empresa de consultoría global Avanade usa con regularidad acciones remotas para administrar los dispositivos usados por sus 30 000 empleados. En un [blog reciente](https://www.microsoft.com/microsoft-365/blog/2018/02/07/the-future-is-on-the-other-side-of-this-bridge/), CIO de Avanade se indica:

> *Nuestro win inmediata de tener la funcionalidad de Intune era la capacidad de restablecer de forma remota Windows en un equipo. Esto es importante para nosotros para equipos perdidos o robados, que es más común en nuestros recursos altamente móviles. * 
>  *Esto es una funcionalidad que en caso contrario, hubiésemos tenido que crear y mantener en un paquete personalizado de Configuration Manager.*

Para obtener más información sobre cómo usar estas acciones remotas, consulte [acciones de dispositivo disponibles](https://docs.microsoft.com/intune/device-management#available-device-actions).


## <a name="value-proposition"></a>Propuesta de valor

Cuando un dispositivo de Configuration Manager se administra conjuntamente, agrega inmediatamente estas funciones que Configuration Manager no tiene de forma nativa. Ahora puede hacer ahora cualquier acción remota que es compatible con Intune. 

Con la administración conjunta, los dispositivos de Configuration Manager ya están al igual que cualquier otro dispositivo administrado por Intune. Por ejemplo, tienen una presencia completa en la nube, y poder lograrlos, siempre tiene acceso a internet. Puede hacer todas estas acciones sin realizar ningún paso adicional más allá de habilitar la administración conjunta.

Puesto que el proceso de inscripción automática es transparente para el usuario, no hay ningún impacto en su productividad. El usuario no necesita hacer nada.


### <a name="available-remote-actions"></a>Acciones remotas disponibles

Utilice estas acciones remotas de Intune una vez que [habilitar la administración conjunta](/sccm/comanage/how-to-enable) en Configuration Manager.

#### <a name="remove-devices"></a>Quitar dispositivos
- **Retirar**: Esta acción quita las aplicaciones administradas y datos (si procede), configuración y correo electrónico los perfiles que se asignaron a dicho dispositivo. El dispositivo, a continuación, se quita de la administración de Intune. Este proceso produce la siguiente acción de retirada de tiempo que el dispositivo se compruebe y recibe el control remoto. La función retirar deja datos personales del usuario en el dispositivo.  

- **Borrar**: Esta acción restaura la configuración predeterminada de fábrica del dispositivo. Si elige la opción de **conservar la cuenta de usuario y el estado de inscripción**, a continuación, se mantienen los datos de usuario. En caso contrario, la unidad se borra de forma segura.  

- **Eliminar**: Si desea quitar los dispositivos de Intune en Azure portal, puede eliminarlas desde el panel de dispositivos específicos. La próxima vez que se registre el dispositivo, quita los datos de la organización almacenados en él.  

Para obtener más información, consulte [quitar dispositivos mediante el borrado, retirar o manualmente anular la inscripción del dispositivo](https://docs.microsoft.com/intune/devices-wipe).

#### <a name="selective-wipe"></a>Borrado selectivo
<!--SCCMDocs issue 973--> Cuando se elige un **borrado selectivo de aplicaciones**, quita los datos de la aplicación de empresa sin quitar los datos personales. Use esta acción cuando un dispositivo se notifica como pérdida o robo. 

Para obtener más información, consulte [borrado solo de los datos corporativos de aplicaciones administradas por Intune](https://docs.microsoft.com/intune/apps-selective-wipe).

#### <a name="sync"></a>sincronización
El **sincronización** fuerza la acción de dispositivo al dispositivo seleccionado a registrarse inmediatamente en Intune. Cuando un dispositivo se registra, recibe de inmediato las acciones o las directivas que haya asignado a él pendientes.

Esta característica puede ayudarle a validar y solucionar problemas de directivas que ha asignado, sin esperar al siguiente programado check-inmediatamente.

Para obtener más información, consulte [sincronizar los dispositivos para obtener las últimas directivas y acciones con Intune](https://docs.microsoft.com/intune/device-sync).

#### <a name="restart"></a>Reiniciar
El **reiniciar** acción de dispositivo hace que el dispositivo que elija reiniciar. Esta acción es útil cuando hay un reinicio pendiente, pero el usuario no está disponible para hacerlo.

Para obtener más información, consulte [reiniciar de forma remota los dispositivos con Intune](https://docs.microsoft.com/intune/device-restart).

#### <a name="fresh-start"></a>Empezar de cero
El **Fresh Start** acción de dispositivo quita todas las aplicaciones instaladas en un dispositivo con Windows 10, versión 1703 o posterior. Empezar de cero ayuda a eliminar aplicaciones preinstaladas de (OEM) que normalmente se instalan con un nuevo dispositivo.

Si elige no conservar los datos de usuario, el dispositivo se restaura a su estado de out-of-box. Anula la inscripción de Azure AD y MDM.

Si tienen predeterminados estándares con respecto a qué aplicaciones deben estar en el dispositivo, esta acción elimina los que no cumplen los criterios.

Para obtener más información, consulte [uso Fresh Start para restablecer dispositivos Windows 10 con Intune](https://docs.microsoft.com/intune/device-fresh-start). 

#### <a name="remote-control"></a>Control remoto
Dispositivos administrados por Intune se pueden administrar remotamente con [TeamViewer](https://www.teamviewer.com/). TeamViewer es un programa de terceros que adquiera por separado.

Para obtener más información, consulte [Use TeamViewer para administrar de forma remota los dispositivos de Intune](https://docs.microsoft.com/intune/device-profile-android-teamviewer). 



## <a name="configure"></a>Configurar

Aparte de control remoto a través de TeamViewer, para empezar a usar estas acciones de dispositivo remoto en Intune, ninguna configuración adicional es necesaria después de [habilitar la administración conjunta](/sccm/comanage/how-to-enable).

Para obtener más información sobre el uso de TeamViewer para el control remoto, consulte [Use TeamViewer para administrar de forma remota los dispositivos de Intune](https://docs.microsoft.com/intune/device-profile-android-teamviewer). 

