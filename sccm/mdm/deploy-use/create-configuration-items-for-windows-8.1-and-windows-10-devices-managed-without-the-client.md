---
title: "Creación de elementos de configuración para dispositivos Windows 8.1 y Windows 10 administrados con Intune | Microsoft Docs"
description: "Use el elemento de configuración de Windows 10 de System Center Configuration Manager para administrar la configuración de los equipos con Windows 10."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 23e1e4dc-623a-4521-ad04-ae9482927097
caps.latest.revision: 20
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: f75bac7887772119f30654fe15c16a8f993cad75
ms.contentlocale: es-es
ms.lasthandoff: 05/17/2017


---
# <a name="how-to-create-configuration-items-for-windows-81-and-windows-10-devices-managed-without-the-system-center-configuration-manager-client"></a>Cómo crear elementos de configuración para dispositivos de Windows 8.1 y Windows 10 administrados sin el cliente de System Center Configuration Manager
||  
|-|  
|Este artículo contiene información sobre la [nueva funcionalidad incluida en la versión 1602](https://technet.microsoft.com/library/mt622084.aspx) de la \(rama actual\) de System Center Configuration Manager. Para usar la nueva funcionalidad, debe [instalar la actualización 1602](https://technet.microsoft.com/library/mt607046.aspx). Si no ha actualizado a la versión más reciente de Configuration Manager, puede [descargar la documentación de la versión que use](https://gallery.technet.microsoft.com/Documentation-for-System-ea90eaf1) desde la Galería de TechNet.|  
  
 Use el elemento de configuración de **Windows 8.1 y Windows 10** de System Center Configuration Manager para administrar la configuración de los dispositivos Windows 8.1 y Windows 10 inscritos en Microsoft Intune o que administra System Center Configuration Manager de forma local.  
  
### <a name="to-create-a-windows-81-and-windows-10-configuration-item"></a>Cómo crear un elemento de configuración de Windows 8.1 y Windows 10  
  
1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad**.  
  
2.  En el área de trabajo **Activos y compatibilidad** , expanda **Configuración de cumplimiento**y, a continuación, haga clic en **Elementos de configuración**.  
  
3.  En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear elemento de configuración**.  
  
4.  En la página **General** del **Asistente para crear elemento de configuración**, escriba un nombre y, opcionalmente, una descripción para el elemento de configuración.  
  
5.  En **Especifique el tipo de elemento de configuración que quiere crear**, seleccione **Windows 8.1 y Windows 10**.  
  
6.  Haga clic en **Categorías** si crea y asigna categorías para ayudarle a buscar y filtrar elementos de configuración en la consola de Configuration Manager.  
  
7.  En la página **Plataformas admitidas** del asistente, seleccione las plataformas de Windows específicas que evaluarán el elemento de configuración.  
  
8.  En la página **Configuración del dispositivo** del asistente, seleccione el grupo de configuración que quiere configurar. Vea [Referencia a configuración de elemento de configuración de Windows 8.1 y Windows 10](#BKMK_Setref) en este tema para obtener detalles y luego haga clic en **Siguiente**.  
  
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
  
##  <a name="windows-81-and-windows-10-configuration-item-settings-reference"></a>Referencia a configuración de elemento de configuración de Windows 8.1 y Windows 10  
  
### <a name="password"></a>Contraseña  
 Esta configuración es solo para dispositivos con Windows 10, y versiones posteriores.  
  
|Configuración|Detalles|  
|-------------|-------------|  
|**Requerir configuración de contraseña en dispositivos**|Se requiere una contraseña en dispositivos compatibles.|  
|**Longitud de contraseña mínima (caracteres)**|La longitud mínima de la contraseña.|  
|**Caducidad de la contraseña en días**|El número de días antes de que se deba cambiar una contraseña.|  
|**Número de contraseñas recordadas**|Impide que se vuelvan a usar contraseñas ya utilizadas.|  
|**Número de intentos de inicio de sesión incorrectos antes de que se borre el dispositivo**|Borra el dispositivo si hay un error en este número de intentos de inicio de sesión.|  
|**Tiempo de inactividad antes de que se bloquee el dispositivo**|Especifique la cantidad de tiempo que un dispositivo puede estar inactivo (sin intervención del usuario) antes de bloquearse.|  
|**Complejidad de la contraseña**|Elija si se puede especificar un PIN como "1234" o si se debe proporcionar una contraseña segura.|  
|**Calidad de contraseña**|Seleccione el nivel requerido de complejidad de la contraseña y también si se pueden usar dispositivos biométricos.|  
|**Enviar NIP de recuperación de contraseña a Exchange Server**||  
  
###  <a name="device"></a>Dispositivo  
  
|Nombre de la configuración|Detalles|  
|------------------|-------------|  
|**Captura de pantalla**|Permite obtener una captura de pantalla del dispositivo.<br /><br /> (Solo Windows 10)|  
|**Envío de datos de diagnóstico**|Permite el envío de archivos de registro de aplicación.<br /><br /> (Solo Windows 8.1)|  
|**Envío de datos de diagnóstico (Windows 10)**|Permite el envío de archivos de registro de aplicación.<br /><br /> (Solo Windows 10)|  
|**Geolocalización**|Permite que el dispositivo use información de servicios de ubicación.<br /><br /> (Solo Windows 10)|  
|**Copiar y pegar**|Usa la función de copiar y pegar para transferir datos entre aplicaciones.<br /><br /> (Solo Windows 10)|
|**Restablecimiento de la configuración de fábrica**|Permite al usuario final restablecer el dispositivo a su configuración inicial.<br /><br /> (Solo Windows 10)|  
|**Bluetooth**|Permite el uso de la capacidad Bluetooth de los dispositivos.|  
|**Modo visible de Bluetooth**|Permite que otros dispositivos Bluetooth puedan detectar el dispositivo.<br /><br /> (Solo Windows 10)|  
|**Anuncios de Bluetooth**|Permitir el uso de anuncios de Bluetooth.<br /><br /> (Solo Windows 10)|  
|**Grabación de voz**|Permite el uso de las características de grabación de voz del dispositivo.<br /><br /> (Solo Windows 10)|
|**Cortana**|Permite usar el asistente de voz de Cortana.<br /><br /> (Solo Windows 10)|
|**Notificaciones del centro de actividades**|Habilita o deshabilita el panel de notificación de Windows 10. <br /><br /> (Solo Windows 10)|
  
### <a name="email-management"></a>Administración de correo electrónico  
 Esta configuración es solo para dispositivos con Windows 8.1 y Windows 10.  
  
|Configuración|Detalles|  
|-------------|-------------|  
|**Correo electrónico POP e IMAP**|Permite la conexión con cuentas de correo electrónico que usan los estándares POP e IMAP.|  
|**Tiempo máximo de conservación de correo electrónico**|Tiempo de conservación de correo electrónico antes de eliminarse del servidor.|  
|**Formatos de mensaje permitidos**|Especifique si los correos electrónicos de usuario pueden ser HTML o texto sin formato únicamente.|  
|**Tamaño máximo para correo electrónico de texto sin formato (descargado automáticamente)**|Controla el tamaño máximo del correo electrónico de texto sin formato cuando se descarga automáticamente.|  
|**Tamaño máximo para correo electrónico HTML (descargado automáticamente)**|Controla el tamaño máximo del correo electrónico HTML cuando se descarga automáticamente.|  
|**Tamaño máximo de datos adjuntos (descargados automáticamente)**|Configura el tamaño máximo del correo electrónico que se descargará automáticamente.|  
|**Sincronización de calendarios**|Permitir la sincronización de calendarios para el dispositivo.|  
|**Cuenta de correo electrónico personalizada**|Permite el uso de una cuenta que no sea de Microsoft en el dispositivo.|  
|**Hacer que la cuenta Microsoft sea opcional en la aplicación Windows Mail**|Configure esta opción para quitar el requisito de una cuenta de Microsoft en Windows Mail.|  
  
### <a name="store"></a>Tienda  
 Esta configuración es solo para dispositivos con Windows 10, y versiones posteriores.  
  
|Configuración|Detalles|  
|-------------|-------------|  
|**Tienda de aplicaciones**|Permite el acceso a la tienda de aplicaciones en el dispositivo.|  
|**Escribir una contraseña para obtener acceso a la tienda de aplicaciones**|Los usuarios deben escribir una contraseña para obtener acceso a la tienda de aplicaciones.|  
|**Compras desde la aplicación**|Permite a los usuarios realizar compras desde la aplicación.|  
  
### <a name="browser"></a>Explorador  
 Esta configuración es solo para dispositivos con Windows 8.1 y Windows 10.  
  
|Configuración|Detalles|  
|-------------|-------------|  
|**Permitir explorador web**|Permitir el uso del explorador web en el dispositivo.|  
|**Autorrellenar**|El usuario puede cambiar la configuración de Autocompletar en el explorador.|  
|**Active scripting**|El explorador puede ejecutar scripts, como scripts de ActiveX.|  
|**Complementos**|El usuario puede agregar complementos en Internet Explorer.|  
|**Bloqueador de elementos emergentes**|Habilita o deshabilita el bloqueador de elementos emergentes del explorador.|  
|**Cookies**|Permite que las cookies se guarden en el dispositivo.|  
|**Advertencia de fraude**|Habilita o deshabilita las advertencias de posibles sitios web fraudulentos.|  
  
###  <a name="internet-explorer"></a>Internet Explorer  
 Esta configuración es solo para dispositivos con Windows 8.1 y Windows 10.  
  
|Nombre de la configuración|Detalles|  
|------------------|-------------|  
|**Enviar siempre el encabezado No realizar seguimiento**|Impide que se envíe información de exploración a sitios de terceros.|  
|**Zona de seguridad de intranet**|Asignar un nivel de seguridad a la zona de seguridad de la intranet.|  
|**Nivel de seguridad para zona de Internet**|Configura el nivel de seguridad para la zona de Internet.|  
|**Nivel de seguridad para zona de intranet**|Configura el nivel de seguridad para la zona de intranet.|  
|**Nivel de seguridad para zona de sitios de confianza**|Configura el nivel de seguridad para la zona de sitios de confianza.|  
|**Nivel de seguridad para zona de sitios restringidos**|Configura el nivel de seguridad para la zona de sitios restringidos.|  
|**Espacios de nombres para la zona de intranet**|Configurar sitios web que se agregan o quitan en la zona de intranet.|  
|**Ir a un sitio de intranet por una entrada de una sola palabra**|Habilita o deshabilita la opción que permite a Internet Explorer ir automáticamente a un sitio de intranet si se escribe un nombre de sitio válido sin un HTTP anterior:|  
|**Opción de menú del modo de empresa**|Permite a los usuarios activar y desactivar el modo de empresa desde el menú **Herramientas** de Internet Explorer.|  
|**Ubicación del informe de registro (URL)**|Especifique una dirección URL donde se registrarán los sitios web visitados cuando el modo de empresa esté activo.|  
|**Ubicación de la lista de sitios de Modo de empresa (URL)**|Especifique la ubicación de la lista de sitios web que van a usar el modo de empresa cuando esté activo.|  
  
###  <a name="cloud"></a>Nube  
 Esta configuración es solo para dispositivos con Windows 8.1 y Windows 10.  
  
|Nombre de la configuración|Detalles|Windows 8.1|Windows 10|  
|------------------|-------------|-----------------|----------------|  
|**Sincronización de la configuración**|Permite la sincronización de configuraciones entre diferentes dispositivos.|Sí|Sí|  
|**Sincronización de credenciales**|Permite la sincronización de credenciales entre diferentes dispositivos.|Sí|Sí|  
|**Cuenta Microsoft**|Permite el uso de una cuenta Microsoft en el dispositivo.|Sí|Sí|  
|**Sincronización de configuraciones a través de conexión de uso medido**|Permite la sincronización de configuraciones cuando se mide la conexión a Internet.|Sí|Sí|  
  
###  <a name="security"></a>Seguridad  
  
|Nombre de la configuración|Detalles|  
|------------------|-------------|  
|**Instalación de archivos sin firmar**|Permite la carga de archivos sin firmar.<br /><br /> (Solo Windows 10)|  
|**Aplicaciones sin firmar**|Permite la carga de aplicaciones sin firmar.<br /><br /> (Solo Windows 10)|  
|**Mensajería SMS y MMS**|Permite mensajería SMS y MMS desde el dispositivo.<br /><br /> (Solo Windows 10)|  
|**Almacenamiento extraíble**|Permite el uso de almacenamiento extraíble, como una tarjeta SD en el dispositivo.<br /><br /> (Solo Windows 10)|  
|**Cámara**|Permite el uso de la cámara del dispositivo.<br /><br /> (Solo Windows 10)|  
|**Transmisión de datos en proximidad (NFC)**|Permite la comunicación mediante el uso de NFC en el dispositivo.<br /><br /> (Solo Windows 10)|  
|**Modo antirrobo**|Controla si el modo antirrobo de Windows 10 está habilitado.<br /><br /> (Solo Windows 10)|  
|**Permitir conexión USB**|Permite que los dispositivos se conecten a este dispositivo con una conexión USB.<br /><br /> (Solo Windows 10)|
|**Archivo de perfil**|Aprovisiona un perfil de VPN para dispositivos Windows RT.<br /><br /> (Solo Windows 8.1)|  
|**Nombre de perfil**|Aprovisiona un perfil de VPN para dispositivos Windows RT.<br /><br /> (Solo Windows 8.1)|  
|**Perfil para todos los usuarios**|Aprovisiona un perfil de VPN para dispositivos Windows RT.<br /><br /> (Solo Windows 8.1)|  
  
###  <a name="peak-synchronization"></a>Sincronización durante horas punta  
 Esta configuración es solo para dispositivos con Windows 10, y versiones posteriores.  
  
|Nombre de la configuración|Detalles|  
|------------------|-------------|  
|**Especifica las horas pico**|Configurar las horas punta de sincronización de dispositivos móviles.|  
|**Frecuencia de sincronización durante horas punta**|Configurar la frecuencia con que se realiza la sincronización durante las horas punta establecidas.|  
|**Frecuencia de sincronización fuera de horas punta**|Configurar la frecuencia con que se realiza la sincronización fuera de las horas punta establecidas.|  
  
###  <a name="roaming"></a>Movilidad  
  
|Nombre de la configuración|Detalles|  
|------------------|-------------|  
|**Administración de dispositivos en movilidad**|Permite que Configuration Manager administre el dispositivo cuando está en itinerancia.<br /><br /> (Solo Windows 10)|  
|**Descarga de software en movilidad**|Permite la descarga de software y aplicaciones cuando se está en movilidad.<br /><br /> (Solo Windows 10)|  
|**Descarga de correo electrónico en movilidad**|Permite descargas de correo electrónico en movilidad.<br /><br /> (Solo Windows 10)|  
|**Itinerancia de datos**|Permite movilidad entre redes al obtener acceso a datos.| 
|**VPN sobre móvil**|Permite al dispositivo acceder a conexiones VPN cuando se conecta a una red móvil.<br /><br /> (Solo Windows 10)|
|**Itinerancia de VPN sobre móvil**|Permite al dispositivo acceder a conexiones VPN en itinerancia en una red móvil.<br /><br /> (Solo Windows 10)| 
  
###  <a name="encryption"></a>Cifrado  
  
|Nombre de la configuración|Detalles|  
|------------------|-------------|  
|**Cifrado de tarjeta de almacenamiento**|Se requieren las tarjetas de almacenamiento utilizadas con el dispositivo que se va a cifrar.<br /><br /> (Solo Windows 10)|  
|**Cifrado de archivo en el dispositivo**|Requiere el cifrado de los archivos en el dispositivo.|  
|**Requerir firma de correo electrónico**|Requiere que los mensajes de correo electrónico se firmen antes de enviarlos.|  
|**Algoritmo de firma**|Seleccione el algoritmo de firma para los mensajes de correo electrónico firmados.|  
|**Requerir cifrado de correo electrónico**|Requiere que los mensajes de correo electrónico se cifren antes de enviarlos.|  
|**Algoritmo de cifrado**|Seleccione el algoritmo para cifrar los mensajes de correo electrónico.|  
  
###  <a name="wireless-communications"></a>Comunicaciones inalámbricas  
 Esta configuración es solo para dispositivos con Windows 10, y versiones posteriores.  
  
|Nombre de la configuración|Detalles|  
|------------------|-------------|  
|**Conexión de red inalámbrica**|Habilita o deshabilita la capacidad Wi-Fi de los dispositivos.|  
|**Tethering Wi-Fi**|Permite que los usuarios usen sus dispositivos como una zona con cobertura inalámbrica móvil.|  
|**Descargar datos con Wi-Fi cuando sea posible**|Configurar esta opción para utilizar la conexión Wi-Fi en el dispositivo cuando sea posible.|  
|**Informes de zonas Wi-Fi**||  
|**Configuración manual de Wi-Fi**||  
  
#### <a name="to-configure-a-wireless-network-connection"></a>Para configurar una conexión de red inalámbrica  
  
1.  En la página **Configure las opciones de comunicación inalámbrica de dispositivo móvil** , haga clic en **Agregar**.  
  
2.  En el cuadro de diálogo **Conexión de red inalámbrica** , especifique la siguiente información sobre la conexión inalámbrica que se aprovisionará en dispositivos móviles:  
  
|Configuración|Más información|  
|-------------|----------------------|  
|**Nombre de red (SSID)**|Escribir el nombre de la red Wi-Fi.|  
|**Conexión de red**|Elija **Internet** o **Trabajo**.|  
|**Autenticación**|Elija el método de autenticación para la conexión inalámbrica desde:<br /><br /> - **Abierto**<br /><br /> - **Compartido**<br /><br /> - **WPA**<br /><br /> - **WPA-PSK**<br /><br /> - **WPA2**<br /><br /> - **WPA2-PSK**|  
|**Cifrado de datos**|Elija el método de cifrado utilizado por esta conexión. Los valores que puede seleccionar variarán según el método de **autenticación** seleccionado:<br /><br /> - **Deshabilitado**<br /><br /> - **WEP**<br /><br /> - **TKIP**<br /><br /> - **AES**|  
|**Índice de clave**|Seleccione un índice de clave de **1** a **4** que se usará cuando el valor de la opción **Cifrado de datos** sea **WEP**.|  
|**Esta red se conecta a Internet**|Seleccione esta opción si desea proporcionar la configuración de proxy que permita que los dispositivos móviles en una conexión inalámbrica se conecten a Internet.|  
|**Configuración de servidor proxy**|Para las opciones **Servidor** y **Puerto** , especifique los valores **HTTP**, **WAP** y **Sockets**que correspondan.|  
|**Habilitar acceso a la red 802.1X**|Seleccione esta opción si desea proteger la conexión mediante la especificación de un tipo de EAP.|  
|**Tipo de EAP**|Elija el tipo de EAP que va a usar en:<br /><br /> - **PEAP**<br> - **Tarjeta inteligente o certificado**|  
  
  
  
### <a name="certificates"></a>Certificados  
 Permite importar certificados para instalar en dispositivos móviles.  
  
 Haga clic en **Importar**y, a continuación, especifique los valores siguientes:  
  
-   **Archivo de certificado** : haga clic en Examinar y después seleccione el archivo de certificado con la extensión **.cer** que quiere importar.  
  
-   **Almacén de destino** : elija uno o más almacenes de destino donde se agregará el certificado importado en el dispositivo móvil desde:  
  
    -   **Raíz**  
  
    -   **CA**  
  
    -   **Normal**  
  
    -   **Con privilegios**  
  
    -   **SPC**  
  
    -   **Del mismo nivel**  
  
-   **Rol** : si **SPC** (certificado de editor de software) se selecciona como almacén de destino, elija el rol que se asociará con el certificado de:  
  
    -   **Operador móvil**  
  
    -   **Administrador**  
  
    -   **Usuario autenticado**  
  
    -   **Administrador de TI**  
  
    -   **Usuario sin autenticar**  
  
    -   **Servidor de aprovisionamiento de confianza**  
  
### <a name="system-security"></a>Seguridad del sistema  
  
|Configuración|Detalles|  
|-------------|-------------|  
|**Control de cuentas de usuario**|Habilita o deshabilita el Control de cuentas de usuario de Windows en el dispositivo.|  
|**Firewall de red**|Habilita o deshabilita el Firewall de Windows.<br /><br /> (Solo Windows 8.1)|  
|**Actualizaciones (Windows 8.1 y versiones anteriores)**|Elija cómo se descargarán las actualizaciones de software de Windows en los equipos. Por ejemplo, puede descargar actualizaciones automáticamente, pero permita que el usuario elija cuándo instalarlas.|  
|**Clasificación mínima de actualizaciones**|Elija la clasificación mínima de las actualizaciones que se van a descargar en los equipos con Windows: **Ninguna**, **Importante**o **Recomendada**.|  
|**Actualizaciones (Windows 10)**|Elija cómo se descargarán las actualizaciones de software de Windows en los equipos. Por ejemplo, puede descargar actualizaciones automáticamente, pero permita que el usuario elija cuándo instalarlas.<br /><br /> (Solo Windows 10)|  
|**Día de instalación**|Elija el día en que se instalarán las actualizaciones.<br /><br /> (Solo Windows 10)|  
|**Hora de instalación**|Elija la hora en que se instalarán las actualizaciones.<br /><br /> (Solo Windows 10)|  
|**SmartScreen**|Habilita o deshabilita Windows SmartScreen.|  
|**Protección antivirus**|Seleccione esta opción para asegurarse de que el software antivirus está instalado en el dispositivo.|  
|**Las firmas de protección antivirus están actualizadas**|Seleccione esta opción para asegurarse de que los archivos de firmas del antivirus están actualizados.|  
|**Características de versión preliminar**|Permite a Microsoft implementar características y configuraciones de la versión preliminar en el dispositivo.<br /><br /> (Solo Windows 10)|  
|**Instalación manual del certificado raíz**|(Solo Windows 10)| 
|**Permitir cancelar suscripción manualmente**|Permite al usuario cancelar la inscripción a la administración mediante una solución de administración de dispositivos móviles (MDM).| 
  
###  <a name="windows-server-work-folders"></a>Carpetas de trabajo de Windows Server  
 Esta configuración es solo para dispositivos con Windows 8.1 y Windows 10.  
  
|Nombre de la configuración|Detalles|  
|------------------|-------------|  
|**Dirección URL de carpetas de trabajo**|Configura la ubicación de una carpeta de trabajo de Windows Server a la que los usuarios pueden conectarse desde su dispositivo.|  
  
### <a name="allowed-and-blocked-apps-windows-phone-only"></a>Aplicaciones permitidas y bloqueadas (solo Windows Phone).  
 Permite especificar una lista de aplicaciones administradas por Intune compatibles o no compatibles en su empresa. Windows Phone puede permitir o bloquear la instalación de estas aplicaciones.  
  
 No puede especificar aplicaciones compatibles y no compatibles en el mismo elemento de configuración.  
  
#### <a name="to-specify-apps-that-will-be-allowed-or-blocked"></a>Para especificar las aplicaciones que se pueden permitir o bloquear  
  
1.  En la página **Lista de aplicaciones permitidas o bloqueadas**, especifique la siguiente información:  
  
    |Configuración|Más información|  
    |-------------|----------------------|  
    |**Lista de aplicaciones bloqueadas**|Seleccione esta opción si desea especificar una lista de aplicaciones que los usuarios no pueden instalar.|  
    |**Lista de aplicaciones permitidas**|Seleccione esta opción si desea especificar una lista de aplicaciones que los usuarios pueden instalar. Se bloqueará la instalación de las demás aplicaciones.|  
    |**Agregar**|Agrega una aplicación a la lista seleccionada. Especifique un nombre de su elección, opcionalmente el editor de la aplicación y la dirección URL de la aplicación en la tienda de aplicaciones.<br /><br /> Para especificar la dirección URL, en la Tienda Windows, busque la aplicación que desea usar.<br /><br /> Abra la página de la aplicación y copie la dirección URL en el Portapapeles. Ya puede usarla como dirección URL en una la lista de aplicaciones permitidas o bloqueadas.<br /><br /> **Ejemplo:** busque la aplicación **Skype** en la tienda. La dirección URL que utilice será **http://www.windowsphone.com/es-es/store/app/skype/c3f8e570-68b3-4d6a-bdbb-c0a3f4360a51**.|  
    |**Editarar**|Permite editar el nombre, el editor y la dirección URL de la aplicación seleccionada.|  
    |**Quitar**|Elimina la aplicación seleccionada de la lista.|  
    |**Importarar**|Importa la lista de las aplicaciones que ha especificado en un archivo de valores separados por comas. Utilice el formato, nombre de la aplicación, editor, dirección URL de la aplicación en el archivo.|  
  
### <a name="windows-10-team"></a>Windows 10 Team  
 Esta configuración es solo para dispositivos con Windows 10 Team.  
  
|Nombre de la configuración|Detalles|  
|------------------|-------------|  
|**Permitir que la pantalla se active automáticamente cuando los sensores detecten a alguien en la habitación**|Permite que el dispositivo se active automáticamente cuando su sensor detecta alguien en la sala.|  
|**PIN necesario para proyección inalámbrica**|Especifica si debe escribir un PIN para poder usar las capacidades de proyección inalámbrica del dispositivo.|  
|**Ventana de mantenimiento**|Configura la ventana cuando las actualizaciones tienen lugar en el dispositivo. Puede configurar la hora de inicio de la ventana y la duración (de 1 a 5 horas).|
|**Azure Operational Insights**|Azure Operational Insights, parte del conjunto de aplicaciones de Microsoft Operations Manager recopila, almacena y analiza datos de archivos de registro de los dispositivos de Windows 10 Team.<br>Para conectarse a Azure Operational Insights, debe especificar un identificador del área de trabajo y una clave del área de trabajo.| 
|**Proyección inalámbrica de Miracast**|Habilite esta opción si desea permitir que el dispositivo Windows 10 Team use dispositivos compatibles con Miracast para el proyecto.<br>Si habilita esta opción, en **Elegir canal de Miracast**, seleccione el canal de Miracast que se usa para el contenido del proyecto.|
|**Información de reunión mostrada en pantalla de inicio de sesión**|Si habilita esta opción, puede elegir la información que se mostrará en el icono **Reuniones** de la pantalla de **inicio de sesión**. Puede:<br><br>- **Mostrar solo el organizador y la hora**<br>- **Mostrar el organizador, la hora y el asunto (asunto oculto para reuniones privadas)**|
|**URL de imagen de fondo de pantalla de bloqueo**|Use esta opción para mostrar un fondo personalizado en la pantalla de **inicio de sesión** de los dispositivos Windows 10 Team desde la dirección URL que especifique.<br>La imagen debe tener el formato PNG y la dirección URL debe comenzar con **https://**.| 
  
### <a name="windows-information-protection"></a>Windows Information Protection  

Con el aumento de los dispositivos propiedad de los empleados en la empresa, también aumenta el riesgo de pérdidas de datos accidentales a través de aplicaciones y servicios, como el correo electrónico, las redes sociales y la nube pública, que están fuera del control de la empresa. Por ejemplo, cuando un empleado envía imágenes de su último proyecto de ingeniería desde su cuenta de correo electrónico personal, copia y pega información de producto en un tweet o guarda un informe de ventas en curso para su almacenamiento en nube pública.

Windows Information Protection (WIP) ayuda a protegerse contra esta pérdida potencial de datos sin interferir en la experiencia de empleado. WIP también ayuda a proteger los datos y aplicaciones de la empresa de pérdidas accidentales de datos en dispositivos tanto propiedad de la empresa como personales que los empleados llevan al trabajo sin necesidad de realizar cambios en su entorno ni en otras aplicaciones.

 Los elementos de configuración de WIP de Configuration Manager administran la lista de aplicaciones protegidas por EDP, las ubicaciones de red de la empresa, el nivel de protección y la configuración de cifrado.

Para obtener información sobre cómo configurar la protección de datos de empresa con Configuration Manager, consulte [Protege los datos de tu empresa con Windows Information Protection (WIP)](https://technet.microsoft.com/itpro/windows/keep-secure/protect-enterprise-data-using-wip).


### <a name="microsoft-edge"></a>Microsoft Edge  
Esta configuración es para dispositivos con Windows 10, y versiones posteriores.  
  
|Nombre de la configuración|Detalles|  
|------------------|-------------|  
|**Permitir sugerencias de búsqueda en la barra de direcciones**|Permite que el motor de búsqueda sugiera sitios a medida que se escriben frases de búsqueda.|  
|**Permitir enviar tráfico de intranet a Internet Explorer**||  
|**Permitir no rastrear**|La opción de no realizar seguimiento informa a los sitios web de que no desea que realicen un seguimiento de su visita a un sitio.|  
|**Habilitar SmartScreen**|Utilizar SmartScreen para comprobar que los archivos que los usuarios descargan no contienen código malintencionado.|  
|**Permitir elementos emergentes**|Permitir o deshabilitar elementos emergentes del explorador.|  
|**Permitir cookies**|Permitir o deshabilitar las cookies.|  
|**Permitir autorrelleno**|Permitir el uso de la característica Autorrellenar del explorador de Edge.|  
|**Permitir administrador de contraseñas**|Permitir el uso de la característica Administrador de contraseñas del explorador de Edge.|  
|**Ubicación de la lista de sitios del modo de empresa**|Especifica dónde se encuentra la lista de sitios web que se abrirá en modo de empresa. Los usuarios no pueden editar esta lista.|  


### <a name="windows-defender"></a>Windows Defender
Esta configuración es para dispositivos con Windows 10, y versiones posteriores.
 
|Nombre de la configuración|Detalles|  
|------------------|-------------|  
|**Permitir supervisión en tiempo real**|Habilita la detección de malware, spyware y otro tipo de software no deseado en tiempo real.|
|**Permitir supervisión del comportamiento**|Permite a Defender comprobar determinados patrones conocidos de actividad sospechosa en los dispositivos.|
|**Habilitar Sistema de inspección de redes**|El Sistema de inspección de redes (NIS) ayuda a proteger los dispositivos contra vulnerabilidades basadas en la red mediante el uso de firmas de vulnerabilidades conocidas desde Microsoft Endpoint Protection Center a fin de detectar y bloquear el tráfico malintencionado.|
|**Examinar todas las descargas**|Controla si Defender examina todos los archivos descargados desde Internet.|
|**Permitir análisis de scripts**|Permite que Defender analice los scripts que se usan en Internet Explorer.|
|**Supervisar la actividad de archivos y programas**|Permite a Defender supervisar la actividad de archivos y programas en los dispositivos.
|**Días de seguimiento de malware resuelto**|Permite que Defender continúe haciendo seguimiento del malware resuelto durante la cantidad de días que se especifique; de ese modo, puede comprobar manualmente los dispositivos que anteriormente estaban afectados. Si establecer el número de días en 0, el malware permanece en la carpeta Cuarentena y no se quita de manera automática.|
|**Permitir acceso a IU de cliente**|Controla si la interfaz de usuario de Windows Defender se oculta a los usuarios.<br>Cuando esta configuración se modifica, surte efecto la próxima vez que se reinicie el equipo del usuario.|
|**Programar un examen del sistema**|Le permite programar un examen del sistema completo o rápido para que se ejecute de manera habitual el día y a la hora que seleccione.|
|**Programar un examen rápido diario**|Permite programar un examen rápido para que se ejecute diariamente a la hora que seleccione.
|**Limitar el uso de la CPU durante un examen**|Permite limitar la cantidad de CPU que pueden usar los exámenes (de 1 a 100).|
|**Examinar archivos de almacenamiento**|Permite que Defender examine archivos de almacenamiento, como archivos .zip o .cab.|
|**Examinar mensajes de correo electrónico**|Permite que Defender examine los mensajes de correo electrónico en cuanto llegan al dispositivo.|
|**Examinar unidades extraíbles**|Permite que Defender examine unidades extraíbles, como sticks USB.|
|**Examinar unidades asignadas**|Permite que Defender examine los archivos de unidades de red asignadas.<br>Si los archivos de la unidad son de solo lectura, Defender no podrá quitar ningún malware que encuentre en ellos.|
|**Examinar archivos abiertos desde carpetas compartidas de red**|Permite que Defender examine archivos de unidades de red compartidas (por ejemplo, a las que se accede desde una ruta de acceso UNC).<br>Si los archivos de la unidad son de solo lectura, Defender no podrá quitar ningún malware que encuentre en ellos.|
|**Intervalo de actualización de firmas**|Especifica el intervalo en función del cual Defender comprueba si hay nuevos archivos de firmas.
|**Permitir la protección de la nube**|Permite o bloquea la recepción de información en Microsoft Active Protection Service sobre la actividad de malware de los dispositivos que administra. Esta información se usa para mejorar el servicio en el futuro.|
|**Pedir a los usuarios el envío de muestras**|Controla si los archivos que podrían requerir que Microsoft los analice en mayor profundidad a fin de determinar si son malintencionados se envían directamente a Microsoft.|
|**Detección de aplicaciones potencialmente no deseadas**|Protege los dispositivos de escritorio de Windows inscritos ante la ejecución de software que Windows Defender clasifica como potencialmente no deseado. Puede protegerse de la ejecución de estas aplicaciones o usar el modo de auditoría para informar cuando se instala una aplicación potencialmente no deseada.|
|**Exclusiones de archivos y carpetas**|Agrega uno o varios archivos y carpetas, como C:\RutaDeAcceso o %Archivosdeprogramas%\RutaDeAcceso\nombredearchivo.exe a la lista de exclusiones. Estos archivos y carpetas no se incluyen en ningún examen en tiempo real ni programado.|
|**Exclusiones de extensiones de archivo**|Agregue una o varias extensiones de archivo, como jpg o txt, a la lista de exclusiones. Los archivos con estas extensiones no se incluyen en ningún examen en tiempo real ni programado.|
|**Exclusiones de proceso**|Agrega uno o más procesos del tipo .exe, .com o .src a la lista de exclusiones. Estos procesos no se incluyen en ningún examen en tiempo real ni programado.|

  
## <a name="see-also"></a>Véase también  
 [Elementos de configuración para dispositivos administrados sin el cliente de System Center Configuration Manager](../../compliance/deploy-use/configuration-items-for-devices-managed-without-the-client.md)
