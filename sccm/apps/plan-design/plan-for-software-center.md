---
title: Planeamiento del centro de software
titleSuffix: Configuration Manager
description: Decida cómo quiere configurar y personalizar la marca del Centro de software para que los usuarios interactúen con Configuration Manager.
ms.date: 05/01/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: c6826794-aa19-469d-ae47-1a0db68a1ff1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 50683b43cff113f7cd77efb5d8798fd24b53f90a
ms.sourcegitcommit: 2db6863c6740380478a4a8beb74f03b8178280ba
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 05/06/2019
ms.locfileid: "65106524"
---
# <a name="plan-for-software-center"></a>Planeamiento del centro de software

*Se aplica a: System Center Configuration Manager (Rama actual)*

Los usuarios cambian la configuración y buscan e instalan aplicaciones desde el Centro de software. Cuando se instala el cliente de Configuration Manager en un dispositivo de Windows, se instala automáticamente también el Centro de software. El nuevo Centro de software tiene un aspecto moderno. Las aplicaciones que solo se hubiesen mostrado en el catálogo de aplicaciones que depende de Silverlight (aplicaciones disponibles para el usuario) ahora se muestran en la pestaña **Aplicaciones** del Centro de software.

Para obtener más información sobre otras características del Centro de software, consulte el [Manual del usuario del Centro de software](/sccm/core/understand/software-center).  


## <a name="bkmk_userex"></a> Configurar el Centro de software  

Revise las mejoras generales en el Centro de software:

### <a name="starting-in-version-1802"></a>A partir de la versión 1802

- La configuración de cliente **Usar nuevo Centro de software** en el grupo **Agente de equipo** está habilitada de manera predeterminada. La versión anterior del Centro de software ya no se admite. Para más información, consulte [Características en desuso y eliminadas](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).  

