---
title: Actualización de clientes de macOS
titleSuffix: Configuration Manager
description: Actualice el cliente de Configuration Manager en equipos Mac.
ms.date: 09/10/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 74c60941-5eae-4905-9e58-252bdb39df96
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: b887a82afce8cf446494e7b9348a0b8c0718e389
ms.sourcegitcommit: cdf2827fb3f44d7522a9b533c115f910aa9c382a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/11/2019
ms.locfileid: "70902568"
---
# <a name="how-to-upgrade-clients-on-mac-computers-in-configuration-manager"></a>Procedimientos para actualizar clientes de Configuration Manager en equipos Mac

*Se aplica a: System Center Configuration Manager (Rama actual)*

Siga los pasos generales que se describen en este artículo para actualizar el cliente de equipos Mac mediante una aplicación de Configuration Manager. También puede descargar el archivo de instalación del cliente de Mac, copiarlo a una ubicación de red compartida o en una carpeta local en el equipo Mac y, después, indicar a los usuarios que ejecuten la instalación de forma manual.  

> [!NOTE]  
> Antes de realizar estos pasos, asegúrese de que el equipo Mac cumple los requisitos previos. Consulte [Sistemas operativos compatibles con equipos Mac](/sccm/plan-design/configs/supported-operating-systems-for-clients-and-devices#mac-computers).  

## <a name="download-the-latest-mac-client"></a>Descarga del cliente de Mac más reciente

El cliente de Mac para Configuration Manager no se suministra en los medios de instalación de Configuration Manager. Descárguelo desde el [Centro de descarga de Microsoft](https://www.microsoft.com/download/details.aspx?id=47719). Los archivos de instalación de cliente de Mac se incluyen en un archivo de Windows Installer denominado **ConfigmgrMacClient.msi**.  

## <a name="create-the-mac-client-installation-file"></a>Creación del archivo de instalación del cliente de Mac

Ejecute **ConfigmgrMacClient.msi** en un equipo que ejecute Windows. Este instalador desempaquetará el archivo de instalación del cliente de Mac, denominado **Macclient.dmg**. De forma predeterminada, puede encontrar este archivo en la carpeta siguiente: **C:\Archivos de programa (x86)\Microsoft\System Center 2012 Configuration Manager Mac Client**.  

## <a name="extract-the-client-installation-files"></a>extraer los archivos de instalación del cliente

Copie **Macclient.dmg** en un equipo Mac. Monte el archivo Macclient.dmg en macOS y, después, copie el contenido en una carpeta del equipo Mac.  

## <a name="create-a-cmmac-file"></a>Creación de un archivo .cmmac

1. Abra la carpeta **Tools** (Herramientas) de los archivos de instalación del cliente de Mac. Use la herramienta **CMAppUtil** para crear un archivo .cmmac a partir del paquete de instalación del cliente. Usará este archivo para crear la aplicación de Configuration Manager.  

2. Copie el nuevo archivo **CMClient.pkg.cmmac** en una ubicación que esté disponible para el equipo en el que se ejecuta la consola de Configuration Manager.  

    Para obtener más información, consulte [Procedimientos adicionales para crear e implementar aplicaciones para equipos Mac](/sccm/apps/get-started/creating-mac-computer-applications#supplemental-procedures-to-create-and-deploy-applications-for-mac-computers).  

## <a name="create-and-deploy-the-app"></a>Creación e implementación de la aplicación

1. En la consola de Configuration Manager, [cree una aplicación](/sccm/apps/get-started/creating-mac-computer-applications) a partir del archivo **CMClient.pkg.cmmac**.  

2. [Implemente esta aplicación](/sccm/apps/deploy-use/deploy-applications) en los equipos Mac de la jerarquía.  

## <a name="install-the-updated-client"></a>Instalación del cliente actualizado

El cliente de Configuration Manager existente en los equipos Mac informará al usuario de que hay una actualización disponible para instalar. Cuando los usuarios instalan al cliente, deben reiniciar su equipo Mac.  

Una vez que se reinicie el equipo, el **Asistente para inscripción de equipos** se ejecuta de forma automática para solicitar un nuevo certificado de usuario.

Si no usa la inscripción de Configuration Manager, pero instala el certificado de cliente independientemente de Configuration Manager, vea [Configuración de clientes para usar un certificado existente](#BKMK_UpgradingClient_MachineEnrollment).  

## <a name="BKMK_UpgradingClient_MachineEnrollment"></a> Configuración de clientes para usar un certificado existente

Use este procedimiento para evitar que se ejecute el Asistente para inscripción de equipos y para configurar el cliente actualizado a fin de que use un certificado de cliente existente.  

1. En la consola de Configuration Manager, [cree un elemento de configuración](/sccm/compliance/deploy-use/create-configuration-items-for-mac-os-x-devices-managed-with-the-client) del tipo **Mac OS X**.  

1. Agregue un valor de tipo **Script**a este elemento de configuración.  

1. Agregue el script siguiente a la configuración:  

  ``` Shell
  #!/bin/sh  
  echo "Starting script\n"  
  echo "Changing directory to MAC Client\n"  
  cd /Users/Administrator/Desktop/'MAC Client'/  
  echo "Import root cert\n"  
  /usr/bin/sudo /usr/bin/security import /Users/Administrator/Desktop/'MAC Client'/Root.pfx -A -k /Library/Keychains/System.Keychain -P ROOT  
  echo "Using openssl to convert pfx to a crt\n"  
  /usr/bin/sudo openssl pkcs12 -in /Users/Administrator/Desktop/'MAC Client'/Root.pfx -out Root1.crt -nokeys -clcerts -passin pass:ROOT  
  echo "Adding trust to root cert\n"  
  /usr/bin/sudo /usr/bin/security add-trusted-cert -d -r trustRoot -k /Library/Keychains/System.Keychain Root1.crt  
  echo "Import client cert\n"  
  /usr/bin/sudo /usr/bin/security import /Users/Administrator/Desktop/'MAC Client'/MacClient.pfx -A -k /Library/Keychains/System.Keychain -P MAC  
  echo "Executing ccmclient with MP\n"  
  sudo ./ccmsetup -MP https://SCCM34387.SCCM34387DOM.NET/omadm/cimhandler.ashx  
  echo "Editing Plist file\n"  
  sudo /usr/libexec/Plistbuddy -c 'Add:SubjectName string CMMAC003L' /Library/'Application Support'/Microsoft/CCM/ccmclient.plist  
  echo "Changing directory to CCM\n"  
  cd /Library/'Application Support'/Microsoft/CCM/  
  echo "Making connection to the server\n"  
  sudo open ./CCMClient  
  echo "Ending Script\n"  
  exit  
  ```  

1. Agregue el elemento de configuración a una [línea base de configuración](/sccm/compliance/deploy-use/create-configuration-baselines). Después, [implemente la línea base de configuración](/sccm/compliance/deploy-use/deploy-configuration-baselines) en todos los equipos Mac que instalan un certificado de forma independiente a Configuration Manager.  
