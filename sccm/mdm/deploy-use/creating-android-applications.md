---
title: Crear aplicaciones de Android | Microsoft Docs
description: Consulte las consideraciones que debe tener en cuenta al crear e implementar aplicaciones para dispositivos Android.
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e025c48c-1514-4ab7-836c-e0635aaa993a
caps.latest.revision: 6
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: 3d90b2cb1e255b9e8827a991779024ccecde9646
ms.lasthandoff: 03/06/2017

---
# <a name="create-android-applications-with-system-center-configuration-manager"></a>Crear aplicaciones Android con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Una aplicación de System Center Configuration Manager tiene uno o varios tipos de implementación que incluyen la información y los archivos de instalación necesarios para implementar un dispositivo. Además tiene reglas que especifican cuándo y cómo se implementa el software.  

 Puede crear aplicaciones mediante los métodos siguientes:  

-   Crear automáticamente los tipos de aplicación y de implementación mediante la lectura de los archivos de instalación de la aplicación.  

-   Crear manualmente la aplicación y, a continuación, agregar los tipos de implementación más adelante.  

-   Importe una aplicación desde un archivo.  

Consulte [Inicie el Asistente para crear aplicaciones](../../apps/deploy-use/create-applications.md#start-the-create-application-wizard) para conocer los pasos necesarios para crear aplicaciones de Configuration Manager y los tipos de implementación. Asimismo, tenga en cuenta las siguientes consideraciones cuando cree e implemente aplicaciones para dispositivos Android.  

## <a name="general-considerations"></a>Consideraciones generales

Configuration Manager admite la implementación de los siguientes tipos de aplicaciones para Android:

|Tipo de dispositivo|Archivos compatibles|
|-|-|
|Android|.apk|

Se admiten las siguientes acciones de implementación:

|Tipo de dispositivo|Acciones admitidas|
|-|-|
|Android|**Disponible**, **Necesario**. El usuario debe dar su consentimiento para la instalación y desinstalación.

