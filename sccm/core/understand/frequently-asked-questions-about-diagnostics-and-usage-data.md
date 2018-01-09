---
title: "Preguntas frecuentes sobre datos de diagnóstico"
titleSuffix: Configuration Manager
description: "Consulte preguntas frecuentes acerca de datos de diagnóstico y uso para System Center Configuration Manager."
ms.custom: na
ms.date: 2/8/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3fe32aa2-d594-4ad0-a291-b8f5395ac50b
caps.latest.revision: "6"
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 91be283558f051f90080ac2e2f7abc09317eac4a
ms.sourcegitcommit: ca9d15dfb1c9eb47ee27ea9b5b39c9f8cdcc0748
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/04/2018
---
# <a name="frequently-asked-questions-about-diagnostics-and-usage-data-for-system-center-configuration-manager"></a>Preguntas frecuentes acerca de datos de diagnóstico y uso para System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

A continuación se muestran preguntas frecuentes sobre datos de diagnóstico y uso para System Center Configuration Manager:  

###  <a name="bkmk_off"></a> ¿Cómo se desactiva la telemetría?  
La telemetría no se puede desactivar. En cambio, puede seleccionar el nivel de datos de telemetría que se recopilarán. También puede usar un punto de conexión de servicio en el modo sin conexión para facilitar la administración después de enviar los datos de telemetría.

La rama actual de Configuration Manager necesita actualizarse de forma periódica para admitir las nuevas versiones de Windows 10 y Microsoft Intune. Microsoft necesita como mínimo el nivel básico de datos de diagnóstico y uso para mantener el producto actualizado, mejorar la experiencia de actualización y mejorar la calidad y la seguridad del producto.

###  <a name="bkmk_retention"></a> ¿Qué es el período de retención de datos?  
 Los datos de diagnóstico y uso se conservan durante un año.  

###  <a name="bkmk_update"></a> ¿Los datos de diagnóstico y uso se envían al instalar o actualizar el producto?  
 No. Solo se envían datos de diagnóstico y uso una vez que el sitio está instalado y en funcionamiento.  

###  <a name="bkmk_frequency"></a> ¿Con qué frecuencia se envían los datos?  
 Los procedimientos almacenados de SQL se ejecutan cada siete días (desde la fecha en que se instaló el sitio). En el modo en línea, el punto de conexión de servicio está configurado para cargar los datos después de ejecutar las consultas. En el modo sin conexión, el administrador usa la herramienta de conexión de servicio para cargar los datos. (Tenga en cuenta que los datos no estarán disponibles inicialmente para su uso sin conexión hasta siete días después de la instalación del sitio).  

###  <a name="bkmk_network"></a> ¿Los datos se pueden usar para formar un mapa de red?  
 Como se muestra en la descripción de los niveles de recopilación de datos de uso para diagnóstico de System Center Configuration Manager, en los detalles del sitio se incluye información sobre la zona horaria de cada sitio. Esto puede ofrecer información general sobre la geolocalización y la dispersión global de los sitios de una jerarquía. En cambio, no se recopilan detalles de la red (como direcciones IP o información geográfica más detallada).
 - [Datos de diagnóstico para 1511](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1511)
 - [Datos de diagnóstico para 1602](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1602)
 - [Datos de diagnóstico para 1606](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1606)
 - [Datos de diagnóstico para 1610](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1610)


###  <a name="bkmk_tables"></a> ¿Se pueden ver datos en tablas personalizadas?  
 No. Los datos de diagnóstico y uso se recopilan a través de procedimientos almacenados de SQL en relación con tablas de producto predeterminadas en la base de datos (que tienen el prefijo **TEL_**). Como parte de la consulta de detección de esquemas SQL, a todos los nombres de tabla se les aplica un algoritmo hash para establecer comparaciones con los valores predeterminados conocidos. Esto puede determinar que existen tablas personalizadas en la base de datos (esto es, que el esquema de base de datos está ampliado respecto del predeterminado), pero no los datos contenidos en las tablas.  

###  <a name="bkmk_databases"></a> ¿Se pueden ver los nombres de otras bases de datos o los datos que contienen?  
 No. Los procedimientos almacenados para recopilar los datos se limitan a la base de datos del sitio.  

## <a name="see-also"></a>Consulte también  
 [Diagnósticos y datos de uso para System Center Configuration Manager](../../core/plan-design/diagnostics/diagnostics-and-usage-data.md)
