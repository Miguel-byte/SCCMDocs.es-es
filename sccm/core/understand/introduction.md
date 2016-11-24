---
title: "Introducción | System Center Configuration Manager"
description: "Obtenga información básica como introducción a System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3343eccf-bf09-41cd-9e68-03e893c7f904
caps.latest.revision: 16
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 46aa1fdf49dcdacb9d5e53963a0f799e5f0a1754


---
# <a name="introduction-to-system-center-configuration-manager"></a>Introducción a System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

System Center Configuration Manager es un miembro del conjunto de soluciones de administración de Microsoft System Center, y puede ayudarle a administrar dispositivos y usuarios locales y en la nube.  

**Configuration Manager puede ayudarle:**   
-   Aumentar la eficacia y la productividad de TI al reducir las tareas manuales y permitirle centrarse en proyectos de alto valor.  
-   Maximizar las inversiones en hardware y software.  
-   Fortalecer la productividad del usuario final al proporcionar el software adecuado en el momento oportuno.  

**Configuration Manager le ayuda a ofrecer servicios de TI más eficaces al habilitar:**  

-   Implementación de software segura y escalable  
-   Administración de la configuración de cumplimiento  
-   Administración exhaustiva de activos de servidores, escritorios, portátiles y dispositivos móviles.  

**Configuration Manager extiende sus soluciones y tecnologías existentes de Microsoft y trabaja junto a ellas.**  

Por ejemplo, Configuration Manager se integra en:  

-   Microsoft Intune para administrar una amplia variedad de plataformas de dispositivos móviles  
-   Windows Server Update Services (WSUS) para administrar las actualizaciones de software  
-   Servicios de servidor de certificados  
-   Exchange Server y Exchange Online  
-   Directiva de grupo de Windows
-   DNS   
-   El kit de implementación automatizada de Windows (ADK de Windows) y la herramienta de migración de estado de usuario (USMT)  
-   Servicios de implementación de Windows (WDS)  
-   Escritorio remoto y Asistencia remota  

Configuration Manager también usa:  

-   Los Servicios de dominio de Active Directory para la seguridad, la ubicación del servicio, la configuración y la detección de los usuarios y dispositivos que quiere administrar.  
-   Microsoft SQL Server como base de datos distribuida de administración de cambios y se integra con SQL Server Reporting Services (SSRS) para producir informes con el fin de supervisar y efectuar un seguimiento de las actividades de administración.  
-   Los roles del sistema de sitio que extienden la funcionalidad de administración y usan los servicios web de Internet Information Services (IIS).  
-   El servicio de transferencia inteligente en segundo plano (BITS) y BranchCache para administrar el ancho de banda de red disponible.  

 Para usar Configuration Manager correctamente, debe planear y probar las características de administración de manera exhaustiva antes de usar Configuration Manager en un entorno de producción. Como aplicación eficaz de administración, Configuration Manager tiene la posibilidad de afectar a todos los equipos de su organización. Si implementa y administra Configuration Manager con una planeación rigurosa y tomando en consideración sus requisitos empresariales, Configuration Manager puede reducir su sobrecarga administrativa y el coste total de propiedad.  

 Use los siguientes temas y secciones adicionales de este tema para obtener más información sobre Configuration Manager:  


**Temas relacionados en esta biblioteca de documentación:**  

-   [Características y funcionalidades de System Center Configuration Manager](../../core/plan-design/changes/features-and-capabilities.md)  
-   [Elegir una solución de administración de dispositivos para System Center Configuration Manager](../../core/plan-design/choose-a-device-management-solution.md)  
-   [Cambios en System Center Configuration Manager en relación a System Center 2012 Configuration Manager](../../core/plan-design/changes/what-has-changed-from-configuration-manager-2012.md)
-   [Aspectos básicos de System Center Configuration Manager](../../core/understand/fundamentals.md)  
-   [Evalúe System Center Configuration Manager mediante la creación de su propio entorno de laboratorio](/sccm/core/get-started/set-up-your-lab)
-   [Buscar ayuda sobre el uso de System Center Configuration Manager](../../core/understand/find-help.md)  
-   [Características eliminadas y en desuso de System Center Configuration Manager](../../core/plan-design/changes/removed-and-deprecated-features.md)  

