---
title: "Datos de diagnóstico para 1511 | System Center Configuration Manager"
description: "Obtenga información acerca de los niveles de datos de diagnóstico y uso que se recopilan en la versión 1511 de System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9e614ae1-47d2-4a93-ba0a-89dc50d1e266
caps.latest.revision: 4
author: Brenduns
ms.author: brenduns
manager: angrobe
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- hu-hu
- it-it
- ja-jp
- ko-kr
- nl-nl
- pl-pl
- pt-br
- pt-pt
- ru-ru
- sv-se
- tr-tr
- zh-cn
- zh-tw
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 3488efcd6638b538f05fae52dfd8918423a32b58

---
# <a name="levels-of-diagnostic-usage-data-collection-for-version-1511-of-system-center-configuration-manager"></a>Niveles de recopilación de datos de uso para diagnóstico para la versión 1511 de System Center Configuration Manager.

*Se aplica a: System Center Configuration Manager (Rama actual)*

La versión 1511 de System Center Configuration Manager recopila tres niveles de datos de diagnóstico y uso: **Básico**, **Mejorado** y **Completo**. De forma predeterminada, esta característica se establece en el nivel Mejorado. Las secciones siguientes proporcionan detalles adicionales de los datos que se recopilan por cada nivel.  

> [!IMPORTANT]  
>  Configuration Manager no recopila códigos de sitio o nombres de sitios, direcciones IP, nombres de usuario o equipo, direcciones físicas o direcciones de correo electrónico en los niveles Básico o Mejorado. Cualquier recopilación de esta información en el nivel Completo no es para ninguna finalidad (potencialmente se incluye en la información avanzada de diagnóstico como archivos de registro o instantáneas de memoria) y Microsoft no la usará para identificarle, ponerse en contacto con usted ni con fines publicitarios.  

##  <a name="a-namebkmkchangea-how-to-change-the-level"></a><a name="bkmk_change"></a> Cambio de nivel  
 Los administradores con un ámbito administrativo basado en roles que incluye los permisos **Modificar** en la clase de objeto **Sitio** pueden cambiar el nivel de datos recopilados en la configuración de datos de diagnóstico y uso de la consola de Configuration Manager.  

##  <a name="a-namebkmklevel1a-level-1---basic"></a><a name="bkmk_level1"></a> Nivel 1: Básico  
 El nivel Básico incluye datos sobre la jerarquía y es necesario para ayudar a mejorar su experiencia de instalación o actualización, así como para determinar qué actualizaciones de Configuration Manager son aplicables a la jerarquía.  

 A partir de System Center Configuration Manager versión 1511, este nivel incluye lo siguiente:  


-   Información de instalación (compilación, tipo de instalación, paquetes de idioma, características que ha habilitado, estado de implementación del paquete de actualización y errores)  

-   Métricas de rendimiento de la base de datos (información del procesamiento de replicación, los principales procedimientos almacenados de SQL Server mediante el uso de procesador y disco)  

-   Configuración básica de la base de datos (procesadores, configuración de clúster, configuración de vistas distribuidas)  

-   Esquema de base de datos de Configuration Manager (hash de todas las definiciones de objeto)  

-   Recuento de versiones de cliente de Configuration Manager y versiones de sistema operativo  

-   Recuento y sistema operativo de los dispositivos administrados y las directivas establecidas por Exchange Connector  

-   Recuento de idiomas de cliente y configuración regional  

-   Recuento de dispositivos Windows 10 por ramificación y compilación  

-   Datos básicos de la jerarquía del sitio de Configuration Manager (lista de sitios, tipo, versión, estado, número de cliente y zona horaria)  

-   Información básica del servidor de sistema de sitio (roles de sistema de sitio usados, estado de SSL y de Internet, sistema operativo, procesadores, máquina física o virtual)  

-   Estadísticas básicas de detección de usuarios (recuento de detección de usuarios, tamaños de grupo mínimo, máximo y promedio)  

-   Información básica de protección de punto de conexión (versiones de cliente antimalware)  

-   Recuentos básicos de aplicación y tipo de implementación (aplicaciones totales, aplicaciones totales con varios tipos de implementación, aplicaciones totales con dependencias, aplicaciones totales reemplazadas, recuento de tecnologías de implementación en uso)  

-   Recuentos básicos de OSD (imágenes)  

-   Tipos de puntos de distribución y puntos de administración e información básica de configuración (protegida, preconfigurada, PXE, multidifusión, estado de SSL, puntos de distribución de extracción o del mismo nivel, MDM habilitado, SSL habilitado, etc.)  

