---
title: Creación de aplicaciones de iOS
titleSuffix: Configuration Manager
description: Crear e implementar aplicaciones para dispositivos iOS en Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: ff633013-5313-4cd3-949c-56d45e777280
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: e4a2d84fe31c3a524b876e3beb34f0e3d25d0089
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56125449"
---
# <a name="create-ios-applications-in-configuration-manager"></a>Crear aplicaciones iOS en Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Una aplicación de Configuration Manager tiene uno o varios tipos de implementación que incluyen la información y los archivos de instalación necesarios para implementar software en un dispositivo. Además tiene reglas que especifican cuándo y cómo se implementa el software.  

Consulte [crear una aplicación](/sccm/apps/deploy-use/create-applications#bkmk_create) para conocer los pasos para crear aplicaciones de Configuration Manager y los tipos de implementación. 

Tenga en cuenta las siguientes consideraciones cuando cree e implemente aplicaciones para dispositivos iOS:  

- Configuration Manager admite la implementación de paquetes .ipa de iOS. No es necesario especificar un archivo de lista de propiedades (.plist) al importar una aplicación de iOS. 

- Implemente las aplicaciones de iOS como **Disponible** o **Requerida**. El usuario debe dar su consentimiento para la instalación y desinstalación.

> [!IMPORTANT]  
>  Actualmente, los usuarios finales no pueden instalar aplicaciones corporativas desde la aplicación Portal de empresa de Microsoft Intune para iOS. Esta limitación se debe a las restricciones en las aplicaciones publicadas en la App Store de iOS. (Consulte las directrices de revisión de la App Store, sección 2). Los usuarios pueden instalar aplicaciones corporativas explorando el portal de Intune en su dispositivo. Estas aplicaciones incluyen aplicaciones administradas de la App Store y paquetes de aplicaciones de línea de negocio. Para obtener más información sobre las funciones de administración de dispositivos móviles que se habilitan con la aplicación Portal de empresa de Microsoft Intune, vea [Funciones de administración de dispositivos inscritos en Microsoft Intune](https://docs.microsoft.com/intune/device-enrollment).  
