---
title: Cambio de la entidad de MDM a Intune
titleSuffix: Configuration Manager
description: Obtenga información acerca de cómo cambiar la entidad de MDM desde Configuration Manager (híbrido) a Intune independiente.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 12/05/2017
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: be503ec9-5324-4f7c-bcf5-77204328e99c
ms.openlocfilehash: 4ded99c2084f274d519680e78fdc54825b3857cb
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2018
ms.locfileid: "53419519"
---
# <a name="change-your-mdm-authority-to-intune-standalone"></a>Cambio de la entidad de MDM a Intune independiente

*Se aplica a: System Center Configuration Manager (rama actual)*    

Puede cambiar un inquilino de Microsoft Intune existente configurado desde la consola de Configuration Manager (MDM híbrida) a Intune independiente. El cambio de entidad de MDM de inquilino a Intune es la fase final del proceso para [migrar usuarios de MDM híbrida y dispositivos a Intune independiente](migrate-hybridmdm-to-intunesa.md) en la configuración solo en la nube.    

> [!Important]    
> Para cambiar la entidad de MDM sin migrar primero usuarios de MDM híbrida a Intune, vea [Cambio de la entidad de MDM](change-mdm-authority.md).

En este artículo se proporciona información sobre cómo cambiar un inquilino existente de Microsoft Intune configurado desde la consola de Configuration Manager (híbrida) a Intune independiente y se presupone que ya ha completado los pasos siguientes:
- Se ha usado la [herramienta de importación de datos de Intune](migrate-import-data.md) para importar objetos de Configuration Manager a Intune. 
- [Se ha preparado Intune para la migración de usuario](migrate-prepare-intune.md) para asegurarse de que los usuarios y sus dispositivos continúan siendo administrados después de la migración.
- [Se ha cambiado la entidad de MDM para usuarios específicos (entidad de MDM mixta)](migrate-mixed-authority.md) para comenzar a administrar los dispositivos de usuario desde Azure Portal.


## <a name="users-and-devices-that-have-not-been-migrated"></a>Usuarios y dispositivos que no se han migrado
Ya ha migrado muchos usuarios y ha probado la funcionalidad de Intune para asegurarse de que todo funciona según lo previsto. Por lo tanto, sus directivas, perfiles, aplicaciones, etc. se han configurado en Intune y ha probado exhaustivamente los objetos en los dispositivos. No debería haber ninguna configuración nueva necesaria para las directivas de nivel del inquilino después del cambio en la entidad de MDM. Sin embargo, para los usuarios y dispositivos que no se han migrado previamente, revise la siguiente información acerca de lo que puede esperar después del cambio en la entidad de MDM:    
- Probablemente haya un tiempo de transición (hasta ocho horas) antes de que el dispositivo se compruebe y se sincronice con el servicio.
- Los dispositivos deben conectarse al servicio después del cambio para que la configuración de la nueva entidad de MDM (Intune independiente) reemplace la configuración existente en el dispositivo.
- Algunas de las opciones básicas (como los perfiles) de la entidad de MDM anterior (híbrida) permanecen en el dispositivo durante siete días. 
- Los dispositivos sin usuarios asociados (normalmente al tener el Programa de inscripción de dispositivos iOS o escenarios de inscripción de forma masiva) no se migran a la nueva entidad de MDM. Para esos dispositivos, debe llamar al soporte técnico para solicitar ayuda para trasladarlos a la nueva entidad de MDM.

