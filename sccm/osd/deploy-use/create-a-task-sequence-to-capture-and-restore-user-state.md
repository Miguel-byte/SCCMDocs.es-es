---
title: Crear una secuencia de tareas para capturar y restaurar el estado de usuario | Microsoft Docs
description: "Use secuencias de tareas de System Center Configuration Manager para capturar y restaurar los datos de estado de usuario en escenarios de implementación de sistema operativo."
ms.custom: na
ms.date: 06/07/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d566d85c-bf7a-40e7-8239-57640a1db5f4
caps.latest.revision: "7"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 3a8e2759812dae2a328cd09efdc13f8534d14379
ms.sourcegitcommit: 31c670a4bce74fd64a7d46ebf7702f65b80d4147
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/13/2017
---
# <a name="create-a-task-sequence-to-capture-and-restore-user-state-in-system-center-configuration-manager"></a>Crear una secuencia de tareas para capturar y restaurar el estado de usuario en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Puede usar secuencias de tareas de System Center Configuration Manager para capturar y restaurar los datos de estado de usuario en los escenarios de implementación de sistema operativo donde quiere conservar el estado de usuario del sistema operativo actual. Según el tipo de tarea de secuencia de tareas que cree, las etapas de captura y restauración podrían agregarse automáticamente como parte de la secuencia de tareas. En otros escenarios, es posible que deba agregar manualmente las etapas de captura y restauración a la secuencia de tareas. En este tema se indican las etapas que se deben agregar a una secuencia de tareas existente para capturar y restaurar los datos de estado de usuario.  

##  <a name="BKMK_CaptureRestoreUserState"></a> Cómo capturar y restaurar los datos de estado de usuario  
 Para capturar y restaurar el estado del usuario, debe agregar las etapas siguientes a la secuencia de tareas:  

-   **Solicitar almacén de estado**: este paso solo es necesario en caso de que se almacene el estado de usuario en el punto de migración de estado.  

-   **Capturar estado de usuario**: este paso permite capturar los datos del estado de usuario y almacenarlos en el punto de migración de estado o localmente con el uso de vínculos.  

-   **Restaurar estado de usuario**: este paso permite restaurar los datos del estado de usuario en el equipo de destino. Puede recuperar los datos desde un punto de migración de estado de usuario o desde el equipo de destino.  

-   **Liberar almacén de estado**: este paso solo es necesario en caso de que se almacene el estado de usuario en el punto de migración de estado. Este paso quita estos datos del punto de migración de estado.  

 Utilice los procedimientos siguientes para agregar los pasos de la secuencia de tareas necesarios para capturar el estado de usuario y restaurar el estado de usuario. Para más información sobre la creación de secuencias de tareas, vea [Manage task sequences to automate tasks (Administrar secuencias de tareas para automatizar tareas)](manage-task-sequences-to-automate-tasks.md).  

#### <a name="to-add-task-sequence-steps-to-capture-the-user-state"></a>Para agregar pasos a una secuencia de tareas para capturar el estado de usuario  

1.  En la lista **Secuencias de tareas** , seleccione una secuencia de tareas y, a continuación, haga clic en **Editar**.  

