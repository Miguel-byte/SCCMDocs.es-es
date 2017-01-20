---
title: Administrar un equipo de Windows de forma remota | System Center Configuration Manager
description: Administre un equipo cliente de Windows remoto mediante System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3c9648c4-645e-4e47-ae10-2da817b8c83b
caps.latest.revision: 5
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 02c11420d3b05ad4eaae31d9413b66459751da70
ms.openlocfilehash: 51a9b7269993bfa133382b88792ac94032824eed


---
# <a name="how-to-remotely-administer-a-windows-client-computer-by-using-system-center-configuration-manager"></a>Cómo administrar de forma remota un equipo cliente de Windows con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Use el procedimiento siguiente para administrar de forma remota un equipo en System Center Configuration Manager.  

 Antes de empezar a usar el control remoto, asegúrese de revisar la información de los siguientes temas:  

-   [Requisitos previos del control remoto en System Center Configuration Manager](../../../../core/clients/manage/remote-control/prerequisites-for-remote-control.md)  

-   [Configuración del control remoto en System Center Configuration Manager](../../../../core/clients/manage/remote-control/configuring-remote-control.md)  

 Puede iniciar el visor de control remoto de Configuration Manager mediante uno de estos tres métodos:  

-   Con la consola de Configuration Manager.  

-   En el símbolo del sistema de Windows.  

-   En el menú **Inicio** de Windows en un equipo que ejecuta la consola de Configuration Manager desde el grupo de programas **Microsoft System Center 2012**.  

### <a name="to-remotely-administer-a-client-computer-from-the-configuration-manager-console"></a>Para administrar de forma remota un equipo cliente desde la consola de Configuration Manager  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad**.  

2.  En el área de trabajo **Activos y compatibilidad** , haga clic en **Dispositivos** o en **Recopilaciones de dispositivos**.  

3.  Seleccione el equipo que quiere administrar de forma remota y, a continuación, en la pestaña **Inicio** , en el grupo **Dispositivo** , haga clic en **Iniciar**y, a continuación, haga clic en **Control remoto**.  

    > [!IMPORTANT]  
    >  Si el permiso **Solicitar al usuario permiso de control remoto** de la configuración de cliente está establecido en **True**, la conexión no se inicia hasta que el usuario en el equipo remoto acepta la solicitud de control remoto. Para obtener más información, consulte [Configuración del control remoto en System Center Configuration Manager](../../../../core/clients/manage/remote-control/configuring-remote-control.md).  

4.  Cuando se abra la ventana **Control remoto de Configuration Manager** , puede administrar de forma remota el equipo cliente. Use las opciones siguientes para configurar la conexión.  

    > [!NOTE]  
    >  Si el equipo al que se conecta tiene varios monitores, la visualización de todos estos monitores se muestra en la ventana de control remoto.  

    -   **Archivo - Conectar**: se establece una conexión con otro equipo. Esta opción no está disponible cuando está activa una sesión de control remoto.  

    -   **Archivo - Desconectar**: desconecta la sesión de control remoto activa, pero no cierra la ventana **Control remoto de Configuration Manager**.  

    -   **Archivo - Salir**: desconecta la sesión de control remoto activa y cierra la ventana **Control remoto de Configuration Manager**.  

        > [!NOTE]  
        >  Cuando se desconecta una sesión de control remoto, se elimina el contenido del Portapapeles de Windows en el equipo que está visualizando.  

    -   **Vista - Pantalla completa**: maximiza la ventana **Control remoto de Configuration Manager** para ocupar todo el espacio de visualización disponible.  

        > [!NOTE]  
        >  Para salir del modo de pantalla completa, presione Ctrl+Alt+Interrumpir.  

    -   **Vista - Ajustar tamaño al contenido**: ajusta la visualización del equipo remoto al tamaño de la ventana **Control remoto de Configuration Manager**.  

    -   **Vista - Barra de estado**: activa o desactiva la visualización de la barra de estado de la ventana **Control remoto de Configuration Manager**.  

    -   **Acción - Enviar tecla Ctrl+Alt+Supr**: envía la combinación de teclas Ctrl+Alt+Supr al equipo remoto.  

    -   **Acción - Habilitar uso compartido del Portapapeles**: le permite copiar elementos del equipo remoto y pegar elementos en él. Si cambia este valor, debe reiniciar la sesión de control remoto para que el cambio surta efecto.  

        > [!NOTE]  
        >  Si no quiere habilitar el uso compartido del Portapapeles en la consola de Configuration Manager, en el equipo que ejecuta la consola, establezca el valor de la clave de registro, **HKEY_CURRENT_USER\Software\Microsoft\ConfigMgr10\Remote Control\Clipboard Sharing** en **0**.  

    -   **Acción - Bloquear teclado y mouse remotos**: bloquea el teclado y el mouse remotos para impedir que el usuario use el equipo remoto.  

    -   **Ayuda - Acerca del Control remoto**: muestra información sobre la versión actual del visor de control remoto.  

5.  Los usuarios del equipo remoto pueden ver más información sobre la sesión de control remoto al hacer clic en el icono **Control remoto** de Configuration Manager del área de notificación de Windows o en el icono de la barra de la sesión de control remoto.  

6.  Cuando ya no necesite la sesión de control remoto, use uno de los métodos detallados anteriormente para finalizar la sesión de control remoto.  

### <a name="to-start-the-remote-control-viewer-from-the-windows-command-line"></a>Puede iniciar el visor de control remoto desde la línea de comandos de Windows.  

-   En el símbolo del sistema de Windows, escriba *<carpeta de instalación de Configuration Manager\>***\AdminConsole\Bin\x64\CmRcViewer.exe**  

    > [!NOTE]  
    >  CmRcViewer.exe admite las siguientes opciones de línea de comandos:  
    >   
    >  -   *<Dirección\>*: especifica el nombre NetBIOS, el nombre de dominio completo (FQDN) o la dirección IP del equipo cliente que al que quiere conectarse.  
    > -   *<Nombre de servidor de sitio\>*: especifica el nombre del servidor de sitio de System Center 2012 Configuration Manager al que quiere enviar mensajes de estado relacionados con la sesión de control remoto.  
    > -   **/?** - Muestra las opciones de línea de comandos para el visor de control remoto.  
    >   
    >  **Ejemplo: CmRcViewer.exe** *<Dirección\>* *<\\\Nombre de servidor de sitio>*  



<!--HONumber=Nov16_HO1-->


