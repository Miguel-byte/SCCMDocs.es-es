---
title: Cómo cerrar su cuenta
titleSuffix: Configuration Manager
description: Cómo quitar el análisis de escritorio de su cuenta de Azure
ms.date: 06/11/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 6e7d2850-b0af-497e-bbc1-bfc2a7420a7a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 805cb79a1986457f04b11fa5f99b30ec098be99b
ms.sourcegitcommit: 659976b943226c5124057429ac7444989f98433f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2019
ms.locfileid: "67159204"
---
# <a name="how-to-close-your-account"></a>Cómo cerrar su cuenta

> [!Note]  
> Esta información se relaciona con un servicio en versión preliminar que puede modificarse sustancialmente antes de su lanzamiento comercial. Microsoft no ofrece ninguna garantía, expresa o implícita, con respecto a la información aquí proporcionada.  

Si la configuración de análisis de escritorio en su entorno y, a continuación, decide que necesita quitarlo, utilice este proceso para cerrar su cuenta.

## <a name="contact-support"></a>Póngase en contacto con soporte técnico

El primer paso es ponerse en contacto con Microsoft Support. Abra una incidencia de soporte técnico para cerrar su cuenta de análisis de escritorio. No continúe con los pasos adicionales hasta que reciba la confirmación de que Microsoft cierra su cuenta.

## <a name="delete-the-solution"></a>Eliminar la solución

1. Inicie sesión en el [portal Azure](https://portal.azure.com) como un usuario con el **Administrador de la compañía** rol.

1. Buscar en **todos los recursos** para el nombre del área de trabajo de análisis de escritorio. Este nombre es lo que ha creado al registrarse para el servicio.

1. Eliminar `Microsoft365Analytics(YourWorkspaceName)` typu **solución**.

Los datos de análisis de escritorio anticuado según la directiva de retención de datos del área de trabajo. Puede seguir usando otras soluciones en la misma área de trabajo.

> [!Important]  
> Si usa el área de trabajo de Log Analytics con otras soluciones, como Windows Analytics, no elimine el área de trabajo.

## <a name="remove-user-and-app-access"></a>Quitar el acceso de usuario y aplicación

1. Inicie sesión en el [portal Azure](https://portal.azure.com) como un usuario con el **Administrador de la compañía** rol. Vaya a **Azure Active Directory**.

1. En **Roles y administradores**, busque el **administrador escritorio Analytics** rol. Quitar a sus miembros.

1. En **grupos**, quitar los miembros de los grupos siguientes:

    - **M365 Los administradores de cliente de análisis (propietarios de Log Analytics)**
    - **M365 Los administradores de cliente de análisis (colaboradores de Log Analytics)**

1. En **aplicaciones empresariales**, eliminar o revocar permisos de acceso para las siguientes aplicaciones:

    - `MaLogAnalyticsReader`

    - La aplicación de Configuration Manager. Para buscar el nombre de la aplicación, vaya a la consola de Configuration Manager. En el **administración** área de trabajo, expanda **servicios en la nube**y seleccione el **Azure Services** nodo. Abra las propiedades de la **escritorio Analytics** de servicio y cambie a la **aplicaciones** ficha. El **aplicación Web** es esta aplicación de Azure.

        > [!Important]  
        > Antes de realizar cambios en esta aplicación en Azure AD, asegúrese de que no está reutilizando con otro servicio en Configuration Manager.

## <a name="disconnect-configuration-manager"></a>Desconectar Configuration Manager

1. Abra la consola de Configuration Manager como un usuario con el **Administrador total** rol.

1. Vaya a la **administración** área de trabajo, expanda **servicios en la nube**y seleccione el **Azure Services** nodo.

1. Eliminar el servicio de análisis de escritorio.

## <a name="reconfigure-clients"></a>Volver a configurar los clientes

### <a name="unenroll-devices"></a>Anular la inscripción de dispositivos

En los dispositivos inscritos, quite el valor CommercialID de las siguientes claves del registro de Windows:

- `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`
- `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

### <a name="windows-diagnostic-data-configuration"></a>Configuración de datos de diagnóstico de Windows

Si no desea que los dispositivos puedan continuar enviando datos de diagnóstico:

- Windows 10: establecer el nivel de datos de diagnóstico en **seguridad**
- Windows 7 SP1 o 8.1: deshabilitar el **datos comerciales participación en claves**

Establecer estos valores mediante uno de los métodos siguientes:

- Directiva de grupo en **configuración del equipo** > **plantillas administrativas** > **componentes de Windows**  >  **Recopilación de datos y las compilaciones de versión preliminar**
- Administración de dispositivos móviles (MDM), como [Microsoft Intune](https://docs.microsoft.com/intune/device-restrictions-windows-10#reporting-and-telemetry)

Para obtener más información, consulte [Configurar los datos de diagnóstico de Windows en la organización](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization).

> [!NOTE]  
> Al aplicar estos cambios, los dispositivos detener inmediatamente el envío de datos de diagnóstico. Puede tardar 24 a 48 horas para que Microsoft pueda detener el procesamiento de información del área de trabajo. Microsoft elimina estos datos de sus servicios en la nube dentro de 30 días o menos.
