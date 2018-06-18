---
title: Integración con Windows Update for Business en Windows 10
titleSuffix: Configuration Manager
description: Use Windows Update for Business para mantener actualizados los dispositivos basados en Windows 10 de su organización para los dispositivos conectados al servicio de Windows Update.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/22/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 183315fe-27bd-456f-b2c5-e8d25e05229b
ms.openlocfilehash: 07616a1c03c0383e9001418043dc6cd7ec117c1d
ms.sourcegitcommit: 493cc42f05b9388ef872e466e5a75d569642b9fc
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2018
ms.locfileid: "34703492"
---
# <a name="integration-with-windows-update-for-business-in-windows-10"></a>Integración con Windows Update for Business en Windows 10

*Se aplica a: System Center Configuration Manager (Rama actual)*

Windows Update para empresas (WUfB) permite mantener los dispositivos basados en Windows 10 de la organización siempre actualizados con las características de Windows y las defensas de seguridad más recientes cuando estos dispositivos se conectan directamente al servicio de Windows Update (WU). Configuration Manager puede diferenciar entre los equipos con Windows 10 que usan WUfB y WSUS para obtener actualizaciones de software.  

 Algunas características de Configuration Manager ya no están disponibles cuando los clientes de Configuration Manager se configuran para recibir actualizaciones de WU, lo que incluye WUfB o Windows Insiders:  

-   Informes de cumplimiento de Windows Update:  

    -   Configuration Manager no tendrá conocimiento de las actualizaciones que se publican en WU. Los clientes de Configuration Manager configurados para recibir actualizaciones de WU mostrarán **desconocido** para estas actualizaciones en la consola de Configuration Manager.  

    -   La solución de problemas de estado de cumplimiento general es difícil porque el estado **desconocido** era solo para los clientes que no habían notificado su estado de examen a WSUS. Ahora también incluye los clientes de Configuration Manager que reciben las actualizaciones de WU.  

    -   El acceso condicional (para los recursos corporativos) según el estado de cumplimiento de actualización no funcionará como se espera para los clientes que reciben actualizaciones de WU, ya que nunca cumplirían con la compatibilidad desde Configuration Manager.  

    -   El cumplimiento de las actualizaciones de definición es parte de los informes de cumplimiento general de actualización y no funcionará como sería de esperar.  El cumplimiento de las actualizaciones de definición también forma parte de la evaluación de acceso condicional.  

-   Los informes generales de Endpoint Protection para Defender según el estado del cumplimiento de las actualizaciones no devolverán resultados precisos debido a la ausencia de datos de análisis.  

-   Configuration Manager no podrá implementar las actualizaciones de Microsoft, como Office, Internet Explorer y Visual Studio, en los clientes que están conectados a WUfB para recibir actualizaciones.  

-   Configuration Manager no podrá implementar actualizaciones de terceros publicadas en WSUS y administradas a través de Configuration Manager en los clientes que están conectados a WUfB para recibir actualizaciones.  

-   La implementación del cliente completo de Configuration Manager que usa la infraestructura de actualizaciones de software no funcionará para los clientes que están conectados a WUfB para recibir actualizaciones.  

## <a name="identify-clients-that-use-wufb-for-windows-10-updates"></a>Identificación de los clientes que utilizan WUfB para las actualizaciones de Windows 10  
 Use el procedimiento siguiente para identificar los clientes que usan WUfB para obtener las actualizaciones de Windows 10. Después, configure estos clientes para que dejen de usar WSUS para obtener las actualizaciones e implemente una configuración de agente cliente para deshabilitar el flujo de trabajo de actualizaciones de software para estos clientes.  

 **Requisitos previos**  

-   Clientes que ejecutan Windows 10 Desktop Pro o Windows 10 Enterprise Edition versión 1511 o posterior  

