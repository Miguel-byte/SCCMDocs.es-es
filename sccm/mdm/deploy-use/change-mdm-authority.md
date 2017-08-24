---
title: Cambio de la entidad de MDM | Microsoft Docs
description: "Obtenga información acerca de cómo cambiar la entidad de MDM desde Configuration Manager (híbrido) a Intune independiente o viceversa."
keywords: 
author: dougeby
manager: angrobe
ms.date: 06/02/2017
ms.topic: article
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: cc397ab5-125f-4f17-905b-fab980194f49
ms.openlocfilehash: 74b9dbb1ed0172d99956e726fca3aec2b658ce77
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/07/2017
---
# <a name="change-your-mdm-authority"></a>Cambio de la entidad de MDM
A partir de la versión 1610 de Configuration Manager y la versión 1705 de Microsoft Intune, puede cambiar la entidad de MDM sin tener que ponerse en contacto con el soporte técnico de Microsoft y sin necesidad de anular y volver a crear la inscripción de sus dispositivos administrados existentes.

## <a name="change-the-mdm-authority-to-intune-standalone"></a>Cambio de la entidad de MDM a Intune independiente
Use esta sección para cambiar un inquilino de Microsoft Intune configurado desde la consola de Configuration Manager (híbrida) a Intune independiente sin tener que anular y volver a crear la inscripción de los dispositivos administrados existentes.

### <a name="key-considerations"></a>Principales consideraciones
Después de cambiar a la nueva entidad de MDM, habrá probablemente un tiempo de transición (hasta 8 horas) antes de que el dispositivo se compruebe y se sincronice con el servicio. Será necesario que configure los parámetros en la nueva entidad de MDM (Intune independiente) para asegurarse de que los dispositivos inscritos seguirán administrados y protegidos después del cambio. y tenga en cuenta lo siguiente:
- Los dispositivos deben conectarse al servicio después del cambio para que la configuración de la nueva entidad de MDM (Intune independiente) reemplace la configuración existente en el dispositivo.
- Después de cambiar la entidad de MDM, algunas de las opciones básicas (como los perfiles) de la entidad de MDM anterior (híbrida) permanecerán en el dispositivo durante 7 días. Se recomienda que configure aplicaciones y parámetros (directivas, perfiles, aplicaciones, etc.) en la nueva entidad de MDM tan pronto como sea posible y que implemente la configuración en los grupos de usuarios que contienen usuarios con dispositivos ya inscritos. En cuanto el dispositivo se conecte con el servicio tras el cambio en la entidad de MDM, recibirá la nueva configuración desde la nueva entidad de MDM, evitando así los tiempos de inactividad en administración y protección. Toda directiva dirigida recientemente sobrescribirá las directivas existentes del dispositivo.
- Después de cambiar a la nueva entidad de MDM, los datos de cumplimiento de la consola de administración de Microsoft Intune pueden tardar hasta una semana en informar con exactitud. Sin embargo, los estados de cumplimiento de Azure Active Directory y en el dispositivo serán precisos para que el dispositivo siga estando protegido.

