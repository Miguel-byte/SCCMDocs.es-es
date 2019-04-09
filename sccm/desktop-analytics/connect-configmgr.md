---
title: Conexión de Configuration Manager
titleSuffix: Configuration Manager
description: Guía de procedimientos para conectar Configuration Manager con análisis de escritorio.
ms.date: 04/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 7ed389c3-a9ab-48ce-a5eb-27d52ee4fb94
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: b30770b912e012aafa3f1d476c4791873752ecc7
ms.sourcegitcommit: 5ee9487c891c37916294bd34a10d04e398f111f7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2019
ms.locfileid: "59069354"
---
# <a name="how-to-connect-configuration-manager-with-desktop-analytics"></a>Cómo conectar Configuration Manager con análisis de escritorio

> [!Note]  
> Esta información se relaciona con un servicio en versión preliminar que puede modificarse sustancialmente antes de su lanzamiento comercial. Microsoft no ofrece ninguna garantía, expresa o implícita, con respecto a la información aquí proporcionada.  

Análisis de escritorio está estrechamente integrado con Configuration Manager. En primer lugar, asegúrese de que el sitio está actualizado para admitir las características más recientes. A continuación, cree la conexión de escritorio Analytics en Configuration Manager. Por último, supervise el estado de la conexión.


## <a name="bkmk_hotfix"></a> Actualizar el sitio

En primer lugar, asegúrese de que el sitio de Configuration Manager se está ejecutando al menos la versión 1810. Para más información, vea [Instalar actualizaciones en consola para Configuration Manager](/sccm/core/servers/manage/install-in-console-updates).