##  <a name="a-namebkmkconsolea-the-configuration-manager-console"></a><a name="BKMK_Console"></a> La consola de Configuration Manager  
 Después de instalar Configuration Manager, use la consola de Configuration Manager para configurar sitios y clientes, y para ejecutar y supervisar tareas de administración. Esta consola es el principal punto de administración y permite administrar varios sitios.  

 Puede usar la consola para ejecutar consolas secundarias para proporcionar soporte para tareas de administración de clientes específicas, como las siguientes:  

-   **Explorador de recursos**, para ver la información de inventario de hardware y software.  
-   **Control remoto**, para realizar una conexión remota a un equipo cliente con el fin de realizar tareas de solución de problemas.  

 Puede instalar la consola de Configuration Manager en equipos adicionales, restringir el acceso y limitar lo que los usuarios administrativos pueden ver en la consola con la administración basada en roles de Configuration Manager.  

 Para obtener más información, consulte [Instalar las consolas de System Center Configuration Manager](../../core/servers/deploy/install/install-consoles.md).

##  <a name="a-namebkmkapplicationcataloga-the-application-catalog-software-center-and-the-company-portal"></a><a name="BKMK_ApplicationCatalog"></a> Catálogo de aplicaciones, Centro de software y portal de la compañía  
 El **Catálogo de aplicaciones** es un sitio web donde los usuarios pueden buscar y solicitar software para sus equipos con Windows. Para utilizar el catálogo de aplicaciones, debe instalar el punto de servicio web del catálogo de aplicaciones y el punto de sitio web del catálogo de aplicaciones para el sitio.  

 El **Centro de software** es una aplicación que se instala si el cliente de Configuration Manager está instalado en equipos con Windows. Los usuarios ejecutan esta aplicación para solicitar software y administrar el software que tienen implementado mediante el uso de Configuration Manager. El Centro de software permite a los usuarios realizar lo siguiente:  

-   Buscar e instalar software desde el Catálogo de aplicaciones.  
-   Ver su historial de solicitudes de software.  
-   Configurar cuándo puede instalar Configuration Manager software en sus dispositivos  
-   Configurar opciones de acceso para el control remoto, si un usuario administrativo tiene habilitado el control remoto.  

 **El portal de empresa** es una aplicación o un sitio web que proporciona funciones similares al catálogo de aplicaciones, pero para dispositivos móviles que Microsoft Intune ha inscrito.  

 Para obtener más información, consulte el tema [Get started with application management in System Center Configuration Manager (Introducción a la administración de aplicaciones en System Center Configuration Manager)](../../apps/understand/introduction-to-application-management.md).  

###  <a name="a-namebkmkclienta-configuration-manager-properties-on-windows-pcs"></a><a name="BKMK_Client"></a> Propiedades de Configuration Manager (en equipos de Windows)  
 Cuando se instala el cliente de Configuration Manager en equipos con Windows, Configuration Manager está instalado en el Panel de control. Por lo general, no es necesario configurar esta aplicación, ya que la configuración del cliente se realiza en la consola de Configuration Manager. Esta aplicación ayuda a los usuarios administrativos y al departamento de soporte técnico a solucionar problemas relacionados con los clientes individuales.  

 Para obtener más información sobre la implementación de clientes, consulte [Client installation methods in System Center Configuration Manager (Métodos de instalación de cliente en System Center Configuration Manager)](../../core/clients/deploy/plan/client-installation-methods.md).  

##  <a name="a-namebkmkexamplescenariosa-example-scenarios-for-configuration-manager"></a><a name="BKMK_ExampleScenarios"></a> Escenarios de ejemplo de Configuration Manager  
 Los siguientes escenarios de ejemplo muestran cómo una empresa llamada Trey Research usa System Center Configuration Manager para permitir que los usuarios:  

