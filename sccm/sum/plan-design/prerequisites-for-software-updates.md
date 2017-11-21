---
title: Requisitos previos para las actualizaciones de software
titleSuffix: Configuration Manager
description: "Obtenga información sobre los requisitos previos para las actualizaciones de software en System Center Configuration Manager."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-sum
ms.assetid: fdf05118-162a-411e-b72e-386b9dc9a5e1
ms.openlocfilehash: 905ecc023dd181a8d4801860898b05aff5e4e07f
ms.sourcegitcommit: 986fc2d54f7c5fa965fd4df42f4db4ecce6b79cb
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="prerequisites-for-software-updates-in-system-center-configuration-manager"></a>Requisitos previos para las actualizaciones de software en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

En este tema aparecen los requisitos previos para las actualizaciones de software en System Center Configuration Manager. Sus dependencias externas e internas se muestran en tablas independientes.  

## <a name="software-update-dependencies-external-to-configuration-manager"></a>Dependencias externas de actualizaciones de software de Configuration Manager  
 En las secciones siguientes se incluyen las dependencias externas para las actualizaciones de software.  

### <a name="internet-information-services-iis"></a>Internet Information Services (IIS)  
 Internet Information Services (IIS) debe estar en los servidores de sistema de sitio para poder ejecutar el punto de actualización de software, el punto de administración y el punto de distribución. Para obtener más información, consulte [Prerequisites for site system roles](../../core/plan-design/configs/site-and-site-system-prerequisites.md) (Requisitos previos de los roles de sistema de sitio).  

### <a name="windows-server-update-services-wsus"></a>Windows Server Update Services (WSUS)  
 WSUS es necesario para la sincronización de las actualizaciones de software y para el análisis de evaluación del cumplimiento de las actualizaciones de software en los clientes. El servidor WSUS debe instalarse antes de crear el rol de sistema de sitio de punto de actualización de software. Se admiten las siguientes versiones de WSUS para un punto de actualización de software:  

-   WSUS 4 (rol de Windows Server 2012 y Windows Server 2012 R2)  

-   WSUS 3.2 (rol de Windows Server 2008 R2)  

 Si hay varios puntos de actualización de software en un sitio, asegúrese de que ejecutan la misma versión de WSUS.  

