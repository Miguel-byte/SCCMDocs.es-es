---
title: Ejemplos de MDT
titleSuffix: Microsoft Deployment Toolkit
description: 'Ejemplos de Microsoft Deployment Toolkit. '
ms.date: 09/09/2016
ms.prod: configuration-manager
ms.technology:
- configmgr-osd
ms.topic: article
ms.assetid: 2ff0100c-b7ef-4e09-8c96-fc1898390b6d
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 6b36da9f98749858829ab591571496532b26f290
ms.sourcegitcommit: 7198ec49d9ce68c6d55bfb9e2d537b5442a132cb
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/09/2018
---
# <a name="microsoft-deployment-toolkit-samples-guide"></a>Guía de ejemplos de Microsoft Deployment Toolkit  
 Esta guía forma parte de Microsoft® Deployment Toolkit (MDT) 2013 y sirve de orientación para un equipo de expertos a lo largo de la implementación de sistemas operativos Windows y Microsoft Office. En concreto, la guía está diseñada para ofrecer opciones de configuración de ejemplo para escenarios de implementación específicos.  

> [!NOTE]
>  En este documento, *Windows* se refiere a los sistemas operativos Windows 8.1, Windows 8, Windows 7, Windows Server 2012 R2, Windows Server 2012 y Windows Server 2008 R2, a menos que se indique lo contrario. MDT no es compatible con las versiones de Windows basadas en el procesador ARM. Asimismo, *MDT* hace referencia a MDT 2013, a menos que se indique lo contrario.  

 **Para usar esta guía**  

 Revise la lista de temas de escenarios en la tabla de contenido.  

1.  Seleccione el escenario que mejor represente los objetivos de implementación de su organización.  

2.  Revise las opciones de configuración de ejemplo del escenario seleccionado.  

3.  Use las opciones de configuración de ejemplo como base para la configuración de su entorno.  

4.  Personalice las opciones de configuración de ejemplo según su entorno.  

 En muchos casos, podría requerirse más de un escenario para completar las opciones de configuración del entorno.  

 Dado que esta guía solo contiene opciones de configuración de ejemplo, las guías que aparecen en la tabla siguiente pueden ayudar a personalizar las opciones de configuración del entorno.  

 |Guía|Esta guía ofrece ayuda para|  
 |-|-|  
 |*Guía de inicio rápido para Microsoft System Center 2012 R2 Configuration Manager* |Usar System Center 2012 R2 Configuration Manager para instalar el sistema operativo Windows 8.1 en un escenario de implementación de equipo nuevo.|  
 |*Guía de inicio rápido para Lite Touch Installation* |Instalar el sistema operativo Windows 8.1 mediante Lite Touch Installation (LTI) con el medio de arranque en un escenario de implementación de equipo nuevo.|  
 |*Guía de inicio rápido para la instalación controlada por el usuario* |Instalar el sistema operativo Windows 8.1 con la instalación controlada por el usuario y System Center 2012 R2 Configuration Manager en un escenario de implementación de equipo nuevo.|  
 |*Uso de Microsoft Deployment Toolkit* |Personalizar aún más los archivos de configuración usados en las implementaciones de Zero Touch Installation (ZTI) y LTI. Esta guía también contiene instrucciones de configuración genéricas y una referencia técnica para las opciones de configuración.|


