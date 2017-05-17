---
title: Carpeta CD.Latest | Microsoft Docs
description: "Obtenga información sobre el nuevo proceso de actualización que proporciona actualizaciones al producto desde la consola de Configuration Manager."
ms.custom: na
ms.date: 05/02/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8db92d67-5d9c-4e9c-80d0-ae6fa0dd4817
caps.latest.revision: 6
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 90775fcf2549080a43e9c1606caa79d9eb90a89c
ms.openlocfilehash: 5c39e09b44500fa2f356f83579bb2fb2c1d0e937
ms.contentlocale: es-es
ms.lasthandoff: 05/17/2017


---
# <a name="the-cdlatest-folder-for-system-center-configuration-manager"></a>La carpeta CD.Latest para System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

System Center Configuration Manager introduce un nuevo proceso de actualización que proporciona actualizaciones al producto desde la consola de Configuration Manager. Para admitir este nuevo método de actualización de Configuration Manager, se crea una nueva carpeta denominada **CD.Latest** que contiene una copia de los archivos de instalación de Configuration Manager de la versión actualizada de su sitio.  

A partir de la actualización 1606, la carpeta CD.Latest contiene una carpeta denominada **Redist** , que contiene los archivos redistribuibles que configura las descargas y los usos. Estos archivos coinciden con la versión de los archivos de Configuration Manager que se encuentran en la carpeta CD.Latest. Al ejecutar el programa de instalación desde una carpeta CD.Latest más reciente, debe utilizar los archivos que coincidan con esa versión del programa de instalación. Para ello puede dirigir el programa de instalación para descargar los archivos nuevos y actuales de Microsoft o dirigir el programa de instalación para utilizar los archivos desde la carpeta Redist incluida en la carpeta CD.Latest.

En cambio, el medio de línea base, como la versión de línea base 1606 que se ha publicado en octubre de 2016, no incluye una carpeta Redist. No se creará la carpeta Redist hasta que se instale una actualización en la consola. Mientras tanto, use la carpeta Redist que ha usado al instalar sitios desde el medio de línea base.  

> [!TIP]
> Si aún no ha instalado la versión 1606, debe asegurarse de que los archivos de redistribución que usa están actualizados. Si no ha descargado los archivos de redistribución recientemente, permita que el programa de instalación lo haga desde Microsoft.   

 A continuación se presentan diferentes escenarios en los que se crea o actualiza la carpeta CD.Latest en un sitio de administración central o un servidor de sitio primario:  

-   Si instala una actualización o una revisión desde la consola de Configuration Manager: la carpeta se crea o se actualiza en la carpeta de instalación de Configuration Manager.  

-   Si ejecuta la tarea de copia de seguridad integrada de Configuration Manager: la carpeta se crea o se actualiza en la ubicación de la carpeta de copia de seguridad designada.  

-  A partir de la versión 1606, la carpeta CD.Latest se crea al instalar un sitio nuevo con un medio de línea base (como la versión 1606 o 1702).

Los archivos de origen de la carpeta CD.Latest se admiten para lo siguiente:  

1.  **Copia de seguridad y recuperación:** para recuperar un sitio, debe utilizar los archivos de origen de una carpeta CD.Latest que coincida con el sitio. Al ejecutar una copia de seguridad de sitio mediante la tarea de copia de seguridad de sitio integrada, la carpeta CD.Latest se incluye como parte de la copia de seguridad.

    -   **Cuando vuelva a instalar el sitio como parte de una recuperación del sitio** , hágalo desde la carpeta CD.Latest incluida en la copia de seguridad. De este modo, el sitio se instala con las versiones de archivo que coinciden con la copia de seguridad del sitio y la base de datos del sitio.  Si no tiene acceso a la versión de la carpeta CD.Latest correcta, puede obtener una carpeta CD.Latest con las versiones de archivo correctas mediante la instalación de un sitio en un entorno de laboratorio y la posterior actualización de dicho sitio para que coincida con la versión que desea recuperar.

        > [!IMPORTANT]  
        >  Si no tiene disponibles la carpeta CD.Lastest correcta y su contenido, no se puede recuperar un sitio y este debe volver a instalarse.  

    -   Cuando no tiene una carpeta CD.Latest pero sí un sitio primario secundario o un sitio de administración central en funcionamiento, puede usar ese sitio como sitio de referencia en una recuperación del sitio.  

2.  **Para instalar un sitio primario secundario:** si desea instalar un nuevo sitio primario secundario debajo de un sitio de administración central que ha instalado una o varias actualizaciones en la consola, debe usar el programa de instalación y los archivos de origen de la carpeta CD.Latest desde el sitio de administración central. Si el programa de instalación se ejecuta desde una copia de la carpeta CD.Latest del sitio de administración central, utiliza los archivos de origen de la instalación que coinciden con la versión del sitio de administración central. Para obtener más información, consulte [Use the Setup Wizard to install sites](../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md) (Usar el asistente para instalación para instalar sitios).  

3.  **Para expandir un sitio primario independiente:** si va a expandir un sitio primario independiente mediante la instalación de un nuevo sitio de administración central, debe usar el programa de instalación y los archivos de origen de la carpeta CD.Latest desde el sitio primario para instalar el nuevo sitio de administración central. Cuando se ejecuta desde una copia de la carpeta CD.Latest desde el sitio primario, utiliza los archivos de origen de instalación que coinciden con la versión del sitio primario. Para obtener más información, consulte [Expandir un sitio primario independiente](../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_expand) en [Use the Setup Wizard to install sites](../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md)(Usar el asistente para instalación para instalar sitios)

> [!IMPORTANT]  
>  Los archivos de origen de CD.Latest actualizados no se admiten para lo siguiente:  
>   
>  -   Instalación de un sitio nuevo para una jerarquía nueva  
>  -   Actualización de un sitio de Microsoft System Center 2012 Configuration Manager a System Center Configuration Manager

