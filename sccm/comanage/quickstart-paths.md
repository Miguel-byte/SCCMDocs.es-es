---
title: Rutas hacia la administración conjunta
titleSuffix: Configuration Manager
description: Comprender los requisitos previos para las dos formas principales para configurar la administración conjunta.
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
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56755538"
---
# <a name="paths-to-co-management"></a>Rutas hacia la administración conjunta

Hay dos métodos principales para configurar la administración conjunta. Es importante comprender los requisitos previos para cada ruta de acceso. Cada uno de ellos requieren una combinación de Azure Active Directory (Azure AD), Configuration Manager, Microsoft Intune y Windows 10. 

1. [La inscripción automática existentes de los dispositivos administrados por Configuration Manager en Intune](#bkmk_path1)  
2. [Arrancar al cliente de Configuration Manager con el aprovisionamiento moderna](#bkmk_path2)  

![Diagrama de rutas de acceso de administración conjunta](media/co-management-paths.png)



## <a name="bkmk_path1"></a> Ruta de acceso 1: Inscripción automática de los clientes existentes

Teniendo esta ruta de acceso puede obtener los dispositivos administrados por Configuration Manager existentes que rápidamente se inscribe en Intune. La administración de estos dispositivos de Configuration Manager no es diferente de antes de habilitar la administración conjunta. Ahora obtendrá todas las ventajas en la nube. Esta ruta de acceso es transparente para los usuarios.

Esto es lo necesita configurarlo:
- Azure AD híbrido
    - Servicios de federación de Active Directory (ADFS) con la autenticación de paso a través (PTA)
    - Azure AD Connect
    - Licencia de Azure AD Premium
    - Configurar híbrida de Azure AD join (elegir una opción):
        - Para los dominios administrados
        - Para los dominios federados
- Agente cliente de configuración híbrida de Azure AD join
- Configurar la inscripción automática de dispositivos a Intune
- Asignar licencias de usuario de Intune
- Habilitar la administración conjunta en Configuration Manager

Para ver un tutorial en esta ruta de acceso, consulte [Tutorial: Habilitar la administración conjunta para los clientes de Configuration Manager existentes](/sccm/comanage/tutorial-co-manage-clients).



## <a name="bkmk_path2"></a> Ruta de acceso 2: Arrancar con aprovisionamiento moderna

Esto es lo necesita configurarlo:

1. [El programa de instalación mejorada HTTP](/sccm/core/plan-design/hierarchy/enhanced-http)  
2. [Creación de los servicios en la nube en Azure](/sccm/core/servers/deploy/configure/azure-services-wizard)  
3. [Configurar el punto de administración y los clientes que usen cloud management gateway](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)  
4. [Usar Intune para implementar al cliente de Configuration Manager](/sccm/comanage/how-to-prepare-win10)  

> [!Note]  
> Un tutorial para esta ruta de acceso disponible próximamente.

