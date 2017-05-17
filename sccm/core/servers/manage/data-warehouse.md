---
title: Almacenamiento de datos | Microsoft Docs
description: Punto de servicio de almacenamiento de datos y base de datos para System Center Configuration Manager
ms.custom: na
ms.date: 3/28/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aaf43e69-68b4-469a-ad58-9b66deb29057
caps.latest.revision: 
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 3c2a07f560e0aa3d2beb7cc50e71c98ac45c27e1
ms.openlocfilehash: 9239f6e749c368835e8594ca2d07378d8555b99e
ms.contentlocale: es-es
ms.lasthandoff: 05/17/2017


---
#  <a name="the-data-warehouse-service-point-for-system-center-configuration-manager"></a>El punto de servicio de almacenamiento de datos para System Center Configuration Manager
*Se aplica a: System Center Configuration Manager (rama actual)*

A partir de la versión 1702 puede usar el punto de servicio de almacenamiento de datos para almacenar y generar informes de datos históricos a largo plazo para su implementación de Configuration Manager.

> [!TIP]  
> Con la versión 1702, se presentó el punto de servicio de almacenamiento de datos como una característica de versión preliminar. Para habilitarla, consulte [Use pre-release features](/sccm/core/servers/manage/pre-release-features) (Uso de características de versión preliminar).

El almacenamiento de datos admite hasta 2 TB de datos, con marcas de tiempo para el seguimiento de cambios. El almacenamiento de datos se consigue mediante sincronizaciones automatizadas desde la base de datos del sitio de Configuration Manager a la base de datos de almacenamiento de datos. Puede acceder a esta información desde su punto de Reporting Services.


Los datos que se sincronizan incluyen lo siguiente de los grupos de datos globales y datos de sitio:
- Mantenimiento de infraestructura
- Seguridad
- Cumplimiento
- Malware   
- Implementaciones de software
- Detalles de inventario (en cambio, el historial de inventario no se sincroniza)

Cuando se instala el rol de sistema de sitio, instala y configura la base de datos del almacén de datos. También instala varios informes de forma que pueda buscar fácilmente estos datos y crear informes sobre ellos.



## <a name="prerequisites-for-the-data-warehouse-service-point"></a>Requisitos previos del punto de servicio de almacenamiento de datos
- El equipo en el que instale el rol de sistema de sitio necesita .NET Framework 4.5.2 o versiones posteriores.
- La cuenta de equipo correspondiente al equipo en el que se instala el rol de sistema de sitio se utiliza para sincronizar datos con la base de datos del almacén de datos. La cuenta requiere los permisos siguientes:  
  - **Administrator** en el equipo que hospedará la base de datos del almacenamiento de datos.
  - **DB_owner** en la base de datos del almacenamiento de datos.
-    La base de datos del almacenamiento de datos es compatible con una instancia predeterminada o con nombre de SQL Server 2012 o posterior. La edición debe ser Enterprise o Datacenter.
  - Grupo de disponibilidad AlwaysOn de SQL Server: esta configuración no se admite.
  - Clúster de SQL Server: no se admiten clústeres de conmutación por error de SQL Server. Esto es porque la base de datos del almacenamiento de datos no se ha probado a fondo en clústeres de conmutación por error de SQL Server.
  - Cuando la base de datos del almacenamiento de datos está ubicada en un emplazamiento remoto respecto a la base de datos del servidor del sitio, debe tener una licencia independiente para el servidor SQL Server que hospeda la base de datos.

> [!IMPORTANT]  
> No se admite el almacenamiento de datos cuando el equipo que ejecuta el punto de servicio de almacenamiento de datos o que hospeda la base de datos de almacenamiento de datos ejecuta uno de los siguientes idiomas:
> - JPN (japonés)
> - KOR (coreano)
> - CHS (chino simplificado)
> - CHT (chino tradicional); este problema se resolverá en una versión futura.


## <a name="install-the-data-warehouse"></a>Instalar el almacenamiento de datos
Puede instalar el rol de sistema de sitio del almacenamiento de datos solo en el sitio de nivel superior de la jerarquía (es decir, un sitio de administración central o un sitio primario independiente).

Cada jerarquía admite una única instancia de este rol y puede encontrarse en cualquier sistema de sitio de ese sitio de nivel superior. El servidor SQL Server que hospeda la base de datos para el almacenamiento puede ser local para el rol de sistema de sitio o remoto. Aunque el almacenamiento de datos funciona con el punto de Reporting Services que está instalado en el mismo sitio, los dos roles de sistema de sitio no necesitan estar instalados en el mismo servidor.   

Para instalar el rol, use el **Asistente para agregar roles de sistema de sitio** o el **Asistente para crear servidor de sistema de sitio**. Para obtener más información, consulte [Instalación de roles de sistema de sitio para System Center Configuration Manager](/sccm/core/servers/deploy/configure/install-site-system-roles).  

