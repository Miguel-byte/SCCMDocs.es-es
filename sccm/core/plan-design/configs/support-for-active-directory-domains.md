---
title: Dominios de Active Directory admitidos
titleSuffix: Configuration Manager
description: Obtenga los requisitos de pertenencia de un sistema de sitio de System Center Configuration Manager en un dominio de Active Directory.
ms.date: 9/18/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8c5a13f8-42d5-4898-b7b6-e594dae8b335
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 02353e516e7af45afe273bc0deff5b227a7c7f2c
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/09/2019
ms.locfileid: "65499432"
---
# <a name="supported-active-directory-domains-for-system-center-configuration-manager"></a>Compatibilidad con los dominios de Active Directory para System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Todos los sistemas de sitio de System Center Configuration Manager deben ser miembros de un dominio de Windows Server Active Directory compatible. Los equipos cliente de Configuration Manager pueden ser miembros del dominio o miembros del grupo de trabajo.  

 **Limitaciones y requisitos:**  

-   La pertenencia a un dominio se aplica a los sistemas de sitio que admiten la administración de cliente basada en Internet en una red perimetral (también conocida como DMZ, zona desmilitarizada y subred filtrada).  

-   No se permite cambiar lo siguiente en un equipo que hospeda un rol de sistema de sitio:  

    -   Pertenencia a dominio *(incluye quitar un sistema de sitio del dominio y volver a unirlo al mismo dominio)*.

    -   Nombre de dominio  

    -   Nombre del equipo  

Debe desinstalar el rol de sistema de sitio (incluido el sitio si es un servidor de sitio) antes de realizar estos cambios.  

**Se admiten dominios con los siguientes niveles funcionales de dominio:**  
- Windows Server 2016

- Windows Server 2012 R2  

- Windows Server 2012

- Windows Server 2008 R2

- Windows Server 2008  







##  <a name="bkmk_Disjoint"></a> Espacio de nombres no contiguo  
Configuration Manager admite la instalación de clientes y sistemas de sitio en un dominio que tiene un espacio de nombres no contiguo.  

Un escenario de espacio de nombres separado es aquel en el que el sufijo del sistema de nombres de dominio (DNS) principal de un equipo no coincide con el nombre de dominio DNS de Active Directory donde reside ese equipo. Se dice que el equipo que usa el sufijo DNS principal que no coincide está separado. Otro escenario de espacio de nombres separado se produce si el nombre de dominio NetBIOS de un controlador de dominio no coincide con el nombre de dominio DNS de Active Directory.  

En la tabla siguiente se identifican los escenarios admitidos para un espacio de nombres separado.  

|Escenario|Más información|  
|--------------|----------------------|  
|**Escenario 1:**<br /><br /> El sufijo DNS principal del controlador de dominio difiere del nombre de dominio DNS de Active Directory. Los equipos que son miembros del dominio pueden estar separados o no separados.|En este escenario, el sufijo DNS principal del controlador de dominio difiere del nombre de dominio DNS de Active Directory. El controlador de dominio está separado en este escenario. Los equipos que son miembros del dominio, como los equipos y los servidores de sitio, pueden tener un sufijo DNS principal que coincida con el sufijo DNS principal del controlador de dominio o que coincida con el nombre de dominio DNS de Active Directory.|  
|**Escenario 2:**<br /><br /> Un equipo miembro en un dominio de Active Directory está separado, aun cuando el controlador de dominio no está separado.|En este escenario, el sufijo DNS principal de un equipo miembro en el que está instalado un sistema de sitio difiere del nombre de dominio DNS de Active Directory, aunque el sufijo DNS principal del controlador de dominio es el mismo que el nombre de dominio DNS de Active Directory. En este escenario, se tiene un controlador de dominio que no está separado y un equipo miembro que está separado. Los equipos miembro que ejecutan el cliente de Configuration Manager pueden tener un sufijo DNS principal que coincida con el sufijo DNS principal del servidor del sistema de sitio no contiguo o que coincida con el nombre de dominio DNS de Active Directory.|  

 Para permitir que un equipo tenga acceso a controladores de dominio que están separados, debe cambiar el atributo de Active Directory de **msDS-AllowedDNSSuffixes** en el contenedor de objetos del dominio. Debe agregar ambos sufijos DNS al atributo.  

 Además, para asegurarse de que la lista de búsqueda de sufijos DNS contiene todos los espacios de nombres DNS que se implementan dentro de la organización, debe configurar la lista de búsqueda para cada equipo en el dominio que está separado. Asegúrese de incluir lo siguiente en la lista de espacios de nombres: el sufijo DNS principal del controlador de dominio, el nombre de dominio DNS y los espacios de nombres adicionales para otros servidores con los que Configuration Manager es posible que interopere. Puede usar la consola de Administración de directivas de grupo para configurar la **Lista de búsqueda de sufijos DNS** (Sistema de nombres de dominio).  

> [!IMPORTANT]  
>  Al hacer referencia a un equipo en Configuration Manager, escriba el equipo con el sufijo DNS principal. Este sufijo debe coincidir con el nombre de dominio completo registrado como el atributo de **dnsHostName** en el dominio de Active Directory y el nombre de entidad de seguridad de servicio asociado con el sistema.  

##  <a name="bkmk_SLD"></a> Dominios de una sola etiqueta  
 Configuration Manager admite clientes y sistemas de sitio en un dominio de una sola etiqueta cuando se cumplen los criterios siguientes:  

-   El dominio de una sola etiqueta en Active Directory Domain Services se debe configurar con un espacio de nombres DNS separado que tenga un dominio de nivel superior válido.  

     **Por ejemplo:** El dominio de una sola etiqueta de Contoso está configurado para tener un espacio de nombres separado en DNS de contoso.com. Por tanto, al especificar el sufijo DNS en Configuration Manager para un equipo en el dominio Contoso, especifique "Contoso.com" y no "Contoso".  

-   Las conexiones de Modelo de objetos componentes distribuido (DCOM) entre los servidores de sitio en el contexto del sistema deben ser correctas mediante el uso de la autenticación Kerberos.  
