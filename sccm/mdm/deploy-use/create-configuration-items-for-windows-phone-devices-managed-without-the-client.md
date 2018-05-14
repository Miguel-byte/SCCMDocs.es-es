---
title: Creación de elementos de configuración para dispositivos Windows Phone administrados con Intune
titleSuffix: Configuration Manager
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: df10dc4d-c9ff-4574-bb33-8d30eb14cfe3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4590077b303d5676aa72a816d785a0864fe2205f
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="how-to-create-configuration-items-for-windows-phone-devices-managed-without-the-system-center-configuration-manager-client"></a>Cómo crear elementos de configuración para dispositivos Windows Phone administrados sin el cliente de System Center Configuration Manager
Use el elemento de configuración de **Windows Phone** de System Center Configuration Manager para administrar la configuración de los dispositivos Windows Phone inscritos en Microsoft Intune o que administra Configuration Manager de forma local.  
  
### <a name="to-create-a-windows-phone-configuration-item"></a>Cómo crear un elemento de configuración de Windows Phone  
  
1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad**.  
  
2.  En el área de trabajo **Activos y compatibilidad** , expanda **Configuración de cumplimiento**y, a continuación, haga clic en **Elementos de configuración**.  
  
3.  En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear elemento de configuración**.  
  
4.  En la página **General** del **Asistente para crear elemento de configuración**, escriba un nombre y, opcionalmente, una descripción para el elemento de configuración.  
  
5.  En **Especifique el tipo de elemento de configuración que quiere crear**, seleccione **Windows Phone**.  
  
6.  Haga clic en **Categorías** si crea y asigna categorías para ayudarle a buscar y filtrar elementos de configuración en la consola de Configuration Manager.  
  
7.  En la página **Plataformas admitidas** del asistente, seleccione las plataformas de Windows Phone específicas que evaluarán el elemento de configuración.  
  
