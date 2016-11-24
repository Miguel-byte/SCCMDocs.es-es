---
title: "Herramienta de conexión de servicio | System Center Configuration Manager"
description: "Obtenga información sobre esta herramienta que le permite conectarse al servicio en la nube de Configuration Manager para cargar manualmente la información de uso."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6e4964c5-43cb-4372-9a89-b62ae6a4775c
caps.latest.revision: 11
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 5fab3a4834f30d48c5c000a7c95c7006eb8e4785


---
# <a name="use-the-service-connection-tool-for-system-center-configuration-manager"></a>Uso de la herramienta de conexión de servicio para System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Use la **herramienta de conexión de servicio** cuando los servidores de sistema de sitio de Configuration Manager no están conectados a Internet, pero quiere estar al día de las actualizaciones más recientes para Configuration Manager.  

 La herramienta le permite conectarse al servicio en la nube de Configuration Manager para cargar manualmente la información de uso de su jerarquía y descargar las actualizaciones. La carga de los datos de uso es necesaria para habilitar el servicio en la nube para proporcionar las actualizaciones correctas para su implementación.  

 **Requisitos previos para usar la herramienta de conexión de servicio:**  

-   Tener instalado un punto de conexión de servicio, que estará establecido en **Sin conexión, conexión a petición**.  

-   La herramienta se debe ejecutar desde un símbolo del sistema.  

