---
title: Creación de aplicaciones Windows
titleSuffix: Configuration Manager
description: Obtenga más información sobre cómo crear e implementar aplicaciones Windows en Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 9181c84e-d74f-44ea-9bb9-f7805eb465fc
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 38732081ce27fde764f7d47a565ce1211cef1f54
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/31/2018
ms.locfileid: "39383570"
---
# <a name="create-windows-applications-in-configuration-manager"></a>Crear aplicaciones Windows en Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Además de los otros requisitos y procedimientos de Configuration Manager para [crear una aplicación](/sccm/apps/deploy-use/create-applications), tenga en cuenta también las consideraciones siguientes al crear e implementar aplicaciones para dispositivos Windows.  



## <a name="bkmk_general"></a> Consideraciones generales  

Configuration Manager admite la implementación de los formatos de paquete de aplicaciones (.appx) y lote de aplicaciones (.appxbundle) de Windows para dispositivos Windows 8.1 y Windows 10.

A partir de la versión 1806, Configuration Manager también admite los nuevos formatos de paquete de aplicaciones (.msix) y lote de aplicaciones (.msixbundle) de Windows 10. En la actualidad, las compilaciones de [Windows Insider Preview](https://insider.windows.com/) más recientes admiten estos formatos nuevos.<!--1357427-->  

- Para obtener información general de MSIX, consulte [A closer look at MSIX](https://blogs.msdn.microsoft.com/sgern/2018/06/18/a-closer-look-at-msix/) (Análisis exhaustivo de MSIX).  

- Para crear una aplicación MSIX, vea [MSIX support introduced in Insider Build 17682](https://techcommunity.microsoft.com/t5/MSIX-Blog/MSIX-support-introduced-in-Insider-Build-17682/ba-p/202376) (Compatibilidad de MSIX introducida en la compilación 17682 de Insider).  

Al crear una aplicación en la consola de Configuration Manager, seleccione el **Tipo** de archivo de instalación de la aplicación como **Paquete de aplicación de Windows (\*.appx, \*.appxbundle, \*.msix, \*.msixbundle)**. Para obtener más información, consulte [Create applications](/sccm/apps/deploy-use/create-applications) (Creación de aplicaciones). 

> [!Note]  
> Para aprovechar las nuevas características de Configuration Manager, primero actualice los clientes a la versión más reciente. Aunque la funcionalidad nueva aparece en la consola de Configuration Manager cuando se actualiza el sitio y la consola, la totalidad del escenario no es funcional hasta que la versión del cliente también es la más reciente.<!--SCCMDocs issue 646-->  



## <a name="bkmk_provision"></a> Aprovisionar los paquetes de aplicación de Windows para todos los usuarios en un dispositivo
<!--1358310--> A partir de la versión 1806, una aplicación se aprovisiona con un paquete de aplicación de Windows para todos los usuarios en el dispositivo. Un ejemplo común de este escenario es el aprovisionamiento de una aplicación de Microsoft Store para empresas y educación —por ejemplo, Minecraft: Education Edition— en todos los dispositivos usados por los alumnos en una escuela. Anteriormente, Configuration Manager solo admitía la instalación de estas aplicaciones por usuario. Tras iniciar sesión en un dispositivo nuevo, un estudiante tendría que esperar para obtener acceso a una aplicación. Ahora, al aprovisionarse la aplicación en el dispositivo para todos los usuarios, estos pueden empezar a trabajar más rápidamente.

> [!Important]  
> Tenga cuidado con la instalación, el aprovisionamiento y la actualización de versiones diferentes del mismo paquete de aplicación de Windows en un dispositivo, ya que puede producir resultados inesperados. Este comportamiento puede producirse si se usa Configuration Manager para aprovisionar la aplicación y, después, se permite a los usuarios actualizar la aplicación desde Microsoft Store. Para obtener más información, consulte las instrucciones del paso siguiente si [administra aplicaciones de Microsoft Store para Empresas](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business#next-steps).  

Al aprovisionar una aplicación con licencia sin conexión, Configuration Manager no permite que Windows la actualice automáticamente desde Microsoft Store.  

Configuration Manager admite el aprovisionamiento de aplicaciones en las versiones siguientes de Windows:<!--SCCMDocs-pr issue 2762-->
- Acción de instalación: Windows 10, versión 1607 y posteriores
- Acción de desinstalación: Windows 10, versión 1703 y posteriores

Para configurar un tipo de implementación de aplicación de Windows para esta característica, habilite la opción **Provision this application for all users on the device** (Aprovisionar esta aplicación para todos los usuarios en el dispositivo). Para obtener más información, consulte [Create applications](/sccm/apps/deploy-use/create-applications) (Creación de aplicaciones).


> [!Note]  
> Si necesita desinstalar una aplicación aprovisionada de dispositivos en los que los usuarios ya han iniciado sesión, deberá crear dos implementaciones de desinstalación. Dirija la primera instalación de desinstalación a una colección de dispositivos que contenga los dispositivos. Dirija la segunda implementación de desinstalación a una colección que contenga los usuarios que ya han iniciado sesión en los dispositivos que incluyan la aplicación aprovisionada. Cuando se desinstala una aplicación aprovisionada de un dispositivo, Windows no desinstala actualmente la aplicación para los usuarios. 



## <a name="bkmk_uwp"></a> Compatibilidad para aplicaciones para Plataforma universal de Windows (UWP)  

Los dispositivos Windows 10 no necesitan una clave de instalación de prueba para instalar las aplicaciones de línea de negocio. Pero para habilitar la instalación de prueba en Windows, la clave del Registro `HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Windows\Appx\AllowAllTrustedApps` debe tener un valor de **1**.  

Si no se configura esta clave del Registro, Configuration Manager establece este valor automáticamente en **1** la primera vez que se implemente una aplicación en el dispositivo. Si este valor se ha establecido en **0**, Configuration Manager no puede cambiarlo automáticamente y se produce un error en la implementación de las aplicaciones de línea de negocio.  

Firme digitalmente las aplicaciones de línea de negocio para UWP. Use un certificado de firma de código que sea de confianza en todos los dispositivos en los que se implemente la aplicación. Use certificados de la PKI de la organización, o bien compre un certificado de un proveedor de terceros cuyo certificado raíz público ya sea de confianza para Windows.  

Para firmar los paquetes de aplicaciones móviles, use la tabla siguiente para determinar el tipo de certificado de firma de código que se va a usar:

| Paquete  | Symantec  | Distinto de Symantec  |
|---------|---------|---------|
| Paquetes **.appx** universales en dispositivos Windows 10 Mobile | Sí | Sí |
| Paquetes **.xap** | Sí | No | 
| Paquetes **.appx** creados para Windows Phone 8.1 para instalar en dispositivos Windows 10 Mobile | Sí | No | 



## <a name="bkmk_mdm-msi"></a> Implementar aplicaciones de Windows Installer en equipos de Windows 10 inscritos con MDM  

El tipo de implementación **Windows Installer a través de MDM (\*.msi)** permite crear e implementar aplicaciones basadas en Windows Installer en dispositivos inscritos con MDM que ejecutan Windows 10.  

Cuando se usa este tipo de implementación, tenga en cuenta los aspectos siguientes:    

-   Solo se carga un único archivo con la extensión MSI.  

-   Configuration Manager usa el código de producto y la versión del producto del archivo para la detección de la aplicación.  

-   Windows usa el comportamiento de reinicio predeterminado de la aplicación. Configuration Manager no controla el comportamiento de reinicio de la aplicación.  

-   Se instalan paquetes MSI por usuario para un solo usuario.  

-   Se instalan paquetes MSI por equipo para todos los usuarios del dispositivo.  

-   Configuration Manager admite las actualizaciones de aplicaciones. El código de producto MSI de cada versión debe ser el mismo.  
