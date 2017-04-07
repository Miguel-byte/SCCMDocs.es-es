---
title: "Creación de elementos de configuración para dispositivos iOS y Mac OS X administrados con Intune | Microsoft Docs"
description: "Use el elemento de configuración de iOS y Mac OS X de System Center Configuration Manager para administrar la configuración de los dispositivos iOS y Mac OS X."
ms.custom: na
ms.date: 03/28/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 613a48ac-c55d-4c4a-94ea-d3747a1b10cb
caps.latest.revision: 15
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: 6e2cb628217598480973d4f728a9e0a7cd5873e7
ms.lasthandoff: 03/27/2017


---
# <a name="how-to-create-configuration-items-for-ios-and-mac-os-x-devices-managed-with-intune"></a>Creación de elementos de configuración para dispositivos iOS y Mac OS X administrados con Intune
Use el elemento de configuración de **iOS y Mac OS X** de System Center Configuration Manager para administrar la configuración de los dispositivos iOS y Mac OS X inscritos en Microsoft Intune o que administra System Center Configuration Manager de forma local.  
  
### <a name="to-create-an-ios-and-mac-os-x-configuration-item"></a>Cómo crear un elemento de configuración de iOS y Mac OS X  
  
1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad**.  
  
2.  En el área de trabajo **Activos y compatibilidad** , expanda **Configuración de cumplimiento**y, a continuación, haga clic en **Elementos de configuración**.  
  
3.  En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear elemento de configuración**.  
  
4.  En la página **General** del **Asistente para crear elemento de configuración**, escriba un nombre y, opcionalmente, una descripción para el elemento de configuración.  
  
5.  En **Especifique el tipo de elemento de configuración que desea crear**, seleccione **iOS y Mac OS X**.  
  
6.  Haga clic en **Categorías** si crea y asigna categorías para ayudarle a buscar y filtrar elementos de configuración en la consola de Configuration Manager.  
  
7.  En la página **Plataformas admitidas** del asistente, seleccione las plataformas de iOS o Mac OS X concretas que evaluarán el elemento de configuración.  
  
