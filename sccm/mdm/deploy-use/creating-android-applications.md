---
title: Crear aplicaciones de Android | Microsoft Docs
description: Consulte las consideraciones que debe tener en cuenta al crear e implementar aplicaciones para dispositivos Android.
ms.custom: na
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e025c48c-1514-4ab7-836c-e0635aaa993a
caps.latest.revision: "6"
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.openlocfilehash: 8fcd8d8172978fdeb1a11b7fa7e79d294591f796
ms.sourcegitcommit: f6a428a8db7145affa388f59e0ad880bdfcf17b5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/14/2017
---
# <a name="create-android-applications-with-system-center-configuration-manager"></a>Crear aplicaciones Android con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Una aplicación de System Center Configuration Manager tiene uno o varios tipos de implementación. Los tipos de implementación comprenden los archivos de instalación y la información necesaria para implementar software en un dispositivo. Además tiene reglas que especifican cuándo y cómo se implementa el software.  

 Puede crear aplicaciones mediante los métodos siguientes:  

-   Crear automáticamente los tipos de aplicación y de implementación mediante la lectura de los archivos de instalación de la aplicación.  
-   Crear manualmente la aplicación y, a continuación, agregar los tipos de implementación más adelante.  
-   Importe una aplicación desde un archivo.  

Consulte [Inicie el Asistente para crear aplicaciones](../../apps/deploy-use/create-applications.md#start-the-create-application-wizard) para conocer los pasos necesarios para crear aplicaciones de Configuration Manager y los tipos de implementación. Además, tenga en cuenta las consideraciones siguientes cuando cree e implemente aplicaciones para dispositivos Android.  

## <a name="general-considerations-for-android-apps"></a>Consideraciones generales para aplicaciones Android

Configuration Manager admite la implementación de los siguientes tipos de aplicaciones para Android:

|Tipo de dispositivo|Archivos compatibles|
|-|-|
|Android|.apk|

Se admiten las siguientes acciones de implementación:

|Tipo de dispositivo|Acciones admitidas|
|-|-|
|Android|**Disponible**, **Requerido** El usuario debe dar su consentimiento para la instalación y desinstalación.|
|Android for Work | **Requerido** |

## <a name="approve-and-deploy-android-for-work-apps"></a>Aprobar e implementar aplicaciones Android for Work
Como administrador de Configuration Manager, también puede aprobar e implementar aplicaciones en el [sitio web de Play for Work](https://play.google.com/work) e implementar las aplicaciones en dispositivos Android for Work administrados.

Siga estos pasos para aprobar aplicaciones en la tienda Play for Work, sincronizarlas con la consola de Configuration Manager e implementarlas en dispositivos Android for Work administrados. Para implementar aplicaciones en los perfiles de trabajo de los usuarios, debe aprobar las aplicaciones en Play for Work y después sincronizarlas con la consola de Configuration Manager.

1. Abra un explorador y vaya a https://play.google.com/work.
2. Inicie sesión con la cuenta de administrador de Google enlazada a su inquilino de Intune.
3. Busque las aplicaciones que le gustaría implementar en su entorno y seleccione **Aprobar** en cada una de ellas para que la aplicación esté disponible para Android for Work.
4. En la consola de Configuration Manager, vaya a **Administrador** > **General** > **Cloud Services** > **Android for Work** y seleccione **Sincronizar**.
5. Espere hasta 10 minutos para que las aplicaciones se sincronicen y, después, vaya a **Biblioteca de software** > **General** > **Administración de aplicaciones** > **Información de licencia para las aplicaciones de la Tienda**.
6. Seleccione una aplicación sincronizada desde Play for Work y elija **Crear aplicación**.
7. Finalice el asistente y seleccione **Cerrar**.
8. Vaya a **Biblioteca de software** > **General** > **Administración de aplicaciones** > **Aplicaciones**, seleccione una aplicación de Android for Work e impleméntela como de costumbre.

Para sincronizar aplicaciones Play for Work con Configuration Manager, debe aprobar primero al menos una aplicación en el sitio web de Play for Work.
