---
title: Administración conjunta para dispositivos de Windows 10
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo administrar simultáneamente dispositivos Windows 10 mediante Configuration Manager y Microsoft Intune.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 08/01/2019
ms.topic: overview
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: d6bbc787-83a5-44b4-ad64-016e5da7413f
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3710cc7178020af1d03bfd02953e2a2f3ed64f26
ms.sourcegitcommit: 16dd488c51b5cf01a7dd4204f7d40ee9ae0abe85
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/02/2019
ms.locfileid: "68743622"
---
# <a name="what-is-co-management"></a>¿Qué es administración conjunta?

<!-- 1350871 -->
La administración conjunta es una de las principales formas de asociar la implementación existente de Configuration Manager a la nube de Microsoft 365. Permite desbloquear funcionalidades adicionales de la nube, como el acceso condicional.

La administración conjunta permite administrar simultáneamente dispositivos Windows 10 mediante Configuration Manager y Microsoft Intune. Permite asociar a la nube su inversión existente en Configuration Manager mediante la incorporación de nuevas funcionalidades. Con la administración conjunta, tiene la flexibilidad para usar la solución tecnológica que mejor funciona para su organización.

Cuando un dispositivo Windows 10 tiene el cliente de Configuration Manager y está inscrito en Intune, el usuario recibe las ventajas de ambos servicios. El usuario controla para qué cargas de trabajo, si corresponde, cambia la entidad desde Configuration Manager a Intune. Configuration Manager sigue administrando todas las demás cargas de trabajo, incluidas las que no cambia a Intune, y todas las demás características de Configuration Manager que no admite la administración conjunta.

También podemos realizar un piloto en una carga de trabajo con una req de dispositivos independiente. El piloto permite probar la funcionalidad de Intune con un subconjunto de dispositivos antes de cambiar a un grupo más grande.

![Diagrama de información general de administración conjunta](media/co-management-overview.svg)

[Ver el diagrama en tamaño completo](media/co-management-overview.svg)

