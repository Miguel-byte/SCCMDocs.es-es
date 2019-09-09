---
title: Solución de problemas de integración de MSfB
titleSuffix: Configuration Manager
description: Proporciona sugerencias y soluciones para solucionar algunos de los problemas más comunes con Microsoft Store para la integración empresarial.
ms.date: 08/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 09929057-ecf2-4d49-aee0-709916932b14
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: e5c77e743e34cd731dec5803e0e5c1a23064f62e
ms.sourcegitcommit: b28a97e22a9a56c5ce3367c750ea2bb4d50449c3
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2019
ms.locfileid: "70243760"
---
# <a name="troubleshoot-the-microsoft-store-for-business-integration-with-configuration-manager"></a>Solución de problemas de la integración de Microsoft Store para empresas con Configuration Manager

En este artículo se proporcionan sugerencias y correcciones de solución de problemas para algunos de los principales problemas que puede tener con la integración de Microsoft Store para empresas (MSfB) con Configuration Manager.

Para obtener más información sobre el uso de la Microsoft Store para empresas con Configuration Manager, consulte [Administración de aplicaciones desde el Microsoft Store para empresas con Configuration Manager](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business).

## <a name="monitor"></a>Monitor

### <a name="component-status"></a>Estado del componente

En la consola de Configuration Manager, vaya al área de trabajo **Supervisión**, expanda **Estado del sistema** y haga clic en el nodo **Estado del componente**. Supervise el estado de los siguientes componentes:

- SMS_BUSINESS_APP_PROCESS_MANAGER
- SMS_CLOUDCONNECTION

### <a name="sync-status"></a>Estado de sincronización

En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Cloud Services** y seleccione el nodo de **Microsoft Store para Empresas**. Compruebe la columna Estado de la **última sincronización** .

### <a name="view-synchronized-apps"></a>Visualización de aplicaciones sincronizadas

En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Administración de aplicaciones** y seleccione el nodo **Información de licencia para las aplicaciones de la Tienda**.


## <a name="log-files"></a>Archivos de registro

### <a name="msfbsyncworkerlog"></a>MSfBSyncWorker. log

Este archivo de registro se encuentra en el punto de conexión de `\Logs` servicio, en en el directorio de instalación de Configuration Manager. Registra información sobre la comunicación con el servicio en la nube. Esta información incluye metadatos, iconos, paquetes y recuperación del archivo de licencia.

