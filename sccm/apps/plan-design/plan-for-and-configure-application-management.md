---
title: "Planear y configurar la administración de aplicaciones"
titleSuffix: Configuration Manager
description: "Implemente y configure las dependencias necesarias para la implementación de aplicaciones en System Center Configuration Manager."
ms.custom: na
ms.date: 02/09/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 2be84a1d-ebb9-47ae-8982-c66d5b92a52a
caps.latest.revision: "13"
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.openlocfilehash: 66317bea84adbddf2d2e94c30a4a72e19229439b
ms.sourcegitcommit: 18ac58374d2d513fe2a197c80f7c8c6890a7d612
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/16/2017
---
# <a name="plan-for-and-configure-application-management-in-system-center-configuration-manager"></a>Planear y configurar la administración de aplicaciones en Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Use la información de este artículo como ayuda para implementar las dependencias necesarias para la implementación de aplicaciones en System Center Configuration Manager.  

## <a name="dependencies-external-to-configuration-manager"></a>Dependencias externas a Configuration Manager  

|Dependencia|Más información|  
|------------------|----------------------|  
|Se requiere Internet Information Services (IIS) en los servidores del sistema de sitio que ejecutan el punto de sitios web del catálogo de aplicaciones, el punto de servicio web del catálogo de aplicaciones, el punto de administración y el punto de distribución.|Para obtener más información sobre este requisito, vea [Configuraciones admitidas](../../core/plan-design/configs/supported-configurations.md).|  
|Dispositivos móviles inscritos por Configuration Manager|Cuando realice la firma de código de aplicaciones para implementarlas en dispositivos móviles, no use un certificado generado mediante una plantilla de versión 3 (**Windows Server 2008, Enterprise Edition**). Esta plantilla de certificado crea un certificado que no es compatible con aplicaciones de Configuration Manager para dispositivos móviles.<br /><br /> Si usa Servicios de certificados de Active Directory para la firma de código de aplicaciones de dispositivos móviles, no use plantillas de certificado de versión 3.|  
|Los clientes se deben configurar para auditar eventos de inicio de sesión si desea crear automáticamente afinidades de dispositivo del usuario.|El cliente de Configuration Manager lee los eventos de inicio de sesión de tipo **Correcto** del registro de eventos de seguridad de los equipos para determinar afinidades automáticas de los dispositivos de usuario.  Estos eventos se habilitan mediante las dos siguientes directivas de auditoría:<br>**Auditar eventos de inicio de sesión de cuenta**<br>**Auditar eventos de inicio de sesión**<br>Para crear automáticamente relaciones entre los usuarios y los dispositivos, asegúrese de que estas dos opciones están habilitadas en los equipos cliente. Puede usar la directiva de grupo de Windows para configurar estas opciones.|  

## <a name="configuration-manager-dependencies"></a>Dependencias de Configuration Manager   

