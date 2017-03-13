---
title: "¿Qué es el nuevo MDM híbrido?  | Microsoft Docs"
description: "Obtenga información sobre las nuevas características de administración de dispositivos móviles disponibles para implementaciones híbridas con System Center Configuration Manager e Intune."
ms.custom: na
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b127cee-61f1-4681-9760-caebed36ddf5
caps.latest.revision: 40
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 69d3e7d51911d6195c2f62a5e81c0faca38ed306
ms.openlocfilehash: a8fd3c24f3267ea451f4c94854e8577046efaeca
ms.lasthandoff: 02/27/2017

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

## <a name="new-hybrid-features-in-february-2017"></a>Nuevas características híbridas de febrero de 2017

### <a name="new-in-microsoft-intune"></a>Novedades de Microsoft Intune

Las siguientes características de Intune que se incorporen en febrero de 2017 funcionan en implementaciones híbridas:

- **Modernización del sitio web del Portal de empresa**

  El sitio web del Portal de empresa admite aplicaciones que se destinan a usuarios que no tienen dispositivos administrados. El sitio web se adapta a otros productos y servicios de Microsoft mediante una nueva combinación de colores de contraste, ilustraciones dinámicas y un menú "hamburguesa" que contiene detalles de contacto con el departamento de soporte técnico e información sobre los dispositivos administrados existentes. La página de inicio se reorganiza para destacar las aplicaciones disponibles para los usuarios, con carruseles para aplicaciones destacadas y actualizadas recientemente. Tiene a su disposición imágenes de antes y después en la página [Novedades de la interfaz de usuario](/intune/whats-new/whats-new-in-intune-app-ui).

- **Nueva dirección del servidor MDM para dispositivos Windows**

  La dirección del servidor MDM para la inscripción de dispositivos Windows Phone y Windows ha cambiado de manage.microsoft.com a enrollment.manage.microsoft.com. Notifique a su usuario que debe utilizar enrollment.manage.microsoft.com como dirección del servidor MDM si se le solicita durante la inscripción de dispositivos Windows Phone o Windows. Esta actualización también requiere que cualquier CNAME del DNS que redirija EnterpriseEnrollment.contoso.com a manage.microsoft.com se sustituya por un CNAME del DNS que redirija EnterpriseEnrollment.contoso.com a EnterpriseEnrollment-s.manage.microsoft.com. Para obtener más información sobre este cambio, visite http://aka.ms/intuneenrollsvrchange.

### <a name="new-in-configuration-manager-technical-preview-1702"></a>Novedades de Configuration Manager Technical Preview 1702

- **Compatibilidad de Android for Work**

  Ya puede administrar dispositivos Android mediante Android for Work en entornos de MDM híbrida con Configuration Manager Technical Preview 1702. Ahora se pueden inscribir dispositivos Android compatibles como dispositivos Android for Work, con lo que se crea un perfil de trabajo en el dispositivo en el que se pueden implementar aplicaciones aprobadas en Play for Work. También puede configurar e implementar elementos de configuración, directivas de cumplimiento y perfiles de acceso a recursos para estos dispositivos.

- **Configuración de cumplimiento de aplicaciones no compatibles**

  Ahora puede crear reglas de aplicaciones no compatibles para aplicaciones Android e iOS en las directivas de cumplimiento. Si los dispositivos tienen instaladas las aplicaciones especificadas, se marcarán como "no compatibles" y perderán el acceso a los recursos de la empresa, de acuerdo con las directivas de acceso condicional aplicadas.

- **Creación y distribución de certificados PFX y compatibilidad con S/MIME**

  Ahora puede crear e implementar certificados PFX en los usuarios de un entorno híbrido. Después, estos certificados pueden usarse para el cifrado y descifrado de correo electrónico S/MIME en los dispositivos inscritos por el usuario.

## <a name="new-hybrid-features-in-january-2017"></a>Nuevas características híbridas de enero de 2017

### <a name="new-in-microsoft-intune"></a>Novedades de Microsoft Intune

Las siguientes características de Intune que se incorporaron en enero de 2017 funcionan en implementaciones híbridas:

- **Compatibilidad con Android 7.1.1**

  Intune ahora es totalmente compatible con Android 7.1.1 y lo administra.

