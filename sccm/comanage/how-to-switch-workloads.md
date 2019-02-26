---
title: Cambiar las cargas de trabajo de administración conjunta
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo cambiar las cargas de trabajo que administra actualmente Configuration Manager a Microsoft Intune.
ms.prod: configuration-manager
ms.technology: configmgr-client
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 01/14/2019
ms.topic: conceptual
ms.assetid: 60e2022f-a4f9-40dd-af01-9ecb37b43878
ms.collection: M365-identity-device-management
ms.openlocfilehash: a4b50d0491644e6be0967c1adcf2db641c1bb1cd
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56755611"
---
# <a name="how-to-switch-configuration-manager-workloads-to-intune"></a>Cómo cambiar las cargas de trabajo de Configuration Manager a Intune

Una de las ventajas de la administración conjunta es cambiar las cargas de trabajo de Configuration Manager a Microsoft Intune. Cuando un dispositivo Windows 10 tiene el cliente de Configuration Manager y se inscribe en Intune, obtenga las ventajas de ambos servicios. Controlar qué cargas de trabajo, si existe, que cambia la entidad de Configuration Manager a Intune. Configuration Manager sigue administrando todas las otras cargas de trabajo, incluidas las cargas de trabajo que no cambie a Intune y no es compatible con todas las demás características de Configuration Manager que la administración conjunta.

Para obtener más información sobre las cargas de trabajo compatibles, consulte [cargas de trabajo](/sccm/comanage/workloads).

Puede cambiar las cargas de trabajo cuando se habilita la administración conjunta o versiones posteriores cuando esté listo. Si ya no ha habilitado la administración conjunta, hágalo primero. Para obtener más información, consulte [cómo habilitar la administración conjunta](/sccm/comanage/how-to-enable).


Después de habilitar la administración conjunta, modifique la configuración en las propiedades de la administración conjunta. 

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Servicios en la nube** y seleccione el nodo **Administración conjunta**.  

2. Seleccione el objeto de administración conjunta y, a continuación, elija **propiedades** en la cinta de opciones.  

3. Cambie a la **cargas de trabajo** ficha. De forma predeterminada, todas las cargas de trabajo se establecen en el **Configuration Manager** configuración. Para cambiar una carga de trabajo, mueva el control deslizante para esa carga de trabajo a la configuración deseada.  

    ![Pestaña de captura de pantalla de cargas de trabajo en la página de propiedades de administración conjunta](media/properties-workloads.png)

    - **Administrador de configuración**: Configuration Manager sigue administrar esta carga de trabajo.  

    - **Definir un programa piloto de Intune**: Cambie esta carga de trabajo solo para los dispositivos en la recopilación piloto. Puede cambiar el **recopilación piloto** en el **ensayo** ficha de la página de propiedades de la administración conjunta.  

    - **Intune**: Cambie esta carga de trabajo para todos los dispositivos Windows 10 inscritos en administración conjunta.  


> [!Important]  
> Antes de cambiar las cargas de trabajo, asegúrese de que configure correctamente y distribuir la carga de trabajo correspondiente en Intune. Asegúrese de que las cargas de trabajo siempre se administren mediante una de las herramientas de administración para los dispositivos.  

<!--1357377--> A partir de la versión 1806 de Configuration Manager, cuando se cambia una carga de trabajo de administración compartida, los dispositivos administrados conjuntamente sincronizan automáticamente la directiva MDM de Microsoft Intune. Esta sincronización también se produce al iniciar la acción **Descargar directiva de equipo** desde Notificaciones de cliente en la consola de Configuration Manager. Para obtener más información, vea [Iniciar la recuperación de directivas de cliente mediante la notificación de cliente](/sccm/core/clients/manage/manage-clients#initiate-client-policy-retrieval-using-client-notification).


