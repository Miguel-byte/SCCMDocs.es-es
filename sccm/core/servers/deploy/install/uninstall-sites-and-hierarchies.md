---
title: Desinstalar sitios | Microsoft Docs
description: "Use estos detalles como guía cuando deba desinstalar un sitio de System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d466edd2-97f0-44c1-a73e-d71abbdbf4a8
caps.latest.revision: 6
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: f41e70c98c4b2ede575debb868978afa3dad1abc


---
# <a name="uninstall-sites-and-hierarchies-in-system-center-configuration-manager"></a>Desinstalar sitios y jerarquías en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Use la siguiente información como guía cuando deba desinstalar sitios de System Center Configuration Manager.  

Para quitar una jerarquía con varios sitios, la secuencia de eliminación es importante:  

-   Inicie la desinstalación de los sitios en la parte inferior de la jerarquía y luego continúe hacia arriba.  

-   Elimine primero los sitios secundarios conectados a los sitios primarios  

-   Después, quite los sitios primarios  

-   Cuando haya quitado todos los sitios primarios, puede desinstalar el sitio de administración central.  


##  <a name="a-namebkmkremovesecondarysitea-remove-a-secondary-site-from-a-hierarchy"></a><a name="BKMK_RemoveSecondarysite"></a> Quitar un sitio secundario de una jerarquía  
No se pueden mover ni volver a asignar sitios secundarios a un nuevo sitio primario principal. Para quitar un sitio secundario de una jerarquía, debe eliminarse del sitio principal directo. Use el Asistente para eliminar sitios secundarios desde la consola de Configuration Manager para quitar el sitio secundario. Cuando se quita un sitio secundario, debe elegir si desea eliminar o desinstalar el sitio secundario:  

-   **Desinstalar el sitio secundario**: utilice esta opción para quitar un sitio secundario funcional que esté accesible desde la red. Esta opción desinstala Configuration Manager del servidor de sitio secundario y después elimina toda la información sobre el sitio y los recursos de la jerarquía de Configuration Manager. Si Configuration Manager ha instalado SQL Server Express como parte de la instalación del sitio secundario, Configuration Manager desinstalará SQL Express cuando desinstale el sitio secundario. Si SQL Server Express se ha instalado antes de instalar el sitio secundario, Configuration Manager no desinstalará SQL Server Express.  

-   **Eliminar el sitio secundario**: utilice esta opción si se cumple alguna de las condiciones siguientes.  

    -   No se ha podido instalar un sitio secundario.  

    -   El sitio secundario continuará mostrándose en la consola de Configuration Manager después de desinstalarlo.  

    Esta opción elimina toda la información sobre el sitio y los recursos de la jerarquía de Configuration Manager, pero mantiene Configuration Manager instalado en el servidor de sitio secundario.  

    > [!NOTE]  
    >  También puede utilizar la herramienta de mantenimiento de jerarquía y la opción **/DELSITE** para eliminar un sitio secundario. Para obtener más información, consulte [Herramienta de mantenimiento de jerarquía (Preinst.exe) para System Center Configuration Manager](../../../../core/servers/manage/hierarchy-maintenance-tool-preinst.exe.md).  

#### <a name="to-uninstall-or-delete-a-secondary-site"></a>Para desinstalar o eliminar un sitio secundario  

1.  Compruebe que el usuario administrativo que ejecuta el programa de instalación tenga los siguientes derechos de seguridad:  

    -   Derechos administrativos en el equipo del sitio secundario.  

    -   Derechos de administrador local en el servidor de base de datos del sitio primario, si es remoto.  

    -   Rol de seguridad Administrador total o Administrador de infraestructuras en el sitio primario principal.  

    -   Derechos de administrador del sistema en la base de datos de sitio secundario.  

2.  En la consola de Configuration Manager, haga clic en **Administración**.  

3.  En el área de trabajo **Administración** , expanda **Configuración del sitio**y, a continuación, haga clic en **Sitios**.  

