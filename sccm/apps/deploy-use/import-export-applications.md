---
title: Importación y exportación de aplicaciones
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo importar y exportar aplicaciones en Configuration Manager para compartirlas entre jerarquías independientes.
ms.date: 05/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: dba00e54-9d5b-4f6b-916d-ead48c66e288
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 02bb394de4f3bb947bdc2669a830167089c42311
ms.sourcegitcommit: 3f43fa8462bf39b2c18b90a11a384d199c2822d8
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 05/30/2019
ms.locfileid: "66411014"
---
# <a name="import-and-export-applications"></a>Importación y exportación de aplicaciones

*Se aplica a: System Center Configuration Manager (Rama actual)*

Use Configuration Manager para importar y exportar aplicaciones entre dos jerarquías. Por ejemplo, copie una aplicación de un entorno de prueba a un entorno de producción.

## <a name="export"></a>Exportar

1. En la consola de Configuration Manager, seleccione el nodo **Aplicaciones**. En el grupo Crear de la cinta de opciones, seleccione **Exportar aplicación**.
1. En la pantalla **General**, escriba una ruta de acceso a un nuevo archivo ZIP al que vaya a realizar la exportación. También puede especificar si quiere exportar *dependencias, relaciones de sustitución, condiciones y entornos virtuales*, así como *contenido para las aplicaciones seleccionadas y dependencias*.  Escriba comentarios del administrador, si quiere, y seleccione **Siguiente**.
1. Compruebe que la aplicación y todas las dependencias se muestran en la página **Objetos relacionados** y seleccione **Siguiente**.
1. En la página Resumen, seleccione **Siguiente**.
1. Una vez completado el proceso, se crea el archivo ZIP y puede cerrar el asistente.

> [!IMPORTANT]
> Si va a copiar esta aplicación en otro entorno, tome el archivo ZIP y la carpeta que lo acompaña. El archivo ZIP debe encontrarse en el mismo directorio que la carpeta creada.

## <a name="import"></a>Importar

> [!NOTE]
> Solo se pueden importar aplicaciones desde rutas de acceso UNC; no puede realizar la importación directamente desde el disco local.

1. En la consola de Configuration Manager, seleccione el nodo **Aplicaciones**. En el grupo Crear de la cinta de opciones, seleccione **Importar aplicación**.
1. Elija el archivo ZIP que quiere importar y seleccione **Siguiente**.
1. En la ventana Contenido de archivo se muestra qué sucede cuando se importa la aplicación. Seleccione **Siguiente**.
1. Revise la pantalla de resumen y seleccione **Siguiente**.
1. Cierre el asistente. La aplicación ya está disponible en el sitio.

## <a name="see-also"></a>Consulte también
 
Automatización de la importación y la exportación de aplicaciones con PowerShell.

* [Import-CMApplication](https://docs.microsoft.com/powershell/module/configurationmanager/import-cmapplication)
* [Export-CMApplication](https://docs.microsoft.com/powershell/module/configurationmanager/export-cmapplication)
