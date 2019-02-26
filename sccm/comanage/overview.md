---
title: Administración conjunta para dispositivos de Windows 10
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo administrar simultáneamente dispositivos Windows 10 mediante Configuration Manager y Microsoft Intune.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 01/14/2019
ms.topic: overview
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: d6bbc787-83a5-44b4-ad64-016e5da7413f
ms.collection: M365-identity-device-management
ms.openlocfilehash: c88bf98e035499c271de8acf9d8fa222e5058447
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56755576"
---
# <a name="what-is-co-management"></a>¿Qué es administración conjunta?

<!-- 1350871 --> Administración conjunta es una de las principales formas para asociar la implementación existente de Configuration Manager a la nube de Microsoft 365. Le ayuda a desbloquear capacidades adicionales basadas en la nube, como el acceso condicional. 

Administración conjunta le permite administrar simultáneamente dispositivos Windows 10 mediante Configuration Manager y Microsoft Intune. Le permite adjuntar en la nube su inversión existente en Configuration Manager mediante la adición de nuevas funcionalidades. Mediante el uso de administración conjunta, tiene la flexibilidad de usar la solución de tecnología que funciona mejor para su organización. 

Cuando un dispositivo Windows 10 tiene el cliente de Configuration Manager y se inscribe en Intune, obtenga las ventajas de ambos servicios. Controlar qué cargas de trabajo, si existe, que cambia la entidad de Configuration Manager a Intune. Configuration Manager sigue administrando todas las otras cargas de trabajo, incluidas las cargas de trabajo que no cambie a Intune y no es compatible con todas las demás características de Configuration Manager que la administración conjunta.

También podemos definir un programa piloto de una carga de trabajo con una colección independiente de dispositivos. Proyectos piloto le permite probar la funcionalidad de Intune con un subconjunto de los dispositivos antes de cambiar un grupo más grande. 

![Diagrama de información general de la administración conjunta](media/co-management-overview.png)



## <a name="paths-to-co-management"></a>Rutas hacia la administración conjunta

Hay dos formas de conseguir la administración conjunta:  

- **Los clientes de Configuration Manager existentes**: Tener dispositivos Windows 10 que ya son clientes de Configuration Manager. Configurar Azure AD híbrido e inscribirlos en Intune.  

- **Nuevos dispositivos basados en internet**: Tiene nuevos dispositivos Windows 10 que unirse a Azure AD e inscribirán automáticamente a Intune. Instalar el cliente de Configuration Manager para llegar a un estado de administración conjunta.  

Para obtener más información sobre las rutas de acceso, consulte [rutas de acceso a la administración conjunta](/sccm/comanage/quickstart-paths).



## <a name="benefits"></a>Ventajas 

Cuando se inscriben a los clientes de Configuration Manager existentes en la administración conjunta, obtendrá el siguiente valor inmediato:  

- Acceso condicional con cumplimiento de dispositivos  

- Acciones remotas basadas en Intune, por ejemplo: reinicio, control remoto o restablecimiento de fábrica

- Visibilidad centralizada del estado del dispositivo  

- Vincular usuarios, dispositivos y aplicaciones con Azure Active Directory (Azure AD)  

- Moderno de aprovisionamiento con Windows Autopilot  

- Acciones remotas

Para obtener más información sobre este valor inmediato de la administración conjunta, vea la serie de guías de inicio rápido para [en la nube conectarse con la administración conjunta](/sccm/comanage/quickstarts).

