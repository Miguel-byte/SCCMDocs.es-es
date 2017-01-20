---
title: "¿Qué es el nuevo MDM híbrido?  | Microsoft Docs"
description: "Obtenga información sobre las nuevas características de administración de dispositivos móviles disponibles para implementaciones híbridas con System Center Configuration Manager e Intune."
ms.custom: na
ms.date: 11/18/2016
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
ms.sourcegitcommit: 9f3088e90c3259adc3c3b9c6873978d1db4dd1d8
ms.openlocfilehash: 05e4a9687d29c5377303afd8b08352a6a77fa58e

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

## <a name="new-hybrid-features-in-december-2016"></a>Nuevas características híbridas de diciembre de 2016

### <a name="new-in-microsoft-intune"></a>Novedades de Microsoft Intune

Las siguientes características de Intune que se incorporaron en diciembre de 2016 funcionan en implementaciones híbridas:

- **La autenticación multifactor (MFA) acerca de la inscripción se está trasladando a Azure Portal**

  Anteriormente, tenía que ir a la consola de Intune o a la consola de Configuration Manager para configurar inscripciones de MFA para Intune. Con esta función actualizada, ahora puede iniciar sesión en [Microsoft Azure Portal] (https://manage.windowsazure.com) con credenciales de Intune y configurar las opciones de MFA a través de Azure AD. Para obtener más información, vea [Autenticación multifactor para Microsoft Intune] (https://aka.ms/mfa_ad).

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
  | Retirar/borrar (quitar todos los datos)   | Quitar un dispositivo remoto | Quitar dispositivo (local y remoto) |
  | Retirar/limpiar (quitar datos de la compañía)   | Restablecer dispositivo | Restablecer dispositivo|
  | Implementaciones de la aplicación nuevas o actualizadas | Instalar aplicaciones de línea de negocio disponibles | Restablecimiento del código de acceso del dispositivo|
  | Bloqueo remoto | | |
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

* [Configuración adicional y una mejor experiencia para los elementos de configuración](/sccm/core/plan-design/changes/whats-new-in-version-1610?branch=sccm-1610-release#new-compliance-settings-for-configuration-items)
* [Configuración adicional para perfiles DEP](#new-in-configuration-manager-technical-preview-1609)
* [Aplicaciones de pago en la Tienda Windows para empresas](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)
* [Tipos de conexión nativos para perfiles de VPN de Windows 10](#new-in-configuration-manager-technical-preview-1609)
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

## <a name="new-hybrid-features-in-october-2016"></a>Nuevas características híbridas de octubre de 2016

### <a name="new-in-microsoft-intune"></a>Novedades de Microsoft Intune

Las siguientes características de Intune que se incorporaron en octubre de 2016 funcionan en implementaciones híbridas.

- **Acceso condicional para la administración de aplicaciones móviles**

  Puede restringir el acceso a Exchange Online de forma que el acceso solo proceda de aplicaciones que admitan las directivas de administración de aplicaciones móviles de Intune, como Outlook. [Esta nueva característica](/intune/deploy-use/allow-policy-managed-apps-access-to-o365) se adapta perfectamente a las directivas de administración de aplicaciones móviles (MAM) de Intune, ya que puede bloquear el acceso a los clientes de correo integrado u otras aplicaciones que no se hayan configurado con las directivas de MAM de Intune. Esto garantiza que los usuarios accedan a los datos de la organización con aplicaciones que pueden estar protegidas mediante MAM de Intune. Puede empezar a trabajar en la administración de aplicaciones móviles de Intune mediante Azure Portal. Busque la nueva sección de acceso condicional en la hoja "Configuración".

-   **Herramienta de ajuste de aplicaciones Intune para Android**

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

## <a name="new-hybrid-features-in-september-2016"></a>Nuevas características híbridas de septiembre de 2016

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

  Si tiene perfiles o elementos de configuración que se destinan a todas las plataformas iOS, también se insertarán en iOS 10. También hemos lanzado una actualización para la versión 1606 de Configuration Manager que permite tener como destino perfiles y elementos de configuración en plataformas iOS individuales, incluido iOS 10. Puede instalar la actualización con la consola de administración de Configuration Manager en **Administración > Información general > Cloud Services > Actualizaciones y mantenimiento**. Encontrará más información sobre la actualización en [http://support.microsoft.com/kb/3192616](http://support.microsoft.com/kb/3192616).

## <a name="new-hybrid-features-in-august-2016"></a>Nuevas características híbridas de agosto de 2016

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

## <a name="new-hybrid-features-in-july-2016"></a>Nuevas características híbridas de julio de 2016

### <a name="new-in-microsoft-intune"></a>Novedades de Microsoft Intune

Las siguientes características de Intune que se incorporaron en julio de 2016 funcionan en implementaciones híbridas.

- **El SDK de Xamarin para aplicaciones de Intune ya está disponible**

  El componente de Xamarin de SDK para aplicaciones de Intune permite habilitar las características de administración de aplicaciones móviles de Intune en las aplicaciones móviles de iOS y Android compiladas con Xamarin. Encontrará el componente en la [tienda de Xamarin](https://components.xamarin.com/view/Microsoft.Intune.MAM) o en la [página de Github de Microsoft Intune](https://github.com/msintuneappsdk).

- **Experiencia del usuario final mejorada al inscribir dispositivos de Windows**

  Al usar el acceso condicional, se han aclarado los pasos de inscripción para Windows 8.1, Windows 10 Desktop y Windows 10 Mobile en el sitio web del portal de empresa. Ahora, los usuarios verán los pasos **Inscripción de dispositivos** y **Unión al lugar de trabajo** por separado, lo que facilita ver el estado del dispositivo y completar el proceso si se produce un error al unirse al lugar de trabajo. El hecho de que los pasos se muestren por separado también debería simplificar el proceso de solución de problemas para los administradores de TI. Antes, cuando los usuarios finales intentaban realizar la inscripción y todos los pasos de inscripción se realizaban correctamente excepto la unión al lugar de trabajo, el dispositivo inscrito no aparecía en la lista de dispositivos para que los usuarios lo identificasen, lo que resultaba confuso.

 - **El borrado completo ya está disponible para dispositivos Windows 10**

    Es posible realizar el borrado de los equipos y portátiles Windows 10 inscritos como dispositivos móviles para restablecer el dispositivo a la configuración de fábrica. Para obtener más información, consulte [How to protect your devices with remote wipe](/sccm/mdm/deploy-use/wipe-lock-reset) (Cómo proteger los dispositivos con el borrado remoto).

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

* Buscar, administrar y distribuir aplicaciones de la Tienda Windows para empresas para dispositivos Windows 10 desde la consola de Configuration Manager ([1604](whats-new-hybrid-archive.md#new-in-1604-technical-preview))
*   Configuración de SmartLock para dispositivos Android ([1604](whats-new-hybrid-archive.md#new-in-1604-technical-preview))
*   VPN desencadenada por la aplicación para dispositivos Windows 10 ([1605](whats-new-hybrid-archive.md#new-in-1605-technical-preview))
*   Nueva experiencia para acciones del dispositivo remoto ([1605](whats-new-hybrid-archive.md#new-in-1605-technical-preview))
*   Tienda Windows para aplicaciones empresariales ([1605](whats-new-hybrid-archive.md#new-in-1605-technical-preview))
*   Mejoras generales para aplicaciones adquiridas por volumen ([1605](whats-new-hybrid-archive.md#new-in-1605-technical-preview))
*   Windows Information Protection (WIP) ([1605](whats-new-hybrid-archive.md#new-in-1605-technical-preview))
*   Declarar previamente dispositivos corporativos con número de serie IMEI o iOS ([1605](whats-new-hybrid-archive.md#new-in-1605-technical-preview))
*   Clasificar automáticamente dispositivos en recopilaciones ([1606](whats-new-hybrid-archive.md#new-in-1606-technical-preview))

Para obtener información sobre la nueva funcionalidad, consulte la documentación de la versión de Technical Preview especificada.

## <a name="notices"></a>Notificaciones

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


## <a name="see-also"></a>Véase también

- [Características híbridas anteriores de MDM](whats-new-hybrid-archive.md)
- [Novedades de MDM en System Center 2012 Configuration Manager](https://technet.microsoft.com/library/mt445560.aspx)



<!--HONumber=Jan17_HO2-->


