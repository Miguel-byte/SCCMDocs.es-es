---
title: "Configuración de cliente | Microsoft Docs"
description: "Seleccione la configuración del cliente mediante la consola de administración de System Center Configuration Manager."
ms.custom: na
ms.date: 08/01/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f7560876-8084-4570-aeab-7fd44f4ba737
caps.latest.revision: "15"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: a8233c361e1a78b14a02f328da445814624e38d8
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/07/2017
---
# <a name="about-client-settings-in-system-center-configuration-manager"></a>Acerca de la configuración de cliente en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Todas las opciones del cliente de System Center Configuration Manager se administran en el nodo **Configuración de cliente** del área de trabajo **Administración** de la consola de Configuration Manager. Configuration Manager incluye una configuración predeterminada. Si cambia la configuración predeterminada del cliente, esta configuración se aplicará a todos los clientes de la jerarquía. También puede establecer la configuración personalizada del cliente, que invalida la configuración predeterminada del cliente si la asigna a las recopilaciones. Para obtener información sobre cómo configurar las opciones de cliente, consulte [How to configure client settings in System Center Configuration Manager](../../../core/clients/deploy/configure-client-settings.md) (Cómo configurar las opciones de cliente en System Center Configuration Manager).  

Muchas de las configuraciones del cliente se explican por sí solas. Aquí se describen otras.  

## <a name="background-intelligent-transfer-service"></a>Servicio de transferencia inteligente en segundo plano  

-   **Limitar el ancho de banda de red máximo para transferencias BITS en segundo plano**  

   Cuando esta opción esté establecida en **True** o **Sí**, los clientes usarán el límite de ancho de banda de BITS.  

-   **Hora de inicio de período de limitación**  

   Especifique la hora de inicio local del período de limitación de BITS.  

-   **Hora de finalización del período de limitación**  

   Especifique la hora de finalización local del período de limitación de BITS. Si coincide con la **hora de inicio del período de limitación**, la limitación de BITS siempre está habilitada.  

-   **Velocidad de transferencia máxima durante el período de limitación (Kbps)**  

   Especifique la velocidad de transferencia máxima que pueden usar los clientes durante el período en cuestión.  

-   **Permitir descargas de BITS fuera del período de limitación**  

   Seleccione esta opción para permitir que los clientes de Configuration Manager puedan usar configuraciones de BITS independientes fuera del período especificado.  

-   **Velocidad de transferencia máxima fuera del período de limitación (Kbps)**  

   Especifique la velocidad de transferencia máxima que los clientes usarán fuera del período de limitación de BITS si ha seleccionado permitir la limitación de BITS fuera del período.  

## <a name="client-cache-settings"></a>Configuración de la memoria caché del cliente

