---
title: Recopilador de registros
titleSuffix: Configuration Manager
description: Usar la herramienta de recopilación de registros para ayudar a solucionar problemas de análisis de escritorio
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 349b2a69-af46-481f-afb2-24d98774e852
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 24f8b723a82f2adb4eb160b0e3edab1efbca1e95
ms.sourcegitcommit: 13ac4f5e600dc1edf69e8566e00968f40e1d1761
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/11/2019
ms.locfileid: "70891759"
---
# <a name="desktop-analytics-log-collector"></a>Recopilador de registros de análisis de escritorio

A partir de Configuration Manager versión 1906, use la herramienta **DesktopAnalyticsLogsCollector. PS1** desde el directorio de instalación Configuration Manager para ayudar a solucionar problemas de inscripción de dispositivos de análisis de escritorio. Ejecuta algunos pasos básicos para solucionar problemas y recopila los registros pertinentes en un solo directorio de trabajo. Puede compartir este contenido con el soporte técnico de Microsoft.


## <a name="prerequisites"></a>Requisitos previos

- Un cliente de análisis de escritorio con Windows 10, Windows 8.1 o Windows 7 con Service Pack 1

- Ejecute el script en el dispositivo como un usuario administrativo y **ejecute como administrador**.

    > [!Tip]
    > Puede usar la característica **scripts** de Configuration Manager con esta herramienta. Para obtener más información, [vea el ejemplo 5: Implementar script a través de **scripts**](#bkmk_ex5)de Configuration Manager.

- PowerShell versión 4,0 o posterior
    - .NET Framework versión 4,6 o posterior
    - Windows Management Framework versión 4,0 o posterior

## <a name="usage"></a>Uso

Obtener el script del contenido de instalación de Configuration Manager:`SMSSETUP\TOOLS\DesktopAnalyticsLogsCollector\DesktopAnalyticsLogsCollector.ps1`

``` Syntax
DesktopAnalyticsLogsCollector.ps1
    [-LogPath] <String>
    [-LogMode] <Int16>
    [-CollectNetTrace] <Int16>
    [-CollectUTCTrace] <Int16>
```

## <a name="parameters"></a>Parámetros

### `-LogPath`

Especifica una ruta de acceso local o UNC para colocar el registro y otros archivos de salida.

**Valores**:

- Ruta de acceso local (longitud máxima = 130), por ejemplo:`c:\myfolder`

- Ruta de acceso UNC (longitud máxima = 130), por ejemplo:`\\myserver\myfolder`

**Tipo**: string

**Posición**: 1

**Valor predeterminado**: `$Env:SystemDrive\M365AnalyticsLogs`(Cuando este parámetro es null, está vacío o es un espacio en blanco, el script crea la carpeta M365AnalyticsLogs en la unidad del sistema).

### `-LogMode`

Especifica el nivel detallado de los registros.

**Valores**:

- `0`: Registrar mensajes de script solo en la ventana de comandos de PowerShell.

- `1`: Registre los mensajes de script en el archivo de registro en la carpeta de salida y la ventana de comandos de PowerShell.

- `2`: Registrar mensajes de script en el archivo de registro solo en la carpeta de salida.

**Tipo**: Int16

**Posición**: 2

**Valor predeterminado**: `1`(Registre los mensajes de script en el archivo de registro y la ventana de comandos de PowerShell).

### `-CollectNetTrace`

Especifica si el script recopila el seguimiento de red.

**Valores**:

- `0`: No habilite el seguimiento de red.

- `1`(cualquier valor entero distinto de cero): Habilitar seguimiento de red y recopilar resultados.

**Tipo**: Int16

**Posición**: 3

**Valor predeterminado**: `0`(No habilite el seguimiento de red)

### `-CollectUTCTrace`

Especifica si el script recopila el seguimiento de la hora UTC de Windows y ejecuta el diagnóstico de conectividad.

**Valores**:

- `0`: No habilite el seguimiento UTC ni ejecute el diagnóstico de conectividad.

- `1`(cualquier valor entero distinto de cero): Habilite el seguimiento UTC, ejecute diagnóstico de conectividad y recopile los resultados.

**Tipo**: Int16

**Posición**: 4

**Valor predeterminado**: `0`(No habilite el seguimiento de UTC ni ejecute el diagnóstico de conectividad)


## <a name="output"></a>Salida

El script crea una *carpeta de trabajo* en la ruta de acceso especificada. Por ejemplo, **M365AnalyticsLogs_yy_MM_dd_HH_mm_ss**. Coloca todos los archivos de salida en esta carpeta de trabajo.

Si habilita el script para escribir en un *archivo de registro*, genera uno en la carpeta de trabajo. Por ejemplo, **M365AnalyticsLogs_ yy_MM_dd_HH_mm_ss. txt**.

El script también genera otros *archivos de diagnóstico* en la carpeta de trabajo. Por ejemplo:

- `installedKBs.txt`: una lista de las actualizaciones de Windows instaladas en el dispositivo
- `appcompat`: datos de compatibilidad de aplicaciones
- `Reg*.txt`: una serie de archivos con datos exportados del registro de Windows


## <a name="examples"></a>Ejemplos

### <a name="bkmk_ex1"></a>Ejemplo 1: Ejecutar script a través de la ventana de comandos de PowerShell con valores predeterminados

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1
```

### <a name="bkmk_ex2"></a>Ejemplo 2: Ejecutar script a través de la ventana de comandos de PowerShell con los parámetros especificados

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1 -LogPath "c:\testABC" -LogMode 0 -CollectNetTrace 0 -CollectUTCTrace 0
```

### <a name="bkmk_ex3"></a>Ejemplo 3: Ejecutar script a través de la ventana de comandos de PowerShell con los parámetros especificados en la posición

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1 "c:\testABC" 2 0 0
```

### <a name="bkmk_ex4"></a>Ejemplo 4: Ejecutar script a través de la ventana de comandos de PowerShell con el parámetro y los mensajes detallados especificados

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1 -LogMode 1 -Verbose
```

### <a name="bkmk_ex5"></a>Ejemplo 5: Implementar script a través de **scripts** de Configuration Manager

Para obtener más información, consulte [Creación y ejecución de scripts de PowerShell desde la consola de Configuration Manager](/sccm/apps/deploy-use/create-deploy-scripts).

DesktopAnalyticsLogsCollector. PS1 está firmado digitalmente por Microsoft. Es posible que tenga que agregar su certificado de firma de código de Microsoft como un editor de confianza en el dispositivo de destino.

1. Abra las propiedades del script en el explorador de Windows. Cambie a la pestaña **firmas digitales** y seleccione **detalles**.

1. En la pestaña **General** , seleccione **Ver certificado**.

    > [!Note]
    > Para distribuir el certificado a través de otros mecanismos, primero exporte el certificado a un archivo. Vaya a la pestaña **detalles** y seleccione **copiar a archivo**.

1. Seleccione **instalar certificado**. Importe el certificado, colocándolo en el almacén de **editores de confianza** .


## <a name="see-also"></a>Consulte también

- [Solución de problemas de Análisis de escritorio](/sccm/desktop-analytics/troubleshooting)

- [Creación y ejecución de scripts de PowerShell desde la consola de Configuration Manager](/sccm/apps/deploy-use/create-deploy-scripts)
