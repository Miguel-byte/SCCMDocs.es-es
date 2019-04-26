---
title: Directivas de cumplimiento de dispositivos
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo administrar directivas de cumplimiento en Configuration Manager para que los dispositivos sean compatibles con directivas de acceso condicional.
ms.date: 03/19/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: ad8fa94d-45bb-4c94-8d86-31234c5cf21c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4e225b7ab54a1061387d1c8ee369641f68bd7889
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62227156"
---
# <a name="device-compliance-policies-in-system-center-configuration-manager"></a>Directivas de cumplimiento de dispositivo en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Las directivas de cumplimiento de Configuration Manager definen las reglas y los valores de configuración que un dispositivo debe cumplir para que se considere conforme a las directivas de acceso condicional. Las directivas de cumplimiento también se pueden usar para supervisar y corregir problemas de compatibilidad con dispositivos independientemente del acceso condicional.  


> [!IMPORTANT]  
>  En este artículo se describen las directivas de cumplimiento para los dispositivos administrados por Microsoft Intune. Las directivas de cumplimiento para dispositivos administrados por el cliente de Configuration Manager se describe en [administrar el acceso a servicios de Office 365 para dispositivos administrados por Configuration Manager](/sccm/protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm).  

 Estas reglas incluyen requisitos como los siguientes:  

-   PIN y contraseñas para tener acceso a un dispositivo  

-   Cifrado de los datos almacenados en el dispositivo  

-   Si el dispositivo está desbloqueado o modificado  

-   Si el correo electrónico en el dispositivo se administra mediante una directiva de Intune, o si el servicio de atestación de estado de dispositivo de Windows notifica el dispositivo como incorrecto.  

-   Aplicaciones que no se pueden instalar en el dispositivo.  


 Puede implementar directivas de cumplimiento para recopilaciones de usuarios. Cuando se implementa una directiva de cumplimiento para un usuario, se comprueba el cumplimiento de todos los dispositivos del usuario.  



## <a name="supported-device-types"></a>Tipos de dispositivos compatibles

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

 **Corregido** = el sistema operativo del dispositivo aplica el cumplimiento. Por ejemplo, se obliga al usuario a establecer un PIN. Nunca hay un caso en que el valor sea no compatible.  

 **En cuarentena** = el sistema operativo del dispositivo no aplica el cumplimiento. Por ejemplo, los dispositivos Android no obligan al usuario a cifrar el dispositivo. En este caso:  

-   Si el usuario se rige por una directiva de acceso condicional, se bloquea el dispositivo.  

-   El portal de empresa o portal web notifica al usuario los problemas de cumplimiento.  



## <a name="devices-without-any-assigned-compliance-policy"></a>Dispositivos sin ninguna directiva de cumplimiento asignada
<!--2520152-->
A partir de julio de 2018, configurar si todos los dispositivos que no haya ninguna directiva de cumplimiento asignada se consideran no conformes o no compatibles. De forma predeterminada, los dispositivos sin directiva de cumplimiento asignada se consideran compatibles. Use los pasos siguientes para cambiar este valor en Azure Portal:

1. Inicie sesión en [Intune en Azure Portal](https://aka.ms/intuneportal).  

2. Seleccione **Cumplimiento del dispositivo** y luego **Configuración de directivas de cumplimiento** en el grupo de configuración.  

3. En la opción **Marcar los dispositivos que no tienen asignada una directiva de cumplimiento como**, seleccione una de las siguientes opciones:  

     - **Compatibles** (predeterminada): los dispositivos sin directiva de cumplimiento asignada se consideran compatibles con la directiva. Si el acceso condicional está habilitado, estos dispositivos tienen acceso a los recursos internos.  

     - **No compatibles**: los dispositivos sin directiva de cumplimiento asignada se consideran no compatibles con la directiva. Si el acceso condicional está habilitado, estos dispositivos no pueden acceder a los recursos internos según las condiciones de la directiva de acceso condicional.  

4. Haga clic en Guardar.  

Se recomienda encarecidamente implementar al menos una directiva de cumplimiento para cada plataforma para todos los usuarios del entorno. Luego establezca esta opción en **No compatibles** con el fin de garantizar la seguridad de los recursos internos. Para obtener más información, vea la entrada de blog [Security Enhancements in the Intune Service](https://aka.ms/compliance_policies) (Mejoras de seguridad en el servicio Intune).



## <a name="next-steps"></a>Pasos siguientes  
[Crear e implementar una directiva de cumplimiento de dispositivos](/sccm/mdm/deploy-use/create-compliance-policy)

### <a name="see-also"></a>Consulte también  
 [Administrar el acceso a servicios en System Center Configuration Manager](/sccm/protect/deploy-use/manage-access-to-services)
