---
title: Solución de problemas de MDT
titleSuffix: Microsoft Deployment Toolkit
description: 'Referencia de solución de problemas para Microsoft Deployment Toolkit '
ms.date: 09/09/2016
ms.prod: configuration-manager
ms.technology:
- configmgr-osd
ms.topic: article
ms.assetid: 91a7a69a-deac-4b0f-aac9-b7bd187c53fb
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: efb65086878a46bfb3485fdd8b0be6f613225261
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2018
---
# <a name="troubleshooting-reference-for-the-microsoft-deployment-toolkit"></a>Referencia de solución de problemas para Microsoft Deployment Toolkit
 La implementación de sistemas operativos y aplicaciones, así como la migración de estado de usuarios puede ser una tarea muy difícil, incluso cuando se está equipado con las herramientas y las instrucciones adecuadas. Esta referencia, que forma parte de Microsoft® Deployment Toolkit (MDT) 2013, proporciona información sobre los problemas conocidos actuales, posibles soluciones para estos problemas e instrucciones para solucionarlos.  

> [!NOTE]
>  En este documento, *Windows* se aplica a los sistemas operativos Windows 8.1, Windows 8, Windows 7, Windows Server 2012 R2, Windows Server 2012 y Windows Server 2008 R2, a menos que se indique lo contrario. MDT no es compatible con las versiones de Windows basadas en el procesador ARM. Del mismo modo, *MDT* hace referencia a MDT 2013, a menos que se indique lo contrario.  

