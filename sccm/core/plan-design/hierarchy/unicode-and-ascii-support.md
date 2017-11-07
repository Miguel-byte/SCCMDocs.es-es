---
title: Compatibilidad con Unicode y ASCII
titleSuffix: Configuration Manager
description: "Obtenga información sobre la compatibilidad con caracteres Unicode y ASCII en objetos de System Center Configuration Manager."
ms.custom: na
ms.date: 3/1/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2bdec799-905f-48bc-aed5-2d92134739e8
caps.latest.revision: "6"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 1314c0bc8de25c343b80f40de7d2a007024a17dd
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/12/2017
---
# <a name="unicode-and-ascii-support-in-system-center-configuration-manager"></a>Compatibilidad con Unicode y ASCII en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

System Center Configuration Manager crea la mayoría de los objetos mediante caracteres Unicode. Sin embargo, varios objetos admiten solo caracteres ASCII o tienen otras limitaciones.  

 En las secciones siguientes se incluyen los objetos que deben utilizar solo caracteres del conjunto de caracteres ASCII, o que tienen otras limitaciones adicionales.  

-   [Objetos que usan caracteres ASCII](#BKMK_ASCIIchar)  

-   [Limitaciones adicionales](#BKMK_OtherCharLimitations)  

-   [Objetos de Configuration Manager que no están localizados](#BKMK_LangNonLocalize)  

##  <a name="BKMK_ASCIIchar"></a> Objetos que usan caracteres ASCII  
 Configuration Manager solo admite el conjunto de caracteres ASCII cuando se crean los siguientes objetos:  

-   Código de sitio  

-   Todos los nombres de equipo de servidor de sistema de sitio  

-   Las cuentas de Configuration Manager siguientes:  

    > [!NOTE]  
    >  Estas cuentas admiten caracteres ASCII y caracteres RUS en un sitio que se ejecuta en ruso.  

    -   Cuenta de instalación de inserción de cliente  

    -   Cuenta de publicación de referencia de estado de mantenimiento  

    -   Cuenta de consulta de referencia de estado de mantenimiento  

    -   Cuenta de conexión a la base de datos del punto de administración  

    -   Cuenta de acceso a la red  

    -   Cuenta de acceso de paquetes  

    -   Cuenta de remitente estándar  

    -   Cuenta de instalación del sistema de sitio  

    -   Cuenta de conexión de punto de actualización de software  

    -   Cuenta del servidor proxy del punto de actualización de software  

    > [!NOTE]  
    >  Las cuentas que especifica para la administración basada en roles admiten Unicode.  
    >   
    >  La cuenta de punto de Reporting Services admite Unicode, con la excepción de caracteres RUS.  

-   Nombre de dominio completo (FQDN) para servidores y sistemas de sitio  

-   Ruta de instalación de Configuration Manager  

-   Nombres de instancia de SQL Server  

-   La ruta de acceso para los siguientes roles de sistema de sitio:  

    -   Punto de servicio web del catálogo de aplicaciones  

    -   Punto de sitios web del catálogo de aplicaciones  

    -   Punto de inscripción  

    -   Punto de proxy de inscripción  

    -   Puede configurar otras fuentes de actualización opcionales si crea una directiva antimalware.  

    -   Punto de migración de estado  

-   La ruta de acceso de las carpetas siguientes:  

    -   La carpeta en la que se almacenan datos de migración de estado de cliente  

    -   La carpeta que contiene los informes de Configuration Manager  

    -   La carpeta en la que se almacena la copia de seguridad de Configuration Manager  

    -   La carpeta en la que se almacenan los archivos de origen de instalación para la configuración del sitio  

    -   La carpeta en la que se almacenan las descargas previas que el programa de instalación necesita  

-   La ruta de acceso de los objetos siguientes:  

    -   Sitio web de IIS  

    -   Ruta de instalación de aplicación virtual  

    -   Nombre de aplicación virtual  

-   Los siguientes objetos para la administración fuera de banda y de AMT:  

    -   El FQDN del equipo basado en AMT  

    -   El nombre de equipo del equipo basado en AMT  

    -   El nombre NetBIOS de dominio  

    -   El nombre del perfil inalámbrico y el SSID  

    -   El nombre de la entidad de certificación raíz de confianza  

    -   El nombre de la entidad de certificación (CA) y los nombres de las plantillas  

    -   El nombre de archivo y la ruta de acceso del archivo de imagen de redirección de IDE  

    -   El contenido del almacenamiento de datos de AMT  

-   Los nombres de los archivos ISO de los medios de arranque  

##  <a name="BKMK_OtherCharLimitations"></a> Limitaciones adicionales  
 Limitaciones adicionales de versiones de idioma y conjuntos de caracteres admitidos:  

-   Configuration Manager no admite el cambio de la configuración regional del equipo del servidor de sitio.  

-   La entidad de certificación (CA) empresarial no admite nombres de equipos cliente en los que se usan conjuntos de caracteres de doble byte (DBCS). Los nombres de equipos cliente que se pueden utilizar están restringidos por la limitación de PKI del conjunto de caracteres IA5. Además, Configuration Manager no admite nombres de entidad de certificación o valores de nombre de asunto que usen DBCS.  

##  <a name="BKMK_LangNonLocalize"></a> Objetos de Configuration Manager que no están localizados  
 La base de datos de Configuration Manager admite Unicode para la mayoría de objetos que almacena y, si es posible, muestra esta información en el idioma del sistema operativo que coincide con la configuración regional del equipo. Para que la interfaz de cliente o la consola de Configuration Manager muestren la información en el idioma del sistema operativo del equipo, la configuración regional del mismo debe coincidir con el idioma de un servidor o un cliente instalado en el sitio.  

 En cambio, varios objetos de Configuration Manager no admiten Unicode y se almacenan en la base de datos mediante ASCII, o tienen limitaciones de idioma adicionales. Esta información siempre se muestra mediante el conjunto de caracteres ASCII o en el idioma que se usó cuando se creó el objeto.  
