---
title: Preparación de Intune para la migración de usuarios
titleSuffix: Configuration Manager
description: Aprenda a preparar Intune en Azure para migrar usuarios desde MDM híbrida.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 12/26/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: db97ae9e-34f4-4e10-a282-cd211f612bb4
ms.collection: M365-identity-device-management
ms.openlocfilehash: e217c7afc2910a23fe3f29fa215d58574f3d79d8
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56137820"
---
# <a name="prepare-intune-for-user-migration"></a>Preparación de Intune para la migración de usuarios 

*Se aplica a: System Center Configuration Manager (rama actual)*    
Antes de migrar los usuarios de MDM híbrida a Intune independiente, siga los pasos para preparar Intune. Estos pasos ayudan a asegurarse de que los usuarios migrados y sus dispositivos siguen administrándose. Cuando complete estos pasos e inicie la migración a Intune, no hay afectar significativamente a sus usuarios.  

## <a name="fix-issues-found-during-data-collection-and-import"></a>Corrección de problemas encontrados durante la importación y la recopilación de datos
Si ha usado la herramienta Intune Data Importer para [importar datos de Configuration Manager a Microsoft Intune](migrate-import-data.md), resumen los objetos no se pudo importar. Algunos de los problemas más frecuentes y pasos para corregirlos en Intune, se muestran en la tabla siguiente: 

|Problema  |Fix  |
|---------|---------|
|Colecciones basadas en la pertenencia directa o complejas no se migran automáticamente.|Crear grupos de Azure Active Directory (Azure AD) en Azure para reemplazar la colección que no se ha importado. A continuación, asigne el objeto al grupo.|
|No puede importables directivas |Vuelva a crear la directiva de Intune.|
|La implementación de un objeto no importado.|Asigne el objeto al grupo. El grupo debe incluir los mismos usuarios de la colección para la implementación.|

## <a name="create-intune-objects"></a>Creación de objetos de Intune 
Si se [importa datos de Configuration Manager a Microsoft Intune](migrate-import-data.md) y se ha corregido problemas durante el proceso, compruebe los objetos importados están configurados correctamente. También puede crear objetos adicionales (directivas, perfiles y aplicaciones) en Intune que necesite en su organización. 

## <a name="assign-intune-licenses-to-migrated-users"></a>Asignación de licencias de Intune a los usuarios migrados
En Configuration Manager, agregue una colección a la suscripción de Intune y los miembros de la colección pueden inscribir sus dispositivos. Mientras está reservada una licencia de Intune para dispositivos inscritos, estas licencias no están asociadas con el usuario o dispositivo. Por ejemplo, no encontraría una licencia de Intune en Azure AD para un usuario que tiene un dispositivo inscrito. 

