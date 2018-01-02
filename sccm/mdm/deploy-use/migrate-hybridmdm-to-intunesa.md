---
title: "Migración de dispositivos y usuarios de MDM híbrida a Intune independiente"
titleSuffix: Configuration Manager
description: "Obtenga información sobre cómo migrar dispositivos y usuarios de MDM híbrida a Intune en Azure."
keywords: 
author: dougeby
manager: angrobe
ms.date: 09/12/2017
ms.topic: article
ms.prod: configmgr-hybrid
ms.service: 
ms.technology: 
ms.assetid: 1dd696ce-3e46-4dfa-a76d-592fe0f0320e
ms.openlocfilehash: 30474f6dd0216078ab1ac1f4bd9f5044f1b174f0
ms.sourcegitcommit: 8c6e9355846ff6a73c534c079e3cdae09cf13c45
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/06/2017
---
# <a name="migrate-hybrid-mdm-users-and-devices-to-intune-standalone"></a>Migración de dispositivos y usuarios de MDM híbrida a Intune independiente

*Se aplica a: System Center Configuration Manager (Rama actual)*    

Cuando haya decidido que está listo para empezar a realizar la migración desde MDM híbrida (Intune integrado con Configuration Manager) a una experiencia solo en la nube mediante Intune en Azure, este es el artículo que debe leer. Si sigue sin saberlo, consulte [Elegir entre Microsoft Intune independiente y administración de dispositivos móviles híbrida con System Center Configuration Manager](https://docs.microsoft.com/sccm/mdm/understand/choose-between-standalone-intune-and-hybrid-mobile-device-management). 

Puede iniciar la migración a Intune independiente siguiendo un método por fases que le permita probar un pequeño subconjunto de usuarios y dispositivos mientras la mayoría de los usuarios y dispositivos se siguen administrando con MDM híbrida. Después de comprobar la funcionalidad de Intune, puede comenzar a migrar más usuarios a Intune.    

En los temas siguientes se proporcionan los pasos para migrar usuarios a Intune independiente con un método por fases.    
  
1.  [Importación de datos de Configuration Manager en Microsoft Intune](migrate-import-data.md)   
    La herramienta Intune Data Importer recopila datos sobre los objetos seleccionados de la jerarquía de Configuration Manager, proporciona detalles sobre los objetos que puede seleccionar para la importación y detalles sobre por qué no se puede importar algún objeto, y permite importar los objetos seleccionados en el inquilino de Microsoft Intune. Aunque este paso es opcional, puede ahorrar mucho tiempo al automatizar el proceso de volver a crear los objetos de Configuration Manager en Intune. 
2.  [Preparación de Intune para la migración de usuarios](migrate-prepare-intune.md)    
    Valide los objetos importados desde Configuration Manager, cree objetos, genere grupos de AAD y realice las asignaciones de objetos a estos grupos, instale conectores de NDES y Exchange, etc. Cuando complete estos pasos e inicie la migración a Intune independiente, el proceso debería ser transparente para los usuarios.  
3.  [Cambio de la entidad de MDM para usuarios específicos (entidad de MDM mixta)](migrate-mixed-authority.md)    
    Configure una entidad de MDM mixta en el mismo inquilino seleccionando algunos usuarios para administrarse en Intune; el resto de los dispositivos seguirán administrándose con MDM híbrida (Intune integrado con Configuration Manager). Puede probar que la funcionalidad de Intune funciona según lo previsto en los dispositivos con un pequeño subconjunto de usuarios antes de iniciar la migración de más usuarios. 
4.  [Cambio de la entidad de MDM a Intune independiente](change-mdm-authority.md)     
    Cambie a la entidad de MDM de inquilino de Configuration Manager a Intune. El resto de los usuarios y dispositivos se migran a Intune independiente. Una vez que haya probado exhaustivamente la funcionalidad de Intune en el paso anterior y, probablemente, migrado la mayoría o todos los usuarios, ya podrá cambiar la entidad de MDM de inquilino.