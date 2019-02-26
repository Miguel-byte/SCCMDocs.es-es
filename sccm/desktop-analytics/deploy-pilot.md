---
title: Implementación piloto
titleSuffix: Configuration Manager
description: Guía de procedimientos para implementar en un grupo piloto de análisis de escritorio.
ms.date: 01/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 637fbd8e-b8ea-4c7e-95ee-a60a323c496e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 797b8ab61f5be2fd851e735c475ed610ed7d3cfe
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56755533"
---
# <a name="how-to-deploy-to-pilot-with-desktop-analytics"></a>Implementación piloto con análisis de escritorio

> [!Note]  
> Esta información se relaciona con un servicio en versión preliminar que puede modificarse sustancialmente antes de su lanzamiento comercial. Microsoft no ofrece ninguna garantía, expresa o implícita, con respecto a la información aquí proporcionada.  

Una de las ventajas del análisis de escritorio es ayudar a identificar el conjunto más pequeño de dispositivos que proporcionan la cobertura más amplia de factores. Se centra en los factores que son más importantes para una prueba piloto de actualizaciones de Windows y Office. Asegurándose de que tiene más éxito del piloto le permite mover más rápidamente y con confianza a las implementaciones amplias en producción.  

[!INCLUDE [Definition of pilot and production](includes/define-pilot-prod.md)]



## <a name="address-issues"></a>Solucionar problemas

Use el portal de análisis de escritorio para revisar cualquier problema notificado a los recursos que podrían bloquear la implementación. A continuación, aprobar, rechazar o modificar la corrección sugerida. Todos los elementos se deben marcar **listo** o **listo (con la corrección)** antes de que comience la implementación piloto. 

1. Vaya al portal de Analytics de escritorio y seleccione **planes de implementación** en el grupo de administración.  

2. Abrir un plan de implementación, seleccione su nombre.  

3. Seleccione **preparación piloto** en el grupo de preparación del menú del plan de implementación.  

4. En el **aplicaciones** pestaña, revise las aplicaciones que necesitan sus comentarios.  

5. Para cada aplicación, seleccione el nombre de la aplicación. En el panel de información, revise la recomendación y seleccione la decisión de actualización. Si elige **no revisado** o **no se puede**, a continuación, análisis de escritorio no incluye los dispositivos con esta aplicación en la implementación piloto.  

6. Repita esta revisión para otros activos.  




## <a name="create-software"></a>Creación de software

Antes de poder implementar Windows o Office, crear los objetos de software en Configuration Manager.

- [Aplicación de Office 365 ProPlus](https://docs.microsoft.com/sccm/sum/deploy-use/manage-office-365-proplus-updates#deploy-office-365-apps)  

- [Secuencia de tareas de actualización en contexto de Windows 10](https://docs.microsoft.com/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system)



## <a name="deploy-to-pilot-devices"></a>Implementar en dispositivos pilotos

Configuration Manager usa los datos de análisis de escritorio para crear una colección para la implementación piloto. No implemente la secuencia de aplicación o tarea mediante una implementación tradicional. Utilice el procedimiento siguiente para crear una implementación integrada de análisis de escritorio:

1. En la consola de Configuration Manager, vaya a la **biblioteca de Software**, expanda **Desktop Analytics mantenimiento**y seleccione el **planes de implementación** nodo.  

2. Seleccione el plan de implementación y, a continuación, seleccione **detalles del Plan de implementación** en la cinta de opciones.  

3. En el **piloto estado** icono, elija uno de los siguientes tipos de objeto en la lista desplegable:  

    - **Aplicación** para Office 365 ProPlus  

    - **Secuencia de tareas** para Windows 10  
  
   Seleccione **implementar**. Esta acción inicia al Asistente para implementar Software para el tipo de objeto seleccionado. 


Vea los siguientes artículos para más información:  

- [Implementar una aplicación](/sccm/apps/deploy-use/deploy-applications#bkmk_deploy)  

- [Implementación de una secuencia de tareas](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS)  


Si el plan de implementación es para Windows 10 y Office 365, repita este proceso para crear una segunda implementación. Por ejemplo, si es la primera implementación para la secuencia de tareas, cree una segunda implementación para la aplicación.



## <a name="monitor"></a>Monitor

### <a name="configuration-manager-console"></a>Consola de Configuration Manager

Supervisión de la misma como cualquier otra implementación de secuencia de tareas y la aplicación de la implementación de usar Configuration Manager. Vea los siguientes artículos para más información:  

- [Supervisar aplicaciones desde la consola de Configuration Manager](/sccm/apps/deploy-use/monitor-applications-from-the-console)  

- [Supervisión de implementaciones del sistema operativo](/sccm/osd/deploy-use/monitor-operating-system-deployments)  


### <a name="desktop-analytics-portal"></a>Portal de análisis de escritorio

Usar el portal de análisis de escritorio para ver el estado de cualquier plan de implementación. Seleccione el plan de implementación y, a continuación, seleccione **Introducción a los planes**. 

![Captura de pantalla de información general del plan de implementación en escritorio Analytics](media/deployment-plan-overview.png)

Seleccione el **piloto** icono. Resume el estado actual de la implementación piloto. Este icono también muestra los datos para el número de dispositivos no iniciados, en curso, completado, o al devolver los problemas.

También se enumeran los dispositivos que informan de errores u otros problemas en el área de detalles de la prueba piloto a la derecha. Para obtener detalles del problema notificado, seleccione **revisión**. Esta acción cambia la vista a la **estado de implementación** página

El **estado de implementación** página enumera los dispositivos en las siguientes categorías:

- No iniciado
- En curso
- Completado
- Necesita atención: los dispositivos
- Necesita atención - problemas

El **necesita atención** categorías muestran la misma información, pero ordenados de manera diferente.

Seleccione una lista específica en cualquiera de las vistas para obtener más detalles sobre el problema detectado.

Medida que se abordan estos problemas de implementación, el panel seguirá mostrando el progreso de los dispositivos. Actualiza como mover dispositivos de **necesita atención** a **completado**.



## <a name="next-steps"></a>Pasos siguientes

Permiten la ejecución piloto durante un período de tiempo para recopilar datos operativos. Anime a los usuarios de dispositivos pilotos para probar aplicaciones, complementos y macros. 

Cuando la implementación piloto cumple los criterios de éxito, vaya al siguiente artículo para implementar en producción.
> [!div class="nextstepaction"]  
> [Implementar en producción](/sccm/desktop-analytics/deploy-prod)  
