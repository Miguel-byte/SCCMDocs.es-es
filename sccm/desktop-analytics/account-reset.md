---
title: Cómo restablecer la cuenta
titleSuffix: Configuration Manager
description: Obtenga información acerca de cómo restablecer su cuenta de análisis de escritorio.
ms.date: 08/16/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 884d4864-950b-4139-b778-d5368e1f6ef2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3eb3f08c7c1358343b4bf06aef80ba84a5fb8d8c
ms.sourcegitcommit: 2b07fb7e2a17b5624429e81f9b6b9b3223b6f16d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/16/2019
ms.locfileid: "69536784"
---
# <a name="how-to-reset-your-account"></a>Cómo restablecer la cuenta

<!-- 3733897 -->

> [!Note]  
> Esta información está relacionada con un servicio de vista previa que se puede modificar sustancialmente antes de que se publique comercialmente. Microsoft no ofrece ninguna garantía, expresa o implícita, con respecto a la información aquí proporcionada.  

Si configura el análisis de escritorio en su entorno, pero desea empezar de nuevo con la incorporación y la inscripción, use este proceso para restablecer la cuenta.

## <a name="prerequisites"></a>Requisitos previos

Solo un **administrador global** puede restablecer la cuenta en el Azure portal.

## <a name="behaviors"></a>comportamientos

- Este proceso no cambia ningún usuario, aplicación o permiso existente Azure AD

- Si decide agregar una nueva área de trabajo, no se conserva ninguna de las siguientes entradas de usuario en los recursos:
    - Importance
    - Propietario
    - Decisión de actualización
    - Notas de corrección

## <a name="process"></a>Process

1. Abra el [portal de análisis de escritorio](https://aka.ms/desktopanalytics) en Microsoft 365 la administración de dispositivos como usuario con el rol de **administrador global** .

1. En el menú **configuración global** , seleccione **servicios conectados**. En la sección inscribir dispositivos, seleccione la opción para **restablecer**.

1. Si decide continuar, se restablecerá la cuenta. Deberá volver a configurar el análisis de escritorio.

## <a name="next-steps"></a>Pasos siguientes

Después del restablecimiento, actualice la página y vuelva a ejecutar el proceso de incorporación. Para obtener más información, consulte [configuración de análisis de escritorio](/sccm/desktop-analytics/set-up).

Si tiene algún problema durante este proceso, póngase en contacto con Soporte técnico de Microsoft para obtener más ayuda.
