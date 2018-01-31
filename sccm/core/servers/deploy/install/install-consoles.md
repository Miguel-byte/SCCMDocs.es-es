---
title: "Instalación de la consola"
titleSuffix: Configuration Manager
description: "Obtenga información sobre la instalación de la consola de Configuration Manager para conectarse a un sitio de administración central o a un sitio primario."
ms.custom: na
ms.date: 1/3/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d39c201f-d364-4e7b-bde4-faa76d747f33
caps.latest.revision: 
author: mestew
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: ca1c62fc6034b33380d9075c4f5430954537781f
ms.sourcegitcommit: e121d8d3dd82b9f2dde2cb5206cbee602ab8e107
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/17/2018
---
# <a name="install-the-system-center-configuration-manager-console"></a>Instalar la consola de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Los administradores usan la consola de System Center Configuration Manager para administrar el entorno de Configuration Manager. Cada consola de Configuration Manager puede conectarse a un sitio de administración central o a un sitio primario. No puede conectar una consola de Configuration Manager a un sitio secundario.

> [!NOTE]  
>  Los objetos que ve un administrador que ejecuta la consola dependen de los permisos asignados a su cuenta de usuario. Para obtener más información sobre la administración basada en roles, consulte [Fundamentals of role-based administration for System Center Configuration Manager (Aspectos básicos de la administración basada en roles de System Center Configuration Manager)](../../../../core/understand/fundamentals-of-role-based-administration.md).  

 Puede instalar la consola de Configuration Manager durante la instalación del servidor de sitio mediante el Asistente para instalación o puede ejecutar una aplicación de instalación independiente que use al Asistente para instalación.  

 Use el siguiente procedimiento para instalar una consola de Configuration Manager mediante la aplicación independiente.  

## <a name="to-install-the-configuration-manager-console-by-using-the-setup-wizard"></a>Para instalar la consola de Configuration Manager mediante el Asistente para instalación  

1.  Compruebe que se cumplen estos requisitos:  

    -  Tiene derechos de **Administrador local** en el equipo en el que se ejecutará la consola.  

    -   Tiene permisos de **Lectura** para la ubicación de los archivos de instalación de la consola de Configuration Manager.  

2.  Vaya a una de estas ubicaciones:  

    -   En el servidor de sitio, vaya a **<*Ruta de instalación del servidor de sitio de Configuration Manager*>\Tools\ConsoleSetup**.  

    -   Desde los medios de origen de Configuration Manager, vaya a **<*Archivos de origen de Configuration Manager*>\Smssetup\Bin\I386**.  

    > [!TIP]  
    >  Como procedimiento recomendado, inicie la instalación de la consola de Configuration Manager desde un servidor de sitio, en lugar de hacerlo desde los medios de instalación de System Center Configuration Manager. El método de instalación del servidor de sitio copia los archivos de instalación de la consola de Configuration Manager y los paquetes de idiomas admitidos para el sitio en la subcarpeta **Tools\ConsoleSetup**. Instalar la consola de Configuration Manager desde los medios de instalación siempre instalará la versión en inglés, independientemente de los idiomas admitidos en el servidor de sitio o la configuración de idioma del sistema operativo que se ejecuta en el equipo. Opcionalmente, puede copiar la carpeta **ConsoleSetup** en una ubicación alternativa para iniciar la instalación.

3.  Para abrir el Asistente para instalación de la consola de Configuration Manager, haga doble clic en **consolesetup.exe**.  

    > [!IMPORTANT]  
    >  Instale siempre la consola de Configuration Manager mediante consolesetup.exe. Aunque la consola de Configuration Manager se puede instalar ejecutando adminconsole.msi, este método no realiza comprobaciones de dependencia ni de requisitos previos, y es posible que la instalación no se realice correctamente.  

4.  En el asistente, haga clic en **Siguiente**.  

5.  En la página **Servidor de sitio**, escriba el nombre de dominio completo (FQDN) del servidor de sitio al que se conectará la consola de Configuration Manager.  

6.  En la página **Carpeta de instalación**, escriba la carpeta de instalación para la consola de Configuration Manager. La ruta de la carpeta no debe contener espacios finales ni caracteres Unicode.  

7.  En la página **Programa para la mejora de la experiencia del usuario**, elija si quiere participar en dicho programa.  

8.  En la página **Listo para instalar**, haga clic en **Instalar** para instalar la consola de Configuration Manager.  

## <a name="to-install-the-configuration-manager-console-from-a-command-prompt"></a>Para instalar la consola de Configuration Manager desde el símbolo del sistema  

1.  En el servidor desde el que instala la consola de Configuration Manager, abra una ventana del símbolo del sistema y vaya a una de las siguientes ubicaciones:  

    -   **<*Ruta de instalación del servidor de sitio de Configuration Manager*>\Tools\ConsoleSetup**  

    -   **<*Medios de instalación de Configuration Manager*>\SMSSETUP\BIN\I386**  

    > [!TIP]  
    >  Al instalar la consola de Configuration Manager desde el símbolo del sistema, siempre se instala la versión en inglés, independientemente de la configuración de idioma del sistema operativo que se ejecute en el equipo. Para instalar la consola de Configuration Manager en un idioma distinto del inglés, debe [instalar la consola de Configuration Manager mediante el Asistente para instalación](#to-install-the-configuration-manager-console-by-using-the-setup-wizard).  

2.  En el símbolo del sistema, escriba **consolesetup.exe**. Elija una de las siguientes opciones de la línea de comandos.  

|  .     | Descripción     |
  | :------------- | :------------- |
  |/q|Instala la consola de Configuration Manager desatendida. Las opciones **EnableSQM**, **TargetDir**y **DefaultSiteServerName** son obligatorias si usa esta opción.|  
  |/uninstall|Desinstala la consola de Configuration Manager. Primero debe especificar esta opción cuando la use con la opción **/q** .|  
  |LangPackDir|Especifica la ruta de acceso a la carpeta que contiene los archivos de idioma. Puede usar el **Descargador del programa de instalación** para descargar los archivos de idioma. Si no utiliza esta opción, el programa de instalación busca la carpeta de idioma en la carpeta actual. Si no se encuentra la carpeta de idioma, el programa de instalación continúa con la instalación únicamente de la versión en inglés. Para obtener más información, consulte [Descargador del programa de instalación](setup-downloader.md).|  
  |TargetDir|Especifica la carpeta de instalación para instalar la consola de Configuration Manager. Esta opción es obligatoria si usa la opción **/q** .|  
  |EnableSQM|Especifica si se va a participar en el Programa para la mejora de la experiencia del usuario (CEIP). Use un valor de **1** para unirse al CEIP y un valor de **0** para no unirse al programa. Esta opción es obligatoria si usa la opción **/q** .|  
  |DefaultSiteServerName|Especifica el FQDN del servidor de sitio al que se conecta la consola cuando se abre. Esta opción es obligatoria si usa la opción **/q** .|  


  **Ejemplos:**

  -  **consolesetup.exe /q TargetDir="D:\Program Files\ConfigMgr" EnableSQM=1 DefaultSiteServerName=MyServer.Contoso.com**  

  -  **consolesetup.exe /q LangPackDir=C:\Downloads\ConfigMgr TargetDir="D:\Program Files\ConfigMgr Console" EnableSQM=1 DefaultSiteServerName=MyServer.Contoso.com**  

  -  **consolesetup.exe /uninstall /q**  
