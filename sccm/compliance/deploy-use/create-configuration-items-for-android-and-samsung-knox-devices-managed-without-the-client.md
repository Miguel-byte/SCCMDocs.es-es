---
title: "Crear elementos de configuración para dispositivos Android y Samsung KNOX administrados sin el cliente de System Center Configuration Manager | System Center Configuration Manager"
description: "Use el elemento de configuración de Android y Samsung KNOX de System Center Configuration Manager para administrar la configuración de los dispositivos."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c28d5ef5-3ea7-4ba2-af01-6600aa805d48
caps.latest.revision: 17
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 8d676d31d519b7b6099c878d94b4c81f1c972887


---
# <a name="create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-system-center-configuration-manager-client"></a>Crear elementos de configuración para dispositivos Android y Samsung KNOX administrados sin el cliente de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*



 Use el elemento de configuración de **Android y Samsung KNOX** de System Center Configuration Manager para administrar la configuración de los dispositivos Android y Samsung KNOX inscritos en Microsoft Intune o que administra System Center Configuration Manager de forma local.  

## <a name="create-an-android-and-samsung-knox-configuration-item"></a>Crear un elemento de configuración de Android y Samsung KNOX  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad** > **Configuración de cumplimiento** > **Elementos de configuración**.  

3.  En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear elemento de configuración**.  

4.  En la página **General** del **Asistente para crear elemento de configuración**, escriba un nombre y, opcionalmente, una descripción para el elemento de configuración.  

5.  En **Especifique el tipo de elemento de configuración que quiere crear**, seleccione **Android y Samsung KNOX**.  

6.  Haga clic en **Categorías** si crea y asigna categorías para ayudarle a buscar y filtrar elementos de configuración en la consola de Configuration Manager.  

7.  En la página **Plataformas admitidas**, seleccione las plataformas de Android y Samsung KNOX específicas que evaluarán el elemento de configuración.  

