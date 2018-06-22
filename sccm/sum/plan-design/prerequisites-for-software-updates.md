---
title: Requisitos previos para las actualizaciones de software
titleSuffix: Configuration Manager
description: Obtenga información sobre los requisitos previos para las actualizaciones de software en System Center Configuration Manager.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 02/02/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: fdf05118-162a-411e-b72e-386b9dc9a5e1
ms.openlocfilehash: 1c5377096ef67057f3f38bb71fb611b7993ecb6b
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32353113"
---
# <a name="prerequisites-for-software-updates-in-system-center-configuration-manager"></a>Requisitos previos para las actualizaciones de software en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

En este artículo se muestran los requisitos previos para las actualizaciones de software en System Center Configuration Manager. Sus dependencias externas e internas se muestran en tablas independientes.  

## <a name="software-update-dependencies-that-are-external-to-configuration-manager"></a>Dependencias de actualizaciones de software externas de Configuration Manager  
 En las siguientes secciones se incluyen las dependencias externas para las actualizaciones de software.  

### <a name="internet-information-services"></a>Internet Information Services  
 Internet Information Services (IIS) debe estar instalado en los servidores de sistema de sitio para poder ejecutar el punto de actualización de software, el punto de administración y el punto de distribución. Para obtener más información, consulte [Prerequisites for site system roles](../../core/plan-design/configs/site-and-site-system-prerequisites.md) (Requisitos previos de los roles de sistema de sitio).  

### <a name="windows-server-update-services"></a>Windows Server Update Services  
 Windows Server Update Services (WSUS) es necesario para la sincronización de las actualizaciones de software y para el análisis de la aplicabilidad de las actualizaciones de software en los clientes. El servidor WSUS debe instalarse antes de crear el rol de punto de actualización de software. Se admiten las siguientes versiones de WSUS para un punto de actualización de software:  

-   WSUS 10.0 (rol de Windows Server 2016)
-   WSUS 6.2 y 6.3 (rol de Windows Server 2012 y Windows Server 2012 R2)  
-   WSUS 3.2 (rol de Windows Server 2008 R2)  

Si hay varios puntos de actualización de software en un sitio, asegúrese de que todos ejecutan la misma versión de WSUS.  

