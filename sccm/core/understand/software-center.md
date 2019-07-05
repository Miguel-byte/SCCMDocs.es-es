---
title: Manual del usuario del Centro de software
titleSuffix: Configuration Manager
description: Obtenga información sobre las características y funcionalidad del Centro de software
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 06/18/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.assetid: 9e68de6e-2b33-442b-b674-a382728d9529
ms.collection: M365-identity-device-management
ms.openlocfilehash: c32f3f24f083537396c64c8f8426f8b6e6d6ee7a
ms.sourcegitcommit: 86968fc2f129e404ff8e08f91a05fa17b5c47527
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2019
ms.locfileid: "67252022"
---
# <a name="software-center-user-guide"></a>Manual del usuario del Centro de software

*Se aplica a: System Center Configuration Manager (Rama actual)*

El administrador de TI de la organización usa el Centro de software para instalar aplicaciones, actualizaciones de software y actualizar Windows. En este manual del usuario se explica la funcionalidad del Centro de software para los usuarios del equipo.

### <a name="general-notes-about-software-center-functionality"></a>Notas generales sobre la funcionalidad del Centro de software
- En este artículo se describen las características más recientes del Centro de software. Si en la organización se usa una versión más antigua, pero que todavía se admite, del Centro de software, no estarán disponibles todas las características. Para obtener más información, póngase en contacto con el administrador de TI.
- El administrador de TI puede deshabilitar algunos aspectos del Centro de software. Su experiencia concreta puede variar.
<!-- - Your IT admin may change the color of Software Center, and add your organization's logo. The images in this article show the default experience. -->



## <a name="how-to-open-software-center"></a>Cómo abrir el Centro de software

El método más sencillo de iniciar el Centro de software en un equipo Windows 10 consiste en presionar **Inicio** y escribir `Software Center`. 

Si se desplaza al menú Inicio, busque el icono **Centro de software** en el grupo **Microsoft System Center**.



## <a name="applications"></a>Aplicaciones

Haga clic en la pestaña **Aplicaciones** para buscar e instalar las aplicaciones que el administrador de TI implementa para usted o este equipo.
- **Todo**: muestra todas las aplicaciones que se pueden instalar.
- **Obligatorio**: el administrador de TI aplica estas aplicaciones. Si desinstala una de estas aplicaciones, el Centro de software vuelve a instalarla.
- **Filtros**: el administrador de TI puede crear categorías de aplicaciones. Si está disponible, haga clic en la lista desplegable para filtrar la vista solamente a las aplicaciones de una categoría específica. Haga clic en **Todas** para mostrar todas las aplicaciones.
- **Ordenar por**: permite reorganizar la lista de aplicaciones. De forma predeterminada esta lista se ordena por **Más recientes**. Las aplicaciones recientemente disponibles se muestran con una etiqueta **New** que está visible durante 7 días.
- **Buscar**: ¿todavía no encuentra lo que busca? Escriba palabras clave en el cuadro Buscar para encontrarlo.
-  **Cambiar la vista**: haga clic en los iconos para cambiar entre vista de lista y vista de mosaico. De forma predeterminada la lista de aplicaciones se muestra como mosaicos gráficos. 
    - Vista de mosaico: el administrador de TI puede personalizar los iconos. Debajo de cada icono se muestra el nombre de la aplicación, el editor y la versión. 
    - Vista de lista: en esta vista, se muestra el icono de la aplicación, el nombre, el editor, la versión y el estado. 


### <a name="install-multiple-applications"></a>Instalar varias aplicaciones 
<!-- 1357126 -->
Instale más de una aplicación a la vez en lugar de esperar a que finalice una antes de iniciar la siguiente. No sirve para todas las aplicaciones:
- La aplicación es visible para usted.
- La aplicación todavía no se descargado o instalado.
- El administrador de TI no requiere la aprobación para instalar la aplicación.

Para instalar más de una aplicación a la vez:
 1. Para entrar en modo de selección múltiple en la vista de lista, haga clic en el icono de selección múltiple. ![Icono de selección múltiple del Centro de software](media/software-center-multi-select-apps.png) en la esquina superior derecha.
 2. Seleccione dos o más aplicaciones para instalar activando la casilla situada la izquierda de las aplicaciones en la lista.
 3. Haga clic en el botón **Instalar seleccionadas**.

Las aplicaciones se instalan como de costumbre, pero ahora de forma sucesiva.




## <a name="updates"></a>Actualizaciones

Haga clic en la pestaña **Actualizaciones** para ver e instalar las actualizaciones de software que el administrador de TI implementa en este equipo.  
- **Todo**: muestra todas las actualizaciones que se pueden instalar.
- **Obligatorio**: el administrador de TI aplica estas actualizaciones.
- **Ordenar por**: permite reorganizar la lista de actualizaciones. De forma predeterminada, esta lista se ordena por **Nombre de aplicación: A a Z**.

