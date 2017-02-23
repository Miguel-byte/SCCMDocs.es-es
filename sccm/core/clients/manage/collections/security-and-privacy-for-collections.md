---
title: Seguridad y privacidad de las recopilaciones | Microsoft Docs
description: Consulte los procedimientos recomendados sobre la seguridad y la privacidad de las recopilaciones en System Center Configuration Manager.
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 30bf2451-5415-4be2-ba8d-21759370cd83
caps.latest.revision: 5
caps.handback.revision: 0
author: andredm7
ms.author: andredm
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: fc392e4440e84614f92218e9c7a09ec1c2c64f53
ms.openlocfilehash: 3379494824804c6be5c051c67a79d25e7eed88f0


---
# <a name="security-and-privacy-for-collections-in-system-center-configuration-manager"></a>Seguridad y privacidad para recopilaciones en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Este tema contiene procedimientos recomendados de seguridad e información de privacidad respecto a las recopilaciones de System Center Configuration Manager.  

 No hay ninguna información de privacidad específica para las recopilaciones en Configuration Manager. Las recopilaciones son contenedores para recursos, como usuarios y dispositivos. La pertenencia a la recopilación depende a menudo de la información que recopila Configuration Manager durante el funcionamiento normal. Por ejemplo, con la información de recursos que se ha recopilado de la detección o inventario, se puede configurar una recopilación para que contenga los dispositivos que cumplen los criterios especificados. Las recopilaciones también pueden basarse en la información de estado actual de las operaciones de administración de cliente, como la implementación de software y la comprobación de cumplimiento. Además de estas recopilaciones basadas en consultas, los usuarios administrativos también pueden agregar recursos a las recopilaciones.  

 Para obtener más información sobre las recopilaciones, consulte [Introducción a las recopilaciones en System Center Configuration Manager](../../../../core/clients/manage/collections/introduction-to-collections.md). Para obtener más información sobre los procedimientos recomendados de seguridad e información de privacidad para las operaciones de Configuration Manager que se pueden usar para configurar la pertenencia a una recopilación, consulte [Security best practices and privacy information for System Center Configuration Manager](../../../../core/plan-design/security/security-best-practices-and-privacy-information.md) (Procedimientos recomendados de seguridad e información de privacidad de System Center Configuration Manager).  

## <a name="security-best-practices-for-collections"></a>Procedimientos recomendados de seguridad para recopilaciones  
 Use el siguiente procedimiento recomendado de seguridad para las recopilaciones.  

|Práctica recomendada de seguridad|Más información|  
|----------------------------|----------------------|  
|Al exportar o importar una recopilación mediante el archivo Managed Object Format (MOF) que está guardado en una ubicación de red, proteja la ubicación y el canal de red.|Restringe quién puede tener acceso a la carpeta de red.<br /><br /> Use la firma del Bloque de mensajes del servidor (SMB) o el protocolo de seguridad de Internet (IPsec) entre la ubicación de red y el servidor de sitio para impedir que un atacante manipule los datos de la recopilación exportada. Use IPsec para cifrar los datos en la red y así evitar la revelación de información.|  

### <a name="security-issues-for-collections"></a>Problemas de seguridad para recopilaciones  
 Las recopilaciones tienen los siguientes problemas de seguridad:  

-   Si se usan variables de recopilación, los administradores locales pueden leer información potencialmente confidencial.  

     Las variables de recopilación pueden usarse al implementar un sistema operativo.  



<!--HONumber=Dec16_HO3-->


