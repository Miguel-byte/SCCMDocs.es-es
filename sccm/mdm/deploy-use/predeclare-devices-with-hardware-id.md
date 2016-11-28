---
title: "Declarar previamente dispositivos con números de serie de iOS o IMEI"
description: "Declare previamente dispositivos corporativos con su número de serie de iOS o IMEI."
ms.custom: na
ms.date: 10/06/2016
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ddb4c68e-e7f7-475a-89e2-7379a86e44c4
caps.latest.revision: 3
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 5c6cf3c1697b49708aa5192b67b08b700da7dc72
ms.openlocfilehash: 43d67aa664037c6da83260d5ada8e574510a8f7b

---
# <a name="predeclare-devices-with-imei-or-ios-serial-numbers"></a>Declarar previamente dispositivos con números de serie de iOS o IMEI

*Se aplica a: System Center Configuration Manager (rama actual)*

Puede identificar los dispositivos corporativos si importa sus números de identidad internacional de equipo móvil (IMEI) o los números de serie de iOS. Puede cargar un archivo de valores separados por comas (.csv) que incluya los números IMEI de los dispositivos o escribir la información de los dispositivos de forma manual.  La información importada establecerá la **propiedad** de los dispositivos que se inscriban como "**Corporativo**" en las listas de dispositivos. Se sigue necesitando una licencia de Intune para cada usuario que acceda al servicio.  

## <a name="predeclare-corporate-owned-devices-with-imei-or-ios-serial-number"></a>Declarar previamente dispositivos corporativos con número de serie de iOS o IMEI

1.  En la consola de Configuration Manager, vaya a Activos y compatibilidad > Introducción > Todos los dispositivos corporativos > Dispositivos declarados previamente y, luego, haga clic en Agregar dispositivos declarados previamente. Se abre el asistente para dispositivos declarados previamente.
2.  Especifique cómo desea agregar la información del dispositivo:
     -  Cargar un archivo .csv que contenga los números IMEI y otros detalles
     -  Agregar manualmente números IMEI y otra información. Para especificar la información manualmente, escriba el número IMEI o el número de serie de iOS y la información de los dispositivos.

      En el caso de los archivos cargados, busque el archivo .csv que contiene información para declarar previamente dispositivos corporativos. El archivo debe tener el siguiente formato, excepto la fila superior, que se proporciona únicamente como guía. Cada fila debe contener un número IMEI o un número de serie de iOS. Solo se pueden declarar previamente los números de serie de los dispositivos iOS; use el número IMEI para el resto de las plataformas de dispositivo. Esta tabla contiene datos de ejemplo:
      | IMEI #  | Número de serie de iOS #  | Sistema operativo | Detalles |
      | :------------ |:---------------|:-----|:-----|
      | 123456789012345    |   | WINDOWS | Dispositivo Windows propiedad de la empresa|
      |       | A1B2C3D4E5C6 |   iOS |  Dispositivo iOS propiedad de la empresa|
      | 223456789012345 | E6D5C4B3A210 |   iOS |    Otro dispositivo iOS|
      | 323456789012345 |        |   iOS |  Un tercer dispositivo iOS|
      | 123456789012346 |         |   Android |     Dispositivo Android propiedad de la empresa|

    No incluya ninguna fila de encabezado en el archivo .csv. El ejemplo anterior incluye un encabezado puramente explicativo.

    **Las columnas aceptan los siguientes valores:**    
      - Columna 1: Número IMEI sin espacios en blanco
      - Columna 2: número de serie de iOS
      - Columna 3: sistema operativo del dispositivo:
         - iOS: todos los dispositivos iOS
         - WINDOWS: incluye Windows Phone, Windows 10 Mobile y equipos de Windows
         - ANDROID: todos los dispositivos Android
      - Columna 4: detalles (opcional): información adicional del dispositivo que aparece en la consola de Configuration Manager. Límite de 1024 caracteres.

    Haga clic en **Siguiente**.

3. Revise los resultados de la importación del archivo. Si antes se importó un número de dispositivo, Configuration Manager muestra los dispositivos y los **detalles** del reemplazo. Seleccione los dispositivos cuyos detalles desea sobrescribir. Los detalles de dispositivo solo se pueden modificar volviendo a importar la identificación del dispositivo o el número de serie. Haga clic en **Siguiente** para continuar o **Atrás** para conservar la información actualizada; luego, finalice el asistente.

4. Si la importación incluye números de serie de iOS, debe asignar los dispositivos a un perfil de inscripción. Seleccione **Perfil de inscripción para asignar** en la lista de perfiles disponibles y haga clic en **Siguiente**.

5. Haga clic en **Siguiente** para ver el resumen y finalizar el asistente.



<!--HONumber=Nov16_HO1-->


