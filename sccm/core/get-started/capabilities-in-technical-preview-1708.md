---
title: Technical Preview 1708
titleSuffix: Configuration Manager
description: Obtenga información sobre las características disponibles en la versión 1708 de Technical Preview para System Center Configuration Manager.
ms.date: 08/25/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 3c061ceb-3bdb-4d4f-8c60-344964bd416b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 5f135ab9389ba50e12d5f4fa81c046a873a74b30
ms.sourcegitcommit: ef3fdf21180e43afd7af6c8264524711435e426e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/24/2019
ms.locfileid: "54897787"
---
# <a name="capabilities-in-technical-preview-1708-for-system-center-configuration-manager"></a>Capacidades de Technical Preview 1708 para System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Technical Preview)*

En este artículo se presentan las características disponibles en Technical Preview para System Center Configuration Manager, versión 1708. Puede instalar esta versión para actualizar y agregar nuevas capacidades al sitio de Technical Preview de Configuration Manager. Antes de instalar esta versión de Technical Preview, revise [Technical Preview para System Center Configuration Manager](../../core/get-started/technical-preview.md) para familiarizarse con los requisitos y las limitaciones generales del uso de este tipo de versiones y para saber cómo actualizar entre versiones y cómo proporcionar comentarios sobre las características de Technical Preview.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**Problemas conocidos de esta Technical Preview:**
- **Error al actualizar a la versión preliminar 1708 cuando hay un servidor de sitio en modo pasivo**. Si ejecuta la versión preliminar 1706 o 1707 y tiene un [servidor de sitio principal en modo pasivo](/sccm/core/get-started/capabilities-in-technical-preview-1706#site-server-role-high-availability), debe desinstalar el servidor de sitio en modo pasivo para poder actualizar correctamente el sitio en versión preliminar a la versión 1708. Puede volver a instalar el servidor de sitio en modo pasivo después de que el sitio ejecuta la versión 1708.

  Para desinstalar el servidor de sitio en modo pasivo:
  1. En la consola vaya a **Administración** > **General** > **Configuración de sitio** > **Servidores y roles del sistema de sitios** y seleccione el servidor de sitio en modo pasivo.
  2. En el panel **Roles del sistema de sitio**, haga clic con el botón derecho en el rol **Servidor de sitio** y después elija **Quitar rol**.
  3. Haga clic con el botón derecho en el servidor de sitio en modo pasivo y después elija **Eliminar**.
  4. Después de que el servidor de sitio se desinstala, en el servidor de sitio principal activo, reinicie el servicio **CONFIGURATION_MANAGER_UPDATE**.




**Estas son las nuevas características que puede probar con esta versión.**  

<!--  Rough Section Template
##  FEATURE

### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="improvements-for-specifying-script-parameters-when-you-deploy-powershell-scripts-from-configuration-manager"></a>Mejora para especificar parámetros de script al implementar scripts de PowerShell desde Configuration Manager
<!-- 1236459 -->

Desde Configuration Manager 1706 en adelante, puede realizar la [creación y ejecución de scripts de PowerShell desde la consola de Configuration Manager](/sccm/apps/deploy-use/create-deploy-scripts).

En la [Technical Preview 1707](/sccm/core/get-started/capabilities-in-technical-preview-1707#add-parameters-when-you-deploy-powershell-scripts-from-configuration-manager) se ha expandido esta capacidad para permitir que Configuration Manager lea parámetros del script.

En esta Technical Preview se ha expandido la capacidad de los parámetros de script de detectar qué parámetros son obligatorios y cuáles son opcionales, y le solicitará que introduzca estos.

### <a name="try-it-out"></a>Haga la prueba

1. Siga las instrucciones de [Creación y ejecución de scripts de PowerShell desde la consola de Configuration Manager](/sccm/apps/deploy-use/create-deploy-scripts).
2. En la nueva página **Parámetros de script** del **Asistente para crear scripts**, elija un parámetro y, después, edite sus valores.
El asistente muestra qué parámetros son obligatorios y cuáles son opcionales.
4. Cuando haya terminado de editar los parámetros, complete el asistente.

Cuando se ejecute la secuencia de comandos, usará los valores de parámetro que haya configurado. Si no ha configurado un parámetro obligatorio, se pedirá al usuario final que proporcione el parámetro cuando se ejecute el script.

## <a name="management-insights"></a>Información de administración
<!-- 1353967 --> Ahora puede obtener información sobre el estado actual del entorno en función del análisis de los datos de la base de datos del sitio. Esta información le ayuda a entender mejor el entorno y tomar medidas en consecuencia. Revise la información de administración en la consola de Configuration Manager en **Administración** > **Management Insights** > **All Insights** (Información de administración > Toda la información). En esta versión, ahora está disponible la siguiente información:

- **Aplicaciones sin implementaciones**: enumera las aplicaciones del entorno sin implementaciones activas. Esto le ayudará a encontrar y eliminar las aplicaciones sin usar para simplificar la lista de aplicaciones mostradas en la consola.
- **Colecciones vacías**: enumera las colecciones del entorno que no tienen miembros. Puede eliminar estas recopilaciones para simplificar la lista que se muestra al implementar los objetos, por ejemplo.


## <a name="restart-computers-from-the-configuration-manager-console"></a>Reinicio de equipos desde la consola de Configuration Manager   
<!-- 1356283 --> A partir de esta versión, puede usar la consola de Configuration Manager para identificar los dispositivos de cliente que requieren un reinicio y, después, usar una acción de notificación de cliente para reiniciarlos.

Para identificar los dispositivos que están pendiente un reinicio, vaya a **Activos y compatibilidad** > **Dispositivos** y seleccione una recopilación con dispositivos que pueden necesitar un reinicio. Después de seleccionar una recopilación, puede ver el estado de cada dispositivo en el panel de detalles en una nueva columna denominada **Reinicio pendiente**. Cada dispositivo tiene un valor de **Sí** o **No**.

Para crear la notificación de cliente para reiniciar un dispositivo:
1.  Busque el dispositivo que quiere reiniciar en el nodo Dispositivos de la consola.
2.  Haga clic con el botón derecho en el dispositivo, seleccione **Notificación de cliente** y, después, seleccione **Reiniciar**. Se abre una ventana de información sobre el reinicio. Haga clic en **Aceptar** para confirmar la solicitud de reinicio.

Cuando el cliente recibe la notificación de un **Centro de software**, se abre la ventana de notificación para informar al usuario sobre el reinicio. De forma predeterminada, el reinicio se produce al cabo de 90 minutos. Puede modificar la hora de reinicio en la [configuración de cliente](/sccm/core/clients/deploy/configure-client-settings). La configuración para el comportamiento del reinicio se encuentra en la pestaña [Reinicio de equipo](/sccm/core/clients/deploy/about-client-settings#computer-restart) de la configuración predeterminada.


### <a name="try-it-out"></a>Haga la prueba
Intente realizar las tareas siguientes y luego envíenos sus **comentarios** desde la pestaña **Inicio** de la cinta para comunicarnos si funcionó:
1.  Implemente una aplicación o actualícela en un dispositivo que requiera el reinicio de dispositivo para completar la instalación.
2.  Busque el dispositivo en el nodo **Activos y compatibilidad** > **Dispositivos** de la consola y compruebe que se muestra **Sí** en la columna **Reinicio pendiente**. Puede tardar hasta 20 minutos en que el estado Reinicio pendiente se refleje en la consola.
3.  Supervise el dispositivo para confirmar que se abre la notificación de Centro de software y que el dispositivo se reinicia correctamente.


## <a name="software-center-customization"></a>Personalización de Centro de software
<!-- 1351224 --> Puede agregar elementos de personalización de marca de empresa y especificar la visibilidad de las pestañas en el Centro de software. Puede agregar el nombre de compañía específico del Centro de software, establecer un tema de color para la configuración de Centro de software, establecer un logotipo de empresa y establecer las pestañas visibles para los dispositivos del cliente.

### <a name="customize-software-center"></a>Personalización de Centro de software

Para modificar el Centro de software:

1. En la consola de **Configuration Manager**, elija  **Administración** > **Configuración de cliente**. Haga clic en la instancia de la configuración de cliente que desea.
2. En la pestaña  **Inicio** , en el grupo  **Propiedades** , haga clic en  **Propiedades**.
3. En el cuadro de diálogo  **Configuración predeterminada** , haga clic en  **Centro de software**.
4. Seleccione **Sí** en **Select new settings to specify company information** (Seleccionar nueva configuración para especificar la información de la empresa) para habilitar la configuración de personalización del Centro de software.
5. Escriba el **nombre de la empresa**.
6. Seleccione la **combinación de colores para el Centro de software**.
7. Haga clic en **Examinar** para navegar hasta el logotipo del Centro de software. El logotipo debe ser un JPEG o PNG de 400 x 100 píxeles, con un tamaño máximo de 750 KB.
8. Seleccione **SÍ** para mostrar las pestañas en el Centro de software en los dispositivos del cliente. Debe estar visible al menos una pestaña:

    -  Habilitar pestaña Aplicaciones
    -  Habilitar pestaña Actualizaciones
    -  Habilitar pestaña Sistemas operativos
    -  Habilitar pestaña Estado de instalación
    -  Habilitar pestaña Cumplimiento de dispositivos
    -  Habilitar pestaña Opciones

### <a name="next-steps"></a>Pasos siguientes

Para más información sobre la administración de aplicaciones en Configuration Manager, consulte [Introducción a la administración de aplicaciones en System Center Configuration Manager](/sccm/apps/understand/introduction-to-application-management).
