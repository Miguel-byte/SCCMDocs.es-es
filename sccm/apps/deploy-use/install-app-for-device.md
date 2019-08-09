---
title: Instalación de aplicaciones para un dispositivo
titleSuffix: Configuration Manager
description: Use Configuration Manager para instalar inmediatamente una aplicación en un dispositivo sin una recopilación.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: c2a71fca-8744-4d72-abf9-9d8c5d2afb00
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ba68dc78f289b779a157398e9487b637318788c6
ms.sourcegitcommit: 72faa1266b31849ce1a23d661a1620b01e94f517
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/26/2019
ms.locfileid: "68537693"
---
# <a name="install-applications-for-a-device"></a>Instalación de aplicaciones para un dispositivo

<!--4402180-->

A partir de la versión 1906, desde la consola de Configuration Manager, puede instalar aplicaciones en un dispositivo en tiempo real. Esta característica puede ayudar a reducir la necesidad de colecciones independientes para cada aplicación.

## <a name="prerequisites"></a>Requisitos previos

- Habilite la [característica opcional](/sccm/core/servers/manage/install-in-console-updates#bkmk_options) **Aprobación de solicitudes de aplicación para los usuarios por dispositivo**.  

- [Implementar la aplicación](/sccm/apps/deploy-use/deploy-applications) como *disponible* para una recopilación de dispositivos.  

    - En la página **configuración de implementación** del Asistente para la implementación, seleccione la opción siguiente: **un administrador debe aprobar una solicitud para esta aplicación en el dispositivo**.  

        > [!Note]  
        > Con esta configuración de implementación, no se envía ninguna directiva al cliente. La aplicación no se muestra como disponible en el centro de software y un usuario no puede instalar la aplicación con esta implementación. Después de usar esta acción para instalar la aplicación, el usuario puede ejecutarla y ver su estado de instalación en el Centro de software.

- La cuenta de usuario necesita los permisos siguientes:

    - **Aplicación**: lectura, aprobación

    - **Recopilación**: lectura, lectura de recursos, modificar recurso, ver archivo recopilado

    Por ejemplo, el rol integrado **Administrador de aplicaciones** tiene estos permisos.


## <a name="process"></a>Proceso

1. En la consola de Configuration Manager, vaya al área de trabajo **Activos y compatibilidad** y haga clic en el nodo **Dispositivos**. Seleccione el dispositivo de destino y después la acción **Instalar aplicación** en la cinta.

1. Seleccione una o varias aplicaciones de la lista. La lista solo muestra las aplicaciones que ya ha implementado con la configuración de requisitos previos.

Esta acción desencadena la instalación en el dispositivo de las aplicaciones previamente implementadas seleccionadas.

Para ver el estado de la aprobación de aplicación, en el área de trabajo **Biblioteca de software**, expanda **Administración de aplicaciones** y seleccione el nodo **Solicitudes de aplicación**.

Supervise la instalación de la aplicación de la forma habitual en el nodo **Implementaciones** del área de trabajo **Supervisión**.


## <a name="see-also"></a>Consulte también

[Aprobar aplicaciones](/sccm/apps/deploy-use/app-approval)
