---
title: Solución de problemas de análisis de escritorio
titleSuffix: Configuration Manager
description: Detalles técnicos para ayudarle a solucionar problemas relacionados con el análisis de escritorio.
ms.date: 06/28/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 63e08f3f-9558-4ed7-9bf3-3a185ddaac5c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 271803e42ba20d8d0340754b3167210414423014
ms.sourcegitcommit: d8cfd0edf2579e2b08a0ca8a0a7b8f53d1e4196f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/28/2019
ms.locfileid: "67463805"
---
# <a name="troubleshoot-desktop-analytics"></a>Solución de problemas de análisis de escritorio

Use los detalles de este artículo para ayudarle a solucionar problemas con Analytics escritorio integrado con Configuration Manager.



## <a name="confirm-prerequisites"></a>Confirme los requisitos previos

Muchos problemas comunes están provocados por los requisitos previos que faltan. En primer lugar, confirme las siguientes configuraciones:

- [Requisitos previos](/sccm/desktop-analytics/overview#prerequisites)  

- [Actualizaciones de componentes de Windows](/sccm/desktop-analytics/enroll-devices#update-devices)  

- [Cómo habilitar el uso compartido de datos](/sccm/desktop-analytics/enable-data-sharing), que tratan los temas siguientes:  

    - Puntos de conexión de Internet a la que los clientes necesitan para conectarse  

    - Autenticación del servidor proxy  

    - Niveles de datos de diagnóstico  



## <a name="monitor-connection-health"></a>Supervisión del estado de conexión

Use la **mantenimiento de la conexión** panel en Configuration Manager para profundizar en categorías por estado de dispositivos. En la consola de Configuration Manager, vaya a la **biblioteca de Software** área de trabajo, expanda el **escritorio Analytics mantenimiento** nodo y seleccione el **estado de conexión** panel.  

Para obtener más información, consulte [supervisar el estado de conexión](/sccm/desktop-analytics/monitor-connection-health).


## <a name="log-files"></a>Archivos de registro

Para obtener más información, consulte [los archivos de registro para el análisis de escritorio](/sccm/core/plan-design/hierarchy/log-files#desktop-analytics)

### <a name="enable-verbose-logging"></a>Habilitar el registro detallado

1. En el punto de conexión de servicio, vaya a la siguiente clave del registro: `HKLM\Software\Microsoft\SMS\Tracing\SMS_SERVICE_CONNECTOR`  
2. Establecer el **LoggingLevel** valor `0`  
3. (Opcional) Ejecute el siguiente comando SQL en la base de datos de sitio:  

    ```SQL
    DELETE FROM M365AProperties WHERE Name = 'M365ATenantUpdateInfo_LastUpdateTime'
    ```

4. Reinicie el **SMS_EXECUTIVE** servicio del servidor de sitio



## <a name="bkmk_AzureADApps"></a> Aplicaciones de Azure AD

Escritorio Analytics agrega las siguientes aplicaciones a Azure AD:

- **Administrador de configuración de Microservicio**: Conecta Configuration Manager con análisis de escritorio. Esta aplicación no tiene ningún requisito de acceso.  

- **MALogAnalyticsReader**: Recupera los grupos de OMS y los dispositivos creados en Log Analytics. Para obtener más información, consulte [rol de aplicación MALogAnalyticsReader](#bkmk_MALogAnalyticsReader).  

Si necesita aprovisionar estas aplicaciones después de completar la instalación, vaya a la **servicios conectados** panel. Seleccione **configurar el acceso de usuarios y aplicaciones**y el aprovisionamiento de las aplicaciones.  

- **Aplicación de Azure AD para Configuration Manager**. Si tiene que aprovisionar o solucionar problemas de conexión tras completar la instalación, consulte [crear e importar aplicación de Configuration Manager](#create-and-import-app-for-configuration-manager). Esta aplicación requiere **escribir datos de colección CM** y **leer datos de colección CM** en el **Configuration Manager Service** API.  


### <a name="create-and-import-app-for-configuration-manager"></a>Crear e importar aplicación de Configuration Manager

Después de completar la [inicial incorporación](/sccm/desktop-analytics/set-up#initial-onboarding) en el portal de análisis de escritorio, siga estos pasos para crear manualmente e importar la aplicación de Configuration Manager si no se puede crear esta aplicación de Azure AD desde configurar servicios de Azure hechicero.

#### <a name="create-app-in-azure-ad"></a>Crear la aplicación en Azure AD

1. Abra el [portal Azure](http://portal.azure.com) como un usuario con *administrador Global* permisos, vaya a **Azure Active Directory**y seleccione **registros de aplicaciones**. A continuación, seleccione **nuevo registro**.  

2. En el **crear** del panel, configure las siguientes opciones:  

    - **Nombre**: un nombre único que identifica la aplicación, por ejemplo: `Desktop-Analytics-Connection`  

    - **Tipos de cuenta admitidos**: **Cuentas en esta organización Active (Contoso)**

    - **(Opcional) del URI de redirección**: **Web**  

    <!--     - **Sign-on URL**: this value isn't used by Configuration Manager, but required by Azure AD. Enter a unique and valid URL, for example: `https://configmgrapp`   -->
  
    Seleccione **registrar**.  

3. Seleccione la aplicación, tenga en cuenta la **Id. de aplicación (cliente)** y **Id. de directorio (inquilino)** . Los valores son GUID que se usan para configurar la conexión de Configuration Manager.  

4. En el **administrar** menú, seleccione **certificados y secretos**. Seleccione **nuevo secreto de cliente**. Escriba un **descripción**, especifique una duración de expiración y, a continuación, seleccione **agregar**. Copia el **valor** de la clave, que se usa para configurar la conexión de Configuration Manager.

    > [!Important]  
    > Esta es la única oportunidad para copiar el valor de clave. Si no copia ahora, deberá crear otra clave.  
    >
    > Guarde el valor de clave en una ubicación segura.  

5. En el **administrar** menú, seleccione **permisos de API**.  

    1. En el **permisos de API** panel, seleccione **agregar un permiso**.  

    2. En el **permisos de solicitud API** panel, cambie a **API que usa mi organización**.  

    3. Busque y seleccione el **Microservice Configuration Manager** API.  

    4. Seleccione el **permisos de la aplicación** grupo. Expanda **CmCollectionData**y seleccione los permisos siguientes: **Escribir datos de colección CM** y **leer datos de colección CM**.  

    5. Seleccione **agregar permisos**.  

6. En el **permisos de API** panel, seleccione **conceder consentimiento del administrador...** . Seleccione **Sí**.  


#### <a name="import-app-in-configuration-manager"></a>Importar aplicaciones en Configuration Manager

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

Para seguir el resto del asistente en el **datos de diagnóstico** página, vea [conectar con el servicio](/sccm/desktop-analytics/connect-configmgr#bkmk_connect).

#### <a name="troubleshoot-app-in-configuration-manager"></a>Solución de problemas de aplicación en Configuration Manager

Si tiene problemas al crear o importar la aplicación, la primera comprobación **SMSAdminUI.log** del error específico. A continuación, compruebe las siguientes configuraciones:

- El inquilino para el servicio de análisis de escritorio se inscribió correctamente. Para obtener más información, consulte [cómo configurar el análisis de escritorio](/sccm/desktop-analytics/set-up).

- Todos los necesarios a los puntos de conexión son accesibles. Para obtener más información, consulte [extremos](/sccm/desktop-analytics/enable-data-sharing#endpoints).

- Asegúrese de que el usuario que inicia sesión tiene los permisos correctos. Para obtener más información, consulte [Requisitos previos](/sccm/desktop-analytics/overview#prerequisites).

- Asegúrese de que el usuario puede iniciar sesión Azure en general. Esta acción se determina si hay cualquier AD Azure general problemas de autenticación.

- Compruebe los mensajes de estado para el **SMS_SERVICE_CONNECTOR** componente referente a la *trabajo de análisis de escritorio*.


### <a name="bkmk_MALogAnalyticsReader"></a> Rol de aplicación MALogAnalyticsReader

Al configurar el análisis de escritorio, da su consentimiento en nombre de su organización. Este consentimiento consiste en asignar el rol de lector de Log Analytics para el área de trabajo de la aplicación de MALogAnalyticsReader. Este rol de aplicación es necesario por el análisis de escritorio.

Si hay un problema con este proceso durante la instalación, use el siguiente proceso para agregar manualmente este permiso:

1. Vaya a la [portal Azure](http://portal.azure.com)y seleccione **todos los recursos**. Seleccione el área de trabajo de tipo **Log Analytics**.  

2. En el menú del área de trabajo, seleccione **control de acceso (IAM)** , a continuación, seleccione **agregar**.  

3. En el **agregar permisos** del panel, configure las siguientes opciones:  

    - **Role**: **Reader**  

    - **Asignar acceso a**: **Usuario, grupo o aplicación de AD Azure**  

    - **Seleccione**: **MALogAnalyticsReader**  

4. Seleccione **Guardar**.

El portal muestra una notificación que agrega la asignación de roles.


## <a name="data-latency"></a>Latencia de datos

<!-- 3846531 -->
Cuando se configura por primera vez el análisis de escritorio, los informes de Configuration Manager y el portal de análisis de escritorio no pueden mostrar datos completos de inmediato. Puede tardar días 2 y 3 para que se produzca lo siguiente:

- Dispositivos activos envían datos de diagnóstico para el servicio de análisis de escritorio
- El servicio procesa los datos
- El servicio se sincroniza con el sitio de Configuration Manager

Al sincronizar las recopilaciones de dispositivos de su jerarquía de Configuration Manager para el análisis de escritorio, puede tardar hasta 10 minutos para las colecciones que aparezca en el portal de análisis de escritorio. De forma similar, cuando se crea un plan de implementación en escritorio Analytics, puede tardar hasta 10 minutos para las nuevas colecciones asociadas con el plan de implementación que aparezca en la jerarquía de Configuration Manager. Las colecciones de la creación de los sitios primarios y el sitio de administración central se sincroniza con el análisis de escritorio.

En el portal de análisis de escritorio, existen dos tipos de datos: **Datos del administrador** y **datos de diagnóstico**:

- **Datos del administrador** hace referencia a los cambios que realice a la configuración de área de trabajo. Por ejemplo, cuando cambia un recurso **actualizar decisión** o **importancia** está cambiando los datos de administrador. Estos cambios suelen tengan un efecto de interés, tal como puede modificar el estado de preparación de un dispositivo con el recurso en cuestión instalado.

- **Datos de diagnóstico** hace referencia a los metadatos del sistema que se cargan desde los dispositivos cliente a Microsoft. Estos datos proporciona análisis de escritorio. Incluye atributos como el inventario de dispositivos, y actualizan el estado de seguridad y la característica.

De forma predeterminada, todos los datos en el portal es automáticamente para el análisis escritorio actualizan diariamente. Esta actualización incluye cambios en los datos de diagnóstico y los cambios realizados en la configuración (datos del administrador). Debe estar visible en el portal de análisis de escritorio por 08:00 A.M. UTC cada día.

Al realizar cambios en los datos de administrador, puede desencadenar una actualización y a petición de los datos de administrador en el área de trabajo. Desde cualquier página en el portal de análisis de escritorio, abra la ventana flotante de moneda de datos:

![Captura de pantalla de la ficha de ventana flotante de moneda de datos en el portal de análisis de escritorio](media/data-currency-flyout.png)

A continuación, seleccione **aplicar cambios**:

![Captura de pantalla del control flotante de moneda datos ampliados en el portal de análisis de escritorio](media/data-currency-flyout-expand.png)

Este proceso normalmente tarda entre 15 y 60 minutos. El tiempo depende el tamaño del área de trabajo y el ámbito de los cambios que necesitan procesos. Cuando se solicita una actualización de datos y a petición, no genera ningún cambio a los datos de diagnóstico.  Para obtener más información, consulte el [preguntas más frecuentes sobre análisis de escritorio](/sccm/desktop-analytics/faq#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal).

Si no ve los cambios que se actualiza dentro de los intervalos de tiempo indicados anteriormente, otro espere 24 horas para la próxima actualización diaria. Si ve retrasos más prolongados, compruebe el panel de estado del servicio. Si el servicio notifica un estado correcto, póngase en contacto con soporte técnico de Microsoft.<!-- 3896921 -->
