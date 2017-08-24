---
title: "Supervisión de clientes: uso de Windows Analytics con Configuration Manager | Microsoft Docs"
description: "Windows Analytics es un conjunto de soluciones que se ejecutan en Operations Management Suite que permiten extraer información valiosa sobre el estado actual del entorno. Para ello, aprovecha los datos de telemetría de Windows que notifican los dispositivos de dicho entorno."
ms.custom: na
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: CF35CE87-3BA8-4A84-9BC8-ABCEA4666212
caps.latest.revision: "23"
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.openlocfilehash: adabe8f475eb12dd44005ec07344e8565be20582
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/07/2017
---
# <a name="use-windows-analytics-with-configuration-manager"></a>Uso de Windows Analytics con Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

[Windows Analytics](https://www.microsoft.com/en-us/WindowsForBusiness/windows-analytics) es un conjunto de soluciones que se ejecutan en [Operations Management Suite](/azure/operations-management-suite/operations-management-suite-overview). Las soluciones permiten obtener información del estado actual del entorno. Los dispositivos del entorno notifican los datos de telemetría de Windows. Con las soluciones del [portal web de Operations Management Suite](https://mms.microsoft.com), se puede acceder a estos datos y también analizarse. En el caso de [Upgrade Readiness](/sccm/core/clients/manage/upgrade/upgrade-analytics), los datos también pueden publicarse directamente en el nodo de supervisión de la consola de Configuration Manager conectando Upgrade Readiness a Configuration Manager.

Los datos de telemetría de Windows que utiliza Windows Analytics no se transfieren directamente al servidor de sitio de Configuration Manager. Los equipos cliente envían los datos de telemetría de Windows al servicio de telemetría. Luego, los datos pertinentes se transfieren a las soluciones de Windows Analytics hospedadas en una de las áreas de trabajo de OMS de la organización. Configuration Manager puede enviarle los datos pertinentes en el portal web con vínculos en contexto o directamente mostrar aquellos que forman parte de las soluciones que se han conectado a Configuration Manager. También se pueden consultar directamente los datos desde el portal web de Operations Management Suite.

>[!Important]
>[Los datos de diagnóstico y uso de Configuration Manager](../../plan-design/diagnostics/diagnostics-and-usage-data.md), que se notifican a Microsoft desde el servidor de sitio de Configuration Manager, son totalmente independientes de Windows Analytics y el servicio de telemetría de Windows.

## <a name="configure-clients-to-report-data-to-windows-analytics"></a>Configuración de clientes para notificar datos a Windows Analytics

Para que los dispositivos cliente notifiquen los datos a Windows Analytics, deben configurarse con una clave de identificador comercial asociada con el área de trabajo de Operations Management Suite que hospeda los datos de Windows Analytics de la organización. Asimismo, deben configurarse para notificar la telemetría en un nivel correspondiente a la solución o las soluciones concretas que se van a utilizar. 

### <a name="configure-windows-analytics-client-settings"></a>Configurar los ajustes de cliente de Windows Analytics
Para configurar Windows Analytics, en la consola de Configuration Manager vaya a **Administración** > **Configuración de cliente**, haga doble clic en **Create Custom Device Client Settings** (Crear configuración de cliente de dispositivo personalizada) y, después, seleccione **Windows Analytics**.  

Configure lo siguiente después de acceder a la pestaña de configuración de **Windows Analytics**:
  -  **Identificador comercial**  
La clave de identificador comercial asigna información desde los dispositivos que administra hasta el área de trabajo de OMS que hospeda los datos de Windows Analyitics de su organización. Si ya ha configurado una clave de identificador comercial para su uso con Upgrade Readiness, úsela. Si todavía no tiene una clave de identificador comercial, vea cómo [generar la clave de identificador comercial]( https://technet.microsoft.com/itpro/windows/deploy/upgrade-readiness-get-started#generate-your-commercial-id-key).

  -  **Nivel de telemetría para los dispositivos Windows 10**   
Para obtener información sobre lo que recopila cada nivel de telemetría de Windows 10, vea la información para [configurar la telemetría de Windows en su organización](https://technet.microsoft.com/itpro/windows/manage/configure-windows-telemetry-in-your-organization#telemetry-levels).

  -  **Sistema de registro de usuario para recopilar datos comerciales en dispositivos Windows 7, 8 y 8.1**   
Para obtener información sobre los datos recopilados de estos sistemas operativos cuando participa, considere descargar el archivo pdf [Windows 7, Windows 8, and Windows 8.1 appraiser telemetry events and fields](https://go.microsoft.com/fwlink/?LinkID=822965) (Campos y eventos de telemetría de valoración de Windows 7, Windows 8 y Windows 8.1) de Microsoft.

  -  **Configurar la recopilación de datos de Internet Explorer**  
En los dispositivos que ejecutan Windows 8.1 o versiones anteriores, la recopilación de datos de Internet Explorer puede permitir que Upgrade Readiness detecte incompatibilidades de aplicaciones web que podrían impedir una actualización sin problemas a Windows 10. La recopilación de datos de Internet Explorer se puede habilitar en función de cada zona de Internet. Para obtener más información acerca de las zonas de Internet, consulte la información sobre las [zonas de seguridad de las direcciones URL](https://msdn.microsoft.com/library/ms537183(v=vs.85).aspx).

## <a name="use-upgrade-readiness-to-identify-windows-10-compatibility-issues"></a>Uso de Upgrade Readiness para identificar problemas de compatibilidad de Windows 10

Upgrade Readiness (antes Upgrade Analytics) permite analizar la preparación del dispositivo y la compatibilidad con Windows 10. Gracias a esta evaluación, las actualizaciones se realizan con menos problemas. Tras conectar Configuration Manager con Upgrade Readiness, podrá acceder a estos datos de compatibilidad de actualización del cliente directamente desde la consola de Configuration Manager. Después, podrá seleccionar dispositivos para su actualización o corrección desde la lista de dispositivos.

Para obtener más información y detalles sobre cómo configurar Upgrade Readiness y conectarse a esta solución, consulte [Upgrade Readiness](../../clients/manage/upgrade/upgrade-analytics.md).

## <a name="use-windows-analytics-to-identify-gaps-in-windows-information-protection-policies"></a>Uso de Windows Analytics para identificar carencias en las directivas de Windows Information Protection

Los dispositivos Windows 10 de la versión 1703 y posteriores que están configurados con una directiva de [Windows Information Protection](https://docs.microsoft.com/en-us/windows/threat-protection/windows-information-protection/protect-enterprise-data-using-wip) (WIP) notifican la telemetría en las aplicaciones que tienen acceso a los datos corporativos del entorno, pero no se tienen en cuenta en las reglas de aplicación de las directivas de WIP. Se trata de aplicaciones que posiblemente necesitan los usuarios del entorno para mantener su productividad, pero cuyo acceso se ha bloqueado, así que saber que acceden a los datos corporativos puede ser útil para mantener las directivas de Windows Information Protection en Configuration Manager. 

Puede acceder a estos datos de Windows Information Protection usando esta [consulta Operations Management Suite](https://go.microsoft.com/fwlink/?linkid=849952).