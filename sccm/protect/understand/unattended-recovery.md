---
title: "Recuperación desatendida"
titleSuffix: Configuration Manager
description: Use un script para recuperar sus sitios en System Center Configuration Manager.
ms.custom: na
ms.date: 6/5/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 828c31d1-3d70-4412-b1a8-c92e7e504d39
caps.latest.revision: 
author: mestew
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: be561de1fd14245e3cf52148683611a307484d3d
ms.sourcegitcommit: daa080cf220835f157a23e8c8e2bd2781b869bb7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/04/2017
---
# <a name="unattended-site-recovery-for-configuration-manager"></a>Recuperación de sitio desatendida de Configuration Manager   

*Se aplica a: System Center Configuration Manager (Rama actual)* Para realizar una [recuperación desatendida](/sccm/protect/understand/recover-sites#site-recovery-procedures) de un sitio primario o un sitio de administración central de Configuration Manager, puede crear un script de instalación desatendida y usar el programa de instalación con la opción de comando **/script**. El script proporciona el mismo tipo de información que solicita el Asistente para instalación, excepto por el hecho de que no existe configuración predeterminada. Deben especificarse todos los valores para las claves de instalación que se aplican al tipo de recuperación que se utiliza.

 Para utilizar la opción de línea de comandos de instalación de /script, debe crear un archivo de inicialización y especificar su nombre después de la opción de línea de comandos de instalación de /script. Más importante que el nombre del archivo es que este tenga la extensión **.ini**. Cuando haga referencia al archivo de inicialización del programa de instalación desde la línea de comandos, tendrá que proporcionar la ruta de acceso completa al archivo. Por ejemplo, si el archivo de inicialización de instalación es *setup.ini* y se almacena en la carpeta *C:\setup*, la línea de comandos sería:

 **setup /script c:\setup\setup.ini**.

> [!IMPORTANT]  
>  Debe tener derechos de administrador para ejecutar el programa de instalación. Cuando ejecute el programa de instalación con el script de instalación desatendida, inicie el símbolo del sistema en un contexto de administrador mediante **Ejecutar como administrador**.

 El script contiene valores, nombres de clave y nombres de sección. Los nombres de clave de sección necesarios varían en función del tipo de recuperación para el que crea el script. No hay un orden determinado para las secciones ni para las claves de las secciones. Las claves no distinguen mayúsculas de minúsculas. Cuando proporciona valores para las claves, el nombre de la clave debe ir seguido por un signo de igual (=) y el valor de la clave.

 Utilice las siguientes secciones como guía para crear un script para una recuperación de sitio desatendida. Las tablas enumeran las claves del script de instalación disponibles, sus valores correspondientes, si son necesarias o no, el tipo de instalación para el que se usan y una breve descripción de cada clave.

## <a name="recover-a-central-administration-site-unattended"></a>Recuperación de un sitio de administración central en modo desatendido
 Utilice la información siguiente para configurar un archivo de script de instalación desatendida para recuperar un sitio de administración central.

 **Identificación**

-   **Nombre de clave** : Action

    -   **Requerido** : sí
    -   **Valores** : RecoverCCAR
    -   **Detalles** : recupera un sitio de administración central


-   **Nombre de clave:** CDLatest

    -   **Necesario:** sí, solo cuando se utilizan medios de la carpeta CD.Latest.
    -   **Valores:** 1 si el valor es distinto de 1, se considera que no se usa CD.Latest.
    -   **Detalles:** el script debe incluir esta clave y valor al ejecutar el programa de instalación desde medios de una carpeta CD.Latest, con el fin de instalar un sitio de administración central o principal, o bien para recuperar estos sitios. Este valor indica al programa de instalación que se están usando medios de la carpeta CD.Latest.

**RecoveryOptions**   
-   **Nombre de clave** : ServerRecoveryOptions   

    -   **Requerido** : sí
    -   **Valores** : 1, 2 o 4  
         1 = servidor de sitio de recuperación y SQL Server.   
         2 = recuperar sólo servidor de sitio.  
         4 = recuperar sólo SQL Server.
    -   **Detalles** : especifica si el programa de instalación recuperará el servidor de sitio, SQL Server o ambos. Las claves asociadas son necesarias cuando se establece el siguiente valor para la configuración de ServerRecoveryOptions:  
        -   **Valor = 1** : tiene la opción de especificar un valor de la clave **SiteServerBackupLocation** para recuperar el sitio mediante una copia de seguridad de sitio. Si no especifica ningún valor, se reinstala el sitio sin restaurarlo desde un conjunto de copia de seguridad.

             se requiere la clave **BackupLocation** cuando configura un valor de **10** para la clave **DatabaseRecoveryOptions** , que se utiliza para restaurar la base de datos de sitio desde la copia de seguridad.

        -   **Valor = 2** : tiene la opción de especificar un valor de la clave **SiteServerBackupLocation** para recuperar el sitio mediante una copia de seguridad de sitio. Si no especifica ningún valor, se reinstala el sitio sin restaurarlo desde un conjunto de copia de seguridad.

        -   **Value = 4** se requiere la clave **BackupLocation** cuando configura un valor de **10** para la clave **DatabaseRecoveryOptions** , que se utiliza para restaurar la base de datos de sitio desde la copia de seguridad.

-   **Nombre de clave** : DatabaseRecoveryOptions

    -   **Requerido** : quizás
    -   **Valores:** 10, 20, 40, 80  
         10 = restaurar la base de datos de sitio desde la copia de seguridad.  
         20 = utilizar una base de datos de sitio que se recuperó manualmente mediante otro método.   
         40 = crear una base de datos nueva para el sitio. Utilice esta opción si no hay ninguna copia de seguridad de base de datos de sitio disponible. Los datos globales y de sitio se recuperan mediante la replicación desde otros sitios.  
         80 = omitir recuperación de base de datos.
    -   **Detalles** : especifica cómo el programa de instalación recuperará la base de datos de sitio en SQL Server. Esta clave es necesaria cuando **ServerRecoveryOptions** tiene un valor de **1** o **4**.


-   **Nombre de clave** : ReferenceSite  

    -   **Requerido** : quizás
    -   **Valores:** &lt;ReferenceSiteFQDN\>
    -   **Detalles** : especifica el sitio primario de referencia que usa el sitio de administración central para recuperar datos globales si la copia de seguridad de la base de datos es anterior al período de retención de seguimiento de cambios, o si se recupera el sitio sin usar una copia de seguridad.

         Si no especifica ningún sitio de referencia y la copia de seguridad es anterior al período de retención de seguimiento de cambios, todos los sitios primarios se reinicializan con los datos restaurados desde el sitio de administración central.

         Si no especifica ningún sitio de referencia y la copia de seguridad pertenece al período de retención de seguimiento de cambios, solo se replicarán desde los sitios primarios los cambios que tuvieron lugar desde la copia de seguridad. Si existen cambios en conflicto de varios sitios primarios, el sitio de administración central utiliza el primero que recibe.

         Esta clave es necesaria cuando **DatabaseRecoveryOptions** tiene un valor de **40**.

-   **Nombre de clave** : SiteServerBackupLocation

    -   **Requerido** : no
    -   **Valores:** &lt;PathToSiteServerBackupSet\>
    -   **Detalles** : especifica la ruta de acceso al conjunto de copia de seguridad del servidor de sitio. Esta clave es opcional si **ServerRecoveryOptions** tiene un valor de **1** o **2**. Especifique un valor para la clave **SiteServerBackupLocation** para recuperar el sitio mediante una copia de seguridad de sitio. Si no especifica ningún valor, se reinstala el sitio sin restaurarlo desde un conjunto de copia de seguridad.


-   **Nombre de clave** : BackupLocation

    -   **Requerido** : quizás
    -   **Valores:** &lt;PathToSiteDatabaseBackupSet\>
    -   **Detalles** : especifica la ruta de acceso al conjunto de copia de seguridad de base de datos de sitio. La clave **BackupLocation** es necesaria cuando configura un valor de **1** o **4** para la clave **ServerRecoveryOptions** , y configura un valor de **10** para la clave **DatabaseRecoveryOptions** .


**Opciones**

-   **Nombre de clave** : ProductID
    -   **Requerido** : sí
    -   **Valores:**   
         xxxxx-xxxxx-xxxxx-xxxxx-xxxxx  
          Eval
    -   **Detalles:** especifica la clave de producto de instalación de Configuration Manager, incluidos los guiones. Si escribe **Eval**, puede instalar la versión de evaluación de Configuration Manager.  


-   **Nombre de clave** : SiteCode

    -   **Requerido** : sí
    -   **Valores:** &lt;Código de sitio\>
    -   **Detalles** : tres caracteres alfanuméricos que identifican de forma única el sitio en la jerarquía. Debe especificar el código del sitio que utilizó el sitio antes de que se produjera el error.


-   **Nombre de clave** : SiteName

    -   **Requerido** : sí
    -   **Valores** : SiteName
    -   **Detalles** : descripción de este sitio.


-   **Nombre de clave** : SMSInstallDir

    -   **Requerido** : sí
    -   **Valores:** &lt;*ConfigMgrInstallationPath*>
    -   **Detalles:** especifica la carpeta de instalación de los archivos de programa de Configuration Manager.
        > [!NOTE]   
        >  Puede especificar la ruta de acceso original o una nueva para la instalación de Configuration Manager.

-   **Nombre de clave** : SDKServer

    -   **Requerido** : sí
    -   **Valores:** &lt;*FQDN del proveedor de SMS*>
    -   **Detalles** : especifica el FQDN del servidor que hospedará el proveedor de SMS. Debe especificar el servidor que hospedaba el proveedor de SMS antes de producirse el error.

         Puede configurar proveedores de SMS adicionales para el sitio después de la instalación inicial.

-   **Nombre de clave** : PrerequisiteComp

    -   **Requerido** : sí
    -   **Valores** : 0 o 1  
         0 = descargar   
         1 = ya se ha descargado
    -   **Detalles** : especifica si se han descargado los archivos de requisitos previos de instalación. Por ejemplo, si utiliza un valor de 0, el programa de instalación descargará los archivos.  


-   **Nombre de clave** : PrerequisitePath

    -   **Requerido** : sí
    -   **Valores:** &lt;*PathToSetupPrerequisiteFiles*>
    -   **Detalles** : especifica la ruta de acceso a los archivos de requisitos previos de instalación. Dependiendo del valor **PrerequisiteComp** , el programa de instalación utiliza esta ruta para almacenar los archivos descargados o localizar los archivos descargados previamente.

-   **Nombre de clave** : AdminConsole

    -   **Requerido** : quizás
    -   **Valores:** 0 o 1 0 = no instalar   
         1 = instalar
    -   **Detalles:** especifica si se va a instalar la consola de Configuration Manager. Esta clave es necesaria, salvo cuando **ServerRecoveryOptions** tiene un valor de **4**.


-   **Nombre de clave** : JoinCEIP

    -   **Requerido** : sí
    -   **Valores** : 0 o 1  
         0 = no unir  
         1 = unir
    -   **Detalles** : especifica si se unirá al Programa para la mejora de la experiencia del usuario.

**SQLConfigOptions**

-   **Nombre de clave** : SQLServerName

    -   **Requerido** : sí
    -   **Valores:** *&lt;SQLServerName\>*
    -   **Detalles**: nombre del servidor, o el nombre de instancia en clúster, que ejecuta SQL Server y donde se hospedará la base de datos del sitio. Debe especificar el mismo servidor que hospedaba la base de datos del sitio antes de producirse el error.


-   **Nombre de clave** : DatabaseName

    -   **Requerido** : sí
    -   **Valores:** *&lt;SiteDatabaseName\>* o *&lt;InstanceName\>*\\*&lt;SiteDatabaseName\>*
    -   **Detalles**: especifica el nombre de la base de datos de SQL Server que se crea o se usa para instalar la base de datos del sitio de administración central. Debe especificar el mismo nombre de base de datos que se utilizó antes de producirse el error.

        > [!IMPORTANT]  
        >  Debe especificar el nombre de instancia y el nombre de la base de datos del sitio si no utiliza la instancia predeterminada.

-   **Nombre de clave** : SQLSSBPort

    -   **Requerido** : no
    -   **Valores:** &lt;*SSBPortNumber*>
    -   **Detalles** : especifique el puerto de SQL Server Service Broker (SSB) usado por SQL Server. Normalmente, SSB está configurado para utilizar el puerto TCP 4022, pero se admiten otros puertos. Debe especificar el mismo puerto SSB que se utilizó antes de producirse el error.

## <a name="recover-a-primary-site-unattended"></a>Recuperación de un sitio primario desatendido
 Utilice la información siguiente para configurar un archivo de script de instalación desatendida para recuperar un sitio de administración central.

 **Identificación**

-   **Nombre de clave** : Action

    -   **Requerido** : sí
    -   **Valores** : RecoverPrimarySite
    -   **Detalles** : recupera un sitio primario.


-   **Nombre de clave:** CDLatest

    -   **Necesario:** sí, solo cuando se utilizan medios de la carpeta CD.Latest.
    -   **Valores:** 1 si el valor es distinto de 1, se considera que no se usa CD.Latest.
    -   **Detalles:** el script debe incluir esta clave y valor al ejecutar el programa de instalación desde medios de una carpeta CD.Latest, con el fin de instalar un sitio de administración central o principal, o bien para recuperar estos sitios. Este valor indica al programa de instalación que se están usando medios de la carpeta CD.Latest.

**RecoveryOptions**

-   **Nombre de clave** : ServerRecoveryOptions

    -   **Requerido** : sí
    -   **Valores** : 1, 2 o 4    
         1 = servidor de sitio de recuperación y SQL Server.   
         2 = recuperar sólo servidor de sitio.  
         4 = recuperar sólo SQL Server.
    -   **Detalles** : especifica si el programa de instalación recuperará el servidor de sitio, SQL Server o ambos. Las claves asociadas son necesarias cuando se establece el siguiente valor para la configuración de ServerRecoveryOptions:

        -   **Valor = 1** : tiene la opción de especificar un valor de la clave **SiteServerBackupLocation** para recuperar el sitio mediante una copia de seguridad de sitio. Si no especifica ningún valor, se reinstala el sitio sin restaurarlo desde un conjunto de copia de seguridad.

             se requiere la clave **BackupLocation** cuando configura un valor de **10** para la clave **DatabaseRecoveryOptions** , que se utiliza para restaurar la base de datos de sitio desde la copia de seguridad.

        -   **Valor = 2** : tiene la opción de especificar un valor de la clave **SiteServerBackupLocation** para recuperar el sitio mediante una copia de seguridad de sitio. Si no especifica ningún valor, se reinstala el sitio sin restaurarlo desde un conjunto de copia de seguridad.

        -   **Value = 4** se requiere la clave **BackupLocation** cuando configura un valor de **10** para la clave **DatabaseRecoveryOptions** , que se utiliza para restaurar la base de datos de sitio desde la copia de seguridad.

-   **Nombre de clave** : DatabaseRecoveryOptions

    -   **Requerido** : quizás
    -   **Valores:** 10, 20, 40, 80  
         10 = restaurar la base de datos de sitio desde la copia de seguridad.  
         20 = utilizar una base de datos de sitio que se recuperó manualmente mediante otro método.     
         40 = crear una base de datos nueva para el sitio. Utilice esta opción si no hay ninguna copia de seguridad de base de datos de sitio disponible. Los datos globales y de sitio se recuperan mediante la replicación desde otros sitios.  
         80 = omitir recuperación de base de datos.
    -   **Detalles** : especifica cómo el programa de instalación recuperará la base de datos de sitio en SQL Server. Esta clave es necesaria cuando **ServerRecoveryOptions** tiene un valor de **1** o **4**.


-   **Nombre de clave** : SiteServerBackupLocation

    -   **Requerido** : no
    -   **Valores:** &lt;PathToSiteServerBackupSet\>
    -   **Detalles** : especifica la ruta de acceso al conjunto de copia de seguridad del servidor de sitio. Esta clave es opcional si **ServerRecoveryOptions** tiene un valor de **1** o **2**. Especifique un valor para la clave **SiteServerBackupLocation** para recuperar el sitio mediante una copia de seguridad de sitio. Si no especifica ningún valor, se reinstala el sitio sin restaurarlo desde un conjunto de copia de seguridad.     


-   **Nombre de clave** : BackupLocation

    -   **Requerido** : quizás
    -   **Valores:** &lt;PathToSiteDatabaseBackupSet\>
    -   **Detalles** : especifica la ruta de acceso al conjunto de copia de seguridad de base de datos de sitio. La clave **BackupLocation** es necesaria cuando configura un valor de **1** o **4** para la clave **ServerRecoveryOptions** , y configura un valor de **10** para la clave **DatabaseRecoveryOptions** .

**Opciones**

-   **Nombre de clave** : ProductID

    -   **Requerido** : sí
    -   **Valores:**     
         xxxxx-xxxxx-xxxxx-xxxxx-xxxxx  
         Eval     
    -   **Detalles:** especifica la clave de producto de instalación de Configuration Manager, incluidos los guiones. Si escribe **Eval**, puede instalar la versión de evaluación de Configuration Manager.  


-   **Nombre de clave** : SiteCode

    -   **Requerido** : sí
    -   **Valores:** &lt;Código de sitio\>
    -   **Detalles** : tres caracteres alfanuméricos que identifican de forma única el sitio en la jerarquía. Debe especificar el código del sitio que utilizó el sitio antes de que se produjera el error.


-   **Nombre de clave** : SiteName

    -   **Requerido** : sí
    -   **Valores** : SiteName
    -   **Detalles** : descripción de este sitio.


-   **Nombre de clave** : SMSInstallDir

    -   **Requerido** : sí
    -   **Valores:** &lt;*ConfigMgrInstallationPath*>
    -   **Detalles:** especifica la carpeta de instalación de los archivos de programa de Configuration Manager.

        > [!NOTE]   
        >  Puede especificar la ruta de acceso original o una nueva para la instalación de Configuration Manager.

-   **Nombre de clave** : SDKServer

    -   **Requerido** : sí
    -   **Valores:** &lt;*FQDN del proveedor de SMS*>
    -   **Detalles** : especifica el FQDN del servidor que hospedará el proveedor de SMS. Debe especificar el servidor que hospedaba el proveedor de SMS antes de producirse el error.

         Puede configurar proveedores de SMS adicionales para el sitio después de la instalación inicial.

-   **Nombre de clave** : PrerequisiteComp

    -   **Requerido** : sí
    -   **Valores** : 0 o 1    
         0 = descargar   
         1 = ya se ha descargado   
    -   **Detalles** : especifica si se han descargado los archivos de requisitos previos de instalación. Por ejemplo, si utiliza un valor de 0, el programa de instalación descargará los archivos.


-   **Nombre de clave** : PrerequisitePath

    -   **Requerido** : sí
    -   **Valores:** &lt;*PathToSetupPrerequisiteFiles*>
    -   **Detalles** : especifica la ruta de acceso a los archivos de requisitos previos de instalación. Dependiendo del valor **PrerequisiteComp** , el programa de instalación utiliza esta ruta para almacenar los archivos descargados o localizar los archivos descargados previamente.


-   **Nombre de clave** : AdminConsole

    -   **Requerido** : quizás
    -   **Valores** : 0 o 1  
         0 = no instalar   
         1 = instalar  
    -   **Detalles:** especifica si se va a instalar la consola de Configuration Manager. Esta clave es necesaria, salvo cuando **ServerRecoveryOptions** tiene un valor de **4**.

-   **Nombre de clave** : JoinCEIP

    -   **Requerido** : sí
    -   **Valores** : 0 o 1    
         0 = no unir  
         1 = unir
    -   **Detalles** : especifica si se unirá al Programa para la mejora de la experiencia del usuario.


**SQLConfigOptions**

-   **Nombre de clave** : SQLServerName

    -   **Requerido** : sí
    -   **Valores:** *&lt;SQLServerName\>*
    -   **Detalles**: nombre del servidor, o el nombre de instancia en clúster, que ejecuta SQL Server y donde se hospedará la base de datos del sitio. Debe especificar el mismo servidor que hospedaba la base de datos del sitio antes de producirse el error.


-   **Nombre de clave** : DatabaseName

    -   **Requerido** : sí
    -   **Valores:** *&lt;SiteDatabaseName\>* o *&lt;InstanceName\>*\\*&lt;SiteDatabaseName\>*
    -   **Detalles**: especifica el nombre de la base de datos de SQL Server que se crea o se usa para instalar la base de datos del sitio de administración central. Debe especificar el mismo nombre de base de datos que se utilizó antes de producirse el error.

        > [!IMPORTANT]    
        >  Debe especificar el nombre de instancia y el nombre de la base de datos del sitio si no utiliza la instancia predeterminada.

-   **Nombre de clave** : SQLSSBPort

    -   **Requerido** : no
    -   **Valores:** &lt;*SSBPortNumber*>
    -   **Detalles** : especifique el puerto de SQL Server Service Broker (SSB) usado por SQL Server. Normalmente, SSB está configurado para utilizar el puerto TCP 4022, pero se admiten otros puertos. Debe especificar el mismo puerto SSB que se utilizó antes de producirse el error.

**Jerarquía ExpansionOption**

-   **Nombre de clave** : CCARSiteServer

    -   **Requerido** : quizás
    -   **Valores:** &lt;*SiteCodeForCentralAdministrationSite*>
    -   **Detalles:** especifica el sitio de administración central al que se asociará un sitio primario al unirse a la jerarquía de Configuration Manager. Esta configuración es necesaria si el sitio primario estaba asociado con un sitio de administración central antes de producirse el error. Debe especificar el código del sitio que utilizó el sitio de administración central antes de que se produjera el error.

-   **Nombre de clave** : CASRetryInterval

    -   **Requerido** : no
    -   **Valores:** &lt;*Interval*>
    -   **Detalles** : especifica el intervalo de reintento (en minutos) para tratar de establecer una conexión con el sitio de administración central después de que la conexión genera un error. Por ejemplo, si se produce un error en la conexión al sitio de administración central, el sitio primario espera el número de minutos especificado en CASRetryInterval y, a continuación, vuelve a intentar establecer la conexión.


-   **Nombre de clave** : WaitForCASTimeout

    -   **Requerido** : no
    -   **Valores:** &lt;*Timeout*>
    -   **Detalles** : especifica el valor de tiempo de espera máximo (en minutos) de un sitio primario para conectarse al sitio de administración central. Por ejemplo, si se produce un error de conexión del sitio primario con el sitio de administración central, el sitio primario vuelve a tratar de establecer la conexión conforme al valor especificado para CASRetryInterval hasta que se alcanza el valor de tiempo de WaitForCASTimeout. Puede especificar un valor entre 0 y 100.
