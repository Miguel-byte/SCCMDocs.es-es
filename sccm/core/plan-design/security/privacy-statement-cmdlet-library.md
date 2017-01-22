---
title: "Declaración de privacidad de System Center Configuration Manager: biblioteca de cmdlets de Configuration Manager | Microsoft Docs"
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
ms.sourcegitcommit: 767d0594eb871462df038997ea3b7e29615e05f7
ms.openlocfilehash: 10d8e8948d66a6b9b74e16a02cfbfc4ced66596c


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



<!--HONumber=Dec16_HO3-->


