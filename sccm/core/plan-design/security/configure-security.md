---
title: Configurar la seguridad en System Center Configuration Manager | Microsoft Docs
description: Configure las opciones relacionadas con la seguridad de System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 552e7e3d-e584-4a7c-9155-0f796a14b678
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6ed317d45d90758832d4157985dd95d5e253c6fc
ms.openlocfilehash: c486c196335174290a925ca59fe42b806d50889d


---
# <a name="configure-security-in-system-center-configuration-manager"></a>Configurar la seguridad en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Use la información de este tema para configurar las siguientes opciones relacionadas con la seguridad de System Center Configuration Manager:  

-   [Configure Settings for Client PKI Certificates](#BKMK_ConfigureClientPKI)  

-   [Configurar la firma y el cifrado](#BKMK_ConfigureSigningEncryption)  

-   [Configure Role-Based Administration](#BKMK_ConfigureRBA)  

-   [Manage Accounts that are Used by Configuration Manager](#BKMK_ManageAccounts)  

##  <a name="a-namebkmkconfigureclientpkia-configure-settings-for-client-pki-certificates"></a><a name="BKMK_ConfigureClientPKI"></a> Configurar opciones de certificados PKI de cliente  
Si desea usar certificados de infraestructura de clave pública (PKI) para conexiones de cliente a sistemas de sitio que usan Internet Information Services (IIS), use el procedimiento siguiente para configurar las opciones de estos certificados.  

#### <a name="to-configure-client-pki-certificate-settings"></a>Para configurar certificados PKI de cliente  

1.  En la consola de Configuration Manager, haga clic en **Administración**.  

2.  En el área de trabajo **Administración** , expanda **Configuración del sitio**, haga clic en **Sitios**y, a continuación, haga clic en el sitio primario que desee configurar.  

3.  En la pestaña **Inicio** , en el grupo **Propiedades** , haga clic en **Propiedades**y, a continuación, haga clic en la pestaña **Comunicación de equipo cliente** .  

    Esta pestaña está disponible solamente en un sitio primario. Si no puede ver la pestaña **Comunicación de equipo cliente** , compruebe que no esté conectado a un sitio de administración central o a un sitio secundario.  

4.  Haga clic en **HTTPS solamente** cuando desee que los clientes asignados al sitio usen siempre un certificado PKI de cliente al conectarse a sistemas de sitio que usen IIS. O bien, haga clic en **HTTPS o HTTP** cuando no necesite que los clientes utilicen certificados PKI.  

5.  Si seleccionó **HTTPS o HTTP**, haga clic en **Usar un certificado de cliente PKI (capacidad de autenticación de cliente) cuando esté disponible** cuando desee usar un certificado PKI de cliente para conexiones HTTP. El cliente utiliza este certificado en lugar de un certificado autofirmado para autenticarse en los sistemas de sitio. Esta opción se selecciona automáticamente si selecciona **HTTPS solamente**.  

    Cuando se detecta que los clientes están en Internet, o están configurados para la administración de clientes solo de Internet, siempre usan un certificado PKI del cliente.  

6.  Haga clic en **Modificar** para configurar su método de selección de cliente elegido cuando haya más de un certificado de cliente PKI disponible en un cliente y, a continuación, haga clic en **Aceptar**.  

    Para más información sobre el método de selección de certificados de cliente, vea [Planeación de la selección de certificados de cliente PKI](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForClientCertificateSelection).  

7.  Active o desactive la casilla para que los clientes comprueben la lista de revocación de certificados (CRL).  

    Para más información sobre la comprobación de la CRL de los clientes, vea [Planeación de la revocación de certificados PKI](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForCRLs).  

8.  Si debe especificar certificados de entidad de certificación (CA) raíz de confianza para clientes, haga clic en **Establecer**, importe los archivos del certificado de CA raíz y, a continuación, haga clic en **Aceptar**.  

    Para más información sobre esta opción, vea [Planeación de los certificados raíz de confianza PKI y la lista de emisores de certificados](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRootCAs).  

9. Haga clic en **Aceptar** para cerrar el cuadro de diálogo de propiedades del sitio.  

Repita este procedimiento para todos los sitios primarios de la jerarquía.  

##  <a name="a-namebkmkconfiguresigningencryptiona-configure-signing-and-encryption"></a><a name="BKMK_ConfigureSigningEncryption"></a> Configurar la firma y el cifrado  
Configure las opciones de firma y cifrado más seguras para los sistemas de sitio que pueden admitir todos los clientes en el sitio. Estas opciones son especialmente importantes cuando se permite a los clientes comunicarse con sistemas de sitio mediante certificados autofirmados a través de HTTP.  

#### <a name="to-configure-signing-and-encryption-for-a-site"></a>Para configurar la firma y el cifrado para un sitio  

1.  En la consola de Configuration Manager, haga clic en **Administración**.  

2.  En el área de trabajo **Administración** , expanda **Configuración del sitio**, haga clic en **Sitios**y, a continuación, haga clic en el sitio primario que desee configurar.  

3.  En la pestaña **Inicio** , en el grupo **Propiedades** , haga clic en **Propiedades**y, a continuación, haga clic en la pestaña **Firma y cifrado** .  

    Esta pestaña está disponible solamente en un sitio primario. Si no puede ver la pestaña **Firma y cifrado** , compruebe que no esté conectado a un sitio de administración central o a un sitio secundario.  

4.  Configure las opciones de firma y cifrado que desee y, a continuación, haga clic en **Aceptar**.  

    > [!WARNING]  
    >  No seleccione **Requerir SHA-256** sin comprobar primero que todos los clientes que puedan estar asignados al sitio pueden admitir este algoritmo hash o que tienen un certificado de autenticación de cliente PKI válido. Puede que tenga que instalar las actualizaciones o las revisiones en los clientes para que admitan SHA-256. Por ejemplo, los equipos que ejecutan Windows Server 2003 SP2 deben instalar una revisión a la que se hace referencia en el [artículo de Knowledge Base 938397](http://go.microsoft.com/fwlink/p/?LinkId=226666).  
    >   
    >  Si selecciona esta opción y los clientes no admiten SHA-256 y usan certificados autofirmados, Configuration Manager los rechaza. En este caso, el componente SMS_MP_CONTROL_MANAGER registra el identificador de mensaje 5443.  

5.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Propiedades** del sitio.  

Repita este procedimiento para todos los sitios primarios de la jerarquía.  

##  <a name="a-namebkmkconfigurerbaa-configure-role-based-administration"></a><a name="BKMK_ConfigureRBA"></a> Configurar la administración basada en roles  
La administración basada en roles combina roles de seguridad, ámbitos de seguridad y recopilaciones asignadas para definir el ámbito administrativo de cada usuario administrativo. Un ámbito administrativo incluye los objetos que puede ver un usuario administrativo en la consola de Configuration Manager y las tareas relacionadas con esos objetos que el usuario administrativo tiene permiso para realizar. Las configuraciones de la administración basada en roles se aplican en cada sitio en una jerarquía.  

Los siguientes vínculos llevan a las secciones correspondientes del tema [Configurar la administración basada en roles de System Center Configuration Manager](../../../core/servers/deploy/configure/configure-role-based-administration.md):  

-   [Create custom security roles (Crear roles de seguridad personalizados)](../../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_CreateSecRole)  

-   [Configurar roles de seguridad](../../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ConfigSecRole)  

-   [Configurar ámbitos de seguridad para un objeto](../../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ConfigSecScope)  

-   [Configurar recopilaciones para administrar la seguridad](../../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ConfigColl)  

-   [Crear un nuevo usuario administrativo](../../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_Create_AdminUser)  

-   [Modify the administrative scope of an administrative user (Modificar el ámbito administrativo de un usuario administrativo)](../../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ModAdminUser)  

> [!IMPORTANT]  
>  Su propio ámbito administrativo define los objetos y valores que se pueden asignar al configurar la administración basada en roles para otro usuario administrativo. Para más información sobre el planeamiento de la administración basada en roles, vea [Fundamentals of role-based administration for System Center Configuration Manager (Aspectos básicos de la administración basada en roles de System Center Configuration Manager)](../../../core/understand/fundamentals-of-role-based-administration.md).  

##  <a name="a-namebkmkmanageaccountsa-manage-accounts-that-are-used-by-configuration-manager"></a><a name="BKMK_ManageAccounts"></a> Administrar las cuentas que usa Configuration Manager  
Configuration Manager es compatible con cuentas de Windows para muchos usos y tareas diferentes.  

Use el procedimiento siguiente para ver qué cuentas están configuradas para las diferentes tareas y para administrar la contraseña que usa Configuration Manager para cada cuenta.  

#### <a name="to-manage-accounts-that-are-used-by-configuration-manager"></a>Para administrar las cuentas que usa Configuration Manager  

1.  En la consola de Configuration Manager, haga clic en **Administración**.  

2.  En el área de trabajo **Administración**, expanda **Seguridad** y haga clic en **Cuentas** para ver las cuentas configuradas para Configuration Manager.  

3.  Para cambiar la contraseña de una cuenta configurada para Configuration Manager, seleccione la cuenta.  

4.  En la pestaña **Inicio** , en el grupo **Propiedades** , haga clic en **Propiedades**.  

5.  Haga clic en **Establecer** para abrir el cuadro de diálogo **Cuenta de usuario de Windows** y especifique la nueva contraseña que usará Configuration Manager para la cuenta.  

    > [!NOTE]  
    >  La contraseña que especifique debe coincidir con la contraseña especificada para la cuenta en Usuarios y equipos de Active Directory.  

6.  Haga clic en **Aceptar** para completar el procedimiento.  



<!--HONumber=Dec16_HO3-->


