---
title: "Preparativos para la implementación de software cliente en Mac | Microsoft Docs"
description: "Tareas de configuración previas a la implementación del cliente de Configuration Manager en Mac."
ms.custom: na
ms.date: 05/04/2017
ms.prod: configuration-manager
ms.reviewer: aaroncz
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2285a953-6a86-4ed5-97dd-cd57b02bc1ee
caps.latest.revision: 12
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: c6a6137fa978e1ea28aefea2aea4e29ba661efd6
ms.openlocfilehash: b3bb72f81812705b4654e268025074402e89a7cb
ms.contentlocale: es-es
ms.lasthandoff: 05/04/2017


---

# <a name="prepare-to-deploy-client-software-to-macs"></a>Preparativos para la implementación de software cliente en Mac

*Se aplica a: System Center Configuration Manager (Rama actual)*

Siga estos pasos para asegurarse de que está listo para [implementar el cliente de Configuration Manager en equipos Mac](/sccm/core/clients/deploy/deploy-clients-to-macs). 

## <a name="mac-prerequisites"></a>Requisitos previos de Mac

El paquete de instalación del cliente Mac no se suministra con los medios de Configuration Manager. Descargue los **clientes para sistemas operativos adicionales** en el [Centro de descarga de Microsoft](http://go.microsoft.com/fwlink/?LinkID=525184).  

**Versiones admitidas:**  

-   **Mac OS X 10.6** (Snow Leopard) 

-   **Mac OS X 10.7** (Lion) 

-   **Mac OS X 10.8** (Mountain Lion)

-   **Mac OS X 10.9** (Mavericks)

-   **Mac OS X 10.9** (Mavericks)  

-   **Mac OS X 10.10** (Yosemite)  

-   **Mac OS X 10.11** (El Capitan)  

-   **Mac OS X 10.12** (macOS Sierra)  

## <a name="certificate-requirements"></a>Requisitos de certificados
Para la instalación y la administración de clientes para equipos Mac se necesitan certificados de infraestructura de clave pública (PKI). Los certificados PKI protegen la comunicación entre los equipos Mac y el sitio de Configuration Manager mediante transferencias de datos cifrados y autenticación mutua. Configuration Manager puede solicitar e instalar un certificado de cliente mediante los Servicios de certificados de Microsoft con una entidad de certificación empresarial (CA) y los roles del sistema de sitio del punto de proxy de inscripción y del punto de inscripción de Configuration Manager. También puede solicitar e instalar un certificado de equipo sin la intervención de Configuration Manager, si el certificado cumple los requisitos para Configuration Manager.   
  
Los clientes Mac de Configuration Manager siempre realizan una comprobación de revocación de certificado. No se puede deshabilitar esta función.  
  
Si los clientes Mac no pueden confirmar el estado de revocación de certificado para un certificado de servidor porque no encuentran la CRL, no podrán conectarse correctamente a sistemas de sitio de Configuration Manager. Compruebe, especialmente para clientes Mac que no están en el mismo bosque que la entidad de certificación emisora, el diseño de la CRL para asegurarse de que los clientes Mac pueden encontrar un punto de distribución CRL (CDP), y conectarse a él, para poder conectarse a servidores de sistema de sitio.  

Antes de instalar el cliente de Configuration Manager en un equipo Mac, decida cómo va a instalar el certificado de cliente:  

-   Usar la inscripción de Configuration Manager mediante la [herramienta CMEnroll](/sccm/core/clients/deploy/deploy-clients-to-macs#install-the-client-and-then-enroll-the-client-certificate-on-the-mac). El proceso de inscripción no admite la renovación automática de certificados por lo que debe volver a inscribir los equipos Mac antes de que expire el certificado instalado.  

-   [Usar una solicitud de certificado y un método de instalación independiente de Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-macs#use-a-certificate-request-and-installation-method-that-is-independent-from-configuration-manager).  

Para obtener más información sobre los requisitos de certificado de cliente Mac y otros certificados PKI necesarios para admitir equipos Mac, consulte [PKI certificate requirements for System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md) (Requisitos de certificados PKI para System Center Configuration Manager).  

Los clientes Mac se asignan automáticamente al sitio de Configuration Manager que los administra. Los clientes Mac se instalan como clientes de solo Internet, incluso si la comunicación está restringida a la intranet. La configuración de cliente implica que se comunicarán con los roles de sistema de sitio (puntos de administración y puntos de distribución) del sitio al que están asignados cuando se configuren estos roles para permitir conexiones de cliente desde Internet. Los equipos Mac no se comunican con roles de sistema de sitio fuera del sitio al que están asignados.  

> [!IMPORTANT]  
>  El cliente Mac de Configuration Manager no se puede usar para conectarse con un punto de administración que está configurado para usar una [réplica de base de datos](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  


## <a name="deploy-a-web-server-certificate-to-site-system-servers"></a>Implementar un certificado de servidor web en servidores de sistema de sitio  
Si estos sistemas de sitio no tienen un certificado de servidor web, debe implementarlo en los equipos que tengan estos roles de sistema de sitio:  

-   Punto de administración  

-   Punto de distribución  

-   Punto de inscripción  

-   Punto de proxy de inscripción  

El certificado de servidor web debe contener el FQDN de Internet que se especifica en las propiedades del sistema de sitio. No es necesario que el servidor sea accesible desde Internet para admitir equipos Mac. Si no requiere administración de cliente basada en Internet, puede especificar el FQDN de la intranet para el FQDN de Internet.  

Especifique el FQDN de Internet del sistema de sitio en el certificado de servidor web para el punto de administración, el punto de distribución y el punto de proxy de inscripción. 

Para ver una implementación de ejemplo en la que se crea y se instala este certificado de servidor web, consulte [Deploying the Web Server Certificate for Site Systems that Run IIS](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012) (Implementación del certificado de servidor web para sistemas de sitio que ejecutan IIS).  


## <a name="deploy-a-client-authentication-certificate-to-site-system-servers"></a>Implementar un certificado de autenticación de cliente en servidores de sistema de sitio  
 Si estos sistemas de sitio no tienen un certificado de autenticación de cliente, impleméntelo en los equipos que tengan estos roles de sistema de sitio:  

-   Punto de administración  

-   Punto de distribución  

 Para ver una implementación de ejemplo en la que se crea y se instala el certificado de cliente para puntos de administración, consulte [Deploying the Client Certificate for Windows Computers](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_client2008_cm2012) (Implementación del certificado de cliente para equipos Windows).  

 Para ver una implementación de ejemplo en la que se crea y se instala el certificado de cliente para puntos de distribución, consulte [Deploying the Client Certificate for Distribution Points](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clientdistributionpoint2008_cm2012) (Implementación del certificado de cliente para puntos de distribución).  

>[!IMPORTANT]
>  Para implementar el cliente en dispositivos que ejecutan macOS Sierra, el nombre de asunto del certificado de punto de administración se debe configurar correctamente mediante, por ejemplo, el FQDN del servidor de punto de administración.

## <a name="prepare-the-client-certificate-template-for-macs"></a>Preparar la plantilla de certificado de cliente para equipos Mac  

 La plantilla de certificado debe tener permisos de **lectura** e **inscripción** para la cuenta de usuario que inscriba el certificado en el equipo Mac.  

 Consulte [Deploying the Client Certificate for Mac Computers](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_MacClient_SP1) (Implementación del certificado de cliente para equipos Mac).  

## <a name="configure-the-management-point-and-distribution-point"></a>Configurar el punto de administración y el punto de distribución  
 Configure los puntos de administración para las siguientes opciones:  

-   HTTPS  

-   Allow client connections from the Internet (Permitir conexiones de cliente desde Internet). Este valor de configuración es necesario para administrar equipos Mac. Sin embargo, eso no significa que los servidores del sistema de sitios deben ser accesibles desde Internet.  

-   Permitir a los dispositivos móviles y equipos Mac usar este punto de administración  

 Aunque no se requieren puntos de distribución para instalar el cliente, debe configurarlos para permitir conexiones de cliente desde Internet si quiere implementar software en estos equipos una vez instalado el cliente.  

 
### <a name="to-configure-management-points-and-distribution-points-to-support-macs"></a>Para configurar puntos de administración y puntos distribución para admitir equipos Mac  

Antes de iniciar este procedimiento, asegúrese de que el servidor de sistema de sitio que ejecuta el punto de administración y el punto de distribución está configurado con un FQDN de Internet. Si estos servidores no admiten la administración de cliente basada en Internet, puede especificar el FQDN de intranet como FQDN de Internet. 

Los roles de sistema de sitio deben estar en un sitio primario.  


1.  En la consola de Configuration Manager, seleccione **Administración** > **Configuración del sitio** > **Servidores y roles del sistema de sitios** y, después, seleccione el servidor que tenga los roles de sistema de sitio correctos.  

3.  En el panel de detalles, haga clic con el botón derecho en **Punto de administración**, seleccione **Propiedades de rol** y, en el cuadro de diálogo **Propiedades de punto de administración**, configure estas opciones:  

    1.  Elija **HTTPS**.  

    2.  Seleccione **Permitir solo conexiones de Internet a los clientes** o **Allow intranet and Internet client connections** (Permitir conexiones de intranet e Internet a los clientes). Estas opciones requieren un FQDN de Internet o de intranet.  

    3.  Seleccione **Permitir a los dispositivos móviles y equipos Mac usar este punto de administración**.  

4.  En el panel de detalles, haga clic con el botón derecho en **Punto de distribución**, seleccione **Propiedades de rol** y, en el cuadro de diálogo **Propiedades de punto de distribución**, configure estas opciones:  

    -   Elija **HTTPS**.  

    -   Seleccione **Permitir solo conexiones de Internet a los clientes** o **Allow intranet and Internet client connections** (Permitir conexiones de intranet e Internet a los clientes). Estas opciones requieren un FQDN de Internet o de intranet.  

    -   Seleccione **Importar certificado**, busque el archivo del certificado del punto de distribución de cliente exportado y, después, especifique la contraseña.  

5.  Repita los pasos del 2 al 4 para todos los puntos de administración y puntos de distribución de los sitios primarios que va a usar con equipos Mac.  

## <a name="configure-the-enrollment-proxy-point-and-the-enrollment-point"></a>Configurar el punto de proxy de inscripción y el punto de inscripción  
 Debe instalar estos dos roles de sistema de sitio en el mismo sitio, pero no es necesario instalarlos en el mismo servidor de sistema de sitio, ni en el mismo bosque de Active Directory.  

 Para obtener más información sobre los distintos roles de sistema de sitio, consulte [Site system roles](../../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md#bkmk_planroles) (Roles de sistema de sitio) en [Plan for site system servers and site system roles for System Center Configuration Manager](../../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md) (Planeamiento de servidores y roles de sistema de sitio para System Center Configuration Manager).  

 Estos procedimientos configuran los roles de sistema de sitio para admitir equipos Mac.   

-   [Nuevo servidor de sistema de sitio](#new-site-system-server)  

-   [Servidor de sistema de sitio existente](#existing-site-system-server)  

###  <a name="new-site-system-server"></a>nuevo servidor de sistema de sitio  

1.  En la consola de Configuration Manager, elija **Administración** >  **Configuración de sitio** > **Servidores y roles del sistema de sitios**.  

3.  En la pestaña **Inicio**, en el grupo **Crear**, elija **Crear servidor del sistema de sitio**.  

4.  En la página **General**, especifique la configuración general para el sistema de sitio.  Asegúrese de especificar un valor para el FQDN de Internet. Si el servidor no va a ser accesible desde Internet, use el FQDN de intranet.  

5.  En la página **Selección de rol del sistema**, seleccione **Punto de proxy de inscripción** y **Punto de inscripción** en la lista de roles disponibles.  

6.  En la página **Punto de proxy de inscripción**, revise la configuración y haga los cambios necesarios.  

7.  En la página de configuración de **Punto de inscripción**, revise la configuración y haga los cambios necesarios. Después, finalice el asistente.  

### <a name="existing-site-system-server"></a>servidor de sistema de sitio existente  

1.  En la consola de Configuration Manager, seleccione **Administración** >  **Configuración del sitio** > **Servidores y roles del sistema de sitios** y, después, seleccione el servidor que quiere usar para admitir equipos Mac.  

3.  En la pestaña **Inicio**, en el grupo **Crear**, elija **Agregar roles del sistema de sitio**.  

4.  En la página **General** , especifique la configuración general del sistema de sitio y, a continuación, haga clic en **Siguiente**. Asegúrese de especificar un valor para el FQDN de Internet. Si el servidor no va a ser accesible desde Internet, use el FQDN de intranet.   

5.  En la página **Selección de rol del sistema**, seleccione **Punto de proxy de inscripción** y **Punto de inscripción** en la lista de roles disponibles.  

6.  En la página **Punto de proxy de inscripción**, revise la configuración y haga los cambios necesarios.  

7.  En la página de configuración de **Punto de inscripción**, revise la configuración y haga los cambios necesarios. Después, finalice el asistente.  

## <a name="install-the-reporting-services-point"></a>instalar el punto de servicios de informes  
 [Instale el punto de servicios de informes](../../../core/servers/manage/configuring-reporting.md) si quiere ejecutar informes para equipos Mac.  

### <a name="next-steps"></a>Pasos siguientes

[Implementar el cliente de Configuration Manager en equipos Mac](/sccm/core/clients/deploy/deploy-clients-to-macs)  
