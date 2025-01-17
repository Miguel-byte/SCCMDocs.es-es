---
title: Requisitos de acceso a Internet
titleSuffix: Configuration Manager
description: Obtenga información sobre los puntos de conexión de Internet para permitir la funcionalidad completa de las características de Configuration Manager.
ms.date: 08/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: b34fe701-5d05-42be-b965-e3dccc9363ca
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 11241176abade1233a6fbdbe2ee3bdd0e3219e48
ms.sourcegitcommit: b28a97e22a9a56c5ce3367c750ea2bb4d50449c3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2019
ms.locfileid: "70243589"
---
# <a name="internet-access-requirements"></a>Requisitos de acceso a Internet

Algunas características de Configuration Manager se basan en la conectividad de Internet para obtener la funcionalidad completa. Si la organización restringe la comunicación de red con Internet mediante un dispositivo proxy o firewall, asegúrese de permitir estos puntos de conexión.

<!-- SCCMDocs-pr #3403 -->

## <a name="bkmk_scp"></a> Punto de conexión de servicio

Estas configuraciones se aplican al equipo que hospeda el punto de conexión de servicio y cualquier firewall que haya entre ese equipo e Internet. Ambos deben permitir las comunicaciones a través de los puertos de salida **TCP 443** para HTTPS y **TCP 80** para HTTP a las ubicaciones de Internet siguientes.

El punto de conexión de servicio admite el uso de un proxy web (con o sin autenticación) para usar estas ubicaciones. Para obtener más información, vea [Compatibilidad de servidor proxy](/sccm/core/plan-design/network/proxy-server-support).

Para más información sobre el punto de conexión de servicio, consulte [Acerca del punto de conexión de servicio](/sccm/core/servers/deploy/configure/about-the-service-connection-point).

Otras características de Configuration Manager pueden requerir puntos de conexión adicionales del punto de conexión de servicio. Para más información, consulte las demás secciones de este artículo:

