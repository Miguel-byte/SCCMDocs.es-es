---
title: Configurar opciones de cliente | Microsoft Docs
description: "Seleccione la configuración de cliente en System Center Configuration Manager."
ms.custom: na
ms.date: 12/12/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 95e9858a-bad4-4651-9e61-2e31dc5050fa
caps.latest.revision: 5
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 809c7938968b4a6efce6ef37fe7b7baf2c9dd3e7
ms.openlocfilehash: 77e17786302c885052c8861107a49ff826accb65

---
# <a name="how-to-configure-client-settings-in-system-center-configuration-manager"></a>Cómo configurar el cliente en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Puede administrar toda la configuración de cliente en System Center Configuration Manager desde **Administración** > **Configuración de cliente**. Modifique la configuración predeterminada si desea configurar opciones para todos los usuarios y dispositivos de la jerarquía que no tienen aplicada ninguna configuración personalizada. Si desea aplicar una configuración diferente solamente a algunos usuarios o dispositivos, cree una configuración personalizada e impleméntela en las recopilaciones.  

Para más información sobre cada opción de cliente, vea [About client settings in System Center Configuration Manager (Acerca de la configuración de cliente en System Center Configuration Manager)](../../../core/clients/deploy/about-client-settings.md).

> [!NOTE]  
>  También puede utilizar elementos de configuración a fin de administrar los clientes para evaluar, seguir y corregir la compatibilidad de la configuración de los dispositivos. Para más información, vea [Ensure device compliance with System Center Configuration Manager (Garantizar el cumplimiento de dispositivos con System Center Configuration Manager)](../../../compliance/understand/ensure-device-compliance.md).  

##  <a name="configure-the-default-client-settings"></a>Configurar las opciones predeterminadas de cliente    

1.  En la consola de Configuration Manager, elija **Administración** > **Configuración de cliente** > **Configuración de cliente predeterminada**.  

3.  En la pestaña **Inicio**, elija **Propiedades**.  

4.  Vea y configure las opciones de cliente para cada grupo de opciones que presenta el panel de navegación.  

 Los equipos cliente se configurarán con estas opciones la próxima vez que descarguen directivas de cliente. Para iniciar la recuperación de directivas para un solo cliente, vea [Initiate Policy Retrieval for a Configuration Manager Client (Iniciar la recuperación de directivas para un cliente de Configuration Manager)](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval) en [How to manage clients in System Center Configuration Manager (Cómo administrar clientes en System Center Configuration Manager)](../../../core/clients/manage/manage-clients.md).  

##  <a name="create-and-deploy-custom-client-settings"></a>Crear e implementar la configuración predeterminada de cliente  
La implementación de esta configuración personalizada reemplaza la configuración de cliente personalizada. Antes de comenzar con este procedimiento, asegúrese de que tiene una recopilación que contiene los usuarios o dispositivos que requieren esta configuración de cliente personalizada.  

1.  En la consola de Configuration Manager, elija **Administración** > **Configuración de cliente**.  

3.  En la pestaña **Inicio**, en el grupo **Crear**, elija **Crear configuración de cliente personalizada** y, luego, elija una de estas opciones:  

    -   **Crear configuración de dispositivo de cliente personalizada**  

    -   **Crear configuración de usuario de cliente personalizada**  

4.  Especifique un nombre único y una descripción opcional.  

5.  Seleccione una o varias de las casillas que muestran un grupo de opciones.  

6.  Elija cada grupo de opciones en el panel de navegación y configure los ajustes disponibles; luego, haga clic en **Aceptar**.   

8.  Seleccione la configuración de cliente personalizada que creó. En la pestaña **Inicio**, en el grupo **Configuración de cliente**, elija **Implementar**.  

9. En el cuadro de diálogo **Seleccionar colección**, seleccione la colección adecuada y, luego, elija **Aceptar**. Puede comprobar la recopilación seleccionada si hace clic en la pestaña **Implementaciones** en el panel de detalles.  

10. Vea el orden de la configuración de cliente personalizada que acaba de crear. Si hay más de una configuración de cliente personalizada, se aplican en función de su número de orden. Si hay algún conflicto, la configuración que tenga el número de orden más bajo reemplaza al resto de configuraciones. Para cambiar el número de orden, en la pestaña **Inicio**, en el grupo **Configuración de cliente**, elija **Subir elemento** o en **Bajar elemento**.  

 Los equipos cliente se configurarán con estas opciones la próxima vez que descarguen directivas de cliente. Para iniciar la recuperación de directivas para un solo cliente, vea [Initiate Policy Retrieval for a Configuration Manager Client (Iniciar la recuperación de directivas para un cliente de Configuration Manager)](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval) en [How to manage clients in System Center Configuration Manager (Cómo administrar clientes en System Center Configuration Manager)](../../../core/clients/manage/manage-clients.md).  

##  <a name="view-client-settings"></a>Ver la configuración de cliente  
 Cuando se han implementado varias configuraciones de cliente en el mismo dispositivo, usuario o grupo de usuarios, el establecimiento de prioridades y la combinación de configuraciones pueden resultar complejos. Para ver la configuración de cliente:  

1.  En la consola de Configuration Manager, elija **Activos y compatibilidad** > **Dispositivos** > **Usuarios** o **Colecciones de usuarios**.  

3.  Seleccione un dispositivo, un usuario o un grupo de usuarios y en el grupo **Configuración de cliente** , seleccione **Configuración de cliente resultante**.  

4.  Seleccione una configuración de cliente en el panel de la izquierda y verá la configuración. En esta vista, la configuración es de solo lectura. 

    > [!NOTE]  
    >  Para ver la configuración de cliente, debe tener acceso de lectura a Configuración de cliente.  

    


<!--HONumber=Dec16_HO3-->


