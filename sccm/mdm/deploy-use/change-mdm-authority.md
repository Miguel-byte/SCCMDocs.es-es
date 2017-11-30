---
title: Cambio de la entidad de MDM
titleSuffix: Configuration Manager
description: "Aprenda a cambiar la entidad de MDM desde Configuration Manager (híbrido) a Intune independiente"
keywords: 
author: dougeby
manager: angrobe
ms.date: 11/17/2017
ms.topic: article
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: cc397ab5-125f-4f17-905b-fab980194f49
ms.openlocfilehash: c61a44cce443a7ff210a626d114068691541aaae
ms.sourcegitcommit: 12d0d53e47bbf1a0bbd85015b8404a44589d1e14
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="change-your-mdm-authority"></a>Cambio de la entidad de MDM
A partir de la versión 1610 de Configuration Manager, puede cambiar la entidad de MDM sin tener que ponerse en contacto con el Soporte técnico de Microsoft y sin necesidad de anular y volver a crear la inscripción de sus dispositivos administrados existentes. En este artículo se proporcionan los pasos para cambiar un inquilino de Microsoft Intune existente configurado desde la consola de Configuration Manager (híbrida) a Intune independiente. Al completar los pasos descritos en este artículo, se administrarán los dispositivos con Microsoft Intune en [Azure Portal](https://portal.azure.com). 

> [!Note]    
> Si quiere cambiar a Configuration Manager (híbrido) un inquilino existente de Microsoft Intune con la entidad de MDM establecida en Intune, vea [Cambio de la entidad de MDM](https://docs.microsoft.com/intune-classic/deploy-use/change-mdm-authority).

> [!Important]    
> En este artículo se cambia la entidad de MDM cuando no haya migrado previamente usuarios. Para cambiar la entidad de MDM una vez que haya [migrado un subconjunto de usuarios](migrate-hybridmdm-to-intunesa.md), vea [Cambio de la entidad de MDM](migrate-change-mdm-authority.md).

## <a name="key-considerations"></a>Principales consideraciones
Después de cambiar a la nueva entidad de MDM, habrá probablemente un tiempo de transición (hasta ocho horas) antes de que el dispositivo se compruebe y se sincronice con el servicio. Debe configurar los parámetros en la nueva entidad de MDM (Intune independiente) para asegurarse de que los dispositivos inscritos siguen administrados y protegidos después del cambio. Tenga en cuenta las siguientes consideraciones:
- Los dispositivos deben conectarse al servicio después del cambio para que la configuración de la nueva entidad de MDM (Intune independiente) reemplace la configuración existente en el dispositivo.
- Después de cambiar la entidad de MDM, algunas de las opciones básicas (como los perfiles) de la entidad de MDM anterior (híbrida) permanecen en el dispositivo durante siete días. Es recomendable configurar aplicaciones y configuraciones (directivas, perfiles, aplicaciones, etc.) en la nueva entidad de MDM tan pronto como sea posible. Además, puede implementar la configuración para los grupos de usuarios que contienen los usuarios con dispositivos ya inscritos. Cuando un dispositivo se conecta al servicio después del cambio de entidad de MDM, recibe la nueva configuración de la nueva entidad de MDM. Toda directiva de destino recientemente sobrescribirá las directivas existentes del dispositivo.
- Después de cambiar a la nueva entidad de MDM, los datos de cumplimiento de [Azure Portal](https://portal.azure.com) pueden tardar hasta una semana en notificarse con exactitud. Sin embargo, los estados de cumplimiento de Azure Active Directory y en el dispositivo serán precisos para que el dispositivo siga estando protegido.
- Los dispositivos sin usuarios asociados (normalmente al tener el Programa de inscripción de dispositivos iOS o escenarios de inscripción de forma masiva) no se migran a la nueva entidad de MDM. Para esos dispositivos, debe llamar al soporte técnico para solicitar ayuda para trasladarlos a la nueva entidad de MDM.

## <a name="prepare-to-change-the-mdm-authority-to-intune-standalone"></a>Preparación para cambiar la entidad de MDM a Intune independiente
Revise la información siguiente para preparar el cambio de la entidad de MDM:
- Debe tener la versión 1610 de Configuration Manager o una posterior para que la opción para cambiar la entidad de MDM esté disponible.
- Un dispositivo puede tardar hasta ocho horas en conectarse al servicio después de cambiar a la nueva entidad de MDM.
- Asegúrese de que todos los usuarios que están administrados actualmente por la instancia híbrida tienen una licencia de Intune o EMS asignada antes de los cambios en la entidad de MDM. Tener la licencia garantiza que el usuario y sus dispositivos se administran por Intune independiente después del cambio en la entidad de MDM. Para obtener más información, consulte [Assign Intune licenses to your user accounts](https://docs.microsoft.com/intune/get-started/start-with-a-paid-subscription-to-microsoft-intune-step-4) (Asignar licencias de Intune a sus cuentas de usuario).
- Asegúrese de que la cuenta de usuario de administrador tiene asignada una licencia de Intune o EMS y confirme que la cuenta de usuario de administrador puede iniciar sesión en Intune antes del cambio a la entidad de MDM. La entidad de MDM debe mostrar **Configurar como Configuration Manager** (inquilino híbrido) en Intune [Azure Portal](https://portal.azure.com) antes del cambio en la entidad de MDM.
- No debería haber ningún impacto perceptible en los usuarios finales durante el cambio de entidad de MDM. 

## <a name="change-the-mdm-authority-to-intune-standalone"></a>Cambio de la entidad de MDM a Intune independiente
El proceso para cambiar la entidad de MDM a Intune independiente incluye los siguientes pasos de alto nivel:  
- En la consola de Configuration Manager, use la opción **Cambiar entidad de MDM a Microsoft Intune** para quitar la suscripción de Microsoft Intune existente.
- En Intune, en [Azure Portal](https://portal.azure.com), configure e implemente las nuevas opciones de configuración y aplicaciones desde la nueva entidad de MDM (Intune).
- La próxima vez que los dispositivos se conecten al servicio, se sincronizarán y recibirán la nueva configuración de la entidad de MDM.

#### <a name="to-change-the-mdm-authority-to-intune-standalone"></a>Para cambiar la entidad de MDM a una instalación de Intune independiente
1. En la consola de Configuration Manager, vaya a **Administración** &gt; **Información general** &gt; **Cloud Services** &gt; **Suscripción a Microsoft Intune** y elimine la suscripción a Intune actual.
2. Seleccione **Cambiar entidad de MDM a Microsoft Intune** y, a continuación, haga clic en **Siguiente**.
   ![Descarga de la solicitud de certificado de Apple Push Notification Service](./media/mdm-change-delete-subscription.png)
3. Inicie sesión en el inquilino de Intune que usó originalmente al configurar la entidad de MDM en Configuration Manager.
4. Haga clic en **Siguiente** y complete el asistente.
5. La entidad de MDM se establece ahora en **Microsoft Intune**. La suscripción a Intune ya no debe mostrarse en el nodo Suscripciones a Microsoft Intune de la consola de Configuration Manager. 
6. Para comprobar que se ha establecido la entidad de MDM, realice los siguientes pasos: a. Inicie sesión en [Azure Portal](https://portal.azure.com) mediante el mismo inquilino de Intune que usó anteriormente. 
    b. Elija **Más servicios** > **Supervisión y administración** > **Intune** > **Inscripción de dispositivos**. La entidad de MDM se muestra en la sección superior derecha de la hoja **Introducción**. 

## <a name="next-steps"></a>Pasos siguientes
Una vez completado el cambio en la entidad de MDM, revise los siguientes pasos:
- Cuando el servicio de Intune detecta que ha cambiado la entidad de MDM de un inquilino, envía un mensaje de notificación a todos los dispositivos inscritos para que inicien el proceso de comprobación y se sincronicen en el servicio (esto no forma parte de la comprobación programada regularmente). Por lo tanto, una vez que cambie la entidad de MDM para el inquilino de híbrido a Intune independiente, todos los dispositivos que estén encendidos y en línea se conectarán en el servicio, recibirán la nueva entidad de MDM y serán administrados en lo sucesivo por Intune independiente. No habrá ninguna interrupción en el proceso de administración y protección de estos dispositivos.
- Los dispositivos que estén apagados o sin conexión durante el cambio en la entidad de MDM (o poco tiempo después) se conectan al servicio y se sincronizarán con él con la nueva entidad de MDM cuando estén encendidos y en línea.  
- Los usuarios pueden cambiar rápidamente a la nueva entidad de MDM iniciando manualmente una comprobación desde el dispositivo en el servicio. Pueden hacerlo fácilmente mediante la aplicación Portal de empresa e iniciando una comprobación de cumplimiento del dispositivo.
- Para validar que todo funciona correctamente después de que los dispositivos se hayan comprobado y sincronizado con el servicio tras el cambio de entidad de MDM, busque los dispositivos en [Azure Portal](https://portal.azure.com). Los dispositivos administrados anteriormente por Configuration Manager (híbrido) ahora aparecerán como dispositivos administrados en Intune.    
- Existe un período transitorio entre el momento en que un dispositivo está sin conexión durante el cambio de entidad de MDM y el momento en que se comprueba la idoneidad de ese dispositivo para su registro en el servicio. Para garantizar que el dispositivo permanece protegido y funcional durante este período transitorio, los siguientes perfiles permanecerán en el dispositivo hasta siete días (o hasta que el dispositivo se conecte con la nueva entidad de MDM y reciba la nueva configuración que sobrescribirá la actual):
    - Perfil de correo electrónico
    - Perfil de VPN
    - Perfil de certificado
    - Perfil de Wi-Fi
    - Perfiles de configuración
- Compruebe que la nueva configuración destinada a sobrescribir la configuración actual tiene el mismo nombre que la anterior para asegurarse de que efectivamente se sobrescribe. En caso contrario, los dispositivos podrían terminar con directivas y perfiles redundantes.    

  > [!TIP]   
  > Es recomendable que cree todas las configuraciones y parámetros de administración, así como las implementaciones, poco después de que se haya completado el cambio a la entidad de MDM. De este modo, se asegurará de que los dispositivos están protegidos y se administran de manera activa durante el período transitorio.   
-  Después de cambiar la entidad de MDM, siga estos pasos para validar que los nuevos dispositivos se inscriben correctamente en la nueva entidad:   
    - Inscripción de un dispositivo nuevo
    - Asegúrese de que el dispositivo recién inscrito aparece en [Azure Portal](https://portal.azure.com).
    - Realice una acción, como el bloqueo remoto, desde [Azure Portal](https://portal.azure.com) en el dispositivo. Si se completa correctamente, el dispositivo se está administrando mediante la nueva entidad de MDM.
- Si tiene problemas con dispositivos concretos, puede anular la inscripción de esos dispositivos y realizarla de nuevo para que se conecten a la nueva entidad y se administren lo antes posible.