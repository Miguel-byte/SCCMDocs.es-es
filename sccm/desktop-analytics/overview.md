---
title: Análisis de escritorio
titleSuffix: Configuration Manager
description: Información general sobre el servicio de análisis de escritorio integrado con Configuration Manager.
ms.date: 06/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: overview
ms.assetid: 38b2bed2-20dd-4ce1-abc0-219343d2c4b8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: b0daf2943b0859227d08069be9c9da69165d5d1a
ms.sourcegitcommit: de3c86077bbf91b793e94e1f60814df18da11bab
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/10/2019
ms.locfileid: "67726231"
---
# <a name="what-is-desktop-analytics"></a>¿Qué es el análisis de escritorio?

> [!Note]  
> Esta información se relaciona con un servicio en versión preliminar que puede modificarse sustancialmente antes de su lanzamiento comercial. Microsoft no ofrece ninguna garantía, expresa o implícita, con respecto a la información aquí proporcionada.  

Análisis de escritorio es un servicio basado en la nube que se integra con Configuration Manager. El servicio proporciona información e inteligencia para tomar decisiones más informadas sobre la preparación de actualización de los clientes de Windows. Combina datos de su organización con datos agregados de millones de dispositivos conectados a los servicios de nube de Microsoft.

Use escritorio Analytics con Configuration Manager para:  

- Crear un inventario de aplicaciones que se ejecutan en su organización  

- Evaluar la compatibilidad de aplicaciones con las últimas actualizaciones de características de Windows 10  

- Identificar problemas de compatibilidad y recibir sugerencias de mitigación según la información sobre los datos de nube habilitada  

- Crear grupos pilotos que representan el estado de aplicación y controlador todo a través de un conjunto mínimo de dispositivos  

- Implementar Windows 10 en dispositivos de pilotos y de producción administradas  

![Captura de pantalla de la página de inicio de análisis de escritorio en el portal de Azure](media/portal-home.png)

> [!Note]  
> Análisis de escritorio es un sucesor de Windows Analytics. El *Windows Analytics* service incluye Upgrade Readiness, cumplimiento de las actualizaciones y mantenimiento de dispositivos.
>
> Todas estas capacidades se combinan en el *Desktop Analytics* service. También escritorio Analytics se integra más estrechamente con Configuration Manager.



## <a name="benefits"></a>Ventajas

Muchos clientes tienen dificultades con cómo estar y mantenerse actualizados con Windows 10. El principal desafío es probar aplicaciones. Este proceso es normalmente manual. Es mucho tiempo para los administradores de TI y los propietarios de aplicaciones para analizar las aplicaciones existentes de forma continua. A continuación, corregir cualquier problema que surja.

Escritorio Analytics proporciona las siguientes ventajas:

- **Inventario de software y dispositivos**: Inventario de los factores clave como aplicaciones y las versiones de Windows.  

- **Identificación de la prueba piloto**: Identificación del conjunto más pequeño de los dispositivos que proporcionan la cobertura más amplia de factores. Se centra en los factores que son más importantes para una prueba piloto de actualizaciones de Windows. Asegurándose de que tiene más éxito del piloto le permite continuar más rápidamente y con confianza con amplia implementaciones en producción.  

- **Emitir identificación**: Con los datos de mercado agregados junto con los datos de su entorno, el servicio predice potencial emite a cómo estar y mantenerse actualizados con Windows. A continuación, se sugiere posibles mitigaciones.  

- **Integración de Configuration Manager**: El servicio en la nube habilita la infraestructura local existente. Use estos datos y análisis para implementar y administrar Windows en los dispositivos.  



## <a name="prerequisites"></a>Requisitos previos

Para utilizar el análisis de escritorio, asegúrese de que su entorno cumple los siguientes requisitos previos.


### <a name="technical"></a>Técnica

- Una suscripción activa de Azure, con [administrador Global](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles#company-administrator) permisos  

    - **Propietario del área de trabajo** o **colaborador** permisos para **configurar el área de trabajo**y los roles siguientes:  

      - [**Administrador de análisis de escritorio** ](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles) rol.

      - [**Colaborador de análisis de registro** ](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#log-analytics-contributor) y [ **Administrador de acceso de usuario** ](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#user-access-administrator) en el grupo de recursos para usar un área de trabajo existente o crear una nueva área de trabajo en un grupo de recursos existente.

      - [**Propietario**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#owner), o [ **colaborador** ](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#contributor) y [ **Administrador de acceso de usuario** ](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#user-access-administrator) permisos en el suscripción para crear un área de trabajo en un grupo de recursos.  

- Configuration Manager, versión 1902 con paquete acumulativo de actualizaciones (4500571) o posterior. Para obtener más información, consulte [actualizar Configuration Manager](/sccm/desktop-analytics/connect-configmgr#bkmk_hotfix).  

    - **Administrador total** rol en Configuration Manager  

- Dispositivos que ejecutan Windows 7, Windows 8.1 o Windows 10  

    - Instale las actualizaciones más recientes. Para obtener más información, consulte [actualizar dispositivos](/sccm/desktop-analytics/enroll-devices#update-devices).  

    - Los dispositivos también deben tener el cliente de Configuration Manager, versión 1902 con paquete acumulativo de actualizaciones (4500571) o posterior. Para obtener más información, consulte [actualizar Configuration Manager](/sccm/desktop-analytics/connect-configmgr#bkmk_hotfix).  

    > [!Note]  
    > Análisis de escritorio no es compatible con las actualizaciones de canal de mantenimiento a largo plazo (LTSC) de Windows 10. Para obtener más información, consulte [Windows como una información general del servicio](https://docs.microsoft.com/windows/deployment/update/waas-overview#long-term-servicing-channel).
    >
    > Escritorio Analytics está diseñado para el mejor escenario de actualización de soporte técnico en el contexto. Si necesita realizar cambios importantes, como de la arquitectura de 32 bits a 64 bits, utilice un escenario de creación de imágenes. Escritorio insights Analytics todavía resultan valiosos en estos escenarios de implementación de sistema operativo clásicos, pero puede pasar por alto la orientación específica de actualización en contexto. Para obtener más información, consulte [escenarios para implementar sistemas operativos de empresa con Configuration Manager](/sccm/osd/deploy-use/scenarios-to-deploy-enterprise-operating-systems).

- Datos de diagnóstico de Windows. Para más información, consulte los siguientes artículos.  

    - [Niveles de datos de diagnóstico](/sccm/desktop-analytics/enable-data-sharing#diagnostic-data-levels)  

    - [Privacidad de análisis de escritorio](/sccm/desktop-analytics/privacy)  

- Conectividad de red desde dispositivos a la nube pública de Microsoft. Para obtener más información, vea [cómo habilitar el uso compartido de datos](/sccm/desktop-analytics/enable-data-sharing)  


### <a name="licensing"></a>Licencias

Escritorio Analytics requiere una de las suscripciones de licencias siguientes:

- Windows 10 Enterprise E3 o E5; o Microsoft 365 F1, E3 o E5  

- Windows 10 Education A3 o A5; o Microsoft 365 A3 o A5  

- Windows VDA E3 o E5  




## <a name="next-steps"></a>Pasos siguientes

El siguiente tutorial proporciona a una guía paso a paso para empezar a trabajar con análisis de escritorio y Configuration Manager:  

- [Implementación piloto de Windows 10](/sccm/desktop-analytics/tutorial-windows10)  