Administración conjunta permite coordinar con Intune para varias cargas de trabajo. Para obtener más información, consulte el [cargas de trabajo](#workloads) sección. 



## <a name="prerequisites"></a>Requisitos previos

Administración conjunta tiene estos requisitos previos en las áreas siguientes:

- [Las licencias](#licensing)  
- [Configuration Manager](#configuration-manager)  
- [Azure Active Directory](#azure-ad) (Azure AD)  
- [Microsoft Intune](#intune)  
- [Windows 10](#windows-10)  
- [Roles y permisos](#permissions-and-roles)  

### <a name="licensing"></a>Licencias

- Azure AD Premium 
- Licencia de EMS o de Intune para todos los usuarios  

    > [!Note]  
    > Un Enterprise Mobility + Security (EMS de) la suscripción incluye Azure Active Directory Premium y Microsoft Intune.

> [!Tip]  
> Asegúrese de que se asigne una licencia de Intune a la cuenta que usas para iniciar sesión en su inquilino. En caso contrario, inicie sesión se produce un error con el mensaje de error "El usuario no reconocido".  


### <a name="configuration-manager"></a>Configuration Manager

Administración conjunta requiere Configuration Manager versión 1710 o posterior.

A partir de Configuration Manager versión 1806, puede conectar varias instancias de Configuration Manager a un único inquilino de Intune. <!--1357944-->  

Habilitar la administración conjunta propio no requiere que se incorpore su sitio con Azure AD. Para el [segundo escenario de ruta de acceso](#paths-to-co-management), los clientes basados en internet de Configuration Manager requieren la [CMG](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway) (CMG). La instancia de CMG requiere que el sitio es [incorporada a Azure AD para la administración en la nube](/sccm/core/servers/deploy/configure/azure-services-wizard). 


### <a name="azure-ad"></a>Azure AD

- Los dispositivos Windows 10 deben estar unidos a Azure AD. Pueden ser cualquiera de los siguientes tipos:  

    - [Unido a Azure AD híbrido](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan), en el que el dispositivo está unido a Active Directory local y registrado con Azure Active Directory.  

    - Solo [Unido a Azure AD](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan). (Este tipo se conoce a veces como "unido al dominio en la nube")<!--SCCMDocs issue 605-->  


### <a name="intune"></a>Intune

- [Configurar Intune](https://docs.microsoft.com/intune/setup-steps)  

- [Habilitar la inscripción automática de Windows 10](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment)  

> [!Note]  
> Si tiene un entorno de MDM híbrido (Intune integrado con Configuration Manager), no puede habilitar la administración conjunta. Sin embargo, puede iniciar la migración de los usuarios a Intune independiente y, después, habilitar sus dispositivos Windows 10 asociados para la administración conjunta. Si quiere saber más sobre la migración a Intune independiente, vea [Iniciar la migración de MDM híbrida a Intune independiente](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa).  
> 
> Si usa una [entidad mixta](/sccm/mdm/deploy-use/migrate-mixed-authority), primero lleve a cabo la migración independiente a Intune. Después, establezca la entidad de MDM en Intune antes de configurar la administración conjunta.<!--SCCMDocs issue #797-->


### <a name="windows-10"></a>Windows 10

Actualice los dispositivos Windows 10, versión 1709 o posterior. Para obtener más información, consulte [adopción de Windows como servicio](/sccm/core/understand/configuration-manager-and-windows-as-service#key-articles-about-adopting-windows-as-a-service).

> [!IMPORTANT]
> Los dispositivos móviles de Windows 10 no admiten la administración conjunta.


### <a name="permissions-and-roles"></a>Roles y permisos
<!--SCCMDocs issue #667-->

| Acción | Rol necesario |
|----|----|
| Configurar una puerta de enlace de administración en la nube en Configuration Manager | Azure **Administrador de suscripciones** |
| Crear aplicaciones de Azure AD desde Configuration Manager | Azure AD **administrador Global** |
| Importar aplicaciones de Azure en Configuration Manager | Administrador de configuración **Administrador total**<br>No hay roles de Azure adicionales necesarios |
| Habilitar la administración conjunta en Configuration Manager | Un usuario de Azure AD<br>Administrador de configuración **Administrador total** con **todas** derechos de ámbito.<!--SCCMDoc issue 626--> | 

Para obtener más información sobre los roles de Azure, vea [Entender los distintos roles](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles).

Para obtener más información acerca de los roles de administrador de configuración, consulte [aspectos básicos de la administración basada en roles](/sccm/core/understand/fundamentals-of-role-based-administration).


## <a name="workloads"></a>Cargas de trabajo 

No tiene que cambiar las cargas de trabajo, o puede realizarlas por separado cuando esté listo. Configuration Manager sigue administrando todas las otras cargas de trabajo, incluidas las cargas de trabajo que no cambie a Intune y no es compatible con todas las demás características de Configuration Manager que la administración conjunta.

Administración conjunta es compatible con las cargas de trabajo siguientes:

- Directivas de cumplimiento  

- Directivas de Windows Update  

- Directivas de acceso a recursos  

- Endpoint Protection  

- Configuración del dispositivo  

- Aplicaciones hacer clic y ejecutar de Office  

- Aplicaciones cliente  

Para obtener más información, consulte [cargas de trabajo](/sccm/comanage/workloads).



## <a name="monitor-co-management"></a>Supervisión de la administración conjunta

El panel de administración conjunta le ayudará a revisar las máquinas que se administran conjuntamente en su entorno. Los gráficos ayudan a identificar los dispositivos que podrían requerir atención.

![Captura de pantalla del panel de administración conjunta](media/co-management-dashboard.png)

Para obtener más información, consulte [cómo supervisar la administración conjunta](/sccm/comanage/how-to-monitor).



## <a name="next-steps"></a>Pasos siguientes

- [Más información sobre el valor inmediato e Introducción a administración conjunta](/sccm/comanage/quickstarts)  

- [Tutorial: Habilitar la administración conjunta para los clientes existentes de Configuration Manager](/sccm/comanage/tutorial-co-manage-clients)  

