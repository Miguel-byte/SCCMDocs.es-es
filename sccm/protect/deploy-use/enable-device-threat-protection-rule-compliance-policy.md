---
title: "Habilitar la regla de protección de dispositivos en la directiva de cumplimiento | System Center Configuration Manager"
description: "Habilite la regla de protección contra amenazas móviles en la directiva de cumplimiento de dispositivos."
ms.custom: na
ms.date: 12/9/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 020f43e8-738e-4a82-91be-27b10cda9665
caps.latest.revision: 
author: andredm7
ms.author: andredm
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 498b8c02dbf1391e6331c8b9ad7b6ef0fdef22d0
ms.openlocfilehash: 319289c9b211935ba10cb6d3da386ffed3c0153e
ms.lasthandoff: 02/23/2017


---
# <a name="create-a-lookout-device-threat-protection-rule"></a>Crear una regla de protección contra amenazas de dispositivo de Lookout

*Se aplica a: System Center Configuration Manager (rama actual)*

## <a name="before-you-begin"></a>Antes de comenzar

Intune con Lookout Mobile Threat Protection le permite detectar amenazas móviles y hacer una evaluación de riesgos en el dispositivo. Puede crear una regla de directiva de cumplimiento en Configuration Manager para incluir la evaluación de riesgos a fin de determinar si el dispositivo es compatible. Luego puede usar la directiva de acceso condicional para permitir o bloquear el acceso a Exchange, SharePoint y otros servicios en función del cumplimiento del dispositivo.

Si desea que Lookout Device Threat Detection influya en la directiva de cumplimiento del dispositivo:

-   La regla **Protección contra amenazas de dispositivo** debe estar habilitada en la directiva de cumplimiento.

-   La página **Estado de Lookout** de la **consola de administrador de Intune** debe indicar **Activo**. Consulte el tema [Habilitar la conexión de Lookout MTP en Intune](https://docs.microsoft.com/sccm/protect/deploy-use/enable-lookout-connection-in-intune) para más detalles e instrucciones sobre cómo activar la integración de Lookout.

Antes de crear la regla de protección contra amenazas de dispositivo en la directiva de cumplimiento, se recomienda que haga lo siguiente:

1.  [Configurar su suscripción con la protección contra amenazas de dispositivo de Lookout](https://docs.microsoft.com/sccm/protect/deploy-use/set-up-your-subscription-with-lookout)

2.  [Habilitar la conexión de Lookout en Intune](https://docs.microsoft.com/sccm/protect/deploy-use/enable-lookout-connection-in-intune)

3.  [Configurar e implementar la aplicación Lookout for Work](https://docs.microsoft.com/sccm/protect/deploy-use/configure-and-deploy-lookout-for-work-apps)

>[!NOTE]
>La regla de cumplimiento solo se aplica una vez que se completa la configuración.

## <a name="to-create-a-device-threat-protection-rule"></a>Para crear una regla de protección contra amenazas de dispositivo

Como parte de la configuración de Lookout Device Threat Protection, en la [consola de Lookout](https://aad.lookout.com), creó una directiva que clasifica las diversas amenazas en niveles alto, medio y bajo. En la directiva de cumplimiento de Intune, usará el nivel de amenaza para establecer el nivel de amenaza máximo permitido.

Para crear una regla de protección contra amenazas de dispositivo de Lookout:

1.  En la consola de Configuration Manager, haga clic en el área de trabajo **Activos y compatibilidad**.

2.  En **Activos y compatibilidad**, expanda **Directivas de cumplimiento.**

3.  Haga clic con el botón derecho en **Directivas de cumplimiento** y, después, seleccione **Crear directiva de cumplimiento**.

4.  Escriba el nombre de la directiva de cumplimiento y después seleccione **Reglas de cumplimiento para dispositivos administrados sin el cliente de Configuration Manager**.

5.  Seleccione las plataformas de sistema operativo que se aprovisionarán con la directiva de cumplimiento (Android 4.1 y versiones posteriores o iOS 8 y versiones posteriores).

6.  En la página **Reglas**, haga clic en **Nueva** para especificar las reglas para un dispositivo compatible.

7.  En la página **Agregar regla**, defina una nueva regla con la siguiente información:
    1.  Condición: nivel máximo de riesgo de protección contra amenazas de dispositivo.
    
    2.  Valor: el valor debe ser uno de los siguientes:
        1.  **Ninguno (protegido)**: es la más segura. Esto significa que el dispositivo no puede tener ninguna amenaza. Si no se encuentra ningún nivel de amenaza, el dispositivo se evalúa como no compatible.
        2.  **Bajo**: el dispositivo se evalúa como conforme si solo hay amenazas de nivel bajo. Cualquier valor por encima coloca al dispositivo en un estado de no conformidad.
        3.  **Medio**: el dispositivo se evalúa como conforme si las amenazas que se encuentran en él son de nivel bajo o medio. Si se detectan amenazas de nivel alto, el dispositivo se determina como no conforme.
        4.  **Alto**: esta opción es la menos segura. Básicamente, permite todos los niveles de amenaza y quizás solo sea útil si usa esta solución únicamente para fines informativos.

>[!IMPORTANT]
>Si crea directivas de acceso condicional para Office 365 y otros servicios, se considera la evaluación de cumplimiento anterior y los dispositivos no conformes se bloquean y no pueden tener acceso a los recursos de la empresa hasta que se resuelva la amenaza.