Cuando instala el rol, Configuration Manager crea la base de datos de almacenamiento de datos en la instancia de SQL Server que especifique. Si especifica el nombre de una base de datos existente (como haría si [moviera la base de datos de almacenamiento de datos a un servidor de SQL Server nuevo](#move-the-data-warehouse-database)), Configuration Manager no crea una base de datos nueva sino que usa la que especifique.

### <a name="configurations-used-during-installation"></a>Configuraciones que se han usado durante la instalación
Página **Selección de rol del sistema**:  

Página **General**:
-     **Configuración de conexión de base de datos de almacenamiento de datos de Configuration Manager**:
 - **Nombre de dominio completo de SQL Server**:  
 Especifique el nombre de dominio completo (FQDN) del servidor que hospeda la base de datos del punto de servicio de almacenamiento de datos.
 - **Nombre de instancia de SQL Server, si corresponde**:   
 Si no utiliza una instancia predeterminada de SQL Server, debe especificar la instancia.
 - **Nombre de la base de datos**:   
 Especifique un nombre para la base de datos de almacenamiento de datos.  Configuration Manager creará la base de datos de almacenamiento de datos con este nombre. Si especifica un nombre de base de datos que ya existe en la instancia de SQL Server, Configuration Manager usará esa base de datos.
 - **Puerto de SQL Server utilizado para la conexión**:   
 Especifique el número de puerto TCP/IP que está configurado para el servidor SQL Server que hospeda la base de datos del almacenamiento de datos. Este puerto lo usa el servicio de sincronización del almacenamiento de datos para conectarse a la base de datos de dicho almacenamiento.  

Página **Programación de sincronización**:   
- **Programación de sincronización**:
 - **Hora de inicio**:  
 Especifique la hora a la que desea que se inicie la sincronización del almacenamiento de datos.
 - **Patrón de periodicidad**:
    - **Diariamente**: permite especificar que la sincronización se ejecute cada día.
    - **Semanalmente**: permite especificar un solo día cada semana, con una periodicidad semanal para la sincronización.

## <a name="reporting"></a>Generación de informes
Después de instalar un punto de servicio de almacenamiento de datos, varios informes pasan a estar disponibles en el punto de Reporting Services que está instalado en el mismo sitio. Si instala el punto de servicio de almacenamiento de datos antes de instalar un punto de Reporting Services, los informes se agregarán automáticamente cuando posteriormente se instale el punto de Reporting Services.

El rol de sistema de sitio de almacenamiento de datos incluye los siguientes informes, que tienen una categoría de **almacenamiento de datos**:
 - **Implementación de aplicaciones - Histórico**:   
 Vea los detalles de la implementación de aplicaciones para una máquina y una aplicación determinada.
 - **Endpoint Protection y compatibilidad con actualizaciones de software - Histórico**: Vea los equipos a los que les faltan actualizaciones de software.  
 - **Inventario de hardware general - Histórico**:      
 Vea todo el inventario de hardware para un equipo específico.
 - **Inventario de software general - Histórico**:      
 Vea todo el inventario de software para un equipo específico.
 - **Información general del mantenimiento de infraestructura - Histórico**:     
 Muestra información general del mantenimiento de su infraestructura de Configuration Manager.
 - **Lista de malware detectado - Histórico**:     
 Vea el malware que se ha detectado en la organización.
 - **Resumen de distribución de software - Histórico**:     
 Un resumen de distribución de software para un equipo y anuncio específico.


## <a name="expand-an-existing-stand-alone-primary-into-a-hierarchy"></a>Expansión de un sitio primario independiente existente en una jerarquía
Antes de instalar un sitio de administración central para expandir un sitio primario independiente existente, primero debe desinstalar el rol de punto de servicio de almacenamiento de datos. Después de instalar el sitio de administración central, puede instalar el rol de sistema de sitio en el sitio de administración central.  

A diferencia de un movimiento de la base de datos del almacenamiento de datos, este cambio produce una pérdida de los datos históricos que se han sincronizado previamente en el sitio primario. No se admite la copia de seguridad de la base de datos desde el sitio primario y su restauración en el sitio de administración central.




## <a name="move-the-data-warehouse-database"></a>Mover la base de datos de almacenamiento de datos
Use los siguientes pasos para mover la base de datos de almacenamiento de datos a un servidor de SQL Server nuevo:

1.    Use SQL Server Management Studio para realizar una copia de seguridad de la base de datos de almacenamiento de datos y, después, restaure esa base de datos en un servidor de SQL Server en el nuevo equipo que hospedará el almacenamiento de datos.   
> [!NOTE]     
> Después de restaurar la base de datos en el nuevo servidor, asegúrese de que los permisos de acceso de la base de datos son los mismos en la nueva base de datos de almacenamiento de datos que en la base de datos de almacenamiento de datos original.  

2.    Use la consola de Configuration Manager para quitar el rol de sistema de sitio del punto de servicio de almacenamiento de datos del servidor actual.
3.    Reinstale el punto de servicio de almacenamiento de datos y especifique el nombre del nuevo servidor de SQL Server y la instancia que hospeda la base de datos de almacenamiento de datos que ha restaurado.
4.    Después de que se instale el rol de sistema de sitio, se completa el movimiento.

## <a name="troubleshooting-data-warehouse-issues"></a>Solución de problemas del almacenamiento de datos
**Archivos de registro**:  
Use los siguientes registros para investigar problemas con la instalación del punto de servicio de almacenamiento de datos o con la sincronización de datos:
 - *DWSSMSI.log* y *DWSSSetup.log*: use estos registros para investigar errores al instalar el punto de servicio de almacenamiento de datos.
 - *Microsoft.ConfigMgrDataWarehouse.log*: use este registro para investigar la sincronización de datos entre la base de datos del sitio y la base de datos de almacenamiento de datos.

**Error de configuración**  
 La instalación del punto de servicio de almacenamiento de datos no se puede realizar en un servidor de sistema de sitio remoto cuando el almacenamiento de datos es el primer rol de sistema de sitio instalado en ese equipo.  
  - **Solución**:   
    Asegúrese de que el equipo en el que va a instalar el punto de servicio de almacenamiento de datos ya hospeda al menos otro rol de sistema de sitio.  


**Problemas de sincronización conocidos**:   
La sincronización genera el siguiente error en *Microsoft.ConfigMgrDataWarehouse.log*: **"Error al rellenar los objetos de esquema"**.  
 - **Solución**:  
    Asegúrese de que la cuenta de equipo del equipo que hospeda el rol de sistema de sitio es **db_owner** en la base de datos del almacenamiento de datos.

Los informes de almacenamiento de datos no se pueden abrir cuando la base de datos del almacenamiento de datos y el punto de servicio de informes se encuentran en diferentes sistemas de sitio.  

 - **Solución**:  
    Conceda a la **cuenta de punto de Reporting Services** el permiso **db_datareader** en la base de datos del almacenamiento de datos.

Al abrir un informe de almacenamiento de datos, se devuelve el siguiente el error:

*Error al procesar el informe. (rsProcessingAborted) No se puede crear una conexión al origen de datos 'AutoGen__39B693BB_524B_47DF_9FDB_9000C3118E82_'. (rsErrorOpeningConnection) Se ha establecido la conexión con el servidor correctamente, pero se ha producido un error durante el inicio de sesión previo del protocolo de enlace. (Proveedor: Proveedor de SSL, error: 0 - La cadena de certificación fue emitida por una entidad que no es de confianza.)*.

- **Solución**: Siga los pasos siguientes para configurar certificados:

  1. En el equipo que hospeda la base de datos del almacenamiento de datos:

    1. Abra IIS, haga clic en **Certificados de servidor**, haga clic con el botón derecho en **Crear certificado autofirmado** y luego especifique el "nombre descriptivo" del nombre del certificado como **Certificado de identificación de SQL Server de almacenamiento de datos**. Seleccione el almacén de certificados como **Personal**.
    2. Abra **Administrador de configuración de SQL Server**, en **Configuración de red de SQL Server**, haga clic con el botón derecho para seleccionar **Propiedades** en **Protocolos para MSSQLSERVER**. A continuación, en la pestaña **Certificado**, seleccione **Certificado de identificación de SQL Server de almacenamiento de datos** como el certificado y luego guarde los cambios.  
    3. Abra **Administrador de configuración de SQL Server**, en **Servicios de SQL Server**, reinicie **Servicio SQL Server** y **Servicio de informes**.
    4.    Abra Microsoft Management Console (MMC) y agregue el complemento para **Certificados**; seleccione la opción de administración del certificado para **Cuenta de equipo** de la máquina local. A continuación, en MMC, expanda la carpeta **Personal** > **Certificados** y exporte el **Certificado de identificación de SQL Server de almacenamiento de datos** como un archivo **DER binario codificado X.509 (.CER)**.    
  2.    En el equipo que hospeda SQL Server Reporting Services, abra MMC y agregue el complemento para **Certificados**; luego, la opción de administración del certificado para **Cuenta de equipo**. En la carpeta **Entidades emisoras raíz de confianza**, importe el **Certificado de identificación de SQL Server de almacenamiento de datos**.


## <a name="data-warehouse-dataflow"></a>Flujo de datos de almacenamiento de datos   
![flujo_almacenamientoDeDatos](./media/datawarehouse.png)

**Sincronización y almacenamiento de datos**

| Paso   | Detalles  |
|:------:|-----------|  
| **1**  |     El servidor de sitio transfiere y almacena datos en la base de datos del sitio.  |  
| **2**  |      Basándose en su programación y configuración, el punto de servicio de almacenamiento de datos obtiene datos de la base de datos del sitio.  |  
| **3**  |  El punto de servicio de almacenamiento de datos transfiere y almacena una copia de los datos sincronizados en la base de datos de almacenamiento de datos. |  
**Generación de informes**

| Paso   | Detalles  |
|:------:|-----------|  
| **A**  |  Mediante informes integrados, un usuario solicita datos. Esta solicitud se pasa al punto de Reporting Services mediante SQL Server Reporting Services. |  
| **B**  |      La mayoría de los informes se refieren a información actual y estas solicitudes se ejecutan en la base de datos del sitio. |  
| **C**  | Cuando un informe solicita datos históricos, mediante uno de los informes con una *Categoría* de **Almacenamiento de datos**, la solicitud se ejecuta en la base de datos de almacenamiento de datos.   |  

