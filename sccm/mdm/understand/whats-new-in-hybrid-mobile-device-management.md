---
title: Novedades de la MDM híbrida
titleSuffix: Configuration Manager
description: Obtenga información sobre las nuevas características de administración de dispositivos móviles disponibles para implementaciones híbridas con Configuration Manager e Intune.
ms.date: 05/28/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 7b127cee-61f1-4681-9760-caebed36ddf5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: b6a4cfbc7e9db5f4402278b73c2ca7ea1d869953
ms.sourcegitcommit: 18a94eb78043cb565b05cd0e9469b939b29cccf0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/29/2019
ms.locfileid: "66355032"
---
# <a name="whats-new-in-hybrid-mobile-device-management-with-configuration-manager-and-microsoft-intune"></a>Novedades de la administración híbrida de dispositivos móviles con Configuration Manager y Microsoft Intune

*Se aplica a: System Center Configuration Manager (Rama actual)*

En este artículo se proporciona información sobre nuevas características de administración de dispositivos móviles (MDM) disponibles para implementaciones híbridas con System Center Configuration Manager y Microsoft Intune.

> [!Important]  
> Desde el 14 de agosto de 2018, la administración híbrida de dispositivos móviles es una [característica en desuso](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). Para más información, vea [¿Qué es la Administración híbrida de dispositivos móviles (MDM)?](/sccm/mdm/understand/hybrid-mobile-device-management).<!--Intune feature 2683117-->  

