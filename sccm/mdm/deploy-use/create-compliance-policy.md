---
title: Crear e implementar una directiva de cumplimiento de dispositivos
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo crear e implementar directivas de cumplimiento de dispositivos en System Center Configuration Manager.
ms.custom: na
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0fd76043-d7ee-423d-8c5f-aa7e9ed58ce0
caps.latest.revision: ''
author: mestew
ms.author: mstewart
manager: dougeby
robots: noindex
ms.openlocfilehash: 2a576f3dac75d7c168b86ab0f26453706bda6115
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/23/2018
---
# <a name="create-and-deploy-a-device-compliance-policy"></a>Crear e implementar una directiva de cumplimiento de dispositivos

*Se aplica a: System Center Configuration Manager (Rama actual)*


## <a name="create-a-compliance-policy"></a>Crear una directiva de cumplimiento

1.  En la consola de System Center Configuration Manager, elija **Activos y compatibilidad**.

2.  En el área de trabajo **Activos y compatibilidad**, expanda **Configuración de cumplimiento** y, a continuación, haga clic en **Directivas de cumplimiento**.

3.  En la pestaña **Inicio**, en el grupo **Crear**, elija **Crear directiva de cumplimiento**.

4.  En la página **General** del Asistente para crear directivas de cumplimiento, especifique la información siguiente:

  * **Nombre**: escriba un nombre único para la directiva de cumplimiento. Puede usar hasta 256 caracteres.

  * **Descripción**: escriba una descripción general del perfil de VPN que ayude a identificarlo en la consola de Configuration Manager. Puede usar hasta 256 caracteres.

  * **Tipo de directiva de cumplimiento**: seleccione el tipo de directiva que quiere crear en función de si Configuration Manager administra el dispositivo. <br /><br /> En el caso de dispositivos administrados por Intune, elija la opción **Reglas de compatibilidad para dispositivos administrados sin el cliente de Configuration Manager** . Al seleccionar esta opción, también puede seleccionar el tipo de plataforma a la que quiere que se aplique esta directiva.

  * **Gravedad de no compatibilidad para informes**: especifique el nivel de gravedad que se notifica si esta directiva de cumplimiento se evalúa como no compatible. Los niveles de gravedad disponibles son:

     * **Ninguno**: los dispositivos que no cumplan esta regla de compatibilidad no notificarán ninguna gravedad de error en los informes de Configuration Manager.
     * **Información**: los dispositivos que no cumplan esta regla de compatibilidad notificarán una gravedad de error de **Información** en los informes de Configuration Manager.   
     * **Advertencia**: los dispositivos que no cumplan esta regla de compatibilidad notificarán una gravedad de error de **Advertencia** en los informes de Configuration Manager.
     * **Crítico**: los dispositivos que no cumplan esta regla de compatibilidad notificarán una gravedad de error de **Crítico** en los informes de Configuration Manager.
     * **Crítico con evento**: los dispositivos que no cumplan esta regla de compatibilidad notificarán una gravedad de error de **Crítico** en los informes de Configuration Manager. El nivel de gravedad **Crítico con evento** también se registra como un evento de Windows en el registro de eventos de la aplicación.      

5.  En la página **Plataformas admitidas**, elija las plataformas de dispositivo en las que se va a evaluar esta directiva de cumplimiento. También puede hacer clic en **Seleccionar todo** para elegir todas las plataformas de dispositivo. Las plataformas admitidas son Windows 7, Windows 8.1 y Windows 10; Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 y Windows Server 2016.

