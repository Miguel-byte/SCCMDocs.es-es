---
title: Configurar Wake On LAN
titleSuffix: Configuration Manager
description: Seleccione la configuración de Wake on LAN en System Center Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: b475a0c8-85d6-4cc4-b11f-32c0cc98239e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: e8e486cd2aad20e9ae0017abed3bb776768c3182
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56138745"
---
# <a name="how-to-configure-wake-on-lan-in-system-center-configuration-manager"></a>Cómo configurar Wake on LAN en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Especifique la configuración de Wake On LAN para System Center Configuration Manager si quiere reactivar los equipos que están en estado de suspensión para instalar el software necesario, por ejemplo, actualizaciones de software, aplicaciones, secuencias de tareas y programas.

Puede complementar Wake On LAN mediante la configuración de cliente de proxy de reactivación. No obstante, para usar el proxy de reactivación, primero debe habilitar Wake On LAN para el sitio y especificar **Usar paquetes de reactivación solamente** y la opción **Unidifusión** para el método de transmisión de Wake On LAN. Esta solución de reactivación también admite conexiones ad hoc, por ejemplo, una conexión a Escritorio remoto.

Utilice el primer procedimiento para configurar un sitio primario para Wake On LAN. Luego, use el segundo procedimiento para especificar la configuración de cliente de proxy de reactivación. Este segundo procedimiento configura las opciones de cliente predeterminadas para la configuración de proxy de reactivación que se aplicarán a todos los equipos de la jerarquía. Si desea que esta configuración solo se aplique a equipos seleccionados, cree una configuración de dispositivo personalizada y asígnela a una recopilación que contenga los equipos que desea configurar para el proxy de reactivación. Para obtener más información acerca de cómo crear configuraciones de cliente personalizadas, consulte [Cómo establecer la configuración del cliente en Configuration Manager](../../../core/clients/deploy/configure-client-settings.md).

Un equipo que recibe la configuración de cliente de proxy de reactivación es probable que detenga su conexión de red entre 1 y 3 segundos. Esto ocurre porque el cliente debe restablecer la tarjeta de interfaz de red para habilitar el controlador de proxy de reactivación en ella.

> [!WARNING]
> Para evitar una interrupción inesperada en los servicios de red, primero evalúe el proxy de reactivación en una infraestructura de red aislada y representativa. A continuación, utilice la configuración de cliente personalizada para expandir la prueba a un grupo seleccionado de equipos en varias subredes. Para más información sobre el funcionamiento del proxy de reactivación, vea [Planear la reactivación de clientes en System Center Configuration Manager](../../../core/clients/deploy/plan/plan-wake-up-clients.md).

## <a name="to-configure-wake-on-lan-for-a-site"></a>Para configurar Wake On LAN para un sitio

1. En la consola de Configuration Manager, vaya a **Administración > Configuración del sitio > Sitios**.
2. Haga clic en el sitio primario para configurar y, luego, haga clic en **Propiedades**.
3. Haga clic en la pestaña **Wake on LAN** y configure las opciones que necesite para este sitio. Para admitir el proxy de reactivación, asegúrese de seleccionar **Usar paquetes de reactivación solamente** y **Unidifusión**. Para más información, vea [Planear la reactivación de clientes en System Center Configuration Manager](../../../core/clients/deploy/plan/plan-wake-up-clients.md).
4. Haga clic en **Aceptar** y repita este procedimiento para todos los sitios primarios de la jerarquía.

## <a name="to-configure-wake-up-proxy-client-settings"></a>Para configurar el cliente proxy de reactivación

1. En la consola de Configuration Manager, vaya a **Administración > Configuración de cliente**.
2. Haga clic en **Configuración de cliente predeterminada** y luego en **Propiedades**.
3. Seleccione **Administración de energía** y luego elija **Sí** para **Habilitar proxy de reactivación**.
4. Revise y, si es necesario, configure las demás opciones del proxy de reactivación. Para más información sobre esta configuración, vea [Power management settings (Configuración de administración de energía)](../../../core/clients/deploy/about-client-settings.md#power-management).
5. Haga clic en **Aceptar** para cerrar el cuadro de diálogo y, luego, haga clic en **Aceptar** para cerrar el cuadro de diálogo Configuración de cliente predeterminada.

Puede utilizar los siguientes informes de Wake On LAN para supervisar la instalación y la configuración del proxy de reactivación:

- Resumen de estado de implementación de proxy de reactivación
- Detalles de estado de implementación de proxy de reactivación

> [!TIP]
> Para comprobar si el proxy de reactivación está en funcionamiento, pruebe la conexión en un equipo inactivo. Por ejemplo, establezca una conexión con una carpeta compartida en ese equipo o intente conectarse al equipo mediante Escritorio remoto. Si usa Direct Access, compruebe que los prefijos IPv6 funcionan realizando las mismas pruebas para un equipo inactivo que se encuentra actualmente en Internet.
