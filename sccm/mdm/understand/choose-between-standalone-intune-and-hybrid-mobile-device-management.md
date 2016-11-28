---
title: "Elegir entre Intune independiente o MDM híbrida | System Center Configuration Manager"
description: "Elija si quiere implementar la administración de dispositivos móviles híbrida con Intune y Configuration Manager o ejecutar Intune de forma independiente."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 73ff9bb9-e605-4b68-92a1-487684fed42d
caps.latest.revision: 10
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 2e6ec1b2b822298d4fa6a17e2d7439167b83080a

---
# <a name="choose-between-microsoft-intune-standalone-and-hybrid-mobile-device-management-with-system-center-configuration-manager"></a>Elegir entre Microsoft Intune independiente y administración de dispositivos móviles híbrida con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Una de las preguntas más frecuentes relacionadas con la administración de dispositivos móviles (MDM) con Microsoft Intune es “¿Debo implementar la MDM híbrida con Intune y Configuration Manager o ejecutar Intune de forma independiente en la configuración de solo en la nube?”. Es una decisión importante que no se puede cambiar fácilmente después de la implementación.  

 Una implementación independiente de Intune no implica ninguna infraestructura local y se administra a través de una consola web. Es ágil y ligera, además de popular en las organizaciones centradas primero en la nube.  

 Una implementación de MDM híbrida implica Intune y Configuration Manager y se administra mediante herramientas familiares para los administradores experimentados de Configuration Manager. Ofrece administración de “único panel” de la MDM y los clientes tradicionales, así como escala en entornos de gran tamaño.  

##  <a name="what-does-intune-standalone-mean"></a>¿Qué significa Intune independiente?  
 Intune en su núcleo es un servicio en la nube. Hay centros de datos de Intune hospedados en Norteamérica, Europa y Asia que proporcionan a los dispositivos móviles directivas de seguridad, perfiles de correo electrónico y Wi-Fi, aplicaciones, inventario, etc.  

 Una implementación independiente de Intune no necesita ninguna infraestructura local. Toda la configuración, la administración, la implementación y la generación de informes se realizan a través de una consola basada en web que es accesible desde cualquier lugar del mundo.  

 Para trabajar con aplicaciones locales, como Microsoft Exchange y el servicio de inscripción de dispositivos de red (NDES), hay conectores locales disponibles para proporcionar conectividad con el servicio Intune.  

 Al ser un servicio en la nube, Intune se puede compilar e implementar en un breve período de tiempo.  

##  <a name="what-does-hybrid-mdm-mean"></a>¿Qué significa MDM híbrida?  
 Para las organizaciones que quieren maximizar su inversión en Configuration Manager, los clientes que necesitan un control más preciso o los clientes que superan las limitaciones de escala de Intune, hay disponible una implementación híbrida que usa Intune para administrar dispositivos móviles.  

 Las implementaciones híbridas necesitan Microsoft System Center 2012 Configuration Manager SP1 o superior.  

 El servicio Intune se conecta a Configuration Manager con el rol de sistema de sitio Punto de conexión de servicio (anteriormente conocido como Microsoft Intune Connector), que se ha instalado en la administración central o en el sitio primario de una jerarquía de Configuration Manager. Un inquilino de Intune solo se puede conectar a una jerarquía de Configuration Manager y una jerarquía de Configuration Manager solo se puede conectar a un inquilino de Intune.  

 En una configuración de MDM híbrida, parte de la sobrecarga de procesamiento y almacenamiento se realiza en la infraestructura local de Configuration Manager. Este aumento de eficacia permite a la MDM híbrida escalar más que Intune independiente.  

 Una implementación híbrida permite el uso de herramientas que resultan familiares a los administradores de Configuration Manager. Cuando se implementa la MDM híbrida, se ponen a disposición de los dispositivos móviles funciones avanzadas como el control de administración basado en roles (RBAC), SQL Server Reporting Services (SSRS) y la agrupación compleja de dispositivos y usuarios mediante consultas de pertenencia a colecciones.  

