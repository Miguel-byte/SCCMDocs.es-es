---
title: Directivas de cumplimiento de dispositivos
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo administrar directivas de cumplimiento en System Center Configuration Manager para que los dispositivos sean compatibles con directivas de acceso condicional.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: ad8fa94d-45bb-4c94-8d86-31234c5cf21c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 776af7499c576f21d47dafec8a668f3c4051ad88
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32347270"
---
# <a name="device-compliance-policies-in-system-center-configuration-manager"></a>Directivas de cumplimiento de dispositivo en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Las **directivas de cumplimiento** en System Center Configuration Manager definen las reglas y los valores de configuración que un dispositivo debe cumplir para que se considere conforme a las directivas de acceso condicional. Las directivas de cumplimiento también se pueden usar para supervisar y corregir problemas de compatibilidad con dispositivos independientemente del acceso condicional.  


> [!IMPORTANT]  
>  En este artículo se describen las directivas de cumplimiento para los dispositivos administrados por Microsoft Intune.    Las directivas de cumplimiento para los equipos administrados por System Center Configuration Manager se describen en [Manage access to O365 services for PCs managed by System Center Configuration Manager](../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md) (Administración del acceso a servicios de O365 para equipos administrados por System Center Configuration Manager).  

 Estas reglas incluyen requisitos como los siguientes:  

-   PIN y contraseñas para tener acceso a un dispositivo

-   Cifrado de los datos almacenados en el dispositivo

-   Si el dispositivo está desbloqueado o modificado  

-   Si el correo electrónico en el dispositivo se administra mediante una directiva de Intune, o si el servicio de atestación de estado de dispositivo de Windows notifica el dispositivo como incorrecto.
-   Aplicaciones que no se pueden instalar en el dispositivo.


 Puede implementar directivas de cumplimiento para recopilaciones de usuarios. Cuando se implementa una directiva de cumplimiento para un usuario, se comprueba el cumplimiento de todos los dispositivos del usuario.  

 En la siguiente tabla se enumeran los tipos de dispositivos compatibles con las directivas de cumplimiento y se indica cómo se administran los valores de configuración no compatibles cuando se usa la directiva con una directiva de acceso condicional.  

|Regla|Windows 8.1 y posterior|Windows Phone 8.1 y versiones posteriores|iOS 6.0 y versiones posteriores|Android 4.0 y versiones posteriores, Samsung Knox Standard 4.0 y versiones posteriores, y Android for Work|  
|----------|---------------------------|---------------------------------|-----------------------|---------------------------|-----------------------------------------|  
|**Configuración de contraseña o PIN**|Corregido|Corregido|Corregido|En cuarentena|  
|**Cifrado del dispositivo**|No aplicable|Corregido|Corregido (estableciendo PIN)|En cuarentena<br>(Android for Work siempre cifrado)|  
|**Dispositivo liberado**|No aplicable|No aplicable|En cuarentena (no es una configuración)|En cuarentena (no es una configuración)|  
|**Perfil de correo electrónico**|No aplicable|No aplicable|En cuarentena|No aplicable|  
|**Versión de SO mínima**|En cuarentena|En cuarentena|En cuarentena|En cuarentena|  
|**Versión de SO máxima**|En cuarentena|En cuarentena|En cuarentena|En cuarentena|  
|**Atestación de estado de dispositivo (actualización 1602)**|Opción no aplicable a Windows 8.1<br /><br /> Windows 10 y Windows 10 Mobile están en cuarentena.|No aplicable|No aplicable|No aplicable|  
|**Aplicaciones que no se pueden instalar**|No aplicable|No aplicable|En cuarentena|En cuarentena|

 **Corregido** = el sistema operativo del dispositivo exige el cumplimiento (por ejemplo, el usuario debe establecer un PIN).  La configuración nunca será no conforme.  

 **En cuarentena** = el sistema operativo del dispositivo no exige el cumplimiento (por ejemplo, los dispositivos Android no obligan al usuario a cifrar el dispositivo).  En este caso:  

-   El dispositivo se bloqueará si el usuario se rige por una directiva de acceso condicional.  

-   El portal de empresa o portal web notificará al usuario los problemas de cumplimiento que se produzcan.  


### <a name="next-steps"></a>Pasos siguientes  
[Crear e implementar una directiva de cumplimiento de dispositivos](create-compliance-policy.md)
### <a name="see-also"></a>Consulte también  
 [Manage access to services in System Center Configuration Manager](../../protect/deploy-use/manage-access-to-services.md) (Administración del acceso a servicios en System Center Configuration Manager)
