---
title: Instalar consolas | System Center Configuration Manager
description: "Obtenga información sobre la instalación de las consolas de Configuration Manager para conectarse a un sitio de administración central o a un sitio primario."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d39c201f-d364-4e7b-bde4-faa76d747f33
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 1483e35a397667a340605c0454c1835ec6067d9e

---
# <a name="install-system-center-configuration-manager-consoles"></a>Instalar las consolas de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*


Los usuarios administrativos usan la consola de System Center Configuration Manager para administrar el entorno de Configuration Manager. Cada consola de Configuration Manager puede conectarse a un sitio de administración central o a un sitio primario. No puede conectar una consola de Configuration Manager a un sitio secundario.


> [!NOTE]  
>  Los objetos que se muestran para el usuario administrativo que ejecuta la consola dependen de los derechos que tenga asignados. Para obtener más información sobre la administración basada en roles, consulte [Fundamentals of role-based administration for System Center Configuration Manager (Aspectos básicos de la administración basada en roles de System Center Configuration Manager)](../../../../core/understand/fundamentals-of-role-based-administration.md).  

 Puede instalar la consola de Configuration Manager durante la instalación del servidor de sitio en el Asistente para instalación, o ejecutar la aplicación independiente.  

 Use el siguiente procedimiento para instalar una consola de Configuration Manager mediante una aplicación independiente.  

## <a name="to-install-a-configuration-manager-console"></a>Para instalar una consola de Configuration Manager  

1.  Compruebe que el usuario administrativo que ejecuta la aplicación de la consola de Configuration Manager tiene los siguientes derechos de seguridad administrativos:  

    -   Derechos de**Administrador local** en el equipo en el que se ejecutará la consola.  

    -   Permiso de**Lectura** para la ubicación de los archivos de instalación de la consola de Configuration Manager.  

2.  Examine una de las siguientes ubicaciones:  

    -   Desde los medios de origen de Configuration Manager, vaya a **&lt;ConfigMgrSourceFiles\>\Smssetup\Bin\I386**.  

    -   En el servidor de sitio, vaya a **&lt;ConfigMgrSiteServerInstallationPath\>\Tools\ConsoleSetup**.  

    > [!TIP]  
    >  Como procedimiento recomendado, inicie la instalación de la consola de Configuration Manager desde un servidor de sitio, en lugar de hacerlo desde los medios de instalación de System Center Configuration Manager. El método de instalación de servidor de sitio copia los archivos de instalación de la consola de Configuration Manager y los paquetes de idiomas admitidos para el sitio en la subcarpeta **Tools\ConsoleSetup**. Si instala la consola de Configuration Manager desde los medios de instalación, siempre se instalará la versión en inglés, independientemente de los idiomas admitidos en el servidor de sitio o la configuración de idioma del sistema operativo que se ejecuta en el equipo. Opcionalmente, puede copiar la carpeta **ConsoleSetup** en una ubicación alternativa para iniciar la instalación.  

3.  Haga doble clic en **consolesetup.exe**. Se abre el Asistente para instalación de la consola de Configuration Manager.  

    > [!IMPORTANT]  
    >  Instale siempre la consola de Configuration Manager mediante consolesetup.exe. Aunque la consola de Configuration Manager se puede instalar ejecutando AdminConsole.msi, este método no realiza comprobaciones de dependencia ni de requisitos previos, y la instalación podría no realizarse correctamente.  

4.  En la página inicial, haga clic en **Siguiente**.  

5.  En la página **Servidor de sitio**, especifique el nombre de dominio completo (FQDN) del servidor de sitio al que se conectará la consola de Configuration Manager.  

6.  En la página **Carpeta de instalación**, especifique la carpeta de instalación para la consola de Configuration Manager. La ruta de la carpeta no debe contener espacios finales ni caracteres Unicode.  

7.  En la página **Programa para la mejora de la experiencia del usuario** , elija si desea participar en dicho programa.  

8.  En la página **Listo para instalar**, haga clic en **Instalar** para instalar la consola de Configuration Manager.  

## <a name="to-install-a-configuration-manager-console-from-a-command-prompt"></a>Para instalar una consola de Configuration Manager desde el símbolo del sistema  

1.  En el servidor desde el que instala la consola de Configuration Manager, abra una ventana del símbolo del sistema y examine una de las siguientes ubicaciones:  

    -   **&lt;ConfigMgrSiteServerInstallationPath\>\Tools\ConsoleSetup**  

    -   **&lt;ConfigMgrInstallationMedia\>\SMSSETUP\BIN\I386**  

    > [!TIP]  
    >  Al instalar una consola de Configuration Manager desde el símbolo del sistema, siempre se instala la versión en inglés, independientemente de la configuración de idioma del sistema operativo que se ejecute en el equipo. Para instalar la consola de Configuration Manager en otro idioma, use el procedimiento anterior.  

2.  Escriba **consolesetup.exe** y elija una de las siguientes opciones de la línea de comandos.  

|  .     | Descripción     |
  | :------------- | :------------- |
  |/q|Instala la consola de Configuration Manager desatendida. Las opciones **EnableSQM**, **TargetDir**y **DefaultSiteServerName** son obligatorias si usa esta opción.|  
  |/uninstall|Desinstala la consola de Configuration Manager. Primero debe especificar esta opción cuando la use con la opción **/q** .|  
  |LangPackDir|Especifica la ruta de acceso a la carpeta que contiene los archivos de idioma. Puede usar el **Descargador del programa de instalación** para descargar los archivos de idioma. Si no utiliza esta opción, el programa de instalación busca la carpeta de idioma en la carpeta actual. Si no se encuentra la carpeta de idioma, el programa de instalación continúa con la instalación únicamente de la versión en inglés. Para obtener más información, consulte [Descargador del programa de instalación](/sccm/core/servers/deploy/install/setup-downloader).|  
  |TargetDir|Especifica la carpeta de instalación para instalar la consola de Configuration Manager. Esta opción es obligatoria si usa la opción **/q** .|  
  |EnableSQM|Especifica si se va a participar en el Programa para la mejora de la experiencia del usuario (CEIP). Utilice un valor de 1 para participar en el Programa para la mejora de la experiencia del usuario, y un valor de 0 para no participar. Esta opción es obligatoria si usa la opción **/q** .|  
  |DefaultSiteServerName|Especifica el FQDN del servidor de sitio al que se conecta la consola cuando se abre. Esta opción es obligatoria si usa la opción **/q** .|  


  **Ejemplos de uso:**  
  -  **consolesetup.exe /q TargetDir="D:\Program Files\ConfigMgr" EnableSQM=1 DefaultSiteServerName=MyServer.Contoso.com**  

  -  **consolesetup.exe /q LangPackDir=C:\Downloads\ConfigMgr TargetDir="D:\Program Files\ConfigMgr" Console EnableSQM=1 DefaultSiteServerName=MyServer.Contoso.com**  

  -  **consolesetup.exe /uninstall /q**  



<!--HONumber=Nov16_HO1-->


