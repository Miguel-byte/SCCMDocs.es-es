---
title: Configurar opciones de cliente | System Center Configuration Manager
description: "Seleccione la configuración de cliente en System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 95e9858a-bad4-4651-9e61-2e31dc5050fa
caps.latest.revision: 5
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 9e3162e04da90748379145e37f6b378badab97d3

---
# <a name="how-to-configure-client-settings-in-system-center-configuration-manager"></a>Cómo configurar el cliente en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Todas las opciones de cliente de System Center Configuration Manager se administran desde el nodo **Configuración de cliente** del área de trabajo **Administración** de la consola de Configuration Manager. Modifique la configuración predeterminada si desea configurar opciones para todos los usuarios y dispositivos de la jerarquía que no tienen aplicada ninguna configuración personalizada. Si desea aplicar una configuración diferente solamente a algunos usuarios o dispositivos, cree una configuración personalizada e impleméntela en las recopilaciones.  

> [!NOTE]  
>  También puede utilizar elementos de configuración a fin de administrar los clientes para evaluar, seguir y corregir la compatibilidad de la configuración de los dispositivos. Para más información, vea [Ensure device compliance with System Center Configuration Manager (Garantizar el cumplimiento de dispositivos con System Center Configuration Manager)](../../../compliance/understand/ensure-device-compliance.md).  

##  <a name="a-namebkmkdefaultclientsettingsa-how-to-configure-the-default-client-settings"></a><a name="BKMK_DefaultClientSettings"></a> Cómo configurar las opciones predeterminadas del cliente  

 Utilice el siguiente procedimiento para configurar las opciones predeterminadas del cliente para todos los clientes de la jerarquía.  

#### <a name="to-configure-the-default-client-settings"></a>Para configurar las opciones predeterminadas del cliente  

1.  En la consola de Configuration Manager, haga clic en **Administración**.  

2.  En el área de trabajo **Administración** , expanda **Configuración de cliente**y, a continuación, haga clic en **Configuración de cliente predeterminada**.  

3.  En la pestaña **Inicio** , haga clic en **Propiedades**.  

4.  Vea y configure las opciones de cliente para cada grupo de opciones que presenta el panel de navegación. Para más información sobre cada opción, vea [About client settings in System Center Configuration Manager (Acerca de la configuración de cliente en System Center Configuration Manager)](../../../core/clients/deploy/about-client-settings.md).  

5.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Configuración de cliente predeterminada** .  

 Los equipos cliente se configurarán con estas opciones la próxima vez que descarguen directivas de cliente. Para iniciar la recuperación de directivas para un solo cliente, vea [Initiate Policy Retrieval for a Configuration Manager Client (Iniciar la recuperación de directivas para un cliente de Configuration Manager)](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval) en [How to manage clients in System Center Configuration Manager (Cómo administrar clientes en System Center Configuration Manager)](../../../core/clients/manage/manage-clients.md).  

##  <a name="a-namebkmkcustomclientsettingsa-how-to-create-and-deploy-custom-client-settings"></a><a name="BKMK_CustomClientSettings"></a> Cómo crear e implementar la configuración de cliente predeterminada  
 Utilice el siguiente procedimiento para configurar e implementar la configuración personalizada para una recopilación seleccionada de usuarios o dispositivos. La implementación de esta configuración personalizada reemplaza la configuración de cliente personalizada.  

> [!NOTE]  
>  Antes de comenzar con este procedimiento, asegúrese de que tiene una recopilación que contiene los usuarios o dispositivos que requieren esta configuración de cliente personalizada.  

#### <a name="to-configure-and-deploy-custom-client-settings"></a>Para configurar e implementar la configuración de cliente personalizada  

1.  En la consola de Configuration Manager, haga clic en **Administración**.  

2.  En el área de trabajo **Administración** , haga clic en **Configuración de cliente**.  

