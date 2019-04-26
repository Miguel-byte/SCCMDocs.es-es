---
title: Creación de aplicaciones de Android
titleSuffix: Configuration Manager
description: Crear e implementar aplicaciones para dispositivos Android en Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: e025c48c-1514-4ab7-836c-e0635aaa993a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: ef070186112642d204aade24039da87c0e3a22f0
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62277045"
---
# <a name="create-android-applications-in-configuration-manager"></a>Crear aplicaciones de Android en Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Una aplicación de Configuration Manager tiene uno o varios tipos de implementación. Los tipos de implementación comprenden los archivos de instalación y la información necesaria para implementar software en un dispositivo. Además tiene reglas que especifican cuándo y cómo se implementa el software.  

Consulte [crear una aplicación](/sccm/apps/deploy-use/create-applications#bkmk_create) para conocer los pasos para crear aplicaciones de Configuration Manager y los tipos de implementación. 

Tenga en cuenta las siguientes consideraciones cuando cree e implemente aplicaciones para dispositivos Android:  



## <a name="general-considerations-for-android-apps"></a>Consideraciones generales para aplicaciones Android

Configuration Manager admite la implementación de paquetes .apk de Android. 

Admite las siguientes acciones de implementación:

|Tipo de dispositivo|Acciones admitidas|
|-|-|
|Android|**Disponible**, **necesario**: El usuario debe dar su consentimiento para la instalación y desinstalación.|
|Android for Work |**Disponible**, **Necesario** |



## <a name="approve-and-deploy-android-for-work-apps"></a>Aprobar e implementar aplicaciones Android for Work

Como administrador de Configuration Manager, también puede aprobar aplicaciones en el [sitio web de Play for Work](https://play.google.com/work). Después, implemente las aplicaciones en dispositivos Android for Work administrados.

Siga estos pasos para aprobar aplicaciones en la tienda Play for Work, sincronizarlas con la consola de Configuration Manager e implementarlas en dispositivos Android for Work administrados. Para implementar aplicaciones en los perfiles de trabajo de usuarios, debe aprobar las aplicaciones en Play for Work. Después, sincronice las aplicaciones con la consola de Configuration Manager.

1. Abra un explorador y vaya a: https://play.google.com/work.  

2. Inicie sesión con la cuenta de administrador de Google enlazada a su inquilino de Microsoft Intune.  

3. Busque las aplicaciones que le gustaría implementar en su entorno. Elija **Aprobar** para cada una de ellas para que la aplicación esté disponible para Android for Work.  

4. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Cloud Services** y haga clic en el nodo **Android for Work**.  

5. Haga clic en **Sincronización** en la cinta.  

6. Espere hasta 10 minutos para que las aplicaciones se sincronicen. Después vaya al área de trabajo **Biblioteca de software**, expanda **Administración de aplicaciones** y seleccione el nodo **Información de licencia para las aplicaciones de la Tienda**.  

7. Seleccione una aplicación sincronizada desde Play for Work y después haga clic en **Crear aplicación**.  

8. Complete el asistente.  

9. Vaya al área de trabajo **Biblioteca de software**, expanda **Administración de aplicaciones** y seleccione el nodo **Aplicaciones**. Seleccione una aplicación Android for Work e impleméntela como de costumbre.  

Para sincronizar aplicaciones Play for Work con Configuration Manager, apruebe primero al menos una aplicación en el sitio web de Play for Work.

Las aplicaciones implementadas como **Disponibles** se muestran en la aplicación Google Play con el distintivo de trabajo en lugar del Portal de empresa. Esto le permite implementar aplicaciones desde un origen de confianza. La aplicación de Google Play con el distintivo de trabajo es un origen de confianza. No debe permitir aplicaciones de orígenes de que no son de confianza.
