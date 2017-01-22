---
title: "Aspectos básicos de la administración de clientes | Microsoft Docs"
description: "Obtenga información sobre las tareas que puede ejecutar para administrar clientes de System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8d4e5641-354e-4439-8b4f-620a760e233d
caps.latest.revision: 4
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: 9648fc831e21f8a5ee6e12cfe7754933ba9f6239


---
# <a name="fundamentals-of-client-management-tasks-for-system-center-configuration-manager"></a>Aspectos básicos de las tareas de administración de clientes de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Después de instalar los clientes de System Center Configuration Manager, hay varias tareas que puede ejecutar para administrar los clientes.  Algunas se inician desde la consola de Configuration Manager, mientras que otras puede iniciarse o visualizarse en un cliente desde la aplicación Configuration Manager de clientes en el panel de control de Windows.  

## <a name="the-console"></a>La consola  
 Desde la consola de Configuration Manager, puede realizar varias tareas de administración de clientes, como las siguientes:  

-   Implementar aplicaciones, actualizaciones de software, scripts de mantenimiento y sistemas operativos. Puede configurar estos elementos para instalarlos en una determinada fecha y hora, o hacer que los usuarios los puedan instalar cuando se soliciten, y puede configurar la desinstalación de aplicaciones.  

-   Permite proteger equipos contra malware y amenazas de seguridad, y notificar la detección de problemas.  

-   Definir los valores de configuración de cliente que desea supervisar y corregir si están en situaciones de no cumplimiento.  

-   Recopilar información de inventario de hardware y software que incluye la supervisión y la conciliación de información de licencias de Microsoft.  

-   Solucionar problemas de equipos mediante el control remoto.  

-   Implementar la configuración de administración de energía para administrar y supervisar el consumo energético de los equipos.  

Para supervisar estas operaciones casi en tiempo real, puede usar la consola de Configuration Manager para ver alertas e información de estado. Para capturar datos y tendencias históricas, puede utilizar las funciones de informes integradas de SQL Reporting Services.  Los clientes envían detalles al sitio como estado de cliente.  La información de estado de cliente proporciona datos sobre el estado del cliente y la actividad del cliente, y puede verse en la consola o mediante informes integrados para Configuration Manager. Estos datos le permiten identificar los equipos que no responden y, en algunos casos, corregir problemas automáticamente.  

 Para más información sobre las tareas de administración para los clientes, consulte [Cómo administrar clientes en System Center Configuration Manager](../../core/clients/manage/manage-clients.md) y [Cómo administrar clientes para servidores Linux y UNIX en System Center Configuration Manager](../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md). Para más información acerca del uso de informes, consulte   
            [Introducción a los informes en System Center Configuration Manager](../../core/servers/manage/introduction-to-reporting.md)  

## <a name="the-windows-control-panel-app"></a>La aplicación del panel de control de Windows  
 Al instalar el software cliente de Configuration Manager, se instala la aplicación cliente de **Configuration Manager** en el Panel de control. A diferencia del Centro de Software, esta aplicación está diseñada para los integrantes del departamento de soporte técnico y no para los usuarios finales. Algunas opciones de configuración requieren permisos administrativos locales y la mayoría de las opciones requieren conocimientos técnicos sobre el funcionamiento de Configuration Manager. Puede utilizar esta aplicación para realizar las siguientes tareas en un cliente:  

-   Ver propiedades sobre el cliente, como el número de compilación, su sitio asignado, el punto de administración con el que se comunica y si el cliente usa un certificado PKI o un certificado autofirmado.  

-   Confirmar que el cliente ha descargado correctamente la directiva de cliente después de la instalación inicial, y que la configuración de cliente está habilitada o deshabilitada como se esperaba según la configuración de cliente establecida en la consola de Configuration Manager.  

-   Iniciar acciones de cliente, como la descarga de la directiva de cliente si hubo cambios recientes de configuración en la consola de Configuration Manager y no quiere esperar hasta la próxima programación.  

-   Asignar manualmente un cliente a un sitio de Configuration Manager o intentar encontrar un sitio, y especificar el sufijo DNS para los puntos de administración que publican en DNS.  

-   Configurar la memoria caché de cliente que almacena temporalmente archivos y eliminar archivos en la memoria caché si necesita más espacio en disco para instalar software.  

-   Configurar opciones para la administración de cliente basada en Internet.  

-   Ver líneas de base de configuración implementadas en el cliente, iniciar la evaluación de compatibilidad y ver informes de cumplimiento.  



<!--HONumber=Dec16_HO3-->


