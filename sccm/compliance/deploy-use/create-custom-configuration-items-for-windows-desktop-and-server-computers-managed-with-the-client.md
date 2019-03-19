---
title: Crear elementos de configuración personalizados
titleSuffix: Configuration Manager
description: Administración de la configuración de equipos y servidores de Windows con un elemento de configuración predeterminado para escritorios y servidores de Windows
ms.date: 03/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 1eb2fcaf-acac-4388-9b31-6cccafacaabe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4253fdd94985a8a9adbc9e782f8397c2f76f5f2c
ms.sourcegitcommit: 4ab85212268e76d3fd22f00e6c74edaa5abde60c
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 03/05/2019
ms.locfileid: "57426896"
---
# <a name="create-custom-configuration-items-for-windows-desktop-and-server-computers-managed-with-the-configuration-manager-client"></a>Creación de elementos de configuración personalizados para equipos de escritorio y servidores de Windows administrados con el cliente de Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*


Use el elemento de configuración de **escritorios y servidores de Windows personalizados** de Configuration Manager para administrar la configuración de equipos y servidores de Windows administrados por el cliente de Configuration Manager.  



## <a name="start-the-wizard"></a>Iniciar el Asistente

1. En la consola de Configuration Manager, vaya al área de trabajo **Activos y compatibilidad**, expanda **Configuración de cumplimiento** y seleccione el nodo **Elementos de configuración**.  

2. En la pestaña **Inicio** de la cinta de opciones, en el grupo **Crear**, seleccione **Crear elemento de configuración**.  

3. En la página **General** del **Asistente para crear elemento de configuración**, escriba un nombre y, opcionalmente, una descripción para el elemento de configuración.  

4. En **Especifique el tipo de elemento de configuración que quiere crear**, seleccione **Windows Desktops and Servers (custom)**.  

    > [!TIP]  
    > Si quiere proporcionar la configuración del método de detección que compruebe la existencia de una aplicación, seleccione **This configuration file contains application settings**.  

5. Para ayudarle a buscar y filtrar elementos de configuración en la consola de Configuration Manager, seleccione **Categorías** para crear y asignar categorías.  



## <a name="detection-methods"></a>Métodos de detección  

Use este procedimiento para proporcionar información de método de detección para el elemento de configuración.  

> [!NOTE]  
> Esta información solo se aplica si selecciona **Este elemento de configuración contiene la configuración de la aplicación** en la página **General** del asistente.  

Un método de detección de Configuration Manager contiene reglas que se usan para detectar si una aplicación ya está instalada en un equipo. Esta detección se produce antes de que el cliente evalúa su compatibilidad para el elemento de configuración. Para detectar si una aplicación está instalada, puede detectar la presencia de un archivo de Windows Installer para la aplicación, utilice una secuencia de comandos personalizada o seleccione **suponer siempre se instala la aplicación** para evaluar el elemento de configuración para el cumplimiento, independientemente de si se instaló la aplicación.  


### <a name="to-detect-an-application-installation-by-using-the-windows-installer-file"></a>Para detectar la instalación de una aplicación mediante el archivo de Windows Installer  

1. En la página **Métodos de detección** del **Asistente para crear un elemento de configuración**, seleccione la opción **Usar la detección de Windows Installer**.  

2. Seleccione **Abrir**, busque el archivo de Windows Installer (.msi) que quiere detectar y, a continuación, seleccione en **Abrir**.  

3. El **versión** campo se rellena automáticamente con el número de versión del archivo de Windows Installer. Si el valor mostrado es incorrecto, escriba un nuevo número de versión aquí.  

4. Si quiere detectar todos los perfiles de usuario del equipo, seleccione **Esta aplicación se instala para uno o más usuarios**.  


### <a name="to-detect-a-specific-application-and-deployment-type"></a>Para detectar una aplicación y un tipo de implementación específicos  

1. En la página **Métodos de detección** del **Asistente para crear un elemento de configuración**, seleccione **Detectar una aplicación y un tipo de implementación específicos**. Elija **seleccione**.   

