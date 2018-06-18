---
title: Novedades de la MDM híbrida
titleSuffix: Configuration Manager
description: Obtenga información sobre las nuevas características de administración de dispositivos móviles disponibles para implementaciones híbridas con Configuration Manager e Intune.
ms.date: 06/04/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 7b127cee-61f1-4681-9760-caebed36ddf5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 62b86310b8a7eb183cc5e759e9c1087b80a72d6b
ms.sourcegitcommit: 032e6e19b819863e43e36b24b57761d0a173d0dc
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2018
ms.locfileid: "34754580"
---
# <a name="whats-new-in-hybrid-mobile-device-management-with-configuration-manager-and-microsoft-intune"></a>Novedades de la administración híbrida de dispositivos móviles con Configuration Manager y Microsoft Intune

*Se aplica a: System Center Configuration Manager (Rama actual)*

En este artículo se proporciona información sobre nuevas características de administración de dispositivos móviles (MDM) disponibles para implementaciones híbridas con System Center Configuration Manager y Microsoft Intune.     

> [!Note]    
> Intune en Azure es la solución de MDM recomendada por Microsoft.     
> - Para obtener más información sobre las nuevas características y actualizaciones de Intune independiente, vea [Novedades de Microsoft Intune](https://docs.microsoft.com/intune/whats-new).    
> - Para obtener más información sobre cómo migrar a Intune independiente, vea [Migrate hybrid MDM users and devices to Intune standalone](https://docs.microsoft.com/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa) (Migrar a Intune independiente usuarios y dispositivos de MDM híbrido).
> - Para obtener más información sobre las actualizaciones de la interfaz de usuario de Intune y de MDM híbrido, vea [Actualizaciones de la interfaz de usuario para las aplicaciones de usuario final de Intune](https://docs.microsoft.com/intune/whats-new-app-ui). 

##  <a name="compatibility-with-configuration-manager-versions"></a>Compatibilidad con versiones de Configuration Manager  
En cada sección de este artículo se enumeran las características híbridas organizadas en tres categorías diferentes. Use las indicaciones siguientes para determinar la compatibilidad de las características de cada categoría con las diferentes versiones de Configuration Manager:  

|Categorías de características|Descripción|
|-|-|
|**Novedades de Microsoft Intune** | En general, todas las características que se enumeran en esta categoría deberían funcionar con todas las versiones de Configuration Manager, incluidas las versiones de System Center 2012 R2 Configuration Manager, ya que estas características solo necesitan el servicio de Intune y ninguna función adicional en Configuration Manager.|
|**Novedades de Configuration Manager Technical Preview**| Todas las funciones que se enumeran en esta categoría funcionan únicamente con la versión especificada de Technical Preview. Para probar estas características, debe instalar la versión de Technical Preview especificada en la descripción de la característica. Para obtener más información, consulte [Technical Preview for System Center Configuration Manager](../../core/get-started/technical-preview.md) (Technical Preview para System Center Configuration Manager).|
|**Novedades de Configuration Manager (rama actual)**| Todas las características que se enumeran en esta categoría funcionan únicamente con la versión especificada de Configuration Manager (rama actual), como la versión 1511 o 1602. Si usa una versión anterior de Configuration Manager para su implementación híbrida, debe actualizar a la versión de Configuration Manager (rama actual) que se especifica en la descripción de la característica. Para obtener más información, consulte [Upgrade to System Center Configuration Manager](../../core/servers/deploy/install/upgrade-to-configuration-manager.md) (Actualizar a System Center Configuration Manager).|



## <a name="may-2018"></a>Mayo de 2018

### <a name="new-in-microsoft-intune"></a>Novedades de Microsoft Intune

#### <a name="intune-app-protection-policies-and-microsoft-edge"></a>Directivas de protección de aplicaciones de Intune y Microsoft Edge 
<!--1818968,1818969-->
Ahora, el explorador Microsoft Edge para dispositivos móviles (iOS y Android) admite directivas de protección de aplicaciones de Microsoft Intune. Los usuarios de dispositivos iOS y Android que inician sesión en la aplicación Edge con sus cuentas de empresa de Azure Active Directory están protegidos por Intune. En dispositivos iOS, la directiva **Requerir Managed Browser para contenido web** permite a los usuarios abrir vínculos en Edge cuando este explorador está administrado.

#### <a name="requesting-help-in-the-company-portal-for-windows-10"></a>Solicitud de ayuda en el Portal de empresa para Windows 10 
<!--1874137-->
El Portal de empresa para Windows 10 ahora envía los registros de aplicación directamente a Microsoft cuando el usuario inicia el flujo de trabajo para obtener ayuda con un problema. Este comportamiento facilita la localización y resolución de problemas que se producen a Microsoft.  


### <a name="new-in-configuration-manager-current-branch"></a>Novedades de Configuration Manager (rama actual)

#### <a name="android-for-work-and-lookout-onboarding-moved-to-intune-on-azure"></a>La incorporación de Android for Work y Lookout se ha movido a Intune en Azure
<!--2355022,2357366-->
Con la última actualización de Intune, puede habilitar y administrar la integración de Android for Work y la integración de Lookout Mobile Threat Defense en inquilinos de administración híbrida de dispositivos móviles en el portal de Intune o de Azure. Antes de la actualización, solo se podían configurar en el portal clásico de Intune (Silverlight).
 
Nota: Lookout es el único proveedor de Mobile Threat Defense (MTD) admitido en entornos híbridos. Si previamente ha utilizado otro proveedor de MTD, seguirá apareciendo en el portal de Intune o de Azure. Si elimina su conector, no podrá volver a agregarlo.
 
Estos cambios no afectan a la funcionalidad existente. Siga usando la consola de Configuration Manager para administrar las aplicaciones relacionadas, los informes y las directivas.
 
Vea los siguientes artículos para más información:
- [Configurar la administración híbrida de dispositivos Android](/sccm/mdm/deploy-use/enroll-hybrid-android)
- [Administrar el acceso a los recursos de la empresa según el dispositivo, la red y el riesgo de aplicación](/sccm/mdm/deploy-use/lookout-mobile-threat-defense-in-configuration-manager)


#### <a name="support-for-new-versions-of-cisco-anyconnect-client-for-ios"></a>Compatibilidad con las nuevas versiones del cliente de Cisco AnyConnect para iOS
<!--1357393-->
Puede habilitar la compatibilidad con Cisco AnyConnect para iOS, versión 4.0.7 o posterior. Si lo hace, los perfiles de VPN de Cisco AnyConnect existentes se etiquetan **Cisco Legacy AnyConnect** y siguen funcionando como antes. La opción **Cisco AnyConnect** es para los nuevos perfiles de VPN que funcionan con Cisco AnyConnect en iOS versión 4.0.7 o posterior.

Para obtener más información sobre cómo habilitar esta característica, vea [Características de versión preliminar](/sccm/core/servers/manage/pre-release-features).

> [!Note]  
> Siga usando la opción **Cisco Legacy AnyConnect** para perfiles de VPN de macOS. 



## <a name="april-2018"></a>Abril de 2018

### <a name="new-in-microsoft-intune"></a>Novedades de Microsoft Intune

#### <a name="intune-adapts-to-fluent-design-system-in-the-company-portal-app-for-windows-10"></a>Intune se adapta a Fluent Design System en la aplicación de Portal de empresa para Windows 10 
<!--1195010-->
La aplicación Portal de empresa de Intune para Windows 10 se ha actualizado con la [vista de navegación de Fluent Design System](/windows/uwp/design/basics/navigation-basics). Observe la lista estática vertical de todas las páginas de nivel superior que aparece a o largo del lateral de la aplicación. Haga clic en cualquier vínculo para ver y cambiar entre páginas rápidamente. Esta actualización es la primera de varias que verá como parte de nuestros esfuerzos para ofrecer una experiencia más adaptable, empática y familiar en Intune. Para ver el aspecto actualizado vaya a [Actualizaciones de la interfaz de usuario para las aplicaciones de usuario final de Intune](/intune/whats-new-app-ui).

#### <a name="improved-device-tiles-in-the-windows-10-company-portal"></a>Iconos de dispositivo mejorados en el Portal de empresa de Windows 10
<!--2213364-->
Se han actualizado los iconos para que sean más accesibles para los usuarios con deficiencia visual y para que funcionen mejor con las herramientas de lectura de pantalla.


#### <a name="test-the-company-portal-for-macos-on-virtual-machines"></a>Probar el Portal de empresa para macOS en máquinas virtuales
<!--2216679-->
Se han publicado instrucciones para ayudar a los administradores de TI a probar la aplicación Portal de empresa para macOS en máquinas virtuales en Parallels Desktop y VMware Fusion. Para obtener más información, vea [Enroll virtual macOS machines for testing](/intune/macos-enroll#enroll-virtual-macos-machines-for-testing) (Inscribir máquinas virtuales de macOS para pruebas).


#### <a name="send-diagnostic-reports-in-company-portal-app-for-macos"></a>Enviar informes de diagnóstico en la aplicación Portal de empresa para macOS
<!--2216677-->
La aplicación Portal de empresa para dispositivos macOS se ha actualizado para mejorar la forma en que los usuarios notifican errores relacionados con Intune. Desde la aplicación Portal de empresa, los empleados pueden:

- Cargar informes de diagnóstico directamente para el equipo de desarrollo de Microsoft.
- Enviar por correo electrónico un identificador de incidente al equipo de soporte técnico de TI de la empresa.


#### <a name="updated-help-experience-on-company-portal-app-for-android"></a>Se ha actualizado la experiencia de Ayuda en la aplicación Portal de empresa para Android. 
<!--1631531-->
Se ha actualizado la experiencia de Ayuda en la aplicación Portal de empresa para Android con el fin de adaptarla a los procedimientos recomendados para la plataforma Android. Ahora, cuando los usuarios detectan un problema en la aplicación, pueden pulsar **Menú** > **Ayuda** y:
- Cargar registros de diagnóstico en Microsoft.
- Enviar un correo electrónico que describa el problema y el identificador de incidentes a una persona de soporte técnico de la empresa.


#### <a name="update-where-to-configure-your-app-protection-policies"></a>Actualización de la ubicación donde se configuran las directivas de protección de aplicaciones 
<!--2144597-->
En el servicio de Microsoft Intune en Azure Portal, vamos a redirigirle temporalmente de la hoja del servicio **Intune App Protection** a la hoja **Aplicación móvil**. Tenga en cuenta que todas las directivas de protección de aplicaciones ya se encuentran en la hoja **Aplicación móvil** de Intune, en Configuración de aplicaciones. En lugar de ir a Intune App Protection, simplemente irá a Intune. En abril de 2018, se suspenderá el redireccionamiento y se quitará por completo la hoja del servicio **Intune App Protection**, para que haya una sola ubicación para las directivas de protección de aplicaciones en Intune. 

**¿Cómo me afecta esto a mí?** Este cambio afectará tanto a los clientes de Intune independientes como a los clientes híbridos (Intune con Configuration Manager). Esta integración le ayudará a simplificar la administración en la nube.

**¿Qué he de hacer para prepararme para este cambio?** Etiquete **Intune** como favorito en lugar de la hoja del servicio **Intune App Protection** y asegúrese de que está familiarizado con el flujo de trabajo de la directiva de protección de aplicaciones de la hoja de la aplicación **Móvil** en Intune. Se le redirigirá durante un breve período de tiempo y luego se quitará la hoja **Intune App Protection**. Recuerde que todas las directivas de protección de aplicaciones ya se encuentran en Intune y que puede modificar cualquiera de las directivas de acceso condicional. Para obtener más información sobre cómo modificar las directivas de acceso condicional, vea [Acceso condicional en Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal). Para obtener más información, vea [¿Qué son las directivas de protección de aplicaciones?](/intune/app-protection-policy) 




#### <a name="user-experience-update-for-the-company-portal-app-for-ios"></a>Actualización de la experiencia de usuario para la aplicación Portal de empresa para iOS 
<!--1412866-->
Hemos publicado una importante actualización de la experiencia de usuario para la aplicación Portal de empresa para iOS. La actualización incluye un completo cambio de diseño visual con una apariencia modernizada. Hemos mantenido la funcionalidad de la aplicación, pero hemos mejorado su facilidad de uso y accesibilidad.  

También verá:
- Compatibilidad con el iPhone X.
- Inicio de la aplicación y carga de las respuestas más rápidos, para ahorrar tiempo a los usuarios.
- Barras de progreso adicionales para proporcionar a los usuarios la información de estado más reciente.
- Mejoras en la forma en que los usuarios cargan los registros, de modo que, si hay algún problema, sea más fácil de informar al respecto.  

Para ver el aspecto actualizado vaya a [Novedades de la interfaz de usuario de aplicaciones](/intune/whats-new-app-ui).



## <a name="march-2018"></a>Marzo de 2018

### <a name="new-in-microsoft-intune"></a>Novedades de Microsoft Intune

#### <a name="windows-company-portal-send-feedback-option-may-no-longer-work"></a>Es posible que la opción Enviar comentarios de la aplicación Portal de empresa de Windows ya no funcione.
<!--2070166-->
La aplicación Portal de empresa de Windows ofrece la opción "Enviar comentarios", que permite a los usuarios enviar comentarios sobre la aplicación a Microsoft. Desde el 30 de abril de 2018, esta opción solo es compatible con la aplicación Portal de empresa de Windows 10, que se ejecuta en la versión 1607 y posteriores de Windows 10.   

**¿Cómo me afecta esto a mí?**

Si no tiene instalada la aplicación Portal de empresa de Windows para usuarios finales, ignore este mensaje.

Si algún usuario final tiene la aplicación Portal de empresa, tenga en cuenta que a partir del 30 de abril, el botón "Enviar comentarios" ya no funciona para la aplicación en estos casos:  

 - Aplicación Portal de empresa de Windows 10 en las versiones 1507 y 1511 de Windows 10  

 - Aplicación Portal de empresa para Windows Phone 8.1  

En los dispositivos afectados, la opción "Enviar comentarios" genera un error y no funciona aunque se intente varias veces. Para enviar comentarios a Microsoft sobre experiencias en estas plataformas, nombramos aquí algunos canales alternativos.

**¿Qué he de hacer para prepararme para este cambio?**

Informe a los usuarios finales de este cambio y actualice las instrucciones del usuario si es necesario. 

Informe a los usuarios del Portal de empresa en Windows Phone 8.1, Windows 10 versión 1507 y Windows 10 versión 1511 de que disponen de otros canales alternativos para realizar comentarios. Pueden:  

- Usar la aplicación Concentrador de comentarios en Windows 10  
- Enviar un correo electrónico a WinCPfeedback@microsoft.com  

Solicite a los usuarios finales en Windows 10 versión 1607 o posterior que actualicen a la versión más reciente del Portal de empresa de Windows que está disponible en Microsoft Store.



#### <a name="azure-active-directory-web-sites-can-require-the-intune-managed-browser-app-and-support-single-sign-on-for-the-managed-browser-public-preview"></a>Los sitios web de Azure Active Directory pueden requerir la aplicación Intune Managed Browser App y admitir el inicio de sesión único para Managed Browser (versión preliminar pública).
<!-- 710595 --> 
Con Azure Active Directory (Azure AD), ya puede restringir el acceso a sitios web en dispositivos móviles para la aplicación Intune Managed Browser. En Managed Browser, los datos del sitio web permanecerán seguros y separados de los datos personales del usuario final. Además, Managed Browser admitirá la función de inicio de sesión único para sitios protegidos por Azure AD. Al iniciar sesión en Managed Browser o al usar Managed Browser en un dispositivo con otra aplicación administrada por Intune, Managed Browser puede acceder a sitios corporativos protegidos por Azure AD sin que el usuario tenga que escribir sus credenciales. Esta función se aplica a sitios como Outlook Web Access (OWA) y SharePoint Online, además de otros sitios corporativos, como los recursos de la intranet a los que se accede mediante Azure App Proxy.



## <a name="february-2018"></a>Febrero de 2018

### <a name="new-in-microsoft-intune"></a>Novedades de Microsoft Intune

- **Compatibilidad de Portal de empresa para MacOS para las inscripciones que usen el administrador de inscripciones de dispositivos**  
    Los usuarios ahora pueden utilizar el administrador de inscripciones de dispositivos cuando se inscriben con Portal de empresa para macOS.
    <!-- 1352411 -->


## <a name="january-2018"></a>Enero de 2018

### <a name="new-in-microsoft-intune"></a>Novedades de Microsoft Intune

- **Aprobación de la aplicación Portal de empresa para Android for Work**  
  Si la organización usa Android for Work, apruebe manualmente la aplicación Portal de empresa para Android. Después, sigue recibiendo actualizaciones automáticas de la tienda Google Play Store administrada.
  <!--1797090 -->  

- **Directivas de acceso condicional de Intune solo disponibles en Azure Portal**   
  A partir de esta versión, debe configurar y administrar las directivas de acceso condicional en [Azure Portal](https://portal.azure.com) desde **Azure Active Directory** > **Acceso condicional**. Para su comodidad, también puede acceder a esta hoja de Intune en Azure Portal en **Intune** > **Acceso condicional**.
  <!-- 1737088 1634311 --> 

- **Cambios en los correos electrónicos sobre cumplimiento**    
  Cuando se envía un correo electrónico para informar de un dispositivo no compatible, se incluyen detalles sobre dicho dispositivo. 
  <!--1637547 -->

- **Nueva funcionalidad para la acción Resolver para dispositivos Android**    
  La aplicación Portal de empresa para Android expande la acción "Resolver" para la opción **Actualizar configuración del dispositivo** para resolver [problemas con el cifrado del dispositivo](https://docs.microsoft.com/intune-user-help/encrypt-your-device-android).
  <!--1583480-->

- **Bloqueo remoto disponible en la aplicación Portal de empresa para Windows 10**    
  Los usuarios finales ya pueden bloquear de forma remota sus dispositivos desde la aplicación del Portal de empresa para Windows 10. Esta acción no se muestra para el dispositivo local que usen activamente.
  <!--676506-->

- **Solución más sencilla de problemas de compatibilidad de la aplicación Portal de empresa para Windows 10**   
  Los usuarios finales con dispositivos Windows pueden pulsar en la razón de no compatibilidad en la aplicación Portal de empresa. Cuando sea posible, esta acción les lleva directamente a la ubicación correcta en la aplicación de configuración para solucionar el problema.
  <!--676546-->    



## <a name="december-2017"></a>Diciembre de 2017

### <a name="new-in-microsoft-intune"></a>Novedades de Microsoft Intune

- **Implementaciones de aplicaciones disponibles que ahora se admiten para Android Enterprise**    
  Ahora puede implementar aplicaciones de Android Enterprise (anteriormente Android for Work) como **Disponibles**, además de **Requeridas**. Para más información, vea [Cómo crear aplicaciones Android con System Center Configuration Manager](/sccm/mdm/deploy-use/creating-android-applications).



## <a name="november-2017"></a>Noviembre de 2017

### <a name="new-in-microsoft-intune"></a>Novedades de Microsoft Intune

- **Protocolo de texto permitido de las aplicaciones administradas**  
  Las aplicaciones administradas por Intune App SDK pueden enviar mensajes SMS.
  <!-- 1414050  -->   

- **La aplicación Portal de empresa para macOS está disponible**   
  Portal de empresa de Intune para macOS tiene una experiencia actualizada. Se ha optimizado para mostrar correctamente toda la información y las notificaciones de cumplimiento que los usuarios necesitan en todos los dispositivos que han inscrito. Además, cuando Portal de empresa de Intune se ha implementado en un dispositivo, Microsoft AutoUpdate para macOS le proporcionará las actualizaciones. Inicie sesión en el sitio web de Portal de empresa de Intune desde un dispositivo macOS para descargar el nuevo Portal de empresa de Intune para macOS.
  <!--1541700-->   

- **Microsoft Planner ahora forma parte de la lista de administración de aplicaciones móviles (MAM) de aplicaciones aprobadas**    
  La aplicación de Microsoft Planner para iOS y Android ahora forma parte de las aplicaciones aprobadas para la administración de aplicaciones móviles (MAM). Configure la aplicación a través de la hoja Intune App Protection de Azure Portal para todos los inquilinos. Para obtener información, vea la [lista de aplicaciones aprobadas para la administración de aplicaciones móviles](https://www.microsoft.com/cloud-platform/microsoft-intune-apps).
  <!-- 1248473 -->    

- **Acceso a los registros de la aplicación administrada para iOS**    
  Ahora, los usuarios finales que tengan Managed Browser instalado pueden ver el estado de administración de todas las aplicaciones publicadas de Microsoft y enviar registros para solucionar problemas con sus aplicaciones iOS administradas.
  <!-- 1469920 -->    

  Para más información sobre cómo habilitar el modo de solución de problemas en Managed Browser en un dispositivo iOS, vea [Cómo tener acceso a los registros de aplicación administrada con Managed Browser en iOS](https://docs.microsoft.com/intune/app-configuration-managed-browser#how-to-access-to-managed-app-logs-using-the-managed-browser-on-ios).

- **Mejoras en el flujo de trabajo de instalación de dispositivos en la aplicación Portal de empresa para iOS en la versión 2.9.0**    
  Se ha mejorado el flujo de trabajo de instalación de dispositivos en la aplicación Portal de empresa para iOS. El lenguaje resulta más fácil de usar y se han combinado pantallas donde era posible. El lenguaje también se ha hecho más específico para la empresa mediante el uso del nombre de la empresa en el texto de instalación. Puede ver este flujo de trabajo actualizado en la página de [novedades de la interfaz de usuario de aplicaciones](https://docs.microsoft.com/intune/whats-new-app-ui#week-of-november-13-2017).

- **Peticiones de comentarios para la aplicación Portal de empresa para Android**    
  Ahora la aplicación Portal de empresa para Android solicita comentarios del usuario final. Estos comentarios se envían directamente a Microsoft, además de ofrecer a los usuarios finales una oportunidad para revisar la aplicación en Google Play Store público. Los comentarios no son obligatorios, por lo que los usuarios pueden descartarlos y continuar usando la aplicación. 
  <!--1165249-->    

- **Información a los usuarios finales de qué información del dispositivo se puede ver en los dispositivos Windows 10**    
  Se agregó **Tipo de propiedad** en la pantalla Detalles del dispositivo en la aplicación Portal de empresa para Windows 10. Esta información permitirá que los usuarios obtengan más información sobre la privacidad directamente en los documentos para el usuario final de Intune. También puede encontrar esta información en la pantalla **Acerca de**.
  <!--1337920-->    

- **Nueva acción Resolver disponible para dispositivos Android**    
  La aplicación Portal de empresa para Android presenta una acción "Resolver" en la página _Actualizar configuración del dispositivo_. Si se selecciona esta opción, se remite al usuario final directamente a la configuración que causa el incumplimiento del dispositivo. La aplicación Portal de empresa para Android actualmente admite esta acción para los valores de configuración [código de acceso de dispositivo](https://docs.microsoft.com/intune-user-help/set-your-pin-or-password-android), [cifrado de dispositivo](https://docs.microsoft.com/intune-user-help/encrypt-your-device-android), [depuración USB](https://docs.microsoft.com/intune-user-help/you-need-to-turn-off-usb-debugging-android) y [orígenes desconocidos](https://docs.microsoft.com/intune-user-help/you-need-to-turn-off-unknown-sources-android). 
  <!--1583480-->    


### <a name="new-in-configuration-manager-current-branch"></a>Novedades de Configuration Manager (rama actual)

- **Acciones de no cumplimiento**    
  Ahora puede configurar una secuencia ordenada de acciones que se aplican a los dispositivos que no cumplen las normas. Por ejemplo, puede notificar a los usuarios de dispositivos no compatibles a través de correo electrónico o marcar los dispositivos como no compatibles. Para obtener más información, vea [Configurar acciones de no cumplimiento](/sccm/mdm/deploy-use/actions-for-noncompliance).
  <!--1321366 -->

- **Configuración de nueva directiva de administración de aplicaciones móviles**     
  Las siguientes opciones se han agregado a la configuración de directiva de administración de aplicaciones móviles:
  - **Deshabilitar sincronización de contactos:** impide que la aplicación guarde los datos en la aplicación de contactos nativa del dispositivo.
  - **Deshabilitar la impresión:** impide que la aplicación imprima datos profesionales o educativos.
  <!-- 1324760 -->    

  Vea [Proteger aplicaciones mediante directivas de administración de aplicaciones móviles en System Center Configuration Manager](/sccm/mdm/deploy-use/protect-apps-using-mam-policies) para probar la nueva configuración de la directiva de protección de aplicaciones.

- **Compatibilidad con dispositivos Windows 10 (ARM64)**     
  Cuando los dispositivos ARM64 que ejecutan Windows 10 estén disponibles, admiten los escenarios híbridos de administración de dispositivos móviles (MDM). Para más información, vea [Compatibilidad con dispositivos Windows 10 (ARM64)](/sccm/core/plan-design/changes/whats-new-in-version-1710#windows-10-arm64-device-support).
  <!-- 1355000 -->    

- **Experiencia mejorada del perfil VPN en la consola de Configuration Manager**     
  Con esta versión hemos actualizado las páginas de propiedades y el asistente de perfiles VPN para mostrar una configuración más adecuada para la plataforma seleccionada. Esta característica estaba disponible anteriormente en Configuration Manager Technical Preview 1709. Ahora están disponibles en implementaciones híbridas con Intune y la versión 1710 de Configuration Manager (Rama actual). Para más información, consulte [Experiencia mejorada del perfil VPN en la consola de Configuration Manager](/sccm/core/plan-design/changes/whats-new-in-version-1710#improved-vpn-profile-experience-in-configuration-manager-console).
  <!-- 1318232 -->


### <a name="new-in-configuration-manger-technical-preview-1711"></a>Novedades de Configuration Manager Technical Preview 1711

- **Nuevas opciones de directivas de cumplimiento para Windows 10**   
  Ahora puede configurar nuevas opciones para las directivas de conformidad en los dispositivos Windows 10. La nueva configuración incluye directivas para Firewall, Control de cuentas de usuario, Antivirus de Windows Defender y control de versiones de compilación del sistema operativo. Para obtener información, vea [Nuevas opciones de directivas de cumplimiento para Windows 10](/sccm/core/get-started/capabilities-in-technical-preview-1711#new-compliance-policy-options-for-windows-10).



## <a name="october-2017"></a>Octubre de 2017

### <a name="new-in-configuration-manager-technical-preview-1709"></a>Novedades de Configuration Manager Technical Preview 1709

- **Experiencia mejorada del perfil VPN en la consola de Configuration Manager**      
  La configuración del perfil de VPN ahora se filtra según la plataforma. Al crear nuevos perfiles de VPN, cada plataforma admitida contiene solo la configuración más adecuada para la plataforma. Los perfiles de VPN existentes no se ven afectados. Puede leer más sobre este cambio [aquí](/sccm/core/get-started/capabilities-in-technical-preview-1709#improved-vpn-profile-experience-in-configuration-manager-console).
  <!-- 1313282 -->


### <a name="new-in-microsoft-intune"></a>Novedades de Microsoft Intune  

- **Ayude a los usuarios a ayudarse ellos mismos con la aplicación Portal de empresa para Android**     
  La aplicación Portal de empresa para Android ahora tiene instrucciones para los usuarios finales que les ayudan a comprender y, posiblemente, solucionar por ellos mismos nuevos casos de uso.
    - Si los usuarios finales han alcanzado el número máximo de dispositivos que pueden agregar, se les guiará al [portal de Azure Active Directory](https://account.activedirectory.windowsazure.com/r/#/profile) para quitar un dispositivo.
    - A los usuarios finales se les indican los pasos que deben seguir para ayudarles a [corregir errores de activación en dispositivos Samsung Knox](https://go.microsoft.com/fwlink/?linkid=859718) o a [desactivar el modo de ahorro de energía](https://docs.microsoft.com/intune-user-help/power-saving-mode-android). Si ninguna de estas soluciones resuelve su problema, se proporciona una explicación de cómo [enviar registros a Microsoft](https://docs.microsoft.com/intune-user-help/send-logs-to-microsoft-android).
  <!-- 1573324, 1573150, 1558616, 1564878 -->      

- **Indicador de progreso de instalación del dispositivo en Portal de empresa de Android**    
  La aplicación Portal de empresa para Android muestra un indicador de progreso de instalación de dispositivos cuando un usuario inscribe sus dispositivos. El indicador muestra estados nuevos, comenzando con "Configurando el dispositivo...", sigue con "Registrando el dispositivo..." y "Finalizando el registro del dispositivo...", y acaba con "Finalizando la configuración del dispositivo...".  
  <!--1565657-->    

- **Compatibilidad con la autenticación basada en certificados en Portal de empresa para iOS**    
  Se ha agregado compatibilidad con la autenticación basada en certificados (CBA) en la aplicación Portal de empresa para iOS. Los usuarios con CBA escriben su nombre de usuario y luego pulsan el vínculo para iniciar sesión con un certificado. CBA ya se admite en las aplicaciones del Portal de empresa de Android y Windows. Puede aprender más sobre la página de [inicio de sesión en la aplicación del Portal de empresa](https://docs.microsoft.com/intune-user-help/sign-in-to-the-company-portal).
  <!--1029830-->   

- **Mejoras en el flujo de trabajo de configuración de dispositivos en Portal de empresa**     
  Se ha mejorado el flujo de trabajo de instalación de dispositivos en la aplicación del Portal de empresa para Android. El lenguaje resulta más fácil de usar y es específico de su empresa. Además, hemos combinado pantallas donde era posible. Puede ver estas mejoras en la página [Novedades de la interfaz de usuario de aplicaciones](https://docs.microsoft.com/intune/whats-new-app-ui#week-of-october-2-2017).
  <!--1490692-->     

- **Guía mejorada en torno a la solicitud de acceso a los contactos en dispositivos Android**     
  La aplicación del Portal de empresa para Android requiere a menudo que el usuario final acepte el permiso de contactos. Si un usuario final rechaza este acceso, puede ver una notificación en aplicación que le avisa de que se le va a conceder acceso condicional. 
  <!--1484985-->     

- **Remedio para el inicio seguro en Android**     
  Los usuarios finales con dispositivos Windows podrán pulsar en la razón de no compatibilidad en la aplicación Portal de empresa. Cuando sea posible, esta acción les lleva directamente a la ubicación correcta en la aplicación de configuración para solucionar el problema. 
  <!--1490712-->    

- **Notificaciones de inserción adicionales para usuarios finales en la aplicación Portal de empresa para Android Oreo**    
  Los usuarios finales ven notificaciones adicionales que indican cuando la aplicación Portal de empresa para Android Oreo realiza tareas en segundo plano, como recuperar directivas desde el servicio Intune. Las notificaciones aumentan la transparencia para los usuarios finales con respecto a cuándo el Portal de empresa realiza tareas administrativas en el dispositivo. Esta mejora forma parte de la [optimización general de la interfaz de usuario de Portal de empresa ](https://blogs.technet.microsoft.com/intunesupport/2017/08/21/android-8-0-o-behaviour-changes-and-microsoft-intune) para la aplicación Portal de empresa para Android Oreo. 
  <!--1475932 -->     

- **Nuevos comportamientos para la aplicación Portal de empresa en perfiles de Android for Work**     
  Cuando inscribe un dispositivo de Android for Work con un perfil de trabajo, es la aplicación del Portal de empresa del perfil de trabajo la que realiza las tareas de administración en el dispositivo. 

  A menos que vaya a usar una aplicación habilitada para MAM en el perfil personal, la aplicación Portal de empresa para Android ya no satisface todos los usos. Para mejorar la experiencia del perfil de trabajo, Intune oculta automáticamente la aplicación personal de Portal de empresa después de una inscripción correcta del perfil de trabajo.

  La aplicación del Portal de empresa para Android se puede habilitar en cualquier momento en el perfil personal; para ello, vaya al [Portal de empresa en Play Store](https://play.google.com/store/apps/details?id=com.microsoft.windowsintune.companyportal) y pulse **Habilitar**.
  <!--1485783-->    

- **Portal de empresa para Windows 8.1 y Windows Phone 8.1 se mueve al modo de mantenimiento**    
  Se ha agregado un aviso para anunciar que las aplicaciones del Portal de empresa para Windows 8.1 y Windows Phone 8.1 se mueven al modo de mantenimiento. Para obtener más información, consulte [Notificaciones](#notices).  
  <!--1428681-->    

- **Bloqueo de la inscripción de los dispositivos Samsung Knox no compatibles**   
  La aplicación del Portal de empresa solo intenta inscribir los dispositivos Samsung Knox compatibles. Para evitar errores de activación de KNOX que impidan la inscripción de MDM, solo se intenta la inscripción de dispositivos si el dispositivo aparece en la [lista de dispositivos publicados por Samsung](https://www.samsungknox.com/knox-supported-devices/knox-workspace). Puede que algunos dispositivos Samsung tengan números de modelo que admitan KNOX y otros no. Compruebe la compatibilidad de Knox con su revendedor de dispositivos antes de su compra e implementación. Puede encontrar la lista completa de dispositivos comprobados en la [configuración de directivas de Android y Samsung KNOX Standard](https://docs.microsoft.com/intune-classic/deploy-use/android-policy-settings-in-microsoft-intune#supported-samsung-knox-standard-devices).
  <!-- 1490695 -->     

- **Finalización del soporte técnico para Android 4.3 y versiones anteriores**     
  Se ha agregado un aviso de finalización del soporte técnico para Android 4.3 y versiones inferiores. Para obtener más información, consulte [Notificaciones](#notices).
  <!--1171126, 1326920 -->     

- **Información a los usuarios finales de qué información del dispositivo se puede ver en los dispositivos inscritos**     
  Se va a agregar la opción **Tipo de propiedad** a la pantalla Detalles del dispositivo en todas las aplicaciones del Portal de empresa. Esta información permite a los usuarios obtener más información sobre privacidad directamente en el artículo [¿Qué información puede ver mi empresa cuando inscribo mi dispositivo?](https://docs.microsoft.com/intune-user-help/what-info-can-your-company-see-when-you-enroll-your-device-in-intune). Esta mejora se va a implementar en todas las aplicaciones de Portal de empresa en un futuro cercano. Esta característica se anunció para iOS en [septiembre](https://docs.microsoft.com/intune/whats-new#week-of-september-11-2017). 
  <!--1165314-->     



## <a name="september-2017"></a>Septiembre de 2017

### <a name="new-in-microsoft-intune"></a>Novedades de Microsoft Intune     

- **Se ha incorporado una acción de actualización a la aplicación Portal de empresa para Windows 10**    
    La aplicación Portal de empresa para Windows 10 permite que los usuarios actualicen los datos de la aplicación, ya sea tirando para actualizar o, en los equipos de escritorio, presionando F5.
    <!-- 1132468 -->     

- **Detalles para los usuarios finales sobre qué información del dispositivo se puede ver para iOS**   
    Se agregó el **tipo de propiedad** en la pantalla Detalles del dispositivo en la aplicación Portal de empresa para iOS. Esta información permitirá que los usuarios obtengan más información sobre la privacidad directamente en los documentos para el usuario final de Intune. También se puede encontrar esta información en la pantalla Acerca de. 
    <!--739894-->    

- **Frases más fáciles de comprender en la aplicación Portal de empresa para Android**   
    El proceso de inscripción de la aplicación Portal de empresa para Android se simplificó con texto nuevo para facilitar la inscripción de los usuarios finales. Si tiene documentación de inscripción personalizada, actualícela para reflejar las pantallas nuevas. Puede encontrar imágenes de ejemplo en la página [Actualizaciones de la interfaz de usuario para las aplicaciones de usuario final de Intune](https://docs.microsoft.com/intune/whats-new-app-ui#week-of-september-11-2017).
    <!---1396349-->    

- **La aplicación Portal de empresa de Windows 10 se agregó a la directiva de autorización de Windows Information Protection**    
    La aplicación Portal de empresa de Windows 10 se actualizó para admitir Windows Information Protection (WIP). La aplicación se puede agregar a la directiva de autorización de WIP. Con este cambio, ya no es necesario agregar la aplicación a la lista de **exentos**. 

    Solo se puede enviar un único elemento de configuración WIP a un dispositivo. Si dos elementos de configuración WIP tienen como destino el mismo dispositivo, no se aplicará ninguna directiva de WIP.
    <!-- 677129 -->    

- **Se agregó un aviso de finalización del soporte para iOS 8.0**    
    Se agregó un aviso para la finalización del soporte de iOS 8.0. Para obtener más información, consulte [Notificaciones](#notices).



## <a name="august-2017"></a>Agosto de 2017

### <a name="new-in-microsoft-intune"></a>Novedades de Microsoft Intune     

- **Nueva experiencia de inicio de sesión para los usuarios de Portal de empresa de Android y de la directiva de protección de aplicaciones**    
  Los usuarios finales pueden ahora examinar aplicaciones, administrar dispositivos y ver la información de contacto de TI mediante la aplicación del Portal de empresa de Android sin inscribir sus dispositivos Android. Además, si un usuario final ya usa una aplicación protegida por directivas de protección de aplicaciones de Intune y se inicia Portal de empresa Android, el usuario final ya no recibirá un aviso para inscribir el dispositivo.
  <!-- 621669 -->



## <a name="july-2017"></a>Julio de 2017

### <a name="new-in-microsoft-intune"></a>Novedades de Microsoft Intune

- **Nuevos avisos de finalización del soporte para Android y Windows Phone**    
    Se agregaron nuevos avisos de finalización del soporte para las versiones de Android y Windows Phone. Para obtener más información, consulte [Notificaciones](#notices).


### <a name="new-in-configuration-manager-current-branch"></a>Novedades de Configuration Manager (rama actual)

Las siguientes características no estaban disponibles anteriormente en las versiones de Configuration Manager Technical Preview. Estas características están ahora disponibles en las implementaciones híbridas con Intune y Configuration Manager (Rama actual) versión 1706.

- [Compatibilidad con Entrust para entidades de certificación de Entrust](/sccm/core/get-started/capabilities-in-technical-preview-1706#support-for-entrust-certification-authorities)
- [Configuración de nueva directiva de administración de aplicaciones móviles](/sccm/core/plan-design/changes/whats-new-in-version-1706#new-mobile-application-management-policy-settings)
- [Actualizaciones a Android para la configuración de uso compartido del trabajo](/sccm/core/plan-design/changes/whats-new-in-version-1706#updates-to-android-for-work-sharing-configuration)
- [Nuevas reglas de directiva de cumplimiento de dispositivos](/sccm/core/plan-design/changes/whats-new-in-version-1706#new-device-compliance-policy-rules)
- [Nuevas opciones de configuración para dispositivos Windows 10 que no están administrados con el cliente de Configuration Manager](/sccm/core/plan-design/changes/whats-new-in-version-1706#new-configuration-settings-for-windows-10-devices-that-are-not-managed-with-the-configuration-manager-client)
- [Compatibilidad con Cisco (IPsec) para perfiles de VPN de macOS](/sccm/core/get-started/capabilities-in-technical-preview-1706#cisco-ipsec-support-for-macos-vpn-profiles)
- [Restricciones de inscripción de iOS y Android](/sccm/core/plan-design/changes/whats-new-in-version-1706#android-and-ios-enrollment-restrictions) 



## <a name="june-2017"></a>Junio de 2017

### <a name="new-in-microsoft-intune"></a>Novedades de Microsoft Intune

- **Cambio de la entidad de MDM**    
  A partir de la versión 1610 de Configuration Manager, puede cambiar la entidad de MDM sin tener que ponerse en contacto con Soporte técnico de Microsoft. Tampoco tiene que anular la inscripción y volver a inscribir los dispositivos administrados existentes. Para obtener más información, consulte [Cambio de la entidad de MDM](/sccm/mdm/deploy-use/change-mdm-authority).

- **Integración del proxy de la aplicación y Managed Browser**    
  El explorador Intune Managed Browser ahora puede integrarse con el servicio Proxy de aplicación de Azure AD para que los usuarios puedan tener acceso a los sitios web internos incluso cuando trabajan de forma remota. Los usuarios del explorador escriben la dirección URL del sitio como harían normalmente y el explorador Managed Browser enruta la solicitud a través de la puerta de enlace web del proxy de aplicación. Para obtener más información, consulte [Administrar el acceso a Internet mediante directivas de explorador administrado](https://docs.microsoft.com/intune/app-configuration-managed-browser).

- **Ahora, la aplicación Portal de empresa para Android tiene una nueva experiencia de usuario final para las directivas de protección de aplicaciones**  
  A raíz de los comentarios de clientes, hemos modificado la aplicación Portal de empresa para Android para que aparezca el botón **Acceso al contenido de la empresa**. El objetivo es impedir que los usuarios finales pasen innecesariamente por el proceso de inscripción cuando solo necesitan tener acceso a las aplicaciones que admiten directivas de protección de aplicaciones, una característica de administración de aplicaciones móviles de Intune. Puede ver estos cambios en la página [Novedades de la interfaz de usuario de aplicaciones](https://docs.microsoft.com/intune/whats-new-app-ui).

- **Nueva acción de menú para quitar fácilmente el Portal de empresa**  
  A raíz de los comentarios de los usuarios, se ha agregado en la aplicación Portal de empresa para Android una nueva acción de menú para iniciar la eliminación del Portal de empresa desde el dispositivo. Con esta acción se quita el dispositivo de administración de Intune para que la aplicación se pueda quitar del dispositivo por parte del usuario. Puede ver estos cambios en la página de [novedades de la interfaz de usuario de aplicaciones](https://docs.microsoft.com/intune/whats-new-app-ui) y en la [documentación de Android para el usuario final](https://docs.microsoft.com/intune-user-help/unenroll-your-device-from-intune-android).

- **Mejoras en la sincronización de aplicaciones con Windows 10 Creators Update**  
  Ahora, la aplicación Portal de empresa para Windows 10 iniciará automáticamente una sincronización para las solicitudes de instalación de aplicaciones destinadas a dispositivos con Windows 10 Creators Update (versión 1703). Este comportamiento reduce el problema por el cual las instalaciones de aplicaciones se detienen durante el estado "Sincronización pendiente". Además, los usuarios podrán iniciar manualmente la sincronización desde la aplicación. Puede ver estos cambios en la página [Novedades de la interfaz de usuario de aplicaciones](https://docs.microsoft.com/intune/whats-new-app-ui).

- **Nueva experiencia guiada para el Portal de empresa de Windows 10**  
  La aplicación Portal de empresa para Windows 10 incluye una experiencia guiada de tutorial de Intune para dispositivos que no se han identificado o inscrito. La nueva experiencia proporciona instrucciones paso a paso que guían al usuario a través del registro en Azure Active Directory (necesario para las características de acceso condicional) y la inscripción de MDM (necesario para las características de administración de dispositivos). Será posible acceder a esta experiencia guiada desde la página de inicio de Portal de empresa. Si los usuarios no completan el registro y la inscripción, pueden seguir utilizando la aplicación pero experimentarán una funcionalidad limitada.

  Esta actualización solo está visible en dispositivos que ejecutan Actualización de aniversario de Windows 10 (compilación 1607) o superior. Puede ver estos cambios en la página [Novedades de la interfaz de usuario de aplicaciones](https://docs.microsoft.com/intune/whats-new-app-ui).

- **Mejoras en los iconos de aplicación en la aplicación Portal de empresa para iOS**  
  Se ha actualizado el diseño de los iconos de aplicación en la página principal para reflejar el color de personalización de marca que establezca para el Portal de empresa. Para obtener más información, consulte [Novedades de la interfaz de usuario de aplicaciones](https://docs.microsoft.com/intune/whats-new-app-ui).

- **El selector de cuenta ya está disponible para la aplicación Portal de empresa para iOS**  
  Si los usuarios de dispositivos iOS usan su cuenta profesional o educativa para iniciar sesión en otras aplicaciones de Microsoft, pueden ver nuestro nuevo selector de cuenta cuando inician sesión en Portal de empresa. Para obtener más información, consulte [Novedades de la interfaz de usuario de aplicaciones](https://docs.microsoft.com/intune/whats-new-app-ui).

### <a name="new-in-configuration-manager-technical-preview-1706"></a>Novedades de Configuration Manager Technical Preview 1706

- **Nuevas opciones para elementos de configuración de Windows**      
  Hay nuevos elementos de configuración de Windows disponibles para las categorías de ajustes Contraseña, Dispositivo, Tienda y Microsoft Edge. Para obtener más información, vea [Nuevas opciones para elementos de configuración de Windows](/sccm/core/get-started/capabilities-in-technical-preview-1706#new-windows-configuration-item-settings).
  <!-- 1354715 -->

- **Nuevas reglas de directiva de cumplimiento de dispositivos**   
  Ahora puede configurar nuevas opciones de directivas de cumplimiento que anteriormente solo estaban disponibles en Intune independiente. Para obtener más información, consulte [Mejoras de la directiva de cumplimiento de dispositivos](/sccm/core/get-started/capabilities-in-technical-preview-1706#new-device-compliance-policy-rules).

- **Restricciones de inscripción de iOS y Android**       
  Los administradores ahora pueden especificar que los usuarios no inscriban los dispositivos personales de Android o iOS en su entorno híbrido. Esta acción permite limitar los dispositivos inscritos a aquellos declarados con anterioridad que pertenezcan a la empresa, o bien a aquellos dispositivos iOS inscritos solo con el Programa de inscripción de dispositivos. Para obtener más información, consulte [Restricciones de inscripción de iOS y Android](/sccm/core/get-started/capabilities-in-technical-preview-1706#android-and-ios-enrollment-restrictions).
  <!-- 1290826 -->

- **Compatibilidad con entidades de certificación de Entrust**      
  Configuration Manager ahora admite entidades de certificación de Entrust. Esta compatibilidad habilita la entrega de certificados PFX para dispositivos inscritos en Microsoft Intune.    
  <!-- 1350740 -->

  Puede configurar Entrust como entidad de certificación al agregar un rol de Punto de registro de certificados en Configuration Manager. Al agregar un nuevo perfil de certificado que emite certificados PFX, puede seleccionar una entidad de certificación de Microsoft o Entrust.

  **Problema conocido**: en la versión 1706 de Technical Preview no se emiten certificados PFX para entidades de certificación de Microsoft. Este problema no afecta a los certificados PFX o a los perfiles de SCEP importados.

- **Compatibilidad con Cisco (IPsec) para perfiles de VPN de macOS**      
  Puede crear un perfil de VPN de macOS con Cisco (IPsec) como tipo de conexión. Para obtener más información, vea [Crear perfiles de VPN](/sccm/mdm/deploy-use/create-vpn-profiles#create-vpn-profiles).
  <!-- 1321367 -->


## <a name="notices"></a>Notificaciones

### <a name="company-portal-for-windows-81-and-windows-phone-81-moving-to-sustaining-mode"></a>El Portal de empresa para Windows 8.1 y Windows Phone 8.1 se mueve al modo de mantenimiento 
<!--1428681-->
*6 de octubre de 2017*   
 
A partir de octubre de 2017, las aplicaciones Portal de empresa para Windows 8.1 y Windows Phone 8.1 pasan al modo de mantenimiento. Este modo significa que las aplicaciones y los escenarios existentes, como inscripción y cumplimiento, se seguirán admitiendo en estas plataformas. Estas aplicaciones se pueden seguir descargando en los canales de lanzamiento existentes, como Microsoft Store. 

Una vez en el modo de mantenimiento, estas aplicaciones solo reciben actualizaciones de seguridad críticas. No habrá actualizaciones adicionales ni características para ellas. En el caso de nuevas características, se recomienda actualizar los dispositivos a Windows 10 o Windows 10 Mobile. 

### <a name="end-of-support-for-ios-80"></a>Finalización del soporte de iOS 8.0 
<!---1164477--->
Las aplicaciones administradas y la aplicación Portal de empresa para iOS necesitan iOS 9.0 y posterior para poder acceder a los recursos de la empresa. Los dispositivos que no estén actualizados antes de septiembre ya no podrán acceder a Portal de empresa ni a esas aplicaciones. 

### <a name="platform-support-reminder-windows-phone-81-mainstream-support-ended-july-11-2017"></a>Recordatorio sobre el soporte técnico para la plataforma: el soporte técnico estándar para Windows Phone 8.1 finalizó el 11 de julio de 2017
<!-- 1327781 -->
*11 de julio de 2017*

La plataforma Windows Phone 8.1 ha llegado a la finalización del soporte técnico estándar. El soporte técnico para equipos con Windows 8.1 no se verá afectado.

Esto no afecta inmediatamente a ningún dispositivo Windows Phone 8.1 administrado por el servicio de Intune, incluidos los dispositivos inscritos en entornos híbridos MDM. Los dispositivos que están inscritos seguirán funcionando. Todas las directivas, configuraciones y aplicaciones siguen funcionando como se espera. Tenga en cuenta que no hay mejoras previstas para la plataforma Windows Phone 8.1 en el servicio de Intune ni para la aplicación Portal de empresa de Windows Phone 8.1.

Se recomienda actualizar los dispositivos Windows Phone 8.1 aptos a Windows 10 Mobile lo antes posible.  

### <a name="end-of-support-for-android-43-and-lower"></a>Finalización del soporte para Android 4.3 y versiones inferiores
<!---1171127--->
*6 de julio de 2017*

Las aplicaciones administradas y la aplicación Portal de empresa para Android necesitan Android 4.4 y posterior para poder acceder a los recursos de la empresa. Los dispositivos que no estén actualizados antes de principios de octubre ya no pueden acceder a Portal de empresa ni a esas aplicaciones. En diciembre, se forzará la retirada de todos los dispositivos inscritos, con lo que ya podrán acceder a los recursos de la empresa. Si está usando directivas de protección de aplicaciones sin MDM, las aplicaciones no recibirán actualizaciones y la calidad de la experiencia se irá reduciendo con el tiempo.



## <a name="see-also"></a>Véase también

- [Notificaciones y características híbridas anteriores de MDM](whats-new-hybrid-archive.md)
- [Novedades de MDM en System Center 2012 Configuration Manager](https://technet.microsoft.com/library/mt445560.aspx)