> [!Note]  
> Al administrar simultáneamente dispositivos Windows 10 mediante Configuration Manager y Microsoft Intune, esta configuración se denomina *administración conjunta*. Al administrar dispositivos con Configuration Manager e inscribirse a un servicio de MDM de terceros, esta configuración se denomina *coexistencia*. Tener dos autoridades de administración para un único dispositivo puede ser complicado si no hay una orquestación correcta entre los dos. Con la administración conjunta, Configuration Manager e Intune equilibran las [cargas de trabajo](#workloads) para asegurarse de que no hay ningún conflicto. Esta interacción no existe con los servicios de terceros, por lo que hay limitaciones con las funcionalidades de administración de coexistencia. Para más información, vea [Coexistencia de MDM de terceros con Configuration Manager](/sccm/comanage/coexistence).


## <a name="paths-to-co-management"></a>Rutas hacia la administración conjunta

Hay dos formas de conseguir la administración conjunta:  

- **Clientes de Configuration Manager existentes**: tiene dispositivos Windows 10 que ya son clientes de Configuration Manager. Puede configurar Azure AD híbrido e inscribirlos en Intune.  

- **Nuevos dispositivos basados en Internet**: tiene dispositivos Windows 10 nuevos que se unen a Azure AD y se inscriben automáticamente en Intune. Puede instalar el cliente de Configuration Manager para alcanzar un estado de administración conjunta.  

Para más información sobre las rutas de acceso, consulte [Rutas hacia la administración conjunta](/sccm/comanage/quickstart-paths).



## <a name="benefits"></a>Ventajas

Cuando inscribe los clientes de Configuration Manager en la administración conjunta, obtiene el valor inmediato siguiente:  

- Acceso condicional con cumplimiento de dispositivos  

- Acciones remotas basadas en Intune, por ejemplo: reinicio, control remoto o restablecimiento de fábrica

- Visibilidad centralizada del estado del dispositivo  

- Vínculo de usuarios, dispositivos y aplicaciones con Azure Active Directory (Azure AD)  

- Aprovisionamiento moderno con Windows Autopilot  

- Acciones remotas

Para más información sobre este valor inmediato gracias a la administración conjunta, consulte la serie de inicios rápidos para la [conexión de la nube con administración conjunta](/sccm/comanage/quickstarts).

La administración conjunta también permite coordinar varias cargas de trabajo con Intune. Para más información, consulte la sección [Cargas de trabajo](#workloads).



## <a name="prerequisites"></a>Requisitos previos

La administración conjunta tiene estos requisitos previos en las áreas siguientes:

- [Licencias](#licensing)  
- [Configuration Manager](#configuration-manager)  
- [Azure Active Directory](#azure-ad) (Azure AD)  
- [Microsoft Intune](#intune)  
- [Windows 10](#windows-10)  
- [Permisos y roles](#permissions-and-roles)  

### <a name="licensing"></a>Licencias

- Azure AD Premium
- Licencia de EMS o de Intune para todos los usuarios  

    > [!Note]  
    > Una suscripción a Enterprise Mobility + Security (EMS) incluye Azure Active Directory Premium y Microsoft Intune.

> [!Tip]  
> Asegúrese de asignar una licencia de Intune a la cuenta que usa para iniciar sesión en el inquilino. De lo contrario, no se podrá iniciar sesión y aparecerá el mensaje de error "Usuario no reconocido".  


### <a name="configuration-manager"></a>Configuration Manager

La administración conjunta requiere la versión 1710 o posterior de Configuration Manager.

A partir de la versión 1806 de Configuration Manager, puede conectar varias instancias de Configuration Manager a un inquilino de Intune único. <!--1357944-->  

Habilitar la administración conjunta no requiere que incorpore su sitio con Azure AD. Para el [segundo escenario de ruta](#paths-to-co-management), los clientes de Configuration Manager basados en Internet requieren [Cloud Management Gateway](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway) (CMG). CMG requiere que el sitio esté [incorporado en Azure AD para la administración en la nube](/sccm/core/servers/deploy/configure/azure-services-wizard). 


### <a name="azure-ad"></a>Azure AD

- Los dispositivos Windows 10 deben estar unidos a Azure AD. Pueden ser cualquiera de los siguientes tipos:  

    - [Unido a Azure AD híbrido](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan), en el que el dispositivo está unido a Active Directory local y registrado con Azure Active Directory.  

    - Solo [Unido a Azure AD](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan). (Este tipo se conoce a veces como "unido al dominio en la nube")<!--SCCMDocs issue 605-->  


### <a name="intune"></a>Intune

- [Configurar Intune](https://docs.microsoft.com/intune/setup-steps)  

- [Habilitar la inscripción automática de Windows 10](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment)  

> [!Note]  
> Si tiene un entorno de MDM híbrido (Intune integrado con Configuration Manager), no puede habilitar la administración conjunta. Sin embargo, puede iniciar la migración de los usuarios a Intune independiente y, después, habilitar sus dispositivos Windows 10 asociados para la administración conjunta. Si quiere saber más sobre la migración a Intune independiente, vea [Iniciar la migración de MDM híbrida a Intune independiente](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa).  
>
> Si usa una [entidad mixta](/sccm/mdm/deploy-use/migrate-mixed-authority), primero lleve a cabo la migración independiente a Intune. Después, establezca la entidad de MDM en Intune antes de configurar la administración conjunta.<!--SCCMDocs issue #797-->


### <a name="windows-10"></a>Windows 10

Actualice los dispositivos a Windows 10, versión 1709 o posterior. Para más información, consulte el artículo sobre la [adopción de Windows como servicio](/sccm/core/understand/configuration-manager-and-windows-as-service#key-articles-about-adopting-windows-as-a-service).

> [!IMPORTANT]
> Los dispositivos móviles con Windows 10 no admiten la administración conjunta.


### <a name="permissions-and-roles"></a>Permisos y roles

<!--SCCMDocs issue #667-->
| Acción | Rol necesario |
|----|----|
| Supervisar la puerta de enlace de administración en la nube en Configuration Manager | **Administrador de suscripción** de Azure |
| Crear aplicaciones de Azure AD desde Configuration Manager | **Administrador global** de Azure AD |
| Importar aplicaciones de Azure en Configuration Manager | **Administrador total** de Configuration Manager<br>No se necesitan roles adicionales de Azure |
| Habilitación de la administración conjunta en Configuration Manager | Un usuario de Azure AD<br>**Administrador total** de Configuration Manager con **todos** los derechos de ámbito.<!--SCCMDoc issue 626--> |

Para obtener más información sobre los roles de Azure, vea [Entender los distintos roles](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles).

Para más información sobre los roles de Configuration Manager, consulte [Conceptos básicos de la administración basada en roles](/sccm/core/understand/fundamentals-of-role-based-administration).


## <a name="workloads"></a>Cargas de trabajo

No es necesario que cambie las cargas de trabajo o puede cambiarlas individualmente cuando esté preparado. Configuration Manager sigue administrando todas las demás cargas de trabajo, incluidas las que no cambia a Intune, y todas las demás características de Configuration Manager que no admite la administración conjunta.

La administración conjunta admite estas cargas de trabajo:

- Directivas de cumplimiento  

- Directivas de Windows Update  

- Directivas de acceso a recursos  

- Endpoint Protection  

- Configuración del dispositivo  

- Aplicaciones hacer clic y ejecutar de Office  

- Aplicaciones cliente  

Para más información, consulte [Cargas de trabajo](/sccm/comanage/workloads).



## <a name="monitor-co-management"></a>Supervisión de la administración conjunta

El panel de administración conjunta le ayudará a revisar las máquinas que se administran conjuntamente en el entorno. Los gráficos ayudan a identificar los dispositivos que podrían requerir atención.

![Captura de pantalla del panel de administración conjunta](media/co-management-dashboard.png)

Para más información, consulte [cómo supervisar la administración conjunta](/sccm/comanage/how-to-monitor).



## <a name="next-steps"></a>Pasos siguientes

- [Obtenga más información sobre el valor inmediato y empiece a trabajar con la administración conjunta](/sccm/comanage/quickstarts)  

- [Tutorial: Habilitación de la administración conjunta para clientes existentes de Configuration Manager](/sccm/comanage/tutorial-co-manage-clients)  
