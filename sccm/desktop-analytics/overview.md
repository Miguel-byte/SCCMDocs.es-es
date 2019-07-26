---
title: Análisis de escritorio
titleSuffix: Configuration Manager
description: Información general del servicio de análisis de escritorio integrado con Configuration Manager.
ms.date: 07/19/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: overview
ms.assetid: 38b2bed2-20dd-4ce1-abc0-219343d2c4b8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 154c142b285c58da714193c964b353dc1e173481
ms.sourcegitcommit: 79c51028f90b6966d6669588f25e8233cf06eb61
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/19/2019
ms.locfileid: "68339261"
---
# <a name="what-is-desktop-analytics"></a>¿Qué es el análisis de escritorio?

> [!Note]  
> Esta información está relacionada con un servicio de vista previa que se puede modificar sustancialmente antes de que se publique comercialmente. Microsoft no ofrece ninguna garantía, expresa o implícita, con respecto a la información aquí proporcionada.  

Análisis de escritorio es un servicio basado en la nube que se integra con Configuration Manager. El servicio proporciona información e inteligencia para tomar decisiones más fundamentadas sobre la preparación de las actualizaciones de los clientes de Windows. Combina datos de su organización con datos agregados de millones de dispositivos conectados a servicios en la nube de Microsoft.

Use el análisis de escritorio con Configuration Manager para:  

- Crear un inventario de las aplicaciones que se ejecutan en su organización  

- Evaluación de la compatibilidad de aplicaciones con las últimas actualizaciones de características de Windows 10  

- Identificar problemas de compatibilidad y recibir sugerencias de mitigación basadas en información de datos habilitada para la nube  

- Crear grupos piloto que representen toda la aplicación y el controlador a través de un conjunto mínimo de dispositivos  

- Implementación de Windows 10 en dispositivos piloto y administrados por producción  

![Captura de pantalla de la Página principal de análisis de escritorio en el Azure Portal](media/portal-home.png)

> [!Note]  
> El análisis de escritorio es una sucesora de Windows Analytics. El servicio de *Windows Analytics* incluye Upgrade Readiness, Update Compliance y estado del dispositivo.
>
> Todas estas funcionalidades se combinan en el servicio de *análisis de escritorio* . El análisis de escritorio también se integra de forma más estrecha con Configuration Manager.



## <a name="benefits"></a>Ventajas

Muchos clientes tienen desafíos para obtener y mantenerse actualizados con Windows 10. El principal desafío es la prueba de las aplicaciones. Este proceso suele ser manual. Es lento para los administradores de ti y los propietarios de aplicaciones el análisis continuo de las aplicaciones existentes. Después, solucione los problemas que surjan.

El análisis de escritorio proporciona las siguientes ventajas:

- **Inventario de dispositivos y software**: Inventario de factores clave como aplicaciones y versiones de Windows.  

- **Identificación piloto**: Identificación del conjunto más pequeño de dispositivos que proporcionan la mayor cobertura de factores. Se centra en los factores que son más importantes para una prueba piloto de actualizaciones y actualizaciones de Windows. Asegurarse de que el piloto es más satisfactorio le permite realizar las implementaciones más rápidas y seguras en producción.  

- **Identificación del problema**: Mediante el uso de datos de mercado agregados junto con datos de su entorno, el servicio predice posibles problemas para obtener y mantenerse actualizados con Windows. Después, sugiere posibles mitigaciones.  

- **Integración de Configuration Manager**: La nube de servicio: habilita la infraestructura local existente. Use estos datos y análisis para implementar y administrar Windows en sus dispositivos.  



## <a name="prerequisites"></a>Requisitos previos

Para usar el análisis de escritorio, asegúrese de que el entorno cumple los requisitos previos siguientes.


### <a name="technical"></a>T