6.  En la página **Reglas** , se establecen una o varias reglas que definen la configuración que los dispositivos deben tener para poder ser evaluados como compatibles. Cuando se crea una directiva de cumplimiento, algunas de las reglas se habilitan de forma predeterminada, pero se pueden editar o eliminar. Para obtener una lista completa de todas las reglas, vea la sección "Reglas de directivas de cumplimiento" más adelante en este artículo.

  > [!NOTE]  
  >  En equipos con Windows, la versión 8.1 del sistema operativo Windows se notifica como 6.3 en lugar de 8.1. Si la regla de la versión de SO se establece en Windows 8.1 para Windows, el dispositivo se notificará como no compatible incluso aunque tenga Windows 8.1. Asegúrese de que está estableciendo la versión *notificada* correcta de Windows para las reglas de SO mínimo y máximo. El número de versión debe coincidir con la versión devuelta por el comando **winver**. Windows Phone no tiene este problema, ya que la versión se notifica como 8.1 según lo previsto. En equipos con sistema operativo Windows 10, la versión debe establecerse en **10.0** más el número de compilación del sistema operativo devuelto por el comando **winver**.

7.  En la página **Resumen** del asistente, revise la configuración realizada y, a continuación, finalice el asistente.

 La nueva directiva aparece en el nodo **Directivas de cumplimiento** del área de trabajo **Activos y compatibilidad**.

## <a name="deploy-a-compliance-policy"></a>Implementar una directiva de cumplimiento

1.  En la consola de Configuration Manager, elija **Activos y compatibilidad**.

2.  En el área de trabajo **Activos y compatibilidad**, expanda **Configuración de cumplimiento** y, a continuación, haga clic en **Directivas de cumplimiento**.

3.  En la pestaña **Inicio**, en el grupo **Implementación**, elija **Implementar**.

4.  En el cuadro de diálogo **Implementar directiva de cumplimiento**, elija **Examinar** para seleccionar la recopilación de usuarios en la que se va a implementar la directiva.

     Además, se pueden seleccionar opciones para generar alertas cuando la directiva no es compatible, y para establecer la programación por medio de la cual se va a evaluar esta directiva para el cumplimiento.

5.  Cuando termine, elija **Aceptar**.

## <a name="monitor-the-compliance-policy"></a>Supervisar la directiva de cumplimiento

#### <a name="to-view-compliance-results-in-the-configuration-manager-console"></a>Para ver los resultados de compatibilidad en la consola de Configuration Manager

1.  En la consola de Configuration Manager, elija **Supervisión**.

2.  En el área de trabajo **Supervisión**, elija **Implementaciones**.

3.  En la lista **Implementaciones** , seleccione la implementación de directiva de cumplimiento para la que desea revisar la información de compatibilidad.

4.  Puede revisar la información de resumen sobre la compatibilidad de la implementación de la directiva en la página principal. Para ver información más detallada, seleccione la implementación y, a continuación, en la pestaña **Inicio** del grupo **Implementación**, seleccione **Ver estado** para abrir la página **Estado de implementación**.

    La página **Estado de implementación** contiene las siguientes pestañas:

    -   **Compatible**: muestra la compatibilidad de la directiva en función del número de activos afectados. Puede seleccionar una regla para crear un nodo temporal en el nodo **Usuarios** o **Dispositivos** en el área de trabajo **Activos y compatibilidad**, que contiene todos los usuarios o los dispositivos compatibles con esta regla. En el panel **Detalles del activo** se muestran los usuarios o los dispositivos compatibles con la directiva. Para mostrar información adicional, haga doble clic en un usuario o dispositivo de la lista.

    -   **Error**: muestra una lista de todos los errores de la implementación de directiva seleccionada, en función del número de activos afectados. Puede hacer clic en una regla para crear un nodo temporal en el nodo **Usuarios** o **Dispositivos**, en el área de trabajo **Activos y compatibilidad**, que contiene todos los usuarios o los dispositivos que generaron errores con esta regla. Cuando se selecciona un usuario o dispositivo, el panel **Detalles del activo** muestra los usuarios o dispositivos afectados por un problema. Para mostrar información adicional sobre el problema, haga doble clic en un dispositivo o usuario de la lista.

    -   **No compatible**: muestra una lista de todas las reglas no compatibles en la directiva, en función del número de activos afectados. Puede seleccionar una regla para crear un nodo temporal en el nodo **Usuarios** o **Dispositivos** en el área de trabajo **Activos y compatibilidad**, que contiene todos los usuarios o los dispositivos no compatibles con esta regla. Cuando se selecciona un usuario o dispositivo, el panel **Detalles del activo** muestra los usuarios o dispositivos afectados por un problema. Para mostrar información adicional sobre el problema, haga doble clic en un usuario o dispositivo de la lista.

    -   **Desconocido**: muestra una lista de todos los usuarios y dispositivos que no notificaron el cumplimiento de la implementación de directiva seleccionada, junto con el estado de cliente actual de los dispositivos.