## <a name="deploying-windows-8-applications-using-mdt"></a>Implementar aplicaciones de Windows 8 con MDT  
 MDT puede implementar paquetes de aplicación de Windows 8, que tienen una extensión de archivo .appx. Estos paquetes de aplicación son nuevos en Windows 8. Para más información sobre estas aplicaciones, vea el [desarrollo de aplicaciones de la Tienda Windows](http://msdn.microsoft.com/windows/apps).  

 Siga estos pasos para implementar aplicaciones de Windows 8 con MDT:  

-   Implemente aplicaciones de Windows 8 con LTI como se describe en [Implementar aplicaciones de Windows 8 con LTI](#DeployWin8LTI).  

-   Implemente aplicaciones de Windows 8 con la instalación controlada por el usuario (UDI) como se describe en [Implementar aplicaciones de Windows 8 con UDI](#DeployWin8UDI).  

###  <a name="DeployWin8LTI"></a> Implementar aplicaciones de Windows 8 con LTI  
 Puede implementar aplicaciones de Windows 8 con LTI de la misma manera que cualquier otra aplicación que inicie el proceso de instalación desde una línea de comandos. Puede agregar aplicaciones de Windows 8 a las implementaciones de LTI en el nodo de aplicaciones de Deployment Workbench.  

 **Para implementar una aplicación de Windows 8 con LTI**  

1.  Cree una carpeta compartida de red en la que se va a almacenar la aplicación.  

2.  Copie la aplicación de Windows 8 en la carpeta compartida de red que ha creado en el paso anterior.  

     Asegúrese de que copia el archivo .appx de aplicación de Windows 8 y los demás archivos necesarios, como el archivo .cer que contiene el certificado de la aplicación.  

3.  Cree un elemento de aplicación de LTI para la aplicación de Windows 8 en el nodo de aplicaciones de Deployment Workbench mediante el Asistente para nuevas aplicaciones.  

     Al completar el Asistente para nuevas aplicaciones, en la página del Asistente **Detalles del comando**, en **Línea de comandos**, escriba **app_file_name** (donde *app_file_name*  es el nombre de la aplicación de Windows 8).  

     Para más información sobre cómo completar el Asistente para nuevas aplicaciones en Deployment Workbench, vea las secciones siguientes en el documento de MDT *Using the Microsoft Deployment Toolkit* (Uso de Microsoft Deployment Toolkit):  

    -   "Create a New Application That Is Deployed from the Deployment Share" (Crear una aplicación que se implementa desde el recurso compartido de implementación)  

    -   "Create a New Application That Is Deployed from Another Network Shared Folder" (Crear una aplicación que se implementa desde otra carpeta compartida de red)  

4.  Seleccione el elemento de aplicación de LTI creado en el paso anterior en una secuencia de tareas de LTI.  

###  <a name="DeployWin8UDI"></a> Implementar aplicaciones de Windows 8 con UDI  
 Puede implementar aplicaciones de Windows 8 con UDI de la misma manera que cualquier otra aplicación que inicie el proceso de instalación desde una línea de comandos. Puede agregar aplicaciones de Windows 8 a las implementaciones de UDI en la página del asistente **ApplicationPage** en el diseñador del Asistente para UDI.  

> [!NOTE]
>  La implementación de Windows 8 y aplicaciones de Windows 8 mediante UDI requiere System Center 2012 R2 Configuration Manager.  

 **Para implementar una aplicación de Windows 8 con UDI**  

1.  Cree una carpeta compartida de red en la que se va a almacenar la aplicación.  

     Será la carpeta de origen para la aplicación de Configuration Manager que creará más adelante en el proceso.  

2.  Copie la aplicación de Windows 8 en la carpeta compartida de red que ha creado en el paso anterior.  

     Asegúrese de que copia el archivo .appx de aplicación de Windows 8 y los demás archivos necesarios, como el archivo .cer que contiene el certificado de la aplicación.  

3.  Agregue la aplicación de Windows 8 como una aplicación de Configuration Manager.  

4.  Cree un elemento de aplicación de Configuration Manager para la aplicación de Windows 8 mediante el Asistente para crear aplicaciones de la consola de Configuration Manager.  

     Al completar el Asistente para crear aplicaciones, cree un tipo de implementación para implementar la aplicación de Windows 8 mediante el Asistente para crear tipos de implementación. En el Asistente para crear tipos de implementación, en la página **Contenido**, en **Programa de instalación**, escriba **app_file_name** (donde *app_file_name* es el nombre de la aplicación de Windows 8).  

     Para más información sobre cómo completar el Asistente para crear aplicaciones en la consola de Configuration Manager, vea las siguientes secciones de la biblioteca de documentación de System Center 2012 Configuration Manager, que se incluye con Configuration Manager:  

    -   [Cómo crear aplicaciones en Configuration Manager](http://technet.microsoft.com/library/gg682159.aspx)  

    -   [Cómo crear tipos de implementación en Configuration Manager](http://technet.microsoft.com/library/gg682174.aspx#BKMK_Step3)  

    -   [Administración de tipos de implementaciones y aplicaciones en Configuration Manager](http://technet.microsoft.com/library/gg682031)  

5.  Asegúrese de que la característica de afinidad entre usuario y dispositivo (UDA) de Configuration Manager está configurada correctamente para admitir la afinidad entre los usuarios y los dispositivos para la implementación de aplicaciones de Configuration Manager.  

     Para más información sobre cómo configurar UDA para admitir la implementación de aplicaciones de Configuration Manager, vea [Administración de afinidad entre usuario y dispositivo en Configuration Manager](http://technet.microsoft.com/library/gg699365).  

6.  Implemente la aplicación creada en el paso 4 para los usuarios de destino.  

     Para más información sobre cómo implementar una aplicación en el usuario, vea [Cómo implementar aplicaciones en Configuration Manager](http://technet.microsoft.com/library/gg682082).  

7.  Configure la página del asistente **ApplicationPage** para incluir la aplicación de Configuration Manager que se ha creado en el paso 4 con el diseñador del Asistente para UDI.  

     Para más información sobre cómo configurar la página del asistente **ApplicationPage** con el diseñador del Asistente para UDI, vea la sección "Step 5-11: Customize the UDI Wizard Configuration File for the Target Computer" (Paso 5-11: personalizar el archivo de configuración del Asistente para UDI para el equipo de destino), en el documento de MDT *Quick start Guide for User-Driven Installation* (Guía de inicio rápido para la instalación controlada por el usuario).  

8.  Seleccione el elemento de aplicación de UDI creado en el paso anterior en una secuencia de tareas de UDI.  

    > [!NOTE]
    >  La aplicación de Windows 8 no se instala por medio de la secuencia de tareas, sino que se instala la primera vez que el usuario inicia sesión en el equipo de destino (según la opción de afinidad entre usuario y dispositivo configurada en el paso 5) mediante la característica de instalador de aplicaciones centradas en el usuario (AppInstall.exe) de UDI.  

     Para más información sobre la característica de instalador de aplicaciones centradas en el usuario de UDI, vea la sección "User-Centric App Installer Reference" (Referencia del instalador de aplicaciones centradas en el usuario) del documento de MDT *Toolkit Reference* (Referencia del kit de herramientas).  

## <a name="managing-mdt-using-windows-powershell"></a>Administración de MDT con Windows PowerShell  
 Puede administrar los recursos compartidos de implementación de MDT con Deployment Workbench y Windows PowerShell. MDT incluye un complemento de Windows PowerShell™ (Microsoft.BDD.SnapIn) que debe cargarse antes de usar las funciones específicas de MDT en Windows PowerShell. El complemento de Windows PowerShell de MDT incluye:  

-   Un proveedor de Windows PowerShell (MDTProvider) que proporciona acceso al contenido de un recurso compartido de implementación.  

-   Cmdlets que permiten administrar recursos compartidos de implementación de MDT.  

 Administre los recursos compartidos de implementación de MDT con Windows PowerShell mediante los pasos siguientes:  

-   Cargue el complemento de Windows PowerShell de MDT como se describe en [Cargar el complemento de Windows PowerShell de MDT](#LoadMDTSnapIn).  

-   Cree un recurso compartido de implementación con Windows PowerShell como se describe en [Crear un recurso compartido de implementación con Windows PowerShell](#CreateDeployShare).  

-   Vea las propiedades del recurso compartido de implementación con Windows PowerShell como se describe en [Ver las propiedades de un recurso compartido de implementación con Windows PowerShell](#ViewDeployShareProp).  

-   Vea la lista de recursos compartidos de implementación con Windows PowerShell como se describe en [Ver la lista de recursos compartidos de implementación con Windows PowerShell](#ViewListDeployShare).  

-   Actualice un recurso compartido de implementación, lo que genera nuevas imágenes de arranque del Entorno de preinstalación de Windows (Windows PE), como se describe en [Actualizar un recurso compartido de implementación con Windows PowerShell](#UpdateDeployShare).  

-   Actualice un recurso compartido de implementación vinculado, que replica contenido de un recurso compartido de implementación en el recurso compartido de implementación vinculado, como se describe en [Actualizar un recurso compartido de implementación vinculado con Windows PowerShell](#UpdateLinkedDeployShare).  

-   Actualice los medios de implementación, que replican contenido de un recurso compartido de implementación en los medios de implementación y, después, generan nuevas imágenes de arranque, como se describe en [Actualizar medios de implementación con Windows PowerShell](#UpdateDeployMedia).  

-   Administre los elementos de un recurso compartido de implementación (por ejemplo, sistemas operativos, paquetes de sistema operativo, aplicaciones y controladores de dispositivo) como se describe en [Administrar elementos de un recurso compartido de implementación con Windows PowerShell](#ManageItemDeployShare).  

-   Automatice el rellenado de los elementos de un recurso compartido de implementación (por ejemplo, sistemas operativos, paquetes de sistema operativo, aplicaciones y controladores de dispositivo) como se describe en [Automatizar el rellenado de un recurso compartido de implementación](#AutomatePopulateDeployShare).  

-   Administre las carpetas de un recurso compartido de implementación con Windows PowerShell como se describe en [Administrar las carpetas de un recurso compartido de implementación con Windows PowerShell](#ManageDeployShareFolder).  

###  <a name="LoadMDTSnapIn"></a> Cargar el complemento de Windows PowerShell de MDT  
 Los cmdlets de MDT se proporcionan en un complemento de Windows PowerShell (**Microsoft.BDD.SnapIn**) que debe cargarse para poder usar los cmdlets de MDT. Puede cargar el complemento de Windows PowerShell de MDT mediante cualquiera de los métodos siguientes:  

-   Cargue el complemento de Windows PowerShell de MDT mediante la consola de módulos de Windows PowerShell como se describe en [Cargar el complemento de Windows PowerShell de MDT con la tarea Importar módulos de sistema](#LoadMDTSnapInImport).  

-   Cargue el complemento de Windows PowerShell de MDT mediante el cmdlet **Add-PSSnapIn** como se describe en [Cargar el complemento de Windows PowerShell de MDT con el cmdlet Add-PSSnapIn](#LoadMDTSnapInCmdlet).  

####  <a name="LoadMDTSnapInImport"></a> Cargar el complemento de Windows PowerShell de MDT con la tarea Importar módulos de sistema  
 La tarea Importar módulos de sistema incluye automáticamente todos los módulos de Windows PowerShell y los complementos que se encuentran en los módulos del directorio %Windir%\System32\WindowsPowerShell\1.0\Modules. MDT instala automáticamente el complemento de Windows PowerShell de MDT (**Microsoft.BDD.SnapIn**) en esa carpeta durante el proceso de instalación de MDT.  

> [!NOTE]
>  La tarea Importar módulos de sistema solo está disponible en Windows 7 y Windows Server 2008 R2 cuando Windows PowerShell 3.0 no está instalado en el equipo. A partir de Windows PowerShell 3.0, los módulos se importan automáticamente la primera vez que se usa un cmdlet en el módulo.  

 Puede iniciar una consola de Windows PowerShell con la tarea Importar módulos de sistema mediante uno de los procedimientos siguientes:  

-   En la barra de tareas, haga clic con el botón derecho en el icono de **Windows PowerShell** y haga clic en **Importar módulos de sistema**.  

-   Haga clic en **Inicio**, seleccione **Herramientas administrativas** y haga clic en **Módulos de PowerShell**.  

 Para más información sobre cómo iniciar una consola de Windows PowerShell con Importar módulos de sistema, vea [Iniciar Windows PowerShell con Importar módulos de sistema](http://msdn.microsoft.com/library/windows/desktop/hh847866.aspx).  

####  <a name="LoadMDTSnapInCmdlet"></a> Cargar el complemento de Windows PowerShell de MDT con el cmdlet Add-PSSnapIn  
 Puede cargar el complemento de Windows PowerShell de MDT (**Microsoft.BDD.PSSnapIn**) desde cualquier entorno de Windows PowerShell con el cmdlet [Add-PSSnapIn](http://technet.microsoft.com/library/hh849705.aspx), como se muestra en el ejemplo siguiente:  

```  
Add-PSSnapin -Name Microsoft.BDD.PSSnapIn  
```  

###  <a name="CreateDeployShare"></a> Crear un recurso compartido de implementación con Windows PowerShell  
 Puede crear recursos compartidos de implementación con los cmdlets de Windows PowerShell de MDT. La carpeta raíz del recurso compartido de implementación se crea y se comparte mediante los cmdlets estándar de Windows PowerShell y llamadas a comandos de clase de Instrumental de administración de Windows (WMI). El recurso compartido de implementación se rellena con el proveedor MDTProvider de Windows PowerShell y el cmdlet [NewPSDrive](http://technet.microsoft.com/library/dd315340.aspx). La unidad MDTProvider de Windows PowerShell se conserva mediante el cmdlet **Add-MDTPersistentDrive**.  

 **Para preparar un recurso compartido de implementación con los cmdlets de Windows PowerShell de MDT**  

1.  Cargue el complemento de Windows PowerShell de MDT como se describe en [Cargar el complemento de Windows PowerShell de MDT](#LoadMDTSnapIn).  

2.  Cree la carpeta que será la raíz del nuevo recurso compartido de implementación con el cmdlet **New-Item**, como se muestra en el ejemplo siguiente y se describe en [Using the New-Item Cmdlet](http://technet.microsoft.com/library/ee176914.aspx) (Uso del cmdlet New-Item):  

    ```  
    New-Item "C:\MDTDeploymentShare$" -Type directory  
    ```  

     El cmdlet muestra que la carpeta se ha creado correctamente.  

3.  Comparta la carpeta que ha creado en el paso anterior mediante la clase **win32_share de WMI** como se muestra en el ejemplo siguiente:  

    ```  
    ([wmiclass]"win32_share").Create("C:\MDTDeploymentShare$", "MDTDeploymentShare$",0)  
    ```  

     La llamada a la clase **win32_share** devuelve los resultados de la llamada. Si el valor de **ReturnValue** es cero (0), la llamada ha tenido éxito.  

4.  Especifique la nueva carpeta compartida como un recurso compartido de implementación mediante el cmdlet [NewPSDrive](http://technet.microsoft.com/library/dd315340.aspx), como se muestra en el ejemplo siguiente:  

    ```  
    New-PSDrive -Name "DS002" -PSProvider "MDTProvider" -Root "C:\MDTDeploymentShare$" -Description "MDT Deployment Share Created with Cmdlets" -NetworkPath "\\WDG-MDT-01\MDTDeploymentShare$" -Verbose  
    ```  

     El cmdlet empieza a crear automáticamente el recurso compartido de implementación y copia la información de la plantilla en el nuevo recurso compartido de implementación. Cuando se complete el proceso de copia, el cmdlet muestra la información del nuevo recurso compartido de implementación.  

    > [!NOTE]
    >  El valor proporcionado en el parámetro *Name* (DS002) debe ser único y no puede ser el igual al de una unidad existente de Windows PowerShell de recursos compartidos de implementación.  

5.  Compruebe que se han creado las carpetas de recurso compartido de implementación adecuadas con el comando **dir**, como se muestra en el ejemplo siguiente:  

    ```  
    dir ds002:  
    ```  

     Se muestra la lista de carpetas predeterminadas en la raíz del recurso compartido de implementación.  

6.  Agregue el nuevo recurso compartido de implementación a la lista de recursos compartidos de implementación de MDT persistentes con el cmdlet **Add-MDTPersistentDrive**, como se muestra en el ejemplo siguiente:  

    ```  
    $NewDS=Get-PSDrive "DS002"  
    Add-MDTPersistentDrive  -Name "DS002" -InputObject $NewDS Verbose  
    ```  

     En este ejemplo, se usa la variable *$NewDS* para pasar el objeto de unidad de Windows PowerShell para el nuevo recurso compartido de implementación al cmdlet.  

     También podría combinar los cmdlets [NewPSDrive](http://technet.microsoft.com/library/dd315340.aspx) y **Add-MDTPersistentDrive**, como se muestra en el ejemplo siguiente:  

    ```  
    New-PSDrive -Name "DS002" -PSProvider "MDTProvider" -Root "C:\MDTDeploymentShare$" -Description "MDT Deployment Share Created with Cmdlets" -NetworkPath "\\WDG-MDT-01\MDTDeploymentShare$" -Verbose | Add-MDTPersistentDrive -Verbose  
    ```  

     En el ejemplo anterior, la canalización de Windows PowerShell proporciona los parámetros *Name* e *InputObject*.  

###  <a name="ViewDeployShareProp"></a> Ver las propiedades de un recurso compartido de implementación con Windows PowerShell  
 Puede ver las propiedades de recursos compartidos de implementación de MDT con el cmdlet [Get-ItemProperty](http://technet.microsoft.com/library/hh849851.aspx) y el proveedor MDTProvider de Windows PowerShell. Estas propiedades también se pueden ver en Deployment Workbench.  

 **Para ver las propiedades de un recurso compartido de implementación con los cmdlets de Windows PowerShell de MDT**  

1.  Cargue el complemento de Windows PowerShell de MDT como se describe en [Cargar el complemento de Windows PowerShell de MDT](#LoadMDTSnapIn).  

2.  Asegúrese de que las implementaciones de MDT que comparten unidades de Windows PowerShell se restauren con el cmdlet **Restore-MDTPersistentDrive**, como se muestra en el ejemplo siguiente:  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Si las implementaciones de MDT que comparten unidades de Windows PowerShell ya están restauradas, recibirá un mensaje de advertencia que indica que el cmdlet no puede restaurar la unidad.  

3.  Compruebe que las implementaciones de MDT que comparten unidades de Windows PowerShell se restauren correctamente con el cmdlet [Get-PSDrive](http://technet.microsoft.com/library/hh849796), como se indica a continuación:  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     Se muestra la lista de unidades de Windows PowerShell que se proporcionan con MDTProvider.  

4.  Para ver las propiedades del recurso compartido de implementación, use el cmdlet [Get-ItemProperty](http://technet.microsoft.com/library/hh849851.aspx) como se muestra en el ejemplo siguiente:  

    ```  
    Get-ItemProperty "DS002:"  
    ```  

     En este ejemplo, *DS002:* es el nombre de una unidad de Windows PowerShell que se devuelve en el paso 3. El cmdlet devuelve las propiedades del recurso compartido de implementación.  

###  <a name="ViewListDeployShare"></a> Ver la lista de recursos compartidos de implementación con Windows PowerShell  
 Puede ver la lista de recursos compartidos de implementación de MDT con el cmdlet [Get-PSDrive](http://technet.microsoft.com/library/hh849796) y el proveedor MDTProvider de Windows PowerShell. La lista de recursos compartidos de implementación también se puede ver en Deployment Workbench.  

 **Para ver una lista de recursos compartidos de implementación con los cmdlets de Windows PowerShell de MDT**  

1.  Cargue el complemento de Windows PowerShell de MDT como se describe en [Cargar el complemento de Windows PowerShell de MDT](#LoadMDTSnapIn).  

2.  Asegúrese de que las implementaciones de MDT que comparten unidades de Windows PowerShell se restauren con el cmdlet **Restore-MDTPersistentDrive**, como se muestra en el ejemplo siguiente:  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Si las implementaciones de MDT que comparten unidades de Windows PowerShell ya están restauradas, recibirá un mensaje de advertencia que indica que el cmdlet no puede restaurar la unidad.  

3.  Para ver la lista de implementaciones de MDT que comparten unidades de Windows PowerShell, una para cada recurso compartido de implementación, use el cmdlet [Get-PSDrive](http://technet.microsoft.com/library/hh849796) como se indica a continuación:  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     Se muestra la lista de unidades de Windows PowerShell que se proporcionan con MDTProvider, una para cada recurso compartido de implementación.  

###  <a name="UpdateDeployShare"></a> Actualizar un recurso compartido de implementación con Windows PowerShell  
 Puede actualizar recursos compartidos de implementación con el cmdlet **Update-MDTDeploymentShare** y el proveedor MDTProvider de Windows PowerShell. Al actualizar un recurso compartido de implementación, se crean las imágenes de arranque de Windows PE (archivos WIM e ISO [Organización internacional de normalización]) necesarias para iniciar la implementación de LTI. Puede realizar el mismo proceso con Deployment Workbench, como se describe en "Update a Deployment Share in the Deployment Workbench" (Actualizar un recurso compartido de implementación en Deployment Workbench).  

 **Para actualizar un recurso compartido de implementación con Windows PowerShell**  

1.  Cargue el complemento de Windows PowerShell de MDT como se describe en [Cargar el complemento de Windows PowerShell de MDT](#LoadMDTSnapIn).  

2.  Asegúrese de que las implementaciones de MDT que comparten unidades de Windows PowerShell se restauren con el cmdlet **Restore-MDTPersistentDrive**, como se muestra en el ejemplo siguiente:  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Si las implementaciones de MDT que comparten unidades de Windows PowerShell ya están restauradas, recibirá un mensaje de advertencia que indica que el cmdlet no puede restaurar la unidad.  

3.  Compruebe que las implementaciones de MDT que comparten unidades de Windows PowerShell se restauren correctamente con el cmdlet [Get-PSDrive](http://technet.microsoft.com/library/hh849796), como se indica a continuación:  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     Se muestra la lista de unidades de Windows PowerShell que se proporcionan con MDTProvider.  

4.  Para actualizar el recurso compartido de implementación use el cmdlet **Update-MDTDeploymentShare**, como se muestra en el ejemplo siguiente:  

    ```  
    Update-MDTDeploymentShare -Path "DS002:" -Force  
    ```  

     En este ejemplo, *DS002:* es el nombre de una unidad de Windows PowerShell que se devuelve en el paso 3.  

    > [!NOTE]
    >  La actualización del recurso compartido de implementación puede tardar mucho tiempo. El progreso del cmdlet se muestra en la parte superior de la consola de Windows PowerShell.  

     El cmdlet se devuelve sin resultados si la actualización se realiza correctamente.  

###  <a name="UpdateLinkedDeployShare"></a> Actualizar un recurso compartido de implementación vinculado con Windows PowerShell  
 Puede actualizar (replicar) recursos compartidos de implementación vinculados con el cmdlet **Update-MDTLinkedDS** y el proveedor MDTProvider de Windows PowerShell. Si se actualiza un recurso compartido de implementación vinculado, se replica el contenido del recurso compartido de implementación original en el recurso compartido de implementación vinculado. Puede realizar el mismo proceso con Deployment Workbench, como se describe en "Replicate Linked Deployment Shares in the Deployment Workbench" (Replicar recursos compartidos de implementación vinculados en Deployment Workbench).  

 **Para actualizar un recurso compartido de implementación vinculado con Windows PowerShell**  

1.  Cargue el complemento de Windows PowerShell de MDT como se describe en [Cargar el complemento de Windows PowerShell de MDT](#LoadMDTSnapIn).  

2.  Asegúrese de que las implementaciones de MDT que comparten unidades de Windows PowerShell se restauren con el cmdlet **Restore-MDTPersistentDrive**, como se muestra en el ejemplo siguiente:  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Si las implementaciones de MDT que comparten unidades de Windows PowerShell ya están restauradas, recibirá un mensaje de advertencia que indica que el cmdlet no puede restaurar la unidad.  

3.  Compruebe que las implementaciones de MDT que comparten unidades de Windows PowerShell se restauren correctamente con el cmdlet [Get-PSDrive](http://technet.microsoft.com/library/hh849796), como se indica a continuación:  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     Se muestra la lista de unidades de Windows PowerShell que se proporcionan con MDTProvider.  

4.  Para actualizar el recurso compartido de implementación use el cmdlet **Update-MDTDeploymentShare**, como se muestra en el ejemplo siguiente:  

    ```  
    Update-MDTLinkedDS -Path "DS002:\Linked Deployment Shares\LINKED002"  
    ```  

     En este ejemplo, *DS002:* es el nombre de una unidad de Windows PowerShell que se devuelve en el paso 3.  

    > [!NOTE]
    >  La actualización del recurso compartido de implementación vinculado puede tardar mucho tiempo. El progreso del cmdlet se muestra en la parte superior de la consola de Windows PowerShell.  

     El cmdlet se devuelve sin resultados si la actualización se realiza correctamente.  

###  <a name="UpdateDeployMedia"></a> Actualizar medios de implementación con Windows PowerShell  
 Puede actualizar (generar) medios de implementación con el cmdlet **Update-MDTMedia** y el proveedor MDTProvider de Windows PowerShell. Si se actualizan los medios de implementación, se replica el contenido del recurso compartido de implementación original en el recurso compartido de implementación vinculado y, después, se generan los archivos .iso y .wim. Puede realizar el mismo proceso con Deployment Workbench, como se describe en "Generate Media Images in the Deployment Workbench" (Generar imágenes de medios en Deployment Workbench).  

 Cuando el cmdlet **Update-MDTMedia** finaliza, se crean los archivos siguientes:  

-   Un archivo .iso en la carpeta *media_folder* (donde *media_folder* es el nombre de la carpeta que ha especificado para los medios).  

     La generación del archivo .iso es una opción que puede configurar como se indica a continuación:  

    -   Seleccione la casilla **Generate a Lite Touch bootable ISO image** (Generar una imagen ISO de arranque de Lite Touch) en la pestaña **General** del cuadro de diálogo **Propiedades de medio** (desactive esta casilla para reducir el tiempo necesario para generar los medios, a menos que necesite crear máquinas virtuales de inicio o DVD de arranque desde el archivo .iso).  

    -   Establezca la misma propiedad con el cmdlet [Set-ItemProperty](http://technet.microsoft.com/library/hh849844).  

-   Archivos WIM en la carpeta *media_folder*\Content\Deploy\Boot (donde *media_folder* es el nombre de la carpeta que ha especificado para los medios).  

 **Para actualizar un recurso compartido de implementación vinculado con Windows PowerShell**  

1.  Cargue el complemento de Windows PowerShell de MDT como se describe en [Cargar el complemento de Windows PowerShell de MDT](#LoadMDTSnapIn).  

2.  Asegúrese de que las implementaciones de MDT que comparten unidades de Windows PowerShell se restauren con el cmdlet **Restore-MDTPersistentDrive**, como se muestra en el ejemplo siguiente:  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Si las implementaciones de MDT que comparten unidades de Windows PowerShell ya están restauradas, recibirá un mensaje de advertencia que indica que el cmdlet no puede restaurar la unidad.  

3.  Compruebe que las implementaciones de MDT que comparten unidades de Windows PowerShell se restauren correctamente con el cmdlet [Get-PSDrive](http://technet.microsoft.com/library/hh849796), como se indica a continuación:  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     Se muestra la lista de unidades de Windows PowerShell que se proporcionan con MDTProvider.  

4.  Para actualizar el recurso compartido de implementación use el cmdlet **Update-MDTDeploymentShare**, como se muestra en el ejemplo siguiente:  

    ```  
    Update-MDTLinkedDS -Path "DS002:\Linked Deployment Shares\LINKED002"  
    ```  

     En este ejemplo, *DS002:* es el nombre de una unidad de Windows PowerShell que se devuelve en el paso 3.  

    > [!NOTE]
    >  La actualización del recurso compartido de implementación vinculado puede tardar mucho tiempo. El progreso del cmdlet se muestra en la parte superior de la consola de Windows PowerShell.  

     El cmdlet se devuelve sin resultados si la actualización se realiza correctamente.  

###  <a name="ManageItemDeployShare"></a> Administrar elementos de un recurso compartido de implementación con Windows PowerShell  
 Un recurso compartido de implementación contiene elementos que se usan para realizar implementaciones, como sistemas operativos, aplicaciones, controladores de dispositivo, paquetes de sistema operativo y secuencias de tareas. Puede administrar estos elementos con los cmdlets de Windows PowerShell y los proporcionados con MDT.  

 Para más información sobre cómo manipular elementos directamente con cmdlets de Windows PowerShell, vea [Manipular elementos directamente](http://technet.microsoft.com/library/dd315266.aspx). La estructura de carpetas de un recurso compartido de implementación también se puede administrar con Windows PowerShell. Para más información, vea [Administrar las carpetas de un recurso compartido de implementación con Windows PowerShell](#ManageDeployShareFolder).  

####  <a name="ImportItemDeployShare"></a> Importar un elemento en un recurso compartido de implementación  
 Con los cmdlets de MDT puede importar todos los tipos de elemento, como sistemas operativos, aplicaciones o controladores de dispositivo. Para cada tipo de elemento, hay un cmdlet de MDT específico. Si quiere importar varios elementos en un recurso compartido de implementación con Windows PowerShell, vea [Automatizar el rellenado de un recurso compartido de implementación](#AutomatePopulateDeployShare).  

 En la tabla siguiente se muestran los cmdlets de Windows PowerShell de MDT que se usan para importar elementos en un recurso compartido de implementación y se proporciona una breve descripción de cada cmdlet. En la sección correspondiente a cada cmdlet se incluyen ejemplos de uso.  

 |**Cmdlet** | **Descripción** |  
 |-|-|  
 |**Import-MDTApplication** |Importa una aplicación en un recurso compartido de implementación.|  
 |**Import-MDTDriver** |Importa uno o varios controladores de dispositivo en un recurso compartido de implementación.|  
 |**Import-MDTOperatingSystem** |Importa uno o varios sistemas operativos en un recurso compartido de implementación.|  
 |**Import-MDTPackage** |Importa uno o varios paquetes de sistema operativo en un recurso compartido de implementación.|  
 |**Import-MDTTaskSequence** |Importa una secuencia de tareas en un recurso compartido de implementación.|  

####  <a name="ViewPropertyDeployShare"></a> Ver las propiedades de un elemento en un recurso compartido de implementación  
 Cada elemento de un recurso compartido de implementación tiene un conjunto diferente de propiedades. Para ver las propiedades de un elemento de un recurso compartido de implementación, use el cmdlet [Get-ItemProperty](http://technet.microsoft.com/library/hh849851.aspx). El cmdlet [Get-ItemProperty](http://technet.microsoft.com/library/hh849851.aspx) usa MDTProvider para mostrar las propiedades de un elemento específico, igual que para ver las propiedades en Deployment Workbench.  

 Si quiere ver las propiedades de varios elementos de un recurso compartido de implementación con Windows PowerShell, vea [Automatizar el rellenado de un recurso compartido de implementación](#AutomatePopulateDeployShare).  

 **Para ver las propiedades de un elemento en un recurso compartido de implementación con Windows PowerShell**  

1.  Cargue el complemento de Windows PowerShell de MDT como se describe en [Cargar el complemento de Windows PowerShell de MDT](#LoadMDTSnapIn).  

2.  Asegúrese de que las implementaciones de MDT que comparten unidades de Windows PowerShell se restauren con el cmdlet **Restore-MDTPersistentDrive**, como se muestra en el ejemplo siguiente:  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Si las implementaciones de MDT que comparten unidades de Windows PowerShell ya están restauradas, recibirá un mensaje de advertencia que indica que el cmdlet no puede restaurar la unidad.  

3.  Compruebe que las implementaciones de MDT que comparten unidades de Windows PowerShell se restauren correctamente con el cmdlet [Get-PSDrive](http://technet.microsoft.com/library/hh849796), como se muestra en el ejemplo siguiente:  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     Se muestra la lista de unidades de Windows PowerShell que se proporcionan con MDTProvider.  

4.  Devuelva una lista de elementos del tipo de elemento cuyas propiedades quiere ver mediante el cmdlet [Get-Item](http://technet.microsoft.com/library/hh849788), como se muestra en el ejemplo siguiente:  

    ```  
    Get-Item "DS001:\Operating Systems\*" | Format-List  
    ```  

     En el ejemplo anterior, se muestra una lista de todos los sistemas operativos del recurso compartido de implementación. La salida se canaliza al cmdlet **Format-List** para que se pueden ver los nombres largos de los sistemas operativos. Para más información sobre cómo usar el cmdlet **Format-List**, vea [Using the Format-List Cmdlet](http://technet.microsoft.com/library/ee176830.aspx) (Uso del Cmdlet Format-List). El mismo proceso podría usarse para devolver la lista de otros tipos de elementos, como controladores de dispositivo o aplicaciones.  

    > [!TIP]
    >  También puede usar el comando **dir** para ver la lista de sistemas operativos, en lugar del cmdlet [Get-Item](http://technet.microsoft.com/library/hh849788).  

5.  Para ver las propiedades de uno de los elementos mostrados en el paso anterior, use el cmdlet [Get-ItemProperty](http://technet.microsoft.com/library/hh849851.aspx) como se muestra en el ejemplo siguiente:  

    ```  
    Get-ItemProperty -Path "DS002:\Operating Systems\Windows 8 in Windows 8 x64 install.wim"  
    ```  

     En este ejemplo, el valor del parámetro *Path* es la ruta de acceso completa de Windows PowerShell al elemento, incluido el nombre de archivo devuelto en el paso anterior. Puede seguir el mismo proceso para ver las propiedades de otros tipos de elementos, como controladores de dispositivo o aplicaciones.  

####  <a name="RemoveItemDeployShare"></a> Quitar un elemento de un recurso compartido de implementación  
 Puede quitar un elemento de un recurso compartido de implementación con el cmdlet [Remove-Item](http://technet.microsoft.com/library/hh849765). El cmdlet [Remove-Item](http://technet.microsoft.com/library/hh849765) usa MDTProvider para quitar un elemento específico, igual que para quitar un elemento de Deployment Workbench. Si quiere quitar varios elementos de un recurso compartido de implementación con Windows PowerShell, vea [Automatizar el rellenado de un recurso compartido de implementación](#AutomatePopulateDeployShare).  

> [!NOTE]
>  Si el elemento que se quita lo usa una secuencia de tareas, se producirá un error en la secuencia de tareas. Antes de quitar un elemento, asegúrese de que no hagan referencia a él otros elementos del recurso compartido de implementación. Una vez que se ha quitado un elemento, no se puede recuperar.  

 **Para quitar un elemento de un recurso compartido de implementación con Windows PowerShell**  

1.  Cargue el complemento de Windows PowerShell de MDT como se describe en [Cargar el complemento de Windows PowerShell de MDT](#LoadMDTSnapIn).  

2.  Asegúrese de que las implementaciones de MDT que comparten unidades de Windows PowerShell se restauren con el cmdlet **Restore-MDTPersistentDrive**, como se muestra en el ejemplo siguiente.  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Si las implementaciones de MDT que comparten unidades de Windows PowerShell ya están restauradas, recibirá un mensaje de advertencia que indica que el cmdlet no puede restaurar la unidad.  

3.  Compruebe que las implementaciones de MDT que comparten unidades de Windows PowerShell se restauren correctamente con el cmdlet [Get-PSDrive](http://technet.microsoft.com/library/hh849796), como se muestra en el ejemplo siguiente:  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     Se muestra la lista de unidades de Windows PowerShell que se proporcionan con MDTProvider.  

4.  Devuelva una lista de elementos del tipo de elemento cuyas propiedades quiere ver mediante el cmdlet [Get-Item](http://technet.microsoft.com/library/hh849788), como se muestra en el ejemplo siguiente:  

    ```  
    Get-Item "DS001:\Operating Systems\*" | Format-List  
    ```  

     En el ejemplo anterior, se muestra una lista de todos los sistemas operativos del recurso compartido de implementación. La salida se canaliza al cmdlet **Format-List** para que se pueden ver los nombres largos de los sistemas operativos. Para más información sobre cómo usar el cmdlet **Format-List**, vea [Using the Format-List Cmdlet](http://technet.microsoft.com/library/ee176830.aspx) (Uso del Cmdlet Format-List). El mismo proceso podría usarse para devolver la lista de otros tipos de elementos, como controladores de dispositivo o aplicaciones.  

    > [!TIP]
    >  También puede usar el comando **dir** para ver la lista de sistemas operativos, en lugar del cmdlet [Get-Item](http://technet.microsoft.com/library/hh849788).  

5.  Para quitar uno de los elementos mostrados en el paso anterior, use el cmdlet [Remove-Item](http://technet.microsoft.com/library/hh849765) como se muestra en el ejemplo siguiente:  

    ```  
    Remove-Item -Path "DS002:\Operating Systems\Windows 8 in Windows 8 x64 install.wim"  
    ```  

     En este ejemplo, el valor del parámetro *Path* es la ruta de acceso completa de Windows PowerShell al elemento, incluido el nombre de archivo devuelto en el paso anterior.  

     El mismo proceso podría usarse para quitar otros tipos de elementos, como controladores de dispositivo o aplicaciones.  

    > [!NOTE]
    >  Si el elemento que se quita lo usa una secuencia de tareas, se producirá un error en la secuencia de tareas. Antes de quitar un elemento, asegúrese de que no hagan referencia a él otros elementos del recurso compartido de implementación.  

###  <a name="AutomatePopulateDeployShare"></a> Automatizar el rellenado de un recurso compartido de implementación  
 Los cmdlets de Windows PowerShell de MDT permiten administrar elementos individuales. Aun así, mediante el uso de algunas de las características de scripts de Windows PowerShell, los cmdlets se pueden usar para automatizar el rellenado de un recurso compartido de implementación.  

 Por ejemplo, una organización podría necesitar implementar varios recursos compartidos de implementación para diferentes unidades de negocio, o una organización podría proporcionar servicios de implementación de sistema operativo a otras organizaciones. En ambos ejemplos, las organizaciones necesitan poder crear y rellenar recursos compartidos de implementación configurados de forma coherente.  

 Un método para administrar varios elementos consiste en usar un archivo de valores separados por comas (CSV) que contenga una lista de todos los elementos que quiere administrar en un recurso compartido de implementación mediante el cmdlet [Import-CSV](http://technet.microsoft.com/library/dd347665.aspx).  

 A continuación se muestra un extracto de un script de Windows PowerShell para importar una lista de aplicaciones basada en la información de un archivo .csv con los cmdlets [Import-CSV](http://technet.microsoft.com/library/dd347665.aspx), [ForEach-Object](http://technet.microsoft.com/library/hh849731) e **Import-MDTApplication**:  

```  
$List=Import-CSV "C:\MDT\Import-MDT-Apps.csv"  
ForEach-Object ($App in $List) {  
Import-MDTApplication –path $App.ApplicationFolder -enable "True" –Name $App.DescriptiveName –ShortName $App.Shortname –Version $App.Version –Publisher $App.Publisher –Language $App.Language –CommandLine $App.CommandLine –WorkingDirectory $App.WorkingDirectory –ApplicationSourcePath $App.SourceFolder –DestinationFolder $App.DestinationFolder –Verbose  
}  
```  

 En este ejemplo, el archivo C:\MDT\Import-MDT-Apps.csv contiene un campo para cada variable necesario para importar una aplicación. Para más información sobre cómo crear un archivo .csv para su uso con el cmdlet [Import-CSV](http://technet.microsoft.com/library/dd347665.aspx), vea [Using the Import-Csv Cmdlet](http://technet.microsoft.com/library/ee176874.aspx) (Uso del cmdlet Import-Csv).  

 Puede usar este método para importar sistemas operativos, controladores de dispositivo y otros elementos de un recurso compartido de implementación mediante los pasos siguientes:  

1.  Cree un archivo .csv para cada tipo de elemento del recurso compartido de implementación que quiera rellenar.  

2.  Para más información sobre cómo crear un archivo .csv para su uso con el cmdlet [Import-CSV](http://technet.microsoft.com/library/dd347665.aspx), vea [Using the Import-Csv Cmdlet](http://technet.microsoft.com/library/ee176874.aspx) (Uso del cmdlet Import-Csv).  

3.  Cree un archivo de script de Windows PowerShell que se usará para automatizar el rellenado del recurso compartido de implementación.  

     Para más información sobre cómo crear un script de Windows PowerShell, vea [Scripting con Windows PowerShell](http://technet.microsoft.com/scriptcenter/powershell.aspx).  

4.  Cree todas las estructuras de carpetas requeridas en el recurso compartido de implementación antes de importar los elementos del recurso compartido de implementación.  

     Para más información, vea [Administrar las carpetas de un recurso compartido de implementación con Windows PowerShell](#ManageDeployShareFolder).  

5.  Agregue la línea del cmdlet [Import-CSV](http://technet.microsoft.com/library/dd347665.aspx) para uno de los archivos .csv creados en el paso 1.  

     Para más información sobre el cmdlet [Import-CSV](http://technet.microsoft.com/library/dd347665.aspx), vea [Using the Import-Csv Cmdlet](http://technet.microsoft.com/library/ee176874.aspx) (Uso del cmdlet Import-Csv).  

6.  Cree un bucle de cmdlet [ForEach-Object](http://technet.microsoft.com/library/hh849731) que procese cada elemento del archivo .csv al que se hace referencia en el cmdlet [Import-CSV](http://technet.microsoft.com/library/dd347665.aspx) del paso anterior.  

     Para más información sobre el cmdlet [ForEach-Object](http://technet.microsoft.com/library/hh849731), vea [Using the ForEach-Object Cmdlet](http://technet.microsoft.com/library/ee176828) (Uso del cmdlet ForEach-Object).  

7.  Agregue el cmdlet de MDT correspondiente para importar los elementos del recurso compartido de implementación en el bucle de cmdlet [ForEach-Object](http://technet.microsoft.com/library/hh849731) creado en el paso anterior.  

     Para más información sobre los cmdlets de MDT usados para importar elementos en un recurso compartido de implementación, vea [Importar un elemento en un recurso compartido de implementación](#ImportItemDeployShare).  

###  <a name="ManageDeployShareFolder"></a> Administrar las carpetas de un recurso compartido de implementación con Windows PowerShell  
 Puede administrar las carpetas de un recurso compartido de implementación con herramientas de línea de comandos, como el comando **mkdir**, o mediante cmdlets de Windows PowerShell, como el cmdlet [New-Item](http://technet.microsoft.com/library/hh849795) y el proveedor MDTProvider de Windows PowerShell. En Deployment Workbench también se puede ver y administrar la misma estructura de carpetas de recursos compartidos de implementación. Para más información sobre cómo manipular elementos directamente con cmdlets de Windows PowerShell, vea [Manipular elementos directamente](http://technet.microsoft.com/library/dd315266.aspx).  

#### <a name="create-a-folder-in-a-deployment-share-using-windows-powershell"></a>Crear una carpeta en un recurso compartido de implementación con Windows PowerShell  
 **Para crear una carpeta en un recurso compartido de implementación con Windows PowerShell**  

1.  Cargue el complemento de Windows PowerShell de MDT como se describe en [Cargar el complemento de Windows PowerShell de MDT](#LoadMDTSnapIn).  

2.  Asegúrese de que las implementaciones de MDT que comparten unidades de Windows PowerShell se restauren con el cmdlet **Restore-MDTPersistentDrive**, como se muestra en el ejemplo siguiente:  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Si las implementaciones de MDT que comparten unidades de Windows PowerShell ya están restauradas, recibirá un mensaje de advertencia que indica que el cmdlet no puede restaurar la unidad.  

3.  Para ver la lista de implementaciones de MDT que comparten unidades de Windows PowerShell, una para cada recurso compartido de implementación, use el cmdlet [Get-PSDrive](http://technet.microsoft.com/library/hh849796) como se indica a continuación:  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     Se muestra la lista de unidades de Windows PowerShell que se proporcionan con MDTProvider, una para cada recurso compartido de implementación.  

4.  Cree una carpeta denominada *Windows_8* en la carpeta de sistemas operativos de un recurso compartido de implementación con el comando **mkdir**, como se muestra en el ejemplo siguiente:  

    ```  
    mkdir "DS002:\Operating Systems\Windows_8"  
    ```  

     En este ejemplo, *DS002:* es el nombre de una unidad de Windows PowerShell que se devuelve en el paso 3.  

5.  Para comprobar que la carpeta se ha creado correctamente, escriba el comando siguiente:  

    ```  
    dir "DS002:\Operating Systems"  
    ```  

     Se muestra la carpeta Windows_8 y las demás carpetas existentes en la carpeta de sistemas operativos.  

6.  Cree una carpeta denominada *Windows_7* en la carpeta de sistemas operativos de un recurso compartido de implementación con el cmdlet [New-Item](http://technet.microsoft.com/library/hh849795), como se muestra en el ejemplo siguiente y se describe en [Using the New-Item Cmdlet](http://technet.microsoft.com/library/ee176914.aspx) (Uso del cmdlet New-Item):  

    ```  
    New-Item "DS002:\Operating Systems\Windows_7" -Type directory  
    ```  

     El cmdlet muestra que la carpeta se ha creado correctamente.  

7.  Para comprobar que la carpeta se ha creado correctamente, escriba el comando siguiente:  

    ```  
    dir "DS002:\Operating Systems"  
    ```  

     Se muestra la carpeta Windows_7 y las demás carpetas existentes en la carpeta de sistemas operativos.  

#### <a name="delete-a-folder-in-a-deployment-share-using-windows-powershell"></a>Eliminar una carpeta de un recurso compartido de implementación con Windows PowerShell  
 **Para eliminar una carpeta de un recurso compartido de implementación con Windows PowerShell**  

1.  Cargue el complemento de Windows PowerShell de MDT como se describe en [Cargar el complemento de Windows PowerShell de MDT](#LoadMDTSnapIn).  

2.  Asegúrese de que las implementaciones de MDT que comparten unidades de Windows PowerShell se restauren con el cmdlet **Restore-MDTPersistentDrive**, como se muestra en el ejemplo siguiente:  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Si las implementaciones de MDT que comparten unidades de Windows PowerShell ya están restauradas, recibirá un mensaje de advertencia que indica que el cmdlet no puede restaurar la unidad.  

3.  Para ver la lista de implementaciones de MDT que comparten unidades de Windows PowerShell, una para cada recurso compartido de implementación, use el cmdlet [Get-PSDrive](http://technet.microsoft.com/library/hh849796) como se indica a continuación:  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     Se muestra la lista de unidades de Windows PowerShell que se proporcionan con MDTProvider, una para cada recurso compartido de implementación.  

4.  Elimine (quite) una carpeta denominada *Windows_8* de la carpeta de sistemas operativos de un recurso compartido de implementación con el comando **mkdir**, como se muestra en el ejemplo siguiente:  

    ```  
    rmdir "DS002:\Operating Systems\Windows_8"  
    ```  

     En este ejemplo, *DS002:* es el nombre de una unidad de Windows PowerShell que se devuelve en el paso 3.  

5.  Para comprobar que la carpeta se ha eliminado correctamente, escriba el comando siguiente:  

    ```  
    dir "DS002:\Operating Systems"  
    ```  

     La carpeta Windows_8 ya no se muestra en la lista de carpetas de la carpeta de sistemas operativos.  

6.  Elimine (quite) una carpeta denominada *Windows_7* de la carpeta de sistemas operativos de un recurso compartido de implementación con el cmdlet [Remove-Item](http://technet.microsoft.com/library/hh849765), como se muestra en el ejemplo siguiente:  

    ```  
    Remove-Item "DS002:\Operating Systems\Windows_7"  
    ```  

     El cmdlet muestra que la carpeta se ha eliminado correctamente.  

7.  Para comprobar que la carpeta se ha creado correctamente, escriba el comando siguiente:  

    ```  
    dir "DS002:\Operating Systems"  
    ```  

     La carpeta Windows_7 ya no se muestra en la lista de carpetas de la carpeta de sistemas operativos.  

#### <a name="rename-a-folder-in-a-deployment-share-using-windows-powershell"></a>Cambiar el nombre de una carpeta de un recurso compartido de implementación con Windows PowerShell  
 **Para cambiar el nombre de una carpeta de un recurso compartido de implementación con Windows PowerShell**  

1.  Cargue el complemento de Windows PowerShell de MDT como se describe en [Cargar el complemento de Windows PowerShell de MDT](#LoadMDTSnapIn).  

2.  Asegúrese de que las implementaciones de MDT que comparten unidades de Windows PowerShell se restauren con el cmdlet **Restore-MDTPersistentDrive**, como se muestra en el ejemplo siguiente:  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Si las implementaciones de MDT que comparten unidades de Windows PowerShell ya están restauradas, recibirá un mensaje de advertencia que indica que el cmdlet no puede restaurar la unidad.  

3.  Para ver la lista de implementaciones de MDT que comparten unidades de Windows PowerShell, una para cada recurso compartido de implementación, use el cmdlet [Get-PSDrive](http://technet.microsoft.com/library/hh849796) como se indica a continuación:  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     Se muestra la lista de unidades de Windows PowerShell que se proporcionan con MDTProvider, una para cada recurso compartido de implementación.  

4.  Cambie el nombre de una carpeta denominada *Windows_8* a *Win_8* en la carpeta de sistemas operativos de un recurso compartido de implementación con el comando **ren**, como se muestra en el ejemplo siguiente:  

    ```  
    ren "DS002:\Operating Systems\Windows_8" "Win_8"  
    ```  

     En este ejemplo, *DS002:* es el nombre de una unidad de Windows PowerShell que se devuelve en el paso 3.  

5.  Para comprobar que la carpeta se ha eliminado correctamente, escriba el comando siguiente:  

    ```  
    dir "DS002:\Operating Systems"  
    ```  

     El nombre de la carpeta Windows_8 se ha cambiado a *Win_8*.  

6.  Cambie el nombre de una carpeta denominada *Windows_7* a *Win_7* en la carpeta de sistemas operativos de un recurso compartido de implementación con el cmdlet [Rename-Item](http://technet.microsoft.com/library/hh849763), como se muestra en el ejemplo siguiente:  

    ```  
    Rename-Item "DS002:\Operating Systems\Windows_7" "Win_7"  
    ```  

     El cmdlet muestra que se ha cambiado el nombre de la carpeta correctamente.  

7.  Para comprobar que la carpeta se ha creado correctamente, escriba el comando siguiente:  

    ```  
    dir "DS002:\Operating Systems"  
    ```  

     El nombre de la carpeta Windows_7 se ha cambiado a *Win_7*.  

## <a name="automating-the-application-of-operating-system-service-packs-in-deployment-shares"></a>Automatizar la aplicación de Service Pack de sistema operativo en recursos compartidos de implementación  
 Los Service Pack de sistema operativo son una parte normal del ciclo de vida del software. Los sistemas operativos existentes en los recursos compartidos de implementación deben actualizarse con estos Service Pack para garantizar que los equipos recién implementados o actualizados estén actualizados con las últimas recomendaciones de seguridad y opciones de configuración.  

 En el caso de que una organización tenga varios recursos compartidos de implementación con varios sistemas operativos en cada recurso, el proceso de actualizar manualmente los sistemas operativos de cada recurso compartido de implementación con los Service Pack puede llevar mucho tiempo. Entre los métodos para automatizar la aplicación de Service Pack de sistema operativo en recursos compartidos de implementación se incluyen los siguientes:  

-   Copiar contenido de origen actualizado que ya contenga el Service Pack (por ejemplo, medios de Windows 7 con SP1) en la carpeta del recurso compartido de implementación en la que reside el sistema operativo, como se describe en [Automatizar la aplicación de Service Pack de sistema operativo desde medios de origen actualizados](#AutomateAppFromUSM).  

-   Aplicar el Service Pack en un equipo de referencia y, después, capturar una imagen actualizada desde un equipo de referencia, como se describe en [Automatizar la aplicación de Service Pack de sistema operativo mediante un equipo de referencia y Windows PowerShell](#AutomateAppUsingRef).  

###  <a name="AutomateAppFromUSM"></a> Automatizar la aplicación de Service Pack de sistema operativo desde medios de origen actualizados  
 Puede automatizar el proceso de actualizar Service Pack de sistema operativo mediante Windows PowerShell cuando dispone de medios de origen que incluyen el Service Pack, como un DVD que tiene Windows 7 con SP1 integrado.  

 Para este método, los medios de origen de sistema operativo con el Service Pack se copian sobre los archivos del sistema operativo existente sin el Service Pack en el recurso compartido de implementación con Windows PowerShell.  

 **Para automatizar la aplicación de Service Pack de sistema operativo desde medios de origen actualizados con Windows PowerShell**  

1.  Cargue el complemento de Windows PowerShell de MDT como se describe en [Cargar el complemento de Windows PowerShell de MDT](#LoadMDTSnapIn).  

2.  Asegúrese de que las implementaciones de MDT que comparten unidades de Windows PowerShell se restauren con el cmdlet **Restore-MDTPersistentDrive**, como se muestra en el ejemplo siguiente:  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Si las implementaciones de MDT que comparten unidades de Windows PowerShell ya están restauradas, recibirá un mensaje de advertencia que indica que el cmdlet no puede restaurar la unidad.  

3.  Para ver la lista de implementaciones de MDT que comparten unidades de Windows PowerShell, una para cada recurso compartido de implementación, use el cmdlet [Get-PSDrive](http://technet.microsoft.com/library/hh849796) como se muestra en el ejemplo siguiente:  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     Se muestra la lista de unidades de Windows PowerShell que se proporcionan con MDTProvider, una para cada recurso compartido de implementación.  

4.  Para quitar del recurso compartido de implementación la carpeta para el sistema operativo existente, use los cmdlets [Get-ChildItem](http://technet.microsoft.com/library/hh849800) y [Remove-Item](http://technet.microsoft.com/library/hh849765), como se muestra en el ejemplo siguiente:  

    ```  
    Get-ChildItem “DS002:\Operating Systems\Windows 7” –recurse | Remove-Item –recurse –force  
    ```  

     En este ejemplo, *DS002:* es el nombre de una unidad de Windows PowerShell que se devuelve en el paso 3.  

5.  Copie el contenido de los archivos de código fuente del sistema operativo que tienen integrado el Service Pack mediante el cmdlet [Copy-Item](http://technet.microsoft.com/library/hh849793), como se muestra en el ejemplo siguiente:  

    ```  
    Copy-Item "E:\*" -Destination "DS002:\Operating Systems\Windows 7"-Recurse -Force  
    ```  

     En este ejemplo, los archivos de código fuente del sistema operativo se encuentran en la unidad E, y *DS002:* es el nombre de una unidad de Windows PowerShell que se devuelve en el paso 3.  

6.  Actualice los medios de implementación de MDT en función de recurso compartido de implementación con el cmdlet **Update-MDTMedia**.  

 Para más información sobre cómo actualizar los medios de implementación de MDT en función del recurso compartido de implementación con el cmdlet **Update-MDTMedia**, vea [Actualizar medios de implementación con Windows PowerShell](#UpdateDeployMedia).  

###  <a name="AutomateAppUsingRef"></a> Automatizar la aplicación de Service Pack de sistema operativo mediante un equipo de referencia y Windows PowerShell  
 Puede automatizar el proceso de actualizar Service Pack de sistema operativo con Windows PowerShell si solo tiene un Service Pack que aún no está integrado en el sistema operativo, por ejemplo, si dispone de SP1 para Windows 7 y todavía no está integrado en una imagen de Windows 7.  

 Para este método, implemente el sistema operativo sin el Service Pack en un equipo de referencia. Después, aplique el Service Pack en el equipo de referencia. Luego, capture una imagen de sistema operativo del equipo de referencia. Por último, copie el archivo .wim capturado sobre el archivo Install.wim en el sistema operativo del recurso compartido de implementación con Windows PowerShell.  

 **Para automatizar la aplicación de Service Pack de sistema operativo desde medios de origen actualizados con Windows PowerShell**  

1.  Implemente el sistema operativo de destino en un equipo de referencia.  

     Para más información sobre cómo realizar una implementación en un equipo de referencia, vea los recursos siguientes en el documento de MDT *Using the Microsoft Deployment Toolkit* (Uso de Microsoft Deployment Toolkit):  

    -   "Preparing for LTI Deployment to the Reference Computer" (Preparación para la implementación de LTI en el equipo de referencia).  

    -   "Deploying To and Capturing an Image of the Reference Computer in LTI" (Implementación y captura de una imagen del equipo de referencia de LTI).  

2.  Instale el Service Pack deseado en el equipo de referencia.  

     Para más información sobre cómo instalar el Service Pack, vea la documentación que lo acompaña.  

3.  Capture una imagen del equipo de referencia mediante la creación y la implementación de una secuencia de tareas basada en la plantilla de secuencia de tareas **Sysprep y captura**.  

     Para más información sobre cómo crear una secuencia de tareas basada en la plantilla de secuencia de tareas **Sysprep y captura**, vea "Create a New Task Sequence in the Deployment Workbench" (Crear una secuencia de tareas en Deployment Workbench).  

4.  Cargue el complemento de Windows PowerShell de MDT como se describe en [Cargar el complemento de Windows PowerShell de MDT](#LoadMDTSnapIn).  

5.  Asegúrese de que las implementaciones de MDT que comparten unidades de Windows PowerShell se restauren con el cmdlet **Restore-MDTPersistentDrive**, como se muestra en el ejemplo siguiente:  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Si las implementaciones de MDT que comparten unidades de Windows PowerShell ya están restauradas, recibirá un mensaje de advertencia que indica que el cmdlet no puede restaurar la unidad.  

6.  Para ver la lista de implementaciones de MDT que comparten unidades de Windows PowerShell, una para cada recurso compartido de implementación, use el cmdlet [Get-PSDrive](http://technet.microsoft.com/library/hh849796) como se muestra en el ejemplo siguiente:  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     Se muestra la lista de unidades de Windows PowerShell que se proporcionan con MDTProvider, una para cada recurso compartido de implementación.  

7.  Copie el archivo .wim capturado en el paso 3 sobre el archivo Install.wim en el sistema operativo del recurso compartido de implementación mediante el cmdlet [Copy-Item](http://technet.microsoft.com/library/hh849793), como se muestra en el ejemplo siguiente:  

    ```  
    Copy-Item "DS002:\Captures\Win7SP1.wim" -Destination "DS002:\Operating Systems\Windows 7\sources\Install.wim" Force  
    ```  

     En este ejemplo, el archivo de imagen de sistema operativo capturado (Win7SP1.wim) en la carpeta de capturas del recurso compartido DS002: es el nombre de una unidad de Windows PowerShell que se devuelve en el paso 6, y el sistema operativo Windows 7 existente se almacena en una carpeta denominada  *Windows 7*.  

8.  Actualice los medios de implementación de MDT en función de recurso compartido de implementación con el cmdlet **Update-MDTMedia**.  

     Para más información sobre cómo actualizar los medios de implementación de MDT en función del recurso compartido de implementación con el cmdlet **Update-MDTMedia**, vea [Actualizar medios de implementación con Windows PowerShell](#UpdateDeployMedia).  

## <a name="customizing-deployment-based-on-chassis-type"></a>Personalizar una implementación basada en el tipo de chasis  
 Puede personalizar una implementación basada en el tipo de chasis del equipo. Los scripts crean variables locales que se pueden procesar en el archivo CustomSettings.ini. Las variables locales `IsLaptop`, `IsDesktop` y `IsServer` indican si se trata de un equipo portátil, un equipo de escritorio o un servidor, respectivamente.  

> [!NOTE]
>  En versiones anteriores de Deployment Workbench, la marca `IsServer` indicaba que el sistema operativo existente era un sistema operativo de servidor (por ejemplo, Windows Server 2003 Enterprise Edition). El nombre de esta marca se ha cambiado a `IsServerOS`.  

 **Para implementar variables locales en el archivo CustomSettings.ini**  

1.  En la sección `[Settings]`, en la línea `Priority`, agregue una sección personalizada para personalizar la implementación según el tipo de chasis (`ByChassisType` en el ejemplo siguiente, donde *Chassis* representa el tipo de equipo).  

2.  Cree la sección personalizada que se corresponda con la sección personalizada definida en el paso 1 (`ByChassisType` en el ejemplo siguiente, donde *Chassis* representa el tipo de equipo).  

3.  Defina una subsección para que la detecte cada tipo de chasis (`Subsection=Laptop-%IsLaptop%, Subsection=Desktop-%IsDesktop%, Subsection=Server-%IsServer%` en el ejemplo siguiente).  

4.  Cree una subsección para cada estado `True` y `False` de cada subsección definida en el paso 3 (como `[Laptop-True], [Laptop-False], [Desktop-True], [Desktop-False]` en el ejemplo siguiente).  

5.  Bajo cada subsección `True` y `False`, agregue la configuración adecuada en función del tipo de chasis.  

 **Lista 1. Ejemplo de personalización de implementación basada en el tipo de chasis en el archivo CustomSettings.ini**  

```  
[Settings]  

Priority=...,ByLaptopType,ByDesktopType,ByServerType  

[ByLaptopType]  
Subsection=Laptop-%IsLaptop%  

[ByDesktopType]  
Subsection=Desktop-%IsDesktop%  

[ByServerType]  
Subsection=Server-%IsServer%  
.  
.  
.  

[Laptop-True]  
.  
.  
.  

[Laptop-False]  
.  
.  
.  

[Desktop-True]  
.  
.  
.  

[Desktop-False]  
.  
.  
.  

[Server-True]  
.  
.  
.  

[Server-False]  
.  
.  
.  
```  

## <a name="deploying-applications-based-on-earlier-application-versions"></a>Implementar aplicaciones basadas en versiones anteriores de la aplicación  
 A menudo, cuando se instala un sistema operativo en un equipo, se instalan las mismas aplicaciones que ya se habían instalado en el equipo. Hágalo mediante scripts de MDT (en particular, ZTIGather.wsf) para consultar dos orígenes de información diferentes:  

-   **La característica de inventario de software de Configuration Manager.** Contiene un registro para cada paquete de aplicación (en este caso, la lista de Programa y características de Windows 8.1, Windows 8, Windows 7, Windows Server 2012 R2, Windows Server 2012 y Windows Server 2008 R2) que estaba instalado la última vez que Configuration Manager realizó un inventario del equipo.  

-   **Una tabla de asignación.** Describe qué paquete y programa deben instalarse para cada registro (dado que los registros de Programa y características y de Agregar o quitar programas no especifican exactamente qué paquete ha instalado la aplicación, lo que hace que sea imposible seleccionar de forma automática el paquete únicamente en función del inventario).  

 **Para realizar una instalación dinámica de aplicación específica del equipo**  

1.  Use la tabla de la base de datos de MDT para conectar paquetes específicos con las aplicaciones que se enumeran en el sistema operativo de destino.  

2.  Rellene la tabla con datos que asocien el paquete adecuado con la aplicación indicada en Programa y características o Agregar o quitar programas.

     **Consulta SQL para rellenar la tabla**  

    ```  
    use [MDTDB]  
    go  
    INSERT INTO [PackageMapping] (ARPName, Packages) VALUES('Office12.0', 'XXX0000F:Install Office 2010 Professional Plus')  
    go  
    ```  

     La fila insertada conecta cualquier equipo que tenga la entrada `Office12.0` con el paquete Microsoft Office 2010 Professional Plus.  

     Esto significa que Microsoft Office 2010 Professional Plus se instalará en cualquier equipo que ejecute el sistema Microsoft Office 2007 (Office 12.0). Agregue entradas similares para los demás paquetes. Todos los elementos para los que no haya entradas se omitirán (no se instalará ningún paquete).  

3.  Cree un procedimiento almacenado para simplificar el proceso de combinar la información en la nueva tabla con los datos de inventario.  

    ```  
    use [MDTDB]  
    go  

    if exists (select * from dbo.sysobjects where id = object_id(N'[dbo].[RetrievePackages]') and OBJECTPROPERTY(id, N'IsProcedure') = 1)  
    drop procedure [dbo].[RetrievePackages]  
    go  

    CREATE PROCEDURE [dbo].[RetrievePackages]  
    @MacAddress CHAR(17)  
    AS  

    SET NOCOUNT ON  

    /* Select and return all the appropriate records based on current inventory */  
    SELECT * FROM PackageMapping  
    WHERE ARPName IN  
    (  
      SELECT ProdID0 FROM CM_DB.dbo.v_GS_ADD_REMOVE_PROGRAMS a, CM_DB.dbo.v_GS_NETWORK_ADAPTER n  
      WHERE a.ResourceID = n.ResourceID AND  
      MACAddress0 = @MacAddress  
    )  
    go  
    ```  

     El procedimiento almacenado del ejemplo anterior da por supuesto que la base de datos del sitio primario central de Configuration Manager reside en el equipo en el que SQL Server se ejecuta como base de datos de MDT. Si la base de datos del sitio primario central reside en un equipo diferente, es necesario realizar las modificaciones apropiadas en el procedimiento almacenado. Además, el nombre de la base de datos (`CM_DB`) debe actualizarse. También considere la posibilidad de conceder a cuentas adicionales acceso de lectura a la vista **v_GS_ADD_REMOVE_PROGRAMS** en la base de datos de Configuration Manager.  

4.  Para configurar el archivo CustomSettings.ini de modo que consulte esta tabla de base de datos, especifique el nombre de una sección (`[DynamicPackages]` en la lista **Priority**) que apunte a la información de la base de datos.  

    ```  
    [Settings]  
    …  
    Priority=MacAddress, DefaultGateway, DynamicPackages, Default  
    …  
    ```  

5.  Cree una sección `[DynamicPackages]` para especificar el nombre de una sección de base de datos.  

    ```  
    [DynamicPackages]  
    SQLDefault=DB_DynamicPackages  
    ```  

6.  Cree una sección de base de datos para especificar la información de la base de datos y los detalles de la consulta.  

    ```  
    [DB_DynamicPackages]  
    SQLServer=SERVER1  
    Database=MDTDB  
    StoredProcedure=RetrievePackages  
    Parameters=MacAddress  
    SQLShare=Logs  
    Instance=SQLEnterprise2005  
    Port=1433  
    Netlib=DBNMPNTW  
    ```  

     En el ejemplo anterior, se consultará la base de datos de MDT denominada *MDTDB* en el equipo que ejecuta la instancia de SQL Server denominada *SERVER1*. La base de datos contiene un procedimiento almacenado denominado `RetrievePackages` (creado en el paso 3).  

 Cuando se ejecuta ZTIGather.wsf, se genera automáticamente una instrucción `SELECT` de Lenguaje de consulta estructurado (SQL) y el valor de la clave personalizada **MakeModelQuery** se pasa como un parámetro a la consulta:  

 ```  
 EXECUTE RetrievePackages ?  
 ```  

 El valor real de la clave personalizada **MACAddress** se sustituirá por el correspondiente signo "?".  Esta consulta devuelve un conjunto de registros con las filas que se especificaron en el paso 2.  

 No se puede pasar un número variable de argumentos a un procedimiento almacenado. Como resultado, cuando un equipo tiene más de una dirección MAC, no se pueden pasar todas las direcciones MAC al procedimiento almacenado. Como alternativa, reemplace el procedimiento almacenado por una vista que permita su consulta con una instrucción `SELECT` con una cláusula `IN` para pasar todos los valores de dirección MAC.  

 En el escenario presentado en este caso, si el equipo actual tiene el valor `Office12.0` insertado en la tabla (paso 2), se devuelve una fila (`XXX0000F:Install Office 2010 Professional Plus`). Esto indica que el proceso de ZTI instalará el paquete XXX0000F:Install Office 2001 Professional Plus durante la fase de restauración de estado.  

## <a name="fully-automated-lti-deployment-scenario"></a>Escenario de implementación de LTI totalmente automatizado  
 El propósito principal de LTI es automatizar al máximo el proceso de implementación. Aunque ZTI proporciona una automatización completa de la implementación mediante los scripts de MDT y Servicios de implementación de Windows, LTI está diseñado para funcionar con menos requisitos de infraestructura.  

 Puede automatizar el Asistente para la implementación de Windows usado en el proceso de implementación de LTI para reducir (o eliminar) las páginas del asistente que se muestran. Para omitir todo el Asistente para la implementación de Windows, especifique la propiedad **SkipWizard** en CustomSettings.ini. Para omitir páginas individuales del asistente, use las propiedades siguientes:  

-   **SkipAdminPassword**  

-   **SkipApplications**  

-   **SkipBDDWelcome**  

-   **SkipBitLocker**  

-   **SkipBitLockerDetails**  

-   **SkipTaskSequence**  

-   **SkipCapture**  

-   **SkipComputerBackup**  

-   **SkipComputerName**  

-   **SkipDomainMembership**  

-   **SkipFinalSummary**  

-   **SkipLocaleSelection**  

-   **SkipPackageDisplay**  

-   **SkipProductKey**  

-   **SkipSummary**  

-   **SkipTimeZone**  

-   **SkipUserData**  

Para más información sobre cada una de estas propiedades, vea la propiedad correspondiente en el documento de MDT *Toolkit Reference* (Referencia del kit de herramientas).  

Para cada página omitida del asistente, proporcione los valores de las propiedades correspondientes que se suelen recopilar a través de la página del asistente en los archivos CustomSettings.ini y BootStrap.ini. Para más información sobre las propiedades que se deben configurar en estos archivos, vea la sección "Providing Properties for Skipped Deployment Wizard Pages" (Proporcionar propiedades para las páginas omitidas del Asistente para la implementación) en el documento de MDT *Toolkit Reference* (Referencia del kit de herramientas).  

## <a name="fully-automated-lti-deployment-for-a-refresh-computer-scenario"></a>Implementación de LTI completamente automatizada para un escenario de actualización de equipo  
 En el ejemplo siguiente se muestra un archivo CustomSettings.ini que se usa en un escenario de actualización de equipo para omitir todas las páginas del Asistente para la implementación de Windows. En este ejemplo, las propiedades que se deben proporcionar al omitir la página del asistente se encuentran justo debajo de la propiedad que omite la página del asistente.  

```  
[Settings]  
Priority=Default  
Properties=MyCustomProperty  

[Default]  
OSInstall=Y  
ScanStateArgs=/v:5 /o /c  
LoadStateArgs=/v:5 /c /lac /lae  
SkipCapture=YES  
SkipAdminPassword=YES  
SkipProductKey=YES  

DeploymentType=REFRESH  

SkipDomainMembership=YES  
JoinDomain=DomainName  
DomainAdmin=Administrator  
DomainAdminDomain=DomainName  
DomainAdminPassword=a_secure_password  

SkipUserData=yes  
UserDataLocation=AUTO  
UDShare=\\Servername\Sharename\Directory  
UDDir=%ComputerName%  

SkipComputerBackup=YES  
ComputerBackuplocation=AUTO  
BackupShare=\\Servername\Backupsharename  
BackupDir=%ComputerName%  

SkipTaskSequence=YES  
TaskSequenceID=Enterprise  

SkipComputerName=YES  
OSDComputerName=%ComputerName%  

SkipPackageDisplay=YES  
LanguagePacks001={3af4e3ce-8122-41a2-9cf9-892145521660}  
LanguagePacks002={84fc70d4-db4b-40dc-a660-d546a50bf226}  

SkipLocaleSelection=YES  
UILanguage=en-US  
UserLocale=en-CA  
KeyboardLocale=0409:00000409  

SkipTimeZone=YES  
TimeZoneName=China Standard Time  

SkipApplications=YES  
Applications001={a26c6358-8db9-4615-90ff-d4511dc2feff}  
Applications002={7e9d10a0-42ef-4a0a-9ee2-90eb2f4e4b98}  
UserID=Administrator  
UserDomain=DomainName  
UserPassword=P@ssw0rd  

SkipBitLocker=YES  
SkipSummary=YES  
Powerusers001=DomainName\Username  
```  

## <a name="fully-automated-lti-deployment-for-a-new-computer-scenario"></a>Implementación de LTI completamente automatizada para un escenario de equipo nuevo  
 En el ejemplo siguiente se muestra un ejemplo de un archivo CustomSettings.ini que se usa en un escenario de equipo nuevo para omitir todas las páginas del Asistente para la implementación de Windows. En este ejemplo, las propiedades que se deben proporcionar al omitir la página del asistente se encuentran justo debajo de la propiedad que omite la página del asistente.  

```  
[Settings]  
Priority=Default  
Properties=MyCustomProperty  

[Default]  
OSInstall=Y  
ScanStateArgs=/v:5 /o /c  
LoadStateArgs=/v:5 /c /lac /lae  

SkipCapture=YES  
ComputerBackupLocation=\\WDG-MDT-01\Backup$\  
BackupFile=MyCustomImage.wim  

SkipAdminPassword=YES  
SkipProductKey=YES  

SkipDomainMembership=YES  
JoinDomain=WOODGROVEBANK  
DomainAdmin=Administrator  
DomainAdminDomain=WOODGROVEBANK  
DomainAdminPassword=P@ssw0rd  

SkipUserData=Yes  
UserDataLocation=\\WDG-MDT-01\UserData$\Directory\usmtdata  

SkipTaskSequence=YES  
TaskSequenceID=Enterprise  

SkipComputerName=YES  
OSDComputerName=%SerialNumber%  

SkipPackageDisplay=YES  
LanguagePacks001={3af4e3ce-8122-41a2-9cf9-892145521660}  
LanguagePacks002={84fc70d4-db4b-40dc-a660-d546a50bf226}  

SkipLocaleSelection=YES  
UILanguage=en-US  
UserLocale=en-CA  
KeyboardLocale=0409:00000409  

SkipTimeZone=YES  
TimeZoneName=China Standard Time  

SkipApplications=YES  
Applications001={a26c6358-8db9-4615-90ff-d4511dc2feff}  
Applications002={7e9d10a0-42ef-4a0a-9ee2-90eb2f4e4b98}  

SkipBitLocker=YES  
SkipSummary=YES  
Powerusers001=WOODGROVEBANK\PilarA  
CaptureGroups=YES  
SLShare=\\WDG-MDT-01\UserData$\Logs  
Home_page=http://www.microsoft.com/NewComputer  
```  

## <a name="calling-web-services-in-mdt"></a>Llamadas a servicios web en MDT  
 En versiones anteriores de MDT, se admitía el procesamiento de reglas mediante CustomSettings.ini y bases de datos, desde donde se podían recuperar valores del equipo local (normalmente mediante WMI) para tomar decisiones sobre lo que se debía hacer en cada equipo durante la implementación. Además, se podían realizar consultas SQL y llamadas a procedimientos almacenados para recuperar información adicional de bases de datos externas. Aun así, este enfoque planteaba problemas, especialmente a la hora de realizar conexiones seguras de SQL.  

 Para ayudar a solucionar estas cuestiones, MDT puede realizar llamadas al servicio web de acuerdo con reglas simples definidas en CustomSettings.ini. Estas solicitudes de servicio web no requieren ningún contexto de seguridad especial y pueden usar cualquier puerto TCP/IP necesario para simplificar las configuraciones de firewall.  

 A continuación muestra cómo configurar CustomSettings.ini para llamar a un servicio web determinado. En este escenario, el servicio web se elige aleatoriamente a partir de una búsqueda en Internet. Se usa un código postal como entrada y se devuelve la ciudad, el estado, el código de área y la zona horaria (como una letra) para el código postal especificado.  

```  
[Settings]  
Priority=Default, USZipService  
Properties=USZip, City, State, Zip, Area_Code, Time_Zones   
[Default]  
USZip=98052   
[USZipService]  
WebService=http://www.webservicex.net/uszip.asmx/GetInfoByZIP  
Parameters=USZip  
```  

 Cuando se ejecuta este código, se obtiene una salida similar al siguiente:
```  
Added new custom property USZIP  
Added new custom property CITY  
Added new custom property STATE  
Added new custom property ZIP  
Added new custom property AREA_CODE  
Added new custom property TIME_ZONES  
Using from [Settings]: Rule Priority = DEFAULT, USZIPSERVICE  
------ Processing the [DEFAULT] section ------  
Property USZIP is now = 98052  
Using from [DEFAULT]: USZIP = 98052  
------ Processing the [USZIPSERVICE] section ------  
Using COMMAND LINE ARG: Ini file = CustomSettings.ini  
CHECKING the [USZIPSERVICE] section  
About to execute web service call to http://www.webservicex.net/uszip.asmx/GetInfoByZIP: USZip=98052  
Response from web service: 200 OK  
Successfully executed the web service.  
Property CITY is now = Redmond  
Obtained CITY value from web service:  CITY = Redmond  
Property STATE is now = WA  
Obtained STATE value from web service:  STATE = WA  
Property ZIP is now = 98052  
Obtained ZIP value from web service:  ZIP = 98052  
Property AREA_CODE is now = 425  
Obtained AREA_CODE value from web service:  AREA_CODE = 425  
------ Done processing CustomSettings.ini ------  
```  

 Hay algunas complicaciones poco importantes que es necesario tener en cuenta al ejecutar un servicio web:  

-   No haga nada especial con los servidores proxy. Si hay un servidor proxy anónimo, úselo, pero la autenticación de servidores proxy puede causar problemas. En la mayoría de los casos, no se llamará a un servicio web.  

-   CustomSettings.ini o ZTIGather.xml busca las propiedades definidas en el marcado XML que se devuelve como resultado de la llamada al servicio web (de la misma forma que sucede con una consulta de base de datos u otra regla). El problema es que la búsqueda XML distingue entre mayúsculas y minúsculas. Afortunadamente, el servicio web que se describe aquí devuelve todos los nombres de propiedad en mayúsculas, que es lo que espera ZTIGather.xml. Es posible volver a asignar entradas en minúsculas o en mayúsculas y minúsculas mezcladas para solucionar este problema.  

-   Se recomienda una solicitud `POST` al servicio web, por lo que la llamada al servicio web debe admitir las solicitudes `POST`.  

## <a name="connecting-to-network-resources"></a>Conectarse a recursos de red  
 Durante los procesos de implementación de LTI y ZTI, puede que necesite tener acceso a un recurso de red en un servidor diferente desde el servidor que hospeda el recurso compartido de implementación. Debe estar autenticado en el otro servidor para poder tener acceso a las carpetas compartidas o los servicios que contiene. Por ejemplo, puede instalar una aplicación desde una carpeta compartida de un servidor distinto del que hospeda el recurso compartido de implementación que usan los scripts de MDT.  

> [!NOTE]
>  Para consultar las bases de datos de SQL Server hospedadas en un servidor que no sea el que hospeda el recurso compartido de implementación, vea las propiedades **Database**, **DBID**, **DBPwd**, **Instance**, **NetLib**, **Order**, **Parameters**, **ParameterCondition**, **SQLServer**, **SQLShare** y **Table** en el documento de MDT *Toolkit Reference* (Referencia del kit de herramientas).  

 Con el script ZTIConnect.wsf, puede conectarse a otros servidores y tener acceso a los recursos que contienen. La sintaxis del script ZTIConnect.wsf es la que se indica a continuación, donde *unc_path* es una ruta de acceso de convención de nomenclatura universal (UNC) para conectarse al servidor:  

```  
Cscript.exe “%SCRIPTROOT%\ZTIConnect.wsf” /uncpath:unc_path  
```  

 En la mayoría de los casos, el script ZTIConnect.wsf se ejecuta como una tarea del secuenciador de tareas. Ejecute el script ZTIConnect.wsf antes de las tareas que requieren acceso a un servidor que no sea el que hospeda el recurso compartido de implementación.  

 **Para agregar el script ZTIConnect.wsf como una tarea a la secuencia de tareas de una compilación**  

1.  Haga clic en **Inicio** y seleccione **All Programs** (Todos los programas). Seleccione **Microsoft Deployment Toolkit** y haga clic en **Deployment Workbench**.  

2.  En el árbol de consola de Deployment Workbench, vaya a Deployment Workbench/Deployment Shares (Recursos compartidos de implementación)/*deployment_share*/Secuencias de tareas, donde *deployment_share* es el nombre del recurso compartido de implementación que se va a configurar.  

3.  En el panel de detalles, haga clic en ***task_sequence***, donde *task_sequence* es la secuencia de tareas que se va a modificar.  

4.  En el panel Acciones, haga clic en **Propiedades**.  

5.  Haga clic en la pestaña Secuencia de tareas, vaya a **grupo**, donde *grupo* es el grupo en el que se va a ejecutar el script ZTIConnec.wsf, y haga clic en **Agregar**. Haga clic en **General** y en **Ejecutar línea de comandos**.  

    > [!NOTE]
    >  Agregue la tarea antes de agregar las tareas que requieren acceso a los recursos del servidor de destino.  

6.  Rellene la pestaña **Propiedades** de la nueva tarea con la información siguiente:

    |**En este cuadro** |**Haga esto** |  
    |-|-|  
    |**Nombre** |Escriba **Conectar a servidor** (donde servidor es el nombre del servidor al que se va a conectar).|  
    |**Descripción** |Escriba un texto que explique por qué se debe realizar la conexión.|  
    |**Comando** |Escriba **Cscript.exe “%SCRIPTROOT%\ZTIConnect.wsf” /uncpath:unc_path**, donde *unc_path* es la ruta de acceso UNC a una carpeta compartida del servidor.|  

7.  Rellene la pestaña **Opciones** de la nueva tarea con la información siguiente. A menos que se especifique lo contrario, acepte los valores predeterminados y haga clic en **Aceptar**.  

    |**En este cuadro** |**Haga esto** |  
    |-|-|  
    |**Códigos de éxito** |Escriba **0 3010**. (El script ZTIConnect.wsf devuelve estos códigos tras finalizar correctamente).|  
    |**Lista de condiciones** |Agregue las condiciones que sean necesarias. (En la mayoría de los casos, esta tarea no requiere ninguna condición).|  

 Después de agregar la tarea que ejecutará el script ZTIConnect.wsf, las tareas siguientes pueden tener acceso a los recursos de red del servidor especificado en la opción **/uncpath** del script ZTIConnect.wsf.  

## <a name="deploying-the-correct-device-drivers-to-computers-with-the-same-hardware-devices-but-different-make-and-model"></a>Implementar los controladores de dispositivo correctos en equipos con los mismos dispositivos de hardware pero marca y modelo diferentes  
 Pueden existir variaciones con prácticamente ninguna diferencia en los nombres y números de modelo en el conjunto de controladores. Estas variaciones en los nombres y los números de modelo pueden aumentar innecesariamente el tiempo invertido en realizar varias entradas de base de datos para un modelo determinado. El siguiente procedimiento muestra cómo definir una propiedad nueva mediante una llamada de función de salida de usuario que devuelve una subcadena del número de modelo.  

 **Para crear alias de modelo**  

1.  Haga clic en **Inicio** y seleccione **All Programs** (Todos los programas). Seleccione **Microsoft Deployment Toolkit** y haga clic en **Deployment Workbench**.  

2.  En el árbol de consola de Deployment Workbench, vaya a Deployment Workbench/Deployment Shares (Recursos compartidos de implementación)/*deployment_share*, donde *deployment_share* es el nombre del recurso compartido de implementación que se va a configurar.  

3.  En el panel Acciones, haga clic en **Propiedades**.  

4.  En el cuadro de diálogo **Propiedades**, haga clic en la pestaña **Reglas**.  

5.  Cree alias para los tipos de hardware en las secciones Marca y Modelo de la base de datos de MDT. Trunque el tipo de modelo en el paréntesis de apertura "(" en el nombre de modelo. Por ejemplo, *HP DL360 (G112)* se convierte en *HP DL360*.  

6.  Agregue la variable personalizada **ModelAlias** a cada sección.  

7.  Cree una sección `[SetModel]`.  

8.  Agregue la sección `[SetModel]` a la opción de configuración **Prioridad** de la sección `[Settings]`.  

9. Agregue una línea a la sección `ModelAlias` para hacer referencia a un script de salida de usuario que truncará el nombre del modelo en "(".  

10. Cree una búsqueda de base de datos **MMApplications**, donde **ModelAlias** es igual a **Modelo**.  

11. Cree un script de salida de usuario y colóquelo en el mismo directorio que el archivo CustomSettings.ini para truncar el nombre del modelo.  

    A continuación se muestra un archivo CustomSettings.ini y el script de salida de usuario, respectivamente.  

     **CustomSettings.ini**:  

    ```  
    [Settings]   
    Priority=SetModel, MMApplications, Default   
    Properties= ModelAlias   
    [SetModel]   
    ModelAlias=#SetModelAlias()#   
    Userexit=Userexit.vbs   
    [MMApplications]   
    SQLServer=Server1  
    Database=MDTDB   
    Netlib=DBNMPNTW   
    SQLShare=logs   
    Table= MakeModelSettings    
    Parameters=Make, ModelAlias   
    ModelAlias=Model   
    Order=Sequence  
    ```  

     **Script de salida de usuario**:  

    ```  
    Function UserExit(sType, sWhen, sDetail, bSkip)   
      UserExit = Success   
    End Function   

    Function SetModelAlias()   
      If Instr(oEnvironment.Item("Model"), "(") <> 0 Then   
        SetModelAlias = Left(oEnvironment.Item("Model"), _  
                          Instr(oEnvironment.Item("Model"), _  
                            "(") - 1)   
        oLogging.CreateEntry "USEREXIT – " & _  
          "ModelAlias has been set to " & SetModelAlias, _  
          LogTypeInfo  
      Else   
        SetModelAlias = oEnvironment.Item("Model")   
        oLogging.CreateEntry " USEREXIT - " & _  
          "ModelAlias has not been changed.", LogTypeInfo   
      End if   
    End Function  
    ```  

## <a name="configuring-conditional-task-sequence-steps"></a>Configurar pasos condicionales de secuencia de tareas  
 En algunos escenarios, debe considerar la posibilidad de ejecutar un paso de secuencia de tareas basado de forma condicional en criterios definidos. Se puede agregar cualquier combinación de estas condiciones para determinar si se debe ejecutar el paso de secuencia de tareas. Por ejemplo, use el valor de una variable de secuencia de tareas y el valor de una configuración del Registro para determinar si se debe ejecutar un paso de secuencia de tareas.  

 Con MDT, ejecute una secuencia de tareas basada de forma condicional en:  

-   Una o varias instrucciones **IF**  

-   Una variable de secuencia de tareas  

-   La versión del sistema operativo de destino  

-   Los resultados booleanos de una consulta WMI  

-   Una configuración del Registro  

-   El software instalado en el equipo de destino  

-   Las propiedades de una carpeta  

-   Las propiedades de un archivo  

### <a name="configuring-a-conditional-task-sequence-step"></a>Configurar un paso condicional de secuencia de tareas  
 Los pasos condicionales de secuencia de tareas se configuran en Deployment Workbench, en la pestaña **Opciones** de un paso de secuencia de tareas. Puede agregar una o varias condiciones al paso de secuencia de tareas para crear la condición adecuada para ejecutar o no ejecutar el paso.  

> [!NOTE]
>  Cada paso condicional de secuencia de tareas necesita al menos una instrucción **IF**.  

 **Para ver la pestaña Opciones de un paso de secuencia de tareas**  

1.  Haga clic en **Inicio** y seleccione **All Programs** (Todos los programas). Seleccione **Microsoft Deployment Toolkit** y haga clic en **Deployment Workbench**.  

2.  En el árbol de consola de Deployment Workbench, vaya a Deployment Workbench/Deployment Shares (Recursos compartidos de implementación)/*deployment_share*/Secuencias de tareas, donde *deployment_share* es el nombre del recurso compartido de implementación que se va a configurar.  

3.  En el panel de detalles, haga clic en **task_sequence**, donde *task_sequence* es el nombre de la secuencia de tareas que se va a configurar.  

4.  En el panel Acciones, haga clic en **Propiedades**.  

5.  En el cuadro de diálogo **Propiedades de** ***task_sequence***, en la pestaña **Secuencia de tareas**, haga clic en ***paso*** (donde *paso* es el nombre del paso de secuencia de tareas que se va a configurar) y haga clic en la pestaña **Opciones**.  

 En la pestaña **Opciones** del paso de secuencia de tareas, realice las acciones siguientes:  

-   **Agregar.** Haga clic en este botón para agregar una condición al paso de secuencia de tareas.  

-   **Quitar.** Haga clic en este botón para quitar una condición de un paso de secuencia de tareas.  

-   **Editar.** Haga clic en este botón para modificar una condición de un paso de secuencia de tareas.  

### <a name="if-statements-in-conditions"></a>Instrucciones IF en condiciones  
 Todas las condiciones de secuencia de tareas incluyen una o varias instrucciones **IF**. Las instrucciones **IF** son la base para crear pasos condicionales de secuencia de tareas. Una condición de paso de secuencia de tareas puede incluir una sola instrucción **IF**, pero se pueden anidar varias instrucciones **IF** bajo la instrucción **IF** de nivel superior para crear condiciones más complejas.  

 Una instrucción **IF** puede basarse en las condiciones indicadas en la tabla siguiente, que se configuran en el cuadro de diálogo **IF Statement Properties** (Propiedades de la instrucción IF).  

 |**Condición** |**Seleccione esta opción para ejecutar la secuencia de tareas si…** |  
 |-|-|  
 |**Todas las condiciones** |Todas las condiciones bajo esta instrucción **IF** deben ser True.|  
 |**Cualquier condición** |Cualquier condición bajo esta instrucción **IF** es True.|  
 |**Ninguno** |Ninguna condición bajo esta instrucción **IF** es True.|  

 Complete la condición para ejecutar el paso de secuencia de tareas mediante la adición de otros criterios a las condiciones (por ejemplo, variables de secuencia de tareas o valores de una configuración del Registro).  

 **Para agregar una condición Instrucción IF a un paso de secuencia de tareas**  

1.  En la pestaña **Opción de** ***paso*** (donde *paso* es el nombre del paso de secuencia de tareas que se va a configurar), haga clic en **Agregar** y en **If statement** (Instrucción IF).  

2.  En el cuadro de diálogo **If Statement Properties** (Propiedades de la instrucción IF), haga clic en **condición** (donde *condición* es una de las condiciones que se muestran en la tabla anterior) y, después, haga clic en **Aceptar**.  

### <a name="task-sequence-variables-in-conditions"></a>Variables de secuencias de tareas en condiciones  
 Use la condición **Variable de secuencia de tareas** para evaluar cualquier variable de secuencia de tareas creada por una tarea **Configurar variable de secuencia de tareas** o por cualquier tarea de la secuencia de tareas. Por ejemplo, considere una red que contiene equipos cliente de Windows XP que forman parte de un dominio y otros que pertenecen a un grupo de trabajo. Sabiendo que la directiva de dominio actual obliga a guardar en la red todas las configuraciones de usuario, es posible que la configuración de usuario se deba guardar únicamente para los equipos que no forman parte del dominio, es decir, para los equipos que pertenecen al grupo de trabajo. En este caso, agregue una condición a la tarea **Capture User Files and Settings** (Capturar archivos y configuración de usuario) que tiene como destino los equipos del grupo de trabajo.  

 **Para agregar una condición basada en una variable de secuencia de tareas**  

1.  En la pestaña **Opciones de** ***paso*** (donde *paso* es el nombre del paso de secuencia de tareas que se va a configurar), haga clic en **Agregar condición** y en **Variable de secuencia de tareas**.  

2.  En el cuadro de diálogo Condición de **Variable de secuencia de tareas**, en el cuadro **Variable**, escriba **OSDJoinType**.  

    > [!NOTE]
    >  Esta variable se establece en **0** para los equipos que están unidos a un dominio y en **1** para los que pertenecen a un grupo de trabajo.  

3.  En el cuadro **Condición**, haga clic en **igual**.  

4.  En el cuadro **Valor**, escriba **1** y haga clic en **Siguiente**.  

### <a name="operating-system-version-in-conditions"></a>Versión del sistema operativo en condiciones  
 Use la condición **Versión del sistema operativo** para comprobar la versión del sistema operativo de un equipo de destino o del cliente (al capturar una imagen). Por ejemplo, considere una red que contiene varios servidores que se actualizarán de Windows Server 2003 a Windows Server 2008. La configuración de red debe copiarse y aplicarse solo a servidores que ejecutan Windows Server 2003. Los demás servidores tendrán la configuración de red predeterminada que usa Windows Server 2008.  

 **Para agregar una condición basada en la versión del sistema operativo**  

1.  En el Editor de secuencia de tareas, haga clic en la tarea **Capturar configuración de red**.  

2.  Haga clic en **Agregar condición** y en **Versión del sistema operativo**.  

3.  En el cuadro **Arquitectura**, haga clic en el servidor que corresponda. En este ejemplo, haga clic en **x86**.  

4.  En el cuadro **Sistema operativo**, haga clic en el sistema operativo y la versión para la que quiere establecer una condición. En este ejemplo, haga clic en **Windows 2003 x86**.  

5.  En el cuadro **Condición**, haga clic en la condición que corresponda y, después, haga clic en **Aceptar**.  

### <a name="file-properties-in-conditions"></a>Propiedades del archivo en condiciones  
 Use la condición **Propiedades del archivo** para comprobar la versión o la marca de tiempo de un archivo concreto para determinar si quiere ejecutar una tarea o un grupo de tareas. En este ejemplo, el entorno de producción contiene una imagen de Windows Server 2003 que se actualiza constantemente y que se usa para todos los servidores nuevos que se agregan a la red. Todos los equipos de servidor del entorno ejecutan una aplicación personalizada que requiere la interfaz de programación de aplicaciones (API) de objetos de acceso a datos (DAO) versión 3.60.6815.  

 Todos los servidores existentes funcionan correctamente, pero los servidores nuevos que se agreguen a la red con la imagen no podrán ejecutar la aplicación. Dado que mantener y actualizar imágenes es responsabilidad de un grupo diferente, usted decide si la secuencia de tareas de implementación se cambia para instalar la versión correspondiente de DAO o si la versión existente de DAO implementada con la imagen es incorrecta.  

 **Para agregar una condición Propiedades del archivo a un paso de secuencia de tareas en Configuration Manager 2007 R3**  

1.  En Configuration Manager 2007 R3, cree un paquete para instalar DAO 3.60.6815. Asigne a este paquete el nombre *DAO* con un programa denominado *InstallDAO*. Para información sobre cómo crear paquetes, vea [How to Create a Package](http://technet.microsoft.com/library/bb693627.aspx) (Cómo crear un paquete).  

2.  Cree un paso **Instalar software** para implementar el paquete DAO.  

3.  Haga clic en el paso de secuencia de tareas **Instalar software** creado en el paso 2 y, después, haga clic en la pestaña **Opciones**.  

4.  Haga clic en **Agregar condición** y en **Propiedades del archivo**.  

5.  En el cuadro **Ruta de acceso**, escriba **C:\Archivos de programa\Microsoft Shared\DAO\dao360.dll**.  

6.  Active la casilla **Check the version** (Comprobar la versión) y haga clic en **no es igual a** para la condición.  

7.  En el cuadro **Versión**, escriba **3.60.6815**.  

8.  En este caso, desactive la casilla **Check the timestamp** (Comprobar la marca de tiempo) y haga clic en **Aceptar**.  

### <a name="folder-properties-in-conditions"></a>Propiedades de la carpeta en condiciones  
 Use la condición **Propiedades de la carpeta** para comprobar la marca de tiempo de una carpeta concreta para determinar si quiere ejecutar una tarea o un grupo de tareas. Por ejemplo, considere una situación en la que una aplicación desarrollada internamente se ha actualizado para que funcione con Windows 8. Pero no todos los equipos de la red tienen instalada la versión más reciente de la aplicación, y debe realizar un proceso de conversión de datos para poder actualizar la aplicación.  

 Si la marca de tiempo de la carpeta en la que se instala la aplicación es 31/12/2007 o anterior, el equipo de destino ejecuta una versión incompatible de la aplicación, por lo que debe ejecutar el proceso de conversión de datos en el equipo de destino. Ejecute forma condicional un paso de secuencia de tareas para ejecutar el proceso de conversión de datos en los equipos que tienen una versión anterior de la aplicación.  

 **Para agregar una condición Propiedades de la carpeta a un paso de secuencia de tareas**  

1.  En la consola de Configuration Manager o en Deployment Workbench, en el Editor de secuencia de tareas, edite ***task_sequence***, donde *task_sequence* es la secuencia de tareas que quiere editar.  

2.  Cree una tarea **Línea de comandos** para realizar el proceso de conversión de datos.  

3.  Haga clic en la tarea creada en el paso 1.  

4.  Haga clic en **Agregar condición** y en **Propiedades de la careta**.  

5.  En el cuadro **Ruta de acceso**, escriba la ruta de acceso de la carpeta que contiene la aplicación.  

6.  Active la casilla **Check the timestamp** (Comprobar la marca de tiempo).  

7.  Haga clic en **Less than or equals** (Menor o igual que) para la condición.  

8.  En el cuadro **Fecha**, haga clic en **31/12/2007**.  

9. En el cuadro **Hora**, haga clic en **12:00:00 a. m.** y, luego, haga clic en **Aceptar**.  

### <a name="registry-settings-in-conditions"></a>Configuración del Registro en condiciones  
 Use la condición **Configuración del Registro** para comprobar la existencia de claves y valores en el Registro y los datos correspondientes almacenados en los valores del Registro. Por ejemplo, considere un caso en el que una aplicación que se usa actualmente en un pequeño conjunto de equipos no se puede ejecutar en Windows 8 y se implementa Windows 8 para actualizar los equipos que ejecutan Windows XP. Cree una condición en la primera tarea de una secuencia para comprobar el Registro en busca de una entrada de la aplicación incompatible e interrumpir el proceso de implementación para ese equipo, si se encuentra.  

 **Para agregar una condición Configuración del Registro a un paso de secuencia de tareas**  

1.  En la consola de Configuration Manager o en Deployment Workbench, en el Editor de secuencia de tareas, edite ***task_sequence***, donde *task_sequence* es la secuencia de tareas que implementa Windows 8.  

2.  Haga clic en la primera tarea de la secuencia y en la pestaña **Opciones**.  

3.  Haga clic en **Agregar condición** y en **Configuración del Registro**.  

4.  En la lista **Clave raíz**, haga clic en **HKEY_LOCAL_MACHINE**.  

5.  En el cuadro **Clave**, escriba **SOFTWARE\WOODGROVE**.  

6.  Haga clic en **no existe** para la condición. En este caso, la tarea se ejecutará y la secuencia continuará solo si la clave no existe.  

7.  Opcionalmente, la condición puede comprobar si un valor no existe si el nombre del valor se escribe en el cuadro **Nombre del valor**.  

8.  Si se ha usado una condición distinta de **existe o no existe**, especifique un valor y el tipo de valor.  

9. Haga clic en **Aceptar**.  

### <a name="wmi-queries-in-conditions"></a>Consultas de WMI en condiciones  
 Use la condición **Consulta de WMI** para ejecutar una consulta de WMI. La condición se evalúa como True si la consulta devuelve al menos un resultado. Por ejemplo, considere que un equipo de implementación debe actualizar el sistema operativo de todos los servidores de un modelo determinado, por ejemplo, Dell 1950. Puede usar una consulta de WMI para comprobar el modelo de cada equipo y continuar con la implementación únicamente si se encuentra el modelo adecuado.  

 **Para agregar una condición Consulta de WMI a un paso de secuencia de tareas**  

1.  En la consola de Configuration Manager o en Deployment Workbench, en el Editor de secuencia de tareas, edite ***task_sequence***, donde *task_sequence* es la secuencia de tareas que actualizará los servidores.  

2.  Haga clic en la primera tarea de la secuencia y en la pestaña **Opciones**.  

3.  Haga clic en **Agregar condición** y en **Consulta de WMI**.  

4.  En el cuadro **Espacio de nombres de WMI**, escriba **root\cimv2**.  

5.  En el cuadro **Consulta WQL**, escriba **Select \* From Win32_ComputerSystem WHERE Model LIKE "%Dell%%1950%"**. Haga clic en **Aceptar**.  

### <a name="installed-software-in-conditions"></a>Software instalado en condiciones  
 Use una condición **Software instalado** para comprobar si una parte determinada del software está instalada en un equipo de destino. Solo se puede evaluar con esta condición el software instalado mediante archivos de Microsoft Installer (MSI). Por ejemplo, imagine que quiere actualizar el sistema operativo de todos los servidores excepto el de aquellos que ejecutan Microsoft SQL Server 2012.  

 **Para agregar una condición Software instalado a un paso de secuencia de tareas**  

1.  En la consola de Configuration Manager o en Deployment Workbench, en el Editor de secuencia de tareas, edite ***task_sequence***, donde *task_sequence* es la secuencia de tareas que actualizará los servidores.  

2.  Haga clic en la primera tarea de la secuencia y en la pestaña **Opciones**.  

3.  Haga clic en **Agregar condición** y en **Software instalado**.  

4.  Haga clic en **Examinar** y en el archivo MSI de SQL Server 2012.  

5.  Active la casilla **Match this specific product** (Coincidir con este producto específico) para especificar que solo los equipos con SQL Server 2012 y ninguna otra versión son los equipos de destino que debe detectar esta consulta.  

6.  Haga clic en **Aceptar**.  

### <a name="complex-conditions"></a>Condiciones complejas  
 Se pueden agrupar varias condiciones mediante **IF** instrucciones para crear condiciones complejas. Por ejemplo, imagine que un paso determinado solo se debe ejecutar para equipos Contoso 1950 que ejecutan Windows Server 2003 o Windows Server 2008. Escrito como una instrucción **IF** programática, tendría un aspecto similar al siguiente:  

```  
IF ((Computer Model IS “Contoso 1950”) AND (operating system=2003 OR operating system=2008))  
```  

 **Para agregar una condición compleja**  

1.  En la consola de Configuration Manager o en Deployment Workbench, en el Editor de secuencia de tareas, edite ***task_sequence***, donde *task_sequence* es la secuencia de tareas que actualizará los servidores.  

2.  Haga clic en el paso de secuencia de tareas al que se va a agregar la condición y, después, haga clic en la pestaña **Opciones**.  

3.  Haga clic en **Agregar condición**, en **If Statement** (Instrucción IF) y en **All conditions** (Todas las condiciones). Haga clic en **Aceptar**.  

4.  Haga clic en la instrucción de condición, en **Agregar condición** y en **Consulta de WMI**.  

5.  Asegúrese de que se ha especificado **root\cimv2** como espacio de nombres de WMI y, luego, en el cuadro **Consulta WQL**, escriba **SELECT \* FROM Win32_ComputerSystem WHERE ComputerModel LIKE “%Contoso%1950%”**. Haga clic en **Aceptar**.  

6.  Haga clic en la instrucción **IF** y en **Agregar condición**. Haga clic en **If statement** (Instrucción IF) y en **Any condition** (Cualquier condición). Haga clic en **Aceptar**.  

7.  Haga clic en la segunda instrucción **IF**. Haga clic en **Agregar condición** y en **Versión del sistema operativo**.  

8.  En el cuadro **Arquitectura**, haga clic en la arquitectura de los servidores. En este ejemplo, haga clic en **x86**.  

9. En el cuadro **Sistema operativo**, haga clic en el sistema operativo y la versión. En este ejemplo, haga clic en **Windows Server 2003 x86 versión original**. Haga clic en **Aceptar**.  

10. Haga clic en la segunda instrucción **IF**. Haga clic en **Agregar condición** y en **Versión del sistema operativo**.  

11. En el cuadro **Arquitectura**, haga clic en la arquitectura de los servidores. En este ejemplo, haga clic en **x86**.  

12. En el cuadro **Sistema operativo**, haga clic en el sistema operativo y la versión. En este ejemplo, haga clic en **Windows Server 2008 x86 versión original**. Haga clic en **Aceptar**.  

## <a name="creating-a-highly-scalable-lti-deployment-infrastructure"></a>Crear una infraestructura de implementación de LTI altamente escalable  
 En este escenario, no hay ninguna distribución electrónica de software disponible para que la aproveche la infraestructura de implementación, por lo que debe usar MDT para crear una infraestructura de implementación de LTI totalmente automatizada. La infraestructura de LTI escalable usa SQL Server, Servicios de implementación de Windows y tecnologías de Replicación del sistema de archivos distribuido (DFS-R) de Windows Server 2003.  

 Para escalar la infraestructura de LTI, haga lo siguiente:  

-   Asegúrese de que existe la infraestructura apropiada, como se describe en [Asegurarse de que existe la infraestructura apropiada](#EnsureInfrastructure).  

-   Agregue contenido a MDT como se describe en [Agregar contenido a MDT](#AddContent).  

-   Prepare Servicios de implementación de Windows como se describe en [Preparar Servicios de implementación de Windows](#PrepareDeployment).  

-   Configure DFS-R como se describe en [Configurar la Replicación del sistema de archivos distribuido](#ConfigureFileReplication).  

-   Prepárese para la replicación de SQL Server como se describe en [Prepararse para la replicación de SQL Server](#PrepareSQLReplication).  

-   Configure la replicación de SQL Server como se describe en [Configurar la replicación de SQL Server](#ConfigureSQLReplication).  

 En este escenario se da por supuesto que MDT está configurado en un servidor de implementación principal y que la configuración de la base de datos de MDT ya se ha completado como se describe al principio de este documento.  

###  <a name="EnsureInfrastructure"></a> Asegurarse de que existe la infraestructura apropiada  
 La infraestructura de implementación de LTI altamente escalable usa una topología de concentrador y radio para la replicación del contenido. Por lo tanto, en primer lugar debe designar un servidor de implementación en el entorno de producción que lleve a cabo el rol de servidor de implementación principal.  En la lista siguiente se indican los componentes necesarios para el servidor de implementación principal.  

 |**Componente necesario** |**Propósito/comentario** |  
 |-|-|  
 |Windows Server 2003 R2|Se necesita para admitir DFS-R.|  
 |MDT |Contiene la copia maestra del recurso compartido de implementación.|  
 |SQL Server 2005|Debe ser una versión completa para permitir la replicación de la base de datos de MDT.|  
 |DFS-R |Se necesita para la replicación del recurso compartido de implementación.|  
 |Servicios de implementación de Windows |Se necesita para permitir que se inicien las instalaciones basadas en PXE de la red.|  

 Cuando haya seleccionado el servidor de implementación principal, aprovisione servidores adicionales en cada sitio para admitir implementaciones de LTI.  En la lista siguiente se indican los componentes necesarios para el servidor de implementación secundario.  

 |**Componente necesario** |**Propósito/comentario** |  
 |-|-|  
 |Windows Server 2003 R2|Se necesita para admitir DFS-R.|  
 |Microsoft SQL Server 2005 Express Edition |Recibe copias replicadas de la base de datos de MDT.|  
 |DFS-R |Se necesita para la replicación del recurso compartido de implementación.|  
 |Servicios de implementación de Windows |Se necesita para permitir que se inicien las instalaciones basadas en PXE de la red.|  

> [!NOTE]
>  Es necesario instalar y configurar Servicios de implementación de Windows en cada servidor secundario, pero no hace falta agregar imágenes de arranque o instalación.  

###  <a name="AddContent"></a> Agregar contenido a MDT  
 Rellene el servidor de implementación principal con contenido mediante Deployment Workbench, y cree y rellene la base de datos de MDT como se describe en las secciones siguientes. Para más información sobre cómo rellenar la base de datos con:  

-   Aplicaciones, vea la sección "Configuring Applications in the Deployment Workbench" (Configurar aplicaciones en Deployment Workbench) en el documento de MDT *Using the Microsoft Deployment Toolkit* (Uso de Microsoft Deployment Toolkit).  

-   Sistemas operativos, vea la sección "Configuring Operating Systems in the Deployment Workbench" (Configurar sistemas operativos en Deployment Workbench) en el documento de MDT *Using the Microsoft Deployment Toolkit* (Uso de Microsoft Deployment Toolkit).  

-   Paquetes de sistema operativo, vea la sección "Configuring Packages in the Deployment Workbench" (Configurar paquetes en Deployment Workbench) en el documento de MDT *Using the Microsoft Deployment Toolkit* (Uso de Microsoft Deployment Toolkit).  

-   Controladores de dispositivo, vea la sección "Configuring Device Drivers in the Deployment Workbench" (Configurar controladores de dispositivo en Deployment Workbench) en el documento de MDT *Using the Microsoft Deployment Toolkit* (Uso de Microsoft Deployment Toolkit).  

-   Secuencias de tareas, vea la sección "Configuring Task Sequences in the Deployment Workbench" (Configurar secuencias de tareas en Deployment Workbench) en el documento de MDT *Using the Microsoft Deployment Toolkit* (Uso de Microsoft Deployment Toolkit).  

> [!NOTE]
>  Asegúrese de que el archivo LiteTouchPE_x86.wim creado al actualizar el recurso compartido de implementación se ha agregado a Servicios de implementación de Windows.  

###  <a name="PrepareDeployment"></a> Preparar Servicios de implementación de Windows  
 Dado que el archivo LiteTouchPE_x86.wim se replicará de forma periódica en el grupo de replicación DFS-R, el almacén de datos de configuración de arranque debe actualizarse periódicamente para reflejar el entorno de Windows PE recién replicado. Lleve a cabo los pasos siguientes en cada uno de los servidores de implementación.  

 **Para preparar Servicios de implementación de Windows**  

1.  Abra una ventana del símbolo del sistema.  

2.  Escriba **WDSUtil/set-server/BCDRefreshPolicy/Enabled:yes/RefreshPeriod:60** y presione ENTRAR.  

> [!NOTE]
>  En el ejemplo que se muestra aquí, el período de actualización se establece en 60 minutos, pero puede configurar este valor para replicar durante el mismo período que DFS-R.  

###  <a name="ConfigureFileReplication"></a> Configurar la Replicación del sistema de archivos distribuido  
 Al escalar la arquitectura de implementación de LTI, use DFS-R como base para replicar el contenido tanto del recurso compartido de implementación de MDT y del entorno de arranque de Lite Touch de Windows PE como del servidor de implementación principal en los servidores de implementación secundarios.  

> [!NOTE]
>  Asegúrese de que DFS-R está instalado antes de realizar los pasos siguientes.  

 **Para configurar DFS-R para replicar el contenido de implementación**  

1.  Abra la consola de administración de DFS.  

2.  En la consola de administración de DFS, expanda Administración de DFS.  

3.  Haga clic en **Replicación** y en **Nuevo grupo de replicación**.  

4.  En el Asistente para nuevo grupo de replicación, en la página **Tipo de grupo de replicación**, haga clic en **New Multipurpose Replication Group** (Nuevo grupo de replicación multipropósito).  

5.  Haga clic en **Siguiente**.  

6.  En la página **Name and Domain** (Nombre y dominio), escriba la información siguiente:  

    -   En el cuadro **Name for replication group** (Nombre del grupo de replicación), escriba un nombre para el grupo de replicación, por ejemplo, **Grupo de replicación de MDT 2010**.  

    -   En el cuadro **Optional description of replication group** (Descripción opcional del grupo de replicación), escriba una descripción del grupo de replicación, por ejemplo, **Grupo para la replicación de datos de MDT 2010**.  

    -   Asegúrese de que el cuadro **Dominio** contiene el nombre de dominio correcto.  

7.  Haga clic en **Siguiente**.  

8.  En la página **Miembros del grupo de replicación**, siga estos pasos:  

    1.  Haga clic en **Agregar**.  

    2.  Escriba los nombres de todos los servidores que van a ser miembros de este grupo de replicación, por ejemplo, todos los servidores de implementación secundarios y el servidor de implementación principal.  

    3.  Haga clic en **Aceptar**.  

9. Haga clic en **Siguiente**.  

10. En la página **Selección de topología**, haga clic en **Concentrador y radio** y en **Siguiente**.  

11. En la página **Miembros concentradores**, haga clic en el servidor de implementación principal y en **Agregar**.  

12. Haga clic en **Siguiente**.  

13. En la página **Conexiones de concentrador y radio**, asegúrese de que por cada servidor de implementación secundario el servidor de implementación principal indicado es el **Miembro concentrador necesario**.  

14. Haga clic en **Siguiente**.  

15. En la página **Programación del grupo de replicación y ancho de banda**, especifique una programación para replicar el contenido entre servidores.  

16. Haga clic en **Siguiente**.  

17. En la página **Miembro principal**, en el cuadro **Miembro principal**, haga clic en el servidor de implementación principal.  

18. Haga clic en **Siguiente**.  

19. En la página **Folders to Replicate** (Carpetas para replicar), haga clic en **Agregar** y lleve a cabo estos pasos:  

    1.  En el cuadro **Local Path of the folder to replicate** (Ruta de acceso local de la carpeta para replicar), haga clic en **Examinar** para ir a la carpeta *X:\\*Deployment, donde *X* es la letra de unidad del servidor de implementación.  

    2.  Haga clic en **Use name based on path** (Usar nombre basado en la ruta de acceso).  

    3.  Haga clic en **Aceptar**.  

    4.  Haga clic en **Agregar**.  

    5.  En el cuadro de diálogo **Add Folder to Replicate** (Agregar carpeta para replicar), haga clic en **Examinar** para ir a la carpeta *X:* \RemoteInstall\Boot.  

    6.  Haga clic en **Use name based on path** (Usar nombre basado en la ruta de acceso).  

20. Haga clic en **Siguiente**.  

21. En la página **Local Path of Distribution on Other Members** (Ruta de acceso local de distribución en otros miembros), siga estos pasos:  

    1.  Seleccione todos los miembros del grupo de distribución y haga clic en **Editar**.  

    2.  En el cuadro de diálogo **Edit Local Path** (Editar ruta de acceso local), haga clic en **Habilitado**.  

    3.  Escriba la ruta de acceso donde se debe almacenar la carpeta del recurso compartido de implementación en el servidor de implementación secundario, por ejemplo, ***X:\Deployment***, donde *X* es la letra de unidad del servidor de implementación.  

    4.  Haga clic en **Aceptar**.  

22. Haga clic en **Siguiente**.  

23. En la página **Local Path of Boot on Other Members** (Ruta de acceso local de arranque en otros miembros), siga estos pasos:  

    1.  Seleccione todos los miembros del grupo de distribución y haga clic en **Editar**.  

    2.  En el cuadro de diálogo **Edit Local Path** (Editar ruta de acceso local), haga clic en **Habilitado**.  

    3.  Escriba la ruta de acceso donde se debe almacenar la carpeta de arranque en el servidor de implementación secundario, por ejemplo, ***X:\RemoteInstall\Boot***, donde *X* es la letra de unidad del servidor de implementación.  

    4.  Haga clic en **Aceptar**.  

24. Haga clic en **Siguiente**.  

25. En la página **Remote Settings and Create Replication Group** (Configuración remota y crear grupo de replicación), haga clic en **Crear** para completar el Asistente para nuevo grupo de replicación.  

26. En la página **Confirmación**, haga clic en **Cerrar** para cerrar el asistente.  

> [!NOTE]
>  Asegúrese de que el nuevo grupo de replicación aparece ahora bajo el nodo de replicación.  

###  <a name="PrepareSQLReplication"></a> Prepararse para la replicación de SQL Server  
 Para poder configurar la replicación de SQL Server, debe completar varios pasos de configuración previa a fin de asegurarse de que los servidores de implementación están configurados correctamente.  

 **Para prepararse para la replicación de SQL Server en el servidor de implementación principal**  

1.  Cree una carpeta para almacenar las instantáneas de base de datos y, después, configure la carpeta como un recurso compartido.  

    > [!NOTE]
    >  Para más información sobre cómo proteger la carpeta de instantáneas, vea [Proteger la carpeta de instantáneas](http://msdn2.microsoft.com/library/ms151151.aspx).  

2.  Asegúrese de que el servicio SQL Server Browser está habilitado y establecido en Automático.  

3.  En el cuadro **SQL Server Surface Area Configuration** (Configuración de área expuesta de SQL Server), haga clic en **Local and Remote connections** (Conexiones locales y remotas).  

 **Para prepararse para la replicación de SQL Server en el servidor de implementación secundario**  

1.  En el cuadro **SQL Server Surface Area Configuration** (Configuración de área expuesta de SQL Server), haga clic en **Local and Remote connections** (Conexiones locales y remotas).  

2.  Opcionalmente, puede crear una base de datos vacía para hospedar la base de datos de MDT replicada.  

> [!NOTE]
>  Esta base de datos debe tener el mismo nombre que la base de datos de MDT del servidor de implementación principal. Por ejemplo, si la base de datos de MDT del servidor de implementación principal se llama *MDTDB*, cree una base de datos vacía denominada *MDTDB* en el servidor de implementación secundario.  

###  <a name="ConfigureSQLReplication"></a> Configurar la replicación de SQL Server  
 Después de configurar la replicación de los archivos y las carpetas necesarios para generar la infraestructura de implementación, configure SQL Server para replicar la base de datos de MDT.  

> [!NOTE]
>  También es posible mantener una sola base de datos de MDT central, pero si se mantiene una versión replicada de la base de datos de MDT, se puede tener un mayor control sobre datos que se transfieren a través de la red de área extensa (WAN).  

 SQL Server 2005 usa un modelo de replicación similar a un modelo de distribución de una revista:  

1.  Una *revista* se pone a disposición (se publica) a través un *publicador*.  

2.  Los *distribuidores* se usan para distribuir la publicación.  

3.  Los *lectores* se pueden suscribir a una publicación para recibirla periódicamente (una *suscripción de inserción*).  

 Esta terminología se usa en la configuración de replicación de SQL Server y en los asistentes de configuración.  

#### <a name="configure-a-sql-server-publisher"></a>Configurar un publicador de SQL Server  
 Para configurar el servidor de implementación principal como un publicador de SQL Server, siga estos pasos:  

1.  Abra SQL Server Management Studio.  

2.  Haga clic con el botón derecho en el nodo **Replicación** y, después, haga clic en **Configurar distribución**.  

3.  En el Asistente para configurar la distribución, haga clic en **Siguiente**.  

4.  En la página **Distribuidor**, haga clic en **will act as its own Distributor; SQL Server will create a distribution database and log** (actuará como su propio distribuidor; SQL Server creará una base de datos y un registro de distribución) y, después, haga clic en **Siguiente**.  

5.  En la página **Carpeta de instantáneas**, en la sección **Preparing for SQL Server Replication** (Prepararse para la replicación de SQL Server), escriba la ruta de acceso UNC a la carpeta de instantáneas que se ha creado.  

6.  En la página **Base de datos de distribución**, haga clic en **Siguiente**.  

7.  En la página **Publicadores**, haga clic en el servidor de implementación principal para configurarlo como distribuidor y, después, haga clic en **Siguiente**.  

8.  En la página **Acciones del asistente**, haga clic en **Configurar distribución** y en **Siguiente**.  

9. Haga clic en **Finalizar** y en **Cerrar** cuando el asistente haya finalizado.  

#### <a name="enable-the-mdt-db-for-replication"></a>Habilitar la base de datos de MDT para la replicación  
 Para habilitar la base de datos de MDT para la replicación en el servidor de implementación principal, siga estos pasos:  

1.  En SQL Server Management Studio, haga clic con el botón derecho en el nodo **Replicación** y, después, haga clic en **Propiedades del publicador**.  

2.  En la página **Propiedades del publicador**, siga estos pasos:  

    1.  Haga clic en **Publisher Databases** (Bases de datos del publicador).  

    2.  Haga clic en la base de datos de MDT y en **Transaccional**.  

    3.  Haga clic en **Aceptar**.  

 La base de datos de MDT ya está configurada para la replicación de instantáneas y la replicación transaccional.  

#### <a name="create-a-publication-of-the-mdt-db"></a>Crear una publicación de la base de datos de MDT  
 Para crear una publicación de la base de datos de MDT a la que se puedan suscribir los servidores de implementación secundarios, siga estos pasos:  

1.  En SQL Server Management Studio, expanda Replicación, haga clic con el botón derecho en **Publicaciones locales** y haga clic en **Nueva publicación**.  

2.  En el Asistente para nueva publicación, haga clic en **Siguiente**.  

3.  En la página **Base de datos de publicación**, haga clic en la base de datos de MDT y en **Siguiente**.  

4.  En la página **Tipo de publicación**, haga clic en **Publicación de instantáneas** y en **Siguiente**.  

5.  En la página **Artículos**, seleccione todas las **Tables, Stored Procedures** (Tablas, procedimientos almacenados) y **Vistas** y, luego, haga clic en **Siguiente**.  

6.  En la página **Problemas de los artículos**, haga clic en **Siguiente**.  

7.  En la página **Filtrar filas de tabla**, haga clic en **Siguiente**.  

8.  En la página **Agente de instantáneas**, siga estos pasos:  

    1.  Seleccione **Create a snapshot immediately and keep the snapshot available to initialize subscriptions** (Crear una instantánea inmediatamente y mantenerla disponible para inicializar suscripciones).  

    2.  Haga clic en **Schedule the Snapshot Agent to run at the following times** (Programar el Asistente de instantáneas para ejecutarse a las horas siguientes).  

    3.  Haga clic en **Cambiar**.  

    > [!NOTE]
    >  Especifique una programación para una hora antes de que se replique la base de datos.  

9. Haga clic en **Siguiente**.  

10. En la página **Seguridad del agente**, seleccione la cuenta con la que se ejecutará el agente de instantáneas y haga clic en **Siguiente**.  

11. En la página **Acciones del asistente**, haga clic en **Create the publication** (Crear la publicación) y en **Siguiente**.  

12. En la página **Complete the Wizard** (Complete el asistente), en el cuadro **nombre de publicación**, escriba un nombre de publicación descriptivo.  

13. Haga clic en **Finalizar** para completar el asistente y, después, haga clic en **Cerrar** cuando el asistente haya creado la publicación.  

    > [!NOTE]
    >  La publicación ahora estará visible bajo el nodo Publicaciones locales en SQL Server Management Studio.  

#### <a name="subscribe-child-deployment-servers-to-the-published-mdt-db"></a>Suscribir servidores de implementación secundarios a la base de datos de MDT publicada  
 Ahora que se ha publicado la base de datos de MDT, puede agregar los servidores de implementación secundarios como suscriptores a esta publicación; es decir, recibirán una copia de la base de datos según una programación, de modo que durante una implementación los equipos cliente pueden consultar una base de datos local de la red, en lugar de ir a través de la WAN.  

 **Para suscribir los servidores de implementación secundarios a la publicación de la base de datos de MDT**  

1.  En SQL Server Management Studio, vaya a Replicación/Publicaciones locales.  

2.  Haga clic con el botón derecho en la publicación creada en la sección anterior y, después, haga clic en **Nuevas suscripciones**.  

3.  En el Asistente para nuevas suscripciones, haga clic en **Siguiente**.  

4.  En la página **Publicación**, haga clic en la publicación creada en la sección anterior.  

5.  En la página **Ubicación del Agente de distribución**, haga clic en **Run all agents at the Distributor SERVERNAME (push subscriptions)** (Ejecutar todos los agentes en el nombreDeServidor del distribuidor (suscripciones de inserción)) y, luego, haga clic en **Siguiente**.  

6.  En la página **Suscriptores**, agregue cada uno de los servidores de implementación secundarios mediante los pasos siguientes:  

    1.  Haga clic en **Agregar suscriptor** y en **Agregar suscriptor de SQL Server**.  

    2.  Agregue cada servidor de implementación secundario.  

    3.  Para cada servidor de implementación secundario agregado, en el cuadro **Base de datos de suscripciones**, haga clic en la base de datos de MDT vacía de ese servidor de implementación secundario.  

    > [!NOTE]
    >  Si la base de datos de MDT vacía todavía no se ha creado, en el cuadro **Base de datos de suscripciones**, seleccione la opción para crear una base de datos.  

    > [!NOTE]
    >  Esta base de datos debe tener el mismo nombre que la base de datos de MDT del servidor de implementación principal. Por ejemplo, si la base de datos de MDT del servidor de implementación principal se llama *MDTDB*, cree una base de datos vacía denominada *MDTDB* en el servidor de implementación secundario.  

7.  Haga clic en **Siguiente**.  

8.  En la página **Seguridad del Agente de distribución**, haga clic en **…** para abrir el cuadro de diálogo **Seguridad del Agente de distribución**.  

9. Escriba los detalles de la cuenta que se va a usar para el Agente de distribución y haga clic en **Siguiente**.  

10. En la página **Programación de sincronización**, siga estos pasos:  

    1.  En el cuadro **Programación del agente**, haga clic en **<Definir programación\>**.  

    2.  Especifique la programación que se usará para replicar la base de datos entre los servidores de implementación principal y secundario y, después, haga clic en **Siguiente**.  

11. En la página **Initialize Subscription** (Inicializar suscripción), haga clic en **Siguiente**.  

12. En la página **Acciones del asistente**, haga clic en **Create the subscription(s)** (Crear las suscripciones) y en **Siguiente**.  

13. Haga clic en **Finalizar** y en **Cerrar** cuando el asistente haya finalizado correctamente.  

 La replicación de SQL Server ya está configurada y la base de datos de MDT se replicará desde el servidor de implementación principal en todos los servidores de implementación secundarios que se hayan suscrito a ella de forma periódica.  

#### <a name="configure-customsettingsini"></a>Configurar CustomSettings.ini  
 La infraestructura de implementación de LTI ya se ha creado correctamente y cada ubicación contendrá un servidor de implementación de LTI con una copia duplicada de los siguientes elementos:  

-   El recurso compartido de implementación  

-   La base de datos de MDT  

-   El entorno de Windows PE de LiteTouchPE_x86 que se ha agregado a los Servicios de implementación de Windows  

 Ahora puede configurar el archivo CustomSettings.ini para que el recurso compartido de implementación use el contenido de implementación (recurso compartido de implementación y base de datos) de su servidor de implementación local, el servidor que proporciona el entorno de LiteTouchPE_x86.wim mediante Servicios de implementación de Windows.  

 Cuando se entrega el archivo LiteTouchPE_x86.wim desde Servicios de implementación de Windows, se configura una clave del Registro con el nombre del servidor de Servicios de implementación de Windows que se usa. MDT captura este nombre de servidor en una variable (%WDSServer%) que puede usar para configurar CustomSettings.ini.  

 **Para usar siempre el servidor de implementación de LTI local**  

> [!NOTE]
>  En el procedimiento siguiente se da por supuesto que el recurso compartido de implementación se ha creado y se ha establecido como recurso Deployment$.  

1.  Haga clic en **Inicio** y seleccione **All Programs** (Todos los programas). Seleccione **Microsoft Deployment Toolkit** y haga clic en **Deployment Workbench**.  

2.  En el árbol de consola de Deployment Workbench, vaya a Deployment Workbench/Deployment Shares (Recursos compartidos de implementación)/*deployment_share*, donde *deployment_share* es el nombre del recurso compartido de implementación que se va a configurar.  

3.  En el panel Acciones, haga clic en **Propiedades**.  

4.  Haga clic en la pestaña **Reglas** y modifique el archivo CustomSettings.ini para configurar las propiedades siguientes:  

    -   Para cada sección de SQL Server agregada, configure **SQLServer** de modo que use el nombre del servidor **%WDSServer%**, por ejemplo, **SQLServer=%WDSServer%**.  

    -   Si va a configurar **DeployRoot**, asegúrese de que **DeployRoot** use la variable **%WDSServer%**, por ejemplo, **DeployRoot=\\\\%WDSServer%\Deployment$**.  

5.  Haga clic en **Edit Bootstrap.ini** (Editar Bootstrap.ini).  

6.  Configure BootStrap.ini para que use la propiedad **%WDSServer%**. Para ello, agregue o cambie el valor de **DeployRoot** a **DeployRoot=\\\\%WDSServer%\Deployment$**.  

7.  Haga clic en **Archivo** y en **Guardar** para guardar los cambios en el archivo BootStrap.ini.  

8.  Haga clic en **Aceptar**.  

     El recurso compartido de implementación y el entorno de Windows PE de LiteTouchPE_x86.wim deben actualizarse.  

9. En el panel Acciones, haga clic en **Update Deployment Share** (Actualizar recurso compartido de implementación).  

     Se inicia el Asistente para actualizar recurso compartido de implementación.  

10. En la página **Opciones**, seleccione las opciones deseadas para actualizar el recurso compartido de implementación y haga clic en **Siguiente**.  

11. En la página **Resumen**, compruebe que la información sea correcta y haga clic en **Siguiente**.  

12. En la página **Confirmación**, haga clic en **Finalizar**.  

 En el ejemplo siguiente se muestra CustomSettings.ini después de realizar los pasos descritos en esta sección.  

 **Ejemplo de CustomSettings.ini configurado para la infraestructura de implementación de LTI escalable**  

```  
[Settings]  
Priority=CSettings,CPackages, CApps, CAdmins, CRoles, Default  
Properties=MyCustomProperty  

[Default]  
OSInstall=Y  
ScanStateArgs=/v:5 /o /c  
LoadStateArgs=/v:5 /c /lac  

[CSettings]  
SQLServer=%WDSServer%  
Instance=  
Database=MDTDB  
Netlib=DBNMPNTW  
SQLShare=  
Table=ComputerSettings  
Parameters=UUID, AssetTag, SerialNumber, MacAddress  
ParameterCondition=OR  

[CPackages]  
SQLServer=%WDSServer%  
Database=MDTDB  
Netlib=DBNMPNTW  
SQLShare=  
Table=ComputerPackages  
Parameters=UUID, AssetTag, SerialNumber, MacAddress  
ParameterCondition=OR  
Order=Sequence  

[CApps]  
SQLServer=%WDSServer%  
Database=MDTDB  
Netlib=DBNMPNTW  
SQLShare=  
Table=ComputerApplications  
Parameters=UUID, AssetTag, SerialNumber, MacAddress  
ParameterCondition=OR  
Order=Sequence  

[CAdmins]  
SQLServer=%WDSServer%  
Database=MDTDB  
Netlib=DBNMPNTW  
SQLShare=  
Table=ComputerAdministrators  
Parameters=UUID, AssetTag, SerialNumber, MacAddress  
ParameterCondition=OR  

[CRoles]  
SQLServer=%WDSServer%  
Database=MDTDB  
Netlib=DBNMPNTW  
SQLShare=  
Table=ComputerRoles  
Parameters=UUID, AssetTag, SerialNumber, MacAddress  
ParameterCondition=OR  
```  

## <a name="selecting-a-local-mdt-server-when-multiple-servers-exist"></a>Seleccionar un servidor de MDT local cuando existen varios servidores  
 En este escenario, se usan varios servidores de MDT para admitir un gran volumen de implementaciones simultáneas e implementaciones en varios sitios. Cuando se inicializa una implementación de LTI, el comportamiento predeterminado consiste en solicitar una ruta de acceso al servidor de MDT para conectarse y tener acceso a los archivos necesarios para iniciar el proceso de implementación.  

 El Asistente para la implementación de Windows puede usar el archivo LocalServer.xml para ofrecer una selección de servidores de implementación conocidos para cada ubicación.  

 Para usar el archivo LocationServer.xml:  

-   Comprenda el propósito y el uso de LocationServer.xml como se describe en [Descripción de LocationServer.xml](#UnderstandingLocationServer).  

-   Cree el archivo LocationServer.xml como se describe en [Crear el archivo LocationServer.xml](#CreateLocationServer).  

-   Agregue el archivo LocationServer.xml al directorio de archivos adicionales como se describe en Agregar el archivo LocationServer.xml al directorio de archivos adicionales.  

-   Actualice el archivo BootStrap.ini como se describe en [Actualizar el archivo BootStrap.ini](#UpdateBootstrap).  

-   Actualice el recurso compartido de implementación como se describe en [Actualizar el recurso compartido de implementación](#UpdateDeploymentShare).  

 En este escenario se da por supuesto que MDT está configurado en un servidor de implementación.  

###  <a name="UnderstandingLocationServer"></a> Descripción de LocationServer.xml  
 En primer lugar, debe entender cómo usa MDT el archivo LocationServer.xml. Durante una implementación de LTI, los scripts de MDT leen y procesan el archivo BootStrap.ini para recopilar información inicial sobre la implementación. Esto se lleva a cabo antes de que se haya establecido una conexión con el servidor de implementación. Por lo tanto, la propiedad **DeployRoot** se suele usar para especificar en el archivo BootStrap.ini el servidor de implementación con el que se debe establecer una conexión.  

 Si el archivo BootStrap.ini no contiene una propiedad **DeployRoot**, los scripts de MDT cargan una página del asistente para solicitarle al usuario una ruta de acceso al servidor de implementación. Al inicializar la página del asistente **HTML Application (HTA)** (Aplicación HTML (HTA)), los scripts de MDT comprueban si existe el archivo LocationServer.xml y, en caso de que así sea, usan LocationServer.xml para mostrar los servidores de implementación disponibles.  

#### <a name="understand-when-to-use-locationserverxml"></a>Entender cuándo se debe usar LocationServer.xml  
 MDT ofrece varias maneras de determinar a qué servidor es necesario conectarse durante una implementación de LTI. A cada escenario le corresponde un método diferente para localizar el servidor de implementación, por lo que es importante entender cuándo se debe usar LocationServer.xml.  

 MDT proporciona varios métodos para detectar automáticamente y usar el servidor de implementación más adecuado. Estos métodos se muestran en la tabla siguiente:

 |**Método** |**Detalles** |  
 |-|-|  
 |**%WDSServer%** |Este método se usa cuando el servidor de MDT está hospedado conjuntamente en el servidor de Servicios de implementación de Windows.<br /><br /> Cuando se inicia una implementación de LTI desde Servicios de implementación de Windows, se crea una variable de entorno (%WDSServer%) y se rellena con el nombre del servidor de Servicios de implementación de Windows.<br /><br /> La variable **DeployRoot** puede usar esta variable para conectarse automáticamente a un recurso compartido de implementación en el servidor de Servicios de implementación de Windows, por ejemplo:<br /><br /> **DeployRoot=\\\\%WDSServer%\Deployment$** |  
 |**Automatización basada en la ubicación** |MDT puede usar la automatización basada en la ubicación en el archivo BootStrap.ini para determinar el servidor en el que debe realizar la implementación.<br /><br /> Use la propiedad **Default Gateway** para distinguir entre las diferentes ubicaciones. Para cada **Default Gateway**, se especifica un servidor de MDT diferente.<br /><br /> Para más información sobre el uso de la automatización basada en la ubicación, vea "Selecting the Methods for Applying Configuration Settings" (Seleccionar métodos para aplicar valores de configuración).|  

 Cada método indicado en la tabla anterior ofrece una manera de automatizar la selección del servidor de implementación en una ubicación específica en escenarios concretos. Estos métodos están destinados a escenarios específicos, por ejemplo, cuando el servidor de MDT está hospedado conjuntamente con Servicios de implementación de Windows.  

 Hay otros escenarios en los que estos enfoques no son adecuados, como cuando hay varios servidores de implementación en una ubicación determinada o la lógica de automatización no es posible (por ejemplo, la red no está lo suficientemente segmentada para permitir que se determine la ubicación o el servidor de MDT es independiente de Servicios de implementación de Windows).  

 En estos casos, el archivo LocationServer.xml proporciona una manera flexible de presentar esta información durante la implementación sin necesidad de conocer los nombres de los servidores ni los nombres de los recursos compartidos de implementación.  

###  <a name="CreateLocationServer"></a> Crear el archivo LocationServer.xml  
 Para mostrar una lista de servidores de implementación disponibles durante la implementación de LTI, cree un archivo LocationServer.xml que contenga información sobre cada servidor. Como no hay ningún archivo LocationServer.xml predeterminado en MDT, siga las instrucciones que se indican a continuación para crear uno.  

#### <a name="create-a-locationserverxml-file-to-support-multiple-locations"></a>Crear un archivo LocationServer.xml para admitir varias ubicaciones  
 La manera más sencilla de crear y usar LocationServer.xml consiste en crear un archivo LocationServer.xml y agregar entradas para cada servidor de implementación del entorno (puede estar en la misma ubicación o en ubicaciones distintas).  

 Para construir el archivo LocationServer.xml, cree una sección para cada servidor y agregue la información siguiente:  

-   Un identificador único.  

-   Un nombre de ubicación, que se usa para presentar un nombre fácilmente identificable para esa ubicación.  

-   Una ruta de acceso UNC al servidor de MDT para esa ubicación.  

 A continuación se muestra cómo se crea el archivo LocationServer.xml con cada una de estas propiedades mediante un archivo de LocationServer.xml de ejemplo configurado para varias ubicaciones.  

 **Archivo LocationServer.xml de ejemplo para admitir varias ubicaciones**  

```  
<?xml version="1.0" encoding="utf-8" ?>  
<servers>  
    <QueryDefault></QueryDefault>  
    <server>  
        <serverid>1</serverid>  
        <friendlyname>  
          Contoso HQ, Seattle, USA  
        </friendlyname>  
        <UNCPath>\\STLDS01\Deployment$</UNCPath>  
    </server>  
    <server>  
        <serverid>2</serverid>  
        <friendlyname>  
          Contoso NYC, New York, USA  
        </friendlyname>  
        <UNCPath>\\NYCDS01\Deployment$</UNCPath>  
    </server>   
</servers>  
```  

 Con este formato, especifique entradas de servidor diferentes para cada ubicación o para los casos en los que haya varios servidores en una ubicación. Para ello, especifique una entrada de servidor diferente para cada servidor de esa ubicación, como se muestra en el ejemplo siguiente.   

 **Archivo LocationServer.xml de ejemplo para admitir varios servidores en varias ubicaciones**  

```  
<?xml version="1.0" encoding="utf-8" ?>  
<servers>  
    <QueryDefault></QueryDefault>  
    <server>  
        <serverid>1</serverid>  
        <friendlyname>  
          Contoso HQ DS1, Seattle, USA  
        </friendlyname>  
        <UNCPath>\\STLDS01\Deployment$</UNCPath>  
    </server>  
    <server>  
        <serverid>2</serverid>  
        <friendlyname>  
          Contoso HQ DS2, Seattle, USA  
        </friendlyname>  
        <UNCPath>\\STLDS02\Deployment$</UNCPath>  
    </server>   
</servers>  
```  

#### <a name="create-a-locationserverxml-file-to-load-balance-multiple-servers-at-different-locations"></a>Crear un archivo LocationServer.xml para equilibrar la carga de varios servidores en ubicaciones diferentes  
 Con LocationServer.xml, especifique varios servidores por cada entrada de ubicación y, después, realice el equilibrio de carga básica de modo que, cuando se elija una ubicación, MDT seleccione automáticamente un servidor de implementación de la lista de servidores disponibles. Para proporcionar esta funcionalidad, el archivo LocationServer.xml permite especificar una métrica de ponderación.  

 A continuación se muestra un ejemplo de un archivo LocationServer.xml configurado para varios servidores en ubicaciones diferentes.  

 **Archivo LocationServer.xml de ejemplo para ubicaciones diferentes**  

```  
<?xml version="1.0" encoding="utf-8" ?>  
<servers>  
    <QueryDefault></QueryDefault>  
    <server>  
        <serverid>1</serverid>  
        <friendlyname>  
          Contoso HQ, Seattle, USA  
        </friendlyname>  
        <Server1>\\STLDS01\Deployment$</Server1>  
        <Server2>\\STLDS02\Deployment$</Server2>  
        <Server3>\\STLDS03\Deployment$</Server3>  
        <Server weight=”1”>\\STLDS01\Deployment$</Server>  
        <Server weight=”2”>\\STLDS02\Deployment$</Server>  
        <Server weight=”4”>\\STLDS03\Deployment$</Server>  
    </server>  
    <server>  
        <serverid>2</serverid>  
        <friendlyname>  
          Contoso NYC, New York, USA  
        </friendlyname>  
        <UNCPath>\\NYCDS01\Deployment$</UNCPath>  
    </server>   
</servers>  
```  

 Especifique la métrica de ponderación mediante la etiqueta <server weight\>, que MDT usa en el proceso de selección de servidor. La probabilidad de que se seleccione un servidor se calcula de la manera siguiente:  

 **Peso del servidor/suma de los pesos de todos los servidores**  

 En el ejemplo anterior, los tres servidores de la sede de Contoso se muestran como 1, 2 y 4. La probabilidad de que un servidor con una ponderación de 2 resulte seleccionado es 2 de 7. Por lo tanto, para usar el sistema de ponderación, determine la capacidad de los servidores disponibles en una ubicación y pondere cada servidor según la capacidad del servidor con respecto a cada uno de los demás servidores.  

### <a name="adding-the-locationserverxml-file-to-the-extra-files-directory"></a>Agregar el archivo LocationServer.xml al directorio de archivos adicionales  
 Después de crear el archivo LocationServer.xml, agréguelo a las imágenes de arranque de Windows PE LiteTouch_x86 y LiteTouch_x64 en la carpeta ***X:\\Deploy\Control***. Use Deployment Workbench para agregar otros archivos y carpetas a estas imágenes de Windows PE. Para ello, especifique un directorio adicional para agregarlo a las propiedades del recurso compartido de implementación.  

 **Para agregar LocationServer.xml al recurso compartido de implementación**  

1.  Cree una carpeta denominada *Extra Files* (Archivos adicionales) en la carpeta del recurso compartido de implementación raíz (por ejemplo, D:\Production Deployment Share\Extra Files).  

2.  Cree una estructura de carpetas en la carpeta Extra Files que refleje la ubicación de Windows PE donde debe residir el archivo adicional.  

     Por ejemplo, el archivo LocationServer.xml debe residir en la carpeta \Deploy\Control en Windows PE. Por lo tanto, cree la misma estructura de carpetas en Extra Files (por ejemplo, D:\Production Deployment Share\Extra Files\Deploy\Control).  

3.  Copie LocationServer.xml en la carpeta *deployment_share*\Extra Files\Deploy\Control, donde *deployment_share* es la ruta de acceso completa de la carpeta raíz del recurso compartido de implementación.  

4.  Haga clic en **Inicio** y seleccione **All Programs** (Todos los programas). Seleccione **Microsoft Deployment Toolkit** y haga clic en **Deployment Workbench**.  

5.  En el árbol de consola de Deployment Workbench, vaya a Deployment Workbench/Deployment Shares (Recursos compartidos de implementación)/*deployment_share*, donde *deployment_share* es el nombre del recurso compartido de implementación que se va a configurar.  

6.  En el panel Acciones, haga clic en **Propiedades**.  

7.  En el cuadro de diálogo ***deployment_shareProperties***, donde deployment_share es el nombre del recurso compartido de implementación, lleve a cabo estos pasos:  

    1.  Haga clic en la pestaña **Windows PE platform Settings** (Configuración de plataforma Windows PE), donde *plataforma* es la arquitectura de la imagen de Windows PE que se va a configurar.  

    2.  En la sección **Windows PE Customizations** (Personalizaciones de Windows PE), en el cuadro **Extra directory to add** (Directorio adicional para agregar), escriba ***path*** (donde *path* es la ruta de acceso absoluta a la carpeta Extra Files, por ejemplo, D:\Production Deployment Share\Extra Files) y haga clic en **Aceptar**.  

###  <a name="UpdateBootstrap"></a> Actualizar el archivo BootStrap.ini  
 Cuando se crea un recurso compartido de implementación mediante Deployment Workbench, se crea y se rellena automáticamente una propiedad **DeployRoot** en el archivo BootStrap.ini. Dado que se usa el archivo LocationServer.xml para rellenar la propiedad **DeployRoot**, debe quitar este valor del archivo BootStrap.ini.  

 **Para quitar la propiedad DeployRoot de BootStrap.ini**  

1.  Haga clic en **Inicio** y seleccione **All Programs** (Todos los programas). Seleccione **Microsoft Deployment Toolkit** y haga clic en **Deployment Workbench**.  

2.  En el árbol de consola de Deployment Workbench, vaya a Deployment Workbench/Deployment Shares (Recursos compartidos de implementación)/*deployment_share*, donde *deployment_share* es el nombre del recurso compartido de implementación que se va a configurar.  

3.  En el panel Acciones, haga clic en **Propiedades**.  

4.  En el cuadro de diálogo ***deployment_shareProperties***, donde *deployment_share* es el nombre del recurso compartido de implementación, haga clic en la pestaña **Reglas** y en **Edit BootStrap.ini** (Editar BootStrap.ini).  

5.  Quite el valor **DeployRoot** (por ejemplo, **DeployRoot=\\\Server\Deployment$**).  

6.  Haga clic en **Archivo** y en **Guardar** para guardar los cambios en el archivo BootStrap.ini.  

7.  Haga clic en **Aceptar** para enviar los cambios.  

###  <a name="UpdateDeploymentShare"></a> Actualizar el recurso compartido de implementación  
 Después, es necesario actualizar el recurso compartido de implementación para generar un nuevo entorno de arranque LiteTouch_x86 y LiteTouch_x64 que contenga el archivo LocationServer.xml y el archivo BootStrap.ini actualizado.  

 **Para actualizar el recurso compartido de implementación**  

1.  Haga clic en **Inicio** y seleccione **All Programs** (Todos los programas). Seleccione **Microsoft Deployment Toolkit** y haga clic en **Deployment Workbench**.  

2.  En el árbol de consola de Deployment Workbench, vaya a Deployment Workbench/Deployment Shares (Recursos compartidos de implementación)/*deployment_share*, donde *deployment_share* es el nombre del recurso compartido de implementación que se va a configurar.  

3.  En el panel Acciones, haga clic en **Update Deployment Share** (Actualizar recurso compartido de implementación).  

     Se inicia el Asistente para actualizar recurso compartido de implementación.  

4.  En la página **Opciones**, seleccione las opciones deseadas para actualizar el recurso compartido de implementación y haga clic en **Siguiente**.  

5.  En la página **Resumen**, compruebe que la información sea correcta y haga clic en **Siguiente**.  

6.  En la página **Confirmación**, haga clic en **Finalizar**.  

> [!NOTE]
>  Cuando el proceso de actualización haya finalizado, agregue los nuevos entornos de Windows PE LiteTouch_x86 y LiteTouch_x64 en Servicios de implementación de Windows, o bien grábelos en los medios de arranque que se usarán durante la implementación.  

## <a name="replacing-an-existing-computer-with-a-new-computer-using-lite-touch-installation"></a>Reemplazar un equipo existente por uno nuevo mediante Lite Touch Installation  
 Puede usar MDT para implementar una imagen en un equipo nuevo que reemplazará a un equipo existente de la arquitectura empresarial. Esta situación podría producirse al actualizar de un sistema operativo a otro (un nuevo sistema operativo podría requerir hardware nuevo) o si la organización necesita equipos más modernos y rápidos para las aplicaciones existentes.  

 Cuando se reemplaza un equipo existente por uno nuevo, Microsoft recomienda tener en cuenta todas las configuraciones que se migrarán de un equipo a otro, como las cuentas de usuario y los datos de estado de usuario. Además, es importante crear una solución de recuperación en caso de que se produzca un error en la migración.  

 En esta implementación de ejemplo, reemplace el equipo existente (WDG-EXIST-01) por uno nuevo (WDG-NEW-02) en el dominio CORP. Para ello, capture los datos de estado de usuario de WDG-EXIST-01 y guárdelos en un recurso compartido de red. Después, implemente una imagen existente en WDG-NEW-02 y, por último, restaure los datos de estado de usuario capturados en WDG-NEW-02. La implementación se realizará desde un servidor de implementación (WDG-MDT-01).  

 En MDT, use la plantilla de secuencia de tareas para reemplazar el cliente estándar a fin de crear una secuencia de tareas que lleve a cabo todas las tareas de implementación necesarias.  

 En esta demostración se da por supuesto lo siguiente:  

-   MDT está instalado en el servidor de implementación (WDG MDT 01).  

-   El recurso compartido de implementación ya se ha creado y rellenado, incluidas las imágenes de sistema operativo, las aplicaciones y los controladores de dispositivo.  

-   Ya se ha capturado una imagen de un equipo de referencia, que se implementará en el equipo nuevo (WDG NEW 02).  

-   Se ha creado una carpeta compartida de red (UserStateCapture$) y se ha compartido en el servidor de implementación (WDG MDT 01) con los permisos adecuados de recurso compartido.  

 Antes de comenzar este ejemplo, debe existir un recurso compartido de implementación. Para más información sobre cómo crear un recurso compartido de implementación, vea la sección "Managing Deployment Shares in the Deployment Workbench" (Administrar recursos compartidos de implementación en Deployment Workbench) en el documento de MDT *Using the Microsoft Deployment Toolkit* (Uso de Microsoft Deployment Toolkit).  

### <a name="step-1-create-a-task-sequence-to-capture-the-user-state"></a>Paso 1: crear una secuencia de tareas para capturar el estado de usuario  
 Cree secuencias de tareas de MDT en el nodo Secuencias de tareas de Deployment Workbench mediante el Asistente para nueva secuencia de tareas. Para llevar a cabo la primera parte del escenario de implementación para reemplazar equipo (capturar el estado de usuario en el equipo existente), seleccione la plantilla de secuencia de tareas para reemplazar el cliente estándar en el Asistente para nueva secuencia de tareas.  

 **Para crear una secuencia de tareas para capturar el estado de usuario en el escenario de implementación para reemplazar equipo**  

1.  Haga clic en **Inicio** y seleccione **All Programs** (Todos los programas). Seleccione **Microsoft Deployment Toolkit** y haga clic en **Deployment Workbench**.  

2.  En el árbol de consola de Deployment Workbench, vaya a Deployment Workbench/Deployment Shares (Recursos compartidos de implementación)/*deployment_share*/Secuencias de tareas, donde *deployment_share* es el nombre del recurso compartido de implementación que se va a configurar.  

3.  En el panel Acciones, haga clic en **Crear nueva secuencia de tareas**.  

     Se inicia el Asistente para nueva secuencia de tareas.  

4.  Rellene el Asistente para nueva secuencia de tareas con la información siguiente. Acepte los valores predeterminados, a menos que se especifique lo contrario.  

    |**En esta página del Asistente** |**Haga esto** |  
    |-|-|  
    |**Configuración general** |1.  En **Id. de secuencia de tareas**, escriba **VISTA_EXIST**.<br />2.  En **Nombre de secuencia de tareas**, escriba **Realizar un escenario para reemplazar equipo en un equipo existente**.<br />3.  Haga clic en **Siguiente**.|  
    |**Seleccionar plantilla** |En **The following task sequence templates are available**. **Select the one you would like to use as a starting point** (Están disponibles las siguientes plantillas de secuencia de tareas. Seleccione la que le gustaría usar como punto de partida), seleccione **Standard Client Replace Task Sequence** (Secuencia de tareas para reemplazar el cliente estándar) y haga clic en **Siguiente**.|  
    |**Resumen** |Compruebe que la información de configuración sea correcta y haga clic en **Siguiente**.|  
    |**Confirmación** |Haga clic en **Finalizar**.|  

 El Asistente para nueva secuencia de tareas finaliza y la secuencia de tareas **VISTA_EXIST** se agrega a la lista de secuencias de tareas.  

### <a name="step-2-create-a-task-sequence-to-deploy-operating-system-and-restore-the-user-state"></a>Paso 2: crear una secuencia de tareas para implementar el sistema operativo y restaurar el estado de usuario  
 Cree secuencias de tareas de MDT en el nodo Secuencias de tareas de Deployment Workbench mediante el Asistente para nueva secuencia de tareas. Para llevar a cabo la segunda parte del escenario de implementación para reemplazar equipo (implementar el sistema operativo y, después, restaurar el estado de usuario en el equipo existente), seleccione la plantilla de secuencia de tareas de cliente estándar en el Asistente para nueva secuencia de tareas.  

 **Para crear una secuencia de tareas para implementar el estado de usuario en el escenario de implementación para reemplazar equipo**  

1.  Haga clic en **Inicio** y seleccione **All Programs** (Todos los programas). Seleccione **Microsoft Deployment Toolkit** y haga clic en **Deployment Workbench**.  

2.  En el árbol de consola de Deployment Workbench, vaya a Deployment Workbench/Deployment Shares (Recursos compartidos de implementación)/*deployment_share*/Secuencias de tareas, donde *deployment_share* es el nombre del recurso compartido de implementación que se va a configurar.  

3.  En el panel Acciones, haga clic en **Crear nueva secuencia de tareas**.  

     Se inicia el Asistente para nueva secuencia de tareas.  

4.  Rellene el Asistente para nueva secuencia de tareas con la información siguiente. Acepte los valores predeterminados, a menos que se especifique lo contrario.  

    |**En esta página del Asistente**|**Haga esto**|  
    |-|-|  
    |**Configuración general**|1.  En **Id. de secuencia de tareas**, escriba **VISTA_NEW**.<br />2.  En **Nombre de secuencia de tareas**, escriba **Realizar un escenario para reemplazar equipo en un equipo nuevo**.<br />3.  Haga clic en **Siguiente**.|  
    |**Seleccionar plantilla**|En **The following task sequence templates are available**. **Select the one you would like to use as a starting point** (Están disponibles las siguientes plantillas de secuencia de tareas. Seleccione la que le gustaría usar como punto de partida), seleccione **Standard Client Task Sequence** (Secuencia de tareas de cliente estándar) y haga clic en **Siguiente**.|  
    |**Seleccione el sistema operativo**|En **The following operating system images are available to be deployed with this task sequence** (Las imágenes de sistema operativo siguientes están disponibles para su implementación con esta secuencia de tareas) seleccione una para su uso, seleccione ***captured_vista_image*** (donde *captured_vista_image* es la imagen capturada que el equipo de referencia ha agregado al nodo Sistemas operativos de Deployment Workbench) y haga clic en *Siguiente*.|  
    |**Especifique la clave del producto**|Seleccione **Do not specify a product key at this time** (No especificar una clave de producto en este momento) y haga clic en **Siguiente**.|  
    |Configuración del sistema operativo|1.  En **Nombre completo**, escriba **Empleado de Woodgrove**.<br />2.  En **Organización**, escriba **Banco Woodgrove**.<br />3.  En **Página principal de Internet Explorer**, escriba **http://www.woodgrovebank.com**.<br />4.  Haga clic en **Siguiente**.|  
    |**Contraseña de administrador**|En **Contraseña de administrador** y **Please confirm Administrator Password** (Confirme la contraseña de administrador), escriba **P@ssw0rd** y haga clic en **Finalizar**.|  
    |**Confirmación**|Haga clic en **Finalizar**.|  

 El Asistente para nueva secuencia de tareas finaliza y la secuencia de tareas **VISTA_NEW** se agrega a la lista de secuencias de tareas.  

### <a name="step-3-customize-the-mdt-configuration-files"></a>Paso 3: personalizar los archivos de configuración de MDT  
 Cuando se haya creado la secuencia de tareas de MDT, personalice los archivos de configuración de MDT que proporcionan los valores de configuración para capturar la información de estado de usuario. En concreto, personalice el archivo CustomSettings.ini mediante su modificación en las propiedades del recurso compartido de implementación creado anteriormente en el proceso de implementación. En un paso posterior, el recurso compartido de implementación se actualizará para garantizar que el archivo de configuración se actualice en el recurso compartido de implementación.  

 **Para personalizar los archivos de configuración de MDT para capturar la información de estado de usuario**  

1.  Haga clic en **Inicio** y seleccione **All Programs** (Todos los programas). Seleccione **Microsoft Deployment Toolkit** y haga clic en **Deployment Workbench**.  

2.  En el árbol de consola de Deployment Workbench, vaya a Deployment Workbench/Deployment Shares (Recursos compartidos de implementación)/*deployment_share*, donde *deployment_share* es el nombre del recurso compartido de implementación que se va a configurar.  

3.  En el panel Acciones, haga clic en **Propiedades**.  

     Se abre el cuadro de diálogo **Propiedades**.  

4.  En el cuadro de diálogo **Propiedades**, haga clic en la pestaña **Reglas**.  

5.  En la pestaña **Reglas**, modifique el archivo CustomSettings.ini para reflejar los cambios necesarios como se muestra en el ejemplo siguiente. Realice las modificaciones adicionales que requiera el entorno.  

     **Archivo CustomSettings.ini personalizado**  

    ```  
    [Settings]  
    Priority=Default  
    Properties=MyCustomProperty  

    [Default]  
    OSInstall=Y  

    UDShare=\\WDG-MDT-01\UserStateCapture$  
    UDDir=%OSDCOMPUTERNAME%  
    UserDataLocation=NETWORK  
    SkipCapture=NO  
    SkipAdminPassword=YES  
    SkipProductKey=YES  

    ```  

6.  En el cuadro de diálogo **Propiedades**, haga clic en **Aceptar**.  

7.  Cierre todas las ventanas y cuadros de diálogo abiertos.  

### <a name="step-4-configure-the-windows-pe-options-for-the-deployment-share"></a>Paso 4: configurar las opciones de Windows PE para el recurso compartido de implementación  
 Configure las opciones de Windows PE para el recurso compartido de implementación en el nodo Recursos compartidos de implementación de Deployment Workbench.  

> [!NOTE]
>  Si los controladores de dispositivo para el equipo existente (WDG-EXIST-01) y el equipo nuevo (WDG-NEW-01) ya están incluidos con Windows Vista, omita este paso y continúe con el paso siguiente.  

 **Para configurar las opciones de Windows PE para el recurso compartido de implementación**  

1.  Haga clic en **Inicio** y seleccione **All Programs** (Todos los programas). Seleccione **Microsoft Deployment Toolkit** y haga clic en **Deployment Workbench**.  

2.  En el árbol de consola de Deployment Workbench, vaya a Deployment Workbench/Deployment Shares (Recursos compartidos de implementación)/*deployment_share*, donde *deployment_share* es el nombre del recurso compartido de implementación que se va a configurar.  

3.  En el panel Acciones, haga clic en **Propiedades**.  

     Se abre el cuadro de diálogo **Propiedades**.  

4.  En el cuadro de diálogo **Propiedades**, en la pestaña **Componentes de la *plataforma* Windows PE** (donde la *plataforma* es la arquitectura de la imagen de Windows PE que se va a configurar), en **Selection profile** (Perfil de selección), seleccione ***device_drivers*** (donde *device_drivers* es el nombre del perfil de selección de controladores de dispositivo) y haga clic en **Aceptar**.  

### <a name="step-5-update-the-deployment-share"></a>Paso 5: actualizar el recurso compartido de implementación  
 Después de configurar las opciones de Windows PE para el recurso compartido de implementación, actualice el recurso compartido de implementación. Al actualizar el recurso compartido de implementación se actualizan todos los archivos de configuración de MDT y se genera una versión personalizada de Windows PE. La versión personalizada de Windows PE se usa para iniciar el equipo de referencia e iniciar el proceso de implementación de LTI.  

 **Para actualizar el recurso compartido de implementación en Deployment Workbench**  

1.  Haga clic en **Inicio** y seleccione **All Programs** (Todos los programas). Seleccione **Microsoft Deployment Toolkit** y haga clic en **Deployment Workbench**.  

2.  En el árbol de consola de Deployment Workbench, vaya a Deployment Workbench/Deployment Shares (Recursos compartidos de implementación)/*deployment_share*, donde *deployment_share* es el nombre del recurso compartido de implementación que se va a configurar.  

3.  En el panel Acciones, haga clic en **Update Deployment Share** (Actualizar recurso compartido de implementación).  

     Se inicia el Asistente para actualizar recurso compartido de implementación.  

4.  En la página **Opciones**, seleccione las opciones deseadas para actualizar el recurso compartido de implementación y haga clic en **Siguiente**.  

5.  En la página **Resumen**, compruebe que la información sea correcta y haga clic en **Siguiente**.  

6.  En la página **Confirmación**, haga clic en **Finalizar**.  

 Deployment Workbench empieza a actualizar el recurso compartido de implementación. Deployment Workbench crea los archivos LiteTouchPE_x86.iso y LiteTouchPE_x86.wim (para los equipos de destino de 32 bits) o los archivos LiteTouchPE_x64.iso y LiteTouchPE_x64.wim (para los equipos de destino de 64 bits) en la carpeta *deployment_share*\Boot (donde *deployment_share* es la carpeta compartida que se usa como recurso compartido de implementación).  

### <a name="step-6-create-the-lti-bootable-media"></a>Paso 6: crear los medios de arranque de LTI  
 Proporcione un método para iniciar el equipo con la versión personalizada de Windows PE creada al actualizar el recurso compartido de implementación. Deployment Workbench crea los archivos LiteTouchPE_x86.iso y LiteTouchPE_x86.wim (para los equipos de destino de 32 bits) o los archivos LiteTouchPE_x64.iso y LiteTouchPE_x64.wim (para los equipos de destino de 64 bits) en la carpeta *deployment_share*\Boot (donde *deployment_share* es la carpeta compartida que se usa como recurso compartido de implementación). Cree los medios de arranque de LTI adecuados a partir de una de estas imágenes.  

 **Para crear los medios de arranque de LTI**  

1.  En el Explorador de Windows, vaya a la carpeta *deployment_share*\Boot, donde *deployment_share* es la carpeta compartida que se usa como recurso compartido de implementación.  

2.  Según el tipo de equipo que se use para el equipo existente (WDG-EXIST-01) y el equipo nuevo (WDG-NEW-02), realice una de las tareas siguientes:  

    -   Si el equipo de referencia es un equipo físico, cree un CD o un DVD del archivo ISO.  

    -   Si el equipo de referencia es una máquina virtual, iníciela directamente desde el archivo ISO o desde un CD o un DVD del archivo ISO.  

### <a name="step-7-start-the-existing-computer-with-the-lti-bootable-media"></a>Paso 7: iniciar el equipo existente con los medios de arranque de LTI  
 Inicie el equipo existente (WDG-EXIST-01) con los medios de arranque de LTI que ha creado anteriormente en el proceso. Este CD inicia Windows PE en el equipo existente y da comienzo al proceso de implementación de MDT. Al final del proceso de implementación de MDT, la información de migración del estado de usuario se almacena en la carpeta compartida UserStateCapture$.  

> [!NOTE]
>  También puede comenzar el proceso de MDT si inicia el equipo de destino desde Servicios de implementación de Windows. Para más información, vea la sección "Preparing Windows Deployment Services" (Preparar Servicios de implementación de Windows) en el documento de MDT *Using the Microsoft Deployment Toolkit* (Uso de Microsoft Deployment Toolkit).  

 **Para iniciar el equipo existente con los medios de arranque de LTI**  

1.  Inicie WDG-EXIST-01 con los medios de arranque de LTI que ha creado anteriormente en el proceso.  

     Se inicia Windows PE y, después, el Asistente para la implementación de Windows.  

2.  Complete el Asistente para la implementación de Windows con la información siguiente. Acepte los valores predeterminados, a menos que se especifique lo contrario.  

    |**En esta página del Asistente**|**Haga esto**|  
    |-|-|  
    |**Welcome to Deployment** (Le damos la bienvenida a la implementación)|Haga clic en **Run the Deployment Wizard** (Ejecutar el Asistente para la implementación) para instalar un nuevo sistema operativo y, después, haga clic en **Siguiente**.|  
    |**Specify Credentials for connecting to network shares** (Escriba las credenciales para conectarse a los recursos compartidos de red)|1.  En **Nombre de usuario**, escriba **Administrador**.<br />2.  En **Contraseña**, escriba **P@ssw0rd**.<br />3.  En **Dominio**, escriba **CORP**.<br />4.  Haga clic en **Aceptar**.|  
    |**Select a task sequence to execute on this computer** (Seleccione una secuencia de tareas para ejecutarla en este equipo)|Haga clic en *Realizar un escenario para reemplazar equipo en un equipo existente* y en **Siguiente**.|  
    |**Specify where to save your data and settings** (Especifique dónde guardar los datos y la configuración)|Haga clic en **Siguiente**.|  
    |**Specify where to save a complete computer backup** (Especifique dónde quiere guardar una copia de seguridad completa del equipo)|Haga clic en **Do not back up the existing computer** (No hacer copia de seguridad del equipo existente) y, luego, haga clic en **Siguiente**.|  
    |**Ready to begin** (Listo para comenzar)|Haga clic en **Comenzar**.|  

     Si se producen errores o advertencias, vea el documento de MDT *Troubleshooting Reference* (Referencia de solución de problemas).  

3.  En el cuadro de diálogo **Resumen de implementación**, haga clic en **Detalles**.  

     Si se han producido errores o advertencias, revíselos y registre la información de diagnóstico.  

4.  En el cuadro de diálogo **Resumen de implementación**, haga clic en **Finalizar**.  

 La información de migración de estado de usuario se captura y se almacena en la carpeta compartida de red (UserStateCapture$) creada anteriormente en el proceso.  

### <a name="step-8-start-the-new-computer-with-the-lti-bootable-media"></a>Paso 8: iniciar el equipo nuevo con los medios de arranque de LTI  
 Inicie el equipo nuevo (WDG-NEW-02) con los medios de arranque de LTI que ha creado anteriormente en el proceso. Este CD inicia Windows PE en el equipo de referencia y da comienzo al proceso de implementación de MDT. Al final del proceso de implementación de MDT, Windows Vista se implementa en el equipo nuevo y se restaura en el nuevo equipo la información de migración de estado de usuario capturada.  

> [!NOTE]
>  También puede comenzar el proceso de MDT si inicia el equipo de destino desde Servicios de implementación de Windows. Para más información, vea la sección "Preparing Windows Deployment Services" (Preparar Servicios de implementación de Windows) en el documento de MDT *Using the Microsoft Deployment Toolkit* (Uso de Microsoft Deployment Toolkit).  

 **Para iniciar el equipo nuevo con los medios de arranque de LTI**  

1.  Inicie WDG-NEW-02 con los medios de arranque de LTI que ha creado anteriormente en el proceso.  

     Se inicia Windows PE y, después, el Asistente para la implementación de Windows.  

2.  Complete el Asistente para la implementación de Windows con la información siguiente. Acepte los valores predeterminados, a menos que se especifique lo contrario.  

    |**En esta página del Asistente**|**Haga esto**|  
    |--|--|
    |**Welcome to Deployment** (Le damos la bienvenida a la implementación)|Haga clic en **Run the Deployment Wizard** (Ejecutar el Asistente para la implementación) para instalar un nuevo sistema operativo y, después, haga clic en **Siguiente**.|  
    |**Specify Credentials for connecting to network shares** (Escriba las credenciales para conectarse a los recursos compartidos de red)|1.  En **Nombre de usuario**, escriba **Administrador**.<br />2.  En **Contraseña**, escriba **P@ssw0rd**.<br />3.  En **Dominio**, escriba **CORP**.<br />4.  Haga clic en **Aceptar**.|  
    |**Select a task sequence to execute on this computer** (Seleccione una secuencia de tareas para ejecutarla en este equipo)|Haga clic en **Realizar un escenario para reemplazar equipo en un equipo nuevo** y en **Siguiente**.|  
    |**Configure the computer name** (Configure el nombre del equipo)|En **Nombre_equipo**, escriba **WDG-NEW-02** y haga clic en **Siguiente**.|  
    |**Join the computer to a domain or workgroup** (Unir el equipo a un dominio o grupo de trabajo)|Haga clic en **Siguiente**.|  
    |**Specify whether to restore user data** (Especifique si quiere restaurar los datos de usuario)|1.  Haga clic en **Specify a location** (Especificar una ubicación).<br />2.  En **Ubicación**, escriba **\\\WDG-MDT-01\UserStateCapture$\WDG-EXIST-01**.<br />3.  Haga clic en **Siguiente**.|  
    |**Locale Selection** (Selección de configuración regional)|Haga clic en **Siguiente**.|  
    |**Set the Time Zone** (Establezca la zona horaria)|Haga clic en **Siguiente**.|  
    |**Specify whether to capture an image** (Especifique si quiere capturar una imagen)|Haga clic en **Do not capture an image of this computer** (No capturar una imagen de este equipo) y en **Siguiente**.|  
    |**Specify the BitLocker configuration** (Especificar la configuración de BitLocker)|Haga clic en **Do not enable BitLocker for this computer** (No habilitar BitLocker para este equipo) y en **Siguiente**.|  
    |**Ready to begin** (Listo para comenzar)|Haga clic en **Comenzar**.|  

     Si se producen errores o advertencias, vea el documento de MDT *Troubleshooting Reference* (Referencia de solución de problemas).  

3.  En el cuadro de diálogo **Resumen de implementación**, haga clic en **Detalles**.  

     Si se han producido errores o advertencias, revíselos y registre la información de diagnóstico.  

4.  En el cuadro de diálogo **Resumen de implementación**, haga clic en **Finalizar**.  

 Windows Vista ya está instalado en el equipo nuevo y también se ha restaurado la información de migración de estado de usuario capturada.  

## <a name="integrating-custom-deployment-code-into-mdt"></a>Integrar código de implementación personalizado en MDT  
 Es habitual que un equipo de implementación se encuentre con requisitos complejos específicos de su entorno de destino que no se pueden cumplir mediante las acciones de las secuencias de tareas predefinidas de Deployment Workbench o los archivos de configuración de MDT predeterminados. En este caso, es necesario implementar código personalizado para satisfacer los requisitos.  

 Para integrar código de implementación personalizado en MDT, haga lo siguiente:  

-   Elija un lenguaje de scripting como se describe en [Elegir el lenguaje de scripting adecuado](#ChooseAppropLanguage).  

-   Aproveche ZTIUtility.vbs como se describe en [Entender cómo aprovechar ZTIUtility](#UnderstandLeverageZTI).  

-   Integre código de implementación personalizado como se describe en [Integrar código de implementación personalizado](#IntegrateCustomDeploy).  

 En las secciones siguientes se da por supuesto que MDT está configurado en un servidor de implementación.  

###  <a name="ChooseAppropLanguage"></a> Elegir el lenguaje de scripting adecuado  
 Aunque es posible llamar como una instalación de aplicación o mediante un paso de secuencia de tareas de MDT a todos los tipos de código que se pueden ejecutar en Windows o Windows PE, Microsoft recomienda usar scripts con el formato de archivos .vbs o .wsf.  

 La ventaja de usar archivos .wsf reside en el registro integrado y en otras funciones predefinidas que ya usan los procesos de ZTI y LTI. Estas funciones están disponibles en el script ZTIUtility que se distribuye con MDT.  

 Cuando se hace referencia a él desde un script personalizado, el script ZTIUtility inicializa las clases de configuración y entorno de MDT. Están disponibles estas clases:  

-   **Logging**. Esta clase proporciona la funcionalidad de registro que usan todos los scripts de MDT. También crea un único archivo de registro para cada script que se ejecuta durante la implementación y un archivo de registro consolidado de todos los scripts. Estos archivos de registro se crean en un formato diseñado para que lo lea TRACE32, una herramienta disponible en [System Center Configuration Manager 2007 Toolkit V2](https://www.microsoft.com/download/en/details.aspx?id=9257).  

-   **Environment**. Esta clase configura las variables de entorno recopiladas mediante el procesamiento de reglas de WMI y MDT y permite hacer referencia a ellas directamente desde el script. Esto permite leer las propiedades de implementación, lo que da acceso a toda la información de configuración que usan los procesos de ZTI y LTI.  

-   **Utility**. Esta clase proporciona utilidades generales que se usan en los scripts de ZTI y LTI. Microsoft recomienda examinar esta clase siempre que se desarrolle código personalizado para comprobar si se puede reutilizar código. Más adelante en esta sección se incluye información adicional sobre algunas de las funcionalidades que se proporcionan en esta clase.  

-   **Database**. Esta clase realiza funciones como conectarse a bases de datos y leer información de estas. En general, no se recomienda tener acceso directamente a la clase database; en su lugar, debe usarse el procesamiento de reglas para realizar búsquedas de base de datos.  

-   **Strings**. Esta clase realiza rutinas comunes de procesamiento de cadena, como crear una lista delimitada de elementos, mostrar un valor hexadecimal, recortar el espacio en blanco de una cadena, alinear a la derecha una cadena, alinear a la izquierda una cadena, forzar a que un valor tenga el formato de cadena, forzar a que un valor tenga el formato de matriz, generar un identificador único global (GUID) aleatorio y realizar conversiones de Base64.  

-   **FileHandling**. Esta clase realiza funciones como normalizar rutas de acceso y copiar, mover y eliminar archivos y carpetas.  

-   **clsRegEx**. Esta clase realiza funciones de expresión regular.  

 En MDT, se ha realizado un par de cambios en la arquitectura de script para que el cliente de Microsoft Visual Basic® Scripting Edition (VBScript) sea más sólido y confiable. Entre estos cambios se incluyen los siguientes:  

-   Cambios importantes en ZTIUtility.vbs (la biblioteca de scripts principal), incluidas nuevas API y un mejor control de errores.  

-   Un nuevo aspecto para la estructura general de los scripts ZTI_*xxx*.wsf.  

 También se ha cambiado la estructura general de los scripts de MDT. La mayoría de los scripts de MDT ahora se encapsula en objetos **Class** de VBScript. La clase se inicializa y se llama con la función **RunNewInstance**.  

> [!NOTE]
>  La mayoría de los scripts existentes de MDT 2008 Update 1 funcionará tal cual en MDT, incluso con los cambios realizados en ZTIUtility.vbs, ya que prácticamente todos los scripts de MDT incluirán ZTIUtility.vbs.  

###  <a name="UnderstandLeverageZTI"></a> Entender cómo aprovechar ZTIUtility  
 El archivo ZTIUtility.vbs contiene las clases de objeto que se pueden aprovechar en el código personalizado. Para integrar código personalizado con MDT, use lo siguiente:  

-   La clase Logging definida en ZTIUtility.vbs como se describe en [Usar la clase Logging de ZTIUtility](#UseZTILogging).  

-   La clase Environment definida en ZTIUtility.vbs como se describe en [Usar la clase Environment de ZTIUtility](#UseZTIEnvironment).  

-   La clase Utility definida en ZTIUtility.vbs como se describe en [Usar la clase Utility de ZTIUtility](#UseZTIUtility).  

####  <a name="UseZTILogging"></a> Usar la clase Logging de ZTIUtility  
 La clase Logging de ZTIUtiliy.vbs proporciona un mecanismo sencillo para que el código personalizado registre información de estado, advertencias y errores de la misma manera que otros scripts durante una implementación de ZTI o LTI. Esta normalización también garantiza que el cuadro de diálogo **LTI Deployment Summary** (Resumen de la implementación de LTI) notifique correctamente el estado de todo el código personalizado que se ejecute.  

 A continuación se muestra un ejemplo de script de código personalizado que usa las funciones **oLogging.CreateEntry** y **TestAndFail** para registrar diferentes tipos de mensajes, según los resultados de las diversas acciones de script.  

 **Script de ejemplo que usa Logging de ZTIUtility: ZTI_Example.wsf**  

```  
<job id="ZTI_Example">  
<script language="VBScript" src="ZTIUtility.vbs"/>  
<script language="VBScript">  

' //*******************************************************  
' //  
' // Copyright (c) Microsoft Corporation.  All rights reserved  
' // Microsoft Deployment Toolkit Solution Accelerator  
' // File: ZTI_Example.wsf  
' //  
' // Purpose: Example of scripting with the  
' //          Microsoft Deployment Toolkit.  
' //  
' // Usage: cscript ZTI_Example.wsf [/debug:true]  
' //  
' //*******************************************************  

Option Explicit  
RunNewInstance  

'//--------------------------------------------------------  
'// Main Class  
'//--------------------------------------------------------  
Class ZTI_Example  

'//--------------------------------------------------------  
'// Main routine  
'//--------------------------------------------------------  

Function Main()  

  Dim iRetVal  
  Dim sScriptPath  

  iRetVal = SUCCESS  

  oLogging.CreateEntry "Begin example script…", _  
    LogTypeInfo  

  ' %ServerA% is a generic variable available within  
  ' every CustomSettings.ini file.  

  sScriptPath = "\\" & oEnvironment.Item("ServerA") & _  
    "\public\products\Applications\User\Technet\USEnglish"  

  ' Validate a connection to server, net connect with  
  ' credentials if necessary.  
  iRetVal = oUtility.ValidateConnection( sScriptPath )  
  TestAndFail iRetVal, 9991, "Validate Connection to [" & _  
    sScriptPath & "]"  

  'Run Setup Program  

  iRetVal = oUtility.RunWithHeartbeat( """" & _  
    sScriptPath & "\setup.exe"" /?" )  
  TestAndFail iRetVal, 9991, "RunWithHeartbeat [" & _  
    sScriptPath & "]"  

  'Perform any cleanup from installation process  

  oShell.RegWrite "HKLM\Software\Microsoft\SomeValue", _  
    "Done with Execution of XXX.", "REG_SZ"  

  Main = iRetVal  

End Function  

End Class  

</script>  
</job>  
```  

> [!NOTE]
>  Si quiere seguir usando scripts que llaman a **ZTIProcess()** con **ProcessResults()** puede hacerlo, pero ciertas características mejoradas de control de errores no estarán habilitadas.  

####  <a name="UseZTIEnvironment"></a> Usar la clase Environment de ZTIUtility  
 La clase Environment de ZTIUtiliy.vbs proporciona acceso a las propiedades de MDT y permite actualizarlas. En el ejemplo anterior, se usa **oEnvironment.Item("Memory")** para recuperar la cantidad de memoria RAM disponible. También se puede usar para recuperar el valor de cualquiera de las propiedades descritas en el documento de MDT *Toolkit Reference* (Referencia del kit de herramientas).  

####  <a name="UseZTIUtility"></a> Usar la clase Utility de ZTIUtility  
 El script ZTIUtility.vbs contiene un número de utilidades de uso frecuente que cualquier script de implementación personalizado puede usar. Puede agregar estas utilidades a cualquier script de la misma manera que las clases **oLogging** y **oEnvironment**.  

En la tabla siguiente se detallan algunas funciones útiles disponibles y su salida. Para obtener una lista completa de las funciones disponibles, vea el archivo ZTIUtility.vbs.  

|**Función**|**Salida**|  
|-|-|
|**oUtility.LocalRootPath**|Devuelve la ruta de acceso de la carpeta raíz que el proceso de implementación usa en el equipo de destino, por ejemplo, C:\MININT.|  
|**oUtility.BootDevice**|Devuelve el dispositivo de arranque del sistema, por ejemplo, MULTI(0)DISK(0)RDISK(0)PARTITION(1).|  
|**oUtility.LogPath**|Devuelve la ruta de acceso a la carpeta de registros que se usa durante la implementación, por ejemplo, C:\MININT\SMSOSD\OSDLOGS.|  
|**oUtility.StatePath**|Devuelve la ruta de acceso del almacén de estado configurado actualmente, por ejemplo, C:\MININT\StateStore.|  
|**oUtility.ScriptName**|Devuelve el nombre del script que llama a la función, por ejemplo, Z-RAMTest.|  
|**oUtility.ScriptDir**|Devuelve la ruta de acceso al script que llama a la función, por ejemplo, \\\server_name\Deployment$\Scripts.|  
|**oUtility.ComputerName**|Determina el nombre de equipo que se usará durante el proceso de compilación, por ejemplo, nombre_equipo.|  
|**oUtility.ReadIni(file, section, item)**|Permite que el elemento especificado se lea desde un archivo .ini.|  
|**oUtility.WriteIni(file, section, item, value)**|Permite que el elemento especificado se escriba en un archivo .ini.|  
|**oUtility.Sections(file)**|Lee las secciones de un archivo .ini y las almacena en un objeto para usarlo como referencia.|  
|**oUtility.SectionContents(file, section)**|Lee el contenido del archivo .ini especificado y lo almacena en un objeto.|  
|**oUtility.RunWithHeartbeat(sCmd)**|Cuando se ejecuta el comando, escribe información de latido en los registros cada 0,5 segundos.|  
|**oUtility.FindFile**<br /><br /> **(sFilename,sFoundPath)**|Busca el archivo especificado en la carpeta DeployRoot y subcarpetas estándar, como Servicing, Tools, USMT, Templates, Scripts y Control.|  
|**oUtility.findMappedDrive(sServerUNC)**|Comprueba si una unidad está asignada a la ruta de acceso UNC especificada y devuelve la letra de unidad.|  
|**oUtility.ValidateConnection(sServerUNC)**|Comprueba si existe una conexión con el servidor especificado y, en caso de que no exista, intenta crear una.|  
|**MapNetworkDrive**<br /><br /> **(sShare, SDomID, sDomPwd)**|Asigna una letra de unidad a la ruta de acceso UNC especificada como recurso compartido y devuelve la letra de unidad que se usa. Si no lo consigue, devuelve un error.|  
|**VerifyPathExists(strPath)**|Comprueba que la ruta de acceso especificada existe.|  
|**oEnvironment.Substitute(sVal)**|Expande las variables o las funciones de una cadena especificada.|  
|**oEnvironment.Item**<br /><br /> **(sName)**|Lee o escribe una variable en un almacén persistente.|  
|**oEnvironment.Exists**<br /><br /> **(sName)**|Comprueba si la variable existe.|  
|**oEnvironment.ListItem**<br /><br /> **(sName)**|Lee o escribe una variable de tipo **array** en un almacén persistente.|  
|**oLogging.ReportFailure**<br /><br /> **(sMessage, iError)**|Se usa para realizar una salida estructurada si se detecta un error irrecuperable.|  
|**oLogging.CreateEvent**<br /><br /> **(iEventID, iType, sMessage, arrParms)**|Escribe un mensaje en el archivo de registro y envía el evento a un servidor definido.|  
|**oLogging.CreateEntry**<br /><br /> **(sLogMsg, iType)**|Escribe un mensaje en el archivo de registro.|  
|**TestAndFail(iRc, iError, sMessage)**|Sale del script con **iError** si **iRc** es False o si se produce un error.|  
|**TestAndLog(iRc , sMessage)**|Registra una advertencia solo si **iRc** es False o se produce un error.|  

###  <a name="IntegrateCustomDeploy"></a> Integrar código de implementación personalizado  
 Se puede integrar código de implementación personalizado en el proceso de MDT de varias maneras, pero, independientemente del método usado, deben cumplirse las dos reglas siguientes:  

-   El nombre del script de código de implementación personalizado siempre debe comenzar por la letra Z.  

-   El código de implementación personalizado debe colocarse en la carpeta Scripts en el recurso compartido de implementación, por ejemplo, D:\Production Deployment Share\Scripts.  

 Los métodos usados con más frecuencia para integrar código personalizado que también garantizan un registro coherente son los siguientes:  

-   Implementar el código como una aplicación de MDT  

-   Iniciar el código como un comando de secuencia de tareas de MDT  

-   Iniciar el código como un script de salida de usuario  

#### <a name="deploy-custom-code-as-an-mdt-application"></a>Implementar el código personalizado como una aplicación de MDT  
 El código de implementación personalizado puede importarse en Deployment Workbench y administrarse de la misma manera que cualquier otra aplicación.  

 **Para crear una aplicación para ejecutar código de implementación personalizado**  

1.  Copie el código de implementación personalizado en la carpeta *deployment_share*\Scripts, (donde *deployment_share* es la ruta de acceso completa del recurso compartido de implementación.  

2.  Haga clic en **Inicio** y seleccione **All Programs** (Todos los programas). Seleccione **Microsoft Deployment Toolkit** y haga clic en **Deployment Workbench**.  

3.  En el árbol de consola de Deployment Workbench, vaya a Deployment Shares/*deployment_share*/Applications, donde *deployment_share* es el nombre del recurso compartido de implementación que se va a configurar.  

4.  En el panel Acciones, haga clic en **Nueva aplicación**.  

     Se inicia el Asistente para nuevas aplicaciones.  

5.  Complete el Asistente para nuevas aplicaciones con la información siguiente. Acepte los valores predeterminados, a menos que se especifique lo contrario.  

    |**En esta página del Asistente**|**Haga esto**|  
    |-|-|  
    |**Tipo de aplicación**|Haga clic en **Application without source files or elsewhere on the network** (Aplicación sin archivos de código fuente o en otra parte de la red) y en **Siguiente**.|  
    |**Detalles**|Complete esta página según la información de la aplicación y haga clic en **Siguiente**.|  
    |**Detalles del comando**|1.  En el cuadro **Línea de comandos**, escriba **cscript.exe %SCRIPTROOT%\custom_code**, donde *custom_code* es el nombre del código personalizado que se ha desarrollado.<br />2.  En el cuadro **Directorio de trabajo**, escriba ***working_directory***, donde working_directory es el nombre del directorio de trabajo del código personalizado, que suele ser la misma carpeta que se ha especificado en el cuadro **Línea de comandos**.<br />3.  Haga clic en **Siguiente**.|  
    |**Resumen**|Compruebe que las opciones de configuración sean correctas y haga clic en **Siguiente**.|  
    |**Confirmación**|Haga clic en **Finalizar**.|  

 La aplicación se muestra en el nodo Aplicaciones de Deployment Workbench.  

#### <a name="add-the-custom-code-as-a-task-sequence-step"></a>Agregar el código personalizado como un paso de secuencia de tareas  
 Es posible llamar directamente al código de implementación personalizado desde cualquier punto dentro de una secuencia de tareas. Esto da acceso a las reglas y opciones habituales de la secuencia de tareas.  

 **Para agregar el código de implementación personalizado a una secuencia de tareas existente**  

1.  Copie el código de implementación personalizado en la carpeta *deployment_share*\Scripts, (donde *deployment_share* es la ruta de acceso completa del recurso compartido de implementación.  

2.  Haga clic en **Inicio** y seleccione **All Programs** (Todos los programas). Seleccione **Microsoft Deployment Toolkit** y haga clic en **Deployment Workbench**.  

3.  En el árbol de consola de Deployment Workbench, vaya a Deployment Workbench/Deployment Shares (Recursos compartidos de implementación)/*deployment_share*/Secuencias de tareas, donde *deployment_share* es el nombre del recurso compartido de implementación que se va a configurar.  

4.  En el panel de detalles, haga clic en ***task_sequence***, donde *task_sequence* es el nombre de la secuencia de tareas que ejecuta el código personalizado.  

5.  En el panel Acciones, haga clic en **Propiedades**.  

6.  En el cuadro de diálogo ***task_sequenceProperties***, haga clic en la pestaña **Secuencia de tareas**.  

7.  En el árbol de consola, vaya a *grupo*, donde *grupo* es el grupo al que se va a agregar el paso de secuencia de tareas.  

8.  Haga clic en **Agregar**, en **General** y en **Ejecutar línea de comandos**.  

9. En el árbol de consola, haga clic en **Ejecutar línea de comandos** y en la pestaña **Propiedades**.  

10. En el cuadro **Nombre**, escriba ***nombre***, donde *nombre* es un nombre descriptivo del código personalizado.  

11. En la pestaña **Propiedades**, en el cuadro **Línea de comandos**, escriba ***command_line***, donde *command_line* es el comando para ejecutar el código personalizado (por ejemplo, **cscript.exe %SCRIPTROOT%\CustomCode.vbs**).  

12. En el cuadro **Start in** (Iniciar en), escriba ***path***, donde *path* es la ruta de acceso completa de la carpeta de trabajo del código personalizado (suele ser la ruta de acceso especificada en el cuadro **Línea de comandos**) y haga clic en **Aceptar**.  

 El paso de secuencia de tareas recién creado aparece en la lista de pasos de secuencia de tareas.  

#### <a name="run-custom-code-as-a-user-exit-script"></a>Ejecutar código como un script de salida de usuario  
 También es posible ejecutar el código personalizado como un script de salida de usuario desde CustomSettings.ini con la directiva **UserExit**. Esto proporciona un mecanismo para pasar información en el proceso de validación de reglas de CustomSettings.ini y proporciona una actualización dinámica de las propiedades de MDT.  

 Para más información sobre los scripts de salida de usuario y la directiva **UserExit**, vea la sección "User Exit Scripts in the CustomSettings.ini File" (Scripts de salida de usuario en el archivo CustomSettings.ini) del documento de MDT *Using the Microsoft Deployment Toolkit* (Uso de Microsoft Deployment Toolkit).  

## <a name="installing-device-drivers-using-various-installation-methods"></a>Instalar controladores de dispositivo mediante distintos métodos de instalación  
 En este escenario, usará MDT para implementar un sistema operativo en diferentes tipos de hardware. Como parte del proceso de implementación, debe identificar e instalar los controladores de dispositivo de modo que cada tipo de hardware funcione correctamente. Hay dos tipos principales de controladores de dispositivo; cada uno de ellos debe administrarse de manera diferente durante el proceso de implementación:  

-   Controladores de dispositivo que contienen un archivo .inf que se puede usar para importar el controlador de dispositivo en Deployment Workbench.  

-   Controladores de dispositivo que están empaquetados como una aplicación y que se deben instalar como tal.  

 Con MDT, puede controlar ambos tipos de controladores como parte de una implementación de sistema operativo.  

 Para instalar controladores de dispositivo:  

-   Determine los métodos de instalación de cada controlador de dispositivo como se describe en [Determinar qué método se debe usar para instalar un controlador de dispositivo](#WhichMethodtoInstallDriver).  

-   Use el método de controladores predeterminados como se describe en [Instalar controladores de dispositivo con el método de controladores predeterminados](#InstallOutofBoxDrivers).  

-   Instálelos como aplicaciones como se describe en [Instalar controladores de dispositivo como aplicaciones](#InstallDriversasApplications).  

 En este escenario se da por supuesto que MDT se ejecuta en un servidor de implementación.  

###  <a name="WhichMethodtoInstallDriver"></a> Determinar qué método se debe usar para instalar un controlador de dispositivo  
 Los fabricantes de hardware publican los controladores de dispositivo de una de las siguientes maneras:  

-   Como un paquete que puede extraer y que contiene archivos .inf usados para importar el controlador en Deployment Workbench.  

-   Como una aplicación que se debe instalar mediante los procesos tradicionales de instalación de aplicaciones.  

 Los paquetes de controladores de dispositivo que se pueden extraer para tener acceso a los archivos .inf pueden usar el proceso automático de detección e instalación de controladores de MDT. Para ello, primero importan el controlador en el nodo de controladores predeterminados de Deployment Workbench.  

 Los paquetes de controladores de dispositivo que no se puede extraer para aislar los archivos .inf o que no funcionan correctamente si no se instalan primero mediante un instalador de aplicaciones como un archivo MSI o Setup.exe pueden usar la característica de instalación de aplicaciones de MDT e instalar el controlador de dispositivo durante el proceso de implementación, como ocurre con cualquier aplicación normal.  

###  <a name="InstallOutofBoxDrivers"></a> Instalar controladores de dispositivo con el método de controladores predeterminados  
 Puede importar paquetes de controladores de dispositivo que incluyan un archivo .inf en Deployment Workbench e instalarlos automáticamente como parte del proceso de implementación. Para llevar a cabo este tipo de implementación de controladores de dispositivo, primero agregue el controlador de dispositivo a Deployment Workbench.  

 **Para agregar el controlador de dispositivo a Deployment Workbench**  

1.  Descargue los controladores de dispositivo necesarios para los tipos de hardware que se van a implementar y extraiga el paquete de controladores de dispositivo en una ubicación temporal.  

2.  Haga clic en **Inicio** y seleccione **All Programs** (Todos los programas). Seleccione **Microsoft Deployment Toolkit** y haga clic en **Deployment Workbench**.  

3.  En el árbol de consola de Deployment Workbench, vaya a Deployment Workbench/Deployment Shares (Recursos compartidos de implementación)/*deployment_share*/Out-of-Box Drivers (Controladores predeterminados), donde *deployment_share* es el nombre del recurso compartido de implementación que se va a configurar.  

4.  En el panel Acciones, haga clic en **Import Drivers** (Importar controladores).  

     Se inicia el Asistente para importar controlador de dispositivo.  

5.  En la página **Specify Directory** (Especifique un directorio), en la sección de directorio **Drive source** (Origen del controlador), haga clic en **Examinar** para ir a la carpeta que contiene los nuevos controladores de dispositivo y, después, haga clic en **Siguiente**.  

    > [!NOTE]
    >  El Asistente para nuevo controlador de dispositivo buscará en todos los subdirectorios del directorio de origen del controlador. Por lo tanto, si hay varios controladores para instalar, extráigalos en carpetas en el mismo directorio raíz y, luego, establezca el directorio de origen del controlador como el directorio raíz que contiene todas las carpetas de origen del controlador.  

6.  En la página **Resumen**, compruebe que la configuración sea correcta y haga clic en **Siguiente** para importar los controladores en Deployment Workbench.  

7.  En la página **Confirmación**, haga clic en **Finalizar**.  

 Si los controladores de dispositivo contienen controladores críticos para el arranque, como controladores de clase de red o almacenamiento masivo, el recurso compartido de implementación debe actualizarse después para generar un nuevo entorno de arranque LiteTouch_x86 y LiteTouch_x64 que contenga los nuevos controladores.  

 **Para agregar controladores de dispositivo a las imágenes de Windows PE de Lite Touch**  

1.  Haga clic en **Inicio** y seleccione **All Programs** (Todos los programas). Seleccione **Microsoft Deployment Toolkit** y haga clic en **Deployment Workbench**.  

2.  En el árbol de consola de Deployment Workbench, vaya a Deployment Workbench/Deployment Shares (Recursos compartidos de implementación)/*deployment_share*, donde *deployment_share* es el nombre del recurso compartido de implementación que se va a configurar.  

3.  En el panel Acciones, haga clic en **Update Deployment Share** (Actualizar recurso compartido de implementación).  

     Se inicia el Asistente para actualizar recurso compartido de implementación.  

4.  En la página **Opciones**, seleccione las opciones deseadas para actualizar el recurso compartido de implementación y haga clic en **Siguiente**.  

5.  En la página **Resumen**, compruebe que la información sea correcta y haga clic en **Siguiente**.  

6.  En la página **Confirmación**, haga clic en **Finalizar**.  

###  <a name="InstallDriversasApplications"></a> Instalar controladores de dispositivo como aplicaciones  
 Los controladores de dispositivo que están empaquetados como aplicaciones y que no se pueden extraer en una carpeta que contiene un archivo .inf, además de archivos de controlador, deben agregarse a Deployment Workbench como una aplicación para la instalación durante el proceso de implementación.  

 Las aplicaciones se pueden especificar como un paso de secuencia de tareas o bien se pueden especificar en CustomSettings.ini, pero las aplicaciones de controlador de dispositivo deben instalarse únicamente cuando la secuencia de tareas se ejecuta en un equipo con los dispositivos. Para asegurarse de esto, ejecute el paso de secuencia de tareas para implementar las aplicaciones de controlador de dispositivo correspondientes como un paso condicional de secuencia de tareas. Es posible especificar los criterios condicionales para ejecutar el paso de secuencia de tareas mediante consultas WMI para el dispositivo en el equipo de destino.  

#### <a name="add-the-device-driver-application-to-the-deployment-workbench"></a>Agregar la aplicación de controlador de dispositivo a Deployment Workbench  
 Cada aplicación de controlador de dispositivo debe importarse primero a Deployment Workbench.  

> [!NOTE]
>  Configure si la aplicación debe estar visible durante la implementación en el cuadro de diálogo **Propiedades** de cualquier aplicación. Para ello, active o desactive la casilla **Hide this application in the Deployment Wizard** (Ocultar esta aplicación en el Asistente para la implementación). Repita este proceso para cada aplicación de controlador de dispositivo que se use durante la implementación.  

 **Para agregar la aplicación de controlador de dispositivo a Deployment Workbench**  

1.  Descargue la aplicación de controlador de dispositivo y guárdela en una ubicación temporal.  

2.  Haga clic en **Inicio** y seleccione **All Programs** (Todos los programas). Seleccione **Microsoft Deployment Toolkit** y haga clic en **Deployment Workbench**.  

3.  En el árbol de consola de Deployment Workbench, vaya a Deployment Workbench/Deployment Shares (Recursos compartidos de implementación)/*deployment_share*/Aplicaciones, donde *deployment_share* es el nombre del recurso compartido de implementación que se va a configurar.  

4.  En el panel Acciones, haga clic en **Nueva aplicación**.  

     Se inicia el Asistente para nuevas aplicaciones.  

5.  En la página **Tipo de aplicación**, haga clic en **Application with source files** (Aplicación con archivos de código fuente) y en **Siguiente**.  

6.  En la página **Detalles**, escriba los detalles pertinentes sobre la aplicación y haga clic en **Siguiente**.  

7.  En la página **Origen**, en la sección **Directorio de origen**, haga clic en **Examinar** y seleccione el directorio que contiene los archivos de código fuente de la aplicación de controlador de dispositivo. Haga clic en **Aceptar**.  

8.  Haga clic en **Siguiente**.  

9. En la página **Destino**, escriba un nombre para el directorio de destino y haga clic en **Siguiente**.  

10. En la página **Detalles del comando**, en la sección **Línea de comandos**, escriba el comando que permite la instalación silenciosa de la aplicación de controlador de dispositivo.  

11. En la página **Resumen**, compruebe que la configuración sea correcta y haga clic en **Siguiente** para importar la aplicación de controlador de dispositivo en Deployment Workbench.  

12. En la página **Confirmación**, haga clic en **Finalizar**.  

 Una vez que se han importado las aplicaciones en Deployment Workbench, agréguelas al proceso de implementación mediante la lógica adecuada para asegurarse de que la aplicación se instala solo cuando se ejecute en el hardware correcto. Existen varios métodos para hacerlo:  

-   Especifique la aplicación de controlador de dispositivo como parte de una secuencia de tareas de implementación.  

-   Especifique la aplicación de controlador de dispositivo en CustomSettings.ini.  

-   Especifique la aplicación de controlador de dispositivo en la base de datos de MDT.  

 Estos métodos se describen de forma más detallada en las secciones siguientes.  

####  <a name="SpecifyDeviceAppTask"></a> Especificar la aplicación de controlador de dispositivo como parte de una secuencia de tareas  
 El primer método para agregar una aplicación de controlador de dispositivo al proceso de implementación consiste en usar una secuencia de tareas para agregar pasos para cada aplicación de controlador de dispositivo.  

 Hay dos maneras principales de administrar aplicaciones de controlador de dispositivo en la secuencia de tareas:  

-   Crear un grupo de secuencia de tareas para cada modelo de hardware y, después, agregar una consulta para ejecutar ese grupo de acciones si el equipo coincide con un tipo de hardware específico.  

-   Crear un grupo de secuencia de tareas para aplicaciones específicas de hardware y, después, agregar consultas para cada acción de secuencia de tareas de modo que cada paso de secuencia de tareas se evalúe en relación con el tipo de hardware y solo se ejecute si se encuentra una coincidencia.  

 **Para crear un grupo de secuencia de tareas para cada tipo de hardware**  

1.  Haga clic en **Inicio** y seleccione **All Programs** (Todos los programas). Seleccione **Microsoft Deployment Toolkit** y haga clic en **Deployment Workbench**.  

2.  En el árbol de consola de Deployment Workbench, vaya a Deployment Workbench/Deployment Shares (Recursos compartidos de implementación)/*deployment_share*/Secuencias de tareas, donde *deployment_share* es el nombre del recurso compartido de implementación que se va a configurar.  

3.  En el panel de detalles, haga clic en ***task_sequence***, donde *task_sequence* es la secuencia de tareas de implementación que tendrá que instalar la aplicación de controlador de dispositivo.  

4.  En el panel Acciones, haga clic en **Propiedades**.  

5.  En el cuadro de diálogo ***task_sequenceProperties***, en la pestaña **Secuencia de tareas**, en el panel de detalles, vaya a Restaurar estado/Windows Update (Pre-Application Installation) (Windows Update (instalación previa a la aplicación)).  

6.  En la pestaña **Secuencia de tareas**, haga clic en **Agregar** y en **Nuevo grupo**.  

     Esto crea un grupo de secuencia de tareas en la secuencia de tareas. Use este nuevo grupo de secuencia de tareas para crear los pasos necesarios para instalar las aplicaciones de controlador de dispositivo específicas del hardware.  

7.  En el panel de detalles, haga clic en **Nuevo grupo**.  

8.  En la pestaña **Propiedades**, en el cuadro **Nombre**, escriba ***group_name***, donde *group_name* es el nombre del grupo (por ejemplo, *Aplicaciones específicas de hardware: Dell Computer Corporation*).  

9. En la pestaña **Opciones**, haga clic en **Agregar** y en **Consultar WMI**.  

10. En el diálogo cuadro **Task Sequence WMI Condition** (Condición de WMI de secuencia de tareas, escriba la información siguiente:  

    -   En el cuadro **Espacio de nombres de WMI**, escriba **root\cimv2**.  

    -   En el cuadro **Consulta WQL**, escriba una consulta WQL (lenguaje de consulta de WMI) mediante la clase **Win32_ComputerSystem** para asegurarse de que la aplicación se instala solo para un tipo concreto de aplicación, por ejemplo:  

         **Select \* FROM Win32_ComputerSystem WHERE Model LIKE *%hardware_model%* AND Manufacturer LIKE *%hardware_manufacturer%***  

         En este ejemplo, *hardware_model* es el nombre del modelo del equipo (por ejemplo, Latitude D620) y *hardware_manufacturer* es el nombre de la marca del equipo (por ejemplo, Dell Corporation).  

         El símbolo **%** es un carácter comodín que se incluye en los nombres para permitir a los administradores devolver cualquier modelo o fabricante de equipo que contenga el valor especificado para ***hardware_model*** o ***hardware_manufacturer***.  

     Para más información sobre las consultas de WMI y WQL, vea la sección "Add WMI Queries to Task Sequence Step Conditions" (Agregar consultas de WMI a condiciones de paso de secuencia de tareas) en el documento de MDT *Using the Microsoft Deployment Toolkit* (Uso de Microsoft Deployment Toolkit) y vea [Querying with WQL](http://msdn.microsoft.com/library/aa392902.aspx) (Realizar consultas con WQL).  

11. Haga clic en **Aceptar** para enviar la consulta y clic en **Aceptar** para enviar los cambios a la secuencia de tareas.  

> [!NOTE]
>  Este proceso debe repetirse para el tipo de hardware de cada aplicación de controlador de dispositivo que vaya a instalarse.  

 Una vez que se han creado los grupos de secuencia de tareas específicos del hardware, se pueden agregar las aplicaciones de controlador de dispositivo a cada grupo.  

 **Para agregar aplicaciones de controlador de dispositivo a grupos de secuencia de tareas específicos del hardware**  

1.  Haga clic en **Inicio** y seleccione **All Programs** (Todos los programas). Seleccione **Microsoft Deployment Toolkit** y haga clic en **Deployment Workbench**.  

2.  En el árbol de consola de Deployment Workbench, vaya a Deployment Workbench/Deployment Shares (Recursos compartidos de implementación)/*deployment_share*/Secuencias de tareas, donde *deployment_share* es el nombre del recurso compartido de implementación que se va a configurar.  

3.  En el panel de detalles, haga clic en ***task_sequence***, donde *task_sequence* es la secuencia de tareas de implementación que tendrá que instalar la aplicación de controlador de dispositivo.  

4.  En el panel Acciones, haga clic en **Propiedades**.  

5.  En el cuadro de diálogo ***task_sequenceProperties***, haga clic en la pestaña **Secuencia de tareas**.  

6.  En el panel de detalles, vaya a Restaurar estado/*hardware_specific_group*, donde *hardware_specific_group* es el nombre del grupo específico del hardware donde se agregará el paso de secuencia de tareas para instalar la aplicación de controlador de dispositivo.  

7.  En la pestaña **Secuencia de tareas**, haga clic en **Agregar**, en **General** y en **Instalar aplicación**.  

     El paso de secuencia de tareas **Instalar aplicación** aparece en el panel de detalles.  

8.  En el panel de detalles, haga clic en **Instalar aplicación**.  

9. En la pestaña **Propiedades**, haga clic en **Install a single application** (Instalar una sola aplicación). En la lista **Application to install** (Aplicación que se va a instalar), seleccione ***hardware_application***, donde *hardware_application* es la aplicación para instalar la aplicación específica del hardware.  

> [!NOTE]
>  Este proceso debe repetirse para cada aplicación de controlador de dispositivo que se vaya a usar durante una implementación.  

#### <a name="specify-the-device-driver-application-in-customsettingsini"></a>Especificar la aplicación de controlador de dispositivo en CustomSettings.ini  
 Cuando se inicia una implementación de LTI o ZTI, una de las primeras acciones que se deben llevar a cabo es el procesamiento de los archivos de control BootStrap.ini y CustomSettings.ini. Ambos archivos contienen reglas que se pueden usar para personalizar dinámicamente la implementación.  

 Debido al modo en que MDT procesa el archivo CustomSettings.ini, puede usarlo para agregar aplicaciones basadas en condiciones específicas. Esta lógica se usará para agregar aplicaciones específicas de controladores de dispositivo durante la implementación en función de tipos de hardware concretos. En CustomSettings.ini se hace referencia a las aplicaciones mediante el GUID de la aplicación, ubicado en el archivo Applications.xml en el recurso compartido de implementación.  

 **Para buscar el GUID de una aplicación importada**  

1.  En el recurso compartido de implementación del servidor de implementación, abra la carpeta Control, por ejemplo, D:\Production Deployment Share\Control.  

2.  Busque y abra el archivo Applications.xml.  

3.  Busque aplicación requerida.  

4.  Para localizar el GUID de la aplicación, busque la línea incluida en las etiquetas `<guid>` de la aplicación, por ejemplo, `<application guid={c303fa6e-3a4d-425e-8102-77db9310e4d0}>`.  

 Como parte del proceso de inicialización, tanto el proceso LTI como el proceso ZTI recopila información sobre el equipo en el que se ejecuta. Durante este proceso, se realizan consultas de WMI y los valores de la clase **Win32_ComputerSystem** para la marca y el fabricante se rellenan como variables **%Make%** y **%Model%**, respectivamente.  

 Estos valores se pueden usar durante el procesamiento del archivo CustomSettings.ini para leer dinámicamente secciones del archivo en función de la marca y el modelo detectados.  A continuación se muestra un ejemplo del archivo CustomSettings.ini.  

 **Ejemplo de CustomSettings.ini configurado para una instalación de aplicación específica del hardware**  

```  
[Settings]  
Priority=Make, Default  
Properties=MyCustomProperty  

[Default]  
OSInstall=Y  

[Dell Computer Corporation]  
Subsection=Dell-%Model%  

[Dell-Latitude D620]  
MandatoryApplications001={1D7DF331-47B7-472C-87B3-442597EC2F7D}  

[Dell-Latitude D610]  
MandatoryApplications001={c303fa6e-3a4d-425e-8102-77db9310e4d0}  
```  

 Use las propiedades siguientes para especificar aplicaciones en CustomSettings.ini:  

-   **Applications**. Esta propiedad se puede usar si los administradores de implementaciones no quieren presentar un asistente para la aplicación como parte del proceso de implementación mediante la especificación de **SkipApplications=YES** en CustomSettings.ini.  

-   **MandatoryApplications**. Esta propiedad se puede usar si los administradores de implementaciones quieren presentar un asistente para la aplicación durante la implementación para permitir que los ingenieros de implementación seleccionen la instalación de otras aplicaciones durante la implementación.  

     Si se usa el asistente para la aplicación sin la propiedad **MandatoryApplications** (por ejemplo, **SkipApplications=NO**), se sobrescribirán las aplicaciones especificadas por la propiedad **Applications**.  

     En el ejemplo anterior se muestra cómo usar los valores de las variables **%Make%** y **%Model%** para manipular dinámicamente la manera en que se crea la lista de aplicaciones. Para encontrar los valores de la marca y el modelo de cada tipo de hardware, use uno de los métodos siguientes:  

-   **La herramienta Información del sistema**. Use el nodo Resumen del sistema de esta herramienta para identificar el **Fabricante del sistema** (marca) y el **Modelo del sistema** (modelo).  

-   **Windows PowerShell**. Use el cmdlet **Get-WMIObject –class Win32_ComputerSystem** para determinar la marca y el modelo del equipo.  

-   **Línea de comandos del Instrumental de administración de Windows**. Use **CSProduct Get Name, Vendor** para devolver el nombre (modelo) y el proveedor (marca) del equipo.  

 **Para modificar CustomSettings.ini a fin de agregar lógica específica del hardware**  

1.  Haga clic en **Inicio** y seleccione **All Programs** (Todos los programas). Seleccione **Microsoft Deployment Toolkit** y haga clic en **Deployment Workbench**.  

2.  En el árbol de consola de Deployment Workbench, vaya a Deployment Workbench/Deployment Shares (Recursos compartidos de implementación)/*deployment_share*, donde *deployment_share* es el nombre del recurso compartido de implementación que se va a configurar.  

3.  En el panel Acciones, haga clic en **Propiedades**.  

4.  Haga clic en la pestaña **Reglas**.  

5.  La información que se escribe en esta pestaña se almacena en el archivo CustomSettings.ini. Modifique las entradas del archivo CustomSettings.ini para agregar lógica para cada modelo de hardware que tenga una aplicación específica de controladores de dispositivo, como se describe en [Especificar la aplicación de controlador de dispositivo como parte de una secuencia de tareas](#SpecifyDeviceAppTask).  

6.  Haga clic en **Aceptar** para enviar los cambios.  

7.  En el panel de detalles, haga clic en *deployment_share*, donde *deployment_share* es el nombre del recurso compartido de implementación que se va a configurar.  

8.  En el panel Acciones, haga clic en **Update Deployment Share** (Actualizar recurso compartido de implementación).  

     Se inicia el Asistente para actualizar recurso compartido de implementación.  

9. En la página **Opciones**, seleccione las opciones deseadas para actualizar el recurso compartido de implementación y haga clic en **Siguiente**.  

10. En la página **Resumen**, compruebe que la información sea correcta y haga clic en **Siguiente**.  

11. En la página **Confirmación**, haga clic en **Finalizar**.  

 De forma predeterminada, todas las aplicaciones disponibles se muestran en el Asistente para la implementación de Windows durante la implementación de LTI. Dado que las aplicaciones específicas de controladores de dispositivo solo se aplican a tipos de hardware concretos, probablemente no le interese que se muestren siempre. Al especificar el paquete de aplicación específico del controlador de dispositivo en CustomSettings.ini, se puede ocultar la aplicación con la opción **Hide the application in the Deployment Wizard** (Ocultar la aplicación en el Asistente para la implementación) en la configuración de la aplicación.  

 **Para ocultar una aplicación en el Asistente para la implementación**  

1.  Haga clic en **Inicio** y seleccione **All Programs** (Todos los programas). Seleccione **Microsoft Deployment Toolkit** y haga clic en **Deployment Workbench**.  

2.  En el árbol de consola de Deployment Workbench, vaya a Deployment Workbench/Deployment Shares (Recursos compartidos de implementación)/*deployment_share*/Aplicaciones, donde *deployment_share* es el nombre del recurso compartido de implementación que se va a configurar.  

3.  En el panel de detalles, haga clic en ***device_driver_application***, donde *device_driver_application* es la aplicación que se va a ocultar en el Asistente para la implementación.  

4.  En el panel Acciones, haga clic en **Propiedades**.  

5.  En la pestaña **General**, active la casilla **Hide the application in the Deployment Wizard** (Ocultar la aplicación en el Asistente para la implementación).  

6.  Haga clic en **Aplicar** y cierre el cuadro de diálogo **Propiedades**.  

#### <a name="specify-the-device-driver-application-in-the-mdt-db"></a>Especificar la aplicación de controlador de dispositivo en la base de datos de MDT  
 La base de datos de MDT es una versión de base de datos del archivo CustomSettings.ini y se puede consultar en el momento de la implementación para obtener información que se usará durante la implementación. Para más información sobre el uso de la base de datos de MDT, vea "Selecting the Methods for Applying Configuration Settings" (Seleccionar métodos para aplicar valores de configuración).  

 Al consultar la base de datos de MDT durante la implementación, existen tres métodos para identificar el equipo de destino:  

-   Buscar el equipo individual (mediante la dirección MAC, la etiqueta de inventario o similar).  

-   Buscar la ubicación del equipo (mediante la puerta de enlace predeterminada).  

-   Buscar la marca y el modelo del equipo (mediante consultas WMI del fabricante o de la marca y el modelo).  

 Para cada entrada de base de datos que cree, puede especificar las propiedades de implementación, las aplicaciones, el uso de paquetes de Configuration Manager y los administradores. Al crear entradas de marca y modelo en la base de datos, puede agregar las aplicaciones de controlador de dispositivo específicas del hardware necesarias.  

 **Para crear entradas en la base de datos de MDT para permitir la instalación de aplicaciones de controlador de dispositivo**  

> [!NOTE]
>  Repita este proceso para cada marca y modelo de hardware que requiera una aplicación de controlador de dispositivo.  

1.  Haga clic en **Inicio** y seleccione **All Programs** (Todos los programas). Seleccione **Microsoft Deployment Toolkit** y haga clic en **Deployment Workbench**.  

2.  En el árbol de consola de Deployment Workbench, vaya a Deployment Workbench/Deployment Shares (Recursos compartidos de implementación)/**deployment_share**/Configuración avanzada/Base de datos/Make and Model (Marca y modelo), donde *deployment_share* es el nombre del recurso compartido de implementación que se va a configurar.  

3.  En el panel Acciones, haga clic en **Nuevo**.  

4.  En el cuadro de diálogo **Propiedades**, en la pestaña **Identidad**, en el cuadro **Marca**, escriba ***make_name***, donde *make_name*  es un nombre fácilmente identificable asociado al fabricante del equipo de destino.  

5.  En el cuadro **Modelo**, escriba ***model_name***, donde *model_name* es un nombre fácilmente identificable asociado al modelo del equipo de destino.  

6.  En la pestaña **Aplicaciones**, agregue cada una de las aplicaciones de controlador de dispositivo necesarias para ese modelo de hardware.  

## <a name="initiating-mdt-using-windows-deployment-services"></a>Iniciar MDT con Servicios de implementación de Windows  
 Windows Server 2008 usa Servicios de implementación de Windows como una versión actualizada y rediseñada de Servicios de instalación remota, la herramienta de implementación predeterminada de Windows Server 2003 con SP2. Con Servicios de implementación de Windows, puede implementar sistemas operativos Windows (especialmente Windows 7, Windows Server 2008 o sistemas operativos posteriores) en una red mediante medios de arranque o un adaptador de red habilitado para PXE del equipo.  

 Antes de implementar Servicios de implementación de Windows, determine cuál de las siguientes opciones de integración se adapta mejor a su entorno:  

-   Opción 1. Arrancar equipos en PXE para iniciar el proceso LTI.  

-   Opción 2. Implementar una imagen de sistema operativo desde el almacén de imágenes de Servicios de implementación de Windows.  

-   Opción 3. Usar la multidifusión con MDT y el rol de servidor de Servicios de implementación de Windows de Windows Server 2008.  

### <a name="option-1-boot-computers-in-pxe-to-initiate-the-lti-process"></a>Opción 1: arrancar equipos en PXE para iniciar el proceso LTI  
 Para reducir al mínimo el costo de administrar implementaciones de sistema operativo, inicie el proceso de implementación de MDT con Servicios de implementación de Windows y Protocolo de configuración dinámica de host. Esto elimina la necesidad de crear y proporcionar medios de arranque a cada equipo de destino.  

#### <a name="create-and-import-the-deployment-workbench-windows-pe-image-into-windows-deployment-services"></a>Crear e importar la imagen de Windows PE de Deployment Workbench en Servicios de implementación de Windows  
 Al crear un nuevo recurso compartido de implementación de MDT o al modificar un recurso compartido de implementación de MDT existente, puede crear una imagen de arranque de Windows PE personalizada. Cuando se actualiza el recurso compartido de implementación, la imagen de arranque de Windows PE se genera y se actualiza automáticamente con información sobre el recurso compartido de implementación, e inserta todos los controladores o componentes adicionales que se han especificado durante la configuración del recurso compartido de implementación.  

 La imagen de arranque de Windows PE se genera como un archivo de imagen ISO, que se puede escribir en un CD o un DVD, y como un archivo WIM de arranque. Puede importar el archivo WIM a Servicios de implementación de Windows para que los equipos que pueden arrancar en PXE puedan descargar y ejecutar la imagen de arranque de Windows PE de LTI en una red usada para inicializar una instalación.  

 **Para crear una imagen de arranque de Windows PE en Deployment Workbench**  

1.  Haga clic en **Inicio** y seleccione **All Programs** (Todos los programas). Seleccione **Microsoft Deployment Toolkit** y haga clic en **Deployment Workbench**.  

2.  En el árbol de consola de Deployment Workbench, vaya a Deployment Workbench/Deployment Shares (Recursos compartidos de implementación)/*deployment_share*, donde *deployment_share* es el nombre del recurso compartido de implementación que se va a configurar.  

3.  En el panel Acciones, haga clic en **Propiedades**.  

     En el cuadro de diálogo ***deployment_shareProperties***, haga clic en la pestaña **Windows PE *platform* Settings** (Configuración de plataforma Windows PE), donde plataforma es la arquitectura de la imagen de Windows PE que se va a configurar.  

4.  En el área **Lite Touch Boot Image Settings** (Configuración de la imagen de arranque de Lite Touch), active la casilla **Generate a Lite Touch bootable RAM disk ISO image** (Generar una imagen ISO de disco RAM de arranque de Lite Touch).  

5.  Haga clic en la pestaña **Windows PE *platform* Components** (Componentes de plataforma Windows PE), donde *plataforma* es la arquitectura de la imagen de Windows PE que se va a configurar.  

6.  En la sección **Driver Injection** (Inserción de controladores), haga clic en los tipos de controlador adecuados para su inclusión.  

    > [!NOTE]
    >  Este paso no es necesario si Windows PE ya incluye los controladores de dispositivo necesarios.  

7.  En la sección **Driver Injection** (Inserción de controladores), en la lista **Selection profile** (Perfil de selección), seleccione el perfil de selección de controladores adecuado.  

8.  En el cuadro de diálogo **Propiedades**, haga clic en **Aceptar**.  

    > [!NOTE]
    >  Este paso no es necesario si Windows PE ya incluye los controladores de dispositivo necesarios.  

9. En el panel de detalles, haga clic en ***deployment_share***, donde *deployment_share* es el nombre del recurso compartido de implementación que se va a configurar.  

10. En el panel Acciones, haga clic en **Update Deployment Share** (Actualizar recurso compartido de implementación).  

     Se inicia el Asistente para actualizar recurso compartido de implementación.  

11. En la página **Opciones**, seleccione las opciones deseadas para actualizar el recurso compartido de implementación y haga clic en **Siguiente**.  

12. En la página **Resumen**, compruebe que la información sea correcta y haga clic en **Siguiente**.  

13. En la página **Confirmación**, haga clic en **Finalizar**.  

     Una vez completado este proceso, la carpeta de arranque del recurso compartido de implementación contendrá una serie de imágenes de arranque, por ejemplo:  

     D:\Production Deployment Share\Boot\LiteTouchPE_x64.iso  

     D:\Production Deployment Share\Boot\LiteTouchPE_x64.wim  

     D:\Production Deployment Share\Boot\LiteTouchPE_x86.iso  

     D:\Production Deployment Share\Boot\LiteTouchPE_x86.wim  

 Puede escribir los archivos ISO que se han generado directamente en un CD o un DVD, o bien usarlos para inicializar el proceso LTI en un hardware nuevo. También puede importar los archivos WIM de arranque en Servicios de implementación de Windows para que los equipos nuevos puedan inicializar el proceso de implementación de LTI sin necesidad de medios físicos.  

 **Para importar la imagen de Windows PE en Servicios de implementación de Windows**  

1.  Inicie la consola de Servicios de implementación de Windows y conéctese a Servicios de implementación de Windows.  

2.  En el árbol de consola, haga clic con el botón derecho en **Imágenes de arranque** y haga clic en **Agregar imagen de arranque**.  

3.  Busque la imagen WIM que se va a importar, por ejemplo, D:\Production Deployment Share\Boot\LiteTouchPE_x86.wim.  

4.  El proceso de importación lee automáticamente los metadatos de la imagen de arranque, pero los valores de **Nombre de la imagen** y **Descripción de la imagen** también se pueden modificar. **Nombre de la imagen** afecta a la información de la opción de arranque que Administración de arranque de Windows muestra cuando el cliente arranca en PXE.  

5.  Cuando se ha importado la imagen de arranque, los equipos que arranquen en PXE y reciban una respuesta de Servicios de implementación de Windows podrán descargar la imagen de arranque de LTI e iniciar una instalación de LTI.  

 La instalación y la configuración de Servicios de implementación de Windows no se tratan en esta guía. Para más información sobre Servicios de implementación de Windows, vea [Windows Deployment Services Guide](http://technet.microsoft.com/library/cc265612.aspx) (Guía de Servicios de implementación de Windows).  

#### <a name="use-windows-deployment-services-to-automatically-detect-the-deployment-server"></a>Usar Servicios de implementación de Windows para detectar automáticamente el servidor de implementación  
 Hay disponible otra opción al usar Servicios de implementación de Windows para hospedar imágenes de arranque de MDT cuando el recurso compartido de implementación de MDT está hospedado en el mismo servidor que Servicios de implementación de Windows.  

 Cuando un cliente PXE carga la imagen de arranque de MDT, el nombre del servidor de Servicios de implementación de Windows que hospeda la imagen de arranque se captura y se coloca en **WDSServer** de MDTProperty. Después, puede hacer referencia a esta propiedad en el archivo BootStrap.ini de la imagen de arranque y en el archivo CustomSettings.ini del recurso compartido de implementación mediante la propiedad **DeployRoot**. Si lo hace, el cliente que arranque desde Servicios de implementación de Windows usará automáticamente el recurso compartido de implementación hospedado en el servidor de Servicios de implementación de Windows. Esto elimina la necesidad de especificar un nombre de servidor en un archivo de configuración.  

 **Para establecer el servidor de Servicios de implementación de Windows local como servidor de implementación**  

1.  Haga clic en **Inicio** y seleccione **All Programs** (Todos los programas). Seleccione **Microsoft Deployment Toolkit** y haga clic en **Deployment Workbench**.  

2.  En el árbol de consola de Deployment Workbench, vaya a Deployment Workbench/Deployment Shares (Recursos compartidos de implementación)/*deployment_share*/Configuración avanzada/Base de datos, donde *deployment_share* es el nombre del recurso compartido de implementación que se va a configurar.  

3.  En el panel Acciones, haga clic en **Propiedades**.  

4.  Haga clic en la pestaña **Reglas**.  

     La información que se escribe en esta pestaña se almacena en el archivo CustomSettings.ini.  

5.  Configure la propiedad **DeployRoot** de modo que use la variable **%WDSServer%**, por ejemplo, **DeployRoot=\\\\%WDSServer%\Deployment$**.  

6.  Haga clic en **Edit Bootstrap.ini** (Editar Bootstrap.ini).  

7.  Configure BootStrap.ini para que use la propiedad **%WDSServer%**. Para ello, agregue o cambie el valor de **DeployRoot** a **DeployRoot=\\\\%WDSServer%\Deployment$**.  

8.  En el menú **Archivo**, haga clic en **Guardar** para guardar los cambios en el archivo BootStrap.ini.  

9. Haga clic en **Aceptar**.  

     El recurso compartido de implementación debe actualizarse.  

10. En el panel de detalles, haga clic en **deployment_share**, donde *deployment_share* es el nombre del recurso compartido de implementación que se va a configurar.  

11. En el panel Acciones, haga clic en **Update Deployment Share** (Actualizar recurso compartido de implementación).  

     Se inicia el Asistente para actualizar recurso compartido de implementación.  

12. En la página **Opciones**, seleccione las opciones deseadas para actualizar el recurso compartido de implementación y haga clic en **Siguiente**.  

13. En la página **Resumen**, compruebe que la información sea correcta y haga clic en **Siguiente**.  

14. En la página **Confirmación**, haga clic en **Finalizar**.  

15. Importe la WIM de arranque actualizada en Servicios de implementación de Windows.  

### <a name="option-2-deploy-an-operating-system-image-from-the-windows-deployment-services-store"></a>Opción 2: implementar una imagen de sistema operativo desde el almacén de Servicios de implementación de Windows  
 Si ya usa Servicios de implementación de Windows para la implementación de sistema operativo, puede ampliar la funcionalidad de MDT. Para ello, configúrelo de modo que haga referencia a las imágenes de sistema operativo de Servicios de implementación de Windows que ya se usan, en lugar de emplear su propio almacén, y de modo que complemente las implementaciones de Servicios de implementación de Windows con la administración de controladores, la implementación de aplicaciones, la instalación de actualizaciones, el procesamiento de reglas y otras funcionalidades de MDT. Una vez que MDT haga referencia a una imagen de sistema operativo de Servicios de implementación de Windows, podrá tratarlo como un sistema operativo que se ha almacenado provisionalmente en un recurso compartido de implementación de MDT.  

 **Para hacer referencia a una imagen de sistema operativo de Servicios de implementación de Windows**  

> [!NOTE]
>  Los pasos siguientes requieren que al menos una imagen de sistema operativo se haya importado previamente en el servidor de Servicios de implementación de Windows.  

1.  Actualice MDT para que pueda tener acceso a imágenes de Servicios de implementación de Windows. Para ello, copie los archivos siguientes de la carpeta de orígenes de los medios de Windows en la carpeta C:\Archivos de programa\Microsoft Deployment Toolkit\bin en el servidor de Servicios de implementación de Windows:  

    -   Wdsclientapi.dll  

    -   Wdscsl.dll  

    -   Wdsimage.dll  

    -   Wdstptc.dll (solo si va a copiar desde los directorios de origen de Windows Server 2008)  

    > [!NOTE]
    >  El directorio de origen de Windows usado debe coincidir con la plataforma del sistema operativo que se ejecuta en el equipo donde está instalado MDT.  

2.  Haga clic en **Inicio** y seleccione **All Programs** (Todos los programas). Seleccione **Microsoft Deployment Toolkit** y haga clic en **Deployment Workbench**.  

3.  En el árbol de consola de Deployment Workbench, vaya a Deployment Workbench/Deployment Shares (Recursos compartidos de implementación)/*deployment_share*/Sistemas operativos, donde *deployment_share* es el nombre del recurso compartido de implementación que se va a configurar.  

4.  En el panel Acciones, haga clic en **Import Operating System** (Importar sistema operativo).  

     Se inicia el Asistente para nuevo sistema operativo.  

5.  En la página **Tipo de SO**, haga clic en **Windows Deployment Services images** (Imágenes de Servicios de implementación de Windows) y en **Siguiente**.  

6.  En la página **Servidor WDS**, escriba el nombre del servidor de Servicios de implementación de Windows al que se va a hacer referencia (por ejemplo, **WDSSvr001**) y haga clic en **Siguiente**.  

7.  En la página **Resumen**, compruebe que la configuración sea correcta y haga clic en **Siguiente**.  

8.  En la página **Confirmación**, haga clic en **Finalizar**.  

     Ahora todas las imágenes disponibles en el servidor de Servicios de implementación de Windows estarán disponibles para las secuencias de tareas de MDT.  

> [!NOTE]
>  La importación de imágenes de Servicios de implementación de Windows no copia los archivos de origen del servidor de Servicios de implementación de Windows en el recurso compartido de implementación. MDT sigue usando los archivos de origen desde su ubicación original.  

### <a name="option-3-use-multicasting-with-mdt-and-the-windows-server-2008-windows-deployment-services-role"></a>Opción 3: usar la multidifusión con MDT y el rol de Servicios de implementación de Windows de Windows Server 2008  
 Con la publicación de Windows Server 2008, se ha mejorado Servicios de implementación de Windows para admitir la implementación de imágenes mediante transmisiones por multidifusión. MDT también incluye actualizaciones para integrar MDT con la multidifusión de Servicios de implementación de Windows.  

 Además, la versión 1.1 actualizada del Kit de instalación automatizada de Windows (AIK de Windows) ahora incluye Wdsmcast.exe. Esto hace que sea posible unirse manualmente a sesiones de multidifusión y permite al cliente iniciar Wdsmcast.exe para copiar archivos desde una sesión de multidifusión activa.  

 El script LTIApply.wsf usa Wdsmcast.exe cuando tiene acceso a archivos de código fuente del sistema operativo desde el recurso compartido de implementación. LTIApply.wsf busca Wdsmcast.exe en el recurso compartido de implementación en las carpetas *deployment_share*\Tools\x86 o *deployment_share*\Tools\x64 (donde *deployment_share* es el nombre de la carpeta del sistema de archivos que contiene el recurso compartido de implementación), en función de la versión de Windows PE que se ejecute.  

 Cuando LTIApply.wsf se ejecuta, siempre intenta tener acceso a imágenes WIM y descargarlas desde una secuencia de multidifusión existente, pero recurre a una copia del archivo estándar si no existe una secuencia de multidifusión.  

> [!NOTE]
>  Este proceso se aplica solo a los archivos de imagen WIM.  

 A continuación se indican los requisitos previos para preparar el servidor de implementación para la multidifusión de MDT:  

-   El servidor de implementación debe ejecutar Windows Server 2008 o una versión posterior.  

-   Es necesario instalar el rol de Servicios de implementación de Windows desde la consola de administración de servidor.  

-   Es necesario instalar el AIK de Windows 1.1 para Windows Server 2008.  

-   Es necesario instalar MDT.  

-   Al igual que sucede con todas las implementaciones que usan MDT, debe haberse importado al menos una imagen WIM de sistema operativo, ya sea como un conjunto completo de archivos de origen o como una imagen personalizada con archivos de instalación.  

> [!NOTE]
>  Es importante usar la versión más reciente del AIK de Windows para la multidifusión; la copia de Windows PE incluida en versiones anteriores del AIK de Windows (por ejemplo, el AIK de Windows 1.0) no es compatible con la descarga desde un servidor de multidifusión.  

 **Para configurar MDT para la multidifusión desde un recurso compartido de implementación existente**  

1.  Haga clic en **Inicio** y seleccione **All Programs** (Todos los programas). Seleccione **Microsoft Deployment Toolkit** y haga clic en **Deployment Workbench**.  

2.  En el árbol de consola de Deployment Workbench, vaya a Deployment Workbench/Deployment Shares (Recursos compartidos de implementación)/*deployment_share*, donde *deployment_share* es el nombre del recurso compartido de implementación que se va a configurar.  

3.  En el panel Acciones, haga clic en **Propiedades**.  

4.  En la pestaña **General**, active la casilla **Enable multicast for this deployment share (requires Windows Server 2008 Windows Deployment Services)** (Habilitar la multidifusión para este recurso compartido de implementación (requiere Servicios de implementación de Windows de Windows Server 2008).  

5.  Haga clic en **Aceptar**.  

6.  En el panel Acciones, haga clic en **Update Deployment Share** (Actualizar recurso compartido de implementación).  

     Se inicia el Asistente para actualizar recurso compartido de implementación.  

7.  En la página **Opciones**, seleccione las opciones deseadas para actualizar el recurso compartido de implementación y haga clic en **Siguiente**.  

8.  En la página **Resumen**, compruebe que la información sea correcta y haga clic en **Siguiente**.  

9. En la página **Confirmación**, haga clic en **Finalizar**.  

 El recurso compartido de implementación ya está configurado para la transmisión por multidifusión de Servicios de implementación de Windows.  

 Este proceso crea una transmisión por multidifusión de Servicios de implementación de Windows de difusión automática que usa directamente el recurso compartido de implementación de MDT existente. MDT no crea transmisiones de difusión programada. Tenga en cuenta también que no se importan imágenes adicionales en Servicios de implementación de Windows y que no es posible usar la multidifusión para las imágenes de arranque, ya que el cliente de multidifusión no se puede cargar hasta después de que se ejecute Windows PE.  

 **Para comprobar que se ha generado la transmisión por multidifusión en Servicios de implementación de Windows**  

1.  Haga clic en **Inicio**, seleccione **Herramientas administrativas** y haga clic en **Servicios de implementación de Windows**.  

2.  En el árbol de consola de Servicios de implementación de Windows, haga clic con el botón derecho en **Servidores** y, después, haga clic en **Agregar servidor**.  

3.  En el cuadro de diálogo **Add Servers(s)** (Agregar servidores), haga clic en **Equipo local** y en **Aceptar**.  

4.  En el árbol de consola de Servicios de implementación de Windows, haga clic en **Servidores** y en ***server_name***, donde *server_name* es el nombre del equipo que ejecuta Servicios de implementación de Windows. Haga clic en **Transmisiones por multidifusión**.  

5.  En el panel de detalles, se mostrará una nueva transmisión de difusión automática para el recurso compartido de implementación, por ejemplo, **BDD Share Deployment$**.  

6.  Compruebe que el estado de la transmisión de difusión automática **BDD Share Deployment$** está establecido en **Activo**.  

 Una vez se ha implementado un equipo, compruebe que el sistema operativo se ha descargado desde una transmisión por multidifusión. Para ello, examine el archivo BDD.log de la carpeta \Windows\Temp\DeploymentLogs.  

 Habrá dos entradas en la carpeta de registros, que comienzan con **Multicast transfer** (Transferencia por multidifusión); compruébelas para asegurarse de que la transferencia se ha realizado correctamente. Para más información sobre las transmisiones por multidifusión con MDT y Servicios de implementación de Windows, vea la sección "Enable Windows Deployment Services Multicast Deployment for LTI Deployments" (Habilitar la implementación por multidifusión de Servicios de implementación de Windows para implementaciones de LTI) en el documento de MDT *Using the Microsoft Deployment Toolkit* (Uso de Microsoft Deployment Toolkit).  

## <a name="performing-staged-deployments-using-mdt-oem-preload"></a>Realizar implementaciones de ensayo con MDT (precarga de OEM)  
 En muchas organizaciones, los equipos se cargan con la imagen del sistema operativo antes de su implementación en la red de producción. En algunos casos, la carga de la imagen del sistema operativo la realiza un equipo de la organización responsable de generar los equipos en un entorno de ensayo. En otros casos, la carga de la imagen del sistema operativo la realiza el proveedor del hardware del equipo, también conocido como el *fabricante de equipo original* (OEM).  

> [!NOTE]
>  El proceso de precarga de OEM solo se admite en MDT para las implementaciones realizadas con LTI. Para Configuration Manager, use la característica de medios preconfigurados.  

### <a name="overview-of-the-oem-preload-process-in-mdt"></a>Información general sobre el proceso de precarga de OEM en MDT  
 El proceso de precarga de OEM se divide en tres fases:  

-   **Fase 1**. Cree una imagen basada en medios del equipo de referencia para aplicarla en el entorno de ensayo.  

-   **Fase 2**. Aplique la imagen del equipo de referencia en el equipo de destino en un entorno de ensayo.  

-   **Fase 3**. Complete la implementación del equipo de destino en el entorno de producción.  

 Las fases 1 y 3 suele llevarlas a cabo la organización de la implementación. Según el uso que se haga del proceso de precarga de OEM en la organización, la fase 2 puede realizarla la organización o el proveedor del hardware del equipo que suministra los equipos. Si la organización realiza la fase 2, el entorno de ensayo se encuentra dentro de la organización. Si un OEM realiza la fase 2, el entorno de ensayo se encuentra en el entorno del OEM.  

#### <a name="overview-of-mdt-configuration-files-in-the-oem-preload-process"></a>Información general sobre los archivos de configuración de MDT en el proceso de precarga de OEM  
 Las secuencias de tareas que se ejecutan durante las fases 1 y 3 del proceso de precarga de OEM usan archivos de configuración de MDT independientes (CustomSettings.ini y Bootstrap.ini). Aun así, ambos archivos de configuración existen simultáneamente en estructuras de carpeta diferentes.  

 En la primera fase, los archivos de configuración se usan durante la creación del equipo de referencia y se almacenan en la carpeta específica de la secuencia de tareas que se usa en esa fase. Los archivos de configuración que se usan en la tercera y última fase del proceso de precarga de OEM se almacenan en la carpeta específica de la secuencia de tareas que se usa en esa fase.  

 Cuando realice modificaciones en los archivos de configuración, asegúrese de que los cambios se corresponden con la secuencia de tareas adecuada de cada fase del proceso de precarga de OEM.  

#### <a name="overview-of-mdt-log-files-in-the-oem-preload-process"></a>Información general sobre los archivos de registro de MDT en el proceso de precarga de OEM  
 Se generan archivos de registro de MDT independientes durante las fases 1 y 3 del proceso de precarga de OEM:  

-   Los archivos de registro de MDT de la fase 1 se almacenan en las carpetas C:\MININT y C:\SMSTSLog.  

-   Los archivos de registro de MDT de la fase 3 se almacenan en la carpeta %WINDIR%\System32\CCM\Logs para implementaciones basadas en x86 o en la carpeta %WINDIR%\SysWow64\CCM\Logs para las implementaciones basadas en x64.  

 Use la carpeta adecuada al diagnosticar o solucionar problemas de implementación relacionados con MDT.  

### <a name="staged-deployments-using-lti"></a>Implementaciones de ensayo con LTI  
 Para las implementaciones de LTI, realice el proceso de precarga de OEM con un tipo de recurso compartido de implementación de *medios extraíbles (medios)*. No se admiten otros tipos de recurso compartido de implementación para el proceso de precarga de OEM.  

 Para llevar a cabo el proceso de precarga de OEM, cree una secuencia de tareas basada en la plantilla de secuencia de tareas de OEM de Litetouch, además de las secuencias de tareas que se usarán para implementar el sistema operativo de destino. Después, cree un recurso compartido de implementación de *medios extraíbles (medios)* que en última instancia creará un archivo ISO con el contenido del recurso compartido de implementación, específicamente el archivo LiteTouchPE_x86.iso o LiteTouchPE_x64.iso (según la plataforma de procesador del equipo de destino). El proceso de actualización del recurso compartido de implementación también crea una estructura de carpetas que se puede usar para crear medios con formato de disco universal.  

#### <a name="lti-oem-preload-processphase-1-create-a-media-based-image"></a>Proceso de precarga de OEM de LTI, fase 1: crear una imagen basada en medios  
 La organización de la implementación realiza la primera fase del proceso de precarga de OEM. La entrega final de esta fase es una imagen de arranque (por ejemplo, un archivo ISO) o un medio de arranque (por ejemplo, un DVD) que se envía al OEM o al entorno de ensayo dentro de la organización de la implementación. La mayoría de estos pasos se realiza en Deployment Workbench.  

 **Para crear una imagen basada en medios para la entrega al OEM o al entorno de ensayo dentro de la organización de la implementación**  

1.  Rellene los nodos siguientes para el recurso compartido de implementación en Deployment Workbench:  

    -   Sistemas operativos  

    -   Aplicaciones  

    -   Paquetes  

    -   Controladores predeterminados  

     Para más información sobre cómo realizar este paso, vea la sección "Managing Deployment Shares in the Deployment Workbench" (Administrar recursos compartidos de implementación en Deployment Workbench) en el documento de MDT *Using the Microsoft Deployment Toolkit* (Uso de Microsoft Deployment Toolkit).  

2.  Cree una secuencia de tareas basada en la plantilla de secuencia de tareas de OEM de Litetouch en Deployment Workbench.  

     Para más información sobre cómo realizar este paso, vea la sección "Configuring Task Sequences in the Deployment Workbench" (Configurar secuencias de tareas en Deployment Workbench) en el documento de MDT *Using the Microsoft Deployment Toolkit* (Uso de Microsoft Deployment Toolkit).  

3.  Cree una o varias secuencias de tareas que se usarán para implementar el sistema operativo de destino en el equipo de destino después de la implementación en el entorno de producción.  

     Para más información sobre cómo realizar este paso, vea la sección "Configuring Task Sequences in the Deployment Workbench" (Configurar secuencias de tareas en Deployment Workbench) en el documento de MDT *Using the Microsoft Deployment Toolkit* (Uso de Microsoft Deployment Toolkit).  

4.  Cree un perfil de selección que incluya las aplicaciones, los sistemas operativos, los controladores, los paquetes y las secuencias de tareas que se necesitan para la implementación de OEM.  

     Para más información sobre cómo realizar este paso, vea la sección "Manage Selection Profiles" (Administrar perfiles de selección) en el documento de MDT *Using the Microsoft Deployment Toolkit* (Uso de Microsoft Deployment Toolkit).  

5.  Cree los medios de implementación.  

     Para más información sobre cómo realizar este paso, vea la sección "Manage LTI Deployment Media" (Administrar los medios de implementación de LTI) en el documento de MDT *Using the Microsoft Deployment Toolkit* (Uso de Microsoft Deployment Toolkit).  

6.  Actualice el medio de implementación creado en Deployment Workbench en el paso anterior.  

     Al actualizar los medios de implementación, Deployment Workbench crea el archivo LiteTouchMedia.iso. Para más información sobre cómo realizar este paso, vea la sección "Manage LTI Deployment Media" (Administrar los medios de implementación de LTI) en el documento de MDT *Using the Microsoft Deployment Toolkit* (Uso de Microsoft Deployment Toolkit).  

7.  Grabe un DVD con el archivo LiteTouchMedia.iso creado en el paso anterior.  

    > [!NOTE]
    >  Si entrega el archivo ISO al entorno de ensayo del OEM o de la organización, este paso no es necesario.  

8.  Entregue el archivo ISO o el DVD al entorno de ensayo del OEM o de la organización.  

#### <a name="lti-oem-preload-processphase-2-apply-the-image-to-the-target-computer"></a>Proceso de precarga de OEM de LTI, fase 2: aplicar la imagen en el equipo de destino  
 La segunda fase del proceso de precarga de OEM la lleva a cabo el OEM o el equipo de implementación en el entorno de ensayo de la organización de la implementación. Durante esta fase del proceso, el archivo .iso o el DVD que se ha creado en la fase 1 se aplica en los equipos de destino. La entrega de esta fase es la imagen que se implementa en los equipos de destino para que estén listos para la implementación en el entorno de producción.  

 **Para aplicar la imagen en los equipos de destino**  

1.  Inicie un equipo de destino con los medios creados en la fase 1.  

     Se inicia Windows PE y, después, el Asistente para la implementación de Windows.  

2.  En el Asistente para la implementación de Windows, haga clic en **OEM Preinstallation Task Sequence for Staging Environment** (Secuencia de tareas de preinstalación de OEM para el entorno de ensayo).  

     La secuencia de tareas se iniciará y el contenido de los medios de arranque se copiará en el disco duro local del equipo de destino.  

3.  Cuando el Asistente para la implementación de Windows se haya completado para la **secuencia de tareas de preinstalación de OEM para el entorno de ensayo**, el disco duro estará listo para iniciar el resto del proceso de implementación mediante la ejecución del Asistente para la implementación de Windows para las demás secuencias de tareas que se usan para implementar el sistema operativo.  

     La **secuencia de tareas de preinstalación de OEM para el entorno de ensayo** se encarga de implementar la imagen en el equipo de destino e iniciar el proceso de LTI. El Asistente para la implementación de Windows se iniciará una segunda vez para ejecutar las secuencias de tareas que se usan para implementar el sistema operativo en el equipo de destino.  

4.  Clone el contenido del primer disco duro en tantos equipos de destino del entorno de ensayo como sea necesario.  

5.  Los equipos de destino se entregan al entorno de producción para la implementación.  

#### <a name="lti-oem-preload-processphase-3-complete-target-computer-deployment"></a>Proceso de precarga de OEM de LTI, fase 3: completar la implementación del equipo de destino  
 La tercera y última fase del proceso de precarga de OEM se realiza en el entorno de producción de la organización de la implementación. Durante esta fase del proceso se inician el equipo de destino y la imagen de medios de arranque, ubicada en el disco duro del entorno de ensayo durante la fase anterior.  

 **Para completar la implementación del equipo de destino en el entorno de producción**  

1.  Inicie el equipo de destino.  

     Se inicia Windows PE y, después, el Asistente para la implementación de Windows.  

2.  Complete el Asistente para la implementación de Windows con la información de configuración específica de cada equipo de destino.  

     Para más información sobre cómo completar este paso, vea la sección "Running the Deployment Wizard" (Ejecutar el Asistente para la implementación) en el documento de MDT *Using the Microsoft Deployment Toolkit* (Uso de Microsoft Deployment Toolkit).  

 Una vez completada esta fase, el equipo de destino estará listo para su uso en el entorno de producción.  

## <a name="using-windows-powershell-to-perform-common-tasks"></a>Usar Windows PowerShell para realizar tareas comunes  
 Las tareas de administración de MDT en Deployment Workbench las llevan a cabo cmdlets subyacentes de Windows PowerShell, que se pueden usar para automatizar tareas administrativas como las indicadas en las secciones siguientes.  

 Puede automatizar la administración de MDT mediante los pasos siguientes:  

-   Cree un recurso compartido de implementación como se describe en [Crear un recurso compartido de implementación](#CreateNewDeployShare).  

-   Cree una carpeta en un recurso compartido de implementación como se describe en [Crear una carpeta](#CreateFolder).  

-   Elimine una carpeta de un recurso compartido de implementación como se describe en [Eliminar una carpeta](#DeleteFolder).  

-   Importe un controlador de dispositivo en un recurso compartido de implementación como se describe en [Importar un controlador de dispositivo](#ImportDeviceDriver).  

-   Elimine un controlador de dispositivo de un recurso compartido de implementación como se describe en [Eliminar un controlador de dispositivo](#DeleteDeviceDriver).  

-   Importe un paquete de sistema operativo en un recurso compartido de implementación como se describe en [Importar un paquete de sistema operativo](#ImportOpSysPackage).  

-   Elimine un paquete de sistema operativo de un recurso compartido de implementación como se describe en [Eliminar un paquete de sistema operativo](#DeleteOpSysPackage).  

-   Importe un sistema operativo en un recurso compartido de implementación como se describe en [Importar un sistema operativo](#ImportOpSys).  

-   Elimine un sistema operativo de un recurso compartido de implementación como se describe en [Eliminar un sistema operativo](#DeleteOpSys).  

-   Cree una aplicación en un recurso compartido de implementación como se describe en [Crear una aplicación](#CreateApplication).  

-   Elimine una aplicación de un recurso compartido de implementación como se describe en [Eliminar una aplicación](#DeleteApplication).  

-   Cree una secuencia de tareas en un recurso compartido de implementación como se describe en [Crear una secuencia de tareas](#CreateTaskSequence).  

-   Elimine una secuencia de tareas de un recurso compartido de implementación como se describe en [Eliminar una secuencia de tareas](#DeleteTaskSequence).  

-   Cree una base de datos de MDT como se describe en [Crear una base de datos de MDT](#CreateMDTDB).  

-   Cree un perfil de selección como se describe en [Crear un perfil de selección](#CreateSelectProfile).  

-   Actualice un recurso compartido de implementación como se describe en [Actualizar un recurso compartido de implementación](#UpdatingDeployShare).  

-   Cree un recurso compartido de implementación vinculado como se describe en [Crear un recurso compartido de implementación vinculado](#CreateLinkedDeployShare).  

-   Actualice un recurso compartido de implementación vinculado como se describe en [Actualizar un recurso compartido de implementación vinculado](#UpdatingLinkedDeployShare).  

-   Elimine un recurso compartido de implementación vinculado como se describe en [Eliminar un recurso compartido de implementación vinculado](#DeleteLinkedDeployShare).  

-   Cree medios de implementación como se describe en [Crear medios](#CreateMedia).  

-   Genere medios de implementación como se describe en [Generar medios](#GenerateMedia).  

-   Elimine medios de implementación como se describe en [Eliminar medios](#DeleteMedia).  

###  <a name="CreateNewDeployShare"></a> Crear un recurso compartido de implementación  
 Los siguientes comandos de Windows PowerShell crean un recurso compartido de implementación en D:\Production Deployment Share denominado *Production$*. El nuevo recurso compartido de implementación se mostrará en Deployment Workbench como Producción.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider "MDTProvider" -Root "D:\Production Deployment Share" -Description "Production" -NetworkPath "\\Deployment_Server\Production$" -Verbose | add-MDTPersistentDrive -Verbose  
    ```  

###  <a name="CreateFolder"></a> Crear una carpeta  
 Los siguientes comandos de Windows PowerShell crean una carpeta de Adobe en el árbol de consola de Deployment Workbench en Deployment Workbench\/Deployment Shares\/Production\/Applications.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    New-item -path "DS002:\Applications" -enable "True" -Name "Adobe" -Comments "This folder contains Adobe software" -ItemType "folder" -Verbose remove-psdrive DS001 -Verbose  
    ```  

    > [!NOTE]
    >  Si agrega "`remove-psdrive`" al script se asegurará de que el proceso en segundo plano finalice antes de continuar.  

###  <a name="DeleteFolder"></a> Eliminar una carpeta  
 Los siguientes comandos de Windows PowerShell eliminan la carpeta Deployment Workbench\/Deployment Shares\/Production\/Applications\/Adobe.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    Remove-item -path "DS002:\Applications\Adobe" -Verbose  
    ```  

> [!NOTE]
>  El script generará un error si la carpeta no está vacía.  

###  <a name="ImportDeviceDriver"></a> Importar un controlador de dispositivo  
 Los siguientes comandos de Windows PowerShell importan el controlador de dispositivo de monitor de Dell 2407WFP en el recurso compartido de implementación de producción.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    Import-mdtdriver -path "DS002:\Out-of-Box Drivers\Monitor" -SourcePath "D:\Drivers\Dell\2407 WFP" -Verbose  
    ```  

###  <a name="DeleteDeviceDriver"></a> Eliminar un controlador de dispositivo  
 El siguiente comando de Windows PowerShell elimina el controlador de monitor de Dell 2407WFP del recurso compartido de implementación de producción.  

```  
Remove-item -path "DS002:\Out-of-Box Drivers\Dell Inc. Monitor 2407WFP.INF 1.0" -Verbose  
```  

###  <a name="ImportOpSysPackage"></a> Importar un paquete de sistema operativo  
 Los siguientes comandos de Windows PowerShell importan todos los paquetes de sistema operativo ubicados en D:\\Updates\\Microsoft\\Vista. Estos paquetes de sistema operativo se almacenarán en el recurso compartido de implementación de producción, que se encuentra en D:\\Production Deployment Share.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    Import-mdtpackage -path "DS002:\Packages" -SourcePath "D:\Updates\Microsoft\Vista" -Verbose  
    ```  

###  <a name="DeleteOpSysPackage"></a> Eliminar un paquete de sistema operativo  
 El siguiente comando de Windows PowerShell elimina el paquete de sistema operativo especificado del recurso compartido de implementación de producción.  

```  
Remove-item -path "DS002:\Packages\Package_1_for_KB940105 neutral x86 6.0.1.0 KB940105" -Verbose  
```  

###  <a name="ImportOpSys"></a> Importar un sistema operativo  
 Los siguientes comandos de Windows PowerShell importan el sistema operativo Windows Vista ubicado en D:\\Operating Systems\\Windows Vista x86. El sistema operativo se almacenará en el recurso compartido de implementación de producción, que se encuentra en D:\\Production Deployment Share.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    Import-mdtoperatingsystem -path "DS002:\Operating Systems" -SourcePath "D:\Operating Systems\Windows Vista x86" -DestinationFolder "Windows Vista x86" -Verbose  
    ```  

###  <a name="DeleteOpSys"></a> Eliminar un sistema operativo  
 El siguiente comando de Windows PowerShell elimina el sistema operativo HOMEBASIC de Windows Vista del recurso compartido de implementación de producción.  

```  
Remove-item -path "DS002:\Operating Systems\Windows Vista HOMEBASIC in Windows Vista x86 install.wim" -Verbose  
```  

###  <a name="CreateApplication"></a> Crear una aplicación  
 Los siguientes comandos de Windows PowerShell crean la aplicación Adobe Reader 9 mediante archivos de origen de D:\\Software\\Adobe\\Reader 9. La aplicación se almacenará en el recurso compartido de implementación de producción, que se encuentra en D:\\Production Deployment Share.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    Import-MDTApplication -path "DS002:\Applications" -enable "True" -Name "Adobe Reader 9" -ShortName "Reader" -Version "9" -Publisher "Adobe" -Language "" -CommandLine "setup.exe" -WorkingDirectory ".\Applications\Adobe Reader 9" -ApplicationSourcePath "D:\Software\Adobe\Reader 9" -DestinationFolder "Adobe Reader 9" -Source ".\Applications\Adobe Reader 9" -Verbose  
    ```  

###  <a name="DeleteApplication"></a> Eliminar una aplicación  
 El siguiente comando de Windows PowerShell elimina la aplicación Adobe Reader 9 del recurso compartido de implementación de producción.  

```  
Remove-item -path "DS002:\Applications\Adobe Reader 9" -Verbose  
```  

###  <a name="CreateTaskSequence"></a> Crear una secuencia de tareas  
 Los siguientes comandos de Windows PowerShell crean la secuencia de tareas **Windows Vista Production Build** (Compilación de producción de Windows Vista) en el recurso compartido de implementación de producción, que se encuentra en D:\\Production Deployment Share.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    Import-mdttasksequence -path "DS002:\Task Sequences" -Name "Windows Vista Business Production Build" -Template "Client.xml" -Comments "Approved for use in the production environment.  This task sequence uses the Standard Client task sequence template" -ID "Vista_Ref" -Version "1.0" -OperatingSystemPath "DS002:\Operating Systems\Windows Vista BUSINESS in Windows Vista x86 install.wim" -FullName "Fabrikam User" -OrgName "Fabrikam" -HomePage "http://www.Fabrikam.com" -AdminPassword "secure_password" -Verbose  
    ```  

###  <a name="DeleteTaskSequence"></a> Eliminar una secuencia de tareas  
 El siguiente comando de Windows PowerShell elimina la secuencia de tareas **Windows Vista Production Build** (Compilación de producción de Windows Vista) del recurso compartido de implementación de producción.  

```  
Remove-item -path "DS002:\Task Sequences\Windows Vista Business Production Build" -force -Verbose  
```  

###  <a name="CreateMDTDB"></a> Crear una base de datos de MDT  
 Los siguientes comandos de Windows PowerShell crean una base de datos de MDT en el servidor *deployment\_server* para el recurso compartido de implementación de producción. La conexión de base de datos se realizará a través de TCP\/IP.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    New-MDTDatabase -path "DS002:" -SQLServer "DeploymentServer" -Netlib "DBMSSOCN" -Database "MDT2010" -SQLShare "DB_Connect" -Force -Verbose  
    ```  

###  <a name="CreateSelectProfile"></a> Crear un perfil de selección  
 Los siguientes comandos de Windows PowerShell crean un perfil de selección de aplicaciones.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    New-item -path "DS002:\Selection Profiles" -enable "True" -Name "Applications" -Comments "" -Definition "<SelectionProfile><Include path="Applications" /></SelectionProfile>" -ReadOnly "False" -Verbose  
    ```  

###  <a name="UpdatingDeployShare"></a> Actualizar un recurso compartido de implementación  
 Los siguientes comandos de Windows PowerShell actualizan el recurso compartido de implementación de producción, que se encuentra en D:\\Production Deployment Share.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  
    
-   ```
    Update\-MDTDeploymentShare \-path "DS002:" \-Verbose  
    ```
    
###  <a name="CreateLinkedDeployShare"></a> Crear un recurso compartido de implementación vinculado  
 Los siguientes comandos de Windows PowerShell crean un recurso compartido de implementación que está vinculado al recurso compartido de implementación de producción y se encuentra en el recurso compartido \\\\*remote\_server\_name*\\Deployment$. El perfil de selección Everything se usa para determinar que contenido se replica en el recurso compartido de implementación vinculado. El contenido del recurso compartido de implementación de producción se combinará con el contenido que ya existe en el recurso compartido \\\\*remote\_server\_name*\\Deployment$.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    New-item -path "DS002:\Linked Deployment Shares" -enable "True" -Name "LINKED001" -Comments "" -Root "\\RemoteServerName\Deployment$" -SelectionProfile "Everything" -Replace "False" -Verbose  
    ```  

###  <a name="UpdatingLinkedDeployShare"></a> Actualizar un recurso compartido de implementación vinculado  
 Los siguientes comandos de Windows PowerShell actualizan el recurso compartido de implementación LINKED001.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    Replicate-MDTContent -path "DS002:\Linked Deployment Shares\LINKED001" -Verbose  
    ```  

###  <a name="DeleteLinkedDeployShare"></a> Eliminar un recurso compartido de implementación vinculado  
 Los siguientes comandos de Windows PowerShell eliminan el recurso compartido de implementación LINKED001.  

-   Add\-PSSnapIn Microsoft.BDD.PSSnapIn  

-   ```  
    Remove-item -path "DS002:\Linked Deployment Shares\LINKED001" -Verbose  
    ```  

###  <a name="CreateMedia"></a> Crear medios  
 Los siguientes comandos de Windows PowerShell crean una carpeta de origen que incluye el contenido usado para crear medios de arranque. El recurso compartido de implementación de producción se usará como origen. El perfil de selección Everything determina qué contenido se coloca en la carpeta de contenido de medios. Cuando se generen los medios, se creará el archivo LiteTouchMedia.iso. Los medios serán compatibles con las plataformas x86 y x64.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    New-item -path "DS002:\Media" -enable "True" -Name "MEDIA001" -Comments "some comment here" -Root "D:\Media" -SelectionProfile "Everything" -SupportX86 "True" -SupportX64 "True" -GenerateISO "True" -ISOName "LiteTouchMedia.iso" -Verbose  
    ```  

-   ```  
    New-PSDrive -Name "MEDIA001" -PSProvider "MDTProvider" -Root "D:\Media\Content" -Description "Embedded media deployment share" -Force -Verbose  
    ```  

###  <a name="GenerateMedia"></a> Generar medios  
 Los siguientes comandos de Windows PowerShell crean el archivo LiteTouchMedia.iso en D:\\Media, que usará el contenido de la carpeta de origen de medios MEDIA001.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    Generate-MDTMedia -path "DS002:\Media\MEDIA001" -Verbose  
    ```  

###  <a name="DeleteMedia"></a> Eliminar medios  
 El siguiente comando de Windows PowerShell elimina los medios MEDIA001 del recurso compartido de implementación de producción.  

```  
Remove-item -path "DS002:\Media\MEDIA001" -Verbos  
```  

## <a name="delaying-domain-join-to-avoid-application-of-group-policy-objects"></a>Retrasar la unión a un dominio para evitar la aplicación de objetos de directiva de grupo  
 Una directiva de grupo es una tecnología avanzada y flexible que permite administrar de forma eficaz un gran número de objetos usuario y equipo de Active Directory Domain Services (AD DS) mediante un modelo centralizado "uno a varios". La configuración de la directiva de grupo está contenida en un objeto de directiva de grupo (GPO) y está vinculada a uno o varios contenedores de servicio de AD DS, como sitios, dominios y unidades organizativas (UO).  

 Algunas organizaciones tienen una configuración de directiva de grupo restrictiva que podría causar problemas durante las implementaciones de sistema operativo. Por ejemplo, la siguiente configuración de directiva de grupo puede interrumpir un proceso de inicio de sesión automático:  

-   Restricciones de inicio de sesión automático  

-   Cambio en el nombre de la cuenta del administrador  

-   Títulos y los banners legales  

-   Directivas de seguridad restrictivas (por ejemplo, la directiva Seguridad especializada-Funcionalidad limitada, o SSLF)  

 Una opción para resolver los problemas que un GPO podría causar durante la implementación consiste en unir el equipo al dominio lo más tarde en el proceso de implementación. Esta unión puede llevarse a cabo mediante un paso de secuencia de tareas personalizado que ejecute el script ZTIDomainJoin.wsf.  

 Para unir el equipo de destino al dominio, el script ZTIDomainJoin.wsf usa las propiedades **DomainAdmin**, **DomainAdminDomain**, **DomainAdminPassword**, **JoinDomain** y **MachineObjectOU**. Puede declarar estas propiedades mediante el Asistente para la implementación de Windows, las reglas de recurso compartido de implementación, la base de datos de MDT y las reglas de recopilación y de equipo de Configuration Manager. La cuenta usada debe tener los derechos necesarios para crear y eliminar objetos de equipo en el dominio.  

 Normalmente, el script ZTIConfigure.wsf actualiza el archivo Unattend.xml o Unattend.txt con los valores especificados por estas propiedades. Después, el programa de instalación de Windows analiza esta configuración y el sistema intenta unirse al dominio al principio del proceso de implementación. Si lo hace, el equipo de destino se somete a la configuración especificada en los GPO de dominio y puede producirse un error en el proceso de implementación.  

 Para retrasar intencionadamente la acción de unir el equipo de destino al dominio durante el proceso de implementación, puede quitar algunos elementos del archivo Unattend.xml. El script ZTIConfigure.wsf omitirá la sobrescritura de propiedades en el archivo Unattend.xml si el elemento de propiedad asociado no se encuentra en el archivo.  

> [!NOTE]
>  Esta solución de ejemplo solo es válida cuando se implementan los sistemas operativos Windows 7, Windows Server 2008 o Windows Server 2008 R2.  

 **Preparar el archivo unattend.xml para que el equipo de destino no intente unirse al dominio durante la instalación de Windows**  

1.  Haga clic en **Inicio** y seleccione **All Programs** (Todos los programas). Seleccione **Microsoft Deployment Toolkit** y haga clic en **Deployment Workbench**.  

2.  En el árbol de consola de Deployment Workbench, vaya a Deployment Workbench/Deployment Shares (Recursos compartidos de implementación)/*deployment_share*/Secuencias de tareas/*task_sequence*, donde *deployment_share* es el nombre del recurso compartido de implementación y *task_sequence* es el nombre de la secuencia de tareas que se va a configurar.  

3.  En el panel Acciones, haga clic en **Propiedades**.  

4.  En la pestaña **OS Info** (Información de SO), haga clic en **Edit Unattend.xml** (Editar Unattend.xml).  

     Se inicia el Administrador de imágenes de sistema de Windows (Windows SIM).  

5.  En el panel **Archivo de respuesta**, vaya a **4 Especialización/Identificación/Credenciales**. Haga clic con el botón derecho en **Credenciales** y seleccione **Eliminar**.  

6.  Haga clic en **Sí**.  

7.  Guarde el archivo de respuesta y salga de Windows SIM.  

8.  Haga clic en **Aceptar** en el cuadro de diálogo **Propiedades** de la secuencia de tareas.  

 Como faltan los elementos `Credentials` en el archivo unattend.xml, el script ZTIConfigure.wsf no puede rellenar la información de unión al dominio en el archivo Unattend.xml, lo que impedirá que el programa de instalación de Windows intente unirse al dominio.  

 **Para agregar un paso de secuencia de tareas que una el equipo de destino al dominio**  

1.  Haga clic en **Inicio** y seleccione **All Programs** (Todos los programas). Seleccione **Microsoft Deployment Toolkit** y haga clic en **Deployment Workbench**.  

2.  En el árbol de consola de Deployment Workbench, vaya a Deployment Workbench/Deployment Shares (Recursos compartidos de implementación)/*deployment_share*/Secuencias de tareas/*task_sequence*, donde *deployment_share* es el nombre del recurso compartido de implementación y *task_sequence* es el nombre de la secuencia de tareas que se va a configurar.  

3.  En el panel Acciones, haga clic en **Propiedades**.  

4.  En la pestaña **Secuencia de tareas**, vaya al nodo Restaurar estado y expándalo.  

5.  Compruebe que esté presente el paso de secuencia de tareas **Recover From Domain** (Recuperar del dominio). En caso afirmativo, vaya al paso 9.  

6.  En el cuadro de diálogo **Propiedades** de la secuencia de tareas, haga clic en **Agregar**, vaya a **Configuración** y haga clic en **Recover From Domain** (Recuperar del dominio).  

7.  Agregue el paso de secuencia de tareas **Recover From Domain** (Recuperar del dominio) al Editor de secuencia de tareas. Compruebe que el paso se encuentra en la ubicación deseada en la secuencia de tareas.  

8.  Compruebe que la configuración del paso de secuencia de tareas **Recover From Domain** (Recuperar del dominio) se ajusta a sus necesidades.  

9. Haga clic en **Aceptar** en el cuadro de diálogo **Propiedades** de la secuencia de tareas para guardar la secuencia de tareas.
