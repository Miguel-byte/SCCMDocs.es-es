---
title: Directivas de Firewall de Windows para Endpoint Protection
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo crear e implementar directivas de firewall para Endpoint Protection en System Center 2012 Configuration Manager.
ms.date: 03/07/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 6ecdfad1-6305-45a8-ae75-3f33b967cb8f
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: d1747cc8c4b43402319ce2924c3eaa680a72f83f
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56125126"
---
# <a name="create-and-deploy-windows-firewall-policies-for-endpoint-protection-in-system-center-configuration-manager"></a>Crear e implementar directivas de Firewall de Windows para Endpoint Protection en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Las directivas de firewall de Endpoint Protection en System Center Configuration Manager permiten realizar tareas básicas de configuración y mantenimiento del Firewall de Windows en equipos cliente de la jerarquía. Puede usar las directivas de Firewall de Windows para realizar las siguientes tareas:  

-   Controlar si el Firewall de Windows está activado o desactivado.  

-   Controlar si se permiten las conexiones entrantes en los equipos cliente.  

-   Controlar si los usuarios reciben notificaciones cuando Firewall de Windows bloquea un programa nuevo.  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad**.  

2.  En el área de trabajo **Activos y compatibilidad**, expanda **Endpoint Protection** y haga clic en **Directivas de Firewall de Windows**.  

3.  En la ficha **Inicio** , en el grupo **Crear** , haga clic en **Crear directiva de Firewall de Windows**.  

4.  En la página **General** del **Asistente para crear directiva de Firewall de Windows**, especifique un nombre y una descripción opcional para esta directiva de firewall y, a continuación, haga clic en **Siguiente**.  

5.  En la página **Configuración de perfil** del asistente, especifique la siguiente configuración para cada perfil de red:  

    > [!IMPORTANT]  
    >  Si quiere implementar directivas de Firewall de Windows en equipos que ejecutan Windows Server 2008 y Windows Vista Service Pack 1, primero debe instalar la [revisión KB971800](http://go.microsoft.com/fwlink/p/?LinkId=231239) en estos equipos.  

    > [!NOTE]  
    >  Para más información acerca de los perfiles de red, consulte la documentación de Windows.  

    -   **Habilitar Firewall de Windows**  

        > [!NOTE]  
        >  Si **Habilitar Firewall de Windows** no está habilitado, las demás opciones de configuración de esta página no estarán disponibles.  

    -   **Bloquear todas las conexiones entrantes, incluidas las de la lista de programas permitidos.**  

    -   **Notificar al usuario cuando Firewall de Windows bloquee un nuevo programa**  

6.  En la página **Resumen** del asistente, revise las acciones que se realizarán y, a continuación, complete el asistente.  

7.  Compruebe que la nueva directiva del Firewall de Windows se muestra en la lista **Directivas de Firewall de Windows** .  

##  <a name="BKMK_Assign"></a> Para implementar una directiva del Firewall de Windows  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad**.  

2.  En el área de trabajo **Activos y compatibilidad**, expanda **Endpoint Protection** y haga clic en **Directivas de Firewall de Windows**.  

3.  En la lista **Directivas de Firewall de Windows** , seleccione la directiva del Firewall de Windows que quiera implementar.  

4.  En la pestaña **Inicio** , en el grupo **Implementación** , haga clic en **Implementar**.  

5.  En el cuadro de diálogo **Implementar directiva de Firewall de Windows** , especifique la recopilación a la que desea asignar esta directiva del Firewall de Windows y una programación de asignación. El cumplimiento de la directiva del Firewall de Windows se evalúa mediante esta programación y la configuración del Firewall de Windows en los clientes que se van a volver a configurar para que coincidan con la directiva del Firewall de Windows.  

6.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Implementar directiva de Firewall de Windows** e implementar la directiva del Firewall de Windows.  

    > [!IMPORTANT]  
    >  Al implementar una directiva de Firewall de Windows en una recopilación, esta directiva se aplica a los equipos en orden aleatorio durante un período de dos horas para evitar el desbordamiento de la red.
