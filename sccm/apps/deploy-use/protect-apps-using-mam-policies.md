---
title: "Proteger aplicaciones mediante directivas de administración de aplicaciones móviles | System Center Configuration Manager"
description: Modifique la funcionalidad de las aplicaciones que implemente para que cumplan las directivas de cumplimiento y seguridad de su empresa.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 309b7936-a5ca-45c5-8bef-10424eb2e091
caps.latest.revision: 13
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: dfbf6b2001e3259abb7246ab463682b0ead4f4e8


---
# <a name="protect-apps-using-mobile-application-management-policies-in-system-center-configuration-manager"></a>Proteger aplicaciones mediante directivas de administración de aplicaciones móviles en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Las directivas de administración de aplicaciones de System Center Configuration Manager permiten modificar la funcionalidad de las aplicaciones que se implementen para así ayudar a armonizarlas con las directivas de cumplimiento y seguridad de la compañía. Por ejemplo, puede limitar las operaciones de cortar, copiar y pegar dentro de una aplicación restringida, o configurar una aplicación para abrir todos los vínculos web dentro de un explorador administrado. Las directivas de administración de aplicaciones son compatibles con:  

-   Dispositivos que ejecutan Android 4 y versiones posteriores.  

-   Dispositivos que ejecutan iOS 7 y versiones posteriores.  

