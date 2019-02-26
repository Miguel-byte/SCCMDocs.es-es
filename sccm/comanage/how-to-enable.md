---
title: Habilitación de la administración conjunta
titleSuffix: Configuration Manager
description: Habilitar rápidamente la administración conjunta en Configuration Manager para obtener el valor inmediato.
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
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56755599"
---
# <a name="how-to-enable-co-management-in-configuration-manager"></a>Cómo habilitar la administración conjunta en Configuration Manager

Al habilitar la administración conjunta, puede obtener el valor inmediato. A continuación, cuando esté listo, puede iniciar la transición de las cargas de trabajo según sea necesario en su entorno.

Asegúrese de que se configuran los requisitos previos de administración conjunta antes de iniciar este proceso. Para obtener más información, consulte [Requisitos previos](/sccm/comanage/overview#prerequisites).



## <a name="process"></a>Proceso

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Servicios en la nube** y seleccione el nodo **Administración conjunta**. Haga clic en **Configurar administración conjunta** en la cinta para abrir el **Asistente para incorporación de la administración conjunta**.  

2. En el **suscripción** página del asistente, seleccione **sesión**. Inicie sesión en su inquilino de Intune y después haga clic en **Siguiente**.  

3. En el **habilitación** página, elija su **la inscripción automática en Intune** establecer, ya sea **piloto** o **todas**.   

    Esta acción permite la inscripción de cliente automática en Intune para los clientes de Configuration Manager existentes. Si elige **Piloto**, solo los clientes de Configuration Manager que sean miembros de la colección piloto se inscribirán de forma automática en Intune. Esta opción permite habilitar la administración conjunta en un subconjunto de los clientes para probarla inicialmente e implementarla con un enfoque por fases.  

    > [!Note]  
    > A partir de la versión 1806, la inscripción automática no es inmediata para todos los clientes. Este comportamiento ayuda a escalar la inscripción mejor para entornos de gran tamaño. Configuration Manager aleatoriza la inscripción según el número de clientes. Por ejemplo, si el entorno tiene 100 000 clientes, cuando se habilita esta configuración, la inscripción tiene lugar durante varios días.<!--1358003-->  

    Si tiene dispositivos basados en internet que ya estén inscritos en Intune, copie la línea de comandos en esta página. Puede usar esta línea de comandos para instalar al cliente de Configuration Manager como una aplicación en Intune.

4. En la página **Cargas de trabajo**, elija para cada carga de trabajo el grupo de dispositivos que quiere pasar a la administración con Intune. Para obtener más información, consulte [cargas de trabajo](/sccm/comanage/workloads).  

    Si solo desea habilitar la administración conjunta, no es necesario cambiar las cargas de trabajo ahora. Puede cambiar las cargas de trabajo más adelante. Para obtener más información, consulte [cómo cambiar las cargas de trabajo](/sccm/comanage/how-to-switch-workloads).  

    El valor **Intune piloto** cambia la carga de trabajo asociada solo para los dispositivos de la colección Piloto. La configuración **Intune** cambia la carga de trabajo asociada para todos los dispositivos Windows 10 administrados conjuntamente.  

    > [!Important] 
    > Antes de cambiar las cargas de trabajo, asegúrese de que configure correctamente y distribuir la carga de trabajo correspondiente en Intune. Asegúrese de que las cargas de trabajo siempre se administren mediante una de las herramientas de administración para los dispositivos.  

5. En el **ensayo** página, configure las opciones siguientes:  

    - **Piloto**: el grupo piloto contiene una o varias colecciones que seleccione. Use este grupo como parte de la implementación por fases de la administración conjunta. Comience con una colección de prueba pequeña y, luego, agregue más colecciones al grupo piloto a medida que implemente la administración conjunta en más usuarios y dispositivos. Puede cambiar las colecciones del grupo piloto en cualquier momento.  

    - **Production**: Configure el **grupo de exclusión** con una o varias colecciones. Los dispositivos que forman parte de cualquiera de las colecciones de este grupo se excluyen del uso de la administración conjunta.  

6. Para habilitar la administración conjunta, siga los pasos del asistente.  



## <a name="next-steps"></a>Pasos siguientes

Ahora que ha habilitado la administración conjunta, mire los artículos siguientes para el valor inmediato, puede obtener en su entorno:

- [Acceso condicional](/sccm/comanage/quickstart-conditional-access)  

- [Acciones remotas de Intune](/sccm/comanage/quickstart-remote-actions)  

- [Estado de cliente](/sccm/comanage/quickstart-client-health)  
