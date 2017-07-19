---
title: Seguridad y privacidad para consultas | Microsoft Docs
description: "Analice los procedimientos recomendados de seguridad y privacidad al consultar información de la base de datos del sitio."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 30080620-20d3-4c38-b8dd-db5516e1acae
caps.latest.revision: 5
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 2087badc9dd1d216352dce232b145a786783ac89
ms.openlocfilehash: e42b13c68ecaeac94245838c2f42e2790799de2b
ms.contentlocale: es-es
ms.lasthandoff: 05/18/2017


---
# <a name="security-and-privacy-for-queries-in-system-center-configuration-manager"></a>Seguridad y privacidad para consultas en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Las consultas de System Center Configuration Manager le permiten devolver información de la base de datos del sitio según los criterios que especifique. Configuration Manager recopila la información de la base de datos del sitio durante el funcionamiento normal. Por ejemplo, con la información que se ha recopilado de la detección o inventario, puede configurar una consulta para identificar los dispositivos que cumplen los criterios especificados.  

 Para obtener más información sobre las consultas, consulte [Introducción a las consultas en System Center Configuration Manager](../../../core/servers/manage/introduction-to-queries.md). Para obtener más información sobre los procedimientos recomendados de seguridad e información de privacidad para las operaciones de Configuration Manager que recopilan información que se puede recuperar usando consultas, consulte [Seguridad y privacidad en System Center Configuration Manager](../../../core/plan-design/security/security-and-privacy.md).  

## <a name="security-best-practices-for-queries"></a>Procedimientos recomendados de seguridad para consultas  
 Use el siguiente procedimiento recomendado de seguridad para consultas.  

|Práctica recomendada de seguridad|Más información|  
|----------------------------|----------------------|  
|Al exportar o importar una consulta que está guardada en una ubicación de red, proteja la ubicación y el canal de red.|Restrinja quién puede tener acceso a la carpeta de red.<br /><br /> Use la firma del Bloque de mensajes del servidor (SMB) o el protocolo de seguridad de Internet (IPsec) entre la ubicación de red y el servidor de sitio para impedir que un atacante manipule los datos de la consulta antes de que se importen.|  

## <a name="see-also"></a>Consulte también  
 [Referencia técnica de consultas para System Center Configuration Manager](../../../core/servers/manage/queries-technical-reference.md)