-   Sean más productivos.  
-   Unifiquen la administración de cumplimiento de los dispositivos para una experiencia de administración más sencilla.  
-   Simplifiquen la administración de dispositivos para reducir los costos operativos de TI.  

 En todos los escenarios, Adán es el administrador principal de Configuration Manager.  

###  <a name="a-namebkmkscenarioempowera-example-scenario-empower-users-by-ensuring-access-to-applications-from-any-device"></a><a name="BKMK_ScenarioEmpower"></a> Escenario de ejemplo: Capacitar a los usuarios garantizando el acceso a aplicaciones desde cualquier dispositivo  
 Trey Research desea garantizar que los empleados tienen acceso a las aplicaciones que necesitan y de la forma más eficaz posible. Adán asigna estos requisitos de la empresa a los escenarios siguientes:  

|Requisito|Estado de administración de cliente actual|Estado de administración de cliente futuro|  
|-----------------|-------------------------------------|------------------------------------|  
|Los empleados nuevos pueden trabajar de forma eficaz desde el primer día.|Cuando los empleados se unen a la empresa, tienen que esperar hasta que las aplicaciones estén instaladas después de iniciar sesión.|Cuando los empleados se unen a la empresa, inician sesión y sus aplicaciones están instaladas y listas para usarlas.|  
|Los empleados pueden solicitar el software adicional que necesiten de forma rápida y sencilla.|Si los empleados necesitan aplicaciones adicionales, presentan un vale al departamento de soporte técnico y después, normalmente, esperan dos días hasta que el vale está procesado y las aplicaciones instaladas.|Si los empleados requieren aplicaciones adicionales, pueden solicitarlas desde un sitio web y se instalan inmediatamente, si no hay ninguna restricción de licencia. Si hay restricciones de licencia, los usuarios deben solicitar la aprobación para poder instalar la aplicación.<br /><br /> El sitio web muestra sólo las aplicaciones que se pueden instalar.|  
|Los empleados pueden utilizar sus dispositivos móviles en el trabajo si dichos dispositivos cumplen las directivas de seguridad, que se supervisan y aplican.<br /><br /> Estas directivas incluyen la aplicación de una contraseña segura, el bloqueo de un dispositivo tras un período de inactividad y el borrado remoto de dispositivos perdidos o robados.|Los empleados conectan sus dispositivos móviles a Exchange Server para utilizar el servicio de correo electrónico pero la información es escasa como para poder confirmar que cumplen las directivas de seguridad de las directivas de buzón predeterminadas de Exchange ActiveSync. El uso personal de los dispositivos móviles corre el riesgo de quedar prohibido, salvo que la organización de TI pueda confirmar el cumplimiento de las directivas.|La organización de TI puede notificar el cumplimiento de seguridad de los dispositivos móviles con la configuración requerida. Esta confirmación permite a los usuarios continuar utilizando sus dispositivos móviles en el trabajo. Los usuarios pueden borrar sus dispositivos móviles de forma remota si los pierden o extravían y el departamento de soporte técnico puede borrar cualquier dispositivo móvil de usuario si se notifica su pérdida o extravío.<br /><br /> Proporcionar inscripción de dispositivos móviles en un entorno PKI para mejorar la seguridad y el control.|  
|Los empleados pueden ser productivos, incluso si no están en sus puestos de trabajo.|Si los empleados no están en su puesto de trabajo y no disponen de equipos portátiles, no pueden tener acceso a sus aplicaciones mediante el uso de equipos quiosco que están disponibles en toda la empresa.|Los empleados pueden utilizar equipos quiosco para tener acceso a sus aplicaciones y datos.|  
|Por lo general, la continuidad del negocio tiene prioridad frente a la instalación de las aplicaciones necesarias y las actualizaciones de software.|Las aplicaciones y actualizaciones de software necesarias se instalan durante el día y, a menudo, interrumpen el trabajo de los usuarios, ya que la velocidad de sus equipos se ralentiza o es necesario reiniciarlos durante la instalación.|Los usuarios pueden configurar su horario laboral para evitar la instalación del software necesario mientras están utilizando su equipo.|  

 Para cumplir los requisitos, Adán usa estas funcionalidades de administración y opciones de configuración de Configuration Manager:  

