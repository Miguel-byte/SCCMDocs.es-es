---
title: Acciones de no cumplimiento
titleSuffix: Configuration Manager
description: Información sobre cómo configurar acciones de no cumplimiento con Configuration Manager
ms.date: 11/10/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: ad8fa94d-45bb-4c94-8d86-31234c5cf21c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: be17e1f2b5c3fec02cdd6fc5f89aee9319c4dbb4
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="set-up-actions-for-non-compliance"></a>Configuración de acciones de no cumplimiento

Las **acciones de no cumplimiento** permiten configurar una secuencia de acciones que se aplican a dispositivos que no cumplen determinadas directivas. Por ejemplo, puede enviar correos electrónicos al usuario final de dispositivos no conformes o marcarlos como no conformes.

## <a name="before-you-begin"></a>Antes de comenzar

> [!IMPORTANT]
> Debe tener, al menos, una directiva de cumplimiento de dispositivos creada para establecer las acciones de no cumplimiento.

Estas son las acciones que se admiten para el no cumplimiento:

- Envío de correos electrónicos al usuario final
- Marcado de dispositivos como no conformes

### <a name="send-e-mail-to-end-user"></a>Envío de correos electrónicos al usuario final

Puede elegir entre plantillas de correo electrónico predeterminadas creadas previamente o crear una notificación de correo electrónico personalizada. Configuration Manager permite personalizar el asunto, el cuerpo del mensaje, incluido el logotipo de la empresa, la información de contacto y destinatarios adicionales.

### <a name="mark-devices-non-compliant"></a>Marcado de dispositivos como no conformes

Puede determinar una programación en número de días durante los cuales se debe bloquear el dispositivo para que no acceda a los recursos corporativos. Puede ser inmediatamente, pero también puede asignar al usuario un período de gracia para que cumpla las directivas de cumplimiento de dispositivos.

### <a name="supported-platforms"></a>Plataformas admitidas

Compatible con [todas las plataformas que se administran mediante Intune](https://docs.microsoft.com/intune/supported-devices-browsers).

## <a name="to-add-an-email-template"></a>Incorporación de una plantilla de correo electrónico

Configuration Manager proporciona plantillas de correo electrónico, pero también puede crear las suyas propias. La plantilla de correo electrónico se usa más adelante en el proceso de creación de acciones de no cumplimiento para comunicarse con los usuarios.

1. En la consola de Configuration Manager, elija **Activos y compatibilidad**.

2. En el área de trabajo **Activos y compatibilidad**, expanda **Configuración de cumplimiento** y, luego, haga clic en **Plantillas de notificación de cumplimiento**.

3. En la pestaña **Inicio**, en **Crear plantilla de notificación de cumplimiento**.

4. Debe escribir la siguiente información: a. Nombre: nombre de la plantilla de correo electrónico.
    b. Desde: dirección de correo electrónico desde la que se envía la notificación de correo electrónico.
    c. Asunto: un tema que explica la notificación de correo electrónico que se envía.
    d. Cuerpo del mensaje: más detalles sobre la notificación de correo electrónico.

    > [!TIP] 
    > También puede incluir el **encabezado de correo electrónico** con el logotipo de la empresa y el pie de página de correo electrónico, que puede incluir información de contacto y el nombre de la empresa. También puede modificarse en las propiedades de la suscripción de Intune.

5. Haga clic en **Aceptar** para guardar la nueva plantilla de correo electrónico.

6. En la página **Agregar acción**, puede seleccionar la nueva plantilla de correo electrónico de la lista.

7. Una vez que la seleccione, haga clic en **Aceptar**.

## <a name="to-create-actions-for-non-compliance"></a>Creación de acciones de no cumplimiento

1. En la consola de Configuration Manager, elija **Activos y compatibilidad**.

2. En el área de trabajo **Activos y compatibilidad**, expanda **Configuración de cumplimiento** y, a continuación, haga clic en **Directivas de cumplimiento**.

3. En la pestaña **Inicio**, en el grupo **Crear**, elija **Crear directiva de cumplimiento**.

4. Seleccione las **plataformas admitidas** que desee y después haga clic en **Siguiente** dos veces. Puede omitir la página **Reglas**.

5. En la página **Acciones de no cumplimiento**, se define lo que ocurre cuando un dispositivo no cumple una determinada directiva. Haga clic en **Nuevo**.
6. Puede elegir dos opciones: **Enviar correo electrónico a usuario final** o **Marcar el dispositivo como no conforme**.

7. Si selecciona **Enviar correo electrónico a usuario final**, debe especificar lo siguiente: a. **Período de gracia (en días):** puede escribir entre 0 y 365 días.
    b. **Destinatarios adicionales (a través de correo electrónico)** c. **Seleccionar plantilla de mensaje**: puede elegir las plantillas de correo electrónico predeterminadas o las personalizadas que haya agregado.
    
    > [!TIP] 
    > También puede agregar una nueva plantilla de correo electrónico al agregar la acción **Enviar correo electrónico a usuario final** haciendo clic en la opción **Nuevo:** de la página **Agregar acción**.

8. Si selecciona **Marcar el dispositivo como no conforme**, debe especificar lo siguiente: a. **Período de gracia (en días):** puede escribir entre 0 y 365 días.

9. Cuando elija la acción y especifique la configuración, haga clic en **Siguiente** dos veces y, luego, en **Cerrar**.


