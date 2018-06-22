---
title: Crear aplicaciones
titleSuffix: Configuration Manager
description: Cree aplicaciones con tipos de implementación, métodos de detección y requisitos para instalar el software.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: cc230ff4-7056-4339-a0a6-6a44cdbb2857
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c9b90dfcc0916f62905af777e45222ceebf8300f
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32341889"
---
# <a name="create-applications-with-system-center-configuration-manager"></a>Crear aplicaciones con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Una aplicación de Configuration Manager tiene uno o varios tipos de implementación. Estos tipos de implementación incluyen la información y los archivos de instalación necesarios para instalar el software en los dispositivos. Un tipo de implementación también tiene reglas, como métodos de detección y requisitos, que especifican cuándo y cómo instala el software el cliente.  

 Cree aplicaciones mediante los métodos siguientes:  

-   Crear automáticamente los tipos de aplicación y de implementación mediante la lectura de los archivos de instalación de la aplicación.  

-   Crear manualmente la aplicación y, a continuación, agregar los tipos de implementación más adelante.  

-   Importe una aplicación desde un archivo.  

> [!NOTE]  
>  Para obtener información detallada sobre cómo crear aplicaciones iOS, Windows Phone y Android, vea [Create applications for mobile devices](../../mdm/deploy-use/create-applications.md) (Creación de aplicaciones para dispositivos móviles).  



## <a name="start-the-create-application-wizard"></a>Inicie el Asistente para crear aplicaciones  

1.  En la consola de Configuration Manager, elija **Biblioteca de software** > **Administración de aplicaciones** > **Aplicaciones**.  

3.  En la pestaña **Inicio**, en el grupo **Crear**, elija **Crear aplicación**.  



## <a name="specify-whether-you-want-to-automatically-detect-application-information-or-manually-define-the-information"></a>especifique si desea detectar automáticamente la información de la aplicación o definir esta información de forma manual  

-   Detecte automáticamente la información de la aplicación para crear una aplicación básica con un solo tipo de implementación. Por ejemplo, un archivo de Windows Installer que no tiene dependencias ni requisitos. Después de crear una aplicación mediante este procedimiento, puede editarla según sea necesario para agregar o modificar los tipos de implementación y agregar métodos de detección, dependencias o requisitos.  

-   Especifique manualmente la información de la aplicación para crear aplicaciones más complejas que tengan varios tipos de implementación, dependencias, métodos de detección o requisitos.  

### <a name="automatically-detect-application-information"></a>Detectar automáticamente la información de la aplicación  

1.  En la página **General** del Asistente para crear aplicaciones, seleccione **Detectar automáticamente la información sobre esta aplicación a partir de archivos de instalación**.  

