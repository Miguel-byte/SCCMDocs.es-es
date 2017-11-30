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
ms.openlocfilehash: a6e430248fdeedd310087c9a32c6d69ca1864a09
ms.sourcegitcommit: 986fc2d54f7c5fa965fd4df42f4db4ecce6b79cb
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
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

<!--
The following provides a typical workflow for migrating users from hybrid MDM to Intune standalone:
1.  Admin runs the Microsoft Intune Data Importer Tool, selecting which objects and assignments to import. Selected objects are imported into Intune standalone.
    1. Some objects cannot be imported because they contain settings the tool does not understand or setting that are not available in Intune standalone.
    2. Assignments are migrated. However, only if the collection an object was targeted to is based on a single Active Directory (AD) security group and the same group exists in Azure Active Directory (AAD).
    > [!Note]    
    > If you want, you can skip this step and create the objects that you want directly in Intune in the Azure portal without running the Intune Data Importer Tool. 
2.  Admin logs into the Intune on Azure portal
    1. Creates any additional objects required for their organization that were not imported by the Microsoft Intune Data Importer tool.
    2. Creates any required AAD groups and makes any additional assignments for each object to AAD groups.
    3. Installs the NDES connector on an on-premises server if using SCEP or PFX certificate deployment.
    4. Installs the Exchange connector on an on-premises server if using conditional access. 
3.  Admin ensures that all existing Intune users in their organization have an Intune license assigned to them using AAD or the Office administrator portal.
4.  Admin selects some test users to migrate to Intune standalone and removes them from the collection associated with the Intune subscription in Configuration Manager.
5.  Once removed from the collection, the user and all devices are managed by Intune in the Azure portal. Remaining users and devices continue to be managed by hybrid mobile device management in Configuration Manager. 
6.  Admin validates that things are working as expected on the device and moves more users to Intune standalone by removing them from the collection associated with the Intune subscription in Configuration Manager.
7.  Once the admin is comfortable with the functionality in Intune standalone, they can move the rest of their users and devices by switching their MDM authority to Intune standalone. This can be done by removing the Intune subscription from SCCM and choosing to change the MDM authority. Tenant level policies will be automatically migrated to Intune standalone, all objects and assignments in Intune standalone will remain, and devices will not be required to re-enroll.
-->