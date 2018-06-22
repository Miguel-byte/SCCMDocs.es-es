---
title: Supervisión de clientes con Windows Analytics
titleSuffix: Configuration Manager
description: Windows Analytics es un conjunto de soluciones que se ejecutan en Operations Management Suite que permiten extraer información valiosa sobre el estado actual del entorno. Para ello, aprovecha los datos de telemetría de Windows que notifican los dispositivos de dicho entorno.
ms.date: 01/02/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: CF35CE87-3BA8-4A84-9BC8-ABCEA4666212
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e792f421520798a0e000384aafcb99f31dc8eb14
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32336143"
---
# <a name="use-windows-analytics-with-configuration-manager"></a>Uso de Windows Analytics con Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

[Windows Analytics](https://www.microsoft.com/WindowsForBusiness/windows-analytics) es un conjunto de soluciones que se ejecutan en [Operations Management Suite](/azure/operations-management-suite/operations-management-suite-overview) (OMS). Estas soluciones permiten obtener información del estado actual del entorno. Los dispositivos de su entorno notifican datos de telemetría de Windows y estos datos se pueden analizar, además de accederse a ellos, mediante soluciones del [portal web de Operations Management Suite](https://mms.microsoft.com). Mediante la conexión de [Upgrade Readiness](/sccm/core/clients/manage/upgrade/upgrade-analytics) a Configuration Manager, se puede tener acceso directo a los datos del nodo **Supervisión** de la consola de Configuration Manager.

Los datos de telemetría de Windows que utiliza Windows Analytics no se transfieren directamente al servidor de sitio de Configuration Manager. Los equipos cliente envían los datos de telemetría de Windows al servicio de telemetría de Windows. Después, este servicio transfiere los datos pertinentes a las soluciones de Windows Analytics hospedadas en una de las áreas de trabajo de OMS de la organización. Configuration Manager puede llevarle a los datos pertinentes en el portal web con vínculos en contexto, o bien mostrar directamente los datos que forman parte de las soluciones que se han conectado a Configuration Manager. También se pueden consultar directamente los datos desde el portal web de Operations Management Suite.

>[!Important]
>[Los datos de diagnóstico y uso de Configuration Manager](../../plan-design/diagnostics/diagnostics-and-usage-data.md), que el servidor de sitio de Configuration Manager notifica a Microsoft, son independientes de Windows Analytics y la telemetría de Windows.

## <a name="configure-clients-to-report-data-to-windows-analytics"></a>Configuración de clientes para notificar datos a Windows Analytics

Para que los dispositivos cliente notifiquen datos a Windows Analytics, debe configurarlos con una clave de id. comercial asociada con el área de trabajo de OMS en la que se hospedan los datos de Windows Analytics. También debe configurar los dispositivos para que notifiquen la telemetría en un nivel correspondiente a las soluciones concretas que quiera usar. 

### <a name="configure-windows-analytics-client-settings"></a>Configurar los ajustes de cliente de Windows Analytics
Para configurar Windows Analytics, en la consola de Configuration Manager vaya a **Administración** > **Configuración de cliente**, haga doble clic en **Create Custom Device Client Settings** (Crear configuración de cliente de dispositivo personalizada) y, después, seleccione **Windows Analytics**.  

Después de desplazarse a la pestaña de configuración de **Windows Analytics**, configure las opciones siguientes:
  -  **Clave de id. comercial**  
La clave de identificador comercial asigna información desde los dispositivos que administra hasta el área de trabajo de OMS que hospeda los datos de Windows Analyitics de su organización. Si ya ha configurado una clave de identificador comercial para su uso con Upgrade Readiness, úsela. Si todavía no tiene una clave de identificador comercial, vea cómo [generar la clave de identificador comercial]( https://technet.microsoft.com/itpro/windows/deploy/upgrade-readiness-get-started#generate-your-commercial-id-key).

  -  **Nivel de telemetría para los dispositivos Windows 10**   
Para obtener información sobre cada nivel de telemetría de Windows 10, vea [Configurar la telemetría de Windows en la organización](https://technet.microsoft.com/itpro/windows/manage/configure-windows-telemetry-in-your-organization#telemetry-levels).

   > [!Note]
   > Con la versión 1710, puede establecer el nivel de recopilación de datos de telemetría de Windows 10 en **Mejorado (limitado)**. Esta configuración le permite obtener información práctica sobre los dispositivos de su entorno sin que los dispositivos informen de todos los datos del nivel de telemetría **Mejorado** con Windows 10, versión 1709 o una versión posterior. El nivel de telemetría Mejorado (limitado) incluye métricas del nivel Básico, así como un subconjunto de datos recopilados del nivel Mejorado que resulta relevante para Windows Analytics.


  -  **Sistema de registro de usuario para recopilar datos comerciales en dispositivos Windows 7, 8 y 8.1**   
Para obtener más información, vea [Windows 7, Windows 8, and Windows 8.1 appraiser telemetry events and fields](https://go.microsoft.com/fwlink/?LinkID=822965) (Eventos y campos de telemetría de evaluador de Windows 7, Windows 8 y Windows 8.1).

  -  **Configurar la recopilación de datos de Internet Explorer**  
En los dispositivos que ejecutan Windows 8.1 o versiones anteriores, la recopilación de datos de Internet Explorer puede permitir que Upgrade Readiness detecte incompatibilidades de aplicaciones web que podrían impedir una actualización sin problemas a Windows 10. La recopilación de datos de Internet Explorer se puede habilitar en función de cada zona de Internet. Para obtener más información acerca de las zonas de Internet, consulte la información sobre las [zonas de seguridad de las direcciones URL](https://msdn.microsoft.com/library/ms537183(v=vs.85).aspx).

## <a name="use-upgrade-readiness-to-identify-windows-10-compatibility-issues"></a>Uso de Upgrade Readiness para identificar problemas de compatibilidad de Windows 10

Upgrade Readiness (antes Upgrade Analytics) permite analizar la preparación del dispositivo y la compatibilidad con Windows 10. Gracias a esta evaluación, las actualizaciones se realizan con menos problemas. Tras conectar Configuration Manager con Upgrade Readiness, se puede tener acceso a estos datos de compatibilidad de actualización del cliente directamente desde la consola de Configuration Manager. Después, seleccione los dispositivos para su actualización o corrección desde la lista de dispositivos.

Para obtener más información y detalles sobre cómo configurar Upgrade Readiness y conectarse a esta solución, consulte [Upgrade Readiness](../../clients/manage/upgrade/upgrade-analytics.md).

## <a name="use-windows-analytics-to-identify-gaps-in-windows-information-protection-policies"></a>Uso de Windows Analytics para identificar carencias en las directivas de Windows Information Protection

Los dispositivos Windows 10 de la versión 1703 y posteriores configurados con una directiva de [Windows Information Protection](https://docs.microsoft.com/windows/threat-protection/windows-information-protection/protect-enterprise-data-using-wip) (WIP) notifican la telemetría en las aplicaciones que tienen acceso a los datos corporativos del entorno, pero no se incluyen las reglas de aplicación de las directivas de WIP. Los usuarios pueden necesitar estas aplicaciones para mantener su productividad, pero WIP bloquea el acceso de los usuarios. Saber que los usuarios tienen acceso a los datos corporativos es útil para el mantenimiento de las directivas de Windows Information Protection en Configuration Manager. 

Obtenga acceso a estos datos de Windows Information Protection mediante esta [consulta de Operations Management Suite](https://go.microsoft.com/fwlink/?linkid=849952).