2.  En la lista desplegable **Tipo** , seleccione el tipo de archivo de instalación de aplicación que desea utilizar para detectar información de la aplicación. Para obtener más información sobre los tipos de instalación disponibles, consulte [Tipos de implementación que admite Configuration Manager](/sccm/apps/deploy-use/create-applications#deployment-types-supported-by-configuration-manager) en este mismo tema.  

3.  En el cuadro **Ubicación**, especifique la ruta de acceso UNC (con el formato *\\\\servidor\\recurso compartido\\\nombre de archivo*) o el vínculo de la tienda del archivo de instalación de la aplicación que quiera usar para detectar la información de la aplicación. Como alternativa, haga clic en **Examinar** para buscar el archivo de instalación.  

    > [!IMPORTANT]  
    >  Si selecciona **Windows Installer (archivo \*.msi)** como tipo de aplicación, se importan todos los archivos de la carpeta especificada y se envían a los puntos de distribución. Asegúrese de que la carpeta que especifique solo contenga los archivos necesarios para instalar la aplicación. Configuration Manager se ha probado y admite hasta 20 000 archivos de aplicación en el paquete de la aplicación. Si la aplicación tiene más archivos, considere la posibilidad de crear varias aplicaciones con un menor número de archivos.  

    >  Debe poder tener acceso a la ruta de acceso UNC que tiene la aplicación y a todas las subcarpetas que incluyen el contenido de la aplicación.  

4.  En la página **Importar información** del Asistente para crear aplicaciones, revise la información que se ha importado y después seleccione **Siguiente**. Si es necesario, puede seleccionar **Anterior** para volver atrás y corregir los errores.  

5.  En la página **Información general** del Asistente para crear aplicaciones, especifique la siguiente información:  

    > [!NOTE]  
    >  Si Configuration Manager detecta automáticamente esta información en los archivos de instalación de la aplicación, ya está rellenada aquí. Además, las opciones mostradas pueden ser diferentes según el tipo de aplicación que cree.  

    -   Información general sobre la aplicación, como el nombre de la aplicación, comentarios y la versión. Para ayudar a encontrar la aplicación en la consola de Configuration Manager, especifique una referencia opcional.  

    -   **Programa de instalación**: Especifique el programa de instalación y las propiedades necesarias para instalar este tipo de implementación de aplicaciones.  

        > [!TIP]  
        >  Si el programa de instalación no aparece, haga clic en **Examinar** y busque la ubicación del programa de instalación.  

    -   **Comportamiento de instalación**: especifique si el tipo de implementación de aplicación se instala únicamente para el usuario que ha iniciado sesión o para todos los usuarios. Una tercera opción consiste en instalar para todos los usuarios si se implementa en un dispositivo o solo para un usuario específico si se implementa en un usuario.  

    -   **Usar una conexión VPN automática (si se configuró)**: Si se ha implementado un perfil de VPN en el dispositivo en el que se inicia la aplicación, inicie la conexión VPN cuando la aplicación se inicie (solo Windows 8.1 y Windows Phone 8.1).  

         En dispositivos Windows Phone 8.1, las conexiones VPN automáticas no se admiten si se ha implementado más de un perfil de VPN en el dispositivo.  

         Para obtener más información, vea [Perfiles de VPN](../../protect/deploy-use/vpn-profiles.md).  

6.  Seleccione **Siguiente**, revise la información de la aplicación en la página **Resumen** y, después, finalice el Asistente para crear aplicaciones.  

La nueva aplicación aparece en el nodo **Aplicaciones** de la consola de Configuration Manager. La creación de la aplicación ha finalizado. Si quiere agregar más tipos de implementación a la aplicación, consulte [Crear tipos de implementación de la aplicación](/sccm/apps/deploy-use/create-applications#create-deployment-types-for-the-application) en este mismo tema.  

### <a name="manually-specify-application-information"></a>Especificar manualmente la información de la aplicación  

1.  En la página **General** del Asistente para crear aplicaciones, seleccione **Especificar manualmente la información de la aplicación** y, después, seleccione **Siguiente**.  

2.  Especifique información general sobre la aplicación, como el nombre de la aplicación, comentarios y la versión. Para ayudar a encontrar la aplicación en la consola de Configuration Manager, especifique una referencia opcional.  

3.  En la página **Catálogo de aplicaciones** del Asistente para crear aplicaciones, especifique la siguiente información:  

    -   **Idioma seleccionado**: en la lista desplegable, seleccione la versión de idioma de la aplicación que quiere configurar. Seleccione **Agregar o quitar** para configurar más idiomas para esta aplicación.  

    -   **Nombre de aplicación localizado**: Especifique el nombre de la aplicación en el idioma seleccionado en la lista desplegable **Idioma seleccionado** .  

        > [!IMPORTANT]  
        >  Debe especificar un nombre de aplicación localizado para cada versión de idioma que configure.  

    -   **Categorías de usuario**: haga clic en **Editar** para especificar categorías de la aplicación en el idioma que ha seleccionado en la lista desplegable **Idioma seleccionado**. Los usuarios del Centro se software pueden utilizar estas categorías seleccionadas como ayuda para filtrar y ordenar las aplicaciones disponibles.  

    -   **Documentación de usuario**: haga clic en **Examinar** para especificar la ubicación de un archivo que los usuarios del Centro de software puedan leer para obtener más información sobre esta aplicación. Esta ubicación es una dirección URL o un nombre de archivo y de ruta de acceso de red.

    -   **Texto del vínculo**: especifique el texto que aparece en lugar de la dirección URL de la aplicación.  

    -   **Dirección URL de privacidad de la aplicación**: Especifique una dirección URL vinculada a la declaración de privacidad de la aplicación.  

    -   **Descripción localizada**: Escriba una descripción para esta aplicación en el idioma seleccionado en la lista desplegable **Idioma seleccionado** .  

    -   **Palabras clave**: Escriba una lista de palabras clave en el idioma seleccionado en la lista desplegable **Idioma seleccionado** . Estas palabras clave ayudan a los usuarios del Centro de software a buscar la aplicación.  

    -   **Icono**: haga clic en **Examinar** para seleccionar un icono para esta aplicación entre los que están disponibles. Si no se especifica un icono, se usa uno predeterminado para esta aplicación. Ahora puede configurar un icono con una dimensión de píxel de hasta 512 x 512.

    -   **Mostrar esta aplicación como destacada y resaltarla en el portal de empresa**: con esta opción, la aplicación se muestra de forma destacada en el portal de empresa.  

4.  En la página **Tipos de implementación** del Asistente para crear aplicaciones, seleccione **Agregar** para crear un tipo de implementación nuevo.  

 Para obtener más información, consulte [Crear tipos de implementación de la aplicación](/sccm/apps/deploy-use/create-applications#create-deployment-types-for-the-application).  

5.  Seleccione **Siguiente**, revise la información de la aplicación en la página **Resumen** y, después, finalice el Asistente para crear aplicaciones.  

La nueva aplicación aparece en el nodo **Aplicaciones** de la consola de Configuration Manager.  



##  <a name="create-deployment-types-for-the-application"></a>Crear tipos de implementación de la aplicación  
 Si se detecta automáticamente la información de la aplicación, es posible que no sea necesario finalizar algunos de los pasos de estos procedimientos.  

### <a name="start-the-create-deployment-type-wizard"></a>Iniciar el Asistente para crear tipos de implementación  

1.  En la consola de Configuration Manager, elija **Biblioteca de software** > **Administración de aplicaciones** > **Aplicaciones**.  

3.  Seleccione una aplicación y, después, en la pestaña **Inicio**, en el grupo **Aplicación**, seleccione **Crear tipo de implementación**.  

> [!TIP]  
>  También puede iniciar el Asistente para crear tipos de implementación desde el Asistente para crear aplicaciones y desde la pestaña **Tipos de implementación** del cuadro de diálogo **Propiedades** de *<nombre de la aplicación\>*.  

### <a name="specify-whether-you-want-to-automatically-detect-deployment-type-information-or-manually-set-up-the-information"></a>Especificar si se quiere detectar automáticamente o configurar manualmente la información de tipo de implementación  
 Use uno de los procedimientos siguientes para detectar automáticamente o configurar manualmente la información de tipo de implementación.  

#### <a name="automatically-detect-deployment-type-information"></a>Detectar automáticamente la información de tipo de implementación  

1.  En la página **General** del Asistente para crear tipos de implementación, seleccione **Identificar automáticamente la información sobre este tipo de implementación a partir de los archivos de instalación**.  

2.  En el cuadro **Tipo**, seleccione el tipo de archivo de instalación de aplicación que quiere usar para detectar información del tipo de implementación.  

3.  En el cuadro **Ubicación**, especifique la ruta de acceso de red o el vínculo de la tienda a los archivos de instalación de la aplicación. Configuration Manager usa estos archivos para detectar la información del tipo de implementación. También puede seleccionar **Examinar** para buscar el archivo de instalación.  

    > [!NOTE]  
    >  Debe tener acceso a la ruta de acceso de red que tiene la aplicación y a todas las subcarpetas que incluyen el contenido de la aplicación.  

4.  En la página **Importar información** del Asistente para crear tipos de implementación, revise la información que se ha importado y después seleccione **Siguiente**. También puede seleccionar **Anterior** para volver atrás y corregir los errores.  

5.  En la página **Información general** del Asistente para crear tipos de implementación, especifique la información siguiente:  

    > [!NOTE]  
    >  Es posible que parte de la información del tipo de implementación ya esté presente si se obtuvo de los archivos de instalación de la aplicación. Además, es posible que las opciones que se muestran difieran, según el tipo de implementación que se va a crear.  

    -   Información general sobre el tipo de implementación, como el nombre, comentarios del administrador y los idiomas disponibles.  

    -   **Programa de instalación**: Especifique el programa de instalación y las propiedades que se requieren para instalar al tipo de implementación.  

    -   **Comportamiento de instalación**: especifique si el tipo de implementación se va a instalar para el usuario actual o para todos los usuarios. Una tercera opción consiste en instalar para todos los usuarios si se implementa en un dispositivo o solo para un usuario específico si se implementa en un usuario.  

    -   **Usar una conexión VPN automática (si se configuró)**: Si se ha implementado un perfil de VPN en el dispositivo en el que se inicia la aplicación, inicie la conexión VPN cuando la aplicación se inicie (solo Windows 8.1 y Windows Phone 8.1). Si se han implementado varios perfiles de VPN en un dispositivo de Windows 8.1, se usará de forma predeterminada el primer perfil de VPN implementado.  

         En dispositivos Windows Phone 8.1, las conexiones VPN automáticas no se admiten si se ha implementado más de un perfil de VPN en el dispositivo.  

         Para obtener más información, vea [Perfiles de VPN](../../protect/deploy-use/vpn-profiles.md).  

6.  Seleccione **Siguiente** y continúe con [Specify content options for the deployment type](/sccm/apps/deploy-use/create-applications#specify-content-options-for-the-deployment-type) (Especificar las opciones de contenido del tipo de implementación).  

#### <a name="manually-set-up-the-deployment-type-information"></a>Configurar manualmente la información del tipo de implementación  

1.  En la página **General** del Asistente para crear tipos de implementación, en la lista desplegable **Tipo**, elija el tipo de archivo de instalación de aplicación para este tipo de implementación. 

2.  Seleccione **Especificar manualmente la información del tipo de implementación** y después haga clic en **Siguiente**.

3.  En la página **Información general** del Asistente para crear tipos de implementación, especifique un nombre para el tipo de implementación. Opcionalmente, especifique una descripción y los idiomas para este tipo de implementación y, después, haga clic en **Siguiente**.  

4.  Continúe con [Especificar las opciones de contenido del tipo de implementación](/sccm/apps/deploy-use/create-applications#specify-content-options-for-the-deployment-type).  

###  <a name="specify-content-options-for-the-deployment-type"></a>Especificar las opciones de contenido del tipo de implementación  

1.  En la página **Contenido** del Asistente para crear tipos de implementación, especifique la siguiente información:  

    -   **Ubicación del contenido**: especifique la ubicación del contenido para este tipo de implementación o haga clic en **Examinar** para elegir la carpeta de contenido del tipo de implementación.  

        > [!IMPORTANT]  
        >  La cuenta del sistema del equipo del servidor de sitio debe tener permisos para la ubicación del contenido que especifique.  

    -   **Configuración del contenido de desinstalación**: especifique una de las opciones siguientes:
        - **Igual que el contenido de instalación**: seleccione esta opción si el contenido de instalación y desinstalación es el mismo. Esta opción es el valor predeterminado.
        - **Ningún contenido de desinstalación**: seleccione esta opción si la aplicación no necesita contenido para la desinstalación.
        - **Diferente del contenido de instalación**: seleccione esta opción si el contenido de desinstalación es diferente al de instalación. Después, especifique la ubicación del contenido de aplicación que se usa para desinstalar la aplicación.
5. Haga clic en **Aceptar** para cerrar el cuadro de diálogo de las propiedades del tipo de implementación.

    -   **Conservar contenido en la memoria caché del cliente**: seleccione esta opción para especificar si el cliente conserva el contenido en caché de manera indefinida. El cliente conserva el contenido incluso si la aplicación ya está instalada. Esta opción es útil en algunas implementaciones, como el software basado en Windows Installer. Windows Installer necesita una copia local del contenido de origen para aplicar las actualizaciones. Aunque esta opción reduce el espacio de caché disponible. Si se selecciona esta opción, podría posteriormente causar un error de una implementación de gran tamaño si la memoria caché no tiene espacio disponible suficiente.  

    -   **Permitir a los clientes compartir el contenido con otros clientes en la misma subred**: para reducir la carga en la red, seleccione esta opción. Los clientes descargan contenido de otros clientes locales en la red que ya han descargado y almacenado contenido en la caché. Esta opción utiliza tecnología Windows BranchCache.  

    -   **Programa de instalación**: especifique el nombre del programa de instalación y los parámetros de instalación necesarios, o bien haga clic en **Examinar** para buscar el archivo de instalación.  

    -   **Inicio de instalación en**: opcionalmente, especifique la carpeta que contiene el programa de instalación para el tipo de implementación. Esta carpeta puede ser una ruta de acceso absoluta en el cliente, o una ruta de acceso a la carpeta del punto de distribución que contiene los archivos de instalación.  

    -   **Programa de desinstalación**: opcionalmente, especifique el nombre del programa de desinstalación y los parámetros necesarios, o bien haga clic en **Examinar** para buscarlo.  

    -   **Inicio de desinstalación en**: opcionalmente, especifique la carpeta que contiene el programa de desinstalación para el tipo de implementación. Esta carpeta puede ser una ruta de acceso absoluta en el cliente. También puede ser una ruta de acceso relativa en un punto de distribución de la carpeta que contiene el paquete.  

    -   **Ejecutar programa de instalación y desinstalación como proceso de 32 bits en clientes de 64 bits**: Utilice las ubicaciones del Registro y de archivos de 32 bits en equipos basados en Windows para ejecutar el programa de instalación del tipo de implementación.  

2.  Elija **Siguiente**.  

### <a name="set-up-detection-methods-to-indicate-the-presence-of-the-deployment-type-windows-pcs-only"></a>Configurar métodos de detección para indicar la presencia del tipo de implementación (solo en PC Windows)  
 Este procedimiento configura un método de detección que indica si el tipo de implementación ya está instalado.  

1.  En la página **Método de detección** del Asistente para crear tipos de implementación, seleccione **Configurar reglas para detectar la presencia de este tipo de implementación** y, después, seleccione **Agregar cláusula**.  

    > [!NOTE]  
    >  También se puede seleccionar **Usar un script personalizado para detectar la presencia de este tipo de implementación**. Para obtener más información, consulte [Usar un script personalizado para determinar la presencia de un tipo de implementación](/sccm/apps/deploy-use/create-applications#Use-a-custom-script-to-check-for-the-presence-of-a-deployment-type).  

2.  En el cuadro de diálogo **Regla de detección** , en la lista desplegable **Tipo de configuración** , seleccione el método que desea utilizar para detectar la presencia del tipo de implementación. Puede elegir entre los siguientes métodos disponibles:  

    -   **Sistema de archivos**: detecte si una carpeta o archivo especificado existe en un dispositivo cliente. Esta detección indica que la aplicación está instalada.  

        > [!NOTE]  
        >  La opción **Sistema de archivos** no admite la especificación de una ruta de acceso UNC a un recurso compartido de red en el campo Ruta de acceso. Solo se puede especificar una ruta de acceso local en el dispositivo cliente.  
        >   
        >  Para comprobar las ubicaciones de archivos de 32 bits para la carpeta o archivo especificado, seleccione primero la opción **Este archivo o carpeta está asociado a una aplicación de 32 bits en sistemas de 64 bits**. Si no se encuentra el archivo o la carpeta, se busca en ubicaciones de 64 bits.  

    -   **Registro**: detecte si existe una clave del Registro especificada o un valor del Registro en un dispositivo cliente. Esta detección indica que la aplicación está instalada.  

        > [!NOTE]  
        >  Para comprobar las ubicaciones del Registro de 32 bits para la clave del Registro especificada, seleccione primero **La clave del Registro está asociada a una aplicación de 32 bits en sistemas de 64 bits**. Si no se encuentra la clave del Registro, se busca en ubicaciones de 64 bits.  

    -   **Windows Installer**: detecte si un archivo de Windows Installer especificado existe en un dispositivo cliente. Esta detección indica que la aplicación está instalada.  

3.  Especifique los detalles sobre el elemento para detectar si este tipo de implementación está instalado. Por ejemplo, puede utilizar un archivo, una carpeta, una clave o un valor del Registro, o un código de producto de Windows Installer.  

4.  Especifique si el elemento debe existir o cumplir una regla. Por ejemplo, si realiza la detección con un archivo, seleccione **La configuración del sistema de archivos debe existir en el sistema de destino para indicar la presencia de esta aplicación**.  

5.  Seleccione **Siguiente** para cerrar el cuadro de diálogo **Regla de detección**.  

####  <a name="use-a-custom-script-to-check-for-the-presence-of-a-deployment-type"></a>Usar un script personalizado para determinar la presencia de un tipo de implementación  

1.  En la página **Método de detección** del Asistente para crear tipos de implementación, seleccione el cuadro **Usar un script personalizado para detectar la presencia de este tipo de implementación** y, después, seleccione **Editar**.  

2.  En el cuadro de diálogo **Editor de scripts** , en la lista desplegable **Tipo de script** , seleccione el lenguaje de script que desea utilizar para detectar el tipo de implementación.  

3.  En el cuadro **Contenido del script**, escriba el script que quiere usar. También puede pegar el contenido de un script existente en este campo o seleccionar **Abrir** para ir a un script existente guardado. Configuration Manager comprueba los resultados del script. Lee los valores escritos por el script en la secuencia de salida estándar (STDOUT), la secuencia de error estándar (STDERR) y el código de salida. Si el script sale con un valor distinto de cero, se produce un error en el script y el estado de detección de la aplicación es desconocido. Si el código de salida es cero y STDOUT contiene datos, el estado de detección de la aplicación es Instalada.  

 Use la tabla siguiente para comprobar a partir de la salida de un script si una aplicación está instalada:  

|Código de salida de script|Detalles|
|--------------------------------|-----------------|
|0|**Datos leídos de STDOUT**: vacío<br /><br /> **Datos leídos de STDERR**: vacío<br /><br /> **Resultado del script**: correcto<br /><br /> **Estado de detección de la aplicación**: no instalado|  
|0|**Datos leídos de STDOUT**: vacío<br /><br /> **Datos leídos de STDERR**: no está vacío<br /><br /> **Resultado del script**: error<br /><br /> **Estado de detección de la aplicación**: desconocido|  
|0|**Datos leídos de STDOUT**: no está vacío<br /><br /> **Datos leídos de STDERR**: vacío<br /><br /> **Resultado del script**: correcto<br /><br /> **Estado de detección de la aplicación** instalado|  
|0|**Datos leídos de STDOUT**: no está vacío<br /><br /> **Datos leídos de STDERR**: no está vacío<br /><br /> **Resultado del script**: correcto<br /><br /> **Estado de detección de la aplicación** instalado|  
|Valor distinto de cero|**Datos leídos de STDOUT**: vacío<br /><br /> **Datos leídos de STDERR**: vacío<br /><br /> **Resultado del script**: error<br /><br /> **Estado de detección de la aplicación**: desconocido|  
|Valor distinto de cero|**Datos leídos de STDOUT**: vacío<br /><br /> **Datos leídos de STDERR**: no está vacío<br /><br /> **Resultado del script**: error<br /><br /> **Estado de detección de la aplicación**: desconocido|  
|Valor distinto de cero|**Datos leídos de STDOUT**: no está vacío<br /><br /> **Datos leídos de STDERR**: vacío<br /><br /> **Resultado del script**: error<br /><br /> **Estado de detección de la aplicación**: desconocido|  
|Valor distinto de cero|**Datos leídos de STDOUT**: no está vacío<br /><br /> **Datos leídos de STDERR**: no está vacío<br /><br /> **Resultado del script**: error<br /><br /> **Estado de detección de la aplicación**: desconocido|  

La tabla siguiente contiene scripts de ejemplo de Microsoft Visual Basic (VB) que puede usar para escribir sus propios scripts de detección de aplicaciones.  

|Script de muestra de Visual Basic|Descripción|  
|--------------------------------|-----------------|  
|**WScript.Quit(1)**|El script devuelve un código de salida distinto de cero, lo que indica que no pudo ejecutarse correctamente. En este caso, el estado de detección de la aplicación es desconocido.|  
|**WScript.StdErr.Write "Error de script"**<br /><br /> **WScript.Quit(0)**|El script devuelve un código de salida de cero, pero el valor de STDERR no está vacío. Este resultado indica que el script no se pudo ejecutar correctamente. En este caso, el estado de detección de la aplicación es desconocido.|  
|**WScript.Quit(0)**|El script devuelve un código de salida de cero, lo que indica que se ejecutó correctamente. Sin embargo, el valor de STDOUT está vacío, lo que indica que la aplicación no está instalada.|  
|**WScript.StdOut.Write "La aplicación está instalada"**<br /><br /> **WScript.Quit(0)**|El script devuelve un código de salida de cero, lo que indica que se ejecutó correctamente. El valor de STDOUT no está vacío, lo que indica que la aplicación está instalada.|  
|**WScript.StdOut.Write "La aplicación está instalada"**<br /><br /> **WScript.StdErr.Write "Completado"**<br /><br /> **WScript.Quit(0)**|El script devuelve un código de salida de cero, lo que indica que se ejecutó correctamente. Los valores de STDOUT y STDERR no están vacíos, lo que indica que la aplicación está instalada.|  

 > [!NOTE]  
 >  El tamaño máximo de un script es 32 kilobytes (KB).  

4.  Seleccione **Aceptar** para cerrar el cuadro de diálogo **Editor de script**.  

### <a name="specify-user-experience-options-for-the-deployment-type"></a>Especificar opciones de experiencia del usuario para el tipo de implementación  
 Esta configuración especifica cómo instala el cliente la aplicación en los dispositivos y lo que el usuario ve.  

1.  En la página **Experiencia del usuario** del Asistente para crear tipos de implementación, especifique la información siguiente:  

    -   **Comportamiento de instalación**: En la lista desplegable, seleccione una de las opciones siguientes:  

        -   **Instalar para el usuario**: la aplicación se instala solo para el usuario en el que se implementa la aplicación.  

        -   **Instalar para el sistema**: La aplicación se instala una sola vez, y está disponible para todos los usuarios.  

        -   **Instalar para el sistema si el recurso es el dispositivo; de lo contrario, instalar para el usuario**: si la aplicación se implementa en un dispositivo, el cliente la instala para todos los usuarios. Si la aplicación se implementa en un usuario, el cliente solo la instala para ese usuario.  

    -   **Requisito de inicio de sesión**: Especifique los requisitos de inicio de sesión para este tipo de implementación mediante las siguientes opciones:  

        -   **Solo cuando un usuario haya iniciado sesión**  

        -   **Tanto si un usuario ha iniciado sesión como si no**  

        -   **Solo cuando ningún usuario haya iniciado sesión**  

        > [!NOTE]  
        >  El valor predeterminado de esta opción es **Solo cuando un usuario haya iniciado sesión**. Si se selecciona **Instalar para el usuario** en la lista desplegable **Comportamiento de la instalación**, esta opción no se puede cambiar.  

    -   **Visibilidad del programa de instalación**: especifique el modo en que el tipo de implementación se ejecuta en los dispositivos cliente. Están disponibles las siguientes opciones:  

        -   **Maximizado**: El tipo de implementación se ejecuta maximizado en dispositivos cliente. Los usuarios ven toda la actividad de instalación.  

        -   **Normal**: El tipo de implementación se ejecuta en modo normal en función de los valores predeterminados del programa y del sistema. Este es el modo predeterminado.  

        -   **Minimizado**: El tipo de implementación se ejecuta en modo minimizado en dispositivos cliente. Los usuarios pueden ver la actividad de instalación en el área de notificación o en la barra de tareas.  

        -   **Oculto**: el tipo de implementación se ejecuta en modo oculto en los dispositivos cliente. Los usuarios no ven ninguna actividad de instalación.  

    -   **Permitir a los usuarios ver la instalación del programa e interactuar con la misma**: especifique si un usuario puede interactuar con la instalación del tipo de implementación para configurar las opciones de instalación.  

        > [!NOTE]  
        >  Si se selecciona la opción **Instalar para el usuario** en la lista desplegable **Comportamiento de instalación**, esta opción está habilitada de forma predeterminada.  

        > [!IMPORTANT]
        > A partir de la versión 1802, este valor es opcional cuando se selecciona el comportamiento **Instalar para el sistema**. Este cambio es principalmente para permitir que un usuario final interactúe con la instalación durante una secuencia de tareas. Por ejemplo, para ejecutar un proceso de instalación que solicite varias opciones al usuario final. En algunos instaladores de aplicaciones no se pueden silenciar los mensajes, o bien el proceso de instalación puede requerir valores de configuración específicos que solo conoce el usuario. <!--1356976-->
        > 
        > Instalar en el contexto de sistema y permitir a los usuarios interactuar con la instalación no es una configuración segura. Para obtener más información, vea [Seguridad y privacidad de la administración de aplicaciones](/sccm/apps/plan-design/security-and-privacy-for-application-management#bkmk_interact).

    -   **Duración máxima permitida de la ejecución (minutos)**: Especifica la duración máxima esperada de la ejecución del programa en el equipo cliente. Puede especificar esta configuración como un número entero mayor que cero. El valor predeterminado es 120 minutos.  

         Este valor se utiliza para:  

        -   Supervisar los resultados a partir del tipo de implementación.  

        -   Comprobar si un tipo de implementación se instala al definir ventanas de mantenimiento en los dispositivos cliente. Cuando se programa una ventana de mantenimiento, el programa solo se inicia si hay suficiente tiempo disponible en la ventana de mantenimiento según el parámetro **Tiempo de ejecución máximo permitido**.  

        > [!IMPORTANT]  
        >  Se puede producir un conflicto si el **Tiempo de ejecución máximo permitido** es mayor que la ventana de mantenimiento programada. Si el usuario configura el tiempo de ejecución máximo en un periodo superior a la duración de las ventanas de mantenimiento disponibles, ese tipo de implementación no se ejecuta.  

    -   **Tiempo de instalación estimado (minutos)**: especifique el tiempo de instalación estimado del tipo de implementación. Los usuarios ven este tiempo en el Centro de Software.  

    -   **Especificar comportamiento de reinicio específico**: especifique la acción posterior a la instalación. Están disponibles las siguientes opciones:  

        -   **Determinar comportamiento en función de códigos de retorno**: controle los reinicios en función de los códigos configurados en la pestaña Códigos de retorno. En el Centro de software se muestra **Puede ser necesario reiniciar**. Si un usuario ha iniciado sesión durante la instalación, se le solicita según la configuración de la experiencia de usuario de la implementación.  

        -   **Ninguna acción específica**: no es necesario reiniciar después de la instalación. El Centro de software notifica que no es necesario reiniciar.  
        -   **El programa de instalación de software puede forzar un reinicio del dispositivo**: Configuration Manager no controla ni inicia un reinicio, pero es posible que la instalación real lo haga sin previo aviso. Use esta opción para impedir que Configuration Manager notifique el error de instalación cuando el programa de instalación inicia un reinicio. En el Centro de software se muestra **Puede ser necesario reiniciar**.  

        -   **El cliente de Configuration Manager forzará un reinicio obligatorio del dispositivo**: Configuration Manager fuerza un reinicio del dispositivo después de una instalación correcta. El Centro de software notifica que es necesario reiniciar. Si un usuario ha iniciado sesión durante la instalación, se le solicita según la configuración de la experiencia de usuario de la implementación.

### <a name="specify-requirements-for-the-deployment-type"></a>Especificar requisitos para el tipo de implementación  

1.  En la página **Requisitos** del Asistente para crear tipos de implementación, seleccione **Agregar** para abrir el cuadro de diálogo **Crear requisito** y agregar un nuevo requisito.  

    > [!NOTE]  
    >  También puede agregar nuevos requisitos en la pestaña **Requisitos** del cuadro de diálogo **Propiedades** de *<nombre de tipo de implementación\>*.  

2.  En la lista desplegable **Categoría**, seleccione si este requisito es para un dispositivo o un usuario. Seleccione **Personalizada** para usar una condición global creada previamente. Si elige **Personalizada**, también puede seleccionar **Crear** para crear una nueva condición global. Para obtener más información sobre las condiciones globales, consulte [Cómo crear condiciones globales](../../apps/deploy-use/create-global-conditions.md).  

    > [!IMPORTANT]  
    >  Si la aplicación se implementa en una recopilación de dispositivos, el cliente omite todos los requisitos con la categoría **Usuario** y la condición **Dispositivo primario**.  
    >   
    >  Si se usó System Center 2012 R2 Configuration Manager SP1 para crear un paquete de Windows y un programa o una secuencia de tareas que tienen Windows 10 como un requisito y, después, se actualiza a System Center Configuration Manager, es posible que se quiten los requisitos de Windows 10. Para corregir este problema, vuelva a especificar los requisitos. Aunque se ha quitado el requisito de la pantalla de requisitos, se sigue procesando correctamente en los dispositivos.  

3.  En la lista desplegable **Condición** , seleccione la condición que desea usar para evaluar si el usuario o el dispositivo cumplen los requisitos de instalación. El contenido de esta lista varía según la categoría seleccionada.  

4.  En la lista desplegable **Operador**, seleccione el operador que se va a usar. Este operador compara la condición seleccionada con el valor especificado. Evalúa si el usuario o el dispositivo cumplen los requisitos de instalación. Los operadores disponibles varían según la condición seleccionada.  

    > [!IMPORTANT]  
    >  Los requisitos disponibles varían en función del tipo de dispositivo que use el tipo de implementación.  

5.  En el cuadro **Valor**, especifique los valores que se van a usar. Estos valores, junto con la condición y el operador seleccionados, evalúan si el usuario o el dispositivo cumplen los requisitos de instalación. Los valores disponibles varían según la condición y el operador seleccionados.  

6.  Seleccione **Aceptar** para guardar los requisitos y cierre el cuadro de diálogo **Crear requisito**.  

### <a name="specify-dependencies-for-the-deployment-type"></a>Especificar dependencias para el tipo de implementación  
 Las dependencias definen uno o más tipos de implementación de otra aplicación que se deben instalar antes de que se instale un tipo de implementación. Puede configurar los tipos de implementación dependientes para que se instalen automáticamente antes de la instalación de un determinado tipo de implementación.  

> [!IMPORTANT]  
>  En algunos casos, un tipo de implementación depende de un tipo de implementación que también tiene dependencias. El número máximo de dependencias admitidas en la cadena es cinco.  

1.  En la página **Dependencias** del Asistente para crear tipos de implementación, haga clic en **Agregar**.  

    > [!IMPORTANT]  
    >  También puede agregar nuevas dependencias en la pestaña **Dependencias** del cuadro de diálogo **Propiedades** de *<nombre de tipo de implementación\>*.  

2.  En el cuadro de diálogo **Agregar dependencia**, seleccione **Agregar**.  

3.  En el cuadro de diálogo **Especificar aplicación requerida** , seleccione una aplicación existente y uno de los tipos de implementación de la aplicación para utilizarlo como una dependencia.  

    > [!TIP]  
    >  Puede seleccionar **Ver** para mostrar las propiedades de la aplicación o del tipo de implementación seleccionado.  

4.  Seleccione **Aceptar** para cerrar el cuadro de diálogo **Especificar aplicación requerida**.  

5.  Si desea que una aplicación dependiente se instale automáticamente, seleccione **Instalación automática** junto a la aplicación dependiente.  

    > [!NOTE]  
    >  No es necesario implementar una aplicación dependiente para que se instale automáticamente.  

6.  En el cuadro de diálogo **Agregar dependencia** en **Nombre del grupo de dependencia**, escriba un nombre que haga referencia a este grupo de dependencias de aplicaciones.  

7.  Opcionalmente, haga clic en los botones **Aumentar prioridad** y **Reducir prioridad**. Estas acciones cambian el orden en que el cliente evalúa cada dependencia.  

8.  Seleccione **Aceptar** para cerrar el cuadro de diálogo **Agregar dependencia**.  

### <a name="confirm-the-deployment-type-settings-and-finish-the-wizard"></a>Confirmar la configuración del tipo de implementación y finalizar el asistente  

1.  Revise el **Resumen**. Pulse **Siguiente** para crear el tipo de implementación. Haga clic en **Anterior** para volver atrás y cambiar la configuración del tipo de implementación.  

2.  Una vez se haya completado la página **Progreso**, revise las acciones realizadas por el asistente y, después, seleccione **Cerrar** para finalizarlo.  

3.  Si se inició el Asistente para crear tipos de implementación desde el Asistente para crear aplicaciones, se vuelve a la página **Tipos de implementación** del Asistente para crear aplicaciones.  



## <a name="set-up-additional-options-for-deployment-types-that-contain-virtual-applications"></a>Configurar opciones adicionales para tipos de implementación que contienen aplicaciones virtuales  
 Use los procedimientos siguientes para configurar opciones adicionales para los tipos de implementación que incluyen aplicaciones virtuales.  

### <a name="set-up-content-options-for-application-virtualization-app-v-deployment-types"></a>Configurar las opciones de contenido de los tipos de implementación de Application Virtualization (App-V)  

1.  En la consola de Configuration Manager, seleccione **Biblioteca de software** > **Aplicaciones**.  

2.  En la lista **Aplicaciones**, seleccione una aplicación que tenga un tipo de implementación de App-V. Después, en la pestaña **Inicio**, en el grupo **Propiedades**, elija **Propiedades**.  

3.  En el cuadro de diálogo **Propiedades** de *<Nombre de la aplicación\>*, en la pestaña **Tipos de implementación**, elija un tipo de implementación de App-V y, después, seleccione **Editar**.  

4.  En el cuadro de diálogo **Propiedades** de *<Nombre del tipo de implementación\>*, en la pestaña **Contenido**, configure las opciones siguientes si es necesario:  

    -   **Conservar contenido en la memoria caché del cliente**: seleccione esta opción para asegurarse de que el contenido de este tipo de implementación no se elimina de la memoria caché del cliente de Configuration Manager.  

    -   **Cargar contenido en la memoria caché de App-V antes del inicio**: Seleccione esta opción para asegurarse de que todo el contenido de la aplicación virtual se carga en la memoria caché de App-V antes de iniciar la aplicación. Esta opción también garantiza que el contenido de la aplicación no está anclado en la caché. El cliente elimina el contenido según sea necesario.  

5.  Seleccione **Aceptar** para cerrar el cuadro de diálogo **Propiedades** de *<Nombre de tipo de implementación\>*.  

6.  Elija **Aceptar** para cerrar el cuadro de diálogo **Propiedades** de *<nombre de aplicación\>*.  

### <a name="set-up-publishing-options-for-app-v-deployment-types"></a>Configurar opciones de publicación de los tipos de implementación de App-V  

1.  En la consola de Configuration Manager, seleccione **Biblioteca de software** > **Aplicaciones**.  

3.  En la lista **Aplicaciones**, seleccione una aplicación que tenga un tipo de implementación de App-V. Después, en la pestaña **Inicio**, en el grupo **Propiedades**, elija **Propiedades**.  

4.  En el cuadro de diálogo **Propiedades** de *<Nombre de la aplicación\>*, en la pestaña **Tipos de implementación**, elija un tipo de implementación de App-V y, después, seleccione **Editar**.  

5.  En el cuadro de diálogo **Propiedades** de *<Nombre de tipo de implementación\>*, en la pestaña **Publicación**, seleccione los elementos de la aplicación virtual que quiere publicar.  

6.  Seleccione **Aceptar** para cerrar el cuadro de diálogo **Propiedades** de *<Nombre de tipo de implementación\>*.  

7.  Elija **Aceptar** para cerrar el cuadro de diálogo **Propiedades** de *<nombre de aplicación\>*.  



## <a name="import-an-application"></a>Importar una aplicación  
 Use el procedimiento siguiente para importar una aplicación en Configuration Manager. Para obtener más información sobre cómo exportar una aplicación, consulte [Management tasks for System Center Configuration Manager applications](../../apps/deploy-use/management-tasks-applications.md) (Tareas de administración para aplicaciones de System Center Configuration Manager).  

1.  En la consola de Configuration Manager, elija **Biblioteca de software** > **Administración de aplicaciones** > **Aplicaciones**.   

3.  En la pestaña **Inicio**, en el grupo **Crear**, seleccione **Importar aplicación**.  

4.  En la página **General** del **Asistente para importar aplicaciones**, haga clic en **Examinar**. Después, especifique una ruta de acceso de red al archivo .zip con la aplicación que se va a importar.  

5.  En la página **Contenido del archivo**, seleccione la acción que se va a realizar si la aplicación que se intenta importar es un duplicado de una aplicación existente. Puede crear una aplicación u omitir el duplicado y agregar una nueva revisión de la aplicación existente.  

6.  En la página **Resumen**, revise las acciones que se realizarán y, después, finalice el asistente.  

 La nueva aplicación se muestra en el nodo **Aplicaciones** .  

> [!TIP]  
>  El cmdlet de Windows PowerShell **Import-CMApplication** realiza la misma función que este procedimiento. Para obtener más información, vea [Import-CMApplication](https://docs.microsoft.com/powershell/module/configurationmanager/import-cmapplication?view=sccm-ps).  



##  <a name="deployment-types-supported-by-configuration-manager"></a>Tipos de implementación que admite Configuration Manager  

|Nombre de tipo de implementación|Más información|  
|--------------------------|----------------------|  
|**Windows Installer (archivo \*.msi)**|Crea un tipo de implementación desde un archivo de Windows Installer.|  
|**Paquete de aplicación de Windows (\*.appx, \*.appxbundle)**|Crea un tipo de implementación para Windows 8 o una versión posterior. Seleccione un archivo de paquete de aplicación de Windows o un paquete de agrupación de aplicaciones de Windows.|  
|**Paquete de aplicación de Windows (en la Tienda Windows)**|Crea un tipo de implementación para Windows 8 o una versión posterior. Especifique un vínculo a la aplicación en Microsoft Store o busque en la tienda para seleccionar la aplicación.<br /><br /> Para implementar la aplicación como un vínculo a Microsoft Store, establezca la configuración de directiva de grupo **Desactivar la aplicación Tienda** en **Deshabilitada** o **No configurada**. Si esta opción está habilitada, los clientes no pueden conectarse a Microsoft Store para descargar e instalar aplicaciones.<br /><br /> Los tipos de implementación de Windows 8 que usan un vínculo a un almacén siempre se evalúan antes que otros tipos de implementación, con independencia de su prioridad.|  
|**Instalador de scripts**|Crea un tipo de implementación que especifica un script que se ejecuta en dispositivos cliente para instalar contenido o realizar una acción.|  
|**Microsoft Application Virtualization 4**|Crear un tipo de implementación a partir de un manifiesto de Microsoft Application Virtualization 4|  
|**Microsoft Application Virtualization 5**|Crea un tipo de implementación de un archivo de paquete de Microsoft Application Virtualization 5.|  
|**Paquete de aplicación de Windows Phone (archivo \*.xap)**|Crea un tipo de implementación de un archivo de paquete de aplicación de Windows Phone.|  
|**Paquete de aplicación de Windows Phone (en la Tienda de Windows Phone)**|Crea un tipo de implementación mediante la especificación de un vínculo a la aplicación en la Tienda de Windows Phone.|  
|**Paquete de aplicación de iOS (archivo \*.ipa)**|Crea un tipo de implementación de un archivo de paquete de aplicación de iOS.|  
|**Paquete de aplicación de iOS en App Store**|Crea un tipo de implementación mediante la especificación de un vínculo a la aplicación de iOS en la App Store.|  
|**Paquete de aplicación de Android (archivo \*.apk)**|Crea un tipo de implementación de un archivo de paquete de aplicación de Android.|  
|**Paquete de aplicación para Android en Google Play**|Crea un tipo de implementación mediante la especificación de un vínculo a la aplicación en Google Play.|  
|**Mac OS X**|Crea un tipo de implementación para equipos Mac desde un archivo .cmmac creado mediante la herramienta CMAppUtil.<br /><br /> Se aplica solo a equipos Mac que ejecutan el cliente de Configuration Manager.|  
|**Aplicación web**|Crea un tipo de implementación que especifica un vínculo a una aplicación web. El tipo de implementación instala un acceso directo a la aplicación web en el dispositivo del usuario.<br /><br /> Si instaló Microsoft Intune Managed Browser en dispositivos iOS o Android, asegúrese de que los usuarios solo pueden usar el explorador administrado para abrir la aplicación. Use uno de los formatos siguientes cuando especifique un vínculo a la aplicación: reemplace **http:** por **http-intunemam:** o **https:** por **https-intunemam:**.<br /><br /> - **http-intunemam://<ruta de acceso a la aplicación web\>**<br /><br /> - **https-intunemam://<ruta de acceso a la aplicación web\>**<br /><br /> Puede usar los requisitos de la aplicación de Configuration Manager para garantizar que las aplicaciones que quiere asociar con el explorador administrado solo se instalan en dispositivos iOS y Android.<br /><br /> Para obtener más información sobre Intune Managed Browser, consulte [Administrar el acceso a Internet mediante directivas de explorador administrado](../../apps/deploy-use/manage-internet-access-using-managed-browser-policies.md).|  
|**Windows Installer a través de MDM (\*.msi)**|Este tipo de instalador le permite crear e implementar aplicaciones basadas en Windows Installer en equipos que ejecuten Windows 10.<br /><br /> Las consideraciones siguientes se aplican cuando se utiliza este tipo de instalador:<br><br>- Solo puede cargar un único archivo con la extensión .msi.<br /><br /> - El código de producto y la versión del producto del archivo se usan para la detección de la aplicación.<br /><br /> - Se usa el comportamiento de reinicio predeterminado de la aplicación. Configuration Manager no controla este reinicio.<br /><br /> - Se instalan paquetes MSI por usuario para un solo usuario.<br /><br /> - Se instalan paquetes MSI por equipo para todos los usuarios del dispositivo.<br /><br /> - Actualmente, los paquetes MSI de modo dual solo se instalan para todos los usuarios del dispositivo.<br /><br /> - Se admiten actualizaciones de aplicaciones cuando el código de producto MSI de cada versión es el mismo.|  



## <a name="next-steps"></a>Pasos siguientes

Después de crear una aplicación en Configuration Manager, el paso siguiente consiste en [implementar la aplicación](/sccm/apps/deploy-use/deploy-applications).