---
title: Rutas hacia la administración conjunta
titleSuffix: Configuration Manager
description: Conozca los requisitos previos de las dos principales maneras de configurar la administración conjunta.
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 5beb5564-2fdf-4f0a-8801-d0cec8214c43
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 803f05dd14da8d280f08f2bcf3608865f384d273
ms.sourcegitcommit: 9aebc20b25cdef0af908918ccfd791f3264a5d94
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "56755538"
---
# <a name="paths-to-co-management"></a>Rutas hacia la administración conjunta

Hay dos maneras principales de configurar la administración conjunta. Es importante entender los requisitos previos de cada ruta. Cada una de ellas requiere una combinación de Azure Active Directory (Azure AD), Configuration Manager, Microsoft Intune y Windows 10. 

1. [Inscripción automática de dispositivos administrados de Configuration Manager en Intune](#bkmk_path1)  
2. [Arranque del cliente de Configuration Manager con aprovisionamiento moderno](#bkmk_path2)  

![Diagramas de las rutas de administración conjunta](media/co-management-paths.png)



## <a name="bkmk_path1"></a> Ruta 1: inscripción automática de clientes existentes

Si toma esta ruta, puede inscribir rápidamente sus dispositivos existentes administrados por Configuration Manager en Intune. La administración de estos dispositivos desde Configuration Manager no es distinta de cómo era antes de habilitar la administración conjunta. Ahora recibirá todas las ventajas basadas en la nube. Esta ruta es transparente para los usuarios.

Tendrá que configurar lo siguiente:
- Azure AD híbrido
    - Servicios de federación de Active Directory (AD FS) con la autenticación de paso a través (PTA)
    - Azure AD Connect
    - Licencia de Azure AD Premium
    - Configure la unión a Azure AD híbrido (elija una opción):
        - Para dominios administrados
        - Para dominios federados
- Configuración del agente cliente para la unión a Azure AD híbrido
- Configuración de la inscripción automática de dispositivos en Intune
- Asignación de licencias de usuario de Intune
- Habilitación de la administración conjunta en Configuration Manager

Para ver un tutorial sobre esta ruta, consulte [Tutorial: Habilitación de la administración conjunta para clientes existentes de Configuration Manager](/sccm/comanage/tutorial-co-manage-clients).



## <a name="bkmk_path2"></a> Ruta 2: arranque con aprovisionamiento moderno

Tendrá que configurar lo siguiente:

1. [Configuración de HTTP mejorado](/sccm/core/plan-design/hierarchy/enhanced-http)  
2. [Creación de los servicios en la nube en Azure](/sccm/core/servers/deploy/configure/azure-services-wizard)  
3. [Configuración del punto de administración y los clientes para usar Cloud Management Gateway](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)  
4. [Uso de Intune para implementar el cliente de Configuration Manager](/sccm/comanage/how-to-prepare-win10)  

> [!Note]  
> Próximamente habrá disponible un tutorial para esta ruta.

