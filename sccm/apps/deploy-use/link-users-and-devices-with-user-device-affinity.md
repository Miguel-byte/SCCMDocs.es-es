---
title: Vincular usuarios y dispositivos con afinidad entre usuario y dispositivo | System Center Configuration Manager
description: "Vincule usuarios y dispositivos con afinidad entre usuario y dispositivo e implemente aplicaciones automáticamente en todos los dispositivos asociados a un usuario."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5b30b0d5-722d-4d4b-9ed7-5a43de315461
caps.latest.revision: 7
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: bb918eb5f7a69cad47de761a3e95e92926524e3a


---
# <a name="link-users-and-devices-with-user-device-affinity-in-system-center-configuration-manager"></a>Vincular usuarios y dispositivos con afinidad entre usuario y dispositivo en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

La afinidad entre usuario y dispositivo en System Center Configuration Manager asocia un usuario a uno o varios dispositivos. Puede que no sea necesario conocer los nombres de los dispositivos de un usuario a fin de implementar una aplicación para ese usuario. En lugar de implementar la aplicación en cada dispositivo del usuario, se implementa la aplicación en el usuario. A continuación, la afinidad entre usuario y dispositivo garantiza automáticamente que la aplicación se instale en todos los dispositivos asociados a ese usuario.  

 Puede definir dispositivos primarios que suelen ser los dispositivos que los usuarios usan a diario para realizar su trabajo. Al crear una afinidad entre un usuario y un dispositivo, obtendrá más opciones de implementación de aplicaciones. Por ejemplo, si un usuario requiere Microsoft Office Visio, puede instalarlo en el dispositivo primario del usuario mediante una implementación de Windows Installer. Sin embargo, en un dispositivo que no es un dispositivo primario, puede implementar Microsoft Office Visio como una aplicación virtual. También puede usar la afinidad entre usuario y dispositivo para preimplementar software en un dispositivo de usuario cuando no ha iniciado sesión, así cuando el usuario inicia sesión, la aplicación ya está instalada y lista para ejecutarse.  

 Debe administrar la información sobre afinidad de dispositivo de usuario para equipos. Configuration Manager administra automáticamente las afinidades de dispositivo del usuario para los dispositivos móviles que inscribe.  

## <a name="manually-configure-user-device-affinity"></a>Configurar manualmente la afinidad entre usuario y dispositivo  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad** > **Dispositivos**.  

3.  Seleccione un dispositivo de la lista. A continuación, en la pestaña **Inicio** , en el grupo **Dispositivos** , haga clic en **Editar usuarios primarios**.  

4.  En el cuadro de diálogo **Editar usuarios primarios** , busque y seleccione los usuarios que desea agregar como usuarios primarios para el dispositivo seleccionado y, a continuación, haga clic en **Agregar**.  

    > [!NOTE]  
    >  La lista **Usuarios primarios** muestra los usuarios que ya son usuarios primarios de este dispositivo y el método por el que se asignó cada relación entre usuario y dispositivo.  

## <a name="configure-primary-devices-for-a-user"></a>Configuración de los dispositivos primarios de un usuario  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad** > **Usuarios**.  

3.  Seleccione un usuario de la lista. A continuación, en la pestaña **Dispositivo** , haga clic **Editar dispositivos primarios**.  

4.  En el cuadro de diálogo **Editar dispositivos primarios** , busque y seleccione los dispositivos que desea agregar como dispositivos primarios para el usuario seleccionado y, a continuación, haga clic en **Agregar**.  

    > [!NOTE]  
    >  La lista **Dispositivos primarios** muestra los dispositivos que ya están configurados como dispositivos primarios para este usuario y el método por el que se asignó cada relación entre usuario y dispositivo.  

## <a name="automatically-create-user-device-affinities-windows-pcs-only"></a>Crear automáticamente afinidades entre usuario y dispositivo (solo en PC con Windows)  
 Configuration Manager lee en el registro de eventos de Windows los datos sobre los inicios de sesión de usuario. Para poder crear automáticamente afinidades de dispositivo del usuario, debe habilitar las dos configuraciones siguientes desde la directiva de seguridad local en los equipos cliente para almacenar los eventos de inicio de sesión en el registro de eventos de Windows.  

