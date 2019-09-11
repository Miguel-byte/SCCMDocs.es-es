---
title: Cómo cerrar la cuenta
titleSuffix: Configuration Manager
description: Cómo quitar el análisis de escritorio de la cuenta de Azure
ms.date: 09/10/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 6e7d2850-b0af-497e-bbc1-bfc2a7420a7a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 387d16b75c688640eba0ed6658b281badd3c7c54
ms.sourcegitcommit: 13ac4f5e600dc1edf69e8566e00968f40e1d1761
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/11/2019
ms.locfileid: "70891737"
---
# <a name="how-to-close-your-account"></a>Cómo cerrar la cuenta

> [!Note]  
> Esta información está relacionada con un servicio de vista previa que se puede modificar sustancialmente antes de que se publique comercialmente. Microsoft no ofrece ninguna garantía, expresa o implícita, con respecto a la información aquí proporcionada.  

Si configura el análisis de escritorio en su entorno y, a continuación, decide que debe quitarlo, use este proceso para cerrar su cuenta.

## <a name="prerequisites"></a>Requisitos previos

Solo un **administrador global** puede cerrar o reactivar la cuenta en el Azure portal.

## <a name="process-to-offboard"></a>Proceso para externalización

1. Abra el [portal de análisis de escritorio](https://aka.ms/desktopanalytics) en Microsoft 365 la administración de dispositivos como usuario con el rol de **administrador global** .

1. En el menú **configuración global** , seleccione **servicios conectados**. En la sección inscribir dispositivos, seleccione la opción **externalización**.

1. Si decide continuar, la cuenta está cerrada.

> [!Important]
> Continúe con el resto de este artículo después de 90 días, o bien, si no va a volver a activarlo.
>
> Si desea cerrar completamente su cuenta sin esperar 90 días, [restablezca](/sccm/desktop-analytics/account-reset) primero la cuenta.

## <a name="reactivate"></a>Reactivar

Durante los próximos 90 días, cualquier administrador de la organización que acceda al portal de análisis de escritorio verá un aviso de que ha optado por externalización.

Un administrador global puede volver A activar la cuenta en un plazo de 90 días. Para restaurar el análisis de escritorio de su organización, seleccione la opción para **volver**.

## <a name="delete-the-solution"></a>Eliminar la solución

> [!Warning]
> Continúe con el resto de este artículo después de 90 días, o bien, si no va a volver a activarlo. Si elimina y desconecta estos otros componentes, no intente reactivar.

1. Inicie sesión en el [Azure portal](https://portal.azure.com) como usuario con el rol de **administrador global** .

1. Busque en **todos los recursos** el nombre del área de trabajo de análisis de escritorio. Este nombre es lo que creó al suscribirse al servicio.

1. Eliminación `Microsoft365Analytics(YourWorkspaceName)` de la **solución**de tipo.

Los datos de análisis de escritorio caducan en función de la Directiva de retención de datos para el área de trabajo. Puede seguir usando cualquier otra solución en la misma área de trabajo.

> [!Important]  
> Si utiliza el área de trabajo Log Analytics con otras soluciones, como Windows Analytics, no elimine el área de trabajo.

## <a name="remove-user-and-app-access"></a>Quitar el acceso de usuario y de aplicación

1. Inicie sesión en el [Azure portal](https://portal.azure.com) como usuario con el rol de **administrador global** . Vaya a **Azure Active Directory**.

1. En **roles y administradores**, busque el rol de **Administrador de Desktop Analytics** . Quite sus miembros.

1. En **grupos**, quite los miembros de los siguientes grupos:

    - **Administradores de cliente de M365 Analytics (propietarios de Log Analytics)**
    - **Administradores de cliente de M365 Analytics (colaboradores Log Analytics)**

1. En **aplicaciones empresariales**, elimine o revoque los permisos de acceso para las siguientes aplicaciones:

    - `MaLogAnalyticsReader`

    - Aplicación de Configuration Manager. Para buscar el nombre de esta aplicación, vaya a la consola de Configuration Manager. En el área de trabajo **Administración** , expanda **Cloud Services**y seleccione el nodo **servicios de Azure** . Abra las propiedades del servicio de **análisis de escritorio** y cambie a la pestaña **aplicaciones** . La **aplicación web** es esta aplicación de Azure.

        > [!Important]  
        > Antes de realizar cambios en esta aplicación en Azure AD, asegúrese de que no la está reutilizando con otro servicio en Configuration Manager.

## <a name="disconnect-configuration-manager"></a>Desconectar Configuration Manager

1. Abra la consola de Configuration Manager como un usuario con el rol de **Administrador total** .

1. Vaya al área de trabajo **Administración** , expanda **Cloud Services**y seleccione el nodo **servicios de Azure** .

1. Elimine el servicio de análisis de escritorio.

## <a name="reconfigure-clients"></a>Volver a configurar los clientes

### <a name="unenroll-devices"></a>Anulación de la inscripción de dispositivos

En los dispositivos inscritos, quite el valor CommercialID de las siguientes claves del registro de Windows:

- `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`
- `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

### <a name="windows-diagnostic-data-configuration"></a>Configuración de datos de diagnóstico de Windows

Si no quiere que los dispositivos sigan enviando datos de diagnóstico:

- Windows 10: establecimiento del nivel de datos de diagnóstico en **seguridad**
- Windows 7 SP1 o 8,1: deshabilitar la **clave de participación de datos comerciales**

Establezca estos valores con uno de los métodos siguientes:

- Directiva de grupo, **en configuración** > del equipo**plantillas administrativas** > **componentes** > **de Windows recopilación de datos y compilaciones de vista previa**
- Administración de dispositivos móviles (MDM), como [Microsoft Intune](https://docs.microsoft.com/intune/device-restrictions-windows-10#reporting-and-telemetry)

Para obtener más información, consulte [Configurar los datos de diagnóstico de Windows en la organización](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization).

> [!NOTE]  
> Al aplicar estos cambios, los dispositivos dejan de enviar datos de diagnóstico inmediatamente. Microsoft puede tardar 24-48 horas en detener el procesamiento de la información del área de trabajo. Microsoft elimina estos datos de sus servicios en la nube en un plazo de 30 días o menos.
