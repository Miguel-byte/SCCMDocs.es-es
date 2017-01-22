---
title: Sitios web para sistemas de sitio | Microsoft Docs
description: "Obtenga información sobre los sitios web predeterminados y personalizados para servidores de sistema de sitio en System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 681f0893-e83b-476e-9ec0-a5dc7c9deeb6
caps.latest.revision: 15
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6ed317d45d90758832d4157985dd95d5e253c6fc
ms.openlocfilehash: 005c9f33367f173993d9626f10a72dd5b0141fbc


---
# <a name="websites-for-site-system-servers-in-system-center-configuration-manager"></a>Websites para servidores de sistema de sitio en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Varios roles de sistema de sitio de Configuration Manager requieren Microsoft Internet Information Services (IIS) y usan el sitio web de IIS predeterminado para hospedar los servicios de sistema de sitio. Si debe ejecutar otras aplicaciones web en el mismo servidor y la configuración no es compatible con Configuration Manager, considere la posibilidad de usar un sitio web personalizado para Configuration Manager.  

> [!TIP]  
>  Como medida de seguridad, se recomienda dedicar un servidor a los sistemas de sitio de Configuration Manager que requieren IIS. Cuando se ejecutan otras aplicaciones en un sistema de sitio de Configuration Manager, aumenta la superficie expuesta a ataques del equipo.  




##  <a name="a-namebkmkwhat2knowa-what-to-know-before-choosing-to-use-custom-websites"></a><a name="BKMK_What2Know"></a> Qué debe saber antes de decidirse a usar sitios web personalizados  
 De forma predeterminada, los roles de sistema de sitio usan el **sitio web predeterminado** en IIS. Esto se configura automáticamente cuando se instala el rol de sistema de sitio. Sin embargo, en los sitios primarios, puede usar en su lugar sitios web personalizados. Al usar sitios web personalizados:  

-   Los sitios web personalizados está habilitados para todo el sitio, no para roles o servidores de sistema de sitio individuales.  

-   En los sitios primarios, cada equipo que hospedará un rol de sistema de sitio aplicable debe configurarse con un sitio web personalizado denominado **SMSWEB**. Hasta que se cree este sitio web y los roles de sistema de sitio en el equipo se configuren para utilizar el sitio web personalizado, los clientes no podrán comunicarse con los roles de sistema de sitio en ese equipo.  

-   Dado que los sitios secundarios se configuran automáticamente para usar un sitio web personalizado cuando su sitio primario principal está configurado para ello, también debe crear sitios web personalizados en IIS en cada servidor de sistema de sitio secundario que requiera IIS.  


  **Requisitos previos para usar sitios web personalizados:**  

 Antes de habilitar la opción de usar sitios web personalizados en un sitio, debe hacer lo siguiente:  

-   Cree un sitio web personalizado denominado **SMSWEB** en IIS en cada servidor de sistema de sitio que requiera IIS. Haga esto en el sitio primario y en todos los sitios secundarios.  

-   Configure el sitio web personalizado para que responda al mismo puerto que configura para la comunicación de cliente de Configuration Manager (puerto de solicitud de cliente).  