#### <a name="to-monitor-the-compliance-status-of-an-individual-device"></a>Para supervisar el estado de cumplimiento de un dispositivo individual

1.  En la consola de Configuration Manager, seleccione el área de trabajo **Activos y compatibilidad**.

2.  Elija **Dispositivos**.

3. Para habilitar más columnas, haga clic con el botón derecho en una de las columnas.

  Puede agregar las siguientes columnas:

  - **Id. de dispositivo de Azure Active Directory**: el identificador único para el dispositivo en Azure Active Directory.

  - **Detalles del error de cumplimiento**: detalles de mensajes de error cuando se produce un problema en el proceso. Si esta columna está en blanco, significa que no se han encontrado errores y que se ha informado correctamente del estado de cumplimiento.

  - **Ubicación del error de cumplimiento**: más detalles sobre dónde se ha producido el error de cumplimiento. Si esta columna está en blanco, significa que no se han encontrado errores y que se ha informado correctamente del estado de cumplimiento. Ejemplos de dónde se podría producir algún error en el proceso de cumplimiento: 
      - Cliente de Configuration Manager
      - Punto de administración
      - Intune
      - Azure Active Directory
<br></br>
  - **Hora de evaluación del cumplimiento**: última vez que se comprobó el cumplimiento.

  - **Hora a la que se estableció el cumplimiento**: última vez que se actualizó el cumplimiento en Azure Active Directory.

  - **Conforme al acceso condicional**: si el equipo cumple o no las directivas de acceso condicional.

  > [!IMPORTANT]
  > Estas columnas no se muestran de manera predeterminada.

#### <a name="to-view-intune-compliance-policies-charts"></a>Para ver los gráficos de directivas de cumplimiento de Intune
1. En la consola de Configuration Manager, elija **Supervisión**.

2. En el área de trabajo **Supervisión**, vaya a **Información general** > **Configuración de cumplimiento** > **Directivas de cumplimiento**.

   Aparecen los gráficos siguientes:

    - **Cumplimiento general de dispositivos**: muestra el cumplimiento general de los dispositivos de todas las directivas de cumplimiento.
    - **Principales razones de incumplimiento**: muestra las directivas principales que los dispositivos incumplen.

3. Elija una sección de cualquier gráfico para explorar en profundidad una lista de los dispositivos de esa categoría.

#### <a name="to-view-a-health-attestation-report"></a>Para ver un informe de atestación de estado

1. En la consola de Configuration Manager, elija **Supervisión**.

2.  Para ver un informe de resumen del estado actual de los dispositivos por su estado de compatibilidad, elija **Seguridad** y luego **Atestación de estado**.

3.  Para ver un informe que muestre todos los dispositivos y todos los atributos de atestación de estado, elija **Seguridad** y luego **Atestación de estado**.

## <a name="compliance-policy-rules"></a>Reglas de directivas de cumplimiento
* **Requerir configuración de contraseña en dispositivos móviles**: se puede exigir a los usuarios que escriban una contraseña para poder obtener acceso al dispositivo.

  **Compatible con:**
    * Windows Phone 8+
    * iOS 6+
    * Android 4.0+
    * Samsung KNOX Standard 4.0+