8.  En la página **Configuración del dispositivo**, seleccione el grupo de configuración que quiere configurar. Consulte [Referencia de configuración de elementos de configuración de Android y Samsung KNOX](/sccm/compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client#android-and-samsung-knox-configuration-item-settings-reference) en este tema para obtener detalles y luego haga clic en **Siguiente**.  

    > [!TIP]  
    >  Si el valor que quiere no aparece, seleccione la casilla **Configurar opciones adicionales que no se encuentran en los grupos de configuración predeterminados**.  

9. En cada página de configuración, configure las opciones que necesita y si quiere corregirlas cuando no sean conformes en dispositivos (si se admite).  

10. Para cada grupo de configuración, también puede elegir la gravedad que se notificará (en los informes de Configuration Manager) cuando se encuentre que un elemento de configuración no es compatible entre las siguientes:  

    -   **Ninguno**: los dispositivos que no cumplan esta regla de cumplimiento no notificarán ninguna gravedad de error.  

    -   **Información**: los dispositivos que no cumplan esta regla de cumplimiento notificarán una gravedad de error de **Información**.  

    -   **Advertencia**: los dispositivos que no cumplan esta regla de cumplimiento notificarán una gravedad de error de **Advertencia**.  

    -   **Crítico**: los dispositivos que no cumplan esta regla de cumplimiento notificarán una gravedad de error de **Crítico**.  

    -   **Crítico con evento**: los dispositivos que no cumplan esta regla de cumplimiento notificarán una gravedad de error de **Crítico**.   

11. En la página **Aplicabilidad de plataforma**, revise cualquier configuración que no sea compatible con las plataformas admitidas que seleccionó anteriormente. Puede regresar y eliminar esta configuración o puede continuar.  

    > [!TIP]  
    >  No se evalúa el cumplimiento de la configuración no admitida.  

12. Complete el asistente.  

 Puede ver el nuevo elemento de configuración en el nodo **Elementos de configuración** del área de trabajo **Activos y compatibilidad** .  

##  <a name="android-and-samsung-knox-configuration-item-settings-reference"></a>Referencia de configuración de elementos de configuración de Android y Samsung KNOX  

### <a name="password"></a>Contraseña  
 Esta configuración se aplica a los dispositivos Android y Samsung KNOX.  

|Configuración|Detalles|  
|-------------|-------------|  
|**Requerir configuración de contraseña en dispositivos móviles**|Se requiere una contraseña en dispositivos compatibles.|  
|**Longitud de contraseña mínima (caracteres)**|La longitud mínima de la contraseña.|  
|**Caducidad de la contraseña en días**|El número de días antes de que se deba cambiar una contraseña.|  
|**Número de contraseñas recordadas**|Impide que se vuelvan a usar contraseñas ya utilizadas.|  
|**Número de intentos de inicio de sesión incorrectos antes de que se borre el dispositivo**|Borra el dispositivo si hay un error en este número de intentos de inicio de sesión.|  
|**Tiempo de inactividad antes de que se bloquee el dispositivo**|Seleccione el periodo que transcurre antes de que el dispositivo se bloquee si no se utiliza.|
|**Calidad de contraseña**|Seleccione el nivel requerido de complejidad de la contraseña y también si se pueden usar dispositivos biométricos.|  
|**Permitir Smart Lock y otros agentes de confianza**|Permite controlar la característica de Smart Lock en dispositivos Android compatibles. Esta funcionalidad del teléfono, conocida también en ocasiones como agentes de confianza, le permite deshabilitar u omitir la contraseña de la pantalla de bloqueo del dispositivo si el dispositivo está en una ubicación de confianza, como cuando se conecta a un dispositivo Bluetooth específico o cuando está cerca de una etiqueta NFC. Esta opción se puede usar para impedir que los usuarios finales configuren Smart Lock.|

###  <a name="device"></a>Dispositivo  
 Esta configuración se aplica solo a los dispositivos Samsung KNOX.  

|Nombre de la configuración|Detalles|  
|------------------|-------------|  
|**Restablecimiento de la configuración de fábrica**|Permite que el usuario realice un restablecimiento de la configuración de fábrica en el dispositivo.|  
|**Uso compartido del Portapapeles entre aplicaciones**|Use el Portapapeles para copiar y pegar entre aplicaciones.|  

### <a name="cloud"></a>Nube  
 Esta configuración se aplica solo a los dispositivos Samsung KNOX.  

|Configuración|Detalles|  
|-------------|-------------|  
|**Copia de seguridad de Google**|Permite el uso de la copia de seguridad de Google.|  
|**Sincronización automática de la cuenta de Google**|Permite que la configuración de la cuenta de Google se sincronice automáticamente.|  

### <a name="security"></a>Seguridad  

|Configuración|Detalles|  
|-------------|-------------|  
|**Cámara**|Permite el uso de la cámara del dispositivo.<br /><br /> Se aplica a dispositivos Android y Samsung KNOX.|  
|**YouTube**|Permite el uso de la aplicación de YouTube en el dispositivo.<br /><br /> Se aplica únicamente a dispositivos Samsung KNOX.|  
|**Desconectar**|Permite que el dispositivo se desconecte.<br /><br /> Se aplica únicamente a dispositivos Samsung KNOX.|  

### <a name="encryption"></a>Cifrado  
 Esta configuración se aplica a los dispositivos Android y Samsung KNOX.  

|Configuración|Detalles|  
|-------------|-------------|  
|**Cifrado de archivo en el dispositivo**|Requiere el cifrado de los archivos en el dispositivo móvil.|  

### <a name="kiosk-mode-samsung-knox-only"></a>Pantalla completa (solo Samsung KNOX)  
 El modo de quiosco permite bloquear un dispositivo para permitir que solo funcionen determinadas características. Por ejemplo, puede permitir que un dispositivo ejecute solo una aplicación administrada que especifique, o puede deshabilitar los botones de volumen de un dispositivo. Esta configuración podría utilizarse para un modelo de demostración de un dispositivo o para un dispositivo que está dedicado a realizar solo una función, como un dispositivo de punto de venta.  

#### <a name="to-configure-kiosk-mode-for-a-samsung-knox-device"></a>Para configurar la pantalla completa para un dispositivo Samsung KNOX  

En la página **Configurar las opciones de pantalla completa para los dispositivos Samsung KNOX** del **Asistente para crear elemento de configuración**, especifique la siguiente información:  

- **Seleccionar aplicación**: haga clic en **Examinar** para seleccionar una aplicación Android de Configuration Manager (con la extensión **.apk**) que se podrá ejecutar cuando el dispositivo esté en pantalla completa. No se podrá ejecutar ninguna otra aplicación en el dispositivo.
- **Botones de volumen**: habilita o deshabilita el uso de los botones de volumen en el dispositivo.
- **Botón de suspensión y reactivación de pantalla**: habilita o deshabilita el botón de reactivación de la suspensión de pantalla en el dispositivo.|  

###  <a name="compliant-and-noncompliant-apps-android"></a>Aplicaciones compatibles y no compatibles (Android)  
 Permite especificar una lista de aplicaciones compatibles y no compatibles de Android en su empresa. A continuación, puede usar informes para mostrar los dispositivos que tienen instaladas aplicaciones no compatibles y el usuario asociado.  

 No puede especificar aplicaciones compatibles y no compatibles en el mismo elemento de configuración.  

#### <a name="to-specify-the-compliant-or-noncompliant-apps-list"></a>Para especificar la lista de aplicaciones compatibles o no compatibles  

1.  En la página **Aplicaciones compatibles y no compatibles (Android)** , especifique la siguiente información:  

    |Configuración|Más información|  
    |-------------|----------------------|  
    |**Lista de aplicaciones no compatibles**|Seleccione esta opción si desea especificar una lista de aplicaciones que se notificarán como no compatibles los usuarios las instalan.|  
    |**Lista de aplicaciones compatibles**|Seleccione esta opción si desea especificar una lista de aplicaciones que los usuarios pueden instalar. Cualquier otra aplicación instalada se notificará como no compatible.|  
    |**Agregar**|Agrega una aplicación a la lista seleccionada. Especifique un nombre de su elección, opcionalmente el editor de la aplicación y la dirección URL de la aplicación en la tienda de aplicaciones.<br /><br /> Para especificar la dirección URL, en la [sección Aplicaciones de Google Play](https://play.google.com/store/apps), busque la aplicación que desea usar.<br /><br /> Abra la página de la aplicación y copie la dirección URL en el Portapapeles. Ya puede utilizarla como dirección URL en una la lista de aplicaciones conformes o no conformes.<br /><br /> **Ejemplo:** busque **Microsoft Office Mobile**en Google Play. La dirección URL que utilice será **https://play.google.com/store/apps/details?id=com.microsoft.office.officehub**.|  
    |**Editarar**|Permite editar el nombre, el editor y la dirección URL de la aplicación seleccionada.|  
    |**Quitar**|Elimina la aplicación seleccionada de la lista.|  
    |**Importarar**|Importa la lista de las aplicaciones que ha especificado en un archivo de valores separados por comas. Utilice el formato, nombre de la aplicación, editor, dirección URL de la aplicación en el archivo.|  

2.  Cuando haya terminado haga clic en **Siguiente**.  

 Puede utilizar una de las siguientes aplicaciones compatibles y no compatibles de supervisión de informes:  

-   **Lista de aplicaciones y dispositivos no compatibles para un usuario específico** : muestra información sobre los usuarios y los dispositivos que tienen instaladas aplicaciones que no son compatibles con una directiva especificada.  

-   **Resumen de usuarios que tienen aplicaciones no compatibles** : muestra información sobre los usuarios que tienen instaladas aplicaciones que no son compatibles con una directiva especificada.  

 Para obtener más información sobre cómo usar los informes, consulte [Generación de informes en System Center Configuration Manager](../../core/servers/manage/reporting.md).  



<!--HONumber=Nov16_HO1-->


