---
title: Almacenamiento de datos
titleSuffix: Configuration Manager
description: Punto de servicio de almacenamiento de datos y base de datos para System Center Configuration Manager
ms.date: 04/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: aaf43e69-68b4-469a-ad58-9b66deb29057
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6d6e1850c07207205cad696918f7cd4eb97d3ec8
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
#  <a name="the-data-warehouse-service-point-for-system-center-configuration-manager"></a>El punto de servicio de almacenamiento de datos para System Center Configuration Manager
*Se aplica a: System Center Configuration Manager (Rama actual)*

<!--1277922-->
Use el punto de servicio de almacenamiento de datos para almacenar y generar informes de datos históricos a largo plazo para su implementación de Configuration Manager.

> [!TIP]
> Esta característica se introdujo por primera vez en la versión 1702 como una [característica de versión preliminar](/sccm/core/servers/manage/pre-release-features). A partir de la versión 1706, ya no es una característica de versión preliminar.  


> [!Note]  
> Configuration Manager no habilita esta característica opcional de forma predeterminada. Deberá habilitarla para poder usarla. Para más información, vea [Habilitar características opcionales de las actualizaciones](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  


El almacenamiento de datos admite hasta 2 TB de datos, con marcas de tiempo para el seguimiento de cambios. El almacenamiento de datos se consigue mediante sincronizaciones automatizadas desde la base de datos del sitio de Configuration Manager a la base de datos de almacenamiento de datos. Puede acceder a esta información desde su punto de servicio de informes. Los datos que se sincronizan con la base de datos de almacenamiento de datos se conservan durante tres años. Periódicamente, una tarea integrada quita los datos anteriores a este período.

Los datos que se sincronizan incluyen lo siguiente de los grupos de datos globales y datos de sitio:
- Mantenimiento de infraestructura
- Seguridad
- Cumplimiento
- Malware   
- Implementaciones de software
- Detalles de inventario (en cambio, el historial de inventario no se sincroniza)

Cuando se instala el rol de sistema de sitio, instala y configura la base de datos del almacén de datos. También instala varios informes de forma que pueda buscar fácilmente estos datos y crear informes sobre ellos.



## <a name="prerequisites-for-the-data-warehouse-service-point"></a>Requisitos previos del punto de servicio de almacenamiento de datos
- El rol de sistema de sitio de almacenamiento de datos solo es compatible con el sitio de nivel superior de la jerarquía (un sitio de administración central o un sitio primario independiente).
- El equipo en el que instale el rol de sistema de sitio necesita .NET Framework 4.5.2 o versiones posteriores.
- Conceda a la **cuenta de punto de Reporting Services** el permiso **db_datareader** en la base de datos del almacenamiento de datos. 
- La cuenta de equipo correspondiente al equipo en el que se instala el rol de sistema de sitio se utiliza para sincronizar datos con la base de datos del almacén de datos. La cuenta requiere los permisos siguientes:  
  - **Administrator** en el equipo que hospeda la base de datos de almacenamiento de datos.
  - **DB_Creator** en la base de datos del almacenamiento de datos.
  - Bien **DB_owner** o **DB_reader** con permisos **execute** para la base de datos de sitio de los sitios de nivel superior.
- La base de datos de almacenamiento de datos requiere el uso de SQL Server 2012 o una versión posterior. La edición puede ser Standard, Enterprise o Datacenter.
- Las siguientes configuraciones de SQL Server se pueden utilizar para hospedar la base de datos de almacenamiento:  
  - Una instancia predeterminada
  - Una instancia con nombre
  - Grupo de disponibilidad de SQL Server Always On
  - Clúster de conmutación por error de SQL Server
- Si usa [vistas distribuidas](/sccm/core/servers/manage/data-transfers-between-sites#bkmk_distviews), debe instalar el rol de sistema de sitio del punto de servicio de almacenamiento de datos en el mismo servidor que hospeda la base de datos del sitio de los sitios de administración central.

Para obtener información sobre las licencias de SQL Server para la base de datos de almacenamiento de datos, consulte las [preguntas más frecuentes sobre productos y licencias](/sccm/core/understand/product-and-licensing-faq). <!-- sms500967 -->


> [!IMPORTANT]  
> No se admite el almacenamiento de datos cuando el equipo que ejecuta el punto de servicio de almacenamiento de datos o que hospeda la base de datos de almacenamiento de datos ejecuta uno de los siguientes idiomas:
> - JPN (japonés)
> - KOR (coreano)
> - CHS (chino simplificado)
> - CHT (chino tradicional); este problema se resolverá en una versión futura.


## <a name="install-the-data-warehouse"></a>Instalación del almacenamiento de datos
Cada jerarquía admite una única instancia de este rol y puede encontrarse en cualquier sistema de sitio de ese sitio de nivel superior. El servidor SQL Server que hospeda la base de datos para el almacenamiento puede ser local para el rol de sistema de sitio o remoto. El almacenamiento de datos trabaja con el punto de servicios de informes instalado en el mismo sitio. No es necesario que instale los dos roles de sistema de sitio en el mismo servidor.   

Para instalar el rol, use el **Asistente para agregar roles de sistema de sitio** o el **Asistente para crear servidor de sistema de sitio**. Para más información, consulte [Instalación de roles de sistema de sitio para System Center Configuration Manager](/sccm/core/servers/deploy/configure/install-site-system-roles).  

Cuando instala el rol, Configuration Manager crea la base de datos de almacenamiento de datos en la instancia de SQL Server que especifique. Si especifica el nombre de una base de datos existente (como haría si [moviera la base de datos de almacenamiento de datos a un servidor de SQL Server nuevo](#move-the-data-warehouse-database)), Configuration Manager no crea una base de datos nueva sino que usa la que especifique.

### <a name="configurations-used-during-installation"></a>Configuraciones que se han usado durante la instalación
Página **Selección de rol del sistema**:  

Página **General**:
-   **Configuración de conexión de base de datos de almacenamiento de datos de Configuration Manager**:
     - **Nombre de dominio completo de SQL Server**: especifique el nombre de dominio completo (FQDN) del servidor que hospeda la base de datos del punto de servicio de almacenamiento de datos.
     - **Nombre de la instancia de SQL Server, si se aplica**: si no utiliza una instancia predeterminada de SQL Server, debe especificar una.
     - **Nombre de la base de datos**: especifique un nombre para la base de datos de almacenamiento de datos. El nombre de la base de datos no puede tener más de 10 caracteres (en una versión futura, aumentaremos esta longitud).
     Configuration Manager creará la base de datos de almacenamiento de datos con este nombre. Si especifica un nombre de base de datos que ya existe en la instancia de SQL Server, Configuration Manager usará esa base de datos.
     - **Puerto de SQL Server usado para la conexión**: especifique el número de puerto TCP/IP que utiliza el servidor SQL Server que hospeda la base de datos del almacenamiento de datos. Este puerto lo usa el servicio de sincronización del almacenamiento de datos para conectarse a la base de datos de dicho almacenamiento.  
     - **Cuenta de punto de servicio de almacenamiento de datos**: a partir de la versión 1802, especifique la cuenta que SQL Server Reporting Services usa al conectarse a la base de datos de almacenamiento de datos. 

Página **Programación de sincronización**:   
- **Programación de sincronización**:
    - **Hora de inicio**: especifique la hora a la que desea que se inicie la sincronización del almacenamiento de datos.
    - **Patrón de periodicidad**:
         - **Diariamente**: permite especificar que la sincronización se ejecute cada día.
         - **Semanalmente**: permite especificar un solo día cada semana, con una periodicidad semanal para la sincronización.


## <a name="reporting"></a>Generación de informes
Después de instalar un punto de servicio de almacenamiento de datos, varios informes pasan a estar disponibles en el punto de servicios de informes que está instalado en el mismo sitio. Si instala el punto de servicio de almacenamiento de datos antes de instalar un punto de servicios de informes, los informes se agregan automáticamente cuando se instale posteriormente el punto de servicios de informes.

>[!WARNING]
>En la versión 1802 de Configuration Manager, se agregó compatibilidad con credenciales alternativas para el punto de almacenamiento de datos. <!--507334-->Si ha actualizado desde una versión anterior de Configuration Manager, debe especificar las credenciales que SQL Server Reporting Services usará para conectarse a la base de datos de almacenamiento de datos. Los informes de almacenamiento de datos no se abrirán hasta que se especifican las credenciales. Para especificar una cuenta, vaya a **Administración** >**Configuración** >**Servidores y roles de sistema de sitio**. Haga clic en el servidor con el punto de servicio de almacenamiento de datos y, después, haga clic con el botón derecho en el rol de punto de servicio de almacenamiento de datos. Seleccione **Propiedades** y, después, especifique la **cuenta de punto de servicio de almacenamiento de datos**.

El rol de sistema de sitio de almacenamiento de datos incluye los siguientes informes, que tienen una categoría de **almacenamiento de datos**:
 - **Implementación de aplicaciones - Histórico**: vea los detalles de la implementación de aplicaciones para una máquina y una aplicación determinada.
 - **Endpoint Protection y compatibilidad con actualizaciones de software - Histórico**: Vea los equipos a los que les faltan actualizaciones de software.  
 - **Inventario de hardware general - Histórico**: vea todo el inventario de hardware de una máquina concreta.
 - **Inventario de software general - Histórico**: ver todo el inventario de software de una máquina concreta.
 - **Información general sobre el mantenimiento de infraestructura - Histórico**: muestra información general del mantenimiento de su infraestructura de Configuration Manager.
 - **Lista de malware detectado - Histórico**: vea el malware que se ha detectado en la organización.
 - **Resumen de distribución de software - Histórico**: un resumen de distribución de software para una máquina y anuncio específico.


## <a name="expand-an-existing-stand-alone-primary-into-a-hierarchy"></a>Expansión de un sitio primario independiente existente en una jerarquía
Antes de instalar un sitio de administración central para expandir un sitio primario independiente existente, primero debe desinstalar el rol de punto de servicio de almacenamiento de datos. Después de instalar el sitio de administración central, puede instalar el rol de sistema de sitio en el sitio de administración central.  

A diferencia de un movimiento de la base de datos del almacenamiento de datos, este cambio produce una pérdida de los datos históricos que se han sincronizado previamente en el sitio primario. No se admite la copia de seguridad de la base de datos desde el sitio principal y su restauración en el sitio de administración central.




## <a name="move-the-data-warehouse-database"></a>Mover la base de datos de almacenamiento de datos
Use los siguientes pasos para mover la base de datos de almacenamiento de datos a un servidor de SQL Server nuevo:

1.  Use SQL Server Management Studio para realizar una copia de seguridad de la base de datos de almacenamiento de datos. A continuación, restaure esa base de datos a una instancia de SQL Server del nuevo equipo que hospeda el almacenamiento de datos.   
> [!NOTE]     
> Después de restaurar la base de datos en el nuevo servidor, asegúrese de que los permisos de acceso de la base de datos son los mismos en la nueva base de datos de almacenamiento de datos que en la base de datos de almacenamiento de datos original.  

2.  Use la consola de Configuration Manager para quitar el rol de sistema de sitio del punto de servicio de almacenamiento de datos del servidor actual.
3.  Vuelva a instalar el punto de servicio de almacenamiento de datos. Especifique el nombre del nuevo servidor de SQL Server y de la instancia que hospeda la base de datos del almacenamiento de datos restaurada.
4.  Después de que se instale el rol de sistema de sitio, se completa el movimiento.

## <a name="troubleshooting-data-warehouse-issues"></a>Solución de problemas del almacenamiento de datos
**Archivos de registro**  
Use los siguientes registros para investigar problemas con la instalación del punto de servicio de almacenamiento de datos o con la sincronización de datos:
 - *DWSSMSI.log* y *DWSSSetup.log*: use estos registros para investigar errores al instalar el punto de servicio de almacenamiento de datos.
 - *Microsoft.ConfigMgrDataWarehouse.log*: use este registro para investigar la sincronización de datos entre la base de datos del sitio y la base de datos de almacenamiento de datos.

**Error de configuración**  
 La instalación del punto de servicio de almacenamiento de datos no se puede realizar en un servidor de sistema de sitio remoto cuando el almacenamiento de datos es el primer rol de sistema de sitio instalado en ese equipo.  
  - **Solución**: asegúrese de que el equipo en el que va a instalar el punto de servicio de almacenamiento de datos ya hospeda al menos otro rol de sistema de sitio.  


**Problemas de sincronización conocidos**:   
La sincronización genera el siguiente mensaje de error en *Microsoft.ConfigMgrDataWarehouse.log*: **"Error al rellenar los objetos de esquema"**.  
 - **Solución**: asegúrese de que la cuenta de equipo del equipo que hospeda el rol de sistema de sitio es **db_owner** en la base de datos de almacenamiento de datos.

Los informes de almacenamiento de datos no se pueden abrir cuando la base de datos del almacenamiento de datos y el punto de servicio de informes se encuentran en diferentes sistemas de sitio.  

 - **Solución**: conceda a la **cuenta de punto de servicios de informes** el permiso **db_datareader** en la base de datos de almacenamiento de datos.

Al abrir un informe de almacenamiento de datos, se devuelve el siguiente el error:

*Error al procesar el informe. (rsProcessingAborted) No se puede crear una conexión al origen de datos 'AutoGen__39B693BB_524B_47DF_9FDB_9000C3118E82_'. (rsErrorOpeningConnection) Se ha establecido la conexión con el servidor correctamente, pero se ha producido un error durante el inicio de sesión previo del protocolo de enlace. (Proveedor: Proveedor de SSL, error: 0 - La cadena de certificación fue emitida por una entidad que no es de confianza.)*.

- **Solución**: Siga los pasos siguientes para configurar certificados:

  1. En el equipo que hospeda la base de datos del almacenamiento de datos:

    1. Abra IIS, haga clic en **Certificados de servidor**, haga clic con el botón derecho en **Crear certificado autofirmado** y luego especifique el "nombre descriptivo" del nombre del certificado como **Certificado de identificación de SQL Server de almacenamiento de datos**. Seleccione el almacén de certificados como **Personal**.
    2. Abra **Administrador de configuración de SQL Server**, en **Configuración de red de SQL Server**, haga clic con el botón derecho para seleccionar **Propiedades** en **Protocolos para MSSQLSERVER**. A continuación, en la pestaña **Certificado**, seleccione **Certificado de identificación de SQL Server de almacenamiento de datos** como el certificado y luego guarde los cambios.  
    3. Abra **Administrador de configuración de SQL Server**. En **Servicios de SQL Server**, reinicie los servicios **Servicio SQL Server** y **Servicio de informes**.
    4.  Abra Microsoft Management Console (MMC) y agregue el complemento para **Certificados**; seleccione la opción de administración del certificado para **Cuenta de equipo** de la máquina local. A continuación, en MMC, expanda la carpeta **Personal** > **Certificados** y exporte el **Certificado de identificación de SQL Server de almacenamiento de datos** como un archivo **DER binario codificado X.509 (.CER)**.    
  2.    En el equipo que hospeda SQL Server Reporting Services, abra MMC y agregue el complemento para **Certificados**; luego, seleccione la opción de administración del certificado para **Cuenta de equipo**. En la carpeta **Entidades emisoras raíz de confianza**, importe el **Certificado de identificación de SQL Server de almacenamiento de datos**.


## <a name="data-warehouse-dataflow"></a>Flujo de datos de almacenamiento de datos   
![Diagrama que muestra el flujo de datos lógicos entre los componentes de sitio del almacenamiento de datos](./media/datawarehouse.png)

**Sincronización y almacenamiento de datos**

| Paso   | Detalles  |
|:------:|-----------|  
| **1**  |  El servidor de sitio transfiere y almacena datos en la base de datos del sitio.  |  
| **2**  |      Basándose en su programación y configuración, el punto de servicio de almacenamiento de datos obtiene datos de la base de datos del sitio.  |  
| **3**  |  El punto de servicio de almacenamiento de datos transfiere y almacena una copia de los datos sincronizados en la base de datos de almacenamiento de datos. |  
**Generación de informes**

| Paso   | Detalles  |
|:------:|-----------|  
| **A**  |  Mediante informes integrados, un usuario solicita datos. Esta solicitud se pasa al punto de servicios de informes mediante SQL Server Reporting Services. |  
| **B**  |      La mayoría de los informes se refieren a información actual y estas solicitudes se ejecutan en la base de datos del sitio. |  
| **C**  | Cuando un informe solicita datos históricos, mediante uno de los informes con una *categoría* de **almacenamiento de datos**, la solicitud se ejecuta en la base de datos de almacenamiento de datos.   |  
