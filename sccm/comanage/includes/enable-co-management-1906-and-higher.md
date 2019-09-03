---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 08/23/2019
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4960c0b9a6c383a73766083a9e385bcd60d799d3
ms.sourcegitcommit: 04dd0c17e47763a3e2b6c44c005428ea7d67f4bd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/26/2019
ms.locfileid: "70036774"
---
<!--3555750 FKA 1357954 --Don't apply H2/H3 in this include file since they are context driven by article-->
1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Servicios en la nube** y seleccione el nodo **Administración conjunta**. Haga clic en **Configurar administración conjunta** en la cinta para abrir el **Asistente para la configuración de administración conjunta**.

2. En la página **Suscripción** del asistente, configure estas opciones:

    - El **entorno de Azure** que se va a usar. Por ejemplo, la nube pública de Azure o la nube de Azure US Government.<!--4075452-->  

    - Haga clic en **Iniciar sesión**. Inicie sesión en su inquilino de Intune y después haga clic en **Siguiente**.  

3. En la página **Habilitación**, elija estas opciones:

   - **Inscripción automática en Azure**: esta acción permite la inscripción automática de clientes en Intune para los clientes existentes de Configuration Manager. Esta opción permite habilitar la administración conjunta en un subconjunto de los clientes para probarla inicialmente e implementarla con un enfoque por fases. Si el usuario anula la inscripción de un dispositivo, se volverá a inscribir en la siguiente evaluación de la directiva. <!--3330596-->

      - **Piloto**: solo los clientes de Configuration Intune que sean miembros de la colección **Inscripción automática en Intune** se inscriben automáticamente en Intune.
      - **Todo**: permite la inscripción automática para todos los clientes de Windows 10, ya sea la versión 1709 o posterior.

   - **Inscripción automática en Intune**: esta colección debe contener todos los clientes que quiera incorporar a la administración conjunta. En esencia, se trata de un superconjunto de todas las demás colecciones de almacenamiento provisional.

   ![Especifique la colección de inscripción automática de Intune ](../media/3555750-co-management-onboarding-enablement.png)

      > [!Note]  
      > A partir de la versión 1806, la inscripción automática no es inmediata para todos los clientes. Este comportamiento ayuda a escalar la inscripción mejor para entornos de gran tamaño. Configuration Manager aleatoriza la inscripción según el número de clientes. Por ejemplo, si el entorno tiene 100 000 clientes, cuando se habilita esta configuración, la inscripción tiene lugar durante varios días.<!--1358003-->  
      >
      > A partir de la versión 1906:
      >
      > - Un nuevo dispositivo administrado de forma conjunta ahora se inscribe automáticamente en el servicio Microsoft Intune en función de su token de *dispositivo* de Azure Active Directory (Azure AD). No es necesario esperar a que un usuario inicie sesión en el dispositivo para iniciar la inscripción automática. Este cambio ayuda a reducir el número de dispositivos con el estado de inscripción *Inicio de sesión de usuario pendiente*.<!-- 4454491 --> Para admitir este comportamiento, el dispositivo debe ejecutar Windows 10, versión 1803 o posterior. Para más información, consulte [Estado de la inscripción de administración conjunta](/sccm/comanage/how-to-monitor#co-management-enrollment-status).
      >
      > - Si ya tiene dispositivos inscritos en la administración conjunta, los dispositivos nuevos ahora se inscriben de inmediato una vez que cumplen con los [requisitos previos](/sccm/comanage/overview#prerequisites).<!--4321130-->

4. En el caso de los dispositivos de Internet ya inscritos en Intune, copie y guarde la línea de comandos en la página **Habilitación**. Usará esta línea de comandos para instalar el cliente de Configuration Manager, así como una aplicación de Intune para los dispositivos de Internet. Si no guarda ahora esta línea de comandos, puede revisar la configuración de la administración conjunta en cualquier momento para obtener esta línea de comandos.

5. En la página **Cargas de trabajo**, elija para cada carga de trabajo el grupo de dispositivos que quiere pasar a la administración con Intune. Para más información, consulte [Cargas de trabajo](/sccm/comanage/workloads). Si solo quiere habilitar la administración conjunta, no es necesario que cambie ahora las cargas de trabajo. Puede cambiarlas más adelante. Para más información, consulte el artículo sobre el [cambio de las cargas de trabajo](/sccm/comanage/how-to-switch-workloads).  

    - **Intune piloto**: cambia la carga de trabajo asociada solo para los dispositivos de las colecciones piloto que especificará en la página **Almacenamiento provisional**. Cada carga de trabajo puede tener una colección piloto distinta.
    - **Intune**: cambia la carga de trabajo asociada para todos los dispositivos Windows 10 administrados conjuntamente.  

    > [!Important]
    > Antes de cambiar las cargas de trabajo, asegúrese de que la carga de trabajo correspondiente en Intune se configuró e implementó correctamente. Asegúrese de que las cargas de trabajo siempre se administren mediante una de las herramientas de administración para los dispositivos.  

6. En la página **Almacenamiento provisional**, especifique la colección piloto para cada una de las cargas de trabajo establecidas en **Intune piloto**.

   ![Especifique la colección de inscripción automática de Intune ](../media/3555750-co-management-onboarding-staging.png)

7. Para habilitar la administración conjunta, siga los pasos del asistente.
