---
title: Proteger los equipos frente al malware
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo implementar Endpoint Protection en Configuration Manager para proteger los equipos frente a los ataques de malware.
ms.date: 05/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 539c7a89-3c03-4571-9cb4-02d455064eeb
author: mestew
ms.author: mstewart
manager: doubeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: e1ab204a8b04b1e19b419a6bb3ca677fab660148
ms.sourcegitcommit: 18a94eb78043cb565b05cd0e9469b939b29cccf0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 05/29/2019
ms.locfileid: "66355075"
---
# <a name="example-scenario-use-endpoint-protection-to-protect-computers-from-malware"></a>Escenario de ejemplo: Uso de Endpoint Protection para proteger los equipos frente al malware

*Se aplica a: System Center Configuration Manager (Rama actual)*

En este artículo se proporciona un escenario de ejemplo sobre cómo se puede implementar Endpoint Protection en Configuration Manager para proteger los equipos de su organización de ataques de malware.  



## <a name="scenario-overview"></a>Información general del escenario

 System Center Configuration Manager está instalado y en uso en Woodgrove Bank. El banco usa actualmente System Center Endpoint Protection para proteger los equipos frente a ataques de malware. Además, el banco usa Directiva de grupo de Windows para asegurar que Firewall de Windows está habilitado en todos los equipos de la empresa y que se notifique a los usuarios cuando Firewall de Windows bloquee un nuevo programa.  

Se les ha pedido a los administradores de Configuration Manager que actualicen el software antimalware de Woodgrove Bank a System Center Endpoint Protection para que el banco pueda beneficiarse de las funciones antimalware más recientes y poder administrar de forma centralizada la solución antimalware desde la consola de Configuration Manager. 


## <a name="business-requirements"></a>Requisitos empresariales

Esta implementación tiene los siguientes requisitos:  

- Use Configuration Manager para administrar la configuración de Firewall de Windows, que está administrada actualmente por la directiva de grupo.  

- Use las actualizaciones de software de Configuration Manager para descargar las definiciones de malware en los equipos. Si las actualizaciones de software no están disponibles, por ejemplo, si el equipo no está conectado a la red corporativa, los equipos deben descargar las actualizaciones de definiciones desde Microsoft Update.  

- Los equipos de usuarios deben llevar a cabo un examen rápido de malware cada día. Los servidores, sin embargo, deben ejecutar un examen completo todos los sábados, fuera del horario comercial, a la 1 A.M.  

- Enviar una alerta de correo electrónico cada vez que se produzca cualquiera de los siguientes eventos:  

  -   Se detecta malware en cualquier equipo  

  -   Se detecta la misma amenaza de malware en más del 5 por ciento de los equipos  

  -   Se detecta la misma amenaza de malware más de cinco veces en cualquier período de 24 horas  

  -   Se detectan más de tres tipos de malware en cualquier período de 24 horas  

  Luego, los administradores siguen estos pasos para implementar Endpoint Protection:  



##  <a name="steps-to-implement-endpoint-protection"></a>Pasos para implementar la protección de extremo  

