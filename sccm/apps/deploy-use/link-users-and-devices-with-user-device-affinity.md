---
title: Vincular usuarios y dispositivos con la afinidad entre usuario y dispositivo
titleSuffix: Configuration Manager
description: Vincule usuarios y dispositivos con afinidad entre usuario y dispositivo e implemente aplicaciones automáticamente en todos los dispositivos asociados a un usuario.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 5b30b0d5-722d-4d4b-9ed7-5a43de315461
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: de833817d36ecf3d8dc7c59f4ab2bc1d0b59517f
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56129976"
---
# <a name="link-users-and-devices-with-user-device-affinity-in-system-center-configuration-manager"></a>Vincular usuarios y dispositivos con afinidad entre usuario y dispositivo en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

La afinidad entre usuario y dispositivo en System Center Configuration Manager (Configuration Manager) asocia un usuario a uno o varios dispositivos. Puede que no sea necesario conocer los nombres de los dispositivos de un usuario a fin de implementar una aplicación para ese usuario. En lugar de implementar la aplicación en cada dispositivo del usuario, se implementa la aplicación en el usuario. A continuación, la afinidad entre usuario y dispositivo garantiza automáticamente que la aplicación se instale en todos los dispositivos asociados a ese usuario.  

 Puede definir dispositivos primarios, que suelen ser los dispositivos que los usuarios usan a diario para realizar su trabajo. Al crear una afinidad entre un usuario y un dispositivo, obtendrá más opciones de implementación de aplicaciones. Por ejemplo, si un usuario necesita Microsoft Visio, puede instalarlo en el dispositivo primario del usuario mediante una implementación de Windows Installer. Pero en un dispositivo que no sea primario, puede implementar Visio como una aplicación virtual. También puede usar la afinidad entre usuario y dispositivo para preimplementar software en un dispositivo de usuario cuando este no ha iniciado sesión. De este modo, cuando el usuario inicie sesión, la aplicación ya estará instalada y lista para ejecutarse.  

 Debe administrar la información sobre afinidad de dispositivo de usuario para equipos. Configuration Manager administra automáticamente las afinidades de dispositivo de usuario de los dispositivos móviles que inscribe.  

## <a name="manually-set-up-user-device-affinity"></a>Configurar manualmente la afinidad entre usuario y dispositivo  

1.  En la consola de Configuration Manager, seleccione **Activos y compatibilidad** > **Dispositivos**.  

3.  Seleccione un dispositivo de la lista. Después, en la pestaña **Inicio**, en el grupo **Dispositivo**, seleccione **Editar usuarios primarios**.  

4.  En el cuadro de diálogo **Editar usuarios primarios**, busque y seleccione los usuarios que quiere agregar como usuarios primarios del dispositivo seleccionado. Seleccione **Agregar**.  

    > [!NOTE]  
    > En la lista **Usuarios primarios** se muestran los usuarios que ya son usuarios primarios de este dispositivo y el método por el que se asignó cada relación entre usuario y dispositivo.  

## <a name="set-up-primary-devices-for-a-user"></a>Configurar los dispositivos primarios de un usuario  

1.  En la consola de Configuration Manager, seleccione **Activos y compatibilidad** > **Usuarios**.  

3.  Seleccione un usuario de la lista. Después, en la pestaña **Dispositivo**, seleccione **Editar dispositivos primarios**.  

4.  En el cuadro de diálogo **Editar dispositivos primarios**, busque y seleccione los dispositivos que quiere agregar como dispositivos primarios del usuario seleccionado. Seleccione **Agregar**.  

    > [!NOTE]  
    > En la lista **Dispositivos primarios** se muestran los dispositivos que ya están configurados como dispositivos primarios para este usuario y el método por el que se asignó cada relación entre usuario y dispositivo.  

## <a name="automatically-create-user-device-affinities-windows-pcs-only"></a>Crear automáticamente afinidades entre usuario y dispositivo (solo en PC con Windows)  
 Configuration Manager lee en el registro de eventos de Windows los datos sobre los inicios de sesión de usuario. Para crear automáticamente afinidades entre usuario y dispositivo, debe activar estas dos opciones en la directiva de seguridad local en los equipos cliente para almacenar los eventos de inicio de sesión en el registro de eventos de Windows:  

