---
title: Declaración de privacidad para cmdlets
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo Microsoft recopila y usa datos relacionados con los cmdlets de Configuration Manager.
ms.date: 01/3/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: bec00fb4-1ac0-4e49-b330-0871b3722459
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: e777c509ae0461120ae195712aaecf7f44813261
ms.sourcegitcommit: 13ac4f5e600dc1edf69e8566e00968f40e1d1761
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/11/2019
ms.locfileid: "70889244"
---
# <a name="configuration-manager-cmdlet-library-privacy-statement"></a>Declaración de privacidad de la biblioteca de cmdlets de Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Esta declaración de privacidad cubre las características de la biblioteca de cmdlets de System Center Configuration Manager.  

## <a name="usage-data"></a>Datos de uso  

#### <a name="what-this-feature-does"></a>Funciones de esta característica

la biblioteca de cmdlets de System Center Configuration Manager le permite administrar una jerarquía de Configuration Manager con scripts y cmdlets de Windows PowerShell. La biblioteca de cmdlets recopila información sobre cómo usar los cmdlets de la biblioteca para identificar tendencias y patrones de uso. La biblioteca de cmdlets también recopila los tipos y números de errores que se reciben al usar los cmdlets.  

#### <a name="information-collected-processed-or-transmitted"></a>Información recopilada, procesada o transmitida
   
Los datos de uso recopilados incluyen el inicio, la detención y la terminación de cmdlets, la ejecución de cmdlets desusados y las métricas de actividad para operaciones del proveedor de SMS relacionadas con los cmdlets. Esta información no contiene datos que identifiquen personalmente al usuario. La información de errores recopilada incluye errores devueltos por los cmdlets y los detalles de error de los errores de excepción. Es posible que algunos informes de detalles de error incluyan identificadores individuales, como un número de serie para un dispositivo que está conectado al equipo. La biblioteca de cmdlets filtra y anonimiza la información de los informes de errores para quitar los identificadores individuales antes de transmitirlos a Microsoft.  

#### <a name="use-of-information"></a>Uso de la información
   
Microsoft usa esta información para mejorar la calidad, la seguridad y la integridad de los productos y servicios que ofrece.  

#### <a name="choicecontrol"></a>Opción/control   

esta característica de datos de uso está habilitada de forma predeterminada. La biblioteca de cmdlets de System Center Configuration Manager incluye dos claves del Registro que controlan esta característica.  

 Para dejar de participar por completo, establezca estos dos valores de clave del Registro. Son para cada uno de los proveedores de Seguimiento de eventos para Windows (ETW):  

- HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Provider:CeipLevel=0 (para dejar de participar en los datos de uso del proveedor de unidad)  

- HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Cmdlets:CeipLevel=0 (para dejar de participar en los datos de uso de los cmdlets)  

  Los cambios en la configuración de datos de uso son específicos para el equipo en el que se realizan.  


## <a name="next-steps"></a>Pasos siguientes

[Documentación de la biblioteca de cmdlets de System Center Configuration Manager](https://docs.microsoft.com/powershell/sccm/configurationmanager/)   
