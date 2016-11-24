---
title: "Instalación de línea de comandos | System Center Configuration Manager"
description: "Obtenga información sobre cómo ejecutar el programa de instalación de System Center Configuration Manager desde un símbolo del sistema para diversas instalaciones de sitio."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e7cdb1a9-140a-436e-ac71-72d083110223
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: ea097188351cd60a13659e2860c5e0a2bac2c069

---
# <a name="use-a-command-line-to-install-system-center-configuration-manager-sites"></a>Usar una línea de comandos para instalar sitios de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

 Si quiere, puede ejecutar el programa de instalación de System Center Configuration Manager desde un símbolo del sistema para diversas instalaciones de sitio.

 ## <a name="supported-tasks-for-command-line-installs"></a>Tareas admitidas para las instalaciones de línea de comandos
 Este método para ejecutar el programa de instalación es compatible con las siguientes tareas de instalación y de mantenimiento del sitio:

-   **Instalar un sitio de administración central o sitio primario desde una línea de comandos:**  
  Consulte [Command-line options for Setup](../../../../core/servers/deploy/install/command-line-options-for-setup.md) (Opciones de línea de comandos para el programa de instalación).

 -  **Modificar los idiomas que se pueden usar en un sitio de administración central o sitio primario:**  
    Para modificar los idiomas que están instalados en un sitio desde una línea de comandos (incluidos los idiomas para dispositivos móviles), debe hacer lo siguiente:  

     -   Ejecute el programa de instalación desde **&lt;ConfigMgrInstallationPath\>\Bin\X64** en el servidor de sitio.
     -   Use la opción de la línea de comandos **/MANAGELANGS** .
     -   Especifique un archivo de script de idioma que especifique los idiomas que desea agregar o quitar.  

    Por ejemplo, use la siguiente sintaxis de comando: **setupwpf.exe /MANAGELANGS &lt;archivo de script de idioma\>**.  

    Para crear el archivo de script de idioma, use la información de [Command line options to manage languages](../../../../core/servers/deploy/install/command-line-options-for-setup.md#bkmk_Lang) (Opciones de línea de comandos para administrar idiomas).  

 -  **Usar un archivo de script de instalación para realizar instalaciones desatendidas de sitios o para recuperar sitios:**  
    Puede ejecutar el programa de instalación desde una línea de comandos y dirigirlo para que use un script de instalación y ejecute una instalación desatendida del sitio. También puede usar esta opción para recuperar un sitio.    

    Para usar un script con el programa de instalación, haga lo siguiente:  

    -   Ejecute el programa de instalación con la opción de línea de comandos **/SCRIPT** y especifique un archivo de script.  

    -   El archivo de script debe configurarse con las claves y los valores necesarios.  

    Para llevar a cabo una instalación desatendida de un sitio de administración central o un sitio primario, el archivo de script se debe configurar con las secciones siguientes:  

    -   Identificación    
    -   Opciones    
    -   SQLConfigOptions    
    -   HierarchyOptions    

    -   CloudConnectorOptions  

    Para recuperar un sitio, debe usar las siguientes secciones del archivo de script:  

    -   Identificación  

    -   Recuperación

     Para obtener más información sobre la copia de seguridad y recuperación, vea la sección Claves de archivo de script de recuperación de sitio desatendida en el tema Copias de seguridad y recuperación en Configuration Manager.  

    Consulte [Unattended Setup script file keys](../../../../core/servers/deploy/install/command-line-options-for-setup.md#bkmk_Unattended) (Claves de archivo de script de instalación desatendida) para obtener una lista de claves y valores que se pueden usar en un archivo de script de instalación desatendida.  

## <a name="about-the-command-line-script-file"></a>Acerca del archivo de script de línea de comandos  

 Para llevar a cabo instalaciones desatendidas de Configuration Manager, puede ejecutar el programa de instalación con la opción de línea de comandos **/SCRIPT** y especificar un archivo de script que contenga opciones de instalación. Este método admite las siguientes tareas:  

-   Instalar un sitio de administración central  

-   Instalar un sitio primario  

-   Instalar una consola de Configuration Manager  

-   Recuperar un sitio  

> [!NOTE]  
>  No puede usar el archivo de script de instalación desatendida para actualizar un sitio de evaluación a una instalación con licencia de Configuration Manager.  

**Para crear el script**:  
El script de instalación se crea automáticamente al [ejecutar el programa de instalación para instalar un sitio mediante la interfaz de usuario](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md).  Cuando se confirma la configuración en la página **Resumen** del asistente:  

-   El programa de instalación crea el script **%TEMP%\ConfigMgrAutoSave.ini**.  Puede cambiar el nombre de este archivo antes de usarlo, pero este debe conservar la extensión de archivo .ini.  

-   El script de instalación desatendida contiene la configuración seleccionada en el asistente.  

-   Después de crear el script, puede modificarlo para instalar otros sitios en la jerarquía.  

-   Luego puede usar este script para realizar una instalación desatendida de Configuration Manager.  

El archivo de script proporciona el mismo tipo de información que solicita el Asistente para instalación, excepto por el hecho de que no existe una configuración predeterminada.   
Deben especificarse todos los valores de las claves de configuración que se aplican al tipo de instalación que esté utilizando.  

Cuando el programa de instalación crea el script de instalación desatendida, se rellena con el valor de clave de producto que especifique durante la instalación. Este puede ser una clave de producto válida, o bien igual al valor EVAL si instala una versión de evaluación de Configuration Manager. El valor de la clave de producto en el script se rellena para habilitar la comprobación de requisitos previos para finalizar.  

Cuando el programa de instalación inicia la instalación real de un sitio, el script creado automáticamente se escribe otra vez para borrar el valor de la clave de producto en el script que crea. Antes de usar el script para la instalación desatendida de un nuevo sitio, puede editarlo para proporcionar una clave de producto válida o especificar una instalación de evaluación de Configuration Manager.  

**El script contiene valores, nombres de clave y nombres de sección:**  

-   Los nombres de clave de sección requeridos varían según el tipo de instalación para el que crea el script.  

-   No hay un orden determinado para las secciones ni para las claves de las secciones.  

-   Las claves no distinguen mayúsculas de minúsculas.  

-   Cuando proporciona valores para las claves, el nombre de la clave debe ir seguido por un signo de igual (=) y el valor de la clave.  

> [!TIP]  
>  Para ver el conjunto completo de opciones, consulte [Command-line options for Setup and scripts](../../../../core/servers/deploy/install/command-line-options-for-setup.md) (Opciones de línea de comandos para el programa de instalación y los scripts).  

## <a name="to-use-the-script-setup-command-line-option"></a>Para usar la opción de línea de comandos de instalación /SCRIPT, haga lo siguiente:

-   Debe usar un archivo de script de instalación y especificar el nombre de archivo después de la opción de línea de comandos del programa de instalación **/SCRIPT** .  

    -   El nombre del archivo debe tener la extensión de nombre de archivo **.ini**  

    -   Cuando hace referencia al archivo de script del programa de instalación en el símbolo del sistema, debe proporcionar la ruta de acceso completa al archivo. Por ejemplo, si su archivo de inicialización de instalación se denomina Setup.ini y se almacena en la carpeta C:\Setup, en el símbolo del sistema, escriba:  **setup /script c:\setup\setup.ini**  

-   La cuenta que ejecuta el programa de instalación debe tener credenciales administrativas en el equipo. Al ejecutar el programa de instalación con el script de instalación desatendida, inicie el símbolo del sistema mediante **Run as administrator**.  



<!--HONumber=Nov16_HO1-->


