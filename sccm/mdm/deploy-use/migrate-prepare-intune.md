---
title: Preparación de Intune para la migración de usuarios
titleSuffix: Configuration Manager
description: Aprenda a preparar Intune en Azure para migrar usuarios desde MDM híbrida.
keywords: ''
author: dougeby
manager: dougeby
ms.date: 12/05/2017
ms.topic: article
ms.prod: configmgr-hybrid
ms.service: ''
ms.technology: ''
ms.assetid: db97ae9e-34f4-4e10-a282-cd211f612bb4
ms.openlocfilehash: 8d636f2c46f3fa14fbc76a605d2cf55a2c0375c6
ms.sourcegitcommit: fb84bcb31d825f454785e3d9d8be669e00fe2b27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="prepare-intune-for-user-migration"></a>Preparación de Intune para la migración de usuarios 

*Se aplica a: System Center Configuration Manager (Rama actual)*    

Antes de migrar usuarios de MDM híbrida (Intune integrado con Configuration Manager) a Intune independiente, debe realizar algunos pasos para preparar Intune. Estos pasos ayudan a garantizar que los usuarios migrados y sus dispositivos siguen administrándose. Cuando complete estos pasos e inicie la migración a Intune, el proceso debería ser transparente para los usuarios.  

## <a name="fix-issues-found-during-data-collection-and-import"></a>Corrección de problemas encontrados durante la importación y la recopilación de datos
Si ha completado el proceso de [importar datos de Configuration Manager en Microsoft Intune](migrate-import-data.md), la herramienta Intune Data Importer proporciona un resumen de todos los objetos que no se pudieron importar. Algunos de los problemas típicos que es probable que se encuentre, así como los pasos que puede seguir para corregir el problema en Intune, se muestran en la tabla siguiente: 

|Problema  |Solución  |
|---------|---------|
|Las recopilaciones complejas o basadas en la pertenencia directa no se migran automáticamente.|Debe crear grupos de Azure Active Directory (AAD) en Azure para reemplazar la recopilación que no se importó. Después, debe asignar el objeto al grupo.|
|Las directivas no se pudieron importar. |Debe volver a crear la directiva en Intune.|
|La implementación de un objeto no importado.|El objeto se debe asignar al grupo. El grupo debe contener los mismos usuarios de la recopilación de la implementación.|

## <a name="create-intune-objects"></a>Creación de objetos de Intune 
Si ha completado el proceso de [importar datos de Configuration Manager en Microsoft Intune](migrate-import-data.md) y ha corregido problemas durante el proceso de importación, debe comprobar que los objetos importados están configurados correctamente. Además, crear más objetos que necesite en su organización (directivas, perfiles, aplicaciones, etc.) en Intune. 

