---
titleSuffix: Configuration Manager
description: Obtenga información sobre la funcionalidad Información de administración disponible en la consola de Configuration Manager.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a79f83be-884c-48e6-94d6-ed0a68c22e2f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9ded020bd654672bb6133c9aad15478c22498ab7
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="management-insights-in-system-center-configuration-manager"></a>Información de administración en System Center Configuration Manager.

*Se aplica a: System Center Configuration Manager (Rama actual)*

La información de administración de System Center Configuration Manager proporciona información sobre el estado actual del entorno. La información se basa en el análisis de los datos de la base de datos del sitio. Esta información le ayuda a entender mejor el entorno y tomar medidas en consecuencia. Esta característica se publicó en la versión 1802 de Configuration Manager. <!--1353967-->

## <a name="review-management-insights-in-the-configuration-manager-console"></a>Revisar Información de administración en la consola de Configuration Manager 
Se necesita el permiso de **lectura del sitio** para ver las reglas.

1. Abra la consola de Configuration Manager. 
2. Vaya al nodo **Administración** y haga clic en **Información de administración**.
3. Seleccione **Toda la información**.
4. Haga doble clic en el **Nombre del grupo de información de administración** que quiera revisar. Como alternativa, resáltelo y haga clic en **Mostrar Insights** en la cinta. 
5. Hay cuatro pestañas disponibles para la revisión junto con los requisitos previos necesarios para ejecutar la regla. 
    - **Todas las reglas**: proporciona la lista completa de las reglas para el grupo de información de administración elegido.
    - **Completa**: enumera las reglas en las que no se necesita ninguna acción. 
    - **En curso**: muestra las reglas en las que algunos requisitos previos están completos, pero no todos.
    - **Acción necesaria**: se enumeran las reglas en las que es necesario realizar acciones. Haga clic con el botón derecho y seleccione **Más detalles** para recuperar los elementos específicos en los que se necesita una acción. 
    - **Requisitos previos**: si una regla necesita que los elementos se completen antes de poder ejecutarlos, aquí se mostrarán los elementos necesarios.   
    
    **Todas las reglas y requisitos previos para el grupo de servicios de nube** ![Información de administración: todas las reglas y requisitos previos para el grupo de servicios de nube](./media/Management-insights-all-cloud-rules.png)

## <a name="management-insights-reevaluation-and-logging"></a>Reevaluación y registro de la información de administración
Las reglas de información de administración vuelven a evaluar su aplicabilidad de acuerdo a una programación semanal. Se puede volver a evaluar una regla a petición si se hace clic en ella y se selecciona **Volver a evaluar**.

**Archivo de registro de reglas de información de administración**: SMS_DataEngine.log
## <a name="management-insights-groups-and-rules"></a>Reglas y grupos de información de administración
Las reglas se organizan en diferentes grupos de información de administración. Cuando se agregan reglas y grupos, se agregan a la lista siguiente:

**Aplicaciones**: información para la administración de aplicaciones.

- **Aplicaciones sin implementaciones**: enumera las aplicaciones del entorno sin implementaciones activas. Esta regla ayuda a encontrar y eliminar las aplicaciones sin usar para simplificar la lista de aplicaciones que se muestran en la consola. 

**Servicios en la nube**: ayuda a integrar con muchos servicios en la nube, lo que permite la administración moderna de los dispositivos. 
 - **Evaluar la preparación de la administración conjunta**: ayuda a comprender qué pasos son necesarios para habilitar la administración conjunta. Esta regla tiene requisitos previos. 
 - **Permitir que los dispositivos estén unidos a Azure Active Directory y sean híbridos**: los dispositivos unidos a Azure AD permiten a los usuarios iniciar sesión con sus credenciales de dominio y también asegurarse de que los dispositivos cumplen los estándares de seguridad y cumplimiento de la organización. 
 - **Modernizar la infraestructura de identidad y acceso**: el servicio en la nube de Azure AD con autenticación multifactor integrada protege los datos confidenciales y las aplicaciones locales y en la nube. 
 - **Actualizar los clientes a Windows 10, versión 1709 o superior**: Windows 10, versión 1709 o superior, mejora y moderniza la experiencia informática de los usuarios. 


**Colecciones**: información que ayuda a simplificar la administración mediante la limpieza y reconfiguración de las colecciones.
   - **Colecciones vacías**: muestra las colecciones del entorno que no tienen miembros. 

**Administración simplificada**: información que ayuda a simplificar la administración cotidiana del entorno. 
   - **Versiones de cliente obsoletas**: enumera todos los clientes cuyas versiones tienen más de dos años. 

**Centro de software**: información para administrar el Centro de software. 
   - **Dirigir a los usuarios al Centro de software en lugar de al Catálogo de aplicaciones**: compruebe si los usuarios han instalado o solicitado aplicaciones del Catálogo de aplicaciones en los últimos 14 días. La funcionalidad principal del Catálogo de aplicaciones ahora se incluye en el Centro de software. La compatibilidad con el sitio web del Catálogo de aplicaciones finaliza con la primera actualización publicada después del 1 de junio de 2018.
   - **Usar la nueva versión del Centro de software**: la versión anterior del Centro de software ya no se admite. Configure los clientes para que usen el nuevo Centro de software. Para ello, habilite la opción de cliente **Agente de equipo** >**Usar el nuevo Centro de software**.

**Windows 10**: información relacionada con la implementación y mantenimiento de Windows 10. El grupo de información de administración de Windows 10 está disponible cuando más de la mitad de los clientes ejecutan Windows 7, Windows 8 o Windows 8.1.
   - **Configurar la telemetría de Windows y la clave de id. comercial**: para usar datos de Upgrade Readiness, los dispositivos deben configurarse con una clave de id. comercial y tener habilitada la telemetría. Los dispositivos Windows 10 se deben establecer en el nivel de telemetría Mejorado (limitado) o superior.
   - **Conexión de Configuration Manager con Upgrade Readiness**: aproveche Upgrade Readiness para acelerar las implementaciones de Windows 10 antes de que Windows 7 quede fuera del soporte técnico. **Configurar la telemetría de Windows y la clave de id. comercial** es un requisito previo.

     **Reglas de información de administración de Windows 10**
    ![Información de administración: reglas para Windows 10](./media/Windows-10-insights-group.png)
    