2. En el cuadro de diálogo **Especificar aplicación** , seleccione la aplicación y un tipo de implementación asociada quiere detectar.  


### <a name="to-detect-an-application-installation-by-using-a-custom-script"></a>Para detectar la instalación de una aplicación mediante un script personalizado  

1. En la página **Métodos de detección** del **Asistente para crear un elemento de configuración**, seleccione la opción **Usar un script personalizado para detectar la aplicación**.  

2. En la lista, seleccione el idioma de la secuencia de comandos. Elija uno de los formatos siguientes:  

    - **VBScript**  

    - **JScript**  

    - **PowerShell**  

        > [!Note]  
        > A partir de la versión 1810, cuando un script de Windows PowerShell se ejecuta como un método de detección, el cliente de Configuration Manager llama a PowerShell con la `-NoProfile` parámetro. Esta opción inicia PowerShell sin perfiles. Un perfil de PowerShell es un script que se ejecuta cuando se inicia PowerShell. <!--3607762-->  

3. Seleccione **Abrir**, vaya al script que quiere usar y, a continuación, seleccione **Abrir**.  



##  <a name="specify-supported-platforms"></a>Especificar plataformas admitidas  

En la página **Plataformas admitidas** del **Asistente para crear un elemento de configuración**, seleccione las versiones de Windows en las que quiere que se evalúe el cumplimiento del elemento de configuración o elija **Seleccionar todo**. 

También puede **especificar manualmente la versión de Windows**. Seleccione **agregar** y especifique el número de compilación de cada parte de la Windows. 



##  <a name="configure-settings"></a>Configurar valores  

Use este procedimiento para configurar las opciones del elemento de configuración.  

Configuración representa el negocio o condiciones técnicas que se utilizan para evaluar el cumplimiento en dispositivos cliente. Puede configurar una nueva configuración o ir a una configuración existente en un equipo de referencia.  

1. En la página **Configuración** del **Asistente para crear un elemento de configuración**, seleccione **Nuevo**.  

