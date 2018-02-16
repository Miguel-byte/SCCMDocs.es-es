---
title: "Variables de acción de secuencias de tareas"
titleSuffix: Configuration Manager
description: "Use variables de acción de secuencia, como las variables de configuración de red, para especificar valores de configuración de un único paso en una secuencia de tareas de Configuration Manager."
ms.custom: na
ms.date: 02/09/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e2269031-0977-4f01-a274-420e00630575
caps.latest.revision: 
caps.handback.revision: 
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2928ecb254d08e4ed08c5e79b55e210ce25dcb61
ms.sourcegitcommit: fbde417e3c3002898bd216a7e110e725ae269893
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2018
---
# <a name="task-sequence-action-variables-in-system-center-configuration-manager"></a>Variables de acción de secuencias de tareas en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Las variables de acción de secuencias de tareas especifican los valores de configuración que se usan en un único paso de una secuencia de tareas de System Center Configuration Manager. De forma predeterminada, el paso de la secuencia de tareas inicializa su configuración antes de ejecutarse. Esta configuración solo está disponible mientras se está ejecutando el paso asociado de la secuencia de tareas. En otras palabras, la secuencia de tareas agrega el valor de la variable de acción al entorno de la secuencia de tareas antes de que se ejecute el paso. La secuencia de tareas quita el valor del entorno después de que se ejecuta el paso.  

## <a name="action-variable-example"></a>Ejemplo de variable de acción  
 Por ejemplo, puede especificar un directorio de inicio para una acción de la línea de comandos si usa la etapa de la secuencia de tareas **Ejecutar línea de comandos** . Esta etapa incluye una propiedad **Iniciar en** cuyo valor predeterminado se almacena en el entorno de secuencia de tareas como la variable **WorkingDirectory** . La variable de entorno **WorkingDirectory** se inicializa antes de que se ejecute la acción de la secuencia de tareas **Ejecutar línea de comandos** . Durante la etapa **Ejecutar línea de comandos** , el valor de **WorkingDirectory** puede obtenerse a través de la propiedad **Empezar en** . Una vez completado el paso (etapa), la secuencia de tareas quita el valor de la variable **WorkingDirectory** del entorno. Si la secuencia contiene otro paso de secuencia de tareas **Ejecutar línea de comandos**, la secuencia de tareas inicializa una nueva variable **WorkingDirectory** y la establece como el valor inicial para ese paso.  

 El valor *predeterminado* de una variable de acción de secuencia de tareas está presente cuando se ejecuta el paso de la secuencia de tareas. Si establece un *nuevo* valor, estará disponible para varios pasos de la secuencia de tareas. Si utiliza uno de los métodos de creación de variables de secuencia de tareas para invalidar el valor de una variable integrada, el nuevo valor permanece en el entorno y reemplaza el valor predeterminado del resto de etapas de la secuencia de tareas. Por ejemplo, si agrega un paso **Configurar variable de secuencia de tareas** como la primera de la secuencia de tareas, lo que establece la variable **WorkingDirectory** en **C:\\**, cualquier paso **Ejecutar línea de comandos** de la secuencia de tareas utiliza el nuevo valor de directorio inicial.  