-   Administración de aplicaciones  
-   Administración de dispositivos móviles  

 Implementa estas opciones mediante los pasos de configuración de la tabla siguiente.  

|Pasos de configuración|Resultado|  
|-------------------------|-------------|  
|Adán se asegura de que los nuevos usuarios tienen cuentas de usuario en Active Directory y crea una nueva recopilación basada en consultas en Configuration Manager para estos usuarios. A continuación, define la afinidad de dispositivo de usuario para estos usuarios mediante la creación de un archivo que asigna las cuentas de usuario a los equipos primarios que van a usar e importa este archivo en Configuration Manager.<br /><br /> Las aplicaciones que deben tener los nuevos usuarios ya están creadas en Configuration Manager. A continuación, implementa estas aplicaciones que tienen el propósito de Requerido en la recopilación que contiene los nuevos usuarios.|Debido a la información de la afinidad de dispositivo de usuario, las aplicaciones se instalan en el equipo o equipos principales de cada usuario antes de que el usuario inicie sesión.<br /><br /> Las aplicaciones están listas para su uso en cuanto el usuario inicie sesión correctamente.|  
|Adán instala y configura los roles de sistema de sitio del catálogo de aplicaciones para que los usuarios puedan buscar aplicaciones que deseen instalar. Crea implementaciones de aplicaciones que tienen el propósito de Disponible y, a continuación, implementa estas aplicaciones en la recopilación que contiene los nuevos usuarios.<br /><br /> En el caso de las aplicaciones que tengan un número limitado de licencias, Adán las configura para que exijan aprobación.|Mediante la configuración de las aplicaciones como disponibles para estos usuarios y con el uso del catálogo de aplicaciones, los usuarios ahora pueden explorar las aplicaciones que pueden instalar. Los usuarios pueden instalar las aplicaciones inmediatamente o solicitar la aprobación y volver al catálogo de aplicaciones para instalarlas después de que el departamento de soporte técnico apruebe su solicitud.|  
|Adán crea un conector de Exchange Server en Configuration Manager para administrar los dispositivos móviles que se conectan al servidor Exchange local de la compañía. Configura este conector con una configuración de seguridad que incluye la necesidad de una contraseña segura y bloquea el dispositivo móvil tras un período de inactividad.<br /><br /> Para la administración adicional de dispositivos que ejecutan Windows Phone 8, Windows RT e iOS, Adán obtiene una suscripción de Microsoft Intune y, después, instala el rol de sistema de sitio de punto de conexión de servicio. Esta solución de administración de dispositivos móviles ofrece a la empresa una mayor capacidad de administración de estos dispositivos. Esto incluye hacer que las aplicaciones estén disponibles para que los usuarios las instalen en estos dispositivos y la administración de la configuración extendida. Además, las conexiones con dispositivos móviles están protegidas mediante el uso de certificados PKI que Intune crea e implementa automáticamente. Después de configurar el punto de conexión de servicio y la suscripción para usarlos con Configuration Manager, Adán envía un correo electrónico a los usuarios propietarios de estos dispositivos móviles para que hagan clic en un vínculo para iniciar el proceso de inscripción.<br /><br /> Para que Microsoft Intune inscriba los dispositivos móviles, Adán usa la configuración de cumplimiento para configurar opciones de seguridad para estos dispositivos móviles. Estas opciones incluyen la necesidad de configurar una contraseña segura y bloquear el dispositivo móvil tras un período de inactividad.|Con estas dos soluciones de administración de dispositivos móviles, la organización de TI ahora puede ofrecer información de informes acerca de los dispositivos móviles usados en la red de la empresa y su compatibilidad con las opciones de seguridad configuradas.<br /><br /> Los usuarios ven cómo borrar de forma remota su dispositivo móvil mediante el catálogo de aplicaciones o el portal de la empresa si pierden su dispositivo móvil o se lo roban. El departamento de soporte técnico también recibe indicaciones de cómo borrar de forma remota un dispositivo móvil para los usuarios mediante el uso de la consola de Configuration Manager.<br /><br /> Además, en el caso de los dispositivos móviles inscritos por Microsoft Intune, Adán ahora puede implementar aplicaciones móviles para que las instalen los usuarios, recopilar más datos de inventario de estos dispositivos y obtener un mejor control de administración sobre estos dispositivos al tener acceso a más opciones de configuración.|  
|Trey Research tiene varios equipos quiosco que utilizan los empleados que visitan la oficina. Los empleados desean tener disponibles sus aplicaciones dondequiera que inicien sesión. Sin embargo, Adán no desea instalar localmente todas las aplicaciones en cada equipo.<br /><br /> Para lograr esto, Adán crea las aplicaciones necesarias que tienen dos tipos de implementación:<br /><br /> **El primero:** una instalación local completa de la aplicación que tenga el requisito de que solo puede instalarse en el dispositivo principal de un usuario.<br /><br /> **El segundo:** una versión virtual de la aplicación que tenga el requisito de que no debe instalarse en el dispositivo principal del usuario.|Cuando los empleados visitantes inicien sesión en un quiosco multimedia, podrán ver las aplicaciones que requieren mostradas como iconos en el escritorio del quiosco multimedia. Cuando ejecutan la aplicación, se transmite como una aplicación virtual. De este modo, pueden ser tan productivos como si se encontraran en su escritorio.|  
|Adán permite a los usuarios saber que pueden configurar sus horas de oficina en el Centro de software y pueden seleccionar opciones para evitar actividades de implementación de software durante este periodo y cuando el equipo esté en modo de presentación.|Dado que los usuarios pueden controlar cuándo Configuration Manager implementa software en sus equipos, los usuarios son más productivos durante su jornada de trabajo.|  

 Estos pasos de configuración y resultados permiten a Trey Research capacitar completamente a sus empleados al garantizarles el acceso a las aplicaciones desde cualquier dispositivo.  