Además de dispositivos administrados, puede usar directivas de administración de aplicaciones móviles para proteger las aplicaciones en dispositivos que no estén administrados por Intune. Con esta nueva capacidad, puede aplicar directivas de administración de aplicaciones móviles en aplicaciones que se conecten a los servicios de Office 365. Esto no se admite en aplicaciones que se conecten a Exchange o SharePoint local.  
Para usar esta nueva capacidad, debe usar el portal de vista previa de Azure. Los siguientes temas le ayudarán a empezar a trabajar:  
-   [Introducción a las directivas de administración de aplicaciones móviles en el portal de Azure](https://technet.microsoft.com/library/mt627830.aspx)  
-   [Crear e implementar directivas de administración de aplicaciones móviles con Microsoft Intune](https://technet.microsoft.com/library/mt627829.aspx)  

A diferencia de los elementos de configuración y las líneas base de Configuration Manager, las directivas de administración de aplicaciones no se implementan directamente. En su lugar, debe asociar la directiva con el tipo de implementación de aplicación que desea restringir. Cuando el tipo de implementación de aplicación se implemente y se instale en dispositivos, se aplicará la configuración especificada.  

Para aplicar restricciones a una aplicación, esta debe incorporar el Kit de desarrollo de software (SDK) para aplicaciones de Microsoft Intune. Existen dos métodos de obtención de este tipo de aplicación:  

-   **Usar una aplicación administrada por directivas** (Android e iOS): tiene integrado el SDK de la aplicación. Para agregar este tipo de aplicación, especifique un vínculo a la aplicación desde una tienda de aplicaciones como, por ejemplo, iTunes Store o Google Play. No es necesario ningún procesamiento adicional para este tipo de aplicación. Para obtener una lista de aplicaciones administradas por directiva disponibles para dispositivos iOS y Android, consulte [Aplicaciones administradas de directivas de administración de aplicaciones móviles de Microsoft Intune](https://technet.microsoft.com/en-us/library/dn708489.aspx).  

-   **Usar una aplicación "ajustada"** (Android e iOS): las aplicaciones se vuelven a empaquetar para incluir el SDK de la aplicación mediante la **herramienta de ajuste de aplicaciones de Microsoft Intune**. Esta herramienta se usa normalmente para procesar aplicaciones de empresa que se hayan creado internamente. No se puede usar para procesar aplicaciones que se hayan descargado desde la tienda de aplicaciones. Consulte [Preparar aplicaciones iOS para la administración de aplicaciones móviles con la herramienta de ajuste de aplicaciones de Microsoft Intune](https://technet.microsoft.com/en-us/library/dn878028.aspx) y [Preparar aplicaciones de Android para la administración de aplicaciones móviles con la herramienta de ajuste de aplicaciones de Microsoft Intune](https://technet.microsoft.com/en-us/library/mt147413.aspx).  

## <a name="create-and-deploy-an-app-with-a-mobile-application-management-policy"></a>Crear e implementar una aplicación con una directiva de administración de aplicaciones móviles  
  
##  <a name="step-1-obtain-the-link-to-a-policy-managed-app-or-create-a-wrapped-app"></a>Paso 1: obtenga el vínculo a una aplicación administrada por directivas o cree una aplicación ajustada  

-   **Para obtener un vínculo a una aplicación administrada por directiva** : desde la tienda de aplicaciones, busque y anote la dirección URL de la aplicación administrada por directiva que desea implementar.  

     Por ejemplo, la dirección URL de la aplicación Microsoft Word para iPad es **https://itunes.apple.com/us/app/microsoft-word-for-ipad/id586447913?mt=8**  

-   **Para crear una aplicación ajustada** : use la información de los temas [Preparar aplicaciones iOS para la administración de aplicaciones móviles con la herramienta de ajuste de aplicaciones de Microsoft Intune](https://technet.microsoft.com/en-us/library/dn878028.aspx) y [Preparar aplicaciones de Android para la administración de aplicaciones móviles con la herramienta de ajuste de aplicaciones de Microsoft Intune](https://technet.microsoft.com/en-us/library/mt147413.aspx) para crear una aplicación ajustada.  

     La herramienta crea una aplicación procesada y un archivo de manifiesto asociado. Usará estos archivos al crear una aplicación de Configuration Manager que contenga la aplicación.  

##  <a name="step-2-create-a-configuration-manager-application-that-contains-an-app"></a>Paso 2: cree una aplicación de Configuration Manager que contenga una aplicación  
 El procedimiento para crear la aplicación de Configuration Manager difiere en función de si usa una aplicación administrada por directiva (vínculo externo) o una aplicación creada con la herramienta de ajuste de aplicaciones de Microsoft Intune para iOS (paquete de aplicación de iOS). Use uno de los procedimientos siguientes para crear la aplicación de Configuration Manager.  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software** > **Administración de aplicaciones** > **Aplicaciones**.  

3.  En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear aplicación** para abrir el Asistente para crear aplicaciones.  

4.  En la página **General** , seleccione **Detectar automáticamente la información sobre esta aplicación a partir de archivos de instalación**.  

5.  En la lista desplegable **Tipo**, seleccione **Paquete de aplicación para iOS (\*archivo *.ipa)**.  

6.  Haga clic en **Examinar** para seleccionar el paquete de aplicación que desee importar y, a continuación, haga clic en **Siguiente**.  

7.  En la página **Información general** , escriba la información de categoría y texto descriptivo que desea que los usuarios vean en el portal de la compañía.  

8.  Complete el asistente.  

 La nueva aplicación se muestra en el nodo **Aplicaciones** del área de trabajo **Biblioteca de software** .  
  
### <a name="create-an-application-containing-a-link-to-a-policy-managed-app"></a>Crear una aplicación que contenga un vínculo a una aplicación administrada por directiva  
  
1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software** > **Administración de aplicaciones** > **Aplicaciones**.  
  
3.  En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear aplicación** para abrir el Asistente para crear aplicaciones.  

4.  En la página **General** , seleccione **Detectar automáticamente la información sobre esta aplicación a partir de archivos de instalación**.  

5.  En la lista desplegable **Tipo** , seleccione una de las opciones siguientes:  

    -   Para iOS: **paquete de aplicaciones para iOS en la App Store**  

    -   Para Android: **paquete de aplicaciones para Android en Google Play**  

6.  Escriba la dirección URL de la aplicación (del paso 1) y, a continuación, haga clic en **Siguiente**.  

7.  En la página **Información general** , escriba la información de categoría y texto descriptivo que desea que los usuarios vean en el portal de la compañía.  

8.  Complete el asistente.  

 La nueva aplicación se muestra en el nodo **Aplicaciones** del área de trabajo **Biblioteca de software** .  

##  <a name="step-3-create-an-application-management-policy"></a>Paso 3: cree una directiva de administración de aplicaciones  
 A continuación, creará una directiva de administración de aplicaciones que asociará a la aplicación. Puede crear una directiva de explorador general o administrado.  
  
1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software** > **Administración de aplicaciones** > **Directivas de administración de aplicaciones**.  
3.  En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear directiva de administración de aplicaciones**.  

4.  En la página **General** , escriba el nombre y la descripción de la directiva y haga clic en **Siguiente**.  

5.  En la página **Tipo de directiva** , seleccione la plataforma y el tipo de directiva y haga clic en **Siguiente**. Los siguientes tipos de directiva están disponibles:  

    -   **General**: el tipo de directiva “General” le permite modificar la funcionalidad de las aplicaciones que implementa para que se ajusten a los requisitos de cumplimiento y las directivas de seguridad de su empresa. Por ejemplo, puede restringir las operaciones de cortar, copiar y pegar en una aplicación restringida.  

    -   **Explorador administrado**: configure si se debe permitir o no que el explorador administrado abra una lista de direcciones URL. El tipo de directiva de explorador administrado permite modificar la funcionalidad de la aplicación de explorador administrado de Intune. Se trata de un explorador web que permite administrar las acciones que pueden realizar los usuarios, incluidos los sitios que pueden visitar y cómo se abren los vínculos a contenido en el explorador. Obtenga más información sobre la  [aplicación Intune Managed Browser para iOS](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8) y [la aplicación Intune Managed Browser para Android](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser&hl=en).  

6.  En la página **Directiva de iOS** o **Directiva de Android** , configure los valores siguientes según sea necesario y, a continuación, haga clic en **Siguiente**. Las opciones pueden diferir en función del tipo de dispositivo para el que va a configurar la directiva.  

|Valor|Más información|  
|-----------|----------------------|  
|**Restringir contenido web para mostrar en un explorador administrado corporativo**|Cuando se habilita esta configuración, los vínculos en la aplicación se abrirán en el explorador administrado. Debe haber implementado esta aplicación en dispositivos para que esta opción funcione.|  
|**Impedir copias de seguridad de Android** o **Impedir copias de seguridad de iTunes e iCloud**|Deshabilita la copia de seguridad de cualquier información procedente de la aplicación.|  
|**Permitir que la aplicación transfiera datos a otras aplicaciones**|Especifica las aplicaciones a las que esta aplicación puede enviar datos. Puede elegir no permitir la transferencia de datos a ninguna aplicación, permitir solo la transferencia a otras aplicaciones restringidas o permitir la transferencia a cualquier aplicación.<br /><br /> Para dispositivos iOS, para evitar la transferencia de documentos entre aplicaciones administradas y no administradas, debe también configurar e implementar una directiva de seguridad de dispositivos móviles que deshabilite la configuración **Permitir documentos administrados en otras aplicaciones no administradas**.<br /><br /> Si selecciona permitir solo la transferencia a otras aplicaciones restringidas, se usarán los visores Image Viewer y PDF Viewer de Intune (si se implementaron) para abrir el contenido de los tipos respectivos.|  
|**Permitir que la aplicación reciba datos de otras aplicaciones**|Especifica las aplicaciones de las que esta aplicación puede recibir datos. Puede elegir no permitir la transferencia de datos desde ninguna aplicación, permitir solo la transferencia desde otras aplicaciones restringidas o permitir la transferencia desde cualquier aplicación.|  
|**Impedir "Guardar como..."**|Deshabilita el uso de la opción **Guardar como...** en cualquier aplicación que use esta directiva.|  
|**Restringir cortar, copiar y pegar con otras aplicaciones**|Especifica cómo pueden usarse las operaciones de cortar, copiar y pegar con la aplicación. Elija de entre las siguientes opciones:<br /><br /> **Bloqueada** : no permitir operaciones de cortar, copiar y pegar entre esta aplicación y otras aplicaciones.<br /><br /> **Aplicaciones administradas por directiva** : permitir solo operaciones de cortar, copiar y pegar entre esta aplicación y otras aplicaciones restringidas.<br /><br /> **Aplicaciones administradas por directiva con Pegar en** : permitir que los datos cortados o copiados desde esta aplicación solo se peguen en otras aplicaciones restringidas. Permitir que los datos cortados o copiados desde cualquier aplicación se peguen en esta aplicación.<br /><br /> **Cualquier aplicación** : sin restricciones para las operaciones de cortar, copiar y pegar en esta aplicación o desde ella.|  
|**Requerir PIN simple en acceso**|Requiere que el usuario escriba un número PIN que especifica al usar esta aplicación. Se pedirá al usuario que lo configure la primera vez que ejecuta la aplicación.|  
|**Número de intentos antes de restablecimiento del PIN**|Especifique el número de intentos de entrada de PIN que pueden realizarse antes de que el usuario deba restablecer el PIN.|  
|**Requerir credenciales corporativas en acceso**|Requiere que el usuario deba introducir su información de inicio de sesión corporativa para tener acceso a la aplicación.|  
|**Requerir cumplimiento de dispositivos con la directiva corporativa en acceso**|Solo permite que se use la aplicación cuando el dispositivo no está liberado ni modificado.|  
|**Volver a comprobar los requisitos de acceso después de (minutos)**|En el campo **Tiempo de espera** , especifique el período de tiempo que debe transcurrir antes de que se vuelvan a comprobar los requisitos de acceso de la aplicación una vez iniciada la aplicación.<br /><br /> En el campo **Período de gracia sin conexión** , si el dispositivo está desconectado, especifique el período de tiempo que debe transcurrir antes de que se vuelvan a comprobar los requisitos de acceso de la aplicación.|  
|**Cifrar datos de aplicación**|Especifica que se cifren todos los datos asociados a esta aplicación, incluidos los datos almacenados externamente como, por ejemplo, tarjetas SD.<br /><br /> **Cifrado para iOS**<br /><br /> En el caso de aplicaciones que están asociadas a una directiva de administración de aplicaciones móviles de Configuration Manager, los datos se cifran en reposo con el cifrado de nivel de dispositivo proporcionado por el sistema operativo. Esta opción se habilita a través de la directiva de PIN del dispositivo que debe establecer el administrador de TI. Cuando se requiere un PIN, los datos se cifrarán según la configuración de la directiva de administración de aplicaciones móviles. Como se indica en la documentación de Apple, [los módulos usados por iOS 7 están certificados mediante FIPS 140-2](http://support.apple.com/en-us/HT202739).<br /><br /> **Cifrado para Android**<br /><br /> En el caso de las aplicaciones que están asociadas a una directiva de administración de aplicaciones móviles de Configuration Manager, Microsoft proporciona el cifrado. Los datos se cifran de forma sincrónica durante las operaciones de E/S de archivos según la configuración de la directiva de administración de aplicaciones móviles. Las aplicaciones administradas en Android usan el cifrado AES-128 en modo CBC mediante las bibliotecas de criptografía de la plataforma. El método de cifrado no está certificado mediante FIPS 140-2. Siempre se cifrará el contenido del almacenamiento del dispositivo.|  
    |**Bloquear captura de pantalla** (solo en dispositivos Android)|Especifica que las funciones de captura de pantalla del dispositivo se bloquean cuando se usa esta aplicación.|  

7.  En la página **Explorador administrado** , seleccione si permite que el explorador administrado abra solo las direcciones URL de la lista o si bloquea el explorador administrado para que no las abra, administre las direcciones URL de la lista y, a continuación, haga clic en **Siguiente**.  

    > [!WARNING]  
    >  Para obtener más información, consulte [Administrar el acceso a Internet mediante directivas de explorador administrado con Configuration Manager](../../apps/deploy-use/manage-internet-access-using-managed-browser-policies.md).  
  
8.  Complete el asistente.  

 La directiva nueva se muestra en el nodo **Directivas de administración de aplicaciones** del área de trabajo **Biblioteca de software** .  

##  <a name="step-4-associate-the-application-management-policy-with-a-deployment-type"></a>Paso 4: asocie la directiva de administración de aplicaciones con un tipo de implementación  
 
 Cuando se crea un tipo de implementación para una aplicación que requiere una directiva de administración de aplicaciones, Configuration Manager reconocerá que una directiva de administración de aplicaciones debe vincularse a este tipo de implementación cuando se implemente la aplicación asociada y le solicitará que asocie una directiva de administración de aplicaciones. Se le solicitará que asocie una directiva general y una directiva de explorador administrado para el explorador administrado. Para obtener más información, consulte [Create applications](../../apps/deploy-use/create-applications.md) (Crear aplicaciones).  
  
> [!IMPORTANT]  
>  Si la aplicación ya está implementada, se producirá un error en la implementación del nuevo tipo de implementación hasta que se realice esta asociación. Puede realizar la asociación en **Propiedades** de la aplicación, en la pestaña **Administración de aplicaciones** .  

> [!IMPORTANT]  
>  En el caso de dispositivos que ejecutan sistemas operativos anteriores a iOS 7.1, las directivas asociadas no se quitarán al desinstalar la aplicación.  
>   
>  Si se anula la inscripción del dispositivo en Configuration Manager, las directivas no se quitan de las aplicaciones. Las aplicaciones que tenían directivas aplicadas conservarán la configuración de las directivas, incluso si la aplicación se desinstala y se vuelve a instalar.  

##  <a name="step-5-monitor-the-app-deployment"></a>Paso 5: supervise la implementación de la aplicación  
 Cuando cree e implemente una aplicación asociada a una directiva de administración de aplicaciones móviles, puede supervisar la aplicación y resolver los conflictos de directivas.  
  
1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software** > **Introducción** > **Implementaciones**.  
  
3.  Seleccione la implementación y, en la pestaña **Inicio** , haga clic en **Propiedades**.  

4.  En el panel de detalles de la implementación, haga clic en **Directivas de administración de aplicaciones** en **Objetos relacionados**.  

 Para obtener más información sobre la supervisión de aplicaciones, consulte [Monitor applications](/sccm/apps/deploy-use/monitor-applications-from-the-console) (Supervisar aplicaciones).  

##  <a name="how-policy-conflicts-are-resolved"></a>Cómo se resuelven los conflictos de directivas  
 Cuando hay un conflicto de directivas de administración de aplicaciones móviles en la primera implementación para el usuario o el dispositivo, el valor específico de la configuración en conflicto se quitará de la directiva implementada en la aplicación y la aplicación usará un valor de conflicto integrado.  

 Cuando hay un conflicto de directivas de administración de aplicaciones móviles en implementaciones posteriores para la aplicación o el usuario, el valor específico de la configuración en conflicto no se actualizará en la directiva de administración de aplicaciones móviles implementada para la aplicación y la aplicación usará el valor existente para dicha configuración.  

 En casos en los que el dispositivo o el usuario recibe dos directivas en conflicto, se aplica el comportamiento siguiente:  

-   Si ya se implementó una directiva para el dispositivo, la configuración de directiva existente no se sobrescribe.  

-   Si todavía no se implementó ninguna directiva para el dispositivo y se implementan dos configuraciones en conflicto, se usa la configuración predeterminada integrada en el dispositivo.  

##  <a name="available-policy-managed-apps"></a>Aplicaciones administradas por directiva disponibles  
 Para obtener una lista de aplicaciones administradas por directiva que están disponibles para dispositivos iOS y Android, consulte [Partners de aplicaciones de Microsoft Intune](https://www.microsoft.com/en-us/cloud-platform/microsoft-intune-partners).  



<!--HONumber=Nov16_HO1-->