> [!WARNING]  
>  La clasificación de actualizaciones de software **Actualizaciones** solo se admite a partir de WSUS 4.0. Antes de sincronizar esta nueva clasificación y poder evaluar los equipos con Windows 10 en un plan de mantenimiento de Windows 10, es fundamental que instale la [revisión 3095113](https://support.microsoft.com/kb/3095113) para WSUS en sus servidores de sitio y puntos de actualización de software. Esta revisión permite a WSUS en un servidor basado en Windows Server 2012 o en Windows Server 2012 R2 sincronizar y distribuir actualizaciones de características para Windows 10. Para obtener más información, consulte [Manage Windows as a service](../../osd/deploy-use/manage-windows-as-a-service.md) (Administrar Windows como servicio).  
>   
>  Si sincroniza las actualizaciones de software con la clasificación **Actualizaciones** antes de instalar la [revisión 3095113](https://support.microsoft.com/kb/3095113), consulte [Recover from synchronizing the Actualizaciones category before you install KB 3095113](#BKMK_RecoverUpgrades).  

### <a name="wsus-administration-console"></a>Consola de administración de WSUS  
 La consola de administración de WSUS es necesaria en el servidor de sitio de Configuration Manager si el punto de actualización de software está en un servidor de sistema de sitio remoto y WSUS no se ha instalado todavía en el servidor de sitio.  

> [!IMPORTANT]  
>  La versión de WSUS en el servidor de sitio debe ser igual a la versión de WSUS que se ejecuta en los puntos de actualización de software.  

> [!IMPORTANT]  
>  No use la consola de administración de WSUS para configurar opciones de WSUS. Configuration Manager se conecta a la instancia de WSUS que se ejecuta en el punto de actualización de software y configura las opciones adecuadas.  

### <a name="windows-update-agent-wua"></a>Agente de Windows Update (WUA)  
 El cliente de WUA es necesario en los clientes para que puedan conectarse al servidor WSUS y recuperar la lista de actualizaciones de software cuyo cumplimiento debe analizarse.  

 Al instalar Configuration Manager, se descarga la versión más reciente de WUA. Después, cuando se instala el cliente de Configuration Manager, WUA se actualizará si es necesario. Sin embargo, si se produce un error en la instalación, debe usar otro método para actualizar WUA.  

## <a name="software-update-dependencies-internal-to-configuration-manager"></a>Dependencias internas de actualizaciones de software de Configuration Manager  
 En las secciones siguientes se incluyen las dependencias internas para las actualizaciones de software en Configuration Manager.  

### <a name="management-points"></a>Puntos de administración  
 Los puntos de administración transfieren información entre los equipos cliente y el sitio de Configuration Manager. Son necesarios para las actualizaciones de software.  

### <a name="software-update-point"></a>Punto de actualización de software  
 Debe instalar un punto de actualización de software en el servidor de WSUS para poder implementar las actualizaciones de software en Configuration Manager. Para obtener más información, consulte [Install and configure a software update point](../get-started/install-a-software-update-point.md) (Instalar y configurar un punto de actualización de software).

### <a name="distribution-points"></a>Puntos de distribución  
 Los puntos de distribución son necesarios para almacenar el contenido de las actualizaciones de software. Para obtener más información sobre cómo instalar puntos de distribución y administrar contenido, consulte [Manage content and content infrastructure](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md) (Administrar el contenido y la infraestructura de contenido).  

### <a name="client-settings-for-software-updates"></a>Configuración de cliente para las actualizaciones de software  
 De forma predeterminada, las actualizaciones de software están habilitadas para los clientes. Sin embargo, hay otras opciones disponibles que controlan cómo y cuándo los clientes evalúan el cumplimiento de las actualizaciones de software y controlan cómo se instalan.  

 Para obtener más información, consulte:  

-   La sección [Configuración de cliente para las actualizaciones de software](../get-started/manage-settings-for-software-updates.md#BKMK_ClientSettings)   

-   El tema sobre la [configuración de cliente para las actualizaciones de software](../../core/clients/deploy/about-client-settings.md#software-updates)  

### <a name="reporting-services-point"></a>Puede configurar otras fuentes de actualización opcionales si crea una directiva antimalware.  
 El rol de sistema de sitio de punto de servicios de informes puede mostrar informes de las actualizaciones de software. Este rol es opcional pero se recomienda. Para obtener más información sobre cómo crear un punto de servicios de informes, consulte [Configuring reporting](../../core/servers/manage/configuring-reporting.md) (Configurar los informes).  

##  <a name="BKMK_RecoverUpgrades"></a> Recuperación de la sincronización de la categoría Actualizaciones antes de instalar KB 3095113  
 Debe instalar la [revisión 3095113](https://support.microsoft.com/kb/3095113) para WSUS en los puntos de actualización de software y en los servidores de sitio antes de sincronizar la clasificación **Actualizaciones** . Si la revisión no está instalada cuando se habilita la clasificación **Actualizaciones** , WSUS verá la actualización de características de la compilación 1511 de Windows 10 aunque no pueda descargar e implementar correctamente los paquetes asociados. Si sincroniza las actualizaciones sin haber instalado primero la [revisión 3095113](https://support.microsoft.com/kb/3095113), la base de datos de WSUS (SUSDB) se rellenará con datos inutilizables que se deben borrar para poder implementar correctamente las actualizaciones.  Utilice el siguiente procedimiento para recuperarse de este problema.  

#### <a name="to-recover-from-synchronizing-the-upgrades-classification-before-you-install-kb-3095113"></a>Para recuperarse de la sincronización de la clasificación Actualizaciones antes de instalar KB 3095113  

1.  Elimine las actualizaciones de software con la clasificación Actualizaciones. Puede usar un script de PowerShell similar al siguiente script de ejemplo:  

    ```  
    $Server = Get-WSUSServer  
    $Config = $Server.GetConfiguration()  
    $Update10563 = “df4e45a3-946d-4467-b3fd-8621174bb666”  
    $UpdateGUID = New-Object Guid($Update10563)  
    $Server.DeleteUpdate($UpdateGUID)  
    ```  

    > [!IMPORTANT]  
    >  Debe ejecutar el script en todos los puntos de actualización de software en su jerarquía de Configuration Manager antes de ir al paso siguiente.  

     Para eliminar las actualizaciones de software con la clasificación Actualizaciones de forma masiva, puede modificar el script de PowerShell para leer varios GUID desde un archivo txt.  

2.  Desactive la clasificación **Actualizaciones** en las propiedades del componente de punto de actualización de software (para obtener información detallada, consulte [Configure classifications and products](../get-started/configure-classifications-and-products.md) [Configurar las clasificaciones y los productos]) y, luego, inicie la sincronización de las actualizaciones de software (para obtener información detallada, consulte [Synchronize software updates](../get-started/synchronize-software-updates.md) [Sincronizar las actualizaciones de software]).  

3.  Instale la [revisión 3095113](https://support.microsoft.com/kb/3095113) para WSUS en sus servidores de sitio y puntos de actualización de software.  

4.  Seleccione la clasificación **Actualizaciones** en las propiedades del componente de punto de actualización de software (para obtener información detallada, consulte [Configure classifications and products](../get-started/configure-classifications-and-products.md) [Configurar las clasificaciones y los productos]) y, luego, inicie la sincronización de las actualizaciones de software (para obtener información detallada, consulte [Synchronize software updates](../get-started/synchronize-software-updates.md) [Sincronizar las actualizaciones de software]).  

## <a name="next-steps"></a>Pasos siguientes
[Preparar la administración de actualizaciones de software](../get-started/prepare-for-software-updates-management.md)
