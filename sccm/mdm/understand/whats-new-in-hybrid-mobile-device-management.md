---
title: "Novedades de la MDM híbrida con Configuration Manager | Microsoft Docs"
description: "Obtenga información sobre las nuevas características de administración de dispositivos móviles disponibles para implementaciones híbridas con Configuration Manager e Intune."
ms.custom: na
ms.date: 06/30/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b127cee-61f1-4681-9760-caebed36ddf5
caps.latest.revision: "40"
author: Mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: 93609815ab4d93eddb99b8461dda9f4b4bf8058e
ms.sourcegitcommit: 9a6f8e028fb5eb2e752da70f42a5b548339bd8f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/14/2017
---
# <a name="whats-new-in-hybrid-mobile-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>Novedades de la administración híbrida de dispositivos móviles con System Center Configuration Manager y Microsoft Intune

*Se aplica a: System Center Configuration Manager (rama actual)*

En este artículo se proporciona información sobre nuevas características de administración de dispositivos móviles (MDM) disponibles para implementaciones híbridas con System Center Configuration Manager y Microsoft Intune.  

##  <a name="compatibility-with-configuration-manager-versions"></a>Compatibilidad con versiones de Configuration Manager  

 En cada sección de este artículo se enumeran las características híbridas organizadas en tres categorías diferentes. Use las indicaciones siguientes para determinar la compatibilidad de las características de cada categoría con las diferentes versiones de Configuration Manager:  

|Categorías de características|Descripción|
|-|-|
|**Novedades de Microsoft Intune** | En general, todas las características que se enumeran en esta categoría deberían funcionar con todas las versiones de Configuration Manager, incluidas las versiones de System Center 2012 R2 Configuration Manager, ya que estas características solo necesitan el servicio de Intune y ninguna función adicional en Configuration Manager.|
|**Novedades de Configuration Manager Technical Preview**| Todas las funciones que se enumeran en esta categoría funcionan únicamente con la versión especificada de Technical Preview. Para probar estas características, debe instalar la versión de Technical Preview especificada en la descripción de la característica. Para más información, consulte [Technical Preview for System Center Configuration Manager](../../core/get-started/technical-preview.md) (Technical Preview para System Center Configuration Manager).|
|**Novedades de Configuration Manager (rama actual)**| Todas las características que se enumeran en esta categoría funcionan únicamente con la versión especificada de Configuration Manager (rama actual), como la versión 1511 o 1602. Si usa una versión anterior de Configuration Manager para su implementación híbrida, debe actualizar a la versión de Configuration Manager (rama actual) que se especifica en la descripción de la característica. Para obtener más información, consulte [Upgrade to System Center Configuration Manager](../../core/servers/deploy/install/upgrade-to-configuration-manager.md) (Actualizar a System Center Configuration Manager).|

## <a name="july-2017"></a>Julio de 2017

### <a name="new-in-microsoft-intune"></a>Novedades de Microsoft Intune

