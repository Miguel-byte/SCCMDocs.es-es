---
title: "Requisitos previos de la implementación de clientes de Windows | System Center Configuration Manager"
description: "Obtenga información sobre los requisitos previos para la implementación de clientes en equipos Windows con System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 1a2a9b48-a95b-4643-b00c-b3079584ae2e
caps.latest.revision: 16
caps.handback.revision: 0
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 03ae6de34742ed0030e42c13639ef853d6b2bedc


---
# <a name="prerequisites-for-deploying-clients-to-windows-computers-in-system-center-configuration-manager"></a>Requisitos previos para la implementación de clientes en equipos Windows con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

La implementación de clientes de Configuration Manager en su entorno tiene las siguientes dependencias externas y dependencias dentro del producto. Además, cada método de implementación de cliente tiene sus propias dependencias, que se deben cumplir para que instalaciones de cliente se realicen correctamente.  

  Asegúrese también de revisar [Configuraciones admitidas para System Center Configuration Manager](../../../core/plan-design/configs/supported-configurations.md) para confirmar que los dispositivos cumplen los requisitos mínimos de hardware y sistema operativo del cliente de Configuration Manager.  

 Para obtener más información sobre los requisitos previos del cliente de Configuration Manager para LINUX y UNIX, consulte [Planning for client deployment to Linux and UNIX computers in System Center Configuration Manager](../../../core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md) (Planificación de la implementación del cliente en equipos Linux y UNIX en System Center Configuration Manager).  

> [!NOTE]  
>  Los números de versión de software que se muestran en este artículo solo indican los números de versión mínimos necesarios.  

##  <a name="a-namebkmkprereqscomputersa-prerequisites-for-computer-clients"></a><a name="BKMK_prereqs_computers"></a> Requisitos previos de los equipos cliente  
 Utilice la siguiente información para determinar los requisitos previos para la instalación del cliente de Configuration Manager en los equipos.  

### <a name="dependencies-external-to-configuration-manager"></a>Dependencias externas a Configuration Manager  

