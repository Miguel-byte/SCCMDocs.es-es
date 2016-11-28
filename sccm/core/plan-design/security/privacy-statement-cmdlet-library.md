---
title: "Declaración de privacidad de System Center Configuration Manager: biblioteca de cmdlets de Configuration Manager"
description: "Conozca cómo Microsoft recopila y usa datos relacionados con la biblioteca de cmdlets de System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bec00fb4-1ac0-4e49-b330-0871b3722459
caps.latest.revision: 5
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 88d11aaed4a0e6575cb859f5dfc3ac425bd2bf38


---
# <a name="system-center-configuration-manager-privacy-statement---configuration-manager-cmdlet-library"></a>Declaración de privacidad de System Center Configuration Manager: biblioteca de cmdlets de Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Esta declaración de privacidad cubre las características de la biblioteca de cmdlets de System Center Configuration Manager.  

## <a name="usage-data"></a>Datos de uso  
 **Qué hace esta característica:**   
la biblioteca de cmdlets de System Center Configuration Manager le permite administrar una jerarquía de Configuration Manager con scripts y cmdlets de Windows PowerShell. La biblioteca de cmdlets recopila información acerca de cómo usar los cmdlets incluidos en la biblioteca con el fin de identificar tendencias y patrones de uso.  La biblioteca de cmdlets también recopila los tipos y números de errores que se producen al usar los cmdlets.  

 **Información recopilada, procesada o transmitida:**   
los datos de uso recopilados incluyen el inicio, detención y terminación de cmdlets; la ejecución de cmdlets desusados; y las métricas de actividad para operaciones del proveedor de SMS relacionadas con los cmdlets. Esta información no contiene datos que identifiquen personalmente al usuario.  La información de errores recopilada incluye errores devueltos por los cmdlets y los detalles de errores de los errores de excepción. Algunos informes de detalles de error podrían contener identificadores individuales, como un número de serie para un dispositivo que está conectado al equipo. La biblioteca de cmdlets filtra y anonimiza la información contenida en los informes de errores para quitar los identificadores individuales antes de transmitirlos a Microsoft.  

 **Uso de la información:**   
usamos esta información para mejorar la calidad, la seguridad y la integridad de los productos y servicios que ofrecemos.  

 **Elección y control:**   
esta característica de Datos de uso está habilitada de forma predeterminada. La biblioteca de cmdlets de System Center Configuration Manager incluye dos claves de registro para controlar esta funcionalidad.  

 Para dejar de participar totalmente tiene que establecer estos dos valores clave del registro, uno para cada uno de los proveedores de seguimiento de eventos para Windows (ETW):  

-   HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Provider:CeipLevel=0 (para dejar de participar en los datos de uso del proveedor de la unidad)  

-   HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Cmdlets:CeipLevel=0 (para dejar de participar en los datos de uso de los cmdlets )  

 Los cambios a la configuración de datos de uso son específicos para el equipo en el que se realizan.  

 Para obtener más información acerca de cómo configurar Datos de uso (recopilación), consulte la [documentación de la biblioteca de cmdlets de System Center Configuration Manager](https://technet.microsoft.com/en-us/library/dn958404.aspx).  

## <a name="update-check"></a>Comprobar actualizaciones  
 **Qué hace esta característica:**   
la biblioteca de cmdlets de System Center Configuration Manager comprueba automáticamente si hay actualizaciones de la la biblioteca diariamente y le notifica para que descargue la biblioteca actualizada.  

 **Información recopilada, procesada o transmitida:**   
la comprobación de actualización de la biblioteca de cmdlets descargará un pequeño archivo de texto desde el Centro de descarga de Microsoft para realizar una comprobación de la versión.   Este archivo no se almacena localmente.  La biblioteca de cmdlets no actualizará automáticamente el software.  

 **Uso de la información:**   
usamos esta información para mejorar la calidad, la seguridad y la integridad de los productos y servicios que ofrecemos.  

 **Elección y control:**   
La comprobación de actualizaciones está habilitada de forma predeterminada.  La biblioteca de cmdlets de System Center Configuration Manager incluye estos cmdlets para controlar la funcionalidad de notificación de la actualización:  

-   `Get-CMCmdletUpdateCheck` obtiene la configuración de la característica de actualización e indicará si la directiva del sistema está invalidando la directiva de usuario.  

-   `Send-CMCmdletUpdateCheck` le permite realizar una comprobación de actualizaciones no programada. Una comprobación no programada no tiene en cuenta la configuración de directivas.  

-   `Set-CMCmdletUpdateCheck` configura las opciones de comprobación de actualizaciones por usuario o por sistema. Debe estar ejecutando la aplicación como administrador para establecer la configuración del sistema.  

 Puede obtener más información acerca de cómo configurar la comprobación de la actualización en la [Documentación de la biblioteca de cmdlets de System Center Configuration Manager](https://technet.microsoft.com/en-us/library/dn958404.aspx).  



<!--HONumber=Nov16_HO1-->