> [!Note]  
> Intune en Azure es la solución de MDM recomendada por Microsoft.
>
> - Para obtener más información sobre las nuevas características y actualizaciones de Intune independiente, vea [Novedades de Microsoft Intune](https://docs.microsoft.com/intune/whats-new).
> - Para obtener más información sobre cómo migrar a Intune independiente, vea [Migrate hybrid MDM users and devices to Intune standalone](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa) (Migrar a Intune independiente usuarios y dispositivos de MDM híbrido).
> - Para obtener más información sobre las actualizaciones de la interfaz de usuario de Intune y de MDM híbrido, vea [Actualizaciones de la interfaz de usuario para las aplicaciones de usuario final de Intune](https://docs.microsoft.com/intune/whats-new-app-ui).



## <a name="compatibility-with-configuration-manager-versions"></a>Compatibilidad con versiones de Configuration Manager  

En cada sección de este artículo se enumeran las características híbridas organizadas en tres categorías diferentes. Use las indicaciones siguientes para determinar la compatibilidad de las características de cada categoría con las diferentes versiones de Configuration Manager:  

|Categorías de características|Descripción|
|-|-|
|**Novedades de Microsoft Intune** | En general, todas las características que se enumeran en esta categoría deberían funcionar con todas las versiones de Configuration Manager, incluidas las versiones de System Center 2012 R2 Configuration Manager, ya que estas características solo necesitan el servicio de Intune y ninguna función adicional en Configuration Manager.|
|**Novedades de Configuration Manager Technical Preview**| Todas las funciones que se enumeran en esta categoría funcionan únicamente con la rama preliminar técnica especificada. Para probar estas características, debe instalar la versión preliminar técnica especificada en la descripción de la característica. Para obtener más información, consulte [Technical Preview para Configuration Manager](/sccm/core/get-started/technical-preview).|
|**Novedades de Configuration Manager (rama actual)**| Todas las características que se enumeran en esta categoría funcionan únicamente con la versión especificada de Configuration Manager (rama actual). Si usa una versión anterior de Configuration Manager para su implementación híbrida, actualice a la versión de Configuration Manager (rama actual) que se especifica en la descripción de la característica. Para obtener más información, consulte [Actualizar a System Center Configuration Manager](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager).|


## <a name="may-2019"></a>Mayo de 2019

### <a name="new-in-microsoft-intune"></a>Novedades de Microsoft Intune

#### <a name="windows-company-portal-app"></a>Aplicación Portal de empresa de Windows

<!-- 3316993 -->

La aplicación de Portal de empresa de Windows ahora tiene una nueva página con la etiqueta **dispositivos**. El **dispositivos** página muestra los usuarios de todos los dispositivos inscritos. Los usuarios verán este cambio en el Portal de empresa cuando utiliza la versión 10.3.4291.0 y versiones posteriores. Para obtener más información, consulte [cómo configurar la aplicación de Portal de empresa de Microsoft Intune](https://docs.microsoft.com/intune/company-portal-app).

#### <a name="android-enterprise-app-management"></a>Administración de aplicaciones de Android Enterprise

<!-- 4459905 -->

Para que sea más fácil de configurar y usar la administración de Android Enterprise, Intune agrega automáticamente las siguientes cuatro Android Enterprise comunes relacionados con las aplicaciones a la consola de administración de Intune:

- [Microsoft Intune](https://play.google.com/store/apps/details?id=com.microsoft.intune): Se usa para escenarios de empresa Android totalmente administrados
- [Microsoft Authenticator](https://play.google.com/store/apps/details?id=com.azure.authenticator): Si utiliza la verificación de dos factores, esta aplicación le ayuda a iniciar sesión en sus cuentas
- [Portal de empresa de Intune](https://play.google.com/store/apps/details?id=com.microsoft.windowsintune.companyportal): Utilizado para las directivas de protección de aplicación (aplicación) y escenarios de perfil de trabajo de Android Enterprise
- [Pantalla principal de Managed](https://play.google.com/store/apps/details?id=com.microsoft.launcher.enterprise): Utilizado para los escenarios de dedicado/quiosco de Android Enterprise

Antes, durante la instalación, era necesario buscar manualmente y aprobar estas aplicaciones en la [tienda Google Play administrado](https://play.google.com/store/apps). Este cambio elimina esos pasos manuales previamente para que sea más fácil y rápido usar la administración de Android Enterprise.

Cuando se conecta primero su inquilino de Intune a Google Play administrado, consulte estas cuatro aplicaciones que se agregan automáticamente a la lista aplicaciones Intune. Para obtener más información, consulte [habilitar inscripción de Android for Work](/sccm/mdm/deploy-use/enroll-hybrid-android#enable-android-for-work-enrollment). Si ya ha conectado al inquilino o ya utiliza Android Enterprise, es necesario hacer nada. Estas cuatro aplicaciones se muestran automáticamente dentro de siete días después de actualizar el servicio de mayo de 2019.

#### <a name="intune-policies-update-authentication-method-and-company-portal-app-installation"></a>Las directivas de Intune actualización método de autenticación y la instalación de la aplicación de Portal de empresa

<!-- 1927359 -->

En los dispositivos ya inscritos mediante el Asistente de instalación a través de uno de los métodos de inscripción de dispositivos corporativos de Apple, Intune no admite el Portal de empresa cuando se instala manualmente los usuarios de la tienda de aplicaciones. Este cambio solo es pertinente cuando se autentica con el Asistente de configuración de Apple durante la inscripción. Solo afecta a los dispositivos iOS inscritos a través de los métodos siguientes:  

- Apple Configurator
- Gestor empresarial de Apple
- Apple School Manager
- Programa de inscripción de dispositivos de Apple (DEP)

Si los usuarios instalación la aplicación de Portal de empresa desde la tienda de aplicaciones y, a continuación, intentan inscribir estos dispositivos a través de él, recibe un error. Además, el **identifique el dispositivo** pantalla de la aplicación de Portal de empresa pronto quedarán obsoleta.

Para instalar el Portal de empresa en dispositivos DEP ya está inscrito, insertar como una aplicación administrada con directivas de configuración de aplicación. Para obtener más información sobre este proceso, consulte [aplicar configuración a aplicaciones iOS con directivas de configuración de aplicaciones en Configuration Manager](/sccm/mdm/deploy-use/configure-ios-apps-with-app-configuration-policies).


## <a name="april-2019"></a>Abril de 2019

### <a name="new-in-microsoft-intune"></a>Novedades de Microsoft Intune

#### <a name="openssl-encryption-for-android-app-protection-policies"></a>Cifrado de OpenSSL para las directivas de protección de aplicaciones Android

<!-- 3747362 -->
Directivas de protección de aplicación (aplicación) de Intune en dispositivos Android ahora usan una biblioteca de cifrado de OpenSSL que FIPS 140-2 compatibles. Para obtener más información, consulte [configuración de directiva de protección de aplicaciones Android en Microsoft Intune](https://docs.microsoft.com/intune/app-protection-policy-settings-android#encryption).


## <a name="march-2019"></a>Marzo de 2019

### <a name="new-in-microsoft-intune"></a>Novedades de Microsoft Intune

#### <a name="user-experience-update-for-the-company-portal-app-for-ios"></a>Actualización de la experiencia de usuario para la aplicación Portal de empresa para iOS

<!-- 2536024 -->
Se ha rediseñado la página principal de la aplicación de Portal de empresa para dispositivos iOS. Con este cambio, la página principal se adapta mejor patrones de la interfaz de usuario de iOS. También se proporciona un mejor descubrimiento de aplicaciones y libros electrónicos.

#### <a name="install-available-apps-using-the-company-portal-app-after-windows-bulk-enrollment"></a>Instalar aplicaciones disponibles para el uso de la aplicación de Portal de empresa después de inscripción masiva de Windows

<!-- 2751523 -->
Dispositivos Windows inscritos en Intune mediante [inscripción masiva de Windows](https://docs.microsoft.com/intune/windows-bulk-enroll) (paquetes de aprovisionamiento) podrán usar la aplicación de Portal de empresa para instalar aplicaciones disponibles. Para obtener más información acerca de la aplicación de Portal de empresa, consulte [agregar manualmente el Portal de empresa de Windows 10](https://docs.microsoft.com/intune/store-apps-company-portal-app) y [cómo configurar la aplicación de Portal de empresa de Microsoft Intune](https://docs.microsoft.com/intune/company-portal-app).

> [!Note]  
> Esta característica todavía no se implementa por completo a todos los clientes. Si no puede usar el Portal de empresa en dispositivos inscritos de forma masiva, tendrá que esperar hasta que este cambio implementa a su cuenta.

#### <a name="app-icons-are-displayed-with-an-automatically-generated-background"></a>Se muestran iconos de aplicación con un fondo generado automáticamente

<!-- 1429026 -->
La aplicación de Portal de empresa de Windows ahora muestra los iconos de aplicación con un fondo generado automáticamente. Este fondo se basa en el color dominante del icono, si se detecta. Cuando sea aplicable, el fondo reemplaza el borde gris que antes era visible en los iconos de aplicación. Verá este cambio en las versiones posteriores a 10.3.3451.0 del Portal de empresa.

#### <a name="changes-to-company-portal-enrollment-for-ios-12-devices"></a>Cambios realizados en la inscripción de Portal de empresa para dispositivos iOS 12

<!-- 3448635 -->  
Portal de empresa para iOS actualiza las pantallas de inscripción de la aplicación y los pasos para alinearse con los cambios de inscripción de MDM que publicó en Apple iOS 12.2. El flujo de trabajo actualizado ahora le pide que:

- Permitir Safari abrir el sitio Web de Portal de empresa (a través de Safari) y descargar el perfil de administración antes de volver a la aplicación de Portal de empresa. 
- Abra la aplicación de configuración para instalar el perfil de administración en su dispositivo.
- Vuelva a la aplicación de Portal de empresa para realizar la inscripción.  

Para obtener más información acerca de cómo puede prepararse para estos cambios, consulte el [post de la comunidad tecnológica de Microsoft](https://aka.ms/CP_changes_iOS12). Para admitir nuevas inscripciones de iOS en el Portal de empresa, consulte [inscribir dispositivos de iOS en Intune](https://docs.microsoft.com/intune/ios-enroll).



## <a name="february-2019"></a>Febrero de 2019

### <a name="new-in-microsoft-intune"></a>Novedades de Microsoft Intune

#### <a name="create-new-intune-tenants-in-azure-portal"></a>Creación de nuevos inquilinos de Intune en Azure portal

<!--3754067-->  
Se ha quitado la capacidad para crear a un nuevo inquilino MDM híbrida como de la 1902 actualización de Intune. Crear a todos los nuevos inquilinos de Intune en Azure portal. Como recordatorio, [hybrid MDM está en desuso](/sccm/mdm/understand/hybrid-mobile-device-management). Clientes actuales de MDM híbrida deberían migrar a Intune independiente tan pronto como sea posible.

Para obtener más información, vea la [entrada del blog de soporte técnico de Intune](https://aka.ms/hybrid_notification).

#### <a name="intune-uses-google-play-protect-apis-on-android-devices"></a>Intune usa Google Play proteger API en dispositivos Android

<!--2577355-->  
Algunos administradores se enfrentan a un panorama BYOD donde los usuarios pueden de raíz o jailbreak sus teléfonos móviles. Este comportamiento, mientras que en ocasiones, no malintencionadas, da como resultado una omisión de muchas de las directivas de Intune que se establecen con el fin de proteger los datos de la organización en los dispositivos de usuario final. Por lo tanto, Intune proporciona la detección de jailbreak y raíz para los dispositivos inscritos y no inscritos.

Con esta versión, Intune ahora aprovecha reproducir proteger las API de Google para agregar a nuestra comprobaciones de detección de raíz existente para los dispositivos no inscritos. Mientras Google no comparte la totalidad de las comprobaciones de detección de raíz que se producen, esperamos que estas API para detectar los usuarios que han modificado sus dispositivos por cualquier motivo de personalización del dispositivo para poder obtener las actualizaciones más recientes del sistema operativo en dispositivos más antiguos. A continuación, se pueden bloquear estos usuarios tengan acceso a datos corporativos o se pueden eliminar sus cuentas de empresa desde sus aplicaciones de directiva habilitada.

#### <a name="new-app-categories-screen-in-the-company-portal-app-for-windows-10"></a>Nuevo **categorías de aplicaciones** pantalla de la aplicación de Portal de empresa para Windows 10

<!--3834780-->  
Para mejorar la experiencia de exploración y la selección de aplicación de Portal de empresa para Windows 10, ahora incluye una nueva pantalla llamada **categorías de aplicaciones**. Ahora, los usuarios ven sus aplicaciones ordenados en categorías como **destacado**, **Education**, y **productividad**. Este cambio aparece en las versiones de Portal de empresa 10.3.3451.0 y versiones posteriores. Para ver la nueva pantalla, consulte [cuáles son las novedades en el interfaz de usuario de la aplicación](https://docs.microsoft.com/intune/whats-new). Para obtener más información acerca de las aplicaciones en el Portal de empresa, consulte [instalar y compartir aplicaciones en el dispositivo](https://docs.microsoft.com/intune-user-help/install-apps-cpapp-windows).  

#### <a name="macos-users-are-prompted-to-update-their-password"></a>los usuarios de macOS le pida que actualice su contraseña

<!--1873216-->  
En los dispositivos macOS, los usuarios finales se pide que actualice su contraseña. Este mensaje se produce cada vez que un usuario ejecuta una tarea que requiere autenticación, como iniciar sesión en el dispositivo. Usuarios también se le pide que actualice su contraseña cuando se hace nada que requiere privilegios administrativos, por ejemplo, solicitar acceso a llaves.  

#### <a name="intune-macos-company-portal-dark-mode"></a>MacOS modo oscuro del Portal de empresa de Intune

<!--3300524-->  
El Portal de empresa de macOS de Intune ahora admite el modo oscuro para macOS. Cuando se habilita el modo oscuro en un dispositivo macOS 10.14 +, el Portal de empresa ajusta su apariencia a los colores que reflejen ese modo.



## <a name="january-2019"></a>Enero de 2019

### <a name="new-in-microsoft-intune"></a>Novedades de Microsoft Intune

#### <a name="intune-app-protection-policies-ui-update"></a>Actualización de la interfaz de usuario de Intune app protection directivas

<!--3251427-->  
Hemos cambiado las etiquetas para la configuración y los botones para protección de aplicaciones de Intune para que sea más fácil comprender cada uno de ellos. Algunos de los cambios incluyen:  

- Los controles se cambian de **Sí** / **ningún** controla principalmente a **bloque** / **permitir** y **deshabilitar** / **habilitar** controles. Las etiquetas también se actualizan.  

- Configuración cambian, por lo que la configuración y su etiqueta están en paralelo en el control, para proporcionar una mejor navegación.  

La configuración predeterminada y el número de opciones que siguen siendo los mismos, pero este cambio permite al usuario a entender, navegar y usar la configuración más fácilmente para aplicar directivas de protección de la aplicación seleccionada. Para obtener más información, consulte [configuración de iOS](https://docs.microsoft.com/intune/app-protection-policy-settings-ios#access-requirements) y [configuración de Android](https://docs.microsoft.com/intune/app-protection-policy-settings-android#access-requirements).

#### <a name="tenant-status-dashboard"></a>Panel de estado de inquilino

<!--1124854-->  
El nuevo [página Estado del inquilino](https://docs.microsoft.com/intune/tenant-status) proporciona una ubicación única donde puede ver el estado y los detalles relacionados para el inquilino. El panel se divide en cuatro áreas:

- **Detalles de inquilino**: Muestra información que incluye el nombre del inquilino y la ubicación, la entidad de MDM, el total de los dispositivos inscritos en el inquilino y la cuenta de su licencia. En esta sección también muestra la versión actual del servicio para el inquilino.  

- **Estado del conector**: Muestra información acerca de los conectores disponibles ha configurado y también se pueden mostrar aquellos que aún no ha habilitado.  

    Según el estado actual de cada conector, se marcan como correcto, advertencia o incorrecto. Seleccione un conector para la obtención de detalles y ver los detalles o configurar más información sobre ella.  

- **Estado del servicio de Intune**: Muestra los detalles sobre los incidentes activos o interrupciones para el inquilino. La información de esta sección se recupera directamente desde el centro de mensajes de Office.  

- **Noticias de Intune**: Muestra mensajes activos para el inquilino. Los mensajes incluyen cosas como notificaciones cuando el inquilino recibe las últimas características de Intune.  La información de esta sección se recupera directamente desde el centro de mensajes de Office.  

#### <a name="new-help-and-support-experience-in-company-portal-for-windows-10"></a>La nueva ayuda y soporte técnico de experiencia en el Portal de empresa para Windows 10

<!--1488939-->  
La nueva página de Ayuda del Portal de empresa y soporte técnico ayuda a los usuarios a solucionar problemas y solicitar ayuda para problemas de aplicación y el acceso. En la página nueva, pueden enviar por correo electrónico de error y los detalles de registro de diagnóstico y encontrar los detalles del departamento de soporte técnico de su organización. También encontrará una sección de preguntas más frecuentes con vínculos a la documentación pertinente de Intune. Para obtener más información y capturas de pantalla, consulte [Obtenga ayuda y soporte técnico en el Portal de empresa para Windows 10](https://docs.microsoft.com/intune-user-help/help-and-support-windows-cpapp).

#### <a name="some-bitlocker-settings-support-windows-10-pro-edition"></a>Algunas opciones de configuración de BitLocker admiten la edición Windows 10 Pro

<!--2727036-->  
Puede crear un elemento de configuración que establece la configuración de endpoint protection en dispositivos Windows 10, incluidos BitLocker. Esta actualización agrega compatibilidad para Windows 10 Professional edition para algunas configuraciones de BitLocker.

Para obtener más información, consulte [configuración de cifrado para Windows 10](/sccm/mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client#encryption).



## <a name="december-2018"></a>Diciembre de 2018

### <a name="new-in-microsoft-intune"></a>Novedades de Microsoft Intune

#### <a name="microsoft-auto-update-version-450-required-for-macos-devices"></a>Versión 4.5.0 de actualización automática de Microsoft para dispositivos macOS

<!--3503442-->  
Para seguir recibiendo actualizaciones para el Portal de empresa y otras aplicaciones de Office, deben actualizar dispositivos macOS administrados por Intune a Microsoft de la actualización automática 4.5.0. Los usuarios que ya tenga esta versión para las aplicaciones de Office.

#### <a name="the-intune-app-sdk-will-support-256-bit-encryption-keys"></a>Intune App SDK será compatible con las claves de cifrado de 256 bits

<!--1832174-->  
Intune App SDK para Android ahora usa las claves de cifrado de 256 bits cuando se habilita el cifrado mediante directivas de protección de aplicaciones. El SDK seguirá proporcionando soporte técnico de claves de 128 bits para la compatibilidad con el contenido y las aplicaciones que usan versiones anteriores de SDK.

#### <a name="intune-requires-macos-1012-or-later"></a>Intune requiere macOS 10.12 o versiones posteriores

<!--2827778-->  
Intune ahora requiere macOS versión 10.12 o versiones posterior. Dispositivos con versiones anteriores de macOS no pueden usar el Portal de empresa para inscribir en Intune. Para recibir soporte técnico y las nuevas características, los usuarios deben actualizar sus dispositivos a macOS 10.12 o versiones posteriores y actualizar el Portal de empresa a la versión más reciente.

Para obtener más información, consulte [Plan de cambio: Intune admite macOS 10.12 y superior en diciembre](#plan-for-change-intune-supports-macos-1012-and-higher-in-december).



## <a name="november-2018"></a>Noviembre de 2018

### <a name="new-in-microsoft-intune"></a>Novedades de Microsoft Intune

#### <a name="new-intune-device-subscription-sku"></a>Nueva suscripción de dispositivo de Intune SKU

<!--3312071-->  
Para ayudar a reducir el costo de administración de dispositivos en las empresas, una nueva suscripción basado en dispositivos SKU ya está disponible. Este dispositivo de Intune SKU es una licencia por dispositivo mensualmente. Precio varía según el programa de licencias. Está disponible en Direct Channel, contrato Enterprise (EA), Microsoft Products y servicios de programa (MPSA) y abrir y proveedor de soluciones en la nube (CSP).

#### <a name="new-apps-support-with-app-protection-policies"></a>Compatibilidad con nuevas aplicaciones con directivas de protección de aplicaciones

<!--3330037-->  
Ahora puede administrar las siguientes aplicaciones con [directivas de protección de aplicaciones de Intune](https://docs.microsoft.com/intune/app-protection-policies):

- Stream (iOS)  
- Hacer (Android, iOS)  
- PowerApps (Android, iOS)  
- Flujo (Android, iOS)  

Use directivas de protección para proteger la transferencia de datos corporativa de control y de datos para estas aplicaciones, al igual que otras aplicaciones administradas por directivas de Intune.

> [!Note]  
> Si aún no está visible en la consola de flujo, agregue flujo al crear o editar las directivas de protección. Seleccione **más aplicaciones**y, a continuación, especifique el *Id. de aplicación* flujo en el campo de entrada. Para su uso Android `com.microsoft.flow`, y para usar iOS `com.microsoft.procsimo`.  



## <a name="october-2018"></a>Octubre de 2018

### <a name="new-in-microsoft-intune"></a>Novedades de Microsoft Intune

#### <a name="updates-for-application-transport-security"></a>Actualizaciones para Seguridad de transporte de aplicaciones

<!--748318-->  
Microsoft Intune es compatible con la capa de transporte (TLS) 1.2 + para proporcionar el cifrado en su clase, para asegurarse de que Intune es más seguro de forma predeterminada y para adaptarlos a otros servicios de Microsoft, como Microsoft Office 365. Con el fin de satisfacer este requisito, en los portales de empresa de iOS y macOS se exigirán los requisitos de Seguridad de transporte de aplicaciones (ATS) actualizados de Apple que también requieren TLS 1.2+. ATS se utiliza para exigir una seguridad más estricta en todas las comunicaciones de aplicación a través de HTTPS. Este cambio afecta a los clientes de Intune que usan las aplicaciones Portal de empresa para iOS y macOS. Para obtener más información, consulte [Intune moving to TLS 1.2 for encryption](https://blogs.technet.microsoft.com/intunesupport/2018/06/05/intune-moving-to-tls-1-2-for-encryption/) (Actualización de Intune a TLS 1.2 para el cifrado).

#### <a name="remove-an-email-profile-from-a-device-even-when-theres-only-one-email-profile"></a>Eliminación de un perfil de correo electrónico de un dispositivo, incluso cuando solo hay un perfil

<!--1818139-->  
Anteriormente, no se pudo quitar un perfil de correo electrónico de un dispositivo si es el único perfil de correo electrónico. Con esta actualización, se cambia este comportamiento. Ahora, puede quitar un perfil de correo electrónico, incluso si es el único en el dispositivo.

#### <a name="remove-pkcs-and-scep-certificates-from-your-devices"></a>Eliminación de certificados PKCS y SCEP de los dispositivos

<!--3218390-->  
En algunos escenarios, los certificados PKCS y SCEP permanecieron en dispositivos, incluso cuando se quita una directiva de un grupo, la eliminación de una configuración o implementación de cumplimiento o un administrador actualizar un perfil SCEP o PKCS existente.

En esta actualización se cambia el comportamiento. Hay algunos escenarios donde los certificados PKCS y SCEP se quitan de los dispositivos y otros escenarios en los que estos certificados se conservan.

#### <a name="access-to-key-profile-properties-using-the-company-portal-app"></a>Acceso a las propiedades de perfil principales mediante la aplicación del Portal de empresa

<!--772203-->  
Los usuarios finales ahora pueden acceder a las propiedades y acciones principales de la cuenta, como el restablecimiento de contraseñas, desde la aplicación del Portal de empresa.

#### <a name="pin-prompt-when-you-change-fingerprints-or-face-id-on-an-ios-device"></a>Solicitud de PIN al cambiar las huellas digitales o Face ID en un dispositivo iOS

<!--2637704-->  
Ahora se solicitará a los usuarios un PIN después de realizar cambios biométricos en su dispositivo iOS. Esto incluye los cambios en Face ID o huellas digitales registrados. El tiempo de la solicitud depende de la configuración del tiempo de expiración de *Volver a comprobar los requisitos de acceso después de (minutos)* .  Si no hay ningún PIN configurado, se pide al usuario que establezca uno.  

Esta característica solo está disponible para iOS y requiere la participación de las aplicaciones que integran el SDK de aplicaciones de Intune para iOS, versión 8.1.1 o posteriores. La integración del SDK es necesaria para poder aplicar el comportamiento en las aplicaciones de destino. Esta integración ocurre de manera gradual y depende de los equipos de la aplicación específica. Algunas aplicaciones participantes incluyen WXP, Outlook, Managed Browser y Yammer.

#### <a name="end-user-device-and-app-content-menu"></a>Menú de contenido de aplicaciones y dispositivos del usuario final

<!--2771453-->  
Los usuarios finales ahora pueden usar el menú contextual del dispositivo y las aplicaciones para desencadenar acciones comunes, como cambiar el nombre de un dispositivo o comprobar el cumplimiento.

#### <a name="windows-company-portal-keyboard-shortcuts"></a>Métodos abreviados de teclado del Portal de empresa de Windows

<!--2771518-->  
Los usuarios finales ahora pueden desencadenar acciones de aplicación y dispositivo en el Portal de empresa de Windows mediante métodos abreviados de teclado (aceleradores).



## <a name="august-2018"></a>Agosto de 2018

### <a name="new-in-microsoft-intune"></a>Novedades de Microsoft Intune

#### <a name="new-user-experience-update-for-the-company-portal-website"></a>Nueva actualización de la experiencia de usuario para el sitio web del Portal de empresa

<!--2000968-->  
En función de sus comentarios, hemos agregado nuevas características para el sitio Web de Portal de empresa. Puede experimentar una mejora considerable en la funcionalidad y la facilidad de uso actuales de los dispositivos Android, iOS y Windows. Las áreas del sitio han adoptado un diseño nuevo, moderno y dinámico. Estas áreas incluyen los detalles del dispositivo, los comentarios, el soporte técnico y la información general del dispositivo. También verá las siguientes mejoras:

- Flujos de trabajo optimizados en todas las plataformas de dispositivo
- Flujos mejorados para la inscripción e identificación de dispositivos
- Mensajes de error más útiles
- Lenguaje más descriptivo y menos terminología técnica
- Capacidad de compartir vínculos directos a aplicaciones
- Rendimiento mejorado de los catálogos de aplicaciones de gran tamaño
- Aumento de accesibilidad para todos los usuarios



## <a name="july-2018"></a>Julio de 2018

### <a name="new-in-microsoft-intune"></a>Novedades de Microsoft Intune

#### <a name="updated-intune-app-sdk-for-android-is-now-available"></a>El SDK de aplicaciones de Intune para Android ya está disponible

<!--2744271-->  
Una versión actualizada de Intune App SDK para Android está disponible para admitir la versión Android circular 9. Si es desarrollador de aplicaciones y usa el SDK de Intune para Android, instale la versión actualizada del SDK de aplicaciones de Intune. Esta actualización se asegura de que la funcionalidad de Intune en aplicaciones Android sigue funcionando según lo esperado en dispositivos con Android9 Pie. Esta versión del SDK de aplicaciones de Intune ofrece un complemento integrado que realiza las actualizaciones del SDK. No es necesario reescribir el código existente que está integrado. Para más información, vea [SDK de Intune para Android](https://github.com/msintuneappsdk/ms-intune-app-sdk-android).

Si usa el estilo del distintivo anterior para Intune, pase a usar el icono del maletín. Para más información sobre la personalización de marca, vea el [sistema de distintivos de aplicaciones de Intune](https://github.com/msintuneappsdk/intune-app-partner-badge).

#### <a name="support-for-security-enhancement-in-intune-service"></a>Compatibilidad con la mejora de seguridad del servicio Intune

<!--2520152-->  
Ahora puede especificar que los dispositivos sin las directivas de cumplimiento asignada no son compatibles en entornos híbridos. Configure este valor en Intune en Azure Portal. Se recomienda encarecidamente habilitar esta característica para proteger los recursos internos.

Esta característica está desactivada de manera predeterminada en inquilinos híbridos. Cuando se habilita esta característica, los dispositivos que no tienen una directiva de cumplimiento asignada se consideran no compatibles. Si también habilita el acceso condicional, estos dispositivos pierden el acceso a los recursos internos. Estos recursos pueden ser Outlook o SharePoint, en función de las directivas de acceso condicional del entorno. Si deja esta opción desactivada, estos dispositivos siguen teniendo el mismo nivel de acceso que en la actualidad.

Para ayudar a determinar el impacto de la activación de esta característica, se proporciona un [script en la Galería TechNet](https://gallery.technet.microsoft.com/SQL-Query-for-Hybrid-MDM-5bcb8695). Cuando se ejecuta este script en la base de datos de Configuration Manager, enumera los dispositivos que no tienen ninguna directiva de cumplimiento.

Vea los siguientes artículos para más información:

- Entrada de blog [Security Enhancements in the Intune Service](https://aka.ms/compliance_policies) (Mejoras de seguridad en el servicio Intune)
- [Directivas de cumplimiento de dispositivo en System Center Configuration Manager](/sccm/mdm/deploy-use/device-compliance-policies)

#### <a name="updates-to-out-of-compliance-messages-in-company-portal-app"></a>Actualizaciones de los mensajes de no compatibilidad en el Portal de empresa

<!--1832222-->  
Nos estamos revisando los mensajes que ven los usuarios de dispositivos cuando un dispositivo está fuera del cumplimiento. Los mensajes conservan sus significados originales, pero se han actualizado para usar un lenguaje más descriptivo y una jerga menos técnica. También estamos actualizando los vínculos a la documentación y las medidas de corrección para mantenerlos actualizados.  

El siguiente texto es un ejemplo de las mejoras que verá en la mensajería:  

- Antes: *Este dispositivo no ha contactado con el servicio de Intune en el período de tiempo especificado requerido por el Administrador de TI. Para resolver este problema, abra la aplicación Portal de empresa en el dispositivo y haga clic en el botón Comprobar el cumplimiento.*  

- Después de: *No se ha registrado el dispositivo con su organización en unos minutos. Para restablecer la conexión, abra la aplicación Portal de empresa en el dispositivo y pulse Comprobar configuración.*  

#### <a name="select-device-categories-by-using-the-access-work-or-school-settings"></a>Selección de las categorías de dispositivos mediante la configuración de acceso profesional o educativo

<!--1058963-->  
Si ha habilitado [asignación de grupo de dispositivos](https://docs.microsoft.com/intune/device-group-mapping), los usuarios en Windows 10 ahora le pide que seleccione una categoría de dispositivo después de la inscripción a través de la **Connect** botón **configuración**  >  **Cuentas** > **acceso profesional o educativo**.  

#### <a name="new-browsing-experiences-in-the-company-portal-app-for-windows"></a>Nuevas experiencias de exploración en la aplicación de Portal de empresa para Windows

<!--2317227-->  
Ahora al examinar o buscar aplicaciones en la aplicación de Portal de empresa para Windows, alternar entre las existentes **iconos** recién agregada y vista **detalles** vista. La nueva vista muestra detalles de la aplicación, como el nombre, el editor, la fecha de publicación y el estado de la instalación.

La vista **Instaladas** de la página **Aplicaciones** le permite ver detalles sobre las instalaciones de aplicaciones completadas y en curso. Para ver el aspecto de la nueva vista, vea [Novedades en la interfaz de usuario](https://docs.microsoft.com/intune/whats-new-app-ui).

#### <a name="more-opportunities-to-sync-in-the-company-portal-app-for-windows"></a>Más oportunidades para la sincronización en la aplicación de Portal de empresa para Windows

<!--2683177-->  
La aplicación de Portal de empresa para Windows ahora le permite iniciar una sincronización directamente desde la barra de tareas de Windows y el menú Inicio. Esta característica es especialmente útil si la única tarea es sincronizar dispositivos y obtener acceso a recursos corporativos. Para obtener acceso a la nueva característica, haga clic con el botón derecho en el icono de Portal de empresa que está anclado a la barra de tareas o al menú Inicio. En las opciones de menú, seleccione **Sincronizar este dispositivo**. (Este menú también se conoce como una Jump List.) Portal de empresa se abre en la página **Configuración** e inicia la sincronización. Para obtener información sobre el procedimiento actualizado, vea [Sincronización manual del dispositivo Windows](https://docs.microsoft.com/intune/intune-user-help/sync-your-device-manually-windows#sync-from-device-taskbar-or-start-menu).



## <a name="june-2018"></a>Junio de 2018

### <a name="new-in-microsoft-intune"></a>Novedades de Microsoft Intune

#### <a name="access-to-macos-company-portal-pre-release-build"></a>Acceso a la compilación de versión preliminar del Portal de empresa de macOS

<!--1734766-->  
Con Microsoft AutoUpdate, suscríbase para recibir las compilaciones al principio uniendo al programa Insider. El registro le permite usar el Portal de empresa actualizado antes de que esté disponible para los usuarios finales.

#### <a name="intune-app-protection-policies-and-microsoft-edge"></a>Directivas de protección de aplicaciones de Intune y Microsoft Edge

<!--1818968,1818969-->  
Ahora, el explorador Microsoft Edge para dispositivos móviles (iOS y Android) admite directivas de protección de aplicaciones de Microsoft Intune. Los usuarios de dispositivos iOS y Android que inician sesión en la aplicación Edge con sus cuentas de empresa de Azure Active Directory están protegidos por Intune. En dispositivos iOS, la directiva **Requerir Managed Browser para contenido web** permite a los usuarios abrir vínculos en Edge cuando este explorador está administrado.



## <a name="may-2018"></a>Mayo de 2018

### <a name="new-in-microsoft-intune"></a>Novedades de Microsoft Intune

#### <a name="requesting-help-in-the-company-portal-for-windows-10"></a>Solicitud de ayuda en el Portal de empresa para Windows 10

<!--1874137-->  
El Portal de empresa para Windows 10 ahora envía los registros de aplicación directamente a Microsoft cuando el usuario inicia el flujo de trabajo para obtener ayuda con un problema. Este comportamiento facilita la localización y resolución de problemas que se producen a Microsoft.  


### <a name="new-in-configuration-manager-current-branch"></a>Novedades de Configuration Manager (rama actual)

#### <a name="android-for-work-and-lookout-onboarding-moved-to-intune-on-azure"></a>La incorporación de Android for Work y Lookout se ha movido a Intune en Azure

<!--2355022,2357366-->  
Con la última actualización de Intune, puede habilitar y administrar la integración de Android for Work y la integración de Lookout Mobile Threat Defense en inquilinos de administración híbrida de dispositivos móviles en el portal de Intune o de Azure. Antes de la actualización, estas opciones solo se podían configurar en el portal clásico de Intune (Silverlight).

Nota: Lookout es el proveedor de defense (MTD) contra amenazas móviles solo que se admite en entornos híbridos. Si previamente ha utilizado otro proveedor de MTD, seguirá apareciendo en Intune en Azure Portal. Si elimina su conector, no podrá volver a agregarlo.

Estos cambios no afectan a la funcionalidad existente. Siga usando la consola de Configuration Manager para administrar las aplicaciones relacionadas, los informes y las directivas.

Vea los siguientes artículos para más información:

- [Configurar la administración híbrida de dispositivos Android](/sccm/mdm/deploy-use/enroll-hybrid-android)
- [Administrar el acceso a los recursos de la empresa según el dispositivo, la red y el riesgo de aplicación](/sccm/mdm/deploy-use/lookout-mobile-threat-defense-in-configuration-manager)

#### <a name="support-for-new-versions-of-cisco-anyconnect-client-for-ios"></a>Compatibilidad con las nuevas versiones del cliente de Cisco AnyConnect para iOS

<!--1357393-->  
Puede habilitar la compatibilidad con Cisco AnyConnect para iOS, versión 4.0.7 o posterior. Si lo hace, los perfiles de VPN de Cisco AnyConnect existentes se etiquetan **Cisco Legacy AnyConnect** y siguen funcionando como antes. La opción **Cisco AnyConnect** es para los nuevos perfiles de VPN que funcionan con Cisco AnyConnect en iOS versión 4.0.7 o posterior.

  > [!Tip]  
  > Cisco AnyConnect 4.0.07x y versiones posteriores para iOS se introdujeron primero en la versión 1802 como una [característica de versión preliminar](/sccm/core/servers/manage/pre-release-features). A partir de la [actualización 4163547](https://support.microsoft.com/help/4163547) de la versión 1802, ya no es una característica de versión preliminar.  

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
En el portal de Azure dentro del servicio de Microsoft Intune, vamos a redirigirle temporalmente de la **Intune App Protection** área para el **aplicación móvil** sección. Todas las directivas de protección de aplicaciones ya se encuentran en la sección **Aplicación móvil** de Intune, en Configuración de aplicaciones. En lugar de ir a Intune App Protection, simplemente irá a Intune. En la actualización de abril de 2018 se detendrá la redirección y quitará totalmente **Intune App Protection**. Después de esta actualización, solo habrá una ubicación para las directivas de protección de aplicaciones en Intune.

**¿Cómo me afecta este cambio?** Este cambio afectará tanto a los clientes de Intune independientes como a los clientes híbridos (Intune con Configuration Manager). Esta integración le ayudará a simplificar la administración en la nube.

**¿Qué he de hacer para prepararme para este cambio?** Etiquete **Intune** como favorito en lugar de **Intune App Protection**. Familiarícese con el flujo de trabajo de la directiva de protección de aplicaciones en el área **Aplicación móvil** dentro de Intune. Se le redirigirá durante un breve período de tiempo y luego se quitará **Intune App Protection**. Recuerde que todas las directivas de protección de aplicaciones ya se encuentran en Intune y que puede modificar cualquiera de las directivas de acceso condicional. Para obtener más información sobre cómo modificar las directivas de acceso condicional, vea [Acceso condicional en Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal). Para obtener más información, consulte [¿cuáles son las directivas de protección de aplicaciones?](https://docs.microsoft.com/intune/app-protection-policy).

#### <a name="user-experience-update-for-the-company-portal-app-for-ios"></a>Actualización de la experiencia de usuario para la aplicación Portal de empresa para iOS

<!--1412866-->  
Hemos publicado una importante actualización de la experiencia de usuario para la aplicación Portal de empresa para iOS. La actualización incluye un completo cambio de diseño visual con una apariencia modernizada. Hemos mantenido la funcionalidad de la aplicación, pero hemos mejorado su facilidad de uso y accesibilidad.  

También verá:

- Compatibilidad con el iPhone X.
- Inicio de la aplicación y carga de las respuestas más rápidos, para ahorrar tiempo a los usuarios.
- Barras de progreso adicionales para proporcionar a los usuarios la información de estado más reciente.
- Mejoras en la forma en que los usuarios cargan los registros, de modo que, si hay algún problema, sea más fácil de informar al respecto.  

Para ver el aspecto actualizado vaya a [Actualizaciones de la interfaz de usuario para las aplicaciones de usuario final de Intune](https://docs.microsoft.com/intune/whats-new-app-ui).



## <a name="march-2018"></a>Marzo de 2018

### <a name="new-in-microsoft-intune"></a>Novedades de Microsoft Intune

#### <a name="windows-company-portal-send-feedback-option-may-no-longer-work"></a>Es posible que la opción Enviar comentarios de la aplicación Portal de empresa de Windows ya no funcione.

<!--2070166-->  
La aplicación Portal de empresa de Windows ofrece la opción "Enviar comentarios", que permite a los usuarios enviar comentarios sobre la aplicación a Microsoft. Desde el 30 de abril de 2018, esta opción solo es compatible con la aplicación Portal de empresa de Windows 10, que se ejecuta en la versión 1607 y posteriores de Windows 10.

**¿Cómo me afecta este cambio?**

Si no tiene instalada la aplicación Portal de empresa de Windows para usuarios finales, ignore este mensaje.

Si algún usuario final tiene la aplicación Portal de empresa, a partir del 30 de abril, el botón "Enviar comentarios" ya no funcionará para la aplicación en estos casos:  

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
  A partir de esta versión, debe configurar y administrar las directivas de acceso condicional en [Azure Portal](https://portal.azure.com) desde **Azure Active Directory** > **Acceso condicional**. Para su comodidad, también puede acceder a esta configuración de Intune en Azure Portal en **Intune** > **Acceso condicional**.
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
  La aplicación de Microsoft Planner para iOS y Android ahora forma parte de las aplicaciones aprobadas para la administración de aplicaciones móviles (MAM). Configure la aplicación a través de Intune App Protection de Azure Portal para todos los inquilinos. Para obtener información, vea la [lista de aplicaciones aprobadas para la administración de aplicaciones móviles](https://www.microsoft.com/cloud-platform/microsoft-intune-apps).
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
  - **Deshabilitar sincronización de contactos**: impide que la aplicación guarde los datos en la aplicación de contactos nativa del dispositivo.
  - **Deshabilitar la impresión**: impide que la aplicación imprima datos profesionales o educativos.
  <!-- 1324760 -->    

  Vea [Proteger aplicaciones mediante directivas de administración de aplicaciones móviles en System Center Configuration Manager](/sccm/mdm/deploy-use/protect-apps-using-mam-policies) para probar la nueva configuración de la directiva de protección de aplicaciones.

- **Compatibilidad con dispositivos Windows 10 (ARM64)**      
  Cuando los dispositivos ARM64 que ejecutan Windows 10 estén disponibles, admiten los escenarios híbridos de administración de dispositivos móviles (MDM). Para más información, vea [Compatibilidad con dispositivos Windows 10 (ARM64)](/sccm/core/plan-design/changes/whats-new-in-version-1710#windows-10-arm64-device-support).
  <!-- 1355000 -->    

- **Experiencia mejorada del perfil VPN en la consola de Configuration Manager**     
  Con esta versión, hemos actualizado las páginas de propiedades y el Asistente para perfiles VPN con el fin de mostrar una configuración más adecuada para la plataforma seleccionada. Esta característica estaba disponible anteriormente en Configuration Manager Technical Preview 1709. Ahora está disponible en implementaciones híbridas con Intune y la versión 1710 de Configuration Manager (Rama actual). Para más información, consulte [Experiencia mejorada del perfil VPN en la consola de Configuration Manager](/sccm/core/plan-design/changes/whats-new-in-version-1710#improved-vpn-profile-experience-in-configuration-manager-console).
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
  Se ha agregado compatibilidad con la autenticación basada en certificados (CBA) en la aplicación Portal de empresa para iOS. Los usuarios con CBA escriben su nombre de usuario y luego pulsan el vínculo “Iniciar sesión con un certificado”. CBA ya se admite en las aplicaciones del Portal de empresa de Android y Windows. Puede obtener más información en la página de [inicio de sesión en la aplicación del Portal de empresa](https://docs.microsoft.com/intune-user-help/sign-in-to-the-company-portal).
  <!--1029830-->   

- **Mejoras en el flujo de trabajo de configuración de dispositivos en Portal de empresa**     
  Se ha mejorado el flujo de trabajo de instalación de dispositivos en la aplicación del Portal de empresa para Android. El lenguaje resulta más fácil de usar y es específico de su empresa. Además, hemos combinado pantallas donde era posible. Puede ver estas mejoras en la página [Novedades de la interfaz de usuario de aplicaciones](https://docs.microsoft.com/intune/whats-new-app-ui#week-of-october-2-2017).
  <!--1490692-->     

- **Guía mejorada en torno a la solicitud de acceso a los contactos en dispositivos Android**     
  La aplicación del Portal de empresa para Android requiere a menudo que el usuario final acepte el permiso de contactos. Si un usuario final rechaza este acceso, verá una notificación en aplicación que debe concederlo para el acceso condicional de alertas. 
  <!--1484985-->     

- **Remedio para el inicio seguro en Android**     
  Los usuarios finales con dispositivos Windows podrán pulsar en la razón de no compatibilidad en la aplicación Portal de empresa. Cuando sea posible, esta acción les lleva directamente a la ubicación correcta en la aplicación de configuración para corregir el problema. 
  <!--1490712-->    

- **Notificaciones de inserción adicionales para usuarios finales en la aplicación Portal de empresa para Android Oreo**    
  Los usuarios finales ven notificaciones adicionales que indican cuando la aplicación Portal de empresa para Android Oreo realiza tareas en segundo plano, como recuperar directivas desde el servicio Intune. Las notificaciones aumentan la transparencia para los usuarios finales con respecto a cuándo el Portal de empresa realiza tareas administrativas en el dispositivo. Esta mejora es parte del total [optimización de la interfaz de usuario del Portal de empresa](https://blogs.technet.microsoft.com/intunesupport/2017/08/21/android-8-0-o-behaviour-changes-and-microsoft-intune) para la aplicación de Portal de empresa para Android Oreo. 
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
  La aplicación del Portal de empresa solo intenta inscribir los dispositivos Samsung Knox compatibles. Para evitar errores de activación de KNOX que impidan la inscripción de MDM, solo se intenta la inscripción de dispositivos si el dispositivo aparece en la [lista de dispositivos publicados por Samsung](https://www.samsungknox.com/knox-supported-devices/knox-workspace). Puede que algunos dispositivos Samsung tengan números de modelo que admitan KNOX y otros no. Compruebe la compatibilidad de Knox con su revendedor de dispositivos antes de su compra e implementación. Puede encontrar la lista completa de dispositivos comprobados en la [configuración de directivas de Android y Samsung KNOX Standard](https://docs.microsoft.com/intune-classic/deploy-use/android-policy-settings-in-microsoft-intune#supported-samsung-knox-standard-devices).
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
    Hemos agregado **el tipo de propiedad** en la pantalla de detalles del dispositivo en la aplicación de Portal de empresa para iOS. Esta información permitirá que los usuarios obtengan más información sobre la privacidad directamente en los documentos para el usuario final de Intune. También se puede encontrar esta información en la pantalla Acerca de. 
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



## <a name="notices"></a>Notificaciones

### <a name="update-your-android-company-portal-app-to-the-latest-version"></a>Actualice la aplicación de Portal de empresa Android a la versión más reciente

<!-- 4536963 -->

Intune periódicamente publica actualizaciones a la aplicación de Portal de empresa Android. En noviembre de 2018, hemos lanzado una actualización de Portal de empresa que incluye un modificador de back-end para prepararse para cambios de Google desde su plataforma de notificación existente en Google Firebase Cloud Messaging (FCM). Cuando Google retira de su plataforma de notificación existente y mueve a FCM, los usuarios deben actualizar su aplicación de Portal de empresa para al menos la versión de noviembre de 2018 para continuar la comunicación con el Store de Google Play.

#### <a name="how-does-this-change-affect-me"></a>¿Cómo me afecta este cambio?

Nuestros datos indican que existen los inquilinos que tienen dispositivos con una versión anterior a 5.0.4269.0 de Portal de empresa. Si esta versión (o posterior) del Portal de empresa no está instalada la aplicación, las acciones iniciadas por el Administrador de dispositivos no funcionen según lo previsto. Estas acciones incluyen la eliminación, restablecimiento de contraseña, instalaciones de aplicaciones disponibles y necesarios y la inscripción de certificados.

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>¿Qué debo hacer para prepararme para este cambio?

Pida a los usuarios de dispositivos Android que no ha actualizado la versión del Portal de empresa para actualizarlo a través de Google Play. Notificar el soporte técnico en caso de que un usuario no ha mantienen actualización automática la aplicación de Portal de empresa. Para obtener más información acerca de la plataforma FCM y el cambio de Google, consulte [Firebase Cloud Messaging](https://firebase.google.com/docs/cloud-messaging/).


### <a name="plan-for-change-intune-supports-macos-1012-and-higher-in-december"></a>Plan de cambio: Intune admite macOS 10.12 y superior en diciembre

<!--2970975-->  

Como Apple ha lanzado macOS 10.14, a partir del mes de diciembre de 2018, Intune será compatible con macOS 10.12 y versiones posteriores. 

#### <a name="how-does-this-affect-me"></a>¿Cómo me afecta esto ahora?

A partir de diciembre, los usuarios que tienen dispositivos con macOS 10.11 y versiones anteriores no podrán usar la aplicación Portal de empresa para inscribirse en Intune. Para seguir obteniendo soporte técnico y recibiendo nuevas características, deberán actualizar el dispositivo a macOS 10.12 o a versiones posteriores y actualizar la aplicación Portal de empresa a la versión más reciente. 

Actualmente, la versión 10.12 de macOS y las versiones posteriores son compatibles con: 
- MacBook (finales de 2009 o versiones posteriores)  
- iMac (finales de 2009 o versiones posteriores)
- MacBook (finales de 2010 o versiones posteriores)  
- MacBook Pro (finales de 2010 o versiones posteriores)  
- Mac Mini (finales de 2010 o versiones posteriores)  
- Mac Pro (finales de 2010 o versiones posteriores)  

A partir de diciembre, los usuarios finales que tengan dispositivos distintos de los mencionados anteriormente no podrán acceder a la versión más reciente de la aplicación Portal de empresa para macOS. Puede seguir administrando los dispositivos ya inscritos que ejecuten versiones no admitidas anteriores a macOS 10.12.

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>¿Qué debo hacer para prepararme para este cambio?

- Solicite a los usuarios que actualicen sus dispositivos a una versión del sistema operativo compatible antes de diciembre de 2018.  
- Compruebe los informes de Intune en Azure Portal para ver qué dispositivos o usuarios pueden verse afectados. Vaya a **Dispositivos** > **Todos los dispositivos** y filtre por **sistema operativo**. Puede agregar columnas adicionales para identificar más fácilmente qué usuarios de su organización tienen dispositivos que ejecutan macOS 10.11.  
- Si usa la administración híbrida de dispositivos móviles (MDM), en la consola de Configuration Manager, vaya al área de trabajo **Activos y compatibilidad** y haga clic en el nodo **Dispositivos**. Haga clic con el botón derecho en las columnas para agregar las columnas **Sistema operativo** y **Versión del cliente**. Después ordene por versión del sistema operativo. Tenga en cuenta que la MDM híbrida está en desuso y que debe cambiar a Intune en Azure tan pronto como sea posible. 
 
#### <a name="additional-information"></a>Información adicional
Para más información, vea [Inscribir un dispositivo macOS en Intune con la aplicación Portal de empresa](https://docs.microsoft.com/intune-user-help/enroll-your-device-in-intune-macos-cp).


### <a name="plan-for-change-use-intune-on-azure-now-for-your-mdm-management"></a>Plan de cambio: Use Intune en Azure ahora para la administración de MDM 
<!--1227338-->  
Hace más de un año, anunciamos [versión preliminar pública de Intune en Azure](https://cloudblogs.microsoft.com/enterprisemobility/2016/12/07/public-preview-of-intune-on-azure/) y se hace con seis meses seguimos [disponibilidad general de la nueva experiencia de administración](https://cloudblogs.microsoft.com/enterprisemobility/2017/06/08/the-new-intune-and-conditional-access-admin-consoles-are-ga/) para Intune. A partir del 31 de agosto de 2018, se desactivará la administración de dispositivos móviles (MDM) en la consola de Silverlight clásica para los clientes que usan Intune independiente. En su lugar, use [Intune en Azure](https://aka.ms/Intune_on_Azure) para sus necesidades de MDM. Si aún usa la consola clásica para MDM, deje de hacerlo y familiarícese con Intune en Azure. No se espera que este cambio afecte a los usuarios finales. La administración clásica de PC con Intune sigue estando disponible en Silverlight. Para más información, vea la [entrada del blog del equipo de soporte técnico de Intune](https://aka.ms/Intune_on_Azure_mdm).


### <a name="plan-for-change-upcoming-macos-and-intune-password-enforcement-change"></a>Plan de cambio: Próximas macOS y cambio de cumplimiento de contraseña de Intune
<!--1873216-->  
En la versión del servicio de septiembre, Intune planea integrar Apple recién publicado "Cambiar contraseña en el siguiente Auth" configuración para dispositivos que ejecutan macOS 10.13 versiones y versiones posteriores. Antes de que esta configuración se introdujese, los proveedores de MDM no tenían ninguna manera de comprobar que el código de acceso en un dispositivo se había cambiado para garantizar el cumplimiento. Las directivas de configuración y cumplimiento de Intune solo comprobaban que la próxima vez que una contraseña se cambiaba en el dispositivo, se marcaría como compatible. Los usuarios de macOS recibirán una solicitud para actualizar su contraseña cuando se integre esta nueva característica de Apple, incluso si su contraseña ya es compatible.

#### <a name="how-does-this-change-affect-me"></a>¿Cómo me afecta este cambio?
Este cambio solo afecta a los clientes de Intune independiente o MDM híbrida con una directiva de dispositivos macOS. Apple ha introducido la configuración Cambiar la contraseña en la nueva autenticación. Ahora Intune puede forzar a los usuarios a actualizar su contraseña a una que sea conforme al insertar una directiva de contraseñas. Si bloquea los recursos de empresa hasta que el dispositivo se marque como compatible, debe tener en cuenta que los usuarios finales pueden tener bloqueado su acceso a recursos corporativos, como correo electrónico o los sitios de SharePoint hasta que restablezcan su contraseña. En el futuro, todas las actualizaciones de las directivas de contraseñas de configuración y cumplimiento obligarán a los usuarios de destino a actualizar sus contraseñas.

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>¿Qué debo hacer para prepararme para este cambio?
Es posible que quiera informar a su departamento de soporte técnico. Si no quiere aplicar esta directiva de dispositivo macOS, desasigne o elimine la directiva de macOS existente. Nuestra investigación de cliente antes de implementar este cambio demuestra que la que mayoría de los clientes no se verán afectados por este cambio. Normalmente, los usuarios finales actualizan su contraseña después de recibir una solicitud para inscribirse con una contraseña o restablecer su contraseña para mantener la conformidad.  


### <a name="plan-for-change-intune-moving-to-support-ios-10-and-later-in-september-2018"></a>Plan de cambio: Mover a la compatibilidad con iOS 10 y versiones posteriores en septiembre de 2018 de Intune 
<!--2454656-->  

En septiembre de 2018, se espera que Apple publique iOS 12. Poco después del lanzamiento, actualizaremos la inscripción de Intune, el Portal de empresa y el explorador administrado para que sean compatibles con iOS 10 y posteriores.

#### <a name="how-does-this-change-affect-me"></a>¿Cómo me afecta este cambio?

Las aplicaciones móviles de Office 365 son compatibles con iOS 10 y versiones posteriores, por lo que es posible que ya haya actualizado su sistema operativo o sus dispositivos. Si es así, esta acción no le afectará.

En cambio, si tiene alguno de los siguientes dispositivos, o bien si quiere inscribir cualquiera de los dispositivos que se enumeran a continuación, solo admiten iOS 9 y versiones anteriores. Para seguir accediendo al Portal de empresa de Intune, debe actualizar estos dispositivos antes de septiembre a dispositivos que admitan iOS 10 o versiones posteriores: 

- iPhone 4S
- iPod Touch 
- iPad 2
- iPad (3ª generación)
- iPad Mini (1ª generación)

A partir de julio, los dispositivos inscritos en MDM con iOS 9 y el Portal de empresa recibirán una notificación para actualizar su SO o dispositivo. Si usa directivas de protección de aplicaciones, también puede establecer el parámetro de acceso "Requerir sistema operativo iOS mínimo (solo es una advertencia)".  

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>¿Qué debo hacer para prepararme para este cambio?

Busque los dispositivos o usuarios que se vean afectados en la organización. En Intune en Azure Portal, vaya a **Dispositivos** > **Todos los dispositivos** y filtre por **SO**.  Haga clic en **Columnas** para ver detalles como la versión del SO. Solicite a los usuarios que actualicen sus dispositivos a una versión del sistema operativo compatible antes de septiembre.


### <a name="company-portal-for-windows-81-and-windows-phone-81-moving-to-sustaining-mode"></a>El Portal de empresa para Windows 8.1 y Windows Phone 8.1 se mueve al modo de mantenimiento 
<!--1428681-->  
*6 de octubre de 2017*   
 
A partir de octubre de 2017, las aplicaciones Portal de empresa para Windows 8.1 y Windows Phone 8.1 pasan al modo de mantenimiento. Este modo significa que las aplicaciones y los escenarios existentes, como inscripción y cumplimiento, se seguirán admitiendo en estas plataformas. Estas aplicaciones se pueden seguir descargando en los canales de lanzamiento existentes, como Microsoft Store. 

Una vez en el modo de mantenimiento, estas aplicaciones solo reciben actualizaciones de seguridad críticas. No habrá actualizaciones adicionales ni características para ellas. En el caso de nuevas características, se recomienda actualizar los dispositivos a Windows 10 o Windows 10 Mobile. 

### <a name="end-of-support-for-ios-80"></a>Finalización del soporte de iOS 8.0 
<!---1164477--->  
Las aplicaciones administradas y la aplicación Portal de empresa para iOS necesitan iOS 9.0 y posterior para poder acceder a los recursos de la empresa. Los dispositivos que no estén actualizados antes de septiembre ya no podrán acceder a Portal de empresa ni a esas aplicaciones. 

### <a name="platform-support-reminder-windows-phone-81-mainstream-support-ended-july-11-2017"></a>Recordatorio de compatibilidad de plataforma: Soporte técnico de Windows Phone 8.1 finalizó el 11 de julio de 2017
<!-- 1327781 -->  
*11 de julio de 2017*

La plataforma Windows Phone 8.1 ha llegado a la finalización del soporte técnico estándar. El soporte técnico para equipos con Windows 8.1 no se verá afectado.

Esto no afecta inmediatamente a ningún dispositivo Windows Phone 8.1 administrado por el servicio de Intune, incluidos los dispositivos inscritos en entornos híbridos MDM. Los dispositivos que están inscritos seguirán funcionando. Todas las directivas, configuraciones y aplicaciones siguen funcionando como se espera. Tenga en cuenta que no hay mejoras previstas para la plataforma Windows Phone 8.1 en el servicio de Intune ni para la aplicación Portal de empresa de Windows Phone 8.1.

Se recomienda actualizar los dispositivos Windows Phone 8.1 aptos a Windows 10 Mobile lo antes posible.  

### <a name="end-of-support-for-android-43-and-lower"></a>Finalización del soporte para Android 4.3 y versiones inferiores
<!---1171127--->  
*6 de julio de 2017*

Las aplicaciones administradas y la aplicación Portal de empresa para Android necesitan Android 4.4 y posterior para poder acceder a los recursos de la empresa. Los dispositivos que no estén actualizados antes de principios de octubre ya no pueden acceder a Portal de empresa ni a esas aplicaciones. En diciembre, se forzará la retirada de todos los dispositivos inscritos, con lo que ya podrán acceder a los recursos de la empresa. Si está usando directivas de protección de aplicaciones sin MDM, las aplicaciones no recibirán actualizaciones y la calidad de la experiencia se irá reduciendo con el paso del tiempo.



## <a name="see-also"></a>Vea también

- [Notificaciones y características híbridas anteriores de MDM](whats-new-hybrid-archive.md)
- [Novedades de MDM en System Center 2012 Configuration Manager](https://technet.microsoft.com/library/mt445560.aspx)
