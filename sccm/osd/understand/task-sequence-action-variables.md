---
title: "Variables de acción de secuencia de tareas | Configuration Manager"
description: "Use variables de acción de secuencia, como las variables de configuración de red, para especificar valores de configuración de un único paso en una secuencia de tareas de Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e2269031-0977-4f01-a274-420e00630575
caps.latest.revision: 10
caps.handback.revision: 0
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: cd0e74bff29110f5483c7132ba989d9933e7e223


---
# <a name="task-sequence-action-variables-in-system-center-configuration-manager"></a>Variables de acción de secuencias de tareas en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Las variables de acción de secuencias de tareas especifican los valores de configuración que se usan en un único paso de una secuencia de tareas de System Center Configuration Manager. De forma predeterminada, la configuración que se usa en una etapa de secuencia de tareas se inicializa antes de que la etapa se ejecute y solo está disponible mientras se ejecuta la etapa de secuencia de tareas asociada. En otras palabras, la configuración de variable de secuencia de tareas se agrega al entorno de secuencia de tareas antes de que se ejecute la etapa de secuencia de tareas, y se quita el valor del entorno de secuencia de tareas después de que se ejecute la etapa de secuencia de tareas.  

## <a name="action-variable-example"></a>Ejemplo de variable de acción  
 Por ejemplo, puede especificar un directorio de inicio para una acción de la línea de comandos si usa la etapa de la secuencia de tareas **Ejecutar línea de comandos** . Esta etapa incluye una propiedad **Iniciar en** cuyo valor predeterminado se almacena en el entorno de secuencia de tareas como la variable **WorkingDirectory** . La variable de entorno **WorkingDirectory** se inicializa antes de que se ejecute la acción de la secuencia de tareas **Ejecutar línea de comandos** . Durante la etapa **Ejecutar línea de comandos** , el valor de **WorkingDirectory** puede obtenerse a través de la propiedad **Empezar en** . A continuación, cuando la etapa de secuencia de tareas se ha completado, el valor de la variable **WorkingDirectory** se quita del entorno de secuencia de tareas. Si la secuencia contiene otra etapa de secuencia de tareas **Ejecutar línea de comandos** , la nueva variable **WorkingDirectory** se inicializa y se establece como el valor inicial para esa etapa.  

 Aunque el valor predeterminado de la configuración de una acción de secuencia de tareas está presente mientras se ejecuta el paso de secuencia de tareas, puede utilizarse cualquier valor nuevo que establezca en varios pasos de la secuencia. Si utiliza uno de los métodos de creación de variables de secuencia de tareas para invalidar el valor de una variable integrada, el nuevo valor permanece en el entorno y reemplaza el valor predeterminado del resto de etapas de la secuencia de tareas. En el ejemplo anterior, si se agrega un paso **Configurar variable de secuencia de tareas** como el primero de la secuencia de tareas y se establece la variable de entorno **WorkingDirectory** en el valor **C:\\**, los dos pasos **Ejecutar línea de comandos** de la secuencia de tareas usarán el nuevo valor de directorio inicial.  

## <a name="action-variables-for-task-sequence-actions"></a>Variables de acción de las acciones de secuencia de tareas  
 Las variables de la secuencia de tareas de Configuration Manager se agrupan por su acción de secuencia de tareas asociada. Consulte los vínculos siguientes para recopilar información sobre las variables de acción asociadas a una acción concreta. Las variables de secuencia de tareas controlan el funcionamiento de la acción de secuencia de tareas. La acción de secuencia de tareas lee o usa las variables marcadas como variables de entrada. De manera alternativa, las variables se pueden establecer como variables de tiempo de ejecución, a través de la acción para establecer variables de secuencia de tareas o a través del objeto COM TSEnvironment. La acción de secuencia de tareas es la única que marca las variables como variables de salida, de modo que las acciones posteriores puedan leerlas en la secuencia de tareas.  

> [!NOTE]  
>  No todas las acciones de las secuencias de tareas están asociadas a un conjunto de variables de secuencias de tareas. Por ejemplo, aunque hay variables asociadas a la acción Habilitar BitLocker, no hay ninguna variable asociada a la acción Deshabilitar BitLocker.  

