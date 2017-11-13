---
title: Seguridad y privacidad de los clientes
titleSuffix: Configuration Manager
description: "Obtenga información sobre la seguridad y privacidad de los clientes en System Center Configuration Manager."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: c1d71899-308f-49d5-adfa-3a3ec0163ed8
caps.latest.revision: "10"
caps.handback.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: b28a461894bcd1cffd3c98bfce9fcfe22cc7a8f0
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/12/2017
---
# <a name="security-and-privacy-for-clients-in-system-center-configuration-manager"></a>Seguridad y privacidad para clientes en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Este artículo contiene información de seguridad y privacidad para clientes de System Center Configuration Manager y para dispositivos móviles administrados mediante el conector de Exchange Server:  

##  <a name="BKMK_Security_Cliients"></a> Prácticas recomendadas de seguridad para clientes  
 Cuando Configuration Manager acepta datos de dispositivos que ejecutan el cliente de Configuration Manager, existe el riesgo de que los clientes ataquen el sitio. Por ejemplo, podrían enviar un inventario con formato incorrecto o intentar sobrecargar los sistemas de sitio. Implemente el cliente de Configuration Manager únicamente en dispositivos fiables. Además, utilice las siguientes prácticas recomendadas de seguridad para proteger el sitio de dispositivos no autorizados o comprometidos:  

 **Use certificados de infraestructura de claves públicas (PKI) para las comunicaciones de cliente con sistemas de sitio que ejecutan IIS.**  

-   Como una propiedad de sitio, configure **Configuración de sistema de sitio** para **HTTPS solamente**.  

-   Instale los clientes con la propiedad **/UsePKICert** de CCMSetup.  

