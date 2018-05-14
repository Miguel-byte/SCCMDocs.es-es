---
title: Creación de elementos de configuración para dispositivos Android y Samsung KNOX Standard administrados con Intune
titleSuffix: Configuration Manager
description: Use el elemento de configuración de Android y Samsung KNOX Standard de System Center Configuration Manager para administrar la configuración de los dispositivos.
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 7b66f3c4-e3bb-4f6a-abd5-55be649ff90d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fbfcc2189e2ce06e6348936caad6c68de51f5bdb
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="how-to-create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-system-center-configuration-manager-client"></a>Cómo crear elementos de configuración para dispositivos Android y Samsung KNOX administrados sin el cliente de System Center Configuration Manager

Use el elemento de configuración de **Android y Samsung KNOX** de System Center Configuration Manager para administrar la configuración de los dispositivos Android y Samsung KNOX inscritos en Microsoft Intune o administrados mediante System Center Configuration Manager de forma local.  

#### <a name="to-create-an-android-and-samsung-knox-configuration-item"></a>Cómo crear un elemento de configuración de Android y Samsung KNOX  

1. En la consola de Configuration Manager, elija **Activos y compatibilidad**.  

2. En el área de trabajo **Activos y compatibilidad**, expanda **Configuración de cumplimiento** y, a continuación, elija **Elementos de configuración**.  

3. En la pestaña **Inicio**, en el grupo **Crear**, elija **Crear elemento de configuración**.  

4. En la página **General** del Asistente para crear elemento de configuración, escriba un nombre y, si quiere, una descripción para el elemento de configuración.  

5. En **Especifique el tipo de elemento de configuración que quiere crear**, elija **Android y Samsung KNOX**.  

6. Elija **Categorías** si crea y asigna categorías que puedan resultar útiles para buscar y filtrar elementos de configuración en la consola de Configuration Manager.  

7. En la página **Plataformas admitidas** del asistente, elija las plataformas específicas de Android y Samsung KNOX que evaluarán el elemento de configuración.  

