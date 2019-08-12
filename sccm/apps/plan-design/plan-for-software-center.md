---
title: Planeamiento del centro de software
titleSuffix: Configuration Manager
description: Decida cómo quiere configurar y personalizar la marca del Centro de software para que los usuarios interactúen con Configuration Manager.
ms.date: 08/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: c6826794-aa19-469d-ae47-1a0db68a1ff1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7fbd8f570fe0e6fad18b964220d5cb723e5fecad
ms.sourcegitcommit: c60fdfb9df107c430389b69b08f9670ce5f526c3
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/09/2019
ms.locfileid: "68859861"
---
# <a name="plan-for-software-center"></a>Planeamiento del centro de software

*Se aplica a: System Center Configuration Manager (Rama actual)*

Los usuarios cambian la configuración y buscan e instalan aplicaciones desde el Centro de software. Cuando se instala el cliente de Configuration Manager en un dispositivo de Windows, se instala automáticamente también el Centro de software.

Para obtener más información sobre otras características del Centro de software, consulte el [Manual del usuario del Centro de software](/sccm/core/understand/software-center).  

## <a name="bkmk_userex"></a> Configurar el Centro de software  

Actualice los sitios y clientes de Configuration Manager a la versión 1906 o posterior para beneficiarse de las mejoras más recientes.

Revise las mejoras generales en el Centro de software:

> [!Important]  
> Estas mejoras iterativas del Centro de software y el punto de administración son para retirar los roles de catálogo de aplicaciones.
>
> - La experiencia del usuario de Silverlight no se admite a partir de la versión 1806 de la rama actual.
> - A partir de la versión 1906, los clientes actualizados usan automáticamente el punto de administración para las implementaciones de aplicaciones disponibles para el usuario. Tampoco puede instalar nuevos roles del catálogo de aplicaciones.
> - En la primera versión de la rama actual después del 31 de octubre de 2019, finalizará el soporte técnico para los roles de catálogo de aplicaciones.  

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

### <a name="starting-in-version-1902"></a>A partir de la versión 1902

- Configure la afinidad entre usuario y dispositivo. Para obtener más información, vea [Vincular usuarios y dispositivos con la afinidad entre usuario y dispositivo](/sccm/apps/deploy-use/link-users-and-devices-with-user-device-affinity).

### <a name="starting-in-version-1906"></a>A partir de la versión 1906

- El Centro de software ahora se comunica con un punto de administración para las aplicaciones destinadas a los usuarios, si existen. Ya no usa el catálogo de aplicaciones. Este cambio facilita la eliminación del catálogo de aplicaciones del sitio.

- Anteriormente, el Centro de software elegía el primero punto de administración de la lista de servidores disponibles. A partir de esta versión, usa el mismo punto de administración que el cliente. Este cambio permite al Centro de software usar el mismo punto de administración del sitio primario asignado que el cliente.

- El punto de administración tiene puntos de conexión del centro de software para admitir estas nuevas características. Ahora comprueba el estado de estos puntos de conexión cada cinco minutos. Notifica los problemas a través de mensajes de estado para el componente de sitio SMS_MP_CONTROL_MANAGER.

- No se pueden agregar nuevos roles del catálogo de aplicaciones al sitio. Los roles existentes continúan funcionando. Solo los clientes existentes usan el catálogo de aplicaciones para las implementaciones disponibles para el usuario. Los clientes actualizados usan automáticamente el punto de administración para todas las implementaciones.

- Puede Agregar hasta 5 pestañas personalizadas al centro de software. Para obtener más información, vea [Acerca de la configuración de cliente](/sccm/core/clients/deploy/about-client-settings#software-center). <!--4063773-->

### <a name="summary-of-infrastructure-requirements-per-version"></a>Resumen de los requisitos de infraestructura por versión

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

> [!IMPORTANT]
> En Configuration Manager 1902, en determinadas circunstancias, el cuadro de diálogo no reemplazará las notificaciones del sistema. Para resolver este problema, instale el [paquete acumulativo de actualizaciones para Configuration Manager versión 1902](https://support.microsoft.com/help/4500571/update-rollup-for-configuration-manager-current-branch-1902). <!--4404715-->

## <a name="branding-software-center"></a>Personalización de la marca del Centro de software

Cambie la apariencia del Centro de software para cumplir con los requisitos de marca de su organización. Esta configuración ayuda a que los usuarios confíen en el Centro de software.

### <a name="configure-software-center-branding"></a>Configuración de la marca del Centro de software

<!-- 1351224 -->
Incorpore elementos de personalización de marca de la organización y especifique la visibilidad de las pestañas para personalizar la apariencia del Centro de software.

Vea los siguientes artículos para más información:

- Grupo de configuración de cliente del [Centro de software](/sccm/core/clients/deploy/about-client-settings#software-center).  
- [Cómo establecer la configuración del cliente](/sccm/core/clients/deploy/configure-client-settings)  

### <a name="branding-priorities"></a>Prioridades de personalización de marca

Configuration Manager aplica la personalización de marca para el Centro de Software según las prioridades siguientes:  

1. Configuración de cliente del **Centro de software**. Para más información, vea [Acerca de la configuración de cliente](/sccm/core/clients/deploy/about-client-settings#software-center).  

2. Configuración de cliente del **Nombre de la organización** en el grupo **Agente de equipo**. Para más información, vea [Acerca de la configuración de cliente](/sccm/core/clients/deploy/about-client-settings#computer-agent).  

#### <a name="application-catalog-branding-priorities"></a>Prioridades de personalización de marca del catálogo de aplicaciones

> [!Important]
> La experiencia del usuario de Silverlight del catálogo de aplicaciones no se admite a partir de la versión 1806 de la rama actual. A partir de la versión 1906, los clientes actualizados usan automáticamente el punto de administración para las implementaciones de aplicaciones disponibles para el usuario. Tampoco puede instalar nuevos roles del catálogo de aplicaciones. En la primera versión de la rama actual después del 31 de octubre de 2019, finalizará el soporte técnico para los roles de catálogo de aplicaciones.  

Si utiliza el catálogo de aplicaciones, la personalización de marca sigue estas prioridades:  

1. Configuración de cliente del **Centro de software**. Para más información, vea [Acerca de la configuración de cliente](/sccm/core/clients/deploy/about-client-settings#software-center).  

2. Si conecta una suscripción de Microsoft Intune a Configuration Manager, el Centro de software muestra el *nombre de la organización*, el *color* y el *logotipo de la empresa* que especifique en las propiedades de la suscripción de Intune. Para más información, vea [Configuring the Microsoft Intune subscription (Configuración de la suscripción de Microsoft Intune)](/sccm/mdm/deploy-use/configure-intune-subscription).  

    > [!Important]
    > La administración de dispositivos móviles es una [característica en desuso](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).

3. El *nombre de organización* y el *color* que especifique en las propiedades de punto de sitios web del catálogo de aplicaciones. Para más información, vea [Punto de sitios web del catálogo de aplicaciones](/sccm/core/servers/deploy/configure/configuration-options-for-site-system-roles#BKMK_ApplicationCatalog_Website).  

4. Configuración de cliente del **Nombre de la organización** en el grupo **Agente de equipo**. Para más información, vea [Acerca de la configuración de cliente](/sccm/core/clients/deploy/about-client-settings#computer-agent).  


## <a name="see-also"></a>Consulte también

- [Manual del usuario del Centro de software](/sccm/core/understand/software-center)
- [Planear y configurar la administración de aplicaciones en Configuration Manager](/sccm/apps/plan-design/plan-for-and-configure-application-management)
