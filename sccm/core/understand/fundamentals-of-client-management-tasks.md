---
title: Aspectos básicos de la administración de clientes
titleSuffix: Configuration Manager
description: Obtenga información sobre las tareas que ejecuta para administrar clientes de System Center Configuration Manager.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8d4e5641-354e-4439-8b4f-620a760e233d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e517b345340619055b03df22638ec0b491c13d40
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32339101"
---
# <a name="fundamentals-of-client-management-tasks-for-system-center-configuration-manager"></a>Aspectos básicos de las tareas de administración de clientes de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Después de instalar los clientes de System Center Configuration Manager, hay varias tareas que ejecuta para administrar los clientes.  Algunas de las tareas se ejecutan desde la consola de Configuration Manager. Otras tareas se ejecutan desde la aplicación cliente de Configuration Manager. La aplicación cliente de Configuration Manager se instala con el software cliente de Configuration Manager.

## <a name="configuration-manager-console-tasks"></a>Tareas de la consola de Configuration Manager
 En la consola de Configuration Manager, puede realizar varias tareas de administración de clientes:  

-   Implementar aplicaciones, actualizaciones de software, scripts de mantenimiento y sistemas operativos. Configurar la instalación de una determinada fecha y hora, hacer que el software esté disponible para que los usuarios lo puedan instalar cuando se les pida o configurar la desinstalación de aplicaciones.  

-   Permite proteger equipos contra malware y amenazas de seguridad, y notificar la detección de problemas.  

-   Definir los valores de configuración de cliente que quiere supervisar y corregir si están en situaciones de no cumplimiento.  

-   Recopilar información de inventario de hardware y software que incluye la supervisión y la conciliación de información de licencias de Microsoft.  

-   Solucionar problemas de equipos mediante el control remoto.  

-   Implementar la configuración de administración de energía para administrar y supervisar el consumo energético de los equipos.  

La consola de Configuration Manager supervisa las tareas anteriores casi en tiempo real. La información de estado y notificaciones de cada tarea está disponible en la consola de Configuration Manager. Para capturar datos y tendencias históricas, use las funciones de informes integradas de SQL Server Reporting Services. Los clientes envían detalles al sitio como estado de cliente.  La información de estado de cliente proporciona datos sobre el estado del cliente y la actividad del cliente, y puede verse en la consola o mediante informes integrados para Configuration Manager. Estos datos le permiten identificar los equipos que no responden y, en algunos casos, corregir problemas automáticamente.  

 Para más información sobre las tareas de administración para los clientes, consulte [Cómo administrar clientes en System Center Configuration Manager](../../core/clients/manage/manage-clients.md) y [Cómo administrar clientes para servidores Linux y UNIX en System Center Configuration Manager](../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md). Para más información acerca del uso de informes, consulte   
            [Introducción a los informes en System Center Configuration Manager](../../core/servers/manage/introduction-to-reporting.md)  

## <a name="configuration-manager-client-application"></a>Aplicación cliente de Configuration Manager  
 Al instalar el software cliente de Configuration Manager, también se instala la aplicación cliente de Configuration Manager. A diferencia del Centro de Software, la aplicación cliente de Configuration Manager está diseñada para los integrantes del departamento de soporte técnico y no para el usuario final. Algunas opciones de configuración requieren permisos administrativos locales y la mayoría de las opciones requieren conocimientos técnicos sobre el funcionamiento de la aplicación cliente de Configuration Manager. Puede utilizar esta aplicación para realizar las siguientes tareas en un cliente:  

-   Ver propiedades sobre el cliente, como el número de compilación, su sitio asignado, el punto de administración con el que se comunica y si el cliente usa un certificado de infraestructura de clave pública (PKI) o un certificado autofirmado.  

-   Asegurarse de que el cliente haya descargado correctamente una directiva de cliente después de que el cliente se instale por primera vez. Asegurarse también de que la configuración de cliente esté habilitada o deshabilitada según lo previsto, de acuerdo con la configuración de cliente que está configurada en la consola de Configuration Manager.  

-   Iniciar acciones de cliente. Por ejemplo, descargue la directiva de cliente si hubo cambios recientes de configuración en la consola de Configuration Manager y no quiere esperar hasta la próxima programación.  

-   Asignar manualmente un cliente a un sitio de Configuration Manager o intentar buscar un sitio. Después, especificar el sufijo del sistema de nombre de dominio (DNS) para los puntos de administración que publique en DNS.  

-   Configurar la caché del cliente que almacena temporalmente los archivos. Después, eliminar archivos en la caché si necesita más espacio en disco para instalar software.  

-   Configurar opciones para la administración de cliente basada en Internet.  

-   Ver líneas de base de configuración implementadas en el cliente, iniciar la evaluación de compatibilidad y ver informes de cumplimiento.  