-   Utilice una lista de revocación de certificados (CRL) y asegúrese de que los clientes y los servidores de comunicación puedan acceder siempre a la misma.  

 Estos certificados son necesarios para los clientes de dispositivos móviles y para las conexiones de equipos cliente en Internet y, a excepción de los puntos de distribución, se recomiendan para todas las conexiones de cliente en la intranet.  

 Para obtener más información sobre los requisitos de los certificados PKI y sobre cómo se usan para proteger Configuration Manager, consulte [Requisitos de certificados PKI para System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

 **Apruebe automáticamente los equipos cliente de dominios de confianza y compruebe y apruebe manualmente los demás equipos**  

 Puede configurar la aprobación para la jerarquía como manual, automática para equipos de dominios de confianza o automática para todos los equipos. El método de aprobación más seguro consiste en aprobar automáticamente los clientes que son miembros de dominios de confianza y, a continuación, comprobar y aprobar manualmente todos los demás equipos. No se recomienda aprobar automáticamente todos los clientes a menos que disponga de otros controles de acceso para evitar que los equipos no confiables accedan a la red.  

 Con la aprobación se identifica un equipo cuando se confía en que está administrado por Configuration Manager si no se puede utilizar la autenticación PKI.  

 Para obtener más información sobre cómo aprobar equipos manualmente, consulte [Manage Clients from the Devices Node](../../../../core/clients/manage/manage-clients.md#BKMK_ManagingClients_DevicesNode) (Administrar clientes desde el nodo Dispositivos).  

 **No utilice el bloqueo para evitar que los clientes accedan a la jerarquía de Configuration Manager**  

 Los clientes bloqueados son rechazados por la infraestructura de Configuration Manager para que no se puedan comunicar con los sistemas de sitio para descargar directivas, cargar datos de inventario o enviar mensajes de estado. De todas formas, no debe usar el bloqueo para proteger la jerarquía de Configuration Manager de equipos no confiables cuando los sistemas de sitio aceptan conexiones de cliente HTTP. En este escenario, un cliente bloqueado podría volver a unirse al sitio con un nuevo certificado autofirmado e identificador de hardware. El bloqueo está diseñado para bloquear medios de arranque perdidos o comprometidos cuando se implementa un sistema operativo en clientes y cuando todos los sistemas de sitio aceptan conexiones de cliente de HTTPS. Si utiliza una infraestructura de clave pública (PKI) compatible con una lista de revocación de certificados (CRL), considere siempre la revocación de certificados como la primera línea de defensa contra certificados que puedan estar comprometidos. El bloqueo de clientes en Configuration Manager ofrece una segunda línea de defensa para proteger la jerarquía.  

 Para obtener más información, consulte [Determine whether to block clients in System Center Configuration Manager](../../../../core/clients/deploy/plan/determine-whether-to-block-clients.md) (Determinar si se deben bloquear clientes en System Center Configuration Manager).  

 **Utilice los métodos de instalación de cliente más seguros que sean prácticos para su entorno:**  

-   Para los equipos de dominio, los métodos de instalación de clientes con directiva de grupo y de instalación de clientes basada en actualizaciones de software son más seguros que la instalación de inserción de cliente.  

-   La creación de imágenes y la instalación manual pueden ser muy seguras si aplica controles de acceso y controles de cambios.  

 De todos los métodos de instalación de clientes, la instalación de inserción de cliente es el menos seguro debido a sus numerosas dependencias, que incluyen los permisos administrativos locales, el recurso compartido Admin$ y numerosas excepciones de firewall. Estas dependencias ocasionan un aumento de la superficie expuesta a ataques.  

 Para obtener más información sobre los diferentes métodos de instalación de cliente, consulte [Client installation methods in System Center Configuration Manager](../../../../core/clients/deploy/plan/client-installation-methods.md) (Métodos de instalación de cliente en System Center Configuration Manager).  

 Además, siempre que sea posible, seleccione un método de instalación de clientes que requiera los mínimos permisos de seguridad en Configuration Manager, y restrinja los usuarios administrativos a los que se asignan roles de seguridad que incluyen permisos que se pueden utilizar para tareas que no sean la implementación de clientes. Por ejemplo, la actualización de cliente automática requiere el rol de seguridad **Administrador total** , que otorga todos los permisos de seguridad a un usuario administrativo.  

 Para obtener más información sobre las dependencias y los permisos de seguridad necesarios para cada método de instalación de clientes, consulte la sección "Installation Method Dependencies" (Dependencias de los métodos de instalación) del tema [Prerequisites for Computer Clients](../../../../core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md#BKMK_prereqs_computers) (Requisitos previos de los equipos cliente).  

 **Si debe utilizar la instalación de inserción de cliente, tome medidas adicionales para proteger la cuenta de instalación de inserción de cliente**  

 Aunque esta cuenta debe ser miembro del grupo **Administradores** local de cada equipo en el que se va a instalar el software cliente de Configuration Manager, no agregue nunca la cuenta de instalación de inserción de cliente al grupo **Admins. del dominio**. En lugar de ello, cree un grupo global y agregue ese grupo global al grupo **Administradores** local de los equipos cliente. También puede crear un objeto de directiva de grupo para agregar una configuración de grupo restringido para agregar la cuenta de instalación de inserción de cliente al grupo **Administradores** local.  

 Para mayor seguridad, cree varias cuentas de instalación de inserción de cliente, cada una con acceso administrativo a un número limitado de equipos, de modo que si una cuenta se ve comprometida solo se vean comprometidos los equipos cliente a los que tiene acceso dicha cuenta.  

 **Quite los certificados antes de la creación de imágenes del equipo cliente**  

 Si piensa implementar los clientes mediante el uso de la tecnología de creación de imágenes, quite siempre los certificados como los certificados PKI que incluyen la autenticación de cliente y los certificados autofirmados antes de capturar la imagen. Si no quita estos certificados, los clientes podrían suplantarse unos a otros y no se podrían comprobar los datos de cada cliente.  

 Para obtener más información acerca del uso de Sysprep para preparar un equipo para la creación de imágenes, consulte la documentación de implementación de Windows.  

 **Asegúrese de que los equipos cliente de Configuration Manager obtienen una copia autorizada de estos certificados:**  

-   La clave raíz confiable de Configuration Manager  

     Si no extendió el esquema de Active Directory para Configuration Manager y los clientes no utilizan certificados PKI cuando se comunican con los puntos de administración, los clientes emplean la clave raíz confiable de Configuration Manager para autenticar los puntos de administración válidos. En este escenario, los clientes no tienen ninguna posibilidad de comprobar si el punto de administración es un punto de administración confiable para la jerarquía a menos que utilicen la clave raíz confiable. Sin la clave raíz confiable, un atacante experimentado podría dirigir los clientes a un punto de administración no autorizado.  

     Si los clientes no pueden descargar la clave raíz confiable de Configuration Manager desde el catálogo global o mediante los certificados PKI, aprovisione previamente los clientes con la clave raíz confiable para asegurarse de que no puedan ser dirigidos a un punto de administración no autorizado. Para obtener más información, consulte [Planning for the Trusted Root Key](../../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK) (Planeación de la clave raíz confiable).  

-   El certificado de firma de servidor de sitio  

     Los clientes utilizan el certificado de firma de servidor de sitio para comprobar que el servidor de sitio firmó la directiva de cliente que descargan desde un punto de administración. Este certificado está autofirmado por el servidor de sitio y publicado en Servicios de dominio de Active Directory.  

     Si los clientes no pueden descargar el certificado de firma de servidor de sitio desde el catálogo global, de forma predeterminada lo descargan desde el punto de administración. Si el punto de administración se ve expuesto a una red no confiable (como Internet), instale manualmente el certificado de firma de servidor de sitio en los clientes para asegurarse de que no puedan ejecutar directivas de cliente alteradas desde un punto de administración comprometido.  

     Para instalar manualmente el certificado de firma de servidor de sitio, utilice la propiedad de CCMSetup Client.msi **SMSSIGNCERT**. Para obtener más información, consulte [About client installation properties in System Center Configuration Manager](../../../../core/clients/deploy/about-client-installation-properties.md) (Acerca de las propiedades de instalación de clientes en System Center Configuration Manager).  

 **No utilice la asignación de sitio automática si el cliente va a descargar la clave raíz confiable desde el primer punto de administración con el que se pone en contacto**  

 Esta práctica recomendada de seguridad está vinculada a la entrada anterior. Para evitar el riesgo de que un nuevo cliente descargue la clave raíz confiable desde un punto de administración no autorizado, utilice la asignación de sitio automática sólo en los siguientes escenarios:  

-   El cliente puede acceder a la información de sitio de Configuration Manager que está publicada en Active Directory Domain Services.  

-   Se aprovisiona previamente el cliente con la clave raíz confiable.  

-   Se utilizan certificados PKI de una entidad de certificación empresarial para establecer la confianza entre el cliente y el punto de administración.  

 Para obtener más información sobre la clave raíz confiable, consulte [Planning for the Trusted Root Key](../../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK) (Planeación de la clave raíz confiable).  

 **Instale equipos cliente con la opción de CCMSetup Client.msi SMSDIRECTORYLOOKUP=NoWINS**  

 El método de ubicación de servicio más seguro para que los clientes encuentren los sitios y los puntos de administración consiste en utilizar Active Directory Domain Services. Si no es posible, por ejemplo, porque no puede extender el esquema de Active Directory para Configuration Manager, o porque los clientes pertenecen a un grupo de trabajo o un bosque que no es de confianza, puede utilizar la publicación en DNS como método de ubicación de servicio alternativo. Si no se puede utilizar ninguno de los dos métodos, los clientes pueden recurrir al uso de WINS si el punto de administración no está configurado para las conexiones de cliente HTTPS.  

 Dado que la publicación en WINS es menos segura que los demás métodos de publicación, configure los equipos cliente para que no recurran al uso de WINS; para ello, especifique SMSDIRECTORYLOOKUP=NoWINS. Si debe utilizar WINS para la ubicación de servicio, utilice SMSDIRECTORYLOOKUP=WINSSECURE (configuración predeterminada), que utiliza la clave raíz confiable de Configuration Manager para validar el certificado autofirmado del punto de administración.  

> [!NOTE]  
>  Cuando el cliente está configurado para SMSDIRECTORYLOOKUP=WINSSECURE y encuentra un punto de administración de WINS, el cliente comprueba su copia de la clave raíz confiable de Configuration Manager que se encuentra en WMI. Si la firma del certificado del punto de administración coincide con la copia del cliente de la clave raíz confiable, el certificado se valida y el cliente se comunica con el punto de administración que encontró mediante WINS. Si la firma del certificado del punto de administración no coincide con la copia del cliente de la clave raíz confiable, el certificado no es válido y el cliente no se puede comunicar con el punto de administración que encontró mediante WINS.  

 **Asegúrese de que las ventanas de mantenimiento son lo suficientemente grandes como para implementar las actualizaciones de software imprescindibles**  

 Puede configurar ventanas de mantenimiento para recopilaciones de dispositivos para restringir los momentos en los que Configuration Manager puede instalar software en estos dispositivos. Si configura una ventana de mantenimiento demasiado pequeña, es posible que el cliente no pueda instalar las actualizaciones de software imprescindibles, lo que hace que el cliente sea vulnerable a los ataques que la actualización de software mitiga.  

 **En el caso de los dispositivos de Windows Embedded con filtros de escritura, tome medidas de seguridad adicionales para reducir la superficie expuesta a ataques si Configuration Manager deshabilita los filtros de escritura para conservar las instalaciones de software y los cambios**  

 Cuando hay filtros de escritura habilitados en los dispositivos de Windows Embedded, cualquier instalación de software o cambio se realiza solamente en la superposición y no se conserva después de reiniciarse el dispositivo. Si utiliza Configuration Manager para deshabilitar temporalmente los filtros de escritura para conservar las instalaciones de software y los cambios, durante este periodo, el dispositivo incrustado es vulnerable a posibles cambios de todos los volúmenes, lo que incluye las carpetas compartidas.  

 Aunque Configuration Manager bloquea el equipo durante este periodo para que solo los administradores locales puedan iniciar sesión, siempre que sea posible, tome medidas de seguridad adicionales para proteger el equipo. Por ejemplo, habilite restricciones adicionales en el firewall y desconecte el dispositivo de la red.  

 Si utiliza ventanas de mantenimiento para conservar los cambios, planee las ventanas con cuidado de modo que el tiempo durante el que los filtros de escritura pueden estar deshabilitados sea lo más corto posible pero se disponga de tiempo suficiente para que las instalaciones de software y los reinicios se completen.  

 **Si utiliza la instalación de clientes basada en actualizaciones de software e instala una versión posterior del cliente en el sitio, actualice la actualización de software que está publicada en el punto de actualización de software para que los clientes reciban la versión más reciente**  

 Si instala una versión posterior del cliente en el sitio, por ejemplo, si actualiza el sitio, la actualización de software de la implementación de cliente que está publicada en el punto de actualización de software no se actualiza automáticamente. Debe volver a publicar el cliente de Configuration Manager en el punto de actualización de software y hacer clic en **Sí** para actualizar el número de versión.  

 Para obtener más información, consulte el procedimiento “To publish the Configuration Manager client to the software update point” (Para publicar el cliente de Configuration Manager en el punto de actualización de software) del tema [How to Install Configuration Manager Clients by Using Software Update-Based Installation](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientSUP) (Instalación de clientes de Configuration Manager mediante la instalación basada en actualizaciones de software).  

 **Configure la opción de Agente de equipo del dispositivo cliente Suspender indicación de PIN de BitLocker en el reinicio como Siempre solo para los equipos de confianza que tienen acceso físico restringido**  

 Si configura esta opción del cliente como **Siempre**, Configuration Manager puede llevar a cabo la instalación de software para garantizar que se instalan las actualizaciones de software imprescindibles y que se reanudan los servicios. Sin embargo, si un atacante intercepta el proceso de reinicio, podría tomar el control del equipo. Utilice esta configuración sólo si confía en el equipo y el acceso físico al equipo está restringido. Por ejemplo, esta configuración podría ser apropiada para los servidores de un centro de datos.  

 **No configure la opción de Agente de equipo del dispositivo cliente Directiva de ejecución de PowerShell como Desviar.**  

 Esta opción del cliente permite que el cliente de Configuration Manager ejecute scripts de PowerShell sin firmar, con lo que podría ejecutarse malware en los equipos cliente. Si debe seleccionar esta opción, utilice una configuración de cliente personalizada y asígnela sólo a los equipos cliente que deben ejecutar scripts de PowerShell sin firmar.  

##  <a name="bkmk_mobile"></a> Prácticas recomendadas de seguridad para dispositivos móviles  
 **Para dispositivos móviles que se inscriben con Configuration Manager y compatibles con Internet: Instale el punto de proxy de inscripción en una red perimetral y el punto de inscripción en la intranet**  

 Esta separación de roles facilita la protección del punto de inscripción contra los ataques. Si el punto de inscripción se ve comprometido, un atacante podría obtener certificados para la autenticación y robar las credenciales de los usuarios que inscriben sus dispositivos móviles.  

 **Para dispositivos móviles: Configure la contraseña para facilitar la protección de los dispositivos móviles contra el acceso no autorizado**  

 Para dispositivos móviles inscritos por Configuration Manager: utilice un elemento de configuración de dispositivo móvil para configurar la contraseña de modo que la complejidad de la contraseña sea el PIN y la longitud de contraseña mínima sea al menos la longitud predeterminada.  

 Para dispositivos móviles que no tienen el cliente de Configuration Manager instalado pero que se administran con el conector de Exchange Server: configure la **Configuración de contraseña** del conector de Exchange Server de modo que la complejidad de la contraseña sea el PIN y especifique al menos la longitud predeterminada para la longitud de contraseña mínima.  

 **Para dispositivos móviles: Para facilitar la prevención de alteraciones de la información de inventario y la información de estado, permita que las aplicaciones se ejecuten solo si están firmadas por empresas de confianza y no permita que se instalen archivos sin firmar**  

 Para ver más dispositivos móviles inscritos por Configuration Manager: utilice un elemento de configuración de dispositivo móvil para configurar la opción de seguridad **Aplicaciones sin firmar** como **Prohibido** y configure **Instalación de archivos sin firmar** de modo que sea una fuente de confianza.  

 Para dispositivos móviles que no tienen el cliente de Configuration Manager instalado pero que se administran mediante el conector de Exchange Server: configure la **Configuración de la aplicación** del conector de Exchange Server de modo que **Instalación de archivos sin firmar** y **Aplicaciones sin firmar** se configuren como **Prohibido**.  

 **Para dispositivos móviles: Contribuya a evitar ataques de elevación de privilegios mediante el bloqueo del dispositivo móvil cuando no se utiliza**  

 Para ver más dispositivos móviles inscritos por Configuration Manager: utilice un elemento de configuración de dispositivo móvil para configurar la opción de contraseña **Tiempo de inactividad en minutos antes de que se bloquee el dispositivo móvil**.  

 Para dispositivos móviles que no tienen el cliente de Configuration Manager instalado pero que se administran mediante el conector de Exchange Server: configure la **Configuración de contraseña** del conector de Exchange Server para configurar **Tiempo de inactividad en minutos antes de que se bloquee el dispositivo móvil**.  

 **Para dispositivos móviles: evite la elevación de privilegios mediante la restricción de los usuarios que pueden inscribir sus dispositivos móviles.**  

 Utilice una configuración de cliente personalizada en lugar de la configuración de cliente predeterminada para permitir sólo a los usuarios autorizados que inscriban sus dispositivos móviles.  

 **Para dispositivos móviles: no implemente aplicaciones para usuarios que tienen dispositivos móviles inscritos por Configuration Manager o Microsoft Intune en los siguientes escenarios:**  

-   Cuando más de una persona utiliza el dispositivo móvil.  

-   Cuando un administrador inscribe el dispositivo en nombre de un usuario.  

-   Cuando el dispositivo se transfiere a otra persona sin retirarlo y volver a inscribirlo.  

 Se crea una relación de afinidad de dispositivo de usuario durante la inscripción, que permite asignar el usuario que realiza la inscripción al dispositivo móvil. Si otro usuario utiliza el dispositivo móvil, podrá ejecutar las aplicaciones implementadas para el usuario original, lo que podría ocasionar una elevación de privilegios. Asimismo, si un administrador inscribe el dispositivo móvil para un usuario, las aplicaciones implementadas para el usuario no se instalarán en el dispositivo móvil, sino que en su lugar podrían instalarse las aplicaciones implementadas para el administrador.  

 A diferencia de la afinidad de dispositivo de usuario para equipos Windows, no se puede definir manualmente la información de la afinidad de dispositivo de usuario para los dispositivos móviles inscritos por Microsoft Intune.  

 Si transfiere la propiedad de un dispositivo móvil inscrito mediante Intune, retire el dispositivo móvil de Intune para quitar la afinidad de dispositivo de usuario y, después, pida al usuario actual que vuelva a inscribirlo.  

 **Para dispositivos móviles: Asegúrese de que los usuarios inscriben sus propios dispositivos móviles para Microsoft Intune**  

 Dado que se crea una relación de afinidad de dispositivo de usuario durante la inscripción, que permite asignar el usuario que realiza la inscripción al dispositivo móvil, si un administrador inscribe el dispositivo móvil para un usuario, las aplicaciones implementadas para el usuario no se instalarán en el dispositivo móvil, sino que en su lugar podrían instalarse las aplicaciones implementadas para el administrador.  

 **Para el conector de Exchange Server: Asegúrese de que la conexión entre el servidor de sitio de Configuration Manager y el equipo con Exchange Server está protegida**  

 Utilice IPsec si se usa Exchange Server local; Exchange hospedado protege automáticamente la conexión mediante SSL.  

 **Para el conector de Exchange Server: utilice el principio de privilegios mínimos para el conector**  

 Para ver una lista de los cmdlets mínimos que necesita el conector de Exchange Server, consulte [Manage mobile devices with System Center Configuration Manager and Exchange](../../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md) (Administrar dispositivos móviles con System Center Configuration Manager y Exchange).  

##  <a name="bkmk_macs"></a> Prácticas recomendadas de seguridad para equipos Mac  
 **Para equipos Mac: almacene y acceda a los archivos de origen del cliente desde una ubicación segura.**  

 Configuration Manager no comprueba si se ha manipulado estos archivos de origen del cliente antes de instalar o inscribir el cliente en el equipo Mac. Descargue esos archivos desde un origen de confianza y almacénelos y tenga acceso a ellos de forma segura.  

 **Para equipos Mac: Independientemente de Configuration Manager, supervise el periodo de validez del certificado inscrito en los usuarios y haga un seguimiento de este.**  

 Para garantizar la continuidad de la actividad, supervise el periodo de validez de los certificados que utiliza para los equipos Mac y realice un seguimiento del mismo. Configuration Manager no admite la renovación automática de este certificado ni le avisa cuando el certificado está a punto de expirar. Un periodo de validez típico es 1 año.  

 Para obtener información sobre cómo renovar el certificado, consulte [Renewing the Mac Client Certificate Manually](../../../../core/clients/deploy/deploy-clients-to-macs.md#renewing-the-mac-client-certificate) (Renovación manual del certificado de cliente Mac).  

 **Para equipos Mac: considere la posibilidad de configurar el certificado de CA raíz de confianza de modo que sea de confianza solo para el protocolo SSL y ayudar, así, a proteger contra la elevación de privilegios.**  

 Cuando inscriba equipos Mac, se instalará automáticamente un certificado de usuario para administrar el cliente de Configuration Manager, junto con el certificado raíz de confianza al que se vincula el certificado de usuario. Si desea restringir la confianza de este certificado raíz únicamente al protocolo SSL, puede utilizar el siguiente procedimiento.  

 Una vez efectuado este procedimiento, no se confiaría en el certificado raíz para validar protocolos diferentes de SSL (por ejemplo, Correo seguro (S/MIME), Protocolo de autenticación extensible (EAP) o la firma de código).  

> [!NOTE]  
>  También puede utilizar este procedimiento si ha instalado el certificado de cliente independientemente de Configuration Manager.  

 Para restringir el certificado de entidad emisora raíz al protocolo SSL solo:  

1.  En el equipo Mac, abra una ventana de terminal.  

2.  Escriba el comando **sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access**  

3.  En el cuadro de diálogo **Acceso a llaveros** , en la sección **Llaves** , haga clic en **Sistema**y, a continuación, en la sección **Categoría** , haga clic en **Certificados**.  

4.  Busque y haga doble clic en el certificado de entidad emisora raíz para el certificado de cliente de Mac.  

5.  En el cuadro de diálogo para el certificado de entidad emisora raíz, expanda la sección **Confianza** y a continuación, realice los siguientes cambios:  

    1.  Para la configuración **Al utilizar este certificado** , cambie la configuración predeterminada de **Confiar siempre** a **Usar ajustes por omisión**.  

    2.  Para la configuración **Secure Sockets Layer (SSL)** , cambie **ningún valor especificado** a **Confiar siempre**.  

6.  Cierre el cuadro de diálogo; cuando se le solicite, escriba la contraseña del administrador y, luego, haga clic en **Actualizar ajustes**.  

##  <a name="BKMK_SecurityIssues_Clients"></a> Problemas de seguridad de los clientes de Configuration Manager  
 Los siguientes problemas de seguridad no disponen de mitigación:  

-   No se autentican los mensajes de estado  

     No se realiza la autenticación de los mensajes de estado. Cuando un punto de administración acepta conexiones de cliente HTTP, cualquier dispositivo puede enviar mensajes de estado al punto de administración. Si el punto de administración acepta conexiones de cliente HTTPS solamente, un dispositivo debe obtener un certificado de autenticación de cliente válido de una entidad de certificación raíz de confianza, pero también podría entonces enviar cualquier tipo de mensaje de estado. Si un cliente envía un mensaje de estado no válido se descartará.  

     Hay varios posibles ataques contra esta vulnerabilidad. Un atacante podría enviar un mensaje de estado ficticio para pasar a ser miembro de una recopilación basada en consultas de mensaje de estado. Cualquier cliente podría iniciar una denegación de servicio contra el punto de administración al desbordarlo con mensajes de estado. Si los mensajes de estado desencadenan acciones en las reglas de filtro de mensajes de estado, un atacante podría desencadenar la regla de filtro de mensajes de estado. Un atacante también podría enviar un mensaje de estado que podría invalidar la información de supervisión.  

-   Las directivas pueden redestinarse a clientes sin destino  

     Existen varios métodos que los atacantes podrían utilizar para hacer que una directiva destinada a un cliente se aplique a un cliente completamente diferente. Por ejemplo, el atacante de un cliente de confianza podría enviar información falsa de inventario o de detección para agregar el equipo a una recopilación a la que no debería pertenecer y, a continuación, recibir todas las implementaciones de dicha recopilación. Aunque existen controles para impedir que los atacantes modifiquen las directivas directamente, los atacantes podrían utilizar una directiva existente para volver a formatear y volver a implementar un sistema operativo y enviarlo a un equipo diferente, creando así una denegación de servicio. Estos tipos de ataques requieren una sincronización precisa y amplios conocimientos de la infraestructura de Configuration Manager.  

-   Los registros de cliente permiten el acceso de usuario  

     Todos los archivos de registro de cliente permiten a los usuarios el acceso de lectura y a los usuarios interactivos el acceso de escritura. Si se habilita el registro detallado, los atacantes podrían leer los archivos de registro para buscar información acerca de vulnerabilidades de sistema o compatibilidad. Los procesos como la instalación de software que se realizan en el contexto de un usuario deben ser capaces de escribir en registros con una cuenta de usuario con derechos reducidos. Esto significa que un atacante también podría escribir en los registros con una cuenta con derechos reducidos.  

     El riesgo más grave consiste en que un atacante podría quitar de los archivos de registro la información que podría necesitar un administrador para realizar tareas de detección de intrusos y auditoría.  

-   Un equipo podría utilizarse para obtener un certificado diseñado para la inscripción de dispositivos móviles  

     Cuando Configuration Manager procesa una solicitud de inscripción, no puede comprobar que la solicitud se originó en un dispositivo móvil en lugar de en un equipo. Si la solicitud proviene de un equipo, puede instalar un certificado PKI que se puede registrar en Configuration Manager. Para contribuir a evitar un ataque de elevación de privilegios en este escenario, permita sólo a los usuarios de confianza que inscriban sus dispositivos móviles y supervise cuidadosamente las actividades de inscripción.  

-   La conexión de un cliente al punto de administración no se desactiva si se bloquea un cliente y el cliente bloqueado puede seguir enviando paquetes de notificaciones de cliente al punto de administración como mensajes de mantenimiento de conexión.  

     Cuando se bloquea un cliente que ya no es de confianza y que ha establecido una comunicación de notificación de cliente, Configuration Manager no desconecta la sesión. El cliente bloqueado puede seguir enviando paquetes a su punto de administración hasta que el cliente se desconecta de la red. Los paquetes solo son paquetes pequeños de mantenimiento de conexión y los clientes no pueden ser administrados por Configuration Manager hasta que se desbloquean.  

-   Cuando utiliza la actualización de cliente automática y el cliente se dirige a un punto de administración para que descargue los archivos de origen de cliente, no se comprueba que el punto de administración sea una fuente de confianza  

-   Cuando los usuarios inscriben equipos Mac, están en riesgo de suplantación de identidad DNS  

     Cuando el equipo Mac se conecta al punto proxy de inscripción durante la inscripción, es poco probable que el equipo Mac ya tenga el certificado de CA raíz. En este momento, el servidor no es de confianza para el equipo Mac y solicitará al usuario que continúe. Si el nombre completo del punto del proxy de inscripción se resuelve mediante un servidor DNS no autorizado, podría dirigir el equipo Mac a un punto de proxy de inscripción malintencionado e instalar certificados de un origen que no es de confianza. Para ayudar a reducir este riesgo, siga los procedimientos recomendados para evitar la suplantación de DNS en su entorno.  

-   La inscripción de Mac no limita las solicitudes de certificados  

     Los usuarios pueden volver a inscribir sus equipos Mac y solicitar cada vez un nuevo certificado de cliente. Configuration Manager no comprueba varias solicitudes o limita el número de certificados solicitados desde un equipo único. Un usuario malintencionado podría ejecutar una secuencia de comandos que repite la solicitud de inscripción de línea de comandos, lo que provocaría una denegación de servicio en la red o en la entidad emisora de certificados (CA). Para ayudar a reducir este riesgo, debe supervisar cuidadosamente la CA emisora de certificados para este tipo de comportamiento sospechoso. Un equipo que muestra este modelo de comportamiento debe bloquearse inmediatamente de la jerarquía de Configuration Manager.  

-   Una confirmación de borrado no comprueba que el dispositivo se haya borrado con éxito  

     Cuando inicie una acción de borrado para un dispositivo móvil y Configuration Manager muestre el estado de borrado que se debe confirmar, la comprobación confirma si Configuration Manager ha enviado correctamente el mensaje y no si el dispositivo ha actuado sobre él. Además, para los dispositivos móviles que se administran mediante el conector de Exchange Server, una confirmación de borrado comprueba que Exchange, no el dispositivo, ha recibido el comando.  

-   Si usa las opciones de confirmación de cambios en los dispositivos de Windows Embedded, las cuentas podrían bloquearse antes de lo previsto.  

     Si el dispositivo de Windows Embedded ejecuta un sistema operativo anterior a Windows 7 y un usuario intenta iniciar sesión mientras los filtros de escritura están deshabilitados para confirmar los cambios efectuados por Configuration Manager, se reduce a la mitad el número de intentos de inicio de sesión incorrectos permitidos antes de que se bloquee la cuenta. Por ejemplo, si **Umbral de bloqueo de cuenta** se configura como 6 y un usuario escribe la contraseña incorrectamente 3 veces, la cuenta se bloquea, con lo que se crea una situación de denegación de servicio.  Si los usuarios deben iniciar sesión en dispositivos incrustados en este escenario, adviértales de la posibilidad de reducción del umbral de bloqueo.  

##  <a name="BKMK_Privacy_Cliients"></a> Información de privacidad para los clientes de Configuration Manager  
 Cuando se implementa el cliente de Configuration Manager, se habilita la configuración del cliente para poder utilizar las funciones de administración de Configuration Manager. Las opciones utilizadas para configurar las funciones se pueden aplicar a todos los clientes de la jerarquía de Configuration Manager, independientemente de si están conectados directamente a la red corporativa, conectados a través de una sesión remota o conectados a Internet aunque compatibles con Configuration Manager.  

 La información del cliente se almacena en la base de datos de Configuration Manager y no se envía a Microsoft. La información se guarda en la base de datos hasta que la tarea de mantenimiento del sitio **Eliminar datos de detección antiguos** la elimina cada 90 días. Puede configurar el intervalo de eliminación.  

 Antes de configurar el cliente de Configuration Manager, tenga en cuenta los requisitos de privacidad.  

### <a name="privacy-information-for-mobile-devices-that-are-enrolled-by-configuration-manager"></a>Información de privacidad para dispositivos móviles inscritos por Configuration Manager  
 Para obtener información de privacidad sobre la inscripción de dispositivos móviles de Configuration Manager, consulte [Declaración de privacidad de System Center Configuration Manager: anexo para dispositivos móviles](../../../../core/misc/privacy/privacy-statement-mobile-device-addendum.md).  

### <a name="client-status"></a>Estado de cliente  
 Configuration Manager supervisa la actividad de los clientes, efectúa evaluaciones periódicas y puede corregir el cliente de Configuration Manager y sus dependencias. El estado de cliente se habilita de manera predeterminada, usa métricas de servidor para la comprobación de la actividad de cliente y acciones de cliente para autocomprobaciones, correcciones y para enviar información de estado de cliente al sitio de Configuration Manager. El cliente ejecuta autocomprobaciones según una programación configurable. El cliente envía los resultados de las comprobaciones al sitio de Configuration Manager. Esta información se cifra durante la transferencia.  

 La información del estado de cliente se almacena en la base de datos de Configuration Manager y no se envía a Microsoft. La información no se almacena en formato cifrado en la base de datos del sitio. La información se retiene en la base de datos hasta que se elimina según el valor configurado en la opción de estado de cliente **Retener el historial de estado de cliente durante el siguiente número de días**. El valor predeterminado de esta configuración es 31 días.  

 Antes de instalar el cliente de Configuration Manager con comprobación de estado de cliente, tenga en cuenta sus requisitos de privacidad.  

##  <a name="BKMK_Privacy_ExchangeConnector"></a> Información de privacidad para dispositivos móviles administrados mediante el conector de Exchange Server  
 El conector de Exchange Server busca y administra dispositivos que se conectan a Exchange Server (locales u hospedados) mediante el protocolo de ActiveSync. Los registros encontrados por el conector de Exchange Server se almacenan en la base de datos de Configuration Manager. Se recopila la información de Exchange Server. No contiene información adicional distinta a la enviada por los dispositivos móviles a Exchange Server.  

 La información del dispositivo móvil no se envía a Microsoft. La información del dispositivo móvil se almacena en la base de datos de Configuration Manager. La información se guarda en la base de datos hasta que la tarea de mantenimiento del sitio **Eliminar datos de detección antiguos** la elimina cada 90 días. Puede configurar el intervalo de eliminación.  

 Antes de instalar y configurar el conector de Exchange Server, tenga en cuenta los requisitos de privacidad.  
