---
title: "Seguridad y privacidad para la administración de sitios | Microsoft Docs"
description: "Optimice la seguridad y la privacidad para la administración de sitios en System Center Configuration Manager."
ms.custom: na
ms.date: 3/1/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1d58176e-abc0-4087-8583-ce70deb4dcf5
caps.latest.revision: 8
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: f9097014c7e988ec8e139e518355c4efb19172b3
ms.openlocfilehash: a60b8c103a303dcae0bd66f3060d5a8f17d1cef9
ms.lasthandoff: 03/04/2017


---
# <a name="security-and-privacy-for-site-administration-in-system-center-configuration-manager"></a>Seguridad y privacidad para la administración de sitios en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Este tema contiene información sobre la seguridad y privacidad de la jerarquía y los sitios de System Center Configuration Manager.

##  <a name="BKMK_Security_Sites"></a> Prácticas recomendadas de seguridad para la administración de sitios  
 Use los siguientes procedimientos recomendados de seguridad para proteger los sitios y la jerarquía de System Center Configuration Manager.  

 **Ejecute el programa de instalación solamente desde un origen de confianza y asegure el canal de comunicación entre el medio de instalación y el servidor de sitio.**  

 Con el fin de evitar que alguien manipule los archivos de origen, ejecute el programa de instalación desde un origen de confianza. Si almacena los archivos en la red, asegure la ubicación de red.  

 Si ejecuta el programa de instalación desde una ubicación de red, para impedir que un atacante manipule los archivos mientras se transmiten por la red, use la firma IPsec o SMB (Bloque de mensajes del servidor) entre la ubicación de origen de los archivos de instalación y el servidor de sitio.  

 Además, si usa el Descargador del programa de instalación para descargar los archivos que necesita el programa de instalación, asegúrese de que también protege la ubicación donde se almacenan estos archivos y el canal de comunicación para esta ubicación cuando ejecute el programa de instalación.  

 **Extienda el esquema de Active Directory para System Center Configuration Manager y publique sitios en Active Directory Domain Services.**  

 Las extensiones de esquema no son necesarias para ejecutar System Center Configuration Manager, pero crean un entorno más seguro porque los clientes y los servidores de sitio de Configuration Manager pueden recuperar información de un origen de confianza.  

 Si los clientes no están en un dominio de confianza, implemente los siguientes roles de sistema de sitio en los dominios de los clientes:  

-   Punto de administración  

-   Punto de distribución  

-   Punto de sitios web del catálogo de aplicaciones  

> [!NOTE]  
>  Un dominio de confianza para Configuration Manager requiere la autenticación Kerberos. Esto significa que si los clientes están en otro bosque que no tiene una confianza de bosque bidireccional con el bosque del servidor de sitio, se considera que estos clientes están en un dominio que no es de confianza. Una confianza externa no es suficiente para este propósito.  

 **Utilice IPsec para proteger las comunicaciones entre servidores de sistema de sitio y sitios.**  

 Aunque Configuration Manager protege la comunicación entre el servidor de sitio y el equipo que ejecuta SQL Server, Configuration Manager no protege las comunicaciones entre los roles de sistema de sitio y SQL Server. Solo algunos sistemas de sitio (el punto de inscripción y el punto de servicio web del catálogo de aplicaciones) pueden configurarse para HTTPS para la comunicación dentro de un sitio.  

 Si no utiliza controles adicionales para proteger estos canales de servidor a servidor, los atacantes pueden utilizar diversos ataques de suplantación de identidad y de tipo "Man in the middle" contra los sistemas de sitio. Use la firma SMB cuando no pueda utilizar IPsec.  

> [!NOTE]  
>  Es especialmente importante proteger el canal de comunicación entre el servidor de sitio y el servidor de origen del paquete. Esta comunicación utiliza SMB. Si no se puede utilizar IPsec para proteger esta comunicación, use la firma SMB para asegurarse de que no se manipulen los archivos antes de que los clientes los descarguen y ejecuten.  

 **No cambie los grupos de seguridad que Configuration Manager crea y administra para la comunicación del sistema de sitio.**  

 Grupos de seguridad:  

-   **SMS_SiteSystemToSiteServerConnection_MP_&lt;SiteCode\>**  

-   **SMS_SiteSystemToSiteServerConnection_SMSProv_&lt;SiteCode\>**  

-   **SMS_SiteSystemToSiteServerConnection_Stat_&lt;SiteCode\>**  