4.  Seleccione el servidor de sitio secundario que desea quitar.  

5.  En la pestaña **Inicio** , en el grupo **Sitio** , haga clic en **Eliminar**.  

6.  En la página **General** , seleccione si desea desinstalar o eliminar el sitio secundario y, a continuación, haga clic en **Siguiente**.  

7.  En la página **Resumen** , compruebe la configuración y, a continuación, haga clic en **Siguiente**.  

8.  En la página **Finalización** , haga clic en **Cerrar** para salir del asistente.  

##  <a name="a-namebkmkuninstallprimarya-uninstall-a-primary-site"></a><a name="BKMK_UninstallPrimary"></a> Desinstalar un sitio primario  
Puede ejecutar el programa de instalación de Configuration Manager para desinstalar un sitio primario que no tiene un sitio secundario asociado. Antes de desinstalar un sitio primario, considere lo siguiente:  

-   Si los clientes de Configuration Manager están dentro de los límites configurados en el sitio y el sitio primario forma parte de una jerarquía de Configuration Manager, considere la opción de agregar los límites en un sitio primario diferente de la jerarquía antes de desinstalar el sitio primario.  

-   Cuando el servidor de sitio primario ya no está disponible, debe utilizar la herramienta de mantenimiento de jerarquía en el sitio de administración central para eliminar el sitio primario de la base de datos de sitio. Para obtener más información, consulte [Herramienta de mantenimiento de jerarquía (Preinst.exe) para System Center Configuration Manager](../../../../core/servers/manage/hierarchy-maintenance-tool-preinst.exe.md).  

Utilice el procedimiento siguiente para desinstalar un sitio primario.  

#### <a name="to-uninstall-a-primary-site"></a>Para desinstalar un sitio primario  

1.  Compruebe que el usuario administrativo que ejecuta el programa de instalación tenga los siguientes derechos de seguridad:  

    -   Derechos de administrador local en el servidor de sitio de administración central.  

    -   Derechos de administrador local en el servidor de base de datos del sitio de administración central, si es remoto.  

    -   Derechos de administrador del sistema en la base de datos de sitio del sitio de administración central.  

    -   Derechos de administrador local en el equipo del sitio primario.  

    -   Derechos de administrador local en el servidor de base de datos del sitio primario, si es remoto.  

    -   Nombre de usuario asociado con el rol de seguridad Administrador total o Administrador de infraestructuras en el sitio de administración central.  

2.  Inicie el programa de instalación de Configuration Manager en el servidor de sitio primario mediante uno de los métodos siguientes:  

    -   En **Inicio**, haga clic en **Programa de instalación de Configuration Manager**.  

    -   Abra Setup.exe en &lt;*Medios de instalación de Configuration Manager*>\SMSSETUP\BIN\X64.  

    -   Abra Setup.exe en &lt;*Ruta de instalación de Configuration Manager*>\BIN\X64.  

3.  En la página **Antes de empezar** , haga clic en **Siguiente**.  

4.  En la página **Introducción** , seleccione **Desinstalar un sitio de Configuration Manager**y, a continuación, haga clic en **Siguiente**.  

5.  En **Desinstalar el sitio de Configuration Manager**, especifique si quiere quitar la base de datos de sitio del servidor de sitio primario y si quiere quitar la consola de Configuration Manager. De forma predeterminada, el programa de instalación elimina ambos elementos.  

    > [!IMPORTANT]  
    >  Si un sitio secundario se adjunta al sitio primario, debe quitar el sitio secundario para desinstalar el sitio primario.  

6.  Haga clic en **Sí** para confirmar la desinstalación del sitio primario de Configuration Manager.  

##  <a name="a-namebkmkuninstallprimarydistviewsa-uninstall-a-primary-site-that-is-configured-with-distributed-views"></a><a name="BKMK_UninstallPrimaryDistViews"></a> Desinstalar un sitio primario configurado con vistas distribuidas  
 Antes de desinstalar un sitio primario secundario con vistas distribuidas configuradas en su vínculo de replicación del sitio de administración central, debe deshabilitar las vistas distribuidas en su jerarquía. Utilice la información siguiente para deshabilitar vistas distribuidas antes de desinstalar un sitio primario.  