- Una suscripción de Azure activa, con permisos de [administrador global](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles#company-administrator) . No se admiten [las cuentas de Microsoft](https://docs.microsoft.com/windows/security/identity-protection/access-control/microsoft-accounts) .  

    > [!Important]  
    > El análisis de escritorio se ofrece actualmente como un servicio de Office 365 y requiere una suscripción de Office 365 en el inquilino de Azure AD. Esto puede no ser un requisito en el futuro.

    - Permisos de propietario  o colaborador del **área de trabajo** para **configurar el área de trabajo**y los roles siguientes:  

      - Rol de [**Administrador de análisis de escritorio**](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles) .

      - [**Log Analytics colaborador**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#log-analytics-contributor) y [**Administrador de acceso de usuario**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#user-access-administrator) en el grupo de recursos para usar un área de trabajo existente o crear una nueva área de trabajo en un grupo de recursos existente.

      - Permisos de [**propietario**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#owner)o colaborador y [**Administrador de acceso de usuario**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#user-access-administrator) en la suscripción para crear un área de trabajo en un nuevo grupo de recursos. [](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#contributor)  

- Configuration Manager, versión 1902 con el paquete acumulativo de actualizaciones (4500571) o posterior. Para obtener más información, vea [actualizar Configuration Manager](/sccm/desktop-analytics/connect-configmgr#bkmk_hotfix).  

    - Rol de **Administrador total** en Configuration Manager  

    > [!Note]  
    > El análisis de escritorio admite un ID. comercial por cada inquilino de Azure Active Directory (Azure AD) y Configuration Manager jerarquía. Si tiene varias jerarquías en su entorno, use distintos identificadores comerciales y Azure AD inquilinos.<!-- 4958160 -->

- Dispositivos que ejecutan Windows 7, Windows 8.1 o Windows 10  

    - Instale las actualizaciones más recientes. Para obtener más información, consulte [actualizar dispositivos](/sccm/desktop-analytics/enroll-devices#update-devices).  

    - Los dispositivos también deben tener el cliente de Configuration Manager, versión 1902 con el paquete acumulativo de actualizaciones (4500571) o posterior. Para obtener más información, vea [actualizar Configuration Manager](/sccm/desktop-analytics/connect-configmgr#bkmk_hotfix).  

    > [!Note]  
    > El análisis de escritorio no es compatible con las actualizaciones de canal de mantenimiento a largo plazo (LTSC) de Windows 10. Para obtener más información, vea [información general de Windows como servicio](https://docs.microsoft.com/windows/deployment/update/waas-overview#long-term-servicing-channel).
    >
    > El análisis de escritorio está diseñado para admitir mejor el escenario de actualización local. Si necesita realizar cambios importantes, como, por ejemplo, de la arquitectura de 32 bits a 64 bits, utilice un escenario de creación de imágenes. Desktop Analytics Insights sigue siendo valioso en estos escenarios de implementación de sistema operativo clásico, pero puede pasar por alto la guía específica de la actualización en contexto. Para obtener más información, consulte [escenarios para implementar sistemas operativos de empresa con Configuration Manager](/sccm/osd/deploy-use/scenarios-to-deploy-enterprise-operating-systems).

- Datos de diagnósticos de Windows. Para más información, consulte los siguientes artículos.  

    - [Niveles de datos de diagnóstico](/sccm/desktop-analytics/enable-data-sharing#diagnostic-data-levels)  

    - [Privacidad de análisis de escritorio](/sccm/desktop-analytics/privacy)  

- Conectividad de red desde dispositivos a la nube pública de Microsoft. Para obtener más información, consulte [Habilitar el uso compartido de datos](/sccm/desktop-analytics/enable-data-sharing) .  


### <a name="licensing"></a>Licencias

El análisis de escritorio requiere una de las siguientes suscripciones de licencia:

- Windows 10 Enterprise E3 o E5; o Microsoft 365 F1, E3 o E5  

- Windows 10 Education a3 o A5; o Microsoft 365 a3 o A5  

- Windows VDA E3 o E5  




## <a name="next-steps"></a>Pasos siguientes

En el siguiente tutorial se proporciona una guía paso a paso para empezar a trabajar con análisis de escritorio y Configuration Manager:  

- [Implementación de Windows 10 en el piloto](/sccm/desktop-analytics/tutorial-windows10)  
