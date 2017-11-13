---
title: 'Escenario: Endpoint Protection protege los equipos frente al malware'
titleSuffix: Configuration Manager
description: "Obtenga información sobre cómo implementar Endpoint Protection en Configuration Manager para proteger los equipos frente a los ataques de malware."
ms.custom: na
ms.date: 03/13/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 539c7a89-3c03-4571-9cb4-02d455064eeb
caps.latest.revision: "8"
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: a0aa02a9091ea9ecdd060f1e7023e9d3f95269a1
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/12/2017
---
# <a name="example-scenario-using-system-center-endpoint-protection-to-protect-computers-from-malware-in-system-center-configuration-manager"></a>Escenario de ejemplo: uso de System Center Endpoint Protection para proteger los equipos frente al malware en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Este tema proporciona un escenario de ejemplo sobre la implementación de Endpoint Protection en Configuration Manager para proteger los equipos de una organización de ataques malintencionados.  

 Juan es el administrador de Configuration Manager en Woodgrove Bank. El banco usa actualmente System Center Endpoint Protection para proteger los equipos frente a ataques de malware. Además, el banco usa Directiva de grupo de Windows para asegurar que Firewall de Windows está habilitado en todos los equipos de la empresa y que se notifique a los usuarios cuando Firewall de Windows bloquee un nuevo programa.  

 Se le ha pedido a Juan que actualice el software antimalware de Woodgrove Bank a System Center Endpoint Protection para que el banco pueda beneficiarse de las funciones antimalware más recientes y poder administrar de forma centralizada la solución antimalware desde la consola de Configuration Manager. Esta implementación tiene los siguientes requisitos:  

-   Use Configuration Manager para administrar la configuración de Firewall de Windows, que está administrada actualmente por la directiva de grupo.  

-   Use las actualizaciones de software de Configuration Manager para descargar las definiciones de malware en los equipos. Si las actualizaciones de software no están disponibles, por ejemplo, si el equipo no está conectado a la red corporativa, los equipos deben descargar las actualizaciones de definiciones desde Microsoft Update.  

-   Los equipos de usuarios deben llevar a cabo un examen rápido de malware cada día. Los servidores, sin embargo, deben ejecutar un examen completo todos los sábados, fuera del horario comercial, a la 1 A.M.  

-   Enviar una alerta de correo electrónico cada vez que se produzca cualquiera de los siguientes eventos:  

    -   Se detecta malware en cualquier equipo  

    -   Se detecta la misma amenaza de malware en más del 5 por ciento de los equipos  

    -   Se detecta la misma amenaza de malware más de 5 veces en cualquier período de 24 horas  

    -   Se detectan más de 3 tipos de malware en cualquier período de 24 horas  

-   Se desinstala la solución antimalware existente.  

 Luego, Juan lleva a cabo los siguientes pasos para implementar Endpoint Protection:  

##  <a name="steps-to-implement-endpoint-protection"></a>Pasos para implementar la protección de extremo  

