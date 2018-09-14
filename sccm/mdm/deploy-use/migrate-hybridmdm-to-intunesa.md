---
title: Migración de recursos de MDM híbrida a Intune independiente
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo migrar dispositivos y usuarios de MDM híbrida a Intune en Azure.
author: aczechowski
manager: dougeby
ms.date: 08/14/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: 1dd696ce-3e46-4dfa-a76d-592fe0f0320e
ms.openlocfilehash: cff1a695f3f3227f7ec849b34b75762b082c3f31
ms.sourcegitcommit: 98c3f7848dc9014de05541aefa09f36d49174784
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/14/2018
ms.locfileid: "42584439"
---
# <a name="migrate-hybrid-mdm-users-and-devices-to-intune-standalone"></a>Migración de dispositivos y usuarios de MDM híbrida a Intune independiente

*Se aplica a: System Center Configuration Manager (Rama actual)*    

Este artículo trata sobre la migración de MDM híbrida a una experiencia solo en la nube mediante Intune en Azure. 

> [!Important]  
> Desde el 14 de agosto de 2018, la administración híbrida de dispositivos móviles es una [característica en desuso](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). Para más información, vea [¿Qué es la Administración híbrida de dispositivos móviles (MDM)?](/sccm/mdm/understand/hybrid-mobile-device-management). <!--Intune feature 2683117-->  


Inicie la migración a Intune independiente siguiendo un enfoque por fases. De este modo, se prueba un pequeño subconjunto de usuarios y dispositivos mientras la mayoría de los usuarios y dispositivos se siguen administrando con MDM híbrida. Después de comprobar la funcionalidad de Intune, empiece a migrar más recursos a Intune.    

Vea los siguientes artículos para más información:    
  
1.  [Importar datos de Configuration Manager a Microsoft Intune](migrate-import-data.md)   

    La herramienta Intune Data Importer:  

    - Recopila datos sobre los objetos seleccionados de la jerarquía de Configuration Manager.  

    - Proporciona detalles acerca de los objetos que puede seleccionar para la importación   

    - Proporciona información sobre por qué no se pueden importar determinados objetos  

    - Le permite importar los objetos seleccionados en el inquilino de Microsoft Intune  

    Este paso es opcional. Puede ahorrarse mucho tiempo gracias a la automatización del proceso de volver a crear los objetos de Configuration Manager en Intune.  

2.  [Preparar Intune para la migración de usuarios](migrate-prepare-intune.md)    

    - Validar los objetos importados desde Configuration Manager  

    - Crear nuevos objetos  

    - Crear grupos de Azure AD y realizar las asignaciones de objetos a estos grupos  

    - Instalar NDES y conectores de Exchange  

    Cuando complete estos pasos e inicie la migración a Intune independiente, el proceso debería ser transparente para los usuarios.   

3.  [Cambiar la entidad de MDM para usuarios específicos (entidad de MDM mixta)](migrate-mixed-authority.md)    

    Configure una entidad de MDM mixta en el mismo inquilino. Seleccione algunos usuarios para que se administren en Intune, sin dejar de administrar el resto de dispositivos con MDM híbrida. Pruebe que la funcionalidad de Intune funcione en los dispositivos con un pequeño subconjunto de usuarios antes de iniciar la migración de más usuarios.   

4.  [Cambio de la entidad de MDM a Intune independiente](change-mdm-authority.md)     

    Cambie a la entidad de MDM de inquilino de Configuration Manager a Intune. El resto de los usuarios y dispositivos se migran a Intune independiente. Una vez que haya probado exhaustivamente la funcionalidad de Intune en el paso anterior y migrado la mayoría de los usuarios o todos ellos, ya podrá cambiar la entidad de MDM de inquilino.



## <a name="request-assistance"></a>Solicitar asistencia
<!--Intune bug 2339232--> Para solicitar asistencia desde el programa Microsoft FastTrack, empiece por visitar [FastTrack para Microsoft 365](https://fasttrack.microsoft.com/microsoft365/capabilities?view=security).

1. Haga clic en "Iniciar sesión" y escriba su identificador de organización.  

2. Vaya al Panel y siga las indicaciones para acceder al formulario de **solicitud de asistencia**.    

3. Microsoft revisa la solicitud y la enruta al equipo adecuado para tratar sus necesidades específicas y la idoneidad.  

Este panel contiene también procedimientos recomendados, herramientas y recursos de los expertos de FastTrack que le ayudarán a que su experiencia de Microsoft Cloud sea excelente.

