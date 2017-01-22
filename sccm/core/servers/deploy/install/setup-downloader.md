---
title: "Descargador del programa de instalación | Microsoft Docs"
description: "Lea sobre esta aplicación independiente diseñada para asegurar que la instalación del sitio usa las versiones actuales de los archivos de instalación principales."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bda87fc5-2e4c-4992-98a4-01770365038c
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: cbe6ebfa80ff8253ec7ed5ad71852fb5cd7e7d91

---
# <a name="setup-downloader-for-system-center-configuration-manager"></a>Descargador del programa de instalación de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Antes de ejecutar el programa de instalación para instalar o actualizar un sitio de System Center Configuration Manager, puede usar esta aplicación independiente (**Setupdl.exe**) de la versión de Configuration Manager que quiera instalar para descargar los archivos de instalación actualizados que necesita el programa de instalación.  

El uso de archivos de instalación actualizados le asegura que la instalación del sitio usará las versiones actuales de los archivos de instalación principales:  

-   Al usar el descargador del programa de instalación para descargar los archivos antes de iniciar la instalación, especifique la carpeta que contendrá los archivos.  

-   La cuenta que use para ejecutar el descargador del programa de instalación debe tener permisos de **Control total** de la carpeta de descarga.  

-   Al ejecutar el programa de instalación para instalar o actualizar un sitio, puede dirigirlo para que use esta copia local de los archivos descargados anteriormente. Esto evita que el programa de instalación tenga que conectarse a Microsoft cuando se inicia la instalación o la actualización del sitio.  

-   Puede usar la misma copia local de los archivos de instalación para instalaciones o actualizaciones posteriores del sitio.  

El descargador del programa de instalación descarga los siguientes tipos de archivos:  

-   Archivos redistribuibles como requisitos previos  

-   Paquetes de idioma  

-   Las últimas actualizaciones del producto para el programa de instalación  

Hay dos opciones para ejecutar el descargador del programa de instalación:  

## <a name="run-setup-downloader-with-the-user-interface"></a>Ejecutar el descargador del programa de instalación con la interfaz de usuario  

1.  En un equipo que tiene acceso a Internet, abra el Explorador de Windows y vaya a **&lt;ConfigMgrInstallationMedia\>\SMSSETUP\BIN\X64**  

2.  Haga doble clic en **Setupdl.exe**. Se abrirá el descargador del programa de instalación.  

3.  Especifique la ruta de acceso de la carpeta en la que se hospedarán los archivos de instalación actualizados y después haga clic en **Descargar**. El descargador del programa de instalación comprueba los archivos que están actualmente en la carpeta de descarga y sólo descarga los archivos que faltan o que son más recientes que los archivos existentes. El descargador del programa de instalación crea subcarpetas para los idiomas descargados. El descargador del programa de instalación creará la carpeta en caso de que no exista.  

4.  Consulte el archivo **ConfigMgrSetup.log** en la raíz de la unidad C para ver los resultados de la descarga.  

## <a name="run-setup-downloader-from-a-command-prompt"></a>Ejecute el descargador del programa de instalación desde el símbolo del sistema  

1.  Abra una ventana del símbolo del sistema y vaya a **&lt;ConfigMgrInstallationMedia\>\SMSSETUP\BIN\X64**  

2.  Ejecute **setupdl.exe** para abrir el descargador del programa de instalación. Si quiere, puede usar las siguientes opciones de línea de comandos con setupdl.exe:  

    -   **/VERIFY**: use esta opción para comprobar los archivos en la carpeta de descarga, que incluyen los archivos de idioma. Consulte el archivo ConfigMgrSetup.log en la raíz de la unidad C para obtener una lista de archivos que no están actualizados. No se descarga ningún archivo al utilizar esta opción.  

    -   **/VERIFYLANG**: use esta opción para comprobar los archivos de idioma en la carpeta de descarga. Consulte el archivo ConfigMgrSetup.log en la raíz de la unidad C para obtener una lista de archivos de idioma que no están actualizados.  

    -   **/LANG**: use esta opción para descargar solo los archivos de idioma en la carpeta de descarga.  

    -   **/NOUI**: use esta opción para iniciar el descargador del programa de instalación sin mostrar la interfaz de usuario. Al usar esta opción, debe especificar la **ruta de acceso de la descarga** como parte de la línea de comandos.  

    -   **&lt;DownloadPath\>**: puede especificar la ruta de acceso a la carpeta de descarga para iniciar el proceso de comprobación o descarga de forma automática. Debe especificar la ruta de acceso de descarga al usar la opción **/NOUI**. Si no se especifica ninguna ruta de acceso de descarga, debe especificarla cuando se abra el descargador del programa de instalación. El descargador del programa de instalación creará la carpeta en caso de que no exista.  

    Ejemplos de uso:  

    -   **setupd &lt;DownloadPath\>**  

        -   El descargador del programa de instalación se inicia, comprueba los archivos de la carpeta de descarga especificada y descarga solo los archivos que faltan o que son más recientes que los archivos existentes  

    -   **setupdl /VERIFY &lt;DownloadPath\>**  

        -   El descargador del programa de instalación se inicia y comprueba los archivos en la carpeta de descarga especificada  

    -   **setupdl /NOUI &lt;DownloadPath\>**  

        -   El descargador del programa de instalación se inicia, comprueba los archivos de la carpeta de descarga especificada y descarga solo los archivos que faltan o que son más recientes que los archivos existentes  

    -   **setupdl /LANG  &lt;DownloadPath\>**  

        -   El descargador del programa de instalación se inicia, comprueba los archivos de la carpeta de descarga especificada y descarga solo los archivos que faltan o que son más recientes que los archivos existentes.  

    -   **setupdl /VERIFY**  

        -   El descargador del programa de instalación se inicia y, a continuación, debe especificar la ruta a la carpeta de descarga. Después de hacer clic en Comprobar, el descargador del programa de instalación comprueba los archivos en la carpeta de descarga  

3.  Consulte el archivo **ConfigMgrSetup.log** en la raíz de la unidad C para ver los resultados de la descarga  



<!--HONumber=Dec16_HO3-->


