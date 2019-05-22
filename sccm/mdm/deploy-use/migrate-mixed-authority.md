---
title: Cambio de la entidad de MDM
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo cambiar la entidad de MDM de MDM híbrida a Intune independiente para usuarios específicos (entidad de MDM mixta).
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 05/21/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: 6f0201d7-5714-4ba0-b2bf-d1acd0203e9a
ms.collection: M365-identity-device-management
ms.openlocfilehash: ccc38188729a05329cc240a9f424ccce9fd433b2
ms.sourcegitcommit: d1df13fc95a1f1540177c294555d9be26161b9cb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/21/2019
ms.locfileid: "65974088"
---
# <a name="change-the-mdm-authority-for-specific-users-mixed-mdm-authority"></a>Cambio de la entidad de MDM para usuarios específicos (entidad de MDM mixta)

*Se aplica a: System Center Configuration Manager (Rama actual)*

Puede configurar una entidad de MDM mixta en el mismo inquilino. Administrar algunos usuarios en Microsoft Intune y otros con MDM híbrida. En este artículo se proporciona información sobre cómo comenzar a mover los usuarios a Intune independiente. Se supone que ha completado los pasos siguientes:  

- Se ha usado la herramienta de importación de datos para [importar objetos de Configuration Manager en Intune](migrate-import-data.md) (opcional).  

- [Se ha preparado Intune para la migración de usuario](migrate-prepare-intune.md) para asegurarse de que los usuarios y sus dispositivos continúan administrándose después de la migración.  

> [!Note]  
> Un restablecimiento completo del inquilino quita todas las directivas, aplicaciones y las inscripciones de dispositivos. Si decide que desea realizar este proceso, llame al soporte técnico para obtener ayuda.  

Administrar los usuarios migrados y sus dispositivos en Intune. Seguir administrando otros dispositivos en Configuration Manager. Para comprobar que todo funciona según lo previsto, comience con un grupo de prueba pequeño de usuarios. A continuación, migra gradualmente más grupos de usuarios. Cuando esté listo, cambiar la entidad de MDM de inquilino de Configuration Manager a Intune independiente.

> [!Important]  
> Desde el 13 de agosto de 2018, la administración híbrida de dispositivos móviles es una [característica en desuso](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). Para más información, vea [¿Qué es la Administración híbrida de dispositivos móviles (MDM)?](/sccm/mdm/understand/hybrid-mobile-device-management).<!--Intune feature 2683117-->  



## <a name="things-to-know-before-you-migrate-users"></a>Aspectos que debe conocer antes de migrar usuarios

- Durante la migración por fases, las aplicaciones o directivas de MDM de Configuration Manager existentes continuarán aplicándose a dispositivos de MDM híbrida.  

- Los dispositivos de los usuarios de la recopilación asociada con la suscripción de Intune pueden inscribirse en MDM híbrida. Todos los dispositivos asociados a usuarios no están en la colección se administran en Intune, siempre y cuando el usuario tenga una licencia de Intune o EMS.  

    > [!Note]  
    > Los usuarios pueden inscribirse en Intune independiente, incluso si se les ha bloqueado a través de la consola de Configuration Manager. Para bloquear completamente la inscripción de un usuario, no asigne licencias para Intune a los usuarios no deseados. No se inscriben sin una licencia.<!--SCCMDocs issue 738-->  

- Al migrar un usuario a Intune, los usuarios y dispositivos aparecen en Intune en Azure Portal después de 15 minutos aproximadamente.  

- Al migrar los usuarios a Intune independiente, continúe para administrar la siguiente configuración de Configuration Manager en los dispositivos de MDM híbrida y de Intune independiente:  

    - [Certificado de Apple Push Notification Service (APN)](/sccm/mdm/deploy-use/enroll-hybrid-ios-mac)  

    - [Programa de inscripción de dispositivos](/sccm/mdm/deploy-use/ios-device-enrollment-program-for-hybrid)  

        > [!Note]  
        > No es necesario volver a crear el token de DEP o quitarlo del Administrador de configuración. Migra automáticamente a Intune 24 horas después de cambiar la entidad de MDM de inquilino de Configuration Manager a Intune. Este cambio es el último paso en la migración. (Si el token de DEP no migra dentro de 24 horas, póngase en contacto con soporte técnico de Microsoft para obtener ayuda.)  

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
    > Continúe para editar las directivas de inquilino mediante la consola de Configuration Manager. Después de [cambiar la entidad MDM de inquilino](/sccm/mdm/deploy-use/change-mdm-authority) a Intune, las directivas de nivel de inquilino que se administra en Configuration Manager automáticamente migración a Intune en Azure. Un ejemplo de esta directiva es para los certificados de Apple Push Notification service (APN).<!--SCCMDocs issue #971-->  

- Si usa certificados de firma de código, se recomienda que migre los usuarios por fases. Después de migrar un dispositivo móvil, realiza una solicitud de un certificado nuevo a una entidad de certificación. Al usar un enfoque por fases para migrar los usuarios (y sus dispositivos), se limita el número de solicitudes de entidad de certificación simultáneas.  

