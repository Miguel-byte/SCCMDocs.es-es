---
title: "Cambio de la entidad de MDM para usuarios específicos (entidad de MDM mixta)"
titleSuffix: Configuration Manager
description: "Aprenda a cambiar la entidad de MDM de MDM híbrida a Intune independiente para algunos usuarios."
keywords: 
author: dougeby
manager: dougeby
ms.date: 09/14/2017
ms.topic: article
ms.prod: configmgr-hybrid
ms.service: 
ms.technology: 
ms.assetid: 6f0201d7-5714-4ba0-b2bf-d1acd0203e9a
ms.openlocfilehash: 31d1d84c225d041f644669f0d3279e6bcd3f75ba
ms.sourcegitcommit: 986fc2d54f7c5fa965fd4df42f4db4ecce6b79cb
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="change-the-mdm-authority-for-specific-users-mixed-mdm-authority"></a>Cambio de la entidad de MDM para usuarios específicos (entidad de MDM mixta) 

*Se aplica a: System Center Configuration Manager (Rama actual)*    

Puede configurar una entidad de MDM mixta en el mismo inquilino seleccionando algunos usuarios para administrarse en Intune y otros para administrarse con MDM híbrida (Intune integrado con Configuration Manager). En este tema se proporciona información sobre cómo comenzar a mover los usuarios a Intune independiente y se da por supuesto que ha completado los pasos siguientes:
- Se ha usado la herramienta de importación de datos para [importar objetos de Configuration Manager en Intune](migrate-import-data.md) (opcional).
- [Se ha preparado Intune para la migración de usuario](migrate-prepare-intune.md) para asegurarse de que los usuarios y sus dispositivos continúan siendo administrados después de la migración.

> [!Note]    
> Si decide que desea realizar un restablecimiento completo del inquilino (lo que eliminará todas las directivas, aplicaciones e inscripciones de dispositivos), llame al servicio de soporte técnico para obtener ayuda.

Los usuarios migrados y sus dispositivos se administrarán en Intune, y otros dispositivos seguirán administrándose en Configuration Manager. Empezará con un grupo de prueba pequeño de usuarios para comprobar que todo funciona según lo previsto. Después, migrará gradualmente más grupos de usuarios hasta que esté listo para cambiar la entidad de MDM de inquilino de Configuration Manager a Intune independiente. 

## <a name="things-to-know-before-you-migrate-users"></a>Aspectos que debe conocer antes de migrar usuarios
- Durante la migración por fases, las aplicaciones o directivas de MDM de Configuration Manager existentes continuarán aplicándose a dispositivos de MDM híbrida.
- Los usuarios se agregan a un grupo de AAD que se designa como el grupo de migración. Todos los dispositivos asociados a los usuarios del grupo de migración se administran en Intune.
- Si los dispositivos se agregan al grupo de AAD, se omiten, salvo que sea un dispositivo sin ningún usuario asociado.
- Los usuarios que no están en un grupo de AAD marcado para la migración automáticamente heredan la entidad de MDM de inquilino (Configuration Manager).
- Al migrar un usuario a Intune, los usuarios y dispositivos aparecerán en el portal de Azure en Intune después de unos 15 minutos.  
- Al migrar los usuarios a Intune independiente, continúe para administrar la siguiente configuración de Configuration Manager en los dispositivos de MDM híbrida y de Intune independiente:
    - [Certificado de Apple Push Notification Service (APN)](/sccm/mdm/deploy-use/enroll-hybrid-ios-mac)
    - [Programa de inscripción de dispositivos](/sccm/mdm/deploy-use/ios-device-enrollment-program-for-hybrid)
    - Perfiles de inscripción
    - [Licencias del Programa de Compras por Volumen (VPP)](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps)
    - Identificadores corporativos 
    - [Certificados de firma de código](/sccm/mdm/deploy-use/enroll-hybrid-windows)
    - [Categorías de dispositivos](/sccm/core/clients/manage/collections/automatically-categorize-devices-into-collections)
    - [Administradores de inscripción](/sccm/mdm/plan-design/device-enrollment-methods)
    - Terms and conditions
    - Archivos SLK de Windows
    - Personalización de marca del Portal de empresa    
      
> [!Important]    
  > Continúe para editar las directivas de inquilino mediante la consola de Configuration Manager. Después de [cambiar la entidad de MDM de inquilino](change-mdm-authority.md) a Intune, administrará estas directivas en Intune en Azure. 
