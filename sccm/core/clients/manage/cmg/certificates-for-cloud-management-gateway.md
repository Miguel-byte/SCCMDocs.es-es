---
title: Certificados de CMG
description: Obtenga información sobre los diferentes certificados digitales que se usan con Cloud Management Gateway.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 11/27/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 71eaa409-b955-45d6-8309-26bf3b3b0911
ms.collection: M365-identity-device-management
ms.openlocfilehash: 69c5f446c465655adb1e9fee1b891a3152af47e9
ms.sourcegitcommit: f38ef9afb0c608c0153230ff819e5f5e0fb1520c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/19/2019
ms.locfileid: "58197102"
---
# <a name="certificates-for-the-cloud-management-gateway"></a>Certificados para Cloud Management Gateway

*Se aplica a: System Center Configuration Manager (Rama actual)*

Según el escenario que use para administrar clientes en Internet con Cloud Management Gateway (CMG), necesita uno o varios de los certificados digitales siguientes:  

- [Certificado de autenticación de servidor CMG](#bkmk_serverauth)  
    - [Certificado raíz de confianza de CMG para clientes](#bkmk_cmgroot)  
    - [Certificado de autenticación de servidor emitido por un proveedor público](#bkmk_serverauthpublic)  
    - [Certificado de autenticación de servidor emitido por una PKI de empresa](#bkmk_serverauthpki)  

- [Certificado de administración de Azure](#bkmk_azuremgmt)  

- [Certificado de autenticación del cliente](#bkmk_clientauth)  
    - [Certificado raíz de confianza de cliente para CMG](#bkmk_clientroot)  

- [Habilitar un punto de administración para HTTPS](#bkmk_mphttps)  


Para obtener más información sobre los diferentes escenarios, vea [Plan for cloud management gateway](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway) (Planificación para Cloud Management Gateway).


### <a name="general-information"></a>Información general
<!--SCCMDocs issue #779-->
Los certificados para Cloud Management Gateway admiten las siguientes configuraciones:  

- Longitud de clave de 2048 o 4096 bits

- A partir de la versión 1710, compatibilidad con proveedores de almacenamiento de claves para claves privadas de certificado. Para obtener más información, consulte [Introducción a los certificados CNG](/sccm/core/plan-design/network/cng-certificates-overview).  

- A partir de la versión 1802, al configurar Windows con la siguiente directiva: **Criptografía de sistema: use algoritmos que cumplan la norma FIPS para cifrado, aplicación de algoritmo hash y firma**.  

- A partir de la versión 1802, es compatible con **TLS 1.2**. Para más información, vea [Referencia técnica de controles criptográficos](/sccm/core/plan-design/security/cryptographic-controls-technical-reference#about-ssl-vulnerabilities).  



## <a name="bkmk_serverauth"></a> Certificado de autenticación de servidor CMG

*Este certificado es necesario en todos los escenarios.*

Este certificado se proporciona al crear la instancia de CMG en la consola de Configuration Manager.

CMG crea un servicio HTTPS al que se conectan los clientes basados en Internet. El servidor requiere un certificado de autenticación de servidor para crear el canal seguro. Puede adquirir un certificado para este fin de un proveedor público o emitirlo desde su propia infraestructura de clave pública (PKI). Para obtener más información, vea [Certificado raíz de confianza de CMG para clientes](#cmg-trusted-root-certificate-to-clients).

 > [!TIP]
 > Este certificado requiere un nombre único global para identificar el servicio de Azure. Antes de solicitar un certificado, confirme que el nombre de dominio de Azure deseado sea único. Por ejemplo, *GraniteFalls.CloudApp.Net*. Inicie sesión en [Microsoft Azure Portal](https://portal.azure.com). Seleccione **Crear un recurso**, elija la categoría **Proceso** y seleccione **Servicio en la nube**. En el campo **Nombre DNS**, escriba el prefijo deseado, por ejemplo, *GraniteFalls*. La interfaz mostrará si el nombre de dominio está disponible o si ya está en uso por otro servicio. No cree el servicio en el portal, simplemente use este proceso para comprobar si el nombre está disponible. 
  
 > [!TIP]
 > Si CMG también se va a habilitar como punto de distribución en la nube, confirme que el nombre del servicio CMG que ha elegido no exista tampoco como nombre de cuenta de Azure Storage. Por ejemplo, *GraniteFalls*. Inicie sesión en [Microsoft Azure Portal] (https://portal.azure.com). Seleccione **Crear un recurso**, elija la categoría **Almacenamiento** y, después, elija **Cuenta de almacenamiento: blob, archivo, tabla, cola**. Haga clic en **Crear** y, en **Detalles de instancia**, escriba el mismo nombre elegido para el servicio CMG, por ejemplo, *GraniteFalls*. La interfaz mostrará si el nombre de la cuenta de almacenamiento está disponible o si ya lo está usando otro servicio. No cree la cuenta de almacenamiento en el portal, simplemente use este proceso para comprobar si el nombre está disponible. Si el nombre del servicio CMG en la nube no existe, pero sí el de la cuenta de Storage, el aprovisionamiento no se realizará correctamente.
 
 > [!NOTE]
 > A partir de la versión 1802, el certificado de autenticación de servidor de CMG admite caracteres comodín. Algunas entidades de certificación emiten certificados con un carácter comodín para el nombre de host. Por ejemplo, **\*.contoso.com**. Algunas organizaciones usan certificados con caracteres comodín para simplificar sus PKI y reducir los costos de mantenimiento.<!--491233-->  
 > 
 > Para más información sobre cómo usar un certificado comodín con una instancia de CMG, vea [Configurar una instancia de CMG](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway#set-up-a-cmg).<!--SCCMDocs issue #565-->  


### <a name="bkmk_cmgroot"></a> Certificado raíz de confianza de CMG para clientes

Los clientes deben confiar en el certificado de autenticación de servidor CMG. Hay dos métodos para conseguir esta relación de confianza: 

- Usar un certificado de un proveedor de certificados público y de confianza global. Por ejemplo, DigiCert, VeriSign o Thawte, entre otros. Los clientes de Windows incluyen entidades de certificación raíz de confianza (CA) de estos proveedores. Al usar un certificado de autenticación de servidor emitido por uno de estos proveedores, los clientes confían automáticamente en él.  

- Usar un certificado emitido por una entidad de certificación de empresa de la infraestructura de clave pública (PKI). La mayoría de las implementaciones de PKI de empresa agregan las entidades de certificación raíz de confianza a clientes de Windows. Por ejemplo, mediante el uso de Servicios de certificados de Active Directory con una directiva de grupo. Si emite el certificado de autenticación de servidor CMG desde una entidad de certificación en la que los clientes no confían automáticamente, agregue el certificado raíz de confianza de la entidad de certificación a los clientes basados en Internet.  

    - También puede usar perfiles de certificado de Configuration Manager para aprovisionar certificados en los clientes. Para obtener más información, vea [Introducción a los perfiles de certificado](/sccm/protect/deploy-use/introduction-to-certificate-profiles).  

> [!Note]  
> A partir de la versión 1806, para crear una instancia de CMG ya no es necesario proporcionar un certificado raíz de confianza en la página Configuración. Este certificado no es necesario cuando se usa Azure Active Directory (Azure AD) para la autenticación de cliente, pero solía ser necesario en el asistente. Si usa certificados de autenticación de cliente PKI, entonces todavía debe agregar un certificado raíz de confianza a la CMG.<!--SCCMDocs-pr issue #2872-->  


### <a name="bkmk_serverauthpublic"></a> Certificado de autenticación de servidor emitido por un proveedor público

Un proveedor de certificados de terceros no puede crear un certificado para CloudApp.net, ya que el dominio es propiedad de Microsoft. Solo puede obtener un certificado emitido para un dominio que sea de su propiedad. La razón principal para adquirir un certificado de un proveedor de terceros es que los clientes ya confíen en el certificado raíz de dicho proveedor.

Siga este procedimiento para crear un alias DNS:

1. Crear un registro de nombre canónico (CNAME) en el DNS público de su organización. Este registro crea un alias para CMG para el nombre descriptivo que se usa en el certificado público.

    Por ejemplo, Contoso asigna a CMG el nombre **GraniteFalls**, que se convierte en **GraniteFalls.CloudApp.Net** en Azure. En el DNS espacio de nombres público de Contoso, contoso.com, el administrador de DNS crea un registro CNAME para **GraniteFalls.Contoso.com** con el nombre del host real, **GraniteFalls.CloudApp.net**.  

2. Con el nombre común (CN) del alias de CNAME, solicite un certificado de autenticación de servidor de un proveedor público.
Por ejemplo, Contoso usa **GraniteFalls.Contoso.com** como CN del certificado.  

3. Cree la instancia de CMG en la consola de Configuration Manager mediante este certificado. En la página **Configuración** del Asistente para crear una instancia de Cloud Management Gateway:   

    - Al agregar el certificado de servidor para este servicio en la nube (desde el **archivo de certificado**), el asistente extrae el nombre de host del nombre común del certificado como nombre del servicio.  

    - Después, anexa ese nombre de host a **cloudapp.net**, o a **usgovcloudapp.net** para la nube de Azure US Government , como FQDN de servicio para crear el servicio en Azure.  

    - Por ejemplo, cuando Contoso crea la instancia de CMG, Configuration Manager extrae el nombre de host **GraniteFalls** desde el nombre común del certificado. Azure crea el servicio real como **GraniteFalls.CloudApp.net**.  

Al crear la instancia de CMG en Configuration Manager, aunque el certificado contiene GraniteFalls.Contoso.com, Configuration Manager solo extrae el nombre de host, por ejemplo: GraniteFalls. Este nombre de host se anexa a CloudApp.net, que Azure necesita al crear un servicio en la nube. El alias CNAME del espacio de nombres DNS para el dominio, Contoso.com, asigna estos dos FQDN conjuntamente. Configuration Manager ofrece a los clientes una directiva para acceder a esta instancia de CMG y la asignación de DNS los une, para que puedan acceder de forma segura al servicio de Azure.<!--SCCMDocs issue #565-->  


### <a name="bkmk_serverauthpki"></a> Certificado de autenticación de servidor emitido por una PKI de empresa

Cree un certificado SSL personalizado para CMG tal como haría para un punto de distribución en la nube. Siga las instrucciones de [Implementación del certificado de servicio para puntos de distribución basados en la nube](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_clouddp2008_cm2012), pero con las siguientes diferencias:

- Cuando se solicita el certificado de servidor web personalizado, proporcione un FQDN para el nombre común del certificado. Este nombre puede ser un nombre de dominio público que ya tenga, o bien puede usar el dominio cloudapp.net. Si usa su propio dominio público, consulte el proceso anterior para crear un alias de DNS en el DNS público de su organización.  

- Al usar el dominio público cloudapp.net para el certificado de servidor web CMG:  

    - En la nube pública de Azure, use un nombre que termine en **cloudapp.net**.  

    - Use un nombre que termine en **usgovcloudapp.net** para la nube del Gobierno de los EE. UU. de Azure.  



## <a name="bkmk_azuremgmt"></a> Certificado de administración de Azure

*Este certificado es necesario para las implementaciones del servicio clásico. No hace falta para las implementaciones de Azure Resource Manager.*

> [!Important]  
> A partir de la versión 1810, las implementaciones de servicio clásico de Azure estarán en desuso en Configuration Manager. Empiece a usar implementaciones de Azure Resource Manager para Cloud Management Gateway. Para obtener más información, vea [Planear para Cloud Management Gateway](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#azure-resource-manager).

Este certificado se proporciona en Azure Portal y al crear la instancia de CMG en la consola de Configuration Manager.

Para crear la instancia de CMG en Azure, el punto de conexión de servicio de Configuration Manager debe autenticarse primero en su suscripción de Azure. Cuando se usa una implementación del servicio clásico, emplea el certificado de administración de Azure para esta autenticación. Un administrador de Azure cargará este certificado en su suscripción. Cuando cree la instancia de CMG en la consola de Configuration Manager, proporcione este certificado.

Para obtener más información e instrucciones sobre cómo cargar un certificado de administración, vea los artículos siguientes de la documentación de Azure:

- [Servicios en la nube y certificados de administración](https://docs.microsoft.com/azure/cloud-services/cloud-services-certs-create#what-are-management-certificates)  

- [Cargar un certificado de administración de Azure Service](https://docs.microsoft.com/azure/azure-api-management-certs)  

> [!IMPORTANT]
> Asegúrese de copiar el identificador de suscripción asociado al certificado de administración, Lo usará para crear la instancia de CMG en la consola de Configuration Manager.



## <a name="bkmk_clientauth"></a> Certificado de autenticación del cliente

*Este certificado es necesario para los clientes basados en Internet que ejecutan Windows 7, Windows 8.1 y dispositivos de Windows 10 no unidos a Azure Active Directory (Azure AD). También es necesario en el punto de conexión de CMG. No hace falta para los clientes de Windows 10 que usen Azure AD.*

Los clientes usan este certificado al autenticarse con CMG. Los dispositivos de Windows 10 híbridos o unidos a un dominio en la nube no necesitan este certificado porque usan Azure AD para autenticarse.

Aprovisione este certificado fuera del contexto de Configuration Manager. Por ejemplo, use Servicios de certificados de Active Directory y una directiva de grupo para emitir certificados de autenticación de cliente. Para obtener más información, vea [Implementación del certificado de cliente para equipos Windows](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_client2008_cm2012).

El punto de conexión de CMG requiere este certificado para reenviar las solicitudes de cliente a un punto de administración HTTPS de forma segura. Si usa Azure AD o HTTP mejorado, este certificado no es necesario. Para obtener más información, vea [Enable management point for HTTPS](#bkmk_mphttps) (Habilitar el punto de administración para HTTPS).


### <a name="bkmk_clientroot"></a> Certificado raíz de confianza de cliente para CMG

*Este certificado es necesario cuando se usan certificados de autenticación de cliente. Cuando todos los clientes usan Azure AD para la autenticación, este certificado no hace falta.* 

Este certificado se proporciona al crear la instancia de CMG en la consola de Configuration Manager.

CMG debe confiar en los certificados de autenticación de cliente. Para conseguir esta relación de confianza, proporcione la cadena de certificados raíz de confianza. Puede especificar dos entidades de certificación raíz de confianza y cuatro entidades de certificación intermedias (subordinadas). 


#### <a name="export-the-client-certificates-trusted-root"></a>Exportar la raíz de confianza del certificado de cliente

Después de emitir un certificado de autenticación de cliente a un equipo, siga este proceso en ese equipo para exportar la raíz de confianza.

1.  Abra el menú Inicio. Escriba "ejecutar" para abrir la ventana de ejecución. Abra `mmc`.  

2.  En el menú Archivo, elija **Agregar o quitar complemento**.  

3.  En el cuadro de diálogo Agregar o quitar complementos, seleccione **Certificados** y **Agregar**.  

    a. En el cuadro de diálogo Complemento de certificados, seleccione **Cuenta de equipo** y **Siguiente**.  

    b. En el cuadro de diálogo Seleccionar equipo, seleccione **Equipo local** y **Finalizar**.  

    c. En el cuadro de diálogo Agregar o quitar complementos, seleccione **Aceptar**.  

4.  Expanda **Certificados**, expanda **Personal** y seleccione **Certificados**.  

5.  Seleccione un certificado cuyo uso previsto sea **Autenticación de cliente**.  

    a. En el menú Acción, seleccione **Abrir**.  

    b. Vaya a la pestaña **Ruta de certificación**.  

    c. Seleccione el certificado siguiente en la cadena y seleccione **Ver certificado**.  

6.  En este nuevo cuadro de diálogo de certificado, vaya a la pestaña **Detalles**. Seleccione **Copiar en archivo…**.  

7.  Complete el Asistente para exportar certificados con el formato de certificado predeterminado, **DER binario codificado X.509 (.CER)**. Anote el nombre y la ubicación del certificado exportado.  

8. Exporte todos los certificados de la ruta de acceso de certificación del certificado de autenticación del cliente original. Tome nota de qué certificados exportados son entidades de certificación intermedias y cuáles son entidades de certificación raíz de confianza.  



## <a name="bkmk_mphttps"></a> Habilitar un punto de administración para HTTPS

Aprovisione este certificado fuera del contexto de Configuration Manager. Por ejemplo, use Servicios de certificados de Active Directory y una directiva de grupo para emitir un certificado de servidor web. Para obtener más información, vea [Requisitos de certificados PKI ](/sccm/core/plan-design/network/pki-certificate-requirements) e [Implementación del certificado de servidor web para sistemas de sitio que ejecutan IIS](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_webserver2008_cm2012).


- En la versión 1710, cuando se administran clientes tradicionales con una identidad local mediante un certificado de autenticación del cliente, este certificado es recomendable pero no obligatorio. Cuando se administran clientes de Windows 10 unidos a Azure AD, este certificado es necesario para los puntos de administración.

- En la versión 1802, este certificado es necesario en todos los escenarios. Solo los puntos de administración que habilite para CMG deben ser HTTPS. Este cambio de comportamiento proporciona una mejor compatibilidad con la autenticación basada en tokens de Azure AD.  

- A partir de la versión 1806, cuando se usa la opción del sitio **Usar los certificados generados por Configuration Manager para sistemas de sitios HTTP**, el punto de administración puede ser HTTP. Para obtener más información, vea [HTTP mejorado](/sccm/core/plan-design/hierarchy/enhanced-http).

### <a name="management-point-client-connection-mode-summary"></a>Resumen del modo de conexión de cliente de punto de administración
En estas tablas se resume si el punto de administración requiere HTTP o HTTPS, en función del tipo de cliente y versión del sitio.

#### <a name="for-internet-based-clients-communicating-with-the-cloud-management-gateway"></a>Para la comunicación de clientes basada en Internet con Cloud Management Gateway
Configure un punto de administración local para permitir conexiones desde la instancia de CMG con el modo de conexión de cliente siguiente:

| Tipo de cliente   | 1710        | 1802        | 1806        | 1810        |
|------------------|-------------|-------------|-------------|-------------|
| Grupo de trabajo        | HTTP, HTTPS | HTTPS       | E-HTTP<sup>[Nota 1](#bkmk_note1)</sup>, HTTPS | E-HTTP<sup>[Nota 1](#bkmk_note1)</sup>, HTTPS |
| Unido a dominio de AD | HTTP, HTTPS | HTTPS       | E-HTTP<sup>[Nota 1](#bkmk_note1)</sup>, HTTPS | E-HTTP<sup>[Nota 1](#bkmk_note1)</sup>, HTTPS |
| Unidos a Azure AD  | HTTPS       | HTTPS       | E-HTTP, HTTPS | E-HTTP, HTTPS |
| Unido a híbrido    | HTTP, HTTPS | HTTPS       | E-HTTP, HTTPS | E-HTTP, HTTPS |

<a name="bkmk_note1"></a> 

> [!Note]  
> **Nota 1**: Esta configuración requiere que el cliente tenga un [certificado de autenticación del cliente](#bkmk_clientauth) y solo es compatible con escenarios centrados en el dispositivo.  

#### <a name="for-on-premises-clients-communicating-with-the-on-premises-management-point"></a>Para la comunicación de clientes locales con el punto de administración local
Configure un punto de administración local con el modo de conexión de cliente siguiente:

| Tipo de cliente   | 1710        | 1802        | 1806        | 1810        |
|------------------|-------------|-------------|-------------|-------------|
| Grupo de trabajo        | HTTP, HTTPS | HTTP, HTTPS | HTTP, HTTPS | HTTP, HTTPS |
| Unido a dominio de AD | HTTP, HTTPS | HTTP, HTTPS | HTTP, HTTPS | HTTP, HTTPS |
| Unidos a Azure AD  | HTTPS       | HTTPS       | HTTPS       | HTTPS       |
| Unido a híbrido    | HTTP, HTTPS | HTTP, HTTPS | HTTP, HTTPS | HTTP, HTTPS |

> [!Note]  
> En la versión 1806, los clientes unidos a un dominio de AD admiten los escenarios centrados en el dispositivo y el usuario para la comunicación con un punto de administración HTTP o HTTPS.  
> 
> Los clientes unidos a Azure AD y a híbrido se pueden comunicar a través de HTTP para los escenarios centrados en el dispositivo, pero necesitan E-HTTP o HTTPS para habilitar los escenarios centrados en el usuario. En caso contrario, se comportan igual que los clientes del grupo de trabajo.  


#### <a name="legend-of-terms"></a>Leyenda de términos
- *Grupo de trabajo*: el dispositivo no está unido a un dominio ni a Azure AD, pero tiene un [certificado de autenticación del cliente](#bkmk_clientauth).  
- *Unido a dominio de AD*: el dispositivo se une un dominio de Active Directory local.  
- *Unido a Azure AD*: también conocido como "unido a un dominio en la nube", el dispositivo se une a un inquilino de Azure Active Directory.  
- *Unido a híbrido*: el dispositivo se une a un dominio de Active Directory y un inquilino de Azure AD.  
- *HTTP*: en las propiedades del punto de administración, las conexiones de cliente se establecen en **HTTP**.  
- *HTTPS*: en las propiedades del punto de administración, las conexiones de cliente se establecen en **HTTPS**.  
- *E-HTTP*: en las propiedades del sitio, en la pestaña Comunicación de equipo cliente, la configuración del sistema de sitio se establece en **HTTPS o HTTP**, y se habilita la opción para **usar los certificados generados por Configuration Manager para sistemas de sitios HTTP**. Configurará el punto de administración para HTTP; el punto de administración de HTTP está preparado para comunicaciones HTTP y HTTPS (escenarios de autenticación por tokens).   



## <a name="next-steps"></a>Pasos siguientes

- [Configurar puerta de enlace de administración en la nube](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)  

- [Preguntas más frecuentes sobre Cloud Management Gateway](/sccm/core/clients/manage/cmg/cloud-management-gateway-faq)  

- [Seguridad y privacidad de la puerta de enlace de administración en la nube](/sccm/core/clients/manage/cmg/security-and-privacy-for-cloud-management-gateway)  
