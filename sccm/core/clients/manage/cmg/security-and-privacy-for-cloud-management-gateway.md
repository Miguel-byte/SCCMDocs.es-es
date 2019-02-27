---
title: Seguridad y privacidad de CMG
description: Obtenga información sobre instrucciones y recomendaciones de seguridad y privacidad con Cloud Management Gateway.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/22/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 7304730b-b517-4c76-aadd-4cbd157dc971
ms.collection: M365-identity-device-management
ms.openlocfilehash: 013d00fd7c207df45b0f6b7910283c3e8b60b44d
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56137177"
---
# <a name="security-and-privacy-for-the-cloud-management-gateway"></a>Seguridad y privacidad de Cloud Management Gateway

*Se aplica a: System Center Configuration Manager (Rama actual)*

En este artículo se incluye información de seguridad y privacidad para Cloud Management Gateway (CMG) de Configuration Manager. Para obtener más información, consulte [Plan for cloud management gateway (Plan para la puerta de enlace de administración en la nube)](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway).

## <a name="cmg-security-details"></a>Detalles de seguridad de CMG
- La instancia de CMG acepta y administra las conexiones desde puntos de conexión de CMG. Usa la autenticación mutua SSL mediante identificadores de conexión y certificados.
- La instancia de CMG acepta y reenvía las solicitudes de cliente mediante los métodos siguientes:
    - Autentica previamente las conexiones mediante el sistema mutuo de SSL con el certificado de autenticación de cliente basado en PKI o Azure AD. 
      - En las instancias de máquina virtual de CMG, IIS comprueba la ruta de acceso del certificado en función de los certificados raíz de confianza que se cargan en la instancia de CMG.
      - IIS en la instancia de máquina virtual también comprueba la revocación de certificados de cliente, si está habilitada. Para obtener más información, vea [Publicar la lista de revocación de certificados](#bkmk_crl).
    - La lista de confianza de certificados comprueba la raíz del certificado de autenticación del cliente. También realiza la misma validación que el punto de administración para el cliente. Para obtener más información, vea [Revisar las entradas en la lista de confianza de certificados del sitio](#bkmk_ctl).
    - Valida y filtra las solicitudes de cliente (direcciones URL) para comprobar si algún punto de conexión de CMG puede atender la solicitud.  
    - Comprueba la longitud de contenido para cada punto de conexión de publicación.
    - Usa comportamiento "round-robin" para equilibrar la carga de los puntos de conexión de CMG en el mismo sitio.
- En el punto de conexión de CMG se usan los métodos siguientes:
    - Crea conexiones HTTPS/TCP coherentes a todas las instancias de máquina virtual de la instancia de CMG. Comprueba y mantiene estas conexiones cada minuto.
    - Usa la autenticación mutua SSL con la instancia de CMG mediante certificados.
    - Reenvía las solicitudes cliente en función de asignaciones de direcciones URL.
    - Notifica el estado de conexión para mostrar el estado de mantenimiento del servicio en la consola.
    - Notifica el tráfico para cada punto de conexión cada cinco minutos.

### <a name="configuration-manager-client-facing-roles"></a>Funciones para el cliente de Configuration Manager
El punto de administración y el punto de actualización de software hospedan puntos de conexión en IIS para atender las solicitudes de cliente. La instancia de CMG no expone todos los puntos de conexión internos. Cada punto de conexión publicado en CMG tiene una asignación de dirección URL.
  - La dirección URL externa es la que el cliente utiliza para comunicarse con CMG.
  - La dirección URL interna es el punto de conexión de CMG utilizado para reenviar las solicitudes al servidor interno.

#### <a name="url-mapping-example"></a>Ejemplo de asignación de dirección URL
Al habilitar el tráfico de CMG en un punto de administración, Configuration Manager crea un conjunto interno de asignaciones de direcciones URL para cada servidor de punto de administración. Por ejemplo: ccm_system, ccm_incoming y sms_mp. La dirección URL externa para el punto de administración ccm_system del punto de administración tendría este aspecto:  
`https://<CMG service name>/CCM_Proxy_MutualAuth/<MP Role ID>/CCM_System`  
La dirección URL es única para cada punto de administración. Después, el cliente de Configuration Manager pone el nombre del punto de administración habilitado para CMG en su lista de puntos de administración de Internet. Este nombre tiene el aspecto siguiente:  
`<CMG service name>/CCM_Proxy_MutualAuth/<MP Role ID>`  
El sitio carga automáticamente todas las direcciones URL externas publicadas en la instancia de CMG. Este comportamiento permite que la instancia de CMG realice el filtrado de direcciones URL. Todas las asignaciones de direcciones URL se replican en el punto de conexión de CMG. Después, reenvía la comunicación a los servidores internos según la dirección URL externa de la solicitud de cliente.



## <a name="security-guidance-for-cmg"></a>Directrices de seguridad para CMG


<a name="bkmk_crl"></a>

### <a name="publish-the-certificate-revocation-list"></a>Publicar la lista de revocación de certificados

Publique la lista de revocación de certificados (CRL) de la PKI para que los clientes basados en Internet tengan acceso. Al implementar una instancia de CMG mediante PKI, configure el servicio para **comprobar la revocación del certificado de cliente** en la pestaña Configuración. Esta opción configura el servicio para usar una lista de revocación de certificados (CRL) publicada. Para obtener más información, vea [Planear la revocación de certificados PKI](/sccm/core/plan-design/security/plan-for-security#BKMK_PlanningForCRLs).



<a name="bkmk_ctl"></a>

### <a name="review-entries-in-the-sites-certificate-trust-list"></a>Revisar las entradas en la lista de confianza de certificados del sitio
<!--503739--> Cada sitio de Configuration Manager incluye una lista de entidades de certificación raíz de confianza, la lista de certificados de confianza (CTL). Para ver y modificar la lista, vaya al área de trabajo Administración, expanda Configuración del sitio y haga clic en Sitios. Seleccione un sitio y haga clic en Propiedades en la cinta. Cambie a la pestaña Comunicación de equipo cliente y, después, haga clic en **Establecer** en Entidades de certificación raíz de confianza.
 
Use una CTL más restrictiva para un sitio con una instancia de CMG mediante la autenticación de cliente de PKI. En caso contrario, los clientes con certificados de autenticación de cliente emitidos por cualquier raíz de confianza que ya existe en el punto de administración se aceptan automáticamente para el registro de cliente.

Este subconjunto ofrece a los administradores mayor control sobre la seguridad. La CTL limita el servidor para que solo se acepten los certificados de cliente emitidos por las entidades de certificación de la CTL. Por ejemplo, Windows se comercializa con varios certificados de conocidas entidades de certificación (CA) de terceros, como VeriSign y Thawte. De forma predeterminada, el equipo que ejecuta IIS confía en los certificados vinculados a estas entidades de certificación conocidas. Si no se configura IIS con una CTL, cualquier equipo que tenga un certificado de cliente emitido por estas entidades de certificación se aceptará como un cliente válido de Configuration Manager. Si se configura IIS con una CTL que no incluya estas entidades de certificación, se rechazarán las conexiones de cliente si el certificado está vinculado a estas entidades de certificación. 


<!--486209-->


<!-- ## Privacy information for CMG -->


## <a name="next-steps"></a>Pasos siguientes

- [Planear puerta de enlace de administración en la nube](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)
- [Configurar puerta de enlace de administración en la nube](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)
- [Preguntas más frecuentes sobre Cloud Management Gateway](/sccm/core/clients/manage/cmg/cloud-management-gateway-faq)
- [Certificados para la puerta de enlace de administración en la nube](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway)