## <a name="assign-intune-licenses-to-migrated-users"></a>Asignación de licencias de Intune a los usuarios migrados
En Configuration Manager, agregue una recopilación a la suscripción de Intune; los miembros de dicha recopilación podrán inscribir sus dispositivos. Aunque se haya reservado una licencia de Intune para los dispositivos inscritos, no están específicamente asociadas con el usuario o dispositivo. Por ejemplo, no encontraría una licencia de Intune en AAD correspondiente a un usuario que tenga un dispositivo inscrito. Sin embargo, en Intune independiente debe configurar una licencia de Intune para cada usuario. Debe hacerlo ANTES de migrar un usuario a Intune independiente para garantizar que ese usuario y sus dispositivos se administren mediante Intune tras el cambio en la entidad de MDM. Para obtener más información, consulte [Assign Intune licenses to your user accounts](https://docs.microsoft.com/intune/licenses-assign) (Asignar licencias de Intune a sus cuentas de usuario). 

## <a name="verify-intune-user-groups"></a>Comprobación de los grupos de usuarios de Intune
Es probable que los usuarios y grupos ya se encuentran en AAD si tiene configurada la sincronización de directorios. Para asegurarse de que los usuarios forman parte del grupo de usuarios correcto, se recomienda revisar los grupos de usuarios de Intune. Destine directivas, perfiles, aplicaciones, etc., a estos grupos. Asegúrese de que los usuarios que migre a Intune independiente formen parte de los grupos correctos. 

## <a name="configure-role-based-administration-control-rbac"></a>Configuración del control de administración basada en roles (RBAC)
Como parte de la migración, configure todos los roles RBAC en Intune y asigne usuarios a esos roles. Tenga en cuenta que existen diferencias entre RBAC en Configuration Manager e Intune, por ejemplo, el ámbito de los recursos. Para obtener más información, consulte [Control de administración basada en roles (RBAC) con Intune](https://docs.microsoft.com/intune/role-based-access-control).

## <a name="assign-apps-and-policies-to-aad-groups"></a>Asignación de aplicaciones y directivas a grupos de AAD
Si ha completado la fase [Importación de datos de Configuration Manager en Microsoft Intune](migrate-import-data.md) del proceso de migración para migrar diferentes objetos de Configuration Manager en Intune, muchos de los objetos ya podrían estar asignados a grupos de AAD. Sin embargo, debe comprobar que todos los objetos (aplicaciones, directivas, perfiles, etc.) están asignados a los grupos de AAD correctos. Si asigna los objetos correctamente, los dispositivos del usuario se configuran automáticamente después de migrar el usuario; el proceso de migración debería ser transparente para los usuarios. Para obtener más información sobre la asignación de objetos a un grupo de AAD, consulte lo siguiente: 
- [Asignación de directivas](https://docs.microsoft.com/intune/get-started-policies) 
- [Asignación de perfiles](https://docs.microsoft.com/intune/device-profile-assign) 
- [Asignación de aplicaciones](https://docs.microsoft.com/intune/get-started-apps) 

## <a name="terms-and-conditions-policy"></a>Directiva de términos y condiciones
Al igual que con otras directivas de inquilino, las de términos y condiciones se migran automáticamente a Intune una vez habilitada la entidad mixta para su inquilino.  Sin embargo, debe asignar los términos y condiciones a un grupo que contenga usuarios migrados para informar con precisión de la aceptación de los usuarios migrados, así como garantizar que se seleccionen correctamente los términos y condiciones para futuras actualizaciones de términos y condiciones o inscripciones de dispositivos. Los usuarios no tienen que volver a aceptar los términos y condiciones, a menos que haya cambios realizados en la directiva en la consola de Configuration Manager. Para obtener más información, consulte [Asignación de los términos y condiciones](https://docs.microsoft.com/intune/terms-and-conditions-create#assign-terms-and-conditions).

## <a name="configure-the-exchange-connector"></a>Configuración de Exchange Connector
Si usa Exchange y tiene una instancia de Exchange Connector local en Configuration Manager, debe [configurar la instancia de Exchange Connector local en Intune](https://docs.microsoft.com/intune/exchange-connector-install). También tenga en cuenta la información de las secciones siguientes para ayudarle a migrar a Intune Exchange Connector y para asegurarse de que el acceso condicional funciona correctamente después de la migración.

### <a name="powershell-scripts-to-help-you-migrate-to-the-intune-exchange-connector"></a>Scripts de PowerShell para ayudarle a migrar a Intune Exchange Connector 
Los scripts de PowerShell están disponibles para ayudarle a prepararse para la transición de sus dispositivos Exchange de Configuration Manager Exchange Connector a Intune Exchange Connector. Aunque la ejecución de estos scripts es opcional, es recomendable ejecutarlos para quitar dispositivos inactivos de Exchange, lo que impide que Intune detecte dispositivos innecesarios. La ejecución de scripts garantiza que los dispositivos detectados a través de Exchange se puedan combinar con los dispositivos inscritos con Intune con la mayor fluidez posible. Ejecute estos scripts antes de configurar Intune Exchange Connector. Los scripts de PowerShell forman parte de la instalación de Intune Data Importer que se usa para [importar datos de Configuration Manager a Microsoft Intune](migrate-import-data.md) en el artículo siguiente. Para más información y descargar los scripts, vaya a la página de GitHub [Microsoft Intune Data Importer](https://github.com/ConfigMgrTools/Intune-Data-Importer).

### <a name="steps-to-ensure-conditional-access-works-properly-after-user-migration"></a>Pasos para garantizar que el acceso condicional funciona correctamente después de la migración de usuarios
Para que el acceso condicional funcione correctamente después de migrar usuarios y para garantizar que los usuarios sigan teniendo acceso a su servidor de correo electrónico, asegúrese de que se cumpla la siguiente condición:
- Si se establece la configuración de nivel de acceso predeterminado de Exchange ActiveSync (DefaultAccessLevel) en Bloquear y Cuarentena, los dispositivos podrían perder el acceso al correo electrónico. 
- Si Exchange Connector está instalado en Configuration Manager y el **nivel de acceso cuando un dispositivo móvil no está administrado por una configuración de regla** tiene un valor de **Permitir acceso**, debe instalar el [conector de Exchange local en Intune](https://docs.microsoft.com/intune/conditional-access-exchange-create#configure-exchange-on-premises-access) antes de migrar los usuarios. Configure el nivel de acceso predeterminado en Intune en la hoja **Exchange local** de **Configuración avanzada de acceso a Exchange ActiveSync**. Para obtener más información, consulte [Configuración del acceso a Exchange local](https://docs.microsoft.com/intune/conditional-access-exchange-create#configure-exchange-on-premises-access).
- Utilice la misma configuración para ambos conectores. El último conector que configure sobrescribe la configuración de la organización de ActiveSync escrita previamente por el otro conector. Si configura los conectores de manera diferente, podrían producirse cambios inesperados en el acceso condicional.
- Quite usuarios del acceso condicional estableciendo destinos en Configuration Manager una vez que se migran a Intune independiente.

## <a name="configure-the-microsoft-intune-certificate-connector"></a>Configuración de Microsoft Intune Certificate Connector
Si usa NDES para emitir certificados mediante SCEP, debe configurar Microsoft Intune Certificate Connector. El equipo que hospeda el conector de NDES en Intune no puede ser el mismo equipo que hospeda el conector de NDES en Configuration Manager. Para obtener más información, consulte [Configuración y administración de certificados SCEP con Intune](https://docs.microsoft.com/en-us/intune/certificates-scep-configure). 

> [!Important]    
> Después de configurar el conector, debe modificar los perfiles SCEP importados para hacer referencia a la nueva dirección URL del servidor.

## <a name="next-step"></a>Paso siguiente
Después de preparar Intune para la migración, está listo para migrar un conjunto de usuarios de prueba a Intune independiente. Para obtener más información, consulte [Cambio de la entidad de MDM para usuarios específicos (entidad de MDM mixta)](migrate-mixed-authority.md).