También deberá instalar la versión 1810 actualización acumulativa 2 (4488598) para admitir la integración con análisis de escritorio. Para obtener más información sobre esta actualización, consulte [actualización acumulativa 2 de la rama actual de Configuration Manager, versión 1810](https://support.microsoft.com/help/4488598).

1. Actualice el sitio con el paquete acumulativo de actualizaciones para la versión 1810. Para más información, vea [Instalar actualizaciones en consola para Configuration Manager](/sccm/core/servers/manage/install-in-console-updates).  

2. Actualice los clientes. Para simplificar el proceso, considere la posibilidad de usar la actualización automática del cliente. Para obtener más información, vea [Actualizar clientes](/sccm/core/clients/manage/upgrade/upgrade-clients#automatic-client-upgrade).  



## <a name="bkmk_connect"></a> Conectarse al servicio

Utilice este procedimiento para conectar Configuration Manager para el análisis de escritorio y configuración de dispositivos. Este procedimiento es un proceso único para asociar la jerarquía para el servicio en la nube.  

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Cloud Services** y haga clic en el nodo **Servicios de Azure**. Seleccione **configurar servicios de Azure** en la cinta de opciones.  

2. En el **Azure Services** página del Asistente para servicios de Azure, configure las siguientes opciones:  

    - Especifique un **Nombre** para el objeto en Configuration Manager.  

    - Especifique una **Descripción** opcional para ayudar a identificar el servicio.  

    - Seleccione **Desktop Analytics** en la lista de servicios disponibles.  
  
   Seleccione **Siguiente**.  

3. En el **aplicación** , seleccione la adecuada **entorno Azure**. A continuación, seleccione **importación** para la aplicación web. Configure las siguientes opciones en el **importar aplicaciones** ventana:  

    - **Nombre del inquilino de Azure AD**: Este nombre es cómo se llama en Configuration Manager  

    - **Id. de inquilino de Azure AD**: El **Id. de directorio** que copió de Azure AD  

    - **Id. de cliente**: El **Id. de aplicación** que copió desde la aplicación de Azure AD  

    - **Clave secreta**: La clave **valor** que copió desde la aplicación de Azure AD  

    - **Expiración de la clave secreta**: La misma fecha de expiración de la clave  

    - **URI de id. de aplicación**: Esta configuración se debería rellenar automáticamente con el siguiente valor: `https://cmmicrosvc.manage.microsoft.com/`  
  
   Seleccione **compruebe**y, a continuación, seleccione **Aceptar** para cerrar la ventana Importar aplicaciones. Seleccione **siguiente** en la página de aplicación del Asistente para servicios de Azure.  

4. En el **datos de diagnóstico** página, configure las opciones siguientes:  

    - **Id. comercial**: este valor se debería rellenar automáticamente con el ID de. su organización  

    - **Nivel de datos de diagnóstico de Windows 10**: seleccione al menos **mejorado (limitado)**  

    - **Permitir que el nombre del dispositivo en los datos de diagnóstico**: seleccione **habilitar**  

        > [!Note]  
        > A partir de Windows 10, versión 1803, el nombre del dispositivo no se envía a Microsoft de forma predeterminada. Si no envía el nombre del dispositivo, aparece en el escritorio de análisis como "Desconocido". Este comportamiento puede dificultar a identificar y evaluar los dispositivos.  

   Seleccione **Siguiente**. El **funcionalidad disponible** página muestra la funcionalidad de análisis de escritorio que está disponible con la configuración de datos de diagnóstico desde la página anterior. Seleccione **siguiente** para continuar o **anterior** para realizar cambios.  

    ![Página de ejemplo la funcionalidad disponible en el Asistente para servicios de Azure](media/available-functionality.png)

5. En el **colecciones** página, configure las opciones siguientes:  

    - **Nombre para mostrar**: El portal de análisis de escritorio muestra esta conexión de Configuration Manager con este nombre. Puede usarlo para diferenciar entre jerarquías diferentes. Por ejemplo, *laboratorio de pruebas* o *producción*.  

    - **Recopilación de destino**: Esta colección incluye todos los dispositivos de Configuration Manager se configura con el Id. comercial y la configuración de datos de diagnóstico. Es el conjunto completo de los dispositivos que Configuration Manager se conecta al servicio de análisis de escritorio.  

    - **Los dispositivos de la recopilación de destino usa un proxy de usuario autenticado para la comunicación saliente**: De forma predeterminada, este valor es **No**. Si es necesario en su entorno, se establece en **Sí**.  

    - **Seleccione las recopilaciones específicas para sincronizar con análisis de escritorio**: Seleccione **agregar** para incluir las colecciones adicionales. Estas colecciones están disponibles en el portal de análisis de escritorio para su agrupación con planes de implementación. No olvide incluir colecciones de exclusión de pruebas y pruebas.  

        Estas colecciones continuarán con la sincronización como sus cambios de pertenencia. Por ejemplo, el plan de implementación usa una colección con una regla de pertenencia a Windows 7. Como esos dispositivos se actualización a Windows 10 y Configuration Manager evalúa la pertenencia a recopilación, quitar esos dispositivos fuera de la recopilación y el plan de implementación.  

        > [!Important]  
        > Asegúrese de que limitar estas colecciones adicionales en la colección de destino. En las propiedades de estas colecciones adicionales, el **recopilación de restricción** debe ser la misma colección, como el análisis de escritorio **recopilación de destino**.<!-- 4097528 -->  

6. Complete el asistente.  

Configuration Manager crea una directiva de configuración para configurar los dispositivos en la colección de destino. Esta directiva incluye la configuración de datos de diagnóstico para habilitar dispositivos para enviar datos a Microsoft. De forma predeterminada, los clientes actualizan la directiva cada hora. Después de recibir la nueva configuración, puede ser más varias horas antes de que los datos están disponibles en análisis de escritorio.



## <a name="bkmk_monitor"></a> Supervisión de estado de conexión

Supervisar la configuración de los dispositivos para el análisis de escritorio. En la consola de Configuration Manager, vaya a la **biblioteca de Software** área de trabajo, expanda el **mantenimiento de Microsoft 365** nodo y seleccione el **mantenimiento de la conexión** panel.  

Para obtener más información, consulte [supervisar el estado de conexión](/sccm/desktop-analytics/troubleshooting#monitor-connection-health).

Configuration Manager se sincroniza todos los planes de implementación de escritorio Analytics dentro de 15 minutos después de crear la conexión. En la consola de Configuration Manager, vaya a la **biblioteca de Software** área de trabajo, expanda el **mantenimiento de Microsoft 365** nodo y seleccione el **planes de implementación** nodo.



## <a name="next-steps"></a>Pasos siguientes

Avance al siguiente artículo para inscribir dispositivos para el análisis de escritorio.
> [!div class="nextstepaction"]  
> [Inscripción de dispositivos](/sccm/desktop-analytics/enroll-devices)  
