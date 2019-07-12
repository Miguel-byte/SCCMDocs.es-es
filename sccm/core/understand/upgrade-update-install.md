---
title: Acerca de la instalación y la actualización
titleSuffix: Configuration Manager
description: Obtenga información acerca de la diferencia entre las condiciones de instalación, actualización al administrar la infraestructura de Configuration Manager.
ms.date: 04/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 17fab17f-304d-4f6a-87c7-30ab4f5521ed
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 263ec638afa62cee4f8fce86a9f7b9e35b37f0bb
ms.sourcegitcommit: f9654cd1a3af6d67de52fedaccceb2e22dafc159
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/09/2019
ms.locfileid: "67676045"
---
# <a name="about-upgrade-update-and-install-for-site-and-hierarchy-infrastructure"></a>Acerca de la actualización e instalación para sitios y jerarquía de infraestructura

*Se aplica a: System Center Configuration Manager (Rama actual)*


Al administrar el sitio de System Center Configuration Manager y la infraestructura de la jerarquía, los términos *mejorar*, *actualizar* e *instalar* se utilizan para describir los tres conceptos independientes.

## <a name="upgrade"></a>Mejorar
La *actualización* o *actualización in situ* se usan al convertir su jerarquía o sitio de Configuration Manager 2012 en uno que ejecuta System Center Configuration Manager.
Cuando actualice a System Center 2012 Configuration Manager para System Center Configuration Manager, continúe usando los mismos servidores para albergar sus sitios y servidores de sitios y conservar los datos existentes y configuraciones para Configuration Manager.  Esto es diferente de [migración](/sccm/core/migration/migrate-data-between-hierarchies), que es una manera de conservar las configuraciones y datos acerca de los dispositivos administrados durante el uso de nuevos sitios de System Center Configuration Manager instalados en el nuevo hardware.

Para obtener más información, consulte [Upgrade to System Center Configuration Manager](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager) (Actualizar a System Center Configuration Manager).



## <a name="update"></a>Actualizar
La *actualización* se usa para instalar actualizaciones en la consola para System Center Configuration Manager, y para actualizaciones fuera de banda que son actualizaciones que no se pueden enviar desde dentro de la consola de Configuration Manager. Las actualizaciones en la consola pueden modificar la versión del sitio de la rama actual (o sitio de vista previa técnica), por lo ejecuta una versión superior. Por ejemplo, si el sitio ejecuta la versión 1806, puede instalar una actualización para la versión 1810. Las actualizaciones también pueden instalar revisiones para un problema conocido sin modificar la versión del sitio.      

Normalmente, las actualizaciones agregan revisiones de seguridad, mejoras de calidad y nuevas características a la implementación existente. Si usa la rama de versión preliminar técnica, una actualización puede instalar una versión más reciente de la versión preliminar técnica.
- Elija cuándo instalar la actualización en la consola, comenzando por el sitio del nivel superior de la jerarquía.
- Puede instalar cualquier actualización disponible desde dentro de la consola. Por ejemplo, si su sitio ejecuta la versión 1802 y se ofrecen 1806 y 1810, considere instalar la versión 1810 porque cada versión incluye las características que estaban disponibles primero en las versiones publicadas anteriormente.
- Después de que se complete una nueva actualización en el sitio de nivel superior, los sitios primarios principales inician automáticamente el proceso de actualización. Sin embargo, puede establecer [Ventanas de servicio](/sccm/core/servers/manage/service-windows) para controlar la temporización de las actualizaciones.
- Los sitios secundarios no instalan automáticamente las actualizaciones. En su lugar, inicie manualmente la actualización desde dentro de la consola de Configuration Manager.

Para obtener información, consulte [Updates for System Center Configuration Manager](/sccm/core/servers/manage/updates) (Actualizaciones para System Center Configuration Manager) y [Technical Preview for System Center Configuration Manager](/sccm/core/get-started/technical-preview) (Technical Preview de System Center Configuration Manager).



## <a name="install"></a>Instalación de
La *instalación* se utiliza cuando crea una nueva jerarquía de Configuration Manager desde el principio o cuando agrega sitios adicionales a una jerarquía existente.  

Cuando se instala un nuevo sitio primario o un sitio de administración central, la ubicación de setup.exe y los archivos de origen relacionados que utiliza dependen de su escenario de instalación.

Para obtener más información, consulte [Preparar la instalación de sitios](/sccm/core/servers/deploy/install/prepare-to-install-sites).
