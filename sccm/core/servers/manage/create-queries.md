---
title: Creación de consultas
titleSuffix: Configuration Manager
description: Descubra cómo crear e importar consultas en System Center Configuration Manager. Incluye ejemplos de consultas y sugerencias.
ms.date: 12/11/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 868049d3-3209-47ec-b34a-9cc26941893a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 12dd7a4d806a82e3c55898e249d1caa2a6ffb508
ms.sourcegitcommit: 19fc4f27667d51502fc9d7d02d164f2837d65dae
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/19/2018
ms.locfileid: "49461297"
---
# <a name="how-to-create-queries-in-system-center-configuration-manager"></a>Cómo crear consultas en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Puede utilizar este tema para crear o importar consultas en System Center Configuration Manager.  

##  <a name="BKMK_Create"></a> Cómo crear consultas  
 Use este procedimiento para crear consultas en Configuration Manager.  

#### <a name="to-create-a-query"></a>Para crear una consulta  

1.  En la consola de Configuration Manager, elija **Supervisión**.  

2.  En el área de trabajo **Supervisión**, elija **Consultas**. A continuación, en el grupo **Crear** de la pestaña **Inicio**, elija **Crear consulta**.  

3.  En la pestaña **General** del **Asistente para crear consultas**, especifique un nombre único y un comentario opcional para la consulta.  

4.  Si desea importar una consulta existente para utilizarla como base para la nueva consulta, elija **Importar instrucción de consulta**. En el cuadro de diálogo **Examinar consulta**, seleccione una consulta existente que desee importar y, a continuación, elija **Aceptar**.  

5.  En la lista **Tipo de objeto**, seleccione el tipo de objeto que quiere que devuelva la consulta. En la tabla siguiente se describen algunos ejemplos del tipo de objeto que puede buscar:  

    |Tipo de objeto|Descripción|  
    |-----------------|-----------------|  
    |**Recurso del sistema**|Use esta opción para buscar los atributos típicos del sistema, como el nombre NetBIOS de un dispositivo, la versión del cliente, la dirección IP del cliente y la información de los Servicios de dominio de Active Directory.|  
    |**Recurso de usuario**|Use esta opción para buscar información típica de usuario como nombres de usuarios, nombres de grupos de usuarios y nombres de grupos de seguridad.|  
    |**Implementación**|Use esta opción para buscar los atributos típicos de una implementación, como el nombre de la implementación, la programación y la recopilación en la que se implementó.|  

6.  Haga clic en **Editar instrucción de consulta** para abrir el cuadro de diálogo **Propiedades de instrucción** *&lt;nombre de la consulta\>*.  