Para instalar las actualizaciones, haga clic en **Instalar todo**.

Para instalar solo actualizaciones específicas, haga clic en el icono para entrar en modo de selección múltiple. Active las actualizaciones que se van a instalar y, después, haga clic en **Instalar seleccionadas**.



## <a name="operating-systems"></a>Sistemas operativos

Haga clic en la pestaña **Sistemas operativos** para ver e instalar las versiones de Windows que el administrador de TI implementa en este equipo.  
- **Todo**: muestra todas las versiones de Windows que se pueden instalar.
- **Obligatorio**: el administrador de TI aplica estas actualizaciones.
- **Ordenar por**: permite reorganizar la lista de actualizaciones. De forma predeterminada, esta lista se ordena por **Nombre de aplicación: A a Z**.



## <a name="installation-status"></a>Estado de la instalación

Haga clic en la pestaña **Estado de instalación** para ver el estado de las aplicaciones. Puede ver los estados siguientes:
- **Instalado**: el Centro de software ya ha instalado esta aplicación en este equipo.
- **Descargando**: el Centro de software está descargando el software para instalarlo en este equipo.
- **Error**: el Centro de software ha encontrado un error al intentar instalar el software.
- **Programado para instalar después de**: muestra la fecha y hora de la siguiente ventana de mantenimiento del dispositivo para instalar software que se publicará próximamente. El administrador de TI define las ventanas de mantenimiento.<!--1358131-->
    - Se puede ver el estado en las pestañas **Todo** y **Próximas**. 
    - Puede instalar antes de la hora de la ventana de mantenimiento haciendo clic en el botón **Instalar ahora**. 

El administrador de TI puede permitirle ver aplicaciones desde el sitio web del catálogo de aplicaciones. Para ver el sitio web, haga clic en **Abrir el sitio web del catálogo de aplicaciones** en la esquina superior derecha. <!--1358214-->

## <a name="device-compliance"></a>Cumplimiento de dispositivos

Haga clic en la pestaña **Cumplimiento de dispositivo** para ver el estado de cumplimiento de este equipo.

Haga clic en **Comprobar cumplimiento** para evaluar la configuración del dispositivo con las directivas de seguridad definidas por el administrador de TI.



## <a name="options"></a>Opciones

Haga clic en la pestaña **Opciones** para ver opciones adicionales para este equipo.

### <a name="work-information"></a>Información del trabajo

Indique el horario en el que suele trabajar. Es posible que el administrador de TI programe las instalaciones de software fuera de su horario laboral. Permita al menos cuatro horas al día para las tareas de mantenimiento del sistema. El administrador de TI puede seguir instalando aplicaciones críticas y actualizaciones de software durante el horario laboral.

   - Haga clic en las listas desplegables para seleccionar la primera y la última hora a la que usa este equipo. De forma predeterminada estos valores son de las **5 a.m.** a las **10 p.m.**

   - Active la casilla situada junto a los días de la semana en los que normalmente usa este equipo. De forma predeterminada, Centro de software solo selecciona los días laborables.  

Especifique si usa este equipo periódicamente para realizar su trabajo. El administrador podría instalar aplicaciones de manera automática o hacer que otras aplicaciones estén disponibles para los equipos principales. <!--3485366-->

   - Seleccione **Normalmente uso este equipo para realizar mi trabajo** si el equipo que usa es un equipo principal.


### <a name="power-management"></a>Administración de energía

El administrador de TI puede establecer directivas de administración de energía. Estas directivas ayudan a la organización a ahorrar electricidad cuando este equipo no está en uso. 

Para que este equipo esté exento de estas directivas, active la casilla **No aplicar la configuración de energía del departamento de TI en este equipo**. Esta opción está deshabilitada de forma predeterminada; el equipo aplica la configuración de energía. 


### <a name="computer-maintenance"></a>Mantenimiento del equipo

Especifique el modo en que el Centro de software aplica los cambios al software antes de la fecha límite.
- **Instalar o desinstalar automáticamente el software necesario y reiniciar el equipo solo fuera del horario de atención especificado**: Esta configuración está deshabilitada de manera predeterminada.
- **Suspender las actividades del Centro de software si el equipo está en modo Presentación**: Esta opción está habilitada de forma predeterminada.
- **Directiva de sincronización**: haga clic en este botón cuando se lo indique el administrador de TI. Este equipo comprueba cualquier novedad con los servidores, como aplicaciones, actualizaciones de software o sistemas operativos.

## <a name="custom-tab-in-software-center"></a>Pestaña personalizada en Centro de software
El administrador de TI podría haber agregado una pestaña adicional al Centro de software. El administrador asigna un nombre a esta ventana y lleva a un sitio web que haya especificado. Por ejemplo, podría tener una pestaña denominada "Departamento de soporte técnico" que lleva al sitio web del departamento de soporte técnico de su organización. <!--1358132-->