-   Estadísticas de telemetría (cuando se ejecutan, tiempo de ejecución, errores)  

##  <a name="a-namebkmklevel2a-level-2---enhanced"></a><a name="bkmk_level2"></a> Nivel 2: Mejorado  
El nivel Mejorado es el valor predeterminado después de la instalación. Este nivel incluye datos recopilados en el nivel Básico, así como datos específicos de característica (frecuencia y duración de uso), configuración de cliente de Configuration Manager (nombre de componente, estado y determinadas opciones como intervalos de sondeo) e información básica sobre las actualizaciones de software.  

Se recomienda este nivel porque proporciona a Microsoft los datos mínimos necesarios para realizar mejoras útiles en versiones futuras de productos y servicios. En este nivel no se recopilan nombres de objetos (sitios, usuarios, equipos u objetos), detalles de objetos relacionados con la seguridad o vulnerabilidades como recuentos de sistemas que necesitan actualizaciones de software.  

A partir de System Center Configuration Manager versión 1511, este nivel incluye lo siguiente:  

-   **Administración de aplicaciones:**  

    -   Información básica de uso o destino para tipos de implementación usados en la organización (usuario frente a dispositivo de destino, necesario frente a disponible)  

    -   Información sobre la implementación de aplicaciones (instalación o desinstalación, necesita aprobación, interacción de usuario habilitada o deshabilitada)  

    -   Estadísticas de solicitudes de aplicación disponibles  

    -   Número de paquetes por tipo  

    -   Recuento de aplicabilidad de aplicación por sistema operativo  

    -   Recuento de implementaciones de paquete o programa  

    -   Recuentos de entornos de App-V y propiedades de implementación  

    -   Recuento de licencias de aplicación con licencia de Windows 10  

    -   Número mínimo y máximo y promedio de implementaciones de aplicaciones por usuario o dispositivo  

    -   Duración y el tipo de ventana de mantenimiento  

-   **Cliente:**  

    -   Lista o recuento de agentes de cliente habilitados  

    -   Recuento de instalaciones de cliente de cada tipo de ubicación de origen  

    -   Recuento de errores de instalación de cliente  

-   **Configuración de cumplimiento:**  

    -   Recuento de elementos de configuración por tipo o  

    -   Información básica de línea de base de configuración (recuento, número de implementaciones y número de referencias)  

    -   Recuento de las implementaciones que hacen referencia a valores integrados (no se captura la opción de configuración)  

    -   Recuento de reglas e implementaciones creadas para la configuración personalizada  

    -   Recuento de plantillas implementadas del Protocolo de inscripción de certificados simple  

-   **Contenido:**  

    -   Recuento de límites por tipo  

    -   Información de grupo de límites (recuento de límites y sistemas de sitio asignados a cada grupo de límites)  

    -   Información de grupo de puntos de distribución (recuento de paquetes y puntos de distribución asignados a cada grupo de puntos de distribución)  

    -   Información de configuración de punto de distribución (uso de caché de ramificación, supervisión de punto de distribución)  

    -   Información de configuración del administrador de distribuciones (subprocesos, intervalo entre reintentos, número de reintentos, configuración de punto de distribución de extracción)  

-   **Endpoint Protection:**  

    -   Antimalware de Endpoint Protection y uso de directivas de Firewall de Windows (número de directivas únicas asignadas al grupo; no incluye información sobre la configuración incluida en la directiva)  

    -   Errores de implementación de EndPoint Protection (recuento de códigos de error de implementación de directiva de Endpoint Protection)  

    -   Recuento de recopilaciones seleccionadas para que aparezcan en el panel de Endpoint Protection  

    -   Recuento de alertas configuradas para la característica de Endpoint Protection  

-   **Administración de aplicaciones móviles (MAM)**  

    -   Recuento de aplicaciones Office con MAM habilitado y de línea de negocio y directiva de sistema operativo  

    -   Recuento de implementaciones de directiva de aplicación MAM  

    -   Recuento de reglas creadas por la configuración de MAM  

-   **Administración de dispositivos móviles (MDM)**  

    -   Recuento de comandos de acciones de dispositivo móvil (bloquear, restablecer PIN, borrar y retirar) emitidos  

    -   Recuento de dispositivos móviles administrados por Configuration Manager y Microsoft Intune, así como la forma en que se inscribieron (masiva, según el usuario)  

    -   Duración de la comprobación de estadísticas y programación de sondeo de dispositivos móviles  

    -   Recuento de directivas de dispositivos móviles  

    -   Recuento de usuarios con varios dispositivos móviles inscritos  