-   [Windows Update for Business](https://technet.microsoft.com/library/mt622730\(v=vs.85\).aspx) está implementado y los clientes utilizan WUfB para obtener las actualizaciones de Windows 10.  

#### <a name="to-identify-clients-that-use-wufb"></a>Para identificar los clientes que utilizan WUfB  

1.  Si se habilitó previamente, deshabilite el agente de Windows Update para que no examine nada con WSUS. La clave del Registro siguiente se puede establecer para indicar si el equipo se examina con WSUS o Windows Update.  Cuando el valor es 2, no se realiza el análisis con WSUS.  
    - **HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU\UseWUServer**

2.  Existe un atributo nuevo, **UseWUServer**, que se encuentra en el nodo **Windows Update** del Explorador de recursos de Configuration Manager.  

3.  Cree una colección basada en el atributo **UseWUServer** para todos los equipos que estén conectados a través de WUfB para conseguir actualizaciones.  

4.  Cree una configuración de agente cliente para deshabilitar el flujo de trabajo de actualización de software. Implemente la configuración en la colección de equipos que están conectados directamente a WUfB.  

5.  Los equipos que se administran a través de WUfB, mostrarán el valor **Desconocido** en el estado de cumplimiento y no se tendrán en cuenta como parte del porcentaje total de cumplimiento.  

## <a name="configure-windows-update-for-business-deferral-policies"></a>Configuración de directivas de aplazamiento de Windows Update para empresas
<!-- 1290890 -->
A partir de la versión 1706 de Configuration Manager, puede configurar directivas de aplazamiento para actualizaciones de características de Windows 10 o actualizaciones de calidad para dispositivos con Windows 10 administradas directamente mediante Windows Update para empresas. Puede administrar las directivas de aplazamiento en el nuevo nodo **Directivas de Windows Update para empresas**, en **Biblioteca de Software** > **Mantenimiento de Windows 10**.

>[!NOTE] 
>A partir de la versión 1802 de Configuration Manager, se pueden establecer directivas de aplazamiento para Windows Insider. <!--507201-->Para obtener más información sobre el programa Windows Insider, vea [Introducción al Programa Windows Insider para empresas](https://docs.microsoft.com/windows/deployment/update/waas-windows-insider-for-business).

### <a name="prerequisites"></a>Requisitos previos
-   Windows 10, versión 1703 o posteriores.
-   Los dispositivos con Windows 10 administrados por Windows Update para empresas deben tener conectividad a Internet.

#### <a name="to-create-a-windows-update-for-business-deferral-policy"></a>Para crear una directiva de aplazamiento para Windows Update para empresas
1. En **Biblioteca de Software** > **Mantenimiento de Windows 10** > **Directivas de Windows Update para empresas**
2. En la pestaña **Inicio**, en el grupo **Crear**, seleccione **Create Windows Update for Business Policy** (Crear directiva de Windows Update para empresas) para abrir el Asistente para creación de directiva de Windows Update para empresas.
3. En la página **General**, proporcione un nombre y una descripción para la directiva.
4. En la página **Deferral Policies** (Directivas de aplazamiento), configure si se van a aplazar o pausar las actualizaciones de características. Las actualizaciones de características son generalmente nuevas características de Windows. Después de configurar el parámetro **Nivel de preparación de la rama**, puede definir si le gustaría aplazar la recepción de actualizaciones de características después de que se pongan a disposición de los usuarios por parte de Microsoft, y por cuánto tiempo.
    - **Nivel de preparación de la rama**: configure la rama para la que el dispositivo recibirá actualizaciones de Windows (Rama actual o Rama actual para empresas).
    - **Período de aplazamiento (días)**: especifique el número de días durante los que se aplazarán las actualizaciones de características. Puede aplazar la recepción de estas actualizaciones de características durante un período de 180 días a partir de su lanzamiento.
    - **Pausar el inicio de las actualizaciones de características**: seleccione si desea pausar la recepción de actualizaciones de características para los dispositivos durante un período de hasta 60 días a partir del momento en que pausa las actualizaciones. Una vez que transcurra el máximo de días, la funcionalidad de pausa expirará automáticamente y el dispositivo buscará actualizaciones aplicables en Windows Update. Después de este análisis, puede pausar las actualizaciones de nuevo. Puede quitar la pausa de las actualizaciones de características desactivando la casilla.   
5. Elija si desea aplazar o pausar las actualizaciones de calidad. Las actualizaciones de calidad suelen ser correcciones y mejoras en la funcionalidad de Windows existente y normalmente se publican el primer martes de cada mes, aunque pueden publicarse en cualquier momento por parte de Microsoft. Puede definir si desea aplazar la recepción de actualizaciones de calidad después de su lanzamiento, y por cuánto tiempo.
    - **Período de aplazamiento (días)**: especifique el número de días durante los que se aplazarán las actualizaciones de características. Puede aplazar la recepción de estas actualizaciones de características durante un período de 180 días a partir de su lanzamiento.
    - **Pausar el inicio de las actualizaciones de calidad**: seleccione si desea pausar la recepción de actualizaciones de calidad para los dispositivos durante un período de hasta 35 días a partir del momento en que pausa las actualizaciones. Una vez que transcurra el máximo de días, la funcionalidad de pausa expirará automáticamente y el dispositivo buscará actualizaciones aplicables en Windows Update. Después de este análisis, puede pausar las actualizaciones de nuevo. Puede quitar la pausa de las actualizaciones de calidad desactivando la casilla.
6. Seleccione **Instalar actualizaciones de otros productos de Microsoft** para habilitar el parámetro de directiva de grupo que permite que la configuración de aplazamiento sea aplicable a Microsoft Update, así como a las actualizaciones de Windows Update.
7. Seleccione **Include drivers with Windows Update** (Incluir controladores con Windows Update) para actualizar automáticamente los controladores desde las actualizaciones de Windows Update. Si desactiva esta opción, no se descargan las actualizaciones de controladores desde Windows Update.
8. Complete el asistente para crear la nueva directiva de aplazamiento.

#### <a name="to-deploy-a-windows-update-for-business-deferral-policy"></a>Para implementar una directiva de aplazamiento para Windows Update para empresas
1. En **Biblioteca de Software** > **Mantenimiento de Windows 10** > **Directivas de Windows Update para empresas**
2. En la pestaña **Inicio** del grupo **Implementación**, seleccione **Implementar la directiva de Windows Update for Business**.
3. Configure las siguientes opciones:
    - **Directiva de configuración que desea implementar:**: seleccione la directiva de Windows Update para empresas que desea implementar.
    - **Recopilación**: haga clic en **Examinar** para seleccionar la recopilación en la que quiere implementar la directiva.
    - **Corregir las reglas no compatibles cuando se admita**: seleccione esta opción para corregir automáticamente las reglas que no sean compatibles con Instrumental de administración de Windows (WMI), el Registro, los scripts y toda la configuración de los dispositivos móviles que Configuration Manager haya inscrito.
    - **Permitir la corrección fuera de la ventana de mantenimiento**: si se ha configurado una ventana de mantenimiento para la recopilación en la que se va a implementar la directiva, habilite esta opción para permitir que la configuración de cumplimiento corrija el valor fuera de la ventana de mantenimiento. Para obtener más información sobre las ventanas de mantenimiento, consulte [Cómo utilizar las ventanas de mantenimiento](/sccm/core/clients/manage/collections/use-maintenance-windows).
    - **Generar una alerta**: configura una alerta que se genera si la compatibilidad de la línea base de configuración es inferior a un determinado porcentaje en una hora y fecha especificadas. También puede especificar si desea que se envíe una alerta a System Center Operations Manager.
    - **Retraso aleatorio (horas)**: especifique una ventana de retraso lo suficientemente grande para evitar un procesamiento excesivo en el Servicio de inscripción de dispositivos de red. El valor predeterminado es 64 horas.
    - **Programación**: especifique la programación de evaluación de cumplimiento según la cual se evalúa el perfil implementado en los equipos cliente. La programación puede ser simple o personalizada. Los equipos cliente evalúan el perfil cuando el usuario inicia sesión.
4.  Complete el asistente para implementar el perfil.
