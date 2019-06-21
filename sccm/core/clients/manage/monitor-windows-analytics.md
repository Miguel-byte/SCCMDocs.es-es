---
title: Supervisión de clientes con Windows Analytics
titleSuffix: Configuration Manager
description: Windows Analytics es un conjunto de soluciones que permiten extraer información valiosa sobre el estado actual de su entorno.
ms.date: 09/04/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: CF35CE87-3BA8-4A84-9BC8-ABCEA4666212
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7836e1779acbfdfbb66d6eac57bc7797abd52563
ms.sourcegitcommit: 3936b869d226cea41fa0090e2cbc92bd530db03a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/20/2019
ms.locfileid: "67286476"
---
# <a name="use-windows-analytics-with-configuration-manager"></a>Uso de Windows Analytics con Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

[Windows Analytics](https://docs.microsoft.com/windows/deployment/update/windows-analytics-overview) es un conjunto de soluciones que permiten obtener información sobre el estado actual de su entorno. Los dispositivos de Windows de su entorno enviarán datos a Microsoft, que puede revisar y analizar a través de estas soluciones. Por ejemplo, conecte [Upgrade Readiness](/sccm/core/clients/manage/upgrade-readiness) a Configuration Manager para tener acceso directo a los datos del área de trabajo **Supervisión** de la consola de Configuration Manager.

Los datos que utiliza Windows Analytics no se transfieren directamente al servidor de sitio de Configuration Manager. Los equipos cliente envían datos al servicio en la nube de Windows. Después, este servicio transfiere los datos pertinentes a las soluciones de Windows Analytics hospedadas en una de las áreas de trabajo de la organización. Configuration Manager luego lo dirige a los datos pertinentes en el portal web con enlaces en contexto. También puede mostrar directamente datos que forman parte de las soluciones que conectó a Configuration Manager.

> [!Important]  
> Configuration Manager informa a Microsoft de los datos de uso y diagnóstico. Estos datos son independientes de los datos de Windows Analytics. Para obtener más información, vea [Diagnósticos y datos de uso](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data).  



## <a name="configure-clients-to-report-data-to-windows-analytics"></a>Configuración de clientes para notificar datos a Windows Analytics

Para que los dispositivos de cliente envíen datos a Windows Analytics, configúrelos con una *clave de identificación comercial*. Esta clave es el área de trabajo de Log Analytics de Azure que hospeda los datos de Windows Analytics. Configure también los dispositivos para que notifiquen los datos en un nivel correspondiente a las soluciones concretas que quiera usar. 

### <a name="configure-windows-analytics-client-settings"></a>Configurar los ajustes de cliente de Windows Analytics
Para configurar Windows Analytics: 
1. En la consola de Configuration Manager, vaya al área de trabajo **Administración** y seleccione el nodo **Configuración de cliente**.  
2. En la cinta, seleccione **Create Custom Device Client Settings** (Crear configuración de cliente de dispositivo personalizada).  
3. Agregue el grupo de **Windows Analytics** a esta directiva de configuración de cliente de dispositivo personalizada.  

Para obtener más información sobre cómo crear configuraciones de cliente de dispositivo personalizadas, vea [Cómo establecer la configuración de cliente](/sccm/core/clients/deploy/configure-client-settings).

Seleccione la pestaña de configuración de **Windows Analytics** y configure las opciones siguientes:  

#### <a name="manage-windows-telemetry-settings-with-configuration-manager"></a>Administración de la configuración de telemetría de Windows con Configuration Manager
Esta configuración debe ser **Sí** para configurar los valores de datos de diagnóstico de Windows en los clientes de Windows.   

#### <a name="commercial-id-key"></a>Clave de identificador comercial
La clave de identificador comercial asigna información desde los dispositivos que administra hasta el área de trabajo de Log Analytics que hospeda los datos de Windows Analyitics de su organización. Si ya ha configurado una clave de identificador comercial para su uso con Upgrade Readiness, úsela. Si todavía no tiene una clave de identificador comercial, vea [Copie la clave de ID de comercial](https://docs.microsoft.com/windows/deployment/update/windows-analytics-get-started#copy-your-commercial-id-key).

#### <a name="windows-10-telemetry"></a>Telemetría de Windows 10
Para obtener más información, consulte [Configurar los datos de diagnóstico de Windows en la organización](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#diagnostic-data-levels).

> [!Note]  
> Ahora puede también establecer el nivel de recopilación de datos de Windows 10 en **Mejorado (limitado)** . Esta configuración le permite obtener información práctica sobre los dispositivos de su entorno sin que los dispositivos informen de todos los datos del nivel **Mejorado** con Windows 10, versión 1709 o una versión posterior. El nivel Mejorado (limitado) incluye métricas del nivel Básico, así como un subconjunto de datos recopilados del nivel Mejorado que resulta relevante para Windows Analytics.

#### <a name="windows-81-and-earlier-telemetry"></a>Telemetría de Windows 8.1 y versiones anteriores   
Para obtener más información, vea [Windows 7, Windows 8, and Windows 8.1 appraiser telemetry events and fields](https://go.microsoft.com/fwlink/?LinkID=822965) (Eventos y campos de telemetría de evaluador de Windows 7, Windows 8 y Windows 8.1).

#### <a name="enable-windows-81-and-earlier-internet-explorer-data-collection"></a>Habilitación de la recopilación de datos de Internet Explorer de Windows 8.1 y versiones anteriores
En dispositivos que ejecutan Windows 8.1 o versiones anteriores, Internet Explorer puede recopilar datos acerca de las aplicaciones web. Estos datos pueden permitir que Upgrade Readiness detecte incompatibilidades de aplicaciones web que podrían impedir una actualización sin problemas a Windows 10. Habilite la recopilación de datos de Internet Explorer en función de la zona de Internet. Para obtener más información acerca de las zonas de Internet, consulte la información sobre las [zonas de seguridad de las direcciones URL](https://docs.microsoft.com/previous-versions/windows/internet-explorer/ie-developer/platform-apis/ms537183\(v=vs.85\)).



## <a name="use-upgrade-readiness-to-identify-windows-10-compatibility-issues"></a>Uso de Upgrade Readiness para identificar problemas de compatibilidad de Windows 10

Upgrade Readiness permite analizar la preparación del dispositivo y la compatibilidad con Windows 10. Gracias a esta evaluación, las actualizaciones se realizan con menos problemas. Tras conectar Configuration Manager con Upgrade Readiness, se puede tener acceso a estos datos de compatibilidad de actualización del cliente directamente desde la consola de Configuration Manager. Después, seleccione los dispositivos para su actualización o corrección desde la lista de dispositivos.

Para obtener más información y detalles sobre cómo configurar Upgrade Readiness y conectarse a esta solución, consulte [Upgrade Readiness](/sccm/core/clients/manage/upgrade-readiness).



## <a name="use-windows-analytics-to-identify-gaps-in-windows-information-protection-policies"></a>Uso de Windows Analytics para identificar carencias en las directivas de Windows Information Protection

Puede configurar Windows 10, versión 1703, y dispositivos posteriores con una directiva de [Windows Information Protection](https://docs.microsoft.com/windows/threat-protection/windows-information-protection/protect-enterprise-data-using-wip) (WIP). Informan de datos de diagnóstico sobre aplicaciones que acceden a datos corporativos en su entorno pero que no están incluidos en las reglas de aplicación de directivas. Los usuarios pueden necesitar estas aplicaciones para mantener su productividad, pero WIP bloquea el acceso de los usuarios. Esta información es útil para mantener las directivas de Windows Information Protection en Configuration Manager. 

