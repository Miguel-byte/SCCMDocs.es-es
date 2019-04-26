---
title: Configuración de la suscripción a Intune
titleSuffix: Configuration Manager
description: Configurar una suscripción de Intune para realizar un seguimiento de las licencias de administración de dispositivos móviles local en Configuration Manager
ms.date: 03/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 1e42b1c1-3d58-481f-8647-5c7ae640c5f5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: aff4fcc67325645387aea1e57354321769a515ca
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62217022"
---
# <a name="set-up-a-microsoft-intune-subscription-for-on-premises-mdm-in-configuration-manager"></a>Configurar una suscripción de Microsoft Intune para MDM local en Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Administrador de configuración local administración de dispositivos móviles (MDM) requiere una suscripción a Microsoft Intune para realizar el seguimiento de licencias. No se usa el servicio de Intune para administrar los dispositivos ni para almacenar información de administración. Por MDM local, toda la administración de dispositivos se controla mediante la infraestructura de Configuration Manager.  

Antes de instalar los roles de sistema de sitio requeridos para MDM local, configure la suscripción a Intune. Esta acción minimiza el tiempo necesario para que los roles de sistema de sitio recién instalados puedan funcionar.  

> [!Note]  
> A partir de la versión 1810, una conexión a Intune ya no es necesaria para nuevas implementaciones de MDM local.<!--3607730, fka 1359124--> La organización sigue necesitando licencias de Intune para usar esta característica. Actualmente no se puede quitar la conexión de Intune de las implementaciones locales de MDM existentes. Para más información, vea la [entrada del blog de soporte técnico de Intune](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Move-from-Hybrid-Mobile-Device-Management-to-Intune-on-Azure/ba-p/280150).  



##  <a name="sign-up-for-microsoft-intune"></a>Suscribirse a Microsoft Intune  

Intune es necesario para que funcione en MDM local. [Registrarse](https://docs.microsoft.com/intune/free-trial-sign-up) para una suscripción de prueba o de pagada. A continuación, vaya al paso siguiente para agregar la suscripción a Configuration Manager.  



##  <a name="add-the-intune-subscription-to-configuration-manager"></a>Agregar la suscripción de Intune a Configuration Manager  

Para agregar la suscripción a Configuration Manager, siga los mismos pasos básicos que daría al agregar la suscripción para MDM híbrida con Intune. Lea las notas siguientes para conocer las diferencias específicas y después siga las instrucciones en [Configurar la suscripción a Intune](/sccm/mdm/deploy-use/configure-intune-subscription).  

> [!NOTE]
>  Al agregar la suscripción de Intune, tenga las siguientes notas en mente:  
> 
> - La colección especificada en el Asistente para agregar suscripciones de Microsoft Intune no se usa para la delegación de derechos de usuario MDM local. Sólo se utiliza para la administración de dispositivos móviles con Intune. Sin embargo, es necesario especificar una colección para que el Asistente continuar.  
> 
> - Se omite el código de sitio que especifique en el Asistente para MDM local. Usa el código de sitio que especifique en la inscripción de perfil que se concede a los usuarios permisos para inscribir dispositivos.  
> 
> - No habilite la autenticación multifactor. No se admite en MDM local.  



##  <a name="configure-the-intune-subscription-for-on-premises-mdm"></a>Configurar la suscripción de Intune para MDM local  

1. En la consola de Configuration Manager, vaya a la **administración** área de trabajo, expanda **servicios en la nube**y seleccione el **suscripciones a Microsoft Intune** nodo. Seleccione la suscripción y, a continuación, elija **propiedades** en la cinta de opciones.   

    1. En la sección de administración de dispositivos en entornos móviles en la parte inferior de la **General** página, elija una de las siguientes opciones:

        - Si tiene previsto tener solo dispositivos administrados de forma local, seleccione la opción de **solo administrar dispositivos locales**.  

            > [!NOTE]  
            > Cuando se habilita esta opción, configure la suscripción a Intune para mantener todos los administración información en su entorno local. No hay datos de administración de dispositivos se replican en la nube.  

        - Si planea tener dispositivos administrados por Intune y Configuration Manager en el entorno local, no configure esta opción.  

    Seleccione **Aceptar** para cerrar las propiedades de suscripción.

2. Si planea administrar dispositivos Windows 10 Mobile, seleccione su suscripción en la lista, seleccione **configurar plataformas** en la cinta de opciones y, a continuación, seleccione **Windows Phone**.  

    1. Seleccione la opción de **Windows Phone 8.1 y Windows 10 Mobile**y, a continuación, seleccione **Aceptar**.  

3. Si planea administrar equipos de escritorio de Windows 10, seleccione su suscripción en la lista, seleccione **configurar plataformas** en la cinta de opciones y, a continuación, seleccione **Windows**.  

    1. Seleccione la opción de **inscripción habilitar Windows**y, a continuación, seleccione **Aceptar**.  