Para cambiar el nivel de registro, cambie `LoggingLevel` el valor `0` a en `HKLM\SOFTWARE\Microsoft\SMS\Tracing\SMS_CLOUDCONNECTION` la clave del registro. Para obtener más información, vea [configurar opciones de registro](/sccm/core/plan-design/hierarchy/about-log-files#bkmk_reg-site).

### <a name="sms_cloudconnectionlog"></a>SMS_CLOUDCONNECTION. log

Este archivo de registro se encuentra en el punto de conexión de `\Logs` servicio, en en el directorio de instalación de Configuration Manager. Si el servicio MSfBSyncWorker no se inicia o se inicia y se detiene repetidamente, revise las entradas de este archivo de registro.

> [!NOTE]
> Este archivo de registro se comparte con otras características.

### <a name="businessappprocessworkerlog"></a>BusinessAppProcessWorker. log

Este archivo de registro se encuentra en el servidor de sitio para el sitio de nivel superior de la jerarquía. Está en el `\Logs` directorio de instalación de Configuration Manager. Registra información acerca de los siguientes procesos:

- Insertar la información de metadatos sincronizada por el componente BusinessAppProcessWorker en la base de datos
- Procesar archivos en`\InstallDir\inboxes\businessappprocess.box`

### <a name="sms_business_app_process_managerlog"></a>SMS_BUSINESS_APP_PROCESS_MANAGER. log

Este archivo de registro se encuentra en el servidor de sitio para el sitio de nivel superior de la jerarquía. Está en el `\Logs` directorio de instalación de Configuration Manager. Si el servicio BusinessAppProcessWorker no se inicia o se inicia y se detiene repetidamente, revise las entradas de este archivo de registro.



## <a name="last-sync-failed"></a>Error en la última sincronización

Cuando se haya *producido un error*en el último estado de sincronización, comience revisando los siguientes [archivos de registro](#log-files) para identificar el síntoma:

- MSfBSyncWorker. log
- SMS_CLOUDCONNECTION. log

A continuación, examine una de las siguientes secciones para ver los problemas comunes:

- [Error de autorización](#bkmk_fail-symptom1)
- [La clave secreta no es válida](#bkmk_fail-symptom2)
- [Error al obtener el token de aplicación](#bkmk_fail-symptom3)
- [La ubicación del contenido no existe](#bkmk_fail-symptom4)
- [Error al hacer que la solicitud HTTP llame al método ' GET '](#bkmk_fail-symptom5)
- [No se pueden escribir más bytes en el búfer](#bkmk_fail-symptom6)

### <a name="bkmk_fail-symptom1"></a> Error de autorización

#### <a name="cause"></a>Causa

Este problema puede producirse si la aplicación configurada Azure Active Directory (Azure AD) no tiene permisos para administrar el Microsoft Store para la empresa de este inquilino.

#### <a name="workaround"></a>Solución alternativa

1. Abra el [portal de Microsoft Store para empresas](https://www.microsoft.com/business-store)e inicie sesión como administrador.
1. Vaya a **configuración**y seleccione **herramientas de administración**.
1. Si la aplicación no aparece en la lista, seleccione **Agregar una herramienta de administración**. Después, busque por nombre y seleccione la aplicación Azure AD asociada con el mismo ClientID que Configuration Manager.
1. Si el estado no se muestra **activo**, seleccione **Activar** en la sección **acción** .
1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Cloud Services** y seleccione el nodo de **Microsoft Store para Empresas**. Sincronizar con la tienda o esperar a que se produzca el siguiente intervalo de sincronización.

> [!Tip]
> Para buscar el ClientID en Configuration Manager:
>
> 1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Cloud Services** y seleccione el nodo **Inquilinos de Azure Active Directory**.
> 1. Seleccione el inquilino que usa para la integración de Microsoft Store para la empresa.
> 1. En el panel de resultados, busque la aplicación coincidente y examine la columna **ID** . de cliente.

### <a name="bkmk_fail-symptom2"></a>La clave secreta no es válida

#### <a name="cause"></a>Causa

Este problema puede producirse si la clave secreta ha expirado en la aplicación Azure AD para la configuración de Microsoft Store para empresas.

#### <a name="resolution"></a>Solución

Renueve la clave secreta de la aplicación Azure AD. Para más información, vea [Renovar clave secreta](/sccm/core/servers/deploy/configure/azure-services-wizard#bkmk_renew).

### <a name="bkmk_fail-symptom3"></a>Error al obtener el token de aplicación

#### <a name="cause"></a>Causa

Este problema puede producirse si la aplicación conectada ya no existe en Azure AD.

#### <a name="resolution"></a>Solución

Elimine y vuelva a crear la conexión al Microsoft Store para empresas.

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Cloud Services** y seleccione el nodo de **Microsoft Store para Empresas**.
1. Seleccione la conexión existente.
1. Seleccione **eliminar** en la cinta de opciones.

A continuación, vuelva a crear la conexión. Vea los siguientes artículos para más información:

- [Configuración de los Servicios de Azure](/sccm/core/servers/deploy/configure/azure-services-wizard)
- [Configuración de la sincronización de Microsoft Store para Empresas](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business#bkmk_setup)

### <a name="bkmk_fail-symptom4"></a>La ubicación del contenido no existe

#### <a name="cause"></a>Causa

Al configurar la conexión Microsoft Store para la empresa, se especifica un recurso compartido de red para almacenar el contenido sincronizado. Este problema puede producirse si este recurso compartido no existe o tiene permisos incorrectos.

Para ver la ubicación que ha configurado:

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Cloud Services** y seleccione el nodo de **Microsoft Store para Empresas**.

1. Seleccione la cuenta y abra sus **propiedades**.

1. Cambie a la pestaña **configuración** . La configuración de **Ubicación** muestra la ruta de acceso de red para almacenar el contenido de la aplicación descargado del Microsoft Store para la empresa.

#### <a name="workaround"></a>Solución alternativa

1. Si aún no existe, cree el recurso compartido.

1. Compruebe los permisos NTFS en la carpeta y los permisos en el recurso compartido de red. Conceda a la cuenta de equipo de los permisos de **lectura** y **escritura** del punto de conexión de servicio.

Si desea volver a configurar la ubicación, elimine y vuelva a crear la conexión con la nueva ubicación de contenido.

### <a name="bkmk_fail-symptom5"></a>Error al hacer que la solicitud HTTP llame al método ' GET '

#### <a name="cause"></a>Causa

Este problema puede producirse si la sincronización de aplicaciones desde el almacén tardó mucho tiempo en haber expirado la dirección URL de contenido.

#### <a name="workaround"></a>Solución alternativa

Vuelva a intentar el proceso de sincronización

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Cloud Services** y seleccione el nodo de **Microsoft Store para Empresas**.
1. Seleccione la conexión. En la cinta de opciones, seleccione **sincronizar desde Microsoft Store para empresas**.

Cada vez, debe continuar. Puede tardar varios reintentos en función de los siguientes factores:

- El número de aplicaciones sin conexión
- El tamaño de los paquetes
- Velocidad de la red

Con cada intento, debería ver el error menos veces. Si el número de errores no se reduce, hay otro problema.

### <a name="bkmk_fail-symptom6"></a>No se pueden escribir más bytes en el búfer

#### <a name="cause"></a>Causa

Este problema puede producirse si el paquete de la aplicación es mayor que 500 MB. Configuration Manager solo admite la sincronización automática de aplicaciones sin conexión con paquetes de menos de 500 MB.

#### <a name="workaround"></a>Solución alternativa

No puede sincronizar automáticamente estas aplicaciones, pero puede descargar el contenido y crear la aplicación manualmente:

1. Obtiene el identificador de la aplicación con error de la línea siguiente en **MSfBSynWorker. log**:

    `Error(s) syncing or downloading application <ApplicationID> from the Microsoft Store for Business.`

1. Vaya al [portal de Microsoft Store para empresas](https://www.microsoft.com/business-store)e inicie sesión como administrador del almacén. Busque la página de esta aplicación.

    > [!Tip]
    > La dirección URL de la página es similar a la siguiente:`https://businessstore.microsoft.com/en-us/store/p/app/ApplicationID`

    1. Seleccione **sin conexión**si aún no está seleccionado. Después, seleccione **administrar**.

    1. Cree una carpeta independiente en el recurso compartido de contenido de la aplicación para todas las plataformas compatibles.

    1. Descargue el paquete en la carpeta del paquete.

    1. Descargue el archivo de licencia codificado como un `.bin` archivo en la carpeta del paquete.

    1. Descargue todos los marcos de trabajo necesarios en la carpeta del paquete.

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Administración de aplicaciones** y seleccione el nodo **Aplicaciones**.

1. [Cree una aplicación](/sccm/apps/deploy-use/create-applications)y especifique manualmente la información de la aplicación.

    1. Cree un tipo de implementación para cada plataforma admitida que descargó anteriormente.

    1. Tipo: **paquete de aplicación de Windows (\*.appx, \*.appxbundle)**

    1. Especifique el appx/appxbundle para el paquete de la aplicación real, no un paquete de dependencias necesario.

Confirme los detalles siguientes en la página de información final de la **importación** :

- **Archivo de licencia:** Especifica el `.bin` archivo. Este archivo de licencia es necesario para las aplicaciones sin conexión.
- **Dependencias de aplicaciones de Windows:** Compruebe que todas las dependencias necesarias se descargan para este paquete.


## <a name="sync-doesnt-run"></a>La sincronización no se ejecuta

En esta sección se tratan los siguientes problemas de sincronización:

- El proceso de sincronización se inicia manualmente, pero no se ejecuta
- El sitio no se sincroniza automáticamente cada día

Para empezar, revise los siguientes [archivos de registro](#log-files) para identificar el síntoma:

- BusinessAppProcessWorker. log
- SMS_BUSINESS_APP_PROCESS_MANAGER. log
- MSfBSyncWorker. log
- SMS_CLOUDCONNECTION. log

A continuación, examine una de las siguientes secciones para ver los problemas comunes:

- [La sincronización manual no se inicia](#bkmk_sync-symptom1)
- [La sincronización diaria automática no se ejecuta y el error "apagando # Worker" en SMS_BUSINESS_APP_PROCESS_MANAGER. log](#bkmk_sync-symptom2)

### <a name="bkmk_sync-symptom1"></a>La sincronización manual no se inicia

#### <a name="cause"></a>Causa

Este problema puede producirse si se inicia una sincronización inferior a 10 minutos después de la sincronización anterior. No se puede sincronizar con más frecuencia que cada 10 minutos.

#### <a name="resolution"></a>Solución

Espere al menos 10 minutos antes de iniciar otra sincronización.

### <a name="bkmk_sync-symptom2"></a>La sincronización diaria automática no se ejecuta y el error "apagando # Worker" en SMS_BUSINESS_APP_PROCESS_MANAGER. log

#### <a name="cause"></a>Causa

Este problema puede producirse si el componente SMS_BUSINESS_APP_PROCESS_MANAGER detiene el subproceso MSfBSyncWorker. El error puede especificar uno `2` o `4` más trabajos.

#### <a name="workaround"></a>Solución alternativa

Reinicie el servicio **SMS_EXECUTIVE** .

Si no puede reiniciar el servicio principal, detenga ambos componentes con trabajos de MSfB y, a continuación, inicie ambos:

1. Abra el registro de Windows en el servidor que ejecuta el punto de conexión de servicio.

1. Vaya a `HKLM\SOFTWARE\Microsoft\SMS\COMPONENTS\SMS_EXECUTIVE\Threads\SMS_CLOUDCONNECTION`

    1. Establezca la operación solicitada en **detenerse**.

    1. Actualizar para comprobar el estado actual = **detenido**.

1. Vaya a `HKLM\SOFTWARE\Microsoft\SMS\COMPONENTS\SMS_EXECUTIVE\Threads\SMS_BUSINESS_APP_PROCESS_MANAGER`

    1. Establezca la operación solicitada en **detenerse**.

    1. Actualizar para comprobar el estado actual = **detenido**.

1. En **SMS_CLOUDCONNECTION**, establezca operación solicitada en **iniciar**.

1. En **SMS_BUSINESS_APP_PROCESS_MANAGER**, establezca operación solicitada en **iniciar**.


## <a name="language-related-issues"></a>Problemas relacionados con el idioma

En esta sección se incluyen los siguientes problemas comunes:

- [No se aplican los cambios de selección de idioma](#bkmk_lang-symptom1)
- [No todos los idiomas seleccionados están presentes para toda la información de licencia](#bkmk_lang-symptom2)

### <a name="bkmk_lang-symptom1"></a>No se aplican los cambios de selección de idioma

#### <a name="cause"></a>Causa

Este problema puede producirse si la selección de idioma se almacena en caché y no se borra después de cambiar los valores de propiedad.

#### <a name="workaround"></a>Solución alternativa

Para resolver este problema, reinicie el servicio **SMS_Executive** .

### <a name="bkmk_lang-symptom2"></a>No todos los idiomas seleccionados están presentes para toda la información de licencia

#### <a name="cause"></a>Causa

Este problema puede producirse si la información de licencia de la aplicación de Microsoft Store para empresas no contiene datos localizados para el idioma especificado.

#### <a name="workaround"></a>Solución alternativa

Agregue manualmente los idiomas que faltan para las aplicaciones creadas.


## <a name="offline-applications"></a>Aplicaciones sin conexión

En esta sección se incluyen los siguientes problemas comunes:

- [No se pudo crear la aplicación sin conexión porque no se puede comprobar el contenido](#bkmk_off-symptom1)
- [No se pudo instalar la aplicación creada a partir de la información de licencia sin conexión](#bkmk_off-symptom2)

### <a name="bkmk_off-symptom1"></a>No se pudo crear la aplicación sin conexión porque no se puede comprobar el contenido

#### <a name="cause"></a>Causa

Este problema puede producirse si el contenido sincronizado para la aplicación sin conexión está dañado o modificado.

#### <a name="workaround"></a>Solución alternativa

Inicie una nueva sincronización. Cuando se complete la sincronización, debe comprobar y descargar los archivos de contenido incorrectos.

### <a name="bkmk_off-symptom2"></a>No se pudo instalar la aplicación creada a partir de la información de licencia sin conexión

#### <a name="cause"></a>Causa

Este problema puede producirse si implementa la aplicación en un cliente que ejecuta una versión de Windows 10 anterior a la versión 1511. Las aplicaciones con licencia sin conexión del Microsoft Store para empresas solo se admiten en la versión 1511 y posteriores de Windows 10.

#### <a name="resolution"></a>Solución

Instale la versión más reciente de Windows 10.


## <a name="next-steps"></a>Pasos siguientes

Para obtener ayuda adicional, vea [buscar ayuda para usar Configuration Manager](/sccm/core/understand/find-help).

<!-- these videos are old...1604/1605, is there still benefit in linking to them?
- Here are also some videos to learn more about it:

  - [How to set up the required prerequisites in AAD and the Microsoft Store for Business portal](https://www.youtube.com/watch?v=fC1AQY42flQ)
  - [Choose languages to sync and create apps from app metadata for each Microsoft Store for Business, and how to create apps from app metadata](https://www.youtube.com/watch?v=VJs-475rfaI)
 -->