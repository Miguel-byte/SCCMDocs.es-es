---
title: Certificados de CMG
description: Obtenga información sobre los diferentes certificados digitales que se usan con Cloud Management Gateway.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/22/2018
ms.topic: article
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.assetid: 71eaa409-b955-45d6-8309-26bf3b3b0911
ms.openlocfilehash: 1c7adec8f8919736c61859791802a96766af31bb
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/23/2018
---
# <a name="certificates-for-the-cloud-management-gateway"></a>Certificados para Cloud Management Gateway

*Se aplica a: System Center Configuration Manager (Rama actual)*

Según el escenario que use para administrar clientes en Internet con Cloud Management Gateway (CMG), necesita uno o varios certificados digitales. Para obtener más información sobre los diferentes escenarios, vea [Plan for cloud management gateway](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway) (Planificación para Cloud Management Gateway).


## <a name="cmg-server-authentication-certificate"></a>Certificado de autenticación de servidor CMG

*Este certificado es necesario en todos los escenarios.*

Este certificado se proporciona al crear la instancia de CMG en la consola de Configuration Manager.

CMG crea un servicio HTTPS al que se conectan los clientes basados en Internet. El servidor requiere un certificado de autenticación de servidor para crear el canal seguro. Puede adquirir un certificado para este fin de un proveedor público o emitirlo desde su propia infraestructura de clave pública (PKI). Para obtener más información, vea [Certificado raíz de confianza de CMG para clientes](#cmg-trusted-root-certificate-to-clients).

 > [!TIP]
 > Este certificado requiere un nombre único global para identificar el servicio de Azure. Antes de solicitar un certificado, confirme que el nombre de dominio de Azure deseado sea único. Por ejemplo, *GraniteFalls.CloudApp.Net*. Inicie sesión en [Microsoft Azure Portal](https://portal.azure.com). Haga clic en **Crear un recurso**, seleccione la categoría **Proceso** y haga clic en **Servicio de nube**. En el campo **Nombre DNS**, escriba el prefijo deseado, por ejemplo, *GraniteFalls*. La interfaz mostrará si el nombre de dominio está disponible o si ya está en uso por otro servicio. No cree el servicio en el portal, simplemente use este proceso para comprobar si el nombre está disponible. 
  
 > [!NOTE]
 > A partir de la versión 1802, el certificado de autenticación de servidor CMG admite caracteres comodín. Algunas entidades de certificación emiten certificados con un carácter comodín para el nombre de host. Por ejemplo, **\*.contoso.com**. Algunas organizaciones usan certificados con caracteres comodín para simplificar sus PKI y reducir los costos de mantenimiento.
 <!--491233-->


### <a name="cmg-trusted-root-certificate-to-clients"></a>Certificado raíz de confianza de CMG para clientes

Los clientes deben confiar en el certificado de autenticación de servidor CMG. Hay dos métodos para conseguir esta relación de confianza:
- Usar un certificado de un proveedor de certificados público y de confianza global. Por ejemplo, VeriSign o Thawte, entre otros. Los clientes de Windows incluyen entidades de certificación raíz de confianza (CA) de estos proveedores. Al usar un certificado de autenticación de servidor emitido por uno de estos proveedores, los clientes confían automáticamente en él. 
- Usar un certificado emitido por una entidad de certificación de empresa de la infraestructura de clave pública (PKI). La mayoría de las implementaciones de PKI de empresa agregan las entidades de certificación raíz de confianza a clientes de Windows. Por ejemplo, mediante el uso de Servicios de certificados de Active Directory con una directiva de grupo. Si emite el certificado de autenticación de servidor CMG desde una entidad de certificación en la que los clientes no confían automáticamente, debe agregar el certificado raíz de confianza de la entidad de certificación a los clientes basados en Internet.
    - También puede usar perfiles de certificado de Configuration Manager para aprovisionar certificados en los clientes. Para obtener más información, vea [Introducción a los perfiles de certificado](/sccm/protect/deploy-use/introduction-to-certificate-profiles).

### <a name="server-authentication-certificate-issued-by-public-provider"></a>Certificado de autenticación de servidor emitido por un proveedor público

Cuando use este método, los clientes confiarán automáticamente en el certificado y no tendrá que crear un certificado personalizado usted mismo. Configuration Manager crea el servicio en Azure con el dominio cloudapp.net. Un proveedor de certificados públicos no puede emitir para usted un certificado con este nombre. Siga este procedimiento para crear un alias DNS:

1. Crear un registro de nombre canónico (CNAME) en el DNS público de su organización. Este registro crea un alias para CMG para el nombre descriptivo que se usa en el certificado público.
Por ejemplo, Contoso asigna a CMG el nombre **GraniteFalls**, que se convierte en **GraniteFalls.CloudApp.Net** en Azure. En el DNS espacio de nombres público de Contoso, contoso.com, el administrador de DNS crea un registro CNAME para **GraniteFalls.Contoso.com** con el nombre del host real, **GraniteFalls.CloudApp.net**.
2. Con el nombre común (CN) del alias de CNAME, solicite un certificado de autenticación de servidor de un proveedor público.
Por ejemplo, Contoso usa **GraniteFalls.Contoso.com** como CN del certificado.
3. Cree la instancia de CMG en la consola de Configuration Manager mediante este certificado. En la página **Configuración** del Asistente para crear una instancia de Cloud Management Gateway: 
    - Al agregar el certificado de servidor para este servicio en la nube (desde el **archivo de certificado**), el asistente extrae el nombre de host del nombre común del certificado como nombre del servicio. 
    - Después, anexa ese nombre de host a **cloudapp.net**, o a **usgovcloudapp.net** para la nube de Azure US Government , como FQDN de servicio para crear el servicio en Azure.
    - Por ejemplo, cuando Contoso crea la instancia de CMG, Configuration Manager extrae el nombre de host **GraniteFalls** desde el nombre común del certificado. Azure crea el servicio real como **GraniteFalls.CloudApp.net**.

### <a name="server-authentication-certificate-issued-from-enterprise-pki"></a>Certificado de autenticación de servidor emitido por una PKI de empresa

Cree un certificado SSL personalizado para CMG tal como haría para un punto de distribución en la nube. Siga las instrucciones de [Implementación del certificado de servicio para puntos de distribución basados en la nube](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_clouddp2008_cm2012), pero con las siguientes diferencias:

- Cuando se solicita el certificado de servidor web personalizado, proporcione un FQDN para el nombre común del certificado. Para usar CMG en la nube pública de Azure, use un nombre que termine en **cloudapp.net**, o **usgovcloudapp.net** para la nube de Azure US Government.



## <a name="azure-management-certificate"></a>Certificado de administración de Azure

*Este certificado es necesario para las implementaciones del servicio clásico. No hace falta para las implementaciones de Azure Resource Manager.*

Este certificado se proporciona en Azure Portal y al crear la instancia de CMG en la consola de Configuration Manager.

Para crear la instancia de CMG en Azure, el punto de conexión de servicio de Configuration Manager debe autenticarse primero en su suscripción de Azure. Cuando se usa una implementación del servicio clásico, emplea el certificado de administración de Azure para esta autenticación. Un administrador de Azure cargará este certificado en su suscripción. Cuando cree la instancia de CMG en la consola de Configuration Manager, proporcione este certificado.

Para obtener más información e instrucciones sobre cómo cargar un certificado de administración, vea los artículos siguientes de la documentación de Azure:

- [Servicios en la nube y certificados de administración](/azure/cloud-services/cloud-services-certs-create#what-are-management-certificates)

- [Cargar un certificado de administración de Azure Service](/azure/azure-api-management-certs)

> [!IMPORTANT]
> Asegúrese de copiar el identificador de suscripción asociado al certificado de administración, Lo usará para crear la instancia de CMG en la consola de Configuration Manager.



## <a name="client-authentication-certificate"></a>Certificado de autenticación del cliente

*Este certificado es necesario para los clientes basados en Internet que ejecutan Windows 7, Windows 8.1 y dispositivos de Windows 10 no unidos a Azure Active Directory (Azure AD). También es necesario en el punto de conexión de CMG. No hace falta para los clientes de Windows 10 unidos a Azure AD.*

Los clientes usan este certificado al autenticarse con CMG. Los dispositivos de Windows 10 híbridos o unidos a un dominio en la nube no necesitan este certificado porque usan Azure AD para autenticarse.

Aprovisione este certificado fuera del contexto de Configuration Manager. Por ejemplo, use Servicios de certificados de Active Directory y una directiva de grupo para emitir certificados de autenticación de cliente. Para obtener más información, vea [Implementación del certificado de cliente para equipos Windows](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_client2008_cm2012).


### <a name="client-trusted-root-certificate-to-cmg"></a>Certificado raíz de confianza de cliente para CMG

*Este certificado es necesario cuando se usan certificados de autenticación de cliente. Cuando todos los clientes usan Azure AD para la autenticación, este certificado no hace falta.* 

Este certificado se proporciona al crear la instancia de CMG en la consola de Configuration Manager.

CMG debe confiar en los certificados de autenticación de cliente. Para conseguir esta relación de confianza, proporcione la cadena de certificados raíz de confianza. Puede especificar dos entidades de certificación raíz de confianza y cuatro entidades de certificación intermedias (subordinadas). 


#### <a name="export-the-client-certificates-trusted-root"></a>Exportar la raíz de confianza del certificado de cliente

Después de emitir un certificado de autenticación de cliente a un equipo, siga este proceso en ese equipo para exportar la raíz de confianza.

1.  Abra el menú Inicio. Escriba "ejecutar" para abrir la ventana de ejecución. Abra **mmc**. 

2.  En el menú Archivo, elija **Agregar o quitar complemento**.

3.  En el cuadro de diálogo Agregar o quitar complementos, seleccione **Certificados** y haga clic en **Agregar**. 
    a. En el cuadro de diálogo Complemento de certificados, seleccione **Cuenta de equipo** y haga clic en **Siguiente**. 
    b. En el cuadro de diálogo Seleccionar equipo, seleccione **Equipo local** y haga clic en **Finalizar**. 
    c. En el cuadro de diálogo Agregar o quitar complementos, haga clic en **Aceptar**.

4.  Expanda **Certificados**, expanda **Personal** y seleccione **Certificados**.

5.  Seleccione un certificado cuyo uso previsto sea **Autenticación de cliente**. 
    a. En el menú Acción, seleccione **Abrir**. 
    b. Cambie a la pestaña **Ruta de certificación**. c. Seleccione el certificado siguiente en la cadena y haga clic en **Ver certificado**.

6.  En este nuevo cuadro de diálogo de certificado, cambie a la pestaña **Detalles**. Haga clic en **Copiar en archivo…**

7.  Complete el Asistente para exportar certificados con el formato de certificado predeterminado, **DER binario codificado X.509 (.CER)**. Anote el nombre y la ubicación del certificado exportado.

8. Exporte todos los certificados de la ruta de acceso de certificación del certificado de autenticación del cliente original. Tome nota de qué certificados exportados son entidades de certificación intermedias y cuáles son entidades de certificación raíz de confianza.



## <a name="enable-management-point-for-https"></a>Habilitar un punto de administración para HTTPS

*Requisitos de certificados*
- En las versiones 1706 o 1710, cuando se administran clientes tradicionales con una identidad local mediante un certificado de autenticación de cliente, este certificado es recomendable pero no obligatorio.
- En la versión 1710, cuando se administran clientes de Windows 10 unidos a Azure AD, este certificado es necesario para los puntos de administración. 
- A partir de la versión 1802, este certificado es necesario en todos los escenarios. 

Aprovisione este certificado fuera del contexto de Configuration Manager. Por ejemplo, use Servicios de certificados de Active Directory y una directiva de grupo para emitir un certificado de servidor web. Para obtener más información, vea [Requisitos de certificados PKI ](/sccm/core/plan-design/network/pki-certificate-requirements) e [Implementación del certificado de servidor web para sistemas de sitio que ejecutan IIS](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_webserver2008_cm2012).



## <a name="next-steps"></a>Pasos siguientes

- [Configurar puerta de enlace de administración en la nube](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)
- [Preguntas más frecuentes sobre Cloud Management Gateway](/sccm/core/clients/manage/cmg/cloud-management-gateway-faq)
- [Seguridad y privacidad de la puerta de enlace de administración en la nube](/sccm/core/clients/manage/cmg/security-and-privacy-for-cloud-management-gateway)