- **Auditar eventos de inicio de sesión de cuenta**  
- **Auditar eventos de inicio de sesión**  

  Para configurar estas opciones, use la directiva de grupo de Windows.  

> [!IMPORTANT]  
> Si un error hace que el registro de eventos de Windows genere un gran número de entradas, es posible que se cree un registro de eventos. Si esto ocurre, podría ser que los eventos de inicio de sesión existentes ya no estén disponibles en Configuration Manager.  
>   
> Preste especial atención cuando active las opciones **Auditar eventos de inicio de sesión de cuenta** y **Auditar eventos de inicio de sesión** en Windows XP. De forma predeterminada, la directiva de retención es de 7 días, y es muy probable que estos eventos llenen el registro de eventos de seguridad. Los usuarios estándar no podrán iniciar sesión si el registro de eventos está lleno. Para evitarlo, establezca la directiva **Método de retención** en **Sobrescribir eventos cuando sea necesario** para el registro de seguridad. Para que haya datos suficientes para la afinidad entre usuario y dispositivo, también debe establecer el tamaño máximo del registro de eventos de seguridad de la directiva en un valor razonable, entre 5 y 20 MB.  

### <a name="set-up-the-site-to-automatically-create-user-device-affinities"></a>Configurar el sitio para que cree automáticamente afinidades entre usuario y dispositivo  

1.  En la consola de Configuration Manager, elija **Administración** > **Configuración de cliente**.  

2.  Para modificar la configuración de cliente predeterminada, seleccione **Configuración de cliente predeterminada** y, después, en la pestaña **Inicio**, en el grupo **Propiedades**, seleccione **Propiedades**. Para crear una configuración de agente de cliente personalizada, seleccione el nodo **Configuración de cliente** y, después, en la pestaña **Inicio**, en el grupo **Crear**, seleccione **Crear configuración de dispositivo de cliente personalizada**.  

    > [!NOTE]  
    > Si modifica la configuración de cliente predeterminada, se implementará en todos los equipos de la jerarquía. Para obtener más información acerca de cómo configurar las opciones de cliente, consulte [How to configure client settings in System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md) (Configuración del cliente en System Center Configuration Manager).  

3.  Para **Afinidad entre usuario y dispositivo**, configure lo siguiente:  

    -   **User device affinity threshold (minutes)** (Umbral de afinidad entre usuario y dispositivo (minutos)). Establezca el número de minutos de uso del dispositivo antes de que se cree una afinidad entre usuario y dispositivo.  

    -   **User device affinity threshold (days)** (Umbral de afinidad entre usuario y dispositivo (días)). Establezca el número de días durante el que se mide el umbral de afinidad basado en el uso.  

    -   **Configurar automáticamente la afinidad de dispositivo de usuario desde los datos del usuario**. Para permitir que el sitio cree automáticamente afinidades entre usuario y dispositivo, seleccione **True** en la lista desplegable. Si selecciona **False**, debe aprobar todas las asignaciones de afinidad entre usuario y dispositivo.  

    > [!TIP]  
    > **Ejemplo:** si establece **Umbral de uso de afinidad de dispositivo de usuario (minutos)** en **60** minutos y **Umbral de uso de afinidad de dispositivo de usuario (días)** en **5** días, el usuario debe usar el dispositivo durante al menos 60 minutos a lo largo de un período de 5 días para que se cree automáticamente una afinidad entre usuario y dispositivo.  

Una vez creada una afinidad entre usuario y dispositivo, Configuration Manager continúa supervisando los umbrales de afinidad entre dispositivo y usuario. Si la actividad de usuario para el dispositivo es inferior a los umbrales que ha establecido, se quitará la afinidad entre usuario y dispositivo. Establezca **User device affinity threshold (days)** (Umbral de afinidad entre usuario y dispositivo (días)) en un valor de al menos **7** días para evitar situaciones en las que una afinidad entre usuario y dispositivo configurada automáticamente pueda perderse cuando el usuario no haya iniciado sesión, por ejemplo, durante un fin de semana.  

## <a name="import-user-device-affinities-from-a-file"></a>Importar afinidades entre usuario y dispositivo desde un archivo  
 Para crear muchas relaciones a la vez, puede importar un archivo que contenga los detalles de varias afinidades entre usuario y dispositivo. Para este procedimiento, es necesario que los dispositivos se hayan detectado y existan como recursos en la base de datos de Configuration Manager. De lo contrario, el procedimiento no podrá realizarse.  

