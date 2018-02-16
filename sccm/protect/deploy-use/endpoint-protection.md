---
title: Endpoint Protection
titleSuffix: Configuration Manager
description: "Obtenga información sobre cómo administrar las directivas antimalware y la seguridad del Firewall de Windows para equipos cliente de su jerarquía de Configuration Manager."
ms.custom: na
ms.date: 02/09/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 76c90f64-d729-456b-8304-01852cd66fb6
caps.latest.revision: 
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 3f8d0d7934a539729793cd0307d6fa5d3e31bf3a
ms.sourcegitcommit: fbde417e3c3002898bd216a7e110e725ae269893
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2018
---
# <a name="endpoint-protection"></a>Endpoint Protection

*Se aplica a: System Center Configuration Manager (Rama actual)*

Endpoint Protection administra las directivas antimalware y la seguridad del Firewall de Windows de los equipos cliente de su jerarquía de Configuration Manager.  

> [!IMPORTANT]  
>  Debe tener una licencia para usar Endpoint Protection para administrar clientes en su jerarquía de Configuration Manager.  

 Si usa Endpoint Protection con Configuration Manager, disfrutará de las siguientes ventajas:  

-   Configuración de directivas antimalware, configuración del Firewall de Windows y administración de la protección contra amenazas avanzada de Windows Defender en grupos de equipos seleccionados  
-   Uso de las actualizaciones de software de Configuration Manager para descargar los archivos de definición de antimalware más recientes a fin de mantener actualizados los equipos cliente  
-   Envío de notificaciones por correo electrónico, supervisión en la consola y visualización de informes. Estas acciones informan a los usuarios administrativos de la presencia de software malintencionado en los equipos cliente.  

Windows Defender ya está instalado en equipos con versiones a partir de Windows 10 y Windows Server 2016. Para estos sistemas operativos, se instala un cliente de administración de Windows Defender cuando se instala el cliente de Configuration Manager. En equipos con Windows 8.1 y versiones anteriores, el cliente de Endpoint Protection se instala con el cliente de Configuration Manager. El cliente de Windows Defender y Endpoint Protection tiene las siguientes funcionalidades:  

-   Detección y corrección de malware y spyware  
-   Detección y corrección de rootkit  
-   Evaluación y definición automática de vulnerabilidades críticas y actualizaciones del motor  
-   Detección de vulnerabilidades de red a través del Sistema de inspección de red  
-   Integración con Cloud Protection Service para informar a Microsoft sobre malware. Si se une a este servicio, el cliente de Endpoint Protection o Windows Defender descargarán las definiciones más recientes desde el Centro de protección contra malware cuando se detecte malware no identificado en un equipo.  

> [!NOTE]  
>  El cliente de Endpoint Protection se puede instalar en un servidor que ejecute Hyper-V y en máquinas virtuales invitadas con sistemas operativos compatibles. Para evitar el uso excesivo de la CPU, las acciones de Endpoint Protection tienen un retraso aleatorio integrado para que los servicios de protección no se ejecuten simultáneamente.  

 Además, la configuración de Firewall de Windows con Endpoint Protection se administra en la consola de Configuration Manager.  

 [Escenario de ejemplo: uso de System Center Endpoint Protection para proteger los equipos frente al malware en System Center Configuration Manager](scenarios-endpoint-protection.md) con Endpoint Protection y el Firewall de Windows.  


## <a name="managing-malware-with-endpoint-protection"></a>Administración de malware con Endpoint Protection  
 Endpoint Protection en Configuration Manager permite crear directivas antimalware que contengan opciones de configuración de cliente de Endpoint Protection. Implemente estas directivas antimalware en equipos cliente. A continuación, supervise el cumplimiento en el nodo **Estado de Endpoint Protection** en **Seguridad** del área de trabajo **Supervisión**. Utilice también los informes de Endpoint Protection en el nodo **Informes**.  

 Información adicional:  

-   [How to create and deploy antimalware policies for Endpoint Protection in System Center Configuration Manager](endpoint-antimalware-policies.md) (Cómo crear e implementar directivas antimalware para Endpoint Protection en System Center Configuration Manager): cree, implemente y supervise directivas antimalware con una lista con los ajustes que puede configurar.  

-   [How to monitor Endpoint Protection in System Center Configuration Manager](monitor-endpoint-protection.md) (Cómo supervisar Endpoint Protection en System Center Configuration Manager): supervise informes de actividad, equipos cliente infectados y mucho más.  