2. En el **General** ficha de la **Crear configuración** diálogo cuadro, proporcione la siguiente información:  

    - **Nombre:** escriba un nombre único para la configuración. Puede utilizar un máximo de 256 caracteres.  

    - **Descripción:** escriba una descripción para la configuración. Puede utilizar un máximo de 256 caracteres.  

    - **Tipo de configuración:** en la lista, elija y configure uno de los siguientes tipos de configuración que se utilizará para esta configuración:  
        - [Consulta de Active Directory](#bkmk_adquery)
        - [Ensamblaje](#bkmk_assembly)
        - [Sistema de archivos](#bkmk_file)
        - [Metabase de IIS](#bkmk_iis)
        - [Clave del Registro](#bkmk_regkey)
        - [Valor del Registro](#bkmk_regval)
        - [Script](#bkmk_script)
        - [Consulta SQL](#bkmk_sql)
        - [Consulta WQL](#bkmk_wql)
        - [Consulta XPath](#bkmk_xpath)

    - **Tipo de datos**: elija el formato en el que la condición devuelve los datos antes de que se usen para evaluar la configuración. La lista **Tipo de datos** no se muestra para todos los tipos de configuración.  

        > [!Tip]  
        > El tipo de datos **Punto flotante** admite solo tres dígitos después del separador decimal.  

3. Configurar detalles adicionales acerca de esta configuración en el **Establecer tipo** lista. Los elementos que se pueden configurar varían según el tipo de configuración seleccionada.  

4. Seleccione **Aceptar** para guardar la configuración y cerrar el cuadro de diálogo **Crear configuración**.  


### <a name="bkmk_adquery"></a> Consulta de Active Directory

- **Prefijo LDAP**: especifique un prefijo válido para que la consulta de los Servicios de dominio de Active Directory evalúe el cumplimiento en equipos cliente. Para realizar una búsqueda de catálogo global, use `LDAP://` o `GC://`.  

- **Nombre distintivo (DN)**: especifique el nombre distintivo del objeto de Active Directory Domain Services cuyo cumplimiento se evaluará en los equipos cliente.  

- **Filtro de búsqueda**: especifique un filtro LDAP opcional para refinar los resultados de la consulta de Active Directory Domain Services y evaluar el cumplimiento en equipos de cliente. Para devolver todos los resultados de la consulta, escriba `(objectclass=*)`.  

- **Ámbito de búsqueda**: especifique el ámbito de búsqueda en Active Directory Domain Services.  

    - **Base**: consulta solo el objeto especificado.  

    - **Un nivel**: esta opción no se usa en esta versión de Configuration Manager.  

    - **Subárbol**: consulta el objeto especificado y su subárbol completo en el directorio.  

- **Propiedad**: especifica la propiedad del objeto de Active Directory Domain Services que se usa para evaluar el cumplimiento en equipos cliente.  

    Por ejemplo, si quiere consultar la propiedad de Active Directory que almacena el número de veces que un usuario escribe mal una contraseña, escriba `badPwdCount` en este campo.  

- **Consulta**: muestra la consulta que se creó a partir de las entradas de **Prefijo LDAP**, **Nombre distintivo (DN)**, **Filtro de búsqueda**, si se especificó, y **Propiedad**.  


### <a name="bkmk_assembly"></a> Ensamblaje

Un ensamblado es un fragmento de código que se puede compartir entre aplicaciones. Los ensamblados pueden tener la extensión de nombre de archivo .dll o .exe. La caché global de ensamblados es la carpeta `%SystemRoot%\Assembly` en los equipos cliente. Esta caché es donde Windows almacena todos los ensamblados compartidos.  

- **Nombre de ensamblado:** Especifica el nombre del objeto de ensamblado que se desea buscar. El nombre no puede ser igual que otros objetos de ensamblado del mismo tipo. Registra por primera vez en la caché global de ensamblados. El nombre de ensamblado puede tener hasta 256 caracteres.  


### <a name="bkmk_file"></a> Sistema de archivos

- **Tipo**: en la lista, seleccione si quiere buscar un **archivo** o una **carpeta**.  

- **Ruta**: especifique la ruta de acceso de la carpeta o archivo especificado en los equipos cliente. Puede especificar las variables de entorno del sistema y la variable de entorno `%USERPROFILE%` en la ruta.  

    > [!NOTE]  
    > Si usas el `%USERPROFILE%` variable de entorno en el **ruta** o **nombre de archivo o carpeta** cuadros, el cliente de Configuration Manager busca en todos los perfiles de usuario en el equipo cliente. Este comportamiento podría ocasionar que buscar varias instancias del archivo o carpeta.  
    >   
    > Si la configuración de cumplimiento no tiene acceso a la ruta especificada, se genera un error de detección. Además, si el archivo que está buscando está actualmente en uso, se genera un error de detección.  

    > [!Tip]  
    > Seleccione **examinar** para configurar el valor de los valores en un equipo de referencia.   

- **Nombre de archivo o carpeta**: especifique el nombre del objeto para buscar archivos o carpetas. Puede especificar las variables de entorno del sistema y la variable de entorno `%USERPROFILE%` en el nombre de archivo o de carpeta. También puede utilizar los caracteres comodín `*` y `?` en el nombre de archivo.  

    > [!NOTE]  
    > Si especifica un nombre de archivo o carpeta y utiliza comodines, esta combinación podría producir una gran cantidad de resultados. Esto podría tener también como resultado un uso intensivo de los recursos del equipo cliente y un tráfico de red elevado cuando se notifiquen los resultados a Configuration Manager.  

- **Incluir subcarpetas**: buscar también en las subcarpetas de la ruta especificada.  

- **Este archivo o carpeta está asociada con una aplicación de 64 bits**: si está habilitada, sólo buscar ubicaciones de archivos de 64 bits como `%ProgramFiles%` en equipos de 64 bits. Si no está habilitada esta opción, busque las ubicaciones de 64 y 32 bits ubicaciones, como `%ProgramFiles(x86)%`.  

    > [!NOTE]  
    > Si el mismo archivo o carpeta existe en ubicaciones de archivo de sistema de 64 y 32 bits en el mismo equipo de 64 bits, la condición global detectará varios archivos.  

    El tipo de configuración **Sistema de archivos** no admite la especificación de una ruta de acceso UNC a un recurso compartido de red en el campo **Ruta de acceso**.  


### <a name="bkmk_iis"></a> Metabase de IIS

- **Ruta de acceso de metabase**: especifique una ruta válida a la metabase de Internet Information Services (IIS). Por ejemplo, `/LM/W3SVC/`.  

- **Id. de propiedad**: especifique la propiedad numérica de la configuración de la metabase de IIS.  


### <a name="bkmk_regkey"></a> Clave del Registro

- **Hive**: seleccione el subárbol del registro que desea buscar

    > [!Tip]  
    > Seleccione **examinar** para configurar el valor de los valores en un equipo de referencia. Para ir a una clave del registro en un equipo remoto, habilite la **registro remoto** servicio en el equipo remoto.  

- **Clave**: especifique el nombre de la clave del Registro que desea buscar. Use el formato `key\subkey`.  

- **Esta clave del Registro está asociada con una aplicación de 64 bits**: especifica si se deben buscar claves del Registro de 64 bits, además de claves del Registro de 32 bits, en clientes que ejecutan una versión de 64 bits de Windows.  

    > [!NOTE]  
    > Si la misma clave del Registro existe en las ubicaciones del Registro de 64 y 32 bits del mismo equipo de 64 bits, la condición global detecta ambas claves del Registro.  


### <a name="bkmk_regval"></a> Valor del Registro

- **Hive**: seleccione el subárbol del registro para buscar.  

    > [!Tip]  
    > Seleccione **examinar** para configurar el valor de los valores en un equipo de referencia. Para ir a un valor del registro en un equipo remoto, habilite la **registro remoto** servicio en el equipo remoto. También necesita permisos de administrador para obtener acceso al equipo remoto.  

- **Clave**: especifique el nombre de clave del registro que se buscará. Use el formato `key\subkey`.  

- **Valor**: especifique el valor que debe estar incluido en la clave del Registro especificada.  

- **Esta clave del Registro está asociada con una aplicación de 64 bits**: busca claves del Registro de 64 bits, además de claves del Registro de 32 bits, en clientes que ejecutan una versión de 64 bits de Windows.  

    > [!NOTE]  
    > Si la misma clave del Registro existe en las ubicaciones del Registro de 64 y 32 bits del mismo equipo de 64 bits, la condición global detecta ambas claves del Registro.  


### <a name="bkmk_script"></a> Script

El valor que devuelve el script se usa para evaluar el cumplimiento de la condición global. Por ejemplo, si usa VBScript, se puede usar el comando **WScript.Echo Result** para devolver el valor de la variable *Result* a la condición global.  

- **Script de detección**: seleccione **agregar Script**y escriba o busque una secuencia de comandos. Este script se utiliza para buscar el valor. Puede utilizar scripts de Windows PowerShell, VBScript o Microsoft JScript.  

- **Script de corrección (opcional)**: seleccione **agregar Script**y escriba o busque una secuencia de comandos. Este script se usa para corregir valores de configuración no compatibles. Puede utilizar scripts de Windows PowerShell, VBScript o Microsoft JScript.  

- **Ejecutar scripts mediante las credenciales de usuario del usuario que inició sesión**: si habilita esta opción, el script se ejecuta en los equipos cliente que utilizan las credenciales de los usuarios que han iniciado sesión.  

> [!Note]  
> A partir de la versión 1810, al usar Windows PowerShell como un script de detección o corrección, el cliente de Configuration Manager llama a PowerShell con la `-NoProfile` parámetro. Esta opción inicia PowerShell sin perfiles. Un perfil de PowerShell es un script que se ejecuta cuando se inicia PowerShell. <!--3607762-->  


### <a name="bkmk_sql"></a> Consulta SQL

- **Instancia de SQL Server**: elija si desea que la consulta SQL se ejecute en la instancia predeterminada, en todas las instancias, o en un nombre de instancia de base de datos determinado.  

    > [!NOTE]  
    > El nombre de instancia debe hacer referencia a una instancia local de SQL Server. Para hacer referencia a una instancia en clúster de SQL, debería utilizar una configuración de script.  

- **Base de datos**: especifique el nombre de la base de datos de Microsoft SQL Server en el que desea ejecutar la consulta SQL.  

- **Columna**: especifica el nombre de columna que devuelve la instrucción Transact-SQL que se usa para evaluar el cumplimiento de la condición global.  

- **Instrucción Transact-SQL**: especifique la consulta SQL completa que se va a utilizar para la condición global. Para usar una consulta SQL existente, seleccione **abierto**.  

    > [!IMPORTANT]  
    > La configuración de consulta SQL no admite los comandos SQL que modifican la base de datos. Solo puede usar los comandos SQL que leen la información de la base de datos.  


### <a name="bkmk_wql"></a> Consulta WQL

- **Namespace**: especifique el espacio de nombres WMI que se evalúe la compatibilidad en los equipos cliente. El valor predeterminado es `root\cimv2`.  

- **Clase**: especificar el destino de la clase WMI en el espacio de nombres anterior.  

- **Propiedad**: especificar la propiedad WMI de destino en la clase anterior.  

- **Cláusula WHERE de la consulta WQL**: especifique una cláusula de calificación para reducir los resultados. Por ejemplo, podría ser la cláusula WHERE para consultar solo el servicio DHCP en la clase Win32_Service, `Name = 'DHCP' and StartMode = 'Auto'`.   


### <a name="bkmk_xpath"></a> Consulta XPath

- **Ruta**: especifique la ruta al archivo .xml en los equipos cliente que se usa para evaluar el cumplimiento. Configuration Manager admite el uso de todas las variables de entorno de sistema de Windows y la variable de usuario `%USERPROFILE%` en el nombre de ruta de acceso.  

- **Nombre de archivo XML**: especifique el nombre de archivo que contiene la consulta XML en la ruta de acceso anterior.  

- **Incluir subcarpetas**: habilite esta opción si desea buscar en las subcarpetas de la ruta especificada.  

- **Este archivo está asociado con una aplicación de 64 bits**: buscar la ubicación del archivo del sistema de 64 bits `%Windir%\System32` además de la ubicación del archivo del sistema de 32 bits `%Windir%\Syswow64` en los clientes de Configuration Manager que ejecutan una versión de 64 bits de Windows.  

- **Consulta XPath**: especifique una consulta válida y completa XML path language (XPath).  

- **Los espacios de nombres**: identificar los espacios de nombres y prefijos que se usará durante la consulta XPath.  

Si se intenta detectar un archivo .xml cifrado, la configuración de cumplimiento encuentra el archivo, pero la consulta XPath no produce ningún resultado. El cliente de Configuration Manager no genera un error.  

Si la consulta XPath no es válida, la configuración se evalúa como no conforme en los equipos cliente.  



##  <a name="configure-compliance-rules"></a>Configurar reglas de cumplimiento  

Las reglas de cumplimiento especifican las condiciones que definen la conformidad de un elemento de configuración. Para poder evaluar el cumplimiento de una configuración, debe tener al menos una regla de cumplimiento. WMI, el registro y la configuración de la secuencia de comandos le permite corregir valores que se encuentran como no conforme. Puede crear nuevas reglas o busque una configuración existente en cualquier elemento de configuración para seleccionar las reglas en ella.  


### <a name="to-create-a-compliance-rule"></a>Para crear una regla de cumplimiento  

1. En la página **Reglas de cumplimiento** del **Asistente para crear un elemento de configuración**, seleccione **Nuevo**.  

2. En el cuadro de diálogo **Crear regla** , proporcione la siguiente información:  

    - **Nombre**: escriba un nombre para la regla de cumplimiento.  

    - **Descripción**: escriba una descripción para la regla de cumplimiento.  

    - **Configuración seleccionada**: haga clic en **Examinar** para abrir el cuadro de diálogo **Seleccionar configuración**. Seleccione la configuración para la que quiere definir una regla o haga clic en **Nueva configuración**. Cuando haya terminado, elija **seleccione**.  

        > [!Tip]  
        > Para ver información acerca de la configuración seleccionada actualmente, seleccione **propiedades**.  

    - **Tipo de regla**: Seleccione el tipo de regla de cumplimiento que desea usar:  

        - **Valor**: cree una regla que compare el valor devuelto por el elemento de configuración con un valor que especifique. Para obtener más información sobre la configuración adicional, consulte [valor reglas](#bkmk_value).  

        - **Existencial**: cree una regla que se evalúe la configuración en función de si existe en un dispositivo cliente o de las veces que se encuentra. Para obtener más información sobre la configuración adicional, consulte [reglas existenciales](#bkmk_exist).  

3. Seleccione **Aceptar** para cerrar el cuadro de diálogo **Crear regla**.  




### <a name="bkmk_value"></a> Reglas de valores  

- **Propiedad**: la propiedad del objeto que se va a comprobar varía en función de la configuración seleccionada. Las propiedades disponibles varían según el tipo de configuración. 

- **La configuración debe ser compatible con lo siguiente...** : Los permisos o reglas disponibles varían según el tipo de configuración.

- **Corregir las reglas no compatibles cuando se admita**: seleccione esta opción si quiere que Configuration Manager corrija automáticamente las reglas no conformes. Configuration Manager admite esta acción con los siguientes tipos de regla:  

    - **Valor del registro**: si no es conforme, el cliente establece el valor del registro. Si no existe, el cliente crea el valor.  

    - **Secuencia de comandos**: el cliente usa el script de corrección especificadas con la configuración.  

    - **Consulta WQL**  

    > [!IMPORTANT]  
    > Solo puede corregir reglas no conformes cuando el operador de regla se establece en **es igual a**.  

- **Notificar la no conformidad si no se encuentra la instancia de esta configuración**: si esta configuración no se encuentra en los equipos cliente, habilite esta opción para el elemento de configuración notificar la no conformidad.  

- **Gravedad de no compatibilidad para informes**: especifique el nivel de gravedad que se indica (en los informes de Configuration Manager) si se produce un error en esta regla de cumplimiento. Los niveles de gravedad siguientes están disponibles:  
    - **Ninguno**  
    - **Información**  
    - **Advertencia**  
    - **Crítica**  
    - **Crítico con evento**: los equipos que no cumplan esta regla de cumplimiento notifican una gravedad de error de **Crítico**. Este nivel de gravedad también se registra como evento de Windows en el registro de eventos de la aplicación.  


### <a name="bkmk_exist"></a> Existenciales reglas 

> [!NOTE]  
> Las opciones mostradas pueden variar según el tipo de configuración para la que configura una regla.  

- **La configuración debe existir en dispositivos cliente**  

- **La configuración no debe existir en dispositivos cliente.**  

- **La configuración ocurre el siguiente número de veces:**  

- **Gravedad de no compatibilidad para informes**: especifique el nivel de gravedad que se indica (en los informes de Configuration Manager) si se produce un error en esta regla de cumplimiento. Los niveles de gravedad siguientes están disponibles:  
    - **Ninguno**  
    - **Información**  
    - **Advertencia**  
    - **Crítica**  
    - **Crítico con evento**: los equipos que no cumplan esta regla de cumplimiento notifican una gravedad de error de **Crítico**. Este nivel de gravedad también se registra como evento de Windows en el registro de eventos de la aplicación.  



## <a name="next-steps"></a>Pasos siguientes

[Crear líneas base de configuración](/sccm/compliance/deploy-use/create-configuration-baselines)
