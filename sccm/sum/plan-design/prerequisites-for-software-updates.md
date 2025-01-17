---
title: Requisitos previos para las actualizaciones de software
titleSuffix: Configuration Manager
description: Obtenga información sobre los requisitos previos para las actualizaciones de software en System Center Configuration Manager.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 08/22/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: fdf05118-162a-411e-b72e-386b9dc9a5e1
ms.collection: M365-identity-device-management
ms.openlocfilehash: 334854072e5c724f2c76432e7a7372c02cab3d54
ms.sourcegitcommit: 13ac4f5e600dc1edf69e8566e00968f40e1d1761
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 09/11/2019
ms.locfileid: "70892256"
---
# <a name="prerequisites-for-software-updates-in-system-center-configuration-manager"></a>Requisitos previos para las actualizaciones de software en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

En este artículo se muestran los requisitos previos para las actualizaciones de software en System Center Configuration Manager. Las dependencias externas e internas de cada requisito previo se muestran en tablas independientes.  

## <a name="software-update-dependencies-that-are-external-to-configuration-manager"></a>Dependencias de actualizaciones de software externas de Configuration Manager  
 En las siguientes secciones se incluyen las dependencias externas para las actualizaciones de software.  

### <a name="internet-information-services"></a>Internet Information Services  
 Internet Information Services (IIS) debe estar instalado en los servidores de sistema de sitio para poder ejecutar el punto de actualización de software, el punto de administración y el punto de distribución. Para obtener más información, consulte [Prerequisites for site system roles](../../core/plan-design/configs/site-and-site-system-prerequisites.md) (Requisitos previos de los roles de sistema de sitio).  

### <a name="windows-server-update-services"></a>Windows Server Update Services  
 Windows Server Update Services (WSUS) es necesario para la sincronización de las actualizaciones de software y para el análisis de la aplicabilidad de las actualizaciones de software en los clientes. El servidor WSUS debe instalarse antes de crear el rol de punto de actualización de software. Se admiten las siguientes versiones de WSUS para un punto de actualización de software:  

