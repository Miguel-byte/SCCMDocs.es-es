---
title: "Propiedades de instalación de cliente en Active Directory Domain Services | System Center Configuration Manager"
description: "Use las propiedades de instalación de cliente publicadas en Active Directory Domain Services en System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 101d7d4d-92db-419d-b2ae-3c1c1dea68e9
caps.latest.revision: 6
caps.handback.revision: 0
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: d5cdaa80abca6d003d3e07c2068c12de64ccab67

---
# <a name="about-client-installation-properties-published-to-active-directory-domain-services-in-system-center-configuration-manager"></a>Acerca de las propiedades de instalación de cliente publicadas en Active Directory Domain Services en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Al extender el esquema de Active Directory para System Center Configuration Manager y publicar el sitio en Active Directory Domain Services, muchas propiedades de instalación de cliente se publican en Active Directory Domain Services. Si un equipo puede ubicar estas propiedades de instalación de cliente, puede usarlas durante la implementación de cliente de Configuration Manager.  

 Las ventajas de utilizar Servicios de dominio de Active Directory para publicar propiedades de instalación de cliente incluyen:  

-   La instalación de cliente basada en punto de actualización de software y las instalaciones de cliente de directiva de grupo no requieren que los parámetros de instalación se aprovisionen en cada equipo.  

-   Dado que esta información se genera automáticamente, se elimina el riesgo de error humano asociado con escribir manualmente las propiedades de la instalación.  

> [!NOTE]  
>  Para obtener más información sobre cómo extender el esquema de Active Directory para Configuration Manager y cómo publicar un sitio, consulte [Extensiones de esquema para System Center Configuration Manager](../../plan-design/network/schema-extensions.md).  

 La instalación de cliente (CCMSetup) usa las propiedades de instalación de cliente publicadas en Servicios de dominio de Active Directory solo si no se especifican otras propiedades mediante cualquiera de los métodos siguientes:  

-   Instalación manual  

-   Aprovisionamiento de propiedades de instalación de cliente mediante una directiva de grupo  

> [!NOTE]  
>  Las propiedades de instalación de cliente se usan para instalar el cliente y se pueden sobrescribir con nuevas configuraciones del correspondiente sitio asignado después de que el cliente se haya instalado y se haya asignado correctamente a un sitio de Configuration Manager.  

 Aplique la información de las secciones siguientes para determinar qué métodos de instalación de cliente de Configuration Manager usan Active Directory Domain Services para obtener las propiedades de instalación de cliente.  

## <a name="client-push-installation"></a>Instalación de inserción de cliente  
 La instalación de inserción de cliente no usa Servicios de dominio de Active Directory para obtener las propiedades de instalación.  

 En vez de ello, puede especificar propiedades de instalación de client.msi en la pestaña **Cliente** del cuadro de diálogo **Propiedades de instalación de inserción de cliente** . Estas opciones y la configuración de sitio relacionada con el cliente se almacenan en un archivo que el cliente lee durante la instalación de cliente.  

> [!NOTE]  
>  No es necesario que especifique ninguna propiedad de CCMSetup para la instalación de inserción de cliente, el punto de estado de reserva o la clave raíz confiable en la pestaña **Cliente** . Estos valores se suministran automáticamente a los clientes cuando se instalan mediante la instalación de inserción de cliente.  

 Las propiedades de client.msi especificadas en la pestaña **Cliente** se publican en Servicios de dominio de Active Directory si el sitio se publica en Servicios de dominio de Active Directory. Las instalaciones de cliente leen esta configuración cuando se ejecuta CCMSetup sin propiedades de instalación.  

## <a name="software-update-point-based-installation"></a>Instalación basada en el punto de actualización de software  
 El método de instalación basada en el punto de actualización de software no es compatible con la incorporación de propiedades de instalación en la línea de comandos de CCMSetup.  

 Si no se ha aprovisionado ninguna propiedad de línea de comandos en el equipo cliente mediante una directiva de grupo, CCMSetup busca propiedades de instalación en Servicios de dominio de Active Directory.  

## <a name="group-policy-installation"></a>Instalación de directiva de grupo  
 El método de instalación de directiva de grupo no es compatible con la incorporación de propiedades de instalación en la línea de comandos de CCMSetup.  

 Si no se ha aprovisionado ninguna propiedad de línea de comandos en el equipo cliente, CCMSetup busca propiedades de instalación en Servicios de dominio de Active Directory.  

## <a name="manual-installation"></a>Instalación manual  
 CCMSetup busca propiedades de instalación en Servicios de dominio de Active Directory en las siguientes circunstancias:  

-   No se especifican propiedades de línea de comandos después del comando CCMSetup.exe.  

-   El equipo no se ha aprovisionado con propiedades de instalación mediante una directiva de grupo.  

## <a name="logon-script-installation"></a>Instalación de script de inicio de sesión  
 CCMSetup busca propiedades de instalación en Servicios de dominio de Active Directory en las siguientes circunstancias:  

-   No se especifican propiedades de línea de comandos después del comando CCMSetup.exe.  

-   El equipo no se ha aprovisionado con propiedades de instalación mediante una directiva de grupo.  

## <a name="software-distribution-installation"></a>Instalación de distribución de software  
 CCMSetup busca propiedades de instalación en Servicios de dominio de Active Directory en las siguientes circunstancias:  

-   No se especifican propiedades de línea de comandos después del comando CCMSetup.exe.  

-   El equipo no se ha aprovisionado con propiedades de instalación mediante una directiva de grupo.  

## <a name="installations-for-clients-that-cannot-access-active-directory-domain-services-for-published-information"></a>Instalaciones para clientes que no pueden acceder a Active Directory Domain Services para obtener información publicada.  
 Entre estos clientes se incluyen:  

-   Equipos de grupo de trabajo  

-   Clientes asignados a un sitio de Configuration Manager que no está publicado en Active Directory Domain Services.  

-   Clientes que se instalan cuando están en Internet  

 Estos equipos cliente no pueden leer las propiedades de instalación de Servicios de dominio de Active Directory y, por lo tanto, no podrán tener acceso a las propiedades de instalación publicadas.  

## <a name="client-installation-properties-published-to-active-directory-domain-services"></a>Propiedades de instalación de cliente publicadas en Active Directory Domain Services  
 Para obtener más información sobre cada uno de los elementos siguientes, consulte [Acerca de las propiedades de instalación de clientes en System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

-   Código de sitio de Configuration Manager.  

-   El certificado de firma de servidor de sitio.  

-   La clave raíz confiable.  

-   Los puertos de comunicación de cliente para HTTP y HTTPS.  

-   El punto de estado de reserva. Si el sitio tiene varios puntos de estado de reserva, se publicará en Servicios de dominio de Active Directory solo el primero que se instaló.  

-   Un valor para indicar que el cliente debe comunicarse solo mediante HTTPS.  

-   Configuración relacionada con certificados PKI:  

    -   Si se utiliza un certificado PKI de cliente.  

    -   Los criterios de selección de certificados, en caso de que sea necesario porque el cliente tiene más de un certificado PKI válido que se puede usar para Configuration Manager.  

    -   Una opción para determinar el certificado que se va a usar si el cliente tiene varios certificados válidos después del proceso de selección de certificado.  

    -   La lista de emisores de certificados que contiene una lista de certificados de CA raíz confiables.  

-   Propiedades de instalación de client.msi especificados en la pestaña **Cliente** del cuadro de diálogo **Propiedades de instalación de inserción de cliente** .



<!--HONumber=Nov16_HO1-->