-   Cada equipo en el que se ejecuta la herramienta (el equipo de punto de conexión de servicio y el equipo que está conectado a Internet) debe ser un sistema de x64 bits y tener instalado lo siguiente:  

    -   Los archivos de x86 y x64 de **Visual C++ Redistributable** .   De forma predeterminada, Configuration Manager instala la versión x64 en el equipo que hospeda el punto de conexión de servicio.  

         Para descargar una copia de los archivos de Visual C++, visite [Paquetes redistribuibles de Visual C++ para Visual Studio 2013](http://www.microsoft.com/download/details.aspx?id=40784) en el Centro de descarga de Microsoft.  

    -   .NET Framework 4.5.2 o una versión posterior.  

-   La cuenta que utilice para ejecutar la herramienta debe tener:
    -   Permisos de**administrador local** en el equipo que hospeda el punto de conexión de servicio (donde se ejecuta la herramienta).
    -   Permisos de**Lectura** para la base de datos del sitio.  



-   Necesitará una unidad USB con suficiente espacio libre para almacenar los archivos y las actualizaciones, u otro método para transferir archivos entre el equipo de punto de conexión de servicio y el equipo que tiene acceso a Internet. (En este escenario se supone que su sitio y los equipos administrados no tienen una conexión directa a Internet).  

**Hay tres pasos principales para usar la herramienta de conexión de servicio:**  

1.  **Preparar**: este paso coloca los datos de uso en un archivo .cab y lo almacena en una unidad USB (o la ubicación alternativa de transferencia que especifique).  

2.  **Conectar**: en este paso tiene que ejecutar la herramienta en un equipo remoto que se conecta a Internet para cargar los datos y descargar actualizaciones.  

3.  **Importar**: este paso importa actualizaciones para Configuration Manager a su sitio, por lo que puede ver e instalar actualizaciones desde la consola de Configuration Manager.  

A partir de la versión 1606, al conectarse a Microsoft puede cargar varios archivos .cab a la vez (cada uno desde una jerarquía distinta) y especificar un servidor proxy y un usuario para el servidor proxy.   

**Para cargar varios archivos .cab:**
 -  Coloque cada archivo .cab que exporte de jerarquías independientes en la misma carpeta. El nombre de cada archivo debe ser único y puede cambiarlo manualmente si lo precisa.
 -  Después, al ejecutar el comando para cargar datos a Microsoft, especifique la carpeta que contiene los archivos .cab. (Antes de la actualización 1606, solo puede cargar datos desde una única jerarquía a la vez y la herramienta requerirá que especifique el nombre del archivo .cab en la carpeta).
 -  Más adelante, cuando ejecute la tarea de importación en el punto de conexión de servicio de una jerarquía, la herramienta importa automáticamente solo los datos de esa jerarquía.  

**Para especificar un servidor proxy:**  
Puede utilizar los siguientes parámetros opcionales para especificar un servidor proxy (para más información acerca del uso de estos parámetros, consulte la sección de parámetros de línea de comandos de este tema):
  - **-proxyserveruri [FQDN_de_servidor_proxy]**  Utilice este parámetro para especificar el servidor proxy para esta conexión.
  -  **-proxyusername [nombreDeUsuario]**  Utilice este parámetro cuando deba especificar un usuario para el servidor proxy.



## <a name="use-the-service-connection-tool"></a>Uso de la herramienta de conexión de servicio  

 Encontrará la herramienta de conexión de servicio (**serviceconnectiontool.exe**) en los medios de instalación de Configuration Manager, en la carpeta **%path%\smssetup\tools\ServiceConnectionTool**. Use siempre la herramienta de conexión de servicio que coincida con la versión de Configuration Manager que use.


 En este procedimiento, los ejemplos de línea de comandos usan los siguientes nombres de archivo y ubicaciones de carpeta (no es necesario usar estas rutas de acceso y nombres de archivo, puede usar otros alternativos en su lugar que coincidan con su entorno y preferencias):  

-   La ruta de acceso a un Stick USB donde se almacenan los datos para la transferencia entre servidores: **D:\USB\\**  

-   El nombre del archivo .cab que contiene los datos exportados desde su sitio: **UsageData.cab**  

-   El nombre de la carpeta vacía donde se almacenarán las actualizaciones descargadas de Configuration Manager para la transferencia entre servidores: **UpdatePacks**  

En el equipo que hospeda el punto de conexión de servicio:  

-   Abra un símbolo del sistema con privilegios administrativos y, a continuación, cambie los directorios a la ubicación que contiene **serviceconnectiontool.exe**.  

     De forma predeterminada, encontrará esta herramienta en los medios de instalación de Configuration Manager, en la carpeta **%path%\smssetup\tools\ServiceConnectionTool**. Todos los archivos en esta carpeta deben estar en la misma carpeta para que funcione la herramienta de conexión de servicio.  

Al ejecutar el comando siguiente, la herramienta prepara un archivo .cab que contiene la información de uso y la copia a una ubicación que especifique. Los datos del archivo .cab se basan en el nivel de datos de uso de diagnóstico que recopilará el sitio de acuerdo con su configuración. (consulte [Diagnostics and usage data for System Center Configuration Manager](../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md) [Diagnósticos y datos de uso para System Center Configuration Manager]).  Ejecute el siguiente comando para crear el archivo .cab:  

-   **serviceconnectiontool.exe -prepare -usagedatadest D:\USB\UsageData.cab**  

También necesitará copiar la carpeta ServiceConnectionTool con todo su contenido en la unidad USB o, de lo contrario, habilitarla en el equipo que utilizará para los pasos 3 y 4.  

#### <a name="to-use-the-service-connection-tool"></a>Para usar la herramienta de conexión de servicio  

1.  En el equipo que hospeda el punto de conexión de servicio:  

    -   Abra un símbolo del sistema con privilegios administrativos y, a continuación, cambie los directorios a la ubicación que contiene **serviceconnectiontool.exe**.   

2.  Ejecute el comando siguiente para que la herramienta prepare un archivo .cab que contiene la información de uso y la copia a una ubicación que especifique:  

    -   **serviceconnectiontool.exe -prepare -usagedatadest D:\USB\UsageData.cab**  

    Si va a cargar los archivos .cab de más de una jerarquía al mismo tiempo, cada archivo .cab de la carpeta debe tener un nombre único. Puede cambiar manualmente el nombre de los archivos que agregue a la carpeta.

    Si desea ver la información de uso que se recopila para cargarse en el servicio en la nube de Configuration Manager, ejecute el siguiente comando para exportar los mismos datos como un archivo .csv que puede ver con una aplicación como Excel:  

    -   **serviceconnectiontool.exe -export -dest D:\USB\UsageData.csv**  

3.  Una vez completado el paso de preparación, mueva la unidad USB (o transfiera los datos exportados mediante otro método) a un equipo que tenga acceso a Internet.  

4.  En el equipo con acceso a Internet, abra un símbolo del sistema con privilegios administrativos y, a continuación, cambie los directorios a la ubicación que contiene una copia de la herramienta  **serviceconnectiontool.exe** y los archivos adicionales de esa carpeta.  

5.  Ejecute el siguiente comando para iniciar la carga de información de uso y la descarga de actualizaciones de Configuration Manager:  

    -   **serviceconnectiontool.exe -connect -usagedatasrc D:\USB -updatepackdest D:\USB\UpdatePacks**

    Para obtener más ejemplos de esta línea de comandos, consulte la sección [Opciones de línea de comandos](../../../core/servers/manage/use-the-service-connection-tool.md#bkmk_cmd) más adelante en este tema.

    > [!NOTE]  
    >  Cuando se ejecuta la línea de comandos para conectar con el servicio en la nube de Configuration Manager, podría producirse un error similar al siguiente:  
    >   
    >  -   Excepción no controlada: System.UnauthorizedAccessException:  
    >   
    >      El acceso a la ruta de acceso 'C:\  
    >     Users\br\AppData\Local\Temp\extractmanifestcab\95F8A562.sql' se ha denegado.  
    >   
    > Este error puede omitirse sin problemas, puede cerrar la ventana de error y continuar.  

6.  Cuando se complete la descarga de actualizaciones para Configuration Manager, mueva la unidad USB (o transfiera los datos exportados mediante otro método) al equipo que hospeda el punto de conexión de servicio.  

7.  En el equipo que hospeda el punto de conexión de servicio, abra un símbolo del sistema con privilegios administrativos, cambie los directorios a la ubicación que contiene **serviceconnectiontool.exe**y, a continuación, ejecute el siguiente comando:  

    -   **serviceconnectiontool.exe -import -updatepacksrc D:\USB\UpdatePacks**  

8.  Una vez finalizada la importación, puede cerrar el símbolo del sistema. (Solo se importan las actualizaciones para la jerarquía aplicable).  

9. Abra la consola de Configuration Manager y vaya a **Administración** >**Cloud Services** > **Actualizaciones y mantenimiento**. Ahora están disponibles para instalar las actualizaciones que se han importado. Para obtener más información sobre la instalación de actualizaciones, consulte [Install in-console updates for System Center Configuration Manager](../../../core/servers/manage/install-in-console-updates.md) (Instalación de actualizaciones en la consola para System Center Configuration Manager).  

## <a name="a-namebkmkcmda-command-line-options"></a><a name="bkmk_cmd"></a> opciones de línea de comandos  
 Para ver la información de ayuda para la herramienta de punto de conexión de servicio, abra el símbolo del sistema para la carpeta que contiene la herramienta y ejecute el comando:  **serviceconnectiontool.exe**.  

|Opciones de línea de comandos|Detalles|  
|---------------------------|-------------|  
|**-prepare -usagedatadest [unidad:][ruta][nombrearchivo.cab]**|Este comando almacena los datos de uso actuales en un archivo .cab.<br /><br /> Ejecute este comando como **administrador local** en el servidor que hospeda el punto de conexión de servicio.<br /><br /> Ejemplo:   **-prepare -usagedatadest D:\USB\Usagedata.cab**|    
|**-connect -usagedatasrc [unidad:][rutaAcceso] -updatepackdest [unidad:][rutaAcceso] -proxyserveruri [nombreCompletoServidorProxy] -proxyusername [nombreUsuario]** <br /> <br /> Si utiliza una versión de Configuration Manager anterior a 1606, debe especificar el nombre del archivo .cab y no podrá utilizar las opciones de un servidor proxy.  Los parámetros de comando admitidos son los siguientes: <br /> **connect -usagedatasrc [unidad:][rutaAcceso][nombreDeArchivo] -updatepackdest [unidad:][rutaAcceso]** |Este comando se conecta al servicio en la nube de Configuration Manager para cargar los archivos .cab de datos de uso desde la ubicación especificada y descargar los paquetes de actualización disponibles y el contenido de la consola. Las opciones para los servidores proxy son opcionales.<br /><br /> Ejecute este comando como **administrador local** en un equipo que pueda conectarse a Internet.<br /><br /> Ejemplo de la conexión sin un servidor proxy: **-connect -usagedatasrc D:\USB\ -updatepackdest D:\USB\UpdatePacks** <br /><br /> Ejemplo para la conexión cuando se utiliza un servidor proxy: **-connect -usagedatasrc D:\USB\Usagedata.cab -updatepackdest D:\USB\UpdatePacks -proxyserveruri itgproxy.redmond.corp.microsoft.com -proxyusername Meg** <br /><br /> Si utiliza una versión anterior a 1606, debe especificar un nombre de archivo para el archivo .cab y no se puede especificar un servidor proxy. Use la siguiente línea de comandos de ejemplo: **-connect -usagedatasrc D:\USB\Usagedata.cab -updatepackdest D:\USB\UpdatePacks**|      
|**-import -updatepacksrc [unidad:][ruta]**|Este comando importa los paquetes de actualización y el contenido de la consola que ha descargado anteriormente a la consola de Configuration Manager.<br /><br /> Ejecute este comando como **administrador local** en el servidor que hospeda el punto de conexión de servicio.<br /><br /> Ejemplo:  **-import -updatepacksrc D:\USB\UpdatePacks**|  
|**-export -dest [unidad:][ruta][nombrearchivo.csv]**|Este comando exporta los datos de uso a un archivo .csv, que puede ver.<br /><br /> Ejecute este comando como **administrador local** en el servidor que hospeda el punto de conexión de servicio.<br /><br /> Ejemplo: **-export -dest D:\USB\usagedata.csv**|  



<!--HONumber=Nov16_HO1-->


