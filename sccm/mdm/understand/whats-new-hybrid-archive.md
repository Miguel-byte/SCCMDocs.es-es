---
title: Archivo de novedades de MDM híbrida
titleSuffix: Configuration Manager
description: Archivo de características anteriores de administración de dispositivos móviles disponibles para implementaciones híbridas con System Center Configuration Manager e Intune.
ms.date: 03/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 4c27b161-9eb7-4cdd-b469-d8eb27e71aea
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 21dc3376212505b15078daddbe9dfb0716486c64
ms.sourcegitcommit: 9648ce8a8b5c82518e7c8b6a7668e0e9b076cae6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/05/2019
ms.locfileid: "70379024"
---
# <a name="past-hybrid-features-with-system-center-configuration-manager-and-microsoft-intune"></a>Características híbridas anteriores con System Center Configuration Manager y Microsoft Intune

*Se aplica a: System Center Configuration Manager (Rama actual)*

En este artículo se proporciona información sobre características anteriores de administración de dispositivos móviles (MDM) disponibles para implementaciones híbridas con System Center Configuration Manager y Microsoft Intune.  

##  <a name="compatibility-with-configuration-manager-versions"></a>Compatibilidad con versiones de Configuration Manager  

 En cada sección de este artículo se enumeran las características híbridas organizadas en tres categorías diferentes. Use las indicaciones siguientes para determinar la compatibilidad de las características de cada categoría con las diferentes versiones de Configuration Manager:  

|Categorías de características|
|-|  
|**Novedades de Microsoft Intune**: en general, todas las características que se enumeran en esta categoría deberían funcionar con todas las versiones de Configuration Manager, incluidas las versiones de System Center 2012 R2 Configuration Manager, ya que estas características solo necesitan el servicio de Intune y ninguna función adicional en Configuration Manager.<br /><br /> **Novedades de Configuration Manager Technical Preview**: todas las características que se enumeran en esta categoría funcionan únicamente con la versión especificada de Technical Preview. Para probar estas características, debe instalar la versión de Technical Preview especificada en la descripción de la característica. Para obtener más información, consulte [Technical Preview for System Center Configuration Manager](../../core/get-started/technical-preview.md) (Technical Preview para System Center Configuration Manager).<br /><br /> **Novedades de Configuration Manager (rama actual)** : todas las características que se enumeran en esta categoría funcionan únicamente con la versión especificada de Configuration Manager (rama actual), como la versión 1511 o 1602. Si usa una versión anterior de Configuration Manager para su implementación híbrida, debe actualizar a la versión de Configuration Manager (rama actual) que se especifica en la descripción de la característica. Para obtener más información, consulte [Upgrade to System Center Configuration Manager](../../core/servers/deploy/install/upgrade-to-configuration-manager.md) (Actualizar a System Center Configuration Manager).|  



## <a name="april-2017"></a>Abril de 2017

### <a name="new-in-microsoft-intune"></a>Novedades de Microsoft Intune

- **MyApps está disponible para Managed Browser**  
  Ahora, Microsoft MyApps ofrece una mejor compatibilidad con Managed Browser. Los usuarios de Managed Browser que no estén destinados a la administración se redirigen directamente al servicio MyApps, donde podrán acceder a sus aplicaciones de SaaS aprovisionadas por el administrador. Los usuarios destinados a la administración de Intune siguen teniendo acceso a MyApps desde el marcador de Managed Browser integrado.

