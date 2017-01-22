---
title: "Crear elementos de configuración de perfiles y datos de usuario | Microsoft Docs"
description: "Use elementos de configuración de perfiles y datos en System Center Configuration Manager para administrar el redireccionamiento de carpetas, archivos sin conexión y perfiles móviles."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9fcbcc81-cd6f-496e-b075-ef1afa2b8ccc
caps.latest.revision: 6
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: f9e939d871e95a3248d8e5d96cb73063a81fd5cf
ms.openlocfilehash: 85b984d739dc9f9d2046186b381eff54ba687c66


---

# <a name="create-user-data-and-profiles-configuration-items-in-system-center-configuration-manager"></a>Crear elementos de configuración de perfiles y datos de usuario en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Los elementos de configuración de perfiles y datos de usuario de System Center Configuration Manager contienen opciones que pueden administrar el redireccionamiento de carpetas, los archivos sin conexión y los perfiles móviles en equipos que ejecutan Windows 8 y versiones posteriores para los usuarios de la jerarquía. Por ejemplo, puede:  

-   Redirigir la carpeta de documentos de un usuario a un recurso compartido de red.  

-   Garantizar que los archivos especificados que se almacenen en la red estén disponibles en el equipo del usuario cuando la conexión de red no lo esté.  

-   Configurar qué archivos de un perfil de usuario móvil se sincronizan con un recurso compartido de red cuando el usuario inicia y cierra sesión.  

 A diferencia de otros elementos de configuración de Configuration Manager, no se agregan elementos de configuración de perfiles y datos de usuario a una línea base de configuración que se implementa posteriormente. En su lugar, se implementa el elemento de configuración directamente mediante el cuadro de diálogo **Implementar elemento de configuración de perfiles y datos de usuario** .  

> [!IMPORTANT]  
>  Solo se pueden implementar elementos de configuración de perfiles y datos de usuario en recopilaciones de usuarios.  

## <a name="enable-user-data-and-profiles-for-compliance-settings"></a>Habilitar perfiles y datos de usuario para la configuración de cumplimiento  
 Use el procedimiento siguiente para definir la configuración de cliente predeterminada para la configuración de cumplimiento de perfiles y datos de usuario que se aplicará a todos los equipos de la jerarquía. Si quiere que esta configuración solo se aplique a algunos equipos, cree una configuración de cliente de dispositivo personalizada y asígnela a una recopilación que contenga los equipos en los que quiere usar la configuración de cumplimiento de perfiles y datos de usuario. Para obtener más información sobre cómo crear configuraciones de dispositivo personalizadas, consulte [How to configure client settings](../../core/clients/deploy/configure-client-settings.md) (Cómo establecer la configuración de cliente).  

1.  En la consola de Configuration Manager, haga clic en **Administración** > **Configuración de cliente** > **Configuración predeterminada**.  

4.  En la pestaña **Inicio** , en el grupo **Propiedades** , haga clic en **Propiedades**.  

5.  En el cuadro de diálogo **Configuración predeterminada** , haga clic en **Configuración de cumplimiento**.  

6.  En la lista desplegable **Habilitar perfiles y datos de usuario** , seleccione **Sí**.  

7.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Configuración predeterminada** .  

## <a name="create-a-user-data-and-profiles-configuration-item"></a>Crear un elemento de configuración de perfiles y datos de usuario  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad** > **Configuración de cumplimiento** > **Perfiles y datos de usuario**.  

3.  En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear elemento de configuración de perfiles y datos de usuario**.  

4.  En la página **General** del **Asistente para crear elemento de configuración de perfiles y datos de usuario**, especifique la siguiente información:  

    -   **Nombre:** escriba un nombre único para el elemento de configuración. Puede utilizar un máximo de 256 caracteres.  

    -   **Descripción:** Proporcione una descripción general de los elementos de configuración y otra información relevante que le permita para identificarlo en la consola de Configuration Manager. Puede utilizar un máximo de 256 caracteres.  

    -   **Redirección de carpetas:** seleccione esta casilla si quiere configurar el redireccionamiento de carpetas de este elemento de configuración.  

    -   **Archivos sin conexión:** seleccione esta casilla si quiere configurar los archivos sin conexión de este elemento de configuración.  

    -   **Perfiles de usuario móvil:** seleccione esta casilla si quiere configurar los perfiles de usuario móvil de este elemento de configuración.  

