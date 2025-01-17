---
title: Vincular usuarios y dispositivos con la afinidad entre usuario y dispositivo
titleSuffix: Configuration Manager
description: Vincule usuarios y dispositivos con afinidad entre usuario y dispositivo e implemente aplicaciones automáticamente en todos los dispositivos asociados a un usuario.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 5b30b0d5-722d-4d4b-9ed7-5a43de315461
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: e1a6b104d35e037c3e63b07b29c80c9709a9e9fe
ms.sourcegitcommit: 72faa1266b31849ce1a23d661a1620b01e94f517
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/26/2019
ms.locfileid: "68534728"
---
# <a name="link-users-and-devices-with-user-device-affinity-in-configuration-manager"></a>Vinculación de usuarios y dispositivos con afinidad en Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

La afinidad entre usuario y dispositivo en Configuration Manager asocia un usuario a uno o varios dispositivos. Este comportamiento puede eliminar la necesidad de conocer los nombres de los dispositivos de un usuario a fin de implementar una aplicación para ese usuario. En lugar de implementar la aplicación en cada dispositivo del usuario, se implementa la aplicación en el usuario. A continuación, la afinidad entre usuario y dispositivo se asegura automáticamente de que la aplicación se instale en todos los dispositivos asociados a ese usuario.  

Defina los dispositivos primarios que usan los usuarios cada día para su trabajo. Al crear una afinidad entre un usuario y un dispositivo, obtendrá más opciones de implementación de aplicaciones. Por ejemplo, si un usuario necesita Microsoft Visio, puede instalarlo en el dispositivo primario del usuario mediante una implementación de Windows Installer. Pero en un dispositivo que no sea primario, puede implementar Visio como una aplicación virtual. También puede usar la afinidad entre usuario y dispositivo para implementar previamente software en el dispositivo de un usuario cuando este no tiene la sesión iniciada. A continuación, cuando el usuario inicia sesión, la aplicación ya está instalada y lista para ejecutarse.  

Usted solamente administra la información sobre afinidad de dispositivo de usuario para equipos. Configuration Manager administra automáticamente las afinidades de dispositivo de usuario de los dispositivos móviles que inscribe.  

## <a name="manually-set-up-user-device-affinity"></a>Configurar manualmente la afinidad entre usuario y dispositivo  

1. En la consola de Configuration Manager, vaya al área de trabajo **Activos y compatibilidad** y haga clic en el nodo **Dispositivos**.  

1. Seleccione un dispositivo. En la pestaña **Inicio** de la cinta de opciones, en el grupo **Dispositivo**, seleccione **Editar usuarios primarios**.  

1. En el cuadro de diálogo **Editar usuarios primarios**, busque y seleccione los usuarios que quiere agregar como usuarios primarios del dispositivo seleccionado. Seleccione **Agregar**.  

    > [!NOTE]  
    > En la lista **Usuarios primarios** se muestran los usuarios que ya son usuarios primarios de este dispositivo y el método por el que se asignó cada relación entre usuario y dispositivo.  

## <a name="set-up-primary-devices-for-a-user"></a>Configurar los dispositivos primarios de un usuario  

1. En la consola de Configuration Manager, vaya al área de trabajo **Activos y compatibilidad** y haga clic en el nodo **Usuarios**.  

1. Seleccione un usuario. En la pestaña **dispositivo** de la cinta de opciones, elija **Editar dispositivos primarios**.  

1. En el cuadro de diálogo **Editar dispositivos primarios**, busque y seleccione los dispositivos que quiere agregar como dispositivos primarios del usuario seleccionado. Seleccione **Agregar**.  

    > [!NOTE]  
    > En la lista **Dispositivos primarios** se muestran los dispositivos que ya están configurados como dispositivos primarios para este usuario y el método por el que se asignó cada relación entre usuario y dispositivo.  

## <a name="automatically-create-user-device-affinities-windows-pcs-only"></a>Crear automáticamente afinidades entre usuario y dispositivo (solo en PC con Windows)

Configuration Manager lee en el registro de eventos de Windows los datos sobre los eventos de inicios de sesión de usuario. Para crear automáticamente afinidades entre el usuario y el dispositivo, active estas dos opciones en la directiva de seguridad local en los equipos cliente para almacenar los eventos de inicio de sesión en el registro de eventos de Windows:  

- **Auditar eventos de inicio de sesión de cuenta**  
- **Auditar eventos de inicio de sesión**  

