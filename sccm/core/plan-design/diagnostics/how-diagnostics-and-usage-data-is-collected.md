---
title: Recopilación de datos de diagnóstico
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo System Center Configuration Manager recopila datos de uso y diagnóstico sobre sí mismo.
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: becfa825-b19f-448c-ab82-bb929255e4ae
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 704c64d314f2eaf4fe2678f316ea729584752d2e
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56125585"
---
# <a name="how-diagnostics-and-usage-data-is-collected-by-system-center-configuration-manager"></a>Cómo System Center Configuration Manager recopila los datos de uso y diagnóstico

*Se aplica a: System Center Configuration Manager (Rama actual)*

Para recopilar los datos de uso y diagnóstico para System Center Configuration Manager, cada sitio primario ejecuta consultas de SQL Server con carácter semanal. En una jerarquía de varios sitio, los datos se replican en el sitio de administración central.  

En el sitio de nivel superior de una jerarquía, el rol de sistema de sitio del punto de conexión de servicio envía esta información cuando busca actualizaciones. El modo del punto de conexión de servicio determina cómo se transfieren los datos:  

-   **En el modo con conexión:** los datos de uso y diagnóstico se envían automáticamente una vez por semana, desde el punto de conexión de servicio al servicio en la nube.  

-   **En el modo sin conexión:** los datos de uso y diagnóstico se transfieren manualmente mediante la herramienta de conexión de servicio. Para obtener más información, consulte [Uso de la herramienta de conexión de servicio para System Center Configuration Manager](../../../core/servers/manage/use-the-service-connection-tool.md).  

Para obtener más información, consulte [Acerca del punto de conexión de servicio en System Center Configuration Manager](../../../core/servers/deploy/configure/about-the-service-connection-point.md).  
