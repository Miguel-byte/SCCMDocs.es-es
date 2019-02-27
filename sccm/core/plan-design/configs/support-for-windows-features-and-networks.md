---
title: Compatibilidad con características de Windows
titleSuffix: Configuration Manager
description: Obtenga información sobre las características de redes y Windows que admite Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 0cf4bacb-6b6d-4d4f-8640-b13fe15873de
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: ae1ac3262acff35e23de4faa1e80c796f5ee4e4b
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56156702"
---
# <a name="support-for-windows-features-and-networks-in-configuration-manager"></a>Compatibilidad con las características y redes de Windows en Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

En este artículo se identifica la compatibilidad de Configuration Manager con características de red y Windows comunes.  



##  <a name="bkmk_branchcache"></a> BranchCache  

Use Windows BranchCache con Configuration Manager cuando lo habilite en los puntos de distribución y configure clientes para que lo usen en modo de caché distribuida.

Establezca la configuración de BranchCache en un tipo de implementación para aplicaciones, en la implementación de un paquete y para secuencias de tareas. A partir de la versión 1802, BranchCache está habilitado de forma predeterminada. 

Cuando se cumplen los requisitos de BranchCache, esta característica permite a los clientes de ubicaciones remotas obtener el contenido de los clientes locales que tienen una memoria caché actual del contenido.  

Por ejemplo, cuando el primer cliente habilitado para BranchCache solicita contenido de un punto de distribución que se ha configurado como un servidor de BranchCache, el cliente descarga y almacena el contenido en la caché. Después, este contenido estará disponible para los clientes en la misma subred que ha solicitado este contenido.

Estos clientes también almacenan en caché el contenido. Otros clientes en la misma subred no tendrán que descargar el contenido desde el punto de distribución. El contenido se distribuye entre varios clientes para futuras transferencias.  


### <a name="requirements-to-support-branchcache-with-configuration-manager"></a>Requisitos para admitir BranchCache con Configuration Manager

#### <a name="configure-distribution-points"></a>Configurar puntos de distribución
Agregue la característica **Windows BranchCache** al servidor del sistema de sitio que está configurado como punto de distribución.    
- Los puntos de distribución en los servidores que se configuran para admitir BranchCache no requieren ninguna configuración adicional.   
- No se puede agregar Windows BranchCache a un punto de distribución basado en la nube. Los puntos de distribución basados en la nube admiten la descarga de contenido por parte de clientes configurados para Windows BranchCache.  

#### <a name="configure-clients"></a>Configurar clientes    
- Los clientes que pueden admitir BranchCache deben configurarse para el modo Caché distribuida de BranchCache.  
- La opción de sistema operativo de la configuración del cliente de BITS debe estar habilitada para admitir BranchCache.  