##  <a name="planning-choices-and-intune-deployment-timelines"></a>Planeamiento de opciones y escalas de tiempo de implementación de Intune  
 La innovación y la evolución de Intune se producen a un ritmo vertiginoso, con actualizaciones mensuales que proporcionan características nuevas o mejoradas, una escala mejorada, nuevas experiencias de la consola de administración mediante el portal de Azure, grupos dinámicos por medio de Azure Active Directory, etc. Por lo tanto, las decisiones de diseño deben tener en cuenta la dirección futura del producto.  

 Muchas de las capacidades exclusivas que proporciona en este momento una configuración híbrida se replicarán funcionalmente en Intune independiente a medida que el servicio se vaya desarrollando a corto, medio y largo plazo.  

 Si está decidiendo entre independiente e híbrida, debería tener en cuenta las escalas de tiempo de implementación. Es habitual que los clientes pasen por varias iteraciones de implementación que incluyen el diseño, la compilación, la prueba de aceptación de los usuarios y las fases piloto, que a menudo llevan varios meses, antes de estar preparados para implementar en producción. Por este motivo, al elegir un diseño de jerarquía de Intune, tenga en cuenta el momento en que se va a producir la implementación real y la dirección del servicio a corto, medio y largo plazo.  

 A medida que el servicio Intune siga evolucionando, nuestro objetivo es simplificar las opciones de configuración. En el futuro, el único motivo para elegir un entorno de MDM híbrida debería ser la necesidad de una única consola de administración para los clientes tradicionales y los dispositivos móviles.  Estamos trabajando mucho para mejorar la escalabilidad, agregando acceso basado en roles a través del portal de Azure y grupos dinámicos mediante una mayor integración de Azure Active Directory, todo alineado con actualizaciones del servicio a corto y medio plazo.  

 Por último, también estamos trabajando para garantizar que independientemente de la opción de configuración que elija hoy, pueda migrar fácilmente entre las opciones de configuración híbrida e independiente sin problemas. En este momento, el cambio entre autoridades de MDM exige intervención manual por parte del servicio de soporte técnico de Microsoft y un esfuerzo considerable por parte del inquilino. Para simplificar esto, nuestro objetivo es permitir la coexistencia de Intune híbrido e independiente, lo que le permitiría mover usuarios entre los dos tipos de administración, pero sin tener que elegir una configuración por encima de la otra.  Este cambio también acaba con la molestia actual de tener que llamar al servicio de soporte técnico y elimina el proceso de cancelar la inscripción de los dispositivos y de volver a inscribirlos.  

##  <a name="pros-and-cons-of-intune-standalone"></a>Ventajas y desventajas de Intune independiente  

|Ventajas|Desventajas|  
|----------|----------|  
|Compilación e implementación rápidas<br /><br /> Ninguna infraestructura local<br /><br /> Actualizaciones y versiones de características más frecuentes<br /><br /> Curva de aprendizaje reducida<br /><br /> Consola de administración disponible externamente|Capacidades de generación de informes limitadas<br /><br /> Restricción de roles de seguridad limitada<br /><br /> Sin herramientas externas (por ejemplo, PowerShell, etc.)<br /><br /> Inventario de aplicaciones limitado<br /><br /> Capacidades de agrupación de dispositivos y usuarios básicas<br /><br /> Necesita Silverlight|  

##  <a name="pros-and-cons-of-hybrid-mdm"></a>Ventajas y desventajas de la MDM híbrida  

|Ventajas|Desventajas|  
|----------|----------|  
|Capacidad de escalar<br /><br /> Herramientas avanzadas (como la consola de Configuration Manager, PowerShell, registro, etc.)<br /><br /> Control de acceso basado en roles (RBAC)<br /><br /> Generación de informes avanzada<br /><br /> Administración de “único panel” para los clientes tradicionales y de MDM<br /><br /> Inventario de aplicaciones ampliado<br /><br /> Agrupación de dispositivos y usuarios avanzada<br /><br /> Varios conectores de Exchange local y Exchange Online admitidos<br /><br /> Varios roles NDES/CRP admitidos<br /><br /> Capacidad de marcar dispositivos como “de empresa”<br /><br /> Mayores capacidades de solución de problemas<br /><br /> CAL de usuario de Configuration Manager incluidas en la suscripción|Complejidad local (configuración y administración)<br /><br /> Curva de aprendizaje pronunciada<br /><br /> Mantenimiento necesario para las actualizaciones y las versiones de características<br /><br /> Requisitos de licencia adicionales (como Windows, SQL Server, etc.)|  

