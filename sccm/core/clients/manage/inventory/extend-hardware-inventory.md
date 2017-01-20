---
title: Ampliar el inventario de hardware | System Center Configuration Manager
description: "Obtenga información sobre cómo ampliar el inventario de hardware en System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: d5bfab4f-c55e-4545-877c-5c8db8bc1891
caps.latest.revision: 10
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: f777295958e9cbc729e3759d354521c96ae3e8ac
ms.openlocfilehash: 4a42e266c4152145a4a1c291804ff98934671692


---
# <a name="how-to-extend-hardware-inventory-in-system-center-configuration-manager"></a>Cómo ampliar el inventario de hardware en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

El inventario de hardware de System Center Configuration Manager lee información sobre los dispositivos desde PC Windows mediante Instrumental de administración de Windows (WMI). WMI es la implementación de Microsoft de Web-Based Enterprise Management (WBEM), un estándar de la industria para acceder a información de administración en un entorno empresarial. En versiones anteriores de Configuration Manager, puede ampliar el inventario de hardware. Para ello, modifique el archivo sms_def.mof del servidor de sitio. Este archivo contiene una lista de clases WMI que puede leer el inventario de hardware de Configuration Manager. Si edita este archivo, puede habilitar y deshabilitar clases existentes y también crear nuevas clases de inventario.  

 El archivo Configuration.mof se usa para definir las clases de datos que se deben inventariar mediante el inventario de hardware en el cliente y no se ha cambiado desde Configuration Manager 2012. Puede crear clases de datos para inventariar clases de datos de repositorios WMI existentes o personalizadas, o claves del Registro que estén en los sistemas cliente.  

 El archivo Configuration.mof también define y registra los proveedores WMI que tienen acceso a información del dispositivo durante el inventario de hardware. Registrar proveedores define el tipo de proveedor que se usará y las clases que admite el proveedor.  

 Cuando los clientes de Configuration Manager solicitan una directiva, por ejemplo, durante el intervalo de sondeo de directiva de cliente estándar, el archivo Configuration.mof se adjunta al cuerpo de la directiva. Este archivo, a continuación, se descarga y se compilan los clientes. Al agregar, modificar o eliminar clases de datos en el archivo Configuration.mof, los clientes compilación automáticamente estos cambios realizados en las clases de datos relacionadas con el inventario. No es necesario hacer nada más para inventariar clases de datos nuevas o modificadas en los clientes de Configuration Manager. Este archivo se encuentra en **<Ubicación de instalación de CM\>\Inboxes\clifiles.src\hinv\\** en los servidores del sitio principal.  

 En Configuration Manager, ya no es necesario editar el archivo sms_def.mof como en Configuration Manager 2007. En su lugar, puede habilitar y deshabilitar clases WMI y agregar nuevas clases que el inventario de hardware deba recopilar mediante la configuración del cliente. Configuration Manager proporciona los siguientes métodos para ampliar el inventario de hardware.  

> [!NOTE]  
>  Si ha cambiado manualmente el archivo Configuration.mof para agregar clases de inventario personalizadas, estos cambios se sobrescribirán cuando actualice a la versión 1602. Para seguir usando las clases personalizadas después de actualizar, debe agregarlas a la sección "Added extensions" del archivo Configuration.mof después de actualizar a 1602.  
> Pero no debe modificar todo lo anterior a esta sección, ya que estas secciones se reservan para que las modifique Configuration Manager. Encontrará una copia de seguridad del archivo Configuration.mof personalizado en:  
> **<Directorio de instalación de CM\>\data\hinvarchive\\**.  

