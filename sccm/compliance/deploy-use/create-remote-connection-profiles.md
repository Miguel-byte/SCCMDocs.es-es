---
title: "Crear perfiles de conexión remota | Microsoft Docs"
description: "Use perfiles de conexión remota de System Center Configuration Manager para permitir a los usuarios conectarse remotamente a equipos de trabajo."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8c6eabc4-5dda-4682-b03e-3a450e6ef65a
caps.latest.revision: "8"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: d12faf657ca99dd572f1b28eb398783426fcdf8c
ms.sourcegitcommit: b438515490e04fb09c82a8af642d38e9a0605178
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/15/2017
---
# <a name="remote-connection-profiles-in-system-center-configuration-manager"></a>Perfiles de conexión remota en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Use perfiles de conexión remota de System Center Configuration Manager para permitir a los usuarios conectarse remotamente a los equipos del trabajo si no están conectados al dominio o si sus equipos personales se conectan a través de Internet.  

 Los usuarios pueden conectarse a su PC del trabajo desde los siguientes tipos de dispositivo:  

-   Equipos que ejecutan Microsoft Windows  

-   Dispositivos que ejecutan iOS  

-   Dispositivos que ejecutan Android  

Los perfiles de conexión remota le permiten implementar la configuración de Conexión a Escritorio remoto en usuarios de su jerarquía de Configuration Manager. A continuación, los usuarios pueden usar el portal de la compañía para obtener acceso a sus equipos principales del trabajo a través de Escritorio remoto mediante la configuración de Conexión a Escritorio remoto proporcionada por el portal de la compañía.  

Se necesita Microsoft Intune para que los usuarios se conecten a sus equipos del trabajo mediante el portal de empresa. Incluso si no usa Intune, los usuarios pueden usar la información del perfil de conexión remota para conectarse a sus equipos del trabajo mediante Escritorio remoto a través de una conexión VPN.  

> [!IMPORTANT]  
>  Cuando se especifica la configuración de perfil de conexión remota mediante la consola de Configuration Manager, la configuración se almacena en la directiva local del equipo cliente. Estas opciones podrían invalidar la configuración de Escritorio remoto establecida por otra aplicación. Además, si usa la directiva de grupo de Windows para establecer la configuración de Escritorio remoto, la configuración especificada en la directiva de grupo invalidará la configuración establecida mediante Configuration Manager.  

 Al instalar Configuration Manager, se crea un grupo de seguridad denominado **Conexión a equipos remotos**. Este grupo se rellena al implementar un perfil de conexión remota que incluye los usuarios principales del equipo en el que se implementa el perfil. Aunque un administrador local puede agregar nombres de usuario al grupo, estos usuarios se quitarán del grupo cuando se vuelva a evaluar la compatibilidad de los perfiles de conexión remota implementados.  

 Si agrega manualmente un usuario a este grupo, el usuario puede iniciar conexiones remotas, pero la información de conexión no se publicará en el portal de la compañía.  

 Si quita manualmente del grupo un usuario agregado por Configuration Manager, este corregirá el cambio automáticamente. Para ello, agregará el usuario de nuevo cuando se vuelva a evaluar la compatibilidad del perfil de conexión remota.  

> [!IMPORTANT]  
>  Si la relación de afinidad entre usuario y dispositivo cambia (por ejemplo, el equipo al que el usuario se conecta deja de ser un dispositivo primario del usuario), Configuration Manager deshabilita el perfil de conexión remota y la configuración de Firewall de Windows para impedir las conexiones al equipo.  

## <a name="prerequisites"></a>Requisitos previos  

### <a name="external-dependencies"></a>Dependencias externas  

|Dependencia|Más información|  
|----------------|----------------------|  
|Servidor de puerta de enlace de Escritorio remoto.|Si desea permitir a los usuarios conectarse a Internet desde fuera del dominio de la compañía, debe instalar y configurar un servidor de puerta de enlace de Escritorio remoto.<br /><br /> Si otra aplicación o configuración de directiva de grupo administra la configuración de Escritorio remoto o Terminal Services, es posible que los perfiles de conexión remota no funcionen correctamente. Al implementar los perfiles de conexión remota desde la consola de Configuration Manager, su configuración se almacena en la directiva local del equipo cliente. Estas opciones podrían invalidar la configuración de Escritorio remoto establecida por otra aplicación. Además, si usa la configuración de directiva de grupo para establecer la configuración de Escritorio remoto, la configuración especificada en la directiva de grupo invalidará la configuración establecida por Configuration Manager.<br /><br /> Para obtener más información acerca de cómo instalar y configurar un servidor de puerta de enlace de Escritorio remoto, consulte la documentación de Windows Server.|  
|Si los equipos cliente ejecutan un firewall basado en host, debe habilitar el programa Mstsc.exe.|Si configura un perfil de conexión remota, debe habilitar la configuración **Permitir excepción del Firewall de Windows para conexiones en dominios de Windows y en redes privadas** . Cuando esta opción está habilitada, Configuration Manager configura automáticamente el Firewall de Windows para habilitar el programa Mstsc.exe. Sin embargo, si los equipos cliente ejecutan otro firewall basado en host, debe configurar manualmente esta dependencia del firewall.<br /><br /> La configuración de la directiva de grupo para configurar Firewall de Windows puede invalidar la configuración establecida en Configuration Manager. Si utiliza la directiva de grupo para configurar el Firewall de Windows, asegúrese de que la configuración de la directiva de grupo no bloquea el programa Mstsc.exe.|  

