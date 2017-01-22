---
title: Paquetes de idioma | Microsoft Docs
description: "Obtenga información sobre los idiomas admitidos que puede usar en System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cd74e5f5-33f6-4566-8c9d-d6a93bfe71ed
caps.latest.revision: 10
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: 35d1008752a3275febef46b8817e97afdb91d580


---
# <a name="language-packs-in-system-center-configuration-manager"></a>Paquetes de idioma en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Este tema proporciona detalles técnicos sobre la compatibilidad de idiomas en System Center Configuration Manager.  

##  <a name="a-namebkmksuplanguagepacksa-supported-operating-system-languages"></a><a name="BKMK_SupLanguagePacks"></a> Idiomas admitidos del sistema operativo  
 Puede instalar compatibilidad para los siguientes idiomas de pantalla mediante la instalación de **paquetes de idioma de servidor** o **paquetes de idioma de cliente** en un sitio de administración central y en sitios primarios. Los archivos de paquete de idioma se descargan al ejecutar el programa de instalación como parte de la descarga de los archivos de requisitos previos y redistribuible. También puede usar el [Descargador del programa de instalación](setup-downloader.md) para descargar estos archivos antes de ejecutar el programa de instalación. Durante la instalación de un sitio, deben seleccionarse los idiomas de cliente y servidor que se admitirán en el sitio de los archivos de paquete de idioma disponibles.  

 Utilice la tabla siguiente para asignar un identificador de configuración regional al idioma que desee admitir en servidores o clientes. Para obtener más información sobre identificadores de configuración regional, consulte [Locale IDs Assigned by Microsoft (identificadores de configuración regional asignados por Microsoft)](http://go.microsoft.com/fwlink/p/?LinkId=252609) en la biblioteca en línea de MSDN.  

### <a name="server-languages"></a>Idiomas del servidor  

|Idioma del servidor|Identificador de configuración regional (LCID)|Código de tres letras|  
|---------------------|------------------------|-----------------------|  
|Inglés (predeterminado)|0409|ENU|  
|Chino (tradicional, Hong Kong RAE)|0c04|ZHH|  
|Chino (simplificado)|0804|CHS|  
|Chino (tradicional, Taiwán)|0404|CHT|  
|Checo|0405|CSY|  
|Neerlandés - Países Bajos|0413|NLD|  
|Francés|040c|FRA|  
|Alemán|0407|DEU|  
|Húngaro|040e|HUN|  
|Italiano - Italia|0410|ITA|  
|Japonés|0411|JPN|  
|Coreano|0412|KOR|  
|Polaco|0415|PLK|  
|Portugués - Brasil|0416|PTB|  
|Portugués - Portugal|0816|PTG|  
|Ruso|0419|RUS|  
|Español - España|0c0a|ESN|  
|Sueco|041d|SVE|  
|Turco|041f|TRK|  

### <a name="client-languages"></a>Idiomas del cliente  

|Idioma del cliente|Identificador de configuración regional (LCID)|Código de tres letras|  
|---------------------|------------------------|-----------------------|  
|Inglés (predeterminado)|0409|ENG|  
|Chino (tradicional, Hong Kong RAE)|0c04|ZHH|  
|Chino - Simplificado|0804|CHS|  
|Chino (tradicional, Taiwán)|0404|CHT|  
|Checo|0405|CSY|  
|Danés|0406|DAN|  
|Neerlandés - Países Bajos|0413|NLD|  
|Finés|040b|FIN|  
|Francés|040c|FRA|  
|Alemán|0407|DEU|  
|Griego|0408|ELL|  
|Húngaro|040e|HUN|  
|Italiano - Italia|0410|ITA|  
|Japonés|0411|JPN|  
|Coreano|0412|KOR|  
|Noruego|0414|NOR|  
|Polaco|0415|PLK|  
|Portugués (Brasil)|0416|PTB|  
|Portugués (Portugal)|0816|PTG|  
|Ruso|0419|RUS|  
|Español - España|0c0a|ESN|  
|Sueco|041d|SVE|  
|Turco|041f|TRK|  

### <a name="mobile-device-client-languages"></a>Idiomas de cliente de dispositivo móvil  
 Cuando se agrega compatibilidad con idiomas de dispositivo móvil, se incluyen todos los idiomas de cliente de dispositivo móvil. No puede seleccionar paquetes de idioma individuales para la compatibilidad con dispositivos móviles.  

### <a name="how-to-identify-installed-language-packs"></a>Identificación de los paquetes de idioma instalados  
Puede identificar los paquetes de idioma instalados en un equipo que ejecuta el cliente de Configuration Manager mediante el identificador de configuración regional (LCID) de los paquetes de idioma instalados en el Registro del equipo. Esta información está disponible en la siguiente ubicación:  

-   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCMSetup\InstalledLangs**  

Puede utilizar el inventario de hardware para recopilar esta información y, a continuación, generar un informe personalizado para ver la información de idioma. Para obtener más información sobre la recopilación de inventario de hardware personalizado, consulte [How to configure hardware inventory in System Center Configuration Manager](../../../../core/clients/manage/inventory/configure-hardware-inventory.md) (Configuración de inventario de hardware en System Center Configuration Manager). Para obtener más información sobre la creación de informes, consulte la sección [Administración de informes de Configuration Manager](../../../../core/servers/manage/operations-and-maintenance-for-reporting.md#BKMK_ManageReports) en el tema [Operaciones y mantenimiento de informes en Configuration Manager](../../../../core/servers/manage/operations-and-maintenance-for-reporting.md).  



<!--HONumber=Dec16_HO3-->


