---
title: Instalación de la consola
titleSuffix: Configuration Manager
description: Instale la consola de Configuration Manager para conectarse a un sitio de administración central o a un sitio primario.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d39c201f-d364-4e7b-bde4-faa76d747f33
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 35bfd908864ee77c19821ce02ab62c03523fae37
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56126953"
---
# <a name="install-the-system-center-configuration-manager-console"></a>Instalar la consola de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Los administradores usan la consola de Configuration Manager para administrar el entorno de Configuration Manager. Cada consola de Configuration Manager puede conectarse a un sitio de administración central o a un sitio primario. No se puede conectar una consola de Configuration Manager a un sitio secundario.

> [!NOTE]  
>  Un administrador ve los objetos en la consola en función de los permisos asignados a su cuenta de usuario. Para obtener más información sobre la administración basada en roles, vea [Aspectos básicos de la administración basada en roles](../../../../core/understand/fundamentals-of-role-based-administration.md).  

 Cuando se instala el servidor de sitio, se puede instalar al mismo tiempo la consola de Configuration Manager. Para instalar la consola de forma independiente a la instalación del servidor de sitio, ejecute el instalador independiente.  

 Use los procedimientos siguientes para instalar la consola de Configuration Manager mediante el instalador independiente.  

## <a name="to-install-the-configuration-manager-console-by-using-the-setup-wizard"></a>Para instalar la consola de Configuration Manager mediante el Asistente para instalación  

1.  Compruebe que se cumplen estos requisitos:  

    -  Tiene derechos de **Administrador** local en el equipo de destino para la consola.  

    -   Tiene permisos de **Lectura** para la ubicación de los archivos de instalación de la consola de Configuration Manager.  

2.  Vaya a una de estas ubicaciones:  

    -   En el servidor de sitio, vaya a: `<Configuration Manager site server installation path>\Tools\ConsoleSetup`  

    -   Desde el medio de origen de Configuration Manager, vaya a: `<Configuration Manager source files>\Smssetup\Bin\I386`  

    > [!TIP]  
    >  Como procedimiento recomendado, inicie el instalador de la consola de Configuration Manager desde un servidor de sitio, en lugar de hacerlo desde los medios de instalación de System Center Configuration Manager. Al instalar el servidor de sitio, copia los archivos de instalación de la consola de Configuration Manager y los paquetes de idioma admitidos para el sitio en la subcarpeta **Tools\ConsoleSetup**. Al instalar la consola de Configuration Manager desde el medio de instalación siempre se instala la versión en inglés. Este comportamiento se produce incluso si el servidor de sitio admite varios idiomas, o bien si el sistema operativo del equipo de destino está establecido en otro idioma. Opcionalmente, puede copiar la carpeta **ConsoleSetup** en una ubicación alternativa para iniciar la instalación.

3.  Para abrir el Asistente para instalación de la consola de Configuration Manager, haga doble clic en **consolesetup.exe**.  

    > [!IMPORTANT]  
    >  Instale siempre la consola de Configuration Manager mediante **consolesetup.exe**. Aunque se puede instalar la consola de Configuration Manager con adminconsole.msi, este método no ejecuta los requisitos previos ni las comprobaciones de dependencia. Es posible que la instalación no se realice correctamente.  

4.  En el asistente, haga clic en **Siguiente**.  

5.  En la página **Servidor de sitio**, escriba el nombre de dominio completo (FQDN) del servidor de sitio al que se conecta la consola de Configuration Manager.  

6.  En la página **Carpeta de instalación**, escriba la carpeta de instalación para la consola de Configuration Manager. La ruta de la carpeta no debe contener espacios finales ni caracteres Unicode.  

7.  En la página **Programa para la mejora de la experiencia del usuario**, elija si quiere participar en dicho programa.  
    > [!Note]  
    > A partir de la versión 1802 de Configuration Manager, la característica CEIP se ha quitado del producto.

8.  En la página **Listo para instalar**, haga clic en **Instalar** para instalar la consola de Configuration Manager.  



## <a name="to-install-the-configuration-manager-console-from-a-command-prompt"></a>Para instalar la consola de Configuration Manager desde el símbolo del sistema  

1.  En el servidor desde el que se instala la consola de Configuration Manager, abra una ventana del símbolo del sistema y vaya a una de las ubicaciones siguientes:  

    -   `<Configuration Manager site server installation path>\Tools\ConsoleSetup`  

    -   `<Configuration Manager installation media>\SMSSETUP\BIN\I386`  

    > [!TIP]  
    >  Al instalar la consola de Configuration Manager desde un símbolo del sistema siempre se instala la versión en inglés. Este comportamiento se produce incluso si el sistema operativo del equipo de destino está establecido en otro idioma. Para instalar la consola de Configuration Manager en un idioma distinto del inglés, debe [instalar la consola de Configuration Manager mediante el Asistente para instalación](#to-install-the-configuration-manager-console-by-using-the-setup-wizard).  

2.  En el símbolo del sistema, escriba **consolesetup.exe**. Elija una de las opciones siguientes de la línea de comandos:  

|  .     | Descripción     |
  |-------------|-------------|
  |/q|Instala la consola de Configuration Manager desatendida. Las opciones **EnableSQM**, **TargetDir**y **DefaultSiteServerName** son obligatorias si usa esta opción.|  
  |/uninstall|Desinstala la consola de Configuration Manager. Especifique primero esta opción cuando la use con la opción **/q**.|  
  |LangPackDir|Especifica la ruta de acceso a la carpeta que contiene los archivos de idioma. Puede usar el **Descargador del programa de instalación** para descargar los archivos de idioma. Si no utiliza esta opción, el programa de instalación busca la carpeta de idioma en la carpeta actual. Si no se encuentra la carpeta de idioma, el programa de instalación continúa con la instalación únicamente de la versión en inglés. Para obtener más información, consulte [Descargador del programa de instalación](setup-downloader.md).|  
  |TargetDir|Especifica la carpeta de instalación para instalar la consola de Configuration Manager. Esta opción es obligatoria si usa la opción **/q** .|  
  |EnableSQM|Especifica si se va a participar en el Programa para la mejora de la experiencia del usuario (CEIP). Use un valor de **1** para unirse al CEIP y un valor de **0** para no unirse al programa. Esta opción es obligatoria si usa la opción **/q** .</br></br>Nota: A partir de la versión 1802 de Configuration Manager, la característica CEIP se ha quitado del producto.  El uso del parámetro hará que la instalación dé error.|  
  |DefaultSiteServerName|Especifica el FQDN del servidor de sitio al que se conecta la consola cuando se abre. Esta opción es obligatoria si usa la opción **/q** .|  


  ### <a name="examples"></a>Ejemplos
  **Para la versión 1802 y más recientes, NO incluya el parámetro EnableSQM**
  -  `ConsoleSetup.exe /q TargetDir="%ProgramFiles%\ConfigMgr Console" DefaultSiteServerName=MyServer.Contoso.com`

  -  `ConsoleSetup.exe /q TargetDir="C:\Program Files\ConfigMgr Console" DefaultSiteServerName=MyServer.Contoso.com EnableSQM=1  LangPackDir=C:\Downloads\ConfigMgr`  

  -  `ConsoleSetup.exe /uninstall /q`  