### <a name="configuration-manager-dependencies"></a>Dependencias de Configuration Manager  

|Dependencia|Más información|  
|----------------|----------------------|  
|Configuration Manager debe estar conectado a Microsoft Intune (lo que se conoce como una configuración híbrida).|Para obtener más información sobre la conexión de Configuration Manager a Microsoft Intune, consulte Administrar dispositivos móviles con Configuration Manager y Microsoft Intune.|  
|Para que un usuario se conecte a un equipo del trabajo en la red de la compañía, dicho equipo debe ser un dispositivo primario del usuario.|Para obtener más información sobre la afinidad entre usuario y dispositivo, consulte [Link users and devices with user device affinity](/sccm/apps/deploy-use/link-users-and-devices-with-user-device-affinity) (Vincular usuarios y dispositivos con afinidad entre usuario y dispositivo).|  
|Para administrar perfiles de conexión remota, se deben tener permisos de seguridad específicos.|El rol de seguridad **Administrador de la configuración de cumplimiento** incluye los permisos necesarios para administrar perfiles de conexión remota. Para obtener más información, consulte <br />[Configure role-based administration](/sccm/core/servers/deploy/configure/configure-role-based-administration) (Configurar la administración basada en roles).|  

## <a name="security-and-privacy-considerations-for-remote-connection-profiles"></a>Consideraciones de seguridad y privacidad para perfiles de conexión remota  

### <a name="security-considerations"></a>Consideraciones de seguridad  

|Práctica recomendada de seguridad|Más información|  
|----------------------------|----------------------|  
|Especifique manualmente la afinidad de dispositivo del usuario en lugar de permitir a los usuarios identificar su dispositivo primario. Además, no habilite la configuración basada en el uso.|Como debe habilitar **Permitir a todos los usuarios principales del equipo de trabajo conectarse remotamente** para poder implementar un perfil de conexión remota, especifique siempre manualmente la afinidad de su dispositivo de usuario. No considere información de autoridad aquélla recopilada de usuarios o del dispositivo. Si implementa perfiles de conexión remota y un usuario administrativo confiable no especifica la afinidad de dispositivo de usuario, es posible que usuarios no autorizados reciban privilegios elevados y que, como resultado, puedan conectarse remotamente a equipos.<br /><br /> Si habilita la configuración basada en el uso, esta información se recopila a través de mensajes de estado que no están protegidos por Configuration Manager. Para mitigar esta amenaza, utilice la firma de bloque de mensajes del servidor (SMB) o el protocolo de seguridad de Internet (IPsec) entre los equipos cliente y el punto de administración.|  
|Restringir los derechos de administración locales en el equipo del servidor de sitio.|Un usuario con derechos administrativos locales en el servidor de sitio puede agregar manualmente miembros al grupo de seguridad de conexión a equipos remotos que Configuration Manager crea y mantiene automáticamente. Esto podría causar una elevación de privilegios, ya que los miembros que se agregan a este grupo reciben permisos de Escritorio remoto.|  

### <a name="privacy-considerations"></a>Consideraciones de privacidad  

-   Si un usuario inicia una conexión para trabajar en un equipo del portal de la compañía, se descarga un archivo con la extensión .rdp o .wsrdp que contiene el nombre de dispositivo y el nombre de servidor de puerta de enlace del Escritorio remoto que se necesita para iniciar la sesión de Escritorio remoto. La extensión del archivo depende del sistema operativo del dispositivo. Por ejemplo, los sistemas operativos Windows 7 y Windows 8 usan un archivo .rdp y Windows 8.1 usa un archivo .wsrdp.  