- No migre las cuentas de usuario que se han agregado como administradores de inscripción de dispositivos en Configuration Manager. Más adelante, cuando cambie su entidad de MDM de inquilino a Intune, estas cuentas de usuario se migrarán correctamente. Si migra la cuenta de usuario DEM antes del cambio de entidad MDM de inquilino, debe agregar manualmente el usuario como un DEM en Intune en Azure. Sin embargo, los dispositivos inscritos mediante un DEM no se migran correctamente. Llame al servicio de soporte técnico para migrar estos dispositivos. Para obtener más información, consulte [Agregar un administrador de inscripción de dispositivos](https://docs.microsoft.com/intune/device-enrollment-manager-enroll#add-a-device-enrollment-manager).  

    > [!Note]  
    > En el modo de entidad mixta, no mueva estas cuentas a Intune quitándolas de la recopilación en la nube de Configuration Manager. Si lo hace, el usuario se convierte en un usuario estándar y no puede inscribir más de 15 dispositivos. En su lugar, puede migrar estos usuarios y sus dispositivos cuando cambie por completo la entidad de MDM para el inquilino.<!--Intune bug 2174210-->  

- Los dispositivos inscritos mediante un DEM y dispositivos sin [afinidad entre usuario y](/sccm/mdm/deploy-use/user-affinity-for-hybrid-managed-devices) no se migran automáticamente a la nueva entidad MDM. Para cambiar la autoridad de administración para estos dispositivos MDM, consulte [Migración de dispositivos sin afinidad de usuario](#migrate-devices-without-user-affinity).  



## <a name="migrate-users-to-intune"></a>Migración de usuarios a Intune

Para comprobar que las configuraciones de Intune funcionan según lo esperado, migre primero un pequeño conjunto de usuarios y sus dispositivos. Después de confirmar que todo funciona según lo previsto, puede iniciar la migración de más grupos de AAD con más usuarios y sus dispositivos.



## <a name="migrate-a-test-group-of-users-to-intune-standalone"></a>Migración de un grupo de prueba de usuarios a Intune independiente

Los dispositivos de los usuarios de la recopilación asociada con la suscripción de Intune pueden inscribirse en MDM híbrida. Cuando se quita un usuario de la colección, si el usuario tiene asignada una licencia de Intune, se migran los dispositivos inscritos a Intune independiente. Si ya no ha asignado licencias a los usuarios que va a migrar, vea [asignar licencias de Intune a las cuentas de usuario](https://docs.microsoft.com/intune/licenses-assign). En la recopilación de la suscripción de Intune, puede excluir recopilaciones de usuarios de su principal para migrar los usuarios de la excluida.

En el ejemplo siguiente, la recopilación de usuarios Híbrido contiene todos los miembros de la recopilación Todos los usuarios. Esta configuración permite a cualquier usuario inscribir un dispositivo en MDM híbrida. Para migrar usuarios a Intune independiente, seleccione Excluir recopilaciones y agregue una recopilación con los usuarios para migrar. Cuando esté listo para migrar más usuarios, agregue más recopilaciones excluidas que incluyan esos usuarios.

![Recopilaciones excluidas](../media/migrate-excludecollections.png)

> [!Note]  
> Cuando tenga el **todos los usuarios** colección seleccionada para la suscripción a Intune, no se permiten para agregar una regla que excluya las recopilaciones. Crear una nueva colección basada en la **todos los usuarios** colección. Compruebe que la colección contiene los usuarios que se esperan. A continuación, edite la suscripción a Intune para usar la nueva colección. Puede excluir recopilaciones de usuarios de la nueva recopilación para migrar usuarios.  

Para migrar un grupo de prueba de usuarios a Intune, cree una recopilación de usuarios que contenga los usuarios para migrar. A continuación, excluya la recopilación de usuario de la colección que se usa para la suscripción de Intune.  

En el siguiente diagrama se proporciona una introducción sobre el funcionamiento de la migración de usuarios.

![Introducción a la entidad mixta](../media/migrate-mixedauthority.svg)

1. Compruebe que el usuario tiene una licencia de Intune o EMS.  

2. Cree una recopilación para que se excluya de la de la suscripción de Intune. En este ejemplo, la recopilación **All Hybrid users** (Todos los usuarios de Híbrido) contiene una regla para excluir los usuarios de la recopilación **Migration pilot** (Piloto de migración). **User1** es un miembro de la recopilación **Migration pilot** (Piloto de migración) y se excluye la recopilación **All Hybrid users** (Todos los usuarios de Híbrido).  

3. **User1**de dispositivos ahora se administran desde Intune en Azure portal.  

4. El resto de los dispositivos se siguen administrando desde la consola de Configuration Manager.  

> [!Important]  
> Cuando se mueve un usuario de híbrido a independiente, la eliminación de directiva se suspende durante siete días.<!-- SCCMDocs issue #1066 -->


## <a name="verify-intune-standalone-functionality"></a>Comprobación de la funcionalidad independiente de Intune

Después de migrar un pequeño conjunto de usuarios, compruebe que los dispositivos del usuario aparecen en Intune. Vaya a **Dispositivos** y seleccione **Todos los dispositivos**.

Después, compruebe que sus directivas, perfiles y aplicaciones funcionan según lo previsto en los dispositivos de usuario.



## <a name="migrate-additional-users"></a>Migración de más usuarios

Una vez que haya comprobado que Intune independiente funciona como esperaba, inicie la migración de más usuarios. Como ha creado una colección con un conjunto de usuarios de prueba, crear colecciones que incluyen los usuarios para migrar. Excluya las de la colección que está asociada la suscripción de Intune. Para obtener más información, consulte [migrar un grupo de prueba de usuarios a Intune independiente](#migrate-a-test-group-of-users-to-intune-standalone).



## <a name="migrate-devices-without-user-affinity"></a>Migración de dispositivos sin afinidad de usuario

Para migrar los dispositivos individuales formulario Configuration Manager a Intune que se han inscrito sin afinidad de usuario, use el cmdlet Switch-MdmDeviceAuthority PowerShell.  Después de migrar los dispositivos seleccionados con el cmdlet, validar en Intune en Azure que la migración se ha producido como esperado para los dispositivos seleccionados. A continuación, cuando esté listo, cambie la entidad de MDM a Intune para el inquilino completar la migración para los dispositivos restantes que tiene Configuration Manager como su entidad de MDM.

### <a name="cmdlet-switch-mdmdeviceauthority"></a>Cmdlet *Switch-MdmDeviceAuthority*

#### <a name="synopsis"></a>SINOPSIS

El cmdlet cambia la entidad de administración de dispositivos MDM sin afinidad de usuario (por ejemplo, dispositivos inscritos de forma masiva). El cmdlet cambia entre Intune y Configuration Manager autoridades de administración. Cambia para los dispositivos especificados basados en sus entidades de administración cuando se ejecuta el cmdlet.

### <a name="syntax"></a>SYNTAX

`Switch-MdmDeviceAuthority -DeviceIds <Guid[]> [-Credential <PSCredential>] [-Force] [-LogFilePath <string>] [-LoggingLevel {Off | Critical | Error | Warning | Information | Verbose | ActivityTracing | All}] [-Confirm] [-WhatIf] [<CommonParameters>]`


### <a name="parameters"></a>PARÁMETROS

#### `-Credential <PSCredential>`

Objeto de credencial de PowerShell para la cuenta de usuario de Azure AD que se usa cuando se cambian las entidades de administración de dispositivos. Si no se especifica el parámetro, se solicitará al usuario las credenciales. El rol de directorio de esta cuenta de usuario debe ser un **administrador global** o un **administrador limitado** con el rol administrativo de **administrador de Intune**.

#### `-DeviceIds <Guid[]>`

Los identificadores de los dispositivos MDM cuya entidad de administración se debe cambiar. Los identificadores de dispositivo son identificadores únicos de los dispositivos mostrados por la consola de Configuration Manager.

#### `-Force [<SwitchParameter>]`

Especifique un parámetro para deshabilitar el mensaje Debe continuar.

#### `-LogFilePath <string>`

Ruta a la ubicación del archivo de registro.

#### `-LoggingLevel <SourceLevels>`

Nivel de registro usado para determinar el tipo de registros que deben escribirse en el archivo de registro.

Estos son los valores posibles para LoggingLevel:

- ActivityTracing
- Todos
- Crítica
- Error
- Información
- Desactivar
- Detallado
- Advertencia

#### `-Confirm [<SwitchParameter>]`

Solicita confirmación antes de ejecutar el comando.

#### `-WhatIf [<SwitchParameter>]`

Describe lo que sucedería si ejecutara el comando sin ejecutarlo realmente.

#### `<CommonParameters>`

Este cmdlet admite los parámetros comunes: Verbose, Debug, ErrorAction, ErrorVariable, WarningAction, WarningVariable, OutBuffer, PipelineVariable y OutVariable. Para obtener más información, vea [about_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

### <a name="example-1"></a>Ejemplo 1

``` powershell
C:\PS>Switch-MdmDeviceAuthority -Credential $creds -DeviceIds $deviceIds

  DeviceId       : 62e6ea43-18f8-4278-bcd4-a4baed2c6d24
  Success        : True
  FailureReason  :
  NewAuthority   : Intune
  CompletionTime : 11/15/2017 8:00:11 PM

Description

-----------

Successfully switched the management authority of the device from Configuration Manager to Intune.
```

### <a name="remarks"></a>COMENTARIOS

- Para ver los ejemplos, escriba: `get-help Switch-MdmDeviceAuthority -examples`  
- Para obtener más información, escriba: `get-help Switch-MdmDeviceAuthority -detailed`  
- Para obtener información técnica, escriba: `get-help Switch-MdmDeviceAuthority -full`  
- Para obtener ayuda en línea, escriba: `get-help Switch-MdmDeviceAuthority -online`  



## <a name="next-steps"></a>Pasos siguientes

Después de migrar los usuarios y probar la funcionalidad de Intune, compruebe si está listo para [cambiar la entidad de MDM](migrate-change-mdm-authority.md) de su inquilino de Intune desde Configuration Manager en Intune.
