---
title: Conexión de Configuration Manager
titleSuffix: Configuration Manager
description: Guía de procedimientos para conectar Configuration Manager con análisis de escritorio.
ms.date: 06/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 7ed389c3-a9ab-48ce-a5eb-27d52ee4fb94
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: fb16dd6e802c58f042b7eee8ae782e7118dabf1c
ms.sourcegitcommit: 659976b943226c5124057429ac7444989f98433f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2019
ms.locfileid: "67159192"
---
# <a name="how-to-connect-configuration-manager-with-desktop-analytics"></a>Cómo conectar Configuration Manager con análisis de escritorio

> [!Note]  
> Esta información se relaciona con un servicio en versión preliminar que puede modificarse sustancialmente antes de su lanzamiento comercial. Microsoft no ofrece ninguna garantía, expresa o implícita, con respecto a la información aquí proporcionada.  

Análisis de escritorio está estrechamente integrado con Configuration Manager. En primer lugar, asegúrese de que el sitio está actualizado para admitir las características más recientes. A continuación, cree la conexión de escritorio Analytics en Configuration Manager. Por último, supervise el estado de la conexión.


## <a name="bkmk_hotfix"></a> Actualizar el sitio

En primer lugar, asegúrese de que el sitio de Configuration Manager se está ejecutando al menos la versión 1902. Para más información, vea [Instalar actualizaciones en consola para Configuration Manager](/sccm/core/servers/manage/install-in-console-updates).

