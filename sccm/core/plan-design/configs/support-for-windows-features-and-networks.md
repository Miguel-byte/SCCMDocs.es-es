---
title: "Compatibilidad con las características de Windows | System Center Configuration Manager"
description: "Descubra qué características de redes y Windows admite System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0cf4bacb-6b6d-4d4f-8640-b13fe15873de
caps.latest.revision: 8
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: e20ad43d9e1e16ef11df0d48d9982db5c53226e1


---
# <a name="support-for-windows-features-and-networks-in-system-center-configuration-manager"></a>Compatibilidad con las características y redes de Windows en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Este tema identifica la compatibilidad de System Center Configuration Manager con las características de red y Windows comunes.  


##  <a name="a-namebkmkbranchcachea-branchcache"></a><a name="bkmk_branchcache"></a> BranchCache  
Windows BranchCache está integrado en Configuration Manager. Puede establecer la configuración de BranchCache en un tipo de implementación para aplicaciones, en la implementación de un paquete y para secuencias de tareas.  

Cuando se cumplen todos los requisitos de BranchCache, esta característica permite a los clientes de ubicaciones remotas obtener el contenido de los clientes locales que tienen una memoria caché actual del contenido.  

Por ejemplo, cuando el primer equipo cliente habilitado para BranchCache solicita contenido desde un punto de distribución que se configuró como un servidor de BranchCache, el equipo cliente descarga y almacena el contenido en la memoria caché. Este contenido está disponible entonces para los clientes de la misma subred que solicitan el mismo contenido. Estos clientes también almacenan el contenido en la memoria caché. De esta manera, los siguientes clientes de la misma subred no tienen que descargar contenido desde el punto de distribución, y el contenido se distribuye por varios clientes en las siguientes transferencias.  

**Para admitir BranchCache con Configuration Manager:**  

-   Agregue la característica **Windows BranchCache** en el servidor del sistema de sitio que está configurado como punto de distribución.  

    -   Los puntos de distribución en los servidores configurados para admitir BranchCache no requieren ninguna configuración adicional.  

    -   No puede agregar Windows BranchCache a un punto de distribución basado en la nube, pero los puntos de distribución basados en la nube permiten que los clientes configurados para Windows BranchCache descarguen contenido.  

**Para habilitar los clientes para que usen BranchCache:**  

-   Los clientes que pueden admitir BranchCache deben configurarse para el modo distribuido de BranchCache.  

-   La opción de sistema operativo de la configuración del cliente de BITS debe estar habilitada para admitir BranchCache.  

**Los siguientes sistemas operativos de cliente son compatibles con Windows BranchCache:**  