|Método|Más información|  
|------------|----------------------|  
|Habilitar o deshabilitar las clases existentes de inventario|Puede habilitar o deshabilitar las clases de inventario predeterminadas que usa Configuration Manager o puede crear una configuración de cliente personalizada que le permita recopilar distintas clases de inventario de hardware de las recopilaciones de clientes especificadas. Para más información, consulte el procedimiento [Cómo habilitar o deshabilitar clases de inventario existentes](#BKMK_Enable) de este tema.|  
|Agregue una nueva clase de inventario|Puede agregar una nueva clase de inventario del espacio de nombres WMI de otro dispositivo. Para más información, consulte el procedimiento [Cómo agregar una clase de inventario nueva](#BKMK_Add) de este tema.|  
|Importar y exportar las clases de inventario de hardware|Puede importar y exportar archivos Managed Object Format (MOF) que contengan clases de inventario de la consola de Configuration Manager. Para más información, consulte los procedimientos [Cómo importar clases de inventario de hardware](#BKMK_Import) y [Cómo exportar clases de inventario de hardware](#BKMK_Export) de este tema.|  
|Crear archivos NOIDMIF|Use archivos NOIDMIF para recopilar información sobre los dispositivos cliente que Configuration Manager no puede inventariar. Por ejemplo, podría desea recopilar información número de dispositivos activos que sólo existe como una etiqueta en el dispositivo. Inventario NOIDMIF se asocia automáticamente con el dispositivo de cliente que se recopilaron de. Para obtener más información, consulte [Cómo crear archivos NOIDMIF](#BKMK_NOIDMIF) en este tema.|  
|Crear archivos IDMIF|Use archivos IDMIF para recopilar información sobre los activos de la organización que no están asociados con un cliente de Configuration Manager, por ejemplo, proyectores, fotocopiadoras e impresoras de red. Para obtener más información, consulte [Cómo crear archivos IDMIF](#BKMK_IDMIF) en este tema.|  

## <a name="procedures-to-extend-hardware-inventory"></a>Procedimientos para ampliar el inventario de hardware  
 Utilice los procedimientos siguientes para ampliar el inventario de hardware, como se describe en la tabla anterior.  

 Estos procedimientos le ayudan a configurar la configuración predeterminada para el inventario de hardware y se aplican a todos los clientes en la jerarquía. Si quiere que esta configuración solo se aplique a algunos clientes, cree una configuración de dispositivo cliente personalizada y asígnela a una recopilación que contenga los dispositivos que quiere inventariar. Para obtener más información acerca de cómo crear configuraciones de cliente personalizadas, consulte [How to configure client settings in System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md).  

###  <a name="a-namebkmkenablea-to-enable-or-disable-existing-inventory-classes"></a><a name="BKMK_Enable"></a> Cómo habilitar o deshabilitar clases de inventario existentes  

1.  En la consola de Configuration Manager, haga clic en **Administración**.  

2.  En el área de trabajo **Administración** , haga clic en **Configuración de cliente**.  

3.  Haga clic en **Configuración de cliente predeterminada**.  

4.  En la pestaña **Inicio** , en el grupo **Propiedades** , haga clic en **Propiedades**.  

5.  En el **configuración de cliente predeterminada** cuadro de diálogo, haga clic en **de inventario de Hardware**.  

6.  En el **configuración de dispositivo** lista, haga clic en **establecer clases**.  

7.  En el **clases de inventario de Hardware** diálogo cuadro, active o desactive las clases y propiedades de clase para recopilar el inventario de hardware. Puede expandir las clases para activar o desactivar las propiedades individuales dentro de esa clase. Utilice la **Buscar clases de inventario** campo para buscar clases individuales.  

    > [!IMPORTANT]  
    >  Cuando se agregan clases nuevas al inventario de hardware de Configuration Manager, aumentará el tamaño del archivo de inventario que se recopila y envía al servidor de sitio. Esto podría afectar negativamente al rendimiento de la red y el sitio de Configuration Manager. Habilitar sólo las clases de inventario que se van a recopilar.  

8.  Haga clic en **Aceptar** para guardar los cambios y cerrar la **clases de inventario de Hardware** cuadro de diálogo.  

###  <a name="a-namebkmkadda-to-add-a-new-inventory-class"></a><a name="BKMK_Add"></a> Cómo agregar una clase de inventario nueva  

1.  En la consola de Configuration Manager, haga clic en **Administración**.  

    > [!IMPORTANT]  
    >  Sólo puede agregar clases de inventario desde el servidor de nivel superior en la jerarquía y modificando la configuración predeterminada del cliente. Esta opción no está disponible al crear la configuración de dispositivo personalizado.  

2.  En el área de trabajo **Administración** , haga clic en **Configuración de cliente**.  

3.  Haga clic en **Configuración de cliente predeterminada**.  

4.  En la pestaña **Inicio** , en el grupo **Propiedades** , haga clic en **Propiedades**.  

5.  En el **configuración de cliente predeterminada** cuadro de diálogo, haga clic en **de inventario de Hardware**.  

6.  En el **configuración de dispositivo** lista, haga clic en **establecer clases**.  

7.  En el **clases de inventario de Hardware** cuadro de diálogo, haga clic en **Agregar**.  

8.  En el **Agregar clase de inventario de Hardware** cuadro de diálogo, haga clic en **Conectar**.  

9. En el **Conectar a Windows Management Instrumentation (WMI)** cuadro de diálogo, especifique el nombre del equipo desde el que se recuperarán las clases WMI y el espacio de nombres WMI para recuperar las clases. Si desea recuperar todas las clases debajo del espacio de nombres WMI que especificó, haga clic en **recursiva**. Si el equipo a que se conecta no es el equipo local, proporcione las credenciales de inicio de sesión de una cuenta que tenga permiso para obtener acceso a WMI en el equipo remoto.  

10. Haga clic en **Conectar**.  

11. En el cuadro de diálogo **Agregar clase de inventario de hardware**, en la lista **Clases de inventario**, seleccione las clases WMI que quiera agregar al inventario de hardware de Configuration Manager.  

12. Si desea modificar la información sobre la clase WMI seleccionada, haga clic en **Editar**, y en el **clase calificadores** diálogo cuadro, proporcione la siguiente información:  

    -   **Nombre para mostrar**: especifique un nombre descriptivo para la clase que se mostrará en el Explorador de recursos.  

    -   **Propiedades**: especifique las unidades en las que se mostrará cada una de las propiedades de la clase WMI.  

     También puede designar propiedades como una propiedad de clave para ayudar a identificar de forma única cada instancia de la clase. Si se ha definido ninguna clave para la clase y se informa de varias instancias de la clase de cliente, se almacena sólo la instancia más reciente que se encuentra en la base de datos.  

     Cuando haya terminado de configurar las propiedades, haga clic en **Aceptar** para cerrar la **clase calificadores** cuadro de diálogo.  

13. Haga clic en Aceptar para cerrar el **Agregar clase de inventario de Hardware** cuadro de diálogo.  

14. Haga clic en **Aceptar** para cerrar la **clases de inventario de Hardware** cuadro de diálogo.  

15. Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Configuración de cliente predeterminada** .  

###  <a name="a-namebkmkimporta-to-import-hardware-inventory-classes"></a><a name="BKMK_Import"></a> Cómo importar clases de inventario de hardware  

1.  En la consola de Configuration Manager, haga clic en **Administración**.  

2.  En el área de trabajo **Administración** , haga clic en **Configuración de cliente**.  

3.  Haga clic en **Configuración de cliente predeterminada**.  

    > [!IMPORTANT]  
    >  Sólo puede importar las clases de inventario cuando se modifica la configuración predeterminada del cliente. Sin embargo, puede utilizar la configuración de cliente personalizada para importar la información que no contenga un cambio de esquema, como cambiar la propiedad de una clase existente de **True** a **False**.  

4.  En la pestaña **Inicio** , en el grupo **Propiedades** , haga clic en **Propiedades**.  

5.  En el **configuración de cliente predeterminada** cuadro de diálogo, haga clic en **de inventario de Hardware**.  

6.  En el **configuración de dispositivo** lista, haga clic en **establecer clases**.  

7.  En el **clases de inventario de Hardware** cuadro de diálogo, haga clic en **importación**.  

8.  En el **importar** cuadro de diálogo, seleccione archivo Managed Object Format (MOF) que desee importar y, a continuación, haga clic en **Aceptar**.  

9. En el **Resumen de importación** diálogo cuadro, revise los elementos que se va a importar y, a continuación, haga clic en **importación**.  

###  <a name="a-namebkmkexporta-to-export-hardware-inventory-classes"></a><a name="BKMK_Export"></a> Cómo exportar clases de inventario de hardware  

1.  En la consola de Configuration Manager, haga clic en **Administración**.  

2.  En el área de trabajo **Administración** , haga clic en **Configuración de cliente**.  

3.  Haga clic en **Configuración de cliente predeterminada**.  

4.  En la pestaña **Inicio** , en el grupo **Propiedades** , haga clic en **Propiedades**.  

5.  En el **configuración de cliente predeterminada** cuadro de diálogo, haga clic en **de inventario de Hardware**.  

6.  En el **configuración de dispositivo** lista, haga clic en **establecer clases**.  

7.  En el **clases de inventario de Hardware** cuadro de diálogo, haga clic en **exportar**.  

    > [!NOTE]  
    >  Cuando se exportan las clases, se exportan todas las clases actualmente seleccionadas.  

8.  En el cuadro de diálogo **Exportar** , especifique el archivo MOF en el que quiere exportar las clases y luego haga clic en **Guardar**.  

## <a name="how-to-use-management-information-files-mif-files-to-extend-hardware-inventory"></a>Cómo usar archivos de información de administración (archivos MIF) para ampliar el inventario de hardware  
 Use archivos MIF para ampliar la información de inventario de hardware que Configuration Manager ha recopilado de los clientes. Durante el inventario de hardware, la información almacenada en los archivos MIF se agrega al informe de inventario de cliente y almacenada en la base de datos del sitio, donde puede usar los datos de la misma forma que utilice datos de inventario de cliente predeterminada. Hay dos tipos de archivos MIF, NOIDMIF e IDMIF. 

> [!IMPORTANT]  
>  Para poder agregar información de archivos MIF a la base de datos de Configuration Manager, primero debe crear o importar la información de clase para ellos. Para más información, consulte las secciones [Cómo agregar una clase de inventario nueva](#BKMK_Add) y [Cómo importar clases de inventario de hardware](#BKMK_Import) de este tema.  

###  <a name="a-namebkmknoidmifa-to-create-noidmif-files"></a><a name="BKMK_NOIDMIF"></a> Cómo crear archivos NOIDMIF  
 Los archivos NOIDMIF se pueden usar para agregar información a un inventario de hardware de cliente que normalmente Configuration Manager no puede recopilar y está asociado a un dispositivo de cliente concreto. Por ejemplo, muchas compañías etiquetar cada equipo de la organización con un número de activo y catalogar estos de forma manual. Cuando se crea un archivo NOIDMIF, esta información puede agregarse a la base de datos de Configuration Manager y se usa para consultas e informes. Para obtener información sobre la creación de archivos NOIDMIF, consulte la documentación del SDK de Configuration Manager.  

> [!IMPORTANT]  
>  Cuando se crea un archivo NOIDMIF, esto debe guardarse en un formato codificado de ANSI. Configuration Manager no puede leer los archivos NOIDMIF guardados en un formato con codificación UTF-8.  

 Después de crear un archivo NOIDMIF, lo almacena en la carpeta *% Windir %***\System32\CCM\Inventory\Noidmifs** carpeta en cada cliente. Configuration Manager recopila información de los archivos NODMIF en esta carpeta durante el siguiente ciclo de inventario de hardware programado.  

###  <a name="a-namebkmkidmifa-to-create-idmif-files"></a><a name="BKMK_IDMIF"></a> Cómo crear archivos IDMIF  
 Los archivos IDMIF se pueden usar para agregar información sobre activos a una base de datos de Configuration Manager que Configuration Manager no podría inventariar normalmente y no está asociada con ningún dispositivo de cliente concreto. Por ejemplo, podría usar IDMIFS para recopilar información sobre proyectores, reproductores de DVD, fotocopiadoras u otros equipos que no contengan un cliente de Configuration Manager. Para obtener información sobre la creación de archivos IDMIF, consulte la documentación del SDK de Configuration Manager.  

 Después de crear un archivo IDMIF, lo almacena en la carpeta *% Windir %***\System32\CCM\Inventory\Idmifs** carpeta en equipos cliente. Configuration Manager recopila información de este archivo durante el siguiente ciclo de inventario de hardware programado. Debe declarar clases nuevas para la información contenida en el archivo agregando o importarlos.  

> [!NOTE] 
> Los archivos MIF podrían contener grandes cantidades de datos y la recopilación de estos datos podría afectar negativamente al rendimiento del sitio. Habilite la recopilación de archivos MIF solo cuando sea necesario y configure la opción **Tamaño de archivo MIF personalizado máximo (KB)** en la configuración del inventario de hardware. Para obtener más información, consulte [Introduction to hardware inventory in System Center Configuration Manager](introduction-to-hardware-inventory.md) (Introducción al inventario de hardware en System Center Configuration Manager).



<!--HONumber=Nov16_HO1-->