También deberá instalar la versión 1902 acumulativo (4500571) para admitir la integración con análisis de escritorio. Para obtener más información sobre esta actualización, consulte [acumulativo de actualizaciones de la rama actual de Configuration Manager, versión 1902](https://support.microsoft.com/help/4500571).

1. Actualice el sitio con el paquete acumulativo de actualizaciones para la versión 1902. Para más información, vea [Instalar actualizaciones en consola para Configuration Manager](/sccm/core/servers/manage/install-in-console-updates).  

2. Actualice los clientes. Para simplificar el proceso, considere la posibilidad de usar la actualización automática del cliente. Para obtener más información, vea [Actualizar clientes](/sccm/core/clients/manage/upgrade/upgrade-clients#automatic-client-upgrade).  



## <a name="bkmk_connect"></a> Conectarse al servicio

Utilice este procedimiento para conectar Configuration Manager para el análisis de escritorio y configuración de dispositivos. Este procedimiento es un proceso único para asociar la jerarquía para el servicio en la nube.  

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Cloud Services** y haga clic en el nodo **Servicios de Azure**. Seleccione **configurar servicios de Azure** en la cinta de opciones.  

    > [!Tip]  
    > En la consola de Configuration Manager, vaya a la **biblioteca de Software** área de trabajo y seleccione el **Desktop Analytics mantenimiento** nodo. En el *nuevo para el análisis de escritorio?* , seleccione el segundo vínculo a *conectar Configuration Manager para el servicio de análisis de escritorio*.  

2. En el **Azure Services** página del Asistente para servicios de Azure, configure las siguientes opciones:  

    - Especifique un **Nombre** para el objeto en Configuration Manager.  

    - Especifique una **Descripción** opcional para ayudar a identificar el servicio.  

    - Seleccione **Desktop Analytics** en la lista de servicios disponibles.  
  
   Seleccione **Siguiente**.  

3. En el **aplicación** , seleccione la adecuada **entorno Azure**. A continuación, seleccione **examinar** para la aplicación web.  

4. Si tiene una aplicación existente que desea volver a usar para este servicio, elíjalo en la lista y seleccione **Aceptar**.  

5. En la mayoría de los casos, puede crear una aplicación para la conexión de escritorio análisis con este asistente. Seleccione **crear**.<!-- 3572123 -->  

    > [!Tip]  
    > Si no se puede crear la aplicación de este asistente, puede crear manualmente la aplicación en Azure AD y, a continuación, importar a Configuration Manager. Para obtener más información, consulte [crear e importar aplicación de Configuration Manager](/sccm/desktop-analytics/troubleshooting#create-and-import-app-for-configuration-manager).  

6. Configure las siguientes opciones en el **crear aplicación de servidor** ventana:  

    - **Nombre de aplicación**: Un nombre descriptivo para la aplicación en Azure AD.

    - **Dirección URL de la página principal**: Configuration Manager no usa este valor, pero es necesario para Azure AD. De forma predeterminada, este valor es `https://ConfigMgrService`.  

    - **URI de id. de aplicación**: este valor debe ser único en el inquilino de Azure AD. En el token de acceso sirve por el cliente de Configuration Manager para solicitar acceso al servicio. De forma predeterminada, este valor es `https://ConfigMgrService`.  

    - **Período de validez de clave secreta**: elija **1 año** o **2 años** en la lista desplegable. El valor predeterminado es un año.  

    Seleccione **inicie sesión en** . Después de autenticarse correctamente en Azure, en la página se muestra el **Nombre de inquilino de Azure AD** como referencia.
        
    > [!Note]  
    > Completar este paso como una **Administrador de la compañía**. Configuration Manager no guarda estas credenciales. Este rol no requiere permisos de Configuration Manager y no tiene que ser la misma cuenta que ejecuta al Asistente para servicios de Azure.  

    Haga clic en **Aceptar** para crear la aplicación web en Azure AD y cerrar el cuadro de diálogo Crear aplicación de servidor. En el cuadro de diálogo de la aplicación de servidor, seleccione **Aceptar**. A continuación, seleccione **siguiente** en la página de aplicación del Asistente para servicios de Azure.  

7. En el **datos de diagnóstico** página, configure las opciones siguientes:  

    - **Id. comercial**: este valor se debería rellenar automáticamente con el identificador de. su organización Si no, asegúrese de que el servidor proxy está configurado para permitir que todo lo necesario [extremos](/sccm/desktop-analytics/enable-data-sharing#endpoints) antes de continuar. También puede recuperar el identificador comercial manualmente desde el [portal de análisis de escritorio](/sccm/desktop-analytics/monitor-connection-health#bkmk_ViewCommercialID).  

    - **Nivel de datos de diagnóstico de Windows 10**: seleccione al menos **básica**. Consulte [niveles de datos de diagnóstico](/sccm/desktop-analytics/enable-data-sharing#diagnostic-data-levels)
  
    - **Permitir que el nombre del dispositivo en los datos de diagnóstico**: seleccione **habilitar**  

        > [!Note]  
        > A partir de Windows 10, versión 1803, el nombre del dispositivo no se envía a Microsoft de forma predeterminada. Si no envía el nombre del dispositivo, aparece en el escritorio de análisis como "Desconocido". Este comportamiento puede dificultar a identificar y evaluar los dispositivos.  

   Seleccione **Siguiente**. El **funcionalidad disponible** página muestra la funcionalidad de análisis de escritorio que está disponible con la configuración de datos de diagnóstico desde la página anterior. Seleccione **siguiente** para continuar o **anterior** para realizar cambios.  

    ![Página de ejemplo la funcionalidad disponible en el Asistente para servicios de Azure](media/available-functionality.png)

8. En el **colecciones** página, configure las opciones siguientes:  

    - **Nombre para mostrar**: El portal de análisis de escritorio muestra esta conexión de Configuration Manager con este nombre. Puede usarlo para diferenciar entre jerarquías diferentes. Por ejemplo, *laboratorio de pruebas* o *producción*.  

    - **Recopilación de destino**: Esta colección incluye todos los dispositivos de Configuration Manager se configura con el Id. comercial y la configuración de datos de diagnóstico. Es el conjunto completo de los dispositivos que Configuration Manager se conecta al servicio de análisis de escritorio.  

    - **Los dispositivos de la recopilación de destino usa un proxy de usuario autenticado para la comunicación saliente**: De forma predeterminada, este valor es **No**. Si es necesario en su entorno, se establece en **Sí**.  

    - **Seleccione las recopilaciones específicas para sincronizar con análisis de escritorio**: Seleccione **agregar** para incluir las colecciones adicionales desde su **recopilación de destino** jerarquía. Estas colecciones están disponibles en el portal de análisis de escritorio para su agrupación con planes de implementación. No olvide incluir colecciones de exclusión de pruebas y pruebas.  <!-- 4097528 -->  

        > [!Important]  
        > Estas colecciones continuarán con la sincronización como sus cambios de pertenencia. Por ejemplo, el plan de implementación usa una colección con una regla de pertenencia a Windows 7. Como esos dispositivos se actualización a Windows 10 y Configuration Manager evalúa la pertenencia a recopilación, quitar esos dispositivos fuera de la recopilación y el plan de implementación.  


9. Complete el asistente.  

Configuration Manager crea una directiva de configuración para configurar los dispositivos en la colección de destino. Esta directiva incluye la configuración de datos de diagnóstico para habilitar dispositivos para enviar datos a Microsoft. De forma predeterminada, los clientes actualizan la directiva cada hora. Después de recibir la nueva configuración, puede ser más varias horas antes de que los datos están disponibles en análisis de escritorio.



## <a name="bkmk_monitor"></a> Supervisión de estado de conexión

Supervisar la configuración de los dispositivos para el análisis de escritorio. En la consola de Configuration Manager, vaya a la **biblioteca de Software** área de trabajo, expanda el **escritorio Analytics mantenimiento** nodo y seleccione el **estado de conexión** panel.  

Para obtener más información, consulte [supervisar el estado de conexión](/sccm/desktop-analytics/troubleshooting#monitor-connection-health).

Configuration Manager sincroniza las colecciones dentro de 60 minutos después de crear la conexión. En el portal de análisis de escritorio, vaya a **piloto Global**y ver las colecciones de dispositivos de Configuration Manager.



## <a name="next-steps"></a>Pasos siguientes

Avance al siguiente artículo para inscribir dispositivos para el análisis de escritorio.
> [!div class="nextstepaction"]  
> [Inscripción de dispositivos](/sccm/desktop-analytics/enroll-devices)  