Para configurar estas opciones, use la directiva de grupo de Windows.  

> [!IMPORTANT]  
> Si un error hace que el registro de eventos de Windows genere un gran número de entradas, es posible que se cree un nuevo registro de eventos. Si se produce este comportamiento, podría ser que los eventos de inicio de sesión existentes no estén disponibles en Configuration Manager.  

### <a name="set-up-the-site-to-automatically-create-user-device-affinities"></a>Configurar el sitio para que cree automáticamente afinidades entre usuario y dispositivo  

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración** y seleccione el nodo **Configuración de cliente**.  

1. Para modificar la configuración de cliente predeterminada, seleccione **configuración de cliente predeterminada**. En la pestaña **Inicio** de la cinta de opciones, en el grupo **Propiedades**, seleccione **Propiedades**.

    Para crear una configuración de agente de cliente personalizada, en la pestaña **Inicio** de la cinta de opciones, en el grupo **crear** , elija **crear configuración de dispositivo de cliente personalizada**.

    > [!NOTE]  
    > Si modifica la configuración de cliente predeterminada, el sitio la implementa en todos los equipos de la jerarquía. Para obtener más información, vea [Cómo configurar el cliente](/sccm/core/clients/deploy/configure-client-settings).  

1. En el grupo de **afinidad entre usuario y dispositivo** , establezca la siguiente configuración:  

    - **Umbral de afinidad de dispositivo de usuario (minutos)** : establezca el número de minutos de uso del dispositivo antes de que el sitio cree una afinidad de dispositivo de usuario.  

    - **Umbral de uso de afinidad de dispositivo de usuario (días)** : establezca la cantidad de días durante la cual el sitio mide el umbral de afinidad basado en el uso.  

    - **Configurar automáticamente la afinidad de dispositivo de usuario a partir de datos de uso**: seleccione **true** para permitir que el sitio cree automáticamente afinidades de dispositivo del usuario. Si selecciona **False**, necesita aprobar todas las asignaciones de afinidad entre usuario y dispositivo.  

    > [!TIP]  
    > Ejemplo: si establece **Umbral de uso de afinidad de dispositivo de usuario (minutos)**  **60** minutos y **Umbral de uso de afinidad de dispositivo de usuario (días)** en **60** días, el usuario debe usar el dispositivo durante al menos 5 minutos a lo largo de un período de 5 días para que se cree automáticamente una afinidad entre usuario y dispositivo.  

Después de que Configuration Manager cree una afinidad entre usuario y dispositivo automática, continúa supervisando los umbrales de afinidad entre el dispositivo y el usuario. Si la actividad de usuario para el dispositivo es inferior a los umbrales que ha establecido, el sitio quita la afinidad entre usuario y dispositivo. Establezca **umbral de afinidad de dispositivo de usuario (días)** en un valor de al menos siete días. Esta configuración evita situaciones en las que una afinidad de dispositivo de usuario configurada automáticamente podría perderse mientras el usuario no haya iniciado sesión, por ejemplo, durante el fin de semana.  


## <a name="import-user-device-affinities-from-a-file"></a>Importar afinidades entre usuario y dispositivo desde un archivo

Para crear muchas relaciones a la vez, importe un archivo que contenga los detalles de varias afinidades entre el usuario y el dispositivo. Asegúrese de que el sitio ya detecta los dispositivos de destino y que existen como recursos en la base de datos de Configuration Manager.  

1. En la consola de Configuration Manager, vaya al área de trabajo **Activos y compatibilidad** y seleccione el nodo **Usuarios** o **Dispositivos**.  

1. En la pestaña **Inicio** de la cinta de opciones, en el grupo **Crear**, seleccione **Importar afinidad de dispositivo de usuario**.  

1. En el Asistente para importar afinidad de dispositivo de usuario, en la página **Elegir asignación**, especifique esta información:  

    - **Nombre del archivo**. Especifique un archivo de valores separados por comas (CSV) que contenga una lista de usuarios y dispositivos entre los que quiere crear una afinidad. En este archivo, cada par de usuario y dispositivo debe encontrarse en una fila propia, con los valores separados por una coma. Use este formato:`<domain>\<username>,<device NetBIOS name>`  

    - **Este archivo tiene encabezados de columna como referencia**. Si el archivo. csv tiene un encabezado de fila superior, seleccione esta opción. El sitio omite la fila de encabezado durante la importación.  

