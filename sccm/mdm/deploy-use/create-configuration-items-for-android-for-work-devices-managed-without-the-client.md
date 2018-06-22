---
title: Creación de elementos de configuración para dispositivos Android for Work administrados con Intune
titleSuffix: Configuration Manager
ms.date: 2017-07-31
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: ab6784fd-8c57-4be9-858f-50fe39f2ff5f
author: aczechowski
ms.author: aaroncz
ms.openlocfilehash: ba70e4d3a87f2a305312449907730174c62c4775
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32351282"
---
# <a name="how-to-create-configuration-items-for-android-for-work-devices-managed-with-intune"></a>Creación de elementos de configuración para dispositivos Android for Work administrados con Intune

 Use el elemento de configuración de **Android for Work** de System Center Configuration Manager para administrar la configuración de los dispositivos Android for Work inscritos en Microsoft Intune o que administra Configuration Manager de forma local.  

### <a name="to-create-an-android-for-work-configuration-item"></a>Para crear elementos de configuración para Android for Work  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad**.  

2.  En el área de trabajo **Activos y compatibilidad** , expanda **Configuración de cumplimiento**y, a continuación, haga clic en **Elementos de configuración**.  

3.  En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear elemento de configuración**.  

4.  En la página **General** del **Asistente para crear elemento de configuración**, escriba un nombre y, opcionalmente, una descripción para el elemento de configuración.  

5.  En **Especifique el tipo de elemento de configuración que quiere crear**, seleccione **Android for Work**.  

6.  Elija **Categorías** si crea y asigna categorías que puedan resultar útiles para buscar y filtrar elementos de configuración en la consola de Configuration Manager.  

  Haga clic en **Siguiente**.

7.  En la página **Configuración del dispositivo** del asistente, seleccione los grupos de configuración que quiere configurar. Consulte [Creación de elementos de configuración para dispositivos Android for Work administrados con Intune](#android-for-work-configuration-item-settings-reference) para obtener información y, luego, haga clic en **Siguiente**.  

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

##  <a name="android-for-work-configuration-item-settings-reference"></a>Referencia de configuración de elementos de configuración de Android for Work  

### <a name="password"></a>Contraseña  

|Configuración|Detalles|  
|-------------|-------------|  
|**Requerir configuración de contraseña en dispositivos**|Se requiere una contraseña en dispositivos compatibles.|  
|**Longitud de contraseña mínima (caracteres)**|La longitud mínima de la contraseña.|  
|**Caducidad de la contraseña en días**|El número de días antes de que se deba cambiar una contraseña.|  
|**Número de contraseñas recordadas**|Impide la reutilización de contraseñas usadas recientemente.|  
|**Número de intentos de inicio de sesión incorrectos antes de que se borre el dispositivo**|Borra el dispositivo si hay un error en este número de intentos de inicio de sesión.|  
|**Tiempo de inactividad antes de que se bloquee el dispositivo**|Seleccione la cantidad de tiempo que el dispositivo no se utilizará antes de bloquearse.|
|**Calidad de contraseña**|Seleccione el nivel requerido de complejidad de la contraseña y también si se pueden usar dispositivos biométricos.|  
|**Permitir Smart Lock y otros agentes de confianza**|Permite controlar la característica de Smart Lock en dispositivos Android compatibles. Esta funcionalidad del teléfono, conocida también en ocasiones como "agentes de confianza", permite deshabilitar u omitir la contraseña de la pantalla de bloqueo del dispositivo si el dispositivo está en una ubicación de confianza, como cuando se conecta a un dispositivo Bluetooth específico o cuando está cerca de una etiqueta NFC. Esta opción se puede usar para impedir que los usuarios finales configuren Smart Lock.|
|**Desbloquear mediante huella digital**|&nbsp;|

###  <a name="work-profile"></a>Perfil de trabajo  
 Esta configuración se aplica solo a los dispositivos Samsung KNOX.  

|Nombre de la configuración|Detalles|  
|------------------|-------------|  
|**Permitir uso compartido de datos entre perfiles de trabajo y perfiles personales**|Elija de entre las siguientes opciones:<br>- **No configurado**<br>- **Restricciones de uso compartido predeterminadas**<br>- **Las aplicaciones del perfil profesional pueden controlar una solicitud de uso compartido del perfil personal**<br>- **Las aplicaciones del perfil personal pueden controlar una solicitud de uso compartido del perfil personal**<br><br>Consulte también la página sobre [configuración de copiar y pegar](#copy-paste-configuration-item-settings) usando el URI personalizado.|  
|**Ocultar notificaciones del perfil de trabajo cuando el dispositivo está bloqueado (Android 6.0+)**||
|**Establecer directiva de permisos de aplicación predeterminada (Android 6.0+)**|Elija de entre las siguientes opciones:<br>- **No configurado**<br>- **Preguntar siempre**<br>- **Concesión automática**<br>- **Denegación automática**|

### <a name="copy-paste-configuration-item-settings"></a>Elementos de configuración de copiar y pegar
Ninguno de las opciones de **Permitir uso compartido de datos entre perfiles de trabajo y perfiles personales:** evitan el comportamiento de copiar y pegar. Use una configuración personalizada que se pueda configurar para evitar la funcionalidad de copiar y pegar. Se puede establecer a través del URI personalizado.

- OMA-URI: ./Vendor/MSFT/WorkProfile/DisallowCrossProfileCopyPaste
- Tipo de valor: booleano

Si se establece DisallowCrossProfileCopyPaste en true, se impide el comportamiento de copiar y pegar entre perfiles personales y profesionales de Android for Work.

## <a name="see-also"></a>Véase también  
 [Elementos de configuración para dispositivos administrados sin el cliente de System Center Configuration Manager](../../compliance/deploy-use/configuration-items-for-devices-managed-without-the-client.md)
