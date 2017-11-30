---
title: "Creación e implementación de directivas de Protección de aplicaciones de Windows Defender"
titleSuffix: Configuration Manager
description: "Creación e implementación de directivas de Protección de aplicaciones de Windows Defender."
ms.custom: na
ms.date: 11/21/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 
caps.latest.revision: "5"
author: ErikjeMS
ms.author: erikje
manager: angrobe
ms.openlocfilehash: db2508e5bbd1435fce432b6ef98d7968e68ea5ab
ms.sourcegitcommit: 12d0d53e47bbf1a0bbd85015b8404a44589d1e14
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="create-and-deploy-windows-defender-application-guard-policy----1351960---"></a>Creación e implementación de directivas de Protección de aplicaciones de Windows Defender <!-- 1351960 -->

Puede crear e implementar directivas de [Protección de aplicaciones de Windows Defender](https://docs.microsoft.com/windows/threat-protection/windows-defender-application-guard/wd-app-guard-overview) utilizando Configuration Manager Endpoint Protection. Estas directivas ayudan a proteger a los usuarios al abrir los sitios web que no sean de confianza en un contenedor aislado seguro al que no puedan tener acceso otras partes del sistema operativo.

## <a name="prerequisites"></a>Requisitos previos

Para crear e implementar una directiva de Protección de aplicaciones de Windows Defender, debe usar la actualización Windows 10 Fall Creators Update. Además, los dispositivos Windows 10 en los que implementa la directiva deben configurarse con una directiva de aislamiento de red. Para obtener más información, consulte [Información general de la Protección de aplicaciones de Windows Defender](https://docs.microsoft.com/en-us/windows/threat-protection/windows-defender-application-guard/wd-app-guard-overview). Esta funcionalidad solo es aplicable a compilaciones de Windows 10 Insider actuales. Para probarla, los clientes deben ejecutar una compilación reciente de Windows 10 Insider.


## <a name="create-a-policy-and-to-browse-the-available-settings"></a>Cree una directiva y examine la configuración disponible:

1. En la consola de Configuration Manager, elija **Activos y compatibilidad**.
2. En el área de trabajo **Activos y compatibilidad**, elija **Introducción** > **Endpoint Protection** > **Protección de aplicaciones de Windows Defender**.
3. En la pestaña **Inicio**, en el grupo **Crear**, haga clic en **Crear directiva de Protección de aplicaciones de Windows Defender**.
4. Con la [entrada de blog](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97) como referencia, puede examinar y configurar las opciones disponibles.
5. En la página **Definición de red**, debe especificar la identidad corporativa y definir los límites de la red corporativa.

    > [!NOTE]
    > Los equipos con Windows 10 solo almacenan una lista de aislamiento de red en el cliente. Puede crear dos tipos diferentes de listas de aislamiento de red e implementarlas en el cliente:
    >
    >  - uno de Windows Information Protection
    >  - otro de Protección de aplicaciones de Windows Defender
    >
    > Si implementa ambas directivas, deben coincidir con estas listas de aislamiento de red. Si implementa listas que no coincidan con el mismo cliente, se producirá un error en la implementación. Para obtener más información, consulte la [documentación de Windows Information Protection](https://docs.microsoft.com/windows/threat-protection/windows-information-protection/create-wip-policy-using-sccm).
    > 
    > 

6. Cuando haya terminado, complete el asistente e implemente la directiva en uno o varios dispositivos de Windows 10.

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información acerca de Protección de aplicaciones de Windows Defender, consulte [esta entrada de blog](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97). Además, para obtener más información sobre el modo independiente de Protección de aplicaciones de Windows Defender, consulte [esta entrada de blog](https://techcommunity.microsoft.com/t5/Windows-Insider-Program/Windows-Defender-Application-Guard-Standalone-mode/td-p/66903).