* **Requerir contraseña para desbloquear un dispositivo inactivo**: se puede exigir a los usuarios que escriban una contraseña para obtener acceso a un dispositivo bloqueado.

  **Compatible con:**
  * Windows Phone 8+
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+

* **Minutos de inactividad antes de que se pida la contraseña**: se puede especificar el tiempo de inactividad que transcurre antes de que el usuario deba volver a escribir la contraseña. Establezca el valor en una de las opciones disponibles: **1 minuto**, **5 minutos**, **15 minutos**, **30 minutos** o **1 hora**.

  Esta regla se debe usar con **Requerir una contraseña para desbloquear un dispositivo inactivo**. El valor establecido aquí determina cuándo el dispositivo se considera inactivo y está bloqueado. Cuando **Requerir contraseña para desbloquear un dispositivo inactivo** está establecido en **Verdadero**, el usuario debe escribir una contraseña para acceder al dispositivo bloqueado.

  **Compatible con:**
  * Windows Phone 8+
  * Windows RT/8.1
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+

* **Requerir actualizaciones automáticas**: se puede exigir que los dispositivos con Windows 8.1 o versiones posteriores instalen las actualizaciones de forma automática y especificar de qué clase.

  El valor se debe establecer en **Ninguno** para evitar la instalación automática. Se puede establecer en **Recomendado** para instalar automáticamente todas las actualizaciones recomendadas. Para instalar solo las actualizaciones clasificadas como importantes, se establece en **Importante**.

  **Compatible con:**
  * Windows Phone 8+

* **Permitir contraseñas sencillas**: se puede permitir a los usuarios crear contraseñas sencillas como "1234" o "1111". Esta configuración está deshabilitada de manera predeterminada.

  **Compatible con:**
  * Windows Phone 8+
  * iOS 6+

* **Longitud mínima de contraseña**: se puede especificar el número mínimo de dígitos o caracteres que debe tener la contraseña del usuario (seis de manera predeterminada).

  **Compatible con:**
  * Windows Phone 8+
  * Windows 8.1
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+

  >[!NOTE]
  >En los dispositivos que ejecutan Windows y están protegidos con una cuenta de Microsoft, la directiva de cumplimiento no podrá evaluarse correctamente si la **longitud mínima de la contraseña** es superior a 8 caracteres o el **número mínimo de conjuntos de caracteres** es superior a 2.

* **Cifrado de archivos en dispositivo móvil**: se puede exigir el cifrado del dispositivo para conectarse a los recursos. Los dispositivos que ejecutan Windows Phone 8 se cifran automáticamente. Los dispositivos que ejecutan iOS se cifran al configurar la opción **Requerir configuración de contraseña en dispositivos móviles**. Esta opción está habilitada de forma predeterminada.

  **Compatible con:**
  * Windows Phone 8+
  * Windows 8.1
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+

* **El dispositivo no debe estar liberado ni modificado**: si se habilita esta configuración, los dispositivos liberados (iOS) o modificados (Android) no son compatibles. Esta configuración está deshabilitada de manera predeterminada.

  **Compatible con:**
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+

