---
title: Comunicaciones entre puntos de conexión
titleSuffix: Configuration Manager
description: Aprenda cómo se comunican los componentes y sistemas de sitio de System Center Configuration Manager a través de una red.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 68fe0e7e-351e-4222-853a-877475adb589
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 603adb982f704c462e043d8c0974fc85a0748863
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32341447"
---
# <a name="communications-between-endpoints-in-system-center-configuration-manager"></a>Comunicaciones entre puntos de conexión en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*


##  <a name="Planning_Intra-site_Com"></a> Comunicaciones entre sistemas de sitio de un sitio  
 Cuando los sistemas de sitio o los componentes de Configuration Manager se comunican a través de la red con otros sistemas de sitio u otros componentes de Configuration Manager del sitio, usan uno de los siguientes protocolos, según la configuración del sitio:  

-   Bloque de mensajes del servidor (SMB)  

-   HTTP  

-   HTTPS  

Con la excepción de la comunicación desde el servidor de sitio a un punto de distribución, las comunicaciones entre los servidores de un sitio se pueden producir en cualquier momento y no usan mecanismos para controlar el ancho de banda de red. Ya que no es posible controlar la comunicación entre sistemas de sitio, asegúrese de instalar servidores de sistema de sitio en ubicaciones que cuenten con redes rápidas y bien conectadas.  

Para administrar fácilmente la transferencia de contenido desde el servidor de sitio a los puntos de distribución:  

-   Configurar el punto de distribución para el control de ancho de banda de red y la programación. Estos controles son similares a las configuraciones usadas por las direcciones entre sitios, por lo que a menudo se puede usar esta configuración en lugar de instalar otro sitio de Configuration Manager cuando la transferencia de contenido a ubicaciones de red remotas es la principal consideración de ancho de banda.  

-   Es posible instalar un punto de distribución como un punto de distribución preconfigurado. Un punto de distribución preconfigurado le permite utilizar el contenido que se coloca manualmente en el servidor de punto de distribución y elimina el requisito de transferir archivos de contenido a través de la red.  

Para más información, vea [Administración del ancho de banda de red para la administración de contenido](manage-network-bandwidth.md).


##  <a name="Planning_Client_to_Site_System"></a> Comunicaciones desde los clientes a los sistemas de sitio y servicios  
Los clientes inician comunicaciones con roles de sistema de sitio, con Servicios de dominio de Active Directory y con servicios en línea. A fin de permitir estas comunicaciones, los firewalls deben permitir el tráfico de red entre los clientes y el extremo de sus comunicaciones. Estos extremos pueden ser los siguientes:  

-   **Punto de sitios web del catálogo de aplicaciones**: admite la comunicación HTTP y HTTPS

-   **Recursos basados en la nube**: incluye Microsoft Azure y Microsoft Intune  

-   **Módulo de directivas de Configuration Manager (NDES)**: admite la comunicación HTTP y HTTPS

-   **Puntos de distribución**: admite la comunicación HTTP y HTTPS, y los puntos de distribución basados en la nube requieren HTTPS  

-   **Punto de estado de reserva**: admite la comunicación HTTP  

-   **Punto de administración**: admite la comunicación HTTP y HTTPS  

-   **Microsoft Update**  

-   **Puntos de actualización de software**: admite la comunicación HTTP y HTTPS  

-   **Punto de migración de estado**: admite la comunicación HTTP y HTTPS  

-   **Distintos servicios de dominio**  

Para que un cliente pueda comunicarse con un rol de sistema de sitio, el cliente usa la ubicación del servicio para encontrar un rol de sistema de sitio que admita el protocolo del cliente (HTTP o HTTPS). De forma predeterminada, los clientes usan el método más seguro que tengan a su disposición:  

-   Para usar HTTPS, es necesario disponer de una infraestructura de clave pública (PKI) e instalar certificados PKI en los clientes y servidores. Para más información sobre el uso de certificados, consulte [Requisitos de certificados PKI para System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md).  

