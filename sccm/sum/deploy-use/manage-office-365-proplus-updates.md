---
title: Administrar las actualizaciones de Office 365 ProPlus | Microsoft Docs
description: "Configuration Manager sincroniza las actualizaciones de cliente de Office 365 desde el catálogo WSUS en el servidor de sitio para que las actualizaciones estén disponibles para su implementación en los clientes."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 03/24/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: eac542eb-9aa1-4c63-b493-f80128e4e99b
ms.translationtype: Human Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: 016580dc6ee3c5268833db941d42416a976d201c
ms.contentlocale: es-es
ms.lasthandoff: 05/17/2017

---

# <a name="manage-office-365-proplus-with-configuration-manager"></a>Administración de Office 365 ProPlus con Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Configuration Manager sincroniza las actualizaciones de cliente de Office 365 y las habilita para implementarlas en los clientes con Office 365 instalado. A partir de la versión 1610 de Configuration Manager, puede revisar la información del cliente de Office 365 en el panel Administración de clientes de Office 365.

A partir de la versión 1602, Configuration Manager tiene la capacidad de administrar las actualizaciones del cliente de Office 365 mediante el flujo de trabajo de administración de actualizaciones de software. Cuando Microsoft publica una nueva actualización de cliente de Office 365 en Content Delivery Network (CDN) de Office, Microsoft también publica un paquete de actualización para Windows Server Update Services (WSUS). Después de que Configuration Manager sincroniza la actualización de cliente de Office 365 desde el catálogo WSUS en el servidor de sitio, la actualización está disponible para implementarla en los clientes.

A partir de la versión 1702, puede iniciar el Instalador de Office 365 desde el panel Administración de clientes de Office 365 para facilitar la experiencia de instalación inicial de la aplicación Office 365. El asistente permite configurar opciones de instalación de Office 365, descargar archivos desde redes de entrega de contenido (CDN) de Office y crear e implementar una aplicación de script con el contenido.

## <a name="office-365-client-management-dashboard"></a>Panel de administración de clientes de Office 365  
A partir de Configuration Manager versión 1610, el panel de administración de clientes de Office 365 está disponible en la consola de Configuration Manager. Para ver el panel, vaya a **Biblioteca de software** > **Información general** > **Administración de clientes de Office 365**.

El panel muestra gráficos para lo siguiente:

