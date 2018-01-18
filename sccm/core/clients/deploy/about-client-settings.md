---
title: "Configuración de cliente"
titleSuffix: Configuration Manager
description: "Seleccione la configuración del cliente mediante la consola de administración de System Center Configuration Manager."
ms.custom: na
ms.date: 01/05/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f7560876-8084-4570-aeab-7fd44f4ba737
caps.latest.revision: "15"
caps.handback.revision: "0"
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 230d608c9ebc8126d7d8e18f7211875a2155bb7b
ms.sourcegitcommit: ac9268e31440ffe91b133c2ba8405d885248d404
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="about-client-settings-in-system-center-configuration-manager"></a>Acerca de la configuración de cliente en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Administre toda la configuración de cliente en la consola de Configuration Manager desde el nodo **Configuración de cliente** del área de trabajo **Administración**. Configuration Manager incluye una configuración predeterminada. Si cambia la configuración predeterminada del cliente, esta configuración se aplicará a todos los clientes de la jerarquía. También puede establecer una configuración de cliente personalizada, que invalida la configuración de cliente predeterminada si la asigna a las colecciones. Para obtener más información, vea [Cómo configurar el cliente](../../../core/clients/deploy/configure-client-settings.md).  
 

## <a name="background-intelligent-transfer-service"></a>Servicio de transferencia inteligente en segundo plano  

-   **Limitar el ancho de banda de red máximo para transferencias BITS en segundo plano**   </br>
   Cuando esta opción es **Sí**, los clientes usan el límite de ancho de banda de BITS. Para configurar las otras opciones de este grupo, debe habilitar esta configuración. 

-   **Hora de inicio de período de limitación**   </br>
   Especifique la hora de inicio local del período de limitación de BITS.  

-   **Hora de finalización del período de limitación**   </br>
   Especifique la hora de finalización local del período de limitación de BITS. Si coincide con la **hora de inicio del período de limitación**, la limitación de BITS siempre está habilitada.  

-   **Velocidad de transferencia máxima durante el período de limitación (Kbps)** </br>
    Especifica la velocidad de transferencia máxima que pueden usar los clientes durante el período en cuestión.  

-   **Permitir descargas de BITS fuera del período de limitación**   </br>
   Permite a los clientes usar configuraciones de BITS independientes fuera del período especificado.  

-   **Velocidad de transferencia máxima fuera del período de limitación (Kbps)**   </br>
   Especifique la velocidad de transferencia máxima que usan los clientes fuera del período de limitación de BITS.  



## <a name="client-cache-settings"></a>Configuración de la memoria caché del cliente