Configuration Manager crea y administra de forma automática estos grupos de seguridad. Esto incluye la eliminación de cuentas de equipo cuando se quita un rol de sistema de sitio.  

Para garantizar la continuidad del servicio y los privilegios mínimos, no modifique manualmente estos grupos.  

**Si los clientes no pueden consultar el servidor de catálogo global para obtener información de Configuration Manager, administre el proceso de aprovisionamiento de la clave raíz confiable.**  

Si los clientes no pueden consultar el catálogo global para obtener información de Configuration Manager, deben emplear la clave raíz confiable para autenticar puntos de administración válidos. La clave raíz confiable se almacena en el Registro del cliente y se puede establecer mediante la directiva de grupo o la configuración manual.  

Si el cliente no tiene una copia de la clave raíz confiable antes de contactar con un punto de administración por primera vez, confiará en el primer punto de administración con el que se comunique. Para reducir el riesgo de que un atacante dirija erróneamente los clientes a un punto de administración no autorizado, puede aprovisionar los clientes previamente con la clave raíz confiable. Para obtener más información, consulte [Planeación de la clave raíz confiable](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

**Utilice números de puerto no predeterminados.**  

El uso de números de puerto no predeterminados puede proporcionar seguridad adicional, ya que hace más difícil a los atacantes explorar el entorno en preparación para un ataque. Si decide usar puertos no predeterminados, planéelos antes de instalar Configuration Manager y úselos de forma coherente en todos los sitios en la jerarquía. Los puertos de solicitud de cliente y Wake on LAN son ejemplos donde se pueden usar números de puerto no predeterminados.  

**Utilice la separación de roles en sistemas de sitio.**  

Aunque puede instalar todos los roles de sistema de sitio en un único equipo, esta práctica se utiliza muy poco en redes de producción porque crea un único punto de error.  

**Reduzca el perfil del ataque.**  

El aislamiento de cada rol de sistema de sitio en un servidor diferente reduce la posibilidad de que un ataque contra las vulnerabilidades de un sistema de sitio se use contra un sistema de sitio diferente. Muchos roles de sistema de sitio requieren la instalación de Internet Information Services (IIS) en el sistema de sitio, lo que supone un aumento de la superficie de ataque. Si debe combinar roles de sistema de sitio para reducir los gastos en hardware, combine roles de sistema de sitio de IIS únicamente con otros roles de sistema de sitio que requieran IIS.  

> [!IMPORTANT]  
>  El rol de punto de estado de reserva es una excepción. Como este rol de sistema de sitio acepta datos no autenticados de los clientes, se recomienda no asignar nunca el rol de punto de estado de reserva a ningún otro rol de sistema de sitio de Configuration Manager.  


**Siga las prácticas recomendadas de seguridad para Windows Server y ejecute al Asistente para configuración de seguridad en todos los sistemas de sitio.**  

El Asistente para configuración de seguridad (SCW) le ayuda a crear una directiva de seguridad que se puede aplicar a cualquier servidor de la red. Después de instalar la plantilla de System Center Configuration Manager, SCW reconoce las aplicaciones, puertos, servicios y roles de sistema de sitio de Configuration Manager. Después, permite la comunicación que se requiere para Configuration Manager y bloquea las comunicaciones que no son necesarias.  

El Asistente para configuración de seguridad se incluye con el kit de herramientas de System Center 2012 Configuration Manager, que puede descargar del Centro de descarga de Microsoft: [System Center 2012 - Configuration Manager Component Add-ons and Extensions](http://go.microsoft.com/fwlink/p/?LinkId=251931) (System Center 2012: complementos y extensiones de componentes de Configuration Manager).  

**Configure direcciones IP estáticas para los sistemas de sitio.**  

Las direcciones IP estáticas son más fáciles de proteger frente a ataques de resolución de nombre.  

Las direcciones IP estáticas también facilitan la configuración de IPsec. El uso de IPsec es una práctica recomendada de seguridad para proteger la comunicación entre sistemas de sitio en Configuration Manager.  

**No instale otras aplicaciones en los servidores de sistema de sitio.**  

Al instalar otras aplicaciones en servidores de sistema de sitio, aumenta la superficie de ataque de Configuration Manager y corre el riesgo de sufrir problemas de incompatibilidad.  

**Exija la firma y habilite el cifrado como una opción de sitio.**  

Habilite las opciones de firma y cifrado para el sitio. Asegúrese de que todos los clientes pueden admitir el algoritmo hash SHA-256 y, después, habilite la opción **Requerir SHA-256**.  

**Restrinja y supervise los usuarios administrativos de Configuration Manager y use la administración basada en roles para conceder los permisos mínimos que requieran estos usuarios.**  

Conceda acceso administrativo a Configuration Manager solo a los usuarios en los que confíe y luego concédales los permisos mínimos que necesiten mediante roles de seguridad integrados o mediante la personalización de roles de seguridad. Los usuarios administrativos que pueden crear, modificar e implementar aplicaciones, secuencias de tareas, actualizaciones de software, elementos de configuración y líneas base de configuración pueden controlar potencialmente los dispositivos en la jerarquía de Configuration Manager.  

Audite periódicamente las asignaciones de usuarios administrativos y su nivel de autorización para comprobar los cambios necesarios.  

Para obtener más información sobre cómo configurar la administración basada en roles, consulte [Configure role-based administration for System Center Configuration Manager](../../../core/servers/deploy/configure/configure-role-based-administration.md) (Configurar la administración basada en roles de System Center Configuration Manager).  

**Proteja las copias de seguridad de Configuration Manager y el canal de comunicación cuando cree copias de seguridad y restauración.**  

Cuando realiza una copia de seguridad de Configuration Manager, esta información incluye los certificados y otros datos confidenciales que un atacante podría usar para la suplantación.  

Al transferir estos datos a través de la red, utilice la firma SMB o IPsec y asegure la ubicación de copia de seguridad.  

**Al exportar o importar objetos desde la consola de Configuration Manager a una ubicación de red, proteja la ubicación y el canal de red.**  

Restrinja quién puede tener acceso a la carpeta de red.  

Use la firma SMB o IPsec entre la ubicación de red y el servidor de sitio, y entre el equipo que ejecuta la consola de Configuration Manager y el servidor de sitio para impedir que un atacante manipule los datos exportados. Use IPsec para cifrar los datos en la red y así evitar la revelación de información.  

**Si un sistema de sitio no se puede desinstalar correctamente o deja de funcionar y no se puede restaurar, quite de forma manual los certificados de Configuration Manager para este servidor desde otros servidores de Configuration Manager.**  

Para quitar la confianza de mismo nivel establecida originalmente con el sistema de sitio y los roles de sistema de sitio, quite de forma manual los certificados de Configuration Manager del servidor que ha dado error en el almacén de certificados de **Personas de confianza** en otros servidores de sistema de sitio. Esto es especialmente importante si reasigna el servidor sin cambiar el formato.  

Para obtener más información sobre estos certificados, consulte la sección **Controles criptográficos para la comunicación de servidor** en [Referencia técnica para los controles criptográficos usados en Configuration Manager](../../../protect/deploy-use/cryptographic-controls-technical-reference.md).  

**No configure sistemas de sitio basados en Internet para enlazar la red perimetral y la intranet.**  

No configure servidores de sistema de sitio para que sean de hosts múltiples, para que se conecten a la red perimetral y la intranet. Aunque esta configuración permite que los sistemas de sitio basados en Internet acepten conexiones de clientes desde Internet y la intranet, se elimina un límite de seguridad entre la red perimetral y la intranet.  

**Si el servidor de sistema de sitio se encuentra en una red que no es de confianza (por ejemplo, una red perimetral), configure el servidor de sitio para iniciar conexiones al sistema de sitio.**  

De forma predeterminada, los sistemas de sitio inician conexiones con el servidor de sitio para transferir datos, lo que puede suponer un riesgo para la seguridad cuando la conexión se inicia en una red que no es de confianza y se dirige a una red de confianza. Cuando los sistemas de sitio aceptan conexiones desde Internet o se encuentran en un bosque que no es de confianza, configure la opción de sistema de sitio **Requerir al servidor de sitio iniciar conexiones a este sistema de sitio** de forma que, después de la instalación del sistema de sitio y cualquier rol de sistema de sitio, todas las conexiones se inicien desde una red de confianza.  

**Si utiliza un servidor proxy web para la administración de cliente basada en Internet, utilice el protocolo de puente de SSL a SSL, mediante el uso de la terminación con autenticación.**  

 Cuando configure la terminación SSL en el servidor proxy web, los paquetes de Internet están sujetos a inspección antes de que se reenvíen a la red interna. El servidor proxy web autentica la conexión desde el cliente, la termina y, a continuación, abre una nueva conexión autenticada para los sistemas de sitio basados en Internet.  

 Cuando los equipos cliente de Configuration Manager usan un servidor proxy web para conectarse a sistemas de sitio basados en Internet, la identidad del cliente (GUID de cliente) se incluye de forma segura en la carga de paquete para que el punto de administración no considere como cliente al servidor proxy web. Si el servidor proxy web no es compatible con los requisitos del protocolo de puente SSL, también se admite el protocolo de túnel SSL. Esta es una opción menos segura porque los paquetes SSL de Internet se reenvían a los sistemas de sitio sin terminación, por lo que no se puede comprobar si incluyen contenido malintencionado.  

 Si el servidor proxy web no es compatible con los requisitos del protocolo de puente SSL, puede utilizar el protocolo de túnel SSL. No obstante, esto es una opción menos segura porque los paquetes SSL de Internet se reenvían a los sistemas de sitio sin terminación, por lo que no se puede comprobar si incluyen contenido malintencionado.  

> [!WARNING]  
>  Los dispositivos móviles que están inscritos mediante Configuration Manager no pueden usar el protocolo de puente SSL y deben usar solo el protocolo de túnel SSL.  

**Configuraciones usadas si configura el sitio para reactivar equipos para instalar software.**  

-   Si usa paquetes de reactivación tradicionales, use la unidifusión en lugar de difusiones dirigidas a la subred.  

-   Si tiene que usar difusiones dirigidas a la subred, configure los enrutadores para permitir solo difusiones dirigidas de IP desde el servidor de sitio y solo en un número de puerto no predeterminado.  

Para obtener más información sobre las diferentes tecnologías de Wake on LAN, consulte [Planear la reactivación de clientes en System Center Configuration Manager](../../../core/clients/deploy/plan/plan-wake-up-clients.md).

**Si utiliza la notificación por correo electrónico, configure el acceso autenticado al servidor SMTP de correo electrónico.**  

Siempre que sea posible, use un servidor de correo compatible con el acceso autenticado y use la cuenta de equipo del servidor de sitio para la autenticación. Si debe especificar una cuenta de usuario para la autenticación, utilice una cuenta que tenga los privilegios mínimos.  

##  <a name="BKMK_Security_SiteServer"></a> Prácticas recomendadas de seguridad para el servidor de sitio  
 Use los siguientes procedimientos recomendados de seguridad para proteger el servidor de sitio de Configuration Manager.  

 **Instale Configuration Manager en un servidor miembro en lugar de en un controlador de dominio.**  

 No es necesario instalar los sistemas de sitio y el servidor de sitio de Configuration Manager en un controlador de dominio. Los controladores de dominio no tienen una base de datos de administración de cuentas de seguridad (SAM) local distinta de la base de datos de dominio. Cuando se instala Configuration Manager en un servidor miembro, se pueden mantener las cuentas de Configuration Manager en la base de datos SAM local en lugar de en la base de datos de dominio.  

 Esta práctica permite además reducir la superficie expuesta a ataques en los controladores de dominio.  

 **Al instalar sitios secundarios, evite copiar los archivos en el servidor de sitio secundario a través de la red.**  

 Cuando ejecute el programa de instalación y cree un sitio secundario, no seleccione la opción de copiar los archivos del sitio primario en el sitio secundario, ni use una ubicación de fuente de red. Si copia los archivos a través de la red, un atacante experimentado podría secuestrar el paquete de instalación del sitio secundario y alterar los archivos antes de que se instalen, aunque resultaría difícil sincronizar este tipo de ataque. Este ataque se puede mitigar mediante el uso de IPsec o SMB al transferir los archivos.  

 En lugar de copiar los archivos a través de la red, en el servidor de sitio secundario, copie los archivos de origen desde la carpeta de medios a una carpeta local. Después, cuando ejecute el programa de instalación para crear un sitio secundario, en la página **Archivos de origen de instalación**, seleccione **Usar los archivos de origen de la siguiente ubicación del equipo de sitio secundario (opción más segura)** y especifique esta carpeta.  

 Para obtener más información, consulte [Install a secondary site](../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_secondary) (Instalar un sitio secundario) en el tema [Use the Setup Wizard to install sites](../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md) (Uso del asistente para instalación para instalar sitios).  

##  <a name="BKMK_Security_SQLServer"></a> Prácticas recomendadas de seguridad para SQL Server  
 Configuration Manager usa SQL Server como base de datos back-end. Si la base de datos se ve comprometida, los atacantes podrían omitir Configuration Manager y obtener acceso a SQL Server directamente para lanzar sus ataques a través de Configuration Manager. Tenga en cuenta que los ataques contra SQL Server son de muy alto riesgo y deben mitigarse de forma adecuada.  

 Use los siguientes procedimientos recomendados de seguridad para proteger SQL Server para Configuration Manager.  

 **No use el servidor de base de datos de sitio de Configuration Manager para ejecutar otras aplicaciones de SQL Server.**  

 Al ampliar el acceso al servidor de base de datos de sitio de Configuration Manager, se incrementa el riesgo para los datos de Configuration Manager. Si la base de datos de sitio de Configuration Manager se ve comprometida, también estarán en peligro las demás aplicaciones del mismo equipo con SQL Server.  

 **Configure SQL Server para utilizar la autenticación de Windows.**  

 Aunque Configuration Manager obtenga acceso a la base de datos de sitio mediante una cuenta y autenticación de Windows, aún se puede configurar SQL Server para que use el modo mixto de SQL Server. El modo mixto de SQL Server permite inicios de sesión de SQL adicionales para obtener acceso a la base de datos, lo que no es necesario e incrementa la superficie expuesta a ataques.  

 **Tome medidas adicionales para asegurarse de que los sitios secundarios que utilizan SQL Server Express tienen las actualizaciones de software más recientes.**  

 Cuando se instala un sitio primario, Configuration Manager descarga SQL Server Express desde el Centro de descarga de Microsoft y copia los archivos en el servidor de sitio primario. Cuando se instala un sitio secundario y se selecciona la opción que permite instalar SQL Server Express, Configuration Manager instala la versión descargada anteriormente y no comprueba si hay nuevas versiones disponibles. Para asegurarse de que el sitio secundario tiene las versiones más recientes, realice una de las tareas siguientes:  

-   Una vez instalado el sitio secundario, ejecute Windows Update en el servidor de sitio secundario.  

-   Antes de instalar el sitio secundario, instale manualmente SQL Server Express en el equipo en el que se va a ejecutar el servidor de sitio secundario y asegúrese de instalar la versión más reciente y las actualizaciones de software correspondientes. Después, instale el sitio secundario y seleccione la opción de usar una instancia de SQL Server existente.  

Ejecute Windows Update periódicamente para estos sitios y todas las versiones instaladas de SQL Server para asegurarse de que disponen de las actualizaciones de software más recientes.  

**Siga las prácticas recomendadas para SQL Server.**  

Identifique y siga las prácticas recomendadas para su versión de SQL Server. En cambio, tenga en cuenta los siguientes requisitos de Configuration Manager:  

-   La cuenta de equipo del servidor de sitio debe ser miembro del grupo de administradores del equipo que ejecuta SQL Server. Si sigue la recomendación de SQL Server de "aprovisionar entidades de seguridad de administración explícitamente", la cuenta usada para ejecutar el programa de instalación en el servidor de sitio debe ser miembro del grupo de usuarios de SQL.  

-   Si instala SQL Server mediante una cuenta de usuario de dominio, asegúrese de que la cuenta de equipo del servidor de sitio está configurada para un nombre de entidad de seguridad de servicio (SPN) publicado en Servicios de dominio de Active Directory. Sin el SPN, se producirá un error en la autenticación Kerberos y se producirá un error en la instalación de Configuration Manager.  

##  <a name="BKMK_Security_IIS"></a> Prácticas recomendadas de seguridad para sistemas de sitio que ejecutan IIS  
Varios roles de sistema de sitio en Configuration Manager requieren IIS. El proceso de protección de IIS permite a Configuration Manager funcionar correctamente y reducir el riesgo de que se produzcan ataques de seguridad. Cuando resulte práctico, minimice el número de servidores que requieren IIS. Por ejemplo, ejecute sólo el número de puntos de administración que requiera para su base de clientes, teniendo en cuenta la alta disponibilidad y el aislamiento de red para la administración de cliente basada en Internet.  

 Utilice las siguientes prácticas recomendadas de seguridad para proteger los sistemas de sitio que ejecutan IIS.  

 **Deshabilite las funciones de IIS que no necesite.**  

 Instale sólo las funciones de IIS mínimas necesarias para el rol de sistema de sitio que vaya a instalar. Para obtener más información, consulte [Site and site system prerequisites](../../../core/plan-design/configs/site-and-site-system-prerequisites.md) (Requisitos previos de sitio y sistema de sitio).  

 **Configure los roles de sistema de sitio para que se requiera HTTPS.**  

 Cuando los clientes se conectan a un sistema de sitio mediante HTTP en lugar de HTTPS, utilizan la autenticación de Windows, que podría recurrir al uso de la autenticación NTLM en lugar de la autenticación Kerberos. Cuando se utiliza la autenticación NTLM, podría ocurrir que los clientes se conecten a un servidor no autorizado.  

 La excepción a esta práctica recomendada de seguridad podrían ser los puntos de distribución, porque las cuentas de acceso de paquetes no funcionan cuando el punto de distribución está configurado para HTTPS. Las cuentas de acceso de paquetes conceden autorización para el contenido, de modo que puede restringir qué usuarios pueden acceder al contenido. Para obtener más información, consulte [Prácticas recomendadas de seguridad para la administración de contenido](../../../core/plan-design/hierarchy/security-and-privacy-for-content-management.md#BKMK_Security_ContentManagement).  

**Configure una lista de certificados de confianza (CTL) en IIS para los roles de sistema de sitio.**  

Roles de sistema de sitio:  

-   Un punto de distribución que está configurado para HTTPS  

-   Un punto de administración que está configurado para HTTPS y es compatible con dispositivos móviles

Una lista de certificados de confianza (CTL) es una lista definida de entidades de certificación raíz de confianza. Si se usa una CTL con una directiva de grupo y una implementación de infraestructura de clave pública (PKI), la CTL permite complementar las entidades de certificación raíz de confianza existentes que están configuradas en la red, como por ejemplo las que se instalan automáticamente con Microsoft Windows o se agregan a través de las entidades de certificación raíz de empresa de Windows. En cambio, cuando se configura una CTL en IIS, esta define un subconjunto de dichas entidades de certificación raíz de confianza.  

Este subconjunto facilita un mayor control de la seguridad, ya que la CTL limita los certificados de cliente que se aceptan a los que son emitidos por las entidades de certificación de la CTL únicamente. Por ejemplo, Windows se comercializa con varios certificados de conocidas entidades de certificación de terceros, como VeriSign y Thawte.

De forma predeterminada, el equipo que ejecuta IIS confía en los certificados que están vinculados a estas conocidas entidades de certificación. Si no configura IIS con una CTL para los roles de sistema de sitio enumerados, cualquier dispositivo que tenga un certificado de cliente emitido por estas entidades de certificación se aceptará como un cliente válido de Configuration Manager. Si configura IIS con una CTL que no incluya estas entidades de certificación, se rechazarán las conexiones de cliente si el certificado está vinculado a estas entidades de certificación. En cambio, para que se acepten los clientes de Configuration Manager para los roles de sistema de sitio enumerados, debe configurar IIS con una CTL que especifique las entidades de certificación usadas por los clientes de Configuration Manager.  

> [!NOTE]  
>  Solo los roles de sistema de sitio enumerados requieren la configuración de una CTL en IIS. La lista de emisores de certificados que Configuration Manager usa para los puntos de administración proporciona la misma funcionalidad para los equipos cliente cuando se conectan a puntos de administración de HTTPS.  

Para obtener más información acerca de cómo configurar una lista de entidades de certificación de confianza en IIS, consulte la documentación de IIS.  

**No ponga el servidor de sitio en un equipo con IIS.**  

La separación de roles ayuda a reducir el perfil de ataque y a mejorar la capacidad de recuperación. Además, la cuenta de equipo del servidor de sitio suele tener privilegios administrativos en todos los roles de sistema de sitio (y posiblemente en los clientes de Configuration Manager, si se usa la instalación de inserción de cliente).  

**Use servidores IIS dedicados para Configuration Manager.**  

Aunque puede hospedar varias aplicaciones web en los servidores IIS que también usa Configuration Manager, esto puede ocasionar un aumento significativo de la superficie expuesta a ataques. La configuración incorrecta de una aplicación podría facilitar que un atacante asumiera el control de un sistema de sitio de Configuration Manager, lo que a su vez podría ocasionar que un atacante asumiera el control de la jerarquía.  

Si debe ejecutar otras aplicaciones web en los sistemas de sitio de Configuration Manager, cree un sitio web personalizado para los sistemas de sitio de Configuration Manager.  

**Use un sitio web personalizado.**  

Para los sistemas de sitio que ejecutan IIS, se puede configurar Configuration Manager para que use un sitio web personalizado en lugar del sitio web predeterminado para IIS. Si tiene que ejecutar otras aplicaciones web en el sistema de sitio, debe usar un sitio web personalizado. Se trata de una configuración para todo el sitio en lugar de una configuración para un sistema de sitio específico.  

Además de proporcionar seguridad adicional, debe utilizar un sitio web personalizado si ejecuta otras aplicaciones web en el sistema de sitio.  

**Si pasa de utilizar el sitio web predeterminado a utilizar un sitio web personalizado una vez instalados los roles de punto de distribución, quite los directorios virtuales predeterminados.**  

Cuando se pasa de usar el sitio web predeterminado a usar un sitio web personalizado, Configuration Manager no quita los directorios virtuales antiguos. Quite los directorios virtuales que Configuration Manager creó originalmente en el sitio web predeterminado.  

Por ejemplo, los directorios virtuales que se deben quitar de un punto de distribución son los siguientes:  

-   SMS_DP_SMSPKG$  

-   SMS_DP_SMSSIG$  

-   NOCERT_SMS_DP_SMSPKG$  

-   NOCERT_SMS_DP_SMSSIG$  

**Siga las prácticas recomendadas para el servidor IIS.**  

Identifique y siga las prácticas recomendadas para su versión del servidor IIS. En cambio, debe tener en cuenta cualquier requisito que Configuration Manager tenga en cuanto a los roles de sistema de sitio específicos. Para obtener más información, consulte [Site and site system prerequisites](../../../core/plan-design/configs/site-and-site-system-prerequisites.md) (Requisitos previos de sitio y sistema de sitio).  

##  <a name="BKMK_Security_ManagementPoint"></a> Prácticas recomendadas de seguridad para el punto de administración  
 Los puntos de administración son la interfaz principal entre los dispositivos y Configuration Manager. Tenga en cuenta que los ataques contra el punto de administración y el servidor en el que se ejecuta son de muy alto riesgo y deben mitigarse de forma adecuada. Aplique todas las prácticas recomendadas de seguridad adecuadas y compruebe si se detecta actividad inusual.  

 Use los siguientes procedimientos recomendados de seguridad para proteger un punto de administración de Configuration Manager.  

**Cuando instale un cliente de Configuration Manager en el punto de administración, asígnelo al sitio de ese punto de administración.**  

 Evite que un cliente de Configuration Manager que está en un sistema de sitio del punto de administración se asigne a un sitio que no sea el sitio del punto de administración.  

 Si migra desde una versión anterior a System Center Configuration Manager, migre el software cliente del punto de administración a System Center Configuration Manager lo antes posible.  

##  <a name="BKMK_Security_FSP"></a> Prácticas recomendadas de seguridad para el punto de estado de reserva  
 Use los siguientes procedimientos recomendados de seguridad si instala un punto de estado de reserva en Configuration Manager.  

 Para obtener más información sobre las consideraciones de seguridad al instalar un punto de estado de reserva, consulte [Determine Whether You Require a Fallback Status Point](../../../core/clients/deploy/plan/determine-the-site-system-roles-for-clients.md#determine-if-you-need-a-fallback-status-point) (Determinar si necesita un punto de estado de reserva).  


**No ejecute otros roles de sistema de sitio en el sistema del sitio y no instale el punto de estado de reserva en un controlador de dominio.**  

 El punto de estado de reserva está diseñado para aceptar comunicación sin autenticar de cualquier equipo, por lo que si ejecuta este rol de sistema de sitio con otros roles de sistema de sitio o en un controlador de dominio aumentará significativamente el riesgo para ese servidor.  

**Si usa certificados PKI para la comunicación de cliente en Configuration Manager, instale el punto de estado de reserva antes de instalar los clientes.**  

 Si los sistemas de sitio de Configuration Manager no aceptan la comunicación de cliente HTTP, podría ignorar que los clientes no se administran a causa de problemas de certificados relacionados con PKI. En cambio, si los clientes se asignan a un punto de estado de reserva, el punto de estado de reserva notificará dichos problemas de certificados.  

 Por motivos de seguridad, no se puede asignar un punto de estado de reserva a los clientes después de la instalación. En su lugar, solo se puede asignar este rol durante la instalación del cliente.  

**Evite usar el punto de estado de reserva en la red perimetral.**  

 Por motivos de diseño, el punto de estado de reserva acepta datos de cualquier cliente. Aunque un punto de estado de reserva en la red perimetral puede ayudarle a solucionar problemas de clientes basados en Internet, debe buscar el equilibrio entre las ventajas que comporta la solución de problemas y el riesgo que implica un sistema de sitio que acepta datos no autenticados en una red de acceso público.  

 Si instala el punto de estado de reserva en la red perimetral o en una red que no es de confianza, configure el servidor de sitio para iniciar las transferencias de datos, en vez de usar la configuración predeterminada que permite al punto de estado de reserva iniciar una conexión con el servidor de sitio.  

##  <a name="BKMK_SecurityIssues_Clients"></a> Problemas de seguridad para la administración de sitios  
 Revise los siguientes problemas de seguridad de Configuration Manager:  

-   Configuration Manager no tiene ninguna defensa contra usuarios administrativos que usan Configuration Manager para atacar la red. Los usuarios administrativos no autorizados son un importante riesgo de seguridad y podrían iniciar numerosos tipos de ataques, que incluyen las estrategias siguientes:  

    -   Usar la implementación de software para instalar y ejecutar de forma automática software malintencionado en cada equipo cliente de Configuration Manager de la empresa.  

    -   Usar el control remoto para controlar de forma remota un cliente de Configuration Manager sin permiso del cliente.  

    -   Configurar intervalos de sondeo de gran velocidad y cantidades de inventario excesivas para crear ataques de denegación de servicio contra clientes y servidores.  

    -   Utilizar un sitio en la jerarquía para escribir datos en los datos de Active Directory de otro sitio.  

    La jerarquía de sitios es el límite de seguridad. Considere que los sitios solo son límites de administración.  

    Audite la actividad de todos los usuarios administrativos y revise los registros de auditoría con regularidad. Requiera la realización de comprobaciones de antecedentes de todos los usuarios administrativos de Configuration Manager y exija comprobaciones periódicas como requisito contractual.  

-   Si el punto de inscripción se ve comprometido, un atacante podría obtener certificados para la autenticación y robar las credenciales de los usuarios que inscriben sus dispositivos móviles.  

    El punto de inscripción se comunica con una entidad de certificación y puede crear, modificar y eliminar objetos de Active Directory. Nunca instale el punto de inscripción en la red perimetral y busque siempre cualquier actividad inusual.  

-   Si se permiten las directivas de usuario para la administración de cliente basada en Internet o se configura el punto de sitios web del catálogo de aplicaciones para los usuarios cuando se encuentran en Internet, su perfil de ataque aumenta.  

    Además de utilizar certificados PKI para las conexiones de cliente y servidor, estas configuraciones requieren autenticación de Windows, que puede tener que utilizar la autenticación NTLM en lugar de Kerberos. La autenticación NTLM es vulnerable a ataques de suplantación de identidad y reproducción. Para autenticar correctamente a un usuario en Internet, debe permitir una conexión entre el servidor de sistema de sitio basado en Internet y un controlador de dominio.  

-   Se requiere el recurso compartido Admin$ en servidores de sistema de sitio.  

    El servidor de sitio de Configuration Manager usa el recurso compartido Admin$ para conectarse y realizar operaciones de servicio en sistemas de sitio. No deshabilite o quite el recurso compartido Admin$.  

-   Configuration Manager usa servicios de resolución de nombres para conectarse a otros equipos y es difícil proteger estos servicios contra ataques de seguridad como la suplantación de identidad, la manipulación, el rechazo, la divulgación de información, la denegación de servicio y la elevación de privilegios.  

    Identifique y siga las recomendaciones de seguridad de la versión de DNS y WINS que utiliza para la resolución de nombres.  

##  <a name="BKMK_Privacy_Cliients"></a> Información de privacidad para la detección  
 La detección crea registros de recursos de red y los almacena en la base de datos de System Center Configuration Manager. Los registros de datos de detección contienen información del equipo como direcciones IP, sistemas operativos y nombres de equipo. Los métodos de detección de Active Directory también se pueden configurar para detectar información almacenada en los Servicios de dominio de Active Directory.  

 El único método de detección habilitado de manera predeterminada es la detección de latidos. En cambio, este método solo detecta equipos que ya tienen el software cliente de System Center Configuration Manager instalado.  

 La información de detección no se envía a Microsoft. En su lugar, se almacena en la base de datos de Configuration Manager. La información se conserva en la base de datos hasta que la tarea de mantenimiento del sitio **Eliminar datos de detección antiguos** la elimina cada 90 días.  

 Antes de configurar métodos de detección adicionales o extender la detección de Active Directory, tenga en cuenta los requisitos de privacidad.  

