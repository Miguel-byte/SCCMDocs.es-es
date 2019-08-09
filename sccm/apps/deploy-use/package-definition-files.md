---
title: Archivos de definición del paquete
titleSuffix: Configuration Manager
description: Obtenga información sobre el uso de archivos de definición de paquetes para crear paquetes y programas en Configuration Manager
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2de963d7-ffb9-43c3-9e1d-fc992b67bebd
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: ba927286e79d88a6e034fd7eb14f5190cb1f34d6
ms.sourcegitcommit: 72faa1266b31849ce1a23d661a1620b01e94f517
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/26/2019
ms.locfileid: "68537683"
---
# <a name="package-definition-files"></a>Archivos de definición del paquete

*Se aplica a: System Center Configuration Manager (Rama actual)*

Los archivos de definición del paquete son scripts para ayudarle a automatizar la creación de [paquetes y programas](/sccm/apps/deploy-use/packages-and-programs) en Configuration Manager. Proporcionan toda la información que Configuration Manager necesita para crear un paquete y un programa, excepto la ubicación de los archivos de origen del paquete.

## <a name="about-the-package-definition-file-format"></a>Sobre el formato de archivo de definición de paquete

Cada archivo de definición del paquete es un archivo de texto ASCII o UTF-8 que utiliza el formato de archivo. ini. Contiene las secciones siguientes:  

### <a name="pdf"></a>[PDF]

Esta sección identifica el archivo como un archivo de definición de paquete. Contiene la siguiente información:  

- **Versión**: especifique la versión del formato de archivo de definición del paquete que el archivo usa. Esta versión corresponde a la versión de Configuration Manager para la que se escribió. Esta entrada es necesaria.  

### <a name="package-definition"></a>[Definición del paquete]

Especifique las propiedades del paquete y del programa. Proporciona la siguiente información:  

- **Nombre**: El nombre del paquete, de hasta 50 caracteres.  

- **Versión** (opcional): versión del paquete, de hasta 32 caracteres.  

- **Icono** (opcional): archivo que contiene el icono que se va a usar para este paquete. Si se especifica, este icono reemplaza al icono de paquete predeterminado en la consola de Configuration Manager.

- **Publisher**: El publicador del paquete, de hasta 32 caracteres.

- **Idioma**: La versión de idioma del paquete, de hasta 32 caracteres.

- **Comentario** (opcional): comentario sobre el paquete, de hasta 127 caracteres.

- **ContainsNoFiles**: esta entrada indica si el paquete tiene archivos de código fuente.  

- **Programas**: los programas definidos para este paquete. Cada nombre de programa se corresponde con un **[programa]** sección en este archivo de definición de paquete.  

    Ejemplo:  

    `Programs=Typical, Custom, Uninstall`  

- **MIFFileName**: El nombre del archivo de formato de información de administración (MIF) que contiene el estado del paquete, hasta 50 caracteres.  

- **MIFName**: el nombre del paquete para la coincidencia de MIF, hasta cincuenta caracteres.  

- **MIFVersion**: el número de versión del paquete para la coincidencia de MIF, hasta treinta y dos caracteres.  

- **MIFPublisher**: el Editor de software del paquete para la coincidencia de MIF, hasta treinta y dos caracteres.  

### <a name="program"></a>[programa]

Incluya una sección [Program] para cada programa que especifique en la entrada **programas** de la sección **[Package Definition]** . En esta sección se define cada programa. Cada sección de programa proporciona la siguiente información:  

- **Nombre**: El nombre del programa, hasta 50 caracteres. Esta entrada debe ser única dentro de un paquete.  

- **Icono** (opcional): especifique el archivo que contiene el icono que se va a usar para este programa. Este icono reemplaza el icono de programa predeterminado en la consola de Configuration Manager. El cliente también muestra este icono al implementar el programa en una colección.

- **Comentario** (opcional): comentario sobre el programa, de hasta 127 caracteres.

- **CommandLine**: especifique la línea de comandos del programa, de hasta 127 caracteres. El comando es relativa a la carpeta de origen del paquete.

- **StartIn**: especifique la carpeta de trabajo del programa, de hasta 127 caracteres. Esta entrada puede ser una ruta de acceso absoluta en el equipo cliente o una ruta de acceso relativa a la carpeta de origen del paquete.

- **Ejecutar**: especifique el modo de programa en que se ejecuta el programa. Puede especificar **minimizada**, **maximizado**, o **Hidden**. Si no incluye esta entrada, el programa se ejecuta en modo normal.  

- **AfterRunning**: especifique alguna acción especial que se produce cuando el programa se completa correctamente. Las opciones disponibles son **SMSRestart**, **ProgramRestart**, o **SMSLogoff**. Si no incluye esta entrada, el programa no ejecuta una acción especial.  

- **EstimatedDiskSpace**: especifique la cantidad de espacio en disco que requiere el programa de software para poder ejecutarse en el equipo. El valor predeterminado es **Unknown**. Puede establecer el valor como un número entero mayor o igual que cero. Si especifica un valor, incluya también las unidades del valor.  

    Ejemplo:  

    `EstimatedDiskSpace=38MB`  

- **EstimatedRunTime**: especifique la duración estimada en minutos que espera que el programa se ejecute en el equipo cliente. El valor predeterminado es **120**. Puede establecer el valor como un número entero mayor que cero o **desconocido**.  

    Ejemplo:  

    `EstimatedRunTime=25`  

- **SupportedClients**: especifique los procesadores y sistemas operativos en los que se ejecuta este programa. Separe las plataformas por comas. Si no incluye esta entrada, el cliente no comprueba las plataformas admitidas para este programa.  