##  <a name="planning-decisions"></a>Decisiones de planeación  
 ![híbrida&#45;decisiones](../../mdm/understand/media/hybrid-decisions.png)  

|Paso|Decisión|
|-|-|  
|<img src="media/hybrid-1.png" style="min-width:32px">|**¿Cuántos dispositivos planea administrar?**<br /><br /> Intune independiente admite hasta 50.000 dispositivos. La MDM híbrida admite hasta 300.000 dispositivos.<br /><br /> Para cualquier implementación de tamaño considerable, independiente o MDM híbrida, se recomienda ponerse en contacto con el equipo de cuentas de Microsoft. El equipo de cuentas de Microsoft puede ponerle en contacto con especialistas de Intune que pueden realizar un análisis más profundo de la escala y las limitaciones.|  
|![híbrida&#45;2](../../mdm/understand/media/hybrid-2.png)|**¿Es necesario el control de acceso específico? (RBAC)**<br /><br /> El control de acceso basado en roles (RBAC) se ha agregado a System Center 2012 Configuration Manager. RBAC permite a los administradores de Configuration Manager diseñar e implementar conjuntos de permisos complejos para restringir el acceso de administrador a las funciones y los objetos de Configuration Manager.<br /><br /> Intune independiente proporciona solo dos roles de administrador: acceso total y acceso de solo lectura.<br /><br /> Si la organización necesita adaptar determinados administradores a determinados usuarios, dispositivos, funciones u objetos, se necesita Configuration Manager con RBAC.<br /><br /> Si la organización tiene un pequeño equipo administrativo y la complejidad del control de acceso no es necesaria, Intune con roles de seguridad integrados es la mejor opción.|  
|![híbrida&#45;3](../../mdm/understand/media/hybrid-3.png)|**¿Son necesarias las capacidades de generación de informes avanzadas?**<br /><br /> La MDM híbrida con Configuration Manager incluye funcionalidad avanzada de generación de informes mediante SQL Server Reporting Services (SSRS). Configuration Manager incluye 34 informes integrados de MDM y más de 400 informes estándar de Configuration Manager. SSRS también permite a los analistas de negocios y a los administradores escribir sus propios informes personalizados. Además, se puede consultar la base de datos de Configuration Manager mediante herramientas externas, como las herramientas de orquestación, a fin de proporcionar funciones concretas, como por ejemplo alertas personalizadas. Al ser Configuration Manager el que ejecuta los informes, todos los informes además pueden incluir datos que no son de MDM, como un inventario de equipos tradicionales junto a un inventario de dispositivos móviles.<br /><br /> Intune independiente proporciona nueve informes. Estos informes no son personalizables y ofrecen variables de entrada limitadas. Los informes se pueden imprimir o exportar a CSV o HTML.<br /><br /> Si la organización necesita funciones avanzadas de generación de informes y tiene el ancho de banda y el conocimiento para administrar SSRS, la MDM híbrida es la mejor opción.<br /><br /> Si la organización quiere un motor de generación de informes fácil de usar e informes predefinidos, la funcionalidad de generación de informes de Intune independiente debería bastar.|  
|![híbrida&#45;4](../../mdm/understand/media/hybrid-4.png)|**¿Administra dispositivos de Windows 10 sin acceso a Internet?**<br /><br /> En Configuration Manager (rama actual), los dispositivos de Windows 10 pueden administrarse a través del canal MDM mediante la infraestructura local únicamente.<br /><br /> La característica de administración local de dispositivos móviles está diseñada para permitir la administración MDM para clientes no accesibles a través de Internet y está destinada principalmente a dispositivos de un solo uso (como quioscos interactivos) y dispositivos IoT.<br /><br /> Debido al enfoque de solo en la nube de Intune independiente, todos los dispositivos administrados deben tener acceso a Internet. Si la organización quiere administrar dispositivos de Windows 10 a través de la administración local de dispositivos móviles, se necesita una configuración de MDM híbrida. Tenga en cuenta que la administración local de dispositivos móviles no admite la administración de dispositivos móviles de Internet e intranet al mismo tiempo.|  
|![híbrida&#45;5](../../mdm/understand/media/hybrid-5.png)|**¿Necesita el inventario de aplicaciones completo?**<br /><br /> De forma predeterminada, Intune independiente solo recopilará el inventario de aplicaciones de aquellas que Intune administra e implementa. Esto significa que los informes de inventario no contienen información sobre aplicaciones de prueba que los usuarios han instalado fuera del Portal de empresa de Intune.<br /><br /> La MDM híbrida con Configuration Manager permite a los administradores designar determinados dispositivos como “de empresa”. Cuando un dispositivo se establece como dispositivo de empresa, se recopila el inventario de aplicaciones ampliado, que proporciona acceso a una lista completa de las aplicaciones de los dispositivos.<br /><br /> Si la organización necesita información sobre las aplicaciones instaladas personalmente desde los dispositivos administrados, se necesita la MDM híbrida. Antes de tomar una decisión basada en esta opción, tenga en cuenta el impacto sobre la privacidad del usuario final.|  
|![híbrida&#45;6](../../mdm/understand/media/hybrid-6.png)|**¿Quiere administrar equipos de la manera tradicional?**<br /><br /> Una ventaja de la MDM híbrida con respecto a la configuración independiente es la administración de “único panel”. Esto significa que una organización puede administrar todo su inventario de equipos de escritorio, servidores y dispositivos móviles desde una herramienta de administración, la consola de Configuration Manager. Además, con el cliente de Configuration Manager, las funciones de administración avanzadas, como el inventario de hardware y software, la administración de actualizaciones de software, la implementación de software y la implementación de sistema operativo, están disponibles para dispositivos que no son móviles.<br /><br /> Si la organización quiere administrar los clientes tradicionales Mac, Linux/UNIX y Windows, Configuration Manager es la plataforma de administración perfecta.<br /><br /> Intune independiente también ofrece administración de equipos tradicionales (Windows 7, 8.1 y 10) mediante el cliente de administración de equipos de Intune. Ofrece administración de equipos básica que incluye inventario de hardware, actualizaciones de Windows, Endpoint Protection e implementación simple de software. El cliente no funciona con Configuration Manager, por lo que puede usarse en implementaciones de MDM híbrida e Intune independiente.|  
|![híbrida&#45;7](../../mdm/understand/media/hybrid-7.png)|**¿Quiere administrar la infraestructura local?**<br /><br /> Cualquier infraestructura local implica un cierto nivel de sobrecarga y complejidad de administración. Configuration Manager es un producto que necesita considerable conocimiento, experiencia e inversión para administrar y mantener su infraestructura.<br /><br /> Como mínimo, la MDM híbrida necesita un sitio primario único de Configuration Manager, con el rol de base de datos, el rol de servicios de generación de informes y el rol de punto de conexión de servicio. Si se necesita administración de equipos tradicionales, los roles de punto de administración, punto de distribución, punto de actualización de software y catálogo de aplicaciones también podrían ser necesarios. Las funciones avanzadas, como la implementación de certificados, la administración de Mac y Endpoint Protection, agregan más roles y complejidad.<br /><br /> La jerarquía de Configuration Manager exige bastante administración y mantenimiento para garantizar que sea correcta y funcione según lo previsto.<br /><br /> Si no quiere la sobrecarga de una jerarquía de Configuration Manager, una implementación de Intune independiente es la mejor opción.|  
|![híbrida&#45;8](../../mdm/understand/media/hybrid-8.png)|**¿Necesita herramientas externas?**<br /><br /> Configuration Manager es un producto maduro de categoría empresarial que incluye muchas formas de interactuar con el servicio sin usar la consola. Una implementación de MDM híbrida permite a los administradores usar el SDK de Configuration Manager o PowerShell para administrar los dispositivos móviles mediante programación. También permite a los administradores usar herramientas como System Center Orchestrator, PowerBI y varios complementos de terceros.<br /><br /> En una implementación de Intune independiente, toda la administración debe realizarse a través de la consola de Silverlight y no hay herramientas externas disponibles.|  
|![híbrida&#45;9](../../mdm/understand/media/hybrid-9.png)|**¿Quiere actualizaciones de características de MDM rápidas?**<br /><br /> Aunque Configuration Manager (rama actual) ofrece un mantenimiento rápido de características y actualizaciones, el desarrollo de servicios en la nube, como Intune, se presta bien a una implementación de producción incluso más rápida.<br /><br /> Intune independiente probablemente recibirá nuevas características antes que una implementación de MDM híbrida.<br /><br /> Si la organización quiere ser puntera, Intune independiente le ofrecerá las características de MDM más novedosas de la manera más rápida.|



<!--HONumber=Nov16_HO1-->