## <a name="action-variables-for-task-sequence-actions"></a>Variables de acción de las acciones de secuencia de tareas  
 Las variables de la secuencia de tareas de Configuration Manager se agrupan por su acción de secuencia de tareas asociada. Consulte los vínculos siguientes para recopilar información sobre las variables de acción asociadas a una acción concreta. Las variables de secuencia de tareas controlan el funcionamiento de la acción de secuencia de tareas. La acción de secuencia de tareas lee o usa las variables marcadas como variables de entrada. De manera alternativa, las variables se pueden establecer en tiempo de ejecución a través del paso [Configurar variable de secuencia de tareas](task-sequence-steps.md#BKMK_SetTaskSequenceVariable) o a través del objeto COM TSEnvironment. Solo la acción de secuencia de tareas marca las variables como variables de salida. Las acciones que tienen lugar posteriormente en la secuencia de tareas leen estas variables de salida.  

> [!NOTE]  
>  No todas las acciones de las secuencias de tareas están asociadas a un conjunto de variables de secuencias de tareas. Por ejemplo, aunque hay variables asociadas a la acción Habilitar BitLocker, no hay ninguna variable asociada a la acción Deshabilitar BitLocker.  



###  <a name="BKMK_ApplyDataImage"></a> Aplicar imágenes de datos   
 Para obtener más información, consulte [Aplicar imágenes de datos](task-sequence-steps.md#BKMK_ApplyDataImage). 

#### <a name="details"></a>Detalles  

|Nombre de variable de acción|Descripción|  
|--------------------------|-----------------|  
|OSDDataImageIndex<br /><br /> (entrada)|Especifica el valor de índice de la imagen que se aplica al equipo de destino.|  
|OSDWipeDestinationPartition<br /><br /> (entrada)|Especifica si se deben eliminar los archivos ubicados en la partición de destino.<br /><br /> Valores válidos:<br /><br /> **true** (valor predeterminado)<br /><br /> **false**|  



###  <a name="BKMK_ApplyDriverPackage"></a> Aplicar paquete de controladores   
Para obtener más información, consulte [Aplicar paquete de controladores](task-sequence-steps.md#BKMK_ApplyDriverPackage).  

#### <a name="details"></a>Detalles  

|Nombre de variable de acción|Descripción|  
|--------------------------|-----------------|  
|OSDApplyDriverBootCriticalContentUniqueID<br /><br /> (entrada)|Especifica el identificador de contenido del controlador del dispositivo de almacenamiento masivo que se debe instalar desde el paquete de controladores. Si no se especifica esta variable, no se instala ningún controlador de almacenamiento masivo.|  
|OSDApplyDriverBootCriticalINFFile<br /><br /> (entrada)|Especifica el archivo INF del controlador de almacenamiento masivo que se debe instalar.<br /><br /> <br /><br /> Esta variable de secuencia de tareas es necesaria si se establece OSDApplyDriverBootCriticalContentUniqueID.|  
|OSDApplyDriverBootCriticalHardwareComponent<br /><br /> (entrada)|Especifica si hay un controlador de dispositivo de almacenamiento instalado; esta variable debe ser **scsi**.<br /><br /> Esta variable de secuencia de tareas es necesaria si se establece OSDApplyDriverBootCriticalContentUniqueID.|  
|OSDApplyDriverBootCriticalID<br /><br /> (entrada)|Especifica el identificador crítico para el arranque del controlador del dispositivo de almacenamiento masivo que se debe instalar. Este identificador se muestra en la sección **scsi** del archivo txtsetup.oem del controlador de dispositivo.<br /><br /> Esta variable de secuencia de tareas es necesaria si se establece OSDApplyDriverBootCriticalContentUniqueID.|  
|OSDAllowUnsignedDriver<br /><br /> (entrada)|Especifica si se va a configurar Windows para permitir la instalación de controladores de dispositivos sin firmar. Esta variable de secuencia de tareas no se utiliza al implementar Windows Vista y sistemas operativos posteriores.<br /><br /> Valores válidos:<br /><br /> **true**<br /><br /> **false** (valor predeterminado)|  



###  <a name="BKMK_ApplyNetworkSettings"></a> Aplicar configuración de red   
 Para obtener más información, consulte [Aplicar configuración de red](task-sequence-steps.md#BKMK_ApplyNetworkSettings).  

#### <a name="details"></a>Detalles  

|Nombre de variable de acción|Descripción|  
|--------------------------|-----------------|  
|OSDAdapter<br /><br /> (entrada)|Esta variable de secuencia de tareas es una variable de matriz. Cada elemento de la matriz representa la configuración de un único adaptador de red en el equipo. El acceso a la configuración de cada adaptador se realiza mediante la combinación del nombre de la variable de matriz con el índice del adaptador de red basado en cero y el nombre de la propiedad.<br /><br />Si en este paso se configuran varios adaptadores de red, las propiedades del segundo adaptador de red se definen mediante el uso del índice en el nombre de variable. Por ejemplo, OSDAdapter1EnableDHCP, OSDAdapter1IPAddressList, OSDAdapter1DNSDomain, OSDAdapter1WINSServerList y OSDAdapter1EnableWINS.<br /><br />Por ejemplo, use los siguientes nombres de variable para definir las propiedades del primer adaptador de red para este paso de secuencia de tareas:<br /><br /> <ul><li>**OSDAdapter0EnableDHCP**: **true** habilita el Protocolo de configuración dinámica de host (DHCP) del adaptador.<br />    Esta opción es necesaria. Los valores posibles son: **True** o **False**.</li><li>**OSDAdapter0IPAddressList**: una lista delimitada por comas de direcciones IP del adaptador. Esta propiedad se omite a menos que el valor de **EnableDHCP** está establecido como **false**.<br />    Esta opción es necesaria.</li><li>**OSDAdapter0SubnetMask**: una lista delimitada por comas de las máscaras de subred. Esta propiedad se omite a menos que el valor de **EnableDHCP** está establecido como **false**.<br />    Esta opción es necesaria.</li><li>**OSDAdapter0Gateways**: una lista delimitada por comas de direcciones IP de puertas de enlace. Esta propiedad se omite a menos que el valor de **EnableDHCP** está establecido como **false**.<br />    Esta opción es necesaria.</li><li>**OSDAdapter0DNSDomain**: dominio del Sistema de nombres de dominio (DNS) del adaptador.</li><li>**OSDAdapter0DNSServerList**: una lista delimitada por comas de los servidores DNS del adaptador.<br />    Esta opción es necesaria.</li><li>**OSDAdapter0EnableDNSRegistration**: su valor debe ser **true** para registrar la dirección IP del adaptador del DNS.</li><li>**OSDAdapter0EnableFullDNSRegistration**: su valor debe ser **true** para registrar la dirección IP del adaptador del DNS con el nombre DNS completo del equipo.</li><li>**OSDAdapter0EnableIPProtocolFiltering**: su valor debe ser **true** para habilitar el filtrado de protocolo IP en el adaptador.</li><li>**OSDAdapter0IPProtocolFilterList**: una lista delimitada por comas de los protocolos que se pueden ejecutar a través de IP. Esta propiedad se omite si el valor de **EnableIPProtocolFiltering** está establecido en **false**.</li><li>**OSDAdapter0EnableTCPFiltering**: su valor debe ser **true** para habilitar el filtrado de puertos TCP para el adaptador.</li><li>**OSDAdapter0TCPFilterPortList**: una lista delimitada por comas de puertos en los que se deben conceder permisos de acceso para TCP. Esta propiedad se omite si el valor de **EnableTCPFiltering** está establecido en **false**.</li><li>**OSDAdapter0TcpipNetbiosOptions**: opciones de NetBIOS sobre TCP/IP. Los valores posibles son:<br /><br /> <ul><li>**0**: usar la configuración de NetBIOS del servidor DHCP.</li><li>**1**: habilitar NetBIOS sobre TCP/IP.</li><li>**2**: deshabilitar NetBIOS sobre TCP/IP.</li></ul></li><li>**OSDAdapter0EnableWINS**: su valor debe ser **true** si se quiere utilizar WINS para la resolución de nombres.</li><li>**OSDAdapter0WINSServerList**; una lista delimitada por comas de direcciones IP del servidor WINS. Esta propiedad se omite a menos que el valor de **EnableWINS** está establecido como **true**.</li><li>**OSDAdapter0MacAddress**: la dirección MAC que se usa para hacer coincidir la configuración con el adaptador de red físico.</li><li>**OSDAdapter0Name**: nombre de la conexión de red tal y como aparece en el programa del panel de control de las conexiones de red. El nombre debe tener entre 0 y 255 caracteres.</li><li>**OSDAdapter0Index**: el índice de la configuración del adaptador de red en la matriz de valores.<br /><br />     OSDAdapterCount=1<br />    OSDAdapter0EnableDHCP=FALSE<br />    OSDAdapter0IPAddressList=192.168.0.40<br />    OSDAdapter0SubnetMask=255.255.255.0<br />    OSDAdapter0Gateways=192.168.0.1<br />    OSDAdapter0DNSSuffix=contoso.com</li></ul>|  
|OSDAdapterCount<br /><br /> (entrada)|Especifica el número de adaptadores de red instalados en el equipo de destino. Cuando se establece el valor de **OSDAdapterCount** , se deben establecer todas las opciones de configuración de cada uno de los adaptadores. Por ejemplo, si establece el valor de **OSDAdapterTCPIPNetbiosOptions** de un adaptador específico, todos los valores de ese adaptador también deben configurarse.<br /><br />Si no se especifica este valor, todos los valores de **OSDAdapter** se omiten.|  
|OSDDNSDomain<br /><br /> (entrada)|Especifica el servidor DNS principal que usa el equipo de destino.|  
|OSDDomainName<br /><br /> (entrada)|Especifica el nombre del dominio de Windows al que se une el equipo de destino. El valor especificado debe ser un nombre de dominio válido de Servicios de dominio de Active Directory.|  
|OSDDomainOUName<br /><br /> (entrada)|Especifica el nombre en formato RFC 1779 de la unidad organizativa (UO) a la que se une el equipo de destino. Si se especifica, el valor debe contener la ruta de acceso completa.<br /><br /> Ejemplo:<br /><br /> **LDAP://OU=MyOu,DC=MyDom,DC=MyCompany,DC=com**|  
|OSDEnableTCPIPFiltering<br /><br /> (entrada)|Especifica si el filtrado TCP/IP está habilitado.<br /><br /> Valores válidos:<br /><br /> **true**<br /><br /> **false** (valor predeterminado)|  
|OSDJoinAccount<br /><br /> (entrada)|Especifica la cuenta de red que se utiliza para agregar el equipo de destino a un dominio de Windows.|  
|OSDJoinPassword<br /><br /> (entrada)|Especifica la contraseña de red que se utiliza para agregar el equipo de destino a un dominio de Windows.|  
|OSDNetworkJoinType<br /><br /> (entrada)|Especifica si el equipo de destino se une a un dominio de Windows o a un grupo de trabajo.<br /><br /> **0** indica que el equipo de destino se une a un dominio de Windows. **1** especifica que el equipo se une a un grupo de trabajo.<br /><br /> Valores válidos:<br /><br /> **0**<br /><br /> **1**|  
|OSDDNSSuffixSearchOrder<br /><br /> (entrada)|Especifica el orden de búsqueda DNS del equipo de destino.|  
|OSDWorkgroupName<br /><br /> (entrada)|Especifica el nombre del grupo de trabajo al que se une el equipo de destino.<br /><br /> Especifique este valor o el valor de **OSDDomainName**. El nombre del grupo de trabajo puede tener un máximo de 32 caracteres.<br /><br /> Ejemplo:<br /><br /> **Contabilidad**|  



###  <a name="BKMK_ApplyOperatingSystem"></a> Aplicar imagen de sistema operativo   
 Para obtener más información, consulte [Aplicar imagen de sistema operativo](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage).  

#### <a name="details"></a>Detalles  

|Nombre de variable de acción|Descripción|  
|--------------------------|-----------------|  
|OSDConfigFileName<br /><br /> (entrada)|Especifica el nombre del archivo de respuesta de implementación de sistema operativo asociado con el paquete de implementación de sistema operativo.|  
|OSDImageIndex<br /><br /> (entrada)|Especifica el valor de índice de la imagen del archivo WIM que se aplica al equipo de destino.|  
|OSDInstallEditionIndex<br /><br /> (entrada)|Especifica la versión de Windows Vista o del sistema operativo posterior que esté instalado. Si no se especifica ninguna versión, el programa de instalación de Windows determinará qué versión se debe instalar mediante la clave de producto referenciada.<br /><br /> Use solamente un valor de cero (0) si se cumplen las condiciones siguientes:<br /><br /> - Va a instalar un sistema operativo anterior a Windows Vista<br />- Va a instalar una edición de licencia por volumen de Windows Vista o una edición posterior, y no se especifica ninguna clave de producto.<br /><br /> Valores válidos:<br /><br /> **0** (valor predeterminado)|  
|OSDTargetSystemDrive (salida)|Especifica la letra de unidad de la partición que contiene los archivos del sistema operativo.|  



###  <a name="BKMK_ApplyWindowsSettings"></a> Aplicar configuraciones de Windows   
 Para obtener más información, consulte [Aplicar configuraciones de Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings).  

#### <a name="details"></a>Detalles  

|Nombre de variable de acción|Descripción|  
|--------------------------|-----------------|  
|OSDComputerName<br /><br /> (entrada)|Especifica el nombre del equipo de destino.<br /><br /> Ejemplo:<br /><br /> **%_SMSTSMachineName%** (valor predeterminado)|  
|OSDProductKey<br /><br /> (entrada)|Especifica la clave de producto de Windows. El valor especificado debe tener entre 1 y 255 caracteres.|  
|OSDRegisteredUserName<br /><br /> (entrada)|Especifica el nombre de usuario registrado de forma predeterminada en el nuevo sistema operativo. El valor especificado debe tener entre 1 y 255 caracteres.|  
|OSDRegisteredOrgName<br /><br /> (entrada)|Especifica el nombre de organización registrado de forma predeterminada en el nuevo sistema operativo. El valor especificado debe tener entre 1 y 255 caracteres.|  
|OSDTimeZone<br /><br /> (entrada)|Especifica la configuración de zona horaria predeterminada que se usa en el nuevo sistema operativo.|  
|OSDServerLicenseMode<br /><br /> (entrada)|Especifica el modo de licencia de Windows Server que se utiliza.<br /><br /> Valores válidos:<br /><br /> **PerSeat**<br /><br /> **PerServer**|  
|OSDServerLicenseConnectionLimit<br /><br /> (entrada)|Especifica el número máximo de conexiones permitidas. El número especificado debe estar comprendido en el intervalo entre 5 y 9999 conexiones.|  
|OSDRandomAdminPassword<br /><br /> (entrada)|Especifica una contraseña generada de forma aleatoria para la cuenta de administrador en el nuevo sistema operativo. Si establece en **true**, el programa de instalación de Windows deshabilita la cuenta de administrador local en el equipo de destino. Si establece en **false**, el programa de instalación de Windows habilita la cuenta de administrador local en el equipo de destino y establece la contraseña de cuenta en el valor de **OSDLocalAdminPassword**.<br /><br /> Valores válidos:<br /><br /> **true** (valor predeterminado)<br /><br /> **false**|  
|OSDLocalAdminPassword<br /><br /> (entrada)|Especifica la contraseña del administrador local. Si habilita la opción **Generar la contraseña de administrador local aleatoriamente y deshabilitar la cuenta en todas las plataformas admitidas**, entonces el paso ignora esta variable. El valor especificado debe tener entre 1 y 255 caracteres.|  



###  <a name="BKMK_AutoApplyDrivers"></a> Aplicar controladores automáticamente   
 Para obtener más información, consulte [Aplicar controladores automáticamente](task-sequence-steps.md#BKMK_AutoApplyDrivers).  

#### <a name="details"></a>Detalles  

|Nombre de variable de acción|Descripción|  
|--------------------------|-----------------|  
|OSDAutoApplyDriverCategoryList<br /><br /> (entrada)|Una lista delimitada por comas de los identificadores únicos de las categorías del catálogo de controladores. El paso **Aplicar controladores automáticamente** solo tiene en cuenta los controladores de al menos una de las categorías especificadas. Este valor es opcional y no está establecido de forma predeterminada. Obtenga los identificadores de categoría disponibles mediante la enumeración de la lista de objetos **SMS_CategoryInstance** en el sitio.|  
|OSDAllowUnsignedDriver<br /><br /> (entrada)|Especifica si Windows está configurado para permitir que se instalen los controladores de dispositivos sin firmar. Esta variable de secuencia de tareas no se utiliza al implementar Windows Vista y sistemas operativos posteriores.<br /><br /> Valores válidos:<br /><br /> **true**<br /><br /> **false** (valor predeterminado)|  
|OSDAutoApplyDriverBestMatch<br /><br /> (entrada)|Si hay varios controladores de dispositivo en el catálogo de controladores que sean compatibles con un dispositivo de hardware, esta variable determina la acción del paso. Si se establece en **true**, el paso solo instala el mejor controlador de dispositivo. Si se establece en **false**, el paso instala todos los controladores de dispositivo compatibles y Windows elige el mejor controlador.<br /><br /> Valores válidos:<br /><br /> **true** (valor predeterminado)<br /><br /> **false**|  
|Valor predeterminado de SMSTSDriverRequestConnectTimeOut:|Cuando se solicita el catálogo de controladores, esta variable es el número de segundos que la secuencia de tareas espera a que se establezca la conexión con el servidor HTTP. Si la conexión tarda más de lo especificado en la configuración del tiempo de espera, la secuencia de tareas cancela la solicitud. De forma predeterminada, el tiempo de espera se establece en **60** segundos.|  
|Valor predeterminado de SMSTSDriverRequestReceiveTimeOut:|Cuando se solicita el catálogo de controladores, esta variable es el número de segundos que la secuencia de tareas espera una respuesta. Si la conexión tarda más de lo especificado en la configuración del tiempo de espera, la secuencia de tareas cancela la solicitud. De forma predeterminada, el tiempo de espera se establece en **480** segundos.|
|Valor predeterminado de SMSTSDriverRequestResolveTimeOut:|Cuando se solicita el catálogo de controladores, esta variable es el número de segundos que la secuencia de tareas espera por la resolución de nombres HTTP. Si la conexión tarda más de lo especificado en la configuración del tiempo de espera, la secuencia de tareas cancela la solicitud. De forma predeterminada, el tiempo de espera se establece en **60** segundos.|
|Valor predeterminado de SMSTSDriverRequestSendTimeOut:|Cuando se envía una solicitud al catálogo de controladores, esta variable es el número de segundos que la secuencia de tareas espera para enviar la solicitud. Si la solicitud tarda más de lo especificado en la configuración del tiempo de espera, la secuencia de tareas cancela la solicitud. De forma predeterminada, el tiempo de espera se establece en **60** segundos.|



###  <a name="BKMK_CaptureNetworkSettings"></a> Capturar configuración de red   
 Para obtener más información, consulte [Capturar configuración de red](task-sequence-steps.md#BKMK_CaptureNetworkSettings).  

#### <a name="details"></a>Detalles  

|Nombre de variable de acción|Descripción|  
|--------------------------|-----------------|  
|OSDMigrateAdapterSettings<br /><br /> (entrada)|Especifica si se captura información de configuración de los ajustes del adaptador de red (TCP/IP, DNS y WINS).<br /><br /> Ejemplo:<br /><br /> **true** (valor predeterminado)<br /><br /> **false**|  
|OSDMigrateNetworkMembership<br /><br /> (entrada)|Especifica si se migra la información de pertenencia a un grupo de trabajo o un dominio como parte de la implementación de sistema operativo.<br /><br /> Ejemplo:<br /><br /> **true** (valor predeterminado)<br /><br /> **false**|  



###  <a name="BKMK_CaptureOperatingSystemImage"></a> Capturar imagen de sistema operativo   
 Para obtener más información, consulte [Capturar imagen de sistema operativo](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage).  

#### <a name="details"></a>Detalles  

|Nombre de variable de acción|Descripción|  
|--------------------------|-----------------|  
|OSDCaptureAccount<br /><br /> (entrada)|Especifica un nombre de cuenta de Windows que tiene permisos para almacenar la imagen capturada en un recurso compartido de red.|  
|OSDCaptureAccountPassword<br /><br /> (entrada)|Especifica la contraseña de la cuenta de Windows que se utiliza para almacenar la imagen capturada en un recurso compartido de red.|  
|OSDCaptureDestination<br /><br /> (entrada)|Especifica la ubicación donde se guarda la imagen capturada del sistema operativo. La longitud máxima del nombre de directorio es 255 caracteres.|  
|OSDImageCreator<br /><br /> (entrada)|Un nombre opcional del usuario que creó la imagen. Este nombre se almacena en el archivo WIM. La longitud máxima del nombre de usuario es 255 caracteres.|  
|OSDImageDescription<br /><br /> (entrada)|Una descripción opcional definida por el usuario de la imagen capturada del sistema operativo. Esta descripción se almacena en el archivo WIM. La longitud máxima de la descripción es 255 caracteres.|  
|OSDImageVersion<br /><br /> (entrada)|Número de versión opcional definido por el usuario que se asigna a la imagen capturada del sistema operativo. Este número de versión se almacena en el archivo WIM. Este valor puede ser una combinación cualquiera de letras con una longitud máxima de 32 caracteres.|  
|OSDTargetSystemRoot<br /><br /> (entrada)|Especifica la ruta de acceso al directorio de Windows del sistema operativo instalado en el equipo de referencia. Este sistema operativo se verifica como un sistema operativo compatible para la captura por parte de Configuration Manager.|  



###  <a name="BKMK_CaptureUserState"></a> Capturar estado de usuario   
 Para obtener más información, consulte [Capturar estado de usuario](task-sequence-steps.md#BKMK_CaptureUserState).  

#### <a name="details"></a>Detalles  

|Nombre de variable de acción|Descripción|  
|--------------------------|-----------------|  
|OSDStateStorePath<br /><br /> (entrada)|La UNC o un nombre de ruta de acceso local de la carpeta donde se guarda el estado de usuario. Sin valor predeterminado.|  
|OSDMigrateAdditionalCaptureOptions<br /><br /> (entrada)|Opciones adicionales de la línea de comandos de la herramienta de migración de estado de usuario (USMT) que la secuencia de tareas utiliza para capturar el estado de usuario. El paso no expone estas opciones en el editor de secuencia de tareas. Especifique estas opciones como una cadena que la secuencia de tareas anexa a la línea de comandos USMT generada automáticamente.<br /><br />Las opciones de USMT especificadas con esta variable de secuencia de tareas no se validan para comprobar su exactitud antes de ejecutar la secuencia de tareas.|  
|OSDMigrateMode<br /><br /> (entrada)|Le permite personalizar los archivos que captura la USMT. Si esta variable se establece en **Simple**, la secuencia de tareas solo usa los archivos de configuración de USMT estándar. Si esta variable se establece en **Advanced**, la variable de secuencia de tareas OSDMigrateConfigFiles especifica los archivos de configuración que usa USMT.<br /><br /> Valores válidos:<br /><br /> **Simple**<br /><br /> **Advanced**|  
|OSDMigrateConfigFiles<br /><br /> (entrada)|Especifica los archivos de configuración que se utilizan para controlar la captura de perfiles de usuario. Esta variable se usa solo si el valor de OSDMigrateMode está establecido en Advanced. Este valor de lista delimitada por comas está configurado para realizar una migración de perfiles de usuario personalizada.<br /><br /> Por ejemplo: miguser.xml,migsys.xml,migapps.xml|  
|OSDMigrateContinueOnLockedFiles<br /><br /> (entrada)|Si USMT no puede capturar algunos archivos, esta variable permite a la captura del estado de usuario continuar.<br /><br /> Valores válidos:<br /><br /> **true** (valor predeterminado)<br /><br /> **false**|  
|OSDMigrateEnableVerboseLogging<br /><br /> (entrada)|Habilita el registro detallado para USMT.<br /><br /> Valores válidos:<br /><br /> **true**<br /><br /> **false** (valor predeterminado)|  
|OSDMigrateSkipEncryptedFiles<br /><br /> (entrada)|Especifica si se capturan los archivos cifrados.<br /><br /> Valores válidos:<br /><br /> **true**<br /><br /> **false** (valor predeterminado)|  
|_OSDMigrateUsmtPackageID<br /><br /> (entrada)|Especifica el identificador del paquete de Configuration Manager que contiene los archivos de USMT. Esta variable es necesaria.|  



###  <a name="BKMK_CaptureWindowsSettings"></a> Capturar configuración de Windows   
 Para obtener más información, consulte [Capturar configuración de Windows](task-sequence-steps.md#BKMK_CaptureWindowsSettings).  

#### <a name="details"></a>Detalles  

|Nombre de variable de acción|Descripción|  
|--------------------------|-----------------|  
|OSDMigrateComputerName<br /><br /> (entrada)|Especifica si se migra el nombre del equipo.<br /><br /> Valores válidos:<br /><br /> **true** (valor predeterminado)<br /><br /> **false**<br /><br /> Si el valor es **true**, la variable OSDComputerName se establece en el nombre NETBIOS del equipo.|  
|OSDComputerName<br /><br /> (salida)|Se establece con el nombre NETBIOS del equipo. El valor se establece solo si la variable OSDMigrateComputerName se establece en **true**.|  
|OSDMigrateRegistrationInfo<br /><br /> (entrada)|Especifica si el paso migra la información del usuario y la organización.<br /><br /> Valores válidos:<br /><br /> **true** (valor predeterminado)<br /><br /> **false**<br /><br /> Si el valor es **true**, la variable OSDRegisteredOrgName se establece en el nombre de organización registrado del equipo.|  
|OSDRegisteredOrgName<br /><br /> (salida)|Se establece con el nombre de organización registrado del equipo. El valor se establece solo si la variable OSDMigrateRegistrationInfo se establece en **true**.|  
|OSDMigrateTimeZone<br /><br /> (entrada)|Especifica si se migra la zona horaria del equipo.<br /><br /> Valores válidos:<br /><br /> **true** (valor predeterminado)<br /><br /> **false**<br /><br /> Si el valor es **true**, la variable OSDTimeZone se establece en la zona horaria del equipo.|  
|OSDTimeZone<br /><br /> (salida)|Se establece con la zona horaria del equipo. El valor se establece solo si la variable OSDMigrateTimeZone se establece en **true**.|  



###  <a name="BKMK_ConnecttoNetworkFolder"></a> Conexión a la carpeta de red   
 Para obtener más información, consulte [Conexión a la carpeta de red](task-sequence-steps.md#BKMK_ConnectToNetworkFolder).  

#### <a name="details"></a>Detalles  

|Nombre de variable de acción|Descripción|  
|--------------------------|-----------------|  
|SMSConnectNetworkFolderAccount<br /><br /> (entrada)|Especifica la cuenta de administrador que se utiliza para conectarse al recurso compartido de red.|  
|SMSConnectNetworkFolderDriveLetter<br /><br /> (entrada)|Especifica la letra de unidad de la red a la que se debe conectar. Este valor es opcional; si no se especifica, la conexión de red no se asigna a una letra de unidad. Si se especifica este valor, debe estar en el intervalo de D: a Z:. Además, no utilice X:, ya que es la letra de unidad que usa Windows PE durante la etapa de Windows PE.<br /><br /> Ejemplo:<br /><br /> **D:**<br /><br /> **E:**|  
|SMSConnectNetworkFolderPassword<br /><br /> (entrada)|Especifica la contraseña de red que se utiliza para conectarse al recurso compartido de red.|  
|SMSConnectNetworkFolderPath<br /><br /> (entrada)|Especifica la ruta de acceso de red para la conexión.<br /><br /> Ejemplo:<br /><br /> **\\\nombreservidor\nombrerecursocompartido**|  



###  <a name="BKMK_EnableBitLocker"></a> Habilitar BitLocker   
 Para obtener más información, consulte [Habilitar BitLocker](task-sequence-steps.md#BKMK_EnableBitLocker).  

#### <a name="details"></a>Detalles  

|Nombre de variable de acción|Descripción|  
|--------------------------|-----------------|  
|OSDBitLockerRecoveryPassword<br /><br /> (entrada)|En lugar de generar una contraseña aleatoria de recuperación, la acción de la secuencia de tareas **Habilitar BitLocker** usa el valor especificado como la contraseña de recuperación. El valor debe ser una contraseña numérica de recuperación de BitLocker válida.|  
|OSDBitLockerStartupKey<br /><br /> (entrada)|En lugar de generar una clave de inicio aleatoria para la opción de administración de claves **Clave de inicio solo en USB**, el paso **Habilitar BitLocker** usa el Módulo de plataforma segura (TPM) como clave de inicio. El valor debe ser una clave de inicio válida de BitLocker de 256 bits con codificación Base64.|  



###  <a name="BKMK_FormatPartitionDisk"></a> Formatear y crear particiones en el disco   
 Para obtener más información, consulte [Formatear y crear particiones en el disco](task-sequence-steps.md#BKMK_FormatandPartitionDisk).  

#### <a name="details"></a>Detalles  

|Nombre de variable de acción|Descripción|  
|--------------------------|-----------------|  
|OSDDiskIndex<br /><br /> (entrada)|Especifica el número de disco físico en el que se van a crear particiones.|  
|OSDDiskpartBiosCompatibilityMode<br /><br /> (entrada)|Al crear particiones del disco duro para que haya compatibilidad con ciertos tipos de BIOS, esta variable especifica si se deben deshabilitar las optimizaciones de alineación de caché. Esto es necesario cuando se implementan sistemas operativos Windows XP o Windows Server 2003. Para más información, consulte el [artículo 931760](http://go.microsoft.com/fwlink/?LinkId=134081) y el [artículo 931761](http://go.microsoft.com/fwlink/?LinkId=134082) de Microsoft Knowledge Base.<br /><br /> Valores válidos:<br /><br /> **true**<br /><br /> **false** (valor predeterminado)| 
|OSDGPTBootDisk<br /><br /> (entrada)|Especifica si se debe crear una partición EFI en un disco duro GPT. Los equipos basados en EFI utilizan esta partición como disco de inicio.<br /><br /> Valores válidos:<br /><br /> **true**<br /><br /> **false** (valor predeterminado)|  
|OSDPartitions<br /><br /> (entrada)|Especifica una matriz de configuración de la partición; vea el tema de SDK para acceder a las variables de la matriz en el entorno de la secuencia de tareas.<br /><br /> Esta variable de secuencia de tareas es una variable de matriz. Cada uno de los elementos de la matriz representa la configuración de una única partición en el disco duro. El acceso a la configuración definida para cada partición se puede realizar mediante la combinación del nombre de la variable de matriz con el número de partición de disco basado en cero y el nombre de la propiedad.<br /><br /> Por ejemplo, use los siguientes nombres de variable para definir las propiedades de la primera partición que este paso crea en el disco duro:<br /><br /> - **OSDPartitions0Type**: especifica el tipo de la partición. Esta propiedad es obligatoria. Los valores válidos son **Primary**, **Extended**, **Logical** y **Hidden**.<br />-   **OSDPartitions0FileSystem**: especifica el tipo de sistema de archivos que se utilizará al formatear la partición. Esta propiedad es opcional. Si no especifica un sistema de archivos, el paso no formatea la partición. Los valores válidos son **FAT32** y **NTFS**.<br />-   **OSDPartitions0Bootable**: especifica si la partición es de arranque. Esta propiedad es obligatoria. Si este valor se establece en **TRUE** en discos MBR, el paso marca esta partición como activa.<br />-   **OSDPartitions0QuickFormat**: especifica el tipo de formato que se utiliza. Esta propiedad es obligatoria. Si este valor se establece en **TRUE**, el paso realiza un formateo rápido. En caso contrario, el paso realiza un formateo completo.<br />-   **OSDPartitions0VolumeName**: especifica el nombre que se asigna al volumen cuando se formatea. Esta propiedad es opcional.<br />-   **OSDPartitions0Size**: especifica el tamaño de la partición. Las unidades las especifica la variable **OSDPartitions0SizeUnits** . Esta propiedad es opcional. Si no se especifica esta propiedad, se crea la partición con todo el espacio libre restante.<br />-   **OSDPartitions0SizeUnits**: el paso utiliza estas unidades para interpretar la variable **OSDPartitions0Size**. Esta propiedad es opcional. Los valores válidos son **MB** (predeterminado), **GB** y **Porcentaje**.<br />-   **OSDPartitions0VolumeLetterVariable**: cuando en este paso se crean las particiones, siempre se utiliza la siguiente letra de unidad disponible en Windows PE. Use esta propiedad opcional para especificar el nombre de otra variable de secuencia de tareas. El paso utiliza esta variable para guardar la nueva letra de unidad para futuras referencias.<br /><br />Si define varias particiones con esta acción de secuencia de tareas, las propiedades de la segunda partición se definen con su índice en el nombre de variable. Por ejemplo: **OSDPartitions1Type**, **OSDPartitions1FileSystem**, **OSDPartitions1Bootable**, **OSDPartitions1QuickFormat** y **OSDPartitions1VolumeName**.|  
|OSDPartitionStyle<br /><br /> (entrada)|Especifica el estilo de partición que se utilizará al crear particiones en el disco. **MBR** indica el estilo de partición de registro de arranque maestro y **GPT** indica el estilo de tabla de particiones GUID.<br /><br /> Valores válidos:<br /><br /> **GPT**<br /><br /> **MBR**|  



###  <a name="BKMK_InstallApplication"></a> Instalar aplicación   
 Para obtener más información, consulte [Instalar aplicación](task-sequence-steps.md#BKMK_InstallApplication).  

#### <a name="details"></a>Detalles  

|Nombre de variable de acción<br /><br /> (entrada)|Descripción|  
|----------------------------------------|-----------------|  
| TSErrorOnWarning |Permite especificar si el motor de secuencia de tareas considera una advertencia detectada como un error durante este paso. La secuencia de tareas establece la variable _TSAppInstallStatus en **Advertencia** cuando una o más aplicaciones (o una dependencia necesaria) no se instalaron porque no se cumplió un requisito. Si se establece esta variable en **True** y la secuencia de tareas establece _TSAppInstallStatus en Advertencia, el resultado es un error. Un valor **False** es el comportamiento predeterminado.| 
|SMSTSMPListRequestTimeoutEnabled|Use esta variable para permitir solicitudes MPList repetidas para actualizar el cliente si este no está en la intranet. <br />De forma predeterminada, esta variable se establece en **True**. Si los clientes no están en Internet, puede establecer esta variable en **False** para evitar retrasos innecesarios. Esta variable solo es aplicable a los pasos de secuencia de tareas de instalación de actualizaciones de aplicaciones y de software.|  
|SMSTSMPListRequestTimeout|Permite especificar la cantidad de milisegundos que una secuencia de tareas espera antes de reintentar instalar una aplicación después de no poder recuperar la lista de puntos de administración de servicios de ubicación. De forma predeterminada, la secuencia de tareas espera **60 000** milisegundos (60 segundos) antes de reintentar el paso, y realiza un máximo de tres reintentos.|  



###  <a name="BKMK_InstallSoftwareUpdates"></a> Instalar actualizaciones de software   
Para obtener más información, consulte [Instalar actualizaciones de software](task-sequence-steps.md#BKMK_InstallSoftwareUpdates).  

#### <a name="details"></a>Detalles  

|Nombre de variable de acción<br /><br /> (entrada)|Descripción|  
|----------------------------------------|-----------------|  
|SMSInstallUpdateTarget<br /><br /> (entrada)|Especifica si se deben instalar todas las actualizaciones o solo las obligatorias.<br /><br /> Valores válidos:<br /><br /> **Todos**<br /><br /> **Obligatorio**|  
|SMSTSSoftwareUpdateScanTimeout| Permite controlar el tiempo de espera para la detección de actualizaciones de software durante este paso. Por ejemplo, aumente el valor si espera que haya numerosas actualizaciones durante el análisis. El valor predeterminado es **1800** segundos (30 minutos). El valor de la variable se establece en segundos. |
|SMSTSWaitForSecondReboot|Esta variable de secuencia de tareas opcional controla el comportamiento del cliente cuando la instalación de una actualización de software requiere dos reinicios. Establezca esta variable antes del paso para evitar que una secuencia de tareas presente errores debido a un segundo reinicio desde la instalación de la actualización de software.<br /><br /> Establezca el valor de SMSTSWaitForSecondReboot en segundos para especificar durante cuánto tiempo se pausa la secuencia de tareas en este paso mientras se reinicia el equipo. Deje tiempo suficiente en caso de que haya un segundo reinicio. <br />Por ejemplo, si establece SMSTSWaitForSecondReboot en 600, la secuencia de tareas se pausa durante 10 minutos tras un reinicio antes de que se ejecuten los pasos adicionales. Esta variable resulta útil cuando un único paso de secuencia de tareas de instalación de actualizaciones de software instala cientos de actualizaciones de software.| 
|SMSTSMPListRequestTimeoutEnabled|Use esta variable para permitir solicitudes MPList repetidas para actualizar el cliente si este no está en la intranet. <br />De forma predeterminada, esta variable se establece en **True**. Si los clientes no están en Internet, puede establecer esta variable en **False** para evitar retrasos innecesarios. Esta variable solo es aplicable a los pasos de secuencia de tareas de instalación de actualizaciones de aplicaciones y de software.|  
|SMSTSMPListRequestTimeout|Use esta variable para especificar la cantidad de milisegundos que espera una secuencia de tareas antes de volver a intentar instalar una actualización de software después de no poder recuperar la lista de puntos de administración de los servicios de ubicación. De forma predeterminada, la secuencia de tareas espera **60 000** milisegundos (60 segundos) antes de reintentar el paso, y realiza un máximo de tres reintentos.|  



###  <a name="BKMK_JoinDomainWorkgroup"></a> Unirse a dominio o grupo de trabajo   
 Para obtener más información, consulte [Unirse a dominio o grupo de trabajo](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup).  

#### <a name="details"></a>Detalles  

|Nombre de variable de acción|Descripción|  
|--------------------------|-----------------|  
|OSDJoinAccount<br /><br /> (entrada)|Especifica la cuenta que utiliza el equipo de destino para unirse a un dominio de Active Directory. Esta variable es necesaria para unirse a un dominio.|  
|OSDJoinDomainName<br /><br /> (entrada)|Especifica el nombre de un dominio de Active Directory al que se une el equipo de destino. El nombre de dominio debe tener entre 1 y 255 caracteres.|  
|OSDJoinDomainOUName<br /><br /> (entrada)|Especifica el nombre en formato RFC 1779 de la unidad organizativa (UO) a la que se une el equipo de destino. Si se especifica, el valor debe contener la ruta de acceso completa. El nombre de la UO debe tener entre 0 y 32 767 caracteres. No se establece este valor si la variable **OSDJoinType** se establece como **1** (unirse al grupo de trabajo).<br /><br /> Ejemplo:<br /><br /> **LDAP://OU=MyOu,DC=MyDom,DC=MyCompany,DC=com**|  
|OSDJoinPassword<br /><br /> (entrada)|Especifica la contraseña de red que usa el equipo de destino para unirse al dominio de Active Directory. Si el entorno de secuencia de tareas no incluye esta variable, el programa de instalación de Windows prueba con una contraseña en blanco. Este valor es necesario si la variable **OSDJoinType** se establece como **0** (unirse al dominio).|  
|OSDJoinSkipReboot<br /><br /> (entrada)|Especifica si se omite el reinicio después de que el equipo de destino se una al dominio o al grupo de trabajo.<br /><br /> Valores válidos:<br /><br /> **true**<br /><br /> **false**|  
|OSDJoinType<br /><br /> (entrada)|Especifica si el equipo de destino se une a un dominio de Windows o a un grupo de trabajo. Para unir el equipo de destino a un dominio de Windows, especifique **0**. Para unir el equipo de destino a un grupo de trabajo, especifique **1**.<br /><br /> Valores válidos:<br /><br /> **0**<br /><br /> **1**|  
|OSDJoinWorkgroupName<br /><br /> (entrada)|Especifica el nombre de un grupo de trabajo al que se une el equipo de destino. El nombre del grupo de trabajo debe tener entre 1 y 32 caracteres.<br /><br /> Ejemplo:<br /><br /> **Contabilidad**|  



###  <a name="BKMK_PrepareWindowsCapture"></a> Prepare Windows for Capture   
 Para obtener más información, consulte [Preparar Windows para la captura](task-sequence-steps.md#BKMK_PrepareWindowsforCapture).  

#### <a name="details"></a>Detalles  

|Nombre de variable de acción|Descripción|  
|--------------------------|-----------------|  
|OSDBuildStorageDriverList<br /><br /> (entrada)|Especifica si Sysprep crea una lista de controladores de dispositivos de almacenamiento masivo. Esta configuración se aplica únicamente a Windows XP y Windows Server 2003. Esta variable rellena la sección [SysprepMassStorage] de sysprep.inf con información sobre todos los controladores de almacenamiento masivo que sean compatibles con la imagen que se va a capturar.<br /><br /> Valores válidos:<br /><br /> **true**<br /><br /> **false** (valor predeterminado)|  
|OSDKeepActivation<br /><br /> (entrada)|Especifica si sysprep restablece la marca de activación del producto.<br /><br /> Valores válidos:<br /><br /> **true**<br /><br /> **false** (valor predeterminado)|  
|OSDTargetSystemRoot<br /><br /> (salida)|Especifica la ruta de acceso al directorio de Windows del sistema operativo instalado en el equipo de referencia. Este sistema operativo se verifica como un sistema operativo compatible para la captura por parte de Configuration Manager.|  



###  <a name="BKMK_ReleaseStateStore"></a> Liberar almacén de estado   
 Para obtener más información, consulte [Liberar almacén de estado](task-sequence-steps.md#BKMK_ReleaseStateStore).  

#### <a name="details"></a>Detalles  

|Nombre de variable de acción|Descripción|  
|--------------------------|-----------------|  
|OSDStateStorePath<br /><br /> (entrada)|El nombre de la ruta de acceso local o UNC a la ubicación desde la que se restaura el estado de usuario. Este valor lo utilizan las acciones de secuencia de tareas **Capturar estado de usuario** y **Restaurar estado de usuario** .|  



###  <a name="BKMK_RequestState"></a> Solicitar almacén de estado   
  Para obtener más información, consulte [Liberar almacén de estado](task-sequence-steps.md#BKMK_ReleaseStateStore).  

#### <a name="details"></a>Detalles  

|Nombre de variable de acción|Descripción|  
|--------------------------|-----------------|  
|OSDStateFallbackToNAA<br /><br /> (entrada)|Esta variable especifica si la secuencia de tareas debe usar la cuenta de acceso a red (NAA) como reserva cuando la cuenta del equipo no se puede conectar al punto de migración de estado.<br /><br /> Valores válidos:<br /><br /> **true**<br /><br /> **false** (valor predeterminado)|  
|OSDStateSMPRetryCount<br /><br /> (entrada)|Especifica el número de veces que esta etapa de la secuencia de tareas intenta encontrar un punto de migración de estado antes de que la etapa produzca un error. El número especificado debe estar entre 0 y 600.|  
|OSDStateSMPRetryTime<br /><br /> (entrada)|Especifica el número de segundos que espera entre reintentos la etapa de la secuencia de tareas. El número de segundos puede tener un máximo de 30 caracteres.|  
|OSDStateStorePath<br /><br /> (salida)|La ruta de acceso UNC a la carpeta en el punto de migración de estado donde se almacena el estado de usuario.|  



###  <a name="BKMK_RestartComputer"></a> Reiniciar equipo   
 Para obtener más información, consulte [Reiniciar equipo](task-sequence-steps.md#BKMK_RestartComputer).  

#### <a name="details"></a>Detalles  

|Nombre de variable de acción|Descripción|  
|--------------------------|-----------------|  
|SMSRebootMessage<br /><br /> (entrada)|Especifica el mensaje que se mostrará a los usuarios antes de reiniciar el equipo de destino. Si esta variable no está establecida, se mostrará un mensaje de texto predeterminado. El mensaje especificado no debe superar los 512 caracteres.<br /><br /> Ejemplo:<br /><br /> **Guarde su trabajo antes de reiniciar el equipo.**|  
|SMSRebootTimeout<br /><br /> (entrada)|Especifica el número de segundos que se muestra la advertencia al usuario antes de reiniciar el equipo. Especifique cero segundos para indicar que no se muestre ningún mensaje de reinicio.<br /><br /> Ejemplo:<br /><br /> **0** (valor predeterminado)<br /><br />  **60**|  



###  <a name="BKMK_RestoreUserState"></a> Restaurar estado de usuario   
  Para obtener más información, consulte [Restaurar estado de usuario](task-sequence-steps.md#BKMK_RestoreUserState).  

#### <a name="details"></a>Detalles  

|Nombre de variable de acción|Descripción|  
|--------------------------|-----------------|  
|OSDStateStorePath<br /><br /> (entrada)|El nombre de la ruta de acceso local o UNC de la carpeta desde la que se restaura el estado de usuario.|  
|OSDMigrateContinueOnRestore<br /><br /> (entrada)|Continuar con el proceso, incluso si USMT no puede restaurar algunos archivos.<br /><br /> Valores válidos:<br /><br /> **true** (valor predeterminado)<br /><br /> **false**|  
|OSDMigrateEnableVerboseLogging<br /><br /> (entrada)|Habilita el registro detallado para la herramienta USMT. Este valor es requerido por la acción.<br /><br /> Valores válidos:<br /><br /> **true**<br /><br /> **false** (valor predeterminado)|  
|OSDMigrateLocalAccounts<br /><br /> (entrada)|Especifica si se restaura la cuenta de equipo local.<br /><br /> Valores válidos:<br /><br /> **true**<br /><br /> **false** (valor predeterminado)|  
|OSDMigrateLocalAccountPassword<br /><br /> (entrada)|Si la variable **OSDMigrateLocalAccounts** es "true", esta variable debe contener la contraseña que se asigna a todas las cuentas locales migradas. USMT asigna la misma contraseña a todas las cuentas locales migradas. Considere esta contraseña como temporal y cámbiela más adelante por algún otro método.|  
|OSDMigrateAdditionalRestoreOptions<br /><br /> (entrada)|Especifica opciones adicionales de la línea de comandos de la herramienta de migración de estado de usuario (USMT) que se utilizan al restaurar el estado de usuario. Las opciones adicionales se especifican en la forma de una cadena que se anexa a la línea de comandos de USMT generada automáticamente. Las opciones de USMT especificadas con esta variable de secuencia de tareas no se validan para comprobar su exactitud antes de ejecutar la secuencia de tareas.|  
|_OSDMigrateUsmtRestorePackageID<br /><br /> (entrada)|Especifica el identificador del paquete de Configuration Manager que contiene los archivos de USMT. Esta variable es necesaria.|  



###  <a name="BKMK_RunCommand"></a> Ejecutar línea de comandos   
  Para obtener más información, consulte [Ejecutar línea de comandos](task-sequence-steps.md#BKMK_RunCommandLine).  

#### <a name="details"></a>Detalles  

|Nombre de variable de acción|Descripción|  
|--------------------------|-----------------|  
|SMSTSDisableWow64Redirection<br /><br /> (entrada)|De forma predeterminada en un sistema operativo de 64 bits, la secuencia de tareas busca y ejecuta el programa en la línea de comandos mediante el redirector del sistema de archivos WOW64. Este comportamiento permite que el comando encuentre las versiones de 32 bits de programas del sistema operativo y los archivos DLL. Si esta variable se establece en **true**, se deshabilita el uso del redirector del sistema de archivos WOW64. El comando busca las versiones nativas de 64 bits de programas del sistema operativo y archivos DLL. Esta variable no tiene ningún efecto cuando se ejecuta en un sistema operativo de 32 bits.|  
|WorkingDirectory<br /><br /> (entrada)|Especifica el directorio inicial de una acción de la línea de comandos. El nombre de directorio especificado no debe superar los 255 caracteres.<br /><br /> Ejemplo:<br /><br /> -   **C:\\**<br />-   **%SystemRoot%**|  
|SMSTSRunCommandLineUserName<br /><br /> (entrada)|Especifica la cuenta mediante la que se ejecuta la línea de comandos. El valor es una cadena con el formato nombredeusuario o dominio\nombredeusuario.|  
|SMSTSRunCommandLinePassword<br /><br /> (entrada)|Especifica la contraseña de la cuenta que especifica la variable SMSTSRunCommandLineUserName.|  



### <a name="set-dynamic-variables"></a>Establecer variables dinámicas  
Para obtener más información, consulte [Establecer variables dinámicas](task-sequence-steps.md#BKMK_SetDynamicVariables).  

#### <a name="details"></a>Detalles  

|Nombre de variable de acción<br /><br /> (entrada)|Descripción|  
|----------------------------------------|-----------------|  
|_SMSTSMake|Especifica la marca del equipo.|  
|_SMSTSModel|Especifica el modelo del equipo.|  
|_SMSTSMacAddresses|Especifica las direcciones MAC que usa el equipo.|  
|_SMSTSIPAddresses|Especifica las direcciones IP que usa el equipo.|  
|_SMSTSSerialNumber|Especifica el número de serie del equipo.|  
|_SMSTSAssetTag|Especifica la etiqueta de inventario del equipo.|  
|_SMSTSUUID|Especifica el UUID del equipo.|  
|_SMSTSDefaultGateways|Especifica las puertas de enlace predeterminadas que usa el equipo.|  



###  <a name="BKMK_SetupWindows"></a> Instalar Windows y Configuration Manager   
  Para obtener más información, consulte [Instalar Windows y Configuration Manager](task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr).  

#### <a name="details"></a>Detalles  

|Nombre de variable de acción<br /><br /> (entrada)|Descripción|  
|----------------------------------------|-----------------|  
|SMSClientInstallProperties<br /><br /> (entrada)|Especifica las propiedades de instalación del cliente que se usan al instalar el cliente de Configuration Manager.|  



### <a name="upgrade-operating-system"></a>Actualizar el sistema operativo  
 Para obtener más información, consulte [Actualizar el sistema operativo](task-sequence-steps.md#BKMK_UpgradeOS).  

#### <a name="details"></a>Detalles  

|Nombre de variable de acción<br /><br /> (entrada)|Descripción|  
|----------------------------------------|-----------------|  
|OSDSetupAdditionalUpgradeOptions<br /><br /> (entrada)|Especifica las opciones adicionales de la línea de comandos que se agregan al programa de instalación de Windows durante la actualización a Windows 10. La secuencia de tareas no verifica las opciones de línea de comandos.<br /><br /> Para más información, consulte [Opciones de la línea de comandos del programa de instalación de Windows](/windows-hardware/manufacture/desktop/windows-setup-command-line-options).|  