7.  En la pestaña **General** del cuadro de diálogo **Propiedades de instrucción** *&lt;nombre de la consulta\>*, especifique los atributos que devuelve esta consulta y cómo se van a mostrar. Seleccione el icono **Nuevo** para agregar un nuevo atributo. También puede seleccionar **Mostrar idioma de consulta** para escribir o editar la consulta directamente en el lenguaje de consulta de WMI (WQL). Para obtener ejemplos de consultas de WMI, consulte la sección [Example WQL queries](#BKMK_Example) en este tema.  

    > [!TIP]  
    > Puede utilizar la siguiente documentación de referencia MSDN que le ayudarán a construir sus propias consultas WQL:  
    >   
    > -   [WQL (SQL para WMI)](http://go.microsoft.com/fwlink/p/?LinkId=256653)  
    > -   [Cláusula WHERE](http://go.microsoft.com/fwlink/p/?LinkId=256654)  
    > -   [Operadores WQL](http://go.microsoft.com/fwlink/p/?LinkId=256655)  

8.  En la pestaña **Criterios** del cuadro de diálogo **Propiedades de instrucción** *&lt;nombre de la consulta\>*, especifique los criterios que se usan para refinar los resultados de la consulta. Por ejemplo, podría devolver solo los recursos que tienen un código de sitio de **XYZ** en los resultados de la consulta. Puede configurar varios criterios para una consulta.  

    > [!IMPORTANT]  
    > Si crea una consulta que no contiene ningún criterio, devolverá todos los dispositivos en la recopilación **Todos los sistemas** .  

9. En la pestaña **Combinaciones** del cuadro de diálogo **Propiedades de instrucción** *&lt;nombre de la consulta\>*, puede combinar datos de dos atributos diferentes en los resultados de la consulta. Aunque Configuration Manager crea automáticamente combinaciones de consulta cuando se eligen atributos diferentes para el resultado de la consulta, la pestaña **Combinaciones** proporciona opciones más avanzadas. Las clases de atributo compatibles con System Center 2012 Configuration Manager se muestran en la tabla siguiente:  

    |Tipo de combinación|Descripción|  
    |---------------|-----------------|  
    |Interna|Muestra solo los resultados coincidentes y la usan siempre las combinaciones que se crean automáticamente.|  
    |Izquierda|Muestra todos los resultados para el atributo base y solo los resultados coincidentes para el atributo de combinación.|  
    |Derecha|Muestra todos los resultados para el atributo de combinación y solo los resultados coincidentes para el atributo base.|  
    |Full|Muestra todos los resultados para el atributo base y el atributo de combinación.|  

     Para obtener información sobre cómo usar operaciones de combinación, consulte la documentación de SQL Server.  

10. Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Propiedades de instrucción** *&lt;nombre de la consulta\>*.  

11. En la pestaña **General** del **Asistente para crear consultas**, especifique si los resultados de esta consulta no se limitan a los miembros de una recopilación, se limitan a los miembros de una recopilación especificada o solicitan una recopilación cada vez que se ejecuta la consulta.  

12. Complete el asistente para crear la consulta. La nueva consulta se muestra en el nodo **Consultas** en el área de trabajo **Supervisión** .  

##  <a name="BKMK_Import"></a> Cómo importar consultas  
 Use este procedimiento para importar una consulta a Configuration Manager. Para obtener información sobre cómo exportar consultas, consulte [How to manage queries in System Center Configuration Manager](../../../core/servers/manage/manage-queries.md) (Cómo administrar consultas en System Center Configuration Manager).  

#### <a name="to-import-a-query"></a>Para importar una consulta  

1.  En la consola de Configuration Manager, elija **Supervisión**.  

2.  En el área de trabajo **Supervisión**, elija **Consultas**. En la pestaña **Inicio**, en el grupo **Crear**, seleccione **Importar objetos**.  

3.  En la página **Nombre de archivo MOF** del **Asistente para importar objetos**, elija **Examinar** para seleccionar el archivo Managed Object Format (MOF) que contiene la consulta que quiere importar.  

4.  Revise la información sobre la consulta que quiere importar y, a continuación, complete el asistente. La nueva consulta se muestra en el nodo **Consultas** en el área de trabajo **Supervisión** .  

##  <a name="BKMK_Example"></a> Example WQL queries

Esta sección contiene consultas de WMI de ejemplo que puede usar en su jerarquía o modificarlas para otros fines. Para usar estas consultas, elija **Mostrar idioma de consulta** en el cuadro de diálogo **Propiedades de instrucción de consulta**. A continuación, copie y pegue la consulta en el campo **Instrucción de consulta**.  

> [!TIP]  
> Use el carácter comodín `%` para indicar cualquier cadena de caracteres. Por ejemplo, `%Visio%` devuelve Microsoft Office Visio 2010.  

### <a name="computers-that-run-windows-7"></a>Equipos que ejecutan Windows 7

Use la siguiente consulta para devolver la versión del sistema operativo y el nombre NetBIOS de todos los equipos que ejecutan Windows 7.  

> [!TIP]  
> Para devolver los equipos que ejecutan Windows Server 2008 R2, cambie `%Workstation 6.1%` a `%Server 6.1%`.  

```  
select SMS_R_System.NetbiosName,  
SMS_R_System.OperatingSystemNameandVersion from    
SMS_R_System where   
SMS_R_System.OperatingSystemNameandVersion like "%Workstation 6.1%"  
```  

### <a name="computers-with-a-specific-software-package-installed"></a>Equipos con un paquete de software específico instalado  

Use la siguiente consulta para devolver el nombre NetBIOS y el nombre del paquete de software de todos los equipos que tienen instalado un paquete de software específico. En este ejemplo se muestran todos los equipos con una versión de Microsoft Visio instalada. Reemplace `Microsoft%Visio%` por el paquete de software que quiere consultar.  

> [!TIP]  
> Esta consulta busca el paquete de software con los nombres que se muestran en la lista de programas del Panel de Control de Windows.  

```  
select SMS_R_System.NetbiosName,   
SMS_G_System_ADD_REMOVE_PROGRAMS.DisplayName from    
SMS_R_System inner join SMS_G_System_ADD_REMOVE_PROGRAMS on   
SMS_G_System_ADD_REMOVE_PROGRAMS.ResourceId =   
SMS_R_System.ResourceId where   
SMS_G_System_ADD_REMOVE_PROGRAMS.DisplayName like "Microsoft%Visio%"  
```  

### <a name="computers-that-are-in-a-specific-active-directory-domain-services-organizational-unit"></a>Equipos que están en una unidad organizativa específica de Active Directory Domain Services

Use la siguiente consulta para devolver el nombre NetBIOS y el nombre de unidad organizativa de todos los equipos de una unidad organizativa. Reemplace el texto `OU Name` por el nombre de la unidad organizativa que quiere consultar.  

```  
select SMS_R_System.NetbiosName,   
SMS_R_System.SystemOUName from    
SMS_R_System where   
SMS_R_System.SystemOUName = "OU Name"  
```  

### <a name="computers-with-a-specific-netbios-name"></a>Equipos con un nombre NetBIOS específico

Use la siguiente consulta para devolver el nombre NetBIOS de todos los equipos que empiecen por una cadena de caracteres específica. En este ejemplo, la consulta devuelve todos los equipos con un nombre NetBIOS que empiece por `ABC`.  

```  
select SMS_R_System.NetbiosName from    
SMS_R_System where SMS_R_System.NetbiosName like "ABC%"  
```  

###  <a name="BKMK_DeviceType"></a> Dispositivos de un tipo específico

Los tipos de dispositivos se almacenan en la base de datos de Configuration Manager en la clase de recurso **sms_r_system** y el nombre de atributo **AgentEdition**. Use la siguiente consulta para recuperar solo los dispositivos que coinciden con la edición de agente del tipo de dispositivo que especifique:  

```  
Select SMS_R_System.ClientEdition from SMS_R_System where SMS_R_System.ClientEdition = <Device ID>  
```  

Use uno de los siguientes valores para *&lt;Id. de dispositivo\>*:  

|Tipo de dispositivo|Valor de AgentEdition|  
|-----------------|---------------------------|  
|Equipo portátil o de escritorio de Windows|0|  
|Dispositivo basado en ARM de Windows (que ejecuta Windows RT)|1|  
|Windows Mobile 6.5|2|  
|Nokia Symbian|3|  
|Windows Phone|4|  
|Equipo Mac|5|  
|Windows CE|6|  
|Windows Embedded|7|  
|iOS|8|  
|iPad|9|  
|iPod Touch|10|  
|Android|11|  
|Sistema Intel en un chip|12|  
|Servidores Unix y Linux|13|  
|Apple macOS (MDM)|14|
|Microsoft HoloLens (MDM)|15|
|Microsoft Surface Hub (MDM)|16|
|Android for Work|17|

 Por ejemplo, si quiere que la consulta devuelva solo los equipos Mac, use la siguiente consulta:  

```  
Select SMS_R_System.ClientEdition from SMS_R_System where SMS_R_System.ClientEdition = 5  
```  

## <a name="see-also"></a>Consulte también  
 [Operaciones y mantenimiento de consultas en System Center Configuration Manager](../../../core/servers/manage/operations-and-maintenance-for-queries.md)