###  <a name="a-namebkmkscenariounifya-example-scenario-unify-compliance-management-for-devices"></a><a name="BKMK_ScenarioUnify"></a> Escenario de ejemplo: Unificar la administración de cumplimiento para dispositivos  
 Trey Research desea una solución de administración de clientes unificada que garantice que sus equipos ejecutan software antivirus que se mantiene actualizado automáticamente. Es decir:  

-   El Firewall de Windows está habilitado.  
-   Las actualizaciones de software críticas están instaladas.  
-   Las claves del Registro específicas están establecidas.  
-   Los dispositivos móviles administrados no pueden instalar o ejecutar aplicaciones sin firmar.  

 La empresa también desea ampliar esta protección a Internet para los equipos portátiles que pasen de la intranet a Internet.  

 Adán asigna estos requisitos de la empresa a los escenarios siguientes:  

|Requisito|Estado de administración de cliente actual|Estado de administración de cliente futuro|  
|-----------------|-------------------------------------|------------------------------------|  
|Todos los equipos ejecutan software antimalware que tiene archivos de definición actualizados y habilita Firewall de Windows.|Diferentes equipos ejecutan soluciones antimalware diferentes que no siempre se mantienen actualizadas y, aunque el Firewall de Windows está habilitado de forma predeterminada, los usuarios a veces lo deshabilitan.<br /><br /> Los usuarios deben ponerse en contacto con el departamento de soporte técnico si se detecta software malintencionado en su equipo.|Todos los equipos ejecutan la misma solución antimalware que descarga automáticamente los archivos de actualización de definición más recientes y vuelve a habilitar automáticamente el Firewall de Windows si los usuarios lo deshabilitan.<br /><br /> El departamento de soporte técnico recibe automáticamente una notificación por correo electrónico si se detecta software malintencionado.|  
|Todos los equipos instalan actualizaciones de software críticas dentro del primer mes del lanzamiento.|Aunque las actualizaciones de software se instalan en los equipos, muchos equipos no instalan automáticamente las actualizaciones de software críticas hasta dos o tres meses después de su lanzamiento. Esto les convierte en vulnerables a ataques durante este período de tiempo.<br /><br /> Cuando haya equipos que no instalen las actualizaciones de software críticas, el departamento de soporte técnico enviará primero mensajes de correo electrónico pidiendo a los usuarios que instalen las actualizaciones. Cuando haya equipos que sigan siendo no compatibles, los ingenieros se conectarán de forma remota a estos equipos e instalarán manualmente las actualizaciones de software que faltan.|Mejore la tasa de compatibilidad actual durante el mes especificado en más del 95% sin enviar mensajes de correo electrónico ni pedir al departamento de soporte técnico que las instale manualmente.|  
|La configuración de seguridad para aplicaciones específicas se comprueba con regularidad y se corrige si es necesario.|Los equipos ejecutan scripts de inicio complejos que se basan en la pertenencia a grupos de los equipos para restablecer los valores del Registro para aplicaciones específicas.<br /><br /> Dado que estos scripts solo se ejecutan al inicio y algunos equipos están encendidos durante días, el departamento de soporte técnico no puede comprobar cambios en la configuración cuando desee.|Los valores del Registro se comprueban y se corrigen automáticamente sin depender de la pertenencia a un grupo del equipo o sin reiniciar el equipo.|  
|Los dispositivos móviles no pueden instalar o ejecutar aplicaciones no seguras.|Se solicita a los usuarios que no descarguen ni ejecuten aplicaciones potencialmente no seguras de Internet, pero no hay ningún control para supervisar o exigir esto.|Los dispositivos móviles que se administran con Microsoft Intune o Configuration Manager impiden automáticamente la instalación o la ejecución de aplicaciones sin firmar.|  
|Los equipos portátiles que pasan de la intranet a Internet deben mantenerse seguros.|En el caso de los usuarios que viajan, con frecuencia no pueden conectarse a través de la red privada virtual diariamente y estos equipos portátiles dejan de cumplir los requisitos de seguridad.|Una conexión a Internet es todo lo necesario para que los equipos portátiles mantengan su compatibilidad con los requisitos de seguridad. Los usuarios no tienen que iniciar sesión o utilizar la red privada virtual.|  

 Para cumplir los requisitos, Adán usa estas funcionalidades de administración y opciones de configuración de Configuration Manager:  

