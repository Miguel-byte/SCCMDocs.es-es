---
title: Habilitación de la administración conjunta
titleSuffix: Configuration Manager
description: Habilite rápidamente la administración conjunta en Configuration Manager para obtener un valor inmediato.
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 8fac7ac5-96a3-4ec1-85cb-623b26bf5b1c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 37dce37551627394da2630fa591a3c803ae8343f
ms.sourcegitcommit: 9aebc20b25cdef0af908918ccfd791f3264a5d94
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "56755599"
---
# <a name="how-to-enable-co-management-in-configuration-manager"></a>Habilitación de la administración conjunta en Configuration Manager

Cuando habilite la administración conjunta, puede obtener un valor inmediato. Una vez que esté listo, puede empezar la transición de cargas de trabajo según sea necesario en el entorno.

Asegúrese de que los requisitos previos de la administración conjunta estén configurados antes de iniciar este proceso. Para obtener más información, consulte [Requisitos previos](/sccm/comanage/overview#prerequisites).



## <a name="process"></a>Proceso

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Servicios en la nube** y seleccione el nodo **Administración conjunta**. Haga clic en **Configurar administración conjunta** en la cinta para abrir el **Asistente para incorporación de la administración conjunta**.  

2. En la página **Suscripción** del asistente, seleccione **Iniciar sesión**. Inicie sesión en su inquilino de Intune y después haga clic en **Siguiente**.  

3. En la página **Habilitación**, elija la opción **Inscripción automática en Intune**, ya sea **Piloto** o **Todo**.   

    Esta acción permite la inscripción automática de clientes en Intune para los clientes existentes de Configuration Manager. Si elige **Piloto**, solo los clientes de Configuration Manager que sean miembros de la colección piloto se inscribirán de forma automática en Intune. Esta opción permite habilitar la administración conjunta en un subconjunto de los clientes para probarla inicialmente e implementarla con un enfoque por fases.  

    > [!Note]  
    > A partir de la versión 1806, la inscripción automática no es inmediata para todos los clientes. Este comportamiento ayuda a escalar la inscripción mejor para entornos de gran tamaño. Configuration Manager aleatoriza la inscripción según el número de clientes. Por ejemplo, si el entorno tiene 100 000 clientes, cuando se habilita esta configuración, la inscripción tiene lugar durante varios días.<!--1358003-->  

    Si tiene dispositivos de Internet ya inscritos en Intune, copie la línea de comandos en esta página. Puede usar esta línea de comandos para instalar el cliente de Configuration Manager como aplicación en Intune.

4. En la página **Cargas de trabajo**, elija para cada carga de trabajo el grupo de dispositivos que quiere pasar a la administración con Intune. Para más información, consulte [Cargas de trabajo](/sccm/comanage/workloads).  

    Si solo quiere habilitar la administración conjunta, no es necesario que cambie ahora las cargas de trabajo. Puede cambiarlas más adelante. Para más información, consulte el artículo sobre el [cambio de las cargas de trabajo](/sccm/comanage/how-to-switch-workloads).  

    El valor **Intune piloto** cambia la carga de trabajo asociada solo para los dispositivos de la colección Piloto. La configuración **Intune** cambia la carga de trabajo asociada para todos los dispositivos Windows 10 administrados conjuntamente.  

    > [!Important] 
    > Antes de cambiar las cargas de trabajo, asegúrese de que la carga de trabajo correspondiente en Intune se configuró e implementó correctamente. Asegúrese de que las cargas de trabajo siempre se administren mediante una de las herramientas de administración para los dispositivos.  

5. En la página **Almacenamiento provisional**, configure estas opciones:  

    - **Piloto**: el grupo piloto contiene una o varias colecciones que seleccione. Use este grupo como parte de la implementación por fases de la administración conjunta. Comience con una colección de prueba pequeña y, luego, agregue más colecciones al grupo piloto a medida que implemente la administración conjunta en más usuarios y dispositivos. Puede cambiar las colecciones del grupo piloto en cualquier momento.  

    - **Production**: Configure el **grupo de exclusión** con una o varias colecciones. Los dispositivos que forman parte de cualquiera de las colecciones de este grupo se excluyen del uso de la administración conjunta.  

6. Para habilitar la administración conjunta, siga los pasos del asistente.  



## <a name="next-steps"></a>Pasos siguientes

Ahora que habilitó la administración conjunta, consulte estos artículos para conocer el valor inmediato que puede obtener en el entorno:

- [Acceso condicional](/sccm/comanage/quickstart-conditional-access)  

- [Acciones remotas de Intune](/sccm/comanage/quickstart-remote-actions)  

- [Estado de cliente](/sccm/comanage/quickstart-client-health)  
