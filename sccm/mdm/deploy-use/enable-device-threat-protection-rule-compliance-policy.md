---
title: Habilitación de la regla de protección de dispositivos en la directiva de cumplimiento
titleSuffix: Configuration Manager
description: Habilite la regla de protección contra amenazas móviles en la directiva de cumplimiento de dispositivos.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 99a5b715-f172-46e1-ac27-ad55bde66d0d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0bae054d3daa5aea8e343fef05aa4578221f17b6
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62226834"
---
# <a name="enable-device-threat-protection-rule-in-the-compliance-policy"></a>Habilitar la regla de protección contra amenazas de dispositivo en la directiva de cumplimiento

*Se aplica a: System Center Configuration Manager (Rama actual)*

Intune con Lookout Mobile Threat Protection le permite detectar amenazas móviles y hacer una evaluación de riesgos en el dispositivo. Puede crear una regla de directiva de cumplimiento en Configuration Manager para incluir la evaluación de riesgos a fin de determinar si el dispositivo está en cumplimiento. Luego puede usar la directiva de acceso condicional para permitir o bloquear el acceso a Exchange, SharePoint y otros servicios en función del cumplimiento del dispositivo.

Si desea que Lookout Device Threat Detection influya en la directiva de cumplimiento del dispositivo:

* La regla **Protección contra amenazas de dispositivo** debe estar habilitada en la directiva de cumplimiento.

* La página **Estado de Lookout** de la **consola de administrador de Intune** debe indicar **Activo**. Consulte el tema [Habilitar la conexión de Lookout MTP en Intune](enable-lookout-connection-in-intune.md) para más detalles e instrucciones sobre cómo activar la integración de Lookout.


Antes de crear la regla de protección contra amenazas de dispositivo en la directiva de cumplimiento, se recomienda [configurar la suscripción con Lookout Device Threat Protection](set-up-your-subscription-with-lookout.md), [habilitar la conexión de Lookout en Intune](enable-lookout-connection-in-intune.md) y [configurar la aplicación Lookout for Work](configure-and-deploy-lookout-for-work-apps.md). La regla de cumplimiento se aplica solo una vez que se completa la configuración.

Para habilitar la regla de protección contra amenazas de dispositivo, puede usar una directiva de cumplimiento existente o crear una nueva.

Como parte de la configuración de Lookout Device Threat Protection, en la [consola de Lookout](https://aad.lookout.com), creó una directiva que clasifica las diversas amenazas en niveles alto, medio y bajo. En la directiva de cumplimiento de Intune usará el nivel de amenaza para establecer el nivel de amenaza máximo permitido.

En la página **Reglas** del asistente para directivas de cumplimiento, defina una regla nueva con la información siguiente:
  * Condición: Nivel de máximo de riesgo de protección de amenazas de dispositivo.
  * Valor: El valor puede ser uno de los siguientes:
    * **Ninguno (protegido)**: Esto es la más segura. Esto significa que el dispositivo no puede tener ninguna amenaza. Si no se encuentra ningún nivel de amenaza, el dispositivo se evalúa como no conforme.
    * **Bajo**: El dispositivo se evalúa como conforme si solo hay amenazas de nivel bajo. Cualquier valor por encima coloca al dispositivo en un estado de no conformidad.
    * **Medio**: El dispositivo se evalúa como conforme si las amenazas que se encuentran en él son de nivel bajo o medio. Si se detectan amenazas de nivel alto, el dispositivo se determina como no conforme.
    * **Alta**: Este es el menos seguro. Básicamente, permite todos los niveles de amenaza y quizás solo sea útil si usa esta solución únicamente para fines informativos.

Si crea directivas de acceso condicional para Office 365 y otros servicios, se considera la evaluación de cumplimiento anterior y los dispositivos no conformes se bloquean y no pueden tener acceso a los recursos de la empresa hasta que se resuelva la amenaza.

El estado de la protección contra amenazas de dispositivo aparece en el nodo **Seguridad** del área de trabajo **Supervisión**.
Un gráfico visual muestra un resumen del estado con los diversos niveles de amenazas. Puede hacer clic en las secciones individuales del gráfico para ver más información, como la cantidad de dispositivos que se indican como no conformes por plataforma y los errores que se informan.
También puede ver el estado individual de los dispositivos en el área de trabajo **Activos y compatibilidad**, en **Dispositivos**.  Puede agregar las columnas **Cumplimiento de amenaza de dispositivo** y **Nivel de amenaza de dispositivo** para ver el estado.  Estas columnas no se muestran de manera predeterminada.
