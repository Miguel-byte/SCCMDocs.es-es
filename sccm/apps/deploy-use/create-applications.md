---
title: Crear aplicaciones | System Center Configuration Manager
description: "Cree e implemente aplicaciones y tipos de implementación con System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cc230ff4-7056-4339-a0a6-6a44cdbb2857
caps.latest.revision: 14
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 7aca3f0a261a5506d68c57904c9b9f0d023c84e2


---
# <a name="create-applications-with-system-center-configuration-manager"></a>Crear aplicaciones con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Una aplicación de System Center Configuration Manager contiene los archivos y la información que se requieren para implementar software en un dispositivo. Una aplicación contiene uno o varios tipos de implementación que incluyen la información y los archivos de instalación necesarios para instalar el software. Además contienen reglas que especifican cuándo y cómo se implementa el software.  

 Puede crear aplicaciones mediante los métodos siguientes:  

-   Crear automáticamente los tipos de aplicación y de implementación mediante la lectura de los archivos de instalación de la aplicación.  

-   Crear manualmente la aplicación y, a continuación, agregar los tipos de implementación más adelante.  

-   Importe una aplicación desde un archivo.  

 Use los pasos siguientes para crear aplicaciones y tipos de implementación de Configuration Manager.  

## <a name="start-the-create-application-wizard"></a>Inicie el Asistente para crear aplicaciones  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software** > **Administración de aplicaciones** > **Aplicaciones**.  

3.  En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear aplicación**.  

## <a name="specify-whether-you-want-to-automatically-detect-application-information-or-manually-define-the-information"></a>especifique si desea detectar automáticamente la información de la aplicación o definir esta información de forma manual  

-   Elija**Detectar automáticamente la información de la aplicación** si quiere crear una aplicación simple que tenga un solo tipo de implementación, como un archivo de Windows Installer sin dependencias ni requisitos. Después de crear una aplicación mediante este procedimiento, puede editarla según sea necesario para agregar o modificar los tipos de implementación y agregar métodos de detección, dependencias o requisitos.  

-   Seleccione**Definir manualmente la información de la aplicación** para crear aplicaciones más complejas, que tengan varios tipos de implementación, dependencias, métodos de detección o requisitos.  

### <a name="automatically-detect-application-information"></a>Detectar automáticamente la información de la aplicación  

1.  En la página **General** del Asistente para crear aplicaciones, active la casilla **Detectar automáticamente la información sobre esta aplicación a partir de archivos de instalación** .  

