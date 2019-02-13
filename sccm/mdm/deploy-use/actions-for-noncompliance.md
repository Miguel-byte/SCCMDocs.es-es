---
title: Acciones de no cumplimiento
titleSuffix: Configuration Manager
description: Información sobre cómo configurar acciones de no cumplimiento con Configuration Manager
ms.date: 08/21/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: ad8fa94d-45bb-4c94-8d86-31234c5cf21c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: cbd996629d3b312febd271757aff69faf5371c64
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56127429"
---
# <a name="set-up-actions-for-non-compliance"></a>Configuración de acciones de no cumplimiento

Las **acciones de no cumplimiento** permiten configurar una secuencia de acciones que se aplican a dispositivos que no cumplen determinadas directivas. Por ejemplo, envíe correos electrónicos al usuario final de dispositivos no conformes o márquelos como no conformes.



## <a name="before-you-begin"></a>Antes de comenzar

> [!IMPORTANT]  
> Par establecer acciones para los casos de no cumplimiento, cree primero al menos una directiva de cumplimiento de dispositivos.  

Estas son las acciones que se admiten para el no cumplimiento:

- Envío de correos electrónicos al usuario final
- Marcado de dispositivos como no conformes

### <a name="send-e-mail-to-end-user"></a>Envío de correos electrónicos al usuario final

Elija entre plantillas de correo electrónico predeterminadas creadas previamente o cree una notificación de correo electrónico personalizada. Configuration Manager permite personalizar el asunto, el cuerpo del mensaje, incluido el logotipo de la empresa, la información de contacto y destinatarios adicionales.

### <a name="mark-devices-non-compliant"></a>Marcado de dispositivos como no conformes

Determine una programación en número de días durante los cuales se debe bloquear el dispositivo para que no acceda a los recursos corporativos. Esta acción puede ser inmediata, pero también puede asignar al usuario un período de gracia para que cumpla las directivas de cumplimiento de dispositivos.

### <a name="supported-platforms"></a>Plataformas admitidas

Compatible con [todas las plataformas que se administran mediante Intune](https://docs.microsoft.com/intune/supported-devices-browsers).



## <a name="to-add-an-email-template"></a>Incorporación de una plantilla de correo electrónico

Configuration Manager proporciona plantillas de correo electrónico, pero también puede crear las suyas propias. La plantilla de correo electrónico se usa más adelante en el proceso de creación de acciones de no cumplimiento para comunicarse con los usuarios.

1. En la consola de Configuration Manager, elija **Activos y compatibilidad**.  

2. En el área de trabajo **Activos y compatibilidad**, expanda **Configuración de cumplimiento** y, luego, haga clic en **Plantillas de notificación de cumplimiento**.  

3. En la pestaña **Inicio**, en **Crear plantilla de notificación de cumplimiento**.  

4. Escriba la información siguiente:  

    a. **Nombre**: Nombre de la plantilla de correo electrónico  

    > [!Note]  
    > El campo **De** se rellena automáticamente con una dirección de correo electrónico sin respuesta de Microsoft.<!--SCCMDocs issue 652-->  

    c. **Asunto**: Un tema que explica la notificación de correo electrónico que se envían  

    d. **Cuerpo del mensaje**: Obtener más detalles sobre la notificación de correo electrónico  

    > [!TIP]  
    > También puede incluir el **encabezado de correo electrónico** con el logotipo de la empresa y el **pie de página de correo electrónico**, que puede incluir información de contacto y el nombre de la empresa. También puede modificar esta información en las propiedades de la suscripción de Intune.  

5. Haga clic en **Aceptar** para guardar la nueva plantilla de correo electrónico.  

6. En la página **Agregar acción**, seleccione la nueva plantilla de correo electrónico de la lista.  

7. Una vez que la seleccione, haga clic en **Aceptar**.  



## <a name="to-create-actions-for-non-compliance"></a>Creación de acciones de no cumplimiento

1. En la consola de Configuration Manager, elija **Activos y compatibilidad**.  

2. En el área de trabajo **Activos y compatibilidad**, expanda **Configuración de cumplimiento** y, a continuación, haga clic en **Directivas de cumplimiento**.  

3. En la pestaña **Inicio**, en el grupo **Crear**, elija **Crear directiva de cumplimiento**.  

4. Seleccione las **plataformas admitidas** que desee y después haga clic en **Siguiente** dos veces. Puede omitir la página **Reglas**.  

5. En la página **Acciones de no cumplimiento**, se define lo que ocurre cuando un dispositivo no cumple una determinada directiva; para ello, haga clic en **Nuevo**.  

6. Puede elegir dos opciones: **Enviar correo electrónico al usuario final** o **marcar el dispositivo como no conforme**.  

7. Si selecciona **Enviar correo electrónico a usuario final**, especifique lo siguiente:  

    a. **Período de gracia (en días):** Escriba un número de días entre 0 y 365  

    b. **Destinatarios adicionales (a través de correo electrónico)**  

    c. **Seleccione la plantilla de mensaje:** Elija una plantilla de correo electrónico predeterminado o personalizado que ha creado.  
    
    > [!TIP]   
    > También puede agregar una nueva plantilla de correo electrónico al agregar la acción **Enviar correo electrónico a usuario final** haciendo clic en la opción **Nuevo:** de la página **Agregar acción**.  

8. Si selecciona **Marcar el dispositivo como no conforme**, debe especificar lo siguiente:  

    a. **Período de gracia (en días):** Escriba un número de días entre 0 y 365  

9. Complete el asistente.  