|Dependencia|Más información|  
|------------------|----------------------|  
|Punto de administración|Los clientes se ponen en contacto con un punto de administración para descargar la directiva de cliente, buscar contenido y conectarse al catálogo de aplicaciones.<br /><br /> Si los clientes no pueden obtener acceso a un punto de administración, no podrán usar el catálogo de aplicaciones.|  
|Punto de distribución|Para poder implementar aplicaciones en clientes, debe tener al menos un punto de distribución en la jerarquía. De forma predeterminada, el servidor de sitio tiene un rol de sitio de punto de distribución habilitado durante una instalación estándar. El número y la ubicación de los puntos de distribución variarán según las necesidades de su empresa.<br /><br /> Para obtener más información sobre cómo instalar puntos de distribución y administrar contenido, consulte [Manage content and content infrastructure](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md) (Administrar el contenido y la infraestructura de contenido).|  
|Configuración de cliente|Varias configuraciones de cliente controlan cómo se instalan las aplicaciones en el cliente y la experiencia del usuario en el mismo. Estas configuraciones de cliente incluyen:<br /><br /><ul><li>Agente de equipo</li><li>Reinicio de equipo</li><li>Implementación de software</li><li>Afinidad entre usuario y dispositivo</li></ul> Para obtener más información sobre la configuración de cliente, vea [Acerca de la configuración de cliente](../../core/clients/deploy/about-client-settings.md).<br /><br /> Para más información sobre cómo especificar la configuración de cliente, consulte [Cómo configurar el cliente](../../core/clients/deploy/configure-client-settings.md).|  
|Cuentas de usuario detectadas para el catálogo de aplicaciones |Para que los usuarios puedan ver y solicitar aplicaciones del catálogo de aplicaciones, primero Configuration Manager debe detectar las cuentas de usuario. Para obtener más información, vea [Ejecutar la detección](/sccm/core/servers/deploy/configure/run-discovery).|  
|Cliente de App-V 4.6 SP1 o posterior para ejecutar aplicaciones virtuales|Para crear aplicaciones virtuales en Configuration Manager, los equipos cliente deben tener instalado App-V 4.6 SP1 o posterior.<br /><br /> También debe actualizar el cliente de App-V con la revisión descrita en el [artículo 2645225](http://go.microsoft.com/fwlink/p/?LinkId=237322) de Knowledge Base para poder implementar aplicaciones virtuales.|  
|Punto de servicio web del catálogo de aplicaciones|El punto de servicio web del catálogo de aplicaciones es un rol de sistema de sitio que proporciona información acerca del software disponible desde la biblioteca de software al sitio web del catálogo de aplicaciones.<br /><br /> Para más información sobre cómo configurar este rol de sistema de sitio, consulte [Configurar el centro de software y el catálogo de aplicaciones (equipos Windows solamente)](/sccm/apps/plan-design/plan-for-and-configure-application-management#configure-software-center-and-the-application-catalog-windows-pcs-only) en este tema.|  
|Punto de sitios web del catálogo de aplicaciones|El punto de sitios web del catálogo de aplicaciones es un rol de sistema de sitio que proporciona a los usuarios una lista del software disponible.<br /><br /> Para más información sobre cómo configurar este rol de sistema de sitio, consulte [Configurar el centro de software y el catálogo de aplicaciones (equipos Windows solamente)](/sccm/apps/plan-design/plan-for-and-configure-application-management#configure-software-center-and-the-application-catalog-windows-pcs-only) en este tema.|  
|Puede configurar otras fuentes de actualización opcionales si crea una directiva antimalware.|Para usar los informes de Configuration Manager para la administración de aplicaciones, primero debe instalar y configurar un punto de servicios de informes.<br /><br /> Para obtener más información, consulte [Generación de informes en System Center Configuration Manager](../../core/servers/manage/reporting.md).|  
|Permisos de seguridad para la administración de aplicaciones|Debe tener los siguientes permisos de seguridad para administrar aplicaciones:<br /><br /> El rol de seguridad **Autor de aplicaciones** incluye los permisos indicados anteriormente que son necesarios para crear, cambiar y retirar aplicaciones en Configuration Manager.<br /><br /> **Para implementar aplicaciones:**<br /><br /> El rol de seguridad **Administrador de implementación de aplicaciones** incluye los permisos indicados anteriormente que son necesarios para implementar aplicaciones en Configuration Manager.<br /><br /> El rol de seguridad **Administrador de aplicaciones** contiene todos los permisos de los roles de seguridad **Autor de aplicaciones** y **Administrador de implementación de aplicaciones** .<br /><br /> Para obtener más información, vea [Configurar la administración basada en roles](../../core/servers/deploy/configure/configure-role-based-administration.md).|  

##  <a name="configure-software-center-and-the-application-catalog-windows-pcs-only"></a>Configurar el centro de software y el catálogo de aplicaciones (equipos Windows solamente)  

 System Center Configuration Manager ahora ofrece dos métodos para que los usuarios cambien la configuración, busquen aplicaciones y las instalen:  

-   **El nuevo Centro de software**: el nuevo Centro de software tiene un aspecto moderno. Las aplicaciones que solo se hubiesen mostrado en el catálogo de aplicaciones que depende de Silverlight (aplicaciones disponibles para el usuario) ahora se muestran en la pestaña **Aplicaciones** del Centro de software. Todavía se puede acceder al catálogo de aplicaciones mediante el vínculo de la pestaña **Estado de la instalación** del Centro de software.  

     Es posible configurar los clientes para usar el nuevo centro de software mediante la habilitación de la opción de cliente **Agente de equipo** > **Usar el nuevo Centro de software**.  

    > [!IMPORTANT]  
    >  Aunque ya no necesite conectarse al catálogo de aplicaciones, debe configurar el punto de sitios web del catálogo de aplicaciones y el punto de servicio web del catálogo de aplicaciones tal como se detalla en la siguiente sección.  

-   **Centro de software anterior y catálogo de aplicaciones**: de forma predeterminada, los usuarios siguen conectándose a la versión anterior del Centro de software y al catálogo de aplicaciones (se requiere un explorador de web habilitado para Silverlight) para examinar las aplicaciones disponibles.  

 Sin importar la versión que decida usar, el centro de software se instala automáticamente al instalar el cliente de Configuration Manager en equipos con Windows.  

    > [!TIP]  
    >  La versión del centro de software que ven los usuarios se basa en la configuración del cliente de Configuration Manager. Esto le ofrece la flexibilidad para controlar qué versión se usa según la configuración de cliente personalizada que implemente en la colección. 

    > [!IMPORTANT]
    > En los próximos meses, quitaremos la versión anterior del Centro de software y ya no estará disponible.
    > Es posible configurar los clientes para usar el nuevo centro de software mediante la habilitación de la opción de cliente **Agente de equipo** > **Usar el nuevo Centro de software**. 

## <a name="steps-to-install-and-configure-the-application-catalog-and-software-center"></a>Pasos para instalar y configurar el catálogo de aplicaciones y el centro de software  

> [!IMPORTANT]  
>  Antes de realizar estos pasos, asegúrese de que se cumplen todos los requisitos previos indicados anteriormente.  

|Pasos|Detalles|Más información|  
|-----------|-------------|----------------------|  
|**Paso 1:** si usa conexiones HTTPS, asegúrese de haber implementado un certificado de servidor web en los servidores de sistema de sitio.|Implemente un certificado de servidor web en los servidores de sistema de sitio que ejecutarán el punto de sitios web del catálogo de aplicaciones y el punto de servicio web del catálogo de aplicaciones.<br /><br /> Además, si desea que los clientes usen el catálogo de aplicaciones desde Internet, implemente un certificado de servidor web en, al menos, un servidor de sistema de sitio de punto de administración y configúrelo para conexiones de cliente desde Internet.|Para más información sobre los requisitos de certificado, consulte [Requisitos de certificado PKI](../../core/plan-design/network/pki-certificate-requirements.md).|  
|**Paso 2:** si usa un certificado PKI de cliente para las conexiones a los puntos de administración, implemente un certificado de autenticación de cliente en los equipos cliente.|Si bien los clientes no usan un certificado de PKI de cliente para conectarse con el catálogo de aplicaciones, deben conectarse a un punto de administración antes de poder usar el catálogo de aplicaciones. Debe implementar un certificado de autenticación del cliente en los equipos cliente en los siguientes escenarios:<br /><br /><ul><li>Todos los puntos de administración de la intranet aceptan únicamente conexiones de cliente HTTPS.</li><li>Los clientes se conectan al catálogo de aplicaciones desde Internet.</li></ul>|Para más información sobre los requisitos de certificado, consulte [Requisitos de certificado PKI](../../core/plan-design/network/pki-certificate-requirements.md).|  
|**Paso 3:** instale y configure el punto de servicio web del catálogo de aplicaciones y el sitio web del catálogo de aplicaciones.|Debe instalar ambos roles de sistema de sitio en el mismo sitio. No es necesario instalarlos en el mismo servidor de sistema de sitio ni en el mismo bosque de Active Directory. Sin embargo, el punto de servicio web del catálogo de aplicaciones debe estar en el mismo bosque que la base de datos del sitio.|Para obtener más información sobre el planeamiento para roles de sistema de sitio, vea [Planeamiento de servidores y roles de sistema de sitio](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md).<br /><br /> Para configurar el punto de servicio web del catálogo de aplicaciones y el punto de sitios web del catálogo de aplicaciones, vea **Paso 3: Instalar y configurar los roles de sistema de sitio del catálogo de aplicaciones**.|  
|**Paso 4:** configure las opciones de cliente para el catálogo de aplicaciones y el centro de software.|Configure las opciones de cliente predeterminadas si desea que todos los usuarios tengan la misma configuración. De lo contrario, configure opciones de cliente personalizadas para recopilaciones específicas.|Para obtener más información sobre la configuración de cliente, vea [Acerca de la configuración de cliente](../../core/clients/deploy/about-client-settings.md).<br /><br /> Para más información sobre cómo configurar estas opciones de cliente, consulte **Paso 4: Configurar las opciones de cliente para el catálogo de aplicaciones y el Centro de software**.|  
|**Paso 5:** compruebe si funciona el catálogo de aplicaciones.|Puede usar el catálogo de aplicaciones directamente desde un explorador o desde el Centro de software.|Vea **Paso 5: comprobar si funciona el catálogo de aplicaciones**.|  

## <a name="supplemental-procedures-to-install-and-configure-the-application-catalog-and-software-center"></a>Procedimientos adicionales para instalar y configurar el catálogo de aplicaciones y el Centro de software  
 Utilice la siguiente información si los pasos de la tabla anterior requieren procedimientos adicionales.  

###  <a name="step-3-install-and-configure-the-application-catalog-site-system-roles"></a>Paso 3: Instalar y configurar los roles del sistema de sitio del catálogo de aplicaciones  
 Estos procedimientos configuran los roles de sistema de sitio para el catálogo de aplicaciones. Elija uno de los dos procedimientos siguientes, dependiendo de si va a instalar un nuevo servidor de sistema de sitio o a usar un servidor de sistema de sitio existente:  

> [!NOTE]  
>  El catálogo de aplicaciones no puede instalarse en un sitio secundario ni en un sitio de administración central.  

####  <a name="to-install-and-configure-the-application-catalog-site-systems-new-site-system-server"></a>Para instalar y configurar los sistemas de sitio del catálogo de aplicaciones: nuevo servidor de sistema de sitio  

1.  En la consola de Configuration Manager, elija **Administración** > **Configuración de sitio** > **Servidores y roles del sistema de sitios**.  

3.  En la pestaña **Inicio**, en el grupo **Crear**, elija **Crear servidor del sistema de sitio**.  

4.  En la página **General**, especifique la configuración general del sistema de sitio y, a continuación, elija **Siguiente**.  

    > [!TIP]  
    >  Si quiere que los equipos cliente tengan acceso al catálogo de aplicaciones a través de Internet, especifique el nombre de dominio completo (FQDN) de Internet.  

5.  En la página **Selección de rol de sistema** , seleccione **Punto de servicio web del catálogo de aplicaciones** y **Punto de sitios web del catálogo de aplicaciones** en la lista de roles disponibles y, a continuación, elija **Siguiente**.  

6.  Complete los pasos restantes.  

####  <a name="to-install-and-configure-the-application-catalog-site-systems-existing-site-system-server"></a>Para instalar y configurar los sistemas de sitio del catálogo de aplicaciones: servidor de sistema de sitio existente  

1.  En la consola de Configuration Manager, elija **Administración** > **Configuración del sitio** > **Servidores y roles del sistema de sitios** y, después, seleccione el servidor que quiere usar para el catálogo de aplicaciones.  

3.  En la pestaña **Inicio**, en el grupo **Servidor**, seleccione **Agregar roles del sistema de sitio**.  

4.  En la página **General**, especifique la configuración general del sistema de sitio y, a continuación, elija **Siguiente**.  

    > [!TIP]  
    >  Si quiere que los equipos cliente tengan acceso al catálogo de aplicaciones a través de Internet, especifique el nombre de dominio completo (FQDN) de Internet.  

5.  En la página **Selección de rol de sistema** , seleccione **Punto de servicio web del catálogo de aplicaciones** y **Punto de sitios web del catálogo de aplicaciones** en la lista de roles disponibles y, a continuación, elija **Siguiente**.  

6.  Complete los pasos restantes.  

7. Compruebe la instalación de estos roles de sistema de sitio mediante mensajes de estado y mediante la revisión de los archivos de registro:  

    Mensajes de estado: Utilice los componentes **SMS_PORTALWEB_CONTROL_MANAGER** y **SMS_AWEBSVC_CONTROL_MANAGER**.  

    Por ejemplo, el identificador de estado **1015** para **SMS_PORTALWEB_CONTROL_MANAGER** confirma que el Administrador de componentes de sitio ha instalado correctamente el punto de sitios web del catálogo de aplicaciones.  

    Archivos de registro: Busque **SMSAWEBSVCSetup.log** y **SMSPORTALWEBSetup.log**.  

    Para más información, busque los archivos de registro **awebsvcMSI.log** y **portlwebMSI.log**.  

###  <a name="step-4-configure-the-client-settings-for-the-application-catalog-and-software-center"></a>Paso 4: Configurar las opciones de cliente para el catálogo de aplicaciones y el Centro de software  
 Este procedimiento configura las opciones de cliente predeterminadas para el catálogo de aplicaciones y el Centro de software que se aplicarán a todos los dispositivos de la jerarquía. Si quiere que esta configuración solo se aplique a determinados dispositivos, puede crear una configuración de cliente personalizada e implementarla en una colección que tenga los dispositivos con la configuración específica. Para más información sobre cómo crear una configuración de dispositivo personalizada, consulte la sección [Cómo crear e implementar la configuración de cliente personalizada](../../core/clients/deploy/configure-client-settings.md#create-and-deploy-custom-client-settings) del tema [Cómo especificar la configuración de cliente en System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md).  

1.  En la consola de Configuration Manager, elija **Administración** > **Configuración de cliente** > **Configuración de cliente predeterminada**.  

3.  En la pestaña **Inicio**, en el grupo **Propiedades**, elija **Propiedades**.  

4.  Revise y configure las opciones relacionadas con las notificaciones de usuario, el catálogo de aplicaciones y el Centro de software. Por ejemplo:  

    1.  Grupo**Agente de equipo** :  

        -   **Punto de sitios web del catálogo de aplicaciones predeterminado**  

        -   **Agregar sitio web predeterminado del catálogo de aplicaciones a una zona de sitios de confianza de Internet Explorer**  

        -   **Nombre de organización mostrado en el Centro de software**  

            > [!TIP]  
            >  Para especificar el nombre de organización mostrado en el catálogo de aplicaciones y configurar el tema de sitio web, use la pestaña **Personalización** en las propiedades de sitio web del catálogo de aplicaciones.  

        -   **Usar el nuevo Centro de software** Establezca esta opción en **Sí** si quiere usar el nuevo Centro de software que permite que los usuarios finales busquen e instalen las aplicaciones disponibles sin necesidad de acceder al catálogo de aplicaciones (que requiere un explorador web habilitado para Silverlight).  

        -   **Instalar permisos**  

        -   **Mostrar notificaciones para nuevas implementaciones**  

    2.  Grupo**Administración de energía** :  

        -   **Permitir a los usuarios excluir su dispositivo de la administración de energía**  

    3.  Grupo**Herramientas remotas** :  

        -   **Los usuarios pueden cambiar la directiva o la configuración de notificaciones en el Centro de software**  

    4.  Grupo**Afinidad entre usuario y dispositivo** :  

        -   **Permitir a los usuarios definir sus dispositivos primarios**  

    > [!NOTE]  
    >  Para obtener más información sobre la configuración de cliente, vea [Acerca de la configuración de cliente en System Center Configuration Manager](../../core/clients/deploy/about-client-settings.md).  

5.  Elija **Aceptar** para cerrar el cuadro de diálogo **Configuración de cliente predeterminada** .  

Los equipos cliente se configurarán con estas opciones la próxima vez que descarguen directivas de cliente. Para iniciar la recuperación de directivas para un solo cliente, vea [Cómo administrar clientes](../../core/clients/manage/manage-clients.md).

#### <a name="to-customize-software-center-branding"></a>Personalización de la marca del Centro de software

La personalización de marca del Centro de software se aplica conforme a las siguientes reglas:

1. Si no está instalado el rol de servidor de sitio del punto de sitios web del catálogo de aplicaciones, el Centro de software mostrará el nombre de organización especificado en el cliente **Agente de equipo** que establece el **Nombre de organización mostrado en el Centro de software**. Para obtener instrucciones, vea [Cómo establecer la configuración del cliente](https://docs.microsoft.com/sccm/core/clients/deploy/configure-client-settings).
2. Si está instalado el rol de servidor de sitio del punto de sitios web del catálogo de aplicaciones, el Centro de software mostrará el nombre de la organización y el color especificados en las propiedades del rol de servidor de sitio del punto de sitios web del catálogo de aplicaciones. Para más información, vea [Configuration options for Application Catalog website point (Opciones de configuración del punto de sitios web del catálogo de aplicaciones)](https://docs.microsoft.com/sccm/core/servers/deploy/configure/configuration-options-for-site-system-roles#BKMK_ApplicationCatalog_Website).
3. Si una suscripción de Microsoft Intune está configurada y conectada a Configuration Manager, el Centro de software mostrará el nombre de la organización, el color y el logotipo de la empresa especificados en las propiedades de la suscripción de Intune. Para más información, vea [Configuring the Microsoft Intune subscription (Configuración de la suscripción de Microsoft Intune)](https://docs.microsoft.com/sccm/mdm/deploy-use/setup-hybrid-mdm#step-3-configure-intune-subscription).

> [!IMPORTANT]  
>  La personalización de marca del Centro de software se sincroniza con el servicio de Intune cada 14 días. Por lo tanto, puede haber un retraso antes de que los cambios realizados en Intune se muestren en Configuration Manager.

###  <a name="step-5-verify-that-the-application-catalog-is-operational"></a>Paso 5: comprobar si funciona el catálogo de aplicaciones  
 Utilice los procedimientos siguientes para comprobar que el catálogo de aplicaciones esté funcionando. Puede usar el catálogo de aplicaciones directamente desde un explorador o desde el Centro de software.  

> [!NOTE]  
>  El catálogo de aplicaciones requiere Microsoft Silverlight, que se instala automáticamente como un requisito previo del cliente de Configuration Manager. Si usa el catálogo de aplicaciones directamente desde un explorador mediante un equipo que no tiene instalado el cliente de Configuration Manager, verifique primero que Microsoft Silverlight esté instalado en el equipo.  

> [!TIP]  
>  La falta de cumplimiento de los requisitos previos está entre uno de los motivos más frecuentes por los que el catálogo de aplicaciones no funciona correctamente después de su instalación. Confirme que se cumplen los requisitos previos del rol de sistema de sitio para los roles de sistema de sitio del catálogo de aplicaciones. Puede hacerlo mediante el artículo [Configuraciones compatibles](../../core/plan-design/configs/supported-configurations.md).  

> [!NOTE]  
>  Si ha iniciado sesión con una cuenta de administrador de dominio, los mensajes de notificación del cliente de Configuration Manager (por ejemplo, los mensajes que indican que hay disponible nuevo software) no se mostrarán.  

### <a name="to-use-the-application-catalog-directly-from-a-browser"></a>Para usar el catálogo de aplicaciones directamente desde un explorador  

-   En un explorador, escriba la dirección del sitio web del catálogo de aplicaciones y compruebe que la página web se muestra con las tres pestañas: **Catálogo de aplicaciones**, **Mis solicitudes de aplicación**y **Mis dispositivos**.  

     Seleccione y use la dirección adecuada de las que se muestran en la siguiente lista para el catálogo de aplicaciones, donde &lt;servidor&gt; es el nombre del equipo, el FQDN de la intranet o el FQDN de Internet:  

    -   Conexiones de cliente HTTPS y configuración de rol de sistema de sitio predeterminadas: **https://&lt;servidor&gt;/CMApplicationCatalog**  

    -   Conexiones de cliente HTTP y configuración de rol de sistema de sitio predeterminada: **http://&lt;servidor&gt;/CMApplicationCatalog**  

    -   Conexiones de cliente HTTPS y configuración de rol de sistema de sitio personalizada: **https://&lt;servidor&gt;:&lt;puerto&gt;/&lt;nombre de aplicación web&gt;**  

    -   Conexiones de cliente HTTP y configuración de rol de sistema de sitio personalizada: **http://&lt;servidor&gt;:&lt;puerto&gt;/&lt;nombre de aplicación web&gt;**  

### <a name="to-use-the-application-catalog-from-software-center-does-not-apply-to-the-new-version-of-software-center"></a>Para usar el catálogo de aplicaciones desde el Centro de software (no se aplica a la nueva versión del Centro de software)  

1.  En un equipo cliente, elija **Inicio** > **Todos los programas** > **Microsoft System Center 2012** > **Configuration Manager** > **Centro de software**.  

2.  Si configuró previamente un nombre de organización para el Centro de software como una opción de configuración del cliente, confirme que se muestra tal como lo especificó.  

3.  Elija **Buscar otras aplicaciones en el catálogo de aplicaciones** y confirme que la página se muestra con las tres pestañas: **Catálogo de aplicaciones**, **Mis solicitudes de aplicación**y **Mis dispositivos**.  

> [!WARNING]  
>  Una vez que haya instalado los roles de sistema de sitio del catálogo de aplicaciones, no verá inmediatamente el catálogo de aplicaciones cuando elija el vínculo **Buscar otras aplicaciones en el catálogo de aplicaciones** desde el Centro de software. El catálogo de aplicaciones estará disponible en el Centro de software después de que el cliente realiza la siguiente descarga de su directiva de cliente o hasta 25 horas después de instalados los roles de sistema de sitio del catálogo de aplicaciones.  
