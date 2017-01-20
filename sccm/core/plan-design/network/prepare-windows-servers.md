---
title: Preparar los servidores de Windows | System Center Configuration Manager
description: "Asegúrese de que un equipo cumpla los requisitos previos para su uso como servidor de sitio o servidor del sistema de sitio de System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 2aca914f-641e-4bc8-98d4-bbf0a2a5276f
caps.latest.revision: 10
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: f0a1cc32285fcb792c3f4cdec616668474708404
ms.openlocfilehash: acf8a401f1ce67a4d8c905c0126c031b97484271


---
# <a name="prepare-windows-servers-to-support-system-center-configuration-manager"></a>Preparar los servidores de Windows para admitir System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Para poder usar un equipo Windows como servidor de sistema de sitio para System Center Configuration Manager, debe asegurarse de que el equipo cumple los requisitos previos para su uso previsto como servidor de sitio o servidor de sistema de sitio.  

-   A menudo, incluyen una o varias características o roles de Windows, que se habilitan con el Administrador del servidor de los equipos.  

-   Como el método para habilitar los roles y características de Windows difiere en los distintos sistemas operativos, vea la documentación de su sistema operativo para obtener información detallada acerca de cómo configurar los sistemas operativos que usa.  

Este artículo proporciona información general sobre los tipos de configuraciones de Windows que son necesarios para admitir sistemas de sitio de Configuration Manager. Para obtener información detallada sobre la configuración de roles de sistema de sitio específicos, consulte [Site and site system prerequisites](/sccm/core/plan-design/configs/site-and-site-system-prerequisites) (Requisitos previos de los sitios y de los sistemas de sitio).

##  <a name="a-namebkmkwinfeaturesa-windows-features-and-roles"></a><a name="BKMK_WinFeatures"></a> Roles y características de Windows  
 Al configurar los roles y características de Windows en un equipo, puede ser necesario reiniciar el equipo para completar la configuración. Por lo tanto, se recomienda identificar los equipos que van a hospedar los roles de sistema de sitio antes de instalar un servidor de sitio o de sistema de sitio de Configuration Manager.
### <a name="features"></a>Funciones  
 se requieren las siguientes características de Windows en determinados servidores de sistema de sitio. Estas deben configurarse antes de instalar un rol de sistema de sitio en ese equipo.  

-   **.NET Framework**: que incluye  

    -   ASP.NET  

    -   Activación HTTP  

    -   Activación no HTTP  

    -   Servicios WCF  

    Los diferentes roles de sistema de sitio requieren diferentes versiones de .NET Framework.  

    Como .NET Framework 4.0 y versiones posteriores no pueden reemplazar la versión 3.5 y anteriores, si las distintas versiones se indican como necesarias, planee habilitar cada versión en el mismo equipo.  

-   **Servicios de transferencia inteligente en segundo plano (BITS)**: los puntos de administración requieren BITS (y opciones seleccionadas automáticamente) para permitir la comunicación con dispositivos administrados.  

-   **BranchCache**: los puntos de distribución pueden configurarse con BranchCache para admitir clientes que usan BranchCache.  

-   **Desduplicación de datos**: se pueden configurar puntos de distribución con desduplicación de datos para que se beneficien de esta característica.  

-   **Compresión diferencial remota (RDC)**: cada equipo que hospeda un servidor de sitio o un punto de distribución requiere RDC.   
    RDC se usa para generar firmas de paquete y realizar comparaciones de firma.  

