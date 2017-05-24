---
title: "Declaración previa de dispositivos con números de serie de iOS o IMEI | Microsoft Docs"
description: "Declare previamente dispositivos corporativos con su número de serie de iOS o IMEI."
ms.custom: na
ms.date: 03/24/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ddb4c68e-e7f7-475a-89e2-7379a86e44c4
caps.latest.revision: 3
author: nathbarn
ms.author: nathbarn
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: e6833951db27b227a3ca22925e9d9f4c3fc443fc
ms.openlocfilehash: e8606b8a9268a0a0668b75070cf35894f4794123
ms.contentlocale: es-es
ms.lasthandoff: 05/17/2017

---
# <a name="predeclare-devices-with-imei-or-ios-serial-numbers"></a>Declarar previamente dispositivos con números de serie de iOS o IMEI

*Se aplica a: System Center Configuration Manager (rama actual)*

Puede identificar los dispositivos corporativos si importa sus números de identidad internacional de equipo móvil (IMEI) o los números de serie de iOS. Puede cargar un archivo de valores separados por comas (.csv) que incluya los números IMEI de los dispositivos o escribir la información de los dispositivos de forma manual.  La información importada establecerá la **propiedad** de los dispositivos que se inscriban como **Corporativo** en las listas de dispositivos. Se sigue necesitando una licencia de Intune para cada usuario que acceda al servicio.  

Al cargar los números de serie para dispositivos iOS que pertenecen a la empresa, deben estar emparejados con un perfil de inscripción corporativa. Los dispositivos deben inscribirse posteriormente mediante el Programa de inscripción de dispositivos (DEP) de Apple o Apple Configurator para que aparezcan como dispositivos que pertenecen a la empresa.

## <a name="how-to-predeclare-corporate-owned-devices"></a>Cómo realizar la declaración previa de dispositivos corporativos

1.    En la consola de Configuration Manager, vaya a **Activos y compatibilidad** > **General** > **Todos los dispositivos corporativos** > **Predeclared devices** (Dispositivos predeclarados).

2.  Haga clic en **Create Predeclared Devices** (Crear dispositivos predeclarados). Se abre el asistente para crear dispositivos predeclarados.

3.    Seleccione cómo quiere agregar la información del dispositivo:

     -    **Cargar un archivo CSV que contenga los números de serie o IMEI y los detalles**

        Para seleccionar esta opción, haga clic en **Examinar** a fin de especificar el archivo .csv que contiene información para declarar previamente dispositivos corporativos. El archivo .csv debe tener el formato correcto. Para obtener más información, consulte [Formato para cargar archivos .csv](#format-for-uploading-csv-files).

     -    **Agregar manualmente los números de serie o IMEI y los detalles**

        Para especificar la información manualmente, escriba el número IMEI o el número de serie de iOS y la información de los dispositivos. Corrija todos los errores o advertencias antes de continuar.

    Haga clic en **Siguiente**.

4. Si ha cargado un archivo .csv, revise los resultados de la importación del archivo. Si se ha importado un número de dispositivo, Configuration Manager muestra los dispositivos y los **detalles** del reemplazo. Seleccione los dispositivos cuyos detalles desea sobrescribir. Los detalles de dispositivo solo se pueden modificar volviendo a importar la identificación del dispositivo o el número de serie.

  Si decide especificar manualmente el número, complete el formulario de los dispositivos que quiere declarar previamente.

  Haga clic en **Siguiente** para continuar.

4. Si en la lista se incluyen números de serie de iOS, seleccione **Enrollment Profile to Assign** (Perfil de inscripción para asignar) en la lista de perfiles disponibles y haga clic en **Siguiente**.

5. Haga clic en **Siguiente** para revisar los detalles y, después, haga clic en **Siguiente** otra vez para cargar los datos.

6. Haga clic en **Cerrar** para finalizar.

## <a name="format-for-uploading-csv-files"></a>Formato para cargar archivos .csv

El archivo .csv que se usa para identificar los dispositivos por número de serie o IMEI debe tener el formato siguiente, excepto la fila superior, que se proporciona únicamente a modo informativo. Cada fila debe contener un número de identificación: un número IMEI o un número de serie de iOS. Puede incluir ambos. Los número IMEI pueden usarse con dispositivos Android, iOS y Windows. También se admiten los números de serie de iOS.  Esta tabla contiene datos de ejemplo:

| Número de IMEI  | Número de serie de iOS  | Sistema operativo | Detalles |
|------------ |---------------|-----|-----|
| 123456789012345    |   | WINDOWS | Dispositivo Windows propiedad de la empresa|
|   | A1B2C3D4E5C6 | IOS |     Dispositivo iOS propiedad de la empresa|
| 223456789012345 | E6D5C4B3A210 |   IOS |     Otro dispositivo iOS|
| 323456789012345 |        |   IOS |     Un tercer dispositivo iOS|
| 123456789012346 |         |   ANDROID |     Dispositivo Android propiedad de la empresa|

No incluya ninguna fila de encabezado en el archivo .csv. En el ejemplo siguiente se muestran los mismos datos en formato CSV:

```
123456789012345,,WINDOWS,Company-owned Windows device
,A1B2C3D4E5C6,IOS,Company-owned iOS device
223456789012345,E6D5C4B3A210,IOS,Another iOS device
323456789012345,,IOS,A third iOS device
123456789012346,,ANDROID,Company-owned Android device
```

Las columnas del archivo .csv aceptan los siguientes valores:

| Columna 1 | Columna 2 | Columna 3 | Columna 4 |
|---|---|---|---|
|Número IMEI sin espacios | Número de serie de iOS | IOS, WINDOWS o ANDROID | Detalles opcionales del dispositivo (límite de 1024 caracteres) |