> [!TIP]  
> El punto de conexión de servicio usa el servicio de Microsoft Intune cuando se conecta a `go.microsoft.com` o `manage.microsoft.com`. Hay un problema conocido por el que el conector de Intune experimenta problemas de conectividad si no está instalado el certificado raíz de Baltimore CyberTrust, si ha expirado o si está dañado en el punto de conexión de servicio. Para más información, consulte [KB 3187516: Service connection point doesn't download updates](https://support.microsoft.com/help/3187516) (El punto de conexión de servicio no descarga las actualizaciones).  

### <a name="a-namebkmk_scp-updates-updates-and-servicing"></a><a name="bkmk_scp-updates"/> Actualizaciones y mantenimiento

Para más información sobre esta función, consulte [Actualizaciones y servicio para Configuration Manager](/sccm/core/servers/manage/updates).

> [!Tip]  
> Habilite estos puntos de conexión para la regla de [conclusiones de administración](/sccm/core/servers/manage/management-insights), **Connect the site to the Microsoft cloud for Configuration Manager updates** (Conectar el sitio a la nube de Microsoft para obtener las actualizaciones de Configuration Manager).

- `*.akamaiedge.net`  

- `*.akamaitechnologies.com`  

- `*.manage.microsoft.com`  

- `go.microsoft.com`  

- `*.blob.core.windows.net`  

- `download.microsoft.com`  

- `download.windowsupdate.com`  

- `sccmconnected-a01.cloudapp.net`  

- `configmgrbits.azureedge.net`  

### <a name="microsoft-intune"></a>Microsoft Intune

Para más información sobre esta función, consulte [MDM híbrida con Configuration Manager y Microsoft Intune](/sccm/mdm/understand/hybrid-mobile-device-management).

- `*manage.microsoft.com`  

- `https://bspmts.mp.microsoft.com/V`  

- `https://login.microsoftonline.com/{TenantID}`  

### <a name="windows-10-servicing"></a>Servicio de actualización de Windows 10

Para más información sobre esta función, consulte [Administración de Windows como servicio](/sccm/osd/deploy-use/manage-windows-as-a-service).

- `download.microsoft.com`  

- `https://go.microsoft.com/fwlink/?LinkID=619849`  

- `dl.delivery.mp.microsoft.com`  

### <a name="azure-services"></a>Servicios de Azure

Para más información sobre esta función, consulte [Configuración de servicios de Azure para utilizarlos con Configuration Manager](/sccm/core/servers/deploy/configure/azure-services-wizard).

- `management.azure.com`  


## <a name="co-management"></a>Administración conjunta

Si inscribe dispositivos de Windows 10 en Microsoft Intune para realizar una administración conjunta, asegúrese de que esos dispositivos puedan acceder a los puntos de conexión que Intune requiere. Para más información, consulte [Puntos de conexión de red de Microsoft Intune](https://docs.microsoft.com/intune/intune-endpoints).


## <a name="microsoft-store-for-business"></a>Microsoft Store para Empresas

Si integra Configuration Manager con [Microsoft Store para Empresas](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business), asegúrese de que el punto de conexión de servicio y los dispositivos de destino puedan acceder al servicio en la nube. Para más información, consulte [Configuración del proxy de Microsoft Store para Empresas](https://docs.microsoft.com/microsoft-store/prerequisites-microsoft-store-for-business#proxy-configuration).


## <a name="bkmk_cloud"></a> Servicios en la nube

<!-- SCCMDocs-pr #3402 -->

En esta sección se tratan las características siguientes:

- Cloud Management Gateway (CMG)
- Punto de distribución de nube (CDP)
- Integración de Azure Active Directory (Azure AD)
- Detección basada en Azure AD

Para implementar el servicio de CMG/CDP, el **punto de conexión de servicio** necesita acceso a:

- Los puntos de conexión específicos de Azure son diferentes para cada entorno, en función de la configuración. Configuration Manager almacena estos puntos de conexión en la base de datos del sitio. Consulte la tabla **AzureEnvironments** de SQL Server para obtener la lista de puntos de conexión de Azure.  

El **punto de conexión de CMG** necesita acceso a los puntos de conexión de servicio siguientes:

- ServiceManagementEndpoint: `https://management.core.windows.net/`  

- StorageEndpoint: `blob.core.windows.net` y `table.core.windows.net`

Para recuperar el token de Azure AD mediante el **cliente** y la **consola de Configuration Manager**:

- ActiveDirectoryEndpoint `https://login.microsoftonline.com/`  

Para la detección del usuario de Azure AD, el **punto de conexión de servicio** necesita acceso a:

- Versión 1810 y anteriores: Punto de conexión de Azure AD Graph `https://graph.windows.net/`  

- Versión 1902 y posteriores: Punto de conexión de Microsoft Graph `https://graph.microsoft.com/`

El sistema de sitio del punto de conexión de Cloud Management Gateway (CMG) admite el uso de un proxy web. Para obtener más información sobre cómo configurar este rol para un proxy, vea [Compatibilidad de servidor proxy](proxy-server-support.md#configure-the-proxy-for-a-site-system-server). El punto de conexión de CMG solo necesita conectarse a los puntos de conexión de servicio de CMG. No necesita acceso a otros puntos de conexión de Azure.

Para más información sobre CMG, consulte [Planear para Cloud Management Gateway](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway).


## <a name="bkmk_sum"></a> Actualizaciones de software

Permita que el punto de actualización de software activo acceda a los puntos de conexión siguientes para que WSUS y las actualizaciones automáticas se puedan comunicar con el servicio en la nube de Microsoft Update:  

- `http://windowsupdate.microsoft.com`  

- `http://*.windowsupdate.microsoft.com`  

- `https://*.windowsupdate.microsoft.com`  

- `http://*.update.microsoft.com`  

- `https://*.update.microsoft.com`  

- `http://*.windowsupdate.com`  

- `http://download.windowsupdate.com`  

- `http://download.microsoft.com`  

- `http://*.download.windowsupdate.com`  

- `http://test.stats.update.microsoft.com`  

- `http://ntservicepack.microsoft.com`  

Para más información sobre las actualizaciones de software, consulte [Planear las actualizaciones de software](/sccm/sum/plan-design/plan-for-software-updates).

### <a name="intranet-firewall"></a>Firewall de intranet

Es posible que tenga que agregar puntos de conexión a un firewall que se encuentra entre dos sistemas de sitio en los casos siguientes:

- Si los sitios secundarios tienen un punto de actualización de software
- Si hay un punto de actualización de software basado en Internet activo remoto en un sitio

#### <a name="software-update-point-on-the-child-site"></a>Punto de actualización de software del sitio secundario

- `http://<FQDN for software update point on child site>`  

- `https://<FQDN for software update point on child site>`  

- `http://<FQDN for software update point on parent site>`  

- `https://<FQDN for software update point on parent site>`  


## <a name="manage-office-365"></a>Administrar Office 365

Si usa Configuration Manager para implementar y actualizar Office 365, permita los siguientes puntos de conexión:

<!-- SCCMDocs#929 -->

- `officecdn.microsoft.com` para sincronizar el punto de actualización de software para las actualizaciones de cliente de Office 365

- `config.office.com` para crear configuraciones personalizadas para las implementaciones de Office 365


## <a name="configuration-manager-console"></a>Consola de Configuration Manager

Los equipos con la consola de Configuration Manager requieren acceso a los puntos de conexión de Internet siguientes para características específicas:

### <a name="in-console-feedback"></a>Comentarios en la consola

- `http://petrol.office.microsoft.com`

Para más información sobre esta característica, consulte [Comentarios sobre el producto](/sccm/core/understand/find-help#product-feedback).

### <a name="community-workspace-documentation-node"></a>Área de trabajo Comunidad, nodo Documentación

- `https://aka.ms`

- `https://raw.githubusercontent.com`

Para más información sobre este nodo de la consola, consulte [Uso de la consola de Configuration Manager](/sccm/core/servers/manage/admin-console).

<!-- 
Community Hub
when in current branch, get details from SCCMDocs-pr #3403 
 -->

### <a name="monitoring-workspace-site-hierarchy-node"></a>Área de trabajo Supervisión, nodo Jerarquía de sitios

Si usa la **vista geográfica**, permita el acceso al punto de conexión siguiente:

- `http://maps.bing.com`


## <a name="desktop-analytics"></a>Análisis de escritorio

Para más información sobre los puntos de conexión requeridos para el servicio en la nube Análisis de escritorio, consulte [Habilitación del uso compartido de datos](/sccm/desktop-analytics/enable-data-sharing#endpoints).


## <a name="microsoft-public-ip-addresses"></a>Direcciones IP públicas de Microsoft

Para más información sobre los intervalos de direcciones IP de Microsoft, consulte [Microsoft Public IP Space](https://www.microsoft.com/download/details.aspx?id=53602) (Espacio de direcciones IP públicas de Microsoft). Estas direcciones se actualizan periódicamente. No hay granularidad por servicio, por lo que se podría usar cualquier dirección IP dentro de estos intervalos.


## <a name="see-also"></a>Consulte también

- [Puertos usados en Configuration Manager](/sccm/core/plan-design/hierarchy/ports)

- [Compatibilidad con servidores proxy en Configuration Manager](/sccm/core/plan-design/network/proxy-server-support)
