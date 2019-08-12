---
title: Centro de soporte técnico OneTrace (versión preliminar)
titleSuffix: Configuration Manager
description: OneTrace es un nuevo visor de registros del Centro de soporte técnico que tiene mejoras relativas a CMTrace.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 4cde43d1-9b09-4601-b389-0776de451b4e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a015277f9a2fb05c4fbecc4d702d63a5a97777ca
ms.sourcegitcommit: 72faa1266b31849ce1a23d661a1620b01e94f517
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/26/2019
ms.locfileid: "68537981"
---
# <a name="support-center-onetrace-preview"></a>Centro de soporte técnico OneTrace (versión preliminar)

<!--3555962-->

A partir de la versión 1906, OneTrace es un nuevo visor de registros del Centro de soporte técnico. Funciona de forma similar a CMTrace, con las mejoras siguientes:

- Una vista con pestañas.
- Ventanas acoplables.
- Funciones de búsqueda mejoradas.
- Capacidad de habilitar filtros sin salir de la vista del registro.
- Sugerencias de la barra de desplazamiento para identificar rápidamente clústeres de errores.
- Apertura de registro rápida para archivos de gran tamaño

![Captura de pantalla del visor de registros OneTrace](media/3555962-onetrace.png)

OneTrace funciona con muchos tipos de archivos de registro, como los siguientes:

- Registros de cliente de Configuration Manager.
- Registros de servidor de Configuration Manager.
- Mensajes de estado
- Archivo de registro ETW de Windows Update en Windows 10.
- Archivo de registro de Windows Update en Windows 7 y Windows 8.1.

## <a name="prerequisites"></a>Requisitos previos

- .NET Framework, versión 4.6 o posteriores

## <a name="install"></a>Instalación de

OneTrace se instala con el Centro de soporte técnico. Busque el instalador del Centro de soporte técnico en la siguiente ruta de acceso del servidor de sitio: `cd.latest\SMSSETUP\Tools\SupportCenter\SupportCenterInstaller.msi`.

> [!Note]  
> El Centro de soporte técnico y OneTrace usan Windows Presentation Foundation (WPF). Este componente no está disponible en Windows PE. Siga usando CMTrace en las imágenes de arranque con implementaciones de secuencia de tareas.  

## <a name="see-also"></a>Consulte también

- [Visor de registros del Centro de soporte técnico](/sccm/core/support/support-center-ui-reference#bkmk_log-viewer)

- [CMTrace](/sccm/core/support/cmtrace)
