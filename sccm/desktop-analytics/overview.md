---
title: Análisis de escritorio
titleSuffix: Configuration Manager
description: Información general sobre el servicio de análisis de escritorio integrado con Configuration Manager.
ms.date: 01/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: overview
ms.assetid: 38b2bed2-20dd-4ce1-abc0-219343d2c4b8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4105a8a81ab3f09dee9cf3ca5a2462ed2bb4183a
ms.sourcegitcommit: 6f4c2987debfba5d02ee67f6b461c1a988a3e201
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59802638"
---
# <a name="what-is-desktop-analytics"></a>¿Qué es el análisis de escritorio?

> [!Note]  
> Esta información se relaciona con un servicio en versión preliminar que puede modificarse sustancialmente antes de su lanzamiento comercial. Microsoft no ofrece ninguna garantía, expresa o implícita, con respecto a la información aquí proporcionada.  

Análisis de escritorio es un servicio basado en la nube que se integra con Configuration Manager. El servicio proporciona información e inteligencia para tomar decisiones más informadas sobre la preparación de actualización de los clientes de Windows y Office. Combina datos de su organización con datos agregados de millones de dispositivos conectados a los servicios de nube de Microsoft. 

Use escritorio Analytics con Configuration Manager para:  

- Crear un inventario de aplicaciones que se ejecutan en su organización  

- Evaluar la compatibilidad de aplicaciones con las últimas actualizaciones de características de Windows 10 y Office 365 ProPlus  

- Identificar problemas de compatibilidad y recibir sugerencias de mitigación según la información sobre los datos de nube habilitada  

- Crear grupos pilotos que representan el estado de aplicación y controlador todo a través de un conjunto mínimo de dispositivos  

- Implementar Windows 10 y Office 365 ProPlus a dispositivos pilotos y de producción administradas  

![Captura de pantalla de la página de inicio de análisis de escritorio en el portal de Azure](media/portal-home.png)

> [!Note]  
> Análisis de escritorio es un sucesor de Windows Analytics. El *Windows Analytics* service incluye Upgrade Readiness, cumplimiento de las actualizaciones y mantenimiento de dispositivos. 
> 
> Todas estas capacidades se combinan en el *Desktop Analytics* service. Análisis de escritorio también está más estrechamente integrado con Configuration Manager e incluyen Windows y Office. 



## <a name="benefits"></a>Ventajas

Muchos clientes tienen dificultades con cómo estar y mantenerse actualizados con Windows 10 y Office 365 ProPlus. El principal desafío es probar aplicaciones. Este proceso es normalmente manual. Es mucho tiempo para los administradores de TI y los propietarios de aplicaciones para analizar las aplicaciones existentes de forma continua. A continuación, corregir cualquier problema que surja. 

Escritorio Analytics proporciona las siguientes ventajas:

- **Inventario de software y dispositivos**: Inventario de los factores clave como aplicaciones, complementos, macros y las versiones de Office y Windows.  

- **Identificación de la prueba piloto**: Identificación del conjunto más pequeño de los dispositivos que proporcionan la cobertura más amplia de factores. Se centra en los factores que son más importantes para una prueba piloto de actualizaciones de Windows y Office. Asegurándose de que tiene más éxito del piloto le permite continuar más rápidamente y con confianza con amplia implementaciones en producción.  

- **Emitir identificación**: Con los datos de mercado agregados junto con los datos de su entorno, el servicio predice potencial emite a cómo estar y mantenerse actualizados con Windows y Office. A continuación, se sugiere posibles mitigaciones.  

- **Integración de Configuration Manager**: El servicio en la nube habilita la infraestructura local existente. Use estos datos y análisis para implementar y administrar Windows y Office en sus dispositivos.  



## <a name="prerequisites"></a>Requisitos previos

Para utilizar el análisis de escritorio, asegúrese de que su entorno cumple los siguientes requisitos previos. 


### <a name="technical"></a>Técnica

- Una suscripción activa de Azure  

    - **Administrador de empresa** permisos en Azure  

- Configuration Manager, versión 1810 con Update Rollup 4488598 o posterior. Para obtener más información, consulte [actualizar Configuration Manager](/sccm/desktop-analytics/connect-configmgr#bkmk_hotfix).  

    - **Administrador total** rol en Configuration Manager  

- Dispositivos que ejecutan Windows 7, Windows 8.1 o Windows 10  

    - Instale las actualizaciones más recientes. Para obtener más información, consulte [actualizar dispositivos](/sccm/desktop-analytics/enroll-devices#update-devices).  

    - Los dispositivos también deben tener el cliente de Configuration Manager, versión 1810 con paquete acumulativo de actualizaciones 4486457 o posterior. Para obtener más información, consulte [actualizar Configuration Manager](/sccm/desktop-analytics/connect-configmgr#bkmk_hotfix).  

- Datos de diagnóstico de Windows. Vea los siguientes artículos para más información:  

    - [Niveles de datos de diagnóstico](/sccm/desktop-analytics/enable-data-sharing#diagnostic-data-levels)  

    - [Privacidad de análisis de escritorio](/sccm/desktop-analytics/privacy)  

- Conectividad de red desde dispositivos a la nube pública de Microsoft. Para obtener más información, vea [cómo habilitar el uso compartido de datos](/sccm/desktop-analytics/enable-data-sharing)  


### <a name="licensing"></a>Licencias

Mayoría de las características de análisis de escritorio no requiere licencias adicionales ni suscripciones. Cuando se configuran correctamente, uso de análisis de escritorio no incurrir en ningún gasto de Azure. 

Para obtener acceso a información de estado de Windows o para exportar datos, existen requisitos de licencia adicionales. Si no tiene una de las siguientes suscripciones, todavía puede configurar y utilizar el análisis de escritorio, pero no es con licencia para usar la información de estado de Windows o para exportar los datos:

- Windows 10 Enterprise o Windows 10 Education: cada dispositivo con Software Assurance activo  

- Windows 10 Enterprise E3 o E5: suscripción por usuario o por dispositivo (incluido con Microsoft 365 F1, E3 o E5)  

- Windows 10 Education A3 o A5 (incluido con Microsoft 365 educación A3 o A5)  

- Windows Virtual Desktop acceso E3 o E5: por dispositivo de la suscripción por usuario  

> [!Note]  
> Las licencias por dispositivo, no tienes que activar cada dispositivo con una licencia. Basta con suficientes licencias para los dispositivos inscritos en análisis de escritorio.  


<!-- 
## Top task
> *Optional*  
> *An effective way to structure your overview article is to create an H2 for the top customer tasks and describe how the product/service helps customers with that task.*  
> *Create a new H2 for each task you list.*  
 -->



## <a name="next-steps"></a>Pasos siguientes

El siguiente tutorial proporciona a una guía paso a paso para empezar a trabajar con análisis de escritorio y Configuration Manager:  

- [Implementar Office 365 en un programa piloto](/sccm/desktop-analytics/tutorial-office-365)  

<!-- for future
- [Deploy Windows 10 to a pilot](/sccm/desktop-analytics/tutorial-windows)  
-->
