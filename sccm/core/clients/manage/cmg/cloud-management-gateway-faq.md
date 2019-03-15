---
title: PREGUNTAS MÁS FRECUENTES SOBRE CLOUD MANAGEMENT GATEWAY
description: Use este artículo para responder a las preguntas más frecuentes sobre Cloud Management Gateway.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 09/10/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 4c1a128d-22fb-49f1-8e0b-36513a8dc117
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4cbb9b37c951c490c1f2245f089fa22707f4c220
ms.sourcegitcommit: f3dd8405018fe1043434386be15c16752c1a4a3c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/07/2019
ms.locfileid: "57558021"
---
# <a name="frequently-asked-questions-about-the-cloud-management-gateway"></a>Preguntas más frecuentes sobre Cloud Management Gateway

*Se aplica a: System Center Configuration Manager (Rama actual)*

En este artículo se responden las preguntas más frecuentes sobre Cloud Management Gateway. Para obtener más información, vea [Plan for cloud management gateway](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway) (Plan para Cloud Management Gateway).


## <a name="frequently-asked-questions"></a>Preguntas más frecuentes

### <a name="what-certificates-do-i-need"></a>¿Qué certificados necesito?

Para obtener más información, vea [certificates for cloud management gateway](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway) (Certificados para Cloud Management Gateway).


### <a name="do-i-need-azure-expressroute"></a>¿Necesito Microsoft Azure ExpressRoute?

[Azure ExpressRoute](/azure/expressroute/expressroute-introduction) permite ampliar la red local a la nube de Microsoft. No se necesita ExpressRoute, ni otras conexiones de red virtual de este tipo, para Cloud Management Gateway de Configuration Manager. El diseño de Cloud Management Gateway permite a los clientes basados en Internet comunicarse a través del servicio de Azure con sistemas de sitio locales sin ninguna configuración de red adicional. Para obtener más información, vea [Plan for cloud management gateway (Plan para Cloud Management Gateway)](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway).

Si la organización usa ExpressRoute, un procedimiento recomendado de seguridad consiste en aislar la suscripción de Azure para la instancia de Cloud Management Gateway. Esta configuración garantiza que el servicio de Cloud Management Gateway no se conecte accidentalmente de esta manera. Para obtener más información, vea [Security and privacy for cloud management gateway](/sccm/core/clients/manage/cmg/security-and-privacy-for-cloud-management-gateway) (Seguridad y privacidad para Cloud Management Gateway).


### <a name="do-i-need-to-maintain-the-azure-virtual-machines"></a>¿Es necesario mantener las máquinas virtuales de Azure?

No se requiere ningún mantenimiento. El diseño de Cloud Management Gateway usa PaaS (plataforma como servicio) de Azure. Mediante la suscripción que se proporciona, Configuration Manager crea las máquinas virtuales (VM) necesarias, el almacenamiento y las redes. Azure protege y actualiza la máquina virtual. Estas máquinas virtuales no forman parte del entorno local, como sucede con la infraestructura como servicio (IaaS). Cloud Management Gateway es una PaaS que extiende el entorno de Configuration Manager a la nube. 

### <a name="how-can-i-ensure-service-continuity-during-service-updates"></a>¿Cómo aseguro la continuidad del servicio durante las actualizaciones del servicio?

Al escalar CMG para incluir dos o más instancias, automáticamente se beneficia de dominios de actualización en Azure. Consulte [Actualización de un servicio en la nube](/azure/cloud-services/cloud-services-update-azure-service).


### <a name="im-already-using-ibcm-if-i-add-cmg-how-do-clients-behave"></a>Ya uso IBCM. Si agrego Cloud Management Gateway, ¿cómo se comportarán los clientes?

Si ya ha implementado la [administración de clientes basada en Internet](/sccm/core/clients/manage/plan-internet-based-client-management) (IBCM), también puede implementar Cloud Management Gateway. Los clientes reciben la directiva para ambos servicios. A medida que se mueven hacia Internet, seleccionan y usan de manera aleatoria uno de estos servicios basados en Internet.


### <a name="do-the-user-accounts-have-to-be-in-the-same-azure-subscription-as-the-subscription-that-hosts-the-cmg-cloud-service"></a>¿Las cuentas de usuario deben formar parte de la misma suscripción de Azure que la suscripción que hospeda el servicio en la nube de CMG?
<!--SCCMDocs-pr issue #2873--> Si el entorno tiene más de una suscripción, puede implementar CMG en cualquier suscripción que pueda hospedar los servicios de nube de Azure. 

Esta pregunta es habitual en los escenarios siguientes:  

- Si dispone de diferentes entornos de prueba y producción de Active Directory y Azure AD, pero una única suscripción de hospedaje de Azure.  

- Su uso de Azure ha crecido orgánicamente en equipos diferentes.  

Si usa una implementación de Resource Manager, incorpore el inquilino de Azure AD asociado. Esta conexión permite a Configuration Manager autenticarse en Azure para crear, implementar y administrar la instancia de CMG.  

Si está usando una autenticación de Azure AD para los usuarios y dispositivos administrados a través de CMG, incorpore ese inquilino de Azure AD. Para obtener más información sobre los servicios de Azure para la administración en la nube, vea [Configuración de servicios de Azure](/sccm/core/servers/deploy/configure/azure-services-wizard). Al incorporar cada inquilino de Azure AD, una sola instancia de CMG puede proporcionar autenticación de Azure AD para varios inquilinos, independientemente de la ubicación del hospedaje.



## <a name="next-steps"></a>Pasos siguientes

- [Planear puerta de enlace de administración en la nube](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)
- [Configurar puerta de enlace de administración en la nube](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)
- [Certificados para la puerta de enlace de administración en la nube](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway)
- [Seguridad y privacidad de la puerta de enlace de administración en la nube](/sccm/core/clients/manage/cmg/security-and-privacy-for-cloud-management-gateway)
- [Números de tamaño y escala de System Center Configuration Manager](/sccm/core/plan-design/configs/size-and-scale-numbers#bkmk_cmg)