8. En la página **Configuración del dispositivo** del asistente, elija el grupo de configuración que quiere configurar. Vea [Referencia de configuración de elementos de configuración de Android y Samsung KNOX](#BKMK_setref) en este tema para obtener detalles y, luego, elija **Siguiente**.  

    > [!TIP]  
    >  Si el valor que quiere no aparece, active la casilla **Configurar opciones adicionales que no se encuentran en los grupos de configuración predeterminados**.  

9. En cada página de configuración, configure las opciones que necesite. Además, elija si quiere corregirlas cuando no sean compatibles en dispositivos (si se admite esta opción).  

10. Para cada grupo de configuración, también puede configurar la gravedad que se notificará cuando se detecte que un elemento de configuración no es compatible:  

    - **Ninguna**. Los dispositivos que no cumplan esta regla de compatibilidad no notificarán ninguna gravedad de error en los informes de Configuration Manager.  

    - **Información**. Los dispositivos que no cumplan esta regla de compatibilidad notificarán una gravedad de error de **Información** en los informes de Configuration Manager.  

    - **Advertencia**. Los dispositivos que no cumplan esta regla de compatibilidad notificarán una gravedad de error de **Advertencia** en los informes de Configuration Manager.  

    - **Crítica**. Los dispositivos que no cumplan esta regla de compatibilidad notificarán una gravedad de error **Crítica** en los informes de Configuration Manager.  

    - **Crítica con evento**. Los dispositivos que no cumplan esta regla de compatibilidad notificarán una gravedad de error **Crítica** en los informes de Configuration Manager. Este nivel de gravedad también se registra como evento de Windows en el registro de eventos de la aplicación.  

11. En la página **Aplicabilidad de plataforma** del asistente, revise cualquier opción de configuración que no sea compatible con las plataformas admitidas que eligió anteriormente. Puede regresar y eliminar esta configuración o puede continuar.  

    > [!TIP]  
    >  No se evalúa el cumplimiento de la configuración no admitida.  

12. Finalice el asistente.  

 Puede ver el nuevo elemento de configuración en el nodo **Elementos de configuración** del área de trabajo **Activos y compatibilidad** .  

## <a name="android-and-samsung-knox-configuration-item-settings-reference"></a>Referencia de configuración de elementos de configuración de Android y Samsung KNOX  

### <a name="password"></a>Contraseña  
Esta configuración se aplica a los dispositivos Android y Samsung KNOX.  

|Configuración|Detalles|  
|-------------|-------------|  
|**Requerir configuración de contraseña en dispositivos**|Requiere una contraseña en dispositivos compatibles.|  
|**Longitud de contraseña mínima (caracteres)**|Especifica la longitud mínima de la contraseña.|  
|**Caducidad de la contraseña en días**|Especifica el número de días antes de que se deba cambiar una contraseña.|  
|**Número de contraseñas recordadas**|Impide que se vuelvan a usar contraseñas ya utilizadas.|  
|**Número de intentos de inicio de sesión incorrectos antes de que se borre el dispositivo**|Borra el dispositivo si hay un error en este número de intentos de inicio de sesión.|  
|**Tiempo de inactividad antes de que se bloquee el dispositivo**|Especifica el periodo que transcurre antes de que el dispositivo se bloquee si no se utiliza.|
|**Calidad de contraseña**|Especifica el nivel requerido de complejidad de la contraseña y si se pueden usar dispositivos biométricos.|  
|**Permitir Smart Lock y otros agentes de confianza**|Permite controlar la característica de Smart Lock en dispositivos Android compatibles. Esta funcionalidad del teléfono le permite deshabilitar u omitir la contraseña de la pantalla de bloqueo del dispositivo si el dispositivo está en una ubicación de confianza, como cuando se conecta a un dispositivo Bluetooth específico o cuando está cerca de una etiqueta NFC. Puede usar esta opción para impedir que los usuarios configuren Smart Lock.|
|**Desbloquear mediante huella digital (KNOX 5.0+)**|Permite usar una huella digital para desbloquear dispositivos compatibles.|

### <a name="device"></a>Dispositivo   

|Configuración|Detalles|  
|------------------|-------------|  
|**Marcación por voz**|Habilita o deshabilita la característica de marcación por voz en el dispositivo.|
|**Asistente de voz**|Permite usar software de asistente de voz en el dispositivo.|
|**Captura de pantalla**|Permite al usuario capturar el contenido en pantalla como una imagen.|
|**Envío de datos de diagnóstico**|Permite enviar información de diagnóstico a Google desde el dispositivo.|
|**Geolocalización**|Permite que el dispositivo use la información de ubicación.|
|**Copiar y pegar**|Permite las funciones de copiar y pegar en el dispositivo.|
|**Restablecimiento de la configuración de fábrica**|Permite que el usuario realice un restablecimiento de fábrica en el dispositivo.|  |
|**Uso compartido del Portapapeles entre aplicaciones**|Permite que el usuario use el Portapapeles para copiar y pegar entre aplicaciones.|  |
|**Bluetooth**|Permite usar Bluetooth en el dispositivo.|

### <a name="store"></a>Tienda

|Configuración|Detalles|  
|------------------|-------------|  
|**Tienda de aplicaciones**|Permite que el usuario acceda a Google Play Store en el dispositivo.|

### <a name="browser"></a>Explorador

|Configuración|Detalles|  
|------------------|-------------|  
|**Permitir explorador web**|Permite el uso del explorador web predeterminado del dispositivo.|
|**Autorrellenar**|Permite usar la función Autorrellenar del explorador web.|
|**Active scripting**|Permite que el explorador web del dispositivo use Active scripting.|
|**Bloqueador de elementos emergentes**|Permite usar el bloqueador de elementos emergentes en el explorador web.|
|**Cookies**|Permite que el explorador web del dispositivo use cookies.|

### <a name="cloud"></a>Nube  

|Configuración|Detalles|  
|-------------|-------------|  
|**Copia de seguridad de Google**|Permite el uso de la copia de seguridad de Google.|  
|**Sincronización automática de la cuenta de Google**|Permite que la configuración de la cuenta de Google se sincronice automáticamente.|  

### <a name="security"></a>Seguridad  

|Configuración|Detalles|  
|-------------|-------------|  
|**Mensajería SMS y MMS**|Permite usar mensajes SMS y MMS en el dispositivo.|
|**Almacenamiento extraíble**|Permite que el dispositivo use un almacenamiento extraíble, como una tarjeta SD.|
|**Cámara**|Permite el uso de la cámara del dispositivo.<br /><br /> Se aplica a dispositivos Android y Samsung KNOX.|
|**Transmisión de datos en proximidad (NFC)**|Permite tareas que usan la transmisión de datos en proximidad, si el dispositivo la admite.|
|**YouTube**|Permite el uso de la aplicación de YouTube en el dispositivo.<br /><br /> Se aplica únicamente a dispositivos Samsung KNOX.|  
|**Desconectar**|Permite que el dispositivo se desconecte.<br /><br /> Se aplica únicamente a dispositivos Samsung KNOX.|  

### <a name="roaming"></a>Movilidad

|Configuración|Detalles|  
|-------------|-------------|  
|Itinerancia de voz|Permite la itinerancia de voz cuando el dispositivo está en una red de telefonía móvil.|
|Itinerancia de datos|Permite la itinerancia de datos cuando el dispositivo está en una red de telefonía móvil.|


### <a name="encryption"></a>Cifrado  
 Esta configuración se aplica a los dispositivos Android y Samsung KNOX.  

|Configuración|Detalles|  
|-------------|-------------|  
|**Cifrado de tarjeta de almacenamiento**|Requiere el cifrado de la tarjeta de almacenamiento del dispositivo.|
|**Cifrado de archivo en el dispositivo**|Requiere el cifrado de los archivos en el dispositivo móvil.|  

### <a name="wireless-communications"></a>Comunicaciones inalámbricas

|Configuración|Detalles|  
|-------------|-------------|  
|**Conexión de red inalámbrica**|Permite usar las funcionalidades de Wi-Fi del dispositivo.|
|**Tethering Wi-Fi**|Permite usar tethering Wi-Fi en el dispositivo.|


### <a name="compliant-and-noncompliant-apps-android"></a>Aplicaciones compatibles y no compatibles (Android)  
Puede especificar una lista de aplicaciones compatibles y no compatibles de Android en su empresa. A continuación, puede usar informes para mostrar los dispositivos que tienen instaladas aplicaciones no compatibles y el usuario asociado.  

No puede especificar aplicaciones compatibles y no compatibles en el mismo elemento de configuración.  

#### <a name="to-specify-the-compliant-or-noncompliant-apps-list"></a>Para especificar la lista de aplicaciones compatibles o no compatibles  

En la página **Aplicaciones compatibles y no compatibles (Android)** , especifique la siguiente información:  

|Configuración|Más información|  
|-------------|----------------------|  
|**Lista de aplicaciones no compatibles**|Especifica una lista de aplicaciones que se notificarán como no compatibles si los usuarios las instalan.|  
|**Lista de aplicaciones compatibles**|Especifica una lista de aplicaciones que los usuarios pueden instalar. Cualquier otra aplicación instalada se notificará como no compatible.|  
|**Agregar**|Agrega una aplicación a la lista seleccionada. Especifique un nombre de su elección, opcionalmente el editor de la aplicación y la dirección URL de la aplicación en la tienda de aplicaciones.<br /><br /> Para especificar la dirección URL, en la [sección Aplicaciones de Google Play](https://play.google.com/store/apps), busque la aplicación que quiera usar.<br /><br /> Abra la página de la aplicación y copie la dirección URL en el Portapapeles. Ya puede utilizarla como dirección URL en una la lista de aplicaciones conformes o no conformes.<br /><br /> **Ejemplo:** busque **Microsoft Office Mobile**en Google Play. La dirección URL que usa será **https://play.google.com/store/apps/details?id=com.microsoft.office.officehub**.|  
|**Editarar**|Permite editar el nombre, el editor y la dirección URL de la aplicación seleccionada.|  
|**Quitar**|Elimina la aplicación seleccionada de la lista.|  
|**Importarar**|Importa la lista de las aplicaciones que ha especificado en un archivo de valores separados por comas. Utilice el formato, el nombre de la aplicación, el editor y la dirección URL de la aplicación en el archivo.|  

## <a name="android-for-work-configuration-items"></a>Elementos de configuración para Android for Work
Android for Work tiene dos grupos de configuración para elementos de configuración:

- **Contraseña**. Idéntica a la configuración para Android "clásico".

- **Perfil de trabajo**. Habilita la siguiente configuración de Android for Work:
  - **Permitir uso compartido de datos entre perfiles de trabajo y perfiles personales**
  - **Ocultar notificaciones del perfil de trabajo cuando el dispositivo está bloqueado** (Android 6.0+)
  - **Establecer directiva de permisos de aplicación predeterminada** (Android 6.0+)

Para crear un elemento de configuración en el perfil de trabajo de Android, elija **Android for Work** en la página **General** y configure los valores para cada uno de los grupos de configuración. Agregue el elemento de configuración a una línea base e impleméntelo como de costumbre. Esta configuración solo se aplicará a los dispositivos inscritos como Android for Work y no a los inscritos como Android.

### <a name="kiosk-mode-samsung-knox-only"></a>Pantalla completa (solo Samsung KNOX)  
Puede usar la pantalla completa para bloquear un dispositivo a fin de permitir que solo funcionen determinadas características. Por ejemplo, puede permitir que un dispositivo ejecute solo una aplicación administrada que especifique, o puede deshabilitar los botones de volumen de un dispositivo. Es posible que esta configuración se utilice para un modelo de demostración de un dispositivo. También se podría usar para un dispositivo que esté dedicado a realizar solo una función, como un dispositivo de punto de venta.  

#### <a name="to-configure-kiosk-mode-for-a-samsung-knox-device"></a>Para configurar la pantalla completa para un dispositivo Samsung KNOX  

1. En la página **Configurar las opciones de pantalla completa para los dispositivos Samsung KNOX** del Asistente para crear elemento de configuración, especifique la siguiente información:  

   |Configuración|Más información|  
   |-------------|----------------------|  
   |**Seleccionar aplicación**|Elija **Examinar** para seleccionar una aplicación Android de Configuration Manager (con la extensión **.apk**) que se podrá ejecutar cuando el dispositivo esté en pantalla completa. No se podrá ejecutar ninguna otra aplicación en el dispositivo.|  
   |**Botones de volumen**|Habilita o deshabilita el uso de los botones de volumen en el dispositivo.|  
   |**Botón de suspensión y reactivación de pantalla**|Habilita o deshabilita el botón de reactivación de la suspensión de pantalla en el dispositivo.|  

2. Cuando termine, elija **Siguiente**.  

## <a name="reports-for-monitoring"></a>Informes para la supervisión
Puede utilizar uno de los siguientes informes para supervisar las aplicaciones conformes y no conformes:  

- **Lista de aplicaciones y dispositivos no conformes para un usuario específico**. Muestra información sobre los usuarios y los dispositivos que tienen aplicaciones instaladas que no cumplen la directiva especificada.  

- **Resumen de usuarios que tienen aplicaciones no conformes**. Muestra información sobre los usuarios que tienen aplicaciones instaladas que no cumplen la directiva especificada.  

Para obtener más información sobre cómo usar los informes, consulte [Generación de informes en System Center Configuration Manager](../../core/servers/manage/reporting.md).  

## <a name="see-also"></a>Consulte también  
[Elementos de configuración para dispositivos administrados sin el cliente de System Center Configuration Manager](../../compliance/deploy-use/configuration-items-for-devices-managed-without-the-client.md)