#### <a name="to-uninstall-a-primary-site-that-is-configured-with-distributed-views"></a>Para desinstalar un sitio primario que está configurado con vistas distribuidas  

1.  Antes de desinstalar un sitio primario, debe deshabilitar las vistas distribuidas en cada vínculo en la jerarquía entre el sitio de administración central y el sitio primario.  

2.  Después de deshabilitar las vistas distribuidas en cada vínculo, confirme que los datos del sitio primario completan la reinicialización en el sitio de administración central. Puede supervisar la inicialización de los datos cuando visualiza el vínculo en el nodo **Replicación de base de datos** del área de trabajo **Supervisión** de la consola de Configuration Manager.  

3.  Después de reinicializar correctamente los datos con el sitio de administración central, puede desinstalar el sitio primario. Para desinstalar un sitio primario, consulte la sección [Desinstalar un sitio primario](#BKMK_UninstallPrimary) en este tema.  

4.  Después de desinstalar completamente el sitio primario, puede volver a configurar las vistas distribuidas en los vínculos a sitios primarios.  

    > [!IMPORTANT]  
    >  Si desinstala el sitio primario antes de deshabilitar las vistas distribuidas de cada sitio o antes de que los datos del sitio primario se reinicialicen correctamente en el sitio de administración central, es posible que se produzca un error en la replicación de datos entre los sitios primarios y el sitio de administración central. En este escenario, debe deshabilitar las vistas distribuidas para cada vínculo en la jerarquía y, a continuación, después de que los datos se reinicialicen correctamente en el sitio de administración central, pude reconfigurar las vistas distribuidas.  

##  <a name="a-namebkmkuninstallcasa-uninstall-the-central-administration-site"></a><a name="BKMK_UninstallCAS"></a> Desinstalar el sitio de administración central  
 Puede ejecutar el programa de instalación de Configuration Manager para desinstalar un sitio de administración central sin ningún sitio primario secundario. Utilice el procedimiento siguiente para desinstalar el sitio de administración central.  

#### <a name="to-uninstall-a-central-administration-site"></a>Para desinstalar un sitio de administración central  

1.  Compruebe que el usuario administrativo que ejecuta el programa de instalación tenga los siguientes derechos de seguridad:  

    -   Derechos de administrador local en el servidor de sitio de administración central.  

    -   Derechos de administrador local en el servidor de base de datos del sitio para el sitio de administración central, si el servidor de base de datos del sitio no está instalado en el servidor de sitio.  

2.  Inicie el programa de instalación de Configuration Manager en el servidor de sitio de administración central mediante uno de los métodos siguientes:  

    -   En **Inicio**, haga clic en **Programa de instalación de Configuration Manager**.  

    -   Abra Setup.exe en &lt;*Medios de instalación de Configuration Manager*>\SMSSETUP\BIN\X64.  

    -   Abra Setup.exe en &lt;*Ruta de instalación de Configuration Manager*>\BIN\X64.  

3.  En la página **Antes de empezar** , haga clic en **Siguiente**.  

4.  En la página **Introducción** , seleccione **Desinstalar un sitio de Configuration Manager**y, a continuación, haga clic en **Siguiente**.  

5.  En **Desinstalar el sitio de Configuration Manager**, especifique si quiere quitar la base de datos del sitio del servidor de sitio de administración central y si quiere quitar la consola de Configuration Manager. De forma predeterminada, el programa de instalación elimina ambos elementos.  

    > [!IMPORTANT]  
    >  Si un sitio primario se adjuntó al sitio de administración central, debe desinstalar el sitio primario para poder desinstalar el sitio de administración central.  

6.  Haga clic en **Sí** para confirmar la desinstalación del sitio de administración central de Configuration Manager.  



<!--HONumber=Dec16_HO3-->


