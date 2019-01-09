---
title: 'Actualización de clientes de macOS '
titleSuffix: Configuration Manager
description: Actualice clientes en equipos Mac en System Center Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 74c60941-5eae-4905-9e58-252bdb39df96
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 37471367e95c6f0edc1d33b951776673037d845c
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2018
ms.locfileid: "53416399"
---
# <a name="how-to-upgrade-clients-on-mac-computers-in-system-center-configuration-manager"></a>Cómo actualizar clientes en equipos Mac en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Siga los pasos generales que se describen a continuación para actualizar el cliente de equipos Mac mediante una aplicación de System Center Configuration Manager. Alternativamente, también puede descargar el archivo de instalación del cliente Mac, copiarlo a una ubicación de red compartida o en una carpeta local en el equipo Mac y, a continuación, solicitar a los usuarios la ejecución manual de la instalación.  

> [!NOTE]  
>  Antes de realizar estos pasos, asegúrese de que el equipo Mac cumple los requisitos previos. Consulte [Sistemas operativos compatibles con equipos Mac](../../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#mac-computers).  

## <a name="step-1-download-the-latest-mac-client-installation-file-from-the-microsoft-download-center"></a>Paso 1: Descargar el archivo de instalación de cliente Mac más reciente del Centro de descarga de Microsoft  
 El cliente Mac para Configuration Manager no se suministra en los medios de instalación de Configuration Manager y debe descargarse del Centro de descarga de Microsoft. El archivo de Windows Installer ConfigmgrMacClient.msi contiene los archivos de instalación de cliente Mac.  

 Puede descargar este archivo desde el [Centro de descarga de Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=525184).  

## <a name="step-2-run-the-downloaded-installation-file-to-create-the-mac-client-installation-file"></a>Paso 2: ejecutar el archivo de instalación descargado para crear el archivo de instalación del cliente Mac  
 En un equipo Windows, ejecute el archivo **ConfigmgrMacClient.msi** que descargó para desempaquetar el archivo de instalación de cliente Mac llamado **Macclient.dmg**. De manera predeterminada, este archivo se encuentra en la carpeta **C:\Archivos de programa (x86)\Microsoft\System Center 2012 Configuration Manager Mac Client** en el equipo Windows después de desempaquetar los archivos.  

## <a name="step-3-extract-the-client-installation-files"></a>Paso 3: extraer los archivos de instalación del cliente  
 Copie el archivo Macclient.dmg en un recurso compartido de red o en una carpeta local en un equipo Mac. A continuación, en el equipo Mac, monte y abra el archivo Macclient.dmg. Copie los archivos en una carpeta en el equipo Mac.  

## <a name="step-4-create-a-cmmac-file-that-can-be-used-to-create-an-application"></a>Paso 4: crear un archivo .cmmac que se puede usar para crear una aplicación  

1. Use la herramienta **CMAppUtil** (en la carpeta **Herramientas** de los archivos de instalación de cliente Mac) para crear un archivo .cmmac a partir del paquete de instalación de cliente. Este archivo se usará para crear la aplicación de Configuration Manager.  

2. Copie el nuevo archivo **CMClient.pkg.cmmac** en una ubicación que esté disponible para el equipo que ejecuta la consola de Configuration Manager.  

   Para obtener más información, consulte [Procedimientos adicionales para crear e implementar aplicaciones para equipos Mac](/sccm/apps/get-started/creating-mac-computer-applications#supplemental-procedures-to-create-and-deploy-applications-for-mac-computers).  

## <a name="step-5-create-and-deploy-an-application-containing-the-mac-client-files"></a>**Paso 5:** crear e implementar una aplicación que contiene los archivos de cliente Mac  

1. En la consola de Configuration Manager, cree una aplicación a partir del archivo **CMClient.pkg.cmmac** que contiene los archivos de instalación de cliente.  

2. Implemente esta aplicación en los equipos Mac en su jerarquía.  

   Para obtener más información, consulte [Creación de aplicaciones para equipos Mac con System Center Configuration Manager](../../../../apps/get-started/creating-mac-computer-applications.md).  

## <a name="step-6-users-install-the-latest-client"></a>Paso 6: los usuarios instalan el cliente más reciente  
 Se informará a los usuarios de clientes Mac de que está disponible una actualización del cliente de Configuration Manager y debe instalarse. Cuando los usuarios instalan al cliente, deben reiniciar su equipo Mac.  

 Después de vez reiniciar el equipo, el Asistente para inscripción de equipos se ejecuta automáticamente para solicitar un nuevo certificado de usuario. El Asistente para inscripción de equipos se ejecutará automáticamente solo la primera vez que se instale el cliente de SCCM. Además, no volverá a ejecutarse si se intenta actualizar el cliente con un nuevo instalador más adelante, puesto que ya tiene un certificado de usuario válido. 

 Si no usa la inscripción de Configuration Manager, pero instala el certificado de cliente independientemente de Configuration Manager, consulte [Configurar el cliente actualizado para usar un certificado existente](#BKMK_UpgradingClient_MachineEnrollment).  

##  <a name="BKMK_UpgradingClient_MachineEnrollment"></a> Configurar el cliente actualizado para usar un certificado existente  
 Ejecute el siguiente procedimiento para evitar que se ejecute el Asistente para inscripción de equipos y para configurar el cliente actualizado a fin de que use un certificado de cliente existente.  

- En la consola de Configuration Manager, cree un elemento de configuración del tipo de **Mac OS X**.  

- Agregue un valor de tipo **Script**a este elemento de configuración.  

- Agregue el script siguiente a la configuración:  

  ```  
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

- Agregue el elemento de configuración a una línea base de configuración y después implemente la línea base de configuración en todos los equipos Mac que instalan un certificado independientemente de Configuration Manager.  

  Para obtener más información sobre cómo crear e implementar elementos de configuración para equipos Mac, consulte [Cómo crear elementos de configuración para dispositivos Mac OS X administrados con el cliente de System Center Configuration Manager](../../../../compliance/deploy-use/create-configuration-items-for-mac-os-x-devices-managed-with-the-client.md) y [Cómo implementar líneas base de configuración en System Center Configuration Manager](../../../../compliance/deploy-use/deploy-configuration-baselines.md).  
