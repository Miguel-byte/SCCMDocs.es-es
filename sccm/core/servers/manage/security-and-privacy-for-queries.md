---
title: Seguridad y privacidad para consultas
titleSuffix: Configuration Manager
description: Analice los procedimientos recomendados de seguridad y privacidad al consultar información de la base de datos del sitio.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 30080620-20d3-4c38-b8dd-db5516e1acae
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 2d84385782df17d4019d6de65bcc7006aeab8b24
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32337622"
---
# <a name="security-and-privacy-for-queries-in-system-center-configuration-manager"></a>Seguridad y privacidad para consultas en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Las consultas de System Center Configuration Manager le permiten devolver información de la base de datos del sitio según los criterios que especifique. Configuration Manager recopila la información de la base de datos del sitio durante el funcionamiento normal. Por ejemplo, utilizando la información que se ha recopilado de descubrimiento o inventario, puede configurar una consulta para identificar los dispositivos que cumplen los criterios especificados.  

 Para obtener más información sobre las consultas, consulte [Introducción a las consultas en System Center Configuration Manager](../../../core/servers/manage/introduction-to-queries.md). Para obtener más información sobre los procedimientos recomendados de seguridad e información de privacidad para las operaciones de Configuration Manager que recopilan información que se puede recuperar usando consultas, consulte [Seguridad y privacidad en System Center Configuration Manager](../../../core/plan-design/security/security-and-privacy.md).  

## <a name="security-best-practices-for-queries"></a>Prácticas recomendadas de seguridad para las consultas  
 Use el siguiente procedimiento recomendado de seguridad para consultas.  

|Práctica recomendada de seguridad|Más información|  
|----------------------------|----------------------|  
|Al exportar o importar una consulta que está guardada en una ubicación de red, proteja la ubicación y el canal de red.|Restrinja quién puede tener acceso a la carpeta de red.<br /><br /> Use la firma del Bloque de mensajes del servidor (SMB) o el protocolo de seguridad de Internet (IPsec) entre la ubicación de red y el servidor de sitio para impedir que un atacante manipule los datos de la consulta antes de que se importen.|  

## <a name="see-also"></a>Consulte también  
 [Referencia técnica de consultas para System Center Configuration Manager](../../../core/servers/manage/queries-technical-reference.md)