- **Configurar BranchCache**

  A partir de la versión 1606, use esta opción para configurar el equipo cliente para [BranchCache](/sccm/core/plan-design/configs/support-for-windows-features-and-networks#branchcache). Para permitir el almacenamiento en caché de BranchCache en el cliente, establezca **Habilitar BranchCache** en **Sí**.

- **Habilitar BranchCache**

Habilita BranchCache en los equipos cliente.

- **Tamaño máximo de la caché de BranchCache (porcentaje de disco)**

- **Configurar el tamaño de la caché de cliente**

  La caché del cliente en los equipos Windows almacena los archivos temporales que se usan para instalar aplicaciones y programas. Elija **Sí** y, luego, especifique lo siguiente:
    - **Tamaño máximo de caché** (megabytes). 
    - **Tamaño de caché máximo** (porcentaje de disco).
El tamaño de la caché de cliente puede expandirse hasta el tamaño máximo en MB o el porcentaje del disco, **lo que sea inferior**. Si esta opción se establece en **No**, el tamaño predeterminado es 5120 MB.

- **Habilitar el cliente de Configuration Manager en el SO completo para compartir contenido**

Habilita la caché del mismo nivel para clientes de Configuration Manager. Después, especifique la información del puerto con el que el cliente se comunica con el equipo del mismo nivel. Configuration Manager configurará automáticamente las reglas de Firewall de Windows para permitir este tráfico. Debe configurar los puertos manualmente si usa otro firewall.




## <a name="client-policy"></a>Directiva de cliente  

-   **Intervalo de sondeo de directiva de cliente (minutos)**  

   Especifique con qué frecuencia descargan los siguientes clientes de Configuration Manager la directiva de cliente:  

  -   Equipos Windows (por ejemplo, equipos de sobremesa, servidores, equipos portátiles)  

  -   Dispositivos móviles inscritos por Configuration Manager  

  -   Equipos Mac  

  -   Equipos que ejecutan Linux o UNIX  

-   **Habilitar sondeo de directiva de usuario en clientes**  

   Si establece esta opción en **True** o **Sí** y Configuration Manager [ha detectado el usuario](../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser), los clientes de los equipos recibirán aplicaciones y programas destinados al usuario que ha iniciado sesión.  

   Ya que el catálogo de aplicaciones recibe la lista de software disponible para usuarios desde el servidor de sitio, no es necesario configurar este valor como **True** o **Sí** para que los usuarios puedan ver y solicitar aplicaciones del catálogo de aplicaciones. Pero si este valor es **False** o **No**, el método siguiente no funcionará cuando los usuarios usen el catálogo de aplicaciones:  

  -   Los usuarios no podrán instalar las aplicaciones que vean en el catálogo de aplicaciones.  

  -   Los usuarios no verán notificaciones acerca de sus solicitudes de aprobación de aplicaciones. En lugar de ello, deberán actualizar el catálogo de aplicaciones y comprobar el estado de aprobación.  

  -   Los usuarios no recibirán revisiones ni actualizaciones de las aplicaciones que se publiquen en el catálogo de aplicaciones. Pero sí verán los cambios de la información de las aplicaciones en el catálogo de aplicaciones.  

  -   Si quita una implementación de aplicación una vez que el cliente instaló la aplicación desde el catálogo de aplicaciones, los clientes comprobarán que la aplicación está instalada durante al menos dos días.  

   Además, si este valor es **False** o **No**, los usuarios no recibirán las aplicaciones requeridas que implemente en ellos, ni ninguna otra tarea de administración de las directivas de usuario.  

   Esta configuración se aplica a los usuarios cuando sus equipos estén en la intranet y conectados a Internet. Debe ser **True** o **Sí** si también quiere habilitar directivas de usuario en Internet.  

-   **Habilitar solicitudes de directiva de usuario de clientes de Internet**  

   Si el cliente y el sitio están configurados para la administración de cliente basada en Internet, y establece esta opción en **True** o **Sí** y se cumplen las dos condiciones siguientes, los usuarios recibirán la directiva de usuario cuando sus equipos estén conectados a Internet:  

  -   La configuración de cliente **Enable user policy polling on clients** (Habilitar sondeo de directiva de usuario en clientes) es **True** o **Habilitar directiva de usuario en clientes** es **Sí**.  

  -   El punto de administración basado en Internet autentica correctamente al usuario mediante la autenticación de Windows (Kerberos o NTLM).  

   Si deja esta opción como **Falso** o **No**, o si alguna de las condiciones no se cumple, los equipos conectados a Internet solo recibirán directivas de equipo. En este escenario, los usuarios sí podrán ver, solicitar e instalar aplicaciones desde un catálogo de aplicaciones basado en Internet. Si este valor es **False** o **No** pero **Enable user policy polling on clients** (Habilitar sondeo de directiva de usuario en clientes) es **True** o **Habilitar directiva de usuario en clientes** es **Sí**, los usuarios no recibirán directivas de usuario hasta que los equipos se conecten a la intranet.  

   Para obtener más información sobre la administración de clientes en Internet, consulte la sección [Considerations for client communications from the Internet or an untrusted forest](../../../core/plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan) (Consideraciones sobre las comunicaciones de cliente desde Internet o desde un bosque que no es de confianza) del tema [Communications between endpoints in System Center Configuration Manager](../../../core/plan-design/hierarchy/communications-between-endpoints.md) (Comunicaciones entre puntos de conexión en System Center Configuration Manager).  

  > [!NOTE]  
  >  Las solicitudes de aprobación de aplicación de los usuarios no requieren directivas de usuario ni autenticación de usuario.  

##  <a name="compliance-settings"></a>Configuración de cumplimiento  

-   **Programar evaluación de compatibilidad**  

     Seleccione **Programar** para crear la programación predeterminada que se mostrará a los usuarios cuando estos implementen una línea base de configuración. Este valor se puede configurar para cada línea de base en el cuadro de diálogo **Implementar línea de base de configuración** .  

-   **Habilitar perfiles y datos de usuario**  

     Seleccione **Sí** para implementar los elementos de configuración de [perfiles y datos de usuario](../../../compliance/deploy-use/create-user-data-and-profiles-configuration-items.md) en los equipos con Windows 8 de su jerarquía.  

## <a name="computer-agent"></a>Agente de equipo  

-   **Punto de sitios web del catálogo de aplicaciones predeterminado**  

     Configuration Manager utiliza este valor para conectar a los usuarios al catálogo de aplicaciones desde el Centro de software. Puede especificar un servidor que hospede el punto de sitios web del catálogo de aplicaciones por su nombre NetBIOS o FQDN, especificar la detección automática o especificar una dirección URL para implementaciones personalizadas. En la mayoría de los casos, la detección automática es la mejor opción, ya que ofrece las siguientes ventajas:  

    -   Los clientes reciben automáticamente un punto de sitios web del catálogo de aplicaciones desde su sitio, si este tiene un punto de sitios web del catálogo de aplicaciones.  

    -   Los puntos de sitios web del catálogo de aplicaciones de la intranet que están configurados para HTTPS tienen preferencia sobre los que no lo están. Esto ayuda a proteger contra un servidor no autorizado.

    -   Si los clientes están configurados para la administración de clientes basados en la intranet y en Internet, se les dará un punto de sitios web del catálogo de aplicaciones basado en Internet cuando se encuentren en Internet, y un punto de sitios web del catálogo de aplicaciones basados en la intranet cuando se encuentren en la intranet.  

     La detección automática no garantiza que se vaya a dar a los clientes el punto de sitios web del catálogo de aplicaciones que esté más cercano a ellos. Puede decidir no utilizar **Detectar automáticamente** por las razones siguientes:  

     -   Desea configurar manualmente el servidor más cercano para los clientes o asegurarse de que no se conectan a un servidor a través de una conexión de red lenta.  

     -   Desea controlar qué clientes se conectan a qué servidor. Esta configuración podría darse por motivos de pruebas, rendimiento o empresariales.  

     -   No desea esperar hasta 25 horas o hasta un cambio de la red para que los clientes se configuren con un punto de sitios web del catálogo de aplicaciones diferente.  

     Si especifica el punto de sitios web del catálogo de aplicaciones en lugar de usar la detección automática, especifique el nombre NetBIOS en lugar del FQDN de intranet. Esto ayuda a reducir la probabilidad de que se soliciten las credenciales a los usuarios cuando se conecten al catálogo de aplicaciones de la intranet. Para utilizar el nombre de NetBIOS, se deben cumplir las siguientes condiciones:  

     -   Se especificó el nombre de NetBIOS en las propiedades del punto de sitios web del catálogo de aplicaciones.  

     -   Usa WINS o todos los clientes están en el mismo dominio que el punto de sitios web del catálogo de aplicaciones.  

     -   El punto de sitios web del catálogo de aplicaciones está configurado para conexiones de cliente HTTP o HTTPS, y el certificado del servidor web tiene el nombre NetBIOS.  

     Normalmente, se les piden las credenciales a los usuarios si la dirección URL tiene un nombre de dominio completo, pero no si la dirección URL es un nombre NetBIOS. Espere que siempre se les solicite a los usuarios cuando se conectan desde Internet, ya que esta conexión debe utilizar el nombre completo de Internet. Si se solicitan credenciales a los usuarios cuando están en Internet, asegúrese de que el servidor que ejecuta el punto de sitios web del catálogo de aplicaciones puede conectarse a un controlador de dominio para la cuenta del usuario, de modo que éste pueda autenticarse mediante Kerberos.  

    > [!NOTE]  
    >  Funcionamiento de la detección automática:  
    >   
    >  el cliente realiza una solicitud de ubicación de servicio a un punto de administración. Si hay un punto de sitios web del catálogo de aplicaciones en el mismo sitio que el cliente, se proporcionará este servidor al cliente como el servidor del catálogo de aplicaciones que debe utilizar. Si hay más de un punto de sitios web del catálogo de aplicaciones disponible en el sitio, los servidores habilitados para HTTPS prevalecerán sobre los que no están habilitados para HTTPS. Después de este filtrado, se proporcionará a todos los clientes uno de los servidores para que los usen como catálogo de aplicaciones; Configuration Manager no lleva a cabo un equilibrio de carga entre varios servidores. Si el sitio del cliente no tiene ningún punto de sitios web del catálogo de aplicaciones, el punto de administración devolverá de forma no determinista uno de la jerarquía.  
    >   
    >  Cuando el cliente está en la intranet, si el punto de sitios web del catálogo de aplicaciones seleccionado está configurado con un nombre NetBIOS para la dirección URL del catálogo de aplicaciones, los clientes recibirán este nombre en lugar del nombre completo de la intranet. Si se detecta que el cliente está en Internet, sólo se proporcionará al cliente el nombre completo de Internet.  
    >   
    >  El cliente realiza dicha solicitud de ubicación de servicio cada 25 horas, o cada vez que detecte un cambio de la red. Por ejemplo, si el cliente pasa de la intranet a Internet, y el cliente puede localizar un punto de administración basado en Internet, este punto proporcionará a los clientes servidores del punto de sitios web del catálogo de aplicaciones basado en Internet.  

-   **Agregar sitio web predeterminado del catálogo de aplicaciones a una zona de sitios de confianza de Internet Explorer**  

     Si esta opción es **True** o **Sí**, la dirección URL del sitio web del catálogo de aplicaciones predeterminada se agregará automáticamente a la zona de sitios de confianza de Internet Explorer en los clientes.  

     Este valor asegura que no está habilitada la configuración de Internet Explorer para el modo protegido. Si el modo protegido está habilitado, es posible que el cliente de Configuration Manager no pueda instalar aplicaciones desde el catálogo de aplicaciones. De forma predeterminada, la zona de sitios de confianza también admite el inicio de sesión de usuario para el catálogo de aplicaciones, lo que requiere la autenticación de Windows.  

     Si deja esta opción como **Falso**, es posible que los clientes de Configuration Manager no puedan instalar aplicaciones del catálogo de aplicaciones a menos que estas opciones de Internet Explorer se configuren en otra zona para la dirección URL del catálogo de aplicaciones que usan los clientes.  

    > [!NOTE]  
    >  Si Configuration Manager agregó un catálogo de aplicaciones predeterminado a la zona de sitios de confianza, Configuration Manager quitará una dirección URL del catálogo de aplicaciones predeterminada anterior que agregó Configuration Manager antes de agregar una entrada nueva.  
    >   
    >  Configuration Manager no puede agregar la dirección URL si ya está especificada en una de las zonas de seguridad. En este escenario, deberá quitar la dirección URL de la otra zona, o bien realizar manualmente la configuración requerida de Internet Explorer.  

-   **Permitir que las aplicaciones de Silverlight se ejecuten en modo de confianza elevado.**  

     Este valor debe ser **Sí** si los usuarios ejecutan el cliente de Configuration Manager y usan el catálogo de aplicaciones.  

     Si cambia esta configuración, entrará en vigor cuando los usuarios carguen sus exploradores o actualicen las ventanas del explorador que tengan abiertas.  

     Para obtener más información sobre esta configuración, consulte la sección [Certificados de Microsoft Silverlight 5 y modo de confianza elevado necesarios para el catálogo de aplicaciones](../../../apps/plan-design/security-and-privacy-for-application-management.md#BKMK_CertificatesSilverlight5) del tema [Seguridad y privacidad de la administración de aplicaciones en System Center Configuration Manager](../../../apps/plan-design/security-and-privacy-for-application-management.md).  

-   **Nombre de organización mostrado en el Centro de software**  

     Escriba el nombre que ven los usuarios en el Centro de software. Esta información de marca ayuda a los usuarios a identificar a esta aplicación como un origen de confianza.  

-   **Usar el nuevo Centro de software**  

     Si esta opción está habilitada, todos los equipos cliente a los que se aplican estas configuraciones de cliente usarán el nuevo Centro de software. En el Centro de software se muestran aplicaciones disponibles para el usuario a las que antes solo se podía tener acceso desde el catálogo de aplicaciones que depende de Silverlight.  

     Los roles de sistema de sitio de punto de sitios web del catálogo de aplicaciones y de punto de servicio web del catálogo de aplicaciones siguen siendo necesarios para que las aplicaciones disponibles para el usuario aparezcan en el Centro de software.  

     Para obtener más información, consulte [Planear y configurar la administración de aplicaciones en Configuration Manager](../../../apps/plan-design/plan-for-and-configure-application-management.md).  

-   **Permisos de instalación**  

    > [!WARNING]  
    >  Esta configuración se aplica al catálogo de aplicaciones y al Centro de software. No tiene efecto cuando los usuarios utilizan el portal de la compañía.  

     Configure cómo pueden iniciar los usuarios la instalación de software, las actualizaciones de software y las secuencias de tareas:  

    -   **Todos los usuarios**: los usuarios que iniciaron sesión en un equipo cliente con cualquier permiso excepto Invitado pueden iniciar la instalación de software, las actualizaciones de software y las secuencias de tareas.  

    -   **Solo administradores**: los usuarios que iniciaron sesión en un equipo cliente deben ser miembros del grupo de administradores locales para iniciar la instalación de software, las actualizaciones de software y las secuencias de tareas.  

    -   **Solo administradores y usuarios primarios**: los usuarios que iniciaron sesión en un equipo cliente deben ser miembros del grupo de administradores locales o usuarios primarios del equipo para iniciar la instalación de software, las actualizaciones de software y las secuencias de tareas.  

    -   **Ningún usuario**: ningún usuario que inició sesión en un equipo cliente podrá iniciar la instalación de software, las actualizaciones de software y las secuencias de tareas. Las implementaciones necesarias para el equipo siempre se instalan en la fecha límite. Los usuarios no pueden iniciar la instalación de software desde el catálogo de aplicaciones o el Centro de software.  

-   **Suspender indicación de PIN de BitLocker en el reinicio**  

     Si la indicación de PIN de BitLocker está configurada en los equipos, esta opción puede omitir el requisito de escribir un PIN cuando se reinicie el equipo después de una instalación de software.  

    -   **Siempre**: Configuration Manager suspenderá temporalmente BitLocker después de que haya instalado software que requiere un reinicio y haya comenzado a reiniciar el equipo. Esta configuración solo se aplica a un reinicio del equipo iniciado por Configuration Manager, y no suspende el requisito de escribir el PIN de BitLocker cuando el usuario reinicie el equipo. El requisito de entrada de PIN de BitLocker se reanudará tras el inicio de Windows.

    -   **Nunca**: Configuration Manager no suspende BitLocker en el siguiente inicio del equipo después de que haya instalado software que requiera un reinicio. En esta situación, la instalación del software no puede finalizar hasta que el usuario escriba el PIN para completar el proceso de inicio estándar y cargue Windows.

-   **Un software adicional administra la implementación de aplicaciones y actualizaciones de software**  

     Habilite esta opción solo si se cumple alguna de las siguientes condiciones:  

    -   Utiliza una solución de proveedor que requiere que esta opción esté habilitada.  

    -   Utilice el kit de desarrollo de software (SDK) de Configuration Manager para administrar las notificaciones de agente de cliente y la instalación de aplicaciones y actualizaciones de software.  

    > [!WARNING]  
    >  Si selecciona esta opción y no se cumple ninguna de estas condiciones, las actualizaciones de software y las aplicaciones necesarias no se instalarán en los clientes. Esta configuración no impide que los usuarios instalen aplicaciones desde el catálogo de aplicaciones, ni que se instalen paquetes, programas y secuencias de tareas en los equipos cliente.  

-   **Directiva de ejecución de PowerShell**  

     Configure cómo pueden ejecutar los clientes de Configuration Manager scripts de Windows PowerShell. Estos scripts se suelen usar para la detección de elementos de configuración para la configuración de compatibilidad. También pueden enviarse en una implementación como script estándar.  

    -   **Desviar**: el cliente de Configuration Manager desvía la configuración de Windows PowerShell en el equipo cliente para que puedan ejecutarse los scripts sin firmar.  

    -   **Restringido**: el cliente de Configuration Manager usa la configuración actual de Windows PowerShell en el equipo cliente. Esta configuración determina si se pueden ejecutar scripts sin firmar.  

    -   **Todos firmados**: el cliente de Configuration Manager ejecuta scripts solo si los ha firmado un editor de confianza. Esta restricción se aplica independientemente de la configuración actual de Windows PowerShell del equipo cliente.  

     Esta opción requiere al menos la versión 2.0 de Windows PowerShell. El valor predeterminado es **Todos firmados**.  

    > [!TIP]  
    >  Si no se ejecutan los scripts sin firmar debido a esta configuración de cliente, Configuration Manager informará de este error de las siguientes maneras:  
    >   
    > -   Identificador de error **0X87D00327** y la descripción **El script no se firmó** como error de estado de implementación en el área de trabajo **Supervisión** de la consola de Configuration Manager.  
    > -   Códigos de error y descripciones de **0X87D00327** y **El script no se firmó** o **0X87D00320** y **Aún no se ha instalado el host de script** con el tipo de error **Error de detección** en informes. Un ejemplo de esto es **Detalles de errores de elementos de configuración en una línea de base de configuración para un activo**.  
    > -   El mensaje **Script is not signed (Error: 87D00327; Source: CCM)** en el archivo **DcmWmiProvider.log** .  

-   **Mostrar notificaciones para nuevas implementaciones**  

     Elija **Sí** si desea que aparezca una notificación para las implementaciones que han estado disponibles menos de una semana.  Este mensaje se mostrará cada vez que se inicie el agente cliente.

-   **Deshabilitar selección aleatoria de fecha límite**  

     Esta configuración determina si el cliente usa un retardo de activación de hasta dos horas para instalar actualizaciones de software necesarias cuando se alcanza la fecha límite. De forma predeterminada, el retardo de activación está deshabilitado.  

     Para escenarios de infraestructura de escritorio virtual (VDI), este retardo puede ayudar a distribuir el procesamiento de la CPU y la transferencia de datos para un equipo que tenga varias máquinas virtuales que ejecutan el cliente de Configuration Manager. Aunque no use VDI, si muchos clientes instalan las mismas actualizaciones al mismo tiempo, se puede incrementar negativamente el uso de la CPU en el servidor del sitio. También puede ralentizar los puntos de distribución y reducir considerablemente el ancho de banda de red disponible.  

     Si las actualizaciones de software necesarias deben instalarse sin demora una vez alcanzada la fecha límite configurada, seleccione **Sí** para esta opción.  

-   **Período de gracia para el cumplimiento tras la fecha límite de la implementación (horas)**

     En algunos casos, es posible que quiera dar más tiempo a los usuarios para instalar las implementaciones de aplicaciones o las actualizaciones de software necesarias más allá de los plazos que estableció. Normalmente esto es necesario cuando un equipo ha estado apagado durante un largo período de tiempo y tiene que instalar muchas implementaciones de aplicaciones o actualizaciones. Por ejemplo, si un usuario acaba de volver de vacaciones, es posible que tenga que esperar bastante mientras se instalan las implementaciones de aplicaciones vencidas. Para solucionar este problema, puede definir un período de gracia de cumplimiento mediante la implementación de la configuración de cliente de Configuration Manager en una colección.

     Puede establecer un período de gracia de entre 1 y 120 horas. Esta configuración se usa en conjunto con la propiedad de implementación **Retrasar el cumplimiento de esta implementación de acuerdo con las preferencias del usuario**. Para obtener más detalles, consulte [Implementar aplicaciones](/sccm/apps/deploy-use/deploy-applications).

##  <a name="computer-restart"></a>Reinicio de equipo  
 Si especifica estos valores de reinicio del equipo, asegúrese de que el valor para el intervalo de notificación temporal de reinicio y el valor para el intervalo final de cuenta atrás tengan una duración inferior al período de mantenimiento más corto que se aplica al equipo.  

 Para obtener más información sobre las ventanas de mantenimiento, consulte [Cómo usar ventanas de mantenimiento en System Center Configuration Manager](../../../core/clients/manage/collections/use-maintenance-windows.md).  

##  <a name="endpoint-protection"></a>Endpoint Protection  

-   **Administrar el cliente de Endpoint Protection en equipos cliente**  

     Seleccione **True** o **Sí** si quiere administrar los clientes existentes de Endpoint Protection en los equipos de la jerarquía.  

     Seleccione esta opción si ya ha instalado el cliente de Endpoint Protection y quiere administrarlo con Configuration Manager.  

     Además, seleccione esta opción si quiere crear un script para desinstalar una solución antimalware existente, instalar el cliente de Endpoint Protection e implementar este script mediante el uso de una aplicación o un paquete y un programa de Configuration Manager.  

-   **Instalar cliente de Endpoint Protection en equipos cliente**  

     Seleccione **True** o **Sí** para instalar y habilitar el cliente de Endpoint Protection en los equipos cliente en los que todavía no esté instalado.  

    > [!NOTE]  
    >  Si el cliente de Endpoint Protection ya está instalado y se selecciona **False** o **No**, no se desinstalará el cliente de Endpoint Protection. Para instalar el cliente de Endpoint Protection, establezca la configuración de cliente **Administrar el cliente de Endpoint Protection en equipos cliente** en **False** o **No**. Después, implemente un paquete y un programa para desinstalar el cliente de Endpoint Protection.  

-   **Para dispositivos de Windows Embedded con filtros de escritura, confirmar la instalación del cliente de Endpoint Protection (reinicio necesario)**  

     Seleccione **Sí** para deshabilitar el filtro de escritura en el dispositivo Windows Embedded y reiniciar el dispositivo. Esto confirma la instalación en el dispositivo.  

     Si se especifica **No** , el cliente se instalará en una superposición temporal que se borrará cuando se reinicie el dispositivo. En esta escenario, el cliente de Endpoint Protection no se confirmará hasta que otra instalación confirme los cambios en el dispositivo. Esta es la configuración predeterminada.  

-   **Suprimir cualquier reinicio de equipo obligatorio después de instalar el cliente de Endpoint Protection**  

     Seleccione **True** o **Sí** para suprimir un reinicio del equipo si es necesario una vez instalado el cliente de Endpoint Protection.  

    > [!IMPORTANT]  
    >  Si el cliente de Endpoint Protection requiere un reinicio del equipo y este valor es **False**, el reinicio tendrá lugar independientemente de las ventanas de mantenimiento que se hayan configurado.  

-   **Período de tiempo permitido que los usuarios pueden posponer un reinicio obligatorio para llevar a cabo la instalación de Endpoint Protection (horas)**  

     Especifique el número de horas que los usuarios pueden posponer un reinicio del equipo si es necesario después de la instalación del cliente de Endpoint Protection. Esta opción solo se puede configurar si la opción **Suprimir cualquier reinicio de equipo obligatorio después de instalar el cliente de Endpoint Protection** es **False**.  

-   **Deshabilitar orígenes alternativos (como Windows Update, Microsoft Windows Server Update Services o recursos compartidos de UNC) para la actualización de definición inicial en los equipos cliente**  

     Seleccione **True** o **Sí** si quiere que Configuration Manager solo instale la actualización de definición inicial en los equipos cliente. Esta configuración puede ser útil para evitar conexiones de red innecesarias y reducir el ancho de banda de red durante la instalación inicial de la actualización de definiciones.  

##  <a name="hardware-inventory"></a>Inventario de hardware  

-   **Tamaño de archivo MIF personalizado máximo (KB)**  

     Especifique el tamaño máximo, en kilobytes, que se permite para cada archivo MIF personalizado que se recopilará de un cliente durante un ciclo de inventario de hardware. Si algún archivo MIF supera este tamaño, el inventario de hardware de Configuration Manager no lo procesará. Puede especificar un tamaño de entre 1 y 5000 KB. De forma predeterminada, este valor está establecido en 250 KB. Esta configuración no afecta al tamaño del archivo de datos de inventario de hardware normal.  

    > [!NOTE]  
    >  Este valor solo está disponible en la configuración predeterminada del cliente.  

-   **Clases de inventario de hardware**  

     En Configuration Manager, puede ampliar la información de hardware que se recopila de los clientes sin necesidad de editar manualmente el archivo sms_def.mof. Seleccione **Establecer clases** si quiere ampliar el inventario de hardware de Configuration Manager. Para obtener más información, consulte [Cómo configurar el inventario de hardware en System Center Configuration Manager](../../../core/clients/manage/inventory/configure-hardware-inventory.md).  

-   **Recopilar archivos MIF**  

     Use esta opción para especificar si quiere recopilar archivos MIF de los clientes de Configuration Manager durante el inventario de hardware.  

     Para que un archivo MIF sea recopilado por el inventario de hardware, deberá estar en la ubicación correcta del equipo cliente. De forma predeterminada, los archivos están ubicados del modo siguiente:  

    -   Los archivos IDMIF deben estar en la carpeta Windows\System32\CCM\Inventory\Idmif.  

    -   Los archivos NOIDMIF deben estar en la carpeta Windows\System32\CCM\Inventory\Noidmif.  

    > [!NOTE]  
    >  Este valor solo está disponible en la configuración predeterminada del cliente.

-   **Retraso aleatorio máximo**

    La recopilación de información de hardware es aleatoria hasta cuatro horas, de manera que la operación no se realiza simultáneamente en todos los clientes. Puede establecer el retraso máximo para limitar el tiempo durante el que tiene lugar la operación.      

##  <a name="metered-internet-connections"></a>Conexiones a Internet de uso medido  
 Puede administrar la forma en que los equipos cliente de Windows 8 se comunican con los sitios de Configuration Manager cuando usan conexiones a Internet de uso medido. En ocasiones, los proveedores de acceso a Internet cobran según la cantidad de datos que envía y recibe cuando se utiliza una conexión a Internet de uso medido.  

> [!NOTE]  
>  La configuración de cliente no se aplica a los equipos cliente de Windows 8 en las siguientes situaciones:  
>   
> -   El equipo está en una conexión de datos de itinerancia: el cliente de Configuration Manager no lleva a cabo ninguna tarea que requiera la transferencia de datos a sitios de Configuration Manager.  
> -   Las propiedades de conexión de red de Windows se configuran como de uso no medido: el cliente de Configuration Manager se comporta como si fuera una conexión a Internet de uso no medido y, de este modo, transfiere datos a los sitios de Configuration Manager.  

-   **Comunicación de clientes en conexiones a Internet de uso medido**  

     En la lista desplegable, elija una de las siguientes opciones para los equipos cliente de Windows 8:  

    -   **Permitir**: se permiten todas las comunicaciones del cliente a través de la conexión a Internet de uso medido a menos que el dispositivo cliente utilice una conexión de datos en movilidad.  

    -   **Limitar**: solo se permiten las siguientes comunicaciones de cliente a través de la conexión a Internet de uso medido:  

        -   Recuperación de la directiva de cliente  

        -   Mensajes de estado del cliente para enviar al sitio  

        -   Solicitudes de instalación de software mediante el catálogo de aplicaciones  

        -   Implementaciones requeridas (una vez alcanzada la fecha límite de instalación)  

        > [!IMPORTANT]  
        >  Si un usuario inicia una instalación de software desde el Centro de software o el catálogo de aplicaciones, éstos siempre estarán permitidos, independientemente de la configuración que tenga la conexión de Internet de uso medido.  

         Si se alcanza el límite de transferencia de datos para la conexión a Internet de uso medido, el cliente ya no intentará comunicarse con los sitios de Configuration Manager.  

    -   **Bloquear**: el cliente de Configuration Manager no intenta comunicarse con los sitios de Configuration Manager si se encuentra en una conexión a Internet de uso medido. Es el valor predeterminado.  

##  <a name="power-management"></a>Administración de energía  

-   **Permitir a los usuarios excluir su dispositivo de la administración de energía**  

     En la lista desplegable, seleccione **True** o **Sí** para permitir que los usuarios del Centro de software excluyan sus equipos de cualquier configuración de administración de energía establecida.  

-   **Habilitar proxy de reactivación**  

     Especifique **Sí** para complementar la configuración de Wake on LAN del sitio cuando se configure para paquetes de unidifusión.  

     Para obtener más información sobre el proxy de reactivación, consulte [Planear la reactivación de clientes en System Center Configuration Manager](../../../core/clients/deploy/plan/plan-wake-up-clients.md).  

    > [!WARNING]  
    >  No habilite el proxy de reactivación en una red de producción sin entender primero cómo funciona y evaluarlo en un entorno de prueba.  

-   **Número de puerto de proxy de reactivación (UDP)**  

     Mantenga el valor predeterminado del número de puerto que los equipos administrados usan para enviar paquetes de reactivación a equipos en suspensión o cambie el número a un valor de su elección.  

     El número de puerto especificado aquí se configura automáticamente para los clientes que ejecuten el Firewall de Windows cuando configure la opción **Excepción del Firewall de Windows para proxy de reactivación**. Si los clientes ejecutan otro firewall, debe configurarlo manualmente para permitir especificar el número de puerto UDP para este valor.  

-   **Número de puerto de Wake On LAN (UDP)**  

     Mantenga el valor predeterminado de 9, a menos que haya cambiado el número de puerto de Wake on LAN (UDP) en la pestaña **Puertos** en las **Propiedades** del sitio.  

    > [!IMPORTANT]  
    >  Este número debe coincidir con el número en las **Propiedades**del sitio. Si cambia este número en un lugar, este no se actualizará automáticamente en el otro lugar.  

##  <a name="remote-tools"></a>Herramientas remotas  

-   **Habilitar control remoto en clientes** y **Perfiles de excepción de firewall**  

     Seleccione si el control remoto de Configuration Manager está habilitado para todos los equipos cliente que reciban esta configuración de cliente. Seleccione **Configurar** para habilitar el control remoto. Opcionalmente, configure las opciones del firewall para permitir que el control remoto trabaje en los equipos cliente.  

     El control remoto está deshabilitado de forma predeterminada.  

    > [!IMPORTANT]  
    >  Si no se configuran las opciones del firewall, el control remoto podría no funcionar correctamente.  

-   **Los usuarios pueden cambiar la directiva o la configuración de notificaciones en el Centro de software**  

     Seleccione si los usuarios pueden cambiar opciones del control remoto desde el Centro de software.  

-   **Permitir el control remoto de un equipo desatendido**  

     Seleccione si un administrador puede usar el control remoto para tener acceso a un equipo cliente que ha cerrado la sesión o está bloqueado. Solo se puede usar el control remoto en un equipo que ha iniciado sesión y está desbloqueado cuando esta opción está deshabilitada.  

-   **Solicitar al usuario permiso de control remoto**  

     Seleccione si el equipo cliente mostrará un mensaje en el que se solicita el permiso del usuario antes de permitir una sesión de control remoto.  

-   **Conceder permiso de control remoto al grupo de administradores locales**  

     Seleccione si los administradores locales del servidor que inicia la conexión de control remoto pueden establecer sesiones de control remoto en los equipos cliente.  

-   **Nivel de acceso permitido**  

     Especifique el nivel de acceso de control remoto que se permitirá. Puede elegir entre:  

    -   Control total  

    -   Ver solo  

    -   Ninguno  

-   **Visores permitidos de control remoto y asistencia remota**  

     Seleccione **Visores** para abrir el cuadro de diálogo **Configurar valor de cliente** y especifique los nombres de los usuarios de Windows que podrán establecer sesiones de control remoto en equipos cliente.  

-   **Mostrar icono de notificación de sesión en la barra de tareas**  

     Seleccione esta opción para mostrar un icono en la barra de tareas de los equipos cliente para indicar que hay activa una sesión de control remoto.  

-   **Mostrar barra de conexión a la sesión**  

     Seleccione esta opción para mostrar una barra de conexión a la sesión de alta visibilidad en los equipos cliente para indicar que hay una sesión de control remoto activa.  

-   **Reproducir un sonido en el cliente**  

     Seleccione esta opción para usar un sonido a fin de indicar si una sesión de control remoto está activa en un equipo cliente. Puede reproducir un sonido cuando se conecte o desconecte la sesión, o puede reproducir un sonido varias veces durante la sesión.  

-   **Administrar configuración de asistencia remota no solicitada**  

     Seleccione esta opción para permitir que Configuration Manager administre sesiones de asistencia remota no solicitada.  

     En una sesión de asistencia remota no solicitada, el usuario del equipo cliente no solicita ayuda para iniciar una sesión.  

-   **Administrar configuración de asistencia remota solicitada**  

     Seleccione esta opción para permitir que Configuration Manager administre sesiones de asistencia remota solicitada.  

     En una sesión de asistencia remota solicitada, el usuario del equipo cliente envía una solicitud de asistencia remota al administrador.  

-   **Nivel de acceso de asistencia remota**  

     Seleccione el nivel de acceso que se va a asignar a las sesiones de asistencia remota que se inician en la consola de Configuration Manager.  

    > [!NOTE]  
    >  El usuario en el equipo cliente siempre debe conceder permiso para que se produzca una sesión de asistencia remota.  

-   **Administrar configuración de Escritorio remoto**  

     Seleccione esta opción para permitir que Configuration Manager administre sesiones de Escritorio remoto en equipos.  

-   **Permitir a los usuarios permitidos conectarse mediante la conexión a Escritorio remoto**  

     Seleccione esta opción para permitir que los usuarios especificados en la lista de visores permitidos se agreguen al grupo de usuarios locales de Escritorio remoto en los equipos cliente.  

-   **Requerir autenticación de nivel de red en equipos que ejecutan el sistema operativo Windows Vista y versiones posteriores**  

     Seleccione esta opción más segura si quiere usar la autenticación de nivel de red para establecer conexiones de Escritorio remoto en equipos cliente que ejecutan Windows Vista o una versión posterior. La autenticación de nivel de red requiere menos recursos del equipo remoto al principio debido a que finaliza la autenticación del usuario antes de establecer una conexión de Escritorio remoto. Este método es más seguro porque puede ayudar a proteger al equipo frente a software o usuarios malintencionados, y reduce el riesgo de ataques por denegación de servicio.  

## <a name="software-deployment"></a>Implementación de software  

-   **Programar la reevaluación para implementaciones**  

     Configure una programación para cuando Configuration Manager vuelva a evaluar las reglas de requisitos para todas las implementaciones. El valor predeterminado es cada 7 días.  

    > [!IMPORTANT]  
    >  Se recomienda que no cambie este valor a un valor inferior al predeterminado. Esto podría afectar negativamente al rendimiento de la red y los equipos cliente.  

     También puede iniciar esta acción desde un equipo cliente de Configuration Manager. Para ello, seleccione la acción **Ciclo de evaluación de implementación de aplicaciones** en la pestaña **Acciones** de **Configuration Manager** en el Panel de control.  

##  <a name="software-inventory"></a>Inventario de software  

-   **Detalle de notificación de inventario**  

     Especifique el nivel de información del archivo en el inventario. Puede crear un inventario de detalles sobre el archivo, detalles sobre el producto asociado al archivo o toda la información del archivo.  

-   **Inventariar estos tipos de archivo**  

     Si quiere especificar los tipos de archivo para incluir en el inventario, seleccione **Tipos** y, después, configure lo siguiente en el cuadro de diálogo **Configurar valor de cliente**:  

    > [!NOTE]  
    >  Si se aplican varias configuraciones de cliente personalizadas a un equipo, se combinará el inventario devuelto por cada configuración.  

    -   Seleccione el icono **Nuevo** para agregar un nuevo tipo de archivo al inventario. Después, especifique la información siguiente en el cuadro de diálogo **Propiedades de archivo inventariado**:  

        -   **Nombre**: proporcione un nombre al archivo que quiere inventariar. Puede usar el carácter **\** para representar cualquier cadena de texto y el carácter **?** para representar un solo carácter. Por ejemplo, si quiere hacer un inventario de todos los archivos con la extensión .doc, especifique el nombre de archivo **\*.doc**.  

        -   **Ubicación**: seleccione **Establecer** para abrir el cuadro de diálogo **Propiedades de ruta de acceso**. Puede configurar el inventario de software para buscar el archivo especificado en todos los discos duros del cliente, buscar en una ruta de acceso especificada (por ejemplo **C:\Carpeta**) o buscar una variable especificada (por ejemplo *%windir%*). También puede buscar en todas las subcarpetas de la ruta de acceso especificada.  

        -   **Excluir archivos cifrados y comprimidos**: cuando se seleccione esta opción, no se incluirá en el inventario ningún archivo comprimido o cifrado.  

        -   **Archivos excluidos en la carpeta Windows**: cuando se seleccione esta opción, no se incluirá en el inventario ningún archivo de la carpeta Windows y sus subcarpetas.  

    -   Seleccione **Aceptar** para cerrar el cuadro de diálogo **Propiedades de archivo inventariado**.  

    -   Agregue todos los archivos que quiera incluir en el inventario y, después, seleccione **Aceptar** para cerrar el cuadro de diálogo **Configurar valor de cliente**.  

-   **Recopilar archivos**  

     Si quiere recopilar archivos de los equipos cliente, seleccione **Archivos** y, después, configure lo siguiente:  

    > [!NOTE]  
    >  Si se aplican varias configuraciones de cliente personalizadas a un equipo, se combinará el inventario devuelto por cada configuración.  

    -   En el cuadro de diálogo **Configurar valor de cliente**, seleccione el icono **Nuevo** para agregar un archivo para su recopilación.  

    -   En el cuadro de diálogo **Propiedades del archivo recopilado** , proporcione la siguiente información:  

        -   **Nombre**: proporcione un nombre al archivo que quiera recopilar. Puede usar el carácter **\** para representar cualquier cadena de texto y el carácter **?** para representar un solo carácter.  

        -   **Ubicación**: seleccione **Establecer** para abrir el cuadro de diálogo **Propiedades de ruta de acceso**. Puede configurar el inventario de software para buscar el archivo que quiere recopilar en todos los discos duros del cliente, buscar en una ruta de acceso especificada (por ejemplo **C:\Carpeta**) o buscar una variable especificada (por ejemplo *%windir%*). También puede buscar en todas las subcarpetas de la ruta de acceso especificada.  

        -   **Excluir archivos cifrados y comprimidos**: cuando se seleccione esta opción, no se recopilará ningún archivo comprimido o cifrado.  

        -   **Detener la recopilación de archivos cuando el tamaño total de archivos supere (KB)**: especifique el tamaño del archivo (en kilobytes) después del cual no se recopilará ninguno más de los archivos especificados en **Nombre**.  

          > [!NOTE]  
          >  El servidor de sitio recopila las cinco versiones cambiadas más recientemente de los archivos recopilados y las almacena en *&lt;directorio de instalación de Configuration Manager\>*\Inboxes\Sinv.box\Filecol. Si un archivo no ha cambiado desde que se recopiló el último inventario de software, ese archivo no se recopilará otra vez.  
          >   
          >  El inventario de software no recopila archivos de más de 20 MB.  
          >   
          >  El valor **Tamaño máximo para todos los archivos recopilados (KB)** del cuadro de diálogo **Configurar valor de cliente** muestra el tamaño máximo de todos los archivos recopilados. Cuando se alcanza este tamaño, se detiene la recopilación de archivos. Los archivos que ya se han recopilado se conservan y se envían al servidor de sitio.  

          > [!IMPORTANT]
          >  Si configura el inventario de software para recopilar muchos archivos de gran tamaño, esto podría afectar negativamente el rendimiento de la red y el servidor de sitio.  

        Para obtener información sobre cómo ver los archivos recopilados, consulte [How to use Resource Explorer to view software inventory in System Center Configuration Manager](../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md) (Cómo usar el Explorador de recursos para ver el inventario de software en System Center Configuration Manager).  

    -   Seleccione **Aceptar** para cerrar el cuadro de diálogo **Propiedades del archivo recopilado**.  

    -   Agregue todos los archivos que quiera recopilar y, después, seleccione **Aceptar** para cerrar el cuadro de diálogo **Configurar valor de cliente**.  

-   **Establecer nombres**  

     Durante el inventario de software, los nombres de fabricantes y productos se recuperan de la información del encabezado de los archivos instalados en los clientes en el sitio. Ya que los nombres en la información de encabezado del archivo no siempre están estandarizados, cuando visualiza la información de inventario de software en el Explorador de recursos o ejecuta consultas es posible que se muestren varias versiones del mismo fabricante o del nombre del producto. Si quiere estandarizar estos nombres para mostrar, seleccione **Establecer nombres** y configure lo siguiente en el cuadro de diálogo **Configurar valor de cliente**:  

    -   **Tipo de nombre**: el inventario de software recopila información sobre los fabricantes y los productos. En la lista desplegable, seleccione si quiere configurar los nombres para mostrar de un **Fabricante** o un **Producto**.  

    -   **Nombre para mostrar**: especifica el nombre para mostrar que quiere usar en lugar de los nombres de la lista **Nombres inventariados**. Puede seleccionar el icono **Nuevo** para especificar un nuevo nombre para mostrar.  

    -   **Nombres inventariados**: seleccione el icono **Nuevo** para agregar un nuevo nombre inventariado que se reemplazará en el inventario de software con el nombre seleccionado en la lista **Nombre para mostrar**. Puede agregar varios nombres que se reemplazarán.  

##  <a name="software-updates"></a>Actualizaciones de software  

-   **Habilitar actualizaciones de software en clientes**  

     Use esta opción para habilitar las actualizaciones de software en los clientes de Configuration Manager. Si desactiva esta opción, Configuration Manager quita del cliente las directivas de implementación existentes. Cuando vuelva a activar esta opción, el cliente descarga la directiva de implementación actual.  

    > [!IMPORTANT]  
    >  Cuando desactiva esta opción, NAP y las directivas de configuración de cumplimiento que se basan en la configuración del dispositivo para las actualizaciones de software dejarán de funcionar.  

-   **Programación de exploración de actualización de software**  

     Utilice esta opción para especificar la frecuencia con la que el cliente inicia un análisis de evaluación del cumplimiento de actualizaciones de software. El análisis de evaluación de cumplimiento determina el estado de las actualizaciones de software en el cliente (por ejemplo, requerida o instalada). Para obtener más información sobre la evaluación de cumplimiento, consulte [Software updates compliance assessment](../../../sum/understand/software-updates-introduction.md#BKMK_SUMCompliance) (Evaluación del cumplimiento de las actualizaciones de software).  

     De forma predeterminada, se usa una programación simple y el examen de cumplimiento se inicia cada 7 días. Puede crear una programación personalizada para especificar el día y la hora de inicio, si desea usar la hora local o UTC, y configurar el intervalo de repetición en un determinado día de la semana.  

    > [!NOTE]  
    >  Si especifica un intervalo de menos de 1 día, Configuration Manager lo establecerá automáticamente de forma predeterminada en 1 día.  

    > [!WARNING]  
    >  La hora de inicio en los equipos cliente es la hora de inicio más una cantidad de tiempo aleatoria de hasta 2 horas. Esto impide que los equipos cliente inicien el análisis y se conecten a Windows Server Update Services (WSUS) en el servidor punto de actualización de software activo al mismo tiempo.  

-   **Programar reevaluación de implementación**  

     Utilice esta opción para configurar la frecuencia con la que el agente cliente de actualizaciones de software vuelve a evaluar el estado de la instalación de actualizaciones de software en equipos cliente de Configuration Manager. Si las actualizaciones de software instaladas previamente ya no figuran en los equipos cliente pero siguen siendo necesarias, se vuelven a instalar.

     La programación de reevaluación de la implementación debe ajustarse según la directiva de la empresa para el cumplimiento de actualizaciones de software, independientemente de si los usuarios tienen la capacidad de desinstalar actualizaciones de software, etc. Tenga en cuenta que cada ciclo de reevaluación de implementación comporta actividad de la CPU del equipo cliente y de la red. De forma predeterminada, se usa una programación simple y el examen de reevaluación de la implementación se inicia cada 7 días.  

    > [!NOTE]  
    >  Si especifica un intervalo de menos de 1 día, Configuration Manager lo establecerá automáticamente de forma predeterminada en 1 día.  

-   **Cuando se alcance una fecha límite de implementación de actualización de software, instalar todas las demás implementaciones de actualización de software cuya fecha límite tenga lugar dentro de un periodo de tiempo específico**  

     Utilice esta opción para instalar todas las actualizaciones de software en las implementaciones requeridas que tienen fechas límite en un periodo de tiempo especificado. Cuando se alcanza una fecha límite de una implementación de actualización de software requerida, se inicia la instalación en los clientes de las actualizaciones de software en la implementación. Esta configuración determina si se va a iniciar la instalación de actualizaciones de software definidas en otras implementaciones necesarias que tienen una fecha límite configurada en el periodo de tiempo especificado.  

     Utilice esta opción para acelerar la instalación de actualizaciones de software para actualizaciones de software necesarias y para, potencialmente, aumentar la seguridad, reducir las notificaciones en pantalla y minimizar los reinicios del sistema en los equipos cliente. De forma predeterminada, esta opción no está habilitada.  

-   **Período de tiempo durante el cual también se instalarán todas las implementaciones pendientes cuya fecha límite sea durante este período**  

     Utilice esta opción para especificar el intervalo de tiempo para la configuración anterior. Puede especificar un valor entre 1 y 23 horas y entre 1 y 365 días. De forma predeterminada, la opción se configura con un valor de 7 días.  

-   **Habilitar instalación de archivos de instalación Express en clientes**

-   **Puerto usado para descargar contenido para archivos de instalación Express**

-   **Habilitar administración del Agente cliente de Office 365** Utilice esta opción para habilitar la administración del Agente cliente de Office 365. Si establece el valor en **Sí**, permite configurar las opciones de instalación de Office 365, descargar archivos desde redes de entrega de contenido (CDN) de Office e implementar los archivos como una aplicación en Configuration Manager.

##  <a name="user-and-device-affinity"></a>Afinidad entre usuario y dispositivo  

-   **Umbral de uso de afinidad de dispositivo de usuario (minutos)**  

     Especifique el número de minutos antes de que Configuration Manager cree una asignación de afinidad de dispositivo de usuario.  

-   **Umbral de uso de afinidad de dispositivo de usuario (días)**  

     Especifica el número de días durante el que se mide el umbral de uso de afinidad.  

    > [!NOTE]  
    >  Por ejemplo, si **Umbral de uso de afinidad de dispositivo de usuario (minutos)** se configura como **60** minutos y **Umbral de uso de afinidad de dispositivo de usuario (días)** se configura como **5** días, el usuario debe usar el dispositivo durante 60 minutos a lo largo de un periodo de 5 días para que se cree automáticamente una afinidad de dispositivo de usuario.  

-   **Configurar automáticamente la afinidad de dispositivo de usuario desde los datos del usuario**  

     Seleccione **True** o **Sí** para que Configuration Manager cree automáticamente afinidades de dispositivo de usuario basadas en la información de uso recopilada.  

##  <a name="mobile-devices"></a>Dispositivos móviles  

-   **Perfil de inscripción de dispositivo móvil**  

     Para poder configurar esta opción, debe configurar la opción de usuario de dispositivo móvil **Permitir a los usuarios inscribir dispositivos móviles** como **Verdadero**. Después, seleccione **Establecer perfil** para especificar un perfil de inscripción que contiene información sobre la plantilla de certificado que quiere usar durante el proceso de inscripción, el sitio que tiene un punto de inscripción y un punto de proxy de inscripción, y el sitio que administrará el dispositivo después de la inscripción.  

    > [!IMPORTANT]  
    >  Asegúrese de configurar una plantilla de certificado para la inscripción de dispositivo móvil antes de configurar esta opción.  

##  <a name="enrollment"></a>Inscripción  

-   **Perfil de inscripción de dispositivo móvil**  

     Para poder configurar esta opción, debe configurar la opción de usuario de inscripción **Permitir a los usuarios inscribir dispositivos móviles y equipos Mac** como **Sí**. Después, seleccione **Establecer perfil** para especificar un perfil de inscripción que contiene información sobre la plantilla de certificado que quiere usar durante el proceso de inscripción, el sitio que tiene un punto de inscripción y un punto de proxy de inscripción, y el sitio que administrará el dispositivo después de la inscripción.  

    > [!IMPORTANT]  
    >  Asegúrese de que ha configurado una plantilla de certificado para la inscripción de dispositivos móviles o para la inscripción de certificados de cliente de Mac antes de configurar esta opción.  

## <a name="user-and-device-affinity"></a>Afinidad entre usuario y dispositivo  

-   **Permitir al usuario definir sus dispositivos primarios**  

     Especifique si los usuarios pueden identificar sus propios dispositivos primarios desde la pestaña **Mis dispositivos** del catálogo de aplicaciones.  
