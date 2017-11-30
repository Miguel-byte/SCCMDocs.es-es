---
title: Cambiar las cargas de trabajo de Configuration Manager a Intune
description: "Obtenga información sobre cómo cambiar las cargas de trabajo que administra actualmente Configuration Manager a Microsoft Intune."
keywords: 
author: dougeby
manager: angrobe
ms.date: 11/20/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: 
ms.assetid: 60e2022f-a4f9-40dd-af01-9ecb37b43878
ms.openlocfilehash: 60aff996ec598cff7572a0e88c631dc9c509e007
ms.sourcegitcommit: 12d0d53e47bbf1a0bbd85015b8404a44589d1e14
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="switch-configuration-manager-workloads-to-intune"></a>Cambiar las cargas de trabajo de Configuration Manager a Intune
En [Preparación de dispositivos Windows 10 para la administración conjunta](co-management-prepare.md), preparó los dispositivos Windows 10 para la administración conjunta. Estos dispositivos ahora están unidos a AD y a Azure AD, están inscritos en Intune y tienen el cliente de Configuration Manager. Es probable que aún tenga dispositivos de Windows 10 unidos a AD y que tenga el cliente de Configuration Manager, pero no que esté unido a Azure AD ni inscrito en Intune. En el siguiente procedimiento se proporcionan los pasos necesarios para habilitar la administración conjunta y preparar el resto de los dispositivos de Windows 10 (clientes de Configuration Manager sin la inscripción de Intune) para la administración conjunta. También podrá empezar a trasladar a Intune determinadas cargas de trabajo de Configuration Manager.

1. En la consola de Configuration Manager, vaya a **Administración** > **Información general** > **Servicios de nube** > **Co-management** (Administración conjunta).    
2. En la pestaña Home (Inicio), en el grupo Manage (Administrar), elija  **Configure co-management** (Configurar administración conjunta) para abrir el Asistente para la incorporación de la administración conjunta.    
3. En la página de suscripción, haga clic en **Iniciar sesión**, inicie sesión con su inquilino de Intune y haga clic en **Siguiente**.   
4. En la página de habilitación, elija **Piloto** o **Todo** para habilitar la inscripción automática en Intune y, luego, haga clic en **Siguiente**. Si elige **Piloto**, solo los clientes de Configuration Manager que sean miembros del grupo piloto se inscribirán automáticamente en Intune. De esta manera podrá habilitar la administración conjunta en un subconjunto de clientes para probarla inicialmente e implementarla con un enfoque por fases. La línea de comandos se puede usar para implementar el cliente de Configuration Manager como una aplicación en Intune para los dispositivos ya inscritos en Intune. Para obtener más información, consulte [Dispositivos de Windows 10 inscritos en Intune](co-management-prepare.md#windows-10-devices-enrolled-in-intune).
5. En la página Cargas de trabajo, elija si quiere cambiar las cargas de trabajo de Configuration Manager para que las administre Intune o Piloto de Intune. Luego, haga clic en **Siguiente**. La configuración **Piloto de Intune** cambia la carga de trabajo asociada solo para los dispositivos del grupo Piloto. La configuración **Intune** cambia la carga de trabajo asociada para todos los dispositivos Windows 10 administrados conjuntamente. 
        
   > [!Important]    
   > Antes de cambiar las cargas de trabajo, asegúrese de que la carga de trabajo correspondiente en Intune se ha configurado e implementado correctamente. De este modo, se garantiza que las cargas de trabajo siempre se administren mediante una de las herramientas de administración de sus dispositivos.   
1. En la página de almacenamiento provisional, configure las opciones siguientes y haga clic en **Siguiente**:
    - **Piloto**: el grupo piloto contiene una o varias recopilaciones que seleccione. Use este grupo como parte de la implementación por fases de la administración conjunta. Puede comenzar con un conjunto de prueba pequeños y, luego, agregar más colecciones al grupo piloto a medida que implemente la administración conjunta en más usuarios y dispositivos. Puede cambiar las colecciones del grupo piloto en cualquier momento desde las propiedades de la administración conjunta.
    - **Producción**: configure el **grupo de exclusión** con una o varias recopilaciones. Los dispositivos que forman parte de cualquiera de las colecciones de este grupo se excluyen del uso de la administración conjunta. 
2. Para habilitar la administración conjunta, siga los pasos del asistente.  

## <a name="modify-your-co-management-settings"></a>Modificación de la configuración de administración conjunta
Después de habilitar la administración conjunta con el asistente, puede modificar la configuración de las propiedades de administración conjunta.  
- En la consola de Configuration Manager, vaya a **Administración** > **Información general** > **Servicios de nube** > **Co-management** (Administración conjunta).  
Seleccione el objeto de administración conjunta y, luego, en la pestaña Inicio, haga clic en **Propiedades**. 

## <a name="monitor-co-management"></a>Supervisión de la administración conjunta
Después de habilitar la administración conjunta, puede supervisar los dispositivos de administración conjunta utilizando los métodos siguientes:
- **Vista SQL y clase WMI**: puede consultar la vista SQL **v&#95;ClientCoManagementState** en la base de datos de sitio de Configuration Manager o en la clase WMI **SMS&#95;Client&#95;ComanagementState**. Con la información de la clase WMI, puede crear recopilaciones personalizadas en Configuration Manager para ayudar a determinar el estado de la implementación de la administración compartida. Para obtener más información, consulte [Cómo crear recopilaciones](/sccm/core/clients/manage/collections/create-collections). Los campos siguientes están disponibles en la vista SQL y la clase WMI: 
    - **MachineId**: especifica un identificador de dispositivo único para el cliente de Configuration Manager.
    - **MDMEnrolled**: especifica si el dispositivo está inscrito en MDM. 
    - **Entidad**: especifica la entidad para la que el dispositivo está inscrito.
    - **ComgmtPolicyPresent**: especifica si la directiva de administración conjunta de Configuration Manager existe en el cliente. Si el valor de **MDMEnrolled** es **0**, el dispositivo no se administra conjuntamente con independencia de si existe la directiva de administración conjunta en el cliente.

   > [!Note]    
   > Un dispositivo se administra conjuntamente cuando los campos **MDMEnrolled** y **ComgmtPolicyPresent** tienen un valor de **1**.

- **Directivas de implementación**: hay dos directivas que se crean en **Supervisión** > **Implementaciones**; una para el grupo piloto y otra para producción. Estas directivas solo informan del número de dispositivos donde Configuration Manager ha aplicado la directiva. No tiene en cuenta cuántos están inscritos en Intune, que es un requisito antes de que los dispositivos se puedan administrar conjuntamente.  

## <a name="check-compliance-for-co-managed-devices"></a>Comprobación del cumplimiento para los dispositivos administrados conjuntamente
Los usuarios pueden usar el Centro de software para comprobar el cumplimiento de sus dispositivos Windows 10 administrados conjuntamente, incluso cuando se administra el acceso condicional mediante Intune o Configuration Manager. Los usuarios también pueden comprobar el cumplimiento mediante la aplicación de Portal de empresa cuando se administra el acceso condicional mediante Intune.

## <a name="next-steps"></a>Pasos siguientes
Use los siguientes recursos para ayudarlo a administrar las cargas de trabajo que cambie a Intune:
- [Directivas de cumplimiento de dispositivos](https://docs.microsoft.com/intune/device-compliance-get-started)
- [Directivas de acceso a recursos](https://docs.microsoft.com/intune/device-profiles)
- [Directivas de Windows Update para empresas](https://docs.microsoft.com/intune/windows-update-for-business-configure)