-   El usuario puede abrir o guardar el archivo .rdp. Si el usuario elige abrir el archivo .rdp, es posible que el archivo se almacene en la memoria caché del explorador web, en función de la configuración de retención del explorador. Si el usuario decide guardar el archivo, no se almacena en la memoria caché del explorador. El archivo se guarda hasta que el usuario lo elimina manualmente.  

-   El archivo .wsrdp se descarga y se guarda automáticamente de forma local. El archivo se sobrescribirá la próxima vez que el usuario ejecute una sesión de Escritorio remoto.  

-   Antes de configurar los perfiles de conexión remota, tenga en cuenta sus requisitos de privacidad.  


## <a name="create-a-remote-connection-profile"></a>Crear un perfil de conexión remota

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad** > **Configuración de cumplimiento** > **Perfiles de conexión remota**.  

3.  En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear perfil de conexión remota**.  

4.  En la página **General** del **Asistente para crear perfil de conexión remota**, especifique un nombre y una descripción opcional para el perfil con un máximo de 256 caracteres para cada uno.  

5.  En la página de configuración **Perfil**, especifique la siguiente configuración para el perfil de conexión remota:  

    -   **Nombre completo y puerto del servidor de puerta de enlace de Escritorio remoto (opcional)** : especifique el nombre del servidor de puerta de enlace de Escritorio remoto que se va a usar para las conexiones.  

        > [!NOTE]  
        >  Configuration Manager no es compatible con el uso de nombres de dominio internacionalizado al especificar un servidor en este cuadro.  
        >   
        >  La longitud del nombre del servidor no debe ser superior a 256 caracteres, y puede contener mayúsculas, minúsculas, caracteres numéricos y los caracteres **–** y **_** , separados por puntos.  

    -   **Permitir conexiones solamente de equipos que ejecutan Escritorio remoto con Autenticación a nivel de red**  

6.  Seleccione **Habilitado** o **Deshabilitado** para las opciones de conexión siguientes:  

    -   **Permitir conexiones remotas a equipos de trabajo**  

    -   **Permitir a todos los usuarios principales del equipo del trabajo conectarse remotamente**  

    -   **Permitir excepción de Firewall de Windows para conexiones en dominios de Windows y en redes privadas**  

    > [!IMPORTANT]  
    >  Las tres opciones deben ser iguales para poder continuar más allá de esta página del asistente.  

7.  En la página **Resumen**, revise las acciones que se realizarán y, después, complete el asistente.  

 El nuevo perfil de conexión remota se muestra en el nodo **Perfiles de conexión remota** en el área de trabajo **Activos y compatibilidad** .  

Implementar un perfil de conexión remota  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad** > **Configuración de cumplimiento** > **Perfiles de conexión remota**.  

3.  En la lista **Perfiles de conexión remota** , seleccione el perfil de conexión remota que desea implementar y, a continuación, en la pestaña **Inicio** , en el grupo **Implementación** , haga clic en **Implementar**.  

4.  En el cuadro de diálogo **Implementar perfil de conexión remota** , especifique la información siguiente:  

    -   **Recopilación** : haga clic en **Examinar** para seleccionar la recopilación de dispositivos en la que desea implementar el perfil de conexión remota.  

    -   **Corregir las reglas no compatibles cuando se admita**: habilite esta opción para corregir automáticamente el perfil de conexión remota si no es conforme en un dispositivo (por ejemplo, si no figura en este).  

    -   **Permitir la corrección fuera de la ventana de mantenimiento**: si se ha configurado una ventana de mantenimiento para la recopilación en la que se va a implementar el perfil de conexión remota, habilite esta opción para que Configuration Manager corrija el perfil de conexión remota fuera de la ventana de mantenimiento. Para obtener más información sobre las ventanas de mantenimiento, consulte [How to use maintenance windows](/sccm/core/clients/manage/collections/use-maintenance-windows) (Cómo usar las ventanas de mantenimiento).  

    -   **Generar una alerta** : habilite esta opción para configurar una alerta que se genera si la compatibilidad del perfil de conexión remota es inferior a un determinado porcentaje en una hora y fecha especificadas. También puede especificar si desea que se envíe una alerta a System Center Operations Manager.  

    -   **Especifique la programación de evaluación de compatibilidad para esta línea de base de configuración** : especifique la programación de evaluación del perfil de conexión remota implementado en dispositivos. Puede especificar una programación simple o personalizada.  

    > [!TIP]  
    >  Si un dispositivo deja una recopilación en la que se ha implementado un perfil de conexión remota, la configuración del perfil de conexión remota se deshabilita en el dispositivo. Sin embargo, para que esto se realice correctamente, debe haber implementado al menos un elemento de configuración o una línea de base de configuración que contenga un elemento de configuración del sitio.  
    >   
    >  Los dispositivos evalúan el perfil cuando el usuario inicia sesión.  
    >   
    >  Si dos perfiles de conexión remota se implementan en la misma recopilación de dispositivos y uno tiene la opción **Corregir las reglas no conformes cuando se admita** activada y el otro tiene misma opción desactivada, y los dos perfiles de conexión remota tienen distintas configuraciones de conexión, es posible que el perfil con la opción desactivada invalide la configuración del otro perfil. Este tipo de implementación de perfil de conexión remota no es compatible con Configuration Manager.  