|||  
|-|-|  
|Windows Installer versión 3.1.4000.2435|Necesario para admitir el uso de los archivos de actualización (.msp) de Windows Installer para paquetes y actualizaciones de software.|  
|[KB2552033](http://go.microsoft.com/fwlink/p/?LinkId=240048)|Instale esta revisión en los servidores de sitio que ejecutan Windows Server 2008 R2 cuando esté habilitada la instalación de inserción de cliente.|  
|Microsoft Background Intelligent Transfer Service (BITS) versión 2.5|Se requiere para permitir transferencias de datos limitadas entre el equipo cliente y los sistemas de sitio de Configuration Manager. BITS no se descarga automáticamente durante la instalación del cliente. Normalmente, si se instala BITS en equipos, es necesario reiniciar para completar la instalación.<br /><br /> La mayoría de los sistemas operativos incluyen BITS pero, si no es así (por ejemplo, Windows Server 2003 R2 SP2), debe instalar BITS antes de instalar el cliente de Configuration Manager.|  
|Programador de tareas de Microsoft|Habilite este servicio en el cliente para completar la instalación del cliente.|  

### <a name="dependencies-external-to-configuration-manager-and-automatically-downloaded-during-installation"></a>Dependencias externas a Configuration Manager y descarga automática durante la instalación  
 El cliente de Configuration Manager tiene algunas dependencias externas potenciales. Estas dependencias dependen del sistema operativo y del software instalado en el equipo cliente.  

 Si estas dependencias son necesarias para completar la instalación del cliente, se instalan automáticamente con el software de cliente.  

|||  
|-|-|  
|Windows Update Agent versión 7.0.6000.363|Necesario para que Windows admita la detección e implementación de actualizaciones.|  
|Microsoft Core XML Services (MSXML) versión 6.20.5002 o posterior|Necesario para admitir el procesamiento de documentos XML en Windows.|  
|Compresión diferencial remota de Microsoft (RDC)|Necesario para optimizar la transmisión de datos a través de la red.|  
|Microsoft Visual C++ 2013 Redistributable versión 12.0.21005.1|Necesario para admitir las operaciones de cliente. Cuando esta actualización se instala en los equipos cliente, podría ser necesario reiniciar para completar la instalación.|  
|Microsoft Visual C++ 2005 Redistributable versión 8.0.50727.42|Necesario para admitir las operaciones de Microsoft SQL Server Compact.|  
|API de creación de imágenes de Windows 6.0.6001.18000|Necesarias para permitir que Configuration Manager administre archivos de imagen de Windows (.wim).|  
|Microsoft Policy Platform 1.2.3514.0|Necesaria para permitir a los clientes evaluar la configuración de la conformidad.|  
|Microsoft Silverlight 5.1.41212.0 (a partir de la versión 1602 de Configuration Manager)|Necesario para admitir la experiencia de usuario del sitio web del catálogo de aplicaciones.|  
|Microsoft .NET Framework versión 4.5.2.|Necesario para admitir las operaciones de cliente. Se instala automáticamente en el equipo cliente si este no tiene Microsoft .NET Framework versión 4.5 o posterior instalado. Para más información, consulte [Detalles adicionales sobre la versión 4.5.2 de Microsoft .NET Framework](#dotNet).|  
|Componentes de Microsoft SQL Server Compact 3.5 SP2|Necesarios para almacenar información relacionada con las operaciones de cliente.|  
|Componentes de creación de imágenes de Microsoft Windows|Requisito de Microsoft .NET Framework 4.0 para Windows Server 2003 o Windows XP SP2 para equipos de 64 bits.|  

####  <a name="a-namedotneta-additional-details-about-microsoft-net-framework-version-452"></a><a name="dotNet"></a> Detalles adicionales sobre la versión 4.5.2 de Microsoft .NET Framework  

> [!NOTE]  
>  El 12 de enero de 2016 finalizó el soporte técnico para .NET 4.0, 4.5 y 4.5.1. Para más información, consulte [Preguntas más frecuentes de la directiva del ciclo de vida de soporte técnico de Microsoft de .NET Framework](https://support.microsoft.com/gp/framework_faq?WT.mc_id=azurebg_email_Trans_943_NET452_Update) en support.microsoft.com.  

 Puede ser necesario reiniciar para completar la instalación de la versión 4.5.2 de Microsoft .NET Framework. El usuario verá la notificación **Es necesario reiniciar** en la bandeja del sistema.  Escenarios comunes que requieren reiniciar los equipos cliente:  

-   Aplicaciones o servicios .NET que estén en ejecución en el equipo.  

-   Faltan una o varias actualizaciones de software necesarias para la instalación de .NET.  

-   El equipo tiene pendiente un reinicio de la instalación anterior de actualizaciones de software de .NET Framework.  

 Después de instalar .NET Framework 4.5.2, sus actualizaciones adicionales se podrían instalar posteriormente, lo que puede requerir reinicios adicionales de los equipos.  

### <a name="configuration-manager-dependencies"></a>Dependencias de Configuration Manager  
 Para obtener más información sobre los siguientes roles de sistema de sitio, consulte [Determine the site system roles for System Center Configuration Manager clients](../../../core/clients/deploy/plan/determine-the-site-system-roles-for-clients.md) (Determinar los roles de sistema de sitio para System Center Configuration Manager).  

|||  
|-|-|  
|Punto de administración|Si bien no es necesario un punto de administración para implementar el cliente de Configuration Manager, debe tener un punto de administración para transferir información entre equipos cliente y servidores de Configuration Manager. Sin un punto de administración, no puede administrar los equipos cliente.|  
|Punto de distribución|El punto de distribución es un rol del sistema de sitio opcional, aunque recomendado para la implementación de clientes. Todos los puntos de distribución hospedan los archivos de origen del cliente, lo que permite a los equipos encontrar el punto de distribución más cercano desde el que descargar los archivos de origen del cliente durante la implementación del cliente. Si el sitio no tiene un punto de distribución, los equipos descargan los archivos de origen del cliente desde su punto de administración.|  
|Punto de estado de reserva|El punto de estado de reserva es un rol del sistema de sitio opcional, aunque recomendado para la implementación de clientes. El punto de estado de reserva efectúa un seguimiento de la implementación del cliente y permite a los equipos del sitio de Configuration Manager enviar mensajes cuando no se pueden comunicar con un punto de administración.|  
|Puede configurar otras fuentes de actualización opcionales si crea una directiva antimalware.|El punto de servicios de informes es un rol de sistema de sitio opcional, pero recomendado, que permite mostrar informes relacionados con la implementación y la administración de clientes. Para obtener más información, consulte [Generación de informes en System Center Configuration Manager](../../../core/servers/manage/reporting.md).|  

### <a name="installation-method-dependencies"></a>Dependencias de los métodos de instalación  
 Los siguientes requisitos previos son específicos para los distintos métodos de instalación de cliente.  

-   Instalación de inserción de cliente  

    -   Las cuentas de instalación de inserción de cliente se utilizan para conectar equipos para instalar el cliente y se especifican en la pestaña **Cuentas** del cuadro de diálogo **Propiedades de instalación de inserción de cliente** . La cuenta debe ser miembro del grupo de administradores locales del equipo de destino.  

         Si no especifica una cuenta de instalación de inserción de cliente, se utilizará la cuenta de equipo de servidor de sitio.  

    -   El equipo en el que se va a instalar el cliente debe haber sido detectado por al menos un método de detección de Configuration Manager.  

    -   El equipo tiene un recurso compartido ADMIN$.  

    -   **Habilitar la instalación de inserción de cliente en recursos asignados** debe estar seleccionada en el cuadro de diálogo **Propiedades de instalación de inserción de cliente** si desea insertar automáticamente el cliente de Configuration Manager en los recursos detectados.  

    -   El equipo cliente debe ser capaz de ponerse en contacto con un punto de distribución o un punto de administración para descargar los archivos auxiliares.  

     Debe tener los permisos de seguridad siguientes para instalar el cliente de Configuration Manager mediante el uso de inserción de cliente:  

    -   Para configurar la cuenta de instalación de inserción de cliente: permisos **Modificar** y Leer para el objeto **Sitio**  

    -   Para utilizar la inserción del cliente para instalar el cliente en colecciones, dispositivos y consultas: permisos **Modificar recursos** y **Leer** para el objeto Colección.  

     El rol de seguridad **Administrador de infraestructuras** incluye los permisos necesarios para administrar la instalación de Inserción del cliente.  

-   Instalación basada en el punto de actualización de software  

    -   Si el esquema de Active Directory no se ha extendido o si está instalando clientes de otro bosque, las propiedades de instalación para CCMSetup.exe se deben haber aprovisionado en el registro del equipo mediante directiva de grupo. Para obtener más información, consulte [Aprovisionamiento de propiedades de instalación de cliente (instalación de clientes con directivas de grupo y basada en actualizaciones de software)](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Provision).  

    -   El cliente de Configuration Manager debe publicarse en el punto de actualización de software.  

    -   El equipo cliente debe ser capaz de ponerse en contacto con un punto de distribución o un punto de administración para descargar archivos auxiliares.  

     Para consultar los permisos de seguridad necesarios para administrar las actualizaciones de software de Configuration Manager, consulte [Prerequisites for software updates in System Center Configuration Manager](../../../sum/plan-design/prerequisites-for-software-updates.md) (Requisitos previos para las actualizaciones de software en System Center Configuration Manager).  

-   Instalación basada en directivas de grupo  

    -   Si el esquema de Active Directory no se ha extendido o si está instalando clientes de otro bosque, las propiedades de instalación para CCMSetup.exe se deben haber aprovisionado en el registro del equipo mediante directiva de grupo. Para obtener más información, consulte [Aprovisionamiento de propiedades de instalación de cliente (instalación de clientes con directivas de grupo y basada en actualizaciones de software)](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Provision).  

    -   El equipo cliente debe ser capaz de ponerse en contacto con un punto de administración para descargar archivos auxiliares.  

-   Instalación de inicio de sesión basado en scripts  

     El equipo cliente debe ser capaz de ponerse en contacto con un punto de distribución o un punto de administración para descargar archivos auxiliares, a menos que especifique CCMSetup.exe en la línea de comandos con la propiedad de línea de comandos **ccmsetup /source**.  

-   Instalación manual  

     El equipo cliente debe ser capaz de ponerse en contacto con un punto de distribución o un punto de administración para descargar archivos auxiliares, a menos que especifique CCMSetup.exe en la línea de comandos con la propiedad de línea de comandos **ccmsetup /source**.  

-   Instalación de equipo de grupo de trabajo  

     Con el fin de obtener acceso a recursos en el dominio de servidor del sitio de Configuration Manager, la cuenta de acceso de red debe estar configurada para el sitio.  

     Para obtener más información sobre cómo configurar la cuenta de acceso a la red, consulte [Fundamental concepts for content management in System Center Configuration Manager](../../plan-design/hierarchy/fundamental-concepts-for-content-management.md) (Conceptos básicos de la administración de contenido en System Center Configuration Manager).  

-   Instalación de software basada en distribución (para actualizaciones únicamente)  

    -   Si el esquema de Active Directory no se ha extendido o si está instalando clientes de otro bosque, las propiedades de instalación para CCMSetup.exe se deben haber aprovisionado en el registro del equipo mediante directiva de grupo. Para obtener más información, consulte [How to Provision Client Installation Properties (Group Policy and Software Update-Based Client Installation)](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Provision) (Aprovisionamiento de propiedades de instalación de cliente [instalación de clientes con directivas de grupo y basada en actualizaciones de software]).  

    -   El equipo cliente debe ser capaz de ponerse en contacto con un punto de distribución o un punto de administración para descargar los archivos auxiliares.  

     Para consultar los permisos de seguridad necesarios para actualizar el cliente de Configuration Manager mediante la administración de aplicaciones, consulte [Seguridad y privacidad de la administración de aplicaciones](../../../apps/plan-design/security-and-privacy-for-application-management.md).  

-   Actualizaciones de cliente automáticas  

     Debe ser miembro del rol de seguridad **Administrador total** para configurar actualizaciones automáticas de cliente.  

### <a name="firewall-requirements"></a>Requisitos de firewall  
 Si hay un firewall entre los servidores del sistema del sitio y los equipos en los que desea instalar el cliente de Configuration Manager, consulte [Windows Firewall and port settings for clients in System Center Configuration Manager](../../../core/clients/deploy/windows-firewall-and-port-settings-for-clients.md) (Configuración de puertos y Firewall de Windows para clientes en System Center Configuration Manager).  

##  <a name="a-namebkmkprereqsmobiledevicesa-prerequisites-for-mobile-device-clients"></a><a name="BKMK_prereqs_mobiledevices"></a> Requisitos previos de los clientes de dispositivos móviles  
 Utilice la siguiente información para determinar los requisitos previos para la instalación del cliente de Configuration Manager en los dispositivos móviles y utilice Configuration Manager para inscribirlos.  

### <a name="dependencies-external-to-configuration-manager"></a>Dependencias externas a Configuration Manager  

-   Se requiere una entidad de certificación (CA) empresarial de Microsoft con plantillas de certificado para implementar y administrar los certificados necesarios para dispositivos móviles.  

     La entidad emisora debe aprobar automáticamente las solicitudes de certificados de los usuarios de dispositivos móviles durante el proceso de inscripción.  

     Para obtener más información sobre los requisitos de certificados, consulte [Security and privacy for certificate profiles in System Center Configuration Manager](../../../protect/plan-design/security-and-privacy-for-certificate-profiles.md) (Seguridad y privacidad para los perfiles de certificados en System Center Configuration Manager).  

-   Un grupo de seguridad que contiene los usuarios que pueden inscribir sus dispositivos móviles.  

     Este grupo de seguridad se utiliza para configurar la plantilla de certificado que se utiliza durante la inscripción de dispositivos móviles.  

-   Opcional, pero recomendado: un alias DNS (registro CNAME), denominado **ConfigMgrEnroll** , configurado para el servidor de sistema de sitio en el que se va a instalar el punto de proxy de inscripción.  

     Este alias DNS es necesario para admitir la detección automática para el servicio de inscripción: si no configura este registro DNS, los usuarios deben especificar manualmente el nombre del servidor de sistema de sitio del punto de proxy de inscripción como parte del proceso de inscripción.  

-   Dependencias del rol de sistema de sitio para los equipos que ejecutarán los roles de sistema de sitio del punto de inscripción y del proxy de inscripción.  

     Consulte [Supported operating systems for site system servers](../../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md) (Sistemas operativos compatibles para los servidores de sistema de sitio).  

### <a name="configuration-manager-dependencies"></a>Dependencias de Configuration Manager  
 Para obtener más información sobre los siguientes roles de sistema de sitio, consulte [Determine the site system roles for System Center Configuration Manager clients](../../../core/clients/deploy/plan/determine-the-site-system-roles-for-clients.md) (Determinar los roles de sistema de sitio para System Center Configuration Manager).  

-   Punto de administración que se configura para las conexiones de cliente HTTPS y se habilita para dispositivos móviles  

     Siempre es necesario un punto de administración para instalar el cliente de Configuration Manager en dispositivos móviles. Además de los requisitos de configuración de HTTPS y la habilitación para dispositivos móviles, el punto de administración debe configurarse con un FQDN de Internet y aceptar conexiones de cliente de Internet.  

-   Punto de inscripción y punto de proxy de inscripción  

     Un punto de proxy de inscripción administra solicitudes de inscripción de dispositivos móviles. El punto de inscripción completa el proceso de inscripción. El punto de inscripción debe estar en el mismo bosque de Active Directory que el servidor de sitio, pero el punto de proxy de inscripción puede estar en otro bosque.  

-   Configuración de cliente para la inscripción de dispositivo móvil  

     Configure las opciones de cliente para que los usuarios puedan inscribir dispositivos móviles y configurar como mínimo un perfil de inscripción.  

-   Puede configurar otras fuentes de actualización opcionales si crea una directiva antimalware.  

     El punto de servicios de informes es un rol de sistema de sitio opcional pero recomendado que permite mostrar informes relacionados con la inscripción de dispositivos móviles y la administración de clientes.  

     Para obtener más información, consulte [Generación de informes en System Center Configuration Manager](../../../core/servers/manage/reporting.md).  

-   Para configurar la inscripción de dispositivos móviles, debe tener los permisos de seguridad siguientes:  

    -   Para agregar, modificar y eliminar roles de sistema de sitio de inscripción: permiso **Modificar** en el objeto **Sitio** .  

    -   La configuración de cliente predeterminada requiere el permiso **Modificar** en el objeto **Sitio** , y la configuración de cliente personalizada requiere permisos **Agente cliente**  .  

     El rol de seguridad **Administrador total** incluye los permisos necesarios para configurar los roles de sistema de sitio de inscripción.  

     Para administrar dispositivos móviles inscritos, debe tener los permisos de seguridad siguientes:  

    -   Para borrar o retirar un dispositivo móvil: **Eliminar recurso** para el objeto **Colección** .  

    -   Para cancelar un comando de borrado o retirado: **Eliminar recurso** para el objeto **Colección** .  

    -   Para permitir y bloquear dispositivos móviles: **Modificar recurso** para el objeto **Colección** .  

    -   Para bloquear de forma remota o restablecer el Bloqueo remoto o restablecer el código de acceso en un dispositivo móvil: **Modificar recurso** para el objeto **Colección** .  

     El rol de seguridad **Administrador de operaciones** incluye los permisos necesarios para administrar dispositivos móviles.  

     Para obtener más información sobre cómo configurar los permisos de seguridad, consulte [Fundamentals of role-based administration for System Center Configuration Manager](../../../core/understand/fundamentals-of-role-based-administration.md) (Conceptos básicos de la administración basada en roles de System Center Configuration Manager) y [Configurar la administración basada en roles de System Center Configuration Manager](../../../core/servers/deploy/configure/configure-role-based-administration.md).  

### <a name="firewall-requirements"></a>Requisitos de firewall  
 Los dispositivos de red intermedios como los enrutadores, los firewalls y, si se corresponde, Firewall de Windows, deben permitir el tráfico relacionado con la inscripción de dispositivos móviles:  

-   Entre los dispositivos móviles y el punto de proxy de inscripción: HTTPS (de manera predeterminada, TCP 443)  

-   Entre el punto de proxy de inscripción y el punto de inscripción: HTTPS (de manera predeterminada, TCP 443)  

 Si utiliza un servidor proxy web, debe configurarse para el protocolo de túnel SSL. El protocolo de puente SSL no es compatible con dispositivos móviles.  



<!--HONumber=Nov16_HO1-->