### <a name="roles"></a>Roles  
 se requieren los siguientes roles de Windows para admitir determinadas funcionalidades, como las actualizaciones de software y las implementaciones de sistema operativo, mientras que los roles de sistema de sitio más comunes requieren IIS.  

 -   **Servicio de inscripción de dispositivos de red** (en Servicios de certificados de Active Directory): este rol de Windows es un requisito previo para el uso de perfiles de certificado en Configuration Manager.  

 -   **Servidor web (IIS)**, que incluye:  

    -   Características HTTP comunes >  

        -   Redirección HTTP  

    -   Desarrollo de aplicaciones >  

        -   Extensibilidad de .NET  

        -   ASP.NET  

        -   Extensiones ISAPI  

        -   Filtros ISAPI  

    -   Herramientas de administración >  

        -   Compatibilidad con la administración de IIS 6  

        -   Compatibilidad con la metabase de IIS 6  

        -   Compatibilidad con WMI de IIS 6  

    -   Seguridad >  

        -   Filtrado de solicitudes  

        -   Autenticación de Windows  

 Los siguientes roles de sistema de sitio usan una o varias de las configuraciones de IIS mostradas:  

    -   Punto de servicio web del catálogo de aplicaciones  

    -   Punto de sitios web del catálogo de aplicaciones  

    -   Punto de distribución  

    -   Punto de inscripción  

    -   Punto de proxy de inscripción  

    -   Punto de estado de reserva  

    -   Punto de administración  

    -   Punto de actualización de software  

    -   Punto de migración de estado  

    La versión mínima de IIS requerida es la versión suministrada con el sistema operativo del servidor de sitio.  

    Además de estas configuraciones de IIS, quizás tenga que configurar [Filtrado de solicitudes IIS para puntos de distribución](#BKMK_IISFiltering).  

-   **Servicios de implementación de Windows**: este rol se utiliza con la implementación del sistema operativo.  

-   **Windows Server Update Services**: este rol es necesario para implementar actualizaciones de software.  

##  <a name="a-namebkmkiisfilteringa-iis-request-filtering-for-distribution-points"></a><a name="BKMK_IISFiltering"></a> Filtrado de solicitudes IIS para puntos de distribución  
 De forma predeterminada, IIS usa el filtrado de solicitudes para impedir el acceso a varias extensiones de nombre de archivo y ubicaciones de carpetas mediante la comunicación HTTP o HTTPS. En un punto de distribución, esto impide que los clientes descarguen paquetes que contienen extensiones o ubicaciones de carpeta bloqueadas.  

 Cuando los archivos de origen de paquete contienen extensiones bloqueadas en IIS por la configuración del filtrado de solicitudes, debe configurar el filtrado de solicitudes para que las permita. Para ello, [edite la característica de filtrado de solicitudes](https://technet.microsoft.com/library/hh831621.aspx) en el Administrador de IIS, en los equipos de los puntos de distribución.  

 Además, Configuration Manager usa las siguientes extensiones de nombre de archivo para paquetes y aplicaciones. Asegúrese de que la configuración del filtrado de solicitudes no bloquea estas extensiones de archivo:  

-   .PCK  

-   .PKG  

-   .STA  

-   .TAR  

Por ejemplo, puede tener archivos de origen para una implementación de software entre los que se incluye una carpeta llamada **bin**, o un archivo con la extensión de nombre de archivo **.mdb** .  

-   De forma predeterminada, el filtrado de solicitudes de IIS bloquea el acceso a estos elementos (**bin** se bloquea como segmento oculto y **.mdb** se bloquea como extensión de nombre de archivo).  

-   Cuando se usa la configuración de IIS predeterminada en un punto de distribución, los clientes que usan BITS no pueden descargar esta implementación de software desde el punto de distribución e indican que están esperando contenido.  

-   Para que los clientes puedan descargar este contenido, en cada punto de distribución correspondiente, edite el **filtrado de solicitudes** en el Administrador de IIS para permitir el acceso a las extensiones de archivo y las carpetas incluidas en los paquetes y las aplicaciones que implemente.  

> [!IMPORTANT]  
>  Las modificaciones que se realicen en el filtro de solicitudes pueden aumentar la superficie del equipo expuesta a ataques.  
>   
>  -   Las modificaciones que se realicen en el nivel de servidor se aplican a todos los sitios web del servidor.  
> -   Las modificaciones que se realicen en sitios web individuales se aplican solo a ese sitio web.  
>   
>  Como recomendación de seguridad, se aconseja ejecutar Configuration Manager en un servidor web dedicado. Si debe ejecutar otras aplicaciones en el servidor web, use un sitio web personalizado para Configuration Manager. Para obtener información, consulte [Websites for site system servers in System Center Configuration Manager](../../../core/plan-design/network/websites-for-site-system-servers.md) (Sitios web para servidores de sistema de sitio en System Center Configuration Manager).  

## <a name="http-verbs"></a>Verbos HTTP
**Puntos de administración:** para garantizar que los clientes puedan comunicarse correctamente con un punto de administración, en el servidor de punto de administración, asegúrese de que los verbos HTTP enumerados a continuación estén permitidos.  
 - GET
 - POST
 - CCM_POST
 - HEAD
 - PROPFIND

**Puntos de distribución:** los puntos de distribución requieren que los verbos HTTP enumerados a continuación estén permitidos.
 - GET
 - HEAD
 - PROFIND

Para obtener información sobre cómo configurar el filtrado de solicitudes, consulte [Configurar el filtrado de solicitudes en IIS](https://technet.microsoft.com/library/hh831621.aspx#Verbs) en TechNet u otra documentación parecida que se aplique a la versión de Windows Server que hospeda su punto de administración.



<!--HONumber=Nov16_HO1-->