- Número de clientes de Office 365
- Versiones de cliente de Office 365
- Idiomas de cliente de Office 365
- Canales de cliente de Office 365     
Para más información, vea [Información general de los canales de actualización para Office 365 ProPlus](https://technet.microsoft.com/library/mt455210.aspx).
<!--- - Automatic deployment rules with Office 365 apps (have Office 365 Client selected in the set of available products). --->

<!---You can take the following actions on the dashboard:
- --->

En la parte superior del panel, use la opción desplegable **Colección** para filtrar los datos del panel por miembros de una colección determinada.

### <a name="display-data-in-the-office-365-client-management-dashboard"></a>Mostrar datos en el panel de administración de clientes de Office 365
Los datos que se muestran en el panel de administración de clientes de Office 365 proceden de inventario de hardware. El inventario de hardware debe estar habilitado y debe seleccionar la clase de inventario de hardware **Configuración de Office 365 ProPlus** antes de que aparezcan en el panel de datos.
#### <a name="to-display-data-in-the-office-365-client-management-dashboard"></a>Para mostrar datos en el panel de administración de clientes de Office 365
1. Habilite el inventario de hardware, si aún no está habilitado. Para obtener más información, consulte [Configurar el inventario de hardware](\sccm\core\clients\manage\configure-hardware-inventory).
2. En la consola de Configuration Manager, navegue a **Administración** > **Configuración de cliente** > **Configuración de cliente predeterminada**.  
3. En la pestaña **Inicio** , en el grupo **Propiedades** , haga clic en **Propiedades**.  
4. En el **configuración de cliente predeterminada** cuadro de diálogo, haga clic en **de inventario de Hardware**.  
5. En el **configuración de dispositivo** lista, haga clic en **establecer clases**.  
6. En el cuadro de diálogo **Clases de inventario de hardware**, seleccione **Configuración de Office 365 ProPlus**.  
7.  Haga clic en **Aceptar** para guardar los cambios y cerrar la **clases de inventario de Hardware** cuadro de diálogo.  
El panel de administración de cliente de Office 365 comenzará a mostrar los datos a medida que se informe del inventario de hardware.

## <a name="deploy-office-365-updates-with-configuration-manager"></a>Implementar actualizaciones de Office 365 con Configuration Manager
Siga estos pasos para implementar actualizaciones de Office 365 con Configuration Manager:

1.  [Compruebe los requisitos](https://technet.microsoft.com/library/mt628083.aspx) para usar Configuration Manager para administrar las actualizaciones de cliente de Office 365 en la sección **Requisitos para usar Configuration Manager para administrar las actualizaciones de cliente de Office 365** del tema.  

2.  [Configurar puntos de actualización de software](../get-started/configure-classifications-and-products.md) para sincronizar las actualizaciones de cliente de Office 365. Definir las **actualizaciones** para la clasificación y seleccionar el **cliente de Office 365** para el producto. Es posible que deba sincronizar actualizaciones de software al menos una vez antes de que el producto Office 365 Client esté disponible para elegirlo. Debe sincronizar las actualizaciones de software después de configurar los puntos de actualización de software para usar la clasificación **Actualizaciones**.
3.  Permita que los clientes de Office 365 reciban actualizaciones de Configuration Manager. Puede hacerlo mediante la configuración de cliente de Configuration Manager o la directiva de grupo. Utilice uno de los métodos siguientes para habilitar el cliente:  
    - Método 1: a partir de Configuration Manager versión 1606, puede usar la configuración de cliente de Configuration Manager para administrar el agente cliente de Office 365. Después de configurar esta opción e implementar las actualizaciones de Office 365, el agente cliente de Configuration Manager se comunica con el de Office 365 para descargar las actualizaciones de Office 365 desde un punto de distribución e instalarlas. Configuration Manager realiza un inventario de la configuración de cliente de Office 365 ProPlus.
      1.  En la consola de Configuration Manager, haga clic en **Administración** > **Información general** > **Configuración de cliente**.  

      2.  Abra la configuración de dispositivo adecuada para habilitar el agente cliente. Para más información sobre las configuraciones de cliente personalizada y predeterminada, vea [Cómo establecer la configuración del cliente en Configuration Manager](../../core/clients/deploy/configure-client-settings.md).  

      3.  Haga clic en **Actualizaciones de software** y seleccione **Sí** para el valor **Habilitar administración del Agente cliente de Office 365**.  

    - Método 2: [permitir a los clientes de Office 365 recibir actualizaciones](https://technet.microsoft.com/library/mt628083.aspx#BKMK_EnableClient) de Configuration Manager mediante la herramienta de implementación de Office o la directiva de grupo.  

4. [Implemente actualizaciones de Office 365](deploy-software-updates.md) en los clientes.   

> [!Important]
> Cuando tiene un cliente de Office 365 con más de un idioma y descarga actualizaciones en menos idiomas, no podrá instalar las actualizaciones. Por ejemplo, supongamos que tiene un cliente de Office 365 con en-us y de-de. En el servidor de sitio, puede descargar e implementar solo contenido en en-us para una actualización de Office 365 aplicable. Cuando el usuario inicia la instalación de esta actualización desde el Centro de software, la actualización se bloqueará mientras se descarga el contenido. Debe descargar e implementar las actualizaciones en los mismos idiomas que los clientes de Office 365.  


## <a name="add-other-languages-for-office-365-update-downloads"></a>Agregar otros idiomas para descargas de actualización de Office 365
A partir de la versión 1610 de Configuration Manager, puede configurar Configuration Manager para descargar actualizaciones de los idiomas compatibles con Office 365, independientemente de si son compatibles con Configuration Manager.
> [!IMPORTANT]  
> La configuración de idiomas de actualización de Office 365 adicionales es una configuración global del sitio. Después de agregar los idiomas con el procedimiento siguiente, todas las actualizaciones de Office 365 se descargarán en esos idiomas, así como en los idiomas que seleccione en la página Selección de idioma del Asistente para descarga de actualizaciones de software o el Asistente para implementación de actualizaciones de software.

### <a name="to-add-support-to-download-updates-for-additional-languages"></a>Para agregar compatibilidad para descargar actualizaciones de idiomas adicionales
Siga este procedimiento en el sitio de administración central o el sitio primario independiente donde esté instalado el rol de sistema de sitio del punto de actualización de software.
1. Desde el símbolo del sistema, escriba *wbemtest* como usuario administrativo para abrir la Herramienta de comprobación del instrumental de administración de Windows.
2. Haga clic en **Conectar** y, después, escriba *root\sms\site_&lt;códigoDeSitio&gt;*.
3. Haga clic en **Consulta** y, después, ejecute la consulta siguiente: *select &#42; from SMS_SCI_Component where componentname ="SMS_WSUS_CONFIGURATION_MANAGER"*  
   ![Consulta WMI](..\media\1-wmiquery.png)
4. En el panel de resultados, haga doble clic en el objeto con el código de sitio del sitio de administración central o del sitio primario independiente.
5. Seleccione la propiedad **Props**, haga clic en **Editar propiedad** y, después, haga clic en **Ver incrustado**.
![Editor de propiedades](..\media\2-propeditor.png)
6. Empiece en el primer resultado de la consulta y abra cada objeto hasta que encuentre el objeto que tenga **AdditionalUpdateLanguagesForO365** para la propiedad **PropertyName**.
7. Seleccione **Value2** y haga clic en **Editar propiedad**.  
![Editar la propiedad Value2](..\media\3-queryresult.png)
8. Agregue idiomas adicionales a la propiedad **Value2** y haga clic en **Guardar propiedad**.  
Por ejemplo, pt-pt (para portugués de Portugal), af-za (para afrikáans de Sudáfrica), nn-no (para noruego nynorsk de Noruega), etc.  
![Agregar idiomas en el Editor de propiedades](..\media\4-props.png)  
9. Haga clic en **Cerrar**, en **Cerrar** y en **Guardar propiedad**, seleccione **Guardar objeto** (si hace clic en **Cerrar** aquí, se descartarán los valores), seleccione **Cerrar** y, después, haga clic en **Salir** para salir de la Herramienta de comprobación del instrumental de administración de Windows.
10. En la consola de Configuration Manager, vaya a **Biblioteca de software** > **Información general** > **Administración de clientes de Office 365** > **Actualizaciones de Office 365**.
11. Ahora, al descargar las actualizaciones de Office 365, se descartarán en el idioma que seleccione en el asistente y en los idiomas que haya configurado en este procedimiento. Para comprobar que las actualizaciones se han descargado en esos idiomas, vaya al archivo de origen del paquete de la actualización y busque los archivos con el código de idioma en el nombre de archivo.  
![Nombres de archivo con idiomas adicionales](..\media\5-verification.png)


## <a name="change-the-update-channel-after-you-enable-office-365-clients-to-receive-updates-from-configuration-manager"></a>Cambiar el canal de actualización después de permitir que los clientes de Office 365 reciban actualizaciones de Configuration Manager
Para cambiar el canal de actualización después de permitir que los clientes de Office 365 reciban actualizaciones de Configuration Manager, puede usar una directiva de grupo para distribuir un cambio del valor de una clave del Registro en los clientes de Office 365. Cambie la clave del Registro **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\ClickToRun\Configuration\CDNBaseUrl** para que use uno de los valores siguientes:

- Canal actual:  
  **CDNBaseUrl** = http&#58;//officecdn.microsoft.com/pr/492350f6-3a01-4f97-b9c0-c7c6ddf67d60

- Canal diferido:  
  **CDNBaseUrl** = http&#58;//officecdn.microsoft.com/pr/7ffbc6bf-bc32-4f92-8982-f9dd17fd3114

- First Release para Canal actual:  
  **CDNBaseUrl** = http&#58;//officecdn.microsoft.com/pr/64256afe-f5d9-4f86-8936-8840a6a4f5be

- First Release para Canal diferido:  
  **CDNBaseUrl** = http&#58;//officecdn.microsoft.com/pr/b8f9b850-328d-4355-9145-c59439a0c4cf

## <a name="deploy-office-365-apps"></a>Implementación de aplicaciones de Office 365  
A partir de la versión 1702, puede iniciar el Instalador de Office 365 desde el panel Administración de clientes de Office 365 para facilitar la experiencia de instalación inicial de la aplicación Office 365. El asistente permite configurar opciones de instalación de Office 365, descargar archivos desde redes de entrega de contenido (CDN) de Office y crear e implementar una aplicación de script para los archivos.

Esto es especialmente útil porque las actualizaciones de Office 365 no son aplicables para los clientes que no tienen instalado Office 365. Antes de la versión 1702, para instalar aplicaciones de Office 365 por primera vez en los clientes, necesita descargar la herramienta de implementación de Office 365 (ODT) y los archivos de origen de la instalación de Office 365, incluidos todos los paquetes de idioma que necesita, así como generar el archivo XML que especifica la versión y el canal correctos de Office. A continuación, necesitaría crear e implementar un paquete heredado o una aplicación de script para que los clientes instalen las aplicaciones de Office 365.

> [!NOTE]
> - El equipo que ejecuta el Instalador de Office 365 debe tener acceso a Internet.  
> - El usuario que ejecuta el Instalador de Office 365 debe tener acceso de **lectura** y **escritura** para el uso compartido de la ubicación de contenido que se ofrece en el asistente.
> - Si recibe un error de descarga 404, copie los archivos siguientes en la carpeta %temp% del usuario:
>    - [releasehistory.xml](http://officecdn.microsoft.com.edgesuite.net/wsus/releasehistory.cab)
>    - [o365client_32bit.xml](http://officecdn.microsoft.com/pr/wsus/ofl.cab)  
> - Después de crear e implementar aplicaciones de Office 365 mediante el Instalador de Office 365, Configuration Manager no administrará las actualizaciones de Office de forma predeterminada. Para permitir que los clientes de Office 365 reciban actualizaciones de Configuration Manager, vea [Implementar actualizaciones de Office 365 con Configuration Manager](#deploy-office-365-updates-with-configuration-manager).

### <a name="to-deploy-office-365-apps-to-clients-from-the-office-365-client-management-dashboard"></a>Para implementar aplicaciones de Office 365 en clientes desde el panel Administración de clientes de Office 365
1. En la consola de Configuration Manager, vaya a **Biblioteca de software** > **Información general** > **Administración de clientes de Office 365**.
2. Haga clic en **Programa de instalación de Office 365** en el panel superior derecho. Se abre el Asistente para la instalación del cliente de Office 365.
3. En la página **Configuración de la aplicación**, proporcione un nombre y una descripción para la aplicación, escriba la ubicación de descarga de los archivos y haga clic en **Siguiente**. Tenga en cuenta que la ubicación se debe especificar con el formato &#92;&#92;*servidor*&#92;*recurso compartido*.
4. En la página **Importar configuración de cliente**, elija si quiere importar la configuración del cliente de Office 365 desde un archivo de configuración XML existente o especificarla manualmente y, luego, haga clic en **Siguiente**.  

    Si tiene un archivo de configuración existente, escriba su ubicación y vaya al paso 7. Tenga en cuenta que la ubicación se debe especificar con el formato &#92;&#92;*servidor*&#92;*recurso compartido*&#92;*nombre archivo*.XML.
5. En la página **Productos de cliente**, seleccione el conjunto de Office 365 que usa, seleccione las aplicaciones que quiere incluir, seleccione los productos de Office adicionales que deberían incluirse y luego haga clic en **Siguiente**.
6. En la página **Configuración de cliente**, elija la configuración que quiere incluir y luego haga clic en **Siguiente**.
7. En la página **Implementación**, elija si quiere implementar la aplicación y haga clic en **Siguiente**.  
Si decide no implementar el paquete en el asistente, vaya al paso 9.
8. Configure el resto de las páginas del asistente como lo haría para una implementación de aplicación normal. Para obtener más información, consulte [Crear e implementar una aplicación](/sccm/apps/get-started/create-and-deploy-an-application).
9. Complete el asistente.
10. Puede implementar o modificar la aplicación igual que cualquier otra aplicación de Configuration Manager desde **Biblioteca de software** > **Información general** > **Administración de aplicaciones** > **Aplicaciones**.   

> [!IMPORTANT]
> Configuration Manager no administra automáticamente la aplicación de Office 365 creada e implementada con el Asistente para aplicaciones de Office 365 en Configuration Manager hasta que habilite de nuevo la configuración **Habilitar administración del Agente cliente de Office 365** del Agente cliente de actualizaciones de software. Para obtener información detallada, vea [Acerca de la configuración de cliente](/sccm/core/clients/deploy/about-client-settings).

>[!NOTE]
>Después de implementar las aplicaciones de Office 365, puede crear reglas de implementación automática para mantener esas aplicaciones. Para crear una regla de implementación automática para las aplicaciones de Office 365, haga clic en **Crear un ADR** en el panel Administración de clientes de Office 365 y seleccione **Cliente de Office 365** al elegir el producto. Para más información, vea [Implementar actualizaciones de software automáticamente](/sccm/sum/deploy-use/automatically-deploy-software-updates).

<!--- You can create an Office 365 app without using the Office 365 Installation Wizard. To do this, you use the Office 2016 Deployment Tool (ODT) to download Office installation source files to a network share, generate Configure.xml that specifies the correct Office version and channel, and so on. Then, create an app for the files using the normal app management process.
> [!Note]
> The Office 365 Installation Wizard was introduced in Configuration Manager version 1702 and provides an easy way to create Office 365 apps.

- [Download the Office 2016 Deployment Tool](http://aka.ms/ODT2016) from the Microsoft Download Center.  
- Review the [configuration options for the Office Deployment Tool](https://technet.microsoft.com/library/jj219426.aspx).

You can create an application just as you would with any other application in Configuration Manager from **Software Library** > **Overview** > **Application Management** > **Applications**. For details, see [Create and deploy an application](/sccm/apps/get-started/create-and-deploy-an-application).
--->

<!--- ## Next steps
Use the Office 365 Client Management dashboard in Configuration Manager to review Office 365 client information and deploy Office 365 apps. For details, see [Manage Office 365 apps](manage-office-365-apps.md). --->