2.  Si utiliza un punto de migración de estado para almacenar el estado de usuario, agregue el paso **Liberar almacén de estado** a la secuencia de tareas. En el cuadro de diálogo **Editor de secuencia de tareas** , haga clic en **Agregar**, seleccione **Estado de usuario**y, a continuación, haga clic en **Solicitar almacén de estado**. Especifique las siguientes propiedades y opciones para el paso **Solicitar almacén de estados** y, a continuación, haga clic en **Aplicar**.  

     En la pestaña **Propiedades** , especifique las opciones siguientes:  

    -   Escriba un nombre y una descripción para el paso.  

    -   Haga clic en **Capturar estado del equipo**.  

    -   En el cuadro **Número de reintentos** , especifique la cantidad de veces que la secuencia de tareas intenta capturar los datos de estado de usuario si ocurre un error.  

    -   En el cuadro **Intervalo entre reintentos (en segundos)** , especifique cuántos segundos debe esperar la secuencia de tareas antes de reintentar capturar los datos.  

    -   Active la casilla **Si una cuenta de equipo no se puede conectar al almacén de estado, usar la cuenta de acceso de red** para especificar si se usa la [cuenta de acceso de red](../../core/plan-design/hierarchy/manage-accounts-to-access-content.md#bkmk_NAA) de Configuration Manager para conectarse al almacén de estado.  

     En la pestaña **Opciones** , especifique las opciones siguientes:  

    -   Active la casilla **Continuar después de un error** si desea que la secuencia de tareas continúe con el paso siguiente si se produce un error en este paso.  

    -   Especifique las condiciones que deben cumplirse para que la secuencia de tareas pueda continuar si se produce un error.  

3.  Agregue el paso **Capturar estado de usuario** a la secuencia de tareas. En el cuadro de diálogo **Editor de secuencia de tareas** , haga clic en **Agregar**, seleccione **Estado de usuario**y, a continuación, haga clic en **Capturar estado de usuario**. Especifique las siguientes propiedades y opciones para el paso **Capturar estado de usuario** y, a continuación, haga clic en **Aceptar**.  

    > [!IMPORTANT]  
    >  Cuando se agrega este paso a la secuencia de tareas, también debe establecerse la variable de secuencia de tareas **OSDStateStorePath** para especificar dónde se almacenan los datos de estado de usuario. Si almacena el estado de usuario localmente, no especifique una carpeta raíz, dado que eso puede provocar un error en la secuencia de tareas. Siempre que almacene los datos de usuario localmente, utilice una carpeta o subcarpeta. Para más información sobre esta variable, vea [Capture User State Task Sequence Action Variables (Variables de acción de la secuencia de tareas Capturar estado de usuario)](../understand/task-sequence-action-variables.md#BKMK_CaptureUserState).  

     En la pestaña **Propiedades** , especifique las opciones siguientes:  

    -   Escriba un nombre y una descripción para el paso.  

    -   Especifique el paquete que contiene el archivo de origen USMT utilizado para capturar los datos de estado de usuario.  

    -   Especifique los perfiles de usuario para capturar:  

        -   Haga clic en **Capturar todos los perfiles de usuario mediante opciones estándar** para capturar todos los perfiles de usuario.  

        -   Haga clic en **Personalizar la captura de perfiles de usuario** para especificar los perfiles de usuario individuales para capturar. Seleccione el archivo de configuración (miguser.xml, migsys.xml o migapp.xml) que contiene la información de perfil de usuario. No puede usar el archivo de configuración config.xml en este caso, pero puede agregarlo manualmente a la línea de comandos de USMT mediante las variables OSDMigrageAdditionalCaptureOptions y OSDMigrateAdditionalRestoreOptions.

    -   Seleccione **Habilitar el registro detallado** para especificar la cantidad de información que se escribirá en los archivos de registro si se produce un error.  

    -   Seleccione **Omitir archivos que usan el Sistema de cifrado de archivos (EFS)**.  

    -   Seleccione **Copiar mediante el acceso al sistema de archivos** para especificar la configuración siguiente:  

        -   **Continuar si algunos archivos no se pueden capturar**: esta opción de configuración permite al paso de la secuencia de tareas continuar con el proceso de migración incluso en el caso de que algunos archivos no se puedan capturar. Si deshabilita esta opción y no se puede capturar un archivo, se produce un error en el paso de la secuencia de tareas. Esta opción está habilitada de forma predeterminada.  

        -   **Capturar localmente mediante vínculos en vez de mediante la copia de archivos**: esta opción de configuración permite usar la característica de migración de vínculo físico disponible en USMT 4.0. Este valor se omite si se utilizan versiones de USMT anteriores a USMT 4.0.  

        -   **Capturar en modo fuera de línea (solo Windows PE)**: esta opción de configuración permite capturar el estado de usuario de Windows PE sin iniciar el sistema operativo existente. Este valor se omite si se utilizan versiones de USMT anteriores a USMT 4.0.  

    -   Seleccione **Capturar mediante el Servicio de instantánea de copia de volumen (VSS)**. Este valor se omite si se utilizan versiones de USMT anteriores a USMT 4.0.  

     En la pestaña **Opciones** , especifique las opciones siguientes:  

    -   Active la casilla **Continuar después de un error** si desea que la secuencia de tareas continúe con el paso siguiente si se produce un error en este paso.  

    -   Especifique las condiciones que deben cumplirse para que la secuencia de tareas pueda continuar si se produce un error.  

4.  Si usa un punto de migración de estado para almacenar el estado de usuario, agregue el paso [Liberar almacén de estado](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore) a la secuencia de tareas. En el cuadro de diálogo **Editor de secuencia de tareas** , haga clic en **Agregar**, seleccione **Estado de usuario**y, a continuación, haga clic en **Liberar almacén de estado**. Especifique las propiedades y las opciones siguientes del paso **Liberar almacén de estado** y, a continuación, haga clic en **Aceptar**.  

    > [!IMPORTANT]  
    >  La acción de la secuencia de tareas que se ejecuta antes del paso **Liberar almacén de estado** debe finalizar correctamente para que se inicie el paso **Liberar almacén de estado** .  

     En la pestaña **Propiedades** , escriba un nombre y una descripción para el paso.  

     En la pestaña **Opciones** , especifique las opciones siguientes.  

    -   Active la casilla **Continuar después de un error** si desea que la secuencia de tareas continúe con el paso siguiente si se produce un error en este paso.  

    -   Especifique las condiciones que deben cumplirse para que la secuencia de tareas pueda continuar si se produce un error.  

 Implemente esta secuencia de tareas para capturar el estado de usuario en un equipo de destino. Para más información sobre cómo implementar secuencias de tareas, vea [Deploy a task sequence (Implementar una secuencia de tareas)](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS).  

#### <a name="to-add-task-sequence-steps-to-restore-the-user-state"></a>Para agregar pasos de secuencia de tareas para restaurar el estado de usuario  

1.  En la lista **Secuencias de tareas** , seleccione una secuencia de tareas y, a continuación, haga clic en **Editar**.  

2.  Agregue el paso [Restaurar estado de usuario](../understand/task-sequence-steps.md#BKMK_RestoreUserState) a la secuencia de tareas. En el cuadro de diálogo **Editor de secuencia de tareas** , haga clic en **Agregar**, seleccione **Estado de usuario**y, a continuación, haga clic en **Restaurar estado de usuario**. Este paso establece una conexión con el punto de migración de estado. Especifique las propiedades y las opciones siguientes del paso **Restaurar estado de usuario** y, a continuación, haga clic en **Aceptar**.  

     En la pestaña **Propiedades** , especifique las siguientes propiedades:  

    -   Escriba un nombre y una descripción para el paso.  

    -   Especifique el paquete que contiene la herramienta USMT para restaurar los datos de estado de usuario.  

    -   Especifique los perfiles de usuario que desea restaurar:  

        -   Haga clic en **Restaurar todos los perfiles de usuario capturados con opciones estándar** para restaurar todos los perfiles de usuario.  

        -   Haga clic en **Customize user profile restore** (Personalizar la restauración de perfiles de usuario) para restaurar los perfiles de usuario individuales. Seleccione el archivo de configuración (miguser.xml, migsys.xml o migapp.xml) que contiene la información de perfil de usuario. No puede usar el archivo de configuración config.xml en este caso, pero puede agregarlo manualmente a la línea de comandos de USMT mediante las variables OSDMigrageAdditionalCaptureOptions y OSDMigrateAdditionalRestoreOptions.

    -   Seleccione **Restaurar perfiles de usuario de equipo local** para proporcionar una nueva contraseña para los perfiles restaurados. No se pueden migrar las contraseñas de perfiles locales.  

        > [!NOTE]  
        >  Si tiene cuentas de usuario local, usa la etapa [Capturar estado de usuario](../understand/task-sequence-steps.md#BKMK_CaptureUserState) y selecciona **Restaurar todos los perfiles de usuario capturados con opciones estándar**, debe seleccionar la opción **Restaurar perfiles de usuario de equipo local** en el paso [Restaurar estado de usuario](../understand/task-sequence-steps.md#BKMK_RestoreUserState) o se producirá un error en la secuencia de tareas.  

    -   Seleccione **Continuar si algunos archivos no se pueden restaurar** si desea que el paso **Restaurar estado de usuario** continúe si un archivo no se puede restaurar.  

         Si almacena el estado de usuario mediante vínculos locales y la restauración no finaliza correctamente, el usuario administrativo puede eliminar manualmente los vínculos físicos que se crearon para almacenar los datos o la secuencia de tareas puede ejecutar la herramienta USMTUtils. Si se usa USMTUtils para eliminar el vínculo físico, agregue un paso [Reiniciar equipo](../understand/task-sequence-steps.md#BKMK_RestartComputer) después de ejecutar USMTUtils.  

    -   Seleccione **Habilitar el registro detallado** para especificar la cantidad de información que se escribirá en los archivos de registro si se produce un error.  

     En la pestaña **Opciones** , especifique las opciones siguientes:  

    -   Active la casilla **Continuar después de un error** si desea que la secuencia de tareas continúe con el paso siguiente si se produce un error en este paso.  

    -   Especifique las condiciones que deben cumplirse para que la secuencia de tareas pueda continuar si se produce un error.  

3.  Si usa un punto de migración de estado para almacenar el estado de usuario, agregue el paso [Liberar almacén de estado](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore) a la secuencia de tareas. En el cuadro de diálogo **Editor de secuencia de tareas** , haga clic en **Agregar**, seleccione **Estado de usuario**y, a continuación, haga clic en **Liberar almacén de estado**. Especifique las propiedades y las opciones siguientes del paso **Liberar almacén de estado** y, a continuación, haga clic en **Aceptar**.  

    > [!IMPORTANT]  
    >  La acción de la secuencia de tareas que se ejecuta antes del paso **Liberar almacén de estado** debe finalizar correctamente para que se inicie el paso **Liberar almacén de estado** .  

     En la pestaña **Propiedades** , escriba un nombre y una descripción para el paso.  

     En la pestaña **Opciones** , especifique las opciones siguientes.  

    -   Active la casilla **Continuar después de un error** si desea que la secuencia de tareas continúe con el paso siguiente si se produce un error en este paso.  

    -   Especifique las condiciones que deben cumplirse para que la secuencia de tareas pueda continuar si se produce un error.  

 Implemente esta secuencia de tareas para restaurar el estado de usuario en un equipo de destino. Para más información sobre la implementación de secuencias de tareas, vea [Deploy a task sequence (Implementar una secuencia de tareas)](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS).  

## <a name="next-steps"></a>Pasos siguientes
[Supervisar la implementación de la secuencia de tareas](monitor-operating-system-deployments.md#BKMK_TSDeployStatus)