Para obtener información, vea [Configurar clientes de BranchCache](https://docs.microsoft.com/windows/deployment/update/waas-branchcache#configure-clients-for-branchcache) en la documentación de Windows.


### <a name="configuration-manager-supported-os-versions-with-windows-branchcache"></a>Versiones de sistema operativo con Windows BranchCache compatibles con Configuration Manager

|Sistema&nbsp;operativo|Detalles sobre compatibilidad|  
|----------------------|---------------------|  
|Windows 7 con SP1|Compatible de forma predeterminada|  
|Windows 8|Compatible de forma predeterminada|  
|Windows 8.1|Compatible de forma predeterminada|  
|Windows 10|Compatible de forma predeterminada|  
|Windows Server 2008 con SP2|**Requiere BITS 4.0**: instale la versión 4.0 de BITS en los clientes de Configuration Manager mediante la distribución de software o actualizaciones de software. Para obtener más información, vea [Windows Management Framework](https://support.microsoft.com/help/968929/windows-management-framework-windows-powershell-2-0-winrm-2-0-and-bits).<br /><br /> En este sistema operativo, la funcionalidad de cliente de BranchCache no es compatible con la distribución de software que se ejecuta desde la red ni con las transferencias de archivos SMB. Además, este sistema operativo no puede usar la funcionalidad de BranchCache con puntos de distribución basados en la nube.|  
|Windows Server 2008 R2|Compatible de forma predeterminada|  
|Windows Server 2012|Compatible de forma predeterminada|  
|Windows Server 2012 R2|Compatible de forma predeterminada|  
|Windows Server 2016|Compatible de forma predeterminada|  

Para obtener más información, vea [BranchCache para Windows](https://docs.microsoft.com/windows-server/networking/branchcache/branchcache) en la documentación de Windows Server.  



##  <a name="bkmk_Workgroups"></a> Equipos en grupos de trabajo  

Configuration Manager ofrece compatibilidad con clientes en grupos de trabajo.  

- Configuration Manager permite mover un cliente de un grupo de trabajo a un dominio o de un dominio a un grupo de trabajo. Para obtener más información, vea [Cómo instalar clientes de Configuration Manager en equipos del grupo de trabajo](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientWorkgroup).  

> [!NOTE]  
>  Aunque se admiten clientes de grupos de trabajo, todos los sistemas de sitio deben ser miembros de un dominio de Active Directory compatible.  



##  <a name="bkmmk_datadedup"></a> Desduplicación de datos  

Configuration Manager admite el uso de la desduplicación de datos con puntos de distribución en los siguientes sistemas operativos:  

-   Windows Server 2016
-   Windows Server 2012 R2  
-   Windows Server 2012  


> [!IMPORTANT]  
>  El volumen que hospeda los archivos de origen del paquete no se puede marcar para la desduplicación de datos. Esta limitación se debe a que la desduplicación de datos usa puntos repetición de análisis. Configuration Manager no admite el uso de una ubicación de origen de contenido con archivos almacenados en puntos de repetición de análisis.  

Para obtener más información, vea [Configuration Manager Distribution Points and Windows Server 2012 Data Deduplication](https://cloudblogs.microsoft.com/enterprisemobility/2014/02/18/configuration-manager-distribution-points-and-windows-server-2012-data-deduplication/) (Puntos de distribución de Configuration Manager y desduplicación de datos de Windows Server 2012) en el blog del equipo de Configuration Manager e [Introducción a la desduplicación de datos](https://docs.microsoft.com/windows-server/storage/data-deduplication/overview) en la documentación de Windows.  



##  <a name="bkmk_DA"></a> DirectAccess  

Configuration Manager es compatible con la característica DirectAccess para la comunicación entre clientes y sistemas de servidor de sitio.  

- Cuando se cumplen todos los requisitos de DirectAccess, habilita los clientes de Configuration Manager en Internet para comunicarse con su sitio asignado como si estuvieran en la intranet.  

- Para las acciones iniciadas por el servidor, como el control remoto y la instalación de inserción de cliente, el equipo iniciador debe ejecutar IPv6. Este protocolo debe ser compatible con todos los dispositivos de red que intervengan.  

Configuration Manager no admite la funcionalidad siguiente sobre DirectAccess:  

-   Implementación del sistema operativo   

-   Comunicación entre sitios de Configuration Manager  

-   Comunicación entre servidores del sistema de sitio de Configuration Manager dentro de un sitio  



##  <a name="bkmk_dualboot"></a> Equipos de arranque dual  

Configuration Manager no puede administrar más de un sistema operativo en el mismo equipo. Si hay más de un sistema operativo en un equipo para administrar, ajuste los métodos de instalación y detección de cliente del sitio para garantizar que el cliente de Configuration Manager solo se instala en el sistema operativo que se debe administrar.  



##  <a name="bkmk_IPv6"></a> IPv6  

Además del protocolo de Internet versión 4 (IPv4), Configuration Manager es compatible con el protocolo de Internet versión 6 (IPv6), con las excepciones siguientes:  

|Función| Excepción para la compatibilidad con IPv6|  
|--------------|-------------------------------|  
|Puntos de distribución basados en la nube|IPv4 es necesario para admitir Microsoft Azure y los puntos de distribución basados en la nube.|  
|Puerta de enlace de administración en la nube|IPv4 es necesario para admitir Microsoft Azure y Cloud Management Gateway.|  
|Dispositivos móviles inscritos por Microsoft Intune y el conector de servicio de Microsoft|IPv4 es necesario para admitir los dispositivos móviles inscritos por Microsoft Intune y el conector de servicio de Microsoft.|  
|Detección de redes|IPv4 es necesario cuando se configura un servidor DHCP para buscar en la detección de redes.|  
|Implementación del sistema operativo|En la versión 1802 y anteriores, IPv4 es necesario para admitir la implementación del sistema operativo.  </br> </br> A partir de la versión 1806, un respondedor PXE se habilita en un punto de distribución sin Servicios de implementación de Windows. Este nuevo servicio de respondedor PXE es compatible con IPv6. Otros aspectos de la característica de implementación del sistema operativo, como la captura o la configuración de direcciones IP estáticas durante la secuencia de tareas siguen requiriendo IPv4. |  
|Comunicación del proxy de reactivación|IPv4 es necesario para admitir los paquetes del proxy de reactivación del de cliente.|  
|Windows CE|IPv4 es necesario para admitir el cliente de Configuration Manager en los dispositivos con Windows CE.|  



##  <a name="bkmk_NAT"></a> Traducción de direcciones de red  

La traducción de direcciones de red (NAT) no se admite en Configuration Manager, a menos que el sitio admita clientes que están en Internet y el cliente detecte que está conectado a Internet. Para obtener más información sobre la administración de clientes basados en Internet, vea [Planear la administración de clientes basados en Internet](/sccm/core/clients/deploy/plan/plan-for-managing-internet-based-clients).  



##  <a name="bkmk_storage"></a> Tecnología de almacenamiento especializado  

Configuration Manager funciona con cualquier hardware que esté certificado en la lista de compatibilidad de hardware de Windows para la versión del sistema operativo en el que está instalado el componente de Configuration Manager.

Los roles del servidor de sitio requieren NTFS, para que Configuration Manager pueda establecer los permisos de archivos y directorios. Configuration Manager asume que tiene la propiedad completa de una unidad lógica. Los sistemas de sitio que se ejecutan en equipos independientes no pueden compartir una partición lógica en ninguna tecnología de almacenamiento. Sin embargo, cada equipo puede usar una partición lógica separada en la misma partición física de un dispositivo de almacenamiento compartido.  

### <a name="support-considerations"></a>Consideraciones sobre la compatibilidad

- **Red de área de almacenamiento**: una red de área de almacenamiento (SAN) se admite cuando un servidor basado en Windows compatible se conecta directamente al volumen que se hospeda en la SAN.  

- **Almacenamiento de instancia única**: Configuration Manager no admite la configuración de paquetes de puntos de distribución y carpetas de firmas en un volumen habilitado para el Almacenamiento de instancia única (SIS).  

     Además, la caché de un cliente de Configuration Manager no se admite en un volumen habilitado para SIS.  

- **Unidad de disco extraíble**: Configuration Manager no admite la instalación de clientes o sistemas de sitio de Configuration Manager en una unidad de disco extraíble.  