1.  En la consola de Configuration Manager, seleccione **Activos y compatibilidad** > **Usuarios** o **Dispositivos**.  

2.  En la pestaña **Inicio**, en el grupo **Crear**, seleccione **Importar afinidad de dispositivo de usuario**.  

3.  En el Asistente para importar afinidad de dispositivo de usuario, en la página **Elegir asignación**, especifique esta información:  

    -   **Nombre del archivo**. Especifique un archivo de valores separados por comas (CSV) que contenga una lista de usuarios y dispositivos entre los que quiere crear una afinidad. En este archivo, cada par de usuario y dispositivo debe encontrarse en una fila propia, con los valores separados por una coma. Use este formato: <*Dominio*>&#92;<*nombre de usuario*>,<*nombre NetBIOS del dispositivo*>.  

    -   **Este archivo tiene encabezados de columna como referencia**. Si el archivo .csv tiene un encabezado en la fila superior, seleccione esta opción y la fila de encabezado se omitirá durante la importación.  

4.  Si el archivo que está importando tiene más de dos elementos en cada fila, puede usar **Columna** y **Asignar** para especificar qué columnas representan usuarios y dispositivos y qué columnas deben omitirse durante la importación.  

5.  Seleccione **Siguiente** y, después, finalice el Asistente para importar afinidad de dispositivo de usuario.  

## <a name="let-users-create-their-own-device-affinities"></a>Permitir que los usuarios creen sus propias afinidades de dispositivo  
 Con los procedimientos siguientes, puede configurar un usuario de modo que cree su propia afinidad entre usuario y dispositivo en la aplicación Centro de software.  

### <a name="set-up-the-site-to-allow-user-created-user-device-affinity-requests"></a>Configurar el sitio para que permita solicitudes de afinidad entre usuario y dispositivo creadas por el usuario  

1.  En la consola de Configuration Manager, elija **Administración** > **Configuración de cliente**.  

2.  Para modificar la configuración de cliente predeterminada, seleccione **Configuración de cliente predeterminada** y, después, en la pestaña **Inicio**, en el grupo **Propiedades**, seleccione **Propiedades**. Para crear una configuración de agente de cliente personalizada, seleccione el nodo **Configuración de cliente** y, después, en la pestaña **Inicio**, en el grupo **Crear**, seleccione **Crear configuración de usuario de cliente personalizada**.  

    > [!NOTE]  
    > Si modifica la configuración de cliente predeterminada, se implementará en todos los equipos de la jerarquía. Para obtener información sobre la configuración de cliente, consulte [How to configure client settings](../../core/clients/deploy/configure-client-settings.md) (Configuración de las opciones de cliente).  

3.  Seleccione **Afinidad entre usuario y dispositivo** de la configuración de cliente y, a continuación, en la lista desplegable **Permitir al usuario definir sus dispositivos primarios** , seleccione **Verdadero**.  

### <a name="set-up-a-user-device-affinity"></a>Configurar una afinidad entre usuario y dispositivo  

1.  En el Catálogo de aplicaciones, seleccione **Mis sistemas**.  

2.  Seleccione la opción **Normalmente uso este equipo para realizar mi trabajo**.  

## <a name="manage-user-device-affinity-requests-from-users"></a>Administrar solicitudes de usuarios de afinidad entre usuario y dispositivo  
 Cuando la configuración de cliente **Configurar automáticamente la afinidad de dispositivo de usuario desde los datos del usuario** está establecida en **Falso**, debe aprobar todas las asignaciones de afinidad entre usuario y dispositivo.  

### <a name="approve-or-reject-a-user-device-affinity-request"></a>Aprobación o rechazo de una solicitud de afinidad entre usuario y dispositivo  

1.  En la consola de Configuration Manager, elija **Activos y compatibilidad**.  

2.  En el área de trabajo **Activos y compatibilidad** , seleccione la recopilación de usuarios o dispositivos para la que desea administrar solicitudes de afinidad.  

3.  En la pestaña **Inicio**, en el grupo **Recopilación**, seleccione **Administrar solicitudes de afinidad**.  

4.  En el cuadro de diálogo **Administrar solicitudes de afinidad de dispositivo de usuario**, seleccione una solicitud de afinidad y, después, seleccione **Aprobar** o **Rechazar**.  
