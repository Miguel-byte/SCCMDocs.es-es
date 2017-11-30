---
title: "Introducción a los certificados CNG"
titleSuffix: Configuration Manager
description: "Artículo de introducción a los certificados CNG en Configuration Manager"
ms.custom: na
ms.date: 11/20/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 
author: vhorne
ms.author: victorh
manager: angrobe
ms.openlocfilehash: f5f5138270d4f14b76b2c41e41ec034a0c12a932
ms.sourcegitcommit: 12d0d53e47bbf1a0bbd85015b8404a44589d1e14
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="cng-certificates-overview"></a>Introducción a los certificados CNG
<!-- 1356191 --> 

Configuration Manager tiene compatibilidad limitada con certificados Cryptography: Next Generation (CNG). Los clientes de Configuration Manager pueden usar un certificado de autenticación del cliente PKI con clave privada en el proveedor de almacenamiento de claves (KSP) de CNG. Gracias a la compatibilidad con KSP, los clientes de Configuration Manager admiten una clave privada basada en hardware, como el KSP de TPM para los certificados de autenticación de cliente PKI.

## <a name="supported-scenarios"></a>Escenarios admitidos
Puede usar plantillas de certificado [Cryptography API: Next Generation (CNG)](https://msdn.microsoft.com/library/windows/desktop/bb204775.aspx) en los siguientes escenarios:

- Registro de cliente y comunicación con un punto de administración de HTTPS.   
- Distribución de software e implementación de aplicaciones con un punto de distribución de HTTPS.   
- Implementación de sistema operativo.  
- SDK de mensajería de cliente (con la actualización más reciente) y proxy de ISV.   
- Configuración de Cloud Management Gateway.  

> [!NOTE]
> CNG es compatible con Crypto API (CAPI). Los certificados CAPI siguen siendo compatibles, incluso cuando se habilita la compatibilidad con CNG en el cliente.

## <a name="unsupported-scenarios"></a>Escenarios no admitidos

Actualmente no se admiten los siguientes escenarios:

- El servicio web del catálogo de aplicaciones, el sitio web del catálogo de aplicaciones y los roles del punto de proxy de inscripción no funcionan cuando instalan en modo HTTPS con un certificado CNG enlazado al sitio web en Internet Information Services (IIS). El Centro de software no muestra como disponibles los paquetes y las aplicaciones que se implementan en recopilaciones de grupos de usuarios o de usuarios.

- El punto de migración de estado no funciona cuando se instala en modo HTTPS con un certificado CNG enlazado al sitio web en IIS.

- El uso de certificados CNG para crear un punto de distribución en la nube.

- La comunicación del módulo de directivas de NDES al punto de registro de certificado (CRP) no se realiza correctamente si el módulo de directivas de NDES está utilizando un certificado CNG para el certificado de autenticación del cliente.

- Si se especifica un certificado CNG, no se crean correctamente soportes físicos de arranque mediante el proceso de creación de soportes físicos de secuencia de tareas.

## <a name="to-use-cng-certificates"></a>Uso de los certificados CNG

Para usar certificados CNG, la entidad de certificación (CA) debe proporcionar plantillas de certificado CNG para las máquinas de destino. Los detalles de la plantilla varían según el escenario; sin embargo, se requieren las siguientes propiedades:

- Pestaña **Compatibilidad**

    - La **entidad de certificación** debe ser Windows Server 2008 o posterior. (Se recomienda Windows Server 2012).

    - El **destinatario del certificado** debe ser Windows Vista o Server 2008 o posterior. (Se recomienda Windows 8/Windows Server 2012).

- Pestaña **Criptografía**

    - La **categoría del proveedor** debe ser **Proveedor de almacenamiento de claves**. (obligatorio)

> [!NOTE]
> Los requisitos para su entorno u organización pueden ser diferentes. Póngase en contacto con su experto PKI. Hay que tener en cuenta un punto importante: una plantilla de certificado debe usar un proveedor de almacenamiento de claves para utilizar CNG.

Para obtener mejores resultados, se recomienda crear el nombre del sujeto a partir de la información de Active Directory. Use el nombre de DNS como **formato de nombre de sujeto** e inclúyalo en el nombre de sujeto alternativo. De lo contrario, tendrá que proporcionar esta información cuando el dispositivo se inscriba en el perfil de certificado.