### <a name="prepare-to-change-the-mdm-authority-to-intune-standalone"></a>Preparación para cambiar la entidad de MDM a Intune independiente
Revise la información siguiente para preparar el cambio de la entidad de MDM:
- Debe tener la versión 1610 de Configuration Manager o una posterior para que la opción para cambiar la entidad de MDM esté disponible.
- Un dispositivo puede tardar hasta 8 horas en conectarse al servicio después de cambiar a la nueva entidad de MDM.
- Asegúrese de que todos los usuarios que están administrados actualmente por la instancia híbrida tienen una licencia de Intune o EMS asignada específicamente antes de los cambios en la entidad de MDM. Esto garantizará que el usuario y sus dispositivos se administren por Intune independiente después del cambio en la entidad de MDM. Para obtener más información, consulte [Assign Intune licenses to your user accounts](https://docs.microsoft.com/intune/get-started/start-with-a-paid-subscription-to-microsoft-intune-step-4) (Asignar licencias de Intune a sus cuentas de usuario).
- Asegúrese de que la cuenta de usuario de administrador tiene asignada una licencia de Intune o EMS y confirme que la cuenta de usuario de administrador puede iniciar sesión en Intune antes del cambio a la entidad de MDM. La entidad de MDM debe mostrar **Configurar como Configuration Manager** (inquilino híbrido) en la consola de administración de Microsoft Intune antes del cambio en la entidad de MDM.
- En la consola de Configuration Manager, quite todos los roles de Administrador de inscripción de dispositivos. Vaya a **Administración** > **Cloud Services** > **Suscripciones a Microsoft Intune**, seleccione la suscripción de Microsoft Intune, haga clic en **Propiedades**, haga clic en la pestaña **Administrador de inscripción de dispositivos** y quite todos los roles de Administrador de inscripción de dispositivos.
- En la consola de Configuration Manager, quite las categorías de dispositivos existentes. Vaya a **Activos y compatibilidad** > **Introducción** > **Recopilaciones de dispositivos**, elija **Administrar categorías de dispositivos** y quite las categorías de dispositivos existentes.
- No debería haber ningún impacto perceptible en los usuarios finales durante el cambio de entidad de MDM. Sin embargo, puede comunicar este cambio a los usuarios para asegurarse de que sus dispositivos están encendidos y de que se conectan al servicio pronto después del cambio. De este modo, estará seguro de que se conectan tantos dispositivos como sea posible al servicio y de que se registran en la nueva entidad lo antes posible.
- Si usa Configuration Manager (inquilino híbrido) para administrar dispositivos iOS antes del cambio de la entidad de MDM, debe asegurarse de que el mismo certificado de servicio de Apple Push Notification Service que se había utilizado previamente en Configuration Manager se renueva y se utiliza para configurar el inquilino de nuevo en Intune independiente.

    > [!IMPORTANT]  
    > Si se utiliza un certificado diferente de Apple Push Notification Service para Intune independiente, se anulará la inscripción de TODOS los dispositivos de iOS y tendrá que repetir su proceso de inscripción. Antes de realizar el cambio en la entidad de MDM, asegúrese de que sabe exactamente qué certificado de Apple Push Notification Service se utilizó para administrar dispositivos iOS en Configuration Manager. Busque el mismo certificado en el portal Apple Push Certificates Portal (https://identity.apple.com) y asegúrese de que el usuario cuyo ID de Apple se usó para crear el certificado original de Apple Push Notification Service está identificado y disponible para renovar el mismo certificado de Apple Push Notification Service como parte del cambio a la nueva entidad de MDM.  

### <a name="change-the-mdm-authority-to-intune-standalone"></a>Cambio de la entidad de MDM a Intune independiente
El proceso para cambiar la entidad de MDM a Intune independiente incluye los siguientes pasos de alto nivel:  
- En la consola de Configuration Manager, use la opción **Cambiar entidad de MDM a Microsoft Intune** para quitar la suscripción de Microsoft Intune existente.
- En la consola de administración de Microsoft Intune, establezca la nueva entidad de MDM en **Intune**.
- Configure el certificado de Apple Push Notification Service con el mismo certificado de Apple Push Notification Service que ha renovado.
- En la consola de administración de Microsoft Intune, configure e implemente las nuevas opciones de configuración y aplicaciones desde la nueva entidad de MDM (Intune).
- La próxima vez que los dispositivos se conecten al servicio, se sincronizarán y recibirán la nueva configuración de la entidad de MDM.

#### <a name="to-change-the-mdm-authority-to-intune-standalone"></a>Para cambiar la entidad de MDM a una instalación de Intune independiente
1.  En la consola de Configuration Manager, vaya a **Administración** &gt; **Información general** &gt; **Cloud Services** &gt; **Suscripción a Microsoft Intune** y elimine la suscripción a Intune actual.
2.  Seleccione **Cambiar entidad de MDM a Microsoft Intune** y, a continuación, haga clic en **Siguiente**.

    ![Descarga de la solicitud de certificado de Apple Push Notification Service](/sccm/mdm/deploy-use/media/mdm-change-delete-subscription.png)
3.  Inicie sesión en el inquilino de Intune que usó originalmente al configurar la entidad de MDM en Configuration Manager.
4.  Haga clic en **Siguiente** y complete el asistente.
5.  Ahora se ha restablecido la entidad de MDM. La suscripción a Intune ya no debe mostrarse en el nodo Suscripciones a Microsoft Intune de la consola de Configuration Manager.
6.  Inicie sesión en la [Consola de administración de Microsoft Intune](http://manage.microsoft.com) utilizando el mismo inquilino de Intune que usó anteriormente.
7.  Confirme que se ha restablecido la entidad de MDM y luego configure la entidad de MDM como **Microsoft Intune**. Después de cambiar la entidad de MDM, debería ver que se refleja en la consola. Para obtener más información, consulte [Configurar entidad de MDM](https://docs.microsoft.com/en-us/intune/deploy-use/prerequisites-for-enrollment#step-2-set-mdm-authority).
<!-- [Azure portal](https://docs.microsoft.com/en-us/intune-azure/enroll-devices/set-mdm-authority) -->


### <a name="configure-the-apns-certificate"></a>Configuración del certificado de Apple Push Notification Service
Cuando tenga los dispositivos iOS, debe configurar el certificado de Apple Push Notification Service en Intune.

#### <a name="to-configure-the-apns-certificate"></a>Para configurar el certificado de Apple Push Notification Service
1.  Descargue la solicitud de certificado de Apple Push Notification Service.
    <!--The process is different depending on how you connect to Intune:
    **Azure portal**   
    In the [Azure portal](https://azure.portal.com), choose **More Services** &gt; **Monitoring + Management** &gt; **Intune**. On the **Intune** blade, choose **Device enrollment** &gt; **Apple Enrollment** &gt; **Apple MDM Push Certificate**, and then select **Download your CSR** to download and save the .csr file locally.   
    <br/>
    **Microsoft Intune administration console**   -->
    En la [consola de administración de Microsoft Intune](http://manage.microsoft.com), vaya a **Administración** &gt; **Administración de dispositivos móviles** &gt; **iOS y Mac OS X** &gt; **Cargar un certificado de APNs** y luego elija **Descargar la solicitud de certificado de APNs**. Guarde la solicitud de firma de certificado (.csr) en el equipo local.
    > [!IMPORTANT]    
    > Debe descargar una nueva solicitud de firma de certificado. No utilice un archivo existente o se producirá un error.

    ![Descarga de la solicitud de certificado de Apple Push Notification Service](/sccm/mdm/deploy-use/media/mdm-change-download-apns-certificate.png)

2.  Vaya al portal [Apple Push Certificates Portal](http://go.microsoft.com/fwlink/?LinkId=269844) e inicie sesión con el **mismo** ID de Apple que se usó para crear y renovar anteriormente el certificado de Apple Push Notification Service que usó en Configuration Manager (híbrido).

    ![Página de inicio de sesión de Apple Push Notification Service](/sccm/mdm/deploy-use/media/mdm-change-apns-portal.png)

3.  Seleccione el certificado de Apple Push Notification Service que usó en Configuration Manager (híbrido) y, a continuación, haga clic en **Renovar**.   

    ![Cuadro de diálogo para renovar Apple Push Notification Service](/sccm/mdm/deploy-use/media/mdm-change-renew-apns.png)

4.  Seleccione la solicitud de firma del certificado de Apple Push Notification Service (.csr) que ha descargado localmente y, a continuación, haga clic en **Cargar**.

    ![Página de inicio de sesión de Apple Push Notification Service](/sccm/mdm/deploy-use/media/mdm-change-renew-apns-upload.png)  
5.  Seleccione el mismo Apple Push Notification Service y, a continuación, haga clic en **Descargar**. Descargue el certificado de Apple Push Notification Service (.pem) y guarde el archivo localmente.  

    ![Página de inicio de sesión de Apple Push Notification Service](/sccm/mdm/deploy-use/media/mdm-change-renew-apns-download.png)

6.  Cargue el certificado de Apple Push Notification Service renovado en el inquilino de Intune con el mismo ID de Apple que antes.
<!--The process is different depending on how to connect to Intune:  
    **Azure portal**   
    In the [Azure portal](https://azure.portal.com), choose **More Services** &gt; **Monitoring + Management** &gt; **Intune**. On the **Intune** blade, choose **Device enrollment** &gt; **Apple Enrollment**  &gt; **Apple MDM Push Certificate**, enter your Apple ID in step 3, select the certificate (.pem) file in step 4, and then click **Upload**.     
    <br/>
    **Microsoft Intune administration console**    -->
    In the [Microsoft Intune administration console](http://manage.microsoft.com), go to **Administration** &gt; **Mobile Device Management** &gt; **iOS and Mac OS X** &gt; **Upload an APNs Certificate**, and then choose **Upload the APNs certificate**. Go to the certificate (.pem) file, choose **Open**, and then enter your **Apple ID**.   

    ![Upload the APNs certificate](/sccm/mdm/deploy-use/media/mdm-change-upload-apns-certificate.png)

### <a name="next-steps"></a>Pasos siguientes
Una vez completado el cambio en la entidad de MDM, revise los siguientes pasos:
- Cuando el servicio de Intune detecta que ha cambiado la entidad de MDM de un inquilino, enviará un mensaje de notificación a todos los dispositivos inscritos para que inicien el proceso de comprobación y se sincronicen en el servicio (esto no forma parte de la comprobación programada regularmente). Por lo tanto, una vez que cambie la entidad de MDM para el inquilino de híbrido a Intune independiente, todos los dispositivos que estén encendidos y en línea se conectarán en el servicio, recibirán la nueva entidad de MDM y serán administrados en lo sucesivo por Intune independiente. No habrá ninguna interrupción en el proceso de administración y protección de estos dispositivos.
- Los dispositivos que estén apagados o sin conexión durante el cambio en la entidad de MDM (o poco tiempo después) se conectarán al servicio y se sincronizarán con él con la nueva entidad de MDM cuando estén encendidos y en línea.  

  Los dispositivos iOS requieren un tiempo adicional para renovar y configurar el certificado de Apple Push Notification Service. Por lo tanto, los dispositivos iOS no recibirán la solicitud de comprobación inicial. Incluso si los dispositivos iOS están encendidos y en línea durante el cambio en la entidad de MDM (o poco tiempo después), pasarán hasta 8 horas (según el tiempo de la siguiente comprobación periódica programada) hasta que los dispositivos iOS se registren en el servicio bajo la nueva entidad de MDM.    

  > [!IMPORTANT]
  > Entre el momento en que cambie la entidad MDM y se cargue el certificado de Apple Push Notification Service renovado en la nueva entidad, las inscripciones de nuevos dispositivos y las comprobaciones de dispositivos iOS darán error. Por lo tanto, es importante revisar y cargar el certificado de Apple Push Notification Service en la nueva entidad tan pronto como sea posible después del cambio de entidad de MDM.   

- Los usuarios pueden cambiar rápidamente a la nueva entidad de MDM iniciando manualmente una comprobación desde el dispositivo en el servicio. Los usuarios pueden hacerlo fácilmente mediante la aplicación Portal de empresa e iniciando una comprobación de cumplimiento del dispositivo.
- Para validar que todo funciona correctamente después de que los dispositivos se hayan comprobado y sincronizado con el servicio tras el cambio de entidad de MDM, busque los dispositivos en la [consola de administración de Microsoft Intune](http://manage.microsoft.com). Los dispositivos administrados anteriormente por Configuration Manager (híbrido) ahora aparecerán como dispositivos administrados.    
- Existe un período transitorio entre el momento en que un dispositivo está sin conexión durante el cambio de entidad de MDM y el momento en que se comprueba la idoneidad de ese dispositivo para su registro en el servicio. Para garantizar que el dispositivo permanece protegido y funcional durante este período transitorio, los elementos siguientes permanecerán en el dispositivo hasta 7 días (o hasta que el dispositivo se conecte con la nueva entidad de MDM y reciba la nueva configuración que sobrescribirá la actual):
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

<!-- After the change in MDM authority and devices check-in with the service, note the following:      - The updated compliance status of devices will only display in the Azure portal immediately.
- There will be a delay for compliance status of devices to display in the Intune administrative console.-->


## <a name="change-the-mdm-authority-to-configuration-manager-hybrid"></a>Cambio de la entidad de MDM a Configuration Manager (híbrido)
Use esta sección para cambiar un inquilino de Microsoft Intune configurado desde Intune y con la entidad de MDM configurada en **Microsoft Intune** (independiente) a **Configuration Manager** (híbrido) sin tener que anular y volver a crear la inscripción de los dispositivos administrados existentes.

### <a name="key-considerations"></a>Principales consideraciones
Después de cambiar a la nueva entidad de MDM, habrá probablemente un tiempo de transición (hasta 8 horas) antes de que el dispositivo se compruebe y se sincronice con el servicio. Será necesario que configure los parámetros en la nueva entidad de MDM (híbrido) para asegurarse de que los dispositivos inscritos seguirán administrados y protegidos después del cambio. y tenga en cuenta lo siguiente:
- Los dispositivos deben conectarse al servicio después del cambio para que la configuración de la nueva entidad de MDM (Intune independiente) reemplace la configuración existente en el dispositivo.
- Después de cambiar la entidad de MDM, algunas de las opciones básicas (como los perfiles) de la entidad de MDM anterior (Intune independiente) permanecerán en el dispositivo durante 7 días o hasta que el dispositivo se conecte al servicio por primera vez. Se recomienda que configure aplicaciones y parámetros (directivas, perfiles, aplicaciones, etc.) en la nueva entidad de MDM (híbrida) tan pronto como sea posible y que implemente la configuración en los grupos de usuarios que contienen usuarios con dispositivos ya inscritos. En cuanto el dispositivo se conecte con el servicio tras el cambio en la entidad de MDM, recibirá la nueva configuración desde la nueva entidad de MDM, evitando así los tiempos de inactividad en administración y protección.

### <a name="prepare-to-change-the-mdm-authority-to-configuration-manager-hybrid"></a>Preparación del cambio de la entidad de MDM a Configuration Manager (híbrido)
Revise la información siguiente para preparar el cambio de la entidad de MDM:
- Debe tener la versión 1610 de Configuration Manager o una posterior para que la opción para cambiar la entidad de MDM esté disponible.
- Un dispositivo puede tardar hasta 8 horas en conectarse al servicio después de cambiar a la nueva entidad de MDM.
- Cree una recopilación de usuarios de Configuration Manager con todos los usuarios que están administrados por Intune independiente que utilizará al configurar la suscripción de Intune en la consola de Configuration Manager. De este modo se asegurará de que el usuario y sus dispositivos tienen una licencia de Configuration Manager asignada y administrada en el entorno híbrido después del cambio a la entidad de MDM.
- Asegúrese de que el usuario Administrador de TI se encuentra también en la recopilación de usuarios.  
- Antes del cambio, la entidad de MDM aparecerá como **Establecer en Microsoft Intune** (independiente) en la consola de administración de Intune.
- La entidad de MDM debe mostrar **Establecer en Microsoft Intune** (inquilino independiente) en la consola de administración de Microsoft Intune antes del cambio en la entidad de MDM.
    > [!NOTE]    
    > Si la entidad de MDM muestra **Managed by Intune and Office 365** (Administrado por Intune y Office 365), los dispositivos de MDM administrados por Office 365 dejarán de estar administrados cuando cambie la entidad de MDM a **Configuration Manager** (híbrido). Se recomienda asignar licencias a esos usuarios para Intune o Enterprise Mobility Suite antes de cambiar la entidad de MDM.   

- En la [consola de administración de Microsoft Intune](http://manage.microsoft.com), vaya al rol Administrador de inscripción de dispositivos. Para ver más información, consulte [Eliminar un administrador de inscripción de dispositivos de Intune](/intune-classic/deploy-use/enroll-corporate-owned-devices-with-the-device-enrollment-manager-in-microsoft-intune#delete-a-device-enrollment-manager-from-intune).
- Desactive las asignaciones de grupos de dispositivos que estén configuradas. Para obtener más información, consulte [Clasificar los dispositivos con la asignación de grupos de dispositivos en Microsoft Intune](/intune-classic/deploy-use/categorize-devices-with-device-group-mapping-in-microsoft-intune).
- No debería haber ningún impacto perceptible en los usuarios finales durante el cambio de entidad de MDM. Sin embargo, puede comunicar este cambio a los usuarios para asegurarse de que sus dispositivos están encendidos y de que se conectan al servicio pronto después del cambio. De este modo, estará seguro de que se conectan tantos dispositivos como sea posible al servicio y de que se registran en la nueva entidad lo antes posible.
- Si usa Intune independiente para administrar dispositivos iOS antes del cambio de la entidad de MDM, debe asegurarse de que el mismo certificado de servicio de Apple Push Notification Service que se había utilizado previamente en Intune se renueva y se utiliza para configurar el inquilino de nuevo en Configuration Manager (híbrido).    

    > [!IMPORTANT]  
    > Si se utiliza un certificado diferente de Apple Push Notification Service para el inquilino híbrido, se anulará la inscripción de TODOS los dispositivos iOS y tendrá que repetir su proceso de inscripción. Antes de realizar el cambio en la entidad de MDM, asegúrese de que sabe exactamente qué certificado de Apple Push Notification Service se utilizó para administrar dispositivos iOS en Intune. Busque el mismo certificado en el portal Apple Push Certificates Portal (https://identity.apple.com) y asegúrese de que el usuario cuyo ID de Apple se usó para crear el certificado original de Apple Push Notification Service está identificado y disponible para renovar el mismo certificado de Apple Push Notification Service como parte del cambio a la nueva entidad de MDM.  

### <a name="change-the-mdm-authority-to-configuration-manager"></a>Cambio de la entidad de MDM a Configuration Manager
El proceso para cambiar la entidad de MDM a Configuration Manager (híbrido) incluye los siguientes pasos de alto nivel:  
- En la consola de Configuration Manager, agregue la inscripción de Microsoft Intune.
- Configure el certificado de Apple Push Notification Service con el mismo certificado de Apple Push Notification Service que ha renovado.
- En la consola de Configuration Manager, configure e implemente las nuevas opciones de configuración y aplicaciones desde la nueva entidad de MDM (híbrido).
- La próxima vez que los dispositivos se conecten al servicio, se sincronizarán y recibirán la nueva configuración de la entidad de MDM.

#### <a name="to-change-the-mdm-authority-to-configuration-manager"></a>Para cambiar la entidad de MDM a Configuration Manager
1.  En la consola de Configuration Manager, vaya a **Administración** &gt; **Información general** &gt; **Cloud Services** &gt; **Suscripción a Microsoft Intune** y seleccione agregar una suscripción a Intune.
2.  Inicie sesión en el inquilino de Intune que usó originalmente al configurar la entidad de MDM en Intune y haga clic en **Siguiente**.
3.  Seleccione **Cambiar entidad de MDM a Configuration Manager** y haga clic en **Siguiente**.
4.  Seleccione la recopilación de usuarios que contendrá todos los usuarios que seguirán administrados por la nueva entidad de MDM híbrida.
5.  Haga clic en **Siguiente** y complete el asistente.  
5.  La entidad de MDM ahora se ha cambiado a **Configuration Manager**.
6.  Inicie sesión en la [consola de administración de Microsoft Intune](http://manage.microsoft.com) con el mismo inquilino de Intune y confirme que la entidad de MDM se ha cambiado a **Configurar como Configuration Manager**.


### <a name="enable-ios-enrollment"></a>Habilitar la inscripción en iOS
Cuando tenga los dispositivos iOS, debe configurar el certificado de Apple Push Notification Service en Configuration Manager.

#### <a name="to-enable-ios-enrollment-and-configure-the-apns-certificate"></a>Para habilitar la inscripción de iOS y configurar el certificado de Apple Push Notification Service

1. **Descarga de una solicitud de firma de certificado**

    1.  En la consola de Configuration Manager, vaya a **Administración** &gt; **Cloud Services** &gt; **Suscripciones a Microsoft Intune** y seleccione **Crear solicitud de certificado APN** para abrir el cuadro de diálogo **Solicitar petición de firma de certificado de Apple Push Notification Service**.  
    2.  Utilice la función**Examinar** para seleccionar la ruta de acceso donde se guardará el nuevo archivo de solicitud de firma de certificado (.csr). Guarde la solicitud de firma de certificado (.csr) en el equipo local.  
    3.  Haga clic en **Descargar**. El nuevo archivo .csr de Microsoft Intune se descarga y Configuration Manager lo guarda.   

    > [!IMPORTANT]
    > Debe descargar una nueva solicitud de firma de certificado. No utilice un archivo existente o se producirá un error.  

2.  Vaya al portal [Apple Push Certificates Portal](http://go.microsoft.com/fwlink/?LinkId=269844) e inicie sesión con el **mismo** ID de Apple que se usó para crear y renovar anteriormente el certificado de Apple Push Notification Service que usó en Intune independiente.

    ![Página de inicio de sesión de Apple Push Notification Service](/sccm/mdm/deploy-use/media/mdm-change-apns-portal.png)

3.  Seleccione el certificado de Apple Push Notification Service que usó en Intune independiente y, a continuación, haga clic en **Renovar**.   

    ![Cuadro de diálogo para renovar Apple Push Notification Service](/sccm/mdm/deploy-use/media/mdm-change-renew-apns.png)

4.  Seleccione la solicitud de firma del certificado de Apple Push Notification Service (.csr) que ha descargado localmente y, a continuación, haga clic en **Cargar**.

    ![Página de inicio de sesión de Apple Push Notification Service](/sccm/mdm/deploy-use/media/mdm-change-renew-apns-upload.png)  
5.  Seleccione el mismo Apple Push Notification Service y, a continuación, haga clic en **Descargar**. Descargue el certificado de Apple Push Notification Service (.pem) y guarde el archivo localmente.  

    ![Página de inicio de sesión de Apple Push Notification Service](/sccm/mdm/deploy-use/media/mdm-change-renew-apns-download.png)

6.  Cargue el certificado de Apple Push Notification Service renovado en el inquilino híbrido con el mismo ID de Apple que antes.

    1.  En la consola de Configuration Manager, vaya a **Administración** &gt; **Cloud Services** &gt; **Suscripción a Microsoft Intune** y seleccione **Configurar plataformas** &gt; **iOS**.  
    2.  En el cuadro de diálogo **Propiedades de suscripción a Microsoft Intune**, seleccione la pestaña **Certificado de APN** y haga clic para seleccionar la casilla **Habilitar inscripción de iOS y Mac OS X (MDM)**.  
    3.  Haga clic en **Examinar**y vaya al archivo de certificado de APNs (.cer) que descargó de Apple. Manager Configuration muestra la información del certificado de APNs. Haga clic en **Aceptar** para guardar en Intune el certificado de APNs.  

        ![Página de propiedades de la suscripción a Intune - iOS](/sccm/mdm/deploy-use/media/mdm-change-subscription-properties-ios.png)

### <a name="enable-android-enrollment"></a>Habilitar la inscripción de Android
1. En la consola de Configuration Manager, vaya a **Administración** &gt; **Cloud Services** &gt; **Suscripción a Microsoft Intune** y seleccione **Configurar plataformas** &gt; **Android**.  
2. Seleccione **Habilitar inscripción de Android** y haga clic en **Aceptar**.

### <a name="enable-windows-enrollment"></a>Habilitación de la inscripción de Windows
1. En la consola de Configuration Manager, vaya a **Administración** &gt; **Cloud Services** &gt; **Suscripción a Microsoft Intune** y seleccione **Configurar plataformas** &gt; **Windows**.  
2. Seleccione **Habilitar la inscripción de Windows** y haga clic en **Aceptar**.

### <a name="enable-windows-phone-enrollment"></a>Habilitación de la inscripción de Windows Phone
1. En la consola de Configuration Manager, vaya a **Administración** &gt; **Cloud Services** &gt; **Suscripción a Microsoft Intune** y seleccione **Configurar plataformas** &gt; **Windows Phone**.  
2. Seleccione la plataforma que desea habilitar y haga clic en **Aceptar**.


### <a name="next-steps"></a>Pasos siguientes
Una vez completado el cambio en la entidad de MDM, revise los siguientes pasos:
- Cuando el servicio de Intune detecta que ha cambiado la entidad de MDM de un inquilino, enviará un mensaje de notificación a todos los dispositivos inscritos para que inicien el proceso de comprobación y se sincronicen en el servicio (esto no forma parte de la comprobación programada regularmente). Por lo tanto, una vez que cambie la entidad de MDM para el inquilino de Intune independiente a híbrido, todos los dispositivos que estén encendidos y en línea se conectarán en el servicio, recibirán la nueva entidad de MDM y serán administrados en lo sucesivo por en inquilino híbrido. No habrá ninguna interrupción en el proceso de administración y protección de estos dispositivos.
- Incluso para los dispositivos que están encendidos y en línea durante el cambio en la entidad de MDM (o poco tiempo después), pasarán hasta 8 horas (según el tiempo de la siguiente comprobación periódica programada) hasta que los dispositivos se registren en el servicio bajo la nueva entidad de MDM.    

  > [!IMPORTANT]
  > Entre el momento en que cambie la entidad MDM y se cargue el certificado de Apple Push Notification Service renovado en la nueva entidad, las inscripciones de nuevos dispositivos y las comprobaciones de dispositivos iOS darán error. Por lo tanto, es importante revisar y cargar el certificado de Apple Push Notification Service en la nueva entidad tan pronto como sea posible después del cambio de entidad de MDM.

- Los usuarios pueden cambiar rápidamente a la nueva entidad de MDM iniciando manualmente una comprobación desde el dispositivo en el servicio. Pueden hacerlo fácilmente mediante la aplicación Portal de empresa e iniciando una comprobación de cumplimiento del dispositivo.
- Para validar que todo funciona correctamente después de que los dispositivos se hayan comprobado y sincronizado con el servicio tras el cambio de entidad de MDM, busque los dispositivos en la consola de Configuration Manager. Los dispositivos administrados anteriormente por Intune ahora aparecerán como dispositivos administrados en la consola de Configuration Manager.    
- Existe un período transitorio entre el momento en que un dispositivo está sin conexión durante el cambio de entidad de MDM y el momento en que se comprueba la idoneidad de ese dispositivo para su registro en el servicio. Para garantizar que el dispositivo permanece protegido y funcional durante este período transitorio, los elementos siguientes permanecerán en el dispositivo hasta 7 días (o hasta que el dispositivo se conecte con la nueva entidad de MDM y reciba la nueva configuración que sobrescribirá la actual):
    - Perfil de correo electrónico
    - Perfil de VPN
    - Perfil de certificado
    - Perfil de Wi-Fi
    - Perfiles de configuración
- Después de cambiar a la nueva entidad de MDM, los datos de cumplimiento de la consola de administración de Microsoft Intune pueden tardar hasta una semana en informar con exactitud. Sin embargo, los estados de cumplimiento de Azure Active Directory y en el dispositivo serán precisos para que el dispositivo siga estando protegido.
- Compruebe que la nueva configuración destinada a sobrescribir la configuración actual tiene el mismo nombre que la anterior para asegurarse de que efectivamente se sobrescribe. En caso contrario, los dispositivos podrían terminar con directivas y perfiles redundantes.
    > [!TIP]   
    > Es recomendable que cree todas las configuraciones y parámetros de administración, así como las implementaciones, poco después de que se haya completado el cambio a la entidad de MDM. De este modo se asegurará de que los dispositivos están protegidos y se administran de manera activa durante el período transitorio.   
-  Después de cambiar la entidad de MDM, siga estos pasos para validar que los nuevos dispositivos se inscriben correctamente en la nueva entidad:   
    - Inscripción de un dispositivo nuevo
    - Asegúrese de que el dispositivo recién inscrito aparece en la consola de Configuration Manager.
    - Realice una acción, como el bloqueo remoto, desde la consola de administración en el dispositivo. Si se completa correctamente, el dispositivo se está administrando mediante la nueva entidad de MDM.
- Si tiene problemas con dispositivos concretos, puede anular la inscripción de esos dispositivos y realizarla de nuevo para que se conecten a la nueva entidad y se administren lo antes posible.
