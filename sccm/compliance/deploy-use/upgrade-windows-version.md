---
title: Actualización de dispositivos Windows a una versión diferente
titleSuffix: Configuration Manager
description: Actualice dispositivos que ejecuten Windows 10 Escritorio o Windows 10 Mobile a otra edición más reciente de forma automática con Configuration Manager.
ms.date: 06/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: b0c9db74-841e-46eb-8924-957cde968bf7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5ef2cd91eed668e66032c184944f448681d18564
ms.sourcegitcommit: f9654cd1a3af6d67de52fedaccceb2e22dafc159
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/09/2019
ms.locfileid: "67677958"
---
# <a name="upgrade-windows-devices-with-the-edition-upgrade-policy-in-system-center-configuration-manager"></a>Actualizar dispositivos de Windows con la directiva de actualización de edición en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*


La **directiva de actualización de ediciones** le permite actualizar automáticamente los dispositivos que ejecutan una de las siguientes versiones de Windows 10 a otra edición:

- Windows 10 Escritorio
- Windows 10 Mobile

Las siguientes rutas de acceso de actualización son compatibles:

- Desde Windows 10 Pro a Windows 10 Enterprise
- Desde Windows 10 Home a Windows 10 Education
- Desde Windows 10 Mobile a Windows 10 Mobile Enterprise

Los dispositivos deben estar inscritos en Microsoft Intune o ejecutar el software cliente de Configuration Manager. Esta directiva actualmente no es compatible con equipos administrados por MDM local.

## <a name="before-you-start"></a>Antes de empezar  
 Antes de empezar a actualizar dispositivos a la versión más reciente, consulte los requisitos previos siguientes:  

-   Para las ediciones de escritorio de Windows 10: una clave de producto válida para instalar la nueva versión de Windows en todos los dispositivos de destino de la directiva. Esta clave de producto puede ser una clave de activación múltiple (CAM) o una clave de licencias por volumen genérica (CLVG). Las CLVG también se conocen como claves de configuración de cliente del servicio de administración de claves (SAC). Para obtener más información, consulte [Plan para la activación por volumen](https://docs.microsoft.com/windows/deployment/volume-activation/plan-for-volume-activation-client). Para obtener una lista de claves de configuración de cliente KMS, consulte el [Apéndice A](https://docs.microsoft.com/windows-server/get-started/kmsclientkeys) de la Guía de activación de Windows Server. <!--496871-->  

-   Para Windows 10 Mobile: un archivo de licencia XML del Centro de servicios de licencias por volumen (CSLV) de Microsoft. Este archivo contiene la información de licencia para la nueva versión de Windows en todos los dispositivos de destino de la directiva.

- Para administrar este tipo de directiva, debe ocupar el rol de seguridad de **Administrador total** de Configuration Manager.

## <a name="configure-the-edition-upgrade-policy"></a>Configurar la directiva de actualización de edición  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad** > **Configuración de cumplimiento** > **Actualización de edición de Windows 10**.  

3.  En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear directiva de actualización de edición**.  

4.  Haga clic en **Crear directiva**.  

5.  En la página **General** del **Asistente para la creación de directiva de actualización de la edición**, especifique la información siguiente:  

    -   **Nombre**: escriba un nombre para la directiva de actualización de ediciones.  

    -   **Descripción** (opcional): si lo desea, escriba una descripción para la directiva que le ayude a identificarla en la consola de Intune.  

    -   **SKU a la que actualizará el dispositivo**: en la lista desplegable, seleccione la edición de destino de Windows 10 Escritorio o Windows 10 Mobile.  

    -   **Información de licencia** : seleccione una de las siguientes opciones.  

        -   **Clave de producto**: escriba una clave de producto válida para la edición de destino de Windows 10 Escritorio.  

            > [!NOTE]  
            >  Después de crear una directiva que contenga una clave de producto, no se puede editar la clave de producto más adelante. Configuration Manager oculta la clave por motivos de seguridad. Para cambiar la clave de producto, debe volver a escribir toda la clave.  

        -   **Archivo de licencia**: haga clic en **Examinar** para seleccionar un archivo de licencia válido en formato XML. Configuration Manager usa este archivo de licencia para actualizar los dispositivos de Windows 10 Mobile.  

6.  Complete el asistente.  


## <a name="deploy-the-edition-upgrade-policy"></a>Implementar la directiva de actualización de edición  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad** > **Configuración de cumplimiento** > **Actualización de edición de Windows 10**.  

3.  Seleccione la directiva de actualización de la edición de Windows 10 que quiere implementar y después, en la pestaña **Inicio** , en el grupo **Implementación** , haga clic en **Implementar**.  

4.  En el cuadro de diálogo **Implementar la actualización de la edición de Windows 10**, primero elija la colección a la que desee implementar la directiva. Seleccione la programación mediante el cual el cliente evalúa la directiva y después haga clic en **Aceptar**. En el caso de los equipos que se administran con el cliente de Configuration Manager, debe implementar la directiva en una recopilación de dispositivos. En el caso de los equipos inscritos con Intune, puede implementar la directiva en una recopilación de usuarios o dispositivos. 



## <a name="next-steps"></a>Pasos siguientes

Supervise esta implementación desde el nodo **Implementaciones** del espacio de trabajo **Supervisión**. Si ve errores que indican un error de implementación, por ejemplo:
- **No se aplica a este dispositivo**
- **Error de conversión de tipo de datos**

Estos errores no significan que hubo un error en la implementación. En el equipo de destino, compruebe que la actualización se realizó correctamente.

Una vez que el cliente haya evaluado la directiva de destino, aplicará la actualización un plazo de dos horas. [Si la ruta de actualización requiere un reinicio](https://docs.microsoft.com/windows/deployment/upgrade/windows-10-edition-upgrades), se reiniciará en ese momento. Asegúrese de informar a los usuarios a los que implemente la directiva, o prográmela para que se ejecute fuera del horario laboral de los usuarios.

Si aparece el siguiente error en **DcmWmiProvider.log** en el cliente, asegúrese de usar la clave correcta para su escenario de activación. Para obtener más información, consulte la sección [Antes de empezar](#before-you-start). Si usa un servicio de administración de claves para la activación, asegúrese de usar una [clave de configuración de cliente KMS](https://docs.microsoft.com/windows-server/get-started/kmsclientkeys).  <!-- 496871 -->   

`Failed to execute CheckApplicabilityMethod with error = 0x80041001 OsEditionUpgradeProvider`
