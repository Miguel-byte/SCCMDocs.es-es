---
title: Cambio de la entidad de MDM | Microsoft Docs
description: "Aprenda a cambiar la entidad de MDM desde Configuration Manager (híbrido) a Intune independiente"
keywords: 
author: dougeby
manager: angrobe
ms.date: 09/14/2017
ms.topic: article
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: cc397ab5-125f-4f17-905b-fab980194f49
ms.openlocfilehash: 489c01f92d42ed12ac5464307a16713ca898d251
ms.sourcegitcommit: 8ac9c2c9ba1fdcbb7cc8d5be898586865fcf67c0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/07/2017
---
# <a name="change-your-mdm-authority"></a>Cambio de la entidad de MDM
A partir de la versión 1610 de Configuration Manager, puede cambiar la entidad de MDM sin tener que ponerse en contacto con el Soporte técnico de Microsoft y sin necesidad de anular y volver a crear la inscripción de sus dispositivos administrados existentes. Este tema proporciona los pasos para cambiar un inquilino de Microsoft Intune existente configurado desde la consola de Configuration Manager (híbrida) a Intune independiente.

> [!Note]    
> Si quiere cambiar a Configuration Manager (híbrido) un inquilino existente de Microsoft Intune con la entidad de MDM establecida en Intune, vea [Cambio de la entidad de MDM](https://docs.microsoft.com/intune-classic/deploy-use/change-mdm-authority).

> [!Important]    
> En este tema se cambia la entidad de MDM cuando no haya migrado previamente usuarios. Para cambiar la entidad de MDM una vez que haya [migrado un subconjunto de usuarios](migrate-hybridmdm-to-intunesa.md), vea [Cambio de la entidad de MDM](migrate-change-mdm-authority.md).

## <a name="key-considerations"></a>Principales consideraciones
Después de cambiar a la nueva entidad de MDM, habrá probablemente un tiempo de transición (hasta ocho horas) antes de que el dispositivo se compruebe y se sincronice con el servicio. Debe configurar los parámetros en la nueva entidad de MDM (Intune independiente) para asegurarse de que los dispositivos inscritos siguen administrados y protegidos después del cambio. Tenga en cuenta las siguientes consideraciones:
- Los dispositivos deben conectarse al servicio después del cambio para que la configuración de la nueva entidad de MDM (Intune independiente) reemplace la configuración existente en el dispositivo.
- Después de cambiar la entidad de MDM, algunas de las opciones básicas (como los perfiles) de la entidad de MDM anterior (híbrida) permanecen en el dispositivo durante siete días. Es recomendable configurar aplicaciones y configuraciones (directivas, perfiles, aplicaciones, etc.) en la nueva entidad de MDM tan pronto como sea posible. Además, puede implementar la configuración para los grupos de usuarios que contienen los usuarios con dispositivos ya inscritos. Cuando un dispositivo se conecta al servicio después del cambio de entidad de MDM, recibe la nueva configuración de la nueva entidad de MDM. Toda directiva dirigida recientemente sobrescribirá las directivas existentes del dispositivo.
- Después de cambiar a la nueva entidad de MDM, los datos de cumplimiento de la consola de administración de Microsoft Intune pueden tardar hasta una semana en informar con exactitud. Sin embargo, los estados de cumplimiento de Azure Active Directory y en el dispositivo serán precisos para que el dispositivo siga estando protegido.
- Los dispositivos sin usuarios asociados (normalmente al tener el Programa de inscripción de dispositivos iOS o escenarios de inscripción de forma masiva) no se migran a la nueva entidad de MDM. Para esos dispositivos, debe llamar al soporte técnico para solicitar ayuda para trasladarlos a la nueva entidad de MDM.

## <a name="prepare-to-change-the-mdm-authority-to-intune-standalone"></a>Preparación para cambiar la entidad de MDM a Intune independiente
Revise la información siguiente para preparar el cambio de la entidad de MDM:
- Debe tener la versión 1610 de Configuration Manager o una posterior para que la opción para cambiar la entidad de MDM esté disponible.
- Un dispositivo puede tardar hasta ocho horas en conectarse al servicio después de cambiar a la nueva entidad de MDM.
- Asegúrese de que todos los usuarios que están administrados actualmente por la instancia híbrida tienen una licencia de Intune o EMS asignada antes de los cambios en la entidad de MDM. Tener la licencia garantiza que el usuario y sus dispositivos se administran por Intune independiente después del cambio en la entidad de MDM. Para obtener más información, consulte [Assign Intune licenses to your user accounts](https://docs.microsoft.com/intune/get-started/start-with-a-paid-subscription-to-microsoft-intune-step-4) (Asignar licencias de Intune a sus cuentas de usuario).
- Asegúrese de que la cuenta de usuario de administrador tiene asignada una licencia de Intune o EMS y confirme que la cuenta de usuario de administrador puede iniciar sesión en Intune antes del cambio a la entidad de MDM. La entidad de MDM debe mostrar **Configurar como Configuration Manager** (inquilino híbrido) en la consola de administración de Microsoft Intune antes del cambio en la entidad de MDM.
- En la consola de Configuration Manager, quite todos los roles de Administrador de inscripción de dispositivos. Vaya a **Administración** > **Cloud Services** > **Suscripciones a Microsoft Intune**, seleccione la suscripción de Microsoft Intune, haga clic en **Propiedades**, haga clic en la pestaña **Administrador de inscripción de dispositivos** y quite todos los roles de Administrador de inscripción de dispositivos.
- En la consola de Configuration Manager, quite las categorías de dispositivos existentes. Vaya a **Activos y compatibilidad** > **Introducción** > **Recopilaciones de dispositivos**, elija **Administrar categorías de dispositivos** y quite las categorías de dispositivos existentes.
- No debería haber ningún impacto perceptible en los usuarios finales durante el cambio de entidad de MDM. 
- Si usa Configuration Manager (inquilino híbrido) para administrar dispositivos iOS antes del cambio de la entidad de MDM, debe asegurarse de que el mismo certificado de servicio de Apple Push Notification Service que se había utilizado previamente en Configuration Manager se renueva y se utiliza para configurar el inquilino de nuevo en Intune independiente.

   > [!IMPORTANT]  
   > Si se utiliza un certificado diferente de Apple Push Notification Service para Intune independiente, se anulará la inscripción de TODOS los dispositivos de iOS y tendrá que repetir su proceso de inscripción. Antes de realizar el cambio en la entidad de MDM, asegúrese de que sabe exactamente qué certificado de Apple Push Notification Service se utilizó para administrar dispositivos iOS en Configuration Manager. Busque el mismo certificado en el portal Apple Push Certificates Portal (https://identity.apple.com) y asegúrese de que el usuario cuyo ID de Apple se usó para crear el certificado original de Apple Push Notification Service está identificado y disponible para renovar el mismo certificado de Apple Push Notification Service como parte del cambio a la nueva entidad de MDM.  

## <a name="change-the-mdm-authority-to-intune-standalone"></a>Cambio de la entidad de MDM a Intune independiente
El proceso para cambiar la entidad de MDM a Intune independiente incluye los siguientes pasos de alto nivel:  
- En la consola de Configuration Manager, use la opción **Cambiar entidad de MDM a Microsoft Intune** para quitar la suscripción de Microsoft Intune existente.
- En la consola de administración de Microsoft Intune, establezca la nueva entidad de MDM en **Intune**.
- Configure el certificado de Apple Push Notification Service con el mismo certificado de Apple Push Notification Service que ha renovado.
- En la consola de administración de Microsoft Intune, configure e implemente las nuevas opciones de configuración y aplicaciones desde la nueva entidad de MDM (Intune).
- La próxima vez que los dispositivos se conecten al servicio, se sincronizarán y recibirán la nueva configuración de la entidad de MDM.

#### <a name="to-change-the-mdm-authority-to-intune-standalone"></a>Para cambiar la entidad de MDM a una instalación de Intune independiente
1. En la consola de Configuration Manager, vaya a **Administración** &gt; **Información general** &gt; **Cloud Services** &gt; **Suscripción a Microsoft Intune** y elimine la suscripción a Intune actual.
2. Seleccione **Cambiar entidad de MDM a Microsoft Intune** y, a continuación, haga clic en **Siguiente**.
   ![Descarga de la solicitud de certificado de Apple Push Notification Service](./media/mdm-change-delete-subscription.png)
3. Inicie sesión en el inquilino de Intune que usó originalmente al configurar la entidad de MDM en Configuration Manager.
4. Haga clic en **Siguiente** y complete el asistente.
5. Ahora se ha restablecido la entidad de MDM. La suscripción a Intune ya no debe mostrarse en el nodo Suscripciones a Microsoft Intune de la consola de Configuration Manager.
6. Inicie sesión en la [Consola de administración de Microsoft Intune](http://manage.microsoft.com) utilizando el mismo inquilino de Intune que usó anteriormente.
7. Confirme que se ha restablecido la entidad de MDM y luego configure la entidad de MDM como **Microsoft Intune**. Después de cambiar la entidad de MDM, debería ver que se refleja en la consola. Para obtener más información, consulte [Configurar entidad de MDM](https://docs.microsoft.com/en-us/intune/deploy-use/prerequisites-for-enrollment#step-2-set-mdm-authority).
<!-- [Azure portal](https://docs.microsoft.com/en-us/intune-azure/enroll-devices/set-mdm-authority) -->


## <a name="configure-the-apns-certificate"></a>Configuración del certificado de Apple Push Notification Service
Cuando tenga los dispositivos iOS, debe configurar el certificado de Apple Push Notification Service en Intune.

#### <a name="to-configure-the-apns-certificate"></a>Para configurar el certificado de Apple Push Notification Service
1. Descargue la solicitud de certificado de Apple Push Notification Service.
   <!--The process is different depending on how you connect to Intune:
    **Azure portal**   
    In the [Azure portal](https://azure.portal.com), choose **More Services** &gt; **Monitoring + Management** &gt; **Intune**. On the **Intune** blade, choose **Device enrollment** &gt; **Apple Enrollment** &gt; **Apple MDM Push Certificate**, and then select **Download your CSR** to download and save the .csr file locally.   
    <br/>
    **Microsoft Intune administration console**   -->
   En la [consola de administración de Microsoft Intune](http://manage.microsoft.com), vaya a **Administración** &gt; **Administración de dispositivos móviles** &gt; **iOS y Mac OS X** &gt; **Cargar un certificado de APNs** y luego elija **Descargar la solicitud de certificado de APNs**. Guarde la solicitud de firma de certificado (.csr) en el equipo local.
   > [!IMPORTANT]    
   > Descargue una nueva solicitud de firma de certificado. No utilice un archivo existente o se producirá un error.

   ![Descarga de la solicitud de certificado de Apple Push Notification Service](./media/mdm-change-download-apns-certificate.png)

2. Vaya al portal [Apple Push Certificates Portal](http://go.microsoft.com/fwlink/?LinkId=269844) e inicie sesión con el **mismo** ID de Apple que se usó para crear y renovar anteriormente el certificado de Apple Push Notification Service que usó en Configuration Manager (híbrido).

   ![Página de inicio de sesión de Apple Push Certificates Portal](./media/mdm-change-apns-portal.png)

3. Seleccione el certificado de Apple Push Notification Service que usó en Configuration Manager (híbrido) y, a continuación, haga clic en **Renovar**.   

    ![Cuadro de diálogo para renovar Apple Push Notification Service](./media/mdm-change-renew-apns.png)

4. Seleccione la solicitud de firma del certificado de Apple Push Notification Service (.csr) que ha descargado localmente y, a continuación, haga clic en **Cargar**.

    ![Página de inicio de sesión de Apple Push Certificates Portal](/sccm/mdm/deploy-use/media/mdm-change-renew-apns-upload.png)
 
5. Seleccione el mismo Apple Push Notification Service y, a continuación, haga clic en **Descargar**. Descargue el certificado de Apple Push Notification Service (.pem) y guarde el archivo localmente.  

   ![Página de inicio de sesión de Apple Push Certificates Portal](./media/mdm-change-renew-apns-download.png)

6. Cargue el certificado de Apple Push Notification Service renovado en el inquilino de Intune con el mismo ID de Apple que antes.
<!--The process is different depending on how to connect to Intune:  
    **Azure portal**   
    In the [Azure portal](https://azure.portal.com), choose **More Services** &gt; **Monitoring + Management** &gt; **Intune**. On the **Intune** blade, choose **Device enrollment** &gt; **Apple Enrollment**  &gt; **Apple MDM Push Certificate**, enter your Apple ID in step 3, select the certificate (.pem) file in step 4, and then click **Upload**.     
    <br/>
    **Microsoft Intune administration console**    -->
    In the [Microsoft Intune administration console](http://manage.microsoft.com), go to **Administration** &gt; **Mobile Device Management** &gt; **iOS and Mac OS X** &gt; **Upload an APNs Certificate**, and then choose **Upload the APNs certificate**. Go to the certificate (.pem) file, choose **Open**, and then enter your **Apple ID**.   

   ![Carga del certificado de Apple Push Notification Service](./media/mdm-change-upload-apns-certificate.png)

## <a name="next-steps"></a>Pasos siguientes
Una vez completado el cambio en la entidad de MDM, revise los siguientes pasos:
- Cuando el servicio de Intune detecta que ha cambiado la entidad de MDM de un inquilino, envía un mensaje de notificación a todos los dispositivos inscritos para que inicien el proceso de comprobación y se sincronicen en el servicio (esto no forma parte de la comprobación programada regularmente). Por lo tanto, una vez que cambie la entidad de MDM para el inquilino de híbrido a Intune independiente, todos los dispositivos que estén encendidos y en línea se conectarán en el servicio, recibirán la nueva entidad de MDM y serán administrados en lo sucesivo por Intune independiente. No habrá ninguna interrupción en el proceso de administración y protección de estos dispositivos.
- Los dispositivos que estén apagados o sin conexión durante el cambio en la entidad de MDM (o poco tiempo después) se conectan al servicio y se sincronizarán con él con la nueva entidad de MDM cuando estén encendidos y en línea.  

  Los dispositivos iOS requieren un tiempo adicional para renovar y configurar el certificado de Apple Push Notification Service. Por lo tanto, los dispositivos iOS no recibirán la solicitud de comprobación inicial. Incluso si los dispositivos iOS están encendidos y en línea durante el cambio en la entidad de MDM (o poco tiempo después), pasarán hasta ocho horas (según el tiempo de la siguiente comprobación periódica programada) hasta que los dispositivos iOS se registren en el servicio bajo la nueva entidad de MDM.    

  > [!IMPORTANT]
  > Entre el momento en que cambie la entidad MDM y se cargue el certificado de Apple Push Notification Service renovado en la nueva entidad, las inscripciones de nuevos dispositivos y las comprobaciones de dispositivos iOS darán error. Por lo tanto, es importante revisar y cargar el certificado de Apple Push Notification Service en la nueva entidad tan pronto como sea posible después del cambio de entidad de MDM.   

- Los usuarios pueden cambiar rápidamente a la nueva entidad de MDM iniciando manualmente una comprobación desde el dispositivo en el servicio. Pueden hacerlo fácilmente mediante la aplicación Portal de empresa e iniciando una comprobación de cumplimiento del dispositivo.
- Para validar que todo funciona correctamente después de que los dispositivos se hayan comprobado y sincronizado con el servicio tras el cambio de entidad de MDM, busque los dispositivos en la [consola de administración de Microsoft Intune](http://manage.microsoft.com). Los dispositivos administrados anteriormente por Configuration Manager (híbrido) ahora aparecerán como dispositivos administrados.    
- Existe un período transitorio entre el momento en que un dispositivo está sin conexión durante el cambio de entidad de MDM y el momento en que se comprueba la idoneidad de ese dispositivo para su registro en el servicio. Para garantizar que el dispositivo permanece protegido y funcional durante este período transitorio, los elementos siguientes permanecerán en el dispositivo hasta siete días (o hasta que el dispositivo se conecte con la nueva entidad de MDM y reciba la nueva configuración que sobrescribirá la actual):
    - Perfil de correo electrónico
    - Perfil de VPN
    - Perfil de certificado
    - Perfil de Wi-Fi
    - Perfiles de configuración
- Compruebe que la nueva configuración destinada a sobrescribir la configuración actual tiene el mismo nombre que la anterior para asegurarse de que efectivamente se sobrescribe. En caso contrario, los dispositivos podrían terminar con directivas y perfiles redundantes.    

  > [!TIP]   
  > Es recomendable que cree todas las configuraciones y parámetros de administración, así como las implementaciones, poco después de que se haya completado el cambio a la entidad de MDM. De este modo se asegurará de que los dispositivos están protegidos y se administran de manera activa durante el período transitorio.   
-  Después de cambiar la entidad de MDM, siga estos pasos para validar que los nuevos dispositivos se inscriben correctamente en la nueva entidad:   
    - Inscripción de un dispositivo nuevo
    - Asegúrese de que el dispositivo recién inscrito aparece en la consola de administración de Intune.
    - Realice una acción, como el bloqueo remoto, desde la consola de administración en el dispositivo. Si se completa correctamente, el dispositivo se está administrando mediante la nueva entidad de MDM.
- Si tiene problemas con dispositivos concretos, puede anular la inscripción de esos dispositivos y realizarla de nuevo para que se conecten a la nueva entidad y se administren lo antes posible.

<!-- After the change in MDM authority and devices check in with the service, note the following:      - The updated compliance status of devices will only display in the Azure portal immediately.
- There will be a delay for compliance status of devices to display in the Intune administrative console.-->