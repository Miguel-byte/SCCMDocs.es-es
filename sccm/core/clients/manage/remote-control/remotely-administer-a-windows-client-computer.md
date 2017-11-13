---
title: "Administración remota de un equipo Windows"
titleSuffix: Configuration Manager
description: Administre un equipo cliente de Windows remoto mediante System Center Configuration Manager.
ms.custom: na
ms.date: 07/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3c9648c4-645e-4e47-ae10-2da817b8c83b
caps.latest.revision: "5"
caps.handback.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 7cce5f2deab7ec6f5c16628dc53e4d1cb5507f37
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/12/2017
---
# <a name="how-to-remotely-administer-a-windows-client-computer-by-using-system-center-configuration-manager"></a>Cómo administrar de forma remota un equipo cliente de Windows con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Antes de empezar a usar el control remoto, asegúrese de revisar la información de los siguientes temas:  

-   [Requisitos previos del control remoto en System Center Configuration Manager](../../../../core/clients/manage/remote-control/prerequisites-for-remote-control.md)  

-   [Configuración del control remoto en System Center Configuration Manager](../../../../core/clients/manage/remote-control/configuring-remote-control.md)  

A continuación se indican tres formas de iniciar el visor de control remoto:  

-   En la consola de Configuration Manager.  

-   En un símbolo del sistema de Windows.  

-   En el menú **Inicio** de Windows en un equipo que ejecute la consola de Configuration Manager desde el grupo de programas **Microsoft System Center**.  

### <a name="to-remotely-administer-a-client-computer-from-the-configuration-manager-console"></a>Para administrar de forma remota un equipo cliente desde la consola de Configuration Manager  

1.  En la consola de Configuration Manager, seleccione **Activos y compatibilidad** > **Dispositivos** o **Recopilaciones de dispositivos**.  

3.  Seleccione el equipo que quiere administrar de forma remota y, después, en la pestaña **Inicio**, en el grupo **Dispositivo**, seleccione **Iniciar** > **Control remoto**.  

    > [!IMPORTANT]  
    >  Si el permiso **Solicitar al usuario permiso de control remoto** de la configuración de cliente está establecido en **True**, la conexión no se inicia hasta que el usuario en el equipo remoto acepta la solicitud de control remoto. Para obtener más información, consulte [Configuración del control remoto en System Center Configuration Manager](../../../../core/clients/manage/remote-control/configuring-remote-control.md).  

4.  Cuando se abra la ventana **Control remoto de Configuration Manager** , puede administrar de forma remota el equipo cliente. Use las opciones siguientes para configurar la conexión.  

    > [!NOTE]  
    >  Si el equipo al que se conecta tiene varios monitores, la visualización de todos los monitores se muestra en la ventana de control remoto.  

    -   **Archivo - Conectar**: se establece una conexión con otro equipo. Esta opción no está disponible cuando está activa una sesión de control remoto.  

    -   **Archivo - Desconectar**: desconecta la sesión de control remoto activa, pero no cierra la ventana **Control remoto de Configuration Manager**.  

    -   **Archivo - Salir**: desconecta la sesión de control remoto activa y cierra la ventana **Control remoto de Configuration Manager**.  

        > [!NOTE]  
        >  Cuando se desconecta una sesión de control remoto, se elimina el contenido del Portapapeles de Windows en el equipo que está visualizando.  

    -   **Ver pantalla completa**: maximiza la ventana **Control remoto de Configuration Manager**.  

        > [!NOTE]  
        >  Para salir del modo de pantalla completa, presione Ctrl+Alt+Interrumpir.  

    -   **Vista - Ajustar tamaño al contenido**: ajusta la visualización del equipo remoto al tamaño de la ventana **Control remoto de Configuration Manager**.  

    -   **Vista - Barra de estado**: activa o desactiva la visualización de la barra de estado de la ventana **Control remoto de Configuration Manager**.  

    -   **Acción - Enviar tecla Ctrl+Alt+Supr**: envía la combinación de teclas Ctrl+Alt+Supr al equipo remoto.  

    -   **Acción - Habilitar uso compartido del Portapapeles**: le permite copiar elementos del equipo remoto y pegar elementos en él. Si cambia este valor, debe reiniciar la sesión de control remoto para que el cambio surta efecto.  

        > [!NOTE]  
        >  Si no quiere habilitar el uso compartido del Portapapeles en la consola de Configuration Manager, en el equipo que ejecuta la consola, establezca el valor de la clave de registro, **HKEY_CURRENT_USER\Software\Microsoft\ConfigMgr10\Remote Control\Clipboard Sharing** en **0**.  

    -   **Acción - Bloquear teclado y mouse remotos**: bloquea el teclado y el mouse remotos para impedir que el usuario use el equipo remoto.  

    -   **Ayuda - Acerca del control remoto**: muestra la versión actual del visor.  

5.  Los usuarios del equipo remoto pueden ver más información sobre la sesión de control remoto al hacer clic en el icono **Control remoto** de Configuration Manager del área de notificación de Windows o en el icono de la barra de la sesión de control remoto.  

### <a name="to-start-the-remote-control-viewer-from-the-windows-command-line"></a>Puede iniciar el visor de control remoto desde la línea de comandos de Windows.  

-   En el símbolo del sistema de Windows, escriba *<carpeta de instalación de Configuration Manager\>***\AdminConsole\Bin\x64\CmRcViewer.exe**  

CmRcViewer.exe admite las siguientes opciones de línea de comandos:  

- *Dirección*: especifica el nombre NetBIOS, el nombre de dominio completo (FQDN) o la dirección IP del equipo cliente que al que quiere conectarse.
- *Nombre de servidor de sitio*: especifica el nombre del servidor de sitio de System Center Configuration Manager al que quiere enviar mensajes de estado relacionados con la sesión de control remoto.
- **/?** - Muestra las opciones de línea de comandos para el visor de control remoto.  
     
**Ejemplo: CmRcViewer.exe** *<Dirección\>* *<\\\Nombre de servidor de sitio>*  
