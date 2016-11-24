---
title: "Actualizar dispositivos Windows a una versión nueva | System Center Configuration Manager"
description: "Actualice dispositivos que ejecuten Windows 10 Escritorio, Windows 10 Mobile o Windows 10 Holographic a una edición más reciente de forma automática."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b0c9db74-841e-46eb-8924-957cde968bf7
caps.latest.revision: 8
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 7ee088f6da266742e7836499a7f0e072bf446a62


---

# <a name="upgrade-windows-devices-with-the-edition-upgrade-policy-in-system-center-configuration-manager"></a>Actualizar dispositivos de Windows con la directiva de actualización de edición en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*


La **directiva de actualización de edición** de System Center Configuration Manager permite actualizar de forma automática los dispositivos que ejecutan una de las siguientes versiones de Windows 10 a una edición más reciente:

- Windows 10 Escritorio
- Windows 10 Mobile
- Windows 10 Holographic

Las siguientes rutas de acceso de actualización son compatibles:
- Desde Windows 10 Pro a Windows 10 Enterprise
- Desde Windows 10 Home a Windows 10 Education
- Desde Windows 10 Mobile a Windows 10 Mobile Enterprise
- Desde Windows 10 Holographic Pro a Windows 10 Holographic Enterprise

Los dispositivos se deben inscribir en Microsoft Intune. Actualmente, esta característica no es compatible con equipos que ejecuten el software cliente de Configuration Manager o equipos administrados por la MDM local.

## <a name="before-you-start"></a>Antes de empezar  
 Antes de empezar a actualizar dispositivos a la versión más reciente, necesitará uno de los elementos siguientes:  

-   Una clave de producto que sea válida para instalar la nueva versión de Windows en todos los dispositivos de destino de la directiva (para sistemas operativos de escritorio).  

-   Un archivo de licencia de Microsoft que contenga la información de licencia para instalar la nueva versión de Windows en todos los dispositivos de destino de la directiva (para Windows 10 Mobile y Windows 10 Holographic).

- Para crear e implementar este tipo de directiva, debe tener asignado el rol de seguridad **Administrador total** de Configuration Manager.

## <a name="configure-the-edition-upgrade-policy"></a>Configurar la directiva de actualización de edición  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad** > **Configuración de cumplimiento** > **Actualización de edición de Windows 10**.  

3.  En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear directiva de actualización de edición**.  

4.  Haga clic en **Crear directiva**.  

5.  En la página **General** del **Asistente para la creación de directiva de actualización de la edición**, especifique la información siguiente:  

    -   **Nombre** : escriba un nombre para la directiva de actualización de edición.  

    -   **Descripción** (opcional): si lo desea, escriba una descripción para la directiva que le ayude a identificarla en la consola de Intune.  

    -   **SKU a la que se actualizará el dispositivo** : en la lista desplegable, seleccione la versión de Windows 10 Desktop, Windows 10 Holographic o Windows 10 Mobile a la que quiere actualizar los dispositivos de destino.  

    -   **Información de licencia** : seleccione una de las siguientes opciones.  

        -   **Clave de producto** : escriba una clave de producto válida de Windows 10, que se usará para actualizar los dispositivos de destino que ejecuten sistemas operativos de escritorio Windows 10.  

            > [!NOTE]  
            >  Después de crear una directiva que contenga una clave de producto, no se puede editar la clave de producto más adelante. Esto se debe a que la clave se oculta por motivos de seguridad. Para cambiar la clave de producto, debe volver a escribir toda la clave.  

        -   **Archivo de licencia** : haga clic en **Examinar** para seleccionar un archivo de licencia válido en formato XML, que se usará para actualizar los dispositivos de destino que ejecuten sistemas operativos Windows 10 Holographic y Windows 10 Mobile.  

6.  Complete el asistente.  

 La nueva directiva se muestra en el nodo **Actualización de la edición de Windows 10** del área de trabajo **Activos y compatibilidad** .  

## <a name="deploy-the-edition-upgrade-policy"></a>Implementar la directiva de actualización de edición  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad** > **Configuración de cumplimiento** > **Actualización de edición de Windows 10**.  

3.  Seleccione la directiva de actualización de la edición de Windows 10 que quiere implementar y después, en la pestaña **Inicio** , en el grupo **Implementación** , haga clic en **Implementar**.  

4.  En el cuadro de diálogo **Implementar actualización de la edición de Windows 10** , seleccione la recopilación de usuarios o dispositivos en los que desea implementar la directiva y la programación con la que se evaluará la directiva y, a continuación, haga clic en **Aceptar**.  

 Puede supervisar las implementaciones que acaba de crear desde el nodo **Implementaciones** del área de trabajo **Supervisión** .  

 Una vez que la directiva alcance un equipo Windows de destino, se reiniciará durante las dos horas posteriores para aplicar la actualización. Asegúrese de informar a los usuarios a los que implemente la directiva, o prográmela para que se ejecute fuera del horario laboral de los usuarios.



<!--HONumber=Nov16_HO1-->