En Intune independiente, configurar una licencia de Intune para cada usuario. Configura la licencia *antes* migrar un usuario a Intune independiente. Esta acción garantiza que el usuario y sus dispositivos se administran mediante Intune tras el cambio de entidad de MDM. Para obtener más información, consulte [Assign Intune licenses to your user accounts](https://docs.microsoft.com/intune/licenses-assign) (Asignar licencias de Intune a sus cuentas de usuario). 

## <a name="verify-intune-user-groups"></a>Comprobación de los grupos de usuarios de Intune
Los usuarios y grupos están probable que ya se encuentran en Azure AD porque tiene configurada la sincronización de directorios. Para asegurarse de que los usuarios forman parte del grupo de usuarios correcto, se recomienda revisar los grupos de usuarios de Intune. Destino directivas, perfiles y aplicaciones a estos grupos. Asegúrese de que los usuarios que migre a Intune independiente formen parte de los grupos correctos. 

## <a name="configure-role-based-administration-control-rbac"></a>Configuración del control de administración basada en roles (RBAC)
Como parte de la migración, configure todos los roles RBAC en Intune y asigne usuarios a esos roles. Hay diferencias entre RBAC en Configuration Manager e Intune, como el ámbito de los recursos. Para obtener más información, consulte [control de administración basada en roles (RBAC) con Intune](https://docs.microsoft.com/intune/role-based-access-control).

## <a name="assign-apps-and-policies-to-aad-groups"></a>Asignación de aplicaciones y directivas a grupos de AAD
Si se [importa datos de Configuration Manager a Microsoft Intune](migrate-import-data.md), muchos de los objetos ya podrían estar asignados a grupos de Azure AD. Compruebe que todos los objetos (aplicaciones, directivas y perfiles) se asignan a la correcta grupos de Azure AD. Si asigna objetos correctamente, los dispositivos del usuario se configuran automáticamente después de migrar el usuario y la migración no deben afectar significativamente a los usuarios. Para obtener más información sobre la asignación de los objetos a un grupo de Azure AD, consulte los artículos siguientes: 
- [Asignación de directivas](https://docs.microsoft.com/intune/get-started-policies)  
- [Asignación de perfiles](https://docs.microsoft.com/intune/device-profile-assign)  
    > [!NOTE]  
    > Cuando Intune implementa el nuevo perfil de correo electrónico, los usuarios reciben un aviso para volver a escribir su contraseña. Este comportamiento se produce en los correos electrónicos que se va a redownloaded en dispositivos de los usuarios. Las modificaciones personalizadas por el usuario deberá realizarse de nuevo. 
- [Asignación de aplicaciones](https://docs.microsoft.com/intune/get-started-apps) 

## <a name="terms-and-conditions-policy"></a>Directiva de términos y condiciones
Al igual que con otras directivas de inquilino, las de términos y condiciones se migran automáticamente a Intune una vez habilitada la entidad mixta para su inquilino.  Sin embargo, debe asignar los términos y condiciones a un grupo que contenga usuarios migran para informar de la aceptación de los usuarios migrados con precisión y asegúrese de que se seleccionen correctamente los términos y condiciones para futuras términos y las actualizaciones de las condiciones o dispositivo inscripciones. Los usuarios no tienen que volver a aceptar los términos y condiciones, a menos que haya cambios realizados a la directiva en la consola de Configuration Manager. Para obtener más información, consulte [asignar términos y condiciones](https://docs.microsoft.com/intune/terms-and-conditions-create#assign-terms-and-conditions).

## <a name="configure-the-exchange-connector"></a>Configuración de Exchange Connector
Si usa Exchange y tiene una instancia de Exchange Connector local en Configuration Manager, debe [configurar la instancia de Exchange Connector local en Intune](https://docs.microsoft.com/intune/exchange-connector-install). Considere también la información en las secciones siguientes le ayudarán a migrar a Intune Exchange Connector y para asegurarse de que el acceso condicional funciona correctamente después de la migración.

### <a name="powershell-scripts-to-help-you-migrate-to-the-intune-exchange-connector"></a>Scripts de PowerShell para ayudarle a migrar a Intune Exchange Connector 
Los scripts de PowerShell están disponibles para ayudarle a prepararse para la transición de sus dispositivos Exchange de Configuration Manager Exchange Connector a Intune Exchange Connector. Aunque la ejecución de estos scripts es opcional, es recomendable ejecutarlos para quitar dispositivos inactivos de Exchange, lo que impide que Intune detecte dispositivos innecesarios. La ejecución de scripts garantiza que los dispositivos detectados a través de Exchange se puedan combinar con los dispositivos inscritos con Intune con la mayor fluidez posible. Ejecute estos scripts antes de configurar Intune Exchange Connector. Los scripts de PowerShell forman parte de la instalación de Intune Data Importer que se usa para [importar datos de Configuration Manager a Microsoft Intune](migrate-import-data.md) en el artículo siguiente. Para más información y descargar los scripts, vaya a la página de GitHub [Microsoft Intune Data Importer](https://github.com/ConfigMgrTools/Intune-Data-Importer).

### <a name="steps-to-make-sure-conditional-access-works-properly-after-user-migration"></a>Pasos para que el acceso condicional está seguro de que funciona correctamente después de la migración de usuario
Para que el acceso condicional funcione correctamente después de migrar los usuarios y para asegurarse de que los usuarios sigan teniendo acceso a su servidor de correo electrónico, asegúrese de que se establecen las siguientes configuraciones:
- Si se establece la configuración de nivel de acceso predeterminado de Exchange ActiveSync (DefaultAccessLevel) en Bloquear y Cuarentena, los dispositivos podrían perder el acceso al correo electrónico. 
- Si está instalado el conector de Exchange en Configuration Manager y el **nivel de acceso cuando un dispositivo móvil no está administrado por una regla** tiene un valor de **permitir el acceso**, instale el [ Conector de Exchange local](https://docs.microsoft.com/intune/conditional-access-exchange-create#configure-exchange-on-premises-access) en Intune antes de migrar los usuarios. Configurar la configuración de nivel de acceso predeterminada en Intune en el **Exchange local** página **configuración de acceso avanzada de Exchange ActiveSync**. Para obtener más información, consulte [configurar Exchange local acceso](https://docs.microsoft.com/intune/conditional-access-exchange-create#configure-exchange-on-premises-access).
- Utilice la misma configuración para ambos conectores. El último conector que configure sobrescribe la configuración de la organización de ActiveSync escrita previamente por el otro conector. Si configura los conectores de manera diferente, podrían producirse cambios inesperados en el acceso condicional.
- Quite usuarios del acceso condicional estableciendo destinos en Configuration Manager una vez que se migran a Intune independiente.

## <a name="configure-the-microsoft-intune-certificate-connector"></a>Configuración de Microsoft Intune Certificate Connector
Si usa NDES para emitir certificados mediante SCEP, debe configurar Microsoft Intune Certificate Connector. El equipo que hospeda el conector NDES en Intune no puede ser el mismo equipo que hospeda el conector NDES en Configuration Manager. Para obtener más información, consulte [configurar y administrar certificados SCEP con Intune](https://docs.microsoft.com/intune/certificates-scep-configure). 

> [!Important]    
> Después de configurar el conector, modificar los perfiles SCEP importados para hacer referencia a la nueva dirección URL del servidor.

## <a name="next-step"></a>Paso siguiente
Después de preparar Intune para la migración, está listo para migrar un conjunto de usuarios de prueba a Intune independiente. Para obtener más información, consulte [cambiar la entidad de MDM para usuarios específicos (entidad mixta)](migrate-mixed-authority.md).