- **Nuevos avisos de finalización del soporte para Android y Windows Phone**

    Se agregaron nuevos avisos de finalización del soporte para las versiones de Android y Windows Phone. Para obtener más información, consulte [Notificaciones](#notices).



### <a name="new-in-configuration-manager-current-branch"></a>Novedades de Configuration Manager (rama actual)

Las siguientes características que estaban disponibles en versiones de Configuration Manager Technical Preview están ahora disponibles en implementaciones híbridas con Intune y la versión 1706 de Configuration Manager (rama actual).

- [Compatibilidad con Entrust para entidades de certificación de Entrust](/sccm/core/get-started/capabilities-in-technical-preview-1706#support-for-entrust-certification-authorities)
- [Configuración de nueva directiva de administración de aplicaciones móviles](/sccm/core/plan-design/changes/whats-new-in-version-1706#new-mobile-application-management-policy-settings)
- [Actualizaciones a Android para la configuración de uso compartido del trabajo](/sccm/core/plan-design/changes/whats-new-in-version-1706#updates-to-android-for-work-sharing-configuration)
- [Nuevas reglas de directiva de cumplimiento de dispositivos](/sccm/core/plan-design/changes/whats-new-in-version-1706#new-device-compliance-policy-rules)
- [Nuevas opciones de configuración para dispositivos Windows 10 que no están administrados con el cliente de Configuration Manager](/sccm/core/plan-design/changes/whats-new-in-version-1706#new-configuration-settings-for-windows-10-devices-that-are-not-managed-with-the-configuration-manager-client)
- [Compatibilidad con Cisco (IPsec) para perfiles de VPN de macOS](/sccm/core/get-started/capabilities-in-technical-preview-1706#cisco-ipsec-support-for-macos-vpn-profiles)
- [Restricciones de inscripción de iOS y Android](/sccm/core/plan-design/changes/whats-new-in-version-1706#android-and-ios-enrollment-restrictions) 

## <a name="june-2017"></a>Junio de 2017

### <a name="new-in-microsoft-intune"></a>Novedades de Microsoft Intune

- **Cambiar la entidad de MDM**

  A partir de la versión 1610 de Configuration Manager y la versión 1705 de Microsoft Intune, puede cambiar la entidad de MDM sin tener que ponerse en contacto con el soporte técnico de Microsoft y sin necesidad de anular y volver a crear la inscripción de sus dispositivos administrados existentes. Para obtener más información, consulte [Cambio de la entidad de MDM]( /sccm/mdm/deploy-use/change-mdm-authority).

- **Integración del proxy de la aplicación y Managed Browser**

  El explorador Intune Managed Browser ahora puede integrarse con el servicio Proxy de aplicación de Azure AD para que los usuarios puedan tener acceso a los sitios web internos incluso cuando trabajan de forma remota. Los usuarios del explorador simplemente escriben la dirección URL del sitio como harían normalmente y el explorador Managed Browser enruta la solicitud a través de la puerta de enlace web del proxy de aplicación. Para obtener más información, consulte [Administrar el acceso a Internet mediante directivas de explorador administrado](/intune/app-configuration-managed-browser).

- **Ahora, la aplicación Portal de empresa para Android tiene una nueva experiencia de usuario final para las directivas de protección de aplicaciones**

  A raíz de los comentarios de clientes, hemos modificado la aplicación Portal de empresa para Android para que aparezca el botón **Acceso al contenido de la empresa**. El objetivo es impedir que los usuarios finales pasen innecesariamente por el proceso de inscripción cuando solo necesitan acceder a las aplicaciones que admiten directivas de protección de aplicaciones, una característica de administración de aplicaciones móviles de Intune. Puede ver estos cambios en la página [Novedades de la interfaz de usuario de aplicaciones](/intune/whats-new-app-ui).

- **Nueva acción de menú para quitar fácilmente el Portal de empresa**

  A raíz de los comentarios de los usuarios, se ha agregado en la aplicación Portal de empresa para Android una nueva acción de menú para iniciar la eliminación del Portal de empresa desde el dispositivo. Con esta acción se quita el dispositivo de administración de Intune para que la aplicación se pueda quitar del dispositivo por parte del usuario. Puede ver estos cambios en la página de [novedades de la interfaz de usuario de aplicaciones](/intune/whats-new-app-ui) y en la [documentación de Android para el usuario final](/intune-user-help/unenroll-your-device-from-intune-android).

- **Mejoras en la sincronización de aplicaciones con Windows 10 Creators Update**

  Ahora, la aplicación Portal de empresa para Windows 10 iniciará automáticamente una sincronización para las solicitudes de instalación de aplicaciones destinadas a dispositivos con Windows 10 Creators Update (versión 1703). De este modo, se reducirá la incidencia del problema por el cual las instalaciones de aplicaciones se detienen durante el estado "Sincronización pendiente". Además, los usuarios podrán iniciar manualmente la sincronización desde la aplicación. Puede ver estos cambios en la página [Novedades de la interfaz de usuario de aplicaciones](/intune/whats-new-app-ui).

- **Nueva experiencia guiada para el Portal de empresa de Windows 10**

  La aplicación de Portal de empresa para Windows 10 incluirá una experiencia guiada de tutorial de Intune para dispositivos que no se han identificado o inscrito. La nueva experiencia proporciona instrucciones paso a paso que guían al usuario a través del registro en Azure Active Directory (necesario para las características de acceso condicional) y la inscripción de MDM (necesario para las características de administración de dispositivos). Será posible acceder a esta experiencia guiada desde la página de inicio del Portal de empresa. Los usuarios pueden seguir utilizando la aplicación si no completan el registro y la inscripción, pero experimentarán una funcionalidad limitada.

  Esta actualización solo está visible en dispositivos que ejecutan Actualización de aniversario de Windows 10 (compilación 1607) o superior. Puede ver estos cambios en la página [Novedades de la interfaz de usuario de aplicaciones](/intune/whats-new-app-ui).

- **Mejoras en los iconos de aplicación en la aplicación Portal de empresa para iOS**

  Se ha actualizado el diseño de los iconos de aplicación en la página principal para reflejar el color de personalización de marca que establezca para el Portal de empresa. Para obtener más información, consulte [Novedades de la interfaz de usuario de aplicaciones](/intune/whats-new-app-ui).

- **El selector de cuenta ya está disponible para la aplicación Portal de empresa para iOS**

  Los usuarios de dispositivos iOS pueden ver nuestro nuevo selector de cuenta cuando inician sesión en el Portal de empresa si usan su cuenta profesional o educativa para iniciar sesión en otras aplicaciones de Microsoft. Para obtener más información, consulte [Novedades de la interfaz de usuario de aplicaciones](/intune/whats-new-app-ui).

### <a name="new-in-configuration-manager-technical-preview-1706"></a>Novedades de Configuration Manager Technical Preview 1706

- **Configuración de nueva directiva de administración de aplicaciones móviles**    

  Ahora están disponibles las siguientes opciones de configuración de directiva de administración de aplicaciones móviles:

  - **Bloquear captura de pantalla	(solo dispositivos Android):** especifica que las funciones de captura de pantalla del dispositivo se bloquean cuando se usa esta aplicación.
  - **Deshabilitar sincronización de contactos:** impide que la aplicación guarde los datos en la aplicación de contactos nativa del dispositivo.
  - **Deshabilitar la impresión:** impide que la aplicación imprima datos profesionales o educativos.

  Vea [Proteger aplicaciones mediante directivas de administración de aplicaciones móviles en System Center Configuration Manager](https://docs.microsoft.com/sccm/mdm/deploy-use/protect-apps-using-mam-policies) para probar la nueva configuración de la directiva de protección de aplicaciones.

- **Nueva configuración de elemento de configuración de Windows** <!-- 1354715 -->    

  Hay nuevos elementos de configuración de Windows disponibles para las categorías de ajustes Contraseña, Dispositivo, Tienda y Microsoft Edge. Para obtener más información, vea [Nuevas opciones para elementos de configuración de Windows](/sccm/core/get-started/capabilities-in-technical-preview-1706#new-windows-configuration-item-settings).

- **Nuevas reglas de directiva de cumplimiento de dispositivos**    

  Ahora puede configurar nuevas opciones de directivas de cumplimiento que anteriormente solo estaban disponibles en Intune independiente. Para obtener más información, consulte [Mejoras de la directiva de cumplimiento de dispositivos](/sccm/core/get-started/capabilities-in-technical-preview-1706#new-device-compliance-policy-rules).

- **Restricciones de inscripción de iOS y Android** <!-- 1290826 -->      

  Los administradores ahora pueden especificar que los usuarios no inscriban los dispositivos personales de Android o iOS en su entorno híbrido. Gracias a esto, se podrán limitar los dispositivos inscritos a aquellos declarados con anterioridad que pertenezcan a la empresa, o bien a aquellos dispositivos iOS inscritos solo con el Programa de inscripción de dispositivos. Para obtener más información, consulte [Restricciones de inscripción de iOS y Android](/sccm/core/get-started/capabilities-in-technical-preview-1706#android-and-ios-enrollment-restrictions).

- **Compatibilidad con entidades de certificación de Entrust** <!-- 1350740 -->     

  Configuration Manager ahora es compatible con entidades de certificación de Entrust; esto habilita la entrega de certificados PFX a dispositivos inscritos en Microsoft Intune.    

  Puede configurar Entrust como entidad de certificación al agregar un rol de Punto de registro de certificados en Configuration Manager. Al agregar un nuevo perfil de certificado que emite certificados PFX, puede seleccionar una entidad de certificación de Microsoft o Entrust.

  **Problema conocido**: en la versión 1706 de Technical Preview, no se emiten certificados PFX para entidades de certificación de Microsoft. Esto no afecta a los certificados PFX o los perfiles de SCEP importados.

- **Compatibilidad con Cisco (IPsec) para perfiles de VPN de macOS** <!-- 1321367 -->    

  Puede crear un perfil de VPN de macOS con Cisco (IPsec) como tipo de conexión. Para obtener más información, vea [Crear perfiles de VPN](/sccm/mdm/deploy-use/create-vpn-profiles#create-vpn-profiles).


## <a name="april-2017"></a>Abril de 2017

### <a name="new-in-microsoft-intune"></a>Novedades de Microsoft Intune

- **MyApps está disponible para Managed Browser**

  Ahora, Microsoft MyApps ofrece una mejor compatibilidad con Managed Browser. Los usuarios de Managed Browser que no estén destinados a la administración se redirigirán directamente al servicio MyApps, donde podrán acceder a sus aplicaciones de SaaS aprovisionadas por el administrador. Los usuarios destinados a la administración de Intune seguirán teniendo acceso a MyApps desde el marcador de Managed Browser integrado.

- **Nuevos iconos para Managed Browser y Portal de empresa**

  Managed Browser recibirá iconos actualizados para la versión de la aplicación de Android y la de iOS. El nuevo icono contendrá la notificación de Intune actualizada para que sea más coherente con otras aplicaciones de Enterprise Mobility + Security (EM+S). Puede ver el icono nuevo de Managed Browser en la [página de novedades de la UI de la aplicación de Intune](/intune/whats-new/whats-new-in-intune-app-ui.md).

  Portal de empresa también recibirá iconos actualizados para las versiones de Windows, iOS y Android de la aplicación a fin de mejorar la coherencia con otras aplicaciones de EM+S. Estos iconos se lanzarán gradualmente en las distintas plataformas desde abril hasta finales de mayo.

- **Indicador de progreso de inicio de sesión del Portal de empresa para Android**

  Una actualización de la aplicación Portal de empresa para Android muestra un indicador de progreso de inicio de sesión cuando el usuario inicia o reanuda la aplicación. El indicador avanza por los nuevos estados, desde "Conectando..." e "Iniciando sesión..." hasta "Comprobando los requisitos de seguridad...", antes de permitir que el usuario acceda a la aplicación. Puede ver las nuevas pantallas de la aplicación Portal de empresa para Android en la [página de novedades de la UI de la aplicación Intune](/intune/whats-new/whats-new-in-intune-app-ui.md).

- **Bloquear el acceso de las aplicaciones a SharePoint Online**

  Ahora puede crear una directiva de acceso condicional basada en aplicaciones para bloquear el acceso a [SharePoint Online](/InTune/deploy-use/mam-ca-for-sharepoint-online) a aquellas aplicaciones a las que no se apliquen directivas de protección. En el escenario de acceso condicional basado en aplicaciones, puede especificar las aplicaciones que quiere que tengan acceso a SharePoint Online mediante Azure Portal.

### <a name="new-in-configuration-manager-technical-preview-1704"></a>Novedades de Configuration Manager Technical Preview 1704

- **Configuración de aplicaciones de Android con directivas de configuración de aplicaciones**

  Puede usar directivas de configuración de aplicaciones en System Center Configuration Manager (Configuration Manager) para distribuir valores preconfigurados cuando un usuario ejecuta una aplicación en dispositivos de Android for Work. Las directivas de configuración de aplicaciones Android solo están disponibles en dispositivos que ejecutan Android for Work y se aplican a las aplicaciones aprobadas en la tienda Play for Work. Para más información sobre cómo probar esta característica, consulte [Configure Android apps with app configuration policies](/sccm/core/get-started/capabilities-in-technical-preview-1704#configure-android-apps-with-app-configuration-policies) (Configuración de aplicaciones Android con directivas de configuración de aplicaciones).

## <a name="march-2017"></a>Marzo de 2017

### <a name="new-in-microsoft-intune"></a>Novedades de Microsoft Intune

- **Nueva experiencia de usuario para la aplicación Portal de empresa para Android**

  La interfaz de usuario de la aplicación Portal de empresa para Android tiene una apariencia más moderna. Las actualizaciones importantes son:

  - Colores: los encabezados de las pestañas de Portal de empresa están coloreados con la personalización de marca definida por TI.
  - Aplicaciones: en la pestaña **Aplicaciones**, se han actualizado los botones **Aplicaciones destacadas** y **Todas las aplicaciones**.
  - Búsqueda: en la pestaña **Aplicaciones**, el botón **Buscar** es un botón de acción flotante.
  - Navegar por las aplicaciones: la vista **Todas las aplicaciones** muestra una vista con las pestañas **Destacadas**, **Todas** y **Categorías** para facilitar la navegación.
  - Soporte técnico: las pestañas **Mis dispositivos** y **Contactar con TI** se han actualizado para mejorar la legibilidad.

  Para obtener más información sobre estos cambios, consulte [Actualizaciones de la interfaz de usuario para las aplicaciones de usuario final de Intune](/intune/whats-new/whats-new-in-intune-app-ui).

- **Script de firma para Portal de empresa de Windows 10**

  Si necesita descargar y transferir localmente la aplicación de Portal de empresa de Windows 10, ahora puede usar un script para simplificar y agilizar el proceso de firma de aplicaciones para su organización.  Para descargar el script y las instrucciones para usarlo, vea [Microsoft Intune Signing Script for Windows 10 Company Portal](https://aka.ms/win10cpscript) (Script de firma de Microsoft Intune para Portal de empresa de Windows 10) en la Galería de TechNet. Para obtener más información sobre este anuncio, consulte [Updating your Windows 10 Company Portal app](https://blogs.technet.microsoft.com/intunesupport/2017/03/13/updating-your-windows-10-company-portal-app/) (Actualización de la aplicación Portal de empresa para Windows 10) en el blog del equipo de soporte técnico de Intune.

- **Compatibilidad mejorada para los usuarios de Android con base en China**

  Debido a la ausencia de Google Play Store en China, los dispositivos Android deben obtener las aplicaciones de mercados chinos. El Portal de empresa admite este flujo de trabajo mediante la redirección de los usuarios de Android de China a tiendas de aplicaciones locales donde podrán descargar las aplicaciones Portal de empresa y Outlook. De esta forma, se mejora la experiencia del usuario cuando se habilitan las directivas de acceso condicional, tanto para la administración de dispositivos móviles como para la administración de aplicaciones móviles. Las aplicaciones Portal de empresa y Outlook para Android están disponibles en las siguientes tiendas de aplicaciones chinas:

  - [Baidu](https://go.microsoft.com/fwlink/?linkid=836946)
  - [Xiaomi](https://go.microsoft.com/fwlink/?linkid=836947)
  - [Tencent](https://go.microsoft.com/fwlink/?linkid=836949)
  - [Huawei](https://go.microsoft.com/fwlink/?linkid=836948)
  - [Wandoujia](https://go.microsoft.com/fwlink/?linkid=836950)

- **Asegurarse de que las aplicaciones de Portal de empresa están actualizadas**

  En diciembre de 2016, se publicó una actualización que habilitaba la aplicación de la autenticación multifactor (MFA) en un grupo de usuarios cuando inscribían un dispositivo iOS, Android, Windows 8.1+ o Windows Phone 8.1+. Esta característica no puede funcionar sin determinadas versiones de línea base de la aplicación Portal de empresa para iOS (v2.1.17+) y Android (v5.0.3419.0+).

  Las capacidades de administración de Intune se mejoran continuamente y numerosas mejoras han coordinado las actualizaciones de las aplicaciones de Portal de empresa en todas las plataformas compatibles. Como resultado, se recomienda mantener activadas las versiones más recientes de las aplicaciones de Portal de empresa instaladas en los dispositivos para aprovechar las mejoras en Intune y para obtener la mejor experiencia de usuario.

  >[!Tip]
  > Pida a los usuarios que configuren los dispositivos para actualizar automáticamente las aplicaciones desde la tienda de aplicaciones correspondiente. Si la aplicación de Portal de empresa para Android está disponible en un recurso compartido de red, se puede descargar la versión más reciente desde el [Centro de descarga de Microsoft](https://www.microsoft.com/download/details.aspx?id=49140).

- **Microsoft Teams ahora está habilitado para MAM en iOS y Android**

  Las aplicaciones de Microsoft Teams para iOS y Android están ahora habilitadas con capacidades de administración de aplicaciones móviles (MAM) de Intune, para poder permitir a los equipos trabajar con libertad entre dispositivos, mientras se garantiza que las conversaciones y los datos de la empresa están protegidos en todo momento. Para obtener más detalles, vea [el anuncio de Microsoft Teams](https://blogs.technet.microsoft.com/enterprisemobility/2017/03/14/microsoft-teams-is-now-generally-available-and-mam-enabled-on-ios-and-android/) en el blog de seguridad y movilidad empresarial.

### <a name="new-in-configuration-manager-technical-preview-1703"></a>Novedades de Configuration Manager Technical Preview 1703

- **Mayor compatibilidad para el Programa de Compras por Volumen de Apple**

   A partir de la versión 1703 de Technical Preview, los siguientes casos del Programa de Compras por Volumen (VPP) ahora son compatibles:

   - Concesión de licencias de dispositivos: las aplicaciones que sean compatibles con la concesión de licencias de dispositivos y estén implementadas en colecciones de dispositivos solo necesitarán una licencia por dispositivo.  Anteriormente era necesario usar una licencia por cada usuario en un dispositivo. Para obtener más información, consulte [Implementación de aplicaciones iOS adquiridas por volumen en colecciones de dispositivos](/sccm/core/get-started/capabilities-in-technical-preview-1703#deploy-volume-purchased-ios-apps-to-device-collections).
   - Uso de varios tokens del VPP en un único inquilino híbrido con ambos tokens en uso para la administración de aplicaciones del VPP.
   - Uso de tokens del VPP para educación con la capacidad para distinguir entre tokens de empresas e instituciones educativas.

### <a name="new-in-configuration-manager-current-branch"></a>Novedades de Configuration Manager (rama actual)

Las siguientes características que estaban disponibles en versiones de Configuration Manager Technical Preview están ahora disponibles en implementaciones híbridas con Intune y la versión 1702 de Configuration Manager (rama actual).

- [Compatibilidad de Android for Work](/sccm/core/plan-design/changes/whats-new-in-version-1702##android-for-work-support)
- [Configuración de cumplimiento de aplicaciones no compatibles](/sccm/core/plan-design/changes/whats-new-in-version-1702#conditional-access-device-compliance-policy-improvements)
- [Creación y distribución de certificados PFX y compatibilidad con S/MIME](/sccm/core/plan-design/changes/whats-new-in-version-1702#improvements-to-certificate-profiles)
- [En los asistentes para creación de MDM híbrida, ya no se pueden seleccionar como destino las versiones de iOS y Android](/sccm/core/plan-design/changes/whats-new-in-version-1702#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm)

También se incluyen las siguientes características adicionales híbridas en la versión 1702 de Configuration Manager (rama actual):

- **Compatibilidad mejorada para el Programa de Compras por Volumen (VPP) de Apple**

  - Ahora puede implementar aplicaciones con licencia para dispositivos y usuarios. Según la capacidad de las aplicaciones para admitir licencias de dispositivo, se solicitará del siguiente modo una licencia adecuada al realizar la implementación:

    | Versión de Configuration Manager | ¿La aplicación admite licencias de dispositivo? | Tipo de colección de implementación | Licencia exigida |
    |-|-|-|-|
    |Anterior a 1702|Sí|usuario|Licencia de usuario|
    |Anterior a 1702|No|usuario|Licencia de usuario|
    |Anterior a 1702|Sí|Dispositivo|Licencia de usuario|
    |Anterior a 1702|No|Dispositivo|Licencia de usuario|
    |1702 y versiones posteriores|Sí|usuario|Licencia de usuario|
    |1702 y versiones posteriores|No|usuario|Licencia de usuario|
    |1702 y versiones posteriores|Sí|Dispositivo|Licencia de dispositivo|
    |1702 y versiones posteriores|No|Dispositivo|Licencia de usuario|

  - Ahora también puede implementar las aplicaciones adquiridas en el Programa de compra por volumen de iOS para educación y realizar un seguimiento de ellas.

  - Ahora puede asociar varios tokens del Programa de compras por volumen de Apple con Configuration Manager.

  Para más información sobre las aplicaciones de iOS compradas por volumen, vea [Administrar aplicaciones de iOS compradas a través de un programa de compras por volumen](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps).

- **Compatibilidad con las aplicaciones de línea de negocio de la Tienda Windows para empresas**

  Ahora se pueden sincronizar aplicaciones de línea de negocio personalizadas en la Tienda Windows para empresas.

- **Nuevas herramientas de supervisión de Mobile Threat Defense**

    Ahora hay nuevas formas de supervisar el estado de cumplimiento con el proveedor de servicios Mobile Threat Defense.

    Para más información, vea [Supervisión de cumplimiento de Mobile Threat Defense](/sccm/mdm/deploy-use/monitor-mobile-threat-defense-compliance).

## <a name="february-2017"></a>Febrero de 2017

### <a name="new-in-microsoft-intune"></a>Novedades de Microsoft Intune

- **Modernización del sitio web del Portal de empresa**

  El sitio web del Portal de empresa admite aplicaciones que se destinan a usuarios que no tienen dispositivos administrados. El sitio web se adapta a otros productos y servicios de Microsoft mediante una nueva combinación de colores de contraste, ilustraciones dinámicas y un menú "hamburguesa" que contiene detalles de contacto con el departamento de soporte técnico e información sobre los dispositivos administrados existentes. La página de inicio se reorganiza para destacar las aplicaciones disponibles para los usuarios, con carruseles para aplicaciones destacadas y actualizadas recientemente. Tiene a su disposición imágenes de antes y después en la página [Novedades de la interfaz de usuario](/intune/whats-new/whats-new-in-intune-app-ui).

- **Nueva dirección del servidor MDM para dispositivos Windows**

  La dirección del servidor MDM para la inscripción de dispositivos Windows Phone y Windows ha cambiado de manage.microsoft.com a enrollment.manage.microsoft.com. Notifique a su usuario que debe utilizar enrollment.manage.microsoft.com como dirección del servidor MDM si se le solicita durante la inscripción de dispositivos Windows Phone o Windows. Esta actualización también requiere que cualquier CNAME del DNS que redirija EnterpriseEnrollment.contoso.com a manage.microsoft.com se sustituya por un CNAME del DNS que redirija EnterpriseEnrollment.contoso.com a EnterpriseEnrollment-s.manage.microsoft.com. Para obtener más información sobre este cambio, visite http://aka.ms/intuneenrollsvrchange.

### <a name="new-in-configuration-manager-technical-preview-1702"></a>Novedades de Configuration Manager Technical Preview 1702

- **Compatibilidad de Android for Work**

  Ya puede administrar dispositivos Android mediante Android for Work en entornos de MDM híbrida con Configuration Manager Technical Preview 1702. Ahora se pueden inscribir dispositivos Android compatibles como dispositivos Android for Work, con lo que se crea un perfil de trabajo en el dispositivo en el que se pueden implementar aplicaciones aprobadas en Play for Work. También puede configurar e implementar elementos de configuración, directivas de cumplimiento y perfiles de acceso a recursos para estos dispositivos. Para más información, vea [Compatibilidad de Android for Work](/sccm/core/get-started/capabilities-in-technical-preview-1702#android-for-work-support).

- **Configuración de cumplimiento de aplicaciones no compatibles**

  Ahora puede crear reglas de aplicaciones no compatibles para aplicaciones Android e iOS en las directivas de cumplimiento. Si los dispositivos tienen instaladas las aplicaciones especificadas, se marcarán como "no compatibles" y no podrán acceder a los recursos de la empresa, según las directivas de acceso condicional aplicadas. Para más información, vea [Mejoras de la directiva de cumplimiento de dispositivos de acceso condicional](/sccm/core/get-started/capabilities-in-technical-preview-1702#conditional-access-device-compliance-policy-improvements).

- **Creación y distribución de certificados PFX y compatibilidad con S/MIME**

  Ahora puede crear e implementar certificados PFX en los usuarios de un entorno híbrido. Después, estos certificados pueden usarse para el cifrado y descifrado de correo electrónico S/MIME en los dispositivos inscritos por el usuario. Para más información, vea [Crear certificados PFX con compatibilidad con S MIME](/sccm/core/get-started/capabilities-in-technical-preview-1702#create-pfx-certificates-with-s-mime-support).

- **Soporte para la configuración adicional de iOS**
   
    Ahora dispone de 42 opciones de iOS adicionales que se pueden configurar como parte de un elemento de configuración. La mayoría de estas opciones (35 en total) se han agregado para dispositivos iOS supervisados. Para más información, vea [Nueva configuración de cumplimiento para dispositivos iOS](/sccm/core/get-started/capabilities-in-technical-preview-1702#new-compliance-settings-for-ios-devices).

## <a name="january-2017"></a>Enero de 2017

### <a name="new-in-microsoft-intune"></a>Novedades de Microsoft Intune

- **Compatibilidad con Android 7.1.1**

  Intune ahora es totalmente compatible con Android 7.1.1 y lo administra.

- **Se ha resuelto el problema por el que los dispositivos iOS están inactivos o la consola de administración no puede comunicarse con ellos**

  Cuando los dispositivos de los usuarios pierden el contacto con Intune, puede aplicar nuevos pasos de solución de problemas para ayudarles a recuperar el acceso a los recursos de la empresa. Vea [Los dispositivos iOS están inactivos o la consola de administración no puede comunicarse con ellos](/intune/troubleshoot/troubleshoot-device-enrollment-in-intune#devices-are-inactive-or-the-admin-console-cannot-communicate-with-them).

### <a name="new-in-configuration-manager-technical-preview-1701"></a>Novedades de Configuration Manager Technical Preview 1701

- **En los asistentes para creación de MDM híbrida, ya no se pueden seleccionar como destino las versiones de iOS y Android**

  A partir de Technical Preview 1701 para la administración de dispositivos móviles (MDM) híbrida, ya no necesita especificar versiones concretas de iOS y Android al crear nuevas directivas y perfiles para dispositivos administrados por Intune. Con este cambio, las implementaciones híbridas pueden ofrecer compatibilidad con mayor rapidez para nuevas versiones de iOS y Android sin necesidad de una nueva versión o extensión de Configuration Manager. Para obtener más información, consulte [En los asistentes para creación de MDM híbrida, ya no se pueden seleccionar como destino las versiones de iOS y Android](/sccm/core/get-started/capabilities-in-technical-preview-1701#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm).


## <a name="notices"></a>Notificaciones

### <a name="platform-support-reminder-windows-phone-81-mainstream-support-ended-july-11-2017"></a>Recordatorio sobre el soporte técnico para la plataforma: el soporte técnico estándar para Windows Phone 8.1 finalizó el 11 de julio de 2017
<!-- 1327781 -->
*11 de julio de 2017*

La plataforma Windows Phone 8.1 ha llegado a la finalización del soporte técnico estándar. El soporte técnico para equipos con Windows 8.1 no se verá afectado.

Esto no afecta inmediatamente a ningún dispositivo Windows Phone 8.1 administrado por el servicio de Intune, incluidos los inscritos en entornos híbridos MDM. Los dispositivos inscritos continuarán funcionando y todas las directivas, configuraciones y aplicaciones seguirán funcionando según lo previsto. Tenga en cuenta que no hay mejoras previstas para la plataforma Windows Phone 8.1 en el servicio de Intune ni para la aplicación Portal de empresa de Windows Phone 8.1.

Se recomienda actualizar los dispositivos Windows Phone 8.1 aptos a Windows 10 Mobile lo antes posible.  

### <a name="end-of-support-for-android-43-and-lower"></a>Finalización del soporte para Android 4.3 y versiones inferiores
<!---1171127--->
*6 de julio de 2017*

Las aplicaciones administradas y la aplicación Portal de empresa para Android necesitan Android 4.4 y posterior para poder acceder a los recursos de la empresa. Los dispositivos que no estén actualizados antes de principios de octubre ya no podrán acceder al Portal de empresa ni a esas aplicaciones. En diciembre, se forzará la retirada de todos los dispositivos inscritos, con lo que ya podrán acceder a los recursos de la empresa. Si está usando directivas de protección de aplicaciones sin MDM, las aplicaciones no recibirán actualizaciones y la calidad de la experiencia se irá reduciendo con el tiempo.


### <a name="system-center-2012-configuration-sp1-and-system-center-2012-r2-configuration-manager-rtm-support-for-hybrid-mobile-device-management-ending-on-april-10-2017"></a>System Center 2012 Configuration SP1 y System Center 2012 R2 Configuration Manager (RTM): La compatibilidad con la administración de dispositivos móviles híbridos finaliza el 10 de abril de 2017
*11 de enero de 2017*

La compatibilidad con System Center 2012 Configuration Manager SP1 y System Center 2012 R2 Configuration Manager RTM finalizó el 12 de julio de 2016. Posteriormente, la compatibilidad con estas versiones en cuanto a la conexión con el servicio de Microsoft Intune para MDM híbrido finalizará el 10 de abril de 2017. Después de esta fecha, MDM híbrido dejará de funcionar con estas versiones. Los dispositivos administrados quedarán esencialmente sin administrar puesto que Intune Connector ya no se conectará al servicio de Intune. No habrá ningún flujo de datos ascendente de Configuration Manager (como las directivas y las aplicaciones) a Intune ni un flujo descendente de los datos del dispositivo administrado a Configuration Manager a no ser que se lleve a cabo una actualización.

Si está ejecutando una implementación híbrida con Configuration Manager 2012 SP1 o R2 RTM, recomendamos que, antes del 10 de abril de 2017, actualice a Configuration Manager (rama actual) o al último Service Pack compatible para Configuration Manager 2012 (R2 SP1 o SP2) para evitar la interrupción del servicio.

Recursos adicionales:
-   [Actualizar a System Center Configuration Manager (rama actual)](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager)
-   [Planificar la actualización a System Center 2012 R2 Configuration Manager SP1](https://technet.microsoft.com/library/jj822981.aspx#BKMK_PlanningR2SP1Upgrade)
-   [Planificar la actualización a System Center 2012 Configuration Manager SP2](https://technet.microsoft.com/library/jj822981.aspx#BKMK_PlanningSP2Upgrade)

### <a name="windows-phone-8-company-portal-upload-deprecated"></a>Carga en desuso del Portal de empresa de Windows Phone 8
*25 de octubre de 2016*

Se ha quitado de la consola de Configuration Manager la capacidad de cargar una aplicación de portal de empresa firmada, ya que la compatibilidad con Intune está quedando en desuso para Windows 8, Windows Phone 8 y Windows RT, y la compatibilidad con el portal de empresa de Windows Phone 8 finalizará en noviembre.  Los dispositivos Windows 8, Windows Phone 8 y Windows RT que ya están inscritos seguirán siendo compatibles, pero no se admitirá la inscripción de más dispositivos con estas plataformas.


### <a name="see-also"></a>Véase también

- [Características híbridas anteriores de MDM](whats-new-hybrid-archive.md)
- [Novedades de MDM en System Center 2012 Configuration Manager](https://technet.microsoft.com/library/mt445560.aspx)
