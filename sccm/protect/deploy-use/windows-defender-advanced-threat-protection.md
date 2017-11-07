---
title: "Protección contra amenazas avanzada de Windows Defender"
titleSuffix: Configuration Manager
description: "Aprenda a administrar y supervisar Protección contra amenazas avanzada de Windows Defender, un nuevo servicio que ayuda a las empresas a responder a los ataques avanzados."
ms.custom: na
ms.date: 03/07/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a5fc033e-828e-4e45-9097-bbbd0697ebdf
caps.latest.revision: "5"
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 561a03c7046accaa8e6d36407c75cbd4248188ce
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/12/2017
---
# <a name="windows-defender-advanced-threat-protection"></a>Protección contra amenazas avanzada de Windows Defender

*Se aplica a: System Center Configuration Manager (rama actual)*

A partir de la versión 1606 de Configuration Manager (rama actual), Endpoint Protection puede ayudar a administrar y supervisar la protección contra amenazas avanzadas de Windows Defender (ATP). Protección contra amenazas avanzada de Windows Defender es un nuevo servicio que ayuda a las empresas a detectar ataques avanzados en sus redes, a investigarlos y a responder a ellos.  Obtenga más información sobre [Protección contra amenazas avanzada de Windows Defender](http://aka.ms/technet-wdatp). Las directivas de Configuration Manager pueden ayudarle a incorporar y supervisar dispositivos administrados de Windows 10, versión 1607 (compilación 14328).

Protección contra amenazas avanzada de Windows Defender es un servicio en el [Centro de seguridad de Windows](https://securitycenter.windows.com). Al agregar e implementar un archivo de configuración de incorporación de cliente, Configuration Manager puede supervisar el estado de implementación y el mantenimiento del agente de Protección contra amenazas avanzada de Windows Defender. La Protección contra amenazas avanzada de Windows Defender solo se admite en equipos que ejecutan el cliente de Configuration Manager. No se admiten la administración de dispositivos móviles local y los equipos administrados con MDM de Intune híbrido.

 **Requisitos previos**  

-   Suscripción al servicio en línea Protección contra amenazas avanzada de Windows Defender  
-   Equipos cliente que ejecutan Windows 10, versión 1607 y posteriores  
-   Equipos cliente que ejecutan la versión de Configuration Manager 1610 o un agente cliente posterior

## <a name="how-to-create-an-onboarding-configuration-file"></a>Creación de un archivo de configuración de incorporación  

 1.  Inicie sesión en el [servicio en línea Protección contra amenazas avanzada de Windows Defender](https://securitycenter.windows.com/).   

 2.  Haga clic en el elemento de menú **Administración de puntos de conexión**.  

 3.  Seleccione **System Center Configuration Manager (rama actual), versión 1606** y haga clic en **Descargar paquete**.  

 4.  Descargue el archivo comprimido (.zip) y extraiga el contenido.

> [!IMPORTANT]
> El archivo de configuración de Protección contra amenazas avanzada de Windows Defender contiene información confidencial que debe mantenerse segura.

## <a name="onboard-devices-for-windows-defender-atp"></a>Dispositivos incorporados para Protección contra amenazas avanzada de Windows Defender  

1.  En la consola de Configuration Manager, vaya a **Activos y compatibilidad** > **Información general** > **Endpoint Protection** > **Directivas de Windows Defender ATP** y haga clic en **Crear directiva de Windows Defender ATP**. Se abre el Asistente para crear directiva de Protección contra amenazas avanzada de Windows Defender.  

2.  Escriba el **Nombre** y la **Descripción** de la directiva de Protección contra amenazas avanzada de Windows Defender y seleccione **Incorporación**. Haga clic en **Siguiente**.  

3.  **Vaya** al archivo de configuración proporcionado por el inquilino del servicio en la nube de Protección contra amenazas avanzada de Windows Defender de la organización. Haga clic en **Siguiente**.  

4.  Especifique los ejemplos de archivos de dispositivos administrados que se recopilan y se comparten para su análisis.  

    -   **Ninguno**   

    -   **Todos los tipos de archivo**  

     Haga clic en **Siguiente**.  

5.  Revise el resumen y finalice el asistente.  

6.  Ahora puede hacer clic en **Implementar** para implementar la directiva de Windows Defender ATP en equipos cliente administrados.  

## <a name="monitor-windows-defender-atp"></a>Supervisión de Protección contra amenazas avanzada de Windows Defender  

1.  En la consola de Configuration Manager, vaya a **Supervisión** > **Información general** > **Seguridad** y luego haga clic en **Protección contra amenazas avanzada de Windows Defender**.  

2.  Revise el panel de Protección contra amenazas avanzada de Windows Defender.  

    -   **Estado de implementación del agente de Windows Defender**: el número y el porcentaje de equipos cliente administrados aptos con directiva de Windows Defender ATP activa incorporados.  

    -   **Estado del agente de Windows Defender ATP**: porcentaje de equipos cliente que envía informes de estado de su agente de Windows Defender ATP.  

        -   **Correcto**: funciona correctamente.  

        -   **Inactivo**: no se ha enviado ningún dato al servicio durante el período.  

        -   **Estado del agente**: el servicio del sistema del agente en Windows no se está ejecutando  

        -   **No incorporado**: se aplicó la directiva, pero el agente no ha notificado la incorporación de la directiva  


## <a name="how-to-create-and-deploy-an-offboarding-configuration-file"></a>Creación e implementación de un archivo de configuración de retirada  

1.  Inicie sesión en el [servicio en línea Protección contra amenazas avanzada de Windows Defender](https://securitycenter.windows.com/).   

2.  Haga clic en el elemento de menú **Administración de puntos de conexión**.  

3.  Seleccione **System Center Configuration Manager (rama actual), versión 1606** y haga clic en **Retirada de punto de conexión**.  

4.  Descargue el archivo comprimido (.zip) y extraiga el contenido. Los archivos de retirada son válidos durante 30 días.

5.  En la consola de Configuration Manager, vaya a **Activos y compatibilidad** > **Información general** > **Endpoint Protection** > **Directivas de Windows Defender ATP** y haga clic en **Crear directiva de Windows Defender ATP**. Se abre el Asistente para crear directiva de Protección contra amenazas avanzada de Windows Defender.  

6.  Escriba el **Nombre** y la **Descripción** de la directiva de Protección contra amenazas avanzada de Windows Defender y seleccione **Retirada**. Haga clic en **Siguiente**.  

7.  **Vaya** al archivo de configuración proporcionado por el inquilino del servicio en la nube de Protección contra amenazas avanzada de Windows Defender de la organización. Haga clic en **Siguiente**.  

8.  Revise el resumen y finalice el asistente.  

9.  Ahora puede hacer clic en **Implementar** para implementar la directiva de Windows Defender ATP en equipos cliente administrados.  

> [!IMPORTANT]
> El archivo de configuración de Protección contra amenazas avanzada de Windows Defender contiene información confidencial que debe mantenerse segura.

[Protección contra amenazas avanzada de Windows Defender](https://technet.microsoft.com/itpro/windows/keep-secure/windows-defender-advanced-threat-protection)

[Solucionar problemas de incorporación de Protección contra amenazas avanzada de Windows Defender](https://technet.microsoft.com/itpro/windows/keep-secure/troubleshoot-onboarding-windows-defender-advanced-threat-protection)