- **Configurar BranchCache** </br>
  Use esta opción para configurar el equipo cliente para [Windows BranchCache](/sccm/core/plan-design/configs/support-for-windows-features-and-networks#branchcache). Para permitir el almacenamiento en caché de BranchCache en el cliente, establezca **Habilitar BranchCache** en **Sí**.

    - **Habilitar BranchCache** </br>
    Habilita BranchCache en los equipos cliente.

    - **Tamaño máximo de la caché de BranchCache (porcentaje de disco)** </br>
    El porcentaje del disco que se permite usar a BranchCache. 

- **Configurar el tamaño de la caché de cliente** </br>
  En la caché del cliente de Configuration Manager en los equipos Windows se almacenan los archivos temporales que se usan para instalar aplicaciones y programas. Si esta opción se establece en **No**, el tamaño predeterminado es 5120 MB.</br>
    Elija **Sí** y, luego, especifique lo siguiente:
    - **Tamaño máximo de caché (MB)**
    - **Tamaño de caché máximo (porcentaje de disco)** </br>
    El tamaño de la caché de cliente se expande hasta el tamaño máximo en megabytes (MB) o el porcentaje del disco, *lo que sea inferior*. 

- **Habilitar el cliente de Configuration Manager en el SO completo para compartir contenido** </br>
    Habilita la [caché del mismo nivel](/sccm/core/plan-design/hierarchy/client-peer-cache) para los clientes de Configuration Manager. Seleccione **Sí** y, después, especifique la información del puerto con el que el cliente se comunica con el equipo del mismo nivel. 
    - **Puerto para difusión de red inicial** (8004 de forma predeterminada)
    - **Puerto para descarga de contenido desde sistema del mismo nivel** (8003 de forma predeterminada) </br>
    Configuration Manager configura automáticamente las reglas de Firewall de Windows para permitir este tráfico. Debe configurar los puertos manualmente si usa otro firewall.




## <a name="client-policy"></a>Directiva de cliente  

-   **Intervalo de sondeo de directiva de cliente (minutos)**  </br>
     Especifica con qué frecuencia descargan los siguientes clientes de Configuration Manager la directiva de cliente:  
      -   Equipos Windows (por ejemplo, equipos de sobremesa, servidores, equipos portátiles)  
      -   Dispositivos móviles inscritos por Configuration Manager  
      -   Equipos Mac  
      -   Equipos que ejecutan Linux o UNIX  

-   **Habilitar directiva de usuario en clientes**   </br>
   Al establecer esta opción en **Sí**y usar la [detección de usuarios](../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser), los clientes reciben las aplicaciones y programas destinados al usuario conectado.  

    El catálogo de aplicaciones recibe la lista de software disponible para los usuarios desde el servidor de sitio. Por tanto, esta configuración no tiene que ser **Sí** para que los usuarios puedan ver y solicitar aplicaciones del catálogo de aplicaciones. Pero si este valor es **No**, los comportamientos siguientes no funcionan cuando los usuarios utilicen el catálogo de aplicaciones:  

      -   Los usuarios no podrán instalar las aplicaciones que vean en el catálogo de aplicaciones.  

      -   Los usuarios no ven las notificaciones sobre las solicitudes de aprobación de aplicaciones. En lugar de ello, deberán actualizar el catálogo de aplicaciones y comprobar el estado de aprobación.  

      -   Los usuarios no reciben revisiones ni actualizaciones de las aplicaciones que se publican en el catálogo de aplicaciones. Pero sí ven los cambios de la información de las aplicaciones en el catálogo de aplicaciones.  

      -   Si quita una implementación de aplicación después de que el cliente la instale desde el catálogo de aplicaciones, los clientes seguirán viendo que la aplicación está instalada durante al menos dos días.  

    Además, cuando este valor es **No**, los usuarios no reciben las aplicaciones requeridas que implemente para ellos. Los usuarios tampoco reciben otras tareas de administración de directivas de usuario.  

    Esta configuración se aplica a los usuarios cuando sus equipos estén en la intranet y conectados a Internet. Debe ser **Sí** si también quiere habilitar directivas de usuario en Internet.  

-   **Habilitar solicitudes de directiva de usuario de clientes de Internet**   </br>
   Establezca esta opción en **Sí** para que los usuarios reciban la directiva de usuario en equipos basados en Internet. También se deben aplicar los requisitos siguientes:  

      -   El cliente y el sitio están configurados para la administración de cliente basada en Internet

      -   El valor **Habilitar directiva de usuario en clientes** es **Sí**  

      -   El punto de administración basado en Internet autentica correctamente al usuario mediante la autenticación de Windows (Kerberos o NTLM)  

       Si esta opción se establece como **No**, o no se cumple alguno de los requisitos anteriores, un equipo conectado a Internet solo recibe directivas de equipo. En este escenario, los usuarios sí podrán ver, solicitar e instalar aplicaciones desde un catálogo de aplicaciones basado en Internet. Si este valor es **No**, pero el de **Habilitar directiva de usuario en clientes** es **Sí**, los usuarios no reciben las directivas de usuario hasta que el equipo se conecte a la intranet.  

       Para obtener más información sobre cómo administrar clientes en Internet, vea [Consideraciones sobre las comunicaciones de cliente desde Internet o desde un bosque que no es de confianza](../../../core/plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan).  

      > [!NOTE]  
      >  Las solicitudes de aprobación de aplicación de los usuarios no requieren directivas de usuario ni autenticación de usuario.  


## <a name="cloud-services"></a>Cloud Services

-   **Permitir acceso al punto de distribución de nube** </br>
    Establezca esta opción en **Sí** para que los clientes obtengan contenido desde un punto de distribución de nube. Esta configuración no requiere que el dispositivo esté basado en Internet.

-    **Registrar automáticamente los nuevos dispositivos de Windows 10 unidos a un dominio con Azure Active Directory** </br> Al configurar Azure Active Directory para admitir la combinación híbrida, Configuration Manager configura los dispositivos Windows 10 para esta funcionalidad. Para obtener más información, vea [Configuración de dispositivos híbridos unidos a Azure Active Directory](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup).

-   **Permite que los clientes usen una puerta de enlace de administración en la nube** </br>
    De forma predeterminada, todos los clientes de itinerancia de Internet usan cualquier instancia de [Cloud Management Gateway](/sccm/core/clients/manage/plan-cloud-management-gateway) disponible. Un ejemplo de cuándo se debe establecer esta opción en **No** es para el uso de ámbito del servicio, por ejemplo durante un proyecto piloto o para ahorrar costos.



##  <a name="compliance-settings"></a>Configuración de cumplimiento  

-   **Habilitar evaluación de compatibilidad en clientes** </br>
    Establezca esta opción en **Sí** para configurar las otras opciones de este grupo.
 
-   **Programar evaluación de compatibilidad**   </br>
     Haga clic en **Programación** para crear la programación predeterminada para las implementaciones de línea base de configuración. Este valor se puede configurar para cada línea de base en el cuadro de diálogo **Implementar línea de base de configuración**.  

-   **Habilitar perfiles y datos de usuario**   </br>
     Seleccione **Sí** si quiere implementar elementos de configuración de [perfiles y datos de usuario](../../../compliance/deploy-use/create-user-data-and-profiles-configuration-items.md).



## <a name="computer-agent"></a>Agente de equipo  
-   Notificaciones de usuario para las implementaciones requeridas </br>
    Para obtener más información sobre las siguientes tres configuraciones, vea [Notificaciones de usuario para las implementaciones requeridas](/sccm/apps/deploy-use/deploy-applications#user-notifications-for-required-deployments):
    -    **La fecha límite de la implementación es de más de 24 horas. Recordar al usuario cada (horas)**
    -   **La fecha límite de la implementación es antes de 24 horas. Recordar al usuario cada (horas)**  </br>
    -   **La fecha límite de la implementación es antes de 1 hora. Recordar al usuario cada (minutos)**  </br>

-   **Punto de sitios web del catálogo de aplicaciones predeterminado**   </br>
     Configuration Manager utiliza este valor para conectar a los usuarios al catálogo de aplicaciones desde el Centro de software. Haga clic en **Sitio web** para especificar un servidor que hospede el punto de sitios web del catálogo de aplicaciones. Escriba su nombre NetBIOS o FQDN, especifique la detección automática o una dirección URL para implementaciones personalizadas. En la mayoría de los casos, la detección automática es la mejor opción, ya que ofrece las siguientes ventajas:  

    -   Si el sitio tiene un punto de sitios web del catálogo de aplicaciones, los clientes reciben automáticamente un punto de sitios web del catálogo de aplicaciones desde su sitio.  

    -   El cliente prefiere puntos de sitios web del catálogo de aplicaciones habilitados para HTTPS en la intranet a servidores solo de HTTP. Esta funcionalidad ayuda a protegerse contra un servidor no autorizado.

    -   El punto de administración ofrece a los clientes basados en Internet un punto de sitios web del catálogo de aplicaciones basado en Internet. El punto de administración proporciona a los clientes basados en intranet un punto de sitios web del catálogo de aplicaciones basado en intranet.  

     La detección automática no garantiza que los clientes reciban el punto de sitios web del catálogo de aplicaciones más cercano. Puede decidir no utilizar **Detectar automáticamente** por las razones siguientes:  

     -   Desea configurar manualmente el servidor más cercano para los clientes o asegurarse de que no se conectan a un servidor a través de una conexión de red lenta.  

     -   Desea controlar qué clientes se conectan a qué servidor. Esta configuración podría darse por motivos de pruebas, rendimiento o empresariales.  

     -   No quiere esperar hasta 25 horas o hasta un cambio de la red para que los clientes usen un punto de sitios web del catálogo de aplicaciones diferente.  

     Si especifica el punto de sitios web del catálogo de aplicaciones en lugar de usar la detección automática, especifique el nombre NetBIOS en lugar del FQDN de intranet. Esta configuración reduce la probabilidad de que el explorador web solicite las credenciales a los usuarios cuando accedan a un catálogo de aplicaciones basado en intranet. Para utilizar el nombre de NetBIOS, se deben cumplir las siguientes condiciones:  

     -   Se especificó el nombre de NetBIOS en las propiedades del punto de sitios web del catálogo de aplicaciones.  

     -   Usa WINS o todos los clientes están en el mismo dominio que el punto de sitios web del catálogo de aplicaciones.  

     -   El punto de sitios web del catálogo de aplicaciones se configura para conexiones de cliente HTTP o el servidor se configura para HTTPS, y el certificado del servidor web tiene el nombre NetBIOS.  

     Normalmente, se les piden las credenciales a los usuarios si la dirección URL tiene un nombre de dominio completo, pero no si la dirección URL es un nombre NetBIOS. Espere que siempre se les solicite a los usuarios cuando se conectan desde Internet, ya que esta conexión debe utilizar el nombre completo de Internet. Cuando se usa un cliente basado en Internet y el explorador web solicita las credenciales a los usuarios, asegúrese de que el punto de sitios web del catálogo de aplicaciones se puede conectar a un controlador de dominio para la cuenta del usuario. Esta configuración permite al usuario autenticarse mediante Kerberos.  

    > [!NOTE]  
    >  Funcionamiento de la detección automática:  
    >   
    >  el cliente realiza una solicitud de ubicación de servicio a un punto de administración. Si hay un punto de sitios web del catálogo de aplicaciones en el mismo sitio que el cliente, se proporcionará este servidor al cliente como el servidor del catálogo de aplicaciones que debe utilizar. Si hay más de un punto de sitios web del catálogo de aplicaciones disponible en el sitio, los servidores habilitados para HTTPS prevalecerán sobre los que no están habilitados para HTTPS. Después de este filtrado, se proporcionará a todos los clientes uno de los servidores para que los usen como catálogo de aplicaciones; Configuration Manager no lleva a cabo un equilibrio de carga entre varios servidores. Si el sitio del cliente no tiene ningún punto de sitios web del catálogo de aplicaciones, el punto de administración devolverá de forma no determinista uno de la jerarquía.  
    >   
    >  Para los clientes basados en intranet, si configura el punto de sitios web del catálogo de aplicaciones con un nombre de NetBIOS para la dirección URL del catálogo de aplicaciones, el punto de administración ofrece a los clientes este nombre de NetBIOS en lugar del FQDN de intranet. Para los clientes basados en Internet, el punto de administración solo ofrece al cliente el FQDN de Internet.  
    >   
    >  El cliente realiza dicha solicitud de ubicación de servicio cada 25 horas, o cada vez que detecte un cambio de la red. Por ejemplo, si el cliente pasa de la intranet a Internet y localiza un punto de administración basado en Internet, este punto proporciona a los clientes servidores del punto de sitios web del catálogo de aplicaciones basado en Internet.  

-   **Agregar sitio web predeterminado del catálogo de aplicaciones a una zona de sitios de confianza de Internet Explorer**   </br>
     Si esta opción es **Sí**, el cliente agrega de forma automática la dirección URL del sitio web del catálogo de aplicaciones predeterminado actual a la zona de sitios de confianza de Internet Explorer.  

     Este valor asegura que no está habilitada la configuración de Internet Explorer para el modo protegido. Si el modo protegido está habilitado, es posible que el cliente de Configuration Manager no pueda instalar aplicaciones desde el catálogo de aplicaciones. De forma predeterminada, la zona de sitios de confianza también admite el inicio de sesión de usuario para el catálogo de aplicaciones, lo que requiere la autenticación de Windows.  

     Si esta opción se mantiene como **No**, es posible que los clientes de Configuration Manager no puedan instalar aplicaciones desde el catálogo de aplicaciones. Un método alternativo consiste en configurar estas opciones de Internet Explorer en otra zona para la dirección URL del catálogo de aplicaciones que usan los clientes.  

    > [!NOTE]  
    >  Cada vez que Configuration Manager agrega un catálogo de aplicaciones predeterminado a la zona de sitios de confianza, quita cualquier dirección URL del catálogo de aplicaciones agregada anteriormente.  
    >   
    >  Si la dirección URL ya está especificada en una de las zonas de seguridad, Configuration Manager no puede agregarla. En este escenario, deberá quitar la dirección URL de la otra zona, o bien realizar manualmente la configuración requerida de Internet Explorer.  

-   **Permitir que las aplicaciones de Silverlight se ejecuten en modo de confianza elevado.**   </br>
     Este valor debe ser **Sí** para que los usuarios utilicen el catálogo de aplicaciones.  

     Si cambia esta configuración, entrará en vigor cuando los usuarios carguen sus exploradores o actualicen las ventanas del explorador que tengan abiertas.  

     Para obtener más información sobre esta configuración, vea [Certificados de Microsoft Silverlight 5 y modo de confianza elevado necesarios para el catálogo de aplicaciones](../../../apps/plan-design/security-and-privacy-for-application-management.md#BKMK_CertificatesSilverlight5).  

-   **Nombre de organización mostrado en el Centro de software**   </br>
     Escriba el nombre que ven los usuarios en el Centro de software. Esta información de marca ayuda a los usuarios a identificar a esta aplicación como un origen de confianza.  

-   **Usar el nuevo Centro de software**   </br>
     Si establece esta configuración de cliente en **Sí**, todos los equipos cliente usan el nuevo Centro de software. En el Centro de software se muestran aplicaciones disponibles para el usuario a las que antes solo se podía tener acceso desde el catálogo de aplicaciones. El catálogo de aplicaciones requiere Silverlight, que no es un requisito previo para el nuevo Centro de software.   

     Los roles de sistema de sitio de punto de sitios web del catálogo de aplicaciones y de punto de servicio web del catálogo de aplicaciones siguen siendo necesarios para que las aplicaciones disponibles para el usuario aparezcan en el Centro de software.  

     Para obtener más información, consulte [Planear y configurar la administración de aplicaciones en Configuration Manager](../../../apps/plan-design/plan-for-and-configure-application-management.md).  

-   **Habilite la comunicación con el servicio de atestación de estado**  </br>
    Establezca esta opción en **Sí** para que los dispositivos Windows 10 usen la [atestación de estado](/sccm/core/servers/manage/health-attestation). Al habilitar esta opción, la siguiente también está disponible para la configuración.

    -   **Usar el servicio de atestación de estado local** </br>
        Establezca esta opción en **Sí** para que los dispositivos usen un servicio local. Establezca esta opción en **No** para que los dispositivos usen el servicio basado en la nube de Microsoft.  

-   **Permisos de instalación**   </br>
    > [!WARNING]  
    >  Esta configuración se aplica al catálogo de aplicaciones y al Centro de software. No tiene efecto cuando los usuarios utilizan el Portal de empresa.  

     Configure cómo pueden iniciar los usuarios la instalación de software, las actualizaciones de software y las secuencias de tareas:  

    -   **Todos los usuarios**: los usuarios con cualquier permiso excepto Invitado  

    -   **Solo los administradores**: los usuarios deben ser miembro del grupo Administradores local  

    -   **Solo administradores y usuarios primarios**: los usuarios deben ser miembro del grupo Administradores local o usuarios primarios del equipo  

    -   **Ningún usuario**: ningún usuario que inició sesión en un equipo cliente podrá iniciar la instalación de software, las actualizaciones de software y las secuencias de tareas. Las implementaciones necesarias para el equipo siempre se instalan en la fecha límite. Los usuarios no pueden iniciar la instalación de software desde el catálogo de aplicaciones o el Centro de software.  

-   **Suspender indicación de PIN de BitLocker en el reinicio**  </br>
     Si los equipos requieren la indicación de PIN de BitLocker, esta opción omite el requisito de escribir un PIN cuando se reinicia el equipo después de una instalación de software.  

    -   **Siempre**: Configuration Manager suspenderá temporalmente BitLocker después de que haya instalado software que requiere un reinicio y haya comenzado a reiniciar el equipo. Esta configuración solo se aplica a un reinicio del equipo iniciado por Configuration Manager. Esta configuración no suspende el requisito de escribir el PIN de BitLocker cuando el usuario reinicia el equipo. El requisito de indicación de PIN de BitLocker se reanuda tras el inicio de Windows.

    -   **Nunca**: Configuration Manager no suspende BitLocker en el siguiente inicio del equipo después de que haya instalado software que requiera un reinicio. En esta situación, la instalación del software no puede finalizar hasta que el usuario escriba el PIN para completar el proceso de inicio estándar y cargue Windows.

-   **Un software adicional administra la implementación de aplicaciones y actualizaciones de software**  </br>
     Habilite esta opción solo si se cumple alguna de las siguientes condiciones:  

    -   Utiliza una solución de proveedor que requiere que esta opción esté habilitada.  

    -   Utilice el kit de desarrollo de software (SDK) de Configuration Manager para administrar las notificaciones de agente de cliente y la instalación de aplicaciones y actualizaciones de software.  

    > [!WARNING]  
    >  Si selecciona esta opción y no se cumple ninguna de estas condiciones, el cliente no instala las actualizaciones de software y las aplicaciones necesarias. Esta configuración no impide que los usuarios instalen aplicaciones desde el catálogo de aplicaciones, ni que se instalen paquetes, programas y secuencias de tareas.  

-   **Directiva de ejecución de PowerShell**  </br>
     Configure cómo pueden ejecutar los clientes de Configuration Manager scripts de Windows PowerShell. Estos scripts se suelen usar para la detección de elementos de configuración para la configuración de compatibilidad. También pueden enviarse en una implementación como script estándar.  

    -   **Desviar**: el cliente de Configuration Manager desvía la configuración de Windows PowerShell en el equipo cliente para que puedan ejecutarse los scripts sin firmar.  

    -   **Restringido**: el cliente de Configuration Manager usa la configuración actual de Windows PowerShell en el equipo cliente. Esta configuración determina si se pueden ejecutar scripts sin firmar.  

    -   **Todos firmados**: el cliente de Configuration Manager ejecuta scripts solo si los ha firmado un editor de confianza. Esta restricción se aplica independientemente de la configuración actual de Windows PowerShell del equipo cliente.  

     Esta opción requiere al menos la versión 2.0 de Windows PowerShell. El valor predeterminado es **Todos firmados**.  

    > [!TIP]  
    >  Si no se ejecutan los scripts sin firmar debido a esta configuración de cliente, Configuration Manager informará de este error de las siguientes maneras:  
    >   
    > -   En el área de trabajo **Supervisión** de la consola se muestra el identificador de error **0x87D00327** del estado de implementación y la descripción **El script no se firmó**  
    > -   Los informes muestran el tipo de error **Error de detección** y, después, el código de error **0x87D00327** y la descripción **El script no se firmó**, o bien el código de error **0x87D00320** y la descripción **Aún no se ha instalado el host de script**. Un informe de ejemplo es **Detalles de errores de elementos de configuración en una línea de base de configuración para un activo**.  
    > -   El archivo **DcmWmiProvider.log** muestra el mensaje **El script no se firmó (Error: 87D00327; Origen: CCM)**.  

-   **Mostrar notificaciones para nuevas implementaciones**  </br>
     Elija **Sí** para mostrar una notificación para las implementaciones disponibles durante menos de una semana.  Este mensaje se muestra cada vez que se inicie el agente cliente.

-   **Deshabilitar selección aleatoria de fecha límite**  </br>
     Después de la fecha límite de la implementación, esta configuración determina si el cliente usa un retardo de activación de hasta dos horas para instalar las actualizaciones de software necesarias. De forma predeterminada, el retardo de activación está deshabilitado.  

     Para escenarios de infraestructura de escritorio virtual (VDI), este retardo ayuda a distribuir el procesamiento de la CPU y la transferencia de datos para un equipo host con varias máquinas virtuales. Aunque no use VDI, que muchos clientes instalen las mismas actualizaciones al mismo tiempo puede incrementar negativamente el uso de la CPU en el servidor de sitio. Este comportamiento también puede ralentizar los puntos de distribución y reducir considerablemente el ancho de banda de red disponible.  

     Si los clientes tienen que instalar las actualizaciones de software en la fecha límite de la implementación sin demora, establezca esta opción en **Sí**. 

-   **Período de gracia para el cumplimiento tras la fecha límite de la implementación (horas)** </br>
     Si quiere proporcionar a los usuarios más tiempo para instalar las implementaciones de actualización de aplicación o software requeridas después de la fecha límite, establezca esta opción en **Sí**. Este período de gracia es para un equipo desactivado durante un período prolongado y el usuario tiene que instalar muchas implementaciones de aplicación o actualización. Por ejemplo, si un usuario vuelve de vacaciones y tiene que esperar mucho tiempo mientras el cliente instala las implementaciones de aplicación atrasadas. 

     Establezca un período de gracia de entre una y 120 horas. Use esta configuración junto con la propiedad de implementación **Retrasar el cumplimiento de esta implementación de acuerdo con las preferencias del usuario**. Para obtener más información, consulte [Deploy applications](/sccm/apps/deploy-use/deploy-applications) (Implementar aplicaciones).



##  <a name="computer-restart"></a>Reinicio de equipo  
 Las opciones siguientes deben tener menos duración que la ventana de mantenimiento más corta que se aplique en el equipo.  

 Para obtener más información sobre las ventanas de mantenimiento, consulte [Cómo usar ventanas de mantenimiento en System Center Configuration Manager](../../../core/clients/manage/collections/use-maintenance-windows.md).  

-   **Mostrar una notificación temporal al usuario que indique el intervalo antes de que el usuario se desconecte o el equipo se inicie (minutos)**
-   **Mostrar un cuadro de diálogo que el usuario no pueda cerrar, que muestre el intervalo de recuento antes de que el usuario se desconecte o el equipo se reinicie (minutos)**



##  <a name="endpoint-protection"></a>Endpoint Protection  
>  [!Tip]   
> Además de la información siguiente, puede encontrar detalles adicionales sobre el uso de las opciones del cliente de Endpoint Protection en [Escenario de ejemplo: uso de System Center Endpoint Protection para proteger los equipos frente al malware en System Center Configuration Manager](/sccm/protect/deploy-use/scenarios-endpoint-protection).

-   **Administrar el cliente de Endpoint Protection en equipos cliente**  </br>
     Seleccione **Sí** si quiere administrar los clientes existentes de Endpoint Protection y Windows Defender en los equipos de la jerarquía.  

     Seleccione esta opción si ya ha instalado el cliente de Endpoint Protection y quiere administrarlo con Configuration Manager.  En esta instalación independiente se incluye un proceso incluido en script en el que se usa una aplicación o un paquete de Configuration Manager y un programa.

-   **Instalar cliente de Endpoint Protection en equipos cliente**   </br>
     Seleccione **Sí** para instalar y habilitar el cliente de Endpoint Protection en los equipos cliente en los que todavía no se ejecute.  

    > [!NOTE]  
    >  Si el cliente de Endpoint Protection ya está instalado y se selecciona **No**, el cliente de Endpoint Protection no se desinstala. Para desinstalar el cliente de Endpoint Protection, establezca la configuración de cliente **Administrar el cliente de Endpoint Protection en equipos cliente** en **No**. Después, implemente un paquete y un programa para desinstalar el cliente de Endpoint Protection.  

-   **Quitar automáticamente el software antimalware instalado anteriormente antes de instalar Endpoint Protection** </br>
    Establezca esta opción en **Sí** para que el cliente de Endpoint Protection intente desinstalar otras aplicaciones antimalware. Varios clientes de antimalware en el mismo dispositivo pueden entrar en conflicto y afectar al rendimiento del sistema.

-   **Permitir la instalación y los reinicios del cliente de Endpoint Protection fuera de las ventanas de mantenimiento. Las ventanas de mantenimiento deben conceder, como mínimo, 30 minutos para la instalación del cliente** </br>
    Establezca esta opción en **Sí** para invalidar los comportamientos de instalación típica con las ventanas de mantenimiento. Esta opción cumple los requisitos empresariales para la prioridad del mantenimiento del sistema por motivos de seguridad. 

-   **Para dispositivos de Windows Embedded con filtros de escritura, confirmar la instalación del cliente de Endpoint Protection (reinicios necesarios)**  </br>
     Seleccione **Sí** para deshabilitar el filtro de escritura en el dispositivo Windows Embedded y reiniciar el dispositivo. Esta acción confirma la instalación en el dispositivo.  

     Si establece opción en **No**, el cliente se instala en una superposición temporal que se borra cuando se reinicia el dispositivo. En este escenario, el cliente de Endpoint Protection no se instala de forma completa hasta que otra instalación confirma los cambios en el dispositivo. Esta configuración es la predeterminada.  

-   **Suprimir cualquier reinicio de equipo obligatorio después de instalar el cliente de Endpoint Protection**  </br>
     Elija **Sí** para suprimir un reinicio del equipo si es necesario después de instalar el cliente de Endpoint Protection.  

    > [!IMPORTANT]  
    >  Si el cliente de Endpoint Protection requiere un reinicio del equipo y esta configuración es **No**, el equipo se reinicia, independientemente de las ventanas de mantenimiento configuradas.  

-   **Período de tiempo permitido que los usuarios pueden posponer un reinicio obligatorio para llevar a cabo la instalación de Endpoint Protection (horas)**  </br>
     Si es necesario reiniciar una vez instalado el cliente de Endpoint Protection, esta configuración especifica el número de horas que los usuarios pueden posponer el reinicio obligatorio. Esta configuración requiere que la opción **Suprimir cualquier reinicio de equipo obligatorio después de instalar el cliente de Endpoint Protection** sea **No**.  

-   **Deshabilitar orígenes alternativos (como Microsoft Windows Update, Microsoft Windows Server Update Services o recursos compartidos de UNC) para la actualización de definición inicial en los equipos cliente**  </br>
     Seleccione **Sí** si quiere que Configuration Manager solo instale la actualización de definición inicial en los equipos cliente. Esta configuración puede ser útil para evitar conexiones de red innecesarias y reducir el ancho de banda de red durante la instalación inicial de la actualización de definiciones.  



##  <a name="enrollment"></a>Inscripción

-   **Intervalo de sondeo para clientes heredados de dispositivos móviles** </br>
    Haga clic en **Establecer intervalo** para especificar el período de tiempo (en horas o minutos) que los dispositivos móviles heredados sondean la directiva. Estos dispositivos incluyen plataformas como Windows CE, Mac OS X y Unix o Linux.

-   **Intervalo de sondeo para dispositivos modernos (minutos)** </br>
    Escriba el número de minutos que los dispositivos modernos sondean la directiva. Esta configuración es para dispositivos Windows 10 administrados a través de la administración local de dispositivos móviles.

-   **Permitir a los usuarios inscribir dispositivos móviles y equipos Mac** </br>
    Para habilitar la inscripción basada en usuario de dispositivos heredados, establezca esta opción en **Sí** y, después, establezca la configuración siguiente:

    -   **Perfil de inscripción** </br>
        Haga clic en **Establecer perfil** para crear o seleccionar un perfil de inscripción. Para obtener más información, vea [Configurar las opciones del cliente para la inscripción](/sccm/core/clients/deploy/deploy-clients-to-macs#configure-client-settings-for-enrollment).

-   **Permitir a los usuarios inscribir dispositivos modernos** </br>
    Para habilitar la inscripción basada en usuario de dispositivos modernos, establezca esta opción en **Sí** y, después, establezca la configuración siguiente:

    -   **Perfil de inscripción de dispositivo moderno** </br>
        Haga clic en **Establecer perfil** para crear o seleccionar un perfil de inscripción. Para obtener más información, vea [Crear un perfil de inscripción que permita a los usuarios inscribir dispositivos modernos](/sccm/mdm/get-started/set-up-device-enrollment-on-premises-mdm#bkmk_createProf).



##  <a name="hardware-inventory"></a>Inventario de hardware  

-   **Habilitar inventario de hardware en clientes** </br>
    De forma predeterminada, esta opción está establecida en **Sí**. Para obtener más información, vea [Introducción al inventario de hardware](/sccm/core/clients/manage/inventory/introduction-to-hardware-inventory).

-   **Programación de inventario de hardware** </br>
    Haga clic en **Programación** para ajustar la frecuencia con la que los clientes ejecutan el ciclo de inventario de hardware. De forma predeterminada, este ciclo tiene lugar cada siete días.

-   **Retraso aleatorio máximo (minutos)** </br>
    Especifique el número máximo de minutos para que el cliente de Configuration Manager seleccione de forma aleatoria el ciclo de inventario de hardware de la programación definida. Esta selección aleatoria entre todos los clientes ayuda a procesar el inventario de equilibrio de carga en el servidor de sitio. Puede especificar un valor de 0 a 480 minutos. De forma predeterminada, este valor se establece en 240 minutos (cuatro horas).

-   **Tamaño de archivo MIF personalizado máximo (KB)**  </br>
     Especifique el tamaño máximo, en kilobytes (KB), que se permite para cada archivo MIF personalizado que el cliente recopila durante un ciclo de inventario de hardware. El agente de inventario de hardware de Configuration Manager no procesa los archivos MIF personalizados que superan este tamaño. Puede especificar un tamaño de entre 1 y 5 120 KB. De forma predeterminada, este valor está establecido en 250 KB. Esta configuración no afecta al tamaño del archivo de datos de inventario de hardware normal.  

    > [!NOTE]  
    >  Este valor solo está disponible en la configuración predeterminada del cliente.  

-   **Clases de inventario de hardware**  </br>
     Haga clic en **Establecer clases** para ampliar la información de hardware que se recopila de los clientes sin necesidad de modificar manualmente el archivo sms_def.mof. Para obtener más información, vea [Cómo configurar el inventario de hardware](../../../core/clients/manage/inventory/configure-hardware-inventory.md).  

-   **Recopilar archivos MIF**  </br>
     Use esta opción para especificar si quiere recopilar archivos MIF de los clientes de Configuration Manager durante el inventario de hardware.  

     Para que un archivo MIF sea recopilado por el inventario de hardware, debe estar en la ubicación correcta del equipo cliente. De forma predeterminada, los archivos se encuentran en las rutas de acceso siguientes:  

    -   Los **archivos IDMIF** deben estar en la carpeta Windows\System32\CCM\Inventory\Idmif 

    -   Los **archivos NOIDMIF** deben estar en la carpeta Windows\System32\CCM\Inventory\Noidmif

    > [!NOTE]  
    >  Este valor solo está disponible en la configuración predeterminada del cliente.

   

##  <a name="metered-internet-connections"></a>Conexiones a Internet de uso medido  
 Administre la forma en que los equipos con Windows 8 y versiones posteriores usan las conexiones a Internet de uso medido para comunicarse con Configuration Manager. En ocasiones, los proveedores de acceso a Internet cobran según la cantidad de datos que envía y recibe cuando se utiliza una conexión a Internet de uso medido.  

> [!NOTE]  
>  La configuración de cliente establecida no se aplica en los escenarios siguientes:  
>   
> -   El equipo está en una conexión de datos de itinerancia: el cliente de Configuration Manager no lleva a cabo ninguna tarea que requiera la transferencia de datos a sitios de Configuration Manager.  
> -   Las propiedades de conexión de red de Windows se configuran como de uso no medido: el cliente de Configuration Manager se comporta como si la conexión fuera de uso no medido y, de este modo, transfiere datos al sitio.  

-   **Comunicación de clientes en conexiones a Internet de uso medido**  </br>
     Elija una de las opciones siguientes para esta configuración:  

    -   **Permitir**: se permiten todas las comunicaciones del cliente a través de la conexión a Internet de uso medido a menos que el dispositivo cliente utilice una conexión de datos en movilidad.  

    -   **Limitar**: solo se permiten las siguientes comunicaciones de cliente a través de la conexión a Internet de uso medido:  

        -   Recuperación de la directiva de cliente  

        -   Mensajes de estado del cliente para enviar al sitio  

        -   Solicitudes de instalación de software mediante el catálogo de aplicaciones  

        -   Implementaciones requeridas (una vez alcanzada la fecha límite de instalación)  

        > [!IMPORTANT]  
        >  El cliente siempre permite las instalaciones de software desde el Centro de software o el catálogo de aplicaciones, independientemente de la configuración de la conexión de Internet de uso medido.  

         Si se alcanza el límite de transferencia de datos para la conexión a Internet de uso medido, el cliente ya no intentará comunicarse con los sitios de Configuration Manager.  

    -   **Bloquear**: el cliente de Configuration Manager no intenta comunicarse con los sitios de Configuration Manager si se encuentra en una conexión a Internet de uso medido. Esta opción es el valor predeterminado.  



##  <a name="power-management"></a>Administración de energía  

-   **Permitir la administración de energía de dispositivos** </br>
    Establezca esta opción en **Sí** para habilitar la administración de energía en los clientes. Para obtener más información, consulte [Introduction to power management](/sccm/core/clients/manage/power/introduction-to-power-management) (Introducción a la administración de energía).

-   **Permitir a los usuarios excluir su dispositivo de la administración de energía**  </br>
     En la lista desplegable, seleccione **Sí** para permitir que los usuarios del Centro de software excluyan sus equipos de cualquier configuración de administración de energía establecida.  

-   **Habilitar proxy de reactivación** </br> 
     Especifique **Sí** para complementar la configuración de Wake on LAN del sitio cuando se configure para paquetes de unidifusión.  

     Para obtener más información sobre el proxy de reactivación, consulte [Planear la reactivación de clientes en System Center Configuration Manager](../../../core/clients/deploy/plan/plan-wake-up-clients.md).  

    > [!WARNING]  
    >  No habilite el proxy de reactivación en una red de producción sin entender primero cómo funciona y evaluarlo en un entorno de prueba.  

    Después, configure las siguientes opciones adicionales según sea necesario:

    -   **Número de puerto de proxy de reactivación (UDP)**  </br>
         El número de puerto que los clientes usan para enviar paquetes de reactivación a equipos en suspensión. Mantenga el puerto predeterminado 25536, o bien cambie el número por un valor de su elección.  

    -   **Número de puerto de Wake On LAN (UDP)** </br> 
         Mantenga el valor predeterminado de 9, a menos que haya cambiado el número de puerto de Wake on LAN (UDP) en la pestaña **Puertos** en las **Propiedades** del sitio.  

        > [!IMPORTANT]  
        >  Este número debe coincidir con el número en las **Propiedades**del sitio. Si cambia este número en un lugar, este no se actualizará automáticamente en el otro lugar.  

    -   **Excepción del Firewall de Windows Defender para el proxy de reactivación** </br>
         El cliente de Configuration Manager configura automáticamente el número de puerto del proxy de reactivación en los dispositivos que ejecutan Firewall de Windows Defender. Haga clic en **Configurar** para especificar los perfiles de firewall deseados.

        Si los clientes ejecutan otro firewall, debe configurarlo manualmente para permitir el **número de puerto de proxy de reactivación (UDP)**.  
        
    -   **Prefijos de IPv6 si son necesarios para DirectAccess u otros dispositivos de red que intervengan. Use una coma para especificar varias entradas** </br>
        Escriba los prefijos de IPv6 necesarios para que el proxy de reactivación funcione en la red.



##  <a name="remote-tools"></a>Herramientas remotas  

-   **Habilitar control remoto en clientes** y **Perfiles de excepción de firewall**  </br>
     Haga clic en **Configurar** para habilitar la característica de control remoto de Configuration Manager. Opcionalmente, configure las opciones del firewall para permitir que el control remoto trabaje en los equipos cliente.  

     El control remoto está deshabilitado de forma predeterminada.  

    > [!IMPORTANT]  
    >  Si no se configuran las opciones del firewall, el control remoto podría no funcionar correctamente.  

-   **Los usuarios pueden cambiar la directiva o la configuración de notificaciones en el Centro de software**  </br>
     Seleccione si los usuarios pueden cambiar opciones del control remoto desde el Centro de software.  

-   **Permitir el control remoto de un equipo desatendido**  </br>
     Seleccione si un administrador puede usar el control remoto para tener acceso a un equipo cliente que ha cerrado la sesión o está bloqueado. Solo se puede usar el control remoto en un equipo que ha iniciado sesión y está desbloqueado cuando esta opción está deshabilitada.  

-   **Solicitar al usuario permiso de control remoto**  </br>
     Seleccione si el equipo cliente muestra un mensaje solicitando el permiso del usuario antes de permitir una sesión de control remoto.  

-   **Solicitar permiso al usuario para transferir contenido del Portapapeles compartido** </br>
    Permita a los usuarios que acepten o rechacen las transferencias de archivos antes de transferir el contenido desde el portapapeles compartido en una sesión de control remoto. Los usuarios solo necesitan conceder permisos una vez por sesión, y el espectador no puede concederse permiso a sí mismo para continuar con la transferencia de archivos.

-   **Conceder permiso de control remoto al grupo de administradores locales**  </br>
     Seleccione si los administradores locales del servidor que inicia la conexión de control remoto pueden establecer sesiones de control remoto en los equipos cliente.  

-   **Nivel de acceso permitido**  </br>
     Especifique el nivel de acceso de control remoto que se permite. Elija una de las opciones siguientes:  
    - **Sin acceso**
    - **Solo vista**
    - **Control total**  

-   **Visores permitidos de control remoto y asistencia remota**  </br>
     Haga clic en **Establecer visores** para especificar los nombres de los usuarios de Windows que pueden establecer sesiones de control remoto en los equipos cliente.  

-   **Mostrar icono de notificación de sesión en la barra de tareas**  </br>
     Establezca esta opción en **Sí** para mostrar un icono en la barra de tareas de Windows del cliente para indicar una sesión de control remoto activa.  

-   **Mostrar barra de conexión a la sesión**  </br>
     Establezca esta opción en **Sí** para mostrar una barra de conexión a la sesión de alta visibilidad en los clientes para indicar que hay una sesión de control remoto activa.  

-   **Reproducir un sonido en el cliente**  </br>
     Configure esta opción para usar un sonido a fin de indicar si una sesión de control remoto está activa en un equipo cliente. Seleccione una de las siguientes opciones:
    - **Sin sonido**
    - **Inicio y final de la sesión** (valor predeterminado)
    - **Varias veces durante la sesión**  

-   **Administrar configuración de asistencia remota no solicitada**  </br>
     Establezca esta opción en **Sí** para permitir que Configuration Manager administre sesiones de asistencia remota no solicitadas.  

     En una sesión de asistencia remota no solicitada, el usuario del equipo cliente no solicitó ayuda para iniciar la sesión.  

-   **Administrar configuración de asistencia remota solicitada**  </br>
     Establezca esta opción en **Sí** para permitir que Configuration Manager administre sesiones de asistencia remota solicitadas.  

     En una sesión de asistencia remota solicitada, el usuario del equipo cliente envió una solicitud de asistencia remota al administrador.  

-   **Nivel de acceso de asistencia remota**  </br>
     Seleccione el nivel de acceso que se va a asignar a las sesiones de asistencia remota que se inician en la consola de Configuration Manager.  Seleccione una de las siguientes opciones:
    - **Ninguna** (valor predeterminado)
    - **Visualización remota**
    - **Control total**

    > [!NOTE]  
    >  El usuario en el equipo cliente siempre debe conceder permiso para que se produzca una sesión de asistencia remota.  

-   **Administrar configuración de Escritorio remoto**  </br>
     Establezca esta opción en **Sí** para permitir que Configuration Manager administre sesiones de Escritorio remoto en los equipos.  

-   **Permitir a los usuarios permitidos conectarse mediante la conexión a Escritorio remoto**  </br>
     Establezca esta opción en **Sí** para agregar los usuarios especificados en la lista de visores permitidos al grupo de usuarios locales de Escritorio remoto en los clientes.  

-   **Requerir autenticación de nivel de red en equipos que ejecutan el sistema operativo Windows Vista y versiones posteriores**  </br>
     Establezca esta opción en **Sí** para usar autenticación a nivel de red (NLA) para establecer conexiones de Escritorio remoto con los equipos cliente. La autenticación a nivel de red requiere menos recursos del equipo remoto al principio dado que finaliza la autenticación del usuario antes de establecer una conexión de Escritorio remoto. El uso de NLA es una configuración más segura. NLA ayuda a proteger al equipo frente a software o usuarios malintencionados, y reduce el riesgo de ataques por denegación de servicio.  



## <a name="software-center"></a>Centro de software

-   **Seleccionar la configuración nueva para especificar la información de la compañía** </br>
    Establezca esta opción en **Sí** y, después, especifique las opciones siguientes para personalizar el Centro de software para su organización:

    - **Nombre de la empresa** </br>
        Escriba el nombre de la organización que ven los usuarios en el Centro de software.
    - **Combinación de colores del Centro de software** </br>
        Haga clic en **Seleccionar color** para definir el color principal usado por el Centro de software.
    - **Seleccionar un logotipo para el Centro de software** </br>
        Haga clic en **Examinar** para seleccionar una imagen para mostrar en el Centro de software. El logotipo debe ser un archivo JPEG, PNG o BMP de 400 x 100 píxeles, con un tamaño máximo de 750 KB. El nombre de archivo del logotipo no debe contener espacios. <!--SMS.503731 space in filename, noticed BMP missing as filetype-->

-   Visibilidad de las pestañas del Centro de software </br>
    Establezca las opciones adicionales de este grupo en **Sí** para que las pestañas siguientes sean visibles en el Centro de software:
    - **Aplicaciones**
    - **Actualizaciones**
    - **Sistemas operativos**
    - **Estado de la instalación**
    - **Cumplimiento de dispositivos**
    - **Opciones**

    Por ejemplo, si la organización no usa las directivas de cumplimiento y quiere ocultar la pestaña Cumplimiento del dispositivo en el Centro de software, establezca la opción **Habilitar pestaña Cumplimiento del dispositivo** en **No**.



## <a name="software-deployment"></a>Implementación de software  

-   **Programar la reevaluación para implementaciones**  </br>
     Configure una programación para cuando Configuration Manager vuelva a evaluar las reglas de requisitos para todas las implementaciones. El valor predeterminado es cada siete días.  

    > [!IMPORTANT]  
    >  Se recomienda que no cambie este valor a un valor inferior al predeterminado. Una programación de reevaluación más exigente afecta de forma negativa al rendimiento de los equipos cliente y de red.  

     Para iniciar esta acción desde un cliente, seleccione el **Ciclo de evaluación de implementación de aplicaciones** desde la pestaña **Acciones** del panel de control de **Configuration Manager**.  



##  <a name="software-inventory"></a>Inventario de software  

-   **Habilitar inventario de software en clientes** </br>
    De forma predeterminada, esta opción está establecida en **Sí**. Para obtener más información, vea [Introducción al inventario de software](/sccm/core/clients/manage/inventory/introduction-to-software-inventory).

-   **Programar inventario de software y recopilación de archivos** </br>
    Haga clic en **Programación** para ajustar la frecuencia con la que los clientes ejecutan los ciclos de inventario de software y recopilación de archivos. De forma predeterminada, este ciclo tiene lugar cada siete días.

-   **Detalle de notificación de inventario**  </br>
     Especifique uno de los niveles siguientes de información de archivo para incluir en el inventario:
    - **Solo archivo**
    - **Solo producto**
    - **Detalles completos** (valor predeterminado)

-   **Inventariar estos tipos de archivo**  </br>
     Si quiere especificar los tipos de archivo para incluir en el inventario, haga clic en **Tipos** y, después, configure las opciones siguientes:  

    > [!NOTE]  
    >  Si se aplican varias configuraciones de cliente personalizadas a un equipo, se combina el inventario devuelto por cada configuración.  

    -   Haga clic en el icono **Nuevo** para agregar un nuevo tipo de archivo al inventario. Después, especifique la información siguiente en el cuadro de diálogo **Propiedades de archivo inventariado**:  

        -   **Nombre**: proporcione un nombre al archivo que quiere inventariar. Use un carácter comodín de asterisco (**&#42;**) para representar cualquier cadena de texto y un signo de interrogación (**?**) para representar cualquier carácter individual. Por ejemplo, si quiere hacer un inventario de todos los archivos con la extensión .doc, especifique el nombre de archivo **\*.doc**.  

        -   **Ubicación**: haga clic en **Establecer** para abrir el cuadro de diálogo **Propiedades de ruta de acceso**. Configure el inventario de software para buscar el archivo especificado en todos los discos duros del cliente, buscar en una ruta de acceso especificada (por ejemplo **C:\Carpeta**) o buscar una variable especificada (por ejemplo *%windir%*). También puede buscar en todas las subcarpetas de la ruta de acceso especificada.  

        -   **Excluir archivos cifrados y comprimidos**: cuando se selecciona esta opción, no se incluye en el inventario ningún archivo comprimido o cifrado.  

        -   **Archivos excluidos en la carpeta Windows**: cuando se selecciona esta opción, no se incluye en el inventario ningún archivo de la carpeta Windows y sus subcarpetas.  

    -   Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Propiedades de archivo inventariado** .  

    -   Agregue todos los archivos que quiera incluir en el inventario y, después, haga clic en **Aceptar** para cerrar el cuadro de diálogo **Configurar valor de cliente**.  

-   **Recopilar archivos**  </br>
     Si quiere recopilar archivos de los equipos cliente, haga clic en **Archivos** y, después, configure las opciones siguientes:  

    > [!NOTE]  
    >  Si se aplican varias configuraciones de cliente personalizadas a un equipo, se combina el inventario devuelto por cada configuración.  

    -   En el cuadro de diálogo **Configurar valor de cliente**, haga clic en el icono **Nuevo** para agregar un archivo para la recopilación.  

    -   En el cuadro de diálogo **Propiedades del archivo recopilado** , proporcione la siguiente información:  

        -   **Nombre**: proporcione un nombre al archivo que quiera recopilar. Use un carácter comodín de asterisco (**&#42;**) para representar cualquier cadena de texto y un signo de interrogación (**?**) para representar cualquier carácter individual.  

        -   **Ubicación**: haga clic en **Establecer** para abrir el cuadro de diálogo **Propiedades de ruta de acceso**. Configure el inventario de software para buscar el archivo que quiere recopilar en todos los discos duros del cliente, buscar en una ruta de acceso especificada (por ejemplo **C:\Carpeta**) o buscar una variable especificada (por ejemplo *%windir%*). También puede buscar en todas las subcarpetas de la ruta de acceso especificada.  

        -   **Excluir archivos cifrados y comprimidos**: cuando se selecciona esta opción, no se recopila ningún archivo comprimido o cifrado.  

        -   **Detener la recopilación de archivos cuando el tamaño total de archivos supere (KB)**: especifique el tamaño del archivo, en kilobytes (KB), después del cual el cliente detiene la recopilación de los archivos especificados.  

          > [!NOTE]  
          >  El servidor de sitio recopila las cinco versiones cambiadas más recientemente de los archivos recopilados y las almacena en *&lt;directorio de instalación de Configuration Manager\>*\Inboxes\Sinv.box\Filecol. Si un archivo no ha cambiado desde el último ciclo de inventario de software, el archivo no se recopila de nuevo.  
          >   
          >  El inventario de software no recopila archivos de más de 20 MB.  
          >   
          >  El valor **Tamaño máximo para todos los archivos recopilados (KB)** del cuadro de diálogo **Configurar valor de cliente** muestra el tamaño máximo de todos los archivos recopilados. Cuando se alcanza este tamaño, se detiene la recopilación de archivos. Los archivos que ya se han recopilado se conservan y se envían al servidor de sitio.  

          > [!IMPORTANT]
          >  Si configura el inventario de software para recopilar muchos archivos de gran tamaño, es posible que esta configuración afecte de forma negativa al rendimiento de la red y el servidor de sitio.  

        Para obtener información sobre cómo ver los archivos recopilados, vea [Cómo usar el Explorador de recursos para ver el inventario de software en System Center Configuration Manager](../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md).  

    -   Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Propiedades del archivo recopilado** .  

    -   Agregue todos los archivos que quiera recopilar y, después, haga clic en **Aceptar** para cerrar el cuadro de diálogo **Configurar valor de cliente**.  

-   **Establecer nombres**  </br>
     El agente de inventario de software recupera los nombres de fabricante y producto de la información del encabezado de archivo. Estos nombres no siempre están estandarizados en la información del encabezado de archivo. Al ver el inventario de software en el Explorador de recursos, pueden aparecer versiones diferentes del mismo nombre de fabricante o producto. Para estandarizar estos nombres para mostrar, haga clic en **Establecer nombres** y, después, configure las opciones siguientes:  

    -   **Tipo de nombre**: el inventario de software recopila información sobre los fabricantes y los productos. Seleccione si quiere configurar los nombres para mostrar de un **Fabricante** o un **Producto**.  

    -   **Nombre para mostrar**: especifica el nombre para mostrar que quiere usar en lugar de los nombres de la lista **Nombres inventariados**. Puede hacer clic en el icono **Nuevo** para especificar un nuevo nombre para mostrar.  

    -   **Nombres inventariados**: haga clic en el icono **Nuevo** para agregar un nombre inventariado. Este nombre se sustituye en el inventario de software por el nombre seleccionado en la lista **Nombre para mostrar**. Puede agregar varios nombres para reemplazar.  



##  <a name="software-metering"></a>Medición de software

-   **Habilitar disponibilidad de software en clientes** </br>
    De forma predeterminada, esta opción está establecida en **Sí**. Para obtener más información, vea [Medición de software](/sccm/apps/deploy-use/monitor-app-usage-with-software-metering#configure-software-metering).

-   **Programar recopilación de datos** </br>
    Haga clic en **Programación** para ajustar la frecuencia con la que los clientes ejecutan el ciclo de medición de software. De forma predeterminada, este ciclo tiene lugar cada siete días.



##  <a name="software-updates"></a>Actualizaciones de software  

-   **Habilitar actualizaciones de software en clientes**  </br>
     Use esta opción para habilitar las actualizaciones de software en los clientes de Configuration Manager. Si desactiva esta opción, Configuration Manager quita del cliente las directivas de implementación existentes. Cuando vuelva a activar esta opción, el cliente descarga la directiva de implementación actual.  

    > [!IMPORTANT]  
    >  Cuando se deshabilita esta configuración, las directivas de cumplimiento que se basan en las actualizaciones de software dejan de funcionar.  

-   **Programación de exploración de actualización de software**  </br>
     Haga clic en **Programación** para especificar la frecuencia con la que el cliente inicia un análisis de evaluación del cumplimiento. Este análisis determina el estado de las actualizaciones de software en el cliente (por ejemplo, requerida o instalada). Para obtener más información sobre la evaluación de cumplimiento, consulte [Software updates compliance assessment](../../../sum/understand/software-updates-introduction.md#BKMK_SUMCompliance) (Evaluación del cumplimiento de las actualizaciones de software).  

     De forma predeterminada, en este análisis se usa una programación simple para iniciar cada siete días. Puede crear una programación personalizada para especificar un día y hora de inicio exactos, usar el Horario universal coordinado (UTC) o la hora local, y configurar el intervalo de repetición en un determinado día de la semana.  

    > [!NOTE]  
    >  Si especifica un intervalo de menos de un día, Configuration Manager lo establece automáticamente de forma predeterminada en un día.  

    > [!WARNING]  
    >  La hora de inicio en los equipos cliente es la hora de inicio más una cantidad de tiempo aleatoria de hasta dos horas. Esta cantidad aleatoria evita que los equipos cliente inicien el análisis y al mismo tiempo se conecten al punto de actualización de software activo.  

-   **Programar reevaluación de implementación**  </br>
     Haga clic en **Programación** para configurar la frecuencia con la que el agente cliente de actualizaciones de software vuelve a evaluar el estado de la instalación de actualizaciones de software en equipos cliente de Configuration Manager. Cuando las actualizaciones de software instaladas previamente ya no se encuentran en los clientes pero siguen siendo necesarias, el cliente vuelve a instalar las actualizaciones de software.

     Ajuste esta programación según la directiva de la empresa para el cumplimiento de actualización de software y si los usuarios pueden desinstalar las actualizaciones de software. Cada ciclo de reevaluación de implementación comporta actividad del procesador del equipo cliente y la red. De forma predeterminada, esta configuración usa una programación simple para iniciar el análisis de reevaluación de implementación cada siete días.  

    > [!NOTE]  
    >  Si especifica un intervalo de menos de un día, Configuration Manager lo establece automáticamente de forma predeterminada en un día.  

-   **Cuando se alcance una fecha límite de implementación de actualización de software, instale todas las demás implementaciones de actualización de software cuya fecha límite tenga lugar dentro de un período de tiempo específico**  </br>
     Establezca esta opción en **Sí** para instalar todas las actualizaciones de software de las implementaciones necesarias con fechas límite que se producen en un período de tiempo especificado. Cuando una implementación de actualización de software requerida alcanza una fecha límite, el cliente inicia la instalación de las actualizaciones de software en la implementación. Esta configuración determina si se deben instalar las actualizaciones de software desde otras implementaciones necesarias que tienen una fecha límite en el tiempo especificado.  

     Use esta opción para acelerar la instalación de actualizaciones de software necesarias. Esta configuración también puede aumentar la seguridad del cliente, reducir las notificaciones de usuario final y los reinicios del cliente. De forma predeterminada, esta opción se establece en **No** y, por tanto, no está habilitada.  

-   **Período de tiempo durante el cual también se instalarán todas las implementaciones pendientes cuya fecha límite sea durante este período**  </br>
     Use esta opción para especificar el período de tiempo para la configuración anterior. Puede especificar un valor entre 1 y 23 horas y entre 1 y 365 días. De forma predeterminada, esta opción se configura con un valor de siete días.  

-   **Habilitar instalación de archivos de instalación Express en clientes** </br>
    Establezca esta opción en **Sí** para permitir que los clientes usen archivos de instalación rápida. Para obtener más información, consulte [Administración de archivos de instalación rápida para actualizaciones de Windows 10](/sccm/sum/deploy-use/manage-express-installation-files-for-windows-10-updates).

    -   **Puerto usado para descargar contenido para archivos de instalación Express** </br>
        Esta opción configura el puerto local para el que agente de escucha HTTP descargue contenido rápido. De forma predeterminada se establece en 8005. No es necesario abrir este puerto en el firewall del cliente.

-   **Habilitar administración del Agente cliente de Office 365** </br>
    Use esta opción para habilitar la administración del Agente cliente de Office 365. Si establece el valor en **Sí**, permite configurar las opciones de instalación de Office 365, descargar archivos desde redes de entrega de contenido (CDN) de Office e implementar los archivos como una aplicación en Configuration Manager. Para más información, vea [Administración de Office 365 ProPlus](/sccm/sum/deploy-use/manage-office-365-proplus-updates).



## <a name="state-messaging"></a>Mensajes de estado

-   **Ciclo de notificación de mensaje de estado (minutos)**  </br>
     Especifica la frecuencia con la que los clientes notifican mensajes de estado. De forma predeterminada esta configuración es de 15 minutos.



##  <a name="user-and-device-affinity"></a>Afinidad entre usuario y dispositivo  

-   **Umbral de uso de afinidad de dispositivo de usuario (minutos)**  </br>
     Especifique el número de minutos antes de que Configuration Manager cree una asignación de afinidad de dispositivo de usuario.  De forma predeterminada este valor es de 2 880 minutos (dos días).

-   **Umbral de uso de afinidad de dispositivo de usuario (días)**  </br>
     Especifique el número de días durante los que el cliente mide el umbral de afinidad de dispositivo basado en uso.  De forma predeterminada, este valor es de 30 días.

    > [!NOTE]  
    >  Por ejemplo, se puede especificar **Umbral de uso de afinidad de dispositivo de usuario (minutos)** como **60** minutos y **Umbral de uso de afinidad de dispositivo de usuario (días)** como **5** días. Después, el usuario debe utilizar el dispositivo durante 60 minutos durante un período de cinco días para crear afinidad automática con el dispositivo.  

-   **Configurar automáticamente la afinidad de dispositivo de usuario desde los datos del usuario**  </br>
     Seleccione **Sí** para crear afinidad de dispositivo automático de usuarios en función de la información de uso que recopila Configuration Manager.  

-   **Permitir al usuario definir sus dispositivos primarios** </br>
    Si este valor es **Sí**, los usuarios pueden identificar sus propios dispositivos primarios en el Centro de software.



## <a name="windows-analytics"></a>Windows Analytics

Para obtener más información sobre estas opciones, vea [Configuración de clientes para notificar datos a Windows Analytics](/sccm/core/clients/manage/monitor-windows-analytics#configure-clients-to-report-data-to-windows-analytics).
    
