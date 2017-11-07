---
title: Instalar Updates Publisher
titleSuffix: Configuration Manager
description: Instalar System Center Updates Publisher en el entorno
ms.custom: na
ms.date: 07/03/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ab5cda93-b67c-4aa5-904d-7b63ce790aa0
caps.latest.revision: "1"
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: NOINDEX, NOFOLLOW
ms.openlocfilehash: 2e11a380ba4c2b3640997d0ce610cba53d5391be
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/12/2017
---
# <a name="install-updates-publisher"></a>Instalar Updates Publisher

*Se aplica a: System Center Updates Publisher*

La información de este tema puede ayudarle a obtener, instalar y configurar Updates Publisher para su uso con el entorno.


## <a name="prerequisites-and-limitations"></a>Requisitos previos y limitaciones
En las secciones siguientes se detallan los requisitos para instalar y usar Updates Publisher, así como las limitaciones y los problemas conocidos para su uso.

### <a name="operating-systems"></a>Sistemas operativos
Instale y ejecute Updates Publisher en ediciones de 64 bits de los sistemas operativos siguientes. No existen requisitos de Service Pack ni de actualización acumulativa mínima.

-   Windows Server 2016 (Standard, Datacenter)
-   Windows Server 2012 R2 (Standard, Datacenter)
-   Windows 10 (Pro, Education, Pro Education, Enterprise)
-   Windows 8.1 (Professional, Enterprise)

### <a name="prerequisites"></a>Requisitos previos
Los siguientes requisitos se aplican al equipo donde se ejecuta Updates Publisher.

-   **Sistema operativo de 64 bits**: el equipo donde instale Updates Publisher debe ejecutar un sistema operativo de 64 bits.
-   **WSUS 4.0 o versiones posteriores**:
    -   En Windows Server, instale la Consola de administración predeterminada para cumplir este requisito.
    -   En Windows 10 y Windows 8.1, instale las [Herramientas de administración remota del servidor (RSAT) para sistemas operativos Windows](https://support.microsoft.com/help/2693643/remote-server-administration-tools-rsat-for-windows-operating-systems). Esto instala la compatibilidad necesaria para usar Updates Publisher (*API y cmdlets de PowerShell* e *Interfaz de usuario de la Consola de administración*).
-   **Permisos**:
    -   Instalación: administrador local
    -   Mayoría de las operaciones: usuario local
    -   Publicación u operaciones que implican WSUS: miembro del grupo de administradores de WSUS en el servidor WSUS.

### <a name="supported-languages"></a>Idiomas compatibles
Updates Publisher solo está disponible en inglés, pero puede administrar actualizaciones en otros idiomas. La compatibilidad de idiomas depende de la tarea, como, por ejemplo, publicar, crear o editar actualizaciones.

Al exportar o publicar actualizaciones, Updates Publisher muestra el título y la descripción de la actualización de software en función de la configuración regional del equipo donde esté instalado Updates Publisher.

Por ejemplo, crea una actualización de software cuyo título está en inglés y en español.

-   Si crea la actualización en un equipo cuya configuración regional corresponde a inglés, verá de forma predeterminada el título y la descripción en inglés.
-   Si luego exporta o publica esa actualización en un equipo cuya configuración regional corresponde a español, en ese equipo verá el título y la descripción en español.

### <a name="publishing"></a>Publicación
Cuando publica actualizaciones de software, puede especificar el idioma del archivo binario de la actualización de software. También puede especificar que el archivo binario es independiente del idioma. Se admiten los idiomas siguientes:

-   Árabe
-   Chino (Hong Kong RAE)
-   Chino (tradicional)
-   Chino (simplificado)
-   Checo
-   Danés
-   Neerlandés
-   Inglés
-   Finés
-   Francés
-   Alemán
-   Griego
-   Hebreo
-   Húngaro
-   Italiano
-   Japonés
-   Coreano
-   Noruego
-   Polaco
-   Portugués
-   Portugués (Brasil)
-   Ruso
-   Español
-   Sueco
-   Turco

### <a name="software-update-titles-and-descriptions"></a>Títulos y descripciones de actualizaciones de software
Se admiten los idiomas siguientes en títulos y descripciones de actualizaciones de software.

-   Chino (tradicional)
-   Chino (simplificado)
-   Inglés
-   Francés
-   Alemán
-   Italiano
-   Japonés
-   Coreano
-   Portugués (Brasil)
-   Ruso
-   Español



## <a name="install-updates-publisher"></a>Instalar Updates Publisher
Obtenga el **UpdatesPubliser.msi** para instalar System Center Updates Publisher desde el [Centro de descarga de Microsoft](https://go.microsoft.com/fwlink/?linkid=847967).

Para instalar Updates Publisher, ejecute el **UpdatesPublisher.msi** en un equipo que cumpla los *requisitos previos*. El instalador crea la siguiente carpeta para que contenga los archivos necesarios para ejecutar Updates Publisher: *&lt;ruta de acceso&gt;\Archivos de programa\Microsoft\UpdatesPublisher*.

Puesto que esta carpeta contiene todos los archivos necesarios para usar Updates Publisher, puede copiar la carpeta y su contenido en otra ubicación o en otro equipo y luego usar Updates Publisher desde esa ubicación. Pero la nueva ubicación o el nuevo equipo debe cumplir los requisitos previos para ejecutar Updates Publisher.

Cuando finalice la instalación, ejecute **UpdatesPublisher.exe** desde la carpeta *UpdatesPublisher* para iniciar Updates Publisher.

## <a name="next-steps"></a>Pasos siguientes
 Después de instalar Updates Publisher, se recomienda [configurar las opciones](updates-publisher-options.md) de Updates Publisher. Debe configurar algunas opciones para poder usar algunas características de Updates Publisher.

 Pero, si quiere usar los valores predeterminados y no tiene previsto implementar actualizaciones en un servidor de actualización ni en dispositivos administrados, puede ir directamente a la sección sobre cómo [administrar catálogos de actualizaciones de software](updates-publisher-catalogs.md) o cómo [crear actualizaciones de software](create-updates-with-updates-publisher.md) y crear sus propios catálogos de actualizaciones.

