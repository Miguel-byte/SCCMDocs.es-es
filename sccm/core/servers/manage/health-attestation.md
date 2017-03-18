---
title: "Atestación de estado | Microsoft Docs"
description: "Obtenga información sobre la funcionalidad de atestación de estado de dispositivos que puede verse en la consola de Configuration Manager."
ms.custom: na
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 91f9de33-b277-4500-acd6-e7d90a2947c9
caps.latest.revision: 17
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: cb42b6f324dc0019c2109be4d91e0eab4dca4d70
ms.openlocfilehash: 9d88e93c1382d5804598f2db258f325954e328b1
ms.lasthandoff: 03/08/2017


---
# <a name="health-attestation-for-system-center-configuration-manager"></a>Atestación de estado para System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Los administradores pueden ver el estado de la [atestación de estado de los dispositivos de Windows 10](https://technet.microsoft.com/library/mt592023.aspx) en la consola de Configuration Manager.  Esta funcionalidad está disponible para equipos y recursos locales administrados por Configuration Manager y dispositivos móviles administrados con Microsoft Intune. Los administradores pueden especificar si la notificación se realiza a través de la nube o de la insfraestructura local. Esto permite a los equipos cliente sin acceso a Internet habilitar y supervisar dispositivos con la atestación de estado. La atestación de estado del dispositivo permite al administrador garantizar que los equipos cliente tienen habilitadas las siguientes configuraciones BIOS, TPM y de software de arranque de confianza:  

-   Antimalware de inicio temprano: el antimalware de inicio temprano (ELAM) protege su equipo cuando se inicia y antes de inicializar controladores de terceros. [Cómo activar ELAM](https://gallery.technet.microsoft.com/How-to-turn-on-Early-84552ec5)  
-   BitLocker: el Cifrado de unidad BitLocker de Windows es un software que permite cifrar todos los datos almacenados en el volumen del sistema operativo Windows.  [Cómo activar Bitlocker](https://gallery.technet.microsoft.com/How-to-turn-on-BitLocker-34294d3d)  
-   Arranque seguro: el arranque seguro es un estándar de seguridad desarrollado por miembros de la industria de PC para ayudar a garantizar que el equipo arranca solo con el software que el fabricante indica como confiable. [Más información sobre el arranque seguro](https://technet.microsoft.com/library/hh824987.aspx)  
-   Integridad de código: la integridad de código es una característica que mejora la seguridad del sistema operativo al validar la integridad de un controlador o un archivo del sistema cada vez que se carga en memoria. [Más información sobre la integridad de código](https://technet.microsoft.com/library/dd348642.aspx)  


##  <a name="device-health-attestation"></a>Atestación de estado del dispositivo  
 La atestación de estado de dispositivos de Configuration Manager muestra lo siguiente:  

-   **Estado de la atestación de estado** : muestra la cantidad de dispositivos que presentan estados de conformidad, no conformidad, error y desconocido.  
-   **Dispositivos que informan de la atestación de estado** : muestra el porcentaje de dispositivos que informan sobre el estado de la atestación de estado.  
-   **Dispositivos no compatibles ordenados por tipo de cliente** : muestra la proporción de dispositivos móviles y equipos que no son compatibles.  
-   **Principales opciones de configuración ausentes de la atestación de estado** : muestra el número de dispositivos que carecen de opciones de configuración de atestación de estado, que se indican por cada opción.  

 **Requisitos:**  

-   Dispositivos cliente que ejecutan Win10  
-   Windows Server 2016 con la [atestación de estado del dispositivo](https://technet.microsoft.com/windows-server-docs/security/device-health-attestation)
-    TPM 2 habilitado  
-   Desbloquear la comunicación entre el agente cliente de Configuration Manager y el servicio de atestación de estado has.spserv.microsoft.com (puerto 443)

### <a name="how-to-enable-health-attestation-service-communication-on-configuration-manager-client-computers"></a>Cómo habilitar la comunicación del servicio de atestación de estado en los equipos cliente de Configuration Manager  

1.  En la consola de Configuration Manager, elija **Administración** > **Introducción** > **Configuración de cliente**.  Seleccione la pestaña para configurar el **agente de equipo** .  

2.  En el cuadro de diálogo **Configuración predeterminada** , seleccione **Agente de equipo** y después desplácese hacia abajo hasta **Habilitar comunicación con el servicio de atestación de estado**.  

3.  Establezca **Habilitar comunicación con el servicio de atestación de estado** en **Sí**y luego haga clic en **Aceptar**.  

### <a name="how-to-enable-on-premises-health-attestation-service-communication-on-configuration-manager-client-computers"></a>Cómo habilitar la comunicación del servicio de atestación de estado local en los equipos cliente de Configuration Manager


1. En la consola de Configuration Manager, vaya a **Administración** > **Información general** > **Configuración de cliente**y, después, establezca **Usar el servicio de atestación de estado local** en **Sí**.


2. Especifique el valor de **URL del servicio de atestación de estado local**y, después, haga clic en **Aceptar**.

## <a name="how-to-view-health-attestation"></a>Cómo ver la atestación de estado  


1.  Para ver la atestación de estado de dispositivo, en la consola de Configuration Manager, vaya al área de trabajo de **Supervisión** , haga clic en el nodo **Seguridad** y luego haga clic en **Atestación de estado**.  

2.  Se muestra la atestación de estado de dispositivo.  

 El estado de la atestación de estado de dispositivos cliente puede usarse para definir reglas de acceso condicional de las directivas de cumplimiento para dispositivos administrados por Configuration Manager con Microsoft Intune. Para más información, consulte [Administrar directivas de cumplimiento de dispositivo en System Center Configuration Manager](/sccm/protect/deploy-use/device-compliance-policies).  

