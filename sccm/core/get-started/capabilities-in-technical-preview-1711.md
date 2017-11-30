---
title: Technical Preview 1711 | Microsoft Docs
titleSuffix: Configuration Manager
description: "Obtenga información sobre las características disponibles en la versión 1711 de Technical Preview para System Center Configuration Manager."
ms.custom: na
ms.date: 11/17/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2e68dc12-6776-437a-9138-45cd7d4bf9cf
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 4c1a51f7ed31768d7f7308bc00feaf960f43918f
ms.sourcegitcommit: b74c1beaabbb628fdf5d6948fa9a6ad719fd5035
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="capabilities-in-technical-preview-1711-for-system-center-configuration-manager"></a>Funcionalidades de Technical Preview 1711 para System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Technical Preview)*

En este artículo se presentan las características disponibles en Technical Preview para System Center Configuration Manager, versión 1711. Puede instalar esta versión para actualizar y agregar nuevas capacidades al sitio de Technical Preview de Configuration Manager. Antes de instalar esta versión de Technical Preview, revise [Technical Preview para System Center Configuration Manager](../../core/get-started/technical-preview.md) para familiarizarse con los requisitos y las limitaciones generales del uso de este tipo de versiones y para saber cómo actualizar entre versiones y cómo proporcionar comentarios sobre las características de Technical Preview.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**Problemas conocidos de esta Technical Preview:**
-   **Compatibilidad con Windows 10, versión 1709 (también conocida como Fall Creators Update)**.  A partir de esta versión de Windows, Windows Media incluye varias ediciones. Al configurar una secuencia de tareas para usar un paquete de actualizaciones del sistema operativo o una imagen del sistema operativo, no olvide seleccionar una [edición que se pueda usar con Configuration Manager](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-as-a-client).
-   **La actualización a una nueva versión preliminar no se puede realizar cuando hay un servidor de sitio en modo pasivo**. Si ejecuta una versión preliminar que tiene un [servidor de sitio primario en modo pasivo](/sccm/core/get-started/capabilities-in-technical-preview-1706#site-server-role-high-availability), debe desinstalarlo para poder actualizar correctamente el sitio en versión preliminar a esta nueva versión preliminar. Puede volver a instalar el servidor de sitio en modo pasivo después de que el sitio finalice la actualización.

  Para desinstalar el servidor de sitio en modo pasivo:
  1. En la consola vaya a **Administración** > **General** > **Configuración de sitio** > **Servidores y roles del sistema de sitios** y seleccione el servidor de sitio en modo pasivo.
  2. En el panel **Roles del sistema de sitio**, haga clic con el botón derecho en el rol **Servidor de sitio** y después elija **Quitar rol**.
  3. Haga clic con el botón derecho en el servidor de sitio en modo pasivo y después elija **Eliminar**.
  4. Después de que el servidor de sitio se desinstala, en el servidor de sitio principal activo, reinicie el servicio **CONFIGURATION_MANAGER_UPDATE**.

**Estas son las nuevas características que puede probar con esta versión.**  

<!--  Section Template
##  FEATURE
### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="improvements-to-run-task-sequence"></a>Mejoras en Ejecutar secuencia de tareas
<!-- 1261338 -->

Esta versión preliminar técnica mejorará el paso Ejecutar secuencia de tareas. Estos son algunos de los elementos que incluyen las mejoras:

 - Compatibilidad con todos los escenarios de implementación de sistemas operativos desde el Centro de Software, el entorno PXE y soportes físicos.
 - Mejoras en las acciones de la consola como copiar, importar, exportar y advertir durante la eliminación de objetos.
 - Compatibilidad con el Asistente para **crear contenido preconfigurado**.
 - Integración con Verificación de la implementación.
 - El paso Ejecutar secuencia de tareas ahora puede usarse en los distintos niveles de secuencias de tareas, no solo en una relación de elementos primarios y secundarios. Las relaciones de varios niveles aumentan la complejidad, así que úselas con precaución. Estas relaciones se siguen comprobando para las referencias circulares.

### <a name="try-it-out"></a>Haga la prueba  

Intente realizar las tareas siguientes y luego envíenos sus **comentarios** desde la pestaña **Inicio** de la cinta para comunicarnos si funcionó:

1. En el editor de secuencia de tareas, haga clic en **Agregar**, seleccione **General** y haga clic en **Ejecutar secuencia de tareas**.
2. Haga clic en **Examinar** para seleccionar la secuencia de tareas secundaria.

## <a name="allow-user-interaction-when-installing-an-application----1356976---"></a>Permitir la interacción del usuario al instalar aplicaciones como <!-- 1356976 -->

Con esta versión preliminar, puede permitir que un usuario final interactúe con la instalación de una aplicación durante la ejecución de la secuencia de tareas. Por ejemplo, ejecute un proceso de instalación que solicite al usuario final diversas opciones. En algunos instaladores de aplicaciones no se pueden silenciar los mensajes, o bien el proceso de instalación puede requerir valores de configuración específicos que solo conoce el usuario. Esta característica permite controlar estos escenarios de instalación.

### <a name="try-it-out"></a>Haga la prueba

Trate de realizar las tareas siguientes y, luego, envíenos sus **comentarios** desde la pestaña **Inicio** de la barra de herramientas para comunicarnos si funcionó:

1.  Cree o edite una aplicación. Para obtener más información, consulte [Creación de aplicaciones con System Center Configuration Manager](/sccm/apps/deploy-use/create-applications).

    a. Elija la pestaña **Experiencia del usuario** en las **propiedades de Windows Installer (archivo \*msi)**.

    b. Seleccione **Instalar para el sistema** en **Comportamiento de instalación**.

    c. Seleccione **Tanto si un usuario inició sesión como si no** en **Requisito de inicio de sesión**.

    d. Seleccione **Normal** en **Visibilidad del programa de instalación**. Puede elegir entre tres opciones: **Minimizada**, **Normal** o **Maximizada**.

    e. Seleccione la casilla **Permitir a los usuarios ver la instalación del programa e interactuar con la misma**.

2.  Cree o edite una secuencia de tareas para instalar la aplicación mediante el paso **Instalar aplicación**. Para obtener más información, vea la sección [Instalar aplicación](/sccm/osd/understand/task-sequence-steps#BKMK_InstallApplication) del artículo [Pasos de la secuencia de tareas en System Center Configuration Manager](/sccm/osd/understand/task-sequence-steps).

    a. Secuencia de tareas de creación de imágenes después del paso Instalar Windows y Configuration Manager.

    b. Secuencia de tareas de actualización local en el grupo de procesamiento posterior.

3.  Implemente la secuencia de tareas en un cliente.
4.  Instale la secuencia de tareas desde el Centro de Software.

Durante el progreso de la secuencia de tareas, la interfaz de instalación de la aplicación aparece en el dispositivo de destino del usuario final. El progreso de la secuencia de tareas se pausa hasta que el usuario final complete el flujo de trabajo de la instalación de la aplicación.

### <a name="install-using-the-wizard"></a>Instalación mediante el asistente

También puede utilizar esta característica al implementar una aplicación mediante el asistente.

1. Cree o edite una aplicación.
2. Implemente la aplicación en un cliente.
3. Instale la aplicación desde el Centro de software. Debe aparecer la interfaz de instalación de la aplicación. El usuario final debe seguir al Asistente para instalación de aplicaciones y la aplicación se instalará correctamente.

## <a name="new-compliance-policy-options-for-windows-10"></a>Nuevas opciones de directivas de cumplimiento para Windows 10
A continuación, se muestran las nuevas directivas de cumplimiento que se pueden configurar en dispositivos Windows 10.
- **Requerir firewall**.  Especifique si un dispositivo debe tener un firewall habilitado y si tiene que estar supervisando todas las redes.
- **Requerir Control de cuentas de usuario**. Especifique que un dispositivo debe tener habilitado el Control de cuentas de usuario.
- **Defender**:
  - **Requerir el Antivirus de Windows Defender**.  Requiera que un dispositivo tenga el Antivirus de Windows Defender habilitado.
  - **Versión del Antivirus de Windows Defender**.  Especifique la versión mínima de las definiciones de spyware que debe tener instaladas un dispositivo.
  - **Requerir firma actual de Antivirus de Windows Defender**. Compruebe que una firma del Antivirus de Windows Defender esté actualizada.
  - **Requerir protección en tiempo real**.  Especifique si un dispositivo debe tener habilitada la protección en tiempo real del Antivirus de Windows Defender.
- **Compilaciones válidas del sistema operativo**.  Especifique los requisitos mínimos y máximos de compilación de sistemas operativos.  

Utilice el Asistente para crear directivas de cumplimiento para configurar estas directivas y seleccionar estas nuevas opciones al agregar una regla a la directiva que va a configurar.  
Aprenda a [crear](/sccm/mdm/deploy-use/create-compliance-policy#create-a-compliance-policy) y a [implementar](/sccm/mdm/deploy-use/create-compliance-policy#deploy-a-compliance-policy) las directivas de cumplimiento.




<!-- When we have another H2 in this topic, Add this Next Steps section back in.  -->

## <a name="next-steps"></a>Pasos siguientes
Para información sobre cómo instalar o actualizar la rama de Technical Preview, vea [Technical Preview para System Center Configuration Manager](/sccm/core/get-started/technical-preview).    