---
title: La carpeta CD.Latest | System Center Configuration Manager
description: "Obtenga información sobre el nuevo proceso de actualización que proporciona actualizaciones al producto desde la consola de Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
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
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: fc63227aa4345fb58e7efc15abd55071fb33e5d5


---
# <a name="the-cdlatest-folder-for-system-center-configuration-manager"></a>La carpeta CD.Latest para System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

System Center Configuration Manager introduce un nuevo proceso de actualización que proporciona actualizaciones al producto desde la consola de Configuration Manager. Para admitir este nuevo método de actualización de Configuration Manager, se crea una nueva carpeta denominada **CD.Latest** que contiene una copia de los archivos de instalación de Configuration Manager de la versión actualizada de su sitio.  

A partir de la actualización 1606, la carpeta CD.Latest contiene una carpeta denominada **Redist** , que contiene los archivos redistribuibles que configura las descargas y los usos. Estos archivos coinciden con la versión de los archivos de Configuration Manager que se encuentran en la carpeta CD.Latest. Al ejecutar el programa de instalación desde una carpeta CD.Latest más reciente, debe utilizar los archivos que coincidan con esa versión del programa de instalación. Para ello puede dirigir el programa de instalación para descargar los archivos nuevos y actuales de Microsoft o dirigir el programa de instalación para utilizar los archivos desde la carpeta Redist incluida en la carpeta CD.Latest.

> [!TIP]
> Si aún no ha instalado la versión 1606, debe asegurarse de que los archivos de redistribución que usa están actualizados. Si no ha descargado los archivos de redistribución recientemente, permita que el programa de instalación lo haga desde Microsoft.   

 A continuación se presentan diferentes escenarios en los que se crea o actualiza la carpeta CD.Latest en un sitio de administración central o un servidor de sitio primario:  

-   Si instala una actualización o una revisión desde la consola de Configuration Manager: la carpeta se crea o se actualiza en la carpeta de instalación de Configuration Manager.  

-   Si ejecuta la tarea de copia de seguridad integrada de Configuration Manager: la carpeta se crea o se actualiza en la ubicación de la carpeta de copia de seguridad designada.  

Los archivos de origen de la carpeta CD.Latest se admiten para lo siguiente:  

1.  **Copia de seguridad y recuperación:** la carpeta CD.Latest contiene archivos de origen que se usan para volver a instalar el sitio como parte de una recuperación del sitio. Para recuperar un sitio de Configuration Manager, la copia de seguridad de sitio debe incluir la carpeta CD.Latest (la tarea de copia de seguridad de sitio integrada incluye de forma automática esta carpeta como parte de la copia de seguridad del sitio).  

    -   **Cuando vuelva a instalar el sitio como parte de una recuperación del sitio** , hágalo desde la carpeta CD.Latest incluida en la copia de seguridad. De este modo, el sitio se instala con las versiones de archivo que coinciden con la copia de seguridad del sitio y la base de datos del sitio.  

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



<!--HONumber=Nov16_HO1-->