- WSUS 10.0.14393 (rol de Windows Server 2016)
- WSUS 10.0.17763 (rol de Windows Server 2019) (requiere Configuration Manager 1810 o posterior)
- WSUS 6.2 y 6.3 (rol de Windows Server 2012 y Windows Server 2012 R2)
  - [Kb 3095113 y kb 3159706 (o una actualización equivalente)](#BKMK_wsus2012) son necesarios para WSUS 6,2 y 6,3 Si implementa actualizaciones de Windows 10.

> [!NOTE]
> - A partir de la versión 1702, Windows Server 2008 R2 no es compatible con el rol del punto de actualización de software. Para obtener más información, vea [Sistemas operativos compatibles con servidores de sistema de sitio](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers#bkmk_2008r2sp1).
> - Si hay varios puntos de actualización de software en un sitio, asegúrese de que todos ejecutan la misma versión de WSUS.

### <a name="wsus-administration-console"></a>Consola de administración de WSUS  
La consola de administración de WSUS es necesaria en el servidor de sitio de Configuration Manager si el punto de actualización de software está en un servidor de sistema de sitio remoto y WSUS no se ha instalado todavía en el servidor de sitio.  

> [!IMPORTANT]  
> - La versión de WSUS en el servidor de sitio debe ser igual a la versión de WSUS que se ejecuta en los puntos de actualización de software.
> - No use la consola de administración de WSUS para configurar opciones de WSUS. Configuration Manager se conecta a la instancia de WSUS que se ejecuta en el punto de actualización de software y configura las opciones adecuadas.  


### <a name="windows-update-agent"></a>Agente de Windows Update  
 El cliente de Agente de Windows Update (WUA) es necesario para que los clientes puedan conectarse al servidor de WSUS. WUA recupera la lista de actualizaciones de software cuyo cumplimiento debe analizarse.  

 Al instalar Configuration Manager, se descarga la versión más reciente de WUA. Después, cuando se instala el cliente de Configuration Manager, WUA se actualizará si es necesario. Si se produce un error en la instalación, debe usar otro método para actualizar WUA.  

## <a name="software-update-dependencies-that-are-internal-to-configuration-manager"></a>Dependencias de actualizaciones de software internas de Configuration Manager  
 En las secciones siguientes se incluyen las dependencias internas para las actualizaciones de software en Configuration Manager.  

### <a name="management-points"></a>Puntos de administración  
 Los puntos de administración transfieren información entre los equipos cliente y el sitio de Configuration Manager. Los puntos de administración son necesarios para las actualizaciones de software.  

### <a name="software-update-points"></a>Puntos de actualización de software  
 Debe instalar un punto de actualización de software en el servidor de WSUS para implementar las actualizaciones de software en Configuration Manager. Para obtener más información, consulte [Install and configure a software update point](../get-started/install-a-software-update-point.md) (Instalar y configurar un punto de actualización de software).

### <a name="distribution-points"></a>Puntos de distribución  
 Los puntos de distribución son necesarios para almacenar el contenido de las actualizaciones de software. Para obtener más información sobre cómo instalar puntos de distribución y administrar contenido, consulte [Manage content and content infrastructure](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md) (Administrar el contenido y la infraestructura de contenido).  

### <a name="client-settings-for-software-updates"></a>Configuración de cliente para las actualizaciones de software  
Las actualizaciones de software están habilitadas para los clientes de forma predeterminada. Hay otras opciones disponibles que controlan cómo y cuándo los clientes evalúan el cumplimiento de las actualizaciones de software y controlan cómo se instalan.  

 Vea los siguientes artículos para más información:  

- [Configuración de cliente para las actualizaciones de software](../get-started/manage-settings-for-software-updates.md#BKMK_ClientSettings)   

- [Configuración de cliente para las actualizaciones de software](../../core/clients/deploy/about-client-settings.md#software-updates)  

### <a name="reporting-services-points"></a>Puntos de servicios de informes  
 El rol de sistema de sitio de punto de servicios de informes puede mostrar informes de las actualizaciones de software. Este rol es opcional pero se recomienda. Para más información sobre cómo crear un punto de servicios de informes, vea [Configuración de informes](../../core/servers/manage/configuring-reporting.md).  

## <a name="BKMK_wsus2012"></a>¿Qué actualizaciones son necesarias en WSUS 6,2 y 6,3?

Se necesitan dos actualizaciones para la sincronización de **actualizaciones** de la clasificación en WSUS 6,2 y 6,3. En ocasiones, es posible que vea un error al descargar o implementar las actualizaciones si se sincronizaron antes de instalar KB3095113 y KB3159706. En la sección siguiente se puede ver información sobre los posibles problemas.  

- Debe instalar [KB 3095113](https://support.microsoft.com/kb/3095113), que se publicó en octubre de 2015, en los puntos de actualización de software y en los servidores de sitio antes de sincronizar la clasificación **Actualizaciones**.
  - Esta actualización habilita la clasificación **actualizaciones** .
- Para atender a la versión 1607 de Windows 10 y versiones posteriores, debe instalar y configurar [KB 3159706](https://support.microsoft.com/en-us/help/3159706). KB 3159706 se lanzó en mayo de 2016.
  - Esta actualización permite a WSUS descifrar de forma nativa los archivos que se usan para actualizar Windows 10, versión 1607 y versiones posteriores.

>[!IMPORTANT]
> Los KB 3095113 y KB 3159706 se incluyen en el **paquete acumulativo de calidad mensual de seguridad** a partir del 2017 de julio. Esto significa que es posible que no vea KB 3095113 y KB 3159706 como actualizaciones instaladas, ya que es posible que se hayan instalado con un resumen. Sin embargo, si necesita alguna de estas actualizaciones, se recomienda instalar un **paquete acumulativo de calidad mensual de seguridad** publicado después del 2017 de octubre, ya que contienen una actualización de WSUS adicional para reducir el uso de memoria en CLIENTWEBSERVICE de WSUS.

## <a name="BKMK_RecoverUpgrades"></a>La descarga de actualizaciones de Windows 10 produce un error con el mensaje "error: firma de certificado no válida" o 0xc1800118

Las actualizaciones y el problema descritos en esta sección solo se aplican a WSUS que se ejecuta en máquinas con Windows Server 2012 o Windows Server 2012 R2 (WSUS 6,2 y 6,3). Normalmente, solo verá los problemas descritos en esta sección Si instaló WSUS antes del 2017 de julio y ha habilitado recientemente la clasificación de **actualizaciones** . Sin embargo, también es posible ver estos problemas en otras situaciones.

### <a name="historical-information-about-kb-3095113"></a>Información histórica sobre KB 3095113

 [KB 3095113](https://support.microsoft.com/kb/3095113) se [publicó como una revisión en el](https://blogs.technet.microsoft.com/wsus/2015/12/03/important-update-for-wsus-4-0-kb-3095113/) 2015 de octubre para agregar compatibilidad con las actualizaciones de Windows 10 a WSUS. La actualización permite a WSUS sincronizar y distribuir actualizaciones en la clasificación de **actualizaciones** para Windows 10.

Si sincroniza las actualizaciones sin haber instalado primero [KB 3095113](https://support.microsoft.com/kb/3095113), la base de datos de WSUS (SUSDB) se rellenará con datos inutilizables. Esos datos deben borrarse para que las actualizaciones se puedan implementar correctamente. Las actualizaciones de Windows 10 en este estado no se pueden descargar mediante el Asistente para descargar actualizaciones de software.

Los errores similares a los siguientes aparecen en la página finalización del Asistente para descargar actualizaciones de software:

``` Output
Error: Upgrade to Windows 10 Pro, version 1511, 10586
Failed to download content id {content_id}. Error: Invalid certificate signature
```

Además, los errores similares al siguiente se registran en el archivo PatchDownloader. log:

``` Log
Download http://wsus.ds.b1.download.windowsupdate.com/d/upgr/2015/12/10586.0.151029-1700.th2_release_...esd...
Authentication of file C:\Users\{username}\AppData\Local\Temp\2\{temporary_filename}.tmp failed, error 0x800b0004
ERROR: DownloadContentFiles() failed with hr=0x80073633
# This log is truncated for readability.
```

Históricamente, cuando se produjeron estos errores, se resolverían mediante una versión modificada de los [pasos de resolución para WSUS](https://blogs.technet.microsoft.com/wsus/2016/01/29/how-to-delete-upgrades-in-wsus/). Dado que estos pasos son similares a la resolución para no realizar los pasos manuales necesarios después de la instalación de KB 3159706, hemos combinado ambos conjuntos de pasos en una única solución de la sección siguiente:

- [Recuperación de la sincronización de actualizaciones antes de instalar KB 3095113 o KB 3159706](#bkmk_fix-upgrades)

### <a name="historical-information-about-kb-3159706"></a>Información histórica sobre KB 3159706

KB 3148812 se publicó inicialmente en abril de 2016 para permitir que WSUS Descifre de forma nativa los archivos. ESD usados para actualizar paquetes de Windows 10. [Kb 3148812 causó problemas para algunos clientes](https://blogs.technet.microsoft.com/wsus/2016/05/05/the-long-term-fix-for-kb3148812-issues/) y se sustituyó por [KB 3159706](https://support.microsoft.com/en-us/help/3159706). KB 3159706 debe instalarse en todos los puntos de actualización de software y servidores de sitio para poder atender a los dispositivos Windows 10 versión 1607 y posteriores. Sin embargo, pueden surgir problemas si no se ha observado que la KB requiere los siguientes pasos manuales después de la instalación:

1. Desde un símbolo del sistema con privilegios elevados, ejecute `"C:\Program Files\Update Services\Tools\wsusutil.exe" postinstall /servicing`.
1. Reinicie el servicio WSUS en todos los servidores WSUS.

Si no se ha dado de hecho que KB 3159706 tenía pasos manuales después de la instalación, o que se ha sincronizado en la actualización de Windows 10 1607 antes de instalar KB 3159706, se producirían problemas al conectarse a la consola de WSUS e implementar la actualización, respectivamente. Cuando un cliente descargó el archivo de actualización, obtendría un [código de error **0xC1800118** ](https://support.microsoft.com/help/3194588/0xc1800118-error-when-you-push-windows-10-version-1607-by-using-wsus).

Dado que los pasos de resolución son similares a la resolución de la sincronización de actualizaciones antes de la instalación de KB 3095113, hemos combinado ambos conjuntos de pasos en una sola resolución en la sección siguiente.
 

### <a name="bkmk_fix-upgrades"></a> Recuperación de la sincronización de actualizaciones antes de instalar KB 3095113 o KB 3159706

Siga los pasos que se indican a continuación para resolver el error 0xc1800118 y "error: firma de certificado no válida":

1. Deshabilite la clasificación **actualizaciones** en WSUS y Configuration Manager. No desea que se produzca una sincronización hasta que se le indiquen estas instrucciones.  
   - Desactive la clasificación **Actualizaciones** en las propiedades del componente de punto de actualización de software del sitio de primer nivel.
     - Para obtener más información, vea [Configurar las clasificaciones y los productos](../get-started/configure-classifications-and-products.md).
   - Desactive la clasificación **actualizaciones** de WSUS en **productos y clasificaciones** en la [página **Opciones** ](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/manage/setting-up-update-synchronizations), o use PowerShell ISE que se ejecuta como administrador.
      ```PowerShell
      Get-WsusClassification | Where-Object -FilterScript {$_.Classification.Title -Eq “Upgrades”} | Set-WsusClassification -Disable
      ```  
     - Si comparte la base de datos de WSUS entre varios servidores WSUS, solo tiene que desactivar las **actualizaciones** una vez para cada base de datos.  
1. En cada servidor WSUS, desde un símbolo del sistema con privilegios `"C:\Program Files\Update Services\Tools\wsusutil.exe" postinstall /servicing`elevados, ejecute:. A continuación, reinicie el servicio WSUS en todos los servidores WSUS.
   -  WSUS coloca la base de datos en [modo de usuario único](https://docs.microsoft.com/sql/relational-databases/databases/set-a-database-to-single-user-mode) antes de comprobar si es necesario el mantenimiento. El servicio se ejecuta o no se ejecuta en función de los resultados de la comprobación. A continuación, la base de datos se vuelve a poner en modo multiusuario. 
   - Si comparte la base de datos de WSUS entre varios servidores WSUS, solo tiene que realizar este servicio una vez para cada base de datos.
1. Elimine todas las actualizaciones de Windows 10 de cada base de datos de WSUS mediante PowerShell ISE que se ejecuta como administrador.
   ```PowerShell
   [reflection.assembly]::LoadWithPartialName("Microsoft.UpdateServices.Administration")
   $wsus = [Microsoft.UpdateServices.Administration.AdminProxy]::GetUpdateServer();
   $wsus.GetUpdates() | Where {$_.UpdateClassificationTitle -eq 'Upgrades' -and $_.Title -match 'Windows 10'} `
   | ForEach-Object {$wsus.DeleteUpdate($_.Id.UpdateId.ToString()); Write-Host $_.Title removed}
   ```
1. Elimine los archivos de la tabla tbFile de cada una de las bases de datos de WSUS usadas por los puntos de actualización de software. En la base de datos de WSUS, ejecute los siguientes comandos desde SQL Server Management Studio:
   ```SQL
   declare @NotNeededFiles table (FileDigest binary(20) UNIQUE)
   insert into @NotNeededFiles(FileDigest) (select FileDigest from tbFile where FileName like '%.esd%'  except select FileDigest from tbFileForRevision)
   delete from tbFileOnServer where FileDigest in (select FileDigest from @NotNeededFiles)
   delete from tbFile where FileDigest in (select FileDigest from @NotNeededFiles)
   ```
1. Inicie la sincronización de las actualizaciones de software en el sitio de nivel superior de Configuration Manager y espere a que se complete. Se produce una sincronización completa porque hemos realizado un cambio en las clasificaciones Configuration Manager cuando se han quitado las **actualizaciones**. Para obtener más información, vea [Sincronizar actualizaciones de software](../get-started/synchronize-software-updates.md).
1. Active la clasificación **Actualizaciones** en las propiedades del componente de punto de actualización de software. A continuación, inicie otra sincronización de las actualizaciones de software para volver a realizar las **actualizaciones** en WSUS y Configuration Manager. No es necesario habilitar la clasificación **actualizaciones** en WSUS, ya que Configuration Manager lo hará automáticamente.
1. Si los clientes recibieron el código de error **0xC1800118** al descargar una actualización, deberá eliminar el almacén de datos usado por el agente de Windows Update. También puede que tenga que eliminar la carpeta de ~ BT oculta en el dispositivo. La próxima vez que el cliente examine, será un examen completo en el servidor WSUS en lugar de un delta. Puede usar un script de PowerShell similar al siguiente script de ejemplo:  
   ```PowerShell
   stop-service wuauserv
   remove-item -path c:\windows\softwaredistribution\datastore -recurse -force
   # If the device has a hidden ~BT folder on the c drive, delete it too by uncommenting the next line.
   # remove-item -path c:\~BT -recurse -force
   start-service wuauserv
   ```

## <a name="next-steps"></a>Pasos siguientes
[Preparar la administración de actualizaciones de software](../get-started/prepare-for-software-updates-management.md)