###  <a name="a-namebkmkapplydataimagea-apply-data-image-task-sequence-action-variables"></a><a name="BKMK_ApplyDataImage"></a> Variables de acción de la secuencia de tareas Aplicar imagen de datos  
 Las variables de esta acción especifican qué imagen de un archivo WIM se debe aplicar al equipo de destino y si se deben eliminar los archivos de la partición de destino. Para obtener más información sobre el paso de secuencia de tareas asociado a estas variables, consulte [Paso de secuencia de tareas Aplicar imagen de datos](task-sequence-steps.md#BKMK_ApplyDataImage).  

#### <a name="details"></a>Detalles  

|Nombre de variable de acción|Descripción|  
|--------------------------|-----------------|  
|OSDDataImageIndex<br /><br /> (entrada)|Especifica el valor de índice de la imagen que se aplica al equipo de destino.|  
|OSDWipeDestinationPartition<br /><br /> (entrada)|Especifica si se deben eliminar los archivos ubicados en la partición de destino.<br /><br /> Valores válidos:<br /><br /> **"true"** (valor predeterminado)<br /><br /> **"false"**|  

###  <a name="a-namebkmkapplydriverpackagea-apply-driver-package-task-sequence-action-variables"></a><a name="BKMK_ApplyDriverPackage"></a> Variables de acción de la secuencia de tareas Aplicar paquetes de controladores  
 Las variables de esta acción especifican información sobre la instalación de controladores de almacenamiento masivo y si se van a instalar controladores sin firmar. Para obtener más información sobre el paso de secuencia de tareas asociado a estas variables, consulte [Aplicar paquete de controladores](task-sequence-steps.md#BKMK_ApplyDriverPackage).  

#### <a name="details"></a>Detalles  

|Nombre de variable de acción|Descripción|  
|--------------------------|-----------------|  
|OSDApplyDriverBootCriticalContentUniqueID<br /><br /> (entrada)|Especifica el identificador de contenido del controlador del dispositivo de almacenamiento masivo que se debe instalar desde el paquete de controladores. Si no se especifica, no se instala ningún controlador de almacenamiento masivo.|  
|OSDApplyDriverBootCriticalINFFile<br /><br /> (entrada)|Especifica el archivo INF del controlador de almacenamiento masivo que se debe instalar.<br /><br /> <br /><br /> Esta variable de secuencia de tareas es necesaria si se establece OSDApplyDriverBootCriticalContentUniqueID.|  
|OSDApplyDriverBootCriticalHardwareComponent<br /><br /> (entrada)|Especifica si hay un controlador de dispositivo de almacenamiento instalado, que debe ser **scsi**.<br /><br /> <br /><br /> Esta variable de secuencia de tareas es necesaria si se establece OSDApplyDriverBootCriticalContentUniqueID.|  
|OSDApplyDriverBootCriticalID<br /><br /> (entrada)|Especifica el identificador crítico para el arranque del controlador del dispositivo de almacenamiento masivo que se debe instalar. Este identificador se muestra en la sección "**scsi**" del archivo txtsetup.oem del controlador de dispositivo.<br /><br /> <br /><br /> Esta variable de secuencia de tareas es necesaria si se establece OSDApplyDriverBootCriticalContentUniqueID.|  
|OSDAllowUnsignedDriver<br /><br /> (entrada)|Especifica si se va a configurar Windows para permitir la instalación de controladores de dispositivos sin firmar. Esta variable de secuencia de tareas no se utiliza al implementar Windows Vista y sistemas operativos posteriores.<br /><br /> Valores válidos:<br /><br /> **"true"**<br /><br /> **"false"** (valor predeterminado)|  

###  <a name="a-namebkmkapplynetworksettingsa-apply-network-settings-task-sequence-action-variables"></a><a name="BKMK_ApplyNetworkSettings"></a> Variables de acción de la secuencia de tareas Aplicar configuración de red  
 Las variables de esta acción especifican la configuración de red del equipo de destino, como la configuración de los adaptadores de red del equipo, la configuración de dominio y la configuración de grupo de trabajo. Para obtener más información sobre el paso de secuencia de tareas asociado a estas variables, consulte [Paso Aplicar configuración de red](task-sequence-steps.md#BKMK_ApplyNetworkSettings).  

#### <a name="details"></a>Detalles  

|Nombre de variable de acción|Descripción|  
|--------------------------|-----------------|  
|OSDAdapter<br /><br /> (entrada)|Esta variable de secuencia de tareas es una variable de matriz. Cada elemento de la matriz representa la configuración de un único adaptador de red en el equipo. Es posible acceder a la configuración definida para cada adaptador mediante la combinación del nombre de la variable de matriz con el índice del adaptador de red basado en cero y el nombre de la propiedad.<br /><br /> <br /><br /> Si varios adaptadores de red se configurarán con esta acción de secuencia de tareas, las propiedades del segundo adaptador de red se definen utilizando su índice en el nombre de la variable; por ejemplo, OSDAdapter1EnableDHCP, OSDAdapter1IPAddressList, OSDAdapter1DNSDomain, OSDAdapter1WINSServerList, OSDAdapter1EnableWINS, etc.<br /><br /> <br /><br /> Por ejemplo, los siguientes nombres de variables pueden utilizarse para definir las propiedades del primer adaptador de red que se configurará mediante esta acción de secuencia de tareas:<br /><br /> <ul><li>**OSDAdapter0EnableDHCP:** su valor debe ser true para habilitar el Protocolo de configuración dinámica de host (DHCP) del adaptador.<br />    Esta opción es necesaria. Los valores posibles son: True o False.</li><li>**OSDAdapter0IPAddressList:** una lista delimitada por comas de direcciones IP del adaptador. Esta propiedad se omite a menos que el valor de **EnableDHCP** está establecido como **false**.<br />    Esta opción es necesaria.</li><li>**OSDAdapter0SubnetMask:** una lista delimitada por comas de las máscaras de subred. Esta propiedad se omite a menos que el valor de **EnableDHCP** está establecido como **false**.<br />    Esta opción es necesaria.</li><li>**OSDAdapter0Gateways:** una lista delimitada por comas de direcciones IP de puertas de enlace. Esta propiedad se omite a menos que el valor de **EnableDHCP** está establecido como **false**.<br />    Esta opción es necesaria.</li><li>**OSDAdapter0DNSDomain** : dominio del Sistema de nombres de dominio (DNS) del adaptador.</li><li>**OSDAdapter0DNSServerList:** una lista delimitada por comas de los servidores DNS del adaptador.<br />    Esta opción es necesaria.</li><li>**OSDAdapter0EnableDNSRegistration:** su valor debe ser **true** para registrar la dirección IP del adaptador del DNS.</li><li>**OSDAdapter0EnableFullDNSRegistration:** su valor debe ser **true** para registrar la dirección IP del adaptador del DNS con el nombre DNS completo del equipo.</li><li>**OSDAdapter0EnableIPProtocolFiltering:** su valor debe ser **true** para habilitar el filtrado de protocolo IP en el adaptador.</li><li>**OSDAdapter0IPProtocolFilterList:** una lista delimitada por comas de los protocolos que se pueden ejecutar a través de IP. Esta propiedad se omite si el valor de **EnableIPProtocolFiltering** está establecido en **false**.</li><li>**OSDAdapter0EnableTCPFiltering:** su valor debe ser **true** para habilitar el filtrado de puertos TCP del adaptador.</li><li>**OSDAdapter0TCPFilterPortList:** una lista delimitada por comas de puertos en los que se deben conceder permisos de acceso para TCP. Esta propiedad se omite si el valor de **EnableTCPFiltering** está establecido en **false**.</li><li>**OSDAdapter0TcpipNetbiosOptions:** opciones de NetBIOS sobre TCP/IP. Los valores posibles son:<br /><br /> <ul><li>0 Usar la configuración de NetBIOS del servidor DHCP.</li><li>1 Habilitar NetBIOS sobre TCP/IP.</li><li>2 Deshabilitar NetBIOS sobre TCP/IP.</li></ul></li><li>**OSDAdapter0EnableWINS:** su valor debe ser **true** si se quiere usar WINS para la resolución de nombres.</li><li>**OSDAdapter0WINSServerList:** una lista delimitada por comas de direcciones IP del servidor WINS. Esta propiedad se omite a menos que el valor de **EnableWINS** está establecido como **true**.</li><li>**OSDAdapter0MacAddress:** la dirección de Media Access Control (MAC) que se usa para hacer coincidir la configuración con el adaptador de red físico.</li><li>**OSDAdapter0Name:** nombre de la conexión de red tal y como aparece en el programa del panel de control de las conexiones de red. El nombre debe tener entre 0 y 255 caracteres.</li><li>**OSDAdapter0Index:** el índice de la configuración del adaptador de red en la matriz de valores.<br /><br />     OSDAdapterCount=1<br />    OSDAdapter0EnableDHCP=FALSE<br />    OSDAdapter0IPAddressList=192.168.0.40<br />    OSDAdapter0SubnetMask=255.255.255.0<br />    OSDAdapter0Gateways=192.168.0.1<br />    OSDAdapter0DNSSuffix=contoso.com</li></ul>|  
|OSDAdapterCount<br /><br /> (entrada)|Especifica el número de adaptadores de red instalados en el equipo de destino. Cuando se establece el valor de **OSDAdapterCount** , se deben establecer todas las opciones de configuración de cada uno de los adaptadores. Por ejemplo, si establece el valor de **OSDAdapterTCPIPNetbiosOptions** de un adaptador específico, todos los valores de ese adaptador también deben configurarse.<br /><br /> <br /><br /> Si no se especifica este valor, todos los valores de **OSDAdapter** se omiten.|  
|OSDDNSDomain<br /><br /> (entrada)|Especifica el servidor DNS principal que usa el equipo de destino.|  
|OSDDomainName<br /><br /> (entrada)|Especifica el nombre del dominio de Windows al que se une el equipo de destino. El valor especificado debe ser un nombre de dominio válido de Servicios de dominio de Active Directory.|  
|OSDDomainOUName<br /><br /> (entrada)|Especifica el nombre en formato RFC 1779 de la unidad organizativa (UO) a la que se une el equipo de destino. Si se especifica, el valor debe contener la ruta de acceso completa.<br /><br /> Ejemplo:<br /><br /> **LDAP://OU=MyOu,DC=MyDom,DC=MyCompany,DC=com**|  
|OSDEnableTCPIPFiltering<br /><br /> (entrada)|Especifica si el filtrado TCP/IP está habilitado.<br /><br /> Valores válidos:<br /><br /> **"true"**<br /><br /> **"false"** (valor predeterminado)|  
|OSDJoinAccount<br /><br /> (entrada)|Especifica la cuenta de red que se utiliza para agregar el equipo de destino a un dominio de Windows.|  
|OSDJoinPassword<br /><br /> (entrada)|Especifica la contraseña de red que se utiliza para agregar el equipo de destino a un dominio de Windows.|  
|OSDNetworkJoinType<br /><br /> (entrada)|Especifica si el equipo de destino se une a un dominio de Windows o a un grupo de trabajo.<br /><br /> **"0"** indica que el equipo de destino se une a un dominio de Windows. **"1"** especifica que el equipo se une a un grupo de trabajo.<br /><br /> Valores válidos:<br /><br /> **"0"**<br /><br /> **"1"**|  
|OSDDNSSuffixSearchOrder<br /><br /> (entrada)|Especifica el orden de búsqueda DNS del equipo de destino.|  
|OSDWorkgroupName<br /><br /> (entrada)|Especifica el nombre del grupo de trabajo al que se une el equipo de destino.<br /><br /> Debe especificar este valor o el valor de **OSDDomainName** . El nombre del grupo de trabajo puede tener un máximo de 32 caracteres.<br /><br /> Ejemplo:<br /><br /> **"Contabilidad"**|  

###  <a name="a-namebkmkapplyoperatingsystema-apply-operating-system-image-task-sequence-action-variables"></a><a name="BKMK_ApplyOperatingSystem"></a> Variables de acción de la secuencia de tareas Aplicar imagen de sistema operativo  
 Las variables de esta acción especifican la configuración del sistema operativo que quiere instalar en el equipo de destino. Para obtener más información sobre el paso de secuencia de tareas asociado a estas variables, consulte [Aplicar imagen de sistema operativo](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage).  

#### <a name="details"></a>Detalles  

|Nombre de variable de acción|Descripción|  
|--------------------------|-----------------|  
|OSDConfigFileName<br /><br /> (entrada)|Especifica el nombre del archivo de respuesta de implementación de sistema operativo asociado con el paquete de implementación de sistema operativo.|  
|OSDImageIndex<br /><br /> (entrada)|Especifica el valor de índice de la imagen del archivo WIM que se aplica al equipo de destino.|  
|OSDInstallEditionIndex<br /><br /> (entrada)|Especifica la versión de Windows Vista o del sistema operativo posterior que esté instalado. Si no se especifica ninguna versión, el programa de instalación de Windows determinará qué versión se debe instalar mediante la clave de producto referenciada.<br /><br /> Use solamente un valor de cero (0) si se cumplen las condiciones siguientes:<br /><br /> - Va a instalar un sistema operativo anterior a Windows Vista<br />- Va a instalar una edición de licencia por volumen de Windows Vista o una edición posterior, y no se especifica ninguna clave de producto.<br /><br /> Valores válidos:<br /><br /> **"0"** (valor predeterminado)|  
|OSDTargetSystemDrive (salida)|Especifica la letra de unidad de la partición que contiene los archivos del sistema operativo.|  

###  <a name="a-namebkmkapplywindowssettingsa-apply-windows-settings-task-sequence-action-variables"></a><a name="BKMK_ApplyWindowsSettings"></a> Variables de acción de la secuencia de tareas Aplicar configuración de Windows  
 Las variables de esta acción especifican la configuración de Windows del equipo de destino, como el nombre del equipo, la clave de producto de Windows, la organización y el usuario registrados, y la contraseña de administrador local. Para obtener más información sobre el paso de secuencia de tareas asociado a estas variables, consulte [Aplicar configuración de Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings).  

#### <a name="details"></a>Detalles  

|Nombre de variable de acción|Descripción|  
|--------------------------|-----------------|  
|OSDComputerName<br /><br /> (entrada)|Especifica el nombre del equipo de destino.<br /><br /> Ejemplo:<br /><br /> **"%_SMSTSMachineName%"** (valor predeterminado)|  
|OSDProductKey<br /><br /> (entrada)|Especifica la clave de producto de Windows. El valor especificado debe tener entre 1 y 255 caracteres.|  
|OSDRegisteredUserName<br /><br /> (entrada)|Especifica el nombre de usuario registrado de forma predeterminada en el nuevo sistema operativo. El valor especificado debe tener entre 1 y 255 caracteres.|  
|OSDRegisteredOrgName<br /><br /> (entrada)|Especifica el nombre de organización registrado de forma predeterminada en el nuevo sistema operativo. El valor especificado debe tener entre 1 y 255 caracteres.|  
|OSDTimeZone<br /><br /> (entrada)|Especifica la configuración de zona horaria predeterminada que se usa en el nuevo sistema operativo.|  
|OSDServerLicenseMode<br /><br /> (entrada)|Especifica el modo de licencia de Windows Server que se utiliza.<br /><br /> Valores válidos:<br /><br /> **"PerSeat"**<br /><br /> **"PerServer"**|  
|OSDServerLicenseConnectionLimit<br /><br /> (entrada)|Especifica el número máximo de conexiones permitidas. El número especificado debe estar comprendido en el intervalo entre 5 y 9999 conexiones.|  
|OSDRandomAdminPassword<br /><br /> (entrada)|Especifica una contraseña generada de forma aleatoria para la cuenta de administrador en el nuevo sistema operativo. Si se establece en **true**, se deshabilitará la cuenta de administrador local en el equipo de destino. Si se establece en **false**, se habilitará la cuenta de administrador local en el equipo de destino y se asignará a la contraseña de la cuenta de administrador local el valor de la variable **OSDLocalAdminPassword**.<br /><br /> Valores válidos:<br /><br /> **"true"** (valor predeterminado)<br /><br /> **"false"**|  
|OSDLocalAdminPassword<br /><br /> (entrada)|Especifica la contraseña del administrador local. Este valor se omite si se habilita la opción **Generar la contraseña de administrador local aleatoriamente y deshabilitar la cuenta en todas las plataformas admitidas** . El valor especificado debe tener entre 1 y 255 caracteres.|  

###  <a name="a-namebkmkautoapplydriversa-auto-apply-drivers-task-sequence-action-variables"></a><a name="BKMK_AutoApplyDrivers"></a> Variables de acción de la secuencia de tareas Aplicar controladores automáticamente  
 Las variables de esta acción especifican los controladores de Windows que están instalados en el equipo de destino y si hay controladores sin firmar instalados. Para obtener más información sobre el paso de secuencia de tareas asociado a estas variables, consulte [Aplicar controladores automáticamente](task-sequence-steps.md#BKMK_AutoApplyDrivers).  

#### <a name="details"></a>Detalles  

|Nombre de variable de acción|Descripción|  
|--------------------------|-----------------|  
|OSDAutoApplyDriverCategoryList<br /><br /> (entrada)|Una lista delimitada por comas de los identificadores únicos de las categorías del catálogo de controladores. Si se especifica, la acción de la secuencia de tareas **Aplicar controladores automáticamente** solamente tiene en cuenta aquellos controladores que se encuentren en al menos una de estas categorías al instalarlos. Este valor es opcional y no está establecido de forma predeterminada. Los identificadores de categoría disponibles pueden obtenerse mediante la enumeración de la lista de objetos **SMS_CategoryInstance** en el sitio.|  
|OSDAllowUnsignedDriver<br /><br /> (entrada)|Especifica si Windows está configurado para permitir que se instalen los controladores de dispositivos sin firmar. Esta variable de secuencia de tareas no se utiliza al implementar Windows Vista y sistemas operativos posteriores.<br /><br /> Valores válidos:<br /><br /> **"true"**<br /><br /> **"false"** (valor predeterminado)|  
|OSDAutoApplyDriverBestMatch<br /><br /> (entrada)|Especifica lo que hace la acción de secuencia de tareas si hay varios controladores de dispositivo en el catálogo de controladores que sean compatibles con un dispositivo de hardware. Si se establece en **"true"**, solo se instalará el mejor controlador de dispositivo.  Si su valor es **false**, se instalarán todos los controladores de dispositivo compatibles y el sistema operativo elegirá el mejor controlador que se debe usar.<br /><br /> Valores válidos:<br /><br /> **"true"** (valor predeterminado)<br /><br /> **"false"**|  

###  <a name="a-namebkmkcapturenetworksettingsa-capture-network-settings-task-sequence-action-variables"></a><a name="BKMK_CaptureNetworkSettings"></a> Variables de acción de la secuencia de tareas Capturar configuración de red  
 Las variables de esta acción especifican si se ha capturado información de configuración de los ajustes del adaptador de red (TCP/IP, DNS y WINS) y si la información de pertenencia a un grupo de trabajo o un dominio se migra como parte de la implementación de sistema operativo. Para obtener más información sobre el paso de secuencia de tareas asociado a estas variables, consulte [Capturar configuración de red](task-sequence-steps.md#BKMK_CaptureNetworkSettings).  

#### <a name="details"></a>Detalles  

|Nombre de variable de acción|Descripción|  
|--------------------------|-----------------|  
|OSDMigrateAdapterSettings<br /><br /> (entrada)|Especifica si se captura información de configuración de los ajustes del adaptador de red (TCP/IP, DNS y WINS).<br /><br /> Ejemplos:<br /><br /> **"true"** (valor predeterminado)<br /><br /> **"false"**|  
|OSDMigrateNetworkMembership<br /><br /> (entrada)|Especifica si se migra la información de pertenencia a un grupo de trabajo o un dominio como parte de la implementación de sistema operativo.<br /><br /> Ejemplos:<br /><br /> **"true"** (valor predeterminado)<br /><br /> **"false"**|  

###  <a name="a-namebkmkcaptureoperatingsystemimagea-capture-operating-system-image-task-sequence-action-variables"></a><a name="BKMK_CaptureOperatingSystemImage"></a> Variables de acción de la secuencia de tareas Capturar imagen de sistema operativo  
 Las variables de esta acción especifican información sobre la imagen de sistema operativo que se va a capturar, como el lugar donde se almacena la imagen, quién creó la imagen y una descripción de la imagen. Para obtener más información sobre el paso de secuencia de tareas asociado a estas variables, consulte [Capturar imagen de sistema operativo](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage).  

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

###  <a name="a-namebkmkcaptureuserstatea-capture-user-state-task-sequence-action-variables"></a><a name="BKMK_CaptureUserState"></a> Variables de acción de la secuencia de tareas Capturar estado de usuario  
 Las variables de esta acción especifican la información que utiliza la Herramienta de migración de estado de usuario (USMT), como la carpeta donde se guarda el estado de usuario, las opciones de la línea de comandos para USMT y los archivos de configuración que se utilizan para controlar la captura de los perfiles de usuario.  Para obtener más información sobre el paso de secuencia de tareas asociado a estas variables, consulte [Capturar estado de usuario](task-sequence-steps.md#BKMK_CaptureUserState).  

#### <a name="details"></a>Detalles  

|Nombre de variable de acción|Descripción|  
|--------------------------|-----------------|  
|OSDStateStorePath<br /><br /> (entrada)|La UNC o un nombre de ruta de acceso local de la carpeta donde se guarda el estado de usuario. Sin valor predeterminado.|  
|OSDMigrateAdditionalCaptureOptions<br /><br /> (entrada)|Especifica las opciones de la línea de comandos de la herramienta de migración de estado de usuario (USMT) que se usan al capturar el estado de usuario, pero no se exponen en la interfaz de usuario de Configuration Manager. Las opciones adicionales se especifican en la forma de una cadena que se anexa a la línea de comandos de USMT generada automáticamente.<br /><br /> <br /><br /> Las opciones de USMT especificadas con esta variable de secuencia de tareas no se validan para comprobar su exactitud antes de ejecutar la secuencia de tareas.|  
|OSDMigrateMode<br /><br /> (entrada)|Le permite personalizar los archivos que captura la USMT. Si esta variable se establece en "Simple", solo se usan los archivos de configuración de USMT estándares. Si esta variable se establece en "Advanced", la variable de secuencia de tareas OSDMigrateConfigFiles especifica los archivos de configuración que usa USMT.<br /><br /> Valores válidos:<br /><br /> **"Simple"**<br /><br /> **"Advanced"**|  
|OSDMigrateConfigFiles<br /><br /> (entrada)|Especifica los archivos de configuración que se utilizan para controlar la captura de perfiles de usuario. Esta variable se usa solo si el valor de OSDMigrateMode está establecido en "Advanced". Este valor de lista delimitada por comas está configurado para realizar una migración de perfiles de usuario personalizada.<br /><br /> Por ejemplo: miguser.xml,migsys.xml,migapps.xml|  
|OSDMigrateContinueOnLockedFiles<br /><br /> (entrada)|Permite que la captura del estado de usuario continúe si algunos archivos no se pueden capturar.<br /><br /> Valores válidos:<br /><br /> **"true"** (valor predeterminado)<br /><br /> **"false"**|  
|OSDMigrateEnableVerboseLogging<br /><br /> (entrada)|Habilita el registro detallado para la herramienta USMT.<br /><br /> Valores válidos:<br /><br /> **"true"**<br /><br /> **"false"** (valor predeterminado)|  
|OSDMigrateSkipEncryptedFiles<br /><br /> (entrada)|Especifica si se capturan los archivos cifrados.<br /><br /> Valores válidos:<br /><br /> **"true"**<br /><br /> **"false"** (valor predeterminado)|  
|_OSDMigrateUsmtPackageID<br /><br /> (entrada)|Especifica el identificador del paquete de Configuration Manager que contendrá los archivos de USMT. Esta variable es necesaria.|  

###  <a name="a-namebkmkcapturewindowssettingsa-capture-windows-settings-task-sequence-action-variables"></a><a name="BKMK_CaptureWindowsSettings"></a> Variables de acción de la secuencia de tareas Capturar configuración de Windows  
 Las variables de esta acción especifican si se migra una configuración específica de Windows al equipo de destino, como el nombre del equipo, el nombre de organización del registro y la información de zona horaria. Para obtener más información sobre el paso de secuencia de tareas asociado a estas variables, consulte [Capturar configuración de Windows](task-sequence-steps.md#BKMK_CaptureWindowsSettings).  

#### <a name="details"></a>Detalles  

|Nombre de variable de acción|Descripción|  
|--------------------------|-----------------|  
|OSDMigrateComputerName<br /><br /> (entrada)|Especifica si se migra el nombre del equipo.<br /><br /> Valores válidos:<br /><br /> **"true"** (valor predeterminado)<br /><br /> **"false"**<br /><br /> Si el valor es "true", la variable OSDComputerName se establece en el nombre NETBIOS del equipo.|  
|OSDComputerName<br /><br /> (salida)|Se establece con el nombre NETBIOS del equipo. El valor se establece solo si la variable OSDMigrateComputerName se establece en "true".|  
|OSDMigrateRegistrationInfo<br /><br /> (entrada)|Especifica si se migra el usuario del equipo y la información de la organización.<br /><br /> Valores válidos:<br /><br /> **"true"** (valor predeterminado)<br /><br /> **"false"**<br /><br /> Si el valor es "true", la variable OSDRegisteredOrgName se establece en el nombre de organización registrado del equipo.|  
|OSDRegisteredOrgName<br /><br /> (salida)|Se establece con el nombre de organización registrado del equipo. El valor se establece solo si la variable OSDMigrateRegistrationInfo se establece en "true".|  
|OSDMigrateTimeZone<br /><br /> (entrada)|Especifica si se migra la zona horaria del equipo.<br /><br /> Valores válidos:<br /><br /> **"true"** (valor predeterminado)<br /><br /> **"false"**<br /><br /> Si el valor es "true", la variable OSDTimeZone se establece en la zona horaria del equipo.|  
|OSDTimeZone<br /><br /> (salida)|Se establece con la zona horaria del equipo. El valor se establece solo si la variable OSDMigrateTimeZone se establece en "true".|  

###  <a name="a-namebkmkconnecttonetworkfoldera-connect-to-network-folder-task-sequence-action-variables"></a><a name="BKMK_ConnecttoNetworkFolder"></a> Variables de acción de la secuencia de tareas Conectarse a carpetas compartidas  
 Las variables de esta acción especifican información sobre una carpeta de una red, como la cuenta utilizada y la contraseña para conectarse a la carpeta de red, la letra de unidad de la carpeta y la ruta de acceso a la carpeta. Para obtener más información sobre el paso de secuencia de tareas asociado a estas variables, consulte [Conectar a carpeta de red](task-sequence-steps.md#BKMK_ConnectToNetworkFolder).  

#### <a name="details"></a>Detalles  

|Nombre de variable de acción|Descripción|  
|--------------------------|-----------------|  
|SMSConnectNetworkFolderAccount<br /><br /> (entrada)|Especifica la cuenta de administrador que se utiliza para conectarse al recurso compartido de red.|  
|SMSConnectNetworkFolderDriveLetter<br /><br /> (entrada)|Especifica la letra de unidad de la red a la que se debe conectar. Este valor es opcional; si no se especifica, la conexión de red no se asigna a una letra de unidad. Si se especifica este valor, debe estar en el intervalo de D: a Z:.  Además, no utilice X:, ya que es la letra de unidad que usa Windows PE durante la etapa de Windows PE.<br /><br /> Ejemplos:<br /><br /> **"D:"**<br /><br /> **"E:"**|  
|SMSConnectNetworkFolderPassword<br /><br /> (entrada)|Especifica la contraseña de red que se utiliza para conectarse al recurso compartido de red.|  
|SMSConnectNetworkFolderPath<br /><br /> (entrada)|Especifica la ruta de acceso de red para la conexión.<br /><br /> Ejemplo:<br /><br /> **"\\\nombreservidor\nombrerecursocompartido"**|  

###  <a name="a-namebkmkconvertdiska-convert-disk-to-dynamic-task-sequence-action-variables"></a><a name="BKMK_ConvertDisk"></a> Variables de acción de la secuencia de tareas Convertir el disco en dinámico  
 La variable de esta acción especifica el número del disco físico que se convertirá de disco básico a dinámico. Para obtener más información sobre el paso de secuencia de tareas asociado a estas variables, consulte [Convertir el disco en dinámico](task-sequence-steps.md#BKMK_ConvertDisktoDynamic).  

#### <a name="details"></a>Detalles  

|Nombre de variable de acción|Descripción|  
|--------------------------|-----------------|  
|OSDConvertDiskIndex<br /><br /> (entrada)|Especifica el número de disco físico que se convierte.|  

###  <a name="a-namebkmkenablebitlockera-enable-bitlocker-task-sequence-action-variables"></a><a name="BKMK_EnableBitLocker"></a> Variables de acción de la secuencia de tareas Habilitar BitLocker  
 Las variables de esta acción especifican las opciones de clave de inicio y la contraseña de recuperación que se utilizan para habilitar BitLocker en el equipo de destino. Para obtener más información sobre el paso de secuencia de tareas asociado a estas variables, consulte [Habilitar BitLocker](task-sequence-steps.md#BKMK_EnableBitLocker).  

#### <a name="details"></a>Detalles  

|Nombre de variable de acción|Descripción|  
|--------------------------|-----------------|  
|OSDBitLockerRecoveryPassword<br /><br /> (entrada)|En lugar de generar una contraseña aleatoria de recuperación, la acción de la secuencia de tareas **Habilitar BitLocker** usa el valor especificado como la contraseña de recuperación. El valor debe ser una contraseña numérica de recuperación de BitLocker válida.|  
|OSDBitLockerStartupKey<br /><br /> (entrada)|En lugar de generar una clave de inicio aleatoria para la opción de administración de claves **Clave de inicio solo en USB**, la acción de secuencia de tareas **Habilitar BitLocker** usa el Módulo de plataforma segura (TPM) como clave de inicio. El valor debe ser una clave de inicio válida de BitLocker de 256 bits con codificación Base64.|  

###  <a name="a-namebkmkformatpartitiondiska-format-and-partition-disk-task-sequence-action-variables"></a><a name="BKMK_FormatPartitionDisk"></a> Variables de acción de la secuencia de tareas Formatear y crear particiones en el disco  
 Las variables de esta acción especifican información de formato y creación de particiones de un disco físico, como el número de disco y una matriz de configuración de la partición. Para obtener más información sobre el paso de secuencia de tareas asociado a estas variables, consulte [Formatear y crear particiones en el disco](task-sequence-steps.md#BKMK_FormatandPartitionDisk).  

#### <a name="details"></a>Detalles  

|Nombre de variable de acción|Descripción|  
|--------------------------|-----------------|  
|OSDDiskIndex<br /><br /> (entrada)|Especifica el número de disco físico en el que se van a crear particiones.|  
|OSDDiskpartBiosCompatibilityMode<br /><br /> (entrada)|Especifica si se deben deshabilitar las optimizaciones de alineación de caché al crear particiones del disco duro, para que haya compatibilidad con ciertos tipos de BIOS. Esto puede ser necesario cuando se implementan sistemas operativos Windows XP o Windows Server 2003. Para más información, consulte el [artículo 931760](http://go.microsoft.com/fwlink/?LinkId=134081) y el [artículo 931761](http://go.microsoft.com/fwlink/?LinkId=134082) de Microsoft Knowledge Base.<br /><br /> Valores válidos:<br /><br /> **"true"**<br /><br /> **"false"** (valor predeterminado)|  
|OSDGPTBootDisk<br /><br /> (entrada)|Especifica si se debe crear una partición EFI en un disco duro GPT para que se puede usar como disco de inicio en equipos basados en EFI.<br /><br /> Valores válidos:<br /><br /> **"true"**<br /><br /> **"false"** (valor predeterminado)|  
|OSDPartitions<br /><br /> (entrada)|Especifica una matriz de configuración de la partición; vea el tema de SDK para acceder a las variables de la matriz en el entorno de la secuencia de tareas.<br /><br /> Esta variable de secuencia de tareas es una variable de matriz. Cada uno de los elementos de la matriz representa la configuración de una única partición en el disco duro. Es posible acceder a la configuración definida para cada partición mediante la combinación del nombre de la variable de matriz con el número de partición de disco basado en cero y el nombre de la propiedad.<br /><br /> Por ejemplo, los siguientes nombres de variables pueden utilizarse para definir las propiedades de la primera partición que se creará mediante esta acción de secuencia de tareas en el disco duro:<br /><br /> - **OSDPartitions0Type:** especifica el tipo de la partición. Se trata de una propiedad necesaria. Los valores válidos son "**Primary**", "**Extended**", "**Logical**" y "**Hidden**".<br />-   **OSDPartitions0FileSystem** : especifica el tipo de sistema de archivos que se utilizará al formatear la partición. Se trata de una propiedad opcional; si no se especifica ningún sistema de archivos, no se formateará la partición. Los valores válidos son "**FAT32**" y "**NTFS**".<br />-   **OSDPartitions0Bootable** : especifica si la partición es de arranque. Se trata de una propiedad necesaria. Si este valor se establece como "**TRUE**" en discos MBR, se convertirá en la partición activa.<br />-   **OSDPartitions0QuickFormat** : especifica el tipo de formato que se utiliza. Se trata de una propiedad necesaria. Si este valor se establece en "**TRUE**", se realizará un formato rápido; en caso contrario, se realizará un formato completo.<br />-   **OSDPartitions0VolumeName** : especifica el nombre que se asigna al volumen cuando se formatea. Se trata de una propiedad opcional.<br />-   **OSDPartitions0Size** : especifica el tamaño de la partición. Las unidades las especifica la variable **OSDPartitions0SizeUnits** . Se trata de una propiedad opcional. Si no se especifica esta propiedad, se crea la partición con todo el espacio libre restante.<br />-   **OSDPartitions0SizeUnits** : especifica las unidades que se utilizarán al interpretar la variable de secuencia de tareas **OSDPartitions0Size** . Se trata de una propiedad opcional. Los valores válidos son "**MB**" (predeterminado), "**GB**" y "**Percent**".<br />-   **OSDPartitions0VolumeLetterVariable** : las particiones siempre utilizan la siguiente letra de unidad disponible en Windows PE cuando se crean. Use esta propiedad opcional para especificar el nombre de otra variable de secuencia de tareas, que se utilizará para guardar la nueva letra de unidad para futuras referencias.<br /><br /> <br /><br /> Si se definirán varias particiones con esta acción de secuencia de tareas, las propiedades de la segunda partición pueden definirse a través de su índice en el nombre de la variable; por ejemplo, **OSDPartitions1Type**, **OSDPartitions1FileSystem**, **OSDPartitions1Bootable**, **OSDPartitions1QuickFormat**, **OSDPartitions1VolumeName** , etc.|  
|OSDPartitionStyle<br /><br /> (entrada)|Especifica el estilo de partición que se utilizará al crear particiones en el disco. "**MBR**" indica el estilo de partición de registro de arranque maestro y "**GPT**" indica el estilo de tabla de particiones GUID.<br /><br /> Valores válidos:<br /><br /> **"GPT"**<br /><br /> **"MBR"**|  

###  <a name="a-namebkmkinstallsoftwareupdatesa-install-software-updates-task-sequence-action-variables"></a><a name="BKMK_InstallSoftwareUpdates"></a> Variables de acción de la secuencia de tareas Instalar actualizaciones de software  
 La variable de esta acción especifica si se deben instalar todas las actualizaciones o solo las obligatorias. Para obtener más información sobre el paso de secuencia de tareas asociado a estas variables, consulte [Instalar actualizaciones de software](task-sequence-steps.md#BKMK_InstallSoftwareUpdates).  

#### <a name="details"></a>Detalles  

|Nombre de variable de acción<br /><br /> (entrada)|Descripción|  
|----------------------------------------|-----------------|  
|SMSInstallUpdateTarget<br /><br /> (entrada)|Especifica si se deben instalar todas las actualizaciones o solo las obligatorias.<br /><br /> Valores válidos:<br /><br /> **"All"**<br /><br /> **"Mandatory"**|  

###  <a name="a-namebkmkjoindomainworkgroupa-join-domain-or-workgroup-task-sequence-action-variables"></a><a name="BKMK_JoinDomainWorkgroup"></a> Variables de acción de secuencia de tareas de unión a un dominio o un grupo de trabajo  
 Las variables de esta acción especifican la información necesaria para unir el equipo de destino a un grupo de trabajo o un dominio de Windows. Para obtener más información sobre el paso de secuencia de tareas asociado a estas variables, consulte [Unirse a dominio o grupo de trabajo](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup).  

#### <a name="details"></a>Detalles  

|Nombre de variable de acción|Descripción|  
|--------------------------|-----------------|  
|OSDJoinAccount<br /><br /> (entrada)|Especifica la cuenta que utiliza el equipo de destino para unirse a un dominio de Windows. Esta variable es necesaria para unirse a un dominio.|  
|OSDJoinDomainName<br /><br /> (entrada)|Especifica el nombre de un dominio de Windows al que se une el equipo de destino. El nombre de dominio de Windows debe tener entre 1 y 255 caracteres.|  
|OSDJoinDomainOUName<br /><br /> (entrada)|Especifica el nombre en formato RFC 1779 de la unidad organizativa (UO) a la que se une el equipo de destino. Si se especifica, el valor debe contener la ruta de acceso completa. El nombre de la UO del dominio de Windows debe tener entre 0 y 32.767 caracteres. No se establece este valor si la variable **OSDJoinType** se establece como "1" (unirse al grupo de trabajo).<br /><br /> Ejemplo:<br /><br /> **LDAP://OU=MyOu,DC=MyDom,DC=MyCompany,DC=com**|  
|OSDJoinPassword<br /><br /> (entrada)|Especifica la contraseña de red que utiliza el equipo de destino para unirse al dominio de Windows. Si no se especifica la variable, se prueba con una contraseña en blanco. Este valor es necesario si la variable **OSDJoinType** se establece como "**0**" (unirse al dominio).|  
|OSDJoinSkipReboot<br /><br /> (entrada)|Especifica si se omite el reinicio después de que el equipo de destino se una al dominio o al grupo de trabajo.<br /><br /> Valores válidos:<br /><br /> **"true"**<br /><br /> **"false"**|  
|OSDJoinType<br /><br /> (entrada)|Especifica si el equipo de destino se une a un dominio de Windows o a un grupo de trabajo. Para unir el equipo de destino a un dominio de Windows, especifique "**0**". Para unir el equipo de destino a un grupo de trabajo, especifique "**1**".<br /><br /> Valores válidos:<br /><br /> **"0"**<br /><br /> **"1"**|  
|OSDJoinWorkgroupName<br /><br /> (entrada)|Especifica el nombre de un grupo de trabajo al que se une el equipo de destino. El nombre del grupo de trabajo debe tener entre 1 y 32 caracteres.<br /><br /> Ejemplo:<br /><br /> **"Contabilidad"**|  

###  <a name="a-namebkmkpreparewindowscapturea-prepare-windows-for-capture-task-sequence-action-variables"></a><a name="BKMK_PrepareWindowsCapture"></a> Variables de acción de la secuencia de tareas Preparar Windows para la captura  
 Las variables de esta acción especifican la información utilizada para capturar el sistema operativo Windows desde el equipo de destino. Para obtener más información sobre el paso de secuencia de tareas asociado a estas variables, consulte [Preparar el cliente de Configuration Manager para la captura](task-sequence-steps.md#BKMK_PrepareConfigMgrClientforCapture).  

#### <a name="details"></a>Detalles  

|Nombre de variable de acción|Descripción|  
|--------------------------|-----------------|  
|OSDBuildStorageDriverList<br /><br /> (entrada)|Especifica si sysprep crea una lista de controladores de dispositivos de almacenamiento masivo. Esta configuración se aplica únicamente a Windows XP y Windows Server 2003. Rellenará la sección [SysprepMassStorage] de sysprep.inf con información sobre todos los controladores de almacenamiento masivo que sean compatibles con la imagen que se va a capturar.<br /><br /> Valores válidos:<br /><br /> **"true"**<br /><br /> **"false"** (valor predeterminado)|  
|OSDKeepActivation<br /><br /> (entrada)|Especifica si sysprep restablece la marca de activación del producto.<br /><br /> Valores válidos:<br /><br /> **"true"**<br /><br /> **"false"** (valor predeterminado)|  
|OSDTargetSystemRoot<br /><br /> (salida)|Especifica la ruta de acceso al directorio de Windows del sistema operativo instalado en el equipo de referencia. Este sistema operativo se verifica como un sistema operativo compatible para la captura por parte de Configuration Manager.|  

###  <a name="a-namebkmkreleasestatestorea-release-state-store-sequence-action-variables"></a><a name="BKMK_ReleaseStateStore"></a> Variables de acción de la secuencia Liberar almacén de estado  
 Las variables de esta acción especifican la información que se utiliza para liberar el estado de usuario almacenado. Para obtener más información sobre el paso de secuencia de tareas asociado a estas variables, consulte [Liberar almacén de estado](task-sequence-steps.md#BKMK_ReleaseStateStore).  

#### <a name="details"></a>Detalles  

|Nombre de variable de acción|Descripción|  
|--------------------------|-----------------|  
|OSDStateStorePath<br /><br /> (entrada)|El nombre de la ruta de acceso local o UNC a la ubicación desde la que se restaura el estado de usuario. Este valor lo utilizan las acciones de secuencia de tareas **Capturar estado de usuario** y **Restaurar estado de usuario** .|  

###  <a name="a-namebkmkrequeststatea-request-state-store-task-sequence-action-variables"></a><a name="BKMK_RequestState"></a> Variables de acción de la secuencia de tareas Solicitar almacén de estado  
 Las variables de esta acción especifican la información que se usa para solicitar el estado de usuario almacenado, como la carpeta en el punto de migración de estado donde se almacenan los datos de usuario. Para obtener más información sobre el paso de secuencia de tareas asociado a estas variables, consulte [Liberar almacén de estado](../../osd/understand/task-sequence-steps.md#BKMK_ReleaseStateStore).  

#### <a name="details"></a>Detalles  

|Nombre de variable de acción|Descripción|  
|--------------------------|-----------------|  
|OSDStateFallbackToNAA<br /><br /> (entrada)|Especifica si se utiliza la cuenta de acceso de red como reserva cuando se produce un error en la cuenta de equipo para conectarse al punto de migración de estado.<br /><br /> Valores válidos:<br /><br /> **"true"**<br /><br /> **"false"** (valor predeterminado)|  
|OSDStateSMPRetryCount<br /><br /> (entrada)|Especifica el número de veces que esta etapa de la secuencia de tareas intenta encontrar un punto de migración de estado antes de que la etapa produzca un error. El número especificado debe estar entre 0 y 600.|  
|OSDStateSMPRetryTime<br /><br /> (entrada)|Especifica el número de segundos que espera entre reintentos la etapa de la secuencia de tareas. El número de segundos puede tener un máximo de 30 caracteres.|  
|OSDStateStorePath<br /><br /> (salida)|La ruta de acceso UNC a la carpeta en el punto de migración de estado donde se almacena el estado de usuario.|  

###  <a name="a-namebkmkrestartcomputera-restart-computer-task-sequence-action-variables"></a><a name="BKMK_RestartComputer"></a> Variables de acción de la secuencia de tareas Reiniciar equipo  
 Las variables de esta acción especifican la información que se utiliza para reiniciar el equipo de destino. Para obtener más información sobre el paso de secuencia de tareas asociado a estas variables, consulte [Reiniciar equipo](task-sequence-steps.md#a-namebkmkrestartcomputera-restart-computer).  

#### <a name="details"></a>Detalles  

|Nombre de variable de acción|Descripción|  
|--------------------------|-----------------|  
|SMSRebootMessage<br /><br /> (entrada)|Especifica el mensaje que se mostrará a los usuarios antes de reiniciar el equipo de destino. Si esta variable no está establecida, se mostrará un mensaje de texto predeterminado. El mensaje especificado no debe superar los 512 caracteres.<br /><br /> Ejemplo:<br /><br /> - "Este equipo se reiniciará; guarde su trabajo".|  
|SMSRebootTimeout<br /><br /> (entrada)|Especifica el número de segundos que se muestra la advertencia al usuario antes de reiniciar el equipo. Especifique cero segundos para indicar que no se muestre ningún mensaje de reinicio.<br /><br /> Ejemplos:<br /><br /> **"0"** (valor predeterminado)<br /><br /> **"5"**<br /><br /> **"10"**|  

###  <a name="a-namebkmkrestoreuserstatea-restore-user-state-task-sequence-action-variables"></a><a name="BKMK_RestoreUserState"></a> Variables de acción de la secuencia de tareas Restaurar estado de usuario  
 Las variables de esta acción especifican la información que se utiliza para restaurar el estado de usuario del equipo de destino, como el nombre de la ruta de acceso de la carpeta desde la que se restaura el estado de usuario y si se restaura la cuenta de equipo local. Para obtener más información sobre el paso de secuencia de tareas asociado a estas variables, consulte [Restaurar estado de usuario](task-sequence-steps.md#BKMK_RestoreUserState).  

#### <a name="details"></a>Detalles  

|Nombre de variable de acción|Descripción|  
|--------------------------|-----------------|  
|OSDStateStorePath<br /><br /> (entrada)|El nombre de la ruta de acceso local o UNC de la carpeta desde la que se restaura el estado de usuario.|  
|OSDMigrateContinueOnRestore<br /><br /> (entrada)|Especifica que la restauración del estado del usuario continuará incluso aunque algunos archivos no se puedan restaurar.<br /><br /> Valores válidos:<br /><br /> **"true"** (valor predeterminado)<br /><br /> **"false"**|  
|OSDMigrateEnableVerboseLogging<br /><br /> (entrada)|Habilita el registro detallado para la herramienta USMT. Este valor es necesario para la acción; se debe establecer en "true" o "false".<br /><br /> Valores válidos:<br /><br /> **"true"**<br /><br /> **"false"** (valor predeterminado)|  
|OSDMigrateLocalAccounts<br /><br /> (entrada)|Especifica si se restaura la cuenta de equipo local.<br /><br /> Valores válidos:<br /><br /> **"true"**<br /><br /> **"false"** (valor predeterminado)|  
|OSDMigrateLocalAccountPassword<br /><br /> (entrada)|Si la variable **OSDMigrateLocalAccounts** es "true", esta variable debe contener la contraseña que se asigna a todas las cuentas locales que se migran. Como se asigna la misma contraseña a todas las cuentas locales migradas, se considera una contraseña temporal que se cambiará más adelante mediante algún método que no sea una implementación de sistema operativo de Configuration Manager.|  
|OSDMigrateAdditionalRestoreOptions<br /><br /> (entrada)|Especifica opciones adicionales de la línea de comandos de la herramienta de migración de estado de usuario (USMT) que se utilizan al restaurar el estado de usuario. Las opciones adicionales se especifican en la forma de una cadena que se anexa a la línea de comandos de USMT generada automáticamente. Las opciones de USMT especificadas con esta variable de secuencia de tareas no se validan para comprobar su exactitud antes de ejecutar la secuencia de tareas.|  
|_OSDMigrateUsmtRestorePackageID<br /><br /> (entrada)|Especifica el identificador del paquete de Configuration Manager que contiene los archivos de USMT. Esta variable es necesaria.|  

###  <a name="a-namebkmkruncommanda-run-command-line-task-sequence-action-variables"></a><a name="BKMK_RunCommand"></a> Variables de acción de la secuencia de tareas Ejecutar línea de comandos  
 Las variables de esta acción especifican la información utilizada para ejecutar un comando desde la línea de comandos, como el directorio de trabajo donde se ejecuta el comando. Para obtener más información sobre el paso de secuencia de tareas asociado a estas variables, consulte [Ejecutar línea de comandos](task-sequence-steps.md#BKMK_RunCommandLine).  

#### <a name="details"></a>Detalles  

|Nombre de variable de acción|Descripción|  
|--------------------------|-----------------|  
|SMSTSDisableWow64Redirection<br /><br /> (entrada)|De forma predeterminada, cuando se ejecuta un sistema operativo de 64 bits, el programa de la línea de comandos se encuentra y ejecuta mediante el redirector del sistema de archivos WOW64, para que se encuentren las versiones de 32 bits de los  archivos DLL y los programas del sistema operativo. Si establece esta variable como "true", se deshabilita el uso del redirector del sistema de archivos WOW64 para que se puedan encontrar las versiones nativas de 64 bits de los archivos DLL y los programas del sistema operativo. Esta variable no tiene ningún efecto cuando se ejecuta en un sistema operativo de 32 bits.|  
|WorkingDirectory<br /><br /> (entrada)|Especifica el directorio inicial de una acción de la línea de comandos. El nombre de directorio especificado no debe superar los 255 caracteres.<br /><br /> Ejemplos:<br /><br /> -   **"C:\\"**<br />-   **"%SystemRoot%"**|  
|SMSTSRunCommandLineUserName<br /><br /> (entrada)|Especifica la cuenta mediante la que se ejecuta la línea de comandos. El valor es una cadena con el formato nombredeusuario o dominio\nombredeusuario.|  
|SMSTSRunCommandLinePassword<br /><br /> (entrada)|Especifica la contraseña de la cuenta que especifica la variable SMSTSRunCommandLineUserName.|  

### <a name="set-dynamic-variables"></a>Establecer variables dinámicas  
 Las variables de esta acción se establecen automáticamente cuando se agrega la etapa de secuencia de tareas Establecer variables dinámicas. Para obtener más información sobre el paso de secuencia de tareas asociado a estas variables, consulte [Establecer variables dinámicas](task-sequence-steps.md#BKMK_SetDynamicVariables).  

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

###  <a name="a-namebkmksetupwindowsa-setup-windows-and-configmgr-task-sequence-action-variables"></a><a name="BKMK_SetupWindows"></a> Variables de acción de la secuencia de tareas Instalar Windows y Configuration Manager  
 La variable de esta acción especifica las propiedades de instalación de cliente que se usan al instalar el cliente de Configuration Manager. Para obtener más información sobre el paso de secuencia de tareas asociado a estas variables, consulte [Instalar Windows y Configuration Manager](task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr).  

#### <a name="details"></a>Detalles  

|Nombre de variable de acción<br /><br /> (entrada)|Descripción|  
|----------------------------------------|-----------------|  
|SMSClientInstallProperties<br /><br /> (entrada)|Especifica las propiedades de instalación del cliente que se usan al instalar el cliente de Configuration Manager.|  

### <a name="upgrade-operating-system"></a>Actualizar el sistema operativo  
 La variable de esta acción especifica las opciones adicionales de la línea de comandos que no están disponibles en la consola de Configuration Manager y se agregan al programa de instalación para una actualización a Windows 10. Para obtener más información sobre el paso de secuencia de tareas asociado a esta variable, consulte [Actualizar sistema operativo](task-sequence-steps.md#BKMK_UpgradeOS).  

#### <a name="details"></a>Detalles  

|Nombre de variable de acción<br /><br /> (entrada)|Descripción|  
|----------------------------------------|-----------------|  
|OSDSetupAdditionalUpgradeOptions<br /><br /> (entrada)|Especifica las opciones adicionales de la línea de comandos que se agregan al programa de instalación durante la actualización a Windows 10. No se comprueban las opciones de la línea de comandos. Por lo tanto, compruebe que la opción que especifique sea precisa.<br /><br /> Para más información, consulte [Opciones de la línea de comandos del programa de instalación de Windows](https://msdn.microsoft.com/library/windows/hardware/dn938368\(v=vs.85\).aspx).|  



<!--HONumber=Nov16_HO1-->