-   **Auditar eventos de inicio de sesión de cuenta**  

-   **Auditar eventos de inicio de sesión**  

 Puede usar la directiva de grupo de Windows para configurar estas opciones.  

> [!IMPORTANT]  
>  Si un error hace que el registro de eventos de Windows genere un gran número de entradas, esto puede ocasionar que se cree un nuevo registro de eventos. Si esto ocurre, podría ser que los eventos de inicio de sesión existentes ya no estén disponibles en Configuration Manager.  
>   
>  Preste especial atención cuando implemente **Auditar sucesos de inicio de sesión de cuenta** y **Auditar sucesos de inicio de sesión** en Windows XP. De forma predeterminada la directiva de retención es de 7 días, y es muy probable que estos eventos llenen el registro de eventos de seguridad. Los usuarios estándar no podrán iniciar sesión si el registro de eventos está lleno. Para evitar este problema, configure también la directiva **Método de retención** para el registro de seguridad en **Sobrescribir eventos cuando sea necesario**. Para permitir suficientes datos para la afinidad de dispositivo de usuario, también debe establecer la directiva Tamaño máximo del registro de seguridad en un valor razonable, entre 5 y 20 MB.  

### <a name="configure-the-site-to-automatically-create-user-device-affinities"></a>Configuración del sitio para crear automáticamente afinidades entre usuario y dispositivo  

1.  En la consola de Configuration Manager, haga clic en **Administración** > **Configuración de cliente**.  

3.  Para modificar la configuración de cliente predeterminada, seleccione **Configuración de cliente predeterminada**y, a continuación, en la pestaña **Inicio** , en el grupo **Propiedades** , haga clic en **Propiedades**. Para crear una configuración de agente de cliente personalizada, seleccione el nodo **Configuración de cliente** y, a continuación, en la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear configuración de dispositivo de cliente personalizada**.  

    > [!NOTE]  
    >  Si modifica la configuración de cliente predeterminada, se implementará en todos los equipos de la jerarquía. Para obtener más información acerca de cómo configurar las opciones de cliente, consulte [How to configure client settings in System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md) (Configuración del cliente en System Center Configuration Manager).  

4.  Para la configuración de cliente **Afinidad entre usuario y dispositivo**, configure las siguientes opciones:  

    -   **Umbral de uso de afinidad de dispositivo de usuario (minutos)** : especifique la cantidad de minutos de uso antes de que se cree una afinidad de dispositivo de usuario.  

    -   **Umbral de uso de afinidad de dispositivo de usuario (días)** : especifique la cantidad de días durante la cual se mide el umbral de afinidad basado en el uso.  

    -   **Configurar automáticamente la afinidad de dispositivo de usuario desde los datos del usuario** : de la lista desplegable, seleccione **Verdadero** para permitir que el sitio cree automáticamente afinidades de dispositivo del usuario. Si selecciona **Falso**, debe aprobar todas las asignaciones de afinidad entre usuario y dispositivo.  

    > [!TIP]  
    >  **Ejemplo:** si el **Umbral de uso de afinidad de dispositivo de usuario (minutos)** se configura como **60** minutos y **Umbral de uso de afinidad de dispositivo de usuario (días)** se configura como **5** días, el usuario debe usar el dispositivo durante, al menos, 60 minutos en un período de 5 días para que se cree automáticamente una afinidad entre usuario y dispositivo.  
   
Una vez creada una afinidad entre usuario y dispositivo, Configuration Manager continúa supervisando los umbrales de afinidad entre dispositivo y usuario. Si la actividad de usuario para el dispositivo cae por debajo de los umbrales configurados, entonces, se quitará la afinidad de dispositivo de usuario. Configure **Umbral de uso de afinidad de dispositivo de usuario (días)** en un valor de, al menos, **7** días para evitar situaciones en las que una afinidad de dispositivo de usuario configurada automáticamente pueda perderse mientras el usuario no haya iniciado sesión, por ejemplo, durante un fin de semana.  

## <a name="import-user-device-affinities-from-a-file"></a>Importar afinidades entre usuario y dispositivo desde un archivo  
 Puede importar un archivo que contiene las afinidades de dispositivo del usuario para poder crear muchas relaciones a la vez. Para este procedimiento, es necesario que los dispositivos se hayan detectado y existan como recursos en la base de datos de Configuration Manager. De lo contrario, este procedimiento no podrá realizarse.  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad** > **Usuarios** o **Dispositivos**.  