1. Si el archivo que importa tiene más de dos elementos en cada fila, puede usar **Columna** y **Asignar** para especificar qué columnas representan usuarios y dispositivos y qué columnas deben omitirse durante la importación.  

1. Complete el asistente.  


## <a name="let-users-create-their-own-device-affinities"></a>Permitir que los usuarios creen sus propias afinidades de dispositivo

Configure un usuario para crear su propia afinidad de dispositivo de usuario en el centro de software.

### <a name="set-up-the-site-to-allow-user-created-user-device-affinity-requests"></a>Configurar el sitio para que permita solicitudes de afinidad entre usuario y dispositivo creadas por el usuario  

1  En la consola de Configuration Manager, vaya al área de trabajo **Administración** y seleccione el nodo **Configuración de cliente**.  

1. Para modificar la configuración de cliente predeterminada, seleccione **configuración de cliente predeterminada**. En la pestaña **Inicio** de la cinta de opciones, en el grupo **Propiedades**, seleccione **Propiedades**.

    Para crear una configuración de agente de cliente personalizada, en la pestaña **Inicio** de la cinta de opciones, en el grupo **crear** , elija **crear configuración de usuario de cliente personalizada**.

    > [!NOTE]  
    > Si modifica la configuración de cliente predeterminada, el sitio la implementa en todos los equipos de la jerarquía. Para más información, vea [Cómo configurar el cliente en System Center Configuration Manager](/sccm/core/clients/deploy/configure-client-settings).  

1. En el grupo de **afinidad entre usuario y dispositivo** , habilite la opción para **permitir al usuario definir sus dispositivos primarios**.  

### <a name="set-up-a-user-device-affinity-in-software-center"></a>Configuración de la afinidad entre usuario y dispositivo en el Centro de software

A partir de la versión 1902, use el centro de software para establecer la afinidad.

1. En el centro de software, vaya a la pestaña **Opciones** .

1. En la sección **información del trabajo** , seleccione la opción **usar este equipo con regularidad para realizar mi trabajo**.

### <a name="set-up-a-user-device-affinity-in-the-application-catalog"></a>Configuración de una afinidad de dispositivo de usuario en el catálogo de aplicaciones

> [!Important]
> La experiencia de usuario de Silverlight del catálogo de aplicaciones no se admite a partir de la versión de la rama actual 1806. A partir de la versión 1906, los clientes actualizados usan automáticamente el punto de administración para las implementaciones de aplicaciones disponibles para el usuario. Tampoco se pueden instalar nuevos roles del catálogo de aplicaciones. En la primera versión de la rama actual después del 31 de octubre de 2019, finalizará el soporte técnico para los roles de catálogo de aplicaciones.  
>
> Vea los siguientes artículos para más información:
>
> - [Configurar el Centro de software](/sccm/apps/plan-design/plan-for-software-center#bkmk_userex)
> - [Características eliminadas y en desuso](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures)  

1. En el catálogo de aplicaciones, seleccione **Mis sistemas**.  

1. Seleccione la opción **Normalmente uso este equipo para realizar mi trabajo**.  


## <a name="manage-user-device-affinity-requests-from-users"></a>Administrar solicitudes de usuarios de afinidad entre usuario y dispositivo

Al deshabilitar la configuración de cliente para **configurar automáticamente la afinidad de dispositivo de usuario a partir de datos de uso**, debe aprobar manualmente todas las asignaciones de afinidad de dispositivo de usuario.  

### <a name="approve-or-reject-a-user-device-affinity-request"></a>Aprobación o rechazo de una solicitud de afinidad entre usuario y dispositivo  

1. En la consola de Configuration Manager, vaya al área de trabajo **Activos y compatibilidad**.  

1. Seleccione la recopilación de usuarios o dispositivos para la que desea administrar solicitudes de afinidad.  

1. En la pestaña **Inicio** de la cinta de opciones, en el grupo **Recopilación**, seleccione **Administrar solicitudes de afinidad**.  

1. En el cuadro de diálogo **Administrar solicitudes de afinidad de dispositivo de usuario**, seleccione una solicitud de afinidad y, después, seleccione **Aprobar** o **Rechazar**.  


## <a name="next-steps"></a>Pasos siguientes

También puede usar Microsoft Intune para buscar el uso principal de un dispositivo inscrito. Para obtener más información, vea [Buscar el usuario principal de un dispositivo](https://docs.microsoft.com/intune/find-primary-user) de Intune en la documentación de Intune.