## <a name="prerequisites"></a>Requisitos previos
Revise la información siguiente para preparar el cambio de la entidad de MDM:
- Debe tener la versión 1610 de Configuration Manager o una posterior para que la opción para cambiar la entidad de MDM esté disponible.
- Asegúrese de que todos los usuarios que están administrados actualmente por la MDM híbrida tengan una licencia de Intune o EMS asignada antes de los cambios en la entidad de MDM. Tener la licencia garantiza que el usuario y sus dispositivos se administran por Intune independiente después del cambio en la entidad de MDM. Para obtener más información, consulte [Assign Intune licenses to your user accounts](https://docs.microsoft.com/intune/get-started/start-with-a-paid-subscription-to-microsoft-intune-step-4) (Asignar licencias de Intune a sus cuentas de usuario).
- Asegúrese de que la cuenta de usuario de administrador tenga asignada una licencia de Intune/EMS.

## <a name="change-the-mdm-authority-to-intune"></a>Cambio de la entidad de MDM a Intune
Utilice el procedimiento siguiente para cambiar la entidad de MDM de inquilino a Intune.

1. En la consola de Configuration Manager, vaya a **Administración** &gt; **Información general** &gt; **Cloud Services** &gt; **Suscripción a Microsoft Intune** y elimine la suscripción a Intune actual.
2. Seleccione **Cambiar entidad de MDM a Microsoft Intune** y, a continuación, haga clic en **Siguiente**.

   ![Cuadro de diálogo para quitar suscripción de Microsoft Intune](media/mdm-change-delete-subscription.png)
3. Inicie sesión en el inquilino de Intune que usó originalmente al configurar la entidad de MDM en Configuration Manager.
4. Haga clic en **Siguiente** y complete el asistente.
5. Ahora se ha restablecido la entidad de MDM. La suscripción a Intune ya no se muestra en el nodo Suscripciones a Microsoft Intune de la consola de Configuration Manager.
6. Inicie sesión en el [portal de Intune](https://aka.ms/IntunePortal).
7. En la hoja de Microsoft Intune, haga clic en **Inscripción de dispositivos**.
8. En la hoja de información general de inscripción de dispositivos, vea la propiedad **Entidad de MDM**.

   > [!Important]    
   > No utilice la consola de Intune clásica. Debe iniciar sesión en Intune en Azure Portal.
9. Confirme que la entidad de MDM se ha cambiado a **Microsoft Intune**. 

## <a name="next-steps"></a>Pasos siguientes
Una vez completado el cambio en la entidad de MDM, revise la siguiente información:
- No debería haber ningún impacto perceptible en los usuarios finales durante el cambio de entidad de MDM. 
- No es necesario volver a configurar las directivas de inquilino. 
- Puede editar las directivas de inquilino de Intune en Azure Portal después del cambio en la entidad de MDM.
-  Después de cambiar la entidad de MDM, siga estos pasos para validar que los nuevos dispositivos se inscriben correctamente en la nueva entidad:   
    - Inscripción de un dispositivo nuevo
    - Asegúrese de que el dispositivo recién inscrito aparece en Intune.
    - Realice una acción, como el bloqueo remoto, desde la consola de administración en el dispositivo. Si se completa correctamente, el dispositivo se está administrando mediante la nueva entidad de MDM.
- Si tiene problemas con dispositivos concretos, puede anular la inscripción de esos dispositivos y realizarla de nuevo para que se conecten a la nueva entidad y se administren lo antes posible.
- Para usuarios y dispositivos que no se han migrado anteriormente:
    - Compruebe que los dispositivos se muestran ahora en la hoja**Dispositivos** como dispositivos administrados. Estos dispositivos deben comprobarse y sincronizarse con el servicio después del cambio de entidad de MDM para que se muestren. 
    - Cuando el servicio de Intune detecta que ha cambiado la entidad de MDM de un inquilino, envía un mensaje de notificación a todos los dispositivos inscritos para que inicien el proceso de comprobación y se sincronicen en el servicio (no forma parte de la comprobación programada regularmente). Por lo tanto, una vez que cambie la entidad de MDM para el inquilino de híbrido a Intune independiente, todos los dispositivos que estén encendidos y en línea se conectan en el servicio, reciben la nueva entidad de MDM y son administrados por Intune independiente a partir de ahora. No hay ninguna interrupción en el proceso de administración y protección de estos dispositivos.
    - Los dispositivos que estén apagados o sin conexión durante el cambio en la entidad de MDM (o poco tiempo después) se conectan al servicio y se sincronizarán con él con la nueva entidad de MDM cuando estén encendidos y en línea.  
    - Los usuarios pueden cambiar rápidamente a la nueva entidad de MDM iniciando manualmente una comprobación desde el dispositivo en el servicio. Pueden realizar la comprobación fácilmente mediante la aplicación Portal de empresa e iniciando una comprobación de cumplimiento del dispositivo.
    - Existe un período transitorio entre el momento en que un dispositivo está sin conexión durante el cambio de entidad de MDM y el momento en que se comprueba la idoneidad de ese dispositivo para su registro en el servicio. Para garantizar que el dispositivo permanece protegido y funcional durante este período transitorio, los siguientes perfiles permanecen en el dispositivo hasta siete días (o hasta que el dispositivo se conecte con la nueva entidad de MDM y reciba la nueva configuración que sobrescribirá la actual):
        - Perfil de correo electrónico
        - Perfil de VPN
        - Perfil de certificado
        - Perfil de Wi-Fi
        - Perfiles de configuración
    - Llame al soporte técnico para ayudar a cambiar la entidad de MDM para los dispositivos que no estén asociados a un usuario. 
