---
title: Impactos de errores de sitio
titleSuffix: Configuration Manager
description: Comprenda los efectos de los diversos errores en un sitio de Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 6f0e08f8-f2e1-4823-90f6-7b1f4341eb46
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: eebd1aaf72cbd7932a919c0a8ffdef6d6af8389f
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56132023"
---
# <a name="site-failure-impacts-in-configuration-manager"></a>Impactos de errores de sitio en Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

El servidor de sitio y cualquiera de los otros sistemas de sitio pueden producir un error y provocar una pérdida de los servicios que normalmente proporcionan. Si instala varios sistemas de sitio en el mismo equipo y se produce un error en ese equipo, todos los servicios que proporcionan normalmente esos sistemas de sitio ya no estarán disponibles.

Parte del proceso de planeación debe incluir información sobre el impacto en el servicio que proporciona a su organización. Dado que cada sistema de sitio en el sitio proporciona una funcionalidad diferente, el impacto de un error en el sitio difiere en función del rol del sistema de sitio erróneo. 

Use [opciones de alta disponibilidad](/sccm/core/servers/deploy/configure/high-availability-options) para ayudar a mitigar el error de un único sistema. También, planee y practique una estrategia de [copias de seguridad y recuperación](/sccm/core/servers/manage/backup-and-recovery) para reducir la cantidad de tiempo que el servicio no está disponible.

Las secciones siguientes describen el impacto cuando el sistema de sitio especificado no está operativo:


### <a name="site-server"></a>Servidor de sitio

- No es posible ninguna administración de sitios. No se puede conectar la consola al sitio.  

- El punto de administración recopila información de cliente y la almacena en caché hasta que se vuelve a conectar el servidor de sitio.  

- Los usuarios pueden ejecutar las implementaciones existentes y los clientes pueden descargar contenido desde puntos de distribución.  


### <a name="site-database"></a>Base de datos del sitio

- No es posible ninguna administración de sitios.  

- Si el cliente de Configuration Manager ya tiene una asignación de directiva con nuevas directivas y el punto de administración ha almacenado en caché el cuerpo de la directiva, el cliente puede realizar una solicitud de cuerpo de la directiva y recibir la respuesta del cuerpo de la directiva. En cambio, el sitio no puede atender a las nuevas solicitudes de asignación de directiva.  

- Los clientes pueden ejecutar implementaciones solo si ya han recibido la directiva y los archivos de código fuente asociados ya se han almacenado en caché localmente en el cliente.  


### <a name="management-point"></a>Punto de administración

- Aunque puede crear nuevas implementaciones, los clientes no las recibirán hasta que un punto de administración esté en línea.  

- Los clientes todavía recopilan el inventario, la medición de software y la información de estado. Almacenan estos datos localmente hasta que el punto de administración está disponible.  

- Los clientes pueden ejecutar implementaciones solo si ya han recibido la directiva y los archivos de código fuente asociados ya se han almacenado en caché localmente en el cliente.  


### <a name="distribution-point"></a>Punto de distribución

- Los clientes de Configuration Manager solo pueden ejecutar las implementaciones si los archivos de código fuente asociados ya se han descargado localmente o están disponibles en un origen del mismo nivel.