- Se recomienda no migrar las cuentas de usuario que se han agregado como administradores de inscripción de dispositivos en Configuration Manager. Más adelante, cuando cambie su entidad de MDM de inquilino a Intune, estas cuentas de usuario se migrarán correctamente. Si migra la cuenta de usuario de administrador de inscripción de dispositivos antes del cambio de entidad MDM de inquilino, tendrá que agregar manualmente el usuario como un administrador de inscripción de dispositivos de Intune en Azure. Sin embargo, los dispositivos inscritos mediante el uso de un administrador de inscripción de dispositivos no se migran correctamente. Debe llamar al servicio de soporte técnico para migrar estos dispositivos. Para obtener más información, consulte [Adición de un administrador de inscripción de dispositivos](https://docs.microsoft.com/en-us/intune/device-enrollment-manager-enroll#add-a-device-enrollment-manager).
- Los dispositivos inscritos mediante un administrador de inscripción de dispositivos y los dispositivos que no tienen usuarios asociados no se migran a la nueva entidad de MDM. Para estos dispositivos, debe llamar al servicio de soporte técnico para ayudarlo con dispositivos específicos. Para los que no tengan soporte técnico, ejecute un restablecimiento de la entidad MDM o limpie los datos en Intune. Debe [cambiar la entidad de MDM](migrate-change-mdm-authority.md) desde la consola de Configuration Manager.

## <a name="migrate-users-to-intune"></a>Migración de usuarios a Intune
Para comprobar que las configuraciones de Intune funcionan según lo esperado, migre primero un pequeño conjunto de usuarios y sus dispositivos. Después de confirmar que todo funciona según lo previsto, puede iniciar la migración de más grupos de AAD con más usuarios y sus dispositivos.

## <a name="migrate-a-test-group-of-users-to-intune-standalone"></a>Migración de un grupo de prueba de usuarios a Intune independiente
Los dispositivos de los usuarios de la recopilación asociada con la suscripción de Intune pueden inscribirse en MDM híbrida. Cuando se quita un usuario de la recopilación, se migran los dispositivos inscritos en Intune independiente si el usuario tiene una licencia de Intune asignada. Si aún no ha asignado licencias a los usuarios que tiene previsto migrar, vea [Asignación de licencias de Intune a las cuentas de usuario](https://docs.microsoft.com/intune/licenses-assign). En la recopilación de la suscripción de Intune, puede excluir recopilaciones de usuarios de su principal para migrar los usuarios de la excluida. 

En el ejemplo siguiente, la recopilación de usuarios Híbrido contiene todos los miembros de la recopilación Todos los usuarios. De este modo, cualquier usuario puede inscribir un dispositivo en MDM híbrida. Para migrar usuarios a Intune independiente, seleccione Excluir recopilaciones y agregue una recopilación con los usuarios para migrar. Cuando esté listo para migrar más usuarios, puede agregar más recopilaciones excluidas que incluyan esos usuarios. 

![Recopilaciones excluidas](../media/migrate-excludecollections.png)

> [!Note] 
> Cuando tenga seleccionada la recopilación **Todos los usuarios** para la suscripción de Intune, no podrá agregar una regla que excluya las recopilaciones. Cree una nueva recopilación basada en la llamada **Todos los usuarios**, compruebe que contiene los usuarios que se esperaba y, luego, edite la suscripción de Intune para usar la nueva recopilación. Puede excluir recopilaciones de usuarios de la nueva recopilación para migrar usuarios. 

Para migrar un grupo de prueba de usuarios a Intune, cree una recopilación de usuarios que contenga los usuarios para migrar y, luego, excluya la recopilación de usuarios de la utilizada para la suscripción de Intune.   

En el siguiente diagrama se proporciona una introducción sobre el funcionamiento de la migración de usuarios.

 ![Introducción a la entidad mixta](../media/migrate-mixedauthority.svg)

1. Compruebe que el usuario tiene una licencia de Intune o EMS. 
2. Cree una recopilación para que se excluya de la de la suscripción de Intune. En este ejemplo, la recopilación **All Hybrid users** (Todos los usuarios de Híbrido) contiene una regla para excluir los usuarios de la recopilación **Migration pilot** (Piloto de migración). **User1** es un miembro de la recopilación **Migration pilot** (Piloto de migración) y se excluye la recopilación **All Hybrid users** (Todos los usuarios de Híbrido). 
3. Los dispositivos de **User1** ahora se administran desde Intune en Azure Portal. 
4. El resto de los dispositivos se siguen administrando desde la consola de Configuration Manager. 

## <a name="verify-intune-standalone-functionality"></a>Comprobación de la funcionalidad independiente de Intune
Después de migrar un pequeño conjunto de usuarios, compruebe que los dispositivos del usuario aparecen en Intune. Vaya a la hoja **Dispositivos** y seleccione **Todos los dispositivos**. 

Después, compruebe que sus directivas, perfiles, aplicaciones, etc., funcionen según lo previsto en los dispositivos de usuario.

## <a name="migrate-additional-users"></a>Migración de más usuarios
Una vez que haya comprobado que Intune independiente funciona como esperaba, puede iniciar la migración de más usuarios. Como ha creado una recopilación con un conjunto de usuarios de prueba, cree recopilaciones que contengan los usuarios para migrar y excluya las de la recopilación asociada con la suscripción a Intune. Para obtener más información, consulte el artículo sobre la [recopilación asociada a su suscripción a Intune](#collection-associated-with-your-intune-subscription).

## <a name="next-steps"></a>Pasos siguientes
Después de haber migrado los usuarios y probado la funcionalidad de Intune, compruebe si está listo para [cambiar la entidad de MDM](migrate-change-mdm-authority.md) de su inquilino de Intune desde Configuration Manager en Intune. 