* **El perfil de correo electrónico debe administrarse mediante Intune**: cuando esta opción se establece en **Sí**, el dispositivo debe usar el perfil de correo electrónico implementado en el dispositivo. El dispositivo se considerará no compatible si el perfil de correo electrónico no está implementado en el mismo grupo de usuarios que el grupo de usuarios al que va dirigida la directiva de compatibilidad.

  También será no compatible si el usuario ya ha configurado en él una cuenta de correo electrónico que coincide con el perfil de correo electrónico de Intune implementado en dicho dispositivo. En este caso, Intune no puede sobrescribir el perfil aprovisionado por el usuario y, por tanto, no puede administrarlo. Para que el dispositivo sea compatible, el usuario puede eliminar la configuración de correo electrónico existente, lo que permite a Intune instalar el perfil de correo electrónico administrado.

  Para obtener información sobre los perfiles de correo electrónico, consulte [Habilitar el acceso al correo electrónico corporativo mediante perfiles de correo electrónico con Microsoft Intune](https://technet.microsoft.com/library/dn800672.aspx). Esta configuración está deshabilitada de manera predeterminada.

  **Compatible con:**
  * iOS 6+

* **Perfil de correo electrónico**: si se selecciona la opción **El perfil de correo electrónico debe administrarse mediante Intune**, haga clic en **Seleccionar** para elegir el perfil de correo mediante el que se deben administrar los dispositivos. El perfil de correo electrónico debe estar presente en el dispositivo.

  **Compatible con:**
  * iOS 6+

* **SO mínimo requerido**: cuando un dispositivo no cumpla el requisito de versión de SO mínima que se especifique, se notificará como no compatible. Además, se mostrará un vínculo con información sobre cómo actualizar el sistema. El usuario puede optar por actualizar el dispositivo, tras lo cual podrá acceder a los recursos de la empresa.

  **Compatible con:**
  * Windows Phone 8+
  * Windows 8.1
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+

* **Versión de SO máxima permitida**: cuando un dispositivo usa una versión de SO posterior a la que se especifica en la regla, se bloquea el acceso a los recursos de la empresa y se solicita al usuario que se ponga en contacto con el administrador de TI. Mientras no se cambie la regla para permitir la versión de SO, este dispositivo no podrá usarse para acceder a los recursos de la empresa.

  **Compatible con:**
  * Windows Phone 8+
  * Windows 8.1
  * iOS 6+
  * Android 4.0+
  * Samsung KNOX Standard 4.0+

* **Requerir que se informe del estado correcto de los dispositivos**: se puede establecer una regla para exigir que se informe del estado correcto de los dispositivos Windows 10 en las directivas de cumplimiento nuevas o existentes. Si habilita esta configuración, los dispositivos Windows 10 se evalúan a través del servicio de atestación de estado (HAS) con respecto a los siguientes puntos de datos:

  - **BitLocker está habilitado**: cuando BitLocker está activado, el dispositivo puede proteger los datos almacenados en la unidad frente al acceso no autorizado cuando el sistema está apagado o entra en estado de hibernación.

   El Cifrado de unidad BitLocker de Windows cifra todos los datos almacenados en el volumen del sistema operativo Windows. BitLocker usa el TPM para ayudar a proteger el sistema operativo Windows y los datos de usuario. Ayuda a garantizar que un equipo no se manipule, incluso si se deja desatendido, se pierde o se lo roban.
   
   Si el equipo está equipado con un TPM compatible, BitLocker usa este para bloquear las claves de cifrado que protegen los datos. Como resultado, las claves no son accesibles hasta que el TPM ha comprobado el estado del equipo.

  - **Está habilitada la integridad del código**: la integridad de código es una característica que valida la integridad de un controlador o un archivo del sistema cada vez que se carga en memoria. La integridad de código detecta si se está cargando un archivo de sistema o controlador sin firma en el kernel. También detecta si un archivo de sistema se ha cambiado por software malintencionado que se ejecuta mediante una cuenta de usuario con privilegios de administrador.

  - **Está habilitado el arranque seguro**: cuando el arranque seguro está habilitado, se obliga al sistema a arrancar en un estado de confianza de fábrica. Además, cuando el arranque seguro está habilitado, los componentes principales que se utilizan para iniciar el equipo deben tener las firmas de cifrado correctas en las que confía la organización que ha fabricado el dispositivo. El firmware UEFI comprueba esto antes de permitir que se inicie el equipo. Si los archivos han sido alterados, vulnerando su firma, el sistema no se iniciará.

  - **El antimalware de inicio temprano está habilitado**: esta configuración solo se aplica a PC. El antimalware de inicio temprano (ELAM) proporciona protección para los equipos de la red cuando se inician y antes de que se inicialicen los controladores de terceros.
  
   Esta regla está desactivada de forma predeterminada.

  Para más información sobre cómo funciona el servicio HAS, consulte [Health Attestation CSP](https://msdn.microsoft.com/library/dn934876.aspx)(CSP de atestación de estado).

  **Compatible con:**
  * Windows 10 y Windows 10 Mobile

> [!NOTE]
> A partir de Configuration Manager 1802, en el Centro de software se muestra el elemento Atestación de estado con el que el dispositivo no es compatible. <!--1235616--> 
![Cumplimiento de Atestación de estado del dispositivo en el Centro de software](./media/Software-Center-noncompliant.PNG)


- **Aplicaciones que no se pueden instalar en el dispositivo**: si los usuarios instalan una aplicación de la lista de aplicaciones no compatibles del administrador, se les bloqueará al intentar obtener acceso al correo electrónico corporativo y a otros recursos corporativos que admiten el acceso condicional. Esta regla requiere el nombre y el identificador de la aplicación al agregar una aplicación a la lista de aplicaciones no compatibles definida por el administrador. También se puede agregar el publicador de la aplicación, pero no es obligatorio.

    **Compatible con:**
      * iOS 6+
      * Android 4.0+
      * Samsung KNOX Standard 4.0+
<br></br>
* **Tipo de contraseña requerida**: especifica si el usuario debe crear una contraseña numérica o alfanumérica. En el caso de las contraseñas alfanuméricas, puede especificar también el número mínimo de juegos de caracteres que debe tener la contraseña. Los cuatro juegos de caracteres son: letras minúsculas, letras mayúsculas, símbolos y números.

    **Compatible con:**
    * Windows Phone 8+
    * Windows 8.1+
    * iOS 6+
<br></br>
* **Bloquear depuración USB en el dispositivo**: no es necesario configurar este parámetro porque la depuración USB ya está deshabilitada en los dispositivos Android for Work.

    **Compatible con:**
    * Android 4.0+
    * Samsung KNOX Standard 4.0+
<br></br>
* **Bloquear aplicaciones de orígenes desconocidos**: requerir que los dispositivos impidan la instalación de aplicaciones desde orígenes desconocidos. No es necesario configurar este valor, ya que los dispositivos Android for Work siempre restringen la instalación de orígenes desconocidos.

    **Compatible con:**
    * Android 4.0+
    * Samsung KNOX Standard 4.0+
<br></br>
* **Requerir examen de amenazas en las aplicaciones**: este valor especifica que la característica Verificar aplicaciones está habilitada en el dispositivo. 

    **Compatible con:**
    * Android 4.2 hasta 4.4
    * Samsung KNOX Standard 4.0+

### <a name="find-an-app-id"></a>Búsqueda de un identificador de aplicación

El identificador de la aplicación es un identificador que identifica de forma única la aplicación en los servicios de aplicaciones de Apple y Google. Un ejemplo es com.contoso.myapp. Para buscar uno:

- **Android**
    - Puede buscar el identificador de la aplicación en la dirección URL de la tienda Google Play Store utilizada para crear la aplicación. Un ejemplo de identificador de aplicación es *…?id=com.companyname.appname&hl=en*

- **iOS**
    1. En la dirección URL de la tienda iTunes, busque el número de identificador, como este del ejemplo: */id875948587?mt=8*

    2. En un explorador web, vaya a la dirección URL siguiente, reemplazando el número por el número de identificador que acaba de encontrar (en este caso, el ejemplo anterior): https://itunes.apple.com/lookup?id=875948587

    3. Descargue y abra el archivo de texto.
  
    4. Busque el texto **bundleid**.

    Un ejemplo de identificador de aplicación es "*bundleId*":"*com.companyname.appname*" 

