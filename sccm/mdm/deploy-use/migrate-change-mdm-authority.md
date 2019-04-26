---
title: Cambio de la entidad de MDM a Intune
titleSuffix: Configuration Manager
description: Obtenga información acerca de cómo cambiar la entidad de MDM desde Configuration Manager (híbrido) a Intune independiente.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 02/27/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: be503ec9-5324-4f7c-bcf5-77204328e99c
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9d6a909be4b1817b9a251046d666839e2e351443
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62282174"
---
# <a name="change-your-mdm-authority-to-intune-standalone"></a>Cambio de la entidad de MDM a Intune independiente

*Se aplica a: System Center Configuration Manager (Rama actual)*    

Puede cambiar un inquilino de Microsoft Intune existente configurado desde la consola de Configuration Manager (MDM híbrida) a Intune independiente. El cambio de entidad de MDM de inquilino a Intune es la fase final del proceso para [migrar usuarios de MDM híbrida y dispositivos a Intune independiente](migrate-hybridmdm-to-intunesa.md) en la configuración solo en la nube.    

> [!Important]    
> Para cambiar la entidad de MDM sin migrar primero usuarios de MDM híbrida a Intune, vea [Cambio de la entidad de MDM](change-mdm-authority.md).

En este artículo se proporciona información acerca de cómo cambiar un inquilino de Microsoft Intune existente configurado desde la consola de Configuration Manager (híbrido) a Intune independiente. Se supone que ya ha completado los pasos siguientes:
- Se ha usado la [herramienta de importación de datos de Intune](migrate-import-data.md) para importar objetos de Configuration Manager a Intune. 
- [Se ha preparado Intune para la migración de usuario](migrate-prepare-intune.md) para asegurarse de que los usuarios y sus dispositivos continúan administrándose después de la migración.
- [Se ha cambiado la entidad de MDM para usuarios específicos (entidad de MDM mixta)](migrate-mixed-authority.md) para comenzar a administrar los dispositivos de usuario desde Azure Portal.


## <a name="users-and-devices-that-havent-been-migrated"></a>Los usuarios y dispositivos que no se han migrado
Ya ha migrado muchos usuarios y probado la funcionalidad de Intune para asegurarse de que todo funciona según lo previsto. Ha configurado las directivas, perfiles y aplicaciones en Intune y que haya probado exhaustivamente los objetos en los dispositivos. No debería haber ninguna configuración nueva necesaria para las directivas de nivel del inquilino después del cambio en la entidad de MDM. Sin embargo, para los usuarios y dispositivos que se haya migrado previamente, revise la siguiente información sobre qué esperar después del cambio en la entidad de MDM:    

- Es probable que un tiempo de transición de hasta ocho horas antes de que el dispositivo se compruebe y se sincroniza con el servicio.  

- Los dispositivos deben conectarse al servicio después del cambio para que la configuración de la nueva entidad de MDM (Intune independiente) reemplace la configuración existente en el dispositivo.  

- Algunas de las opciones básicas (como los perfiles) de la entidad de MDM anterior (híbrida) permanecen en el dispositivo durante siete días.  

- Los dispositivos que no tienen usuarios asociados no se migran a la nueva entidad de MDM. Estos dispositivos suelen con escenarios para el programa de inscripción de iOS o inscripción masiva. Para esos dispositivos, debe llamar al soporte técnico para solicitar ayuda para trasladarlos a la nueva entidad de MDM.