-   Endpoint Protection  
-   Actualizaciones de software  
-   Configuración de compatibilidad  
-   Administración de dispositivos móviles  
-   Administración de cliente basada en Internet  

 Implementa estas opciones mediante los pasos de configuración de la tabla siguiente.  

|Pasos de configuración|Resultado|  
|-------------------------|-------------|  
|Adán configura Endpoint Protection, permite que la configuración de cliente desinstale otras soluciones antimalware y habilita el Firewall de Windows. Configura reglas de implementación automática para que los equipos comprueben e instalen las últimas actualizaciones de definición de forma regular.|La solución antimalware única ayuda a proteger todos los equipos con una sobrecarga administrativa mínima. Dado que el departamento de soporte técnico recibe automáticamente una notificación por correo electrónico si se detecta antimalware, los problemas pueden resolverse rápidamente. Esto ayuda a evitar ataques contra otros equipos.|  
|Para ayudar a incrementar las tasas de cumplimiento, Adán usa reglas de implementación automática, define ventanas de mantenimiento para los servidores e investiga las ventajas y desventajas de usar Wake on LAN en equipos que hibernan.|Aumenta el cumplimiento de las actualizaciones de software críticas y se reduce la necesidad de que los usuarios o el departamento de soporte técnico instalen las actualizaciones de software de forma manual.|  
|Adán utiliza la configuración de cumplimiento para comprobar la presencia de las aplicaciones especificadas. Cuando se detectan las aplicaciones, los elementos de configuración comprueban los valores del Registro y los corrigen automáticamente si están fuera del cumplimiento.|Mediante el uso de elementos de configuración y líneas de base de configuración que estén implementados en todos los equipos y que comprueben el cumplimiento todos los días, ya no serán necesarios scripts separados que se basen en la pertenencia del equipo y los reinicios del equipo.|  
|Adán utiliza la configuración de cumplimiento para dispositivos móviles inscritos y configura el conector de Exchange Server para que las aplicaciones sin firmar tengan prohibido instalarse y ejecutarse en dispositivos móviles.|Mediante la prohibición de las aplicaciones sin firmar, los dispositivos móviles están protegidos automáticamente frente a aplicaciones potencialmente dañinas.|  
|Adán se asegura de que los servidores de sistema de sitio y los equipos tienen los certificados PKI que requiere Configuration Manager para conexiones HTTPS y, a continuación, instala roles de sistema de sitio adicionales en la red perimetral que aceptan conexiones de cliente desde Internet.|Los equipos que se mueven de la intranet a Internet automáticamente siguen siendo administrados por Configuration Manager cuando tienen una conexión a Internet. Esos equipos no dependen de que los usuarios inicien sesión en su equipo o se conecten a la red privada virtual.<br /><br /> Se sigue administrando estos equipos: antimalware y Firewall de Windows, actualizaciones de software y elementos de configuración. Como resultado, los niveles de cumplimiento aumentan automáticamente.|  

 Estos pasos de configuración y resultados hacen que Trey Research unifique correctamente la administración de cumplimiento para dispositivos.  

