---
title: Crear consultas | System Center Configuration Manager
description: "Descubra cómo crear e importar consultas en System Center Configuration Manager. Incluye ejemplos de consultas y sugerencias."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 868049d3-3209-47ec-b34a-9cc26941893a
caps.latest.revision: 5
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 1cbba80a73fdd66d84d38e710c02cc79ab972b81


---
# <a name="how-to-create-queries-in-system-center-configuration-manager"></a>Cómo crear consultas en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Consulte las siguientes secciones de este tema para crear o importar consultas en System Center Configuration Manager.  

-   [How to Create Queries](#BKMK_Create)  

-   [How to Import Queries](#BKMK_Import)  

-   [Example WQL Queries](#BKMK_Example)  

##  <a name="a-namebkmkcreatea-how-to-create-queries"></a><a name="BKMK_Create"></a> Cómo crear consultas  
 Use este procedimiento para crear consultas en Configuration Manager.  

#### <a name="to-create-a-query"></a>Para crear una consulta  

1.  En la consola de Configuration Manager, haga clic en **Supervisión**.  

2.  En el área de trabajo **Supervisión** , haga clic en **Consultas** y, a continuación, en la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear consulta**.  

3.  En la pestaña **General** del **Asistente para crear consultas**, especifique un nombre único y un comentario opcional para la consulta.  

4.  Si quiere importar una consulta existente para usarla como base para la nueva consulta, haga clic en **Importar instrucción de consulta** y, a continuación, en el cuadro de diálogo **Examinar consulta** , seleccione la consulta existente que quiera importar y haga clic en **Aceptar**.  

5.  En la lista **Tipo de objeto** , seleccione el tipo de objeto que quiere que devuelva la consulta. En la tabla siguiente se describen algunos ejemplos del tipo de objeto que puede buscar:  

    |Tipo de objeto|Descripción|  
    |-----------------|-----------------|  
    |**Recurso del sistema**|Use esta opción para buscar los atributos típicos del sistema, como el nombre NetBIOS de un dispositivo, la versión del cliente, la dirección IP del cliente y la información de los Servicios de dominio de Active Directory.|  
    |**Recurso de usuario**|Use esta opción para buscar información típica de usuario como nombres de usuarios, nombres de grupos de usuarios y nombres de grupos de seguridad.|  
    |**Implementación**|Use esta opción para buscar los atributos típicos de una implementación, como el nombre de la implementación, la programación y la recopilación en la que se implementó.|  

6.  Haga clic en **Editar instrucción de consulta** para abrir el cuadro de diálogo **Propiedades de instrucción** *&lt;nombre de la consulta\>*.  

7.  En la pestaña **General** del cuadro de diálogo **Propiedades de instrucción** *&lt;nombre de la consulta\>*, especifique los atributos que devuelve esta consulta y cómo se mostrarán. Haga clic en el icono **Nuevo** para agregar un nuevo atributo. También puede hacer clic en **Mostrar idioma de consulta** para escribir o editar la consulta directamente en el lenguaje de consulta de WMI (WQL). Para obtener ejemplos de consultas de WMI, consulte la sección [Example WQL queries](#BKMK_Example) en este tema.  

    > [!TIP]  
    >  Puede usar la siguiente documentación de referencia MSDN para ayudarle a construir sus propias consultas WQL:  
    >   
    >  -   [WQL (SQL para WMI)](http://go.microsoft.com/fwlink/p/?LinkId=256653)  
    > -   [Cláusula WHERE](http://go.microsoft.com/fwlink/p/?LinkId=256654)  
    > -   [Operadores WQL](http://go.microsoft.com/fwlink/p/?LinkId=256655)  

8.  En la pestaña **Criterios** del cuadro de diálogo **Propiedades de instrucción** *&lt;nombre de la consulta\>*, especifique los criterios que se usan para refinar los resultados de la consulta. Por ejemplo, podría devolver solo los recursos que tienen un código de sitio de **XYZ** en los resultados de la consulta. Puede configurar varios criterios para una consulta.  

    > [!IMPORTANT]  
    >  Si crea una consulta que no contiene ningún criterio, devolverá todos los dispositivos en la recopilación **Todos los sistemas** .  

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

##  <a name="a-namebkmkimporta-how-to-import-queries"></a><a name="BKMK_Import"></a> Cómo importar consultas  
 Use este procedimiento para importar una consulta a Configuration Manager. Para obtener información sobre cómo exportar consultas, consulte [How to manage queries in System Center Configuration Manager](../../../core/servers/manage/manage-queries.md) (Cómo administrar consultas en System Center Configuration Manager).  

#### <a name="to-import-a-query"></a>Para importar una consulta  

1.  En la consola de Configuration Manager, haga clic en **Supervisión**.  

2.  En el área de trabajo **Supervisión** , haga clic en **Consultas** y, a continuación, en la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Importar objetos**.  

3.  En la página **Nombre de archivo MOF** del **Asistente para importar objetos**, haga clic en **Examinar** para seleccionar el archivo Managed Object Format (MOF) que contiene la consulta que quiere importar.  

4.  Revise la información sobre la consulta que quiere importar y, a continuación, complete el asistente. La nueva consulta se muestra en el nodo **Consultas** en el área de trabajo **Supervisión** .  

##  <a name="a-namebkmkexamplea-example-wql-queries"></a><a name="BKMK_Example"></a> Example WQL queries  
 Esta sección contiene consultas de WMI de ejemplo que puede usar en su jerarquía o modificarlas para otros fines. Para usar estas consultas, haga clic en **Mostrar idioma de consulta** del cuadro de diálogo **Propiedades de instrucción de consulta** y, a continuación, copie y pegue la consulta en el campo **Instrucción de consulta** .  

> [!TIP]  
>  Use el carácter comodín **%** para indicar cualquier cadena de caracteres. Por ejemplo, **%Visio%** devuelve Microsoft Office Visio 2010.  

### <a name="computers-that-run-windows-7"></a>Equipos que ejecutan Windows 7  
 Use la siguiente consulta para devolver la versión del sistema operativo y el nombre NetBIOS de todos los equipos que ejecutan Windows 7.  

> [!TIP]  
>  Para devolver los equipos que ejecutan Windows Server 2008 R2, cambie **%Workstation 6.1%** a **%Server 6.1%**.  

```  
select SMS_R_System.NetbiosName,  
SMS_R_System.OperatingSystemNameandVersion from    
SMS_R_System where   
SMS_R_System.OperatingSystemNameandVersion like "%Workstation 6.1%"  
```  

### <a name="computers-with-a-specific-software-package-installed"></a>Equipos con un paquete de software específico instalado  
 Use la siguiente consulta para devolver el nombre NetBIOS y el nombre del paquete de software de todos los equipos que tienen instalado un paquete de software específico. En este ejemplo se muestran todos los equipos con una versión de Microsoft Visio instalada. Reemplace **%Visio%** con el paquete de software que quiere consultar.  

> [!TIP]  
>  Esta consulta busca el paquete de software con los nombres que se muestran en la lista de programas del Panel de Control de Windows.  

```  
select SMS_R_System.NetbiosName,   
SMS_G_System_ADD_REMOVE_PROGRAMS.DisplayName from    
SMS_R_System inner join SMS_G_System_ADD_REMOVE_PROGRAMS on   
SMS_G_System_ADD_REMOVE_PROGRAMS.ResourceId =   
SMS_R_System.ResourceId where   
SMS_G_System_ADD_REMOVE_PROGRAMS.DisplayName like "%Visio%"  
```  

### <a name="computers-that-are-in-a-specific-active-directory-domain-services-organizational-unit-ou"></a>Equipos que están en una unidad organizativa (UO) específica de los Servicios de dominio de Active Directory  
 Use la siguiente consulta para devolver el nombre NetBIOS y el nombre de UO de todos los equipos de una UO. Reemplace el texto **OU Name** con el nombre de la UO que quiere consultar.  

```  
select SMS_R_System.NetbiosName,   
SMS_R_System.SystemOUName from    
SMS_R_System where   
SMS_R_System.SystemOUName = "OU Name"  
```  

### <a name="computers-with-a-specific-netbios-name"></a>Equipos con un nombre NetBIOS específico  
 Use la siguiente consulta para devolver el nombre NetBIOS de todos los equipos que empiecen por una cadena de caracteres específica. En este ejemplo, la consulta devuelve todos los equipos con un nombre NetBIOS que empiece por **ABC**.  

```  
select SMS_R_System.NetbiosName from    
SMS_R_System where SMS_R_System.NetbiosName like "ABC%"  
```  

###  <a name="a-namebkmkdevicetypea-devices-of-a-specific-type"></a><a name="BKMK_DeviceType"></a> Dispositivos de un tipo específico  
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

 Por ejemplo, si quiere que la consulta devuelva solo los equipos Mac, use la siguiente consulta:  

```  
Select SMS_R_System.ClientEdition from SMS_R_System where SMS_R_System.ClientEdition = 5  
```  

## <a name="see-also"></a>Véase también  
 [Operaciones y mantenimiento de consultas en System Center Configuration Manager](../../../core/servers/manage/operations-and-maintenance-for-queries.md)



<!--HONumber=Nov16_HO1-->