-   Por cada sitio web personalizado o predeterminado que use una carpeta personalizada, coloque una copia del tipo de documento predeterminado que use en la carpeta raíz que hospeda el sitio web. Por ejemplo, en un equipo con Windows Server 2008 R2 con las configuraciones predeterminadas, **iisstart.htm** es uno de los distintos tipos de documentos disponibles. Puede encontrar este archivo en la raíz del sitio web predeterminado y, luego, colocar una copia de este archivo (o una copia del tipo de documento predeterminado que use) en la carpeta raíz que hospeda el sitio web personalizado SMSWEB. Para obtener más información sobre los tipos de documento predeterminados, consulte [Default Document &lt;defaultDocument\> for IIS](http://www.iis.net/configreference/system.webserver/defaultdocument) (Documento predeterminado <documentoPredeterminado> para IIS).  

**Acerca de los requisitos de IIS:**
**Los siguientes roles de sistema de sitio requieren IIS y un sitio web para hospedar los servicios de sistema de sitio:**  

-   Punto de servicio web del catálogo de aplicaciones  

-   Punto de sitios web del catálogo de aplicaciones  

-   Punto de distribución  

-   Punto de inscripción  

-   Punto de proxy de inscripción  

-   Punto de estado de reserva  

-   Punto de administración  

-   Punto de actualización de software  

-   Punto de migración de estado  

Consideraciones adicionales:  

-   Cuando un sitio primario tiene habilitados sitios web personalizados, los clientes asignados a ese sitio se dirigen para que se comuniquen con los sitios web personalizados, en lugar de con los sitios web predeterminados en los servidores de sistema de sitio aplicables.  

-   Si va a usar sitios web personalizados para un sitio primario, considere el uso de sitios web personalizados para todos los sitios primarios de la jerarquía para asegurarse de que los clientes pueden moverse correctamente en la jerarquía. (La movilidad significa que un equipo cliente se mueve a un nuevo segmento de red que está administrado por otro sitio. La movilidad puede afectar a los recursos a los que el cliente puede acceder localmente en lugar de acceder a través de un vínculo WAN).  

-   Los roles de sistema de sitio que usan IIS pero que no aceptan conexiones de cliente, como el punto de servicios de informes, también usan el sitio web SMSWEB en vez del sitio web predeterminado.  

-   Los sitios web personalizados requieren la asignación de números de puerto distintos de los que usa el sitio web predeterminado del equipo. El sitio web predeterminado y el sitio web personalizado no se pueden ejecutar al mismo tiempo si ambos sitios tratan de usar los mismos puertos TCP/IP.  

-   Los puertos TCP/IP que se configuran en IIS para el sitio web personalizado deben coincidir con los puertos de solicitud de cliente para el sitio.  

## <a name="switching-between-default-and-custom-websites"></a>Alternancia entre sitios web predeterminados y personalizados  
Aunque puede activar o desactivar la casilla para usar sitios web personalizados en un sitio primario en cualquier momento (se trata de la casilla de la pestaña General en las propiedades de los sitios), debe llevar a cabo una planeación cuidadosa antes de proceder a este cambio. Cuando se cambia esta configuración, todos los roles de sistema de sitio aplicables en el sitio primario y en los sitios secundarios deben desinstalarse y volver a instalarse:  

Los siguientes roles **se reinstalan automáticamente**:  

-   Punto de administración  

-   Punto de distribución  

-   Punto de actualización de software  

-   Punto de estado de reserva  

-   Punto de migración de estado  

Los siguientes roles deben **reinstalarse manualmente**:  

-   Punto de servicio web del catálogo de aplicaciones  

-   Punto de sitios web del catálogo de aplicaciones  

-   Punto de inscripción  

-   Punto de proxy de inscripción  

Además:  

-   Cuando se pasa de usar el sitio web predeterminado a usar un sitio web personalizado, Configuration Manager no quita los directorios virtuales antiguos. Si quiere quitar los archivos que usó Configuration Manager, debe eliminar manualmente los directorios virtuales que se crearon en el sitio web predeterminado.  

-   Si cambia el sitio para que use sitios web personalizados, los clientes que ya están asignados al sitio deben volver a configurarse para que usen los nuevos puertos de solicitud de cliente para los sitios web personalizados. Consulte [How to configure client communication ports in System Center Configuration Manager](../../../core/clients/deploy/configure-client-communication-ports.md) (Configurar puertos de comunicación de cliente en System Center Configuration Manager).  

## <a name="configure-custom-websites"></a>Configurar sitios web personalizados  
Dado que los pasos para crear un sitio web personalizado varían según las versiones del sistema operativo, debe consultar la documentación de la versión de su sistema operativo para conocer los pasos exactos, pero puede usar la información siguiente cuando sea aplicable:  

-   El nombre del sitio web debe ser: **SMSWEB**.  

-   Al configurar el protocolo HTTPS, debe especificar un certificado SSL para poder guardar la configuración.  

-   Después de crear el sitio web personalizado, quite los puertos de sitio web personalizado que se usan desde otros sitios web en IIS:  

    1.  Edite los **enlaces** de los demás sitios web para quitar los puertos que coinciden con los asignados al sitio web **SMSWEB** .  

    2.  Inicie el sitio web **SMSWEB** .  

    3.  Reinicie el servicio **SMS_SITE_COMPONENT_MANAGER** en el servidor de sitio.  



<!--HONumber=Dec16_HO3-->


