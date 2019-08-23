---
title: Referencia de variables de secuencia de tareas
titleSuffix: Configuration Manager
description: Obtenga información sobre las variables para controlar y personalizar una secuencia de tareas de Configuration Manager.
ms.date: 08/16/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 62f15230-d3a6-4afc-abd4-1e07e7ba6c97
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2283b87f305471f2831042f4b6b66d1c8a735b24
ms.sourcegitcommit: f7e4ff38d4b4afb49e3bccafa28514be406a9d7b
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/16/2019
ms.locfileid: "69549539"
---
# <a name="task-sequence-variables"></a>Variables de la secuencia de tareas

*Se aplica a: System Center Configuration Manager (Rama actual)*

Este artículo es una referencia para todas las variables disponibles en orden alfabético. Utilice la función **Buscar** (normalmente **CTRL** + **F**) para buscar una variable específica. La variable señala si es específica para un paso en particular. El artículo sobre los [pasos de la secuencia de tareas](/sccm/osd/understand/task-sequence-steps) incluye la lista de variables específicas de cada paso.

Para obtener más información, vea [Using task sequence variables](/sccm/osd/understand/using-task-sequence-variables) (Uso de las variables de la secuencia de tareas).

## <a name="bkmk_tsvar"></a> Referencia de variables de secuencia de tareas

### <a name="OSDDetectedWinDir"></a> _OSDDetectedWinDir

La secuencia de tareas examina las unidades de disco duro del equipo para ver si existe una instalación anterior del sistema operativo cuando se inicia Windows PE. La ubicación de la carpeta de Windows se almacena en esta variable. Puede configurar la secuencia de tareas para recuperar este valor del entorno y utilizarlo para especificar la misma ubicación de carpeta de Windows para la nueva instalación del sistema operativo.

### <a name="OSDDetectedWinDrive"></a> _OSDDetectedWinDrive

La secuencia de tareas examina las unidades de disco duro del equipo para ver si existe una instalación anterior del sistema operativo cuando se inicia Windows PE. La ubicación de la unidad de disco duro donde está instalado el sistema operativo se almacena en esta variable. Puede configurar la secuencia de tareas para recuperar este valor del entorno y utilizarlo para especificar la misma ubicación de unidad de disco duro para el nuevo sistema operativo.

### <a name="OSDMigrateUsmtPackageID"></a> _OSDMigrateUsmtPackageID