8.  En la página **Configuración del dispositivo** del asistente, seleccione el grupo de configuración que quiere configurar. Vea [Referencia de configuración de elementos de configuración de Windows Phone](#BKMK_Setref) en este tema para obtener detalles y luego haga clic en **Siguiente**.  
  
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
  
##  <a name="windows-phone-configuration-item-settings-reference"></a>Referencia de configuración de elementos de configuración de Windows Phone  
  
### <a name="password"></a>Contraseña  
 Esta configuración se aplica a Windows Phone 8 y Windows Phone 8.1.  
  
|Configuración|Detalles|  
|-------------|-------------|  
|**Requerir configuración de contraseña en dispositivos**|Se requiere una contraseña en dispositivos compatibles.|  
|**Longitud de contraseña mínima (caracteres)**|La longitud mínima de la contraseña.|  
|**Caducidad de la contraseña en días**|El número de días antes de que se deba cambiar una contraseña.|  
|**Número de contraseñas recordadas**|Impide que se vuelvan a usar contraseñas ya utilizadas.|  
|**Número de intentos de inicio de sesión incorrectos antes de que se borre el dispositivo**|Borra el dispositivo si hay un error en este número de intentos de inicio de sesión.|  
|**Complejidad de la contraseña**|Elija si se puede especificar un PIN como "1234" o si se debe proporcionar una contraseña segura.|  
|**Enviar NIP de recuperación de contraseña a Exchange Server**||  
  
### <a name="device"></a>Dispositivo  
  
|Configuración|Detalles|  
|-------------|-------------|  
|**Captura de pantalla**|Permite al usuario obtener una captura de pantalla del dispositivo.<br /><br /> (Solo Windows Phone 8.1)|  
|**Envío de datos de diagnóstico**|Permite el envío de archivos de registro de aplicación.|  
|**Geolocalización**|Permite que el dispositivo use información de servicios de ubicación.<br /><br /> (Solo Windows Phone 8.1)|  
|**Copiar y pegar**|Usa la función de copiar y pegar para transferir datos entre aplicaciones.<br /><br /> (Solo Windows Phone 8.1)|  
|**Bluetooth**|Permite el uso de la capacidad Bluetooth en el dispositivo.|  
  
### <a name="email-management"></a>Administración de correo electrónico  
 Esta configuración se aplica a Windows Phone 8 y Windows Phone 8.1.  
  
|Configuración|Detalles|  
|-------------|-------------|  
|**Correo electrónico POP e IMAP**|Permite la conexión con cuentas de correo electrónico que usan los estándares POP e IMAP.|  
|**Tiempo máximo de conservación de correo electrónico**|Tiempo de conservación de correo electrónico antes de eliminarse del servidor.|  
|**Formatos de mensaje permitidos**|Especifique si los correos electrónicos de usuario pueden ser HTML o texto sin formato únicamente.|  
|**Tamaño máximo para correo electrónico de texto sin formato (descargado automáticamente)**|Controla el tamaño máximo del correo electrónico de texto sin formato cuando se descarga automáticamente.|  
|**Tamaño máximo para correo electrónico HTML (descargado automáticamente)**|Controla el tamaño máximo del correo electrónico HTML cuando se descarga automáticamente.|  
|**Tamaño máximo de datos adjuntos (descargados automáticamente)**|Configura el tamaño máximo del correo electrónico que se descargará automáticamente.|  
|**Sincronización de calendarios**||  
|**Cuenta de correo electrónico personalizada**|Permite el uso de una cuenta que no sea de Microsoft en el dispositivo.|  
|**Hacer que la cuenta Microsoft sea opcional en la aplicación Windows Mail**|No es necesario usar una cuenta Microsoft para iniciar sesión en Correo de Windows.|  
  
### <a name="store"></a>Tienda  
 Esta configuración se aplica solo a dispositivos Windows Phone 8.1.  
  
|Configuración|Detalles|  
|-------------|-------------|  
|**Tienda de aplicaciones**|Permite el acceso a la tienda de aplicaciones en el dispositivo.|  
  
### <a name="browser"></a>Explorador  
 Esta configuración se aplica a Windows Phone 8 y Windows Phone 8.1.  
  
|Configuración|Detalles|  
|-------------|-------------|  
|**Permitir explorador web**|Habilita o deshabilita el explorador de Internet predeterminado.|  
|**Autorrellenar**|El usuario puede cambiar la configuración de Autocompletar en el explorador.|  
|**Active scripting**|El explorador puede ejecutar scripts, como scripts de ActiveX.|  
|**Complementos**|El usuario puede agregar complementos en Internet Explorer.|  
|**Bloqueador de elementos emergentes**|Habilita o deshabilita el bloqueador de elementos emergentes del explorador.|  
|**Advertencia de fraude**|Habilita o deshabilita las advertencias de posibles sitios web fraudulentos.|  
  
### <a name="internet-explorer"></a>Internet Explorer  
 Esta configuración se aplica a Windows Phone 8 y Windows Phone 8.1.  
  
|Configuración|Detalles|  
|-------------|-------------|  
|**Enviar siempre el encabezado No realizar seguimiento**|Impide que se envíe información de exploración a sitios de terceros.|  
|**Zona de seguridad de intranet**||  
|**Nivel de seguridad para zona de Internet**|Configura el nivel de seguridad para la zona de Internet.|  
|**Nivel de seguridad para zona de intranet**|Configura el nivel de seguridad para la zona de intranet.|  
|**Nivel de seguridad para zona de sitios de confianza**|Configura el nivel de seguridad para la zona de sitios de confianza.|  
|**Nivel de seguridad para zona de sitios restringidos**|Configura el nivel de seguridad para la zona de sitios restringidos.|  
|**Espacios de nombres para la zona de intranet**||  
|**Ir a un sitio de intranet por una entrada de una sola palabra**|Habilita o deshabilita la opción que permite a Internet Explorer ir automáticamente a un sitio de intranet si se escribe un nombre de sitio válido sin un HTTP anterior:|  
|**Opción del menú Modo de empresa**|Permite a los usuarios activar y desactivar el modo de empresa desde el menú **Herramientas** de Internet Explorer.|  
|**Ubicación del informe de registro (URL)**|Especifique una dirección URL donde se registrarán los sitios web visitados cuando el modo de empresa esté activo.|  
|**Ubicación de la lista de sitios de Modo de empresa (URL)**|Especifique la ubicación de la lista de sitios web que van a usar el modo de empresa cuando esté activo.|  
  
### <a name="cloud"></a>Nube  
  
|Configuración|Detalles|  
|-------------|-------------|  
|**Sincronización de la configuración**|Permite la sincronización de configuraciones entre diferentes dispositivos.|  
|**Sincronización de credenciales**|Permite la sincronización de credenciales entre diferentes dispositivos.|  
|**Cuenta Microsoft**|Permite el uso de una cuenta Microsoft en el dispositivo.<br /><br /> (Solo Windows Phone 8.1)|  
|**Sincronización de configuraciones a través de conexión de uso medido**|Permite la sincronización de configuraciones cuando se mide la conexión a Internet.|  
  
### <a name="security"></a>Seguridad  
  
|Configuración|Detalles|  
|-------------|-------------|  
|**Instalación de archivos sin firmar**|Permite la carga de archivos sin firmar.|  
|**Aplicaciones sin firmar**|Permite la carga de aplicaciones sin firmar.|  
|**Mensajería SMS y MMS**|Permite mensajería SMS y MMS desde el dispositivo.|  
|**Almacenamiento extraíble**|Permite el uso de almacenamiento extraíble, como una tarjeta SD en el dispositivo.|  
|**Cámara**|Permite el uso de la cámara del dispositivo.|  
|**Transmisión de datos en proximidad (NFC)**|Permite la comunicación mediante el uso de NFC en el dispositivo.<br /><br /> (Solo Windows Phone 8.1)|  
|**Permitir conexión USB**|Permite que los periféricos se conecten a este dispositivo a través de USB.|
  
### <a name="peak-synchronization"></a>Sincronización durante horas punta  
 Esta configuración se aplica a Windows Phone 8 y Windows Phone 8.1.  
  
|Configuración|Detalles|  
|-------------|-------------|  
|**Especifica las horas pico**|Permite especificar un período de tiempo que usarán las dos configuraciones siguientes.|  
|**Frecuencia de sincronización durante horas punta**|Permite elegir la frecuencia con que el dispositivo se sincronizará durante el tiempo máximo especificado.|  
|**Frecuencia de sincronización fuera de horas punta**|Permite elegir la frecuencia con que el dispositivo se sincronizará fuera del tiempo máximo especificado.|  
  
### <a name="roaming"></a>Movilidad  
 Esta configuración se aplica a Windows Phone 8 y Windows Phone 8.1.  
  
|Configuración|Detalles|  
|-------------|-------------|  
|**Administración de dispositivos en movilidad**|Permite que Configuration Manager administre el dispositivo cuando está en itinerancia.|  
|**Descarga de software en movilidad**|Permite la descarga de software y aplicaciones cuando se está en movilidad.|  
|**Descarga de correo electrónico en movilidad**|Permite descargas de correo electrónico en movilidad.|  
|**Itinerancia de datos**|Permite movilidad entre redes al obtener acceso a datos.|  
  
### <a name="encryption"></a>Cifrado  
 Esta configuración se aplica a Windows Phone 8 y Windows Phone 8.1.  
  
|Configuración|Detalles|  
|-------------|-------------|  
|**Cifrado de tarjeta de almacenamiento**|Se requieren las tarjetas de almacenamiento utilizadas con el dispositivo que se va a cifrar.|  
|**Cifrado de archivo en el dispositivo**|Requiere el cifrado de los archivos en el dispositivo móvil.|  
|**Requerir firma de correo electrónico**|Requiere que los mensajes de correo electrónico se firmen antes de enviarlos.|  
|**Algoritmo de firma**|Selecciona el algoritmo utilizado para firmar los mensajes de correo electrónico.|  
|**Requerir cifrado de correo electrónico**|Requiere que los mensajes de correo electrónico se cifren antes de enviarlos.|  
|**Algoritmo de cifrado**|Selecciona el algoritmo utilizado para cifrar los mensajes de correo electrónico.|  
  
###  <a name="wireless-communications"></a>Comunicaciones inalámbricas  
 Esta configuración se aplica a Windows Phone 8 y Windows Phone 8.1.  
  
|Nombre de la configuración|Detalles|  
|------------------|-------------|  
|**Conexión de red inalámbrica**|Habilita o deshabilita la capacidad Wi-Fi de los dispositivos.|  
|**Tethering Wi-Fi**|Permite que los usuarios usen sus dispositivos como una zona con cobertura inalámbrica móvil.|  
|**Descargar datos con Wi-Fi cuando sea posible**||  
|**Informes de zonas Wi-Fi**||  
  
##### <a name="to-configure-a-wireless-network-connection"></a>Para configurar una conexión de red inalámbrica  
  
1.  En la página **Configure las opciones de comunicación inalámbrica de dispositivo móvil** , haga clic en **Agregar**.  
  
2.  En el cuadro de diálogo **Conexión de red inalámbrica** , especifique la siguiente información sobre la conexión inalámbrica que se aprovisionará en dispositivos móviles:  
  
|Configuración|Más información|  
|-------------|----------------------|  
|**Nombre de red (SSID)**||  
|**Conexión de red**|Elija **Internet** o **Trabajo**.|  
|**Autenticación**|Elija el método de autenticación para la conexión inalámbrica desde:<br><br> - **Abierto**<br> - **Compartido**<br> - **WPA**<br> - **WPA-PSK**<br> - **WPA2**<br> - **WPA2-PSK**|  
|**Cifrado de datos**|Elija el método de cifrado utilizado por esta conexión. Los valores que puede seleccionar variarán según el método de **autenticación** seleccionado:<br><br> - **Deshabilitado**<br> - **WEP**<br> - **TKIP**<br> - **AES**|  
|**Índice de clave**|Seleccione un índice de clave de **1** a **4** que se usará cuando el valor de la opción **Cifrado de datos** sea **WEP**.|  
|**Esta red se conecta a Internet**|Seleccione esta opción si desea proporcionar la configuración de proxy que permita que los dispositivos móviles en una conexión inalámbrica se conecten a Internet.|  
|**Configuración de servidor proxy**|Para las opciones **Servidor** y **Puerto** , especifique los valores **HTTP**, **WAP** y **Sockets**que correspondan.|  
|**Habilitar acceso a la red 802.1X**|Seleccione esta opción si desea proteger la conexión mediante la especificación de un tipo de EAP.|  
|**Tipo de EAP**|Elija el tipo de EAP que va a usar en:<br><br> - **PEAP**<br> - **Tarjeta inteligente o certificado**|  
    
  
###  <a name="certificates"></a>Certificados  
 Permite importar certificados para instalar en dispositivos móviles.  
  
 Haga clic en **Importar**y, a continuación, especifique los valores siguientes:  
  
-   **Archivo de certificado** : haga clic en **Examinar** y, a continuación, seleccione el archivo de certificado con la extensión **.cer** que desea importar.  
  
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
 Esta configuración se aplica a Windows Phone 8 y Windows Phone 8.1.  
  
|Configuración|Detalles|  
|-------------|-------------|  
|**Control de cuentas de usuario**|Habilita o deshabilita el Control de cuentas de usuario de Windows en el dispositivo.|  
|**Firewall de red**|Habilita o deshabilita el Firewall de Windows.|  
|**Actualizaciones**|Elija cómo se descargarán las actualizaciones de software de Windows en los equipos. Por ejemplo, puede descargar actualizaciones automáticamente, pero permita que el usuario elija cuándo instalarlas.|  
|**Clasificación mínima de actualizaciones**|Elija la clasificación mínima de las actualizaciones que se van a descargar en los equipos con Windows: **Ninguna**, **Importante**o **Recomendada**.|  
|**SmartScreen**|Habilita o deshabilita Windows SmartScreen.|  
|**Protección antivirus**|Se asegura de que el dispositivo esté protegido por el software antivirus|  
|**Las firmas de protección antivirus están actualizadas**|Se asegura de que los archivos de firmas del antivirus están actualizados.|
|**Permitir cancelar suscripción manualmente**|Permite al usuario eliminar su dispositivo de MDM.|  
  
### <a name="windows-server-work-folders"></a>Carpetas de trabajo de Windows Server  
 Esta configuración se aplica a Windows Phone 8 y Windows Phone 8.1.  
  
|Configuración|Detalles|  
|-------------|-------------|  
|**Dirección URL de carpetas de trabajo**|Configura la ubicación de una carpeta de trabajo de Windows Server a la que los usuarios pueden conectarse desde su dispositivo.|  
  
### <a name="allowed-and-blocked-apps-list-windows-phone-81-only"></a>Lista de aplicaciones permitidas y bloqueadas (solo Windows Phone 8.1)  
 Permite especificar la lista de aplicaciones de Windows Phone que son compatibles o no en su empresa. Los usuarios no pueden instalar las aplicaciones que especifique como bloqueadas. Si especifica una lista de aplicaciones permitidas, los usuarios solo pueden instalar esas aplicaciones.  
  
 No puede especificar aplicaciones permitidas y bloqueadas en el mismo elemento de configuración.  
  
> [!IMPORTANT]  
>  Si especifica una lista de aplicaciones permitidas, debe asegurarse de que la aplicación de portal de empresa y todas las aplicaciones que haya implementado en dispositivos Windows Phone 8.1 estén en la lista de aplicaciones **Permitidas** .  
  
##### <a name="to-specify-an-allowed-or-blocked-apps-list"></a>Para especificar una lista de aplicaciones permitidas o bloqueadas  
  
1.  En la página **Lista de aplicaciones permitidas y bloqueadas (Windows Phone 8.1)** , especifique la siguiente información:  
  
|||  
|-|-|  
|Configuración|Más información|  
|**Lista de aplicaciones bloqueadas**|Seleccione esta opción si desea especificar una lista de aplicaciones que los usuarios no podrán instalar.|  
|**Lista de aplicaciones permitidas**|Seleccione esta opción si desea especificar una lista de aplicaciones que los usuarios pueden instalar.|  
|**Agregar**|Agrega una aplicación a la lista seleccionada. Especifique un nombre de su elección (opcionalmente puede ser el editor de la aplicación) y la dirección URL de la aplicación en la tienda de aplicaciones.<br /><br /> Para especificar la dirección URL, en la página de la tienda de Windows Phone, busque la aplicación que desea usar.<br /><br /> **Ejemplo:** busque la aplicación **Skype** en la tienda. La dirección URL que usa será http://www.windowsphone.com/en-us/store/app/skype/c3f8e570-68b3-4d6a-bdbb-c0a3f4360a51.<br /><br /> Para la aplicación del portal de la empresa, o aplicaciones de línea de negocio, no es necesario especificar una dirección URL completa, solo el GUID de la aplicación.|  
|**Editarar**|Permite editar el nombre, el editor y la dirección URL de la aplicación seleccionada.|  
|**Quitar**|Elimina la aplicación seleccionada de la lista.|  
|**Importarar**|Importa la lista de las aplicaciones que ha especificado en un archivo de valores separados por comas. Utilice el formato, nombre de la aplicación, editor, dirección URL de la aplicación en el archivo.|  
  
## <a name="see-also"></a>Véase también  
 [Elementos de configuración para dispositivos administrados sin el cliente de System Center Configuration Manager](../../compliance/deploy-use/configuration-items-for-devices-managed-without-the-client.md)