|Proceso|Referencia|  
|-------------|---------------|  
|Los administradores revisan la información disponible sobre los conceptos básicos de Endpoint Protection en Configuration Manager.|Para obtener información general sobre Endpoint Protection, consulte [Endpoint Protection in System Center Configuration Manager](endpoint-protection.md) (Endpoint Protection in System Center Configuration Manager).|  
|Los administradores revisan e implementan los requisitos previos necesarios para usar Endpoint Protection.|Para obtener información sobre los requisitos previos de Endpoint Protection, consulte [Planning for Endpoint Protection](../plan-design/planning-for-endpoint-protection.md) (Planeación de Endpoint Protection).|  
|Los administradores instalan el rol de sistema de sitio de Endpoint Protection únicamente en un servidor de sistema de sitios, en la parte superior de la jerarquía de Woodgrove Bank.|Para obtener más información sobre cómo instalar el rol de sistema de sitio de Endpoint Protection, consulte "Prerequisites" (Requisitos previos) en [Configure Endpoint Protection](configure-endpoint-protection.md) (Configurar Endpoint Protection).|  
|Los administradores configuran Configuration Manager para usar un servidor SMTP con el fin de enviar las alertas de correo electrónico.<br /><br /> **Nota:** debe configurar un servidor SMTP solo si quiere recibir una notificación por correo electrónico cuando se genere una alerta de Endpoint Protection.|Para obtener más información, consulte [Configure alerts in Endpoint Protection](endpoint-configure-alerts.md) (Configurar alertas en Endpoint Protection).|  
|Los administradores crean una recopilación de dispositivos que contiene todos los equipos y servidores para instalar el cliente de Endpoint Protection. Denominan esta recopilación **Todos los equipos protegidos por Endpoint Protection**.<br /><br /> **Sugerencia**: No puede configurar alertas para recopilaciones de usuario.|Para obtener más información sobre cómo crear recopilaciones, consulte [Cómo crear recopilaciones en System Center Configuration Manager](../../core/clients/manage/collections/create-collections.md).|  
|Los administradores configuran las siguientes alertas para la recopilación: <br /><br />1) **Se detectó malware**: los administradores configuran una gravedad de alerta de **Crítico**. <br /><br />2) **El mismo tipo de malware se detecta en varios equipos**: los administradores configuran una gravedad de alerta de **Crítico** y especifican que la alerta se generará cuando más de un 5 % de los equipos hayan detectado malware. <br /><br />3) **El mismo tipo de malware se detecta repetidamente en un equipo durante el intervalo especificado**: los administradores configuran una gravedad de alerta de Crítico y especifican que la alerta se generará cuando se detecte malware más de cinco veces en un período de 24 horas. <br /><br />4) **Se detectaron varios tipos de malware en un mismo equipo durante el intervalo especificado**: los administradores configuran una gravedad de alerta de Crítico y especifican que la alerta se generará cuando se detecten más de tres tipos de malware en un período de 24 horas.<br /><br /> El valor de **Gravedad de alerta** indica el nivel de alerta que se mostrará en la consola de Configuration Manager y en las alertas que reciben en un mensaje de correo electrónico.<br /><br /> Además, seleccionan la opción **Ver esta recopilación en el panel de Endpoint Protection** para poder supervisar las alertas en el consola de Configuration Manager.|Consulte "Configure Alerts for Endpoint Protection" (Configurar alertas para Endpoint Protection) en [Configuring Endpoint Protection in System Center Configuration Manager](endpoint-configure-alerts.md) (Configurar Endpoint Protection en System Center Configuration Manager).|  
|Los administradores configuran las actualizaciones de software de Configuration Manager para descargar e implementar actualizaciones de definiciones tres veces al día mediante una regla de implementación automática.|Para obtener más información, consulte la sección "Using Configuration Manager Software Updates to Deliver Definition Updates" (Uso de las actualizaciones de software de Configuration Manager para entregar actualizaciones de definiciones) del tema [Use Configuration Manager software updates to deliver definition updates](endpoint-definitions-configmgr.md) (Uso de las actualizaciones de software de Configuration Manager para entregar actualizaciones de definiciones).|  
|Los administradores examinan la configuración de la directiva antimalware predeterminada, que contiene la configuración de seguridad recomendada de Microsoft. Para que los equipos realicen un examen rápido diario, cambian la configuración siguiente:<br /><br /> 1) **Ejecutar un examen rápido diario en los equipos cliente**: **Sí**.<br /><br /> 2) **Tiempo de programación de examen rápido diario**:  **9:00 AM**.<br /><br /> Los administradores se dan cuenta de que **Actualizaciones distribuidas desde Microsoft Update** está seleccionada de forma predeterminada como un origen de actualización de definiciones. De este modo, se cumple el requisito empresarial según el cual los equipos deben descargar definiciones desde Microsoft Update cuando no se reciban actualizaciones de software de Configuration Manager.|Consulte [Crear e implementar directivas antimalware para Endpoint Protection en System Center Configuration Manager](endpoint-antimalware-policies.md).|  
|Los administradores crean una recopilación que contiene solo los servidores de Woodgrove Bank denominados **Servidores de Woodgrove Bank**.|Consulte [Cómo crear recopilaciones en System Center Configuration Manager](../../core/clients/manage/collections/create-collections.md).|  
|Los administradores crean una directiva antimalware personalizada denominada **Directiva de servidor de Woodgrove Bank**. Agregan solo la configuración de **Exámenes programados** y realizan los siguientes cambios:<br /><br /> **Tipo de examen**:  **Completo**<br /><br /> **Día de examen**:  **Sábado**<br /><br /> **Hora de examen**: **1:00 a.m.**<br /><br /> **Programar un examen rápido diario en los equipos cliente**:  **No**.|Consulte [Crear e implementar directivas antimalware para Endpoint Protection en System Center Configuration Manager](endpoint-antimalware-policies.md).|  
|Los administradores implementan la directiva antimalware personalizada **Directiva de servidor de Woodgrove Bank** en la recopilación **Servidores de Woodgrove Bank**.|Vea "Implementar una directiva antimalware en los equipos cliente" del artículo [Crear e implementar directivas antimalware para Endpoint Protection en System Center Configuration Manager](endpoint-antimalware-policies.md).|  
|Los administradores crean un conjunto de opciones de configuración de dispositivo cliente personalizada para Endpoint Protection y lo denominan **Configuración de Endpoint Protection de Woodgrove Bank**.<br /><br /> **Nota**: Si no quiere instalar y habilitar Endpoint Protection en todos los clientes de la jerarquía, asegúrese de que las opciones **Administrar el cliente de Endpoint Protection en equipos cliente** e **Instalar cliente de Endpoint Protection en equipos cliente** están configuradas como **No** en la configuración de cliente predeterminada.|Para obtener más información, consulte [Configure Custom Client Settings for Endpoint Protection](endpoint-protection-configure-client.md) (Configurar opciones de cliente personalizadas para Endpoint Protection).|  
|Configuran las opciones siguientes para Endpoint Protection:<br /><br /> **Administrar el cliente de Endpoint Protection en equipos cliente**:  **Sí**<br /><br /> Esta configuración y este valor garantizan que cualquier cliente de Endpoint Protection existente que se instale esté administrado por Configuration Manager.<br /><br /> **Instalar cliente de Endpoint Protection en equipos cliente**:  **Sí**.</br></br>**Nota**: A partir de la versión 1802 de Configuration Manager, no es necesario que los dispositivos con Windows 10 tengan instalado el agente de Endpoint Protection. Si ya está instalado en los dispositivos Windows 10, Configuration Manager no lo quitará. Los administradores pueden quitar el Agente de Endpoint Protection en los dispositivos Windows 10 en los que se ejecute como mínimo la versión 1802 del cliente.|Para obtener más información, consulte [Configure Custom Client Settings for Endpoint Protection](endpoint-protection-configure-client.md) (Configurar opciones de cliente personalizadas para Endpoint Protection).|  
|Los administradores implementan la configuración de cliente **Configuración de Endpoint Protection de Woodgrove Bank** en la recopilación **Todos los equipos protegidos por Endpoint Protection**.|Consulte la sección “Configure Custom Client Settings for Endpoint Protection” (Configurar opciones de cliente personalizadas para Endpoint Protection) del tema [Configuring Endpoint Protection in Configuration Manager](endpoint-antimalware-policies.md) (Configurar Endpoint Protection en Configuration Manager).|  
|Los administradores usan el Asistente para crear directivas de Firewall de Windows para crear una directiva mediante la configuración de los siguientes valores para el perfil de dominio:<br /><br /> 1) **Habilitar Firewall de Windows**: **Sí**<br /><br /> 2)<br />                    **Notificar al usuario cuando Firewall de Windows bloquea un nuevo programa**: **Sí**|Consulte [Crear e implementar directivas de Firewall de Windows para Endpoint Protection](../../protect/deploy-use/create-windows-firewall-policies.md).|  
|Los administradores implementan la nueva directiva de firewall en la recopilación **Todos los equipos protegidos por Endpoint Protection** que crearon anteriormente.|Consulte “To deploy a Windows Firewall policy” (Para implementar una directiva de Firewall de Windows) en el tema [Crear e implementar directivas de Firewall de Windows para Endpoint Protection](create-windows-firewall-policies.md).|  
|Los administradores usan las tareas de administración disponibles para que Endpoint Protection administre las directivas antimalware y de Firewall de Windows, efectúe análisis de equipos a petición cuando sea necesario, obligue a los equipos a descargar las últimas definiciones y especifique otras acciones que se deban llevar a cabo cuando se detecte malware.|Consulte [Administrar las directivas antimalware y la configuración de firewall para Endpoint Protection en System Center Configuration Manager](endpoint-antimalware-firewall.md).|  
|Los administradores usan los métodos siguientes para supervisar el estado de Endpoint Protection y las acciones que lleva a cabo Endpoint Protection:<br /><br /> 1) Mediante el uso del nodo **Estado de Endpoint Protection** en **Seguridad** del área de trabajo **Supervisión**.<br /><br /> 2) Mediante el uso del nodo **Endpoint Protection** del área de trabajo **Activos y compatibilidad**.<br /><br /> 3) Mediante los informes integrados de Configuration Manager.|Consulte [Cómo supervisar Endpoint Protection en System Center Configuration Manager](monitor-endpoint-protection.md).|  

 Los administradores notifican la implementación correcta de Endpoint Protection a su administrador y confirman que ahora los equipos de Woodgrove Bank están protegidos contra malware, según los requisitos empresariales que se le asignaron. 

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información, vea [Configurar Endpoint Protection](/sccm/protect/deploy-use/endpoint-protection-configure).