-   [How to manage antimalware policies and firewall settings for Endpoint Protection in System Center Configuration Manager](endpoint-antimalware-firewall.md) (Cómo administrar las directivas antimalware y la configuración de firewall para Endpoint Protection en System Center Configuration Manager): elimine el malware que se encuentra en los equipos cliente.  


## <a name="managing-windows-firewall-with-endpoint-protection"></a>Administración del Firewall de Windows con Endpoint Protection  
 Endpoint Protection en Configuration Manager proporciona administración básica del Firewall de Windows en los equipos cliente. Para cada perfil de red, puede configurar las siguientes opciones:  

-   Habilitar o deshabilitar el Firewall de Windows.  

-   Bloquear todas las conexiones entrantes, incluidas las de la lista de programas permitidos.  

-   Notificar al usuario cuando el Firewall de Windows bloquee un nuevo programa.  

> [!NOTE]  
>  Endpoint Protection es compatible solo con la administración del Firewall de Windows.  


 Para obtener más información, consulte [Crear e implementar directivas de Firewall de Windows para Endpoint Protection](create-windows-firewall-policies.md).  


## <a name="windows-defender-advanced-threat-protection"></a>Protección contra amenazas avanzada de Windows Defender

Endpoint Protection administra y supervisa el servicio Protección contra amenazas avanzada (ATP) de Windows Defender. El servicio ATP de Windows Defender ayuda a las empresas a detectar e investigar ataques avanzados en la red corporativa, y responder a ellos. Para obtener más información, consulte [Protección contra amenazas avanzada de Windows Defender (ATP)](windows-defender-advanced-threat-protection.md).

## <a name="endpoint-protection-workflow"></a>Flujo de trabajo de Endpoint Protection  
 Use el siguiente diagrama para entender mejor el flujo de trabajo para implementar Endpoint Protection en su jerarquía de Configuration Manager.  

 ![Flujo de trabajo de Endpoint Protection](../media/Endpoint-Protection-Workflow.gif)  

## <a name="endpoint-protection-client-for-mac-computers-and-linux-servers"></a>Cliente de Endpoint Protection para equipos Mac y servidores Linux  
 System Center Endpoint Protection incluye un cliente de Endpoint Protection para Linux y para equipos Mac. A estos clientes no se les suministra Configuration Manager, por lo que debe descargar los siguientes productos del [Centro de servicios de licencias por volumen de Microsoft](https://www.microsoft.com/licensing/servicecenter/default.aspx).  

-   System Center Endpoint Protection para Mac  

-   System Center Endpoint Protection para Linux  


> [!IMPORTANT]  
>  Debe ser un cliente de licencia por volumen de Microsoft para descargar los archivos de instalación de Endpoint Protection para Linux y Mac.  

 Estos productos no se pueden administrar desde la consola de Configuration Manager. Sin embargo, se suministra un módulo de administración de System Center Operations Manager con los archivos de instalación, que permite administrar el cliente para Linux mediante Operations Manager.  

### <a name="how-to-get-the-endpoint-protection-client-for-mac-computers-and-linux-servers"></a>Cómo obtener el cliente de Endpoint Protection para equipos Mac y servidores Linux

Siga estos pasos para descargar el archivo de imagen que contiene el software cliente de Endpoint Protection y la documentación para equipos Mac y servidores Linux.
1. Inicie sesión en el [Centro de servicios de licencias por volumen de Microsoft](https://www.microsoft.com/licensing/servicecenter/default.aspx).
2. Seleccione la pestaña **Descargas y claves** de la parte superior del sitio web.
3. Filtre por el producto **System Center Endpoint Protection (rama actual)**.
4. Haga clic en el vínculo **Descargar**.
5. Haga clic en **Continue**. Debería ver varios archivos, incluido uno llamado: **System Center Endpoint Protection (rama actual: versión 1606) for Linux OS and Macintosh OS Multilanguage 32/64 bit 1878 MB ISO**.
6. Haga clic en el icono de flecha para descargar el archivo. El nombre del archivo es **SW_DVD5_Sys_Ctr_Endpnt_Prtctn_1606_MultiLang_-3_EptProt_Lin_Mac_MLF_X21-67050.ISO**.

La actualización de enero de 2018 (X21-67050) incluye las siguientes versiones:

- System Center Endpoint Protection para Mac 4.5.32.0 (compatible con macOS 10.13 High Sierra)
- System Center Endpoint Protection para Linux 4.5.20.0 

 Para más información acerca de cómo instalar y administrar los clientes de Endpoint Protection en equipos Linux y Mac, use la documentación que acompaña a estos productos. Encontrará la documentación del producto en la carpeta **Documentation** del archivo .ISO.
