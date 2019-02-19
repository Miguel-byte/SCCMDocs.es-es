---
title: Compatibilidad internacional
titleSuffix: Configuration Manager
description: Configure System Center Configuration Manager para que cumpla con los requisitos internacionales específicos.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 46dd9cb2-a812-4b6a-a747-b840f92fef8b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7c76f0213ffb30432c51430f3fd98b911ab5d627
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56129160"
---
# <a name="international-support-in-system-center-configuration-manager"></a>Compatibilidad internacional en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

En las secciones siguientes se proporcionan detalles técnicos para que System Center Configuration Manager sea compatible con determinados requisitos internacionales.  

## <a name="gb18030-requirements"></a>Requisitos de GB18030  
 Configuration Manager cumple los estándares definidos en GB18030 para poder usar Configuration Manager en China. Una implementación de Configuration Manager debe tener la configuración siguiente para cumplir los requisitos de GB18030:  

-   Los equipos de servidor de sitio y de SQL Server que se usan con Configuration Manager deben usar un sistema operativo chino.  

-   Las bases de datos del sitio y las instancias de SQL Server en la jerarquía deben utilizar la misma intercalación, y debe ser una las siguientes:  

    -   Chinese_Simplified_Pinyin_100_CI_AI  

    -   Chinese_Simplified_Stroke_Order_100_CI_AI  

    > [!NOTE]  
    >  Estas intercalaciones de base de datos son una excepción de los requisitos que se mencionan en [Versiones de SQL Server compatibles con System Center Configuration Manager](../../../core/plan-design/configs/support-for-sql-server-versions.md).  

-   Debe colocar un archivo de nombre **GB18030.SMS** en la carpeta raíz del volumen de sistema de cada equipo de servidor de sitio en la jerarquía. Este archivo no contiene datos y puede ser un archivo de texto vacío con este nombre para cumplir el requisito.  
