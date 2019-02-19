---
title: 'Creación de elementos de configuración para equipos Windows administrado por el cliente '
titleSuffix: Configuration Manager
description: Administre la configuración de equipos y servidores de Windows con un elemento de configuración de escritorios y servidores de Windows.
ms.date: 11/18/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 1eb2fcaf-acac-4388-9b31-6cccafacaabe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: ba02c1c3558cc7c0f7280e9517d7b67ee8e46eec
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56130384"
---
# <a name="how-to-create-custom-configuration-items-for-windows-desktop-and-server-computers-managed-with-the-system-center-configuration-manager-client"></a>Cómo crear elementos de configuración personalizados para equipos de escritorio y servidores de Windows administrados con el cliente de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*


Use el elemento de configuración de **escritorios y servidores de Windows personalizados** de System Center Configuration Manager para administrar la configuración de equipos y servidores de Windows administrados por el cliente de Configuration Manager.  

## <a name="start-the-create-configuration-item-wizard"></a>Iniciar el Asistente para crear elemento de configuración

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad** > **Configuración de cumplimiento** > **Elementos de configuración**.  

3.  En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear elemento de configuración**.  

4.  En la página **General** del **Asistente para crear elemento de configuración**, escriba un nombre y, opcionalmente, una descripción para el elemento de configuración.  

5.  En **Especifique el tipo de elemento de configuración que quiere crear**, seleccione **Windows Desktops and Servers (custom)**.  

    > [!TIP]  
    >  Si quiere proporcionar la configuración del método de detección que compruebe la existencia de una aplicación, seleccione **This configuration file contains application settings**.  

6.  Haga clic en **Categorías** si crea y asigna categorías para ayudarle a buscar y filtrar elementos de configuración en la consola de Configuration Manager.  

## <a name="provide-detection-method-information"></a>Proporcionar información de método de detección  
 Use este procedimiento para proporcionar información de método de detección para el elemento de configuración.  

> [!NOTE]  
>  Se aplica sólo si seleccionó **este elemento de configuración contiene la configuración de la aplicación** en el **General** página del asistente.  

 Un método de detección de Configuration Manager contiene reglas que se usan para detectar si una aplicación ya está instalada en un equipo. Esta detección se produce antes de que se evalúa el elemento de configuración para el cumplimiento de normas. Para detectar si una aplicación está instalada, puede detectar la presencia de un archivo de Windows Installer para la aplicación, utilice una secuencia de comandos personalizada o seleccione **suponer siempre se instala la aplicación** para evaluar el elemento de configuración para el cumplimiento, independientemente de si se instaló la aplicación.  

 Use estos procedimientos para configurar los métodos de detección en System Center Configuration Manager.  

### <a name="to-detect-an-application-installation-by-using-the-windows-installer-file"></a>Para detectar la instalación de una aplicación mediante el archivo de Windows Installer  

1.  En el **métodos de detección** página de la **Asistente para crear un elemento de configuración**, seleccione la **la detección del instalador de Windows Use** casilla de verificación.  

2.  Haga clic en **abiertos**, busque el archivo de Windows Installer (.msi) que desea detectar y, a continuación, haga clic en **abiertos**.  

3.  El **versión** cuadro se rellena automáticamente con el número de versión del archivo de Windows Installer que seleccionó. Puede escribir un nuevo número de versión en esta casilla si el valor mostrado es incorrecto.  

4.  Seleccione la casilla **Esta aplicación se instala para uno o más usuarios** si quiere detectar todos los perfiles de usuario del equipo.  

### <a name="to-detect-a-specific-application-and-deployment-type"></a>Para detectar una aplicación y un tipo de implementación específicos  

1.  En la página **Métodos de detección** del **Asistente para crear un elemento de configuración**, seleccione la casilla **Detectar una aplicación y un tipo de implementación específicos** y, a continuación, haga clic en **Seleccionar**.  

2.  En el cuadro de diálogo **Especificar aplicación** , seleccione la aplicación y un tipo de implementación asociada quiere detectar.  