- Los usuarios pueden examinar e instalar aplicaciones disponibles para el usuario desde dispositivos unidos a Azure Active Directory (Azure AD). Para obtener más información, vea cómo [implementar aplicaciones disponibles para el usuario en dispositivos unidos a Azure AD](/sccm/apps/deploy-use/deploy-applications#deploy-user-available-applications-on-azure-ad-joined-devices).  

### <a name="starting-in-version-1806"></a>A partir de la versión 1806

- Especifique la visibilidad del vínculo del sitio web del catálogo de aplicaciones en la pestaña **Estado de instalación** del Centro de software. Para obtener más información, vea la configuración de cliente del [Centro de software](/sccm/core/clients/deploy/about-client-settings#software-center).  

- Los roles del catálogo de aplicaciones ya no son necesarios para mostrar las aplicaciones disponibles para el usuario en el Centro de software. Este cambio ayuda a reducir la infraestructura de servidor necesaria para entregar las aplicaciones a los usuarios. El Centro de software se basa ahora en el punto de administración para obtener esta información, lo que facilita el escalado de los entornos de mayor tamaño al asignarlos a [grupos de límites](/sccm/core/servers/deploy/configure/boundary-groups#management-points).<!--1358309-->  

    > [!Note]  
    > Si está usando actualmente el catálogo de aplicaciones, y actualiza Configuration Manager a la versión 1806, este sigue funcionando. Los roles de punto de sitios web y punto de servicio web del catálogo de aplicaciones ya no son *necesarios*, aunque todavía son *compatibles*. La **experiencia de usuario de Silverlight** del *punto de sitios web* del catálogo de aplicaciones ya no se admite. Para más información, consulte [Características en desuso y eliminadas](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).
    >
    > Comience a planear la retirada de los roles del catálogo de aplicaciones de su infraestructura en el futuro. Aproveche las mejoras del Centro de software para usar el punto de administración y simplificar su entorno de Configuration Manager.  

Use la siguiente tabla para ayudar a comprender los requisitos para el Centro de software según la versión específica de Configuration Manager:

| Tipo de dispositivo | Versión del sitio | Infraestructura |
|-----------------|--------------|----------------|
| Dispositivo unido a Azure AD<br>(o "unido al dominio en la nube") | 1802 o 1806 | Punto de administración para todas las implementaciones de aplicación |
| Dispositivo [unido a Azure AD híbrido](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup) en Internet | 1802 o 1806 | Punto de administración y Cloud Management Gateway para todas las implementaciones de aplicaciones |
| Dispositivo unido a dominio de Active Directory local | 1802 | Catálogo de aplicaciones necesario para las aplicaciones disponibles para el usuario a través del Centro de software |
| Dispositivo unido a dominio de Active Directory local | 1806 | Punto de administración para todas las implementaciones de aplicación |

> [!Important]  
> Para aprovechar las nuevas características de Configuration Manager, primero actualice los clientes a la versión más reciente. Aunque la funcionalidad nueva aparece en la consola de Configuration Manager cuando se actualiza el sitio y la consola, la totalidad del escenario no es funcional hasta que la versión del cliente también es la más reciente.


## <a name="bkmk_impact"></a> Reemplazo de las notificaciones del sistema por una ventana de diálogo

<!--3555947-->
A veces los usuarios no ven la notificación del sistema de Windows sobre un reinicio o una implementación necesaria. Entonces no ven la experiencia de posponer el recordatorio. Este comportamiento puede conducir a una mala experiencia de usuario cuando el cliente llega a una fecha límite.

A partir de la versión 1902, cuando [se requieren cambios de software](#software-changes-are-required) o [es necesario reiniciar](#restart-required) las implementaciones, tiene la opción de usar una ventana de diálogo más intrusiva.

### <a name="software-changes-are-required"></a>Deben realizarse cambios en el software

Cuando [implemente una aplicación](/sccm/apps/deploy-use/deploy-applications) según sea necesario con una fecha límite en el futuro, en la página **Experiencia del usuario** del Asistente para implementar software, seleccione las siguientes opciones de notificación de usuario:

- **Mostrar en el Centro de software y mostrar todas las notificaciones**
- **Cuando se requieren cambios de software, mostrar al usuario una ventana de cuadro de diálogo en lugar de una notificación del sistema**.

La configuración de esta opción de implementación cambia la experiencia del usuario para este escenario.

Desde la notificación del sistema siguiente:

![Notificación del sistema de que se requieren cambios de software](media/3555947-required-toast.png)  

En la ventana de diálogo siguiente:

![Ventana de diálogo de cambios de software necesarios](media/3555947-required-dialog.png)


### <a name="restart-required"></a>Es necesario reiniciar

En el grupo de configuración del cliente [Reinicio de equipo](/sccm/core/clients/deploy/about-client-settings#computer-restart), habilite la siguiente opción: **Cuando una implementación requiere reiniciar, mostrar al usuario una ventana de cuadro de diálogo en lugar de una notificación del sistema**.  

Cuando se realiza esta configuración del cliente, cambia la experiencia de usuario en todas las implementaciones necesarias que requieren un reinicio de los siguientes tipos:

- [Aplicación](/sccm/apps/deploy-use/deploy-applications)
- [Secuencia de tareas](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS)
- [Actualización de software](/sccm/sum/deploy-use/deploy-software-updates)

Desde la notificación del sistema siguiente:

![Notificación del sistema de reinicio necesario](media/3555947-restart-toast.png)  

En la ventana de diálogo siguiente:

![Ventana de diálogo con el reinicio del equipo](media/3555947-restart-dialog.png)


## <a name="branding-software-center"></a>Personalización de la marca del Centro de software

Cambie la apariencia del Centro de software para cumplir con los requisitos de marca de su organización. Esta configuración ayuda a que los usuarios confíen en el Centro de software.

Configuration Manager aplica la personalización de marca para el Centro de Software según las prioridades siguientes:  

- Si no ha instalado el catálogo de aplicaciones (recomendado):  

    1. Configuración de cliente del **Centro de software**. Para más información, vea [Acerca de la configuración de cliente](/sccm/core/clients/deploy/about-client-settings#software-center).  

    2. Configuración de cliente del **Nombre de la organización** en el grupo **Agente de equipo**. Para más información, vea [Acerca de la configuración de cliente](/sccm/core/clients/deploy/about-client-settings#computer-agent).  

- Si ha instalado el catálogo de aplicaciones:  

    1. Configuración de cliente del **Centro de software**. Para más información, vea [Acerca de la configuración de cliente](/sccm/core/clients/deploy/about-client-settings#software-center).  

    2. Si conecta una suscripción de Microsoft Intune a Configuration Manager, el Centro de software muestra el *nombre de la organización*, el *color* y el *logotipo de la empresa* que especifique en las propiedades de la suscripción de Intune. Para más información, vea [Configuring the Microsoft Intune subscription (Configuración de la suscripción de Microsoft Intune)](/sccm/mdm/deploy-use/configure-intune-subscription).  

    3. El *nombre de organización* y el *color* que especifique en las propiedades de punto de sitios web del catálogo de aplicaciones. Para más información, vea [Configuration options for Application Catalog website point (Opciones de configuración del punto de sitios web del catálogo de aplicaciones)](/sccm/core/servers/deploy/configure/configuration-options-for-site-system-roles#BKMK_ApplicationCatalog_Website).  

    4. Configuración de cliente del **Nombre de la organización** en el grupo **Agente de equipo**. Para más información, vea [Acerca de la configuración de cliente](/sccm/core/clients/deploy/about-client-settings#computer-agent).  

### <a name="configure-software-center-branding"></a>Configuración de la marca del Centro de software

<!-- 1351224 -->
Incorpore elementos de personalización de marca de la organización y especifique la visibilidad de las pestañas para personalizar la apariencia del Centro de software.

Vea los siguientes artículos para más información:

- Grupo de configuración de cliente del [Centro de software](/sccm/core/clients/deploy/about-client-settings#software-center).  
- [Cómo establecer la configuración del cliente](/sccm/core/clients/deploy/configure-client-settings)  


## <a name="see-also"></a>Consulte también

- [Manual del usuario del Centro de software](/sccm/core/understand/software-center)
- [Planear y configurar la administración de aplicaciones en Configuration Manager](/sccm/apps/plan-design/plan-for-and-configure-application-management)