## <a name="prerequisites"></a>Requisitos previos
Revise la información siguiente para preparar el cambio de la entidad de MDM:
- Debe tener la versión 1610 de Configuration Manager o una posterior para que la opción para cambiar la entidad de MDM esté disponible.
- Asegúrese de asignar una licencia de Intune o EMS a todos los usuarios que están administrados por MDM híbrida. La licencia se asegura de que el usuario y sus dispositivos administrados por Intune independiente después del cambio en la entidad de MDM. Para obtener más información, consulte [Assign Intune licenses to your user accounts](https://docs.microsoft.com/intune/get-started/start-with-a-paid-subscription-to-microsoft-intune-step-4) (Asignar licencias de Intune a sus cuentas de usuario).
- Asegúrese de que la cuenta de usuario de administrador tenga asignada una licencia de Intune/EMS.

## <a name="change-the-mdm-authority-to-intune"></a>Cambio de la entidad de MDM a Intune
Utilice el procedimiento siguiente para cambiar la entidad de MDM de inquilino a Intune.

1. En la consola de Configuration Manager, vaya a la **administración** área de trabajo, expanda **servicios en la nube**y seleccione el **suscripción a Microsoft Intune** nodo. Elimine la suscripción de Intune existente.  

2. Seleccione **cambiar entidad de MDM a Microsoft Intune**y, a continuación, seleccione **siguiente**.

    ![Cuadro de diálogo para quitar suscripción de Microsoft Intune](media/mdm-change-delete-subscription.png)  

3. Inicie sesión en el inquilino de Intune que usó originalmente al configurar la entidad de MDM en Configuration Manager. Seleccione **siguiente** y complete el asistente.

    Ahora se ha restablecido la entidad de MDM. La suscripción a Intune ya no se muestra en el nodo Suscripciones a Microsoft Intune de la consola de Configuration Manager.  

4. Inicie sesión en el [portal Intune](https://aka.ms/IntunePortal).

5. Seleccione **inscripción de dispositivos**.  

6. En la información general de inscripción de dispositivos, consulte el **entidad de MDM** propiedad.

   > [!Important]    
   > No use la consola clásica de Intune. Inicie sesión en Intune en Azure portal.  

7. Confirme que la entidad de MDM se ha cambiado a **Microsoft Intune**. 



## <a name="after-migration"></a>Después de la migración

Una vez completado el cambio en la entidad de MDM, revise la siguiente información:

- No debería haber ningún impacto perceptible en los usuarios finales durante el cambio de entidad de MDM.  

- No tiene que volver a configurar las directivas de inquilino.  

- Si tiene que editar las directivas de inquilino, realice esta acción desde Intune en Azure portal.  

- Si tiene problemas con algún dispositivo, anule su inscripción y vuelva a inscribirlo. Esta acción obtiene ellos conectados a la nueva entidad y administrado tan pronto como sea posible.


#### <a name="validate-new-device-enrollment"></a>Validar la nueva inscripción de dispositivos
Después de cambiar la entidad de MDM, siga estos pasos para validar que los nuevos dispositivos se inscriben correctamente a la nueva entidad:   
1. Inscripción de un dispositivo nuevo
2. Asegúrese de que el dispositivo recién inscrito aparece en Intune
3. Iniciar una acción de dispositivo desde el portal de Intune, como [bloqueo remoto](https://docs.microsoft.com/intune/device-remote-lock). Si es correcto, el dispositivo se administra correctamente por la entidad de MDM.


#### <a name="for-users-and-devices-that-you-havent-previously-migrated"></a>Para los usuarios y dispositivos que se haya migrado previamente

- Compruebe que los dispositivos se muestran ahora en el **dispositivos** página como dispositivos administrados. Antes de que se muestran, deben comprobar estos dispositivos y se sincronice con el servicio después del cambio en la entidad de MDM. 

- Cuando el servicio de Intune detecta que ha cambiado la entidad MDM de un inquilino, envía un mensaje de notificación a todos los dispositivos inscritos. Indica los dispositivos para la comprobación y se sincronicen con el servicio. Esta notificación se produce fuera en la comprobación programada regularmente. Después de cambiar la entidad de MDM para el inquilino de híbrido a Intune independiente, todos los dispositivos en línea se conectarán en el servicio. Se recibirán la nueva entidad MDM y, a continuación, se administran por Intune independiente en el futuro. No hay ninguna interrupción en la administración y protección de estos dispositivos.

- Para los dispositivos que están sin conexión durante o inmediatamente después del cambio en la entidad de MDM, que conectarán a y sincronización con el servicio en la nueva entidad de MDM cuando están encendidos y en línea.  

- Puede cambiar rápidamente a la nueva entidad MDM iniciando manualmente una comprobación de desde el dispositivo al servicio. Use la aplicación de Portal de empresa para iniciar una comprobación de cumplimiento.

- Hay un período transitorio, cuando un dispositivo está sin conexión durante el cambio en la entidad de MDM y cuando ese dispositivo se registra en el servicio. Para asegurarse de que el dispositivo permanece protegido y funcional durante este período transitorio, los siguientes perfiles permanecen en el dispositivo hasta siete días. También puede permanecer hasta que el dispositivo se conecta con la nueva entidad MDM y reciba la nueva configuración que sobrescribirá la existente:
    - Perfil de correo electrónico
    - Perfil de VPN
    - Perfil de certificado
    - Perfil de Wi-Fi
    - Perfiles de configuración

- Para los dispositivos que no están asociados a un usuario, llame al soporte técnico para ayudar a cambiar la entidad de MDM. 

#### <a name="bkmk-ki-dep"></a> Registros de dispositivos de DEP de Apple
<!--ICM 105091970-->
Después de completar la migración de MDM híbrida, es posible que observe registros permanecen en la consola de administrador de configuración de dispositivo de DEP de Apple. Una vez que cambie la entidad de MDM a Intune, no se puede quitar estos dispositivos de Configuration Manager. 

Hay dos soluciones alternativas:

- Si ve este comportamiento antes de cambiar la entidad de MDM, eliminar, a continuación, los registros DEP de Configuration Manager.  

- Si ya ha migrado y todavía está usando Configuration Manager, use el siguiente comando SQL en la base de datos de sitio para quitar los registros:  

    ```SQL
    Delete from MDMCorpOwnedDevices where DeviceType=8 and DiscoverySources=4
    ```



## <a name="next-steps"></a>Pasos siguientes

Ahora que ha finalizado la migración, administrar los dispositivos móviles con Intune. Para obtener más información, consulte [cuáles son las novedades en Microsoft Intune](https://docs.microsoft.com/intune/whats-new).