### <a name="to-detect-an-application-installation-by-using-a-custom-script"></a>Para detectar la instalación de una aplicación mediante un script personalizado  

1.  En el **métodos de detección** página de la **Asistente para crear un elemento de configuración**, seleccione la **utilizar una secuencia de comandos personalizada para detectar esta aplicación** casilla de verificación.  

2.  En la lista, seleccione el idioma de la secuencia de comandos que desea abrir. Elija una de las secuencias de comandos siguientes:  

    -   **VBScript**  

    -   **JScript**  

    -   **PowerShell**  

3.  Haga clic en **Abrir**, vaya al script que quiere usar y, a continuación, haga clic en **Abrir**.  

##  <a name="configure-settings"></a>Configurar valores  
 Use este procedimiento para configurar las opciones del elemento de configuración.  

 Configuración representa el negocio o condiciones técnicas que se utilizan para evaluar el cumplimiento en dispositivos cliente. Puede configurar una nueva configuración o ir a una configuración existente en un equipo de referencia.  

1. En el **configuración** página de la **Asistente para crear un elemento de configuración**, haga clic en **nuevo**.  

2. En el **General** ficha de la **Crear configuración** diálogo cuadro, proporcione la siguiente información:  

   - **Nombre:** escriba un nombre único para la configuración. Puede utilizar un máximo de 256 caracteres.  

   - **Descripción:** especifique una descripción para la configuración. Puede utilizar un máximo de 256 caracteres.  

   - **Tipo de configuración:** en la lista, elija y configure uno de los siguientes tipos de configuración que se usará para esta configuración:  

     - **Consulta de Active Directory**  

        **Prefijo LDAP** : especifique un prefijo válido para que la consulta de los Servicios de dominio de Active Directory evalúe el cumplimiento en equipos cliente. Puede usar **LDAP: / /** para una o **GC: / /** para realizar una búsqueda de catálogo global.  

        **Nombre distintivo (DN)** -especifique el nombre distintivo del objeto de servicios de dominio de Active Directory que se evalúe la compatibilidad en los equipos cliente.  

        Por ejemplo, si quiere evaluar un valor relacionado con un usuario llamado John Smith en el dominio corp.contoso.com, escriba lo siguiente:  

       - **Filtro de búsqueda** : especifique un filtro LDAP opcional para refinar los resultados de la consulta de Servicios de dominio de Active Directory y evaluar el cumplimiento en equipos de cliente.  

          Para devolver todos los resultados de la consulta, escriba **(objectclass=\*)**.  

       - **Ámbito de búsqueda**: especifique el ámbito de búsqueda en Servicios de dominio de Active Directory. Puede elegir entre:  

         -   **Base** -consulta sólo el objeto especificado.  

         -   **Un nivel**: esta opción no se usa en esta versión de Configuration Manager.  

         -   **Subárbol** -consulta el objeto especificado y su subárbol completo en el directorio.  

       - **Propiedad** -especificar la propiedad del objeto de servicios de dominio de Active Directory que se utiliza para evaluar el cumplimiento en equipos cliente.  

          Por ejemplo, si desea consultar la propiedad de Active Directory **badPwdCount**, que almacena el número de veces que un usuario escribe mal una contraseña, escriba **badPwdCount** en este campo.  

       - **Consulta** -muestra la consulta construida a partir de las entradas de **prefijo LDAP**, **nombre distintivo (DN)**, **filtro de búsqueda** (si se especifica), y **propiedad**, que se utilizan para evaluar el cumplimiento en equipos cliente.  

         Para obtener más información sobre cómo crear consultas LDAP, consulte la documentación de Windows Server.  

     - **Ensamblaje**  

        Configure lo siguiente para este tipo de configuración:  

       - **Nombre de ensamblado:** especifica el nombre del objeto de ensamblado que se quiere buscar. El nombre no puede ser igual que otros objetos de ensamblado del mismo tipo y debe estar registrado en la caché Global de ensamblados. El nombre de ensamblado puede tener hasta 256 caracteres.  

         Un ensamblado es un fragmento de código que se puede compartir entre aplicaciones. Los ensamblados pueden tener la extensión de nombre de archivo .dll o .exe. La caché Global de ensamblados es una carpeta denominada *%systemroot%\Assembly* en el cliente se almacenan equipos donde todos los ensamblados compartidos.  

     - **Sistema de archivos**  

       - **Tipo** : en la lista, seleccione si quiere buscar un **Archivo** o una **Carpeta**.  

       - **Ruta** -especificar la ruta de acceso de la carpeta o archivo especificado en los equipos cliente. Puede especificar las variables de entorno del sistema y la variable de entorno *% USERPROFILE %* en la ruta.  

         > [!NOTE]  
         >  Si usa la variable de entorno *%USERPROFILE%* en los cuadros **Ruta** o **Nombre de archivo o carpeta** , se buscan en todos los perfiles de usuario del equipo cliente, lo que podría dar lugar a varias instancias del archivo o carpeta que se encuentra.  
         >   
         >  Si la configuración de cumplimiento no tiene acceso a la ruta especificada, se genera un error de detección. Además, si el archivo que está buscando está actualmente en uso, se genera un error de detección.  

       - **Nombre de archivo o carpeta** -especifique el nombre del objeto para buscar archivos o carpetas. Puede especificar las variables de entorno del sistema y la variable de entorno *% USERPROFILE %* en el nombre de archivo o de carpeta. También puede usar los caracteres comodín * y ? en el nombre de archivo.  

         > [!NOTE]  
         >  Si especifica un nombre de archivo o carpeta y usa caracteres comodín, esta combinación puede producir una gran cantidad de resultados y dar lugar a un uso intensivo de recursos en el equipo cliente, así como un tráfico de red elevado cuando se notifican los resultados a Configuration Manager.  

       - **Incluir subcarpetas** : habilite esta opción si desea buscar en las subcarpetas de la ruta especificada.  

       - **Este archivo o carpeta está asociada a una aplicación de 64 bits** : si está habilitado, sólo ubicaciones de archivos de 64 bits (como *% ProgramFiles %*) se comprobará en equipos de 64 bits. Si esta opción no está habilitada, se comprobarán las ubicaciones de 64 y 32 bits (como *ProgramFiles(x86)%*).  

         > [!NOTE]  
         >  Si el mismo archivo o carpeta existe en ubicaciones de archivo de sistema de 64 y 32 bits en el mismo equipo de 64 bits, la condición global detectará varios archivos.  

         El tipo de configuración **Sistema de archivos** no admite la especificación de una ruta UNC a un recurso compartido de red en el cuadro **Ruta** .  

     - **Metabase de IIS**  

       -   **Ruta de acceso de metabase** : especifique una ruta válida a la metabase de Internet Information Services (IIS).  

       -   **Id. de propiedad** : especifique la propiedad numérica de la configuración de la metabase de IIS.  

     - **Clave del Registro**  

       -   **Subárbol** : en la lista, seleccione el subárbol del Registro en el que quiere realizar la búsqueda.  

       -   **Clave** : especifique el nombre de la clave del Registro que desea buscar. Use el formato *clave\subclave*.  

       -   **Esta clave del registro está asociada con una aplicación de 64 bits** -especifica si se deben buscar las claves del registro de 64 bits además de las claves del registro de 32 bits en clientes que ejecutan una versión de 64 bits de Windows.  

           > [!NOTE]  
           >  Si la misma clave del Registro existe en las ubicaciones del Registro de 64 y 32 bits del mismo equipo de 64 bits, la condición global detecta ambas claves del Registro.  

     - **Valor del Registro**  

       - **Subárbol** : en la lista, seleccione el subárbol del Registro en el que quiere realizar la búsqueda.  

       - **Clave** : especifique el nombre de la clave del Registro que desea buscar. Use el formato *clave\subclave*.  

       - **Valor** : especifique el valor que debe estar incluido en la clave del Registro especificada.  

       - **Esta clave del Registro está asociada con una aplicación de 64 bits** : especifica si se deben buscar claves del Registro de 64 bits, además de claves del Registro de 32 bits, en clientes que ejecutan una versión de 64 bits de Windows.  

         > [!NOTE]  
         >  Si la misma clave del Registro existe en las ubicaciones del Registro de 64 y 32 bits del mismo equipo de 64 bits, la condición global detecta ambas claves del Registro.  

         También puede hacer clic en **Examinar** para ir a una ubicación del Registro en el equipo o en un equipo remoto. Para examinar un equipo remoto, debe tener derechos de administrador en el equipo remoto y el equipo remoto debe estar ejecutando el servicio Registro remoto.  

     - **Script**  

       -   **Script de detección** : haga clic en **Agregar** para especificar o buscar el script que se va a usar. Puede utilizar scripts de Windows PowerShell, VBScript o Microsoft JScript.  

       -   **Ejecutar scripts mediante las credenciales de usuario del usuario que inició sesión** : si habilita esta opción, el script se ejecuta en los equipos cliente que usan las credenciales del usuario que inició sesión.  

           > [!NOTE]  
           >  El valor que devuelve el script se usa para evaluar el cumplimiento de la condición global. Por ejemplo, si usa VBScript, se puede usar el comando **WScript.Echo Result** para devolver el valor de la variable *Result* a la condición global.  

     - **Consulta SQL**  

       -   **Instancia de SQL Server** : elija si desea que la consulta SQL se ejecute en la instancia predeterminada, en todas las instancias, o en un nombre de instancia de base de datos determinado.  

           > [!NOTE]  
           >  El nombre de instancia debe hacer referencia a una instancia local de SQL Server. Para hacer referencia a una instancia en clúster de SQL, debería utilizar una configuración de script.  

       -   **Base de datos** -especifique el nombre de la base de datos de Microsoft SQL Server en el que desea ejecutar la consulta SQL.  

       -   **Columna** -especifique el nombre de columna devuelto por la instrucción de Transact-SQL que se utiliza para evaluar el cumplimiento de la condición global.  

       -   **Instrucción Transact-SQL** : especifique la consulta SQL completa que se va a utilizar para la condición global. También puede hacer clic en **Abrir** para abrir una consulta SQL existente.  

           > [!IMPORTANT]  
           >  La configuración de consulta SQL no admite los comandos SQL que modifican la base de datos. Solo puede usar los comandos SQL que leen la información de la base de datos.  

     - **Consulta WQL**  

       -   **Espacio de nombres** -especifique el espacio de nombres del Instrumental de administración de Windows (WMI) que se utiliza para crear una consulta WQL que se evalúe la compatibilidad en los equipos cliente. El valor predeterminado es Root\cimv2.  

       -   **Clase** -especifica la clase WMI que se utiliza para crear una consulta WQL que se evalúe la compatibilidad en los equipos cliente.  

       -   **Propiedad** -especifica la propiedad WMI que se utiliza para crear una consulta WQL que se evalúe la compatibilidad en los equipos cliente.  

       -   **Cláusula WHERE de consulta WQL** : puede utilizar el elemento **Cláusula WHERE de consulta WQL** para especificar una cláusula WHERE que se aplicará a la propiedad, clase y espacio de nombres especificados en los equipos cliente.  

     - **Consulta XPath**  

       - **Ruta** : especifique la ruta al archivo .xml en los equipos cliente que se usa para evaluar el cumplimiento. Configuration Manager admite el uso de todas las variables de entorno de sistema de Windows y la variable de usuario *%USERPROFILE%* en el nombre de ruta de acceso.  

       - **Nombre de archivo XML** -especifique el nombre de archivo que contiene la consulta XML que se utiliza para evaluar el cumplimiento en equipos cliente.  

       - **Incluir subcarpetas** : habilite esta opción si desea buscar en las subcarpetas de la ruta especificada.  

       - **Este archivo está asociado con una aplicación de 64 bits**: elija si se debe buscar en la ubicación de archivo de sistema de 64 bits (*%windir%* \System32), además de en la ubicación de archivo de sistema de 32 bits (*%windir%* \Syswow64) en clientes de Configuration Manager que ejecutan una versión de 64 bits de Windows.  

       - **Consulta XPath** -especifique una completa XML path language (XPath) consulta válida que se usa para evaluar el cumplimiento en equipos cliente.  

       - **Espacios de nombres** : abre el cuadro de diálogo **Espacio de nombres XML** para identificar los prefijos y espacios de nombres que se deben usar durante la consulta XPath.  

         Si se intenta detectar un archivo .xml cifrado, la configuración de cumplimiento encuentra el archivo, pero la consulta XPath no produce ningún resultado y no se genera ningún error.  

         Si la consulta XPath no es válida, la configuración se evalúa como no conforme en los equipos cliente.  

   - **Tipo de datos:** en la lista, elija el formato en el que la condición devuelve los datos antes de que se usen para evaluar la configuración. El **tipo de datos** no se muestra la lista de todos los tipos de valor.  

     > [!NOTE]  
     >  El **punto flotante** tipo de datos admite sólo 3 dígitos después del separador decimal.  

3. Configurar detalles adicionales acerca de esta configuración en el **Establecer tipo** lista. Los elementos que pueden configurar varían según el tipo de configuración que ha seleccionado.  

   > [!NOTE]  
   >  Cuando se crea la configuración del tipo **sistema de archivos**, **clave del registro**, y **valor del registro**, puede hacer clic en **Examinar** para configurar el valor de los valores en un equipo de referencia. Para buscar una clave del registro o un valor en un equipo remoto, el equipo remoto debe tener habilitado el servicio de registro remoto.  

4. Haga clic en **Aceptar** para guardar la configuración y cerrar el cuadro de diálogo **Crear configuración** .  

##  <a name="configure-compliance-rules"></a>Configurar reglas de cumplimiento  
 Use el procedimiento siguiente para configurar reglas de cumplimiento para el elemento de configuración.  

 Las reglas de cumplimiento especifican las condiciones que definen la conformidad de un elemento de configuración. Para poder evaluar el cumplimiento de una configuración, debe tener al menos una regla de cumplimiento. WMI, el registro y la configuración de la secuencia de comandos le permite corregir valores que se encuentran como no conforme. Puede crear nuevas reglas o busque una configuración existente en cualquier elemento de configuración para seleccionar las reglas en ella.  

### <a name="to-create-a-compliance-rule"></a>Para crear una regla de cumplimiento  

1.  En el **reglas de conformidad** página de la **Asistente para crear un elemento de configuración**, haga clic en **nuevo**.  

2.  En el cuadro de diálogo **Crear regla** , proporcione la siguiente información:  

    -   **Nombre:** escriba un nombre para la regla de cumplimiento.  

    -   **Descripción:** escriba una descripción para la regla de cumplimiento.  

    -   **Configuración seleccionada:** haga clic en **Examinar** para abrir el cuadro de diálogo **Seleccionar configuración**. Seleccione la configuración que desea definir una regla de, o haga clic en **nueva configuración**. Cuando haya terminado, haga clic en **seleccione**.  

        > [!NOTE]  
        >  También puede hacer clic en **propiedades** para ver información acerca de la configuración seleccionada actualmente.  

    -   **Tipo de regla**: seleccione el tipo de regla de cumplimiento que quiere usar:  

        -   **Valor** crear una regla que compara el valor devuelto por el elemento de configuración con un valor que especifique.  

        -   **Existential** crear una regla que se evalúa como el ajuste en función de si existe en un dispositivo de cliente o en el número de veces que se encuentra.  

    -   Para un tipo de regla de **valor**, especifique la siguiente información:  

        -   **La configuración debe cumplir la siguiente regla** : seleccione un operador y un valor que se evalúe la compatibilidad con la configuración seleccionada. Puede utilizar los operadores siguientes:  

            |Operador|Más información|  
            |--------------|----------------------|  
            |Igual a|No hay información adicional|  
            |No es igual a|No hay información adicional|  
            |Mayor que|No hay información adicional|  
            |Menor que|No hay información adicional|  
            |Entre|No hay información adicional|  
            |Mayor o igual que|No hay información adicional|  
            |Menor o igual que|No hay información adicional|  
            |Uno de|En el cuadro de texto, especifique una entrada en cada línea.|  
            |Ninguno de|En el cuadro de texto, especifique una entrada en cada línea.|  

        -   **Corregir las reglas no compatibles cuando se admita** : seleccione esta opción si quiere que Configuration Manager corrija automáticamente las reglas no conformes. Configuration Manager puede corregir automáticamente los siguientes tipos de regla:  

            -   **Valor del registro** : el valor del registro se corrige si no es conforme y crea si no existe.  

            -   **Secuencia de comandos** (de ejecutar automáticamente un script de corrección).  

            -   **Consulta WQL**  

            > [!IMPORTANT]  
            >  Solo puede corregir reglas no conformes cuando el operador de regla se establece en **es igual a**.  

        -   **Incumplimiento de informes si no se encuentra la instancia de la configuración** : el elemento de configuración informa incumplimiento si esta configuración no se encuentra en los equipos cliente.  

        -   **Gravedad de la falta de cumplimiento de los informes:** especifique el nivel de gravedad que se indica (en los informes de Configuration Manager) si se produce un error en esta regla de cumplimiento. Los niveles de gravedad disponibles son los siguientes:  

            -   **Ninguno**: los equipos que no cumplan esta regla de cumplimiento no notifican una gravedad de error.  

            -   **Información**: los equipos que no cumplan esta regla de cumplimiento notifican una gravedad de error de **Información**.  

            -   **Advertencia**: los equipos que no cumplan esta regla de cumplimiento notifican una gravedad de error de **Advertencia**.  

            -   **Crítico**: los equipos que no cumplan esta regla de cumplimiento notifican una gravedad de error de **Crítico**.  

            -   **Crítico con evento**: los equipos que no cumplan esta regla de cumplimiento notifican una gravedad de error de **Crítico**. Este nivel de gravedad también se registra como evento de Windows en el registro de eventos de la aplicación.  

        -   Para un tipo de regla **Existencial**, especifique la siguiente información:  

            > [!NOTE]  
            >  Las opciones mostradas pueden variar según el tipo de configuración para la que configura una regla.  

            -   **La configuración debe existir en dispositivos cliente.**  

            -   **La configuración no debe existir en dispositivos cliente.**  

            -   **La configuración ocurre el siguiente número de veces:**  

        -   **Gravedad de la falta de cumplimiento de los informes:** especifique el nivel de gravedad que se indica (en los informes de Configuration Manager) si se produce un error en esta regla de cumplimiento. Los niveles de gravedad disponibles son los siguientes:  

            -   **Ninguno**: los equipos que no cumplan esta regla de cumplimiento no notifican una gravedad de error.  

            -   **Información**: los equipos que no cumplan esta regla de cumplimiento notifican una gravedad de error de **Información**.  

            -   **Advertencia**: los equipos que no cumplan esta regla de cumplimiento notifican una gravedad de error de **Advertencia**.  

            -   **Crítico**: los equipos que no cumplan esta regla de cumplimiento notifican una gravedad de error de **Crítico**.  

            -   **Crítico con evento**: los equipos que no cumplan esta regla de cumplimiento notifican una gravedad de error de **Crítico**. Este nivel de gravedad también se registra como evento de Windows en el registro de eventos de la aplicación.  

3.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Crear regla** .  

##  <a name="specify-supported-platforms"></a>Especificar plataformas admitidas  
 Las plataformas admitidas son los sistemas operativos en los que se evalúa el cumplimiento de un elemento de configuración.  

En la página **Plataformas admitidas** del **Asistente para crear elemento de configuración**, seleccione en la lista las versiones de Windows en las que quiere que se evalúe el cumplimiento del elemento de configuración o haga clic en **Seleccionar todo**.  

## <a name="complete-the-wizard"></a>Completar el asistente  
 En la página **Resumen** del asistente, revise las acciones que deberán realizarse y, a continuación, complete el asistente. El nuevo elemento de configuración se muestra en el **elementos de configuración** nodo en el **activos y compatibilidad** área de trabajo.  