- **Se ha resuelto el problema por el que los dispositivos iOS están inactivos o la consola de administración no puede comunicarse con ellos**

  Cuando los dispositivos de los usuarios pierden el contacto con Intune, puede aplicar nuevos pasos de solución de problemas para ayudarles a recuperar el acceso a los recursos de la empresa. Vea [Los dispositivos iOS están inactivos o la consola de administración no puede comunicarse con ellos](/intune/troubleshoot/troubleshoot-device-enrollment-in-intune#devices-are-inactive-or-the-admin-console-cannot-communicate-with-them).

### <a name="new-in-configuration-manager-technical-preview-1701"></a>Novedades de Configuration Manager Technical Preview 1701

- **En los asistentes para creación de MDM híbrida, ya no se pueden seleccionar como destino las versiones de iOS y Android**

  A partir de Technical Preview 1701 para la administración de dispositivos móviles (MDM) híbrida, ya no necesita especificar versiones concretas de iOS y Android al crear nuevas directivas y perfiles para dispositivos administrados por Intune. Con este cambio, las implementaciones híbridas pueden ofrecer compatibilidad con mayor rapidez para nuevas versiones de iOS y Android sin necesidad de una nueva versión o extensión de Configuration Manager. Para obtener más información, consulte [En los asistentes para creación de MDM híbrida, ya no se pueden seleccionar como destino las versiones de iOS y Android](/sccm/core/get-started/capabilities-in-technical-preview-1701#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm).


## <a name="new-hybrid-features-in-december-2016"></a>Nuevas características híbridas de diciembre de 2016

### <a name="new-in-microsoft-intune"></a>Novedades de Microsoft Intune

Las siguientes características de Intune que se incorporaron en diciembre de 2016 funcionan en implementaciones híbridas:

- **La autenticación multifactor (MFA) acerca de la inscripción se está trasladando a Azure Portal**

  Anteriormente, tenía que ir a la consola de Intune o a la consola de Configuration Manager para configurar inscripciones de MFA para Intune. Con esta función actualizada, ahora puede iniciar sesión en [Microsoft Azure Portal] (https://manage.windowsazure.com) con credenciales de Intune y configurar las opciones de MFA a través de Azure AD. Para obtener más información, vea [Autenticación multifactor para Microsoft Intune] (https://aka.ms/mfa_ad).

- **Aplicación de portal de empresa para Android ahora disponible en China**

  La aplicación de portal de empresa para Android está ahora disponible en China. Debido a la ausencia de Google Play Store en China, los dispositivos Android deben obtener aplicaciones de mercados de aplicaciones chinos. La aplicación de portal de empresa para Android está disponible para su descarga en las siguientes tiendas:

  -    [Baidu](https://go.microsoft.com/fwlink/?linkid=836946)
  -    [Huawei](https://go.microsoft.com/fwlink/?linkid=836948)
  -    [Tencent](https://go.microsoft.com/fwlink/?linkid=836949)
  -    [Wandoujia](https://go.microsoft.com/fwlink/?linkid=836950)
  -    [Xiaomi](https://go.microsoft.com/fwlink/?linkid=836947)

  La aplicación de portal de empresa para Android utiliza Google Play Services para comunicarse con el servicio de Microsoft Intune. Puesto que Google Play Services no está disponible aún en China, llevar a cabo cualquier de las siguientes tareas puede tardar hasta 8 horas en completarse.

  | Consola de administración de Configuration Manager | Aplicación de portal de empresa de Intune para Android | Sitio web del portal de empresa de Intune |
  |----|----|----|        
  | Retirar/borrar (quitar todos los datos)    | Quitar un dispositivo remoto | Quitar dispositivo (local y remoto) |
  | Retirar/limpiar (quitar datos de la compañía)    | Restablecer dispositivo | Restablecer dispositivo|
  | Implementaciones de la aplicación nuevas o actualizadas | Instalar aplicaciones de línea de negocio disponibles | Restablecimiento del código de acceso del dispositivo|
  | Bloqueo remoto    | | |
  | Restablecimiento de la contraseña | | |        


## <a name="new-hybrid-features-in-november-2016"></a>Nuevas funciones híbridas en noviembre de 2016

### <a name="new-in-microsoft-intune"></a>Novedades de Microsoft Intune

Las siguientes funciones de Intune que se incorporaron en noviembre de 2016 funcionan en implementaciones híbridas:

- **El nuevo portal de empresa de Microsoft Intune está disponible para los dispositivos Windows 10**

  Microsoft ha lanzado una nueva [aplicación de portal de empresa para dispositivos Windows 10](https://www.microsoft.com/store/apps/9wzdncrfj3pz). Esta aplicación, que aprovecha el nuevo formato de Windows 10 Universal, proporciona una experiencia de usuario actualizada que es idéntica en todos los dispositivos de Windows 10, PC y móvil, mientras sigue permitiendo las mismas funcionalidades que ofrecían las aplicaciones de portal de empresa anteriores.

  La nueva aplicación aprovecha las funciones de plataforma como el inicio de sesión único (SSO) y la autenticación basada en certificados en dispositivos Windows 10. La aplicación está disponible como una actualización del portal de empresa de Windows 8.1 existente y este se instala desde la Tienda Windows. Para obtener más información, vaya al [Blog del equipo de soporte técnico de Intune](http://aka.ms/intunecp_universalapp).

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


## <a name="notices"></a>Notificaciones

### <a name="system-center-2012-configuration-sp1-and-system-center-2012-r2-configuration-manager-rtm-support-for-hybrid-mobile-device-management-ending-on-april-10-2017"></a>System Center 2012 Configuration SP1 y System Center 2012 R2 Configuration Manager (RTM): La compatibilidad con la administración de dispositivos móviles híbridos finaliza el 10 de abril de 2017

*11 de enero de 2017*

La compatibilidad con System Center 2012 Configuration Manager SP1 y System Center 2012 R2 Configuration Manager RTM finalizó el 12 de julio de 2016. Posteriormente, la compatibilidad con estas versiones en cuanto a la conexión con el servicio de Microsoft Intune para MDM híbrido finalizará el 10 de abril de 2017. Después de esta fecha, MDM híbrido dejará de funcionar con estas versiones. Los dispositivos administrados quedarán esencialmente sin administrar puesto que Intune Connector ya no se conectará al servicio de Intune. No habrá ningún flujo de datos ascendente de Configuration Manager (como las directivas y las aplicaciones) a Intune ni un flujo descendente de los datos del dispositivo administrado a Configuration Manager a no ser que se lleve a cabo una actualización.

Si está ejecutando una implementación híbrida con Configuration Manager 2012 SP1 o R2 RTM, recomendamos que, antes del 10 de abril de 2017, actualice a Configuration Manager (rama actual) o al último Service Pack compatible para Configuration Manager 2012 (R2 SP1 o SP2) para evitar la interrupción del servicio.

Recursos adicionales:
-    [Actualizar a System Center Configuration Manager (rama actual)](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager)
-    [Planificar la actualización a System Center 2012 R2 Configuration Manager SP1](https://technet.microsoft.com/library/jj822981.aspx#BKMK_PlanningR2SP1Upgrade)
-    [Planificar la actualización a System Center 2012 Configuration Manager SP2](https://technet.microsoft.com/library/jj822981.aspx#BKMK_PlanningSP2Upgrade)

### <a name="windows-phone-8-company-portal-upload-deprecated"></a>Carga en desuso del Portal de empresa de Windows Phone 8
*25 de octubre de 2016*

Se ha quitado de la consola de Configuration Manager la capacidad de cargar una aplicación de portal de empresa firmada, ya que la compatibilidad con Intune está quedando en desuso para Windows 8, Windows Phone 8 y Windows RT, y la compatibilidad con el portal de empresa de Windows Phone 8 finalizará en noviembre.  Los dispositivos Windows 8, Windows Phone 8 y Windows RT que ya están inscritos seguirán siendo compatibles, pero no se admitirá la inscripción de más dispositivos con estas plataformas.


### <a name="see-also"></a>Véase también

- [Características híbridas anteriores de MDM](whats-new-hybrid-archive.md)
- [Novedades de MDM en System Center 2012 Configuration Manager](https://technet.microsoft.com/library/mt445560.aspx)