5.  En la página **Redirección de carpetas** del **Asistente para crear elemento de configuración de perfiles y datos de usuario**, especifique cómo quiere que los equipos cliente de los usuarios que reciben este elemento de configuración administren la redirección de carpetas. Puede configurar los ajustes de cualquier dispositivo en el que el usuario inicie sesión o solo los dispositivos primarios del usuario. Para más información sobre la redirección de carpetas, consulte la documentación de Windows Server.  

    > [!NOTE]  
    >  Esta página solo aparece si seleccionó **Redirección de carpetas** en la página **General** del asistente.  

6.  En la página **Archivos sin conexión** del **Asistente para crear elemento de configuración de perfiles y datos de usuario**, puede habilitar o deshabilitar el uso de archivos sin conexión de los usuarios que reciben este elemento de configuración y establecer los ajustes del comportamiento de los archivos sin conexión. También puede especificar los archivos sin conexión que siempre estarán disponibles en cualquier equipo en el que el usuario inicie sesión. Para más información sobre los archivos sin conexión, consulte la documentación de Windows Server.  

    > [!NOTE]  
    >  Esta página solo aparece si activó la casilla **Archivos sin conexión** en la página **General** del asistente.  

7.  En la página **Perfiles móviles** del **Asistente para crear elemento de configuración de perfiles y datos de usuario**, puede configurar si los perfiles móviles deben estar disponibles en equipos en los que el usuario inicie sesión y también configurar más información sobre el comportamiento de estos perfiles. Para más información sobre los perfiles móviles, consulte la documentación de Windows Server.  

    > [!NOTE]  
    >  Esta página solo aparece si activó la casilla **Perfiles de usuario móvil** en la página **General** del asistente.  

8.  Complete el asistente.  

 El nuevo elemento de configuración de perfiles y datos de usuario se muestra en el nodo **Perfiles y datos de usuario** del área de trabajo **Activos y compatibilidad** .  

## <a name="deploy-a-user-data-and-profiles-configuration-item"></a>Implementar un elemento de configuración de perfiles y datos de usuario  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad** > **Configuración de cumplimiento** > **Perfiles y datos de usuario**.  

3.  Seleccione el elemento de configuración de perfiles y datos de usuario que quiere implementar y luego, en la pestaña **Inicio** , en el grupo **Implementación** , haga clic en **Implementar**.  

4.  En el cuadro de diálogo **Implementar elemento de configuración de perfiles y datos de usuario** , especifique la siguiente información.  

    -   **Recopilación** : haga clic en **Examinar** para seleccionar la recopilación de usuarios en la que quiere implementar el elemento de configuración.  

        > [!IMPORTANT]  
        >  Solo se pueden implementar elementos de configuración de perfiles y datos de usuario en recopilaciones de usuarios.  

    -   **Corregir las reglas no compatibles cuando se admita** : habilite esta opción para corregir automáticamente las reglas que se evalúen como no compatibles en los equipos cliente.  

    -   **Permitir la corrección fuera de la ventana de mantenimiento** : si se ha configurado una ventana de mantenimiento para la recopilación en la que se va a implementar el elemento de configuración, habilite esta opción para permitir que la configuración de cumplimiento corrija el valor fuera de la ventana de mantenimiento. Para obtener más información sobre las ventanas de mantenimiento, consulte [How to use maintenance windows](../../core/clients/manage/collections/use-maintenance-windows.md) (Cómo usar las ventanas de mantenimiento).  

    -   **Generar una alerta** : habilite esta opción para configurar una alerta que se genere si la compatibilidad del elemento de configuración es inferior a un determinado porcentaje en una hora y fecha especificadas. También puede especificar si desea que se envíe una alerta a System Center Operations Manager.  

    -   **Especifique la programación de evaluación de cumplimiento para este elemento de configuración** : especifica la programación por la que se evalúa el elemento de configuración implementado en los equipos cliente. Puede ser una programación simple o personalizada.  

5.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Implementar elemento de configuración de perfiles y datos de usuario** y crear la implementación.  

## <a name="monitor-a-user-data-and-profiles-configuration-item"></a>Supervisar un elemento de configuración de perfiles y datos de usuario  
 Supervise este tipo de elemento de configuración de la misma manera que supervisa otras configuraciones de cumplimiento.  

 Para obtener más información, consulte [How to monitor compliance settings](../../compliance/deploy-use/monitor-compliance-settings.md) (Cómo supervisar la configuración de cumplimiento).  



<!--HONumber=Dec16_HO3-->


