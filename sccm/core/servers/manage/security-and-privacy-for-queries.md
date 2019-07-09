---
title: Seguridad y privacidad para consultas
titleSuffix: Configuration Manager
description: Analice los procedimientos recomendados de seguridad y privacidad al consultar información de la base de datos del sitio.
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 30080620-20d3-4c38-b8dd-db5516e1acae
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0315124b44af4359528b590bf0a6b325bfd14eb1
ms.sourcegitcommit: 3a3f40f3d39cbecfb9219a64c0185ea4b2ef9671
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/04/2019
ms.locfileid: "67561988"
---
# <a name="security-and-privacy-for-queries-in-system-center-configuration-manager"></a>Seguridad y privacidad para consultas en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Las consultas de System Center Configuration Manager le permiten recuperar información de la base de datos del sitio según los criterios que especifique. Configuration Manager recopila la información de la base de datos del sitio durante el funcionamiento normal. Por ejemplo, con la información que se ha recopilado durante la detección o el inventario, puede configurar una consulta para identificar los dispositivos que cumplen los criterios especificados.  

 Para obtener más información sobre las consultas, consulte [Introducción a las consultas en System Center Configuration Manager](../../../core/servers/manage/introduction-to-queries.md). Para conocer los procedimientos recomendados de seguridad y la información de privacidad de las operaciones de Configuration Manager que recopilan los datos que se pueden recuperar mediante consultas, consulte [Seguridad y privacidad en System Center Configuration Manager](../../../core/plan-design/security/security-and-privacy.md).  

## <a name="security-best-practices-for-queries"></a>Procedimientos recomendados de seguridad para las consultas

 Use este procedimiento recomendado para las consultas.  

|Práctica recomendada de seguridad|Más información|  
|----------------------------|----------------------|  
|Al exportar o importar una consulta que está guardada en una ubicación de red, proteja la ubicación y el canal de red.|Restrinja quién puede tener acceso a la carpeta de red.<br /><br /> Use la firma del Bloque de mensajes del servidor (SMB) o el protocolo de seguridad de Internet (IPsec) entre la ubicación de red y el servidor de sitio para impedir que un atacante manipule los datos de la consulta antes de que se importen.|  

## <a name="next-steps"></a>Pasos siguientes
  
[Seguridad y privacidad en System Center Configuration Manager](../../../core/plan-design/security/security-and-privacy.md)