|Proceso|Referencia|  
|-------------|---------------|  
|Juan revisa la información disponible sobre los conceptos básicos de Endpoint Protection en Configuration Manager.|Para obtener información general sobre Endpoint Protection, consulte [Endpoint Protection in System Center Configuration Manager](endpoint-protection.md) (Endpoint Protection in System Center Configuration Manager).|  
|Juan revisa e implementa los requisitos previos necesarios para usar Endpoint Protection.|Para obtener información sobre los requisitos previos de Endpoint Protection, consulte [Planning for Endpoint Protection](../plan-design/planning-for-endpoint-protection.md) (Planeación de Endpoint Protection).|  
|Juan instala el rol de sistema de sitio de Endpoint Protection únicamente en un servidor de sistema de sitios, en la parte superior de la jerarquía de Woodgrove Bank.|Para obtener más información sobre cómo instalar el rol de sistema de sitio de Endpoint Protection, consulte "Prerequisites" (Requisitos previos) en [Configure Endpoint Protection](configure-endpoint-protection.md) (Configurar Endpoint Protection).|  
|Juan configura Configuration Manager para usar un servidor SMTP para enviar las alertas de correo electrónico.<br /><br /> **Nota:** debe configurar un servidor SMTP solo si quiere recibir una notificación por correo electrónico cuando se genere una alerta de Endpoint Protection.|Para obtener más información, consulte [Configure alerts in Endpoint Protection](endpoint-configure-alerts.md) (Configurar alertas en Endpoint Protection).|  
|Juan crea una recopilación de dispositivos que contiene todos los equipos y servidores para instalar el cliente de Endpoint Protection. Denomina esta recopilación **Todos los equipos protegidos por Endpoint Protection**.<br /><br /> **Sugerencia:** no puede configurar alertas para recopilaciones de usuario.|Para obtener más información sobre cómo crear recopilaciones, consulte [How to create collections in System Center Configuration Manager](../../core/clients/manage/collections/create-collections.md) (Cómo crear recopilaciones en System Center Configuration Manager).|  
|Configura las siguientes alertas para la colección: <br /><br />1) **Se detecta software malintencionado**: Juan configura una gravedad de alerta de **crítico**. <br /><br />2) **El mismo tipo de malware se detecta en un número de equipos**: Juan configura una gravedad de alerta de **crítico** y especifica que la alerta se generará cuando más de un 5 por ciento de los equipos tengan software malintencionado detectado. <br /><br />3) **El mismo tipo de malware se detecta repetidamente en el intervalo especificado en un equipo**: Juan configura una gravedad de alerta de **crítico** y especifica que la alerta se generará cuando se detecte software malintencionado más de 5 veces en un período de 24 horas. <br /><br />4) **Se detectan varios tipos de malware en el mismo equipo en el intervalo especificado**: Juan configura una gravedad de alerta de **crítico** y especifica que la alerta se generará cuando se generen más de 3 tipos de malware en un período de 24 horas.<br /><br /> El valor de **Gravedad de alerta** indica el nivel de alerta que se mostrará en la consola de Configuration Manager y en las alertas que recibe en un mensaje de correo electrónico.<br /><br /> Además, selecciona la opción **Ver esta recopilación en el panel de Endpoint Protection** para poder supervisar las alertas en el consola de Configuration Manager.|Consulte "Configure Alerts for Endpoint Protection" (Configurar alertas para Endpoint Protection) en [Configuring Endpoint Protection in System Center Configuration Manager](endpoint-configure-alerts.md) (Configurar Endpoint Protection en System Center Configuration Manager).|  
|Juan configura las actualizaciones de software de Configuration Manager para descargar e implementar actualizaciones de definiciones tres veces al día mediante una regla de implementación automática.|Para obtener más información, consulte la sección "Using Configuration Manager Software Updates to Deliver Definition Updates" (Uso de las actualizaciones de software de Configuration Manager para entregar actualizaciones de definiciones) del tema [Use Configuration Manager software updates to deliver definition updates](endpoint-definitions-configmgr.md) (Uso de las actualizaciones de software de Configuration Manager para entregar actualizaciones de definiciones).|  
|Juan examina la configuración de la directiva antimalware predeterminada, que contiene la configuración de seguridad recomendada de Microsoft. Para que los equipos realicen un examen rápido diario, cambia la configuración siguiente:<br /><br /> 1) **Ejecutar un examen rápido diario en los equipos cliente**: **Sí**.<br /><br /> 2) **Tiempo de programación de examen rápido diario**:  **9:00 AM**.<br /><br /> Juan se da cuenta de que **Actualizaciones distribuidas desde Microsoft Update** está seleccionada de forma predeterminada como un origen de actualización de definiciones. De este modo se cumple el requisito de empresarial según el cual los equipos deben descargar definiciones desde Microsoft Update cuando no se reciban actualizaciones de software de Configuration Manager.|Consulte [How to create and deploy antimalware policies for Endpoint Protection in System Center Configuration Manager](endpoint-antimalware-policies.md) (Crear e implementar directivas antimalware para Endpoint Protection en System Center Configuration Manager).|  
|Juan crea una recopilación que contiene solo los servidores de Woodgrove Bank denominados **Servidores de Woodgrove Bank**.|Consulte [Cómo crear recopilaciones en System Center Configuration Manager](../../core/clients/manage/collections/create-collections.md).|  
|Juan crea una directiva antimalware personalizada denominada **Directiva de servidor de Woodgrove Bank**. Agrega solo la configuración de **Exámenes programados** y realiza los siguientes cambios:<br /><br /> **Tipo de examen**:  **Completo**<br /><br /> **Día de examen**:  **Sábado**<br /><br /> **Hora de examen**: **1:00 a.m.**<br /><br /> **Programar un examen rápido diario en los equipos cliente**:  **No**.|Consulte [How to create and deploy antimalware policies for Endpoint Protection in System Center Configuration Manager](endpoint-antimalware-policies.md) (Crear e implementar directivas antimalware para Endpoint Protection en System Center Configuration Manager).|  
|Juan implementa la directiva antimalware personalizada **Directiva de servidor de Woodgrove Bank** a la recopilación **Servidores de Woodgrove Bank** .|Consulte la sección “To deploy an antimalware policy to client computers” (Para implementar una directiva antimalware en los equipos cliente) del tema [How to create and deploy antimalware policies for Endpoint Protection](endpoint-antimalware-policies.md) (Crear e implementar directivas antimalware para Endpoint Protection).|  
|Juan crea un nuevo conjunto de opciones de configuración de dispositivo cliente personalizada para Endpoint Protection y lo denomina **Configuración de Endpoint Protection de Woodgrove Bank**.<br /><br /> **Nota**: Si no quiere instalar y habilitar Endpoint Protection en todos los clientes de la jerarquía, asegúrese de que las opciones **Administrar el cliente de Endpoint Protection en equipos cliente** e **Instalar cliente de Endpoint Protection en equipos cliente** están configuradas como **No** en la configuración de cliente predeterminada.|Para obtener más información, consulte [Configure Custom Client Settings for Endpoint Protection](endpoint-protection-configure-client.md) (Configurar opciones de cliente personalizadas para Endpoint Protection).|  
|Configura las opciones siguientes para Endpoint Protection:<br /><br /> **Administrar el cliente de Endpoint Protection en equipos cliente**:  **Sí**<br /><br /> Esta configuración y este valor garantizan que cualquier cliente de Endpoint Protection existente que se instale esté administrado por Configuration Manager.<br /><br /> **Instalar cliente de Endpoint Protection en equipos cliente**:  **Sí**.<br /><br /> **Quitar automáticamente el software antimalware instalado anteriormente antes de instalar Endpoint Protection**:  **Sí**.<br /><br /> Esta configuración y el valor cumplen el requisito empresarial de que se quite el software antimalware existente antes de que Endpoint Protection esté instalado y habilitado.|Para obtener más información, consulte [Configure Custom Client Settings for Endpoint Protection](endpoint-protection-configure-client.md) (Configurar opciones de cliente personalizadas para Endpoint Protection).|  
|Juan implementa la configuración de cliente **Configuración de Endpoint Protection de Woodgrove Bank** en la recopilación **Todos los equipos protegidos por Endpoint Protection**.|Consulte la sección “Configure Custom Client Settings for Endpoint Protection” (Configurar opciones de cliente personalizadas para Endpoint Protection) del tema [Configuring Endpoint Protection in Configuration Manager](endpoint-antimalware-policies.md) (Configurar Endpoint Protection en Configuration Manager).|  
|Juan usa el Asistente para crear directivas de Firewall de Windows para crear una directiva mediante la configuración de los siguientes valores para el perfil de dominio:<br /><br /> 1) **Habilitar Firewall de Windows**: **Sí**<br /><br /> 2)<br />                    **Notificar al usuario cuando Firewall de Windows bloquea un nuevo programa**: **Sí**|Consulte [How to create and deploy Windows Firewall policies for Endpoint Protection in System Center Configuration Manager](../../protect/deploy-use/create-windows-firewall-policies.md) (Crear e implementar directivas de Firewall de Windows para Endpoint Protection).|  
|Juan implementa la nueva directiva de firewall en la recopilación **Todos los equipos protegidos por Endpoint Protection** que creó anteriormente.|Consulte “To deploy a Windows Firewall policy” (Para implementar una directiva de Firewall de Windows) en el tema [How to create and deploy Windows Firewall policies for Endpoint Protection in System Center Configuration Manager](create-windows-firewall-policies.md) (Crear e implementar directivas de Firewall de Windows para Endpoint Protection).|  
|Juan usa las tareas de administración disponibles para que Endpoint Protection administre las directivas antimalware y de Firewall de Windows, efectúe análisis de equipos a petición cuando sea necesario, obligue a los equipos a descargar las últimas definiciones y especifique otras acciones que se deban llevar a cabo cuando se detecte malware.|Consulte [How to manage antimalware policies and firewall settings for Endpoint Protection in System Center Configuration Manager](endpoint-antimalware-firewall.md) (Administrar las directivas antimalware y la configuración de firewall para Endpoint Protection en System Center Configuration Manager).|  
|Juan usa los métodos siguientes para supervisar el estado de Endpoint Protection y las acciones que lleva a cabo Endpoint Protection:<br /><br /> 1) Mediante el uso del nodo **Estado de Endpoint Protection** en **Seguridad** del área de trabajo **Supervisión**.<br /><br /> 2) Mediante el uso del nodo **Endpoint Protection** del área de trabajo **Activos y compatibilidad**.<br /><br /> 3) Mediante los informes integrados de Configuration Manager.|Consulte [How to monitor Endpoint Protection in System Center Configuration Manager](monitor-endpoint-protection.md) (Cómo supervisar Endpoint Protection en System Center Configuration Manager).|  

 Juan notifica la implementación correcta de Endpoint Protection a su administrador y confirma que ahora los equipos de Woodgrove Bank están protegidos contra antimalware, según los requisitos empresariales que se le asignaron.