8.  En la página **Configuración del dispositivo** del asistente, seleccione el grupo de configuración que quiere configurar. Vea [Referencia de configuración de elementos de configuración de iOS y Mac OS X](#BKMK_Setref) en este tema para obtener detalles y luego haga clic en **Siguiente**.  
  
    > [!TIP]  
    >  Si el valor que quiere no aparece, seleccione la casilla **Configurar opciones adicionales que no se encuentran en los grupos de configuración predeterminados**.  
  
9. En cada página de configuración, configure las opciones que necesita y si quiere corregirlas cuando no sean conformes en dispositivos (si se admite).  
  
10. Para cada grupo de configuración, también puede elegir la gravedad que se notificará cuando se encuentre que un elemento de configuración no es conforme entre las siguientes:  
  
    -   **Ninguno**: los dispositivos que no cumplan esta regla de compatibilidad no notificarán ninguna gravedad de error en los informes de Configuration Manager.  
  
    -   **Información**: los dispositivos que no cumplan esta regla de compatibilidad notificarán una gravedad de error de **Información** en los informes de Configuration Manager.  
  
    -   **Advertencia**: los dispositivos que no cumplan esta regla de compatibilidad notificarán una gravedad de error de **Advertencia** en los informes de Configuration Manager.  
  
    -   **Crítico**: los dispositivos que no cumplan esta regla de compatibilidad notificarán una gravedad de error de **Crítico** en los informes de Configuration Manager.  
  
    -   **Crítico con evento**: los dispositivos que no cumplan esta regla de compatibilidad notificarán una gravedad de error de **Crítico** en los informes de Configuration Manager. Este nivel de gravedad también se registra como evento de Windows en el registro de eventos de la aplicación.  
  
11. En la página **Aplicabilidad de plataforma** del asistente, revise cualquier configuración que no sea conforme a las plataformas admitidas que seleccionó anteriormente. Puede regresar y eliminar esta configuración o puede continuar.  
  
    > [!TIP]  
    >  No se evalúa el cumplimiento de la configuración no admitida.  
  
12. Complete el asistente.  
  
 Puede ver el nuevo elemento de configuración en el nodo **Elementos de configuración** del área de trabajo **Activos y compatibilidad** .  
  
##  <a name="ios-and-mac-os-x-configuration-item-settings-reference"></a>Referencia de configuración de elementos de configuración de iOS y Mac OS X  
  
###  <a name="password"></a>Contraseña  
  
|Nombre de la configuración|Detalles|  
|------------------|-------------|  
|**Requerir configuración de contraseña en dispositivos móviles**|Se requiere una contraseña en dispositivos compatibles.|  
|**Longitud de contraseña mínima (caracteres)**|La longitud mínima de la contraseña.|  
|**Caducidad de la contraseña en días**|El número de días antes de que se deba cambiar una contraseña.|  
|**Número de contraseñas recordadas**|Impide que se vuelvan a usar contraseñas ya utilizadas.|  
|**Número de intentos de inicio de sesión incorrectos antes de que se borre el dispositivo**|Borra el dispositivo si hay un error en este número de intentos de inicio de sesión.<br /><br /> (Solo iOS)|  
|**Complejidad de la contraseña**|Elija si se puede especificar un PIN como "1234" o si se debe proporcionar una contraseña segura.| 
|**Permitir contraseñas sencillas**|Permitir contraseñas sencillas como **0000** y **1234**.|
|**Desbloquear mediante huella digital**|Permite desbloquea el dispositivo mediante el uso de una huella digital.|
|**Modificación del código de acceso** (solo supervisado)|Permitir la adición, modificación o eliminación de la contraseña del dispositivo.|
  
###  <a name="device"></a>Dispositivo  
 Esta configuración se aplica a dispositivos iOS y Mac OS X.  
  
|Nombre de la configuración|Detalles|  
|------------------|-------------|  
|**Agregar amigos de centro de juegos**|Permite agregar amigos en la aplicación Centro de juegos.|
|**Marcación por voz**|Permite el uso de la característica de marcación por voz en el dispositivo.|  
|**Asistente de voz**|Permite el uso de una aplicación de asistente de voz como Siri.|  
|**Asistente de voz durante un bloqueo**|Permite el uso de una aplicación de asistente de voz como Siri cuando el dispositivo está bloqueado.|  
|**Captura de pantalla**|Permite obtener una captura de pantalla del dispositivo.|  
|**Cliente de chat de vídeo**|Permite el uso de aplicaciones de videollamada como Facetime.|  
|**Juego multijugador**|Permite jugar con otros jugadores en Internet.|  
|**Software de cartera personal durante un bloqueo**|Permite el uso de software de cartera personal como la libreta.|  
|**Envío de datos de diagnóstico**|Permite el envío de archivos de registro de aplicación.|  
|**Notificaciones del centro de actividades**|Permite al usuario acceder a la vista de notificaciones sin que sea necesario desbloquear el dispositivo.|
|**Apple Music** (solo supervisado)|Permite el uso de la aplicación Apple Music.|
|**Podcasts** (solo supervisado)|Permite el uso de la aplicación Podcasts.|
|**Aplicación Mensajes** (solo supervisado)|Permite el uso de la aplicación Mensajes para enviar mensajes de texto.|
|**Modificación del fondo de pantalla** (solo supervisado)|Permite al usuario modificar el fondo de pantalla del dispositivo.|
|**Búsqueda de definiciones de palabras** (solo supervisado)|Habilita la característica de iOS que permite resaltar una palabra y buscar su definición.|
|**Detección de muñeca para Apple Watch enlazados**|Cuando se habilita, Apple Watch no mostrará notificaciones si no está agotado.|
|**Filtro de obscenidad de Siri** (solo supervisado)|Impide que Siri dicte o hable un lenguaje obsceno.|
|**Modificación del nombre de dispositivo** (solo supervisado)|Permite al usuario modificar el nombre del dispositivo.|
|**Modificación de la configuración del envío de diagnósticos** (solo supervisado)|Permite o bloquea el dispositivo para enviar datos de diagnóstico a Apple.|
|**Game Center** (solo supervisado)|Permite el uso de la aplicación Game Center.|
|**iTunes Radio** (solo supervisado)|Permite el uso de la aplicación iTunes Radio.|
|**Apple News** (solo supervisado)|Permite el uso de la aplicación Apple News.|
|**Enlace con Apple Watch** (solo supervisado)|Permite que el dispositivo se enlace con Apple Watch.|
|**Corrección automática** (solo supervisado)|Permite que el dispositivo corrija automáticamente las palabras mal escritas.|
|**Modificación de Bluetooth** (solo supervisado)|Permite al usuario cambiar la configuración de Bluetooth en el dispositivo.|
|**Cambios en la configuración de uso de datos móviles de la aplicación** (solo supervisado)|Permite al usuario controlar qué aplicaciones pueden utilizar datos móviles.|
|**Métodos abreviados de teclado** (solo supervisado)|Permite el uso de métodos abreviados de teclado.|
|**Teclados predictivos** (solo supervisado)|Permite el uso de teclados predictivos que sugieren palabras que el usuario podría desear.|
|**Revisión ortográfica de teclado** (solo supervisado)|Permite el corrector ortográfico de dispositivo.|
|**Modificación de la configuración de notificación** (solo supervisado)|Permite al usuario modificar la configuración de notificación del dispositivo.|
|**Devolver resultados de Internet en búsquedas de Spotlight** (solo supervisado)|Permite que la búsqueda de Spotlight se conecte a Internet para proporcionar más resultados.|
|**Usar Siri para consultar el contenido generado por el usuario de Internet** (solo supervisado)|Permite que Siri acceda a sitios web para responder preguntas.|

  
###  <a name="store"></a>Tienda  
 Esta configuración se aplica solo a los dispositivos iOS.  
  
|Nombre de la configuración|Detalles|  
|------------------|-------------|  
|**Tienda de aplicaciones**|Permite el acceso a la tienda de aplicaciones en el dispositivo.|  
|**Escribir una contraseña para obtener acceso a la tienda de aplicaciones**|Los usuarios deben escribir una contraseña para obtener acceso a la tienda de aplicaciones.|  
|**Compras desde la aplicación**|Permite a los usuarios realizar compras desde la aplicación.|
|**Instalación de aplicaciones solo con Apple Configurator e iTunes** (solo supervisado)|Habilita o deshabilita la Tienda de aplicaciones desde la pantalla principal del dispositivo. Los usuarios todavía pueden usar iTunes o la herramienta Apple Configurator para instalar y actualizar aplicaciones.|
|**Acceso a la tienda de iBooks** (solo supervisado)|Permite al usuario examinar y comprar libros desde la tienda de iBooks.|
|**Descargas de aplicaciones automáticas** (solo supervisado)|Permite a las aplicaciones descargadas en otros dispositivos descargarse automáticamente en este dispositivo. Esta configuración no afecta a las actualizaciones de la aplicación.|

  
###  <a name="browser"></a>Explorador  
 Esta configuración se aplica solo a los dispositivos iOS.  
  
|Nombre de la configuración|Detalles|  
|------------------|-------------|  
|**Explorador predeterminado**|El usuario puede cambiar el explorador de Internet predeterminado.|  
|**Autorrellenar**|El usuario puede cambiar la configuración de Autocompletar en el explorador.|  
|**Active scripting**|El explorador puede ejecutar scripts, como scripts de ActiveX.|  
|**Bloqueador de elementos emergentes**|Habilita o deshabilita el bloqueador de elementos emergentes del explorador.|  
|**Cookies**|Permite que las cookies se guarden en el dispositivo.|  
|**Advertencia de fraude**|Habilita o deshabilita las advertencias de posibles sitios web fraudulentos.|  
  
###  <a name="content-rating"></a>Clasificación de contenido  
 Esta configuración se aplica solo a los dispositivos iOS.  
  
|Nombre de la configuración|Detalles|  
|------------------|-------------|  
|**Contenido para adultos en tienda de medios**|Especifique si desea permitir el acceso a contenido para adultos desde la App Store.|  
|**Región de clasificación**|Especifica el país para el que desea aplicar las restricciones de clasificaciones.|  
|**Clasificación de película**|Especifique el valor máximo de clasificación de contenido de película que desea permitir.|  
|**Clasificación de programa de TV**|Especifique el valor máximo de clasificación de contenido de programa de TV que desea permitir.|  
|**Clasificación de aplicación**|Especifique el valor máximo de clasificación de contenido de aplicación que desea permitir.| 
|**Contenido marcado como "Erótico" de iBook Store** (solo supervisado)|Permite al usuario descargar libros con la categoría "Erótico".| 
  
> [!NOTE]  
>  Las clasificaciones que puede seleccionar variarán según la **Región de clasificación** seleccionada.  
  
###  <a name="cloud"></a>Nube  
 Esta configuración se aplica solo a los dispositivos iOS.  
  
|Nombre de la configuración|Detalles|  
|------------------|-------------|  
|**Copia de seguridad en nube**|Permita copias de seguridad en un servicio en la nube como iCloud.|  
|**Copia de seguridad cifrada**|Permita el cifrado de las copias de seguridad en un servicio en la nube.|  
|**Sincronización de documentos**|Permita la sincronización de documentos en un servicio en la nube.|  
|**Sincronización de fotos**|Permita la sincronización de fotos en un servicio en la nube.| 
|**Biblioteca de fotografías de iCloud**|Si se establece en **n**, deshabilita el uso de la Fototeca de iCloud que permite a los usuarios almacenar fotografías y vídeos en la nube. Todas las fotos no descargadas íntegramente de la Fototeca de iCloud en el dispositivo se eliminarán del dispositivo si se establece en **No**.|
|**Uso compartido de fotografías de iCloud**|Se establece en **No** para deshabilitar la foto compartida de iCloud en el dispositivo.|
|**Handoff para continuar las actividades en otro dispositivo**|Permite al usuario continuar el trabajo iniciado en un dispositivo iOS en otro dispositivo iOS o Mac OS.|
|**Sincronización de datos desde aplicaciones administradas en iCloud**|Permite a las aplicaciones administradas con Intune sincronizar datos con la cuenta de iCloud del usuario.|

  
###  <a name="security"></a>Seguridad  
 Esta configuración se aplica solo a los dispositivos iOS.  
  
|Nombre de la configuración|Detalles|  
|------------------|-------------|  
|**Cámara**|Permite el uso de la cámara del dispositivo.| 
|**Confiar en nuevos autores de aplicaciones empresariales**|Permite al usuario seleccionar aplicaciones de confianza no descargadas desde la tienda de aplicaciones.| 
  
###  <a name="roaming"></a>Movilidad  
 Esta configuración se aplica solo a los dispositivos iOS.  
  
|Nombre de la configuración|Detalles|  
|------------------|-------------|  
|**Itinerancia de voz**|Permite llamadas de voz en movilidad.|  
|**Sincronización automática en movilidad**|Permite que el dispositivo se sincronice automáticamente en movilidad.|  
|**Itinerancia de datos**|Permite movilidad entre redes al obtener acceso a datos.|  
  
###  <a name="system-security"></a>Seguridad del sistema  
 Esta configuración se aplica solo a los dispositivos iOS.  
  
|Nombre de la configuración|Detalles|  
|------------------|-------------|  
|**El usuario acepta certificados de TLS que no son de confianza**|Si **Permitido**, permite que el usuario acepte estos certificados. Si **Prohibido**, se rechazan automáticamente los certificados que no son de confianza.|
|**Permitir bloqueo de activación (solo modo supervisado)**|Utilice esta opción para habilitar el bloqueo de activación de iOS en los dispositivos iOS **supervisados** que administra. Para más información sobre el bloqueo de activación, vea [Administración del bloqueo de activación de iOS con System Center Configuration Manager](../../mdm/deploy-use/manage-ios-activation-lock.md).
|**Centro de control de pantalla de bloqueo**|Controla si se puede tener acceso a la aplicación de centro de control cuando el dispositivo está bloqueado.|  
|**Vista de notificación de pantalla de bloqueo**|Controla si se pueden ver notificaciones cuando el dispositivo está bloqueado.|  
|**Vista Hoy de pantalla de bloqueo**|Controla si se puede ver la vista Hoy cuando el dispositivo está bloqueado.|  
|**Modificar configuración de cuenta** (solo supervisado)|Permite al usuario cambiar la configuración de la cuenta, como los ajustes del correo electrónico.|
|**Hacer cambios en la configuración de la aplicación Buscar a mis amigos** (solo supervisado)|Permite al usuario cambiar la configuración de la aplicación Encontrar más amigos.|
|**Usar el emparejamiento de host para controlar los dispositivos con los que se puede emparejar un dispositivo iOS** (solo supervisado)|Permite el emparejamiento de host para que el administrador pueda controlar con qué dispositivos puede emparejarse un dispositivo iOS.|
|**Borrar todo el contenido y la configuración** (solo supervisado)|Permite al usuario usar la opción de borrar todo el contenido y la configuración del dispositivo.|
|**Configurar restricciones en el dispositivo** (solo supervisado)|Permite al usuario configurar restricciones de dispositivos (controles parentales) en el dispositivo.|
|**Instalar certificados y perfiles de configuración** (solo supervisado)|Permite al usuario instalar certificados y perfiles de configuración.|
|**Contraseña para las solicitudes salientes de AirPlay**|Requiere una contraseña de emparejamiento cuando el usuario utiliza AirPlay para transmitir contenido a otros dispositivos de Apple.|
  
###  <a name="data-protection"></a>Protección de datos  
 Esta configuración se aplica solo a los dispositivos iOS.  
  
|Nombre de la configuración|Detalles|  
|------------------|-------------|  
|**Abrir documentos en aplicaciones administradas en otras aplicaciones no administradas**|Para su uso con aplicaciones administradas por parte de las directivas de administración de aplicaciones de Configuration Manager.|  
|**Abrir documentos en aplicaciones no administradas en otras aplicaciones administradas**|Para su uso con aplicaciones administradas por parte de las directivas de administración de aplicaciones de Configuration Manager.| 
|**Tratar AirDrop como destino no administrado** (solo supervisado)|Las aplicaciones administradas dejan de poder enviar datos a través de Airdrop.|
|**AirDrop** (solo supervisado)|Permitir el uso de la característica AirDrop para intercambiar el contenido con dispositivos cercanos.|
  
###  <a name="compliant-and-noncompliant-apps-ios"></a>Aplicaciones compatibles y no compatibles (iOS)  
 Permite especificar una lista de las aplicaciones compatibles y de las no compatibles de iOS en su empresa. A continuación, puede usar informes para mostrar los dispositivos que tienen instaladas aplicaciones no compatibles y el usuario asociado.  
  
 No puede especificar aplicaciones compatibles y no compatibles en el mismo elemento de configuración.  
  
#### <a name="to-specify-the-compliant-or-noncompliant-apps-list"></a>Para especificar la lista de aplicaciones compatibles o no compatibles  
  
1.  En la página **Aplicaciones compatibles y no compatibles (iOS)** , especifique la siguiente información:  
  
    -   **Lista de aplicaciones no conformes**: seleccione esta opción si desea especificar una lista de aplicaciones que se notificarán como no compatibles si los usuarios las instalan.  
  
    -   **Lista de aplicaciones compatibles**: seleccione esta opción si desea especificar una lista de aplicaciones que los usuarios pueden instalar. Cualquier otra aplicación instalada se notificará como no compatible.  
  
    -   **Agregar**: agrega una aplicación a la lista seleccionada. Especifique un nombre de su elección, opcionalmente el editor de la aplicación y la dirección URL de la aplicación en la tienda de aplicaciones.  
  
         Para especificar la dirección URL, en iTunes App Store, busque la aplicación que desea usar.  
  
         Abra la página de la aplicación y copie la dirección URL en el Portapapeles. Ya puede utilizarla como dirección URL en una la lista de aplicaciones conformes o no conformes.  
  
         **Ejemplo:** busque la aplicación **Microsoft Word para iPad** en la tienda. La dirección URL que utilice será **https://itunes.apple.com/es/app/microsoft-word-for-ipad/id586447913?mt=8**.  
  
    -   **Editar**: permite editar el nombre, el editor y la dirección URL de la aplicación seleccionada.  
  
    -   **Quitar**: elimina la aplicación seleccionada de la lista.  
  
    -   **Importar**: importa la lista de las aplicaciones que ha especificado en un archivo de valores separados por comas. Utilice el formato, nombre de la aplicación, editor, dirección URL de la aplicación en el archivo.  
  
2.  Cuando haya terminado haga clic en **Siguiente**.  
  
 Puede utilizar una de las siguientes aplicaciones compatibles y no compatibles de supervisión de informes:  
  
-   **Lista de aplicaciones y dispositivos no compatibles para un usuario específico** : muestra información sobre los usuarios y los dispositivos que tienen instaladas aplicaciones que no son compatibles con una directiva especificada.  
  
-   **Resumen de usuarios que tienen aplicaciones no compatibles** : muestra información sobre los usuarios que tienen instaladas aplicaciones que no son compatibles con una directiva especificada.  
  
 Para obtener más información sobre cómo usar los informes, consulte [Generación de informes en System Center Configuration Manager](../../core/servers/manage/reporting.md).  
  
###  <a name="compliant-and-noncompliant-apps-mac-os-x"></a>Aplicaciones compatibles y no compatibles (Mac OS X)  
 Permite especificar una lista de aplicaciones de Mac OS X que son compatibles o no compatibles en su empresa. A continuación, puede usar informes para mostrar los dispositivos que tienen instaladas aplicaciones no compatibles y el usuario asociado.  
  
 No puede especificar aplicaciones compatibles y no compatibles en el mismo elemento de configuración.  
  
#### <a name="to-specify-the-compliant-or-noncompliant-apps-list"></a>Para especificar la lista de aplicaciones compatibles o no compatibles  
  
1.  En la página **Aplicaciones compatibles y no compatibles (Mac OS X)** , especifique la siguiente información:  
  
    -   **Lista de aplicaciones no conformes**: seleccione esta opción si desea especificar una lista de aplicaciones que se notificarán como no compatibles si los usuarios las instalan.  
  
    -   **Lista de aplicaciones compatibles**: seleccione esta opción si desea especificar una lista de aplicaciones que los usuarios pueden instalar. Cualquier otra aplicación instalada se notificará como no compatible.  
  
    -   **Agregar**: agrega una aplicación a la lista seleccionada. Especifique un nombre de su elección (opcionalmente, el editor de la aplicación) y el identificador de paquete de la aplicación.  
  
        > [!TIP]  
        >  Para buscar el identificador de paquete de una aplicación, siga estos pasos en un equipo Mac que tenga la aplicación instalada:  
        >   
        >  1.  Abra la carpeta en la que está instalada la aplicación (por ejemplo, **/Applications**)  
        > 2.  Seleccione el paquete *<nombre de aplicación\>***.app** y elija **Mostrar contenido del paquete**  
        > 3.  Abra el archivo **Info.plist**  
        > 4.  Compruebe el valor asociado a la clave **CFBundleIdentifier**  
        >   
        >  El formato del identificador de paquete es **com.contoso.appname**  
  
    -   **Editar**: permite editar el nombre, el publicador y el identificador de paquete de la aplicación seleccionada.  
  
    -   **Quitar**: elimina la aplicación seleccionada de la lista.  
  
    -   **Importar**: importa la lista de las aplicaciones que ha especificado en un archivo de valores separados por comas. Use el formato, el nombre de la aplicación, el editor y el identificador de paquete de la aplicación en el archivo.  
  
2.  Cuando haya terminado haga clic en **Siguiente**.  
  
 Puede utilizar una de las siguientes aplicaciones compatibles y no compatibles de supervisión de informes:  
  
-   **Lista de aplicaciones y dispositivos no compatibles para un usuario específico** : muestra información sobre los usuarios y los dispositivos que tienen instaladas aplicaciones que no son compatibles con una directiva especificada.  
  
-   **Resumen de usuarios que tienen aplicaciones no compatibles** : muestra información sobre los usuarios que tienen instaladas aplicaciones que no son compatibles con una directiva especificada.  
  
 Para obtener más información sobre cómo usar los informes, consulte [Generación de informes en System Center Configuration Manager](../../core/servers/manage/reporting.md).  
  
### <a name="ios-and-mac-os-x-custom-profile-settings"></a>Configuración de perfiles personalizados de iOS y Mac OS X  
 Use los **Perfiles personalizados de iOS y Mac OS X** para implementar la configuración que creó mediante la [herramienta Apple Configurator](https://itunes.apple.com/us/app/apple-configurator-2/id1037126344?mt=12) en dispositivos iOS y Mac OS X. Esta herramienta permite crear muchas configuraciones para controlar el funcionamiento de estos dispositivos y exportarlas a un perfil de configuración. Después, puede importar este perfil de configuración en un perfil personalizado de iOS y Mac OS X e implementar la configuración para los usuarios y dispositivos de la organización.  
  
> [!NOTE]  
>  Asegúrese de que la configuración que exporta de la herramienta Apple Configurator sea compatible con la versión de iOS o Mac OS X en los dispositivos en los que implementa el perfil. Para obtener información sobre la resolución de las opciones de configuración incompatibles, busque la referencia de perfiles de configuración y la referencia del protocolo de administración de dispositivos móviles en el sitio web para [desarrolladores de Apple](https://developer.apple.com/) .  
  
#### <a name="to-create-an-ios-and-mac-os-x-custom-profile"></a>Cómo crear un perfil personalizado de iOS y Mac OS X  
  
1.  En la página **Configurar opciones de perfil personalizado de iOS y Mac OS X** del **Asistente para crear un elemento de configuración**, especifique la siguiente información:  
  
    -   **Nombre del perfil de configuración personalizado (que se muestra a los usuarios)**: especifique el nombre de la directiva que se mostrará en el dispositivo y en los informes de Configuration Manager.  
  
    -   **Importar**: elija un archivo que haya exportado desde la herramienta Apple Configurator.  
  
    -   **Detalles del perfil de configuración**: muestra el archivo ha importado.  
  
    -   **Corregir configuraciones no compatibles** -  
  
         Seleccione si desea corregir las opciones de configuración no compatibles (si se admiten).  
  
    -   **Gravedad de no compatibilidad para informes**: especifique el nivel de gravedad que indica si esta directiva de cumplimiento se evalúa como no compatible. Los niveles de gravedad disponibles son los siguientes:  
  
        > [!NOTE]  
        >  Cuando un dispositivo Mac OS X está en modo de suspensión, no se pueden entregar ni inventariar las directivas y los perfiles. Como resultado, la consola de Configuration Manager puede mostrar de forma temporal el estado Configuraciones de directivas con errores hasta que el dispositivo salga del modo de suspensión.  
  
        -   **Ninguno**: los dispositivos que no cumplan esta regla de compatibilidad no notificarán ninguna gravedad de error en los informes de Configuration Manager.  
  
        -   **Información**: los dispositivos que no cumplan esta regla de compatibilidad notificarán una gravedad de error de **Información** en los informes de Configuration Manager.  
  
        -   **Advertencia**: los dispositivos que no cumplan esta regla de compatibilidad notificarán una gravedad de error de **Advertencia** en los informes de Configuration Manager.  
  
        -   **Crítico**: los dispositivos que no cumplan esta regla de compatibilidad notificarán una gravedad de error de **Crítico** en los informes de Configuration Manager.  
  
        -   **Crítico con evento**: los dispositivos que no cumplan esta regla de compatibilidad notificarán una gravedad de error de **Crítico** en los informes de Configuration Manager. Este nivel de gravedad también se registra como evento de Windows en el registro de eventos de la aplicación.  
  
#### <a name="how-to-create-a-configuration-profile-file"></a>Cómo crear un archivo de perfil de configuración  
 Para crear el archivo del perfil de configuración usado por la directiva personalizada se pueden seguir dos procesos distintos:  
  
-   Exportar el archivo (con la extensión **.mobileconfig**) desde la herramienta Apple Configurator.  
  
-   Crear el archivo mediante el esquema apropiado de la [referencia principal de los perfiles de configuración de Apple](https://developer.apple.com/library/ios/featuredarticles/iPhoneConfigurationProfileRef/Introduction/Introduction.html).  
  
###  <a name="kiosk-mode-ios"></a>Modo de quiosco (iOS)  
 El modo de quiosco permite bloquear un dispositivo para permitir que solo funcionen determinadas características. Por ejemplo, puede permitir que un dispositivo ejecute solo una aplicación administrada que especifique, o puede deshabilitar los botones de volumen de un dispositivo. Esta configuración podría utilizarse para un modelo de demostración de un dispositivo o para un dispositivo que está dedicado a realizar solo una función, como un dispositivo de punto de venta.  
  
#### <a name="to-configure-kiosk-mode-for-ios-devices"></a>Cómo configurar el modo de quiosco de los dispositivos iOS  
  
1.  En la página **Configurar opciones de pantalla completa para dispositivos iOS** del **Asistente para crear un elemento de configuración**, especifique la siguiente información:  
  
    -   **Seleccionar aplicación**: seleccione la aplicación que podrá ejecutar cuando el dispositivo esté en pantalla completa. No se podrá ejecutar ninguna otra aplicación en el dispositivo. Elija de entre las siguientes opciones:  
  
        -   **Aplicación administrada** : haga clic en Examinar y, a continuación, seleccione una aplicación administrada.  
  
        -   **Aplicación de la Tienda** : especifique la dirección URL a una aplicación en la tienda de aplicaciones y, a continuación, haga clic en **Obtener id. de aplicación** para rellenar el campo **Id. de la aplicación** .  
  
         Para buscar la dirección URL de la aplicación:  
  
        -   Con la ayuda de un motor de búsqueda, busque la aplicación que desea usar en iTunes App Store y abra la página de la aplicación.  
  
        -   Copie la dirección URL de la página y úsela como dirección URL para especificar la aplicación que desea ejecutar en modo de pantalla completa.  
  
        -   **Ejemplo:** busque **Microsoft Word para iPad**. La dirección URL que utilice será **https://itunes.apple.com/es/app/microsoft-word-for-ipad/id586447913?mt=8**.  
  
    -   **Táctil**: habilita o deshabilita la pantalla táctil en el dispositivo.  
  
    -   **Rotación de pantalla**: habilita o deshabilita el cambio de orientación de la pantalla cuando el dispositivo gira.  
  
    -   **Botones de volumen**: habilita o deshabilita el uso de los botones de volumen en el dispositivo.  
  
    -   **Cambio de timbre**: habilita o deshabilita el conmutador de timbre (silencio) en el dispositivo.  
  
    -   **Botón de suspensión y reactivación de pantalla**: habilita o deshabilita el botón de reactivación de la suspensión de pantalla en el dispositivo.  
  
    -   **Bloqueo automático**: habilita o deshabilita el bloqueo automático del dispositivo.  
  
    -   **Audio mono**: habilita o deshabilita la configuración de accesibilidad **Audio mono**.  
  
    -   **VoiceOver**: habilita o deshabilita la opción de accesibilidad **VoiceOver**, que lee en voz alta el texto de la pantalla del dispositivo.  
  
    -   **Ajustes de VoiceOver**: habilita o deshabilita los ajustes de VoiceOver, que permiten ajustar la función VoiceOver (por ejemplo, la rapidez con la que se lee el texto en pantalla en voz alta).  
  
    -   **Zoom**: habilita o deshabilita la configuración de accesibilidad de **Zoom**, que permite usar un toque para hacer zoom en la pantalla del dispositivo.  
  
    -   **Ajustes de zoom**: habilita o deshabilita los ajustes de zoom que permiten ajustar la función de zoom.  
  
    -   **Invertir colores**: habilita o deshabilita la configuración de accesibilidad **Invertir colores**, que ajusta la pantalla para ayudar a los usuarios con discapacidades visuales.  
  
    -   **Ajustes de invertir colores**: habilita o deshabilita los ajustes de invertir colores que permiten ajustar la función de invertir colores.  
  
    -   **AssistiveTouch**: habilita o deshabilita la configuración de accesibilidad **AssistiveTouch** que ayuda a los usuarios a realizar gestos en pantalla que podrían resultarles difíciles.  
  
    -   **Ajustes de AssistiveTouch**: habilita o deshabilita los ajustes de la interacción táctil de asistencia que le permiten ajustar la función de interacción táctil de asistencia.  
  
    -   **Selección de voz**: habilita o deshabilita la configuración de accesibilidad **Reproducir selección** que lee en voz alta el texto que seleccione.  
  
    -   **Corregir configuraciones no compatibles**: seleccione esta opción si desea corregir las opciones de configuración no compatibles (si se admiten).  
  
    -   **Gravedad de no compatibilidad para informes**: especifique el nivel de gravedad que indica si esta directiva de cumplimiento se evalúa como no compatible. Los niveles de gravedad disponibles son:  
  
        -   **Ninguno**: los dispositivos que no cumplan esta regla de compatibilidad no notificarán ninguna gravedad de error en los informes de Configuration Manager.  
  
        -   **Información**: los dispositivos que no cumplan esta regla de compatibilidad notificarán una gravedad de error de **Información** en los informes de Configuration Manager.  
  
        -   **Advertencia**: los dispositivos que no cumplan esta regla de compatibilidad notificarán una gravedad de error de **Advertencia** en los informes de Configuration Manager.  
  
        -   **Crítico**: los dispositivos que no cumplan esta regla de compatibilidad notificarán una gravedad de error de **Crítico** en los informes de Configuration Manager.  
  
        -   **Crítico con evento**: los dispositivos que no cumplan esta regla de compatibilidad notificarán una gravedad de error de **Crítico** en los informes de Configuration Manager. Este nivel de gravedad también se registra como evento de Windows en el registro de eventos de la aplicación.  
  
## <a name="see-also"></a>Véase también  
 [Elementos de configuración para dispositivos administrados sin el cliente de System Center Configuration Manager](../../compliance/deploy-use/configuration-items-for-devices-managed-without-the-client.md)