- **Nuevos iconos para Managed Browser y Portal de empresa**  
  Managed Browser recibirá iconos actualizados para la versión de la aplicación de Android y la de iOS. El nuevo icono contiene la notificación de Intune actualizada para que sea más coherente con otras aplicaciones de Enterprise Mobility + Security (EM+S). Puede ver el icono nuevo de Managed Browser en la [página de novedades de la UI de la aplicación de Intune](https://docs.microsoft.com/intune/whats-new-app-ui).

  Portal de empresa también recibirá iconos actualizados para las versiones de Windows, iOS y Android de la aplicación a fin de mejorar la coherencia con otras aplicaciones de EM+S. Estos iconos se van a publicar gradualmente en las distintas plataformas desde abril hasta finales de mayo.

- **Indicador de progreso de inicio de sesión del Portal de empresa para Android**  
  Una actualización de la aplicación Portal de empresa para Android muestra un indicador de progreso de inicio de sesión cuando el usuario inicia o reanuda la aplicación. El indicador avanza por los nuevos estados, desde "Conectando..." e "Iniciando sesión..." hasta "Comprobando los requisitos de seguridad...", antes de permitir que el usuario acceda a la aplicación. Puede ver las nuevas pantallas de la aplicación Portal de empresa para Android en la [página de novedades de la UI de la aplicación Intune](https://docs.microsoft.com/intune/whats-new-app-ui).

- **Bloquear el acceso de las aplicaciones a SharePoint Online**  
  Ahora puede crear una directiva de acceso condicional basada en aplicaciones para bloquear el acceso a [SharePoint Online](https://docs.microsoft.com/intune-classic/deploy-use/mam-ca-for-sharepoint-online) a aquellas aplicaciones a las que no se apliquen directivas de protección. En el escenario de acceso condicional basado en aplicaciones, puede especificar las aplicaciones que quiere que tengan acceso a SharePoint Online mediante Azure Portal.

### <a name="new-in-configuration-manager-technical-preview-1704"></a>Novedades de Configuration Manager Technical Preview 1704

- **Configuración de aplicaciones de Android con directivas de configuración de aplicaciones**  
  Cuando un usuario ejecuta una aplicación en dispositivos Android for Work, utiliza directivas de configuración de aplicaciones en Configuration Manager para distribuir valores preconfigurados. Las directivas de configuración de aplicaciones Android solo están disponibles en los dispositivos que ejecutan Android for Work, Estas directivas se aplican a las aplicaciones aprobadas en la tienda Play for Work. Para más información, consulte [Configuración de aplicaciones Android con directivas de configuración de aplicaciones](/sccm/core/get-started/capabilities-in-technical-preview-1704#configure-android-apps-with-app-configuration-policies).



## <a name="march-2017"></a>Marzo de 2017

### <a name="new-in-microsoft-intune"></a>Novedades de Microsoft Intune

- **Nueva experiencia de usuario para la aplicación Portal de empresa para Android**  
  La interfaz de usuario de la aplicación Portal de empresa para Android tiene una apariencia más moderna. Las actualizaciones importantes son:

  - Colorea Portal de empresa encabezados de pestaña están coloreados en la personalización de marca definida por ti.
  - Instala En la pestaña **aplicaciones** , se actualizan los botones **aplicaciones destacadas** y **todas las aplicaciones** .
  - Buscan En la pestaña **aplicaciones** , el botón **Buscar** es un botón de acción flotante.
  - Navegar por las aplicaciones: La vista **todas las aplicaciones** muestra una vista con pestañas **destacadas**, **todas**y **categorías** para facilitar la navegación.
  - Ser Las pestañas **mis dispositivos** y **contactar con ti** se han actualizado para mejorar la legibilidad.

  Para obtener más información sobre estos cambios, consulte [Actualizaciones de la interfaz de usuario para las aplicaciones de usuario final de Intune](https://docs.microsoft.com/intune/whats-new-app-ui).

- **Script de firma para Portal de empresa de Windows 10**  
  Si necesita descargar y transferir localmente la aplicación de Portal de empresa de Windows 10, ahora puede usar un script para simplificar y agilizar el proceso de firma de aplicaciones para su organización. Para descargar el script y las instrucciones para usarlo, vea [Microsoft Intune Signing Script for Windows 10 Company Portal](https://aka.ms/win10cpscript) (Script de firma de Microsoft Intune para Portal de empresa de Windows 10) en la Galería de TechNet. Para obtener más información sobre este anuncio, consulte [Updating your Windows 10 Company Portal app](https://blogs.technet.microsoft.com/intunesupport/2017/03/13/updating-your-windows-10-company-portal-app/) (Actualización de la aplicación Portal de empresa para Windows 10) en el blog del equipo de soporte técnico de Intune.

- **Compatibilidad mejorada para los usuarios de Android con base en China**  
  Debido a la ausencia de Google Play Store en China, los dispositivos Android deben obtener las aplicaciones de mercados chinos. Portal de empresa admite este flujo de trabajo. Redirige a los usuarios de Android en China para que descarguen las aplicaciones de Portal de empresa y Outlook en tiendas de aplicaciones locales. Este comportamiento mejora la experiencia del usuario cuando se habilitan las directivas de acceso condicional, tanto para la administración de dispositivos móviles como para la administración de aplicaciones móviles. Las aplicaciones Portal de empresa y Outlook para Android están disponibles en las siguientes tiendas de aplicaciones chinas:

  - [Baidu](https://go.microsoft.com/fwlink/?linkid=836946)
  - [Xiaomi](https://go.microsoft.com/fwlink/?linkid=836947)
  - [Tencent](https://go.microsoft.com/fwlink/?linkid=836949)
  - [Huawei](https://go.microsoft.com/fwlink/?linkid=836948)
  - [Wandoujia](https://go.microsoft.com/fwlink/?linkid=836950)

- **Asegurarse de que las aplicaciones de Portal de empresa están actualizadas**  
  En diciembre de 2016, se publicó una actualización que habilitaba la aplicación de la autenticación multifactor (MFA) en un grupo de usuarios cuando inscribían un dispositivo iOS, Android, Windows 8.1+ o Windows Phone 8.1+. Esta característica no puede funcionar sin determinadas versiones de base de referencia de la aplicación Portal de empresa para iOS (v2.1.17+) y Android (v5.0.3419.0+).

  Las funcionalidades de administración de Intune mejoran continuamente. Numerosas mejoras han coordinado las actualizaciones de las aplicaciones de Portal de empresa en todas las plataformas compatibles. Se recomienda que mantenga las últimas versiones de las aplicaciones de Portal de empresa instaladas en los dispositivos. Esta práctica aprovecha las mejoras de Intune para una mejor experiencia del usuario.

  >[!Tip]
  > Pida a los usuarios que configuren los dispositivos para actualizar automáticamente las aplicaciones desde la tienda de aplicaciones correspondiente. Si la aplicación de Portal de empresa para Android está disponible en un recurso compartido de red, se puede descargar la versión más reciente desde el [Centro de descarga de Microsoft](https://www.microsoft.com/download/details.aspx?id=49140).

- **Microsoft Teams ahora está habilitado para MAM en iOS y Android**  
  Las aplicaciones de Microsoft Teams para iOS y Android ahora están habilitadas con las funcionalidades de administración de aplicaciones móviles (MAM) de Intune. Ofrezca a sus equipos la capacidad de trabajar libremente en todos los dispositivos, al tiempo que garantiza la protección de las conversaciones y los datos corporativos. Para más información, consulte [el anuncio de Microsoft Teams](https://blogs.technet.microsoft.com/enterprisemobility/2017/03/14/microsoft-teams-is-now-generally-available-and-mam-enabled-on-ios-and-android/) en el blog de seguridad y movilidad empresarial.

### <a name="new-in-configuration-manager-technical-preview-1703"></a>Novedades de Configuration Manager Technical Preview 1703

- **Mayor compatibilidad para el Programa de Compras por Volumen de Apple**  
   A partir de la versión 1703 de Technical Preview, los siguientes casos del Programa de Compras por Volumen (VPP) ahora son compatibles:

   - Concesión de licencias de dispositivos: las aplicaciones que sean compatibles con la concesión de licencias de dispositivos y estén implementadas en colecciones de dispositivos solo necesitarán una licencia por dispositivo. Anteriormente era necesario usar una licencia por cada usuario en un dispositivo. Para obtener más información, consulte [Implementación de aplicaciones iOS adquiridas por volumen en colecciones de dispositivos](/sccm/core/get-started/capabilities-in-technical-preview-1703#deploy-volume-purchased-ios-apps-to-device-collections).
   - Uso de varios tokens del VPP en un único inquilino híbrido con ambos tokens en uso para la administración de aplicaciones del VPP.
   - Uso de tokens del VPP para educación con la capacidad para distinguir entre tokens de empresas e instituciones educativas.

### <a name="new-in-configuration-manager-current-branch"></a>Novedades de Configuration Manager (rama actual)

Las siguientes características no estaban disponibles anteriormente en las versiones de Configuration Manager Technical Preview. Ahora están disponibles en las implementaciones híbridas con Intune y Configuration Manager (Rama actual) versión 1702.

- [Compatibilidad de Android for Work](/sccm/core/plan-design/changes/whats-new-in-version-1702##android-for-work-support)
- [Configuración de cumplimiento de aplicaciones no compatibles](/sccm/core/plan-design/changes/whats-new-in-version-1702#conditional-access-device-compliance-policy-improvements)
- [Creación y distribución de certificados PFX y compatibilidad con S/MIME](/sccm/core/plan-design/changes/whats-new-in-version-1702#mobile-device-management)
- [En los asistentes para creación de MDM híbrida, ya no se pueden seleccionar como destino las versiones de iOS y Android](/sccm/core/plan-design/changes/whats-new-in-version-1702#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm)

También se incluyen las siguientes características adicionales híbridas en la versión 1702 de Configuration Manager (rama actual):

- **Compatibilidad mejorada para el Programa de Compras por Volumen (VPP) de Apple**  
  - Ahora puede implementar aplicaciones con licencia para dispositivos y usuarios. Según la capacidad de las aplicaciones para admitir licencias de dispositivo, se solicitará del siguiente modo una licencia adecuada al realizar la implementación:

    | Versión de Configuration Manager | ¿La aplicación admite licencias de dispositivo? | Tipo de colección de implementación | Licencia exigida |
    |-|-|-|-|
    |Anterior a 1702|Sí|Usuario|Licencia de usuario|
    |Anterior a 1702|Sin|Usuario|Licencia de usuario|
    |Anterior a 1702|Sí|Dispositivo|Licencia de usuario|
    |Anterior a 1702|Sin|Dispositivo|Licencia de usuario|
    |1702 y versiones posteriores|Sí|Usuario|Licencia de usuario|
    |1702 y versiones posteriores|Sin|Usuario|Licencia de usuario|
    |1702 y versiones posteriores|Sí|Dispositivo|Licencia de dispositivo|
    |1702 y versiones posteriores|Sin|Dispositivo|Licencia de usuario|

  - Ahora también puede implementar las aplicaciones adquiridas en el Programa de compra por volumen de iOS para educación y realizar un seguimiento de ellas.

  - Ahora puede asociar varios tokens del Programa de compras por volumen de Apple con Configuration Manager.

  Para más información sobre las aplicaciones de iOS compradas por volumen, vea [Administrar aplicaciones de iOS compradas a través de un programa de compras por volumen](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps).

- **Compatibilidad con aplicaciones de línea de negocio en Microsoft Store para Empresas**  
  Ahora se pueden sincronizar las aplicaciones de línea de negocio personalizadas desde Microsoft Store para Empresas.

- **Nuevas herramientas de supervisión de Mobile Threat Defense**  
    Ahora hay nuevas formas de supervisar el estado de cumplimiento con el proveedor de servicios Mobile Threat Defense.

    Para más información, vea [Supervisión de cumplimiento de Mobile Threat Defense](/sccm/mdm/deploy-use/monitor-mobile-threat-defense-compliance).





## <a name="february-2017"></a>Febrero de 2017

### <a name="new-in-microsoft-intune"></a>Novedades de Microsoft Intune

- **Modernización del sitio web del Portal de empresa**

  El sitio web del Portal de empresa admite aplicaciones que se destinan a usuarios que no tienen dispositivos administrados. El sitio web se adapta a otros productos y servicios de Microsoft mediante una nueva combinación de colores de contraste, ilustraciones dinámicas y un menú "hamburguesa" que contiene detalles de contacto con el departamento de soporte técnico e información sobre los dispositivos administrados existentes. La página de inicio se reorganiza para destacar las aplicaciones disponibles para los usuarios, con carruseles para aplicaciones destacadas y actualizadas recientemente. Tiene a su disposición imágenes de antes y después en la página [Novedades de la interfaz de usuario](https://docs.microsoft.com/intune/whats-new-app-ui).

- **Nueva dirección del servidor MDM para dispositivos Windows**

  La dirección del servidor MDM para la inscripción de dispositivos Windows Phone y Windows ha cambiado de manage.microsoft.com a enrollment.manage.microsoft.com. Notifique a su usuario que debe utilizar enrollment.manage.microsoft.com como dirección del servidor MDM si se le solicita durante la inscripción de dispositivos Windows Phone o Windows. Esta actualización también requiere que cualquier CNAME del DNS que redirija EnterpriseEnrollment.contoso.com a manage.microsoft.com se sustituya por un CNAME del DNS que redirija EnterpriseEnrollment.contoso.com a EnterpriseEnrollment-s.manage.microsoft.com. Para obtener información adicional sobre este cambio, visite https://aka.ms/intuneenrollsvrchange.

### <a name="new-in-configuration-manager-technical-preview-1702"></a>Novedades de Configuration Manager Technical Preview 1702

- **Compatibilidad de Android for Work**

  Ya puede administrar dispositivos Android mediante Android for Work en entornos de MDM híbrida con Configuration Manager Technical Preview 1702. Ahora se pueden inscribir dispositivos Android compatibles como dispositivos Android for Work, con lo que se crea un perfil de trabajo en el dispositivo en el que se pueden implementar aplicaciones aprobadas en Play for Work. También puede configurar e implementar elementos de configuración, directivas de cumplimiento y perfiles de acceso a recursos para estos dispositivos. Para más información, vea [Compatibilidad de Android for Work](/sccm/core/get-started/capabilities-in-technical-preview-1702#android-for-work-support).

- **Configuración de cumplimiento de aplicaciones no compatibles**

  Ahora puede crear reglas de aplicaciones no compatibles para aplicaciones Android e iOS en las directivas de cumplimiento. Si los dispositivos tienen instaladas las aplicaciones especificadas, se marcan como "no compatibles" y no pueden acceder a los recursos de la empresa, según las directivas de acceso condicional aplicadas. Para más información, consulte [Mejoras de la directiva de cumplimiento de dispositivos de acceso condicional](/sccm/core/get-started/capabilities-in-technical-preview-1702#conditional-access-device-compliance-policy-improvements).

- **Creación y distribución de certificados PFX y compatibilidad con S/MIME**

  Ahora puede crear e implementar certificados PFX en los usuarios de un entorno híbrido. Después, estos certificados pueden usarse para el cifrado y descifrado de correo electrónico S/MIME en los dispositivos inscritos por el usuario. Para más información, vea [Crear certificados PFX con compatibilidad con S MIME](/sccm/core/get-started/capabilities-in-technical-preview-1702#create-pfx-certificates-with-s-mime-support).

- **Soporte para la configuración adicional de iOS**
   
    Ahora dispone de 42 opciones de iOS adicionales que se pueden configurar como parte de un elemento de configuración. La mayoría de estas opciones (35 en total) se han agregado para dispositivos iOS supervisados. Para más información, vea [Nueva configuración de cumplimiento para dispositivos iOS](/sccm/core/get-started/capabilities-in-technical-preview-1702#new-compliance-settings-for-ios-devices).



## <a name="january-2017"></a>Enero de 2017

### <a name="new-in-microsoft-intune"></a>Novedades de Microsoft Intune

- **Compatibilidad con Android 7.1.1**

  Intune ahora es totalmente compatible con Android 7.1.1 y lo administra.

- **Se ha resuelto el problema por el que los dispositivos iOS están inactivos o la consola de administración no puede comunicarse con ellos**

  Cuando los dispositivos de los usuarios pierden el contacto con Intune, puede aplicar nuevos pasos de solución de problemas para ayudarles a recuperar el acceso a los recursos de la empresa. Vea [Los dispositivos iOS están inactivos o la consola de administración no puede comunicarse con ellos](https://docs.microsoft.com/intune/troubleshoot/troubleshoot-device-enrollment-in-intune#devices-are-inactive-or-the-admin-console-cant-communicate-with-them).

### <a name="new-in-configuration-manager-technical-preview-1701"></a>Novedades de Configuration Manager Technical Preview 1701

- **En los asistentes para creación de MDM híbrida, ya no se pueden seleccionar como destino las versiones de iOS y Android**

  A partir de Technical Preview 1701 para la administración de dispositivos móviles (MDM) híbrida, ya no necesita especificar versiones concretas de iOS y Android al crear nuevas directivas y perfiles para dispositivos administrados por Intune. Con este cambio, las implementaciones híbridas pueden ofrecer compatibilidad con mayor rapidez para nuevas versiones de iOS y Android sin necesidad de una nueva versión o extensión de Configuration Manager. Para obtener más información, consulte [En los asistentes para creación de MDM híbrida, ya no se pueden seleccionar como destino las versiones de iOS y Android](/sccm/core/get-started/capabilities-in-technical-preview-1701#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm).



## <a name="december-2016"></a>Diciembre de 2016

### <a name="new-in-microsoft-intune"></a>Novedades de Microsoft Intune

- **La autenticación multifactor (MFA) acerca de la inscripción se está trasladando a Azure Portal**

  Anteriormente, tenía que ir a la consola de Intune o a la consola de Configuration Manager para configurar inscripciones de MFA para Intune. Con esta característica actualizada, ahora inicia sesión en el [Microsoft Azure portal](https://manage.windowsazure.com) con las credenciales de Intune y configura las opciones de MFA a través de Azure ad. Para más información, vea [Autenticación multifactor para inscripciones de dispositivos de Intune](https://aka.ms/mfa_ad).

- **Aplicación de portal de empresa para Android ahora disponible en China**

  La aplicación de portal de empresa para Android está ahora disponible en China. Debido a la ausencia de Google Play Store en China, los dispositivos Android deben obtener aplicaciones de mercados de aplicaciones chinos. La aplicación de portal de empresa para Android está disponible para su descarga en las siguientes tiendas:

  - [Baidu](https://go.microsoft.com/fwlink/?linkid=836946)
  - [Huawei](https://go.microsoft.com/fwlink/?linkid=836948)
  - [Tencent](https://go.microsoft.com/fwlink/?linkid=836949)
  - [Wandoujia](https://go.microsoft.com/fwlink/?linkid=836950)
  - [Xiaomi](https://go.microsoft.com/fwlink/?linkid=836947)

  La aplicación de portal de empresa para Android utiliza Google Play Services para comunicarse con el servicio de Microsoft Intune. Puesto que Google Play Services no está disponible aún en China, llevar a cabo cualquier de las siguientes tareas puede tardar hasta 8 horas en completarse.

  | Consola de administración de Configuration Manager | Aplicación de portal de empresa de Intune para Android | Sitio web del portal de empresa de Intune |
  |----|----|----|
  | Retirar/borrar (quitar todos los datos)| Quitar un dispositivo remoto | Quitar dispositivo (local y remoto) |
  | Retirar/limpiar (quitar datos de la compañía)| Restablecer dispositivo | Restablecer dispositivo|
  | Implementaciones de la aplicación nuevas o actualizadas | Instalar aplicaciones de línea de negocio disponibles | Restablecimiento del código de acceso del dispositivo|
  | Bloqueo remoto| | |
  | Restablecimiento de la contraseña | | |


## <a name="november-2016"></a>Noviembre de 2016

### <a name="new-in-microsoft-intune"></a>Novedades de Microsoft Intune

- **El nuevo portal de empresa de Microsoft Intune está disponible para los dispositivos Windows 10**

  Microsoft ha lanzado una nueva [aplicación de portal de empresa para dispositivos Windows 10](https://www.microsoft.com/store/apps/9wzdncrfj3pz). Esta aplicación, que aprovecha el nuevo formato de Windows 10 Universal, proporciona una experiencia de usuario actualizada que es idéntica en todos los dispositivos de Windows 10, PC y móvil, mientras sigue permitiendo las mismas funcionalidades que ofrecían las aplicaciones de portal de empresa anteriores.

  La nueva aplicación aprovecha las funciones de plataforma como el inicio de sesión único (SSO) y la autenticación basada en certificados en dispositivos Windows 10. La aplicación está disponible como una actualización del portal de empresa de Windows 8.1 existente y este se instala desde la Tienda Windows. Para obtener más información, vaya al [Blog del equipo de soporte técnico de Intune](https://aka.ms/intunecp_universalapp).

  La nueva aplicación de portal de empresa también muestra cualquier aplicación de la Tienda de Windows para empresas marcada como **Disponible** en la consola de Configuration Manager.


### <a name="new-in-configuration-manager-current-branch"></a>Novedades de Configuration Manager (rama actual)

Las siguientes características que estaban disponibles en versiones de Configuration Manager Technical Preview están ahora disponibles en implementaciones híbridas con Intune y la versión 1610 de Configuration Manager (rama actual).

* [Configuración adicional y una mejor experiencia para los elementos de configuración](/sccm/core/plan-design/changes/whats-new-in-version-1610#new-compliance-settings-for-configuration-items)
* [Configuración adicional para perfiles DEP](whats-new-hybrid-archive.md#new-in-configuration-manager-technical-preview-1609)
* [Aplicaciones de pago en la Tienda Windows para empresas](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)
* [Tipos de conexión nativos para perfiles de VPN de Windows 10](whats-new-hybrid-archive.md#new-in-configuration-manager-technical-preview-1609)
* [Gráficos de cumplimiento de Intune](/sccm/protect/deploy-use/create-compliance-policy#monitor-the-compliance-policy)
* [Sincronización de solicitud de la directiva desde la consola](/sccm/mdm/deploy-use/sync-intune-device)
* [Opciones de configuración de Windows Defender](/sccm/compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client#windows-defender)

También se incluyen las siguientes funciones adicionales híbridas en versión 1610 de Configuration Manager (rama actual):

- **Mayor número de dispositivos inscritos**

  Ahora puede permitir a los usuarios inscribir hasta 15 dispositivos. Anteriormente el límite era de cinco dispositivos por usuario.


- **Soporte técnico de seguridad adicional**

  Además del administrador total, los siguientes roles de seguridad integrados ahora tienen acceso total a los elementos en el nodo de todos los dispositivos corporativos, incluidos los dispositivos declarados con anterioridad, los perfiles de inscripción de iOS y los perfiles de inscripción de Windows:

    - Administrador de activos
    - Administrador de acceso a los recursos de la empresa

  Aún se concede acceso de solo lectura a estas áreas de la consola de Configuration Manager para el rol de analista de solo lectura.

- **Acceso de VPN de desencadenamiento automático de aplicaciones de protección de la información de Windows**

  Puede agregar un dominio principal de Windows Information Protection en los perfiles de VPN de Windows 10 que hacen que todas las aplicaciones asociadas activen automáticamente una conexión VPN cuando se ejecuten en el dispositivo. Esta opción solo está disponible cuando se elige un tipo de conexión nativa.

- **Acceso condicional para perfiles de VPN de Windows 10**

    Ahora puede requerir que los dispositivos Windows 10 inscritos en Azure Active Directory sean compatibles para disponer de acceso a la VPN a través de perfiles de VPN de Windows 10 creados en la consola de Configuration Manager. Esto es posible a través de la nueva casilla **Habilitar acceso condicional para esta conexión VPN** en la página Método de autenticación en el asistente para perfiles VPN y propiedades de perfil VPN para perfiles de VPN de Windows 10. Esta opción solo está disponible cuando se elige un tipo de conexión nativa.

    También puede especificar un certificado independiente para la autenticación de inicio de sesión único si habilita el acceso condicional para el perfil.

## <a name="october-2016"></a>Octubre de 2016

### <a name="new-in-microsoft-intune"></a>Novedades de Microsoft Intune

Las siguientes características de Intune que se incorporaron en octubre de 2016 funcionan en implementaciones híbridas.

- **Acceso condicional para la administración de aplicaciones móviles**

  Puede restringir el acceso a Exchange Online de forma que el acceso solo proceda de aplicaciones que admitan las directivas de administración de aplicaciones móviles de Intune, como Outlook. [Esta nueva característica](/intune/deploy-use/allow-policy-managed-apps-access-to-o365) se adapta perfectamente a las directivas de administración de aplicaciones móviles (MAM) de Intune, ya que puede bloquear el acceso a los clientes de correo integrado u otras aplicaciones que no se hayan configurado con las directivas de MAM de Intune. Esto garantiza que los usuarios accedan a los datos de la organización con aplicaciones que pueden estar protegidas mediante MAM de Intune. Puede empezar a trabajar en la administración de aplicaciones móviles de Intune mediante Azure Portal. Busque la nueva sección de acceso condicional en la hoja "Configuración".

- **Herramienta de ajuste de aplicaciones Intune para Android**

  Puede habilitar las aplicaciones para que usen directivas de administración de aplicaciones móviles (MAM) de Intune mediante la herramienta de ajuste de aplicaciones de Intune.

- **Compatibilidad de Android Samsung KNOX Standard con Intune**

  Determinados modelos del teléfono Samsung Galaxy Ace no pueden administrarse con Intune como los dispositivos Samsung KNOX Standard. Cuando inscriba estos dispositivos con Intune, se administrarán como dispositivos estándar de Android.

  Los números de los modelos afectados son:

  - SM-G313HU
  - SM-G313HY
  - SM-G313M
  - SM-G313MY
  - SM-G313U

  Ni usted ni los usuarios finales deben realizar ninguna otra acción. Para obtener más información, visite el sitio web de Samsung KNOX.

### <a name="new-in-configuration-manager-technical-preview-1610"></a>Novedades de Configuration Manager Technical Preview 1610

Se han incorporado las siguientes características híbridas nuevas en octubre de 2016 para Configuration Manager Technical Preview 1610.

- **Solicitar la sincronización de directivas desde la consola de administración**

  Puede solicitar la sincronización de directivas en un dispositivo móvil inscrito desde la consola de Configuration Manager, en lugar de solicitar la sincronización en la aplicación de portal de empresa en el propio dispositivo. Se trata de una acción nueva denominada **Send Sync Request** (Enviar solicitud de sincronización) del menú Acciones de dispositivo remoto, que aparece en la cinta de opciones cuando se selecciona un dispositivo móvil en el nodo Dispositivos.

- **Opciones de configuración de Windows Defender**

  Ahora puede establecer la configuración de cliente de Windows Defender en equipos Windows 10 inscritos en Intune mediante elementos de configuración de la consola de Configuration Manager. Hay un nuevo grupo de configuración denominado **Windows Defender** en el Asistente para elemento de configuración. Tenga en cuenta que esto solo se admite en Windows 10 versión 1511 y superiores.


### <a name="new-in-configuration-manager-current-branch"></a>Novedades de Configuration Manager (rama actual)

No se ha incorporado ninguna característica híbrida nueva en agosto de 2016 para Configuration Manager (rama actual).

## <a name="september-2016"></a>Septiembre de 2016

### <a name="new-in-microsoft-intune"></a>Novedades de Microsoft Intune

Las siguientes características de Intune que se incorporaron en septiembre de 2016 funcionan en implementaciones híbridas.

- **Adición de "Notificaciones" en el portal de empresa para Android**

  Se ha agregado un nuevo icono Notificaciones al Portal de empresa para Android en la página principal. Al seleccionar este icono se obtiene acceso a la página Notificaciones, que muestra a todos los usuarios todos los elementos que requieren atención en la aplicación del Portal de empresa, como la falta de conformidad del dispositivo, la actualización de la inscripción o la activación de la inscripción. La aplicación del Portal de empresa de iOS ya tiene esta experiencia en notificaciones. Tener la nueva página Notificaciones significa que el usuario no verá la página Configuración de acceso de la empresa cada vez que inicien o reanuden el Portal de empresa siempre que el dispositivo ya esté inscrito. Si crea su propia guía de usuario final, es posible que quiera actualizar la documentación para reflejar este cambio. Busque las capturas de pantalla actualizadas [aquí](https://aka.ms/androidcpupdate).

- **Cambios en la compatibilidad de la aplicación de portal de empresa de iOS**

  Ahora, todos los usuarios de la aplicación de portal de empresa de Microsoft Intune para iOS tendrán que usar la versión más reciente. Los usuarios nuevos solo podrán descargar la versión más reciente y los usuarios actuales tendrán que llevar a cabo la actualización. La versión más reciente requiere iOS 8.0 o posterior, de modo que los dispositivos que ejecutan versiones anteriores de iOS no podrán usar el portal de empresa o inscribirse hasta que actualicen su dispositivo a iOS 8.0 o posterior y, después, actualicen la aplicación de portal de empresa a la versión más reciente. Los dispositivos inscritos que ejecutan versiones anteriores a iOS 8.0 seguirán administrándose y apareciendo en la consola de administración de Intune.

- **Botón de comentarios agregado a la aplicación de portal de empresa de Windows Phone 8.1**

  La aplicación de Portal de empresa de Windows Phone 8.1 permite a los usuarios finales pueden enviar comentarios acerca de la aplicación mediante un nuevo botón "Enviar comentarios". Para buscar el botón, los usuarios seleccionan el menú de "tres puntos" en la parte inferior derecha de la pantalla de la aplicación de Portal de empresa y, a continuación, seleccionan **Enviar comentarios**. Los comentarios recopilados y anónimos ayudarán a Microsoft a mejorar la experiencia de la aplicación del Portal de empresa para los usuarios.

### <a name="new-in-configuration-manager-technical-preview-1609"></a>Novedades de Configuration Manager Technical Preview 1609

Se han incorporado las siguientes características híbridas nuevas en septiembre de 2016 para Configuration Manager Technical Preview 1609.

- **Configuración adicional y una mejor experiencia para la configuración de elementos de configuración**

  Se han agregado opciones nuevas para Windows, iOS y Android. Además, solo se muestran en el asistente las opciones que se aplican a las plataformas que seleccione en la página Plataformas compatibles. Para obtener más información, consulte [New compliance settings for configuration items in TP 1609](/sccm/core/get-started/capabilities-in-technical-preview-1609#new-compliance-settings-for-configuration-items) (Nueva configuración de cumplimiento para elementos de configuración en TP 1609).

- **Configuración adicional para perfiles DEP**

  Se han agregado TouchID, ApplePay y Zoom como opciones configurables en perfiles DEP para dispositivos iOS.

- **Aplicaciones de pago en la Tienda Windows para empresas**

  Ahora puede agregar aplicaciones de pago y gratuitas en la Tienda Windows para empresas e implementarlas en los usuarios de la organización. Para obtener más información, consulte [Enhancements to Windows Store for Business in TP 1609](/sccm/core/get-started/capabilities-in-technical-preview-1609#enhancements-to-windows-store-for-business-integration-with-configuration-manager) (Mejoras en la Tienda Windows para empresas en TP 1609).

- **Tipos de conexión nativos para perfiles de VPN de Windows 10**

  Ahora, puede crear perfiles de VPN de Windows 10 para MDM con tipos de conexión Microsoft Automatic, IKEv2 y PPTP en la consola de Configuration Manager sin usar OMA-URI.

- **Gráficos de cumplimiento de Intune**

  Puede obtener una vista rápida del cumplimiento general del dispositivo y de los principales motivos de incumplimiento mediante los nuevos gráficos incluidos en el área de trabajo Supervisión. Para obtener más información, consulte [Intune compliance charts in TP 1609](/sccm/core/get-started/capabilities-in-technical-preview-1609#intune-compliance-charts) (Gráficos de cumplimiento de Intune en TP 1609).

### <a name="new-in-configuration-manager-current-branch"></a>Novedades de Configuration Manager (rama actual)

La siguiente característica nueva incorporada en septiembre de 2016 está disponible en implementaciones híbridas con Microsoft Intune y la versión 1606 de Configuration Manager (rama actual).

- **Compatibilidad con iOS 10**

  Si tiene perfiles o elementos de configuración que se destinan a todas las plataformas iOS, también se insertarán en iOS 10. También hemos lanzado una actualización para la versión 1606 de Configuration Manager que permite tener como destino perfiles y elementos de configuración en plataformas iOS individuales, incluido iOS 10. Puede instalar la actualización con la consola de administración de Configuration Manager en **Administración > Información general > Cloud Services > Actualizaciones y mantenimiento**. Encontrará más información sobre la actualización en [https://support.microsoft.com/kb/3192616](https://support.microsoft.com/kb/3192616).

## <a name="august-2016"></a>Agosto de 2016

### <a name="new-in-microsoft-intune"></a>Novedades de Microsoft Intune

Las siguientes características de Intune que se incorporaron en agosto de 2016 funcionan en implementaciones híbridas.

- **Compatibilidad con Android 7 en la aplicación de portal de empresa**

  La aplicación de portal de empresa de Intune para Android proporciona compatibilidad desde el principio para el próximo sistema operativo Android 7.0 para dispositivos móviles.

- **Eliminación de Google de la capacidad de restablecimiento del código de acceso remoto en dispositivos Android 7.0**

  Google está quitando la capacidad de los administradores de TI y usuarios finales de restablecer el código de acceso de dispositivos Android 7.0 de forma remota. Anteriormente, los administradores de TI podían restablecer remotamente la el código de acceso de un usuario y los usuarios finales podrían restablecer sus códigos de acceso desde el sitio web de Portal de empresa.

- **Directiva de aplicaciones permitidas y bloqueadas para dispositivos Samsung KNOX Standard**

  Ahora puede configurar una directiva personalizada para dispositivos Samsung KNOX Standard que le permite crear uno de los siguientes elementos:

  - Una lista de aplicaciones para las que se ha bloqueado la ejecución en el dispositivo. Aunque esté instalada, una aplicación definida en la lista bloqueada no puede activarse en el dispositivo.
  - Una lista de aplicaciones que los usuarios del dispositivo pueden instalar desde la tienda de Google Play. No se pueden instalar otras aplicaciones de la tienda.

  Esta configuración solo pueden usarla dispositivos que ejecutan Samsung KNOX Standard. Para más información, vea [Uso de directivas personalizadas para permitir y bloquear aplicaciones para dispositivos Samsung KNOX Standard](/intune/deploy-use/custom-policy-to-allow-and-block-samsung-knox-apps).

- **Vínculo de comentarios del portal de empresa a Microsoft**

   El sitio web de Portal de empresa permite a los usuarios finales seleccionar un nuevo vínculo "Comentarios", en la parte inferior de la página, para enviar comentarios a Microsoft acerca de su experiencia con el sitio. Los comentarios recopilados y anónimos ayudarán a Microsoft a mejorar la experiencia del sitio web del Portal de empresa para usuarios.

- **Versión mínima del explorador administrado de iOS actualizada a 8.0**

  La aplicación del explorador administrado de Microsoft Intune para iOS se actualizó para admitir los dispositivos que ejecutan iOS 8.0 o posterior. Aunque los dispositivos iOS 7.1 pueden seguir usando la aplicación del explorador administrado existente, asegúrese de que los usuarios actualizan a iOS 8.0 o superior para acceder a las nuevas funciones de explorador administrado y aprovecharlas al máximo.

### <a name="new-in-configuration-manager-technical-preview"></a>Novedades de Configuration Manager Technical Preview

No se ha incorporado ninguna característica híbrida nueva en agosto de 2016 para Configuration Manager Technical Preview.

### <a name="new-in-configuration-manager-current-branch"></a>Novedades de Configuration Manager (rama actual)

No se ha incorporado ninguna característica híbrida nueva en agosto de 2016 para Configuration Manager (rama actual).

## <a name="july-2016"></a>Julio de 2016

### <a name="new-in-microsoft-intune"></a>Novedades de Microsoft Intune

Las siguientes características de Intune que se incorporaron en julio de 2016 funcionan en implementaciones híbridas.

- **El SDK de Xamarin para aplicaciones de Intune ya está disponible**

  El componente de Xamarin de SDK para aplicaciones de Intune permite habilitar las características de administración de aplicaciones móviles de Intune en las aplicaciones móviles de iOS y Android compiladas con Xamarin. Encontrará el componente en la [tienda de Xamarin](https://components.xamarin.com/view/Microsoft.Intune.MAM) o en la [página de Github de Microsoft Intune](https://github.com/msintuneappsdk).

- **Experiencia del usuario final mejorada al inscribir dispositivos de Windows**

  Al usar el acceso condicional, se han aclarado los pasos de inscripción para Windows 8.1, Windows 10 Desktop y Windows 10 Mobile en el sitio web del portal de empresa. Ahora, los usuarios verán los pasos **Inscripción de dispositivos** y **Unión al lugar de trabajo** por separado, lo que facilita ver el estado del dispositivo y completar el proceso si se produce un error al unirse al lugar de trabajo. El hecho de que los pasos se muestren por separado también debería simplificar el proceso de solución de problemas para los administradores de TI. Antes, cuando los usuarios finales intentaban realizar la inscripción y todos los pasos de inscripción se realizaban correctamente excepto la unión al lugar de trabajo, el dispositivo inscrito no aparecía en la lista de dispositivos para que los usuarios lo identificasen, lo que resultaba confuso.

  - **El borrado completo ya está disponible para dispositivos Windows 10**

    Es posible realizar el borrado de los equipos y portátiles Windows 10 inscritos como dispositivos móviles para restablecer el dispositivo a la configuración de fábrica. Para obtener más información, consulte [How to protect your devices with remote wipe](/sccm/mdm/deploy-use/wipe-lock-reset-devices) (Cómo proteger los dispositivos con el borrado remoto).

- **Cambios en las cuentas de los administradores de inscripción de dispositivos en la aplicación de portal de empresa de iOS**

  Para mejorar el rendimiento y el escalado, Intune ya no muestra todos los dispositivos de los administradores de inscripción de dispositivos (DEM) en el panel Mis dispositivos de la aplicación de portal de empresa de iOS. Solo se muestra el dispositivo local que ejecuta la aplicación, en el caso de que se haya inscrito mediante la aplicación de portal de empresa.

  El usuario DEM puede realizar acciones en el dispositivo local, pero la administración remota de otros dispositivos inscritos solo se puede realizar desde la consola de administración de Intune. Además, el empleo en Intune de cuentas DEM con el Programa de inscripción de dispositivos de Apple o la herramienta Apple Configurator está quedando en desuso. Estos métodos de inscripción ya admiten la inscripción sin usuarios para dispositivos iOS compartidos.

  Use cuentas DEM únicamente cuando no esté disponible la inscripción sin usuarios para dispositivos compartidos. Para obtener más información, consulte [Enroll corporate-owned devices with the Device Enrollment Manager in Microsoft Intune](../deploy-use/enroll-devices-with-device-enrollment-manager.md) (Inscribir dispositivos propiedad de la empresa con el administrador de inscripción de dispositivos de Microsoft Intune).

- **Cambios en la aplicación de portal de empresa de Android**

  Si los usuarios finales de Android ven un mensaje de error que dice que al dispositivo le falta un certificado necesario, pueden pulsar el botón "Cómo solucionar este problema" para conocer los pasos necesarios para instalar el certificado que falta. Si los usuarios completan los pasos pero ven otro mensaje de error que indica que falta un certificado, se les solicitará que se pongan en contacto con su administrador de TI y le proporcionen este vínculo, que incluye los pasos que los administradores de TI pueden usar para solucionar el problema del certificado.

- **Restringir las instalaciones de aplicaciones de carga lateral para dispositivos Android inscritos**

  Los dispositivos Android ya no pueden instalar aplicaciones a través del sitio web del portal de empresa a menos que los dispositivos se hayan inscrito en Intune mediante la aplicación de portal de empresa para Android.


### <a name="new-in-configuration-manager-technical-preview"></a>Novedades de Configuration Manager Technical Preview

No se ha incorporado ninguna característica híbrida nueva en julio de 2016 para Configuration Manager Technical Preview.

### <a name="new-in-configuration-manager-current-branch"></a>Novedades de Configuration Manager (rama actual)

Las siguientes características que estaban disponibles en versiones de Configuration Manager Technical Preview están ahora disponibles en implementaciones híbridas con Intune y la versión 1606 de Configuration Manager (rama actual).

* Buscar, administrar y distribuir aplicaciones de la Tienda Windows para empresas para dispositivos Windows 10 desde la consola de Configuration Manager ([1604](#new-in-1604-technical-preview))
* Configuración de SmartLock para dispositivos Android ([1604](#new-in-1604-technical-preview))
* VPN desencadenada por la aplicación para dispositivos Windows 10 ([1605](#new-in-1605-technical-preview))
* Nueva experiencia para acciones del dispositivo remoto ([1605](#new-in-1605-technical-preview))
* Tienda Windows para aplicaciones empresariales ([1605](#new-in-1605-technical-preview))
* Mejoras generales para aplicaciones adquiridas por volumen ([1605](#new-in-1605-technical-preview))
* Windows Information Protection (WIP) ([1605](#new-in-1605-technical-preview))
* Declarar previamente dispositivos corporativos con número de serie IMEI o iOS ([1605](#new-in-1605-technical-preview))
* Clasificar automáticamente dispositivos en recopilaciones ([1606](#new-in-1606-technical-preview))

Para obtener información sobre la nueva funcionalidad, consulte la documentación de la versión de Technical Preview especificada.

## <a name="june-2016"></a>Junio de 2016

### <a name="new-in-microsoft-intune"></a>Novedades de Microsoft Intune
Las siguientes características de Intune que se incorporaron en junio de 2016 funcionan en implementaciones híbridas.

- **Mantenimiento del servicio de Intune** La información de mantenimiento del servicio de Intune se ha movido a una ubicación central con otros servicios de Microsoft. Ahora encontrará esta información en el centro de administración de Microsoft 365 en Service Health. Para obtener más información, consulte esta [entrada de blog](https://blogs.technet.microsoft.com/enterprisemobility/2016/04/28/intune-service-health-is-now-available-in-the-office-365-portal/).

- **Mejor experiencia de configuración de directiva de datos de empresa de Windows 10**

  Intune tiene ahora una mejor experiencia para configurar la directiva de protección de información de Windows 10. Las mejoras incluyen mejores formas de crear reglas de aplicaciones y especificar la definición de límite de red, así como otras opciones de Windows Information Protection. Para obtener más información, consulte [Crear una directiva de Windows Information Protection (WIP) con Microsoft Intune](https://technet.microsoft.com/itpro/windows/keep-secure/create-wip-policy-using-intune).

- **Directiva de control de acceso a la red de ISE de Cisco para Intune**

  Los clientes que usan el motor de servicio de identidad (ISE) 2.1 de Cisco y también usan Microsoft Intune pueden establecer una directiva de control de acceso a la red en ISE. Con esta directiva, los dispositivos que necesitan conectarse a la red mediante Wi-Fi o VPN deben cumplir las condiciones siguientes para que se les permita el acceso:

  - Deben administrarse mediante Intune.
  - Deben cumplir todas las directivas de cumplimiento de Intune implementadas.

  Se solicitará a los usuarios finales de dispositivos no conformes que los inscriban y corrijan los problemas de cumplimiento para tener acceso.

- **Acceso condicional para el explorador**

  Puede establecer una directiva de acceso condicional para Exchange Online y SharePoint Online de modo que solo sean accesibles desde los exploradores web admitidos en dispositivos iOS y Android administrados y conformes. Se les solicitará a los usuarios finales que intenten iniciar sesión en sitios de Outlook Web Access (OWA) y SharePoint con dispositivos iOS y Android que inscriban sus dispositivos con Intune y que corrijan los posibles problemas de incumplimiento para poder completar el inicio de sesión. Para obtener más información, consulte

  * [Restringir el acceso de correo electrónico a Exchange Online y nuevo Exchange Online dedicado con Intune](https://docs.microsoft.com/intune/deploy-use/restrict-access-to-exchange-online-with-microsoft-intune)
  * [Restringir el acceso a SharePoint Online con Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/restrict-access-to-sharepoint-online-with-microsoft-intune)

- **Compatibilidad de Dynamics CRM Online con el acceso condicional**

  Puede establecer una directiva de acceso condicional para Dynamics CRM Online de modo que solo sea accesible para dispositivos iOS y Android administrados y conformes. Se les solicitará a los usuarios finales que intenten iniciar sesión en la aplicación móvil de Dynamics CRM con dispositivos iOS y Android que los inscriban en Intune y que corrijan los posibles problemas de incumplimiento para poder completar el inicio de sesión. Para obtener más información, consulte [Restrict access to Dynamics CRM Online with Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/restrict-access-to-dynamics-crm-online-with-microsoft-intune) (Restringir el acceso a Dynamics CRM Online con Microsoft Intune).

- **Actualizaciones en la aplicación de portal de empresa de Android**

  Intune tiene ahora las nuevas directivas siguientes que afectarán a los usuarios del portal de empresa Android:   

  Directiva  |Efecto en los usuarios  
  ---------|---------
  Requerir que los dispositivos impidan la instalación de aplicaciones desde orígenes desconocidos (Android 4.0 y versiones posteriores)     |  Los usuarios finales con dispositivos Android 4.0 o versiones posteriores verán el mensaje "Debe deshabilitarse la instalación desde orígenes desconocidos". Los usuarios tendrán que ir a **Ajustes > Seguridad** en sus dispositivos y desactivar **Orígenes desconocidos**. Un vínculo incluido en el mensaje de compatibilidad permite a los usuarios obtener más información sobre el mensaje y por qué deben desactivar esta opción de configuración.
  Requerir que los dispositivos impidan la instalación de aplicaciones desde orígenes desconocidos (Android 4.0 y versiones posteriores)  |    Los usuarios finales con dispositivos Android 4.0 o versiones posteriores verán el mensaje "Buscar amenazas de seguridad en el dispositivo". Los usuarios tendrán que ir a **Ajustes > Google > Seguridad** en sus dispositivos y activar **Buscar amenazas de seguridad en el dispositivo**. Un vínculo incluido en el mensaje de compatibilidad permite a los usuarios obtener más información sobre el mensaje y por qué deben activar esta opción de configuración.     
  Requerir que la depuración USB esté deshabilitada (Android 4.2 y versiones posteriores)  | Los usuarios finales con dispositivos Android 4.2 o versiones posteriores verán el mensaje "La depuración USB debe deshabilitarse". Los usuarios tendrán que ir a **Ajustes > Opciones del desarrollador** en sus dispositivos y desactivar **Depuración USB**. Un vínculo incluido en el mensaje de compatibilidad permite a los usuarios obtener más información sobre el mensaje y por qué deben desactivar esta opción de configuración.
  Nivel de revisión de seguridad mínimo de Android (Android 6.0 y versiones posteriores)  | Los usuarios finales con dispositivos Android 6.0 o versiones posteriores verán el mensaje "Este dispositivo no cumple el nivel mínimo de revisión de seguridad de Android". Los usuarios tendrán que instalar la revisión de seguridad necesaria. Un vínculo incluido en el mensaje de compatibilidad permite a los usuarios obtener información sobre cómo instalar la revisión de seguridad necesaria y ver la revisión de seguridad que está instalada actualmente.

- **Actualizaciones en la aplicación de portal de empresa de iOS**

  * Ahora, cuando los usuarios finales instalen aplicaciones de línea de negocio, verán una experiencia mejorada de instalación de aplicaciones. Si la instalación de la aplicación tarda mucho tiempo, los usuarios pueden sincronizar manualmente el dispositivo para forzar la reanudación del proceso de sincronización. Para revisar las instrucciones para el usuario final, consulte Sincronización manual del dispositivo iOS.
  * La aplicación de portal de empresa de Microsoft Intune para iOS se ha actualizado para admitir la versión de iOS 8.0 y posteriores. Esta actualización significa que los usuarios finales pueden instalar la aplicación de portal de empresa e inscribir nuevos dispositivos en Intune solo si el dispositivo ejecuta la versión de iOS 8.0 o posterior. Los usuarios que ya han inscrito dispositivos que se ejecutan con una versión no compatible de iOS pueden seguir utilizando la aplicación Portal de empresa que está en su dispositivo.


### <a name="new-in-1606-technical-preview"></a>Novedades de Technical Preview 1606
Las siguientes características nuevas incorporadas en junio de 2016 están disponibles en implementaciones híbridas con Intune y Configuration Manager Technical Preview 1606.

- **Clasificar automáticamente dispositivos en recopilaciones**

  Puede crear categorías de dispositivos, que se pueden usar para colocar automáticamente los dispositivos en recopilaciones de dispositivos cuando se usa Configuration Manager con Intune. Después, cuando los usuarios inscriben un dispositivo en Intune, tienen que elegir una categoría de dispositivos. Además, puede cambiar la categoría de un dispositivo desde la consola de Configuration Manager. Para obtener más información, consulte [Automatically categorize devices into collections](/sccm/core/get-started/capabilities-in-technical-preview-1606#dmp_category) (Clasificar automáticamente dispositivos en recopilaciones) en [Capabilities in Technical Preview 1606 for System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1606) (Capacidades de Technical Preview 1606 para System Center Configuration Manager).

  > [!IMPORTANT]
  > Esta capacidad funciona con la versión de junio de 2016 de Microsoft Intune. Asegúrese de haber actualizado a esta versión antes de probar estos procedimientos.

### <a name="new-in-configuration-manager-current-branch"></a>Novedades de Configuration Manager (rama actual)
No se ha incorporado ninguna característica híbrida nueva en junio de 2016 para Configuration Manager (rama actual).

##  <a name="may-2016"></a>Mayo de 2016  

### <a name="new-in-microsoft-intune"></a>Novedades de Microsoft Intune  
 Las siguientes características de Intune que se incorporaron en mayo de 2016 funcionan en implementaciones híbridas.

- **SDK DE MAM: Configuración de longitud de PIN de soporte**

  Ahora puede especificar la longitud del PIN para aplicaciones MAM como si se tratara de un PIN de dispositivo. Esto requiere que los usuarios finales cumplan las nuevas restricciones que establezca. La pantalla de PIN se ha modificado ligeramente para tener en cuenta la entrada más larga. Para obtener más información, consulte [Opciones de configuración de directiva de administración de aplicaciones móviles de Android](https://docs.microsoft.com/intune/deploy-use/android-mam-policy-settings) y [Configuración de directiva de administración de aplicaciones móviles iOS](https://docs.microsoft.com/intune/deploy-use/ios-mam-policy-settings).  

- **Skype Empresarial para iOS y Android**

  Ahora puede tener como destino Skype Empresarial con [MAM sin directivas de inscripción](https://docs.microsoft.com/intune/deploy-use/get-ready-to-configure-mobile-app-management-policies-with-microsoft-intune). Una vez que el usuario inicie sesión, se aplicarán las directivas de MAM.  

- **Nuevas aplicaciones disponibles para la administración con directivas de MAM**

  Ahora, las aplicaciones de Microsoft Word, Excel y PowerPoint para Android pueden asociarse con directivas de MAM en dispositivos que no estén inscritos con Intune. Para obtener una lista completa de las aplicaciones compatibles, vaya a la galería de aplicaciones móviles de Microsoft Intune en la página de [partners de aplicaciones de Microsoft Intune](https://www.microsoft.com/server-cloud/products/microsoft-intune/partners.aspx).  

- **Aplicación de portal de empresa de Android: Notificaciones del sistema para el usuario final**

  Cuando los usuarios finales inscriben o eliminan sus dispositivos desde el portal de empresa, aparecen notificaciones del sistema de la aplicación de portal de empresa de Android.  

- **Sitio Web Portal de empresa: El banner de identificación de dispositivos proporcionará más información a los usuarios finales**

  Ahora, los usuarios finales pueden identificar más fácilmente el dispositivo que han seleccionado al usar el sitio web del portal de empresa. Si se selecciona un dispositivo erróneo, pueden seleccionar el dispositivo correcto mediante el vínculo **Pulse aquí** situado en el titular de la página principal.  


### <a name="new-in-1605-technical-preview"></a>Novedades de Technical Preview 1605  
 Las siguientes características nuevas incorporadas en mayo de 2016 están disponibles en implementaciones híbridas con Intune y Configuration Manager Technical Preview 1605. Estas características requieren que se use la consola de Configuration Manager para la configuración y la administración.  

- **VPN desencadenada por la aplicación para dispositivos Windows 10**

  En los dispositivos Windows 10 administrados con Configuration Manager con Intune, puede agregar una lista de aplicaciones que abran automáticamente una conexión VPN que haya configurado mediante la consola de administración de Configuration Manager. Para obtener más información, consulte [App-triggered VPN for Windows 10 devices](/sccm/core/get-started/capabilities-in-technical-preview-1605) (VPN desencadenada por la aplicación para dispositivos Windows 10) en [Capabilities in Technical Preview 1605 for System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605) (Capacidades de Technical Preview 1605 para System Center Configuration Manager).  

- **Nueva experiencia para acciones de dispositivo remoto**

  Se ha mejorado la experiencia para realizar acciones de dispositivo remoto desde la consola de Configuration Manager.

  Acciones comunes como **Retirar/borrar**, **Restablecer contraseña**, **Bloqueo remoto** y **Omitir bloqueo de activación** ahora se encuentran en el menú **Acciones de dispositivo remoto**, al que se accede desde el área de trabajo **Activos y compatibilidad**.

  Para obtener más información, consulte [New experience for remote device actions](/sccm/core/get-started/capabilities-in-technical-preview-1605#BKMK_Remote) (Nueva experiencia para acciones del dispositivo remoto) en [Capabilities in Technical Preview 1605 for System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605) (Capacidades de Technical Preview 1605 para System Center Configuration Manager).  

- **Tienda Windows para aplicaciones empresariales**

  La [Tienda Windows para empresas](https://www.microsoft.com/business-store) es el lugar donde puede buscar y adquirir aplicaciones para su organización, individualmente o por volumen. Al conectar la tienda a Configuration Manager, puede administrar aplicaciones adquiridas por volumen desde la consola de Configuration Manager. Para obtener más información, consulte [Windows Store for Business apps](/sccm/core/get-started/capabilities-in-technical-preview-1605#BKMK_WSFB) (Tienda Windows para aplicaciones empresariales) en [Capabilities in Technical Preview 1605 for System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605) (Capacidades de Technical Preview 1605 para System Center Configuration Manager).  

- **Mejoras generales para aplicaciones adquiridas por volumen**

  Las aplicaciones adquiridas por volumen en la Tienda Windows para empresas e iOS App Store se han consolidado en la misma vista, **Información de licencia para las aplicaciones de la Tienda**. Además, se ha mejorado la forma en que se crean aplicaciones adquiridas por volumen para iOS. Para obtener más información, consulte [General improvements for volume-purchased apps](/sccm/core/get-started/capabilities-in-technical-preview-1605#BKMK_VPP2) (Mejoras generales para aplicaciones adquiridas por volumen) en [Capabilities in Technical Preview 1605 for System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605) (Capacidades de Technical Preview 1605 para System Center Configuration Manager).  

- **Declarar previamente dispositivos corporativos con número de serie IMEI o iOS**

  Ahora puede identificar los dispositivos corporativos si importa sus números de identidad internacional de equipo móvil (IMEI). Puede cargar un archivo de valores separados por comas (.csv) que incluya los números IMEI de los dispositivos o escribir la información de los dispositivos de forma manual.  También puede importar los números de serie de los dispositivos iOS.  Para obtener más información, consulte [Pre-declare corporate-owned devices with IMEI or iOS serial number](../../core/get-started/capabilities-in-technical-preview-1605.md#BKMK_IMEI) (Declarar previamente dispositivos corporativos con número de serie IMEI o iOS) en [Capabilities in Technical Preview 1605 for System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605) (Capacidades de Technical Preview 1605 para System Center Configuration Manager).  

- **Windows Information Protection (WIP)**

  Puede crear elementos de configuración que le permitan implementar directivas de Windows Information Protection (WIP), incluso que le permitan elegir las aplicaciones protegidas, el nivel de protección WIP y cómo buscar datos empresariales en la red. Para obtener más información sobre WIP, consulte los temas siguientes:  

  -   [Protege los datos de tu empresa con Windows Information Protection (WIP)](https://technet.microsoft.com/itpro/windows/keep-secure/protect-enterprise-data-using-wip)  

  -   [Crear e implementar una directiva de Windows Information Protection (WIP) con System Center Configuration Manager](https://technet.microsoft.com/itpro/windows/keep-secure/create-wip-policy-using-sccm)  

### <a name="new-in-configuration-manager-current-branch"></a>Novedades de Configuration Manager (rama actual)  
 No se ha incorporado ninguna característica híbrida nueva en mayo de 2016 para Configuration Manager (rama actual).  

##  <a name="april-2016"></a>Abril de 2016  

### <a name="new-in-microsoft-intune"></a>Novedades de Microsoft Intune  
 Las siguientes características de Intune que se incorporaron en abril de 2016 funcionan en implementaciones híbridas.  

- **Compatibilidad con usuario MAM**

  Ahora puede ver el estado de las directivas de administración de aplicaciones para cualquier usuario del inquilino de Azure Active Directory (AAD).  Para obtener más información, consulte [Supervisión de directivas de administración de aplicaciones móviles con Microsoft Intune](/intune/deploy-use/monitor-mobile-app-management-policies-with-microsoft-intune) en la biblioteca de Intune.  

- **Controles MAM para impedir la sincronización de contactos de Outlook (Android)**

  Hay disponible una nueva opción de configuración que permite impedir que una aplicación sincronice los contactos en la libreta de direcciones nativa de dispositivos Android. Esta nueva opción es compatible inicialmente con la aplicación de Outlook en dispositivos Android. Para obtener más información, consulte [Crear e implementar directivas de administración de aplicaciones móviles con Microsoft Intune](/intune/deploy-use/monitor-mobile-app-management-policies-with-microsoft-intune) en la biblioteca de Intune.  

- **Mejoras en el sitio web del portal de empresa**

  Ahora, cuando los usuarios de Windows 10 Mobile y Windows Phone 8.1 instalen aplicaciones de línea de negocio, verán los siguientes estados nuevos que proporcionan más detalles sobre el estado de la instalación:  

  -   **Esperando a que se sincronice el dispositivo**: el usuario ha pulsado "Instalar" y el dispositivo intenta sincronizarse con la infraestructura de Intune. Es necesario que se lleve a cabo la sincronización para que se complete la instalación. El mensaje "Esperando a que se sincronice el dispositivo" también es un vínculo que los usuarios pueden pulsar para obtener instrucciones sobre cómo sincronizar manualmente sus dispositivos con Intune si el proceso de sincronización tarda demasiado o se detiene.  

  -   **Descargando**: se está procesando la solicitud de descarga del usuario y el dispositivo está descargando e instalando la aplicación.  

- **Mejoras en la aplicación de portal de empresa de Android**

  Los usuarios que no han inscrito el dispositivo en Intune y que no tienen instalado el certificado correcto no podrán iniciar sesión en la aplicación de portal de empresa de Android y verán el mensaje "No puede iniciar sesión porque falta un certificado necesario en su dispositivo". El mensaje incluye un vínculo "Cómo solucionar este problema" que los usuarios pueden pulsar para ver las instrucciones de instalación del certificado. Para ver los pasos que los usuarios finales siguen para resolver el problema, consulte [El dispositivo no tiene un certificado necesario](/intune/enduser/using-your-android-device-with-intune) en la biblioteca de Intune.  

- **Mejoras en la aplicación de portal de empresa de iOS**

  Se ha agregado compatibilidad con la acción de deslizar para actualizar como método de actualización del contenido de la pantalla principal, que incluye las aplicaciones de la lista, los dispositivos de la lista y la información de contacto de TI. La acción de deslizar para actualizar no comprueba la información de cumplimiento o de las directivas. Para hacerlo, es necesario seleccionar el icono del dispositivo actual y pulsar el botón **Sincronizar**.  

- **Mejoras en la aplicación de portal de empresa de Windows 10 Mobile y Windows Phone 8.1**

  Ahora, cuando los usuarios finales instalen aplicaciones de línea de negocio, verán una experiencia mejorada de instalación de aplicaciones. Si la instalación de la aplicación tarda mucho tiempo, los usuarios pueden sincronizar manualmente el dispositivo para forzar la reanudación del proceso de sincronización. Para revisar las instrucciones para el usuario final, consulte [Sync your device manually to speed up app installations](/intune/enduser/using-your-windows-device-with-intune) (Sincronización manual del dispositivo para acelerar las instalaciones de aplicaciones) en la biblioteca de Intune.  

###  <a name="new-in-1604-technical-preview"></a>Novedades de Technical Preview 1604
 Las siguientes características nuevas incorporadas en abril de 2016 están disponibles en implementaciones híbridas con Intune y Configuration Manager Technical Preview 1604. Estas características requieren que se use la consola de Configuration Manager para la configuración y la administración.  

- **Buscar, administrar y distribuir aplicaciones de la Tienda Windows para empresas para dispositivos Windows 10 desde la consola de Configuration Manager**


  Hay compatibilidad con la Tienda Windows para empresas en Configuration Manager Technical Preview 1604 para ayudarle a buscar, administrar y distribuir aplicaciones en los dispositivos Windows 10 que administre. Para obtener información, consulte [Manage volume-purchased apps from the Windows Store for Business](/sccm/core/get-started/capabilities-in-technical-preview-1604#BKMK_WindowsVPP) (Administración de aplicaciones adquiridas por volumen de la Tienda Windows para empresas) en [Capabilities in Technical Preview 1604 for System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1604) (Capacidades de Technical Preview 1604 para System Center Configuration Manager).  

- **Configuración de Smart Lock para dispositivos Android**

  Se ha agregado un nuevo valor de configuración al elemento de configuración de Android y Samsung KNOX Standard que le permite controlar la característica Smart Lock en dispositivos Android compatibles.  Puede utilizar esta opción para impedir que los usuarios finales configuren SmartLock. Consulte [SmartLock setting for Android devices](/sccm/core/get-started/capabilities-in-technical-preview-1604#BKMK_Smart) (Configuración de Smart Lock para dispositivos Android) en [Capabilities in Technical Preview 1604 for System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1604) (Capacidades de Technical Preview 1604 para System Center Configuration Manager).  

### <a name="new-in-configuration-manager-current-branch"></a>Novedades de Configuration Manager (rama actual)  
 No se ha incorporado ninguna característica híbrida nueva en abril de 2016 para Configuration Manager (rama actual).  

##  <a name="march-2016"></a>Marzo de 2016  

### <a name="new-in-microsoft-intune"></a>Novedades de Microsoft Intune  
 Las siguientes características de Intune que se incorporaron en marzo de 2016 funcionan en implementaciones híbridas.  

- **Controles MAM para impedir la sincronización de contactos de Outlook (iOS)**

  Hay disponible una nueva opción de configuración que permite impedir que una aplicación sincronice los contactos en la libreta de direcciones nativa de dispositivos iOS. Esta nueva opción es compatible con la aplicación de Outlook en dispositivos iOS. Para obtener más información sobre esta y otras opciones, consulte [Crear e implementar directivas de administración de aplicaciones móviles ](/intune/deploy-use/monitor-mobile-app-management-policies-with-microsoft-intune) en la biblioteca de Intune.  

- **Skype Empresarial Online admite el acceso condicional**

  Puede establecer una directiva de acceso condicional para Skype Empresarial Online de modo que solo sea accesible para dispositivos iOS y Android administrados y conformes.  Para obtener más información, consulte [Manage access to Skype for Business Online](/intune/deploy-use/restrict-access-to-skype-for-business-online-with-microsoft-intune) (Administrar el acceso a Skype Empresarial Online) en la biblioteca de Intune.  

- **Compatibilidad con iOS 9.3**

  El lunes 21 de marzo, Apple anunció la disponibilidad de iOS 9.3. Todas las características de Intune que están disponibles actualmente para administrar dispositivos iOS seguirán funcionando sin problemas cuando los usuarios actualicen sus dispositivos a iOS 9.3.  

- **Paquetes de aplicaciones de Windows disponibles directamente desde el sitio web del portal de empresa**

  Los usuarios de equipos Windows 8, Windows 8.1 y Windows RT ya pueden instalar paquetes de aplicaciones de Windows (con la extensión .appx) directamente desde el sitio web del portal de empresa. Antes, para poder instalar aplicaciones, tenía que ser usted quien implementara la aplicación de portal de empresa en los dispositivos de los usuarios, o bien tenían que instalarla ellos mismos.  

- **Los usuarios pueden bloquear de forma remota su dispositivo desde el sitio web del portal de empresa**

  Se ha agregado una nueva opción de bloqueo remoto al sitio web del portal de empresa para permitir que los usuarios bloqueen de forma remota su dispositivo desde el portal si lo pierden o se lo roban.  

- **Aprovechar las ventajas de la administración de "Open In" de iOS para dispositivos inscritos en una solución MDM de terceros**

  Puede usar su proveedor de administración de dispositivos móviles (MDM) de terceros para aprovechar las ventajas de la administración de "Open In" de iOS. Puede establecer las restricciones en los valores del perfil de configuración e implementar la aplicación con el software MDM. Cuando el usuario instala la aplicación administrada, se aplican las restricciones. Lea los detalles: [Microsoft Intune las directivas de administración de aplicaciones móviles y iOS abiertas](/intune/deploy-use/introduction-to-device-compliance-policies-in-microsoft-intune) en la biblioteca de Intune.  

- **Aplicaciones de Microsoft que admiten MAM**

  La lista de aplicaciones de Microsoft que se pueden usar con directivas de administración de aplicaciones móviles de Intune se ha actualizado para incluir las aplicaciones más recientes (para dispositivos inscritos únicamente con Intune).  

- **Implementar Adobe Reader para Microsoft Intune en dispositivos iOS administrados por Intune en la empresa**

  La aplicación Adobe Reader para iOS ahora puede administrarse en dispositivos inscritos con la directiva de administración de aplicaciones móviles de Intune.  

- Se admite la aplicación Rights Management sharing con Android

  Los administradores de TI pueden implementar directivas de administración de aplicaciones móviles para que los usuarios finales puedan ver imágenes, AV y archivos PDF de forma más segura, independientemente de si el departamento de TI usa Intune para administrar los dispositivos.  

- **Mejoras en la aplicación de portal de empresa de Android e iOS**

  -   Cuando los usuarios inicien una aplicación administrada mediante la administración de aplicaciones móviles (MAM), verán un mensaje que les informa de que la empresa administra la aplicación. Ahora, los usuarios pueden pulsar el vínculo "Más información" para obtener más información sobre el significado de las "aplicaciones administradas". También pueden pulsar "No mostrar de nuevo" para que el mensaje ya no aparezca al iniciar la aplicación.  

  -   Se han agregado pantallas nuevas para guiar a los usuarios a lo largo del proceso de inscripción y proporcionarles más detalles sobre los motivos por los que deben inscribir los dispositivos, así como información sobre lo que pueden y no pueden ver los administradores de TI en los dispositivos inscritos.  

  -   Ahora, los mensajes de error de inscripción se muestran en la aplicación de portal de empresa.  

### <a name="new-in-configuration-manager-technical-preview"></a>Novedades de Configuration Manager Technical Preview  
 No se ha incorporado ninguna característica híbrida nueva en marzo de 2016 para Configuration Manager Technical Preview.  

### <a name="new-in-configuration-manager-current-branch"></a>Novedades de Configuration Manager (rama actual)  
 Las siguientes características nuevas incorporadas en marzo de 2016 están disponibles en implementaciones híbridas con Intune y la versión 1602 de Configuration Manager (rama actual). Estas características requieren que se use la consola de Configuration Manager para la configuración y la administración.  

- **Directivas de configuración de aplicaciones de iOS**

  En la versión 1602 de Configuration Manager (rama actual), puede usar las directivas de configuración de aplicaciones para proporcionar la configuración que puede ser necesaria cuando el usuario ejecuta una aplicación de iOS. Para obtener más información, consulte [Configure iOS apps with app configuration policies in System Center Configuration Manager](/sccm/apps/deploy-use/configure-ios-apps-with-app-configuration-policies) (Configurar aplicaciones de iOS con directivas de configuración de aplicaciones en System Center Configuration Manager).  

- **Administración de aplicaciones de iOS adquiridas por volumen**

  En la versión 1602 de Configuration Manager (rama actual), puede implementar y administrar las aplicaciones que compró por volumen por medio del Programa de Compras por Volumen de Apple (VPP). Para ello, importe la información de licencia desde App Store y haga un seguimiento de la cantidad de licencias que se han usado. Para obtener más información, consulte [Administrar aplicaciones de iOS compradas por volumen con System Center Configuration Manager](/sccm/apps/deploy-use/manage-volume-purchased-ios-apps).  

- **Creación automática de aplicaciones móviles de Office**

  A partir de la versión 1602 de Configuration Manager (rama actual), se crean las siguientes aplicaciones móviles de Microsoft Office para Android e iOS cuando se actualiza desde la versión 1511:  

  -   Microsoft Word  
  -   Microsoft Excel  
  -   Microsoft PowerPoint  
  -   Microsoft OneDrive  
  -   Microsoft OneNote (solo iOS)  
  -   Microsoft Outlook  

  Encontrará estas aplicaciones en el nodo Aplicaciones de la consola de Configuration Manager. Para obtener más información sobre cómo implementar aplicaciones, consulte [How to deploy applications with System Center Configuration Manager](../../apps/deploy-use/deploy-applications.md) (Implementación de aplicaciones con System Center Configuration Manager).  

- **Configuración de pantalla completa para dispositivos Samsung KNOX Standard con Android**

  El modo de quiosco permite bloquear un dispositivo para permitir que solo funcionen determinadas características.  A partir de la versión 1602 de Configuration Manager (rama actual), puede especificar la configuración de pantalla completa para dispositivos Samsung KNOX Standard. Para obtener más información, consulte [Crear elementos de configuración para dispositivos Android y Samsung KNOX Standard administrados sin el cliente de System Center Configuration Manager](/sccm/compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client).  

- **Bloqueo de activación de iOS**

  A partir de la versión 1602 de Configuration Manager (rama actual), puede administrar el bloqueo de activación de iOS, una característica de la aplicación Buscar mi iPhone disponible en dispositivos iOS 7.1 y versiones posteriores. El bloqueo de activación se habilita automáticamente cuando se usa la aplicación Buscar mi iPhone en un dispositivo.  Para obtener más información, consulte [Manage iOS Activation Lock bypass for System Center Configuration Manager](/sccm/mdm/deploy-use/manage-ios-activation-lock#bypass-activation-lock) (Administración de la omisión del bloqueo de activación de iOS para System Center Configuration Manager).  



## <a name="notices"></a>Notificaciones

### <a name="system-center-2012-configuration-sp1-and-system-center-2012-r2-configuration-manager-rtm-support-for-hybrid-mobile-device-management-ending-on-april-10-2017"></a>System Center 2012 Configuration SP1 y System Center 2012 R2 Configuration Manager (RTM): Compatibilidad con la administración híbrida de dispositivos móviles finaliza el 10 de abril de 2017
*11 de enero de 2017*

La compatibilidad con System Center 2012 Configuration Manager SP1 y System Center 2012 R2 Configuration Manager RTM finalizó el 12 de julio de 2016. Posteriormente, la compatibilidad con estas versiones en cuanto a la conexión con el servicio de Microsoft Intune para MDM híbrido finalizará el 10 de abril de 2017. Después de esta fecha, MDM híbrido dejará de funcionar con estas versiones. Los dispositivos administrados quedarán esencialmente sin administrar puesto que Intune Connector ya no se conectará al servicio de Intune. No habrá ningún flujo de datos ascendente de Configuration Manager (como las directivas y las aplicaciones) a Intune ni un flujo descendente de los datos del dispositivo administrado a Configuration Manager a no ser que se lleve a cabo una actualización.

Si está ejecutando una implementación híbrida con Configuration Manager 2012 SP1 o R2 RTM, recomendamos que, antes del 10 de abril de 2017, actualice a Configuration Manager (rama actual) o al último Service Pack compatible para Configuration Manager 2012 (R2 SP1 o SP2) para evitar la interrupción del servicio.

Recursos adicionales:
- [Actualizar a System Center Configuration Manager (rama actual)](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager)
- [Planificar la actualización a System Center 2012 R2 Configuration Manager SP1](https://technet.microsoft.com/library/jj822981.aspx#BKMK_PlanningR2SP1Upgrade)
- [Planificar la actualización a System Center 2012 Configuration Manager SP2](https://technet.microsoft.com/library/jj822981.aspx#BKMK_PlanningSP2Upgrade)

### <a name="windows-phone-8-company-portal-upload-deprecated"></a>Carga en desuso del Portal de empresa de Windows Phone 8
*25 de octubre de 2016*

Se ha quitado de la consola de Configuration Manager la capacidad de cargar una aplicación de portal de empresa firmada, ya que la compatibilidad con Intune está quedando en desuso para Windows 8, Windows Phone 8 y Windows RT, y la compatibilidad con el portal de empresa de Windows Phone 8 finalizará en noviembre.  Los dispositivos Windows 8, Windows Phone 8 y Windows RT que ya están inscritos seguirán siendo compatibles, pero no se admitirá la inscripción de más dispositivos con estas plataformas.