###  <a name="a-namebkmkscenariosimplifya-example-scenario-simplify-client-management-for-devices"></a><a name="BKMK_ScenarioSimplify"></a> Escenario de ejemplo: Simplificar la administración de clientes para dispositivos  
 Trey Research quiere que todos los equipos nuevos instalen automáticamente la imagen del equipo base de la empresa que ejecuta Windows 7. Una vez instalada la imagen del sistema operativo en estos equipos, se deben administrar y supervisar para cualquier software adicional que instalen los usuarios. Los equipos que almacenan información altamente confidencial requieren directivas de administración más restrictivas que los demás equipos. Por ejemplo, los ingenieros del departamento de soporte técnico no deben conectarse a ellos de forma remota, debe utilizarse la entrada de PIN de BitLocker para los reinicios y solo los administradores locales pueden instalar software.  

 Adán asigna estos requisitos de la empresa a los escenarios siguientes:  

|Requisito|Estado de administración de cliente actual|Estado de administración de cliente futuro|  
|-----------------|-------------------------------------|------------------------------------|  
|Se instalan nuevos equipos con Windows 7.|El departamento de soporte técnico instala y configura Windows 7 para los usuarios y, a continuación, envía al equipo a la ubicación respectiva.|Los equipos nuevos van directos al destino final, están conectados a la red, e instalan y configuran Windows 7 automáticamente.|  
|Los equipos deben ser administrados y supervisados. Esto incluye el inventario de hardware y software para ayudar a determinar los requisitos de licencias.|El cliente de Configuration Manager se implementa mediante la inserción de cliente automática y el departamento de soporte técnico investiga los errores de instalación y los clientes que no envían datos de inventario cuando se espera que lo hagan.<br /><br /> Los errores son frecuentes debido a las dependencias de instalación que no se cumplen y los daños en WMI en el cliente.|Los datos del inventario y de la instalación del cliente que se recopilan de los equipos son más confiables y requieren menos intervención por parte del departamento de soporte técnico. Los informes muestran el uso de software para obtener información de licencia.|  
|Algunos equipos deben tener directivas de administración más rigurosas.|Debido a las directivas de administración más rigurosas, estos equipos no son administrados actualmente por Configuration Manager.|Administre estos equipos mediante Configuration Manager sin sobrecarga administrativa adicional para dar cabida a las excepciones.|  

 Para cumplir los requisitos, Adán usa estas funcionalidades de administración y opciones de configuración de Configuration Manager:  