- **SupportedClientMinVersionX**, **SupportedClientMaxVersionX**: especifique el intervalo de inicio a fin de los números de versiones de los sistemas operativos especificados en la entrada **SupportedClients**.  

    Ejemplo:  

    ```INI
    SupportedClients=Win NT (I386),Win NT (IA64),Win NT (x64)  
    Win NT (I386) MinVersion1=5.00.2195.4  
    Win NT (I386) MaxVersion1=5.00.2195.4  
    Win NT (I386) MinVersion2=5.10.2600.2  
    Win NT (I386) MaxVersion2=5.10.2600.2  
    Win NT (I386) MinVersion3=5.20.0000.0  
    Win NT (I386) MaxVersion3=5.20.9999.9999  
    Win NT (I386) MinVersion4=5.20.3790.0  
    Win NT (I386) MaxVersion4=5.20.3790.2  
    Win NT (I386) MinVersion5=6.00.0000.0  
    Win NT (I386) MaxVersion5=6.00.9999.9999  
    Win NT (IA64) MinVersion1=5.20.0000.0  
    Win NT (IA64) MaxVersion1=5.20.9999.9999  
    Win NT (x64) MinVersion1=5.20.0000.0  
    Win NT (x64) MaxVersion1=5.20.9999.9999  
    Win NT (x64) MinVersion2=5.20.3790.0  
    Win NT (x64) MaxVersion2=5.20.9999.9999  
    Win NT (x64) MinVersion3=5.20.3790.0  
    Win NT (x64) MaxVersion3=5.20.3790.2  
    Win NT (x64) MinVersion4=6.00.0000.0  
    Win NT (x64) MaxVersion4=6.00.9999.9999
    ```  

- **AdditionalProgramRequirements** (opcional): escriba otra información o requisitos de los equipos cliente, hasta 127 caracteres.

- **CanRunWhen**: especifique el estado de usuario que el programa requiere para ejecutarse en el equipo cliente. Los valores disponibles son **UserLoggedOn**, **NoUserLoggedOn**, o **AnyUserStatus**. El valor predeterminado es **UserLoggedOn**.  

- **UserInputRequired**: especifique si el programa requiere interacción con el usuario. Los valores disponibles son **True** o **False**. El valor predeterminado es **True**. Esta entrada se establece en **False** si **CanRunWhen** no está establecido en **UserLoggedOn**.  

- **AdminRightsRequired**: especifique si el programa requiere credenciales administrativas en el equipo para ejecutarse. Los valores disponibles son **True** o **False**. El valor predeterminado es **False**. Esta entrada se establece en **True** si **CanRunWhen** no está establecido en **UserLoggedOn**.  

- **UseInstallAccount**: especifique si el programa usa la cuenta de instalación del software cliente cuando se ejecuta en equipos cliente. De forma predeterminada, este valor es **False**. Este valor también es **False** si **CanRunWhen** está establecido en **UserLoggedOn**.  

- **DriveLetterConnection**: especifique si el programa requiere la conexión de una letra de unidad con los archivos del paquete en el punto de distribución. Puede especificar **True** o **False**. El valor predeterminado es **False**, lo que permite al programa usar una conexión de convención de nomenclatura universal (UNC). Cuando este valor se establece en **True**, el cliente usa la siguiente letra de unidad disponible, comenzando por Z: y continuando hacia atrás.  

- **SpecifyDrive** (opcional): especifique una letra de unidad que el programa necesita para conectarse a los archivos del paquete en el punto de distribución. Este valor fuerza el uso de la letra de unidad especificada para las conexiones de cliente a los puntos de distribución.

- **ReconnectDriveAtLogon**: especifique si el equipo se vuelve a conectar al punto de distribución cuando el usuario inicia sesión. Los valores disponibles son **True** o **False**. El valor predeterminado es **False**.  

- **DependentProgram**: especifique un programa de este paquete que se debe ejecutar antes del programa actual. Esta entrada usa el formato `DependentProgram=<ProgramName>`, donde `<ProgramName>` es la entrada del **nombre** de ese programa en el archivo de definición del paquete. Si no hay ningún programa dependiente, deje en blanco esta entrada.  

    Ejemplo:  

    `DependentProgram=Admin`  
    `DependentProgram=`  

- **Asignación**: especifique cómo se asigna el programa a los usuarios. Este valor puede ser:

    - **FirstUser**: solo el primer usuario que inicia sesión en el cliente ejecuta el programa
    - **EveryUser**: todos los usuarios que inician sesión ejecutan el programa

    Cuando **CanRunWhen** no está establecido en **UserLoggedOn**, esta entrada se establece en **FirstUser**.  

- **Deshabilitado**: especifique si se puede implementar este programa en los clientes. Los valores disponibles son **True** o **False**. El valor predeterminado es **False**.  


## <a name="use-a-package-definition-file"></a>Use un archivo de definición de paquete  

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Administración de aplicaciones** y seleccione el nodo **Paquetes**.  

2. En la pestaña **Inicio** de la cinta, en el grupo **Crear**, seleccione **Crear paquete a partir de definición**.  

3. En la página **definición de paquete** del **Asistente para crear paquete a partir de definición**, elija un archivo de definición de paquete existente. Para abrir un nuevo archivo de definición de paquete, elija **examinar**. Después de especificar un nuevo archivo de definición del paquete, selecciónelo en la lista **definición de paquete** .

4. En la página **Archivos de origen**, especifique la información sobre los archivos de origen necesarios para el paquete y el programa.  

5. Si el paquete requiere archivos de origen, en la página **carpeta de origen** , especifique la ubicación desde la que el sitio puede obtener los archivos de origen.  

6. Complete el asistente.  


## <a name="see-also"></a>Consulte también

[Paquetes y programas](/sccm/apps/deploy-use/packages-and-programs)