3.  En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear configuración de cliente personalizada**y, a continuación, haga clic en una de las siguientes opciones en función de si desea crear una configuración de cliente personalizada para dispositivos o para usuarios:  

    -   **Crear configuración de dispositivo de cliente personalizada**  

    -   **Crear configuración de usuario de cliente personalizada**  

4.  En el cuadro de diálogo **Crear configuración de dispositivo personalizada** o **Crear configuración de usuario personalizada** , especifique un nombre único para la configuración personalizada y una descripción opcional.  

5.  Seleccione una o varias de las casillas de verificación disponibles, las cuales mostrarán un grupo de opciones.  

6.  Haga clic en la configuración del primer grupo desde el panel de navegación y, a continuación, vea y configure la configuración personalizada disponible. Repita este proceso para el resto de las configuraciones de grupo. Para más información sobre cada opción de cliente, vea [About client settings in System Center Configuration Manager (Acerca de la configuración de cliente en System Center Configuration Manager)](../../../core/clients/deploy/about-client-settings.md).  

7.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Crear configuración de dispositivo personalizada** o **Crear configuración de usuario personalizada** .  

8.  Seleccione la configuración de cliente personalizada que acaba de crear. En la pestaña **Inicio** , en el grupo **Configuración de cliente** , haga clic en **Implementar**.  

9. En el cuadro de diálogo **Seleccionar recopilación** , seleccione la recopilación que contiene los dispositivos o los usuarios en los que se va a establecer la configuración personalizada y, a continuación, haga clic en **Aceptar**. Puede comprobar la recopilación seleccionada si hace clic en la pestaña **Implementaciones** en el panel de detalles.  

10. Vea el orden de la configuración de cliente personalizada que acaba de crear. Si hay más de una configuración de cliente personalizada, se aplican en función de su número de orden. Si hay algún conflicto, la configuración que tenga el número de orden más bajo reemplaza al resto de configuraciones. Para cambiar el número de orden, en la pestaña **Inicio** , en el grupo **Configuración de cliente** , haga clic en **Subir elemento** o en **Bajar elemento**.  

 Los equipos cliente se configurarán con estas opciones la próxima vez que descarguen directivas de cliente. Para iniciar la recuperación de directivas para un solo cliente, vea [Initiate Policy Retrieval for a Configuration Manager Client (Iniciar la recuperación de directivas para un cliente de Configuration Manager)](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval) en [How to manage clients in System Center Configuration Manager (Cómo administrar clientes en System Center Configuration Manager)](../../../core/clients/manage/manage-clients.md).  

##  <a name="a-namebkmkresultantclientsettingsa-how-to-view-resultant-client-settings"></a><a name="BKMK_ResultantClientSettings"></a> Cómo visualizar la configuración de cliente resultante  
 Cuando se han implementado varias configuraciones de cliente en el mismo dispositivo, usuario o grupo de usuarios, el establecimiento de prioridades y la combinación de configuraciones pueden resultar complejos. Utilice el procedimiento siguiente para ver la configuración de cliente resultante calculada.  

#### <a name="to-view-the-resultant-client-settings"></a>Para ver la configuración de cliente resultante  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad**.  

2.  En el área de trabajo **Activos y compatibilidad** , haga clic en **Dispositivos**, **Usuarios**o **Recopilaciones de usuarios**.  

3.  Seleccione un dispositivo, un usuario o un grupo de usuarios y en el grupo **Configuración de cliente** , seleccione **Configuración de cliente resultante**.  Como alternativa, haga clic con el botón secundario en el dispositivo, el usuario o el grupo de usuarios, seleccione **Configuración de cliente**y haga clic en **Configuración de cliente resultante**.  

4.  Seleccione una configuración de cliente en el panel izquierdo y se mostrará la configuración resultante.  

    > [!NOTE]  
    >  Para ver la configuración de cliente resultante, el usuario que ha iniciado sesión debe tener acceso de lectura a la configuración del cliente.  

    > [!NOTE]  
    >  La configuración resultante que se muestra es de solo lectura. Para modificar la configuración, utilice los procedimientos anteriores.  



<!--HONumber=Nov16_HO1-->