5.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Implementar perfil de conexión remota** y crear la implementación.  

## <a name="monitor-a-remote-connection-profile"></a>Supervisar un perfil de conexión remota  

### <a name="view-compliance-results-in-the-configuration-manager-console"></a>Ver los resultados de cumplimiento en la consola de Configuration Manager  

1.  En la consola de Configuration Manager, haga clic en **Supervisión** > **Implementaciones**.  

3.  En la lista **Implementaciones** , seleccione la implementación del perfil de conexión remota para el que desea revisar la información de compatibilidad.  

4.  Puede revisar la información de resumen sobre la compatibilidad de la implementación del perfil de conexión remota en la página principal. Para ver información más detallada, seleccione la implementación del perfil de conexión remota y, a continuación, en la pestaña **Inicio** , en el grupo **Implementación** , haga clic en **Ver estado** para abrir la página **Estado de implementación** .  

     La página **Estado de implementación** contiene las siguientes pestañas:  

    -   **Compatible:** muestra el cumplimiento del perfil de conexión remota en función del número de activos afectados. Puede hacer doble clic en una regla para crear un nodo temporal en el nodo **Usuarios** , en el área de trabajo **Activos y compatibilidad** . Este nodo contiene todos los dispositivos que son compatibles con el perfil de conexión remota. El panel **Detalles del activo** muestra los dispositivos que son compatibles con el perfil. Haga doble clic en un dispositivo de la lista para mostrar información adicional.  

        > [!IMPORTANT]  
        >  Un perfil de conexión remota no se evalúa si no es aplicable en un dispositivo cliente. Sin embargo, se devuelve como compatible.  

    -   **Error:** muestra una lista de todos los errores de la implementación de perfil de conexión remota seleccionada, en función del número de activos afectados. Puede hacer doble clic en una regla para crear un nodo temporal en el nodo **Usuarios** del área de trabajo **Activos y compatibilidad** . Este nodo contiene todos los dispositivos que generaron errores con este perfil. Cuando se selecciona un dispositivo, el panel **Detalles del activo** muestra los dispositivos afectados por el problema seleccionado. Haga doble clic en un dispositivo de la lista para mostrar información adicional sobre el problema.  

    -   **No compatible:** muestra una lista de todas las reglas no conformes en el perfil de conexión remota en función del número de activos afectados. Puede hacer doble clic en una regla para crear un nodo temporal en el nodo **Usuarios** del área de trabajo **Activos y compatibilidad** . El nodo contiene todos los dispositivos que no son compatibles con este perfil. Cuando se selecciona un dispositivo, el panel **Detalles del activo** muestra los dispositivos afectados por el problema seleccionado. Haga doble clic en un dispositivo de la lista para mostrar información adicional sobre el problema.  

    -   **Desconocido:** muestra una lista de todos los dispositivos que no notificaron el cumplimiento de la implementación de perfil de conexión remota seleccionada y el estado de cliente actual de los dispositivos.  

5.  En la página **Estado de implementación** , puede revisar información detallada sobre la compatibilidad del perfil de conexión remota implementado. Se crea un nodo temporal en el nodo **Implementaciones** que le permite encontrar esta información rápidamente.  

### <a name="view-compliance-results-with-reports"></a>Ver los resultados del cumplimiento de con informes  
 Configuration Manager incluye informes integrados que se pueden usar para supervisar la información de perfiles de conexión remota. Estos informes tienen la categoría de informe de **Administración de compatibilidad y configuración**.  

> [!IMPORTANT]  
>  Debe usar un carácter comodín (%) para utilizar los parámetros **Filtro del dispositivo** y **Filtro de usuarios** en los informes de configuración de cumplimiento.  

 Para obtener más información sobre cómo configurar la generación de informes en Configuration Manager, consulte [Reporting in System Center Configuration Manager](/sccm/core/servers/manage/reporting) (Generación de informes en System Center Configuration Manager).  
