---
title: Definiciones de malware de Endpoint Protection desde un recurso compartido de red
titleSuffix: Configuration Manager
description: Aprenda a habilitar la descarga de definiciones de malware de Endpoint Protection desde Microsoft Update para Configuration Manager.
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: ab7626ae-d4bf-4ca6-ab25-c61f96800a02
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 0d8037f2258f97e2782d475598ca62d2f605e5cd
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="enable-endpoint-protection-malware-definitions-to-download-from-microsoft-updates-for-configuration-manager"></a>Habilitar la descarga de definiciones de malware de Endpoint Protection desde Microsoft Update para Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*


 Si selecciona la opción para descargar actualizaciones de definiciones desde Microsoft Update, los clientes buscarán actualizaciones en el sitio de Microsoft Update durante el intervalo definido en la sección **Actualizaciones de definiciones** del cuadro de diálogo de directiva antimalware.

 Este método puede resultar útil cuando el cliente no tiene conectividad con el sitio de Configuration Manager o cuando se quiere que los usuarios puedan iniciar actualizaciones de definiciones.

> [!IMPORTANT]
>  Los clientes deben tener acceso a Microsoft Update en Internet para poder usar este método de descarga de actualizaciones de definiciones.

## <a name="using-the-microsoft-malware-protection-center-to-download-definitions"></a>Uso del Centro de protección contra malware de Microsoft para descargar definiciones
 Puede configurar los clientes para que descarguen actualizaciones de definiciones desde el Centro de protección contra malware de Microsoft. Los clientes de Endpoint Protection usan esta opción para descargar actualizaciones de definiciones si no han podido descargarlas desde otro origen. Este método de actualización puede resultar útil si hay un problema con la infraestructura de Configuration Manager que impide la entrega de actualizaciones.

> [!IMPORTANT]
>  Los clientes deben tener acceso a Microsoft Update en Internet para poder usar este método de descarga de actualizaciones de definiciones.


> [!div class="button"]
[Paso siguiente >](endpoint-antimalware-policies.md)

> [!div class="button"]
[Atrás >](endpoint-configure-alerts.md)