*Se aplica al paso [Capturar estado de usuario](task-sequence-steps.md#BKMK_CaptureUserState).*

(entrada)

Especifica el identificador del paquete de Configuration Manager que contiene los archivos de USMT. Esta variable es necesaria.

### <a name="OSDMigrateUsmtRestorePackageID"></a> _OSDMigrateUsmtRestorePackageID

*Se aplica al paso [Restaurar estado de usuario](task-sequence-steps.md#BKMK_RestoreUserState).*

(entrada)

Especifica el identificador del paquete de Configuration Manager que contiene los archivos de USMT. Esta variable es necesaria.

### <a name="SMSTSAdvertID"></a> _SMSTSAdvertID

Almacena el id. único de implementación de secuencia de tareas en ejecución. Usa el mismo formato que un identificador de implementación de distribución de software de Configuration Manager. Si la secuencia de tareas se está ejecutando desde un medio independiente, esta variable no se define.

#### <a name="example"></a>Ejemplo

`ABC20001`

### <a name="SMSTSAssetTag"></a> _SMSTSAssetTag

*Se aplica al paso [Establecer variables dinámicas](task-sequence-steps.md#BKMK_SetDynamicVariables).*

Especifica la etiqueta de inventario del equipo.

### <a name="SMSTSBootImageID"></a> _SMSTSBootImageID

Si la secuencia de tareas que se ejecuta actualmente hace referencia a un paquete de imagen de arranque, esta variable almacena el identificador del paquete de imagen de arranque. Si la secuencia de tareas no hace referencia a un paquete de imagen de arranque, no se establece esta variable.

#### <a name="example"></a>Ejemplo

`ABC00001`  

### <a name="SMSTSBootUEFI"></a> _SMSTSBootUEFI

La secuencia de tareas establece esta variable cuando detecta un equipo que está en modo UEFI.

### <a name="SMSTSClientCache"></a> _SMSTSClientCache

<!-- SCCMDocs issue 1400 -->
La secuencia de tareas establece esta variable cuando almacena en caché contenido en la unidad local. La variable contiene la ruta de acceso a la caché. Si esta variable no existe, no hay ninguna caché.

### <a name="SMSTSClientGUID"></a> _SMSTSClientGUID

Almacena el valor del GUID del cliente de Configuration Manager. Si la secuencia de tareas se está ejecutando desde un medio independiente, esta variable no se define.

#### <a name="example"></a>Ejemplo

`0a1a9a4b-fc56-44f6-b7cd-c3f8ee37c04c`

### <a name="SMSTSCurrentActionName"></a> _SMSTSCurrentActionName

Especifica el nombre del paso de la secuencia de tareas actualmente en ejecución. Esta variable se establece antes de que el administrador de la secuencia de tareas ejecute cada paso individual.

#### <a name="example"></a>Ejemplo

`run command line`

### <a name="SMSTSDefaultGateways"></a> _SMSTSDefaultGateways

*Se aplica al paso [Establecer variables dinámicas](task-sequence-steps.md#BKMK_SetDynamicVariables).*

Especifica las puertas de enlace predeterminadas que usa el equipo.

### <a name="SMSTSDownloadOnDemand"></a> _SMSTSDownloadOnDemand

Si la secuencia de tareas actual se ejecuta en modo de descarga a petición, esta variable es `true`. El modo de descarga a petición significa que el administrador de la secuencia de tareas descarga contenido localmente solo cuando debe acceder al contenido.

### <a name="SMSTSInWinPE"></a> _SMSTSInWinPE

Si el paso de secuencia de tareas actual se ejecuta en Windows PE, esta variable es `true`. Pruebe esta variable de secuencia de tareas para saber cuál es el entorno de sistema operativo actual.

### <a name="SMSTSIPAddresses"></a> _SMSTSIPAddresses

*Se aplica al paso [Establecer variables dinámicas](task-sequence-steps.md#BKMK_SetDynamicVariables).*

Especifica las direcciones IP que usa el equipo.

### <a name="SMSTSLastActionName"></a> _SMSTSLastActionName

*A partir de la versión 1810*  

Almacena el nombre de la última acción que se ha ejecutado. Esta variable está relacionada con **_SMSTSLastActionRetCode**. La secuencia de tareas registra estos valores en el archivo smsts.log. Esta variable es beneficiosa al solucionar problemas de una secuencia de tareas. Cuando se produce un error en un paso, un script personalizado puede incluir el nombre del paso junto con el código de retorno.

### <a name="SMSTSLastActionRetCode"></a> _SMSTSLastActionRetCode

Almacena el código de retorno de la última acción que se ha ejecutado. Esta variable se puede usar como una condición para saber si el siguiente paso se ejecuta.

#### <a name="example"></a>Ejemplo

`0`

### <a name="SMSTSLastActionSucceeded"></a> _SMSTSLastActionSucceeded

- Si el último paso se completó correctamente, esta variable es `true`.  

- Si se produce un error en el último paso, es `false`.  

- Si la secuencia de tareas omitió la última acción debido a que el paso está deshabilitado o la condición asociada se evaluó como **false**, esta variable no se restablece. y sigue teniendo el valor de la acción anterior.  

### <a name="SMSTSLastContentDownloadLocation"></a>_SMSTSLastContentDownloadLocation

<!-- 2840337 -->
A partir de la versión 1906, esta variable contiene la última ubicación donde la secuencia de tareas ha descargado o intentado descargar el contenido. Inspeccione esta variable en lugar de analizar los registros de cliente para esta ubicación de contenido.

### <a name="SMSTSLaunchMode"></a> _SMSTSLaunchMode

Especifica que la secuencia de tareas se inició a través de uno de los métodos siguientes:  

- **SMS**: el cliente de Configuration Manager, como cuando un usuario lo inicia desde el Centro de Software
- **UFD**: un medio USB heredado
- **UFD+FORMAT**: un medio USB más reciente
- **CD**: un CD de arranque
- **DVD**: un DVD de arranque
- **PXE**: arranque de red con PXE
- **HD**: un medio preconfigurado en un disco duro

### <a name="SMSTSLogPath"></a> _SMSTSLogPath

Almacena la ruta de acceso completa del directorio de registro. Use este valor para determinar dónde registran sus acciones los pasos de la secuencia de tareas. Este valor no se establece si no hay una unidad de disco duro disponible.

### <a name="SMSTSMacAddresses"></a> _SMSTSMacAddresses

*Se aplica al paso [Establecer variables dinámicas](task-sequence-steps.md#BKMK_SetDynamicVariables).*

Especifica las direcciones MAC que usa el equipo.

### <a name="SMSTSMachineName"></a> _SMSTSMachineName

Almacena y especifica el nombre del equipo. Almacena el nombre del equipo que la secuencia de tareas utiliza para registrar todos los mensajes de estado. Para cambiar el nombre del equipo en el nuevo sistema operativo, use la variable [OSDComputerName](#OSDComputerName-input).

### <a name="SMSTSMake"></a> _SMSTSMake

*Se aplica al paso [Establecer variables dinámicas](task-sequence-steps.md#BKMK_SetDynamicVariables).*

Especifica la marca del equipo.

### <a name="SMSTSMDataPath"></a> _SMSTSMDataPath

Especifica la ruta de acceso definida por la variable [SMSTSLocalDataDrive](#SMSTSLocalDataDrive). Si SMSTSLocalDataDrive se define antes de iniciar la secuencia de tareas (por ejemplo, al establecer una variable de la recopilación), Configuration Manager define la variable _SMSTSMDataPath después de que se inicie la secuencia de tareas.

### <a name="SMSTSMediaType"></a> _SMSTSMediaType

Especifica el tipo de medio que se usa para iniciar la instalación. Algunos ejemplos de tipos de medios son medios de arranque, medios completos, PXE y medios preconfigurados.

### <a name="SMSTSModel"></a> _SMSTSModel

*Se aplica al paso [Establecer variables dinámicas](task-sequence-steps.md#BKMK_SetDynamicVariables).*

Especifica el modelo del equipo.

### <a name="SMSTSMP"></a> _SMSTSMP

Almacena la dirección URL o IP de un punto de administración de Configuration Manager.

### <a name="SMSTSMPPort"></a> _SMSTSMPPort

Almacena el número de puerto de un punto de administración de Configuration Manager.

### <a name="SMSTSOrgName"></a> _SMSTSOrgName

Almacena el nombre del título de personalización de marca que la secuencia de tareas muestra en el cuadro de diálogo de progreso.

### <a name="SMSTSOSUpgradeActionReturnCode"></a> _SMSTSOSUpgradeActionReturnCode

*Se aplica al paso [Actualizar sistema operativo](task-sequence-steps.md#BKMK_UpgradeOS).*

Almacena el valor de código de salida devuelto por el programa de instalación de Windows que indica si la operación se ha realizado correctamente o no. Esta variable es útil con la opción de línea de comandos `/Compat`.

#### <a name="example"></a>Ejemplo

Al completarse el análisis de solo compatibilidad, se realizan acciones en pasos posteriores en función de si el código de salida es correcto o incorrecto. Si se ejecuta correctamente, inicie la actualización. O establezca un marcador en el entorno para recopilar con el inventario de hardware. Por ejemplo, agregue un archivo o establezca una clave del Registro. Utilice este marcador para crear una colección de equipos que estén preparados para actualizarse o que requieran una acción antes de la actualización.

### <a name="SMSTSPackageID"></a> _SMSTSPackageID

Almacena el identificador de la secuencia de tareas que se ejecuta actualmente. Este identificador usa el mismo formato que un identificador de paquete de Configuration Manager.

#### <a name="example"></a>Ejemplo

`HJT00001`

### <a name="SMSTSPackageName"></a> _SMSTSPackageName

Almacena el nombre de la secuencia de tareas que se ejecuta actualmente. Un administrador de Configuration Manager especifica este nombre al crear la secuencia de tareas.

#### <a name="example"></a>Ejemplo

`Deploy Windows 10 task sequence`

### <a name="SMSTSRunFromDP"></a> _SMSTSRunFromDP

Se configura en `true` si la secuencia de tareas actual se ejecuta en modo de ejecución desde un punto de distribución. Este modo significa que el administrador de la secuencia de tareas obtiene los recursos compartidos de paquete necesarios de un punto de distribución.

### <a name="SMSTSSerialNumber"></a> _SMSTSSerialNumber

*Se aplica al paso [Establecer variables dinámicas](task-sequence-steps.md#BKMK_SetDynamicVariables).*

Especifica el número de serie del equipo.

### <a name="SMSTSSetupRollback"></a> _SMSTSSetupRollback

Especifica si el programa de instalación de Windows realiza una operación de reversión durante una actualización local. Los valores de la variable pueden ser `true` o `false`.

### <a name="SMSTSSiteCode"></a> _SMSTSSiteCode

Almacena el código de sitio de Configuration Manager.

#### <a name="example"></a>Ejemplo

`ABC`

### <a name="SMSTSTimezone"></a> _SMSTSTimezone

Esta variable almacena la información de zona horaria con el siguiente formato:

```
Bias,StandardBias,DaylightBias,StandardDate.wYear,wMonth,wDayOfWeek,wDay,wHour,wMinute,wSecond,wMilliseconds,DaylightDate.wYear,wMonth,wDayOfWeek,wDay,wHour,wMinute,wSecond,wMilliseconds,StandardName,DaylightName
```

#### <a name="example"></a>Ejemplo

Para la zona horaria **Hora oriental (EE. UU. y Canadá)** :

```
300,0,-60,0,11,0,1,2,0,0,0,0,3,0,2,2,0,0,0,Eastern Standard Time,Eastern Daylight Time
```

### <a name="SMSTSType"></a> _SMSTSType

Especifica el tipo de la secuencia de tareas que se ejecuta actualmente. Puede tener uno de los siguientes valores:  

- **1** : una secuencia de tareas genérica
- **2**: una secuencia de tareas de implementación de SO

### <a name="SMSTSUseCRL"></a> _SMSTSUseCRL

Si la secuencia de tareas utiliza HTTPS para comunicarse con el punto de administración, esta variable especifica si usa la lista de revocación de certificados (CRL).

### <a name="SMSTSUserStarted"></a> _SMSTSUserStarted

Especifica si un usuario inició una secuencia de tareas. Esta variable se establece únicamente si la secuencia de tareas se inició desde el Centro de software. Por ejemplo, si [_SMSTSLaunchMode](#SMSTSLaunchMode) está establecido en `SMS`.

Esta variable puede tener los siguientes valores:  

- `true`: indica que un usuario inició la secuencia de tareas manualmente desde el Centro de software.  

- `false`: indica que el programador de Configuration Manager inició automáticamente la secuencia de tareas.

### <a name="SMSTSUseSSL"></a> _SMSTSUseSSL

Especifica si la secuencia de tareas usa SSL para comunicarse con el punto de administración de Configuration Manager. Si configura los sistemas de sitio para HTTPS, el valor se establece en `true`.

### <a name="SMSTSUUID"></a> _SMSTSUUID

*Se aplica al paso [Establecer variables dinámicas](task-sequence-steps.md#BKMK_SetDynamicVariables).*

Especifica el UUID del equipo.

### <a name="SMSTSWTG"></a> _SMSTSWTG

Especifica si el equipo se ejecuta como un dispositivo Windows To Go.

### <a name="TSAppInstallStatus"></a> _TSAppInstallStatus

La secuencia de tareas establece esta variable con el estado de la instalación de la aplicación durante el paso [Instalar aplicación](task-sequence-steps.md#BKMK_InstallApplication). Establece uno de los siguientes valores:  

- **Sin definir**: no se ha ejecutado el paso Instalar aplicación.  

- **Error**: al menos una aplicación genera error durante el paso Instalar aplicación.  

- **Advertencia**: no se produjeron errores durante el paso Instalar aplicación. Una o varias aplicaciones (o una dependencia necesaria) no se instalaron porque no se cumplió un requisito.  

- **Correcto**: no se detectaron errores ni advertencias durante el paso Instalar aplicación.  

### <a name="OSDAdapter"></a> OSDAdapter

*Se aplica al paso [Aplicar configuración de red](task-sequence-steps.md#BKMK_ApplyNetworkSettings).*

(entrada)

Esta variable de secuencia de tareas es una variable de *matriz*. Cada elemento de la matriz representa la configuración de un único adaptador de red en el equipo. El acceso a la configuración de cada adaptador se realiza mediante la combinación del nombre de la variable de matriz con el índice del adaptador de red basado en cero y el nombre de la propiedad.

Si el paso Aplicar configuración de red configura varios adaptadores de red, las propiedades del *segundo* adaptador de red se definen mediante el uso del índice **1** en el nombre de variable. Por ejemplo: OSDAdapter1EnableDHCP, OSDAdapter1IPAddressList y OSDAdapter1DNSDomain.

Use los siguientes nombres de variable para definir las propiedades del *primer* adaptador de red para el paso para configurar:

#### <a name="osdadapter0enabledhcp"></a>OSDAdapter0EnableDHCP

Esta opción es necesaria. Los valores posibles son `True` o `False`. Por ejemplo:

`true`: habilitar el Protocolo de configuración dinámica de host (DHCP) del adaptador

#### <a name="osdadapter0ipaddresslist"></a>OSDAdapter0IPAddressList

Una lista delimitada por comas de direcciones IP del adaptador. Esta propiedad se omite a menos que el valor de **EnableDHCP** está establecido como `false`. Esta opción es necesaria.

#### <a name="osdadapter0subnetmask"></a>OSDAdapter0SubnetMask

Una lista delimitada por comas de las máscaras de subred. Esta propiedad se omite a menos que el valor de **EnableDHCP** está establecido como `false`. Esta opción es necesaria.

#### <a name="osdadapter0gateways"></a>OSDAdapter0Gateways

Una lista delimitada por comas de direcciones IP de puertas de enlace. Esta propiedad se omite a menos que el valor de **EnableDHCP** está establecido como `false`. Esta opción es necesaria.

#### <a name="osdadapter0dnsdomain"></a>OSDAdapter0DNSDomain

Dominio del Sistema de nombres de dominio (DNS) del adaptador.

#### <a name="osdadapter0dnsserverlist"></a>OSDAdapter0DNSServerList

Una lista delimitada por comas de los servidores DNS del adaptador. Esta opción es necesaria.

#### <a name="osdadapter0enablednsregistration"></a>OSDAdapter0EnableDNSRegistration

Establézcalo en `true` para registrar la dirección IP del adaptador en DNS.

#### <a name="osdadapter0enablefulldnsregistration"></a>OSDAdapter0EnableFullDNSRegistration

Establézcalo en `true` para registrar la dirección IP del adaptador del DNS con el nombre DNS completo del equipo.

#### <a name="osdadapter0enableipprotocolfiltering"></a>OSDAdapter0EnableIPProtocolFiltering

Establézcalo en `true` para habilitar el filtrado de protocolo IP en el adaptador.

#### <a name="osdadapter0ipprotocolfilterlist"></a>OSDAdapter0IPProtocolFilterList

Una lista delimitada por comas de los protocolos que se pueden ejecutar a través de IP. Esta propiedad se omite si el valor de **EnableIPProtocolFiltering** está establecido en `false`.

#### <a name="osdadapter0enabletcpfiltering"></a>OSDAdapter0EnableTCPFiltering

Establézcalo en `true` para habilitar el filtrado de puertos TCP para el adaptador.

#### <a name="osdadapter0tcpfilterportlist"></a>OSDAdapter0TCPFilterPortList

Una lista delimitada por comas de puertos en los que se deben conceder permisos de acceso para TCP. Esta propiedad se omite si el valor de **EnableTCPFiltering** está establecido en `false`.

#### <a name="osdadapter0tcpipnetbiosoptions"></a>OSDAdapter0TcpipNetbiosOptions

Opciones para NetBIOS sobre TCP/IP. Los valores posibles son:  

- `0`: usar la configuración de NetBIOS del servidor DHCP  
- `1`: habilitar NetBIOS sobre TCP/IP  
- `2`: deshabilitar NetBIOS sobre TCP/IP  

#### <a name="osdadapter0enablewins"></a>OSDAdapter0EnableWINS

Establézcalo en `true` para utilizar WINS para la resolución de nombres.

#### <a name="osdadapter0winsserverlist"></a>OSDAdapter0WINSServerList

Una lista delimitada por comas de direcciones IP del servidor WINS. Esta propiedad se omite a menos que el valor de **EnableWINS** está establecido como `true`.

#### <a name="osdadapter0macaddress"></a>OSDAdapter0MacAddress

La dirección MAC que se usa para hacer coincidir la configuración con el adaptador de red físico.

#### <a name="osdadapter0name"></a>OSDAdapter0Name

El nombre de la conexión de red tal y como aparece en el programa del panel de control de las conexiones de red. El nombre debe tener entre 0 y 255 caracteres.

#### <a name="osdadapter0index"></a>OSDAdapter0Index

El índice de la configuración del adaptador de red en la matriz de valores.

#### <a name="example"></a>Ejemplo

- **OSDAdapterCount** = `1`  
- **OSDAdapter0EnableDHCP** = `FALSE`  
- **OSDAdapter0IPAddressList** = `192.168.0.40`  
- **OSDAdapter0SubnetMask** = `255.255.255.0`  
- **OSDAdapter0Gateways** = `192.168.0.1`  
- **OSDAdapter0DNSSuffix** = `contoso.com`  

### <a name="OSDAdapterCount"></a> OSDAdapterCount

*Se aplica al paso [Aplicar configuración de red](task-sequence-steps.md#BKMK_ApplyNetworkSettings).*

(entrada)

Especifica el número de adaptadores de red instalados en el equipo de destino. Cuando se establece el valor de **OSDAdapterCount**, se deben establecer todas las opciones de configuración de cada uno de los adaptadores.

Por ejemplo, si establece el valor de **OSDAdapter0TCPIPNetbiosOptions** del primer adaptador, debe configurar todos los valores de ese adaptador.

Si no especifica este valor, la secuencia de tareas omite todos los valores de **OSDAdapter**.

### <a name="OSDApplyDriverBootCriticalContentUniqueID"></a> OSDApplyDriverBootCriticalContentUniqueID

*Se aplica al paso [Aplicar paquete de controladores](task-sequence-steps.md#BKMK_ApplyDriverPackage).*

(entrada)

Especifica el identificador de contenido del controlador del dispositivo de almacenamiento masivo que se debe instalar desde el paquete de controladores. Si no se especifica esta variable, no se instala ningún controlador de almacenamiento masivo.

### <a name="OSDApplyDriverBootCriticalHardwareComponent"></a> OSDApplyDriverBootCriticalHardwareComponent

*Se aplica al paso [Aplicar paquete de controladores](task-sequence-steps.md#BKMK_ApplyDriverPackage).*

(entrada)

Especifica si hay un controlador de dispositivo de almacenamiento instalado; esta variable debe ser **scsi**.

Esta variable es necesaria si se establece [OSDApplyDriverBootCriticalContentUniqueID](#OSDApplyDriverBootCriticalContentUniqueID).

### <a name="OSDApplyDriverBootCriticalID"></a> OSDApplyDriverBootCriticalID

*Se aplica al paso [Aplicar paquete de controladores](task-sequence-steps.md#BKMK_ApplyDriverPackage).*

(entrada)

Especifica el identificador crítico para el arranque del controlador del dispositivo de almacenamiento masivo que se debe instalar. Este identificador se muestra en la sección **scsi** del archivo txtsetup.oem del controlador de dispositivo.

Esta variable es necesaria si se establece [OSDApplyDriverBootCriticalContentUniqueID](#OSDApplyDriverBootCriticalContentUniqueID).

### <a name="OSDApplyDriverBootCriticalINFFile"></a> OSDApplyDriverBootCriticalINFFile

*Se aplica al paso [Aplicar paquete de controladores](task-sequence-steps.md#BKMK_ApplyDriverPackage).*

(entrada)

Especifica el archivo INF del controlador de almacenamiento masivo que se debe instalar.

Esta variable es necesaria si se establece [OSDApplyDriverBootCriticalContentUniqueID](#OSDApplyDriverBootCriticalContentUniqueID).

### <a name="OSDAutoApplyDriverBestMatch"></a> OSDAutoApplyDriverBestMatch

*Se aplica al paso [Aplicar controladores automáticamente](task-sequence-steps.md#BKMK_AutoApplyDrivers).*

(entrada)

Si hay varios controladores de dispositivo en el catálogo de controladores que sean compatibles con un dispositivo de hardware, esta variable determina la acción del paso.

#### <a name="valid-values"></a>Valores válidos

- `true` (valor predeterminado): instalar solo el mejor controlador de dispositivo  

- `false`: instala todos los controladores de dispositivo compatibles y Windows elige el mejor controlador  

### <a name="OSDAutoApplyDriverCategoryList"></a> OSDAutoApplyDriverCategoryList

*Se aplica al paso [Aplicar controladores automáticamente](task-sequence-steps.md#BKMK_AutoApplyDrivers).*

(entrada)

Una lista delimitada por comas de los identificadores únicos de las categorías del catálogo de controladores. El paso **Aplicar controladores automáticamente** solo tiene en cuenta los controladores de al menos una de las categorías especificadas. Este valor es opcional y no está establecido de forma predeterminada. Obtenga los identificadores de categoría disponibles mediante la enumeración de la lista de objetos **SMS_CategoryInstance** en el sitio.

### <a name="OSDBitLockerRebootCount"></a>OSDBitLockerRebootCount

*Se aplica al paso [Deshabilitar BitLocker](task-sequence-steps.md#BKMK_DisableBitLocker).*

<!-- 4512937 -->
A partir de la versión 1906, utilice esta variable para establecer el número de reinicios después del cual reanudar la protección.

#### <a name="valid-values"></a>Valores válidos

Entero de `1` a `15`.

### <a name="OSDBitLockerRebootCountOverride"></a>OSDBitLockerRebootCountOverride

*Se aplica al paso [Deshabilitar BitLocker](task-sequence-steps.md#BKMK_DisableBitLocker).*

<!-- 4512937 -->
A partir de la versión 1906, establezca este valor para invalidar el recuento establecido por el paso o la variable [OSDBitLockerRebootCount](#OSDBitLockerRebootCount) . Aunque los otros métodos solo aceptan valores de 1 a 15, si esta variable se establece en 0, BitLocker permanece deshabilitado de forma indefinida. Esta variable es útil cuando la secuencia de tareas establece un valor, pero quiere establecer un valor independiente para cada colección o dispositivo.

#### <a name="valid-values"></a>Valores válidos

Entero de `0` a `15`.

### <a name="OSDBitLockerRecoveryPassword"></a> OSDBitLockerRecoveryPassword

*Se aplica al paso [Habilitar BitLocker](task-sequence-steps.md#BKMK_EnableBitLocker).*

(entrada)

En lugar de generar una contraseña aleatoria de recuperación, el paso **Habilitar BitLocker** usa el valor especificado como la contraseña de recuperación. El valor debe ser una contraseña numérica de recuperación de BitLocker válida.

### <a name="OSDBitLockerStartupKey"></a> OSDBitLockerStartupKey

*Se aplica al paso [Habilitar BitLocker](task-sequence-steps.md#BKMK_EnableBitLocker).*

(entrada)

En lugar de generar una clave de inicio aleatoria para la opción de administración de claves **Clave de inicio solo en USB**, el paso **Habilitar BitLocker** usa el Módulo de plataforma segura (TPM) como clave de inicio. El valor debe ser una clave de inicio válida de BitLocker de 256 bits con codificación Base64.

### <a name="OSDCaptureAccount"></a> OSDCaptureAccount

*Se aplica al paso [Capturar imagen de sistema operativo](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage).*

(entrada)

Especifica un nombre de cuenta de Windows que tiene permisos para almacenar la imagen capturada en un recurso compartido de red ([OSDCaptureDestination](#OSDCaptureDestination)). Especifique también el valor de [OSDCaptureAccountPassword](#OSDCaptureAccountPassword).

Para obtener más información sobre la cuenta de captura de imagen del sistema operativo, consulte [Cuentas](/sccm/core/plan-design/hierarchy/accounts#capture-os-image-account).

### <a name="OSDCaptureAccountPassword"></a> OSDCaptureAccountPassword

*Se aplica al paso [Capturar imagen de sistema operativo](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage).*

(entrada)

Especifica la contraseña de la cuenta de Windows ([OSDCaptureAccount](#OSDCaptureAccount)) que se utiliza para almacenar la imagen capturada en un recurso compartido de red ([OSDCaptureDestination](#OSDCaptureDestination)).

### <a name="OSDCaptureDestination"></a> OSDCaptureDestination

*Se aplica al paso [Capturar imagen de sistema operativo](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage).*

(entrada)

Especifica la ubicación en la que la secuencia de tareas guarda la imagen del sistema operativo capturada. La longitud máxima del nombre de directorio es 255 caracteres. Si el recurso compartido de red requiere autenticación, especifique las variables [OSDCaptureAccount](#OSDCaptureAccount) y [OSDCaptureAccountPassword](#OSDCaptureAccountPassword).

### <a name="OSDComputerName-input"></a> OSDComputerName (input)

*Se aplica al paso [Aplicar configuraciones de Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

Especifica el nombre del equipo de destino.

#### <a name="example"></a>Ejemplo

`%_SMSTSMachineName%` (valor predeterminado)

### <a name="OSDComputerName-output"></a> OSDComputerName (salida)

*Se aplica al paso [Capturar configuración de Windows](task-sequence-steps.md#BKMK_CaptureWindowsSettings).*

Se establece con el nombre NETBIOS del equipo. El valor se establece solo si la variable [OSDMigrateComputerName](#OSDMigrateComputerName) se establece en `true`.

### <a name="OSDConfigFileName"></a> OSDConfigFileName

*Se aplica al paso [Aplicar imagen de sistema operativo](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage).*

(entrada)

Especifica el nombre del archivo de respuesta de implementación de sistema operativo asociado con el paquete de imagen de implementación de sistema operativo.  

### <a name="OSDDataImageIndex"></a> OSDDataImageIndex

*Se aplica al paso [Aplicar imagen de datos](task-sequence-steps.md#BKMK_ApplyDataImage).*

(entrada)

Especifica el valor de índice de la imagen que se aplica al equipo de destino.

### <a name="OSDDiskIndex"></a> OSDDiskIndex

*Se aplica al paso [Formatear y crear particiones en el disco](task-sequence-steps.md#BKMK_FormatandPartitionDisk).*

(entrada)

Especifica el número de disco físico en el que se van a crear particiones.

### <a name="OSDDNSDomain"></a> OSDDNSDomain

*Se aplica al paso [Aplicar configuración de red](task-sequence-steps.md#BKMK_ApplyNetworkSettings).*

(entrada)

Especifica el servidor DNS principal que usa el equipo de destino.

### <a name="OSDDNSSuffixSearchOrder"></a> OSDDNSSuffixSearchOrder

*Se aplica al paso [Aplicar configuración de red](task-sequence-steps.md#BKMK_ApplyNetworkSettings).*

(entrada)

Especifica el orden de búsqueda DNS del equipo de destino.

### <a name="OSDDomainName"></a> OSDDomainName

*Se aplica al paso [Aplicar configuración de red](task-sequence-steps.md#BKMK_ApplyNetworkSettings).*

(entrada)

Especifica el nombre de un dominio de Active Directory al que se une el equipo de destino. El valor especificado debe ser un nombre de dominio válido de Servicios de dominio de Active Directory.

### <a name="OSDDomainOUName"></a> OSDDomainOUName

*Se aplica al paso [Aplicar configuración de red](task-sequence-steps.md#BKMK_ApplyNetworkSettings).*

(entrada)

Especifica el nombre en formato RFC 1779 de la unidad organizativa (UO) a la que se une el equipo de destino. Si se especifica, el valor debe contener la ruta de acceso completa.

#### <a name="example"></a>Ejemplo

`LDAP://OU=MyOu,DC=MyDom,DC=MyCompany,DC=com`

### <a name="OSDDoNotLogCommand"></a> OSDDoNotLogCommand

<!--1358493-->
*A partir de la versión 1806*  
*Se aplica al paso [Instalar paquete](/sccm/osd/understand/task-sequence-steps#BKMK_InstallPackage).*

*A partir de la versión 1902*  
*Se aplica al paso [Ejecutar línea de comandos](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine).*

(entrada)

Para evitar la visualización o el registro de información posiblemente confidencial, establezca esta variable en `TRUE`. Esta variable enmascara el nombre del programa en **smsts.log** durante un paso **Instalar paquete**.

A partir de la versión 1902, al establecer esta variable en `TRUE`, también se oculta la línea de comandos del paso **Ejecutar línea de comandos** del archivo de registro.<!--3654172-->

### <a name="OSDEnableTCPIPFiltering"></a> OSDEnableTCPIPFiltering

*Se aplica al paso [Aplicar configuración de red](task-sequence-steps.md#BKMK_ApplyNetworkSettings).*

(entrada)

Especifica si el filtrado TCP/IP está habilitado.

#### <a name="valid-values"></a>Valores válidos

- `true`  
- `false` (valor predeterminado)  

### <a name="OSDGPTBootDisk"></a> OSDGPTBootDisk

*Se aplica al paso [Formatear y crear particiones en el disco](task-sequence-steps.md#BKMK_FormatandPartitionDisk).*

(entrada)

Especifica si se debe crear una partición EFI en un disco duro GPT. Los equipos basados en EFI utilizan esta partición como disco de inicio.

#### <a name="valid-values"></a>Valores válidos

- `true`  
- `false` (valor predeterminado)

### <a name="OSDImageCreator"></a> OSDImageCreator

*Se aplica al paso [Capturar imagen de sistema operativo](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage).*

(entrada)

Un nombre opcional del usuario que creó la imagen. Este nombre se almacena en el archivo WIM. La longitud máxima del nombre de usuario es 255 caracteres.

### <a name="OSDImageDescription"></a> OSDImageDescription

*Se aplica al paso [Capturar imagen de sistema operativo](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage).*

(entrada)

Una descripción opcional definida por el usuario de la imagen capturada del sistema operativo. Esta descripción se almacena en el archivo WIM. La longitud máxima de la descripción es 255 caracteres.

### <a name="OSDImageIndex"></a> OSDImageIndex

*Se aplica al paso [Aplicar imagen de sistema operativo](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage).*

(entrada)

Especifica el valor de índice de la imagen del archivo WIM que se aplica al equipo de destino.

### <a name="OSDImageVersion"></a> OSDImageVersion

*Se aplica al paso [Capturar imagen de sistema operativo](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage).*

(entrada)

Número de versión opcional definido por el usuario que se asigna a la imagen capturada del sistema operativo. Este número de versión se almacena en el archivo WIM. Este valor puede ser una combinación cualquiera de caracteres alfanuméricos con una longitud máxima de 32.

### <a name="OSDInstallDriversAdditionalOptions"></a> OSDInstallDriversAdditionalOptions

<!--516679/2840016-->
*A partir de la versión 1806*  
*Se aplica al paso [Aplicar paquete de controladores](/sccm/osd/understand/task-sequence-steps#BKMK_ApplyDriverPackage).*

(entrada)

Especifica opciones adicionales para agregar a la línea de comandos de DISM al aplicar un paquete de controladores. La secuencia de tareas no verifica las opciones de línea de comandos.

Para usar esta variable, habilite el parámetro **Install driver package via running DISM with recurse option** (Instalar paquete de controladores mediante la ejecución de DISM con la opción de recursividad) en el paso **Aplicar paquete de controladores**.

Para más información, vea [Opciones de línea de comandos del marco DISM de Windows 10](https://docs.microsoft.com/windows-hardware/manufacture/desktop/deployment-image-servicing-and-management--dism--command-line-options).

### <a name="OSDJoinAccount"></a> OSDJoinAccount

*Se aplica a los pasos siguientes:*  

- [Aplicar configuración de red](task-sequence-steps.md#BKMK_ApplyNetworkSettings)  
- [Unirse a dominio o grupo de trabajo](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup)  

(entrada)

Especifica la cuenta de usuario de dominio que se utiliza para agregar el equipo de destino al dominio. Esta variable es necesaria para unirse a un dominio.

Para obtener más información sobre la cuenta de unión a dominio de la secuencia de tareas, consulte [Cuentas](/sccm/core/plan-design/hierarchy/accounts#task-sequence-domain-join-account).

### <a name="OSDJoinDomainName"></a> OSDJoinDomainName

*Se aplica al paso [Unirse a dominio o grupo de trabajo](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup).*

(entrada)

Especifica el nombre de un dominio de Active Directory al que se une el equipo de destino. El nombre de dominio debe tener entre 1 y 255 caracteres.

### <a name="OSDJoinDomainOUName"></a> OSDJoinDomainOUName

*Se aplica al paso [Unirse a dominio o grupo de trabajo](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup).*

(entrada)

Especifica el nombre en formato RFC 1779 de la unidad organizativa (UO) a la que se une el equipo de destino. Si se especifica, el valor debe contener la ruta de acceso completa. El nombre de la UO debe tener entre 0 y 32 767 caracteres. No se establece este valor si la variable [OSDJoinType](#OSDJoinType) se establece como `1` (unirse al grupo de trabajo).

#### <a name="example"></a>Ejemplo

`LDAP://OU=MyOu,DC=MyDom,DC=MyCompany,DC=com`  

### <a name="OSDJoinPassword"></a> OSDJoinPassword

*Se aplica a los pasos siguientes:*  

- [Aplicar configuración de red](task-sequence-steps.md#BKMK_ApplyNetworkSettings)  
- [Unirse a dominio o grupo de trabajo](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup)  

(entrada)

Especifica la contraseña para [OSDJoinAccount](#OSDJoinAccount) que usa el equipo de destino para unirse al dominio de Active Directory. Si el entorno de secuencia de tareas no incluye esta variable, el programa de instalación de Windows prueba con una contraseña en blanco. Este valor es necesario si la variable [OSDJoinType](#OSDJoinType) se establece como `0` (unirse al dominio).

### <a name="OSDJoinSkipReboot"></a> OSDJoinSkipReboot

*Se aplica al paso [Unirse a dominio o grupo de trabajo](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup).*

(entrada)

Especifica si se omite el reinicio después de que el equipo de destino se una al dominio o al grupo de trabajo.

#### <a name="valid-values"></a>Valores válidos

- `true`  
- `false`  

### <a name="OSDJoinType"></a> OSDJoinType

*Se aplica al paso [Unirse a dominio o grupo de trabajo](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup).*

(entrada)

Especifica si el equipo de destino se une a un dominio de Windows o a un grupo de trabajo.

#### <a name="valid-values"></a>Valores válidos

- `0`: unir el equipo de destino a un dominio de Windows  
- `1`: unir el equipo de destino a un grupo de trabajo  

### <a name="OSDJoinWorkgroupName"></a> OSDJoinWorkgroupName

*Se aplica al paso [Unirse a dominio o grupo de trabajo](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup).*

(entrada)

Especifica el nombre de un grupo de trabajo al que se une el equipo de destino. El nombre del grupo de trabajo debe tener entre 1 y 32 caracteres.

### <a name="OSDKeepActivation"></a> OSDKeepActivation

*Se aplica al paso [Preparar Windows para la captura](task-sequence-steps.md#BKMK_PrepareWindowsforCapture).*

(entrada)

Especifica si sysprep restablece la marca de activación del producto.

#### <a name="valid-values"></a>Valores válidos

- `true`
- `false` (valor predeterminado)

### <a name="OSDLocalAdminPassword"></a> OSDLocalAdminPassword

*Se aplica al paso [Aplicar configuraciones de Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

(entrada)

Especifica la contraseña de la cuenta de administrador local. Si habilita la opción de **Generar la contraseña de administrador local aleatoriamente y deshabilitar la cuenta en todas las plataformas admitidas**, entonces el paso ignora esta variable. El valor especificado debe tener entre 1 y 255 caracteres.

### <a name="OSDLogPowerShellParameters"></a> OSDLogPowerShellParameters

<!--3556028-->
*A partir de la versión 1902*  
*Se aplica a al paso [Ejecutar script PowerShell](/sccm/osd/understand/task-sequence-steps#BKMK_RunPowerShellScript).*

(entrada)

Para evitar el registro de información posiblemente confidencial, el paso **Ejecutar script de PowerShell** no registra parámetros de script en el archivo **smsts.log**. Para incluir los parámetros del script en el registro de secuencia de tareas, establezca esta variable en **TRUE**.

### <a name="OSDMigrateAdapterSettings"></a> OSDMigrateAdapterSettings

*Se aplica al paso [Capturar configuración de red](task-sequence-steps.md#BKMK_CaptureNetworkSettings).*

(entrada)

Especifica si la secuencia de tareas captura la información del adaptador de red. Esta información incluye la configuración de TCP/IP, DNS y WINS.

#### <a name="valid-values"></a>Valores válidos

- `true` (valor predeterminado)
- `false`

### <a name="OSDMigrateAdditionalCaptureOptions"></a> OSDMigrateAdditionalCaptureOptions

*Se aplica al paso [Capturar estado de usuario](task-sequence-steps.md#BKMK_CaptureUserState).*

(entrada)

Especifique opciones adicionales de la línea de comandos de la herramienta de migración de estado de usuario (USMT) que la secuencia de tareas utiliza para capturar el estado de usuario. El paso no expone estas opciones en el editor de secuencia de tareas. Especifique estas opciones como una cadena que la secuencia de tareas anexa a la línea de comandos USMT generada automáticamente para ScanState.

Las opciones de USMT especificadas con esta variable de secuencia de tareas no se validan para comprobar su exactitud antes de ejecutar la secuencia de tareas.

Para obtener más información sobre las opciones disponibles, consulte [ScanState Syntax](https://docs.microsoft.com/windows/deployment/usmt/usmt-scanstate-syntax) (Sintaxis de ScanState).

### <a name="OSDMigrateAdditionalRestoreOptions"></a> OSDMigrateAdditionalRestoreOptions

*Se aplica al paso [Restaurar estado de usuario](task-sequence-steps.md#BKMK_RestoreUserState).*

(entrada)

Especifica opciones adicionales de la línea de comandos de la herramienta de migración de estado de usuario (USMT) que la secuencia de tareas utiliza al restaurar el estado de usuario. Especifique las opciones adicionales como una cadena que la secuencia de tareas anexa a la línea de comandos USMT generada automáticamente para LoadState.

Las opciones de USMT especificadas con esta variable de secuencia de tareas no se validan para comprobar su exactitud antes de ejecutar la secuencia de tareas.

Para obtener más información sobre las opciones disponibles, consulte [LoadState Syntax](https://docs.microsoft.com/windows/deployment/usmt/usmt-loadstate-syntax) (Sintaxis de LoadState).

### <a name="OSDMigrateComputerName"></a> OSDMigrateComputerName

*Se aplica al paso [Capturar configuración de Windows](task-sequence-steps.md#BKMK_CaptureWindowsSettings).*

(entrada)

Especifica si se migra el nombre del equipo.

#### <a name="valid-values"></a>Valores válidos

- `true` (valor predeterminado). La variable [OSDComputerName (salida)](#OSDComputerName-output) se establece en el nombre NETBIOS del equipo.  
- `false`  

### <a name="OSDMigrateConfigFiles"></a> OSDMigrateConfigFiles

*Se aplica al paso [Capturar estado de usuario](task-sequence-steps.md#BKMK_CaptureUserState).*

(entrada)

Especifica los archivos de configuración que se utilizan para controlar la captura de perfiles de usuario. Esta variable se usa solo si el valor de [OSDMigrateMode](#OSDMigrateMode) está establecido en `Advanced`. Este valor de lista delimitada por comas está configurado para realizar una migración de perfiles de usuario personalizada.

#### <a name="example"></a>Ejemplo

`miguser.xml,migsys.xml,migapps.xml`  

### <a name="OSDMigrateContinueOnLockedFiles"></a> OSDMigrateContinueOnLockedFiles

*Se aplica al paso [Capturar estado de usuario](task-sequence-steps.md#BKMK_CaptureUserState).*

(entrada)

Si USMT no puede capturar algunos archivos, esta variable permite a la captura del estado de usuario continuar.

#### <a name="valid-values"></a>Valores válidos

- `true` (valor predeterminado)  
- `false`  

### <a name="OSDMigrateContinueOnRestore"></a> OSDMigrateContinueOnRestore

*Se aplica al paso [Restaurar estado de usuario](task-sequence-steps.md#BKMK_RestoreUserState).*

(entrada)

Continuar con el proceso, incluso si USMT no puede restaurar algunos archivos.

#### <a name="valid-values"></a>Valores válidos

- `true` (valor predeterminado)  
- `false`  

### <a name="OSDMigrateEnableVerboseLogging"></a> OSDMigrateEnableVerboseLogging

*Se aplica a los pasos siguientes:*  

- [Capturar estado de usuario](task-sequence-steps.md#BKMK_CaptureUserState)  
- [Restaurar estado de usuario](task-sequence-steps.md#BKMK_RestoreUserState)  

(entrada)

Habilita el registro detallado para USMT. El paso requiere este valor.

#### <a name="valid-values"></a>Valores válidos

- `true`  
- `false` (valor predeterminado)  

### <a name="OSDMigrateLocalAccounts"></a> OSDMigrateLocalAccounts

*Se aplica al paso [Restaurar estado de usuario](task-sequence-steps.md#BKMK_RestoreUserState).*

(entrada)

Especifica si se restaura la cuenta de equipo local.

#### <a name="valid-values"></a>Valores válidos

- `true`  
- `false` (valor predeterminado)  

### <a name="OSDMigrateLocalAccountPassword"></a> OSDMigrateLocalAccountPassword

*Se aplica al paso [Restaurar estado de usuario](task-sequence-steps.md#BKMK_RestoreUserState).*

(entrada)

Si la variable [OSDMigrateLocalAccounts](#OSDMigrateLocalAccounts) es `true`, esta variable debe contener la contraseña que se asigna a *todas* las cuentas locales migradas. USMT asigna la misma contraseña a todas las cuentas locales migradas. Considere esta contraseña como temporal y cámbiela más adelante por algún otro método.

### <a name="OSDMigrateMode"></a> OSDMigrateMode

*Se aplica al paso [Capturar estado de usuario](task-sequence-steps.md#BKMK_CaptureUserState).*

(entrada)

Le permite personalizar los archivos que captura la USMT.

#### <a name="valid-values"></a>Valores válidos

- `Simple`: la secuencia de tareas solo usa los archivos de configuración de USMT estándar  

- `Advanced`: la variable de secuencia de tareas [OSDMigrateConfigFiles](#OSDMigrateConfigFiles) especifica los archivos de configuración que usa USMT  

### <a name="OSDMigrateNetworkMembership"></a> OSDMigrateNetworkMembership

*Se aplica al paso [Capturar configuración de red](task-sequence-steps.md#BKMK_CaptureNetworkSettings).*

(entrada)

Especifica si la secuencia de tareas migra la información de pertenencia a grupo de trabajo o dominio.

#### <a name="valid-values"></a>Valores válidos

- `true` (valor predeterminado)
- `false`

### <a name="OSDMigrateRegistrationInfo"></a> OSDMigrateRegistrationInfo

*Se aplica al paso [Capturar configuración de Windows](task-sequence-steps.md#BKMK_CaptureWindowsSettings).*

(entrada)

Especifica si el paso migra la información del usuario y la organización.

#### <a name="valid-values"></a>Valores válidos

- `true` (valor predeterminado). La variable [OSDRegisteredOrgName (salida)](#OSDRegisteredOrgName-output) se establece en el nombre de organización registrado del equipo.  
- `false`  

### <a name="OSDMigrateSkipEncryptedFiles"></a> OSDMigrateSkipEncryptedFiles

*Se aplica al paso [Capturar estado de usuario](task-sequence-steps.md#BKMK_CaptureUserState).*

(entrada)

Especifica si se capturan los archivos cifrados.

#### <a name="valid-values"></a>Valores válidos

- `true`  
- `false` (valor predeterminado)  

### <a name="OSDMigrateTimeZone"></a> OSDMigrateTimeZone

*Se aplica al paso [Capturar configuración de Windows](task-sequence-steps.md#BKMK_CaptureWindowsSettings).*

(entrada)

Especifica si se migra la zona horaria del equipo.

#### <a name="valid-values"></a>Valores válidos

- `true` (valor predeterminado). La variable [OSDTimeZone (salida)](#OSDTimeZone-output) se establece en la zona horaria del equipo.  
- `false`  

### <a name="OSDNetworkJoinType"></a> OSDNetworkJoinType

*Se aplica al paso [Aplicar configuración de red](task-sequence-steps.md#BKMK_ApplyNetworkSettings).*

(entrada)

Especifica si el equipo de destino se une a un dominio de Active Directory o a un grupo de trabajo.

#### <a name="value-values"></a>Valores del parámetro

- `0`: unirse a un dominio de Active Directory  
- `1`: unirse a un grupo de trabajo

### <a name="OSDPartitions"></a> OSDPartitions

*Se aplica al paso [Formatear y crear particiones en el disco](task-sequence-steps.md#BKMK_FormatandPartitionDisk).*

(entrada)

Esta variable de secuencia de tareas es una variable de matriz de la configuración de particiones. Cada uno de los elementos de la matriz representa la configuración de una única partición en el disco duro. El acceso a la configuración definida para cada partición se puede realizar mediante la combinación del nombre de la variable de matriz con el número de partición de disco basado en cero y el nombre de la propiedad.

Use los siguientes nombres de variable para definir las propiedades de la *primera* partición que este paso crea en el disco duro:

#### <a name="osdpartitions0type"></a>OSDPartitions0Type

Especifica el tipo de partición. Esta propiedad es obligatoria. Los valores válidos son `Primary`, `Extended`, `Logical` y `Hidden`.

#### <a name="osdpartitions0filesystem"></a>OSDPartitions0FileSystem

Especifica el tipo de sistema de archivos que se utilizará al formatear la partición. Esta propiedad es opcional. Si no especifica un sistema de archivos, el paso no formatea la partición. Los valores válidos son `FAT32` y `NTFS`.

#### <a name="osdpartitions0bootable"></a>OSDPartitions0Bootable

Especifica si la partición es de arranque. Esta propiedad es obligatoria. Si este valor se establece en `TRUE` en discos MBR, el paso marca esta partición como activa.

#### <a name="osdpartitions0quickformat"></a>OSDPartitions0QuickFormat

Especifica el tipo de formato que se utiliza. Esta propiedad es obligatoria. Si este valor se establece en `TRUE`, el paso realiza un formateo rápido. En caso contrario, el paso realiza un formateo completo.

#### <a name="osdpartitions0volumename"></a>OSDPartitions0VolumeName

Especifica el nombre que se asigna al volumen cuando se formatea. Esta propiedad es opcional.

#### <a name="osdpartitions0size"></a>OSDPartitions0Size

Especifica el tamaño de la partición. Esta propiedad es opcional. Si no se especifica esta propiedad, se crea la partición con todo el espacio libre restante. Las unidades las especifica la variable **OSDPartitions0SizeUnits** .

#### <a name="osdpartitions0sizeunits"></a>OSDPartitions0SizeUnits

El paso utiliza estas unidades para interpretar la variable **OSDPartitions0Size**. Esta propiedad es opcional. Los valores válidos son `MB` (valor predeterminado), `GB`, y `Percent`.

#### <a name="osdpartitions0volumelettervariable"></a>OSDPartitions0VolumeLetterVariable

Cuando en este paso se crean las particiones, siempre se utiliza la siguiente letra de unidad disponible en Windows PE. Use esta propiedad opcional para especificar el nombre de otra variable de secuencia de tareas. El paso utiliza esta variable para guardar la nueva letra de unidad para futuras referencias.

Si define varias particiones con este paso de secuencia de tareas, las propiedades de la *segunda* partición se definen con su índice **1** en el nombre de variable. Por ejemplo: **OSDPartitions1Type**, **OSDPartitions1FileSystem**, **OSDPartitions1Bootable**, **OSDPartitions1QuickFormat** y **OSDPartitions1VolumeName**.

### <a name="OSDPartitionStyle"></a> OSDPartitionStyle

*Se aplica al paso [Formatear y crear particiones en el disco](task-sequence-steps.md#BKMK_FormatandPartitionDisk).*

(entrada)

Especifica el estilo de partición que se utilizará al crear particiones en el disco.

#### <a name="valid-values"></a>Valores válidos

- `GPT`: se usa el estilo de la tabla de particiones GUID
- `MBR`: se usa el estilo de particiones del registro de arranque maestro

### <a name="OSDProductKey"></a> OSDProductKey

*Se aplica al paso [Aplicar configuraciones de Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

(entrada)

Especifica la clave de producto de Windows. El valor especificado debe tener entre 1 y 255 caracteres.

### <a name="OSDRandomAdminPassword"></a> OSDRandomAdminPassword

*Se aplica al paso [Aplicar configuraciones de Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

(entrada)

Especifica una contraseña generada de forma aleatoria para la cuenta de administrador local en el nuevo sistema operativo.

#### <a name="valid-values"></a>Valores válidos

- `true` (valor predeterminado): el programa de instalación de Windows deshabilita la cuenta de administrador local en el equipo de destino  

- `false`: el programa de instalación de Windows habilita la cuenta de administrador local en el equipo de destino y establece la contraseña de cuenta en el valor de [OSDLocalAdminPassword](#OSDLocalAdminPassword)  

### <a name="OSDRegisteredOrgName-input"></a> OSDRegisteredOrgName (entrada)

*Se aplica al paso [Aplicar configuraciones de Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

Especifica el nombre de organización registrado de forma predeterminada en el nuevo sistema operativo. El valor especificado debe tener entre 1 y 255 caracteres.

### <a name="OSDRegisteredOrgName-output"></a> OSDRegisteredOrgName (salida)

*Se aplica al paso [Capturar configuración de Windows](task-sequence-steps.md#BKMK_CaptureWindowsSettings).*

Se establece con el nombre de organización registrado del equipo. El valor se establece solo si la variable [OSDMigrateRegistrationInfo](#OSDMigrateRegistrationInfo) se establece en `true`.

### <a name="OSDRegisteredUserName"></a> OSDRegisteredUserName

*Se aplica al paso [Aplicar configuraciones de Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

(entrada)

Especifica el nombre de usuario registrado de forma predeterminada en el nuevo sistema operativo. El valor especificado debe tener entre 1 y 255 caracteres.

### <a name="OSDServerLicenseConnectionLimit"></a> OSDServerLicenseConnectionLimit

*Se aplica al paso [Aplicar configuraciones de Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

(entrada)

Especifica el número máximo de conexiones permitidas. El número especificado debe estar comprendido en el intervalo entre 5 y 9999 conexiones.

### <a name="OSDServerLicenseMode"></a> OSDServerLicenseMode

*Se aplica al paso [Aplicar configuraciones de Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

(entrada)

Especifica el modo de licencia de Windows Server que se utiliza.

#### <a name="valid-values"></a>Valores válidos

- `PerSeat`
- `PerServer`

### <a name="OSDSetupAdditionalUpgradeOptions"></a> OSDSetupAdditionalUpgradeOptions

*Se aplica al paso [Actualizar sistema operativo](task-sequence-steps.md#BKMK_UpgradeOS).*

(entrada)

Especifica las opciones adicionales de la línea de comandos que se agregan al programa de instalación de Windows durante la actualización a Windows 10. La secuencia de tareas no verifica las opciones de línea de comandos.

Para más información, consulte [Opciones de la línea de comandos del programa de instalación de Windows](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options).

### <a name="OSDStateFallbackToNAA"></a> OSDStateFallbackToNAA

*Se aplica al paso [Solicitar almacén de estado](task-sequence-steps.md#BKMK_RequestStateStore).*

(entrada)

Esta variable especifica si la secuencia de tareas debe usar la cuenta de acceso a red (NAA) como reserva cuando la cuenta del equipo no se puede conectar al punto de migración de estado.

Para más información acerca de la cuenta de acceso a la red, consulte [Cuentas](/sccm/core/plan-design/hierarchy/accounts#network-access-account).

#### <a name="valid-values"></a>Valores válidos

- `true`  
- `false` (valor predeterminado)  

### <a name="OSDStateSMPRetryCount"></a> OSDStateSMPRetryCount

*Se aplica al paso [Solicitar almacén de estado](task-sequence-steps.md#BKMK_RequestStateStore).*

(entrada)

Especifica el número de veces que esta etapa de la secuencia de tareas intenta encontrar un punto de migración de estado antes de que la etapa produzca un error. El número especificado debe estar entre 0 y 600.

### <a name="OSDStateSMPRetryTime"></a> OSDStateSMPRetryTime

*Se aplica al paso [Solicitar almacén de estado](task-sequence-steps.md#BKMK_RequestStateStore).*

(entrada)

Especifica el número de segundos que espera entre reintentos la etapa de la secuencia de tareas. El número de segundos puede tener un máximo de 30 caracteres.

### <a name="OSDStateStorePath"></a> OSDStateStorePath

*Se aplica a los pasos siguientes:*  

- [Capturar estado de usuario](task-sequence-steps.md#BKMK_CaptureUserState)  
- [Liberar almacén de estado](task-sequence-steps.md#BKMK_ReleaseStateStore)  
- [Solicitar almacén de estado](task-sequence-steps.md#BKMK_RequestStateStore)  
- [Restaurar estado de usuario](task-sequence-steps.md#BKMK_RestoreUserState)  

(entrada)

El recurso compartido de red o el nombre de ruta de acceso local de la carpeta donde la secuencia de tareas guarda o restaura el estado de usuario. No hay ningún valor predeterminado.

### <a name="OSDTargetSystemDrive"></a> OSDTargetSystemDrive

*Se aplica al paso [Aplicar imagen de sistema operativo](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage).*

(salida)

Especifica la letra de unidad de la partición que contiene los archivos del sistema operativo después de aplicarse la imagen.

### <a name="OSDTargetSystemRoot-input"></a> OSDTargetSystemRoot (input)

*Se aplica al paso [Capturar imagen de sistema operativo](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage).*

Especifica la ruta de acceso al directorio de Windows del sistema operativo instalado en el equipo de referencia. La secuencia de tareas comprueba que se trata de un sistema operativo compatible para la captura por parte de Configuration Manager.

### <a name="OSDTargetSystemRoot-output"></a> OSDTargetSystemRoot (output)

*Se aplica al paso [Preparar Windows para la captura](task-sequence-steps.md#BKMK_PrepareWindowsforCapture).*

Especifica la ruta de acceso al directorio de Windows del sistema operativo instalado en el equipo de referencia. La secuencia de tareas comprueba que se trata de un sistema operativo compatible para la captura por parte de Configuration Manager.

### <a name="OSDTimeZone-input"></a> OSDTimeZone (input)

*Se aplica al paso [Aplicar configuraciones de Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

Especifica la configuración de zona horaria predeterminada que se usa en el nuevo sistema operativo.

### <a name="OSDTimeZone-output"></a> OSDTimeZone (salida)

*Se aplica al paso [Capturar configuración de Windows](task-sequence-steps.md#BKMK_CaptureWindowsSettings).*

Se establece con la zona horaria del equipo. El valor se establece solo si la variable [OSDMigrateTimeZone](#OSDMigrateTimeZone) se establece en `true`.

### <a name="OSDWipeDestinationPartition"></a> OSDWipeDestinationPartition

*Se aplica al paso [Aplicar imagen de datos](task-sequence-steps.md#BKMK_ApplyDataImage).*

(entrada)

Especifica si se deben eliminar los archivos ubicados en la partición de destino.

#### <a name="valid-values"></a>Valores válidos

- `true` (valor predeterminado)
- `false`

### <a name="OSDWorkgroupName"></a> OSDWorkgroupName

*Se aplica al paso [Aplicar configuración de red](task-sequence-steps.md#BKMK_ApplyNetworkSettings).*

(entrada)

Especifica el nombre del grupo de trabajo al que se une el equipo de destino.

Especifique esta variable o la variable de [OSDDomainName](#OSDDomainName). El nombre del grupo de trabajo puede tener un máximo de 32 caracteres.

### <a name="SMSClientInstallProperties"></a> SMSClientInstallProperties

*Se aplica al paso [Instalar Windows y Configuration Manager](task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr).*

(entrada)

Especifica las propiedades de instalación del cliente que usa la secuencia de tareas al instalar el cliente de Configuration Manager.

Para obtener más información, vea [Acerca de los parámetros y propiedades de instalación de cliente](/sccm/core/clients/deploy/about-client-installation-properties).

### <a name="SMSConnectNetworkFolderAccount"></a> SMSConnectNetworkFolderAccount

*Se aplica al paso [Conectar a carpeta de red](task-sequence-steps.md#BKMK_ConnectToNetworkFolder).*

(entrada)

Especifica la cuenta de usuario que se utiliza para conectarse al recurso compartido de red en [SMSConnectNetworkFolderPath](#SMSConnectNetworkFolderPath). Especifique la contraseña de la cuenta con el valor [SMSConnectNetworkFolderPassword](#SMSConnectNetworkFolderPassword).

Para obtener más información sobre la cuenta de conexión de la carpeta de red de la secuencia de tareas, consulte [Cuentas](/sccm/core/plan-design/hierarchy/accounts#task-sequence-network-folder-connection-account).

### <a name="SMSConnectNetworkFolderDriveLetter"></a> SMSConnectNetworkFolderDriveLetter

*Se aplica al paso [Conectar a carpeta de red](task-sequence-steps.md#BKMK_ConnectToNetworkFolder).*

(entrada)

Especifica la letra de unidad de la red a la que se debe conectar. Este valor es opcional. Si no se especifica, la conexión de red no se asigna a una letra de unidad. Si se especifica este valor, debe estar en el rango de D a Z. No use X, puesto que es la letra de unidad que usa Windows PE durante la fase de Windows PE.

#### <a name="examples"></a>Ejemplos

- `D:`  
- `E:`  

### <a name="SMSConnectNetworkFolderPassword"></a> SMSConnectNetworkFolderPassword

*Se aplica al paso [Conectar a carpeta de red](task-sequence-steps.md#BKMK_ConnectToNetworkFolder).*

(entrada)

Especifica la contraseña para [SMSConnectNetworkFolderAccount](#SMSConnectNetworkFolderAccount) que se utiliza para conectarse al recurso compartido de red en [SMSConnectNetworkFolderPath](#SMSConnectNetworkFolderPath).

### <a name="SMSConnectNetworkFolderPath"></a> SMSConnectNetworkFolderPath

*Se aplica al paso [Conectar a carpeta de red](task-sequence-steps.md#BKMK_ConnectToNetworkFolder).*

(entrada)

Especifica la ruta de acceso de red para la conexión. Si necesita asignar esta ruta de acceso a una letra de unidad, use el valor de [SMSConnectNetworkFolderDriveLetter](#SMSConnectNetworkFolderDriveLetter).

#### <a name="example"></a>Ejemplo

`\\server\share`

### <a name="SMSInstallUpdateTarget"></a> SMSInstallUpdateTarget

*Se aplica al paso [Instalar actualizaciones de software](task-sequence-steps.md#BKMK_InstallSoftwareUpdates).*

(entrada)

Especifica si se deben instalar todas las actualizaciones o solo las obligatorias.

#### <a name="valid-values"></a>Valores válidos

- `All`  
- `Mandatory`  

### <a name="SMSRebootMessage"></a> SMSRebootMessage

*Se aplica al paso [Reiniciar equipo](task-sequence-steps.md#BKMK_RestartComputer).*

(entrada)

Especifica el mensaje que se mostrará a los usuarios antes de reiniciar el equipo de destino. Si esta variable no está establecida, se mostrará un mensaje de texto predeterminado. El mensaje especificado no puede superar los 512 caracteres.

#### <a name="example"></a>Ejemplo

`Save your work before the computer restarts.`  

### <a name="SMSRebootTimeout"></a> SMSRebootTimeout

*Se aplica al paso [Reiniciar equipo](task-sequence-steps.md#BKMK_RestartComputer).*

(entrada)

Especifica el número de segundos que se muestra la advertencia al usuario antes de reiniciar el equipo.

#### <a name="examples"></a>Ejemplos

- `0` (valor predeterminado): no mostrar un mensaje de reinicio  
- `60`: mostrar la advertencia durante un minuto  

### <a name="SMSTSAssignmentsDownloadInterval"></a> SMSTSAssignmentsDownloadInterval

Número de segundos que deben transcurrir antes de que el cliente intente descargar la directiva desde el último intento en el que no se devolvió ninguna directiva. De forma predeterminada, el cliente esperará **0** segundos.

Puede establecer esta variable mediante un comando de preinicio desde un medio o PXE.

### <a name="SMSTSAssignmentsDownloadRetry"></a> SMSTSAssignmentsDownloadRetry

Número de veces que un cliente intenta descargar la directiva después de que no se encontraran directivas en el primer intento. De forma predeterminada, el cliente lo reintenta **0** veces.

Puede establecer esta variable mediante un comando de preinicio desde un medio o PXE.

### <a name="SMSTSAssignUsersMode"></a> SMSTSAssignUsersMode

Especifica el modo en que una secuencia de tareas asocia usuarios con el equipo de destino. Establezca la variable en uno de los siguientes valores:  

- **Auto**: cuando la secuencia de tareas implementa el sistema operativo en el equipo de destino, crea una relación entre los usuarios especificados y un equipo de destino.  

- **Pendiente**: la secuencia de tareas crea una relación entre los usuarios especificados y el equipo de destino. Un administrador debe aprobar la relación.  

- **Deshabilitado**: la secuencia de tareas no asocia usuarios al equipo de destino cuando se implementa el sistema operativo.

### <a name="SMSTSDisableStatusRetry"></a> SMSTSDisableStatusRetry

<!--512358-->
En escenarios desconectados, el motor de secuencia de tareas intenta repetidamente enviar mensajes de estado al punto de administración. Este comportamiento en este escenario provoca retrasos en el procesamiento de la secuencia de tareas.

A partir de la versión 1802, establezca esta variable en `true` y el motor de secuencia de tareas no intenta enviar mensajes de estado después de que el primer mensaje no se envíe. Este primer intento incluye varios reintentos.

Cuando se reinicia la secuencia de tareas, el valor de esta variable persiste. Pero la secuencia de tareas intenta enviar un mensaje de estado inicial. Este primer intento incluye varios reintentos. Si se realiza correctamente, la secuencia de tareas sigue enviando mensajes de estado independientemente del valor de esta variable. Si no se puede enviar el mensaje de estado, la secuencia de tareas usa el valor de esta variable.

> [!NOTE]  
> Los [informes de estado de la secuencia de tareas](/sccm/core/servers/manage/list-of-reports#task-sequence---deployment-status) se basan en estos mensajes de estado para mostrar el progreso, el historial y los detalles de cada paso. Si no se envían mensajes de estado, no se ponen en cola. Cuando la conectividad se restaura en el punto de administración, no se envían en un momento posterior. Este comportamiento hace que los informes de estado de la secuencia de tareas sean incompletos y faltan elementos.

### <a name="SMSTSDisableWow64Redirection"></a> SMSTSDisableWow64Redirection

*Se aplica al paso [Ejecutar línea de comandos](task-sequence-steps.md#BKMK_RunCommandLine).*

(entrada)

De forma predeterminada en un sistema operativo de 64 bits, la secuencia de tareas busca y ejecuta el programa en la línea de comandos mediante el redirector del sistema de archivos WOW64. Este comportamiento permite que el comando encuentre las versiones de 32 bits de programas del sistema operativo y los archivos DLL. Si esta variable se establece en `true`, se deshabilita el uso del redirector del sistema de archivos WOW64. El comando busca las versiones nativas de 64 bits de programas del sistema operativo y archivos DLL. Esta variable no tiene ningún efecto cuando se ejecuta en un sistema operativo de 32 bits.

### <a name="SMSTSDownloadAbortCode"></a> SMSTSDownloadAbortCode

Esta variable contiene el valor del código de anulación para el descargador de programas externos. Este programa se especifica en la variable [SMSTSDownloadProgram](#SMSTSDownloadProgram). Si el programa devuelve un código de error igual al valor de la variable SMSTSDownloadAbortCode, se produce un error en la descarga de contenido y no se intenta ningún otro método de descarga.

### <a name="SMSTSDownloadProgram"></a> SMSTSDownloadProgram

Utilice esta variable para especificar un proveedor de contenido alternativo (ACP). Un ACP es un programa descargador que se usa para descargar el contenido. La secuencia de tareas usa el ACP en lugar del descargador de Configuration Manager predeterminado. Como parte del proceso de descarga de contenido, la secuencia de tareas comprueba esta variable. Si se especifica, la secuencia de tareas ejecuta el programa para descargar el contenido.

### <a name="SMSTSDownloadRetryCount"></a> SMSTSDownloadRetryCount

Número de veces que Configuration Manager intenta descargar contenido desde un punto de distribución. De forma predeterminada, el cliente lo reintenta **2** veces.

### <a name="SMSTSDownloadRetryDelay"></a> SMSTSDownloadRetryDelay

Número de segundos que espera Configuration Manager antes de volver a intentar descargar contenido desde un punto de distribución. De forma predeterminada, el cliente esperará **15** segundos antes de volver a intentarlo.

### <a name="SMSTSDriverRequestConnectTimeOut"></a> SMSTSDriverRequestConnectTimeOut

*Se aplica al paso [Aplicar controladores automáticamente](task-sequence-steps.md#BKMK_AutoApplyDrivers).*

Cuando se solicita el catálogo de controladores, esta variable es el número de segundos que la secuencia de tareas espera a que se establezca la conexión con el servidor HTTP. Si la conexión tarda más de lo especificado en la configuración del tiempo de espera, la secuencia de tareas cancela la solicitud. De forma predeterminada, el tiempo de espera se establece en **60** segundos.

### <a name="SMSTSDriverRequestReceiveTimeOut"></a> SMSTSDriverRequestReceiveTimeOut

*Se aplica al paso [Aplicar controladores automáticamente](task-sequence-steps.md#BKMK_AutoApplyDrivers).*

Cuando se solicita el catálogo de controladores, esta variable es el número de segundos que la secuencia de tareas espera una respuesta. Si la conexión tarda más de lo especificado en la configuración del tiempo de espera, la secuencia de tareas cancela la solicitud. De forma predeterminada, el tiempo de espera se establece en **480** segundos.

### <a name="SMSTSDriverRequestResolveTimeOut"></a> SMSTSDriverRequestResolveTimeOut

*Se aplica al paso [Aplicar controladores automáticamente](task-sequence-steps.md#BKMK_AutoApplyDrivers).*

Cuando se solicita el catálogo de controladores, esta variable es el número de segundos que la secuencia de tareas espera por la resolución de nombres HTTP. Si la conexión tarda más de lo especificado en la configuración del tiempo de espera, la secuencia de tareas cancela la solicitud. De forma predeterminada, el tiempo de espera se establece en **60** segundos.

### <a name="SMSTSDriverRequestSendTimeOut"></a> SMSTSDriverRequestSendTimeOut

*Se aplica al paso [Aplicar controladores automáticamente](task-sequence-steps.md#BKMK_AutoApplyDrivers).*

Cuando se envía una solicitud al catálogo de controladores, esta variable es el número de segundos que la secuencia de tareas espera para enviar la solicitud. Si la solicitud tarda más de lo especificado en la configuración del tiempo de espera, la secuencia de tareas cancela la solicitud. De forma predeterminada, el tiempo de espera se establece en **60** segundos.

### <a name="SMSTSErrorDialogTimeout"></a> SMSTSErrorDialogTimeout

Cuando se produce un error en una secuencia de tareas, muestra un cuadro de diálogo con el error. La secuencia de tareas lo descarta automáticamente después del número de segundos especificado por esta variable. De forma predeterminada, este valor es **900** segundos (15 minutos).

### <a name="SMSTSLanguageFolder"></a> SMSTSLanguageFolder

Utilice esta variable para cambiar el idioma de visualización de una imagen de arranque independiente del idioma.

### <a name="SMSTSLocalDataDrive"></a> SMSTSLocalDataDrive

Especifica la ubicación en la que la secuencia de tareas almacena los archivos temporales en el equipo de destino mientras se ejecuta.

Establezca esta variable antes de iniciar la secuencia de tareas (por ejemplo, estableciendo una variable de la recopilación). Una vez que se inicia la secuencia de tareas, Configuration Manager define la variable [_SMSTSMDataPath](#SMSTSMDataPath).

### <a name="SMSTSMP"></a> SMSTSMP

Use esta variable para especificar la dirección URL o IP de un punto de administración de Configuration Manager.

### <a name="SMSTSMPListRequestTimeoutEnabled"></a> SMSTSMPListRequestTimeoutEnabled

*Se aplica a los pasos siguientes:*  

- [Instalar aplicación](task-sequence-steps.md#BKMK_InstallApplication)  
- [Instalar actualizaciones de software](task-sequence-steps.md#BKMK_InstallSoftwareUpdates)  

(entrada)

Use esta variable para permitir solicitudes MPList repetidas para actualizar el cliente si este no está en la intranet. De forma predeterminada, esta variable se establece en `True`.

Si los clientes no están en Internet, establezca esta variable en `False` para evitar retrasos innecesarios.

### <a name="SMSTSMPListRequestTimeout"></a> SMSTSMPListRequestTimeout

*Se aplica a los pasos siguientes:*  

- [Instalar aplicación](task-sequence-steps.md#BKMK_InstallApplication)  
- [Instalar actualizaciones de software](task-sequence-steps.md#BKMK_InstallSoftwareUpdates)  

(entrada)

Si la secuencia de tareas no puede recuperar la lista de puntos de administración de servicios de ubicación, esta variable especifica los milisegundos que espera antes de volver a intentar el paso. De forma predeterminada, la secuencia de tareas espera `60000` milisegundos (60 segundos) antes de reintentar el paso. Lo reintenta hasta tres veces.

### <a name="SMSTSPeerDownload"></a> SMSTSPeerDownload

Use esta variable para permitir que el cliente use el almacenamiento en caché del mismo nivel en Windows PE. El establecimiento de esta variable en `true` habilita esta funcionalidad.

### <a name="SMSTSPeerRequestPort"></a> SMSTSPeerRequestPort

Puerto de red personalizado que la memoria caché de mismo nivel de Windows PE utiliza para la difusión inicial. El puerto predeterminado configurado en el cliente es **8004**.

### <a name="SMSTSPersistContent"></a> SMSTSPersistContent

Utilice esta variable para conservar temporalmente contenido en la memoria caché de la secuencia de tareas. Esta variable es diferente de [SMSTSPreserveContent](#SMSTSPreserveContent), que mantiene contenido en la caché de cliente de Configuration Manager una vez completada la secuencia de tareas. SMSTSPersistContent usa la memoria caché de la secuencia de tareas, SMSTSPreserveContent usa la caché del cliente de Configuration Manager.

### <a name="SMSTSPostAction"></a> SMSTSPostAction

Especifica un comando que se ejecuta una vez completada la secuencia de tareas. Por ejemplo, especifique un script que permite escribir filtros en los dispositivos incrustados después de la secuencia de tareas implemente un sistema operativo en el dispositivo.

### <a name="SMSTSPreferredAdvertID"></a> SMSTSPreferredAdvertID

Fuerza la secuencia de tareas para que ejecute una determinada implementación de destino en el equipo de destino. Establezca esta variable a través de un comando de preinicio desde un medio o PXE. Si esta variable se establece, la secuencia de tareas invalida todas las implementaciones necesarias.

### <a name="SMSTSPreserveContent"></a> SMSTSPreserveContent

Esta variable marca la conservación del contenido de la secuencia de tareas en la memoria caché del cliente de Configuration Manager después de la implementación. Esta variable es diferente de [SMSTSPersistContent](#SMSTSPersistContent), que solo conserva el contenido mientras dure la secuencia de tareas. SMSTSPersistContent usa la memoria caché de la secuencia de tareas, SMSTSPreserveContent usa la caché del cliente de Configuration Manager. Establezca SMSTSPreserveContent en `true` para habilitar esta funcionalidad.

### <a name="SMSTSRebootDelay"></a> SMSTSRebootDelay

Especifica el número de segundos que se debe para esperar antes de reiniciar el equipo. Si esta variable es cero (0), el administrador de la secuencia de tareas no mostrará un cuadro de diálogo de notificación antes del reinicio.

#### <a name="example"></a>Ejemplo

- `0`: no mostrar una notificación  

- `60`: mostrar una notificación durante un minuto  

### <a name="SMSTSRebootDelayNext"></a>SMSTSRebootDelayNext

<!--4447680-->
A partir de la versión 1906, use esta variable con la variable [SMSTSRebootDelay](/sccm/osd/understand/task-sequence-variables#SMSTSRebootDelay) existente. Si desea que los reinicios posteriores se realicen con un tiempo de espera distinto al primero, defina SMSTSRebootDelayNext con un valor diferente en segundos.

#### <a name="example"></a>Ejemplo

Desea proporcionar a los usuarios una notificación de reinicio de sesenta minutos al principio de una secuencia de tareas de actualización en contexto de Windows 10. Después de ese primer tiempo de espera largo, desea que los tiempos de espera adicionales sean solo de 60 segundos. Establezca SMSTSRebootDelay en `3600` y SMSTSRebootDelayNext en `60`.  


### <a name="SMSTSRebootMessage"></a> SMSTSRebootMessage

Especifica el mensaje que se mostrará en el cuadro de diálogo de notificación de reinicio. Si esta variable no se establece, aparecerá un mensaje predeterminado.

#### <a name="example"></a>Ejemplo

`The task sequence is restarting this computer`

### <a name="SMSTSRebootRequested"></a> SMSTSRebootRequested

Indica que se ha solicitado el reinicio una vez completado el paso actual de la secuencia de tareas. Si se requiere un reinicio, basta con establecer esta variable en `true` y el administrador de la secuencia de tareas reiniciará el equipo después de este paso de la secuencia de tareas. Si el paso de secuencia de tareas requiere un reinicio para completar la acción, establezca esta variable. Una vez reiniciado el equipo, la secuencia de tareas seguirá ejecutándose desde el paso siguiente de la secuencia de tareas.

### <a name="SMSTSRetryRequested"></a> SMSTSRetryRequested

Solicita un reintento después de que se haya completado el paso actual de la secuencia de tareas. Si esta variable de secuencia de tareas se establece, establezca también la variable [SMSTSRebootRequested](#SMSTSRebootRequested) en `true`. Una vez reiniciado el equipo, el administrador de la secuencia de tareas vuelve a ejecutar el mismo paso de la secuencia de tareas.

### <a name="SMSTSRunCommandLineUserName"></a> SMSTSRunCommandLineUserName

*Se aplica al paso [Ejecutar línea de comandos](task-sequence-steps.md#BKMK_RunCommandLine).*

(entrada)

Especifica la cuenta mediante la que se ejecuta la línea de comandos. El valor es una cadena con el formato nombredeusuario o dominio\nombredeusuario. Especifique la contraseña de la cuenta con la variable [SMSTSRunCommandLinePassword](#SMSTSRunCommandLinePassword).

Para obtener más información sobre la cuenta de "ejecutar como" de la secuencia de tareas, consulte [Cuentas](/sccm/core/plan-design/hierarchy/accounts#task-sequence-run-as-account).

### <a name="SMSTSRunCommandLinePassword"></a> SMSTSRunCommandLinePassword

*Se aplica al paso [Ejecutar línea de comandos](task-sequence-steps.md#BKMK_RunCommandLine).*

(entrada)

Especifica la contraseña de la cuenta que especifica la variable [SMSTSRunCommandLineUserName](#SMSTSRunCommandLineUserName).

### <a name="SMSTSSoftwareUpdateScanTimeout"></a> SMSTSSoftwareUpdateScanTimeout

*Se aplica al paso [Instalar actualizaciones de software](task-sequence-steps.md#BKMK_InstallSoftwareUpdates).*

(entrada)

Permite controlar el tiempo de espera para la detección de actualizaciones de software durante este paso. Por ejemplo, aumente el valor si espera que haya numerosas actualizaciones durante el análisis. El valor predeterminado es `1800` segundos (30 minutos). El valor de la variable se establece en segundos.

> [!NOTE]  
> A partir de la versión 1802, el valor predeterminado es `3600` segundos (60 minutos).  

### <a name="SMSTSUDAUsers"></a> SMSTSUDAUsers

Especifica los usuarios principales del equipo de destino con el formato siguiente: `<DomainName>\<UserName>`. Separe varios usuarios con una coma (`,`). Para obtener más información, consulte [Associate users with a destination computer](/sccm/osd/get-started/associate-users-with-a-destination-computer) (Asociar usuarios a un equipo de destino).

#### <a name="example"></a>Ejemplo

`contoso\jqpublic, contoso\megb, contoso\janedoh`

### <a name="SMSTSWaitForSecondReboot"></a> SMSTSWaitForSecondReboot

*Se aplica al paso [Instalar actualizaciones de software](task-sequence-steps.md#BKMK_InstallSoftwareUpdates).*

(entrada)

Esta variable de secuencia de tareas opcional controla el comportamiento del cliente cuando la instalación de una actualización de software requiere dos reinicios. Establezca esta variable antes del paso para evitar que una secuencia de tareas presente errores debido a un segundo reinicio desde la instalación de la actualización de software.

Establezca el valor de SMSTSWaitForSecondReboot en segundos para especificar durante cuánto tiempo se pausa la secuencia de tareas en este paso mientras se reinicia el equipo. Deje tiempo suficiente en caso de que haya un segundo reinicio.

Por ejemplo, si establece SMSTSWaitForSecondReboot en `600`, la secuencia de tareas se pausa durante 10 minutos tras un reinicio antes de que se ejecuten los pasos adicionales. Esta variable resulta útil cuando un único paso de secuencia de tareas de instalación de actualizaciones de software instala cientos de actualizaciones de software.

### <a name="TSDebugMode"></a>TSDebugMode

<!--3612274-->
A partir de la versión 1906, establezca esta `TRUE` variable en en un objeto de equipo o colección en el que se implementa la secuencia de tareas. Cualquier dispositivo que tenga este conjunto de variables colocará cualquier secuencia de tareas implementada en el modo de depuración.

Para más información, consulte [Depurar una secuencia de tareas](/sccm/osd/deploy-use/debug-task-sequence).

### <a name="TSDisableProgressUI"></a> TSDisableProgressUI

<!-- 1354291 -->
Use esta variable para controlar cuándo la secuencia de tareas muestra el progreso a los usuarios finales. Para ocultar o mostrar el progreso en momentos diferentes, establezca esta variable varias veces en una secuencia de tareas.  

- `true`: ocultar el progreso de la secuencia de tareas  

- `false`: mostrar el progreso de la secuencia de tareas  

### <a name="TSErrorOnWarning"></a> TSErrorOnWarning

*Se aplica al paso [Instalar aplicación](task-sequence-steps.md#BKMK_InstallApplication).*

(entrada)

Permite especificar si el motor de secuencia de tareas considera una advertencia detectada como un error durante este paso. La secuencia de tareas establece la variable [_TSAppInstallStatus](#TSAppInstallStatus) en `Warning` cuando una o más aplicaciones (o una dependencia necesaria) no se instalaron porque no se cumplió un requisito. Si se establece esta variable en `True` y la secuencia de tareas establece **_TSAppInstallStatus** en `Warning`, el resultado es un error. Un valor de `False` es el comportamiento predeterminado.

### <a name="WorkingDirectory"></a> WorkingDirectory

*Se aplica al paso [Ejecutar línea de comandos](task-sequence-steps.md#BKMK_RunCommandLine).*

(entrada)

Especifica el directorio inicial de una acción de la línea de comandos. El nombre de directorio especificado no puede superar los 255 caracteres.

#### <a name="examples"></a>Ejemplos

- `C:\`  
- `%SystemRoot%`  


## <a name="deprecated-variables"></a>Variables en desuso

Las siguientes variables están en desuso:

- **OSDAllowUnsignedDriver**: no se utiliza al implementar Windows Vista y sistemas operativos posteriores
- **OSDBuildStorageDriverList**: solo se aplica a Windows XP y Windows Server 2003
- **OSDDiskpartBiosCompatibilityMode**: solo se necesita para implementar Windows XP o Windows Server 2003
- **OSDInstallEditionIndex**: no se necesita después de Windows Vista
- **OSDPreserveDriveLetter**: para obtener más información, consulte [OSDPreserveDriveLetter](#osdpreservedriveletter)

### <a name="osdpreservedriveletter"></a>OSDPreserveDriveLetter

> [!Important]
> Esta variable de secuencia de tareas está en desuso.
>
> Durante la implementación del sistema operativo, el programa de instalación de Windows determina, de forma predeterminada, cuál es la mejor letra de unidad (normalmente C:).

*Comportamiento anterior*: al aplicar una imagen, la variable OSDPreverveDriveLetter determina si la secuencia de tareas utiliza la letra de unidad capturada en el archivo de imagen (WIM). Establezca el valor de esta variable en `false` para usar la ubicación que especifique en el valor de **Destino** del paso de la secuencia de tareas **Aplicar el sistema operativo**. Para obtener más información, consulte [Aplicar imagen de sistema operativo](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage).


## <a name="see-also"></a>Consulte también

- [Pasos de la secuencia de tareas](/sccm/osd/understand/task-sequence-steps)
- [Using task sequence variables](/sccm/osd/understand/using-task-sequence-variables) (Uso de variables de secuencia de tareas)
- [Planificación de consideraciones para la automatización de tareas](/sccm/osd/plan-design/planning-considerations-for-automating-tasks)