-   **Solución de problemas de Microsoft Intune:**  

    -   Recuento y tamaño de los mensajes de estado, condición, inventario, RDR, DDR, UDX, estado de inquilino, POL, LOG, certificado, CRP, resincronización, CFD, RDO, BEX, ISM y de cumplimiento descargados de Microsoft Intune  

    -   Recuento y tamaño de los mensajes de acciones de dispositivo (borrar, retirar, bloquear), telemetría y de datos replicados en Microsoft Intune  

    -   Estadísticas de sincronización de usuario completas y diferenciales para Microsoft Intune  

-   **Administración local de dispositivos móviles (MDM):**  

    -   Estadísticas de implementaciones correctas o con errores para las implementaciones locales de aplicaciones MDM  

    -   Recuento de perfiles y paquetes de inscripción masiva de Windows 10  

-   **Implementación de sistema operativo:**  

    -   Recuento de imágenes de arranque, controladores, paquetes de controladores, puntos de distribución habilitados para multidifusión, puntos de distribución habilitados para PXE y secuencias de tareas  

-   **Actualizaciones de software:**  

    -   Número total o promedio de recopilaciones que tienen implementaciones de actualización de software y número máximo o promedio de actualizaciones implementadas  

    -   Número de reglas de implementación automática asociadas a la sincronización  

    -   Número de reglas de implementación automática que crean actualizaciones nuevas o agregan otras a un grupo existente  

    -   Diferencias disponibles y de fecha límite usadas en reglas de implementación automática  

    -   Número promedio y máximo de las asignaciones por actualización  

    -   Recuento de actualizaciones creadas e implementadas con System Center Updates Publisher  

    -   Recuento de grupos de actualizaciones y asignaciones  

    -   Recuento de paquetes de actualización y el número mínimo, máximo y promedio de puntos de distribución de destino con paquetes  

    -   Número de grupos de actualizaciones y número mínimo, máximo y promedio de actualizaciones por grupo  

    -   Número de actualizaciones y porcentaje de las actualizaciones implementadas, caducadas, sustituidas, descargadas y que contienen CLUF  

    -   Códigos de error de búsqueda de actualizaciones y recuento de máquinas  

    -   Evaluación de actualizaciones de cliente y programaciones de búsquedas  

    -   Programación de la sincronización del punto de actualización de software  

    -   Número de reglas de implementación automática con varias implementaciones  

    -   Configuraciones usadas para planes de mantenimiento activos de Windows 10  

    -   Versiones de contenido del panel de Windows 10  

    -   Recuento de clientes de Windows 10 que usan Windows Update para la empresa  

    -   Estadísticas de aplicación de revisiones de clúster  

    -   Recuento de actualizaciones implementadas de Office 365  

-   **Datos de SQL o de rendimiento:**  

    -   Recuento de tablas de base de datos más grandes  

    -   Información de réplicas siempre activadas de SQL  

    -   Recuento de recopilaciones por tipo  

##  <a name="a-namebkmklevel3a-level-3---full"></a><a name="bkmk_level3"></a> Nivel 3: Completo  
El nivel Completo incluye todos los datos de Básico y Mejorado. También incluye información adicional sobre Endpoint Protection, porcentajes de cumplimiento de actualización e información de actualización de software.  Este nivel también puede incluir información avanzada de diagnóstico como archivos del sistema e instantáneas de memoria que pueden incluir información personal que existía en los archivos de registro o de memoria en el momento de la captura.  

A partir de System Center Configuration Manager versión 1511, este nivel incluye lo siguiente:  

-   Evaluación de recopilación y estadísticas de actualización  

-   Resumen de estado de Endpoint Protection (incluido el recuento de clientes protegidos, en peligro, desconocidos y no admitidos)  

-   Configuración de directivas de Endpoint Protection  

-   Información de implementación de actualización de software (porcentaje de implementaciones de destino con cliente frente a hora UTC, necesaria frente a opcional frente a silenciosa, supresión de reinicio)  

-   Cumplimiento general de las implementaciones de actualizaciones de software.  

-   Información de la programación de evaluación de reglas de implementación automática  

-   Número de clientes con directiva de protección de acceso a la red  

-   Recuentos y códigos de error de implementación de actualizaciones de software  

-   Número mínimo, máximo y promedio de clientes inactivos en recopilaciones de implementación de actualizaciones de software  

-   Recuento de grupos con actualizaciones de software caducadas  

-   Número mínimo, máximo y promedio de actualizaciones de software por paquete  

-   Porcentajes de éxito de búsqueda de actualizaciones de software  

-   Número mínimo, máximo y promedio de horas desde la última búsqueda de actualizaciones de software  



<!--HONumber=Nov16_HO1-->


