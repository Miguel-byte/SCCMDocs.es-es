---
title: Creación de aplicaciones Windows
titleSuffix: Configuration Manager
description: Consulte las consideraciones que debe tener en cuenta al crear e implementar aplicaciones para dispositivos Windows.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9181c84e-d74f-44ea-9bb9-f7805eb465fc
caps.latest.revision: 8
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.openlocfilehash: 76e421571fa96d5e9ee808ac5d61361f52c6cbe3
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2018
---
# <a name="create-windows-applications-with-system-center-configuration-manager"></a>Crear aplicaciones de Windows con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Además de los otros requisitos y procedimientos de System Center Configuration Manager para crear una aplicación, también debe tener en cuenta las consideraciones siguientes al crear e implementar aplicaciones para dispositivos Windows.  

## <a name="general-considerations"></a>Consideraciones generales  
 Configuration Manager admite la implementación de los siguientes tipos de archivo de aplicaciones:  

|Tipo de dispositivo|Tipos de archivo compatibles|  
|-----------------|---------------------|  
|Windows RT y Windows RT 8.1|\*.appx, \*.appxbundle|  
|Windows 8.1 y posterior inscrito como dispositivo móvil|\*.appx, \*.appxbundle|  

 Se admiten las siguientes acciones de implementación:  

|Tipo de dispositivo|Acciones admitidas|  
|-----------------|-----------------------|  
|Windows 8.1 y posterior|disponible, necesario, desinstalar|  
|Windows RT|disponible, necesario, desinstalar|  

## <a name="support-for-universal-windows-platform-uwp-apps"></a>Compatibilidad de las aplicaciones de la Plataforma universal de Windows (UWP)  
 Los dispositivos de Windows 10 no necesitan una clave de instalación de prueba para instalar las aplicaciones de línea de negocio. Sin embargo, para habilitar la instalación de prueba, la clave del Registro **HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Windows\Appx\AllowAllTrustedApps** debe tener un valor de 1.  

 Si esta clave del Registro no está configurada, Configuration Manager establecerá automáticamente este valor en **1** la primera vez que implemente una aplicación en el dispositivo. Si estableció este valor en **0**, Configuration Manager no podrá cambiar automáticamente el valor y se producirá un error en la implementación de las aplicaciones de línea de negocio.  

 Debe firmar las aplicaciones de línea de negocio de la Plataforma universal de Windows con un certificado de firma de código de confianza en cada dispositivo en el que implemente la aplicación. Puede usar certificados de una infraestructura PKI interna o un certificado procedente de un certificado raíz público de terceros instalado en el dispositivo.  

 En los dispositivos de Windows 10 Mobile, puede usar un certificado de firma de código que no sea Symantec para firmar aplicaciones universales con extensión **.appx** . En cuanto a aplicaciones **.xap** y paquetes **.appx** compilados para Windows Phone 8.1 que desee instalar en dispositivos de Windows 10 Mobile, debe usar un certificado de firma de código de Symantec.  

## <a name="deploy-windows-installer-apps-to-enrolled-windows-10-pcs"></a>Implementar aplicaciones de Windows Installer en equipos de Windows 10 inscritos  
 El tipo de instalador **Windows Installer a través de MDM (\*.msi)** le permite crear e implementar aplicaciones basadas en Windows Installer para equipos inscritos que ejecutan Windows 10.  

 Las consideraciones siguientes se aplican cuando se utiliza este tipo de instalador:  

-   Solo puede cargar un único archivo con la extensión .msi.  

-   El código de producto y la versión del producto del archivo se usan para la detección de la aplicación.  

-   Se utilizará el comportamiento de reinicio predeterminado de la aplicación. Configuration Manager no lo controla.  

-   Se instalarán paquetes MSI por usuario para un solo usuario.  

-   Se instalarán paquetes MSI por máquina para todos los usuarios del dispositivo.  

-   Se admiten actualizaciones de aplicaciones si el código de producto MSI de cada versión es el mismo.  
