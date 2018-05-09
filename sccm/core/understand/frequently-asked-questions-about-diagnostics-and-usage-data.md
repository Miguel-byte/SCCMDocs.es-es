---
title: Preguntas más frecuentes sobre datos de uso y diagnóstico
titleSuffix: Configuration Manager
description: Consulte preguntas frecuentes acerca de datos de diagnóstico y uso para System Center Configuration Manager.
ms.date: 04/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 3fe32aa2-d594-4ad0-a291-b8f5395ac50b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b4174c68d5a6ccd31355d976b7830b6d09f39d91
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="frequently-asked-questions-about-diagnostics-and-usage-data-for-system-center-configuration-manager"></a>Preguntas frecuentes acerca de datos de diagnóstico y uso para System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

En este artículo encontrará respuestas a preguntas frecuentes sobre datos de diagnóstico y uso en Configuration Manager.

## <a name="faqs"></a>Preguntas más frecuentes

###  <a name="bkmk_off"></a> ¿Cómo se desactiva la telemetría?  
La telemetría no se puede desactivar. En cambio, puede seleccionar el nivel de datos de telemetría que se recopilarán. Para ayudar a administrar cuándo se envían los datos de telemetría, use el punto de conexión de servicio en el modo sin conexión.

La rama actual de Configuration Manager necesita actualizarse de forma periódica para admitir las nuevas versiones de Windows 10 y Microsoft Intune. Microsoft necesita como mínimo el nivel básico de datos de diagnóstico y uso. Estos datos sirven para mantener el producto actualizado, mejorar la experiencia de actualización y mejorar la calidad y la seguridad del producto.

###  <a name="bkmk_retention"></a> ¿Qué es el período de retención de datos?  
 Los datos de diagnóstico y uso se almacenan durante un año.  

###  <a name="bkmk_update"></a> ¿Los datos de diagnóstico y uso se envían al instalar o actualizar el producto?  
 No. Solo se envían datos de diagnóstico y uso una vez que el sitio está instalado y en funcionamiento.  

###  <a name="bkmk_frequency"></a> ¿Con qué frecuencia se envían los datos?  
 Los procedimientos almacenados de SQL se ejecutan cada siete días desde la fecha en que se instaló el sitio. En el modo en línea, el punto de conexión de servicio está configurado para cargar los datos después de ejecutar las consultas. En el modo sin conexión, el administrador usa la herramienta de conexión de servicio para cargar los datos. (Los datos no están disponibles inicialmente para su uso sin conexión hasta que transcurran siete días tras la instalación del sitio).  

###  <a name="bkmk_network"></a> ¿Los datos se pueden usar para formar un mapa de red?  
 Como se muestra en la descripción de los niveles de datos de diagnóstico y uso, los detalles del sitio incluyen información sobre la zona horaria de cada sitio. Esto puede ofrecer información general sobre la geolocalización y la dispersión global de los sitios de una jerarquía. Estos datos no reflejan ningún detalle de red (como direcciones IP) o información geográfica más detallada. Para más información, vea la lista de [artículos de datos de diagnóstico y uso](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data#articles) y busque los niveles de recopilación de datos de diagnóstico y uso correspondiente a la versión que esté usando.


###  <a name="bkmk_tables"></a> ¿Se pueden ver datos en tablas personalizadas?  
 No. Configuration Manager recopila datos de uso y diagnóstico a través de procedimientos almacenados de SQL. Estos procedimientos almacenados se ejecutan en tablas de productos predeterminadas de la base de datos. Todas estas tablas SQL tienen el prefijo **TEL_**. Como parte de la consulta de detección de esquemas SQL, a todos los nombres de tabla se les aplica un algoritmo hash para establecer comparaciones con los valores predeterminados conocidos. Este comportamiento determina que hay tablas personalizadas en la base de datos. La presencia de tablas personalizadas indica que el esquema de la base de datos se ha extendido desde el valor predeterminado. No incluye ninguno de los datos almacenados en esas tablas.  

###  <a name="bkmk_databases"></a> ¿Se pueden ver los nombres de otras bases de datos o los datos que contienen? 
 No. Los procedimientos almacenados para recopilar los datos se limitan a la base de datos del sitio.  

### <a name="bkmk_gdpr"></a> ¿Se rige Configuration Manager por el Reglamento general de protección de datos (RGPD)?
 No. Configuration Manager no se rige por la supervisión de RGPD, sino que es un producto local que el usuario implementa, administra y opera directamente. Los datos de diagnóstico y uso que Microsoft recopila mejoran la experiencia de instalación, la calidad y la seguridad de las versiones futuras. Estos datos sí se rigen por la supervisión de RGPD. No se recopila y ni transmite a Microsoft ningún tipo de información de identificación del usuario final ni identificadores seudónimos de usuario final. Para más información sobre RGPD, vaya al [Centro de confianza de Microsoft sobre RGPD](https://microsoft.com/gdpr). Para más información sobre los datos de Configuration Manager, vea [Datos de diagnóstico y uso](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data).


## <a name="see-also"></a>Consulte también  
 [Diagnósticos y datos de uso](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data)