2.  En la lista desplegable **Tipo** , seleccione el tipo de archivo de instalación de aplicación que desea utilizar para detectar información de la aplicación. Para obtener más información sobre los tipos de instalación disponibles, consulte [Tipos de implementación que admite Configuration Manager](/sccm/apps/deploy-use/create-applications#deployment-types-supported-by-configuration-manager) en este mismo tema.  
  
3.  En el campo **Ubicación**, especifique la ruta de acceso UNC con el formato *\\\\servidor\\recurso compartido\\\nombre de archivo* o el vínculo de la tienda del archivo de instalación de la aplicación que quiera usar para detectar la información de la aplicación. Como alternativa, haga clic en **Examinar** para buscar el archivo de instalación.  
    > [!IMPORTANT]  
    >  Si selecciona **Windows Installer (archivo \*.msi)** como tipo de aplicación, todos los archivos de la carpeta que especifique se importarán con la aplicación y se enviarán a los puntos de distribución. Asegúrese de que la carpeta que especifique solo contenga los archivos necesarios para instalar la aplicación. Configuration Manager se ha probado y admite hasta 20 000 archivos de aplicación en el paquete de la aplicación. Si la aplicación contiene más archivos, considere la posibilidad de crear varias aplicaciones con un menor número de archivos.  
    >  Debe poder acceder a la ruta de acceso UNC que contiene la aplicación y a todas las subcarpetas que tienen el contenido de la aplicación.  

4.  En la página **Importar información** del Asistente para crear aplicaciones, revise la información que se importó y, a continuación, haga clic en **Siguiente**. Si es necesario, puede hacer clic en **Anterior** para volver atrás y corregir los errores.  

5.  En la página **Información general** del Asistente para crear aplicaciones, especifique la siguiente información:  

    > [!NOTE]  
    >  Es posible que parte de esta información ya esté especificada si se obtuvo automáticamente de los archivos de instalación de la aplicación. Además, las opciones mostradas pueden ser diferentes según el tipo de aplicación que cree.  

    -   Proporcione información general sobre la aplicación, como el nombre de la aplicación, comentarios, la versión y una referencia opcional que le ayude a hacer referencia a la aplicación en la consola de Configuration Manager.  

    -   **Programa de instalación** : especifique el programa de instalación y las propiedades necesarias para instalar este tipo de implementación de aplicación.  

        > [!TIP]  
        >  Si el programa de instalación no se muestra, haga clic en **Examinar** y busque la ubicación del programa de instalación.  

    -   **Comportamiento de instalación** : especifique si quiere instalar el tipo de implementación de aplicación únicamente para el usuario que inició la sesión o para todos los usuarios. También puede especificar que el tipo de implementación se instale para todos los usuarios si se implementa en un dispositivo o solo para un usuario específico si se implementa en un usuario.  

    -   **Usar una conexión VPN automática (si se configuró)** : si se ha implementado un perfil de VPN en el dispositivo en el que se inicia la aplicación, la conexión VPN se inicia cuando lo hace la aplicación (solo en Windows 8.1 y Windows Phone 8.1).  

         En dispositivos de Windows Phone 8.1, las conexiones VPN automáticas no se admiten si se ha implementado más de un perfil de VPN.  
  
         Para obtener más información sobre los perfiles de VPN, consulte [Perfiles de VPN](../../protect/deploy-use/vpn-profiles.md).  
  
6.  Haga clic en **Siguiente**, revise la información de la aplicación en la página **Resumen** y, a continuación, complete el Asistente para crear aplicaciones.  

 La nueva aplicación se muestra en el nodo **Aplicaciones** de la consola de Configuration Manager. La creación de la aplicación ha finalizado. Si quiere agregar más tipos de implementación a la aplicación, consulte [Crear tipos de implementación de la aplicación](/sccm/apps/deploy-use/create-applications#create-deployment-types-for-the-application) en este mismo tema.  

### <a name="manually-specify-application-information"></a>Especificar manualmente la información de la aplicación  

1.  En la página **General** del Asistente para crear aplicaciones, seleccione **Especificar manualmente la información de la aplicación**y, a continuación, haga clic en **Siguiente**.  

2.  Especifique información general sobre la aplicación, como el nombre de la aplicación, comentarios, la versión y una referencia opcional que le ayude a encontrar la aplicación en la consola de Configuration Manager.  

3.  En la página **Catálogo de aplicaciones** del Asistente para crear aplicaciones, especifique la siguiente información:  

    -   **Idioma seleccionado** : en la lista desplegable, seleccione la versión de idioma de la aplicación que quiere configurar. Haga clic en **Agregar o quitar** para configurar más idiomas para esta aplicación.  

    -   **Nombre localizado de la aplicación** : especifique el nombre de la aplicación en el idioma que seleccionó en la lista desplegable **Idioma seleccionado** .  

        > [!IMPORTANT]  
        >  Debe especificar un nombre de aplicación localizado para cada versión de idioma que configure.  

    -   **Categorías de usuario** : haga clic en **Editar** para especificar categorías de la aplicación en el idioma que seleccionó en la lista desplegable **Idioma seleccionado** . Los usuarios del Centro se software pueden utilizar estas categorías seleccionadas como ayuda para filtrar y ordenar las aplicaciones disponibles.  

    -   **Documentación de usuario** : haga clic en **Examinar** para especificar la dirección URL, o el nombre de archivo y la ruta de acceso UNC, de un archivo que los usuarios del Centro de software puedan leer para obtener más información sobre la aplicación.  

    -   **Texto del vínculo** : especifique el texto que aparecerá en lugar de la dirección URL de la aplicación.  

    -   **Dirección URL de privacidad de la aplicación** : especifique una dirección URL vinculada a la declaración de privacidad de la aplicación.  

    -   **Descripción localizada** : especifique una descripción para esta aplicación en el idioma que seleccionó en la lista desplegable **Idioma seleccionado** .  

    -   **Palabras clave** : especifique una lista de palabras clave en el idioma que seleccionó en la lista desplegable **Idioma seleccionado** . Estas palabras clave ayudarán a los usuarios del Centro de software a encontrar la aplicación.  

    -   **Icono** : haga clic en **Examinar** para seleccionar un icono para esta aplicación entre los que están disponibles. Si no especifica un icono, se utilizará un icono predeterminado para esta aplicación.  

    -   **Mostrar esta aplicación como destacada y resaltarla en el portal de empresa** : seleccione esta opción para que la aplicación se muestre de forma destacada en el portal de empresa.  

4.  En la página **Tipos de implementación** del Asistente para crear aplicaciones, haga clic en **Agregar** para crear un tipo de implementación nuevo.  
Para obtener más información, consulte [Crear tipos de implementación de la aplicación](/sccm/apps/deploy-use/create-applications#create-deployment-types-for-the-application) en este mismo tema.  

5.  Haga clic en **Siguiente**, revise la información de la aplicación en la página **Resumen** y, a continuación, complete el Asistente para crear aplicaciones.  

 La nueva aplicación aparece en el nodo **Aplicaciones** de la consola de Configuration Manager.  

##  <a name="create-deployment-types-for-the-application"></a>Crear tipos de implementación de la aplicación  
 Si activa la casilla **Identificar automáticamente la información sobre este tipo de implementación a partir de los archivos de instalación** en la página **General** del Asistente para crear tipos de implementación, puede que no precise completar algunos de los pasos que se describen en los procedimientos siguientes.  

## <a name="start-the-create-deployment-type-wizard"></a>Iniciar el Asistente para crear tipos de implementación  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software** > **Administración de aplicaciones** > **Aplicaciones**.  

3.  Seleccione una aplicación y después, en la pestaña **Inicio** , en el grupo **Aplicación** , haga clic en **Crear tipo de implementación**.  

> [!TIP]  
>  También puede iniciar el Asistente para crear tipos de implementación desde el Asistente para crear aplicaciones y desde la pestaña **Tipos de implementación** del cuadro de diálogo **Propiedades de** *<nombre de la aplicación>\>*.  

## <a name="specify-whether-you-want-to-automatically-detect-deployment-type-information-or-manually-configure-the-information"></a>Especificar si quiere detectar automáticamente la información de tipo de implementación o definirla manualmente  
 Utilice uno de los procedimientos siguientes para detectar automáticamente o configurar manualmente la información de tipo de implementación.  

### <a name="automatically-detect-the-deployment-type-information"></a>Detectar automáticamente la información de tipo de implementación  

1.  En la página **General** del Asistente para crear tipos de implementación, active la casilla **Identificar automáticamente la información sobre este tipo de implementación a partir de los archivos de instalación** .  

2.  En el campo **Tipo** , seleccione el tipo de archivo de instalación de aplicación que desea utilizar para detectar información del tipo de implementación.  
  
3.  En el campo **Ubicación**, especifique la ruta UNC con el formato *\\\\servidor\\recurso compartido\\nombre de archivo* o el vínculo de la tienda a los archivos de instalación de la aplicación y el contenido que quiera usar para detectar la información de tipo de implementación. También puede hacer clic **Examinar** para buscar el archivo de instalación.  
    > [!NOTE]  
    >  Debe poder acceder a la ruta de acceso UNC que contiene la aplicación y todas las subcarpetas que tienen el contenido de la aplicación.  

4.  En la página **Importar información** del Asistente para crear tipos de implementación, revise la información que se importó y, a continuación, haga clic en **Siguiente**. También puede hacer clic en **Anterior** para volver atrás y corregir los errores que pudiese haber.  

5.  En la página **Información general** del Asistente para crear tipos de implementación, especifique la información siguiente:  

    > [!NOTE]  
    >  Es posible que parte de la información del tipo de implementación ya esté presente si se obtuvo de los archivos de instalación de la aplicación. Además, las opciones mostradas pueden diferir según el tipo de implementación que se va a crear.  

    -   Especifique la información general sobre el tipo de implementación, como el nombre, los comentarios del administrador y los idiomas disponibles.  

    -   **Programa de instalación** : especifique el programa de instalación y las propiedades que se requieren para instalar al tipo de implementación.  

    -   **Comportamiento de instalación** : especifique si quiere instalar el tipo de implementación para el usuario que inició la sesión o para todos los usuarios. También puede especificar que el tipo de implementación se instale para todos los usuarios si se implementa en un dispositivo, o instalar el tipo de implementación solo para un usuario si se implementa en un usuario.  

    -   **Usar una conexión VPN automática (si se configuró)** : si se ha implementado un perfil de VPN en el dispositivo en el que se inicia la aplicación, la conexión VPN se inicia cuando lo hace la aplicación (solo en Windows 8.1 y Windows Phone 8.1). Si se han implementado varios perfiles de VPN en un dispositivo de Windows 8.1, se usará de forma predeterminada el primer perfil de VPN implementado.  

         En dispositivos de Windows Phone 8.1, las conexiones VPN automáticas no se admiten si se ha implementado más de un perfil de VPN.  

         Para obtener más información sobre los perfiles de VPN, consulte [VPN profiles in System Center Configuration Manager](../../protect/deploy-use/vpn-profiles.md) (Perfiles de VPN en System Center Configuration Manager).  

6.  Haga clic en **Siguiente** y continúe con [Especificar las opciones de contenido del tipo de implementación](/sccm/apps/deploy-use/create-applications#specify-content-options-for-the-deployment-type).  

### <a name="manually-configure-the-deployment-type-information"></a>Configurar manualmente la información del tipo de implementación  

1.  En la página **General** del Asistente para crear tipos de implementación, seleccione **Especificar manualmente la información del tipo de implementación**.  

2.  En el campo **Tipo** , elija el tipo de archivo de instalación de aplicación que desea utilizar para detectar información del tipo de implementación. Puede elegir los mismos tipos de instalación que usaría para detectar automáticamente la información del tipo de implementación, y también puede especificar un script para instalar el tipo de implementación.  

3.  En la página **Información general** del Asistente para crear tipos de implementación, especifique un nombre para el tipo de implementación, una descripción opcional, los idiomas en los que desea que este tipo de implementación esté disponible y, a continuación, haga clic en **Siguiente**.  

4.  Continúe con [Especificar las opciones de contenido del tipo de implementación](/sccm/apps/deploy-use/create-applications#specify-content-options-for-the-deployment-type).  

##  <a name="specify-content-options-for-the-deployment-type"></a>Especificar las opciones de contenido del tipo de implementación  

1.  En la página **Contenido** del Asistente para crear tipos de implementación, especifique la siguiente información:  
  
    -   Ubicación del contenido: especifique la ubicación del contenido para este tipo de implementación o haga clic en **Examinar** para seleccionar la carpeta de contenido del tipo de implementación.  
        > [!IMPORTANT]  
        >  La cuenta del sistema del equipo del servidor de sitio debe tener permisos para la ubicación del contenido que especifique.  

    -   **Conservar contenido en la memoria caché del cliente** : seleccione esta opción para especificar si el contenido debe conservarse en la memoria caché del equipo cliente de manera indefinida, incluso aunque ya se haya ejecutado. Si bien esta opción puede ser útil en algunas implementaciones como, por ejemplo, la implementación de software basado en Windows Installer que requiere que haya una copia de origen local disponible para aplicar las actualizaciones, reducirá el espacio libre en la memoria caché. Si se selecciona esta opción, podría posteriormente causar un error de una implementación de gran tamaño si la memoria caché no tiene espacio disponible suficiente.  

    -   **Permitir a los clientes compartir el contenido con otros clientes en la misma subred** : seleccione esta opción para reducir la carga de la red permitiendo a los clientes la descarga de contenido de otros clientes locales de la red que ya han descargado y almacenado en caché el contenido. Esta opción utiliza tecnología Windows BranchCache.  

    -   **Programa de instalación** : especifique el nombre del programa de instalación y los parámetros de instalación necesarios o haga clic en **Examinar** para buscar la ubicación del archivo de instalación.  

    -   **Inicio de instalación en** : opcionalmente, puede especificar la carpeta que contiene el programa de instalación para el tipo de implementación. Esta carpeta puede ser una ruta de acceso absoluta en el cliente, o una ruta de acceso a la carpeta del punto de distribución que contiene los archivos de instalación.  

    -   **Desinstalar programa** : opcionalmente, puede especificar el nombre del programa de desinstalación y los parámetros necesarios o hacer clic en **Examinar** para buscarlo.  

    -   **Inicio de desinstalación en** : opcionalmente, puede especificar la carpeta que contiene el programa de desinstalación para el tipo de implementación. Esta carpeta puede ser una ruta de acceso absoluta en el cliente, o una ruta de acceso relacionada con la carpeta del punto de distribución que contiene el paquete.  

    -   **Ejecutar programa de instalación y desinstalación como proceso de 32 bits en clientes de 64 bits** : utilice las ubicaciones del Registro y de archivos de 32 bits en equipos basados en Windows para ejecutar el programa de instalación del tipo de implementación.  

2.  Haga clic en **Siguiente**.  

## <a name="configure-detection-methods-to-indicate-the-presence-of-the-deployment-type-windows-pcs-only"></a>Configurar métodos de detección para indicar la presencia del tipo de implementación (solo en PC Windows)  
 Este procedimiento configura un método de detección que indica si el tipo de implementación ya está instalado.  

1.  En la página **Método de detección** del Asistente para crear tipos de implementación, seleccione **Configurar reglas para detectar la presencia de este tipo de implementación**y, a continuación, haga clic en **Agregar cláusula**.  

    > [!NOTE]  
    >  También se puede seleccionar **Usar un script personalizado para detectar la presencia de este tipo de implementación**. Para obtener más información, consulte la sección Usar un script personalizado para determinar la presencia de un tipo de implementación de este tema.  

2.  En el cuadro de diálogo **Regla de detección** , en la lista desplegable **Tipo de configuración** , seleccione el método que desea utilizar para detectar la presencia del tipo de implementación. Puede elegir entre los siguientes métodos disponibles:  

    -   **Sistema de archivos** : use este método para detectar si una carpeta o un archivo especificados existen en un dispositivo cliente, lo que indicaría que la aplicación está instalada.  

        > [!NOTE]  
        >  El tipo de configuración **Sistema de archivos** no admite la especificación de una ruta de acceso UNC a un recurso compartido de red en el campo Ruta de acceso. Solo se puede especificar una ruta de acceso local en el dispositivo cliente.  
        >   
        >  Seleccione la opción **Este archivo o carpeta está asociado a una aplicación de 32 bits en sistemas de 64 bits** para comprobar primero ubicaciones de archivos de 32 bits para la carpeta o archivo especificado. Si no se encuentra el archivo o la carpeta, se realizará la búsqueda en ubicaciones de 64 bits.  

    -   **Registro** : puede usar este método para detectar si una clave o un valor del Registro especificados existen en un dispositivo cliente, lo que indicaría que la aplicación está instalada.  

        > [!NOTE]  
        >  Seleccione la opción **La clave del Registro está asociada a una aplicación de 32 bits en sistemas de 64 bits** para comprobar primero ubicaciones del Registro de 32 bits para la clave del Registro especificada. Si no se encuentra la clave del Registro, se realizará la búsqueda en ubicaciones de 64 bits.  

    -   **Windows Installer** : use este método para detectar si un archivo de Windows Installer especificado existe en un dispositivo cliente, lo que indicaría que la aplicación está instalada.  

3.  Especifique los detalles sobre el elemento que desea utilizar para detectar si está instalado este tipo de implementación. Por ejemplo, puede utilizar un archivo, una carpeta, una clave o un valor del Registro, o un código de producto de Windows Installer.  

4.  Especifique los detalles acerca del valor que desea evaluar con respecto al elemento que se utiliza para detectar si está instalado el tipo de implementación. Por ejemplo, si utiliza un archivo para determinar si el tipo de implementación está instalado, puede activar la casilla **La configuración del sistema de archivos debe existir en el sistema de destino para indicar la presencia de esta aplicación** .  

5.  Haga clic en **Siguiente** para cerrar el cuadro de diálogo **Regla de detección** .  

###  <a name="use-a-custom-script-to-determine-the-presence-of-a-deployment-type"></a>Usar un script personalizado para determinar la presencia de un tipo de implementación  

1.  En la página **Método de detección** del Asistente para crear tipos de implementación, active la casilla **Usar un script personalizado para detectar la presencia de este tipo de implementación** y, a continuación, haga clic en **Editar**.  

2.  En el cuadro de diálogo **Editor de scripts** , en la lista desplegable **Tipo de script** , seleccione el lenguaje de script que desea utilizar para detectar el tipo de implementación.  

3.  En el campo **Contenido del script** , escriba el script que desea utilizar. También puede pegar el contenido de un script existente en este campo o hacer clic en **Abrir** para ir a un script existente guardado anteriormente. Configuration Manager determina los resultados del script mediante la lectura de los valores escritos en las secuencias de salida Standard Out (STDOUT) y Standard Error (STDERR), y el código de salida del script. Si el código de salida es un valor distinto de cero, se ha producido un error del script y el estado de detección de la aplicación se desconoce. Si el código de salida es cero y STDOUT contiene datos, el estado de detección de la aplicación es Instalada.  

Utilice la tabla siguiente para determinar cómo se puede usar la salida de un script para establecer si una determinada aplicación está instalada.  

|Código de salida de script|Detalles|
|-|-|
|0|**Datos leídos de STDOUT** (vacío)<br /><br /> **Datos leídos de STDERR** (vacío)<br /><br /> **Resultado del script** (correcto)<br /><br /> **Estado de detección de la aplicación** (no instalado)|  
|0|**Datos leídos de STDOUT** (vacío)<br /><br /> **Datos leídos de STDERR** (no está vacío)<br /><br /> **Resultado del script** (error)<br /><br /> **Estado de detección de la aplicación** (desconocido)|  
|0|**Datos leídos de STDOUT** (no está vacío)<br /><br /> **Datos leídos de STDERR** (vacío)<br /><br /> **Resultado del script** (correcto)<br /><br /> **Estado de detección de la aplicación** (instalado)|  
|0|**Datos leídos de STDOUT** (no está vacío)<br /><br /> **Datos leídos de STDERR** (no está vacío)<br /><br /> **Resultado del script** (correcto)<br /><br /> **Estado de detección de la aplicación** (instalado)|  
|Valor distinto de cero|**Datos leídos de STDOUT** (vacío)<br /><br /> **Datos leídos de STDERR** (vacío)<br /><br /> **Resultado del script** (error)<br /><br /> **Estado de detección de la aplicación** (desconocido)|  
|Valor distinto de cero|**Datos leídos de STDOUT** (vacío)<br /><br /> **Datos leídos de STDERR** (no está vacío)<br /><br /> **Resultado del script** (error)<br /><br /> **Estado de detección de la aplicación** (desconocido)|  
|Valor distinto de cero|**Datos leídos de STDOUT** (no está vacío)<br /><br /> **Datos leídos de STDERR** (vacío)<br /><br /> **Resultado del script** (error)<br /><br /> **Estado de detección de la aplicación** (desconocido)|  
|Valor distinto de cero|**Datos leídos de STDOUT** (no está vacío)<br /><br /> **Datos leídos de STDERR** (no está vacío)<br /><br /> **Resultado del script** (error)<br /><br /> **Estado de detección de la aplicación** (desconocido)|  

La tabla siguiente contiene scripts de muestra de Microsoft Visual Basic (VB) que puede utilizar para escribir sus propios scripts de detección de aplicaciones.  

|Script de muestra de Visual Basic|Descripción|  
|--------------------------------|-----------------|  
|**WScript.Quit(1)**|El script devuelve un código de salida distinto de cero, lo que indica que no pudo ejecutarse correctamente. En este caso, el estado de detección de la aplicación es desconocido.|  
|**WScript.StdErr.Write "Error de script"**<br /><br /> **WScript.Quit(0)**|El script devuelve un código de salida de cero, pero el valor de STDERR no está vacío, lo que indica que no se ha podido ejecutar correctamente el script. En este caso, el estado de detección de la aplicación es desconocido.|  
|**WScript.Quit(0)**|El script devuelve un código de salida de cero, lo que indica que se ejecutó correctamente. Sin embargo, el valor de STDOUT está vacío, lo que indica que la aplicación no está instalada.|  
|**WScript.StdOut.Write "La aplicación está instalada"**<br /><br /> **WScript.Quit(0)**|El script devuelve un código de salida de cero, lo que indica que se ejecutó correctamente. El valor de STDOUT no está vacío, lo que indica que la aplicación está instalada.|  
|**WScript.StdOut.Write "La aplicación está instalada"**<br /><br /> **WScript.StdErr.Write "Completado"**<br /><br /> **WScript.Quit(0)**|El script devuelve un código de salida de cero, lo que indica que se ejecutó correctamente. Los valores de STDOUT y STDERR no están vacíos, lo que indica que la aplicación está instalada.|  

> [!NOTE]  
    >  El tamaño máximo de un script es 32 kilobytes (KB).  

4.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Editor de script** .  

## <a name="specify-user-experience-options-for-the-deployment-type"></a>Especificar opciones de experiencia del usuario para el tipo de implementación  
 Esta configuración especifica cómo se instalará la aplicación en los dispositivos y lo que el usuario verá.  

1.  En la página **Experiencia del usuario** del Asistente para crear tipos de implementación, especifique la información siguiente:  

    -   **Comportamiento de instalación** : en la lista desplegable, seleccione una de las opciones que se muestran a continuación.  

        -   **Instalar para el usuario** : la aplicación se instala solo para el usuario al que se implementa la aplicación.  

        -   **Instalar para el sistema** : la aplicación se instala solo una vez y está disponible para todos los usuarios.  

        -   **Instalar para el sistema si el recurso es el dispositivo; de lo contrario, instalar para el usuario** : si la aplicación se implementa en un dispositivo, se instalará para todos los usuarios. Si la aplicación se implementa en un usuario, se instalará solo para ese usuario.  

    -   **Requisito de inicio de sesión** : especifique los requisitos de inicio de sesión para este tipo de implementación de entre las siguientes opciones:  

        -   **Solo cuando un usuario haya iniciado sesión**  

        -   **Tanto si un usuario ha iniciado sesión como si no**  

        -   **Solo cuando ningún usuario haya iniciado sesión**  

        > [!NOTE]  
        >  La opción predeterminada será **Solo cuando un usuario haya iniciado sesión**, y no se puede cambiar si se seleccionó **Instalar para el usuario** en la lista desplegable **Comportamiento de instalación** .  

    -   **Visibilidad del programa de instalación** : especifique el modo en que el tipo de implementación se ejecutará en dispositivos cliente. Están disponibles las siguientes opciones:  

        -   **Maximizado** : el tipo de implementación se ejecuta maximizado en dispositivos cliente. Los usuarios verán toda la actividad de instalación.  

        -   **Normal** : el tipo de implementación se ejecuta en el modo normal en función de los valores predeterminados del programa y del sistema. Este es el modo predeterminado.  

        -   **Minimizado** : el tipo de implementación se ejecuta minimizado en dispositivos cliente. Los usuarios pueden ver la actividad de instalación en el área de notificación o en la barra de tareas.  

        -   **Oculto** : el tipo de implementación se ejecuta de forma oculta en los dispositivos cliente y los usuarios no ven ninguna actividad de instalación.  

    -   **Permitir a los usuarios ver la instalación del programa e interactuar con la misma** : especifica si un usuario puede interactuar con la instalación del tipo de implementación para configurar las opciones de instalación.  

        > [!NOTE]  
        >  Esta opción está habilitada de forma predeterminada si se seleccionó la opción **Instalar para el usuario** en la lista desplegable **Comportamiento de instalación** .  

    -   **Tiempo de ejecución máximo permitido (minutos)** : especifique el tiempo máximo que se espera que el programa se ejecute en el equipo cliente. Puede especificar esta configuración como un número entero mayor que cero. El valor predeterminado es 120 minutos.  

         Este valor se utiliza para:  

        -   Supervisar los resultados a partir del tipo de implementación.  

        -   Determinar si un tipo de implementación se instalará al definir las ventanas de mantenimiento en dispositivos cliente. Si se ha programado una ventana de mantenimiento, los programas se iniciarán solo si hay suficiente tiempo disponible en la ventana de mantenimiento según el parámetro **Tiempo de ejecución máximo permitido** .  

        > [!IMPORTANT]  
        >  Se puede producir un conflicto si el **Tiempo de ejecución máximo permitido** es mayor que la ventana de mantenimiento programada. Si el usuario configura la duración máxima de la ejecución como un periodo que excede la duración de las ventanas de mantenimiento disponibles, ese tipo de implementación no se ejecutará.  

2.  **Tiempo de instalación estimado (minutos)** : especifique el tiempo estimado que tardará la instalación del tipo de implementación. Esto se muestra a los usuarios del Centro de software.  

## <a name="specify-requirements-for-the-deployment-type"></a>Especificar requisitos para el tipo de implementación  

1.  En la página **Requisitos** del Asistente para crear tipos de implementación, haga clic en **Agregar** para abrir el cuadro de diálogo **Crear requisito** y agregar un nuevo requisito.  

    > [!NOTE]  
    >  También puede agregar nuevos requisitos en la pestaña **Requisitos** del cuadro de diálogo **Propiedades de** *<nombre de tipo de implementación\>*.  
  
2.  En la lista desplegable **Categoría** , seleccione si este requisito es para un dispositivo o un usuario, o seleccione **Personalizada** para usar una condición global creada previamente. Si se selecciona **Personalizada**, también puede hacer clic en **Crear** para crear una nueva condición global. Para obtener más información sobre las condiciones globales, consulte [How to create global conditions](../../apps/deploy-use/create-global-conditions.md) (Cómo crear condiciones globales).  
  

    > [!IMPORTANT]  
    >  Si se crea un requisito de la categoría **Usuario** y la condición **Dispositivo primario**y, luego, se implementa la aplicación en una colección de dispositivos, el requisito se omitirá.  
    >   
    >  Si ha creado un paquete de Windows y un programa o una secuencia de tareas que tienen Windows 10 como un requisito usando System Center 2012 R2 Configuration Manager SP1 y, después, actualiza a System Center Configuration Manager, los requisitos de Windows 10 podrían quitarse. Para corregir este problema, vuelva a especificar los requisitos. Tenga en cuenta que, aunque se ha quitado el requisito de la pantalla de requisitos, aún se está procesando correctamente en los dispositivos.  

3.  En la lista desplegable **Condición** , seleccione la condición que desea usar para evaluar si el usuario o el dispositivo cumplen los requisitos de instalación. El contenido de esta lista variará según la categoría seleccionada.  

4.  En la lista desplegable **Operador** , seleccione el operador que se utilizará para comparar la condición seleccionada con el valor especificado para evaluar si el usuario o el dispositivo cumplen los requisitos de instalación. Los operadores disponibles variarán según la condición seleccionada.  

    > [!IMPORTANT]  
    >  Los requisitos disponibles variarán en función del tipo de dispositivo del tipo de implementación.  

5.  En el campo **Valor** , especifique los valores que se utilizarán con la condición y el operador seleccionados para evaluar si el usuario o el dispositivo cumplen los requisitos de instalación. Los valores disponibles variarán según la condición seleccionada y el operador seleccionado.  

6.  Haga clic en **Aceptar** para guardar los requisitos y cierre el cuadro de diálogo **Crear requisito** .  

## <a name="specify-dependencies-for-the-deployment-type"></a>Especificar dependencias para el tipo de implementación  
 Las dependencias definen uno o más tipos de implementación de otra aplicación que se deben instalar antes de que se instale un tipo de implementación. Puede configurar los tipos de implementación dependientes para que se instalen automáticamente antes de la instalación de un determinado tipo de implementación.  

> [!IMPORTANT]  
>  En algunos casos, un tipo de implementación depende de un tipo de implementación que también contiene dependencias. En este escenario, en el que hay una cadena de dependencias, el número máximo de dependencias admitidas en la cadena es **cinco**.  

1.  En la página **Dependencias** del Asistente para crear tipos de implementación, haga clic en **Agregar** si desea especificar los tipos de implementación que se deben instalar para poder realizar la instalación de este tipo de implementación.  

    > [!IMPORTANT]  
    >  También puede agregar nuevas dependencias en la pestaña **Dependencias** del cuadro de diálogo**Propiedades** de *<nombre del tipo de implementación\>*.  

2.  En el cuadro de diálogo **Agregar dependencia** , haga clic en **Agregar**.  

3.  En el cuadro de diálogo **Especificar aplicación requerida** , seleccione una aplicación existente y uno de los tipos de implementación de la aplicación para utilizarlo como una dependencia.  

    > [!TIP]  
    >  Puede hacer clic en **Ver** para mostrar las propiedades del la aplicación o del tipo de implementación seleccionado.  

4.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Especificar aplicación requerida** .  

5.  Si desea que una aplicación dependiente se instale automáticamente, seleccione **Instalación automática** junto a la aplicación dependiente.  

    > [!NOTE]  
    >  No es necesario que se implemente una aplicación dependiente para que se instale automáticamente.  

6.  En cuadro de diálogo **Agregar dependencia** , en el campo **Nombre del grupo de dependencia** , escriba un nombre que haga referencia a este grupo de dependencias de aplicaciones.  

7.  Opcionalmente, use los botones **Aumentar prioridad** y **Disminuir prioridad** para cambiar el orden en el que se evalúa cada dependencia.  

8.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Agregar dependencia** .  

## <a name="confirm-the-deployment-type-settings-and-complete-the-wizard"></a>confirmar la configuración del tipo de implementación y completar el asistente  

1.  En la página **Resumen** del Asistente para crear tipos de implementación, revise las acciones que el asistente realizará. Haga clic en **Siguiente** para crear el tipo de implementación, o haga clic en **Anterior** para cambiar la configuración del tipo de implementación.  

2.  Una vez se haya completado la página **Progreso**, revise las acciones realizadas por el asistente y después haga clic en **Cerrar** para completarlo.  

3.  Si inició el Asistente para crear tipos de implementación desde el Asistente para crear aplicaciones, volverá a la página **Tipos de implementación** del Asistente para crear aplicaciones.  

## <a name="configure-additional-options-for-deployment-types-that-contain-virtual-applications"></a>Configurar opciones adicionales para tipos de implementación que contienen aplicaciones virtuales  
 Utilice los procedimientos siguientes para configurar opciones adicionales para los tipos de implementación que contienen aplicaciones virtuales.  

### <a name="configure-content-options-for-application-virtualization-app-v-deployment-types"></a>Configurar las opciones de contenido de los tipos de implementación de Application Virtualization (App-V)  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software** > **Aplicaciones**.  

3.  En la lista **Aplicaciones** , seleccione una aplicación que contenga un tipo de implementación de App-V. A continuación, en la pestaña **Inicio** , en el grupo **Propiedades** , haga clic en **Propiedades**.  

4.  En el cuadro de diálogo **Propiedades** de *<nombre de la aplicación\>*, en la pestaña **Tipos de implementación**, seleccione un tipo de implementación de App-V y después haga clic en **Editar**.  

5.  En el cuadro de diálogo **Propiedades** de *<nombre del tipo de implementación\>*, en la pestaña **Contenido**, configure las opciones siguientes si es necesario:  

    -   **Conservar contenido en la memoria caché del cliente**: seleccione esta opción para asegurarse de que el contenido de este tipo de implementación no se elimina de la memoria caché del cliente de Configuration Manager.  

    -   **Cargar contenido en la memoria caché de App-V antes del inicio** : seleccione esta opción para garantizar que todo el contenido de la aplicación virtual se cargue en la memoria caché de App-V antes de que la aplicación se inicie. La selección de esta opción también garantiza que el contenido de la aplicación no está anclado en la memoria caché y se puede eliminar según sea necesario.  

6.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Propiedades** de *<nombre del tipo de implementación\>*.  

7.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Propiedades** de *<nombre de aplicación\>*.  

### <a name="configure-publishing-options-for-app-v-deployment-types"></a>Configurar opciones de publicación de los tipos de implementación de App-V  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software** > **Aplicaciones**.  

3.  En la lista **Aplicaciones** , seleccione una aplicación que contenga un tipo de implementación de App-V. A continuación, en la pestaña **Inicio** , en el grupo **Propiedades** , haga clic en **Propiedades**.  

4.  En el cuadro de diálogo **Propiedades** de *<nombre de la aplicación\>*, en la pestaña **Tipos de implementación**, seleccione un tipo de implementación de App-V y después haga clic en **Editar**.  

5.  En el cuadro de diálogo **Propiedades** de *<nombre del tipo de implementación\>*, en la pestaña **Publicación**, seleccione los elementos de la aplicación virtual que quiera publicar.  

6.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Propiedades** de *<nombre del tipo de implementación\>*.  

7.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Propiedades** de *<nombre de aplicación\>*.  

## <a name="import-an-application"></a>Importar una aplicación  
 Use el procedimiento siguiente para importar una aplicación en Configuration Manager. Para obtener más información sobre cómo exportar una aplicación, consulte [Management tasks for System Center Configuration Manager applications](../../apps/deploy-use/management-tasks-applications.md) (Tareas de administración para aplicaciones de System Center Configuration Manager).  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software** > **Administración de aplicaciones** > **Aplicaciones**.  

3.  En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Importar aplicación**.  

4.  En la página **General** del **Asistente para importar aplicaciones**, haga clic en **Examinar** y luego especifique una ruta de acceso UNC para el archivo comprimido (archivo .zip) que contenga la aplicación que quiere importar.  

5.  En la página **Contenido del archivo**, seleccione la acción que se realizará si la aplicación que intenta importar es un duplicado de una aplicación existente. Puede especificar que se cree una nueva aplicación o que se omita el duplicado y se agregue una nueva revisión a la aplicación existente.  

6.  En la página **Resumen**, revise las acciones que se realizarán y después complete el asistente.  

 La nueva aplicación se muestra en el nodo **Aplicaciones** .  

> [!TIP]  
>  El cmdlet de Windows PowerShell **Import-CMApplication** realiza la misma función que este procedimiento. Para obtener más información, consulte [Import-CMApplication](https://technet.microsoft.com/library/jj821738.aspx) en la documentación de referencia del cmdlet de Microsoft System Center 2012 Configuration Manager SP1.  

##  <a name="deployment-types-supported-by-configuration-manager"></a>Tipos de implementación que admite Configuration Manager  

|Nombre de tipo de implementación|Más información|  
|--------------------------|----------------------|  
|**Windows Installer (archivo \*.msi)**|Crea un tipo de implementación desde un archivo de Windows Installer.|  
|**Paquete de aplicación de Windows (\*.appx, \*.appxbundle)**|Crea un tipo de implementación para el sistema operativo Windows 8, Windows RT o una versión posterior, a partir de un archivo de paquete de aplicación de Windows o un paquete de agrupación de aplicaciones de Windows.|  
|**Paquete de aplicación de Windows (en la Tienda Windows)**|Crea un tipo de implementación para Windows 8, Windows RT o una versión posterior, mediante la especificación de un vínculo a la aplicación en la Tienda Windows o navegando por la tienda para seleccionar la aplicación que necesita.<br /><br /> Si desea implementar la aplicación como un vínculo a la Tienda Windows, asegúrese de que la configuración de directiva de grupo **Desactivar la aplicación Tienda** se establece como **Deshabilitada** o **No configurada**. Si esta opción está habilitada, los clientes no podrán conectarse a la Tienda Windows para descargar e instalar aplicaciones.<br /><br /> Los tipos de implementación de Windows 8 que usan un vínculo a un almacén siempre se evalúan antes que otros tipos de implementación, con independencia de su prioridad.|  
|**Instalador de scripts**|Crea un tipo de implementación que especifica un script que se ejecuta en dispositivos cliente para instalar contenido o realizar una acción.|  
|**Microsoft Application Virtualization 4**|Crear un tipo de implementación a partir de un manifiesto de Microsoft Application Virtualization 4|  
|**Microsoft Application Virtualization 5**|Crea un tipo de implementación de un archivo de paquete de Microsoft Application Virtualization 5.|  
|**Paquete de aplicación de Windows Phone (archivo \*.xap)**|Crea un tipo de implementación de un archivo de paquete de aplicación de Windows Phone.|  
|**Paquete de aplicación de Windows Phone (en la Tienda de Windows Phone)**|Crea un tipo de implementación mediante la especificación de un vínculo a la aplicación en la Tienda de Windows Phone.|  
|**Archivo .CAB de Windows Mobile**|Crea un tipo de implementación para dispositivos Windows Mobile a partir de un archivo .cab de Windows Mobile.|  
|**Paquete de aplicación de iOS (archivo \*.ipa)**|Crea un tipo de implementación de un archivo de paquete de aplicación de iOS.|  
|**Paquete de aplicación de iOS en App Store**|Crea un tipo de implementación mediante la especificación de un vínculo a la aplicación de iOS en la App Store.|  
|**Paquete de aplicación de Android (archivo \*.apk)**|Crea un tipo de implementación de un archivo de paquete de aplicación de Android.|  
|**Paquete de aplicación para Android en Google Play**|Crea un tipo de implementación mediante la especificación de un vínculo a la aplicación en Google Play.|  
|**Mac OS X**|Crea un tipo de implementación para equipos Mac desde un archivo .cmmac creado mediante la herramienta CMAppUtil.<br /><br /> Se aplica a equipos Mac que ejecutan solo el cliente de Configuration Manager.|  
|**Aplicación web**|Crea un tipo de implementación que especifica un vínculo a una aplicación web. El tipo de implementación instala un acceso directo a la aplicación web en el dispositivo del usuario.<br /><br /> Si ha instalado Intune Managed Browser en dispositivos iOS o Android que administra, puede asegurarse de que los usuarios solo pueden utilizar el explorador administrado para abrir la aplicación. Para ello, use uno de los siguientes formatos cuando especifique un vínculo a la aplicación al reemplazar **http:** con **http-intunemam:** o **https:** con **https-intunemam:**<br /><br /> - **http-intunemam://<ruta de acceso a la aplicación web\>**<br /><br /> - **https-intunemam://<ruta de acceso a la aplicación web\>**<br /><br /> Puede usar los requisitos de la aplicación de Configuration Manager para garantizar que las aplicaciones que quiere asociar con el explorador administrado solo se instalan en dispositivos iOS y Android.<br />aspx).<br /><br /> Para obtener más información sobre Intune Managed Browser, consulte [Administrar el acceso a Internet mediante directivas de explorador administrado con Microsoft Intune](../../apps/deploy-use/manage-internet-access-using-managed-browser-policies.md).|  
|**Windows Installer a través de MDM (\*.msi)**|Este tipo de instalador le permite crear e implementar aplicaciones basadas en Windows Installer en equipos que ejecuten Windows 10.<br /><br /> Las consideraciones siguientes se aplican cuando se utiliza este tipo de instalador:<br><br>- Solo puede cargar un único archivo con la extensión .msi.<br /><br /> - El código de producto y la versión del producto del archivo se usan para la detección de la aplicación.<br /><br /> - Se utilizará el comportamiento de reinicio predeterminado de la aplicación. Configuration Manager no lo controla.<br /><br /> - Los paquetes MSI por usuario se instalarán para un solo usuario.<br /><br /> - Los paquetes MSI por máquina se instalarán para todos los usuarios del dispositivo.<br /><br /> - Actualmente, los paquetes MSI de modo dual solo se instalan para todos los usuarios del dispositivo.<br /><br /> - Se admiten actualizaciones de aplicaciones cuando el código de producto MSI de cada versión es el mismo.|  



<!--HONumber=Nov16_HO1-->