-   Cuando se implementa un rol de sistema de sitio que usa Internet Information Services (IIS) y que admite la comunicación desde clientes, es necesario especificar si los clientes se conectan al sistema de sitio mediante HTTP o HTTPS. Si utiliza HTTP, también debe tener en cuenta las opciones de firma y cifrado. Para más información, vea [Planeación de la firma y el cifrado](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForSigningEncryption) en [Planificar la seguridad en System Center Configuration Manager](../../../core/plan-design/security/plan-for-security.md).  

Para más información sobre la ubicación del servicio por clientes, consulte [Comprender cómo los clientes buscan servicios y recursos de sitio para System Center Configuration Manager](../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

Para más información sobre los puertos y protocolos que los clientes usan al comunicarse con estos puntos de conexión, vea [Puertos que se usan en System Center Configuration Manager](../../../core/plan-design/hierarchy/ports.md).  

###  <a name="BKMK_clientspan"></a> Consideraciones sobre las comunicaciones de cliente desde Internet o desde un bosque que no es de confianza  
Los siguientes roles de sistema de sitio instalados en los sitios primarios admiten conexiones provenientes de clientes que se encuentran en ubicaciones que no son de confianza, como Internet o un bosque que no es de confianza. (Los sitios secundarios no admiten conexiones de cliente desde ubicaciones que no son de confianza):  

-   Punto de sitios web del catálogo de aplicaciones  

-   Módulo de directivas de Configuration Manager  

-   Punto de distribución (los puntos de distribución basados en la nube requieren HTTPS)  

-   Punto de proxy de inscripción  

-   Punto de estado de reserva  

-   Punto de administración  

-   Punto de actualización de software  

**Sobre los sistemas de sitio con conexión a Internet:**   
No es necesario tener una relación de confianza entre el bosque de un cliente y el de un servidor de sistema de sitio. Pero cuando el bosque que contiene un sistema de sitio con conexión a Internet confía en el bosque que contiene las cuentas de usuario, esta configuración admite directivas basadas en usuario para los dispositivos en Internet si se habilita la configuración de cliente de **directiva de cliente** **Habilitar solicitudes de directiva de usuario de clientes de Internet**.  

Por ejemplo, las configuraciones siguientes ilustran cuándo la administración de cliente basada en Internet es compatible con las directivas de usuario para dispositivos de Internet:  

-   El punto de administración basado en Internet se encuentra en la red perimetral, donde se encuentra un controlador de dominio de solo lectura para autenticar al usuario, y el firewall que interviene admite los paquetes de Active Directory.  

-   La cuenta de usuario está en el bosque A (la intranet) y el punto de administración basado en Internet se encuentra en el bosque B (la red perimetral). El bosque B confía en el bosque A y el firewall que interviene admite los paquetes de autenticación.  

-   La cuenta de usuario y el punto de administración basado en Internet están en el bosque A (la intranet). El punto de administración se publica en Internet mediante el uso de un servidor proxy web (como Forefront Threat Management Gateway).  

> [!NOTE]  
>  Si se produce un error en la autenticación Kerberos, a continuación, se intenta automáticamente la autenticación NTLM.  

Como se muestra en el ejemplo anterior, es posible colocar sistemas de sitio basados en Internet en la intranet cuando están publicados en Internet mediante un servidor proxy web, como ISA Server y Forefront Threat Management Gateway. Estos sistemas de sitio pueden configurarse para conexión de cliente solo desde Internet, o para conexiones de cliente desde Internet e intranet. Cuando se usa un servidor proxy web, puede configurarlo para protocolo de puente de Capa de sockets seguros (SSL) a SSL (más seguro) o protocolo de túnel SSL de esta forma:  

-   **Protocolo de puente SSL a SSL:**   
    La configuración recomendada cuando se usan servidores proxy web para la administración de clientes basada en Internet es el protocolo de puente SSL a SSL, que usa la terminación SSL con autenticación. Los equipos cliente deben ser autenticados mediante autenticación de equipo, mientras que los clientes heredados de dispositivos móviles se autentican mediante autenticación de usuario. Los dispositivos móviles inscritos por Configuration Manager no son compatibles con el protocolo de puente SSL.  

     La ventaja de terminación SSL en el servidor proxy web es que los paquetes de Internet están sujetos a inspección antes de que se reenvíen a la red interna. El servidor proxy web autentica la conexión desde el cliente, la termina y, a continuación, abre una nueva conexión autenticada para los sistemas de sitio basados en Internet. Cuando los clientes de Configuration Manager usan un servidor proxy web, la identidad del cliente (GUID de cliente) se incluye de forma segura en la carga de paquete para que el punto de administración no considere como cliente al servidor proxy web. En Configuration Manager no se admite el protocolo de puente con HTTP a HTTPS o de HTTPS a HTTP.  

-   **Protocolo de túnel**:   
    Si su servidor proxy web no puede admitir los requisitos del protocolo de puente SSL o si quiere configurar la compatibilidad con Internet para dispositivos móviles inscritos por Configuration Manager, también se admite el protocolo de túnel SSL. Esto es una opción menos segura porque los paquetes SSL de Internet se reenvían a los sistemas de sitio sin terminación SSL, por lo que no se puede comprobar si incluyen contenido malintencionado. Cuando se utiliza el protocolo de túnel SSL, no hay ningún requisito de certificado para el servidor proxy web.  

##  <a name="Plan_Com_X-Forest"></a> Comunicaciones entre bosques de Active Directory  
System Center Configuration Manager es compatible con sitios y jerarquías que se distribuyen por bosques de Active Directory.  

Configuration Manager también admite equipos de dominio que no están en el mismo bosque de Active Directory que el servidor de sitio, y equipos que están en grupos de trabajo:  

-   **Para que el bosque del servidor de sitio admita equipos de dominio en un bosque que no es de confianza**, puede hacer lo siguiente:  

    -   Instalar roles de sistema de sitio en ese bosque que no es de confianza, con la opción para publicar información del sitio en ese bosque de Active Directory.  

    -   Administrar estos equipos como si fueran equipos de grupo de trabajo.  

  Cuando se instalan servidores de sistema de sitio en un bosque de Active Directory que no es de confianza, la comunicación entre cliente y servidor desde los clientes de dicho bosque se mantiene en ese bosque y Configuration Manager puede autenticar el equipo mediante Kerberos. Cuando se publica información del sitio en el bosque del cliente, los clientes se benefician de la posibilidad de recuperar información del sitio, como una lista de los puntos de administración disponibles, desde su bosque de Active Directory, en lugar de tener que descargar esta información desde su punto de administración asignado.  

  > [!NOTE]  
  >  Si desea administrar dispositivos que están en Internet, puede instalar roles de sistema de sitio basados en Internet en su red perimetral cuando los servidores de sistema de sitio estén en un bosque de Active Directory. Este escenario no requiere una confianza bidireccional entre la red perimetral y el bosque del servidor de sitio.  

-   **Para admitir equipos en un grupo de trabajo**, debe:  

    -   Aprobar manualmente los equipos del grupo de trabajo cuando usen conexiones de cliente HTTP en roles de sistema de sitio. El motivo es que Configuration Manager no puede autenticar estos equipos mediante Kerberos.  

    -   Configure los clientes del grupo de trabajo para usar la cuenta de acceso a la red para que estos equipos puedan recuperar contenido de los puntos de distribución.  

    -   Proporcione un mecanismo alternativo para que los clientes del grupo de trabajo puedan buscar los puntos de administración. Puede usar publicación en DNS, WINS o asignar directamente un punto de administración. Esto se debe a que estos clientes no pueden recuperar la información de sitio de Servicios de dominio de Active Directory.  

    Recursos relacionados de esta biblioteca de contenido:  

    -   [Administrar registros en conflicto para clientes de Configuration Manager](../../../core/clients/manage/manage-clients.md#BKMK_ConflictingRecords)  

    -   [Cuenta de acceso a la red](../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#accounts-used-for-content-management)  

    -   [How to Install Configuration Manager Clients on Workgroup Computers (Cómo instalar clientes de Configuration Manager en equipos de grupo de trabajo)](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientWorkgroup)  

###  <a name="bkmk_span"></a> Escenarios para admitir un sitio o una jerarquía que abarca varios dominios y bosques  

#### <a name="communication-between-sites-in-a-hierarchy-that-spans-forests"></a>Comunicación entre sitios en una jerarquía que abarca bosques  
Este escenario requiere una confianza de bosque bidireccional que admita la autenticación Kerberos.  Si no dispone de una confianza de bosque bidireccional que admita la autenticación Kerberos, Configuration Manager no admitirá un sitio secundario en el bosque remoto.  

 **Configuration Manager admite la instalación de un sitio secundario en un bosque remoto que tenga la confianza bidireccional necesaria con el bosque del sitio primario**  

-   Por ejemplo, puede colocar un sitio secundario en un bosque diferente al del sitio primario principal siempre y cuando exista la confianza necesaria.  

> [!NOTE]  
>  Un sitio secundario puede ser un sitio primario (donde el sitio de administración central es el sitio principal), o un sitio secundario.  

La comunicación entre sitios de Configuration Manager usa replicación de base de datos y transferencias basadas en archivos. Cuando se instala un sitio, se debe especificar una cuenta con la que instalar el sitio en el servidor designado. Esta cuenta también establece y mantiene la comunicación entre sitios.  

Una vez que el sitio se instala correctamente e inicia las transferencias basadas en archivos y la replicación de base de datos, no es necesario configurar nada más para la comunicación con el sitio.  

**Cuando existe una confianza de bosque bidireccional, Configuration Manager no exige ningún paso de configuración adicional.**  

De forma predeterminada, al instalar un nuevo sitio como un elemento secundario de otro sitio, Configuration Manager configura lo siguiente:  

-   Una ruta de replicación basada en archivos entre sitios en cada sitio que use la cuenta de equipo del servidor de sitio. Configuration Manager agrega la cuenta de equipo de cada equipo al grupo **SMS_SiteToSiteConnection_&lt;código de sitio\>** en el equipo de destino.  

-   Una replicación de base de datos entre el servidor SQL Server de cada sitio.  

También se deben realizar las siguientes configuraciones:  

-   Los firewalls y dispositivos de red que intervienen deben permitir los paquetes de red que Configuration Manager necesita.  

-   La resolución de nombres debe funcionar entre los bosques.  

-   Para instalar un sitio o un rol de sistema de sitio, debe especificar una cuenta que tenga permisos de administrador local en el equipo especificado.  

#### <a name="communication-in-a-site-that-spans-forests"></a>La comunicación en un sitio que abarca bosques  
Este escenario no requiere una confianza de bosque bidireccional.  

**Los sitios primarios admiten la instalación de roles de sistema de sitio en equipos de bosques remotos**.  

-   El punto de servicio web del catálogo de aplicaciones es la única excepción.  Solo se admite en el mismo bosque que el servidor de sitio.  

-   Cuando el rol de sistema de sitio acepta conexiones de Internet, por motivos de seguridad se recomienda instalar los roles de sistema de sitio en una ubicación donde los límites del bosque proporcionen protección al servidor de sitio (por ejemplo, en una red perimetral).  

**Para instalar un rol de sistema de sitio en un equipo de un bosque que no es de confianza:**  

-   Hay que especificar una **cuenta de instalación del sistema de sitio**, que se usa para instalar el rol de sistema de sitio. (Esta cuenta debe tener privilegios administrativos locales para la conexión). Después, instale los roles de sistema de sitio en el equipo especificado.  

-   Hay que seleccionar la opción de sistema de sitio **Requerir al servidor de sitio iniciar conexiones a este sistema de sitio**. Esto permite al servidor del sitio establecer conexiones con el servidor de sistema de sitio para transferir datos. Esto impide que el equipo en la ubicación que no es de confianza inicie contacto con el servidor de sitio que está dentro de su red de confianza. Estas conexiones usan la **cuenta de instalación del sistema de sitio**.  

**Para usar un rol de sistema de sitio instalado en un bosque que no es de confianza,** los firewalls deben permitir el tráfico de red aunque el servidor de sitio inicie la transferencia de datos.  

Además, los siguientes roles de sistema de sitio requieren acceso directo a la base de datos del sitio. Por tanto, los firewalls deben permitir el tráfico pertinente desde el bosque que no es de confianza hasta SQL Server en el sitio:  

-   Punto de sincronización de Asset Intelligence  

-   Punto de Endpoint Protection  

-   Punto de inscripción  

-   Punto de administración  

-   Punto de servicio de informes  

-   Punto de migración de estado  

Para más información, vea [Puertos que se usan en System Center Configuration Manager](../../../core/plan-design/hierarchy/ports.md).  

**Tal vez necesite configurar el acceso del rol de sistema de sitio a la base de datos del sitio:**  

Ambos roles de sistema de sitio de punto de administración y punto de inscripción se conectan a la base de datos del sitio.  

-   De forma predeterminada, cuando estos roles de sistema de sitio están instalados, Configuration Manager configura la cuenta de equipo del nuevo servidor de sistema de sitio como la cuenta de conexión para el rol de sistema de sitio y después agrega la cuenta al rol de base de datos de SQL Server apropiado.  

-   Cuando se instalan estos roles de sistema de sitio en un dominio que no es de confianza, se debe configurar la cuenta de conexión del rol de sistema de sitio para que permita al rol obtener información de la base de datos.  

Si configura una cuenta de usuario de dominio para que sea la cuenta de conexión para estos roles de sistema de sitio, asegúrese de que la cuenta de usuario de dominio tenga acceso adecuado a la base de datos de SQL Server en ese sitio:  

-   Punto de administración: **Cuenta de conexión a la base de datos del punto de administración**  

-   Punto de inscripción: **Cuenta de conexión de punto de inscripción**  

Tenga en cuenta la siguiente información adicional cuando planee roles de sistema de sitio en otros bosques:  

-   Si ejecuta Firewall de Windows, configure los perfiles de firewall aplicables para que pueda haber comunicación entre el servidor de base de datos de sitio y los equipos instalados con roles de sistema de sitio remoto. Para más información sobre los perfiles de firewall, vea [Descripción de los perfiles de firewall](http://go.microsoft.com/fwlink/p/?LinkId=233629).  

-   Cuando el punto de administración basado en Internet confía en el bosque que contiene las cuentas de usuario, se admiten las directivas de usuario. Cuando no existe confianza, solo se admiten las directivas de equipo.  

#### <a name="communication-between-clients-and-site-system-roles-when-the-clients-are-not-in-the-same-active-directory-forest-as-their-site-server"></a>Comunicación entre clientes y roles de sistema de sitio cuando los clientes no están en el mismo bosque de Active Directory que su servidor de sitio  
Configuration Manager admite los siguientes escenarios para los clientes que no están en el mismo bosque que el servidor de sitio de su sitio:  

-   Hay una confianza de bosque bidireccional entre el bosque del cliente y el bosque del servidor de sitio.  

-   El servidor de rol de sistema de sitio se encuentra en el mismo bosque que el cliente.  

-   El cliente está en un equipo de dominio que no tiene una confianza de bosque bidireccional con el servidor de sitio y los roles de sistema de sitio no están instalados en el bosque del cliente.  

-   El cliente está en un equipo de grupo de trabajo.  

Los clientes de un equipo unido a un dominio pueden usar Servicios de dominio de Active Directory para la ubicación del servicio cuando su sitio se publica en el bosque de Active Directory.  

Para publicar información del sitio en otro bosque de Active Directory, debe realizar lo siguiente:  

-   Especificar el bosque y, a continuación, habilitar la publicación en ese bosque en el nodo **Bosques de Active Directory** del área de trabajo **Administración** .  

-   Configurar cada sitio para publicar sus datos en Servicios de dominio de Active Directory. Esta configuración permite a los clientes de ese bosque recuperar información del sitio y buscar puntos de administración. Para los clientes que no pueden usar Active Directory Domain Services para la ubicación del servicio, se puede usar DNS, WINS o el punto de administración asignado del cliente.  

###  <a name="bkmk_xchange"></a> Colocar el conector de Exchange Server en un bosque remoto  
Para admitir este escenario, asegúrese de que la resolución de nombres funcione a través de los bosques (por ejemplo, configure los reenvíos de DNS) y especifique el FQDN de la intranet del servidor Exchange Server al configurar el conector de Exchange Server. Para más información, consulte [Administrar dispositivos móviles mediante System Center Configuration Manager y Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  