> [!WARNING]  
>  La clasificación de actualizaciones de software **Actualizaciones** solo se admite a partir de WSUS 4.0. Antes de sincronizar esta nueva clasificación y poder evaluar los equipos con Windows 10 en un plan de mantenimiento de Windows 10, es fundamental que instale la [revisión 3095113](https://support.microsoft.com/kb/3095113) para WSUS en sus servidores de sitio y puntos de actualización de software. Esta revisión permite a WSUS en un servidor basado en Windows Server 2012 o en Windows Server 2012 R2 sincronizar y distribuir actualizaciones de características para Windows 10. Para obtener más información, consulte [Manage Windows as a service](../../osd/deploy-use/manage-windows-as-a-service.md) (Administrar Windows como servicio).  
>   
>  Si sincroniza las actualizaciones de software con la clasificación **Actualizaciones** antes de instalar la [revisión 3095113](https://support.microsoft.com/kb/3095113), consulte [Recover from synchronizing the Actualizaciones category before you install KB 3095113](#BKMK_RecoverUpgrades).  

### <a name="wsus-administration-console"></a>Consola de administración de WSUS  
 La consola de administración de WSUS es necesaria en el servidor de sitio de Configuration Manager si el punto de actualización de software está en un servidor de sistema de sitio remoto y WSUS no se ha instalado todavía en el servidor de sitio.  

> [!IMPORTANT]  
> La versión de WSUS en el servidor de sitio debe ser igual a la versión de WSUS que se ejecuta en los puntos de actualización de software.
>
> No use la consola de administración de WSUS para configurar opciones de WSUS. Configuration Manager se conecta a la instancia de WSUS que se ejecuta en el punto de actualización de software y configura las opciones adecuadas.  



### <a name="windows-update-agent"></a>Agente de Windows Update  
 El cliente de Agente de Windows Update (WUA) es necesario para que los clientes puedan conectarse al servidor de WSUS. WUA recupera la lista de actualizaciones de software cuyo cumplimiento debe analizarse.  

 Al instalar Configuration Manager, se descarga la versión más reciente de WUA. Después, cuando se instala el cliente de Configuration Manager, WUA se actualizará si es necesario. En cambio, si se produce un error en la instalación, debe usar otro método para actualizar WUA.  

## <a name="software-update-dependencies-that-are-internal-to-configuration-manager"></a>Dependencias de actualizaciones de software internas de Configuration Manager  
 En las secciones siguientes se incluyen las dependencias internas para las actualizaciones de software en Configuration Manager.  

### <a name="management-points"></a>Puntos de administración  
 Los puntos de administración transfieren información entre los equipos cliente y el sitio de Configuration Manager. Estos puntos son necesarios para las actualizaciones de software.  

### <a name="software-update-points"></a>Puntos de actualización de software  
 Debe instalar un punto de actualización de software en el servidor de WSUS para poder implementar las actualizaciones de software en Configuration Manager. Para obtener más información, consulte [Install and configure a software update point](../get-started/install-a-software-update-point.md) (Instalar y configurar un punto de actualización de software).

### <a name="distribution-points"></a>Puntos de distribución  
 Los puntos de distribución son necesarios para almacenar el contenido de las actualizaciones de software. Para obtener más información sobre cómo instalar puntos de distribución y administrar contenido, consulte [Manage content and content infrastructure](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md) (Administrar el contenido y la infraestructura de contenido).  

### <a name="client-settings-for-software-updates"></a>Configuración de cliente para las actualizaciones de software  
 Las actualizaciones de software están habilitadas para los clientes de forma predeterminada. Sin embargo, hay otras opciones disponibles que controlan cómo y cuándo los clientes evalúan el cumplimiento de las actualizaciones de software y controlan cómo se instalan.  

 Vea los siguientes artículos para más información:  

-   [Configuración de cliente para las actualizaciones de software](../get-started/manage-settings-for-software-updates.md#BKMK_ClientSettings)   

-   [Configuración de cliente para las actualizaciones de software](../../core/clients/deploy/about-client-settings.md#software-updates)  

### <a name="reporting-services-points"></a>Puntos de servicios de informes  
 El rol de sistema de sitio de punto de servicios de informes puede mostrar informes de las actualizaciones de software. Este rol es opcional pero se recomienda. Para más información sobre cómo crear un punto de servicios de informes, vea [Configuración de informes](../../core/servers/manage/configuring-reporting.md).  

##  <a name="BKMK_RecoverUpgrades"></a> Recuperación de la sincronización de la categoría Actualizaciones antes de instalar KB 3095113  
 Debe instalar la [revisión 3095113](https://support.microsoft.com/kb/3095113) para WSUS en los puntos de actualización de software y en los servidores de sitio antes de sincronizar la clasificación **Actualizaciones** . Si la revisión no está instalada cuando se habilita la clasificación **Actualizaciones**, WSUS verá la actualización de características de la compilación 1511 de Windows 10 aunque no pueda descargar e implementar correctamente los paquetes asociados. 
 
 Si sincroniza las actualizaciones sin haber instalado primero la [revisión 3095113](https://support.microsoft.com/kb/3095113), la base de datos de WSUS (SUSDB) se rellenará con datos inutilizables. Esos datos deben borrarse para que las actualizaciones se puedan implementar correctamente. Utilice el siguiente procedimiento para recuperarse de este problema.  

#### <a name="to-recover-from-synchronizing-the-upgrades-classification-before-you-install-kb-3095113"></a>Para recuperarse de la sincronización de la clasificación Actualizaciones antes de instalar KB 3095113  

1.  Elimine las actualizaciones de software con la clasificación **Actualizaciones**. Puede usar un script de PowerShell similar al siguiente script de ejemplo:  

    ```  
    $Server = Get-WSUSServer  
    $Config = $Server.GetConfiguration()  
    $Update10563 = “df4e45a3-946d-4467-b3fd-8621174bb666”  
    $UpdateGUID = New-Object Guid($Update10563)  
    $Server.DeleteUpdate($UpdateGUID)  
    ```  

    > [!IMPORTANT]  
    >  Debe ejecutar el script en todos los puntos de actualización de software en su jerarquía de Configuration Manager antes de ir al paso siguiente.  

     Para eliminar las actualizaciones de software con la clasificación **Actualizaciones** de forma masiva, puede modificar el script de PowerShell para leer varios GUID desde un archivo de texto.  

2.  Desactive la clasificación **Actualizaciones** en las propiedades del componente Punto de actualización de software. Para más información, vea [Configurar las clasificaciones y los productos](../get-started/configure-classifications-and-products.md). Luego, inicie la sincronización de las actualizaciones de software. Para más información, vea [Sincronizar actualizaciones de software](../get-started/synchronize-software-updates.md).  

3.  Instale la [revisión 3095113](https://support.microsoft.com/kb/3095113) para WSUS en sus servidores de sitio y puntos de actualización de software.  

4.  Active la clasificación **Actualizaciones** en las propiedades del componente Punto de actualización de software. Para más información, vea [Configurar las clasificaciones y los productos](../get-started/configure-classifications-and-products.md). Luego, inicie la sincronización de las actualizaciones de software. Para más información, vea [Sincronizar actualizaciones de software](../get-started/synchronize-software-updates.md).  

## <a name="next-steps"></a>Pasos siguientes
[Preparar la administración de actualizaciones de software](../get-started/prepare-for-software-updates-management.md)
