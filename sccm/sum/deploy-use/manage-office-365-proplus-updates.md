---
title: "Administración de las actualizaciones de Office 365 ProPlus"
titleSuffix: Configuration Manager
description: "Configuration Manager sincroniza las actualizaciones de cliente de Office 365 desde el catálogo WSUS en el servidor de sitio para que las actualizaciones estén disponibles para su implementación en los clientes."
keywords: 
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 02/16/2018
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: eac542eb-9aa1-4c63-b493-f80128e4e99b
ms.openlocfilehash: 2f765df84b94524cf56f6d1d9e051157f1a325ef
ms.sourcegitcommit: 45ff3ffa040eada5656b17f47dcabd3c637bdb60
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/23/2018
---
# <a name="manage-office-365-proplus-with-configuration-manager"></a>Administración de Office 365 ProPlus con Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Configuration Manager permite administrar aplicaciones de Office 365 ProPlus de las siguientes formas:

- [Panel de administración de clientes de Office 365](#office-365-client-management-dashboard): a partir de la versión 1610 de Configuration Manager, la información de los clientes de Office 365 se puede revisar en el panel de administración de clientes de Office 365.    

- [Implementación de aplicaciones de Office 365](#deploy-office-365-apps): a partir de la versión 1702, se puede iniciar el Instalador de Office 365 desde el panel de administración de clientes de Office 365 para facilitar la instalación inicial de las aplicaciones de Office 365. El asistente permite configurar opciones de instalación de Office 365, descargar archivos desde redes de entrega de contenido (CDN) de Office y crear e implementar una aplicación de script con el contenido.    

- [Implementación de actualizaciones de Office 365](#deploy-office-365-updates): a partir de la versión 1602 de Configuration Manager, se pueden administrar las actualizaciones de cliente de Office 365 mediante el flujo de trabajo de administración de actualizaciones de software. Cuando Microsoft publica una nueva actualización de cliente de Office 365 en Content Delivery Network (CDN) de Office, Microsoft también publica un paquete de actualización para Windows Server Update Services (WSUS). Después de que Configuration Manager sincroniza la actualización de cliente de Office 365 desde el catálogo WSUS en el servidor de sitio, la actualización está disponible para implementarla en los clientes.    

- [Adición de idiomas para descargar actualizaciones de Office 365](#add-languages-for-office-365-update-downloads): a partir de la versión 1610 de Configuration Manager, se puede agregar compatibilidad para Configuration Manager para descargar actualizaciones de los idiomas compatibles con Office 365. Esto significa que no es necesario que Configuration Manager admita el idioma mientras lo haga Office 365. Antes de la versión 1610 de Configuration Manager, debe descargar e implementar actualizaciones en los mismos idiomas configurados en los clientes de Office 365. 

- [Cambio del canal de actualización](#change-the-update-channel-after-you-enable-office-365-clients-to-receive-updates-from-configuration-manager): con este fin, se puede usar una directiva de grupo para distribuir un cambio del valor de una clave del Registro en los clientes de Office 365.


## <a name="office-365-client-management-dashboard"></a>Panel de administración de clientes de Office 365  
El panel de administración de clientes de Office 365 proporciona una serie de gráficos con la siguiente información:

- Número de clientes de Office 365
- Versiones de cliente de Office 365
- Idiomas de cliente de Office 365
- Canales de cliente de Office 365     
  Para más información, vea [Información general de los canales de actualización para Office 365 ProPlus](https://technet.microsoft.com/library/mt455210.aspx).

Para ver el panel de administración de clientes de Office 365 en la consola de Configuration Manager, vaya a **Biblioteca de software** > **Información general** > **Administración de clientes de Office 365**. En la parte superior del panel, use la opción desplegable **Colección** para filtrar los datos del panel por miembros de una colección determinada.

### <a name="display-data-in-the-office-365-client-management-dashboard"></a>Mostrar datos en el panel de administración de clientes de Office 365
Los datos que se muestran en el panel de administración de clientes de Office 365 proceden de inventario de hardware. Habilite el inventario de hardware y seleccione la clase de inventario de hardware **Configuraciones de Office 365 ProPlus** antes de que los datos aparezcan en el panel.
#### <a name="to-display-data-in-the-office-365-client-management-dashboard"></a>Para mostrar datos en el panel de administración de clientes de Office 365
1. Habilite el inventario de hardware, si aún no está habilitado. Para obtener más información, consulte [Configurar el inventario de hardware](\sccm\core\clients\manage\configure-hardware-inventory).
2. En la consola de Configuration Manager, navegue a **Administración** > **Configuración de cliente** > **Configuración de cliente predeterminada**.  
3. En la pestaña **Inicio** , en el grupo **Propiedades** , haga clic en **Propiedades**.  
4. En el **configuración de cliente predeterminada** cuadro de diálogo, haga clic en **de inventario de Hardware**.  
5. En el **configuración de dispositivo** lista, haga clic en **establecer clases**.  
6. En el cuadro de diálogo **Clases de inventario de hardware**, seleccione **Configuración de Office 365 ProPlus**.  
7.  Haga clic en **Aceptar** para guardar los cambios y cerrar la **clases de inventario de Hardware** cuadro de diálogo. <br/>El panel de administración de clientes de Office 365 comenzará a mostrar los datos a medida que se informe del inventario de hardware.

## <a name="deploy-office-365-apps"></a>Implementación de aplicaciones de Office 365  
A partir de la versión 1702, se puede iniciar el Instalador de Office 365 desde el panel de administración de clientes de Office 365 para realizar la instalación inicial de las aplicaciones de Office 365. El asistente permite configurar opciones de instalación de Office 365, descargar archivos desde redes de entrega de contenido (CDN) de Office y crear e implementar una aplicación de script para los archivos. Hasta que Office 365 no esté instalado en los clientes, no se podrán realizar actualizaciones de Office 365.

Con las versiones anteriores de Configuration Manager, hay que realizar los siguientes pasos para instalar por primera vez aplicaciones de Office 365 en los clientes:
- Descargar la herramienta de implementación de Office 365 (ODT)
- Descargar los archivos de origen de instalación de Office 365 (incluidos todos los paquetes de idioma necesarios)
- Generar el archivo Configuration.xml que especifica la versión y el canal correctos de Office
- Crear e implementar un paquete heredado o una aplicación de script para que los clientes instalen las aplicaciones de Office 365

### <a name="requirements"></a>requisitos
- El equipo que ejecuta el Instalador de Office 365 debe tener acceso a Internet.  
- El usuario que ejecuta el Instalador de Office 365 debe tener acceso de **lectura** y **escritura** para el uso compartido de la ubicación de contenido que se ofrece en el asistente.
- Si recibe un error de descarga 404, copie los archivos siguientes en la carpeta %temp% del usuario:
  - [releasehistory.xml](http://officecdn.microsoft.com/pr/wsus/releasehistory.cab)
  - [o365client_32bit.xml](http://officecdn.microsoft.com/pr/wsus/ofl.cab)  


### <a name="to-deploy-office-365-apps-to-clients-from-the-office-365-client-management-dashboard"></a>Para implementar aplicaciones de Office 365 en clientes desde el panel Administración de clientes de Office 365
1. En la consola de Configuration Manager, vaya a **Biblioteca de software** > **Información general** > **Administración de clientes de Office 365**.
2. Haga clic en **Programa de instalación de Office 365** en el panel superior derecho. Se abre el Asistente para la instalación del cliente de Office 365.
3. En la página **Configuración de la aplicación**, proporcione un nombre y una descripción para la aplicación, escriba la ubicación de descarga de los archivos y haga clic en **Siguiente**. La ubicación se debe especificar de la siguiente forma: &#92;&#92;*servidor*&#92;*recurso compartido*.
4. En la página **Importar configuración de cliente**, elija si quiere importar la configuración del cliente de Office 365 desde un archivo de configuración XML existente o especificarla manualmente y, luego, haga clic en **Siguiente**.  

    Si tiene un archivo de configuración existente, escriba su ubicación y vaya al paso 7. Debe especificar la ubicación con el formato &#92;&#92;*servidor*&#92;*recurso compartido*&#92;*nombre archivo*.XML.
    > [!IMPORTANT]    
    > El archivo de configuración XML debe contener solo [idiomas admitidos por el cliente Office 365 ProPlus](https://technet.microsoft.com/library/cc179219&#40;v=office.16&#41;.aspx).

5. En la página **Productos de cliente**, seleccione el conjunto de aplicaciones Office 365 que use. Seleccione las aplicaciones que quiera incluir. Seleccione los productos de Office adicionales que deban incluirse y, después, haga clic en **Siguiente**.
6. En la página **Configuración de cliente**, elija la configuración que quiere incluir y luego haga clic en **Siguiente**.
7. En la página **Implementación**, elija si quiere implementar la aplicación y haga clic en **Siguiente**. <br/>Si decide no implementar el paquete en el asistente, vaya al paso 9.
8. Configure el resto de las páginas del asistente como lo haría para una implementación de aplicación normal. Para obtener más información, consulte [Crear e implementar una aplicación](/sccm/apps/get-started/create-and-deploy-an-application).
9. Complete el asistente.
10. Puede implementar o modificar la aplicación en **Biblioteca de software** > **Información general** > **Administración de aplicaciones** > **Aplicaciones**.    

Después de crear e implementar aplicaciones de Office 365 mediante el Instalador de Office 365, Configuration Manager no administrará las actualizaciones de Office de forma predeterminada. Para permitir que los clientes de Office 365 reciban actualizaciones de Configuration Manager, vea [Implementar actualizaciones de Office 365 con Configuration Manager](#deploy-office-365-updates-with-configuration-manager).

>[!NOTE]
>Después de implementar las aplicaciones de Office 365, puede crear reglas de implementación automática para mantener esas aplicaciones. Para crear una regla de implementación automática para las aplicaciones de Office 365, haga clic en **Crear un ADR** desde el panel de administración de clientes de Office 365. Seleccione **Cliente de Office 365** cuando elija el producto. Para más información, vea [Implementar actualizaciones de software automáticamente](/sccm/sum/deploy-use/automatically-deploy-software-updates).


## <a name="deploy-office-365-updates"></a>Implementación de actualizaciones de Office 365
A partir de la versión 1706 de Configuration Manager, las actualizaciones de cliente de Office 365 se han movido al nodo **Administración de clientes de Office 365** >**Actualizaciones de Office 365**. Esto no afectará a la configuración de ADR. 

Siga estos pasos para implementar actualizaciones de Office 365 con Configuration Manager:

1.  [Compruebe los requisitos](https://technet.microsoft.com/library/mt628083.aspx) para usar Configuration Manager para administrar las actualizaciones de cliente de Office 365 en la sección **Requisitos para usar Configuration Manager para administrar las actualizaciones de cliente de Office 365** del artículo.  

2.  [Configurar puntos de actualización de software](../get-started/configure-classifications-and-products.md) para sincronizar las actualizaciones de cliente de Office 365. Definir las **actualizaciones** para la clasificación y seleccionar el **cliente de Office 365** para el producto. Sincronice las actualizaciones de software después de configurar los puntos de actualización de software para usar la clasificación **Actualizaciones**.
3.  Permita que los clientes de Office 365 reciban actualizaciones de Configuration Manager. Use la directiva de grupo o la configuración de cliente de Configuration Manager para habilitar el cliente.   

    **Método 1**: a partir de la versión 1606 de Configuration Manager, se puede usar la configuración de cliente de Configuration Manager para administrar el agente cliente de Office 365. Después de configurar esta opción e implementar las actualizaciones de Office 365, el agente cliente de Configuration Manager se comunica con el de Office 365 para descargar las actualizaciones de Office 365 desde un punto de distribución e instalarlas. Configuration Manager realiza un inventario de la configuración de cliente de Office 365 ProPlus.    

      1.  En la consola de Configuration Manager, haga clic en **Administración** > **Información general** > **Configuración de cliente**.  

      2.  Abra la configuración de dispositivo adecuada para habilitar el agente cliente. Para más información sobre las configuraciones de cliente personalizada y predeterminada, vea [Cómo establecer la configuración del cliente en Configuration Manager](../../core/clients/deploy/configure-client-settings.md).  

      3.  Haga clic en **Actualizaciones de software** y seleccione **Sí** para el valor **Habilitar administración del Agente cliente de Office 365**.  

    **Método 2**: [permita que los clientes de Office 365 reciban actualizaciones](https://technet.microsoft.com/library/mt628083.aspx#BKMK_EnableClient) de Configuration Manager mediante la directiva de grupo o la herramienta de implementación de Office.  

4. [Implemente actualizaciones de Office 365](deploy-software-updates.md) en los clientes.   

> [!Important]
> Antes de la versión 1610 de Configuration Manager, debe descargar e implementar actualizaciones en los mismos idiomas configurados en los clientes de Office 365. Por ejemplo, supongamos que tiene un cliente de Office 365 configurado con los idiomas en-us y de-de. En el servidor de sitio, descargue e implemente solo el contenido de en-us correspondiente a una actualización de Office 365 correspondiente. Cuando el usuario inicie la instalación de esta actualización desde el Centro de software, la actualización se bloquea mientras se descarga el contenido para de-de.   

## <a name="restart-behavior-and-client-notifications-for-office-365-updates"></a>Comportamiento al reiniciar y notificaciones de cliente para las actualizaciones de Office 365
Al implementar una actualización a un cliente de Office 365, el comportamiento de reinicio y las notificaciones de cliente serán distintas en función de la versión de Configuration Manager. En la tabla siguiente se proporciona información sobre la experiencia de usuario final cuando el cliente recibe una actualización de Office 365:

|Versión de Configuration Manager |Experiencia del usuario final|  
|----------------|---------------------|
|Antes de la 1610|Se establece una marca de reinicio y la actualización se instala después de reiniciar el equipo.|
|1610|Las aplicaciones de Office 365 se cierran sin previo aviso antes de instalar la actualización.|
|1610 con actualización <br/>1702|Se establece una marca de reinicio y la actualización se instala después de reiniciar el equipo.|
|1706|El cliente recibe notificaciones emergentes y en la aplicación, así como un cuadro de diálogo de cuenta atrás, antes de instalar la actualización.|

> [!Important]
> Desde la versión 1706 de Configuration Manager, tenga en cuenta los siguientes detalles:
>
>- Un icono de notificación se muestra en el área de notificación de la barra de tareas para aplicaciones necesarias, donde la fecha límite es 48 horas y el contenido de la actualización se ha descargado. 
>- Un cuadro de diálogo de cuenta atrás se muestra en las aplicaciones necesarias, donde la fecha límite es de 7,5 horas y la actualización se ha descargado. El usuario puede posponer el cuadro de diálogo de cuenta atrás hasta tres veces antes de la fecha límite. Cuando se hace, se muestra la cuenta atrás de nuevo después de 2 horas. Si no se pospone, hay una cuenta regresiva de 30 minutos y la actualización se instala cuando expira la cuenta atrás.
>- Una notificación emergente podría no mostrarse hasta que el usuario haga clic en el icono del área de notificación. Además, si en el área de notificación hay poco espacio, el icono de notificación podría no mostrarse, a menos que el usuario abra o expanda el área de notificación. 
>- El cuadro de diálogo de notificación y cuenta atrás podría iniciarse, aunque el usuario no esté trabajando activamente en el dispositivo. Por ejemplo, cuando el dispositivo está bloqueado por la noche, por lo que es posible que las aplicaciones de Office que se ejecutan en el dispositivo se cierren forzosamente para instalar la actualización. Antes de cerrar la aplicación, Office guarda los datos de aplicación para evitar la pérdida de datos. 
>- Si la fecha límite ya ha pasado o está configurada para iniciarse lo antes posible, las aplicaciones de Office en ejecución podrían cerrarse forzosamente sin enviar notificaciones. 
>- Si el usuario instala una actualización de Office antes de la fecha límite, Configuration Manager comprueba que está instalada la actualización cuando se alcanza la fecha límite. Si no se detecta la actualización en el dispositivo, se instala la actualización. 
>- La barra de notificación en aplicación no se muestra en una aplicación de Office en ejecución antes de descargarse la actualización. Después de descargarse, la notificación en aplicación solo se muestra para las aplicaciones recién abiertas.
>- Para las actualizaciones de Office que desencadena una ventana de servicio o las programadas para un horario no comercial, las aplicaciones de Office en ejecución podrían cerrarse forzosamente para instalar la actualización sin enviar notificaciones. 



## <a name="add-languages-for-office-365-update-downloads"></a>Adición de idiomas para descargar actualizaciones de Office 365
A partir de la versión 1610 de Configuration Manager, esta utilidad puede configurarse para descargar actualizaciones de los idiomas compatibles con Office 365, independientemente de si son compatibles con Configuration Manager.    

> [!IMPORTANT]  
> La configuración de idiomas de actualización de Office 365 adicionales es una configuración global del sitio. Después de agregar los idiomas con el procedimiento siguiente, todas las actualizaciones de Office 365 se descargarán en esos idiomas, y en los que seleccione en la página **Selección de idioma** del Asistente para descargar actualizaciones de software o del Asistente para implementar actualizaciones de software.

### <a name="to-add-support-to-download-updates-for-additional-languages"></a>Para agregar compatibilidad para descargar actualizaciones de idiomas adicionales
Siga el procedimiento de abajo en el punto de actualización de software del sitio de administración central o del sitio primario independiente.
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
8. Agregue idiomas adicionales a la propiedad **Value2** y haga clic en **Guardar propiedad**. <br/> Por ejemplo, pt-pt (para portugués de Portugal), af-za (para afrikáans de Sudáfrica), nn-no (para noruego nynorsk de Noruega), etc.  
![Agregar idiomas en el Editor de propiedades](..\media\4-props.png)  
9. Haga clic en **Cerrar**, en **Cerrar** y en **Guardar propiedad**, seleccione **Guardar objeto** (si aquí hace clic en **Cerrar**, se descartarán los valores) y **Cerrar**; después, haga clic en **Salir** para salir de la herramienta de comprobación del Instrumental de administración de Windows.
10. En la consola de Configuration Manager, vaya a **Biblioteca de software** > **Información general** > **Administración de clientes de Office 365** > **Actualizaciones de Office 365**.
11. Ahora, las actualizaciones de Office 365 se descargarán en los idiomas seleccionados en el asistente y en los que haya configurado en este procedimiento. Para comprobar que las actualizaciones se han descargado en esos idiomas, vaya al origen del paquete de la actualización y busque los archivos con el código de idioma en el nombre de archivo.  
![Nombres de archivo con idiomas adicionales](..\media\5-verification.png)


## <a name="change-the-update-channel-after-you-enable-office-365-clients-to-receive-updates-from-configuration-manager"></a>Cambiar el canal de actualización después de permitir que los clientes de Office 365 reciban actualizaciones de Configuration Manager
Para cambiar el canal de actualización después de permitir que los clientes de Office 365 reciban actualizaciones de Configuration Manager, se puede usar una directiva de grupo para distribuir un cambio del valor de una clave del Registro en los clientes de Office 365. Cambie la clave del Registro **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\ClickToRun\Configuration\CDNBaseUrl** para que use uno de los valores siguientes:

- Canal mensual <br/>
<i>(anteriormente Canal actual)</i>:  
  **CDNBaseUrl** = http&#58;//officecdn.microsoft.com/pr/492350f6-3a01-4f97-b9c0-c7c6ddf67d60

- Canal semianual <br/>
<i>(anteriormente Canal diferido:)</i>:  
  **CDNBaseUrl** = http&#58;//officecdn.microsoft.com/pr/7ffbc6bf-bc32-4f92-8982-f9dd17fd3114

- Canal mensual (dirigido)<Br/>
 <i>(anteriormente First Release para Canal actual)</i>:  
  **CDNBaseUrl** = http&#58;//officecdn.microsoft.com/pr/64256afe-f5d9-4f86-8936-8840a6a4f5be

- Canal semianual (dirigido) <br/>
<i>(anteriormente Primera versión de Canal diferido)</i>:  
  **CDNBaseUrl** = http&#58;//officecdn.microsoft.com/pr/b8f9b850-328d-4355-9145-c59439a0c4cf
<!--the channel names changed in Sept 2017- https://docs.microsoft.com/en-us/DeployOffice/overview-of-update-channels-for-office-365-proplus?ui=en-US&rs=en-US&ad=US>


<!--- You can create an Office 365 app without using the Office 365 Installation Wizard. To do this, you use the Office 2016 Deployment Tool (ODT) to download Office installation source files to a network share, generate Configure.xml that specifies the correct Office version and channel, and so on. Then, create an app for the files using the normal app management process.
> [!Note]
> The Office 365 Installation Wizard was introduced in Configuration Manager version 1702 and provides an easy way to create Office 365 apps.

- [Download the Office 2016 Deployment Tool](http://aka.ms/ODT2016) from the Microsoft Download Center.  
- Review the [configuration options for the Office Deployment Tool](https://technet.microsoft.com/library/jj219426.aspx).

You can create an application just as you would with any other application in Configuration Manager from **Software Library** > **Overview** > **Application Management** > **Applications**. For details, see [Create and deploy an application](/sccm/apps/get-started/create-and-deploy-an-application).
--->

<!--- ## Next steps
Use the Office 365 Client Management dashboard in Configuration Manager to review Office 365 client information and deploy Office 365 apps. For details, see [Manage Office 365 apps](manage-office-365-apps.md). --->
