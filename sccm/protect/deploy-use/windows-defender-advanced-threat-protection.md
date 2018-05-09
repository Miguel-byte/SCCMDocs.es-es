---
title: Protección contra amenazas avanzada de Windows Defender
titleSuffix: Configuration Manager
description: Aprenda a administrar y supervisar Protección contra amenazas avanzada de Windows Defender, un nuevo servicio que ayuda a las empresas a responder a los ataques avanzados.
ms.date: 03/07/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a5fc033e-828e-4e45-9097-bbbd0697ebdf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 10d746f88d0e7b869e2b73d389944f3b382d687d
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="windows-defender-advanced-threat-protection"></a>Protección contra amenazas avanzada de Windows Defender

*Se aplica a: System Center Configuration Manager (Rama actual)*

A partir de la versión 1606 de Configuration Manager (rama actual), Endpoint Protection puede ayudar a administrar y supervisar la [Protección contra amenazas avanzada (ATP) de Windows Defender](http://aka.ms/technet-wdatp). Protección contra amenazas avanzada de Windows Defender ayuda a las empresas a detectar e investigar ataques avanzados en sus redes, y responder ante ellos.  Las directivas de Configuration Manager o Microsoft Intune pueden ayudarle a incorporar y supervisar dispositivos administrados con Windows 10, versión 1607 (compilación 14328) o versiones posteriores.

Protección contra amenazas avanzada de Windows Defender es un servicio del [Centro de seguridad avanzada de Windows Defender](https://securitycenter.windows.com). Al agregar e implementar un archivo de configuración de incorporación de cliente, Configuration Manager puede supervisar el estado de implementación y el mantenimiento del agente de Protección contra amenazas avanzada de Windows Defender. Protección contra amenazas avanzada de Windows Defender se admite en equipos que ejecutan el cliente de Configuration Manager o que están administrados por Microsoft Intune, pero no se admiten equipos con una administración híbrida de MDM e Intune.

 **Requisitos previos**  

-   Suscripción al servicio en línea Protección de amenazas avanzada de Windows Defender  
-   Equipos cliente que ejecutan Windows 10, versión 1607 y posteriores  
-   Equipos cliente que ejecutan Configuration Manager versión 1610 o un agente cliente posterior, o administrados por Microsoft Intune

## <a name="how-to-create-an-onboarding-configuration-file"></a>Cómo crear un archivo de configuración de incorporación de cliente  

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
