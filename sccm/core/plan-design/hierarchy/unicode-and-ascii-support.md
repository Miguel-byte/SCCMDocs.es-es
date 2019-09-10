---
title: Compatibilidad con Unicode y ASCII
titleSuffix: Configuration Manager
description: Conozca la compatibilidad con caracteres Unicode y ASCII en los objetos de Configuration Manager.
ms.date: 08/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 2bdec799-905f-48bc-aed5-2d92134739e8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0214abdf1dd7ce735542ebace443c8aed297b2c3
ms.sourcegitcommit: f679fc1e46c191a1780ae961d155c927fc353dce
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/30/2019
ms.locfileid: "70176726"
---
# <a name="unicode-and-ascii-support-in-configuration-manager"></a>Compatibilidad con Unicode y ASCII en Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Configuration Manager crea la mayoría de los objetos mediante caracteres Unicode. Sin embargo, varios de ellos admiten solo caracteres ASCII o tienen otras limitaciones.  

## <a name="BKMK_ASCIIchar"></a> Objetos que usan caracteres ASCII

Al crear los siguientes objetos, Configuration Manager solo admite el conjunto de caracteres ASCII:  

- Código de sitio  

- Todos los nombres de equipo de servidor de sistema de sitio  

- Las cuentas de Configuration Manager siguientes:  

    > [!NOTE]  
    > Estas cuentas admiten caracteres ASCII y caracteres RUS en un sitio que se ejecuta en ruso.  

    - Cuenta de instalación de inserción de cliente  

    - Cuenta de conexión a la base de datos del punto de administración  

    - Cuenta de acceso a la red  

    - Cuenta de acceso de paquetes  

    - Cuenta de remitente estándar  

    - Cuenta de instalación del sistema de sitio  

    - Cuenta de conexión de punto de actualización de software  

    - Cuenta del servidor proxy del punto de actualización de software  

    > [!NOTE]  
    > Las cuentas que especifica para la administración basada en roles admiten Unicode.  
    >
    > La cuenta de punto de servicios de informes admite Unicode, con la excepción de caracteres RUS.  

- Nombre de dominio completo (FQDN) para servidores y sistemas de sitio  

- Ruta de instalación de Configuration Manager  

- Nombres de instancia de SQL Server  

- La ruta de acceso para los siguientes roles de sistema de sitio:  

    - Punto de inscripción  

    - Punto de proxy de inscripción  

    - Punto de servicios de informes  

    - Punto de migración de estado  

- La ruta de acceso de las carpetas siguientes:  

    - La carpeta en la que se almacenan datos de migración de estado de cliente  

    - La carpeta que contiene los informes de Configuration Manager  

    - La carpeta en la que se almacena la copia de seguridad de Configuration Manager  

    - La carpeta en la que se almacenan los archivos de origen de instalación para la configuración del sitio  

    - La carpeta en la que se almacenan las descargas previas que el programa de instalación necesita  

- La ruta de acceso de los objetos siguientes:  

    - Sitio web de IIS  

    - Ruta de instalación de aplicación virtual  

    - Nombre de aplicación virtual  

- Los nombres de los archivos ISO de los medios de arranque  


## <a name="BKMK_OtherCharLimitations"></a> Limitaciones adicionales

Limitaciones adicionales de versiones de idioma y conjuntos de caracteres admitidos:  

- Configuration Manager no admite el cambio de la configuración regional del equipo del servidor de sitio.  

- La entidad de certificación (CA) empresarial no admite nombres de equipo cliente en los que se usen conjuntos de caracteres de doble byte (DBCS). Los nombres de equipos cliente que se pueden utilizar están restringidos por la limitación de PKI del conjunto de caracteres IA5. Configuration Manager no admite nombres de entidad de certificación o valores de nombre de asunto que usen DBCS.  


## <a name="BKMK_LangNonLocalize"></a> Objetos que no están localizados

La base de datos de Configuration Manager admite Unicode en la mayoría de los objetos que almacena. Cuando es posible, muestra esta información en el idioma del sistema operativo que coincide con la configuración regional de un equipo. Para que la interfaz de cliente o la consola de Configuration Manager muestren la información en el idioma del sistema operativo del equipo, la configuración regional del mismo debe coincidir con el idioma de un servidor o un cliente instalado en el sitio.  

Varios objetos de Configuration Manager no admiten Unicode. Se almacenan en la base de datos mediante ASCII o tienen limitaciones de idioma adicionales. Esta información siempre se muestra con el conjunto de caracteres ASCII o en el idioma que se usó cuando se creó el objeto.  