-   Implementación de sistema operativo  
-   Implementación del cliente y estado del cliente  
-   Configuración de compatibilidad  
-   Configuración de cliente  
-   Inventario y Asset Intelligence  
-   Administración basada en roles  

 Implementa estas opciones mediante los pasos de configuración de la tabla siguiente.  

|Pasos de configuración|Resultado|  
|-------------------------|-------------|  
|Adán captura una imagen de sistema operativo en un equipo que tiene instalado Windows 7 y que está configurado según las especificaciones de la compañía. A continuación, implementa el sistema operativo en nuevos equipos mediante la compatibilidad con equipos desconocidos y PXE. También instala el cliente de Configuration Manager como parte de la implementación de sistema operativo.|Los nuevos equipos están en funcionamiento con prontitud y sin la intervención del servicio técnico.|  
|Adán configura la instalación de inserción de cliente automática de todo el sitio para instalar el cliente de Configuration Manager en los equipos detectados. Esto garantiza que los equipos a los que no se ha aplicado la imagen con el cliente, lo instalen para que Configuration Manager lo administre.<br /><br /> Adán configura el estado de cliente para corregir automáticamente los problemas de cliente detectados. Adán también establece la configuración de cliente que permite la recopilación de datos de inventario requeridos y configura Asset Intelligence.|La instalación del cliente con el sistema operativo es más rápida y confiable que esperar a que Configuration Manager detecte el equipo e instale los archivos de origen de cliente en el mismo. Sin embargo, si se deja la opción de instalación de inserción de cliente automática activada, se proporciona una copia de seguridad del equipo que ya dispone del sistema operativo instalado para instalar el cliente cuando el equipo se conecta a la red.<br /><br /> La configuración de cliente garantiza que los clientes envían su información de inventario al sitio con regularidad. Esto, además de las pruebas de estado de cliente, le permite mantener al cliente en ejecución con una intervención mínima del departamento de soporte técnico. Por ejemplo, los daños en WMI se detectan y corrigen automáticamente.<br /><br /> Los informes de Asset Intelligence le permiten supervisar el uso de software y las licencias.|  
|Adán crea una recopilación de los equipos que deben tener una configuración de directiva más estricta y crea una opción de dispositivo de cliente personalizada para la recopilación que incluye la deshabilitación del control remoto, habilita la entrada del PIN de BitLocker y permite a los administradores locales instalar software.<br /><br /> Adán configura la administración basada en roles, por lo que los ingenieros de soporte técnico no ven esta recopilación de equipos y, por lo tanto, se impide que accidentalmente los administren como equipos estándar.|Estos equipos son administrados por Configuration Manager, pero con una configuración específica que no requiere un nuevo sitio.<br /><br /> Los ingenieros de soporte técnico no pueden visualizar la recopilación de estos equipos, lo que reduce la posibilidad de que accidentalmente envíen implementaciones y scripts de equipos estándar.|  

 Estos pasos y resultados de configuración simplifican la administración de clientes para dispositivos en Trey Research.  

##  <a name="a-namebkmknextstepsa-next-steps"></a><a name="BKMK_NextSteps"></a> Pasos siguientes  
 Antes de instalar Configuration Manager, familiarícese con los conceptos y términos básicos de Configuration Manager.  

-   Si está familiarizado con System Center 2012 Configuration Manager, consulte [Cambios en System Center Configuration Manager respecto a System Center 2012 Configuration Manager](../../core/plan-design/changes/what-has-changed-from-configuration-manager-2012.md) para conocer las nuevas funcionalidades.  
-   Para obtener información general técnica de System Center Configuration Manager, consulte [Fundamentals of System Center Configuration Manager (Aspectos básicos de System Center Configuration Manager)](../../core/understand/fundamentals.md).  

 Cuando se haya familiarizado con los conceptos básicos, use la documentación de System Center Configuration Manager para implementar y usar correctamente Configuration Manager.  



<!--HONumber=Nov16_HO1-->


