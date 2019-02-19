---
title: Planeamiento de la base de datos del sitio
titleSuffix: Configuration Manager
description: Tenga en cuenta la base de datos y el rol de servidor de base de datos de sitio cuando planifique la jerarquía de System Center Configuration Manager.
ms.date: 03/08/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 104fb4cc-6e83-40a3-8e6b-ac909fb9ec7d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0c9134fa0bbabf5425ce17d21b143d71437aea36
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56136388"
---
# <a name="plan-for-the-site-database-for-system-center-configuration-manager"></a>Planificar la base de datos del sitio de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

El servidor de base de datos de sitio es un equipo que ejecuta una versión compatible de Microsoft SQL Server. SQL Server se usa para almacenar información para los sitios de Configuration Manager. Cada sitio de una jerarquía de Configuration Manager contiene una base de datos del sitio y un servidor al que se asigna el rol de servidor de base de datos de sitio.  

-   Para los sitios de administración central y primarios, puede instalar SQL Server en el servidor del sitio o puede instalar SQL Server en un equipo que no sea el servidor del sitio.  

-   En los sitios secundarios puede usar SQL Server Express en lugar de una instalación completa de SQL Server, aunque el servidor de base de datos se debe ejecutar en el servidor de sitio secundario.  

-  Para el uso del grupo de disponibilidad de SQL, el modelo de recuperación de base de datos debe establecerse en COMPLETA  

-  Para el uso del grupo de disponibilidad no de SQL, el modelo de recuperación de base de datos debe establecerse en SIMPLE  

Encontrará más información sobre los modos de recuperación de SQL en [Modelos de recuperación (SQL Server)](https://docs.microsoft.com/sql/relational-databases/backup-restore/recovery-models-sql-server).

Las siguientes configuraciones de SQL Server se pueden utilizar para hospedar la base de datos del sitio:  

-   La instancia predeterminada de SQL Server  

-   Una instancia con nombre en un único equipo que ejecute SQL Server  

-   Una instancia con nombre en una instancia en clúster de SQL Server  

-   Un grupo de disponibilidad AlwaysOn de SQL Server (a partir de la versión 1602 de System Center Configuration Manager)


Para hospedar la base de datos de sitio, SQL Server debe cumplir los requisitos detallados en [Support for SQL Server versions for System Center Configuration Manager](../../../core/plan-design/configs/support-for-sql-server-versions.md) (Compatibilidad con versiones de SQL Server para System Center Configuration Manager).  



## <a name="remote-database-server-location-considerations"></a>Consideraciones sobre la ubicación del servidor de base de datos remoto  

Si usa un equipo de servidor de base de datos remoto, asegúrese de que la conexión de red que intervenga sea una conexión de red de alta disponibilidad y ancho de banda alto. El servidor de sitio y algunos roles de sistema de sitio deben comunicarse constantemente con el servidor remoto que hospeda la base de datos del sitio.

-   La cantidad de ancho de banda requerida para las comunicaciones con el servidor de base de datos depende de una combinación de muchas configuraciones de sitio y cliente distintas. Por lo tanto, el ancho de banda real necesario no se puede predecir adecuadamente.  

-   Cada equipo que ejecuta el proveedor de SMS y que se conecta a la base de datos del sitio aumenta los requisitos de ancho de banda de red.  

-   El equipo que ejecuta SQL Server debe estar ubicado en un dominio que tenga una confianza bidireccional con el servidor de sitio y con todos los equipos que ejecutan el proveedor de SMS.  

-   No puede utilizar un SQL Server en clúster para el servidor de base de datos del sitio cuando la base de datos del sitio comparte ubicación con el servidor de sitio.  


Normalmente, un servidor de sistema de sitio admite roles de sistema de sitio de un único sitio de Configuration Manager. En cambio, puede usar distintas instancias de SQL Server (en servidores en clúster o que no estén en clúster que ejecuten SQL Server) para hospedar una base de datos de varios sitios de Configuration Manager. Para admitir bases de datos de sitios diferentes, debe configurar cada instancia de SQL Server para usar puertos exclusivos para la comunicación.  