|Sistema operativo|Detalles sobre compatibilidad|  
|----------------------|---------------------|  
|Windows 7 con SP1|Compatible de forma predeterminada|  
|Windows 8|Compatible de forma predeterminada|  
|Windows 8.1|Compatible de forma predeterminada|  
|Windows 10|Compatible de forma predeterminada|  
|Windows Server 2008 con SP2|**Requiere BITS 4.0**: puede instalar la versión 4.0 de BITS en los clientes de Configuration Manager mediante la distribución de software o actualizaciones de software. Para obtener más información sobre la versión 4.0 de BITS, vea [Windows Management Framework](http://go.microsoft.com/fwlink/p/?LinkId=181979).<br /><br /> En este sistema operativo, la funcionalidad de cliente de BranchCache no es compatible con la distribución de software que se ejecuta desde la red ni con las transferencias de archivos SMB. Además, este sistema operativo no puede usar la funcionalidad de BranchCache con puntos de distribución basados en la nube.|  
|Windows Server 2008 R2|Compatible de forma predeterminada|  
|Windows Server 2012|Compatible de forma predeterminada|  
|Windows Server 2012 R2|Compatible de forma predeterminada|  

 Para obtener más información sobre BranchCache, vea [BranchCache para Windows](http://go.microsoft.com/fwlink/p/?LinkId=177945) en la documentación de Windows Server.  

##  <a name="a-namebkmkworkgroupsa-computers-in-workgroups"></a><a name="bkmk_Workgroups"></a> Equipos en grupos de trabajo  
Configuration Manager ofrece compatibilidad con clientes en grupos de trabajo.  

-   Configuration Manager permite mover un cliente de un grupo de trabajo a un dominio o de un dominio a un grupo de trabajo. Para obtener más información, consulte la sección [Instalación de clientes de Configuration Manager en equipos de grupo de trabajo](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientWorkgroup) en el tema [Implementar clientes en equipos Windows con System Center Configuration Manager](../../../core/clients/deploy/deploy-clients-to-windows-computers.md).  

> [!NOTE]  
>  Aunque se admiten clientes de grupos de trabajo, todos los sistemas de sitio deben ser miembros de un dominio de Active Directory compatible.  


##  <a name="a-namebkmmkdatadedupa-data-deduplication"></a><a name="bkmmk_datadedup"></a> Desduplicación de datos  
Configuration Manager admite el uso de la desduplicación de datos con puntos de distribución en los siguientes sistemas operativos:  

-   Windows Server 2012  

-   Windows Server 2012 R2  

> [!IMPORTANT]  
>  No se puede marcar para la desduplicación de datos el volumen que hospeda archivos de origen del paquete. Esto se debe a que la desduplicación de datos usa puntos de repetición de análisis y Configuration Manager no admite el uso de una ubicación de origen de contenido con archivos almacenados en los puntos de repetición de análisis.  

Para obtener más información, consulte [Configuration Manager Distribution Points and Windows Server 2012 Data Deduplication](http://blogs.technet.com/b/configmgrteam/archive/2014/02/18/configuration-manager-distribution-points-and-windows-server-2012-data-deduplication.aspx) (Puntos de distribución de Configuration Manager y desduplicación de datos de Windows Server 2012) en el blog del equipo de Configuration Manager e [Introducción a la desduplicación de datos](http://technet.microsoft.com/library/hh831602.aspx) en la biblioteca de TechNet de Windows Server.  

##  <a name="a-namebkmkdaa-directaccess"></a><a name="bkmk_DA"></a> DirectAccess  
Configuration Manager es compatible con la característica DirectAccess en Windows Server 2008 R2 para la comunicación entre clientes y servidores del sistema de sitio.  

-   Cuando se cumplen todos los requisitos de DirectAccess, mediante el uso de esta característica, los clientes de Configuration Manager en Internet pueden comunicarse con su sitio asignado como si estuvieran en la intranet.  

-   Para las acciones iniciadas por el servidor, como la instalación de inserción de cliente y el control remoto, el equipo iniciador (por ejemplo, el servidor de sitio) debe ejecutar IPv6 y este protocolo debe ser compatible con todos los dispositivos de red que intervengan.  

Configuration Manager no admite lo siguiente en DirectAccess:  

-   Implementación de sistemas operativos  

-   Comunicación entre sitios de Configuration Manager  

-   Comunicación entre servidores del sistema de sitio de Configuration Manager dentro de un sitio  

##  <a name="a-namebkmkdualboota-dual-boot-computers"></a><a name="bkmk_dualboot"></a> Equipos de arranque dual  
 Configuration Manager no puede administrar más de un sistema operativo en un equipo único. Si hay más de un sistema operativo en un equipo que se debe administrar, ajuste los métodos de instalación y detección que se usan para garantizar que el cliente de Configuration Manager está instalado solo en el sistema operativo que debe administrarse.  

##  <a name="a-namebkmkipv6a-internet-protocol-version-6"></a><a name="bkmk_IPv6"></a> Protocolo de Internet versión 6  
 Configuration Manager es compatible con el protocolo de Internet versión 6 (IPv6) además del protocolo de Internet versión 4 (IPv4), con las excepciones siguientes:  

|Función|Excepción para la compatibilidad con IPv6|  
|--------------|-------------------------------|  
|Puntos de distribución basados en la nube|IPv4 es necesario para admitir Microsoft Azure y los puntos de distribución basados en la nube.|  
|Dispositivos móviles inscritos por Microsoft Intune y el conector de servicio de Microsoft|IPv4 es necesario para admitir los dispositivos móviles inscritos por Microsoft Intune y el conector de servicio de Microsoft.|  
|Detección de redes|IPv4 es necesario cuando se configura un servidor DHCP para buscar en la detección de redes.|  
|Implementación de sistema operativo|IPv4 es necesario para admitir la implementación del sistema operativo.|  
|Comunicación del proxy de reactivación|IPv4 es necesario para admitir los paquetes del proxy de reactivación del de cliente.|  
|Windows CE|IPv4 es necesario para admitir el cliente de Configuration Manager en los dispositivos con Windows CE.|  

##  <a name="a-namebkmknata-network-address-translation"></a><a name="bkmk_NAT"></a> Traducción de direcciones de red  
 La traducción de direcciones de red (NAT) no se admite en Configuration Manager, a menos que el sitio sea compatible con los clientes que están en Internet y el cliente detecte que está conectado a Internet. Para obtener más información sobre la administración de cliente basada en Internet, consulte [Planificar la administración de clientes basados en Internet en System Center Configuration Manager](../../../core/clients/deploy/plan/plan-for-managing-internet-based-clients.md).  

##  <a name="a-namebkmkstoragea-specialized-storage-technology"></a><a name="bkmk_storage"></a> Tecnología de almacenamiento especializado  
 Configuration Manager funciona con cualquier hardware que esté certificado en la lista de compatibilidad de hardware de Windows para la versión del sistema operativo en el que está instalado el componente de Configuration Manager. Los roles del servidor de sitio requieren sistemas de archivos NTFS para que se puedan establecer los permisos de archivos y directorios. Dado que Configuration Manager da por supuesto que tiene una propiedad completa de una unidad lógica, los sistemas de sitio que se ejecutan en equipos independientes no pueden compartir una partición lógica en ninguna tecnología de almacenamiento. Sin embargo, cada equipo puede usar una partición lógica separada en la misma partición física de un dispositivo de almacenamiento compartido.  

 **Consideraciones sobre la compatibilidad:**  

-   **Red de área de almacenamiento**: una red de área de almacenamiento (SAN) es compatible cuando un servidor basado en Windows compatible está asociado directamente al volumen hospedado en la SAN.  

-   **Almacenamiento de instancia única**: Configuration Manager no admite la configuración de paquetes de puntos de distribución y carpetas de firmas en un volumen habilitado para el Almacenamiento de instancia única (SIS).  

     Además, la memoria caché de un cliente de Configuration Manager no se admite en un volumen habilitado para SIS.  

-   **Unidad de disco extraíble**: Configuration Manager no admite la instalación de clientes o sistemas de sitio de Configuration Manager en una unidad de disco extraíble.  



<!--HONumber=Nov16_HO1-->