3.  En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Importar afinidad de dispositivo de usuario**.  

4.  En la página **Elegir asignación** del **Asistente para importar afinidad de dispositivo de usuario**, especifique la siguiente información:  

    -   **Nombre de archivo** : especifique un archivo de valores separados por comas (.csv) que contenga una lista de usuarios y dispositivos entre los que desea crear una afinidad. En este archivo, cada par de usuario y dispositivo debe encontrarse en una línea independiente, separada por una coma. Use el formato *<dominio>\>\\<nombre de usuario\>*,*<nombre de NetBIOS del dispositivo\>*.  

    -   **Este archivo tiene encabezados de columna como referencia** : si el archivo de valores separados por comas tiene una línea de encabezado superior, seleccione esta opción y la línea de encabezado se omitirá durante la importación.  

5.  Si el archivo que está importando contiene más de dos elementos en cada línea, puede usar **Columna** y **Asignar** para especificar qué columnas representan usuarios y dispositivos y qué columnas deben omitirse durante la importación.  

6.  Haga clic en **Siguiente** y, a continuación, complete la **Asistente para importar afinidad de dispositivo de usuario**.  

## <a name="let-end-users-create-a-user-device-affinity"></a>Permiso para que los usuarios finales creen una afinidad entre usuario y dispositivo  
 Use estos procedimientos para permitir que los usuarios creen su propia afinidad entre usuario y dispositivo desde el Centro de software.  

### <a name="configure-the-site-to-allow-user-created-user-device-affinity-requests"></a>Configuración del sitio para permitir solicitudes creadas por el usuario de afinidades entre usuario y dispositivo  

1.  En la consola de Configuration Manager, haga clic en **Administración** > **Configuración de cliente**.  

3.  Para modificar la configuración de cliente predeterminada, seleccione **Configuración de cliente predeterminada**y, a continuación, en la pestaña **Inicio** , en el grupo **Propiedades** , haga clic en **Propiedades**. Para crear una configuración de agente de cliente personalizada, seleccione el nodo **Configuración de cliente** y, a continuación, en la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear configuración de cliente personalizada para usuarios**.  

    > [!NOTE]  
    >  Si modifica la configuración de cliente predeterminada, se implementará en todos los equipos de la jerarquía. Para obtener información sobre la configuración de cliente, consulte [How to configure client settings](../../core/clients/deploy/configure-client-settings.md) (Configuración de las opciones de cliente).  

4.  Seleccione **Afinidad entre usuario y dispositivo** de la configuración de cliente y, a continuación, en la lista desplegable **Permitir al usuario definir sus dispositivos primarios** , seleccione **Verdadero**.  

### <a name="configure-a-user-device-affinity"></a>Configuración de una afinidad de dispositivo de usuario  

1.  En el Catálogo de aplicaciones, haga clic en **Mis sistemas**.  

2.  Habilite la opción **Normalmente uso este equipo para realizar mi trabajo**.  

## <a name="manage-user-device-affinity-requests-from-users"></a>Administrar solicitudes de usuarios de afinidad entre usuario y dispositivo  
 Cuando la configuración de cliente **Configurar automáticamente la afinidad de dispositivo de usuario desde los datos del usuario** está establecida en **Falso**, debe aprobar todas las asignaciones de afinidad entre usuario y dispositivo.  

### <a name="approve-or-reject-a-user-device-affinity-request"></a>Aprobación o rechazo de una solicitud de afinidad entre usuario y dispositivo  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad**.  

2.  En el área de trabajo **Activos y compatibilidad** , seleccione la recopilación de usuarios o dispositivos para la que desea administrar solicitudes de afinidad.  

3.  En la pestaña **Inicio** , en el grupo **Recopilación** , haga clic en **Administrar solicitudes de afinidad**.  

4.  En el cuadro de diálogo **Administrar solicitudes de afinidad de dispositivo de usuario** , seleccione una solicitud de afinidad y, a continuación, haga clic en **Aprobar** o **Rechazar**.  



<!--HONumber=Nov16_HO1-->


