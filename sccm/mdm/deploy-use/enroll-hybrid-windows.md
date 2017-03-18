---
title: "Configurar la administración híbrida de dispositivos Windows con System Center Configuration Manager y Microsoft Intune | Microsoft Docs"
description: "Configure la administración de dispositivos Windows con System Center Configuration Manager y Microsoft Intune."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: dc1f70f5-64ab-42ab-aa91-d3858803e12f
caps.latest.revision: 9
author: mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: a4fc4a16c78b0eaa0dcefdd596b049eacf1d255b
ms.lasthandoff: 03/06/2017


---
# <a name="set-up-windows-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>Configurar la administración híbrida de dispositivos Windows con System Center Configuration Manager y Microsoft Intune

*Se aplica a: System Center Configuration Manager (rama actual)*

Puede usar Configuration Manager con Intune para administrar equipos de escritorio, equipos portátiles y otros dispositivos que ejecutan Windows como dispositivos móviles. Puede configurar Azure Active Directory para permitir la inscripción automática de PC Windows. También puede configurar Configuration Manager para que simplifique la inscripción al usar la aplicación de portal de empresa.


Entre las opciones de inscripción de Windows se incluyen las siguientes:

- [Inscripción automática con Azure AD](#azure-active-directory-enrollment)
- [PC Windows](#configure-windows-pc-enrollment)
- [Dispositivos Windows 10 Mobile y Windows Phone](#enable-windows-phone-devices)

## <a name="azure-active-directory-enrollment"></a>Inscripción con Azure Active Directory

La inscripción automática permite a los usuarios inscribir en Intune PC Windows 10 y dispositivos Windows 10 Mobile corporativos o personales. Para ello, deben agregar una cuenta profesional o educativa y aceptar que se administre. En segundo plano, el dispositivo del usuario se registra y se une a Azure Active Directory. Una vez que se ha registrado, el dispositivo puede administrarse con Intune.

**Requisitos previos**
- Suscripción a Azure Active Directory Premium ([suscripción de prueba](http://go.microsoft.com/fwlink/?LinkID=816845))
- Suscripción a Microsoft Intune


### <a name="configure-automatic-mdm-enrollment"></a>Configurar la inscripción de MDM automática

1. En el [Portal de administración de Azure](https://manage.windowsazure.com) (https://manage.windowsazure.com), vaya al nodo **Active Directory** y seleccione su directorio.

2. Haga clic en la pestaña **Aplicaciones** y verá **Microsoft Intune** en la lista de aplicaciones.

    ![Aplicaciones de Azure AD con Microsoft Intune](../media/aad-intune-app.png)

3. Haga clic en la flecha de **Microsoft Intune** y verá una página que le permite configurar Microsoft Intune.

4. Haga clic en **Configurar** para empezar a configurar la inscripción de MDM automática con Microsoft Intune.

5. Especifique las direcciones URL de Intune:

  - **Dirección URL de inscripción de MDM**: use el valor predeterminado.
  - **Dirección URL de términos de uso de MDM**: use el valor predeterminado. En esta dirección URL se muestran los términos de uso para los usuarios cuando realizan la inscripción de dispositivos.
  - **Dirección URL de cumplimiento de MDM**: use el valor predeterminado. Si se encuentra un dispositivo que no es compatible, se muestra el mensaje **Acceso denegado** con esta dirección URL. La dirección URL apunta a una página que ayuda a los usuarios a comprender por qué el dispositivo no es compatible con la directiva y cómo pueden conseguir que vuelva a serlo.

6.  Especifique qué dispositivos de los usuarios deben administrarse mediante Microsoft Intune. Los dispositivos Windows 10 de estos usuarios se inscribirán automáticamente para la administración con Microsoft Intune.

  - **Todos**
  - **Grupos**
  - **Ninguno**

7. Elija **Guardar**.

## <a name="configure-windows-pc-enrollment"></a>Configurar la inscripción de PC Windows
 Para habilitar la administración de dispositivos móviles Windows, debe habilitar la administración del sistema operativo.  También puede agregar un CNAME DNS para simplificar la inscripción de los usuarios.

### <a name="create-dns-alias-for-device-enrollment"></a>Creación de un alias DNS para la inscripción de dispositivos  
 Un alias DNS (tipo de registro CNAME) facilita a los usuarios la inscripción de sus dispositivos, ya que rellena automáticamente el nombre del servidor durante la inscripción. Para crear un alias DNS (tipo de registro CNAME), tendrá que configurar un CNAME en los registros DNS de su empresa que redirija las solicitudes enviadas a una dirección URL del dominio de su empresa a servidores de servicios en la nube de Microsoft.  Por ejemplo, si el dominio de su empresa es contoso.com, debe crear un CNAME en DNS que redirija EnterpriseEnrollment.contoso.com a EnterpriseEnrollment-s.manage.microsoft.com.  

 Aunque la creación de entradas DNS CNAME es opcional, los registros CNAME facilitan la inscripción para los usuarios. Si no se encuentra ningún registro CNAME de inscripción, se pedirá a los usuarios que escriban de forma manual el nombre del servidor MDM (enrollment.manage.microsoft.com).

|Tipo|Nombre de host|Apunta a|  
|----------|---------------|---------------|  
|CNAME|EnterpriseEnrollment.company_domain.com|EnterpriseEnrollment-s.manage.microsoft.com|  
|CNAME|EnterpriseRegistration.company_domain.com|EnterpriseRegistration.windows.net|  
### <a name="to-enable-enrollment-for-windows-devices"></a>Para habilitar la inscripción de dispositivos Windows  

1.  **Requisitos previos**: para poder configurar la inscripción en cualquier plataforma, complete los requisitos previos y los procedimientos de [Setup hybrid MDM](setup-hybrid-mdm.md) (Configurar la MDM híbrida).  

2.  En la consola de Configuration Manager, en el área de trabajo **Administración** , vaya a **Servicios en la nube** > **Suscripciones a Microsoft Intune**.  

    > [!WARNING]  
    >  Si hay abierto otro cuadro de diálogo de Configuration Manager, ciérrelo antes de continuar con este procedimiento.  

3.  En la pestaña **Inicio** , haga clic en **Configurar plataformas**y, a continuación, haga clic en **Windows**.  

4.  En la pestaña **General** , seleccione **Habilitar la inscripción de Windows**.  

 Cuando esté listo, necesitará que los usuarios sepan cómo inscribir sus dispositivos. Consulte [Qué decirles a los usuarios finales sobre el uso de Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune). Esta información se aplica a Microsoft Intune y a dispositivos móviles administrados por Configuration Manager.

## <a name="enable-windows-phone-devices"></a>Habilitar dispositivos Windows Phone  
  Si los usuarios solo inscribirán dispositivos con Windows Phone 8.1 y posterior y no implementarán aplicaciones de línea de negocio en dispositivos Windows Phone, no es necesario ningún certificado de Symantec. Después de habilitar la inscripción de Windows Phone, debe indicar a los usuarios que instalen la aplicación Portal de empresa desde la Tienda de Windows Phone para inscribir sus dispositivos.  

  Complete los siguientes pasos para los dispositivos Windows Phone que vaya a administrar.  

### <a name="to-enable-enrollment-for-windows-phone-81-and-later-devices"></a>Para habilitar la inscripción de dispositivos con Windows Phone 8.1 y posterior  

 1.  **Requisitos previos**: para poder configurar la inscripción en cualquier plataforma, complete los requisitos previos y los procedimientos de [Setup hybrid MDM](setup-hybrid-mdm.md) (Configurar la MDM híbrida).  

 2.  En la consola de Configuration Manager, en el área de trabajo **Administración** , vaya a **Servicios en la nube** > **Suscripciones a Microsoft Intune**.  

     > [!WARNING]  
     >  Si hay abierto otro cuadro de diálogo de Configuration Manager, ciérrelo antes de continuar con este procedimiento.  

 3.  En la pestaña **Inicio** , haga clic en **Configurar plataformas**y, a continuación, haga clic en **Windows Phone**.  

 4.  En la pestaña **General** , elija  **Windows Phone 8.1 y Windows 10 Mobile**. Puede cargar datos de archivo AET .xml o un archivo .pfx para admitir la implementación del Portal de empresa, o indicar a los usuarios que descarguen el Portal de empresa de la Tienda de Windows Phone.  

      Haga clic en **Aceptar**.  

  Cuando esté listo, necesitará que los usuarios sepan cómo inscribir sus dispositivos. Consulte [Qué decirles a los usuarios finales sobre el uso de Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune). Esta información se aplica a Microsoft Intune y a dispositivos móviles administrados por Configuration Manager.  

  > [!div class="button"]
  [< Paso anterior](create-service-connection-point.md)  [Paso siguiente >](set-up-additional-management.md)

