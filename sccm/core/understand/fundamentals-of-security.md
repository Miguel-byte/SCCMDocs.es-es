---
title: "Aspectos básicos de la seguridad | System Center Configuration Manager"
description: "Obtenga información sobre las capas de seguridad en System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 035b7f73-8b78-4ed1-835e-a31f9a5c4a02
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: cb84efcaac281aa8c9338cd69ce32054ea775de3


---
# <a name="fundamentals-of-security-for-system-center-configuration-manager"></a>Aspectos básicos de la seguridad en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

La seguridad en System Center Configuration Manager consta de varias capas. La primera cada procede de las características de seguridad de Windows para el sistema operativo y la red, e incluyen:  

-   Uso compartido de archivos para transferir archivos entre componentes de Configuration Manager  

-   Listas de control de acceso (ACL) para proteger archivos y claves del Registro  

-   IPsec para proteger las comunicaciones  

-   Directivas de grupo para establecer directivas de seguridad  

-   Permisos de DCOM para aplicaciones distribuidas, como la consola de Configuration Manager  

-   Servicios de dominio de Active Directory para almacenar entidades de seguridad  

-   Seguridad de cuenta de Windows, incluidos determinados grupos que se crean durante el programa de instalación de Configuration Manager  

Los componentes de seguridad adicionales, como firewalls y detección de intrusiones, proporcionan una protección de gran magnitud en todo el entorno. Los certificados emitidos por implementaciones de PKI estándar del sector permiten proporcionar autenticación, firma y cifrado.  

Además de la seguridad proporcionada por la infraestructura de red y de Windows Server, Configuration Manager controla el acceso a la consola de Configuration Manager y sus recursos de varias maneras. De manera predeterminada, solo los administradores locales tienen derechos sobre los archivos y las claves del Registro que se requieren para ejecutar la consola de Configuration Manager en los equipos en los que está instalada.  

La siguiente capa de seguridad se basa en el acceso a través del Instrumental de administración de Windows (WMI) y, específicamente, mediante el **proveedor de SMS**. El proveedor de SMS es un componente de Configuration Manager que concede a los usuarios acceso a la base de datos del sitio para consultar información. De forma predeterminada, el acceso al proveedor está limitado a los miembros del grupo **Administradores SMS** . En principio, este grupo solo contiene el usuario que ha instalado Configuration Manager. Para conceder a otras cuentas permisos en el depósito del modelo de información común (CIM) y el proveedor de SMS, agréguelas al grupo Administradores de SMS.  

La capa final de seguridad se basa en los permisos de objetos de la base de datos del sitio. De manera predeterminada, la cuenta de sistema local y la cuenta de usuario que ha usado para instalar Configuration Manager pueden administrar todos los objetos de la base de datos del sitio. Puede conceder y restringir permisos a usuarios administrativos adicionales en la consola de Configuration Manager mediante la **administración basada en roles**.  

En el resto de este tema se tratan aspectos de seguridad relacionados con Configuration Manager.  

## <a name="role-based-administration"></a>Administración basada en roles  
 Configuration Manager usa la administración basada en roles para proteger objetos como recopilaciones, implementaciones y sitios. Este modelo de administración define y administra de manera centralizada la configuración de acceso de seguridad de la totalidad de la jerarquía para todos los sitios y sus configuraciones. Se asignan roles de seguridad a usuarios administrativos y permisos de grupo en varios tipos de objetos de Configuration Manager como, por ejemplo, permisos para crear o cambiar la configuración de cliente. Los ámbitos de seguridad agrupan instancias específicas de objetos que un usuario administrativo se encarga de administrar, por ejemplo, una aplicación que instala Microsoft Office. La combinación de roles de seguridad, ámbitos de seguridad y recopilaciones define los objetos que un usuario administrativo puede ver y administrar. Configuration Manager instala algunos roles de seguridad predeterminados para tareas de administración habituales. Sin embargo, puede crear sus propios roles de seguridad para satisfacer sus requisitos empresariales.  

 Para obtener más información, consulte [Configure role-based administration for System Center Configuration Manager (Configurar la administración basada en roles en System Center Configuration Manager)](../../core/servers/deploy/configure/configure-role-based-administration.md).  

## <a name="securing-client-endpoints"></a>Protección de extremos de cliente  
 La comunicación del cliente con roles de sistema de sitio se protege mediante certificados autofirmados o certificados de infraestructura de clave pública (PKI). Los clientes de equipos que Configuration Manager detecta en Internet y los clientes de dispositivo móvil deben usar certificados PKI para que los puntos de conexión de clientes puedan protegerse mediante HTTPS. Los roles de sistema de sitio a los que los clientes se conectan se pueden configurar para la comunicación de cliente HTTPS o HTTP. Los equipos cliente siempre se comunican mediante el método más seguro disponible, y solo vuelven a usar HTTP, el método de comunicación menos seguro en la intranet, si tiene roles de sistema de sitio que permiten la comunicación HTTP.  

 Para obtener más información, consulte [Cryptographic controls technical reference for System Center Configuration Manager (Referencia técnica de controles criptográficos de System Center Configuration Manager)](../../protect/deploy-use/cryptographic-controls-technical-reference.md).  

## <a name="configuration-manager-accounts-and-groups"></a>Cuentas y grupos de Configuration Manager  
 Configuration Manager usa la cuenta **Sistema local** para la mayoría de las operaciones de sitio. Sin embargo, algunas tareas de administración podrían requerir la creación y el mantenimiento de cuentas adicionales. Durante la instalación se crean varios roles de SQL Server y grupos predeterminados. Sin embargo, es posible que tenga que agregar manualmente cuentas de equipo o usuario a estos roles y grupos predeterminados.  

 Para obtener más información, consulte [Cuentas que se usan en System Center Configuration Manager](../../core/plan-design/hierarchy/accounts.md).  

## <a name="privacy"></a>Privacidad  
 A pesar de que los productos de administración empresarial ofrecen muchas ventajas ya que permiten administrar de forma eficaz una gran cantidad de clientes, también se debe tener en cuenta que este software podría afectar a la privacidad de los usuarios de su organización. System Center Configuration Manager incluye un gran número de herramientas para la recopilación de datos y la supervisión de dispositivos, algunas de las cuales podrían ocasionar problemas relacionados con la privacidad.  

 Por ejemplo, al instalar el cliente de Configuration Manager, muchas opciones de administración se habilitan de manera predeterminada. Como resultado, el software cliente envía información al sitio de Configuration Manager. La información del cliente se almacena en la base de datos de Configuration Manager y esta no se envía a Microsoft. Antes de implementar System Center Configuration Manager, tenga en cuenta los requisitos de privacidad.  



<!--HONumber=Nov16_HO1-->


