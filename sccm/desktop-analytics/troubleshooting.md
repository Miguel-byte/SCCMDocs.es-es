---
title: Solución de problemas de análisis de escritorio
titleSuffix: Configuration Manager
description: Detalles técnicos para ayudarle a solucionar problemas con el análisis de escritorio.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 63e08f3f-9558-4ed7-9bf3-3a185ddaac5c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: f9e13911ef7337ca4f1f9fb2291aa026c90cfee8
ms.sourcegitcommit: 72faa1266b31849ce1a23d661a1620b01e94f517
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/26/2019
ms.locfileid: "68536014"
---
# <a name="troubleshoot-desktop-analytics"></a>Solución de problemas de análisis de escritorio

Use los detalles de este artículo como ayuda para solucionar problemas de análisis de escritorio integrados con Configuration Manager.



## <a name="confirm-prerequisites"></a>Confirmar los requisitos previos

Muchos problemas comunes se deben a que faltan requisitos previos. En primer lugar, confirme las siguientes configuraciones:

- [Requisitos previos](/sccm/desktop-analytics/overview#prerequisites)  

- [Actualizaciones de componentes de Windows](/sccm/desktop-analytics/enroll-devices#update-devices)  

- [Cómo habilitar el uso compartido de datos](/sccm/desktop-analytics/enable-data-sharing), que trata los temas siguientes:  

    - Extremos de Internet a los que los clientes necesitan conectarse  

    - Autenticación de servidor proxy  

    - Niveles de datos de diagnóstico  



## <a name="monitor-connection-health"></a>Supervisión del estado de conexión

Use el panel de estado de la **conexión** en Configuration Manager para profundizar en las categorías por estado de dispositivo. En la consola de Configuration Manager, vaya al área de trabajo **biblioteca de software** , expanda el nodo servicio de **análisis de escritorio** y seleccione el panel estado de la **conexión** .  

Para obtener más información, consulte [supervisar el estado](/sccm/desktop-analytics/monitor-connection-health)de la conexión.


## <a name="log-files"></a>Archivos de registro

Para obtener más información, consulte [archivos de registro para el análisis de escritorio](/sccm/core/plan-design/hierarchy/log-files#desktop-analytics) .

A partir de Configuration Manager versión 1906, use la herramienta **DesktopAnalyticsLogsCollector. PS1** desde el directorio de instalación Configuration Manager para ayudar a solucionar problemas de análisis de escritorio. Ejecuta algunos pasos básicos de solución de problemas y recopila los registros pertinentes en un único directorio de trabajo. Para obtener más información, vea recopiladores de [registros](/sccm/desktop-analytics/log-collector).

### <a name="enable-verbose-logging"></a>Habilitar el registro detallado

1. En el punto de conexión de servicio, vaya a la siguiente clave del registro:`HKLM\Software\Microsoft\SMS\Tracing\SMS_SERVICE_CONNECTOR`  
2. Establezca el valor de **LoggingLevel** en`0`  


## <a name="bkmk_AzureADApps"></a>Aplicaciones Azure AD

El análisis de escritorio agrega las siguientes aplicaciones a su Azure AD:

- **Microservicio de Configuration Manager**: Conecta Configuration Manager con el análisis de escritorio. Esta aplicación no tiene ningún requisito de acceso.  

- **MALogAnalyticsReader**: Recupera los grupos y dispositivos de OMS creados en Log Analytics. Para obtener más información, vea [rol de aplicación MALogAnalyticsReader](#bkmk_MALogAnalyticsReader).  

Si necesita aprovisionar estas aplicaciones después de completar la instalación, vaya al panel **servicios conectados** . Seleccione **configurar usuarios y aplicaciones acceso**y aprovisione las aplicaciones.  

- **Azure ad aplicación para Configuration Manager**. Si necesita aprovisionar o solucionar problemas de conexión después de completar la instalación, consulte [creación e importación de una aplicación para Configuration Manager](#create-and-import-app-for-configuration-manager). Esta aplicación requiere **escribir datos de la colección cm** y leer los datos de la **colección cm** en la API del **servicio Configuration Manager** .  


### <a name="create-and-import-app-for-configuration-manager"></a>Creación e importación de una aplicación para Configuration Manager

Si no puede crear la aplicación de Azure AD para Configuration Manager desde el Asistente para configurar servicios de Azure, o si desea volver a usar una aplicación existente, debe crearla e importarla manualmente. Después de completar la [incorporación inicial](/sccm/desktop-analytics/set-up#initial-onboarding) en el portal de análisis de escritorio, siga estos pasos:

#### <a name="create-app-in-azure-ad"></a>Creación de una aplicación en Azure AD

1. Abra el [Azure portal](http://portal.azure.com) como usuario con permisos de *administrador global* , vaya a **Azure Active Directory**y seleccione **registros de aplicaciones**. Después, seleccione **nuevo registro**.  

2. En el panel **crear** , configure las siguientes opciones:  

    - **Nombre**: un nombre único que identifica la aplicación, por ejemplo:`Desktop-Analytics-Connection`  

    - **Tipos de cuenta admitidos**: **Cuentas solo en este directorio de la organización (contoso)**

    - **URI de redirección (opcional)** : **Web**  

    <!--     - **Sign-on URL**: this value isn't used by Configuration Manager, but required by Azure AD. Enter a unique and valid URL, for example: `https://configmgrapp`   -->
  
    Seleccione **Registrar**.  

3. Seleccione la aplicación, tenga en cuenta el identificador de la **aplicación (cliente)** y el **identificador de directorio (inquilino)** . Los valores son los GUID que se usan para configurar la conexión de Configuration Manager.  

4. En el menú **administrar** , seleccione **certificados & secretos**. Seleccione **nuevo secreto de cliente**. Escriba una **Descripción**, especifique una duración de expiración y, a continuación, seleccione **Agregar**. Copie el **valor** de la clave, que se usa para configurar la conexión de Configuration Manager.

    > [!Important]  
    > Esta es la única oportunidad para copiar el valor de clave. Si no lo copia ahora, debe crear otra clave.  
    >
    > Guarde el valor de clave en una ubicación segura.  

5. En el menú **administrar** , seleccione **permisos**de la API.  

    1. En el panel permisos de la **API** , seleccione **Agregar un permiso**.  

    2. En el panel **solicitar permisos de API** , cambie a las **API que usa mi organización**.  

    3. Busque y seleccione la API de microservicio de **Configuration Manager** .  

    4. Seleccione el grupo **permisos de aplicación** . Expanda **CmCollectionData**y seleccione los dos permisos siguientes: **Escribir datos de la colección cm** y **leer datos de la colección cm**.  

    5. Seleccione **Agregar permisos**.  

6. En el panel permisos de la **API** , seleccione conceder **consentimiento de administración..** .. Seleccione **Sí**.  


#### <a name="import-app-in-configuration-manager"></a>Importar aplicación en Configuration Manager

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Cloud Services** y haga clic en el nodo **Servicios de Azure**. Seleccione **configurar servicios de Azure** en la cinta de opciones.  

2. En la página **servicios de Azure** del Asistente para servicios de Azure, configure las siguientes opciones:  

    - Especifique un **Nombre** para el objeto en Configuration Manager.  

    - Especifique una **Descripción** opcional para ayudar a identificar el servicio.  

    - Seleccione **análisis de escritorio** en la lista de servicios disponibles.  
  
   Seleccione **Next** (Siguiente).  

3. En la página de la **aplicación** , seleccione el **entorno de Azure**adecuado. A continuación, seleccione **importar** para la aplicación Web. Configure las siguientes opciones en la ventana **importar aplicaciones** :  

    - **Nombre del inquilino de Azure ad**: Este nombre es cómo se denomina en Configuration Manager  

    - **Azure ad ID. de inquilino**: El **ID. de directorio** que ha copiado de Azure ad  

    - **Id. de cliente**: El **identificador** de la aplicación que copió de la aplicación Azure ad  

    - **Clave secreta**: El **valor** de clave que ha copiado de la aplicación Azure ad  

    - **Expiración de la clave secreta**: La misma fecha de expiración de la clave  

    - **URI de id. de aplicación**: Esta configuración debe rellenarse automáticamente con el siguiente valor:`https://cmmicrosvc.manage.microsoft.com/`  
  
   Seleccione **comprobar**y, a continuación, seleccione **Aceptar** para cerrar la ventana importar aplicaciones. Seleccione **siguiente** en la página aplicación del Asistente para servicios de Azure.  

Para continuar con el resto del asistente en la página **datos de diagnóstico** , consulte [conexión al servicio](/sccm/desktop-analytics/connect-configmgr#bkmk_connect).

#### <a name="troubleshoot-app-in-configuration-manager"></a>Solución de problemas de la aplicación en Configuration Manager

Si tiene problemas para crear o importar la aplicación, compruebe en primer lugar **SMSAdminUI. log** el error específico. A continuación, compruebe las siguientes configuraciones:

- Ha inscrito correctamente el inquilino en el servicio de análisis de escritorio. Para obtener más información, consulte [configuración de análisis de escritorio](/sccm/desktop-analytics/set-up).

- Se puede tener acceso a todos los puntos de conexión necesarios. Para obtener más información, consulte [puntos de conexión](/sccm/desktop-analytics/enable-data-sharing#endpoints).

- Asegúrese de que el usuario que inicia sesión tenga los permisos correctos. Para obtener más información, consulte [Requisitos previos](/sccm/desktop-analytics/overview#prerequisites).

- Asegúrese de que el usuario puede iniciar sesión en Azure en general. Esta acción determina si hay algún problema de autenticación general Azure AD.

- Compruebe los mensajes de estado del componente **SMS_SERVICE_CONNECTOR** con respecto al *trabajador de análisis de escritorio*.


### <a name="bkmk_MALogAnalyticsReader"></a>Rol de aplicación MALogAnalyticsReader

Al configurar el análisis de escritorio, da su consentimiento en nombre de su organización. Este consentimiento es asignar a la aplicación MALogAnalyticsReader el rol lector Log Analytics para el área de trabajo. El análisis de escritorio requiere este rol de aplicación.

Si hay un problema con este proceso durante la instalación, utilice el siguiente proceso para agregar manualmente este permiso:

1. Vaya al [Azure portal](http://portal.azure.com)y seleccione todos los **recursos**. Seleccione el área de trabajo de tipo **log Analytics**.  

2. En el menú del área de trabajo, seleccione **control de acceso (IAM)** y, a continuación, seleccione **Agregar**.  

3. En el panel **Agregar permisos** , configure las siguientes opciones:  

    - **Rol**: **Omisión**  

    - **Asignación de acceso a**: **Azure AD usuario, grupo o aplicación**  

    - **Seleccione**: **MALogAnalyticsReader**  

4. Seleccione **Guardar**.

El portal muestra una notificación de que agregó la asignación de roles.


## <a name="data-latency"></a>Latencia de datos

<!-- 3846531 -->
La primera vez que se configura el análisis de escritorio, es posible que los informes de Configuration Manager y el portal de análisis de escritorio no muestren los datos completos de inmediato. Pueden transcurrir 2-3 días para que se produzcan los siguientes pasos:

- Los dispositivos activos envían datos de diagnóstico al servicio de análisis de escritorio
- El servicio procesa los datos
- El servicio se sincroniza con el sitio de Configuration Manager

Al sincronizar las recopilaciones de dispositivos de la jerarquía de Configuration Manager con el análisis de escritorio, las colecciones pueden tardar hasta 10 minutos en aparecer en el portal de análisis de escritorio. Del mismo modo, cuando se crea un plan de implementación en análisis de escritorio, las nuevas colecciones asociadas al plan de implementación pueden tardar hasta 10 minutos en aparecer en la jerarquía de Configuration Manager. Los sitios primarios crean las colecciones y el sitio de administración central se sincroniza con el análisis de escritorio.

En el portal de análisis de escritorio, hay dos tipos de datos: Datos de **Administrador** y **datos de diagnóstico**:

- Los **datos del administrador** hacen referencia a los cambios que realice en la configuración del área de trabajo. Por ejemplo, al cambiar la decisión o la **importancia** de la **actualización** de un activo, se están cambiando los datos del administrador. Estos cambios suelen tener un efecto compuesto, ya que pueden modificar el estado de disponibilidad de un dispositivo con el recurso en cuestión instalado.

- Los **datos de diagnóstico** hacen referencia a los metadatos del sistema cargados desde dispositivos cliente a Microsoft. Estos datos potencian el análisis del escritorio. Incluye atributos como el inventario de dispositivos y la seguridad y el estado de actualización de características.

De forma predeterminada, todos los datos del portal de análisis de escritorio se actualizan de forma automática diariamente. Esta actualización incluye cambios en los datos de diagnóstico y los cambios que realice en la configuración (datos de administrador). Debe estar visible en el portal de análisis de escritorio a las 08:00 A.M. UTC cada día.

Al realizar cambios en los datos del administrador, puede desencadenar una actualización a petición de los datos del administrador en el área de trabajo. En cualquier página del portal de análisis de escritorio, abra el control flotante de moneda de datos:

![Captura de pantalla de la pestaña flotante de moneda de datos en el portal de análisis de escritorio](media/data-currency-flyout.png)

Después, seleccione **aplicar cambios**:

![Captura de pantalla del control flotante de moneda de datos expandido en el portal de análisis de escritorio](media/data-currency-flyout-expand.png)

Este proceso suele tardar entre 15-60 minutos. El tiempo depende del tamaño del área de trabajo y del ámbito de los cambios que necesitan procesos. Cuando se solicita una actualización de datos a petición, no se producen cambios en los datos de diagnóstico.  Para obtener más información, consulte las [p + f de análisis de escritorio](/sccm/desktop-analytics/faq#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal).

Si no ve los cambios actualizados dentro de los intervalos de tiempo indicados anteriormente, espere a que transcurran otras 24 horas para la próxima actualización diaria. Si ve retrasos más largos, consulte el panel de estado del servicio. Si el servicio informa de un estado correcto, póngase en contacto con el soporte técnico de Microsoft.<!-- 3896921 -->
