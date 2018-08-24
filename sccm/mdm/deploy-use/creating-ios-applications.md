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
ms.openlocfilehash: 246ca26b8fab3a1006e8d72b803c298fe48df9df
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/31/2018
ms.locfileid: "39385242"
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