> [!NOTE]
>  Microsoft Diagnostics and Recovery Toolset (DaRT) contiene herramientas eficaces para la recuperación y solución de problemas de los equipos cliente que no se inician o que se han vuelto inestables. Puede usar DaRT para determinar la causa de un fallo, restaurar archivos perdidos y así sucesivamente. También puede usar DaRT como herramienta de solución de problemas al desarrollar e implementar un sistema operativo Windows. Por ejemplo, si una imagen integrada no se inicia correctamente, puede iniciar el equipo cliente que contiene la imagen mediante el uso del disco de reparación de emergencia, que consiste en un entorno de diagnóstico. Después puede explorar el disco duro del equipo cliente, ver el registro de eventos, quitar actualizaciones, cambiar la configuración del sistema operativo, entre otras acciones. DaRT forma parte de Microsoft Desktop Optimization Pack para Software Assurance. Para saber más sobre DaRT, vea [http://www.microsoft.com/windows/enterprise/products-and-technologies/mdop/dart.aspx](http://www.microsoft.com/windows/enterprise/products-and-technologies/mdop/dart.aspx).  

## <a name="understanding-logs"></a>Comprender los registros  
 Para poder empezar a solucionar problemas de MDT de manera eficaz, debe comprender claramente los distintos archivos .log que se usan durante una implementación del sistema operativo. Cuando se sabe en qué archivos de registro se puede buscar determinada condición de error y en qué momento, aquellos problemas que parecían misteriosos y difíciles de comprender se vuelven claros y comprensibles.  

 El formato de archivo de registro de MDT está diseñado para ser leído por Trace32, que forma parte de System Center Configuration Manager 2007 Toolkit V2, disponible para descargarlo desde el [Centro de descarga de Microsoft](http://www.microsoft.com/download/details.aspx?id=9257). Los registros también los puede leer la herramienta de registro de seguimiento (CMTrace) de Configuration Manager, que está disponible con System Center 2012 Configuration Manager y versiones posteriores. Use estas herramientas siempre que sea posible para leer los archivos de registro, porque facilita mucho más la tarea de encontrar errores.  

 En el resto de esta sección se detallan los archivos de registro creados durante la implementación, así como durante la instalación de Windows. En esta sección también se proporcionan ejemplos de cuándo se deben usar los archivos para solucionar problemas.  

### <a name="mdt-logs"></a>Registros de MDT  
 Cada script de MDT crea automáticamente archivos de registro cuando se ejecuta. Los nombres de estos archivos de registro coinciden con el nombre del script; por ejemplo, ZTIGather.wsf crea un archivo de registro denominado *ZTIGather.log*. Cada script también actualiza un archivo de registro principal común (BDD.log) que agrega el contenido de los archivos de registro creados por los scripts de MDT. Los archivos de registro de MDT residen en C:\MININT\SMSOSD\OSDLOGS durante el proceso de implementación. Según el tipo de implementación que se realice, al finalizar la implementación se mueven los archivos de registro a %WINDIR%\SMSOSD o % WINDIR%\TEMP\SMSOSD. Para las implementaciones de Lite Touch Installation (LTI), los registros empiezan en C:\MININT\SMSOSD\OSDLogs. Terminan en %WINDIR%\TEMP\DeploymentLogs cuando se completa el procesamiento de la secuencia de tareas.  

 MDT crea estos archivos de registro:  

-   **BDD.log**. Este es el archivo de registro de MDT agregado que se copia en una ubicación de red al final de la implementación si se especifica la propiedad **SLShare** en el archivo Customsettings.ini.  

-   **LiteTouch.log**. Este archivo se crea durante las implementaciones de LTI. Se encuentra en %WINDIR%\TEMP\DeploymentLogs a menos que especifique la opción **/debug:true**.  

-   **Scriptname*.log**. Este archivo se crea a partir de cada script de MDT. *Scriptname* representa el nombre del script en cuestión.  

-   **Smsts.log** Este archivo lo crea el secuenciador de tareas y describe todas las transacciones del secuenciador de tareas. Según el escenario de implementación, pueden residir en %TEMP%, %WINDIR%\System32\ccm\logs o C:\\\_SMSTaskSequence o C:\SMSTSLog.  

-   **Wizard.log**. Los asistentes de implementación crean y actualizan este archivo.  

-   **WPEinit.log**. Este archivo se crea durante el proceso de inicialización de Windows PE y resulta útil para solucionar errores producidos al iniciar Windows PE.  

-   **DeploymentWorkbench_*id*.log**. Este archivo de registro se crea en la carpeta %temp% cuando se especifica un **/debug** al iniciar Deployment Workbench.  

### <a name="configuration-manager-operating-system-deployment-logs"></a>Registros de implementación del sistema operativo en Configuration Manager  
 Para más información sobre qué archivos de registro de implementación del sistema operativo se crearon mediante Microsoft System Center 2012 R2 Configuration Manager, vea [Referencia técnica para archivos de registro en Configuration Manager](http://technet.microsoft.com/library/hh427342.aspx).  

 Cuando se ejecuta la Herramienta de migración de estado de usuario (USMT) de Windows, MDT agrega automáticamente las opciones de registro para guardar los archivos de registro de USMT en las ubicaciones de archivo de registro de MDT. Estos son los archivos de registro y cuándo se crean:  

-   **USMTEstimate.log**. Se crea al evaluar los requisitos de USMT.  

-   **USMTCapture.log**. Creado por USMT al capturar datos.  

-   **USMTRestore.log**. Creado por USMT al restaurar datos.  

 El script ZeroTouchInstallation.vbs examina automáticamente los archivos de registro del progreso de USMT en busca de errores y advertencias. El script genera el identificador de evento 41010 para Microsoft System Center Operations Manager con el siguiente resumen (donde *usmt_type* es **ESTIMATE**, **SCANSTATE** o **LOADSTATE**; *error_count* es el número total de errores encontrados, y *warning_count* es el número total de advertencias encontradas):  

```  
ZTI USMT <usmt_type> reported <error_count> errors and <warning_count> warnings  
```  

 Si el recuento de errores es mayor que 0, este evento es un tipo de error. Si el recuento de advertencias es mayor que 0 pero sin errores, el evento es un tipo de advertencia. En caso contrario, el evento es de tipo informativo.  

## <a name="identifying-error-codes"></a>Identificación de códigos de error  
En la tabla 1 se muestran los códigos de error creados por los scripts de MDT junto con una descripción de cada uno de ellos. Estos códigos de error se registran en el archivo BDD.log.  

### <a name="table-1-error-codes-and-their-description"></a>Tabla 1. Códigos de error y su descripción  

|**Código de error**|**Descripción**|  
|-|-|  
|5201|No se pudo establecer una conexión al recurso compartido de implementación. La implementación no continuará.|  
|5203|No se pudo establecer una conexión al recurso compartido de implementación. La implementación no continuará.|  
|5205|No se pudo establecer una conexión al recurso compartido de implementación. La implementación no continuará.|  
|5206|Se ha cancelado el Asistente para la implementación o no se completó correctamente. La implementación no continuará.|  
|5207|No se pudo establecer una conexión al recurso compartido de implementación. La implementación no continuará.|  
|5208|**DeploymentType** no se ha establecido. Debe establecer algún valor para **SkipWizard**.|  
|5208|No se ha podido encontrar el secuenciador de tareas de SMS. La implementación no continuará.|  
|5400|Cree el objeto: **Set *class_instance* = New *class_name***|  
|5490|Cree MSXML2.DOMDocument.|  
|5495|Cree MSXML2.DOMDocument.ParseErr.ErrCode.|  
|5496|LoadControlFile.FindFile: *ConfigFile*|  
|5601|Compruebe que existe el GUID del SO: %OSGUID%.|  
|5602|Abra el XML con el GUID del SO: %OSGUID%.|  
|5610|Compruebe el archivo.|  
|5630|Compruebe el archivo: *ImagePath*.|  
|5640|Compruebe el archivo: *ImagePath*.|  
|5641|Busque el archivo: ImageX.exe.|  
|5643|Busque Bootsect.exe.|  
|5650|Compruebe el directorio: *rutaDeOrigen*.|  
|5651|Compruebe el directorio: *rutaDeOrigen*\Plataforma.|  
|5652|Busque el archivo: bootsect.exe.|  
|6001|Compruebe la letra de unidad.|  
|6002|Compruebe la letra de unidad.|  
|6010|Haga una prueba de TSGUID.|  
|6020|Robocopy devolvió el valor: *valor*.|  
|6021|Robocopy devolvió el valor: *valor*.|  
|6101|Busque el archivo: *DeployCab*.|  
|6102|Expanda los archivos de Sysprep a partir de DEPLOY.CAB.|  
|6111|Ejecute Sysprep.exe.|  
|6121|Ejecute Sysprep.|  
|6191|Haga una prueba de **CloneTag** en el Registro para comprobar que Sysprep se ha completado.|  
|6192|Haga una prueba de **SystemSetupInProgress** en el Registro para comprobar que Sysprep se ha completado.|  
|6401|Servidor DHCP autorizado.|  
|6501|No se puede realizar la copia de seguridad del equipo porque no se ha especificado ninguna ruta de red (**recursoCompartidoDeCopiaDeSeguridad**, **directorioDeCopiaDeSeguridad**).|  
|6502|ERROR: No se puede encontrar IMAGEX; no se puede realizar la copia de seguridad.|  
|6601|GetObject(... root/wmi:BCDStore).|  
|6602|BCD.OpenStore (*BCDStore*).|  
|6701|Protectores configurados.|  
|6702|Archivos de arranque movidos.|  
|6703|Cree partición de BDE.|  
|6704|Unidad desfragmentada.|  
|6705|Reduzca la unidad.|  
|6706|Probando más de una partición.|  
|6707|Cree archivos de arranque.|  
|6708|Cifre el disco.|  
|6709|Conéctese al proveedor de WMI de MicrosoftVolumeEncryption.|  
|6710|Cifrando el disco.|  
|6711|**ProtectKeyWithTPM**.|  
|6712|**ProtectKeyWithTPMAndPIN**.|  
|6713|**ProtectKeyWithTPMAndStartupKey**.|  
|6714|Guarde la clave externa en el archivo.|  
|6715|Proteja con la clave externa.|  
|6716|Guarde la clave externa en el archivo.|  
|6717|Proteja la clave con contraseña numérica.|  
|6718|**GetKeyProtectorNumberialP@ssword.**|  
|6718|Permita guardar la contraseña en el archivo.|  
|6719|Abra *archivoDeContraseña*.|  
|6720|Cifre la unidad.|  
|6721|Abra *archivoDeParteDeDisco*.|  
|6722|Cree partición.|  
|6723|Obtenga la unidad BDE existente.|  
|6724|Abra *archivoDeParteDeDisco*.|  
|6727|Intente abrir *archivoDeParteDeDisco*.|  
|6729|Cree un archivo de texto *archivoDeParteDeDisco*.|  
|6730|Ejecute **cmd /c DISKPART.EXE /s *archivoDeParteDeDisco* >> *rutaDeRegistro*\ZTIMarkActive_diskpart.log 2>&1**|  
|6731|Busque bcdboot.exe.|  
|6732|Conéctese al proveedor de Microsoft TPM.|  
|6733|Obtenga una instancia de TPM en la clase de proveedor.|  
|6734|Obtenga la instancia de TPM.|  
|6735|Compruebe si TPM está habilitado.|  
|6736|Compruebe si TPM está activado.|  
|6737|Compruebe si TPM tiene propietario.|  
|6738|Compruebe si se permite la propiedad de TPM.|  
|6739|Compruebe si TPM está habilitado.|  
|6740|Compruebe si TPM está activado.|  
|6741|Compruebe si TPM tiene propietario y se permite su propiedad.|  
|6741|Contraseña del propietario de TPM establecida.|  
|6742|Propietario de TPM P@ssword establecido en **AdminP@ssword**.|  
|6743|Establezca el propietario de TPM P@ssword en un valor.|  
|6744|Compruebe si TPM está habilitado.|  
|6745|Compruebe el propietario de TPM.|  
|6746|Compruebe el par de claves para su aprobación.|  
|6747|Compruebe si TPM está activado.|  
|6748|Compruebe si se permite la propiedad de TPM.|  
|6749|Convierta el propietario p@ssword a la autorización de propietario.|  
|6750|Cree el par de claves de aprobación.|  
|6751|Cambie la autorización de propietario.|  
|6752|Ejecute **Cmd**.|  
|6753|Valide TPM.|  
|6754|Obtenga la instancia de BDE.|  
|6755|Proteja la clave con TPM.|  
|6756|Busque un medio extraíble para configurar. **ProtectKeyWithTpmAndStartupKey**.|  
|6757|Proteja la clave con TMP y la clave de inicio.|  
|6758|Busque el pin de BDE.|  
|6759|Proteja la clave con TPM y pin.|  
|6760|Busque medios extraíbles para **BDEKeyLocation**.|  
|6761|Proteja con la clave externa.|  
|6762|La recuperación de P@ssword se está guardando en *archivoDeContraseña*.|  
|6764|Configure la directiva de BitLocker.|  
|7000|No se puede encontrar ZTIConfigure.xml; anulando.|  
|7001|Buscando un archivo de respuesta desatendida.|  
|7100|ERROR: Solo debe ejecutar este script en el sistema operativo completo.|  
|7101|ERROR: No hay suficientes valores suministrados para generar el archivo de respuesta de DCPromo.|  
|7102|ERROR: No se especificaron propiedades obligatorias para crear un nuevo DC de réplica.|  
|7103|ERROR: No se especificaron propiedades obligatorias para crear un nuevo dominio secundario de réplica.|  
|7104|ERROR: No se especificaron propiedades obligatorias para crear un nuevo bosque.|  
|7105|ERROR: No se especificaron propiedades obligatorias para crear un nuevo bosque.|  
|7200|No se puede configurar el servidor DHCP porque el servicio no está instalado.|  
|7201|No se pueden leer los detalles de los ámbitos; error de `GetScopeDetails()`.|  
|7202|No hay suficientes valores especificados para la creación de ámbito.|  
|7203|No hay suficientes valores proporcionados para establecer el intervalo de IP para este ámbito.|  
|7204|Ningún valor especificado para el intervalo de exclusión del ámbito.|  
|7300|No se pueden emitir comandos de DNS.|  
|7700|No es un escenario de nuevo equipo; saliendo de la partición de disco.|  
|7701|El disco no es lo suficientemente grande como para particiones de sistema y de BDE; se necesita 1,5 GB.|  
|7702|El disco no es lo suficientemente grande como para particiones de sistema y de WinRE; se necesitan 10 GB.|  
|7703|DeployRoot está en el disco número *índiceDeDisco*. Ejecutar un escenario de OEM: omitir.|  
|7704|Ejecutar un escenario de OEM: omitir.|  
|7704|No se permiten las particiones extendidas y lógicas con BitLocker.|  
|7712|Compruebe que Drive/*unidadDeVolumen* está presente. Formato.|  
|7900|Findfile: Microsoft.BDD.PnpEnum.exe.|  
|7901|**AllDrivers.Exists("*GUID*").**|  
|7904|**AllDrivers.Exists("*GUID*").**|  
|9200|Findfile(PkgMgr.exe).|  
|9601|ERROR: La tarea de restauración de estado de ZTITatoo debe ejecutarse en el sistema operativo completo; anulando.|  
|9701|El código de retorno de la estimación de USMT es distinto de cero; rc = *Error*.|  
|9702|No es posible realizar la captura del estado del usuario; no hay suficiente espacio local y no se ha especificado ninguna ruta de acceso de red (UDShare, UDDir).|  
|9703|Código de retorno distinto de cero de la captura de USMT; rc = *Error*.|  
|9704|No se especificó ninguna opción de línea de comandos válida.|  
|9801|ERROR: Al intentar implementar un sistema operativo cliente en una máquina que ejecuta un sistema operativo de servidor.|  
|9802|ERROR: Al intentar implementar un sistema operativo de servidor en una máquina que ejecuta un sistema operativo de cliente.|  
|9803|ERROR: La máquina no está autorizada para actualizarse (OSInstall =*OSInstall*); anulando.|  
|9804|ERROR: *memoria* MB de memoria es insuficiente. Se necesitan al menos *memoria* MB de memoria.|  
|9805|ERROR: La velocidad del procesador de *velocidadDeProcesador* MHz no es suficiente.  Se necesita al menos un procesador con *velocidadDeProcesador* MHz.|  
|9806|ERROR: No hay suficiente espacio disponible en *unidad*. Se necesitan *tamaño* MB más.|  
|9807|ERROR: No hay suficiente espacio disponible en *unidad*. Se necesitan *tamaño* MB más.|  
|9901|El script ZTIWindowsUpdate no debe ejecutarse en Windows PE.|  
|9902|ZTIWindowsUpdate se ha ejecutado y ha generado errores demasiadas veces. Count = *recuento*.|  
|9903|Problema inesperado al instalar el Agente de Windows Update actualizado; rc = *Error*.|  
|9904|No se pudo crear el objeto: **Microsoft.Update.Session**.|  
|9905|No se pudo crear el objeto: **Microsoft.Update.UpdateColl**.|  
|9906|No se encontró el archivo crítico *archivo*; anulando.|  
|10000|Crear objeto: **Set oLTICleanup = New LTICleanup**.|  
|10201|No se puede unir al dominio *dominio*. Detenga la instalación.|  
|10203|FindFile(LTISuspend.wsf).|  
|10204|Ejecute el programa *LTISuspend*.|  
|41024|Ejecute ImageX.|  
|52012|No se establecen todos los parámetros del asistente.|  

 El listado 1 proporciona un extracto de un archivo de registro que muestra cómo buscar el código de error. En este extracto, el código de error notificado es 5001.  

 **Listado 1. Extracto de un archivo SMSTS.log que contiene el código de Error 5001**  

```  
.  
.  
.  
The operating system installation failed. Please contact your system administrator for assistance.  

The action "Zero Touch Installation - Validation" failed with exit code 5001  
.  
.  
.  

```  

### <a name="converting-error-codes"></a>Conversión de códigos de error  
 Muchos códigos de error mostrados en los archivos de registro parecen crípticos y difíciles de correlacionar con una condición de error real. Pero en este proceso se muestra cómo convertir un código de error y obtener información significativa que puede ayudarle a resolver el problema.  

 **Problema:** Se produce un error en una captura de imagen con el código de error 0x80070040.  

 **Posible solución 1:** El código de error que se presenta tiene el formato hexadecimal que debe convertir al formato decimal. Para hacerlo, necesita una calculadora científica. La calculadora que se incluye con cualquier sistema operativo Windows vale perfectamente para esta tarea.  

 **Para convertir un código de error**  

1.  Haga clic en **Inicio** y seleccione **Todos los programas**. Elija **Accesorios** y haga clic en **Calculadora**.  

2.  En el menú **Ver**, haga clic en **Científica**.  

3.  Seleccione **Hexa** y escriba los cuatro últimos dígitos del código, en este caso, **0040**, tal y como se muestra en la figura 1.  

     ![Referencia de solución de problemas 1](media/TroubleshootingReference1.jpg "Referencia de solución de problemas 1")  
Ilustración 1. Conversión de errores  

     **Figura 1. Conversión de errores**  

     Tenga en cuenta que no se muestran ceros a la izquierda mientras la calculadora está en modo Hexadecimal.  

4.  Select **Dec**.  

     El valor hexadecimal *40* se convierte en un valor decimal de *64*.  

5.  Abra una ventana del símbolo del sistema, escriba **NET HELPMSG 64** y presione ENTRAR.  

     El comando **NET HELPMSG** convierte el código de error numérico en texto legible. En el caso del código de error que se muestra aquí, se traduce a “El nombre de red especificado ya no está disponible”.  

 Esta información indica que puede que haya un problema de red en el equipo de destino o entre el equipo de destino y el servidor donde se encuentra el recurso compartido de implementación. El problema puede consistir en que los controladores de red no están instalados correctamente o que la velocidad y la configuración de dúplex no coinciden.  

 **Posible solución 2:** Use la utilidad de búsqueda de códigos de error de Microsoft Exchange Server. Esta utilidad de la línea de comandos le ayudará a traducir los códigos de error. Puede descargarla del [Centro de descargas de Microsoft](http://www.microsoft.com/download/details.aspx?id=985).  

### <a name="review-of-sample-logs"></a>Revisión de registros de ejemplo  
 MDT crea archivos de registro que se pueden usar para solucionar problemas en el proceso de implementación de MDT. En las siguientes secciones se proporcionan ejemplos de cómo usar los archivos de registro de MDT para solucionar problemas durante el proceso de implementación:  

-   Problemas relacionados con errores de acceso a la base de datos de MDT, como se describe en [Error al acceder a la base de datos](#FailuretoAccesstheDatabase)  

####  <a name="FailuretoAccesstheDatabase"></a> Error al acceder a la base de datos  
 **Problema:** Se produce un error al ejecutar una implementación que usó el archivo CustomSettings.ini que contiene varias secciones y especifica, mediante la propiedad **Priority**, la prioridad de procesamiento de cada sección. BDD.log contiene estos mensajes de error:  

-   ```  
    ERROR - Opening Record Set (Error Number = -2147217911) (Error Description: The SELECT permission was denied on the object 'ComputerAdministrators', database 'AdminDB', schema 'dbo'.)  
    ```  

-   ```  
    ADO error: The SELECT permission was denied on the object 'ComputerAdministrators', database 'AdminDB', schema 'dbo'. (Error #-2147217911; Source: Microsoft OLE DB Provider for SQL Server; SQL State: 42000; NativeError: 229  
    ```  

-   ```  
    ERROR - Unhandled error returned by ZTIGather: Object required (424)  
    ```  

> [!NOTE]
>  Para mayor claridad, el contenido del archivo de registro anterior se ha representado tal y como aparece al visualizarlo mediante el programa Trace32.  

 **Posible solución:** El problema, como se indicó en la primera línea del ejemplo de archivo de registro, es que se denegó el permiso para acceder a la base de datos. Por lo tanto, el script no puede establecer una conexión segura a la base de datos, posiblemente porque no había ningún identificador de usuario y contraseña. Como resultado, se intentó acceder a la base de datos a través de la cuenta de equipo. La manera más fácil de solucionar este problema es conceder a todos los usuarios el acceso de lectura a la base de datos.  

## <a name="troubleshooting"></a>Solución de problemas  
 Antes de embarcarse a fondo en procesos de solución de problemas, revise estos elementos y asegúrese de que se cumplen los requisitos relacionados:  

-   Si no se cumplen todos los requisitos previos de software y hardware, pueden producirse problemas de instalación.  

### <a name="application-installation"></a>Instalación de la aplicación  
 Revise los problemas relacionados con la instalación de aplicaciones y sus soluciones:  

-   Archivos de origen de la instalación que están bloqueados por motivos de seguridad, como se describe en [Archivos ejecutables bloqueados](#BlockedExecutables)  

-   Pérdida de conectividad de red, como se describe en [Conexiones de red perdidas](#LostNetworkConnections)  

-   Error de instalación 30029 al instalar el sistema Microsoft Office 2007 o los archivos relacionados, como se describe en [Sistema Microsoft Office 2007](#MicrosoftOfficeSystem)  

####  <a name="BlockedExecutables"></a> Archivos ejecutables bloqueados  
 **Problema:** Si los archivos de origen de instalación se descargan de Internet, es probable que se marquen con uno o más flujos de datos del sistema de archivos NTFS. Para saber más sobre los flujos de datos NTFS, vea [Flujos de archivos](http://msdn2.microsoft.com/library/aa364404\(VS.85\).aspx). La existencia de flujos de datos del sistema de archivos NTFS puede provocar que se muestre un mensaje **Abrir archivo - Advertencia de seguridad**. La instalación no continuará hasta que haga clic en **Ejecutar** en el símbolo del sistema.  

 En la figura 2 se muestran los flujos de datos del sistema de archivos NTFS que usan el comando **More** y la [utilidad Streams](http://technet.microsoft.com/sysinternals/bb897440.aspx).  

 ![Referencia de solución de problemas 2](media/TroubleshootingReference2.jpg "Referencia de solución de problemas 2")  
Figura 2. Flujos de datos NTFS  

 **Figura 2. Flujos de datos NTFS**  

 **Posible solución 1:** Haga clic con el botón derecho en el archivo de origen de la instalación y, después, haga clic en **Propiedades**. Haga clic en **Desbloquear** luego en **Aceptar** para quitar los flujos de datos del sistema de archivos NTFS del archivo. Repita este proceso para cada archivo de origen de la instalación que esté bloqueado por la existencia de uno o más flujos de datos del sistema de archivos NTFS.  

 **Posible solución 2:** Use la utilidad Streams, como se muestra en la figura 2 con referencia \_Ref308173670 \\h, para quitar los flujos de datos del sistema de archivos NTFS del archivo de origen de la instalación. La utilidad Streams puede quitar flujos de datos del sistema de archivos NTFS de uno o más archivos o carpetas a la vez.  

####  <a name="LostNetworkConnections"></a> Conexiones de red perdidas  
 **Problema:** Puede producirse un error de instalación si se instalan controladores de dispositivos o se alteran las configuraciones de red y de dispositivo. Estos cambios pueden dar lugar a un lapso en la conectividad de red que provoca un error en la instalación.  

 **Posible solución:** Implemente el script ZTICacheUtil.vbs para habilitar la descarga y la ejecución para la instalación. Este script está diseñado para ajustar el anuncio para que permita habilitar la descarga y la ejecución. La descarga usa el Servicio de transferencia inteligente en segundo plano \(BITS\) si el punto de distribución de Configuration Manager es el Sistema distribuido de creación y control de versiones web y está habilitado para BITS. Al mismo tiempo, modifica Configuration Manager para que ejecute el script ZTICache.vbs en primer lugar, lo que garantiza que el programa no se eliminará durante el proceso de implementación.  

####  <a name="MicrosoftOfficeSystem"></a> 2007 Microsoft Office system  
 **Problema:** Al implementar el sistema Microsoft Office 2007 e incluir un archivo \(MSP\) de revisión de Windows Installer, es posible que se produzca un error de instalación con el código de error 30029.  

 Si se investiga más a fondo ZTIApplications.log encontramos estos mensajes:  

-   ```  
    About to run command: \\Server\Deployment$\Tools\X86\bddrun.exe \\Server\Share\Microsoft\Office\2007\Professional\setup.exe /adminfile \\Server\Share\Microsoft\Office\2007\Professional\file.msp  
    ```  

-   ```  
    ZTI Heartbeat: command has been running for 12 minutes (process ID 1600) Return code from command = 30029  
    ```  

-   ```  
    Application Microsoft Office 2007 Professional returned an unexpected return code: 30029  
    ```  

 **Posible solución 1:** Reubique el archivo MSP en el directorio de actualizaciones y, después, ejecute setup.exe sin especificar la opción **\//adminfile**. Para más información sobre cómo implementar las actualizaciones durante la instalación, vea [Implementación de 2007 Office system](http://technet.microsoft.com/library/cc303395\(v=Office.12\).aspx).  

 **Posible solución 2:** Compruebe que el archivo MSP no tiene activada la casilla **Suprimir modal**. Para más información sobre la configuración de este valor, vea [Información general sobre la implementación de 2007 Office system](http://technet.microsoft.com/library/bb490141.aspx).  

### <a name="autologon"></a>Inicio de sesión automático  
 Revise los problemas relacionados con el inicio de sesión automático y sus soluciones:  

-   Interrupción de los procesos de implementación de LTI e instalación sin retoques \(ZTI\) debido a los banners de seguridad de inicio de sesión, tal y como se describen en [Banners de seguridad de inicio de sesión](#LogonSecutiryBanners).  

-   Interrupción de los procesos de implementación de LTI y ZTI debido a las solicitudes de credenciales de usuario, tal y como se describe en [Solicitud de credenciales de usuario](#PromtedforUserCredentials).  

####  <a name="LogonSecutiryBanners"></a> Banners de seguridad de inicio de sesión  
 **Problema:** Las secuencias de tareas de MDT se procesan durante una sesión de usuario interactivo, que requiere que el equipo de destino pueda iniciar sesión automáticamente con una cuenta administrativa especificada. Si hay un objeto de directiva de grupo \(GPO\) que aplica un banner de seguridad de inicio de sesión, este inicio de sesión automático no podrá continuar porque el banner de seguridad detiene el proceso de inicio de sesión mientras espera a que un usuario acepte la directiva indicada.  

 **Posible solución:** Asegúrese de que el GPO se aplica a las unidades organizativas específicas \(UO\) y no se incluye en el GPO del dominio predeterminado. Al agregar equipos al dominio, especifique que se agreguen a una unidad organizativa que no esté afectada por un GPO que aplica un banner de seguridad de inicio de sesión. En el Editor de secuencias de tareas, como último paso de la secuencia de tareas, incluya un script que reubique la cuenta de equipo en la unidad organizativa que quiera.  

> [!NOTE]
>  Si va a reusar cuentas de Active Directory® Domain Services \(AD DS\), asegúrese de que antes de implementar en el equipo de destino, la cuenta del equipo de destino se ha reubicado en una UO que no esté afectada por el GPO que aplica el banner de inicio de sesión de seguridad.  

####  <a name="PromtedforUserCredentials"></a> Solicitud de credenciales de usuario  
 **Problema:** Ha creado una imagen de un equipo que se ha unido al dominio. Al implementar la nueva imagen en un equipo de destino, el proceso de implementación se detiene, porque no se produce el inicio de sesión automático y se pide al usuario que indique las credenciales adecuadas. El proceso de implementación se reanuda cuando se proporcionan las credenciales y el usuario inicia sesión.  

 **Posible solución:** Al capturar imágenes, el equipo de origen no debe estar unido a un dominio. Si el equipo se unió a un dominio, debe unir el equipo a un grupo de trabajo, volver a capturar la imagen e intentar la implementación en un equipo de destino para determinar si se resuelve el problema.  

### <a name="bios"></a>BIOS  
 **Problema:** Al implementar en un equipo de destino que está equipado con la tecnología de Intel vPro, es posible que la implementación termine con un error de detención. Aunque todos los controladores actualizados se han incluido como controladores listos para usar en Deployment Workbench, el equipo de destino no se inicia.  

 Posible solución: Revise la configuración del sistema básico de entrada y salida \(BIOS\) del equipo de destino para determinar si el modo Advanced Technology Attachment está configurado como Advanced Host Controller Interface \(AHCI\). Por desgracia, algunos sistemas operativos de Windows no son compatibles con AHCI de manera predeterminada.  

### <a name="database-problems"></a>Problemas de base de datos  
 Revise los problemas relacionados con bases de datos y sus soluciones:  

-   Errores provocados por firewalls mal configurados en el servidor de base de datos, como se describe en [Solicitudes de explorador de SQL Server bloqueadas](#BlockedSQLServerBrowserRequests)  

-   Errores provocados por conexiones interrumpidas con el servidor de base de datos, como se describe en [Conexiones de canalización con nombre](#NamedPipeConnections)  

####  <a name="BlockedSQLServerBrowserRequests"></a> Solicitudes de explorador de SQL Server bloqueadas  
 **Problema:** Durante el proceso de implementación de MDT, se puede recuperar información de bases de datos de Microsoft SQL Server®. Pero pueden producirse errores relacionados con un firewall mal configurado en el servidor de base de datos.  

 **Posible solución:** Con Firewall de Windows en Windows Server puede impedir el acceso no autorizado a los recursos del equipo. Pero si el firewall está mal configurado, es posible que se bloqueen los intentos para conectarse a una instancia de SQL Server. Para acceder a una instancia de SQL Server que está detrás del firewall, configure el firewall en el equipo que ejecuta SQL Server. Para más información sobre la configuración de puertos de firewall para SQL Server, vea el artículo de Soporte técnico de Microsoft [Cómo abrir el puerto de firewall para SQL Server en Windows Server 2008](http://support.microsoft.com/kb/968872).  

####  <a name="NamedPipeConnections"></a> Conexiones de canalización con nombre  
 **Problema:** Durante el proceso de implementación de MDT, se puede recuperar información de bases de datos de SQL Server. Pero pueden producirse errores relacionados con conexiones interrumpidas de SQL Server. El motivo puede ser que no se han habilitado conexiones de canalización con nombre en Microsoft SQL Server.  

 **Posible solución:** Para resolver estos problemas, habilite canalizaciones con nombre en SQL Server. Especifique también la propiedad **SQLShare**, que es necesaria al realizar una conexión a una base de datos externa mediante canalizaciones con nombre. Cuando se conecte mediante canalizaciones con nombre, use la seguridad integrada para realizar la conexión a la base de datos. En el caso de implementaciones de LTI, la cuenta de usuario que especifique realizará la conexión a la base de datos. Para implementaciones de ZTI que usen Configuration Manager, la cuenta de acceso de red se conecta a la base de datos. Dado que Windows PE no tiene ningún contexto de seguridad de forma predeterminada, debe realizar una conexión de red al servidor de base de datos para establecer un contexto de seguridad del usuario que va a realizar la conexión.  

 El recurso compartido de red especificado por la propiedad **SQLShare** proporciona un medio para conectarse al servidor para obtener un contexto de seguridad adecuado. Debe tener acceso de lectura al recurso compartido. Después de realizar la conexión, puede establecer la conexión de canalización con nombre a la base de datos. La propiedad **SQLShare** no es necesaria y no debe usarse al realizar una conexión TCP\/IP a la base de datos.  

 Habilite las conexiones de canalización con nombre mediante estas tareas según la versión de SQL Server que esté usando:  

-   Habilite conexiones de canalización con nombre para SQL Server 2008 R2, tal y como se describe en [Habilitar conexiones de canalización con nombre en SQL Server 2008 R2](#EnableNamedPipeConnectionsinSQLServer).  

-   Habilite conexiones de canalización con nombre para SQL Server 2005, tal y como se describe en [Habilitar conexiones de canalización con nombre en SQL Server 2005](#EnableNamedPipeConnectionsinSQL).  

#####  <a name="EnableNamedPipeConnectionsinSQLServer"></a> Habilitar conexiones de canalización con nombre en SQL Server 2008 R2  
 Para habilitar conexiones de canalización con nombre en SQL Server 2008 R2, siga estos pasos:  

1.  En el equipo que ejecuta SQL Server 2008 R2 y que hospeda la base de datos que se va a consultar, haga clic en **Inicio** y elija **Todos los programas**. Seleccione **Microsoft SQL Server 2008 R2** y haga clic en **SQL Server Management Studio**.  

2.  En la consola de **Microsoft SQL Server Management Studio**, en el **Explorador de objetos**, haga clic con el botón derecho en ***nombre\_servidor\_sql*** y elija **Propiedades** \(donde *nombre\_servidor\_sql* es el nombre del equipo que ejecuta SQL Server que se va a configurar\).  

3.  Se muestra el cuadro de diálogo Propiedades del servidor \- ***nombre\_servidor\_sql***.  

4.  En el cuadro de diálogo **Propiedades del servidor** \- ***nombre\_servidor\_sql***, en **Seleccionar una página**, haga clic en **Conexiones**.  

5.  En la página **Conexiones**, compruebe que está marcada la casilla **Permitir conexiones remotas con este servidor** y haga clic en **Aceptar**.  

6.  Cierre la consola de Microsoft SQL Server Management Studio.  

7.  En el equipo que ejecuta SQL Server 2008 R2 y que hospeda la base de datos que se va a consultar, haga clic en **Inicio** y elija **Todos los programas**. Seleccione **Microsoft SQL Server 2008 R2**, elija **Herramientas de configuración** y haga clic en **SQL Server Configuration Manager**.  

8.  En la consola de **SQL Server Configuration Manager**, vaya a SQL Server Configuration Manager \(Local\) \/ Configuración de red de SQL Server \/ Protocolos para *instancia\_sql* \(donde *instancia\_sql* es el nombre de la instancia de SQL Server que se va a configurar\).  

9. En el panel de detalles, haga clic con el botón derecho en **Canalizaciones con nombre** y después en **Habilitar**.  

     Se muestra un cuadro de diálogo de advertencia que indica que se guardarán los cambios, pero no surtirán efecto hasta que se detenga el servicio y se reinicie.  

10. En el cuadro de diálogo **Advertencia**, haga clic en **Aceptar**.  

11. En la consola de **SQL Server Configuration Manager**, vaya a SQL Server Configuration Manager \(Local\) \/ SQL Server Services.  

12. En el panel de detalles, haga clic con el botón derecho en **SQL Server*\(instancia\_sql\)***, y luego en **Reiniciar** \(donde *instancia\_sql* es el nombre de la instancia de SQL Server que configuró en el paso 2\).  

     Se muestra la barra de progreso de SQL Server Configuration Manager que indica el estado de reinicio de los servicios. Una vez reiniciado el servicio, se cierra la barra de progreso.  

13. Cierre la consola de SQL Server Configuration Manager.  

 Para más información, vea [How to enable remote connections in SQL Server 2008](http://blogs.msdn.com/b/walzenbach/archive/2010/04/14/how-to-enable-remote-connections-in-sql-server-2008.aspx) (Procedimiento para habilitar conexiones remotas en SQL Server 2008).  

#####  <a name="EnableNamedPipeConnectionsinSQL"></a> Habilitar conexiones de canalización con nombre en SQL Server 2005  
 Para habilitar conexiones de canalización con nombre en SQL Server 2005, siga estos pasos:  

1.  En el equipo que ejecuta SQL Server 2005 y que hospeda la base de datos que se va a consultar, haga clic en **Inicio** y elija **Todos los programas**. Seleccione **Microsoft SQL Server 2005**, elija **Herramientas de configuración** y haga clic en **Configuración de área expuesta de SQL Server**.  

2.  En el cuadro de diálogo **Configuración de área expuesta de SQL Server 2005**, haga clic en **Configuración de superficie para servicios y conexiones**.  

3.  En el cuadro de diálogo **Configuración de superficie para servicios y conexiones – *nombre\_servidor*** \(donde *nombre\_servidor* es el nombre del equipo que ejecuta SQL Server 2005\), en **Select a component and then configure its services and connections** (Seleccionar un componente y configurar sus servicios y conexiones), vaya a MSSQLSERVER\\Database Engine y haga clic en **Conexiones remotas**.  

4.  Haga clic en **Local and remote connections** (Conexiones locales y remotas), elija **Using both  TCP\/IP and named pipes** (Usar TCP/IP y canalizaciones con nombre) y, después, haga clic en **Aplicar**.  

5.  En el cuadro de diálogo **Configuración de superficie para servicios y conexiones – *nombre\_servidor*** \(donde *nombre\_servidor* es el nombre del equipo que ejecuta SQL Server 2005\), en **Select a component and then configure its services and connections** (Seleccionar un componente y configurar sus servicios y conexiones), vaya a MSSQLSERVER\\Database Engine y haga clic en **Servicio**.  

6.  Haga clic en **Detener**.  

     Se detiene el servicio MSSQLSERVER.  

7.  Haga clic en **Iniciar**.  

     Se inicia el servicio MSSQLSERVER.  

8.  Haga clic en **Aceptar**.  

9. Cierre Configuración de área expuesta de SQL Server 2005.  

 Para más información, vea el artículo de Soporte técnico de Microsoft [Cómo configurar SQL Server 2005 para permitir conexiones remotas](http://support.microsoft.com/kb/914277).  

### <a name="deployment-scripts"></a>Scripts de implementación  
 Revise los problemas relacionados con MDT y sus soluciones:  

-   Se solicitan credenciales de usuario y se recibe el error 0x80070035, tal y como se describe en [Script de credenciales](#Credentials_script)  

-   Aparece el mensaje de error "No se encontró Wuredist.cab" como se describe en [ZTIWindowsUpdate](#ZTIWindowsUpdate)  

####  <a name="Credentials_script"></a> Script de credenciales  
 **Problema:** Durante el último inicio de un equipo recién implementado, se pide al usuario que proporcione las credenciales de usuario y es posible que reciba el error 0x80070035, lo que indica que no se encontró la ruta de acceso de red.  

 **Posible solución:** Asegúrese de que el archivo WIM no incluye una carpeta MININT o \_SMSTaskSequence. Para eliminar estas carpetas, primero use la utilidad ImageX para montar el archivo WIM y, luego, elimine las carpetas.  

> [!NOTE]
>  Si se produce un error de acceso denegado al intentar eliminar las carpetas desde el archivo WIM, abra una ventana del símbolo del sistema, cambie a la raíz de la imagen contenida en el archivo WIM y, después, ejecute **RD MININT** y **RD \_SMSTaskSequence**.  

####  <a name="ZTIWindowsUpdate"></a> ZTIWindowsUpdate  
 **Problema:** Si usa el script ZTIWindowsUpdate.wsf para aplicar actualizaciones de software durante la implementación, tenga en cuenta que este script puede comunicarse directamente con el sitio web de Microsoft Update para descargar e instalar los archivos binarios necesarios del agente de Windows Update, buscar actualizaciones de software aplicables, descargar los archivos binarios para las actualizaciones de software aplicables y, después, instalar los archivos binarios descargados. Este proceso requiere que la infraestructura de red esté configuradas para permitir que el equipo de destino obtenga acceso al sitio web de Microsoft Update.  

 Si el recurso compartido de implementación no contiene los archivos de instalación del agente de Windows Update y el equipo de destino no tiene acceso a Internet adecuado, se notifica el error "No se encontró wuredist.cab" en los archivos ZTIWindowsUpdate.log y BDD.log.  

 **Posible solución:** Siga los pasos descritos en la sección "ZTIWindowsUpdate.wsf", en el documento *Toolkit Reference* (Referencia del kit de herramientas) de MDT.  

### <a name="deployment-shares"></a>Recursos compartidos de implementación  
 Revise los problemas relacionados con los recursos compartidos de implementación y sus soluciones:  

-   Al actualizar archivos WIM se generan errores si se actualiza un recurso compartido de implementación tal y como se describe en [Error al actualizar archivos WIM](#FailuretoUpdateWIMFiles).  

####  <a name="FailuretoUpdateWIMFiles"></a> Error al actualizar archivos WIM  
 En un entorno “sencillo”:  

-   MDT normalmente recoge WIMGAPI. DLL de C:\\Windows\\system32 \(siempre en la ruta de acceso\). La versión de este WIMGAPI.DLL debe coincidir con la versión \(compilación\) del sistema operativo.  

-   En un sistema operativo de 64 bits, MDT siempre usa el archivo x64 WIMGAPI.DLL; en la ruta de acceso del sistema debe haber solo ese archivo. En un sistema operativo de 32 bits, MDT siempre usa el archivo x86 WIMGAPI.DLL; en la ruta de acceso del sistema debe haber solo ese archivo. \(Otros productos, como Configuration Manager, usan la versión de 32 bits de WIMGAPI.DLL, incluso en un sistema operativo de 64 bits, pero administran e instalan esa versión.\)  

 **Problema:** Al intentar actualizar un recurso compartido de implementación, se informa al usuario de que el montaje de uno o varios archivos .wim no se realizó correctamente.  

 **Posible solución:** Abra una ventana del símbolo del sistema y ejecute **where WIMGAPI.DLL**. Para la primera entrada de la lista \(la primera ubicación encontrada al buscar en la ruta de acceso\), asegúrese de que la propiedad **Version** coincide con la compilación de Windows Assessment and Deployment Kit \(Windows ADK\) que está instalada. Asegúrese también de que la propiedad coincide con el número de compilación del sistema operativo.  

### <a name="the-windows-deployment-wizard"></a>Asistente para implementación de Windows  
 Revise los problemas relacionados con el Asistente para implementación de Windows y sus soluciones:  

-   Las páginas del Asistente para implementación de Windows se muestran incluso cuando LTI está configurado para omitir las páginas del asistente, tal y como se describe en [No se omiten las páginas del asistente](#WizardPagesareNotSkipped).  

####  <a name="WizardPagesareNotSkipped"></a> No se omiten las páginas del asistente  
 **Problema:** Se muestra una página del asistente aunque la base de datos de MDT o el archivo CustomSettings.ini especifican que se debe omitir el asistente.  

 **Posible solución:** Para omitir correctamente una página del asistente, incluya todas las propiedades que se especificarían en esa página del asistente cuando sea necesario en la base de datos de MDT o el archivo CustomSettings.ini junto con los valores adecuados. Si una propiedad está mal configurada para una página del asistente omitida, se mostrará esta página. Para más información sobre qué propiedades se necesitan para asegurarse de que se omita una página del asistente, vea la sección "Providing Properties for Skipped Deployment Wizard Pages" (Proporcionar propiedades para las páginas omitidas del Asistente para la implementación) en el documento de MDT *Toolkit Reference* (Referencia del kit de herramientas).  

### <a name="disks-and-partitioning"></a>Discos y particiones  
 Revise los problemas relacionados con la partición de disco y sus soluciones:  

-   Problemas de Cifrado de unidad BitLocker®, tal y como se describe en [Cifrado de unidad BitLocker](#BitLockerDriveEncryption)  

-   Errores de partición de disco, tal y como se describe en Errores de particiones de disco  

-   Errores en escenarios de actualización de implementación de equipos, provocados por discos lógicos o dinámicos, tal y como se describe en [Compatibilidad con discos dinámicos y lógicos](#SupportforLoogicalandDynamicDisks)  

####  <a name="BitLockerDriveEncryption"></a> Cifrado de unidad BitLocker  
 Para implementar BitLocker se requiere una configuración específica para la implementación apropiada. Los siguientes posibles problemas pueden estar relacionados con la configuración del equipo de destino:  

-   En las implementaciones de ZTI y UDI, el script ZTIBde.wsf produce el error “No se puede abrir la clave del Registro ‘HKEY\_CURRENT\_USER\\Control Panel\\International\\LocaleName’ para su lectura”, como se describe en [Error del script ZTIBde.wsf “No se puede abrir la clave del Registro ‘HKEY_CURRENT_USER\Control Panel\International\LocaleName’ para su lectura”](#ZTIBde.wsf).  

-   Dispositivos USB, unidades de CD, unidades de DVD u otros dispositivos de medios extraíbles en el equipo de destino que aparecen como varias letras de unidad, tal y como se describe en [Los dispositivos aparecen como varias letras de unidad](#DevicesAppearasMultipleDriveLetters)  

-   Reducción de la unidad C en el equipo de destino para proporcionar suficiente espacio en disco sin asignar, tal y como se describe en [Problemas al reducir discos](#ProblemswithShrinkingDisks)  

#####  <a name="ZTIBde.wsf"></a> Error del script ZTIBde.wsf “No se puede abrir la clave del Registro ‘HKEY\_CURRENT\_USER\\Control Panel\\International\\LocaleName’ para su lectura”  
 **Problema:** Al intentar implementar BitLocker en el equipo de destino en ZTI o UDI, el script ZTIBde.wsf genera el error “No se puede abrir la clave del Registro ‘HKEY\_CURRENT\_USER\\Control Panel\\International\\LocaleName’ para lectura.”  

 **Posible solución:** Especifique la configuración regional en la propiedad **UILanguage**. En ZTI y UDI, el script ZTIBde.wsf se ejecuta en el control del sistema, por lo que no se carga un perfil de usuario completo. Cuando el script ZTIBde.wsf intenta leer la información de configuración regional, esta no está en el Registro, porque el \(perfil de usuario\) del Registro no se ha cargado completamente. Para solucionarlo, especifique la configuración regional en la propiedad **UILanguage**.  

#####  <a name="DevicesAppearasMultipleDriveLetters"></a> Los dispositivos aparecen como varias letras de unidad  
 **Problema:** Algunos dispositivos pueden aparecer como varias letras de unidad lógica, en función de cómo se hayan particionado. En algunos casos, puede emular una unidad de disquete de 1,44\- megas \(MB\) y una unidad de almacenamiento de memoria. Por lo tanto, es posible que Windows asigne las mismas letras de unidad de dispositivo A y B para la emulación de disquete y F para la unidad de almacenamiento de memoria. De forma predeterminada, los scripts de MDT usan la letra de unidad menor \(en este ejemplo, A\).  

 **Posible solución:** Invalide el valor predeterminado en la página **Specify the BitLocker recovery details** (Especificar detalles de recuperación de BitLocker) del Asistente para implementación de Windows. La página de resumen del Asistente para implementación de Windows muestra una advertencia para informar al usuario de la letra de unidad que se seleccionó para almacenar la información de recuperación de BitLocker. Además, los archivos BDD.log y ZTIBDE.log registran los dispositivos de medios extraíbles detectados y qué dispositivo se seleccionó para almacenar la información de recuperación de BitLocker.  

#####  <a name="ProblemswithShrinkingDisks"></a> Problemas al reducir discos  
 **Problema:** No hay suficiente espacio en disco sin asignar en el equipo de destino para habilitar BitLocker. Para implementar BitLocker en un equipo de destino, se necesitan al menos 2 gigas \(GB\) de disco sin asignar para crear el volumen del sistema. El *volumen del sistema* es el volumen que contiene los archivos específicos del hardware necesarios para cargar Windows después de que el BIOS haya arrancado el equipo.  

 **Posible solución 1:** En los equipos existentes, use la herramienta Diskpart para reducir la unidad C para que se puede crear el volumen del sistema. Aunque en algunos casos, la herramienta Diskpart puede reducir unidad C lo suficiente como para proporcionar los 2 GB de espacio en disco sin asignar, posiblemente porque el espacio en disco está fragmentado en la unidad C.  

 Una posible solución para este problema es desfragmentar la unidad C. Para ello, siga estos pasos:  

1.  Ejecute el comando **shrink querymax** de Diskpart para identificar la cantidad máxima de espacio en disco que puede estar sin asignar.  

2.  Si el valor devuelto en el paso 1 es inferior a 2 GB, borre cualquier archivo innecesario en la unidad C y desfragméntela.  

3.  Vuelva a ejecutar el comando **shrink querymax** de Diskpart para comprobar que hay más de 2 GB de espacio en disco sin asignar.  

4.  Si el valor devuelto en el paso 3 sigue siendo menos de 2 GB, realice una de estas tareas:  

    -   Desfragmente la unidad C varias veces para asegurarse de que está totalmente optimizada.  

    -   Haga una copia de seguridad de los datos en la unidad C, elimine la partición existente, cree una nueva partición y, después, restaure los datos en la nueva partición.  

 **Posible solución 2:** El script ZTIBDE.wsf ejecuta la herramienta de preparación de disco \(bdehdcfg.exe\) y configura el tamaño de la partición de volumen del sistema a 2 GB de forma predeterminada. Puede personalizar el script de ZTIBDE.wsf para cambiar el valor predeterminado, si es necesario. Aunque no recomendamos modificar los scripts de MDT.  

####  <a name="SupportforLoogicalandDynamicDisks"></a> Compatibilidad con discos dinámicos y lógicos  
 **Problema:** Al realizar un escenario de implementación de actualización de equipo, se puede producir un error en el proceso de implementación cuando se implementa en un equipo de destino que está usando unidades lógicas o discos dinámicos.  

 **Posible solución:** MDT no admite la implementación de sistemas operativos en unidades lógicas o en discos dinámicos.  

### <a name="domain-join"></a>Unión al dominio  
 **Problema:** Durante la implementación, use el Asistente para implementación de Windows para proporcionar toda la información necesaria para el equipo de destino, incluidas las credenciales, la información de unión de dominio y la configuración de IP estática. Cuando termine la instalación, puede ver que el sistema no se ha unido al dominio y aún está en un grupo de trabajo.  

 **Posible solución:** Una implementación de LTI de MDT configura la información de IP estática después de que el sistema operativo esté en funcionamiento. Si el equipo de destino se encuentra en un segmento de red que no tiene el protocolo de configuración dinámica de host \(DHCP\), se producirá un error en una unión de dominio automatizada especificada en Unattend.xml cuando no haya ningún DHCP.  

 Configure Unattend.xml para unirse a un grupo de trabajo. Después, use el paso de secuencia de tareas **Recover from Domain** (Recuperar desde dominio) integrado para agregar un paso en la secuencia de tareas para unirse al dominio después de haber aplicado la dirección IP estática.  

### <a name="driver-installation"></a>Instalación de controladores  
 Para garantizar la mejor experiencia posible, la instalación de dispositivos de hardware y controladores de software debe ejecutarse de la manera más eficiente posible, con poca o ninguna intervención del usuario. Microsoft proporciona herramientas e instrucciones para ayudarle a crear paquetes de instalación que cumplan este objetivo. Para obtener información general sobre la instalación de controladores, vea [Device and Driver Installation](http://www.microsoft.com/whdc/driver/install/default.mspx) (Instalación de dispositivos y controladores).  

 Revise los problemas relacionados con la instalación de controladores de dispositivos y sus soluciones:  

-   Problemas que se producen al usar controladores de almacenamiento masivo de $OEM$ con MDT, tal y como se describe en Combinar controladores de almacenamiento masivo de $OEM$ con la lógica de almacenamiento masivo de MDT  

-   Solución de problemas de instalación de controladores de dispositivos mediante el archivo SetupAPI.log, tal y como se describe en [Solucionar problemas de instalación de dispositivos con SetupAPI.log](#TroubleshootDeviceInstallationwithSetupAPI.log)  

####  <a name="TroubleshootDeviceInstallationwithSetupAPI.log"></a> Solucionar problemas de instalación de dispositivos con SetupAPI.log  
 En las notas del producto [Solucionar problemas de instalación de dispositivos con el archivo de registro SetupAPI](http://msdn.microsoft.com/windows/hardware/gg463393.aspx) se proporciona información sobre la depuración de instalación de dispositivos de Windows. En concreto, el documento proporciona instrucciones para que desarrolladores y evaluadores de controladores interpreten el archivo de registro SetupAPI.  

 Uno de los archivos de registro más útiles para depuración es el archivo SetupAPI.log. Este archivo de texto sin formato mantiene la información que SetupAPI registra sobre la instalación de dispositivos, la instalación de Service Pack y la instalación de actualizaciones. En concreto, el archivo mantiene un registro de cambios de dispositivos y controladores, además de cambios importantes del sistema a partir de la instalación de Windows más reciente. Este documento se centra en usar el archivo de registro SetupAPI para solucionar problemas de instalación de dispositivos, pero no describe las secciones del archivo de registro que están asociadas con las instalaciones de Service Pack y actualizaciones.  

### <a name="new-computer-deployments"></a>Implementaciones en equipos nuevos  
 Revise los problemas relacionados con escenarios de implementaciones en equipos nuevos y sus soluciones:  

-   Problemas al iniciar el proceso de implementación con el entorno de ejecución previo al arranque \(PXE\), tal y como se describe en [Arranque con PXE](#PXEBoot)  

####  <a name="PXEBoot"></a>Arranque con PXE  
 Para describirlo brevemente, el protocolo PXE funciona así: el equipo cliente inicia el protocolo mediante la difusión de un paquete de detección DHCP que contiene una extensión que identifica la solicitud como procedente de un equipo cliente que implementa el protocolo PXE. Suponiendo que haya disponible un servidor de arranque que implementa este protocolo extendido, el servidor de arranque envía una oferta que contiene la dirección IP del servidor que realizará el mantenimiento del cliente. El cliente usa el protocolo trivial de transferencia de archivos para descargar el archivo ejecutable desde el servidor de arranque. Por último, el equipo cliente ejecuta el programa de arranque descargado.  

 La fase inicial de este protocolo se superpone en un subconjunto de mensajes DHCP para permitir que el cliente detecte un servidor de arranque \(es decir, un servidor que ofrece archivos ejecutables para la instalación de nuevos equipos\). El equipo cliente puede aprovechar para obtener una dirección IP \(lo cual es el comportamiento esperado\), pero no es necesario que lo haga.  

 La segunda fase de este protocolo se produce entre el equipo cliente y un servidor de arranque, y usa el formato de mensaje de DHCP como un formato cómodo para la comunicación. En cualquier caso, esta segunda fase está relacionada con los servicios DHCP estándar. En las páginas siguientes se describe el proceso detallado durante la inicialización del equipo cliente de PXE.  

 Para más información sobre cómo solucionar problemas relacionados con el arranque de PXE en Servicios de implementación de Windows que se ejecutan en modo heredado o mixto, vea el artículo de Soporte técnico de Microsoft [Description of PXE Interaction Among PXE Client, DHCP, and RIS Server](http://support.microsoft.com/kb/244036) (Descripción de la interacción de PXE entre el cliente de PXE, DHCP y el servidor RIS).  

 Revise estas soluciones para los problemas de arranque de PXE:  

-   Deshabilite el registro de Windows PE para SetupAPI.log, tal y como se describe en [Deshabilitar el registro de Windows PE en Servicios de implementación de Windows](#DisableWindowsPELogginginWindowsDeploymentServices).  

-   Asegúrese de que DHCP está configurado correctamente, tal y como se describe en [Garantizar la correcta configuración de DHCP](#EnsuretheProperDHCPConfiguration).  

-   Mejore los tiempos de respuesta para asignar direcciones IP a equipos cliente de PXE, tal y como se describe en [Mejorar el tiempo de respuesta de la asignación de direcciones IP de PXE](#ImprovePXEIPAddressAssignmentResponseTime).  

#####  <a name="DisableWindowsPELogginginWindowsDeploymentServices"></a> Deshabilitar el registro de Windows PE en Servicios de implementación de Windows  
 El primer procedimiento recomendado consiste en asegurarse de que se ha deshabilitado el registro en setupapi.log.  

#####  <a name="EnsuretheProperDHCPConfiguration"></a> Garantizar la correcta configuración de DHCP  
 En función de los modelos de enrutador que se estén usando, la configuración de enrutador específica del reenvío de difusión DHCP puede admitirse para una subred \(o interfaz de enrutador\) o un host específico. Si los servidores DHCP y el equipo que ejecuta Servicios de implementación de Windows son equipos independientes, asegúrese de que los enrutadores que reenvían las difusiones DHCP están diseñados para que los servidores DHCP y los servidores de Servicios de implementación de Windows reciban las difusiones de cliente; en caso contrario, el equipo cliente no recibe una respuesta a su solicitud de arranque remoto.  

 ¿Hay un enrutador entre el equipo cliente y el servidor de instalación remota que no permite el paso de solicitudes o respuestas basadas en DHCP? Cuando el equipo cliente de Servicios de implementación de Windows y el servidor de Servicios de implementación de Windows se encuentran en subredes independientes, configure el enrutador entre los dos sistemas para reenviar paquetes DHCP al servidor de Servicios de implementación de Windows. Esta disposición es necesaria, porque los equipos cliente de Servicios de implementación de Windows detectan un servidor de Servicios de implementación de Windows mediante el uso de un mensaje de difusión DHCP. Si no se configura el reenvío de DHCP en un enrutador, las difusiones DHCP de los equipos cliente no llegan al servidor de Servicios de implementación de Windows. Este proceso de reenvío de DHCP se conoce a veces como *proxy DHCP* o *dirección IP de aplicación auxiliar* en manuales de configuración de enrutadores. Lea las instrucciones del enrutador para saber más sobre cómo configurar el reenvío de DHCP en un enrutador específico.  

#####  <a name="ImprovePXEIPAddressAssignmentResponseTime"></a> Mejorar el tiempo de respuesta de la asignación de dirección IP de PXE  
 Compruebe estos elementos si el equipo cliente de PXE está tardando mucho \(de 15 a 20 segundos\) en recuperar una dirección IP:  

-   ¿El adaptador de red en el equipo de destino y el conmutador o el enrutador están configurados a la misma velocidad \(automática, dúplex, completa, etc.\)?  

-   ¿La dirección IP del servidor de Servicios de implementación de Windows se encuentra en el archivo de aplicación auxiliar IP en el enrutador a través del cual se realiza la conexión? Si la lista de direcciones IP en el archivo de aplicación auxiliar IP es larga, ¿puede mover la dirección para el servidor de Servicios de implementación de Windows cerca de la parte superior?  

### <a name="restarting-the-deployment-process"></a>Reiniciar el proceso de implementación  
 **Problema:** Al probar y solucionar problemas de una secuencia de tareas nuevas o modificadas, puede que necesite reiniciar el equipo de destino para que el proceso de implementación puede empezar de nuevo desde el principio. Pueden producirse resultados inesperados, ya que MDT realiza un seguimiento de su progreso escribiendo datos en el disco duro; cualquier reinicio del equipo de destino hace que MDT continúe por donde se quedó en el reinicio anterior.  

 **Posible solución:** Para permitir que el proceso de implementación se reinicie desde el principio, elimine las carpetas C:\\MININT y C:\\\_SMSTaskSequence antes de reiniciar el equipo de destino.  

### <a name="sysprep"></a>Sysprep  
 Revise los problemas relacionados con Sysprep y sus soluciones:  

-   El equipo de destino no aparece en la unidad organizativa de AD DS correcta, tal y como se describe en [La cuenta de equipo está en la unidad organizativa incorrecta](#ComputerAccountisintheWrongOU).  

####  <a name="ComputerAccountisintheWrongOU"></a> La cuenta de equipo está en la unidad organizativa incorrecta  
 **Problema:** El equipo de destino está unido correctamente al dominio, pero la cuenta de equipo está en la unidad organizativa incorrecta.  

 **Posible solución 1:** Si ya hay una cuenta para el equipo de destino, la cuenta permanecerá en su unidad organizativa original. Para mover la cuenta a la unidad organizativa especificada, agregue un paso de secuencia de tareas que use una herramienta de automatización, como Microsoft Visual Basic® Scripting Edition, para mover la cuenta.  

 **Posible solución 2:** Compruebe que la unidad organizativa especificada está en el formato correcto y que existe. El formato correcto de la unidad organizativa debe ser `OU=Reception,OU=NYC,DC=Woodgrovebank,DC=com`.  

### <a name="configuration-manager"></a>Configuration Manager  
 **Problema:** El mensaje de error que se muestra en la figura 3 REF \_Ref308174600 \\h aparece cuando se intenta crear un punto de servicio PXE de Configuration Manager usando la opción **Create self\-signed PXE certificate** (Crear certificado PXE autofirmado).  

 ![ReferenciaDeSoluciónDeProblemas3](media/TroubleshootingReference3.jpg "ReferenciaDeSoluciónDeProblemas3")  
Figura SEQ Figura \\\* ÁRABE 3. Error de punto de servicio PXE  

 **Figura SEQ Figura \\\* ÁRABE 3. Error de punto de servicio PXE**  

 **Posible solución:** Si un punto de servicio PXE existía previamente en el servidor que se está configurando, es posible que el punto de servicio PXE no haya eliminado los certificados creados automáticamente cuando se desinstaló. Elimine la carpeta de certificado PXE de C:\\Documents and Settings\\*nombre\_usuario*\\Application Data\\Microsoft\\Crypto\\RSA, donde *nombre\_usuario* es el nombre del usuario que realiza la configuración actual o que llevó a cabo la configuración anterior. El asistente para nuevo rol de sitio en la consola de Configuration Manager deberá finalizar correctamente cuando se haya eliminado la carpeta.  

### <a name="task-sequences"></a>Secuencias de tareas  
 Revise los problemas relacionados con secuencias de tareas y sus soluciones:  

-   La secuencia de tareas no finaliza correctamente o tiene un comportamiento imprevisible, tal y como se describe en [La secuencia de tareas no finaliza correctamente](#TaskSequenceDoesNotFinishSuccessfully).  

-   Las secuencias de tareas del fabricante de equipos originales \(OEM\) en LTI se enumeran en las imágenes de arranque con la arquitectura de procesador opuesta, tal y como se describe en [La secuencia de tareas de OEM aparece de forma incorrecta para una imagen de arranque creada para una arquitectura de procesador distinta](#OEMTaskSequenceIncorrectlyAppearsforBootImage).  

-   El Asistente para implementación de Windows muestra el mensaje de error “Elemento de secuencia de tareas incorrecto \(GUID de SO no válido\)”, tal y como se describe en [Mensaje de elemento de secuencia de tareas incorrecto (GUID de sistema operativo no válido) en el Asistente para implementación de Windows](#BadTaskSequenceItem).  

-   Al configurar un nombre de conexión de red, se muestra el mensaje “Escriba un nombre válido para el adaptador de red”, tal y como se describe en [Aplicar configuración de red](#ApplyNetworkSettings).  

-   Problemas que se pueden producir como resultado de una configuración incorrecta de continuar en caso de error para los pasos de secuencias de tareas, tal y como se describe en [Usar Continuar en caso de error](#UseContinueonError).  

####  <a name="TaskSequenceDoesNotFinishSuccessfully"></a> La secuencia de tareas no finaliza correctamente  
 **Problema:** Es posible que la secuencia de tareas no finalice correctamente o tenga un comportamiento impredecible.  

 **Posible solución:** Es posible que el paso **Instalar sistema operativo** de la secuencia de tareas \(para LTI\) o el paso **Aplicar imagen de sistema operativo** de la secuencia de tareas \(para UDI y ZTI\) se hayan modificado después de la creación del paso de secuencia de tareas, lo que puede generar resultados impredecibles. Por ejemplo, si se creó una secuencia de tareas para implementar una imagen de Windows 8.1 de 32 bits y después se cambió el paso de secuencia de taras **Instalar sistema operativo** o el paso de secuencia de tareas **Aplicar imagen de sistema operativo** para hacer referencia a una imagen de Windows 8.1 de 64 bits, es posible que la secuencia de tareas no se ejecute correctamente.  

 Se recomienda crear una nueva secuencia de tareas para implementar una imagen de sistema operativo diferente.  

####  <a name="OEMTaskSequenceIncorrectlyAppearsforBootImage"></a> La secuencia de tareas de OEM aparece de forma incorrecta para una imagen de arranque creada para una arquitectura de procesador diferente  
 **Problema:** Una secuencia de tareas basada en una plantilla de secuencia de tareas de OEM en LTI aparece para una imagen de arranque con una arquitectura de procesador distinta. Por ejemplo, una secuencia de tareas de OEM que implementa un sistema operativo de 64 bits se muestra en una imagen de arranque de 32 bits.  

 **Posible solución:** Este es el comportamiento esperado, ya que las secuencias de tareas de OEM en LTI que no se consideran “específicas de la plataforma” siempre se mostrarán, independientemente de la arquitectura de procesador de la imagen de arranque.  

####  <a name="BadTaskSequenceItem"></a> Mensaje de elemento de secuencia de tareas incorrecto \(GUID de sistema operativo no válido\) en el Asistente para implementación de Windows  
 **Problema:** Cuando se ejecuta el Asistente para implementación de Windows, se muestra el mensaje de error “Elemento de secuencia de tareas incorrecto \(GUID de sistema operativo no válido\)”. El sistema operativo se muestra en el archivo OperatingSystem.xml, pero el sistema operativo no se muestra en el área de trabajo de implementación.  

 **Posible solución:** El origen del sistema operativo original tiene dos o más archivos WIM asociados. Se elimina una SKU que está asociada a una secuencia de tareas, pero todavía existen otras SKU para el origen del sistema operativo. Cuando la secuencia de tareas que hace referencia a la SKU eliminada se selecciona en la página del asistente **Select a task sequence to execute on this computer** (Seleccione una secuencia de tareas para ejecutar en este equipo) en el Asistente para implementación de Windows, se muestra el mensaje de error “Elemento de secuencia de tarea incorrecto \(GUID de sistema operativo no válido\)” al hacer clic en **Siguiente** en la página del asistente.  

 Para solucionar este problema, realice una de estas tareas:  

-   Quite todas las SKU del origen del sistema operativo. El Asistente para implementación de Windows tiene un comportamiento normal y no se muestra el mensaje de error.  

-   Cambie la secuencia de tareas para que use una imagen de sistema operativo diferente.  

####  <a name="ApplyNetworkSettings"></a> Aplicar configuración de red  
 **Problema:** Al configurar el nombre de conexión de red en Deployment Workbench, un error de validación mostrará el mensaje “Escriba un nombre válido para el adaptador de red”.  

 **Posible solución:** Quite cualquier espacio y caracteres no válidos en el nombre de la conexión especificada.  

####  <a name="UseContinueonError"></a> Usar Continuar en caso de error  
 Si se configura una secuencia de tareas de MDT para que no continúe en caso de error y la secuencia de tareas devuelve un error, se omiten todas las secuencias de tareas restantes en ese grupo de secuencia de tareas. Aunque sí se procesan los grupos de secuencias de tareas restantes. Tenga en cuenta lo siguiente:  

 Se han creado dos grupos de secuencias de tareas y cada grupo contiene más de un paso de secuencia de tareas:  

-   Grupo A  

    -   Paso A  

    -   Paso B  

-   Grupo B  

    -   Paso A  

    -   Paso B  

 Si un grupo A\\paso A está configurado para no continuar en caso de error, entonces el grupo A\\paso B no se procesará. Pero sí se procesarán todos los pasos de secuencia de tareas en el grupo B.  

### <a name="the-user-state-migration-tool"></a>Herramienta de migración de estado de usuario  
 Revise los problemas relacionados con USMT y sus soluciones:  

-   Es posible que los accesos directos que llevan a documentos almacenados en carpetas del recurso compartido de red no se restauren correctamente, tal y como se describe en [Faltan accesos directos de escritorio](#MissingDesktopShortcuts).  

####  <a name="MissingDesktopShortcuts"></a> Faltan accesos directos de escritorio  
 **Problema:** Al usar USMT para migrar datos de usuario, es posible que no se restauren los accesos directos que apuntan a documentos de red. Los accesos directos se capturan durante Scanstate, pero nunca se restauran en el equipo de destino durante Loadstate.  

 **Posible solución:** Edite el archivo MigUser.xml y marque como comentario la línea siguiente:  

 Original:  

```  
<include> filter='MigXmlHelper.IgnoreIrrelevantLinks()'>  
```  

 Modificada:  

```  
<include> <!-- filter='MigXmlHelper.IgnoreIrrelevantLinks()'> -->  
```  

### <a name="windows-imaging-format-files"></a>Archivos de formato de imágenes de Windows  
 Revise los problemas relacionados con WIM y sus soluciones:  

-   Se producen errores en las implementaciones de LTI y ZTI con errores de archivo WIM en el archivo BDD.log, tal y como se describe en [Archivo WIM dañado](#CorruptWIMFile).  

####  <a name="CorruptWIMFile"></a> Archivo WIM dañado  
 **Problema:** Al implementar una imagen, se produce un error en la implementación con las siguientes entradas en el archivo BDD.log:  

-   ```  
    The image \\Server\Deployment$\Operating Systems\Windows\version1.wim was not applied successfully by ImageX, rc = 2  
    ```  

-   ```  
    LTIApply COMPLETED.  Return Value = 2  
    ```  

-   ```  
    ZTI ERROR - Non-zero return code by LTIApply, rc = 2  
    ```  

 Para investigar el problema, monte el archivo WIM con ImageX que genera el error “Datos no válidos”. Si investiga más descubre que la marca de fecha del archivo .wim es muchos años antes de la fecha actual. Es posible que otro proceso, como un programa antivirus, mantuviera el archivo .wim abierto después de haberlo cerrado previamente al finalizar un proceso de lectura o escritura.  

 **Posible solución:** Restaure el archivo .wim desde un soporte físico de copia de seguridad.  

### <a name="windows-pe"></a>Windows PE  
 Revise los problemas relacionados con Windows PE y sus soluciones:  

-   No se inicia el proceso de implementación de LTI o ZTI debido a que no hay suficiente memoria RAM o a los adaptadores de red inalámbrica, tal y como se describe en [Proceso de implementación no iniciado: memoria RAM o adaptador de red inalámbrica limitados](#LimitedRamorWirelessNetworkAdapter).  

-   No se inicia el proceso de implementación de LTI o ZTI porque faltan componentes de Windows PE, tal y como se describe en [Proceso de implementación no iniciado: faltan componentes](#MissingComponents).  

-   No se inicia el proceso de implementación de LTI o ZTI porque faltan controladores de dispositivos o son incorrectos, tal y como se describe en [Proceso de implementación no iniciado: faltan controladores o son incorrectos](#MissingorIncorrectDrivers).  

####  <a name="LimitedRamorWirelessNetworkAdapter"></a> Proceso de implementación no iniciado: memoria RAM o adaptador de red inalámbrica limitados  
 **Problema:** Al implementar una imagen en determinados equipos de destino, se inicia Windows PE, se ejecuta **wpeinit**, se abre una ventana del símbolo del sistema, pero no se inicia realmente el proceso de implementación. Si soluciona el problema asignando una unidad de red desde el equipo de destino, se indica que los controladores del adaptador de red no están cargados.  

 **Posible solución 1:** El Asistente para implementación no se inicia porque no hay suficiente memoria RAM. Compruebe que el equipo de destino tiene al menos 512 MB de RAM y que ninguna memoria de vídeo compartida consume más de 64 MB de 512 MB.  

 Las versiones de Windows PE que admite MDT no pueden ejecutarse en un equipo de destino que tenga menos de 512 MB de RAM.  

 **Posible solución 2:** No incluya los controladores inalámbricos en la imagen de Windows PE.  

####  <a name="MissingComponents"></a> Proceso de implementación no iniciado: faltan componentes  
 **Problema:** Cuando se solucionan problemas de una implementación incorrecta, al revisar el archivo BDD.log se muestra esta entrada:  

```  
ERROR - Unable to create ADODB.Connection object, impossible to query SQL Server: ActiveX component can't create object (429).  
```  

 **Posible solución:** Este error puede indicar que la imagen de Windows PE no se creó mediante MDT. Si está usando Configuration Manager, no use una de las imágenes de Windows PE existentes que creó Configuration Manager; es preferible que cree una imagen mediante el asistente para importar secuencias de tareas de implementación de Microsoft.  

> [!NOTE]
>  Las imágenes de Windows PE creadas por Configuration Manager contienen componentes que admiten scripting, XML e Instrumental de administración de Windows (WMI), pero no contienen los componentes que admiten Objetos de datos Microsoft ActiveX® (ADO).  

####  <a name="MissingorIncorrectDrivers"></a> Proceso de implementación no iniciado: faltan controladores o son incorrectos  
 **Problema:** Al implementar en determinados equipos de destino, se inicia Windows PE, se ejecuta **wpeinit**, se abre una ventana del símbolo del sistema, pero no se inicia realmente el proceso de implementación. Si soluciona el problema asignando una unidad de red desde el equipo de destino, se indica que los controladores del adaptador de red no están cargados. Al revisar el archivo SetupAPI.log ubicado en *X*:\Windows\System32\Inf, se indica que Windows PE genera errores cuando está configurando el adaptador de red. Uno de estos errores es “Este controlador no está diseñado para esta plataforma”. Los controladores de la lista **Out-of-Box Drivers** (Controladores listos para usar) se han insertado en la imagen.  

 **Posible solución:** Es posible que Windows PE tenga un conflicto entre dos controladores. Al configurar los valores para la imagen de Windows PE en Deployment Workbench, cree un grupo de controladores de Windows PE que contenga solo el adaptador de red y los controladores de almacenamiento y, después, configure el recurso compartido de implementación para que use solo el grupo de controladores de Windows PE.  

## <a name="deployment-process-flow-charts"></a>Diagramas de flujo del proceso de implementación  
 En esta sección se proporcionan dos conjuntos de diagramas de flujo de MDT: uno para las implementaciones de LTI y otro para las implementaciones de ZTI con Configuration Manager. Cada diagrama de flujo muestran las tareas que se ejecutan durante ese tipo de implementación.  

 Familiarícese con los diagramas de flujo del proceso de implementación haciendo lo siguiente:  

-   Revise los diagramas de flujo del proceso de implementación de LTI, tal y como se describe en [Diagramas de flujo del proceso de implementación de LTI](#LTIDeploymentProcessFlowcharts)  

-   Revise los diagramas de flujo del proceso de implementación de ZTI, tal y como se describe en [Diagramas de flujo del proceso de implementación de ZTI](#ZTIDevelopmentProcessFlowcharts)  

###  <a name="LTIDeploymentProcessFlowcharts"></a> Diagramas de flujo del proceso de implementación de LTI  
 Se proporcionan diagramas de flujo para las siguientes fases:  

-   Validación (figura 4)  

-   Captura de estado (figuras 5 y 6)  

-   Preinstalación (figuras 7, 8 y 9)  

-   Instalación (figura 10)  

-   Postinstalación (figuras 11 y 12)  

-   Restauración de estado (figuras 13, 14, 15 y 16)  

 ![ReferenciaDeSoluciónDeProblemas4](media/TroubleshootingReference4.jpg "ReferenciaDeSoluciónDeProblemas4")  
Ilustración 4. Diagrama de flujo para la fase de validación  

 **Figura 4. Diagrama de flujo para la fase de validación**  

 ![ReferenciaDeSoluciónDeProblemas5](media/TroubleshootingReference5.jpg "ReferenciaDeSoluciónDeProblemas5")  
Figura 5. Diagrama de flujo para la fase de captura de estado (1 de 2)  

 **Figura 5. Diagrama de flujo para la fase de captura de estado (1 de 2)**  

 ![ReferenciaDeSoluciónDeProblemas6](media/TroubleshootingReference6.jpg "ReferenciaDeSoluciónDeProblemas6")  
Figura 6. Diagrama de flujo para la fase de captura de estado (2 de 2)  

 **Figura 6. Diagrama de flujo para la fase de captura de estado (2 de 2)**  

 ![ReferenciaDeSoluciónDeProblemas7](media/TroubleshootingReference7.jpg "ReferenciaDeSoluciónDeProblemas7")  
Figura 7. Diagrama de flujo para la fase de preinstalación (1 de 3)  

 **Figura 7. Diagrama de flujo para la fase de preinstalación (1 de 3)**  

 ![ReferenciaDeSoluciónDeProblemas8](media/TroubleshootingReference8.jpg "ReferenciaDeSoluciónDeProblemas8")  
Figura 8. Diagrama de flujo para la fase de preinstalación (2 de 3)  

 **Figura 8. Diagrama de flujo para la fase de preinstalación (2 de 3)**  

 ![ReferenciaDeSoluciónDeProblemas9](media/TroubleshootingReference9.jpg "ReferenciaDeSoluciónDeProblemas9")  
Figura 9. Diagrama de flujo para la fase de preinstalación (3 de 3)  

 **Figura 9. Diagrama de flujo para la fase de preinstalación (3 de 3)**  

 ![ReferenciaDeSoluciónDeProblemas10](media/TroubleshootingReference10.jpg "ReferenciaDeSoluciónDeProblemas10")  
Figura 10. Diagrama de flujo para la fase de instalación  

 **Figura 10. Diagrama de flujo para la fase de instalación**  

 ![ReferenciaDeSoluciónDeProblemas11](media/TroubleshootingReference11.jpg "ReferenciaDeSoluciónDeProblemas11")  
Figura 11. Diagrama de flujo para la fase de postinstalación (1 de 2)  

 **Figura 11. Diagrama de flujo para la fase de postinstalación (1 de 2)**  

 ![ReferenciaDeSoluciónDeProblemas12](media/TroubleshootingReference12.jpg "ReferenciaDeSoluciónDeProblemas12")  
Figura 12 Diagrama de flujo para la fase de postinstalación (2 de 2)  

 **Figura 12 Diagrama de flujo para la fase de postinstalación (2 de 2)**  

 ![ReferenciaDeSoluciónDeProblemas13](media/TroubleshootingReference13.jpg "ReferenciaDeSoluciónDeProblemas13")  
Figura 13. Diagrama de flujo para la fase de restauración de estado (1 de 4)  

 **Figura 13. Diagrama de flujo para la fase de restauración de estado (1 de 4)**  

 ![ReferenciaDeSoluciónDeProblemas14](media/TroubleshootingReference14.jpg "ReferenciaDeSoluciónDeProblemas14")  
Figura 14. Diagrama de flujo para la fase de restauración de estado (2 de 4)  

 **Figura 14. Diagrama de flujo para la fase de restauración de estado (2 de 4)**  

 ![ReferenciaDeSoluciónDeProblemas15](media/TroubleshootingReference15.jpg "ReferenciaDeSoluciónDeProblemas15")  
Figura 15. Diagrama de flujo para la fase de restauración de estado (3 de 4)  

 **Figura 15. Diagrama de flujo para la fase de restauración de estado (3 de 4)**  

 ![ReferenciaDeSoluciónDeProblemas16](media/TroubleshootingReference16.jpg "ReferenciaDeSoluciónDeProblemas16")  
Figura 16. Diagrama de flujo para la fase de restauración de estado (4 de 4)  

 **Figura 16. Diagrama de flujo para la fase de restauración de estado (4 de 4)**  

###  <a name="ZTIDevelopmentProcessFlowcharts"></a> Diagramas de flujo del proceso de implementación de ZTI  
 Se proporcionan diagramas de flujo para las siguientes fases de implementación de ZTI con Configuration Manager:  

-   Inicialización (figura 17)  

-   Validación (figura 18)  

-   Captura de estado (figura 19)  

-   Preinstalación (figura 20)  

-   Instalación (figura 21)  

-   Postinstalación (figura 22)  

-   Restauración de estado (figuras 23 y 24)  

-   Captura (figura 25)  

 ![ReferenciaDeSoluciónDeProblemas17](media/TroubleshootingReference17.jpg "ReferenciaDeSoluciónDeProblemas17")  
Figura 17. Diagrama de flujo para la fase de inicialización  

 **Figura 17. Diagrama de flujo para la fase de inicialización**  

 ![ReferenciaDeSoluciónDeProblemas18](media/TroubleshootingReference18.jpg "ReferenciaDeSoluciónDeProblemas18")  
Figura 18. Diagrama de flujo para la fase de validación  

 **Figura 18. Diagrama de flujo para la fase de validación**  

 ![ReferenciaDeSoluciónDeProblemas19](media/TroubleshootingReference19.jpg "ReferenciaDeSoluciónDeProblemas19")  
Figura 19. Diagrama de flujo para la fase de captura de estado  

 **Figura 19. Diagrama de flujo para la fase de captura de estado**  

 ![ReferenciaDeSoluciónDeProblemas20](media/TroubleshootingReference20.jpg "ReferenciaDeSoluciónDeProblemas20")  
Figura 20. Diagrama de flujo para la fase de preinstalación  

 **Figura 20. Diagrama de flujo para la fase de preinstalación**  

 ![ReferenciaDeSoluciónDeProblemas21](media/TroubleshootingReference21.jpg "ReferenciaDeSoluciónDeProblemas21")  
Figura 21. Diagrama de flujo para la fase de instalación  

 **Figura 21. Diagrama de flujo para la fase de instalación**  

 ![ReferenciaDeSoluciónDeProblemas22](media/TroubleshootingReference22.jpg "ReferenciaDeSoluciónDeProblemas22")  
Figura 22. Diagrama de flujo para la fase de postinstalación  

 **Figura 22. Diagrama de flujo para la fase de postinstalación**  

 ![ReferenciaDeSoluciónDeProblemas23](media/TroubleshootingReference23.jpg "ReferenciaDeSoluciónDeProblemas23")  
Figura 23. Diagrama de flujo para la fase de restauración de estado (1 de 2)  

 **Figura 23. Diagrama de flujo para la fase de restauración de estado (1 de 2)**  

 ![ReferenciaDeSoluciónDeProblemas24](media/TroubleshootingReference24.jpg "ReferenciaDeSoluciónDeProblemas24")  
Figura 24. Diagrama de flujo para la fase de restauración de estado (2 de 2)  

 **Figura 24. Diagrama de flujo para la fase de restauración de estado (2 de 2)**  

 ![ReferenciaDeSoluciónDeProblemas25](media/TroubleshootingReference25.jpg "ReferenciaDeSoluciónDeProblemas25")  
Figura 25. Diagrama de flujo para la fase de captura  

 **Figura 25. Diagrama de flujo para la fase de captura**  

## <a name="finding-additional-help"></a>Buscar ayuda adicional  
 Encontrará más ayuda para resolver problemas de implementación de MDT haciendo lo siguiente:  

-   Póngase en contacto con Soporte técnico de Microsoft, tal y como se describe en [Soporte técnico de Microsoft](#MicrosoftSupport)  

-   Obtenga soporte técnico adicional a través de blogs y otros recursos de Internet, tal y como se describe en [Soporte técnico en Internet](#InternetSupport)  

###  <a name="MicrosoftSupport"></a> Soporte técnico de Microsoft  
 Microsoft ofrece compatibilidad con los niveles Premier y Professional de Microsoft Deployment Toolkit.  

 Soporte técnico de nivel Professional: [http://support.microsoft.com/](http://support.microsoft.com/)  

 Soporte técnico de nivel Premier: [https://premier.microsoft.com/](https://premier.microsoft.com/)  

> [!NOTE]
>  Al ponerse en contacto con el soporte técnico, indique claramente que el problema está relacionado con MDT y especifique la versión.  

###  <a name="InternetSupport"></a> Soporte técnico en Internet  
 Muchas fuentes en línea ofrecen ayuda adicional para solucionar problemas con MDT, más allá de lo que se abarca en esta referencia. Entre estas fuentes en línea se incluyen:  

-   Blogs hospedadas por Microsoft  

    -   [Blog del equipo de MDT](http://blogs.technet.com/b/msdeployment/)  

    -   [Blog del equipo de Configuration Manager](http://blogs.technet.com/b/configmgrteam/)  

    -   [Blog de Michael Niehaus](http://blogs.technet.com/b/mniehaus/) (Michael Niehaus escribe sobre la implementación de Windows y Microsoft Office).  

-   Grupos de noticias y foros hospedados por Microsoft:  

     Los siguientes grupos de noticias y foros están disponibles con ayuda de los empleados de Microsoft, compañeros del sector y profesionales más valiosos de Microsoft:  

    -   [Configuration Manager - Implementación del sistema operativo](http://social.technet.microsoft.com/Forums/home?forum=configmanagerosd)  

    -   [Instalación, configuración e implementación de Windows 8](http://social.technet.microsoft.com/Forums/windows/home?forum=w8itproinstall)  

-   Fuentes de información relacionada con la implementación ajenas a Microsoft:  

    -   [DeployVista.com](http://www.deployvista.com/)  

    -   [myITforum.com](http://www.myitforum.com/)
