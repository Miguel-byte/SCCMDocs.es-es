---
title: 'Tutorial: implementación de Office 365'
titleSuffix: Configuration Manager
description: Un tutorial sobre el uso de escritorio de análisis y Configuration Manager para implementar Office 365 en un grupo piloto.
ms.date: 04/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: tutorial
ms.assetid: 0b2b633a-91d7-4497-8c2a-1fc7aa310bb1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4d21b2b94c53390a9fcdbc1be640578060042ea9
ms.sourcegitcommit: 5ee9487c891c37916294bd34a10d04e398f111f7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2019
ms.locfileid: "59069456"
---
# <a name="tutorial-deploy-office-365-to-pilot"></a>Tutorial: Implementación piloto de Office 365

> [!Note]  
> Esta información se relaciona con un servicio en versión preliminar que puede modificarse sustancialmente antes de su lanzamiento comercial. Microsoft no ofrece ninguna garantía, expresa o implícita, con respecto a la información aquí proporcionada.  

Este tutorial usa el escritorio de análisis y Configuration Manager para implementar Office 365 ProPlus en un grupo piloto. Resalta la integración del servicio de nube para ofrecer información útil para implementar la aplicación con el producto local. Use escritorio análisis para determinar los dispositivos que mejor se pone en un grupo piloto. A continuación, use Configuration Manager para obtener actual con Office.

En este tutorial, obtendrá información sobre cómo:  

> [!div class="checklist"]  
> * Configurar análisis de escritorio en el portal de Azure  
> * Conectar Configuration Manager y la configuración de dispositivos  
> * Crear un plan de implementación de análisis de escritorio para Office 365 ProPlus  
> * Implementar Office 365 ProPlus en Configuration Manager en el grupo piloto  

Si no tiene una suscripción de Azure, cree un [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de comenzar. Cuando se configuran correctamente, uso de análisis de escritorio no incurrir en ningún gasto de Azure.

Análisis de escritorio usa un *área de trabajo de Log Analytics* en su suscripción de Azure. Un área de trabajo es básicamente un contenedor que incluye información de la cuenta y la información de configuración sencilla para la cuenta. Para obtener más información, consulte [Administrar áreas de trabajo](https://docs.microsoft.com/azure/log-analytics/log-analytics-manage-access?toc=/azure/azure-monitor/toc.json).



## <a name="prerequisites"></a>Requisitos previos

Antes de empezar este tutorial, asegúrese de que tiene los siguientes requisitos previos:  

- Una suscripción activa de Azure, con **Administrador de la compañía** permisos  

- Configuration Manager, versión 1810 con Update Rollup 4488598 o posterior, con **Administrador total** rol  

- Al menos un dispositivo Windows 10 con las siguientes configuraciones:  

    - Windows 10, versión 1709 o posterior

    - La última actualización acumulativa de calidad de Windows 10  

    - Versión de cliente 1810 con paquete acumulativo de actualizaciones 4486457 o una versión posterior de Configuration Manager  

    - Una versión de Windows basada en el instalador de Office, como Office 2013  

- Aprobación de la empresa para configurar el nivel de datos de diagnóstico de Windows para **mejorado (limitado)** en los dispositivos pilotos  

    Para obtener más información, consulte [privacidad escritorio Analytics](/sccm/desktop-analytics/privacy).

- Conectividad de red del dispositivo con los siguientes puntos de conexión de internet:

    - `https://v10c.events.data.microsoft.com`  
    - `https://settings-win.data.microsoft.com`  
    - `http://adl.windows.com`  
    - `https://watson.telemetry.microsoft.com`  
    - `https://umwatsonc.events.data.microsoft.com`  
    - `https://ceuswatcab01.blob.core.windows.net`  
    - `https://ceuswatcab02.blob.core.windows.net`  
    - `https://eaus2watcab01.blob.core.windows.net`  
    - `https://eaus2watcab02.blob.core.windows.net`  
    - `https://weus2watcab01.blob.core.windows.net`  
    - `https://weus2watcab02.blob.core.windows.net`  
    - `https://www.msftncsi.com`  
    - `https://www.msftconnecttest.com`  
    - `https://kmwatsonc.events.data.microsoft.com`  
    - `https://oca.telemetry.microsoft.com`  
    - `https://login.live.com`  
    - `https://nexusrules.officeapps.live.com`  
    - `https://nexus.officeapps.live.com`  
    - `https://office.pipe.aria.microsoft.com`  
    - `https://graph.windows.net` (en función de servidor de Configuration Manager)
    - `https://fef.msua06.manage.microsoft.com` (en función de servidor de Configuration Manager)

    Para obtener más información, consulte [cómo habilitar el uso compartido para el escritorio de análisis de datos](/sccm/desktop-analytics/enable-data-sharing#endpoints).  

> [!Important]  
> Estos requisitos previos son para los fines de este tutorial. Para obtener más información sobre los requisitos previos generales para el análisis de escritorio con Configuration Manager, consulte [requisitos previos](/sccm/desktop-analytics/overview#prerequisites).  



## <a name="set-up-desktop-analytics"></a>Configuración del análisis de escritorio

Utilice este procedimiento para iniciar sesión el análisis de escritorio y configurarlo en su suscripción. Este procedimiento es un proceso único para configurar los análisis de escritorio de su organización.  

1. Abra el portal de análisis de escritorio en administración de dispositivos de Microsoft 365 como un usuario con **Administrador de la compañía** permisos. Seleccione **iniciar**.  

2. En el **acepte el contrato de servicio** página, revise el contrato de servicio y seleccione **Accept**.  

3. En el **confirmar la suscripción** página, la lista de licencias aplicables necesarias son para las características del estado de dispositivos de Windows de análisis de escritorio. Seleccione **Siguiente** para continuar.  

4. En el **dar acceso a los usuarios** página, análisis de escritorio configura previamente dos grupos de seguridad en Azure Active Directory:  

    - **Los propietarios del área de trabajo**: Crear y administrar áreas de trabajo. Estas cuentas necesitan acceso de propietario a la suscripción de Azure.  

    - **Los colaboradores del área de trabajo**: Crear y administrar planes de implementación en esta área de trabajo. No necesitan ningún acceso de Azure adicionales.  
  
   Para agregar un usuario a cualquier grupo, escriba su dirección de correo electrónico o de nombre en el **escriba la dirección de correo electrónico o nombre** sección del grupo adecuado. Cuando termine, seleccione **siguiente**.

5. En la página para **configurar el área de trabajo**:  

    - Para usar un área de trabajo para el análisis de escritorio, selecciónela y continúe con el paso siguiente.  

    - Para crear un área de trabajo para el análisis de escritorio, seleccione **Agregar área de trabajo**.  

        1. Escriba un **nombre de área de trabajo**.  

        2. Seleccione la lista desplegable para **seleccione el nombre de la suscripción de Azure para esta área de trabajo**y elija la suscripción de Azure para esta área de trabajo.  

        3. Seleccione el **región** en la lista y, a continuación, seleccione **agregar**.  

6. Seleccione un área de trabajo nueva o existente y, a continuación, seleccione **establecer como área de trabajo de análisis de escritorio**.  A continuación, seleccione **continuar** en el **confirmar y concederle acceso** cuadro de diálogo.  

7. En la nueva pestaña del explorador, elija una cuenta para que use para iniciar sesión. Seleccione la opción de **dar su consentimiento en nombre de su organización** y seleccione **Accept**.  

8. En la página a **configurar el área de trabajo**, seleccione **siguiente**.  

9. En el **últimos pasos** página, seleccione **vaya al escritorio Analytics**. El portal de Azure muestra el análisis de escritorio **inicio** página.  


### <a name="create-an-app-in-azure-ad-for-configuration-manager"></a>Crear una aplicación en Azure AD para Configuration Manager  

1. En el [portal Azure](https://portal.azure.com), vaya a **Azure Active Directory**y seleccione **registros de aplicaciones**. A continuación, seleccione **nuevo registro de aplicaciones**.  

2. En el **crear** del panel, configure las siguientes opciones:  

    - **Nombre**: un nombre único que identifica la aplicación, por ejemplo: `Desktop-Analytics-Connection`  

    - **Tipo de aplicación**: **Aplicación Web / API**  

    - **Dirección URL de inicio de sesión**: este valor no se usa Configuration Manager, pero necesario para Azure AD. Escriba una dirección URL válida y única, por ejemplo: `https://configmgrapp`  
  
    Seleccione **crear**.  

3. Seleccione la aplicación y tenga en cuenta la **Id. de aplicación**. Este valor es un GUID que se usa para configurar la conexión de Configuration Manager.  

4. Seleccione **configuración** en la aplicación y, a continuación, seleccione **claves**. En el **contraseñas** sección, especifique un **descripción de la clave**, especifique una fecha de expiración **duración**y, a continuación, seleccione **guardar**. Copia el **valor** de la clave, que se usa para configurar la conexión de Configuration Manager.

    > [!Important]  
    > Esta es la única oportunidad para copiar el valor de clave. Si no copia ahora, deberá crear otra clave.  
    >
    > Guarde el valor de clave en una ubicación segura.  

5. En la aplicación **configuración** panel, seleccione **permisos necesarios**.  

    1. En el **permisos necesarios** panel, seleccione **agregar**.  

    2. En el **agregar acceso de API** panel, **seleccionar una API**.  

    3. Busque el **Microservicio del Administrador de configuración** API. Selecciónelo y, a continuación, elija **seleccione**.  

    4. En el **habilitar acceso** del panel, seleccione los permisos de aplicación: **Escribir datos de colección CM** y **leer datos de colección CM**. A continuación, elija **seleccione**.  

    5. En el **agregar acceso de API** panel, seleccione **realiza**.  

6. En el **permisos necesarios** página, seleccione **concederlos**. Seleccione **Sí**.  

7. Copie el identificador de inquilino de Azure AD. Este valor es un GUID que se usa para configurar la conexión de Configuration Manager. Seleccione **Azure Active Directory** en el menú principal y, a continuación, seleccione **propiedades**. Copia el **Id. de directorio** valor.  



## <a name="connect-configuration-manager"></a>Conexión de Configuration Manager

Utilice este procedimiento para actualizar Configuration Manager, conexión a escritorio Analytics y configuración de dispositivos. Este procedimiento es un proceso único para asociar la jerarquía para el servicio en la nube.  


### <a name="update-configuration-manager"></a>Actualizar Configuration Manager

Instale la versión de Configuration Manager 1810 acumulativo (4486457) para admitir la integración con análisis de escritorio. Para obtener más información sobre esta actualización, consulte [acumulativo de actualizaciones de la rama actual de Configuration Manager, versión 1810](https://support.microsoft.com/help/4486457).

1. Actualice el sitio con el paquete acumulativo de actualizaciones para la versión 1810. Para más información, vea [Instalar actualizaciones en consola para Configuration Manager](/sccm/core/servers/manage/install-in-console-updates).  

2. Actualice los clientes. Para simplificar el proceso, considere la posibilidad de usar la actualización automática del cliente. Para obtener más información, vea [Actualizar clientes](/sccm/core/clients/manage/upgrade/upgrade-clients#automatic-client-upgrade).  


### <a name="connect-to-the-service"></a>Conectarse al servicio

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Cloud Services** y haga clic en el nodo **Servicios de Azure**. Seleccione **configurar servicios de Azure** en la cinta de opciones.  

2. En el **Azure Services** página del Asistente para servicios de Azure, configure las siguientes opciones:  

    - Especifique un **nombre** para el objeto en Configuration Manager  

    - Especificar un elemento opcional **descripción** para ayudarle a identificar el servicio  

    - Seleccione **Desktop Analytics** en la lista de servicios disponibles  
  
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
  
   Seleccione **Siguiente**. El **funcionalidad disponible** página muestra la funcionalidad de análisis de escritorio que está disponible con la configuración de datos de diagnóstico desde la página anterior. Seleccione **Siguiente**.  

5. En el **colecciones** página, configure las opciones siguientes:  

    - **Nombre para mostrar**: El portal de análisis de escritorio muestra esta conexión de Configuration Manager con este nombre. Puede usarlo para diferenciar entre jerarquías diferentes. Por ejemplo, *laboratorio de pruebas* o *producción*.  

    - **Recopilación de destino**: Esta colección incluye todos los dispositivos de Configuration Manager se configura con el Id. comercial y la configuración de datos de diagnóstico. Es el conjunto completo de los dispositivos que Configuration Manager se conecta al servicio de análisis de escritorio.  

    - **Los dispositivos de la recopilación de destino usa un proxy de usuario autenticado para la comunicación saliente**: De forma predeterminada, este valor es **No**. Si es necesario en su entorno, se establece en **Sí**.  

    - **Seleccione las recopilaciones específicas para sincronizar con análisis de escritorio**: Seleccione **agregar** para incluir las colecciones adicionales. Estas colecciones están disponibles en el portal de análisis de escritorio para su agrupación con planes de implementación. No olvide incluir colecciones de exclusión de pruebas y pruebas.  

        Estas colecciones continuarán con la sincronización como sus cambios de pertenencia. Por ejemplo, el plan de implementación usa una colección con una regla de pertenencia a Windows 7. Como esos dispositivos se actualización a Windows 10 y Configuration Manager evalúa la pertenencia a recopilación, quitar esos dispositivos fuera de la recopilación y el plan de implementación.  

6. Complete el asistente.  

Configuration Manager crea una directiva de configuración para configurar los dispositivos en la colección de destino. Esta directiva incluye la configuración de datos de diagnóstico para habilitar dispositivos para enviar datos a Microsoft. De forma predeterminada, los clientes actualizan la directiva cada hora. Después de recibir la nueva configuración, puede ser más varias horas antes de que los datos están disponibles en análisis de escritorio.

Supervisar la configuración de los dispositivos para el análisis de escritorio. En la consola de Configuration Manager, vaya a la **biblioteca de Software** área de trabajo, expanda el **mantenimiento de Microsoft 365** nodo y seleccione el **mantenimiento de la conexión** panel.  

Configuration Manager se sincroniza todos los planes de implementación de escritorio Analytics dentro de 15 minutos después de crear la conexión. En la consola de Configuration Manager, vaya a la **biblioteca de Software** área de trabajo, expanda el **mantenimiento de Microsoft 365** nodo y seleccione el **planes de implementación** nodo.



## <a name="create-a-desktop-analytics-deployment-plan"></a>Crear un plan de implementación de análisis de escritorio

Utilice este procedimiento para crear un plan de implementación en escritorio Analytics.

1. Abra el [portal de análisis de escritorio](https://aka.ms/m365aprod). Use las credenciales que tienen al menos **colaboradores del área de trabajo** permisos.  

2. Seleccione **planes de implementación** en el grupo de administración.  

3. En el **planes de implementación** panel, seleccione **crear**.  

4. En el **Crear plan de implementación** panel, configure las siguientes opciones:  

    - **Nombre**: Planear un nombre único para la implementación, por ejemplo `Office 365 pilot`  

    - **Productos y versiones**: Seleccione el **Office** producto y la versión recomendada más reciente disponible. Por ejemplo, **clientes de Office 365, versión 1808 (recomendado)**.  

    - **Grupos de dispositivos**: Seleccione uno o más grupos y, a continuación, seleccione **establecer como destino grupos**. Grupos con **sccm** como el origen son colecciones sincronizadas desde Configuration Manager.  

    - **Las reglas de preparación**: Estas reglas ayudan a determinar qué dispositivos necesarios para actualización. Seleccione **las aplicaciones de Office** y configure las siguientes opciones:  

        - Actualización de Office 365 ProPlus de 32 bits a 64 bits. Esta configuración solo se aplica a dispositivos que ejecutan una versión de 64 bits de Windows. El valor predeterminado es **Sí**.  

        - Al actualizar desde una versión anterior de Office, deje anterior está en desuso las aplicaciones de Office. Este comportamiento se aplica incluso si esas aplicaciones no existen en la versión más reciente de Office. El valor predeterminado es **No**.  

        - Instalar bajo el umbral de recuento de los complementos de Office. El umbral predeterminado es `2%`. Complementos debajo de este umbral se establecen automáticamente en *bajo número de instalaciones*. Análisis de escritorio no validación estos complementos durante la prueba piloto. 

            Si un complemento se instala en un mayor porcentaje de equipos a este umbral, el plan de implementación marca como el complemento *Noteworthy*. A continuación, puede decidir su importancia para la prueba durante la fase piloto.  

    - **Fecha de finalización**: Elija la fecha por el que se debe implementar completamente Office en todos los dispositivos de destino.  

5. Seleccione **crear**. El nuevo plan aparece en la lista de planes de implementación mientras se está procesando. Proceso puede tardar hasta 48 horas antes de continuar con el paso siguiente.  

6. Abrir el plan de implementación, seleccione su nombre.  

7. En el menú del plan de implementación, en el **preparar** grupo, seleccione **identificar importancia**.  

    1. En el **complementos de Office** pestaña, seleccione esta opción para mostrar sólo **no revisado** activos.  

    2. Seleccione cada complemento y, a continuación, seleccione **editar**. Puede seleccionar más de una aplicación para editar al mismo tiempo.  

    3. Elija un nivel de importancia de la **importancia** lista. Si desea que el análisis de escritorio para validar el complemento durante el programa piloto, seleccione **crítico** o **importante**. No valida los complementos marcados como **importante no**. Tenga en cuenta el riesgo de compatibilidad y otra información del plan al asignar niveles de importancia.  

        Al asignar niveles de importancia, también puede elegir la decisión de actualización.  

    4. Seleccione **guardar** cuando haya terminado.  

8. En el menú del plan de implementación, en el **preparar** grupo, seleccione **identificar piloto**.  

    1. Revise los dispositivos recomendados para la prueba piloto.  

    2. Seleccione cada dispositivo y seleccione **agregar piloto**. Si no está de acuerdo con la recomendación, seleccione **reemplazar**.  

        Para obtener más información sobre cómo escritorio Analytics hace que estas recomendaciones, seleccione el icono de información en la esquina superior derecha de la **identificar piloto** panel.



## <a name="deploy-office-365-in-configuration-manager"></a>Implementación de Office 365 en Configuration Manager

Utilice este procedimiento para implementar Office 365 ProPlus en Configuration Manager en el grupo piloto.

- Si aún no tiene uno, en primer lugar [crear una aplicación para Office 365 ProPlus](#bkmk_create-app)  

- [Implementar la aplicación](#bkmk_deploy-app) con el plan de implementación de análisis de escritorio  

- [Instale la aplicación](#bkmk_install-app) desde el centro de Software en un dispositivo de destino  

<!-- 
- [Monitor](#bkmk_monitor-app) status in Configuration Manager  
 -->

### <a name="bkmk_create-app"></a> Crear una aplicación para Office 365 ProPlus

1. En la consola de Configuration Manager, vaya a la **biblioteca de Software**y seleccione el **administración de clientes de Office 365** nodo. Seleccione el **instalador de Office 365** icono en el panel.  

2. En el **configuración de la aplicación** , proporcione un **nombre** para esta aplicación. Por ejemplo, `Office 365 ProPlus`. Opcionalmente, especificar un **descripción**. Especifique el **ubicación del contenido** para los archivos de instalación y, a continuación, seleccione **siguiente**.  

3. En el **configuración Office** página, seleccione **ir a la herramienta de personalización de Office**. Configurar las opciones de implementación necesarios para la instalación de Office 365:  

    1. En el **productos y versiones** grupo, seleccione **Office 365 ProPlus** en la lista y seleccione **agregar**.  

    2. En el **lenguaje** grupo, seleccione el idioma principal.  

    3. En el **de actualización** grupo, asegúrese de que la configuración a **desinstale cualquier versión MSI de Office, incluidas Visio y Project** es **en**.  

    4. Configure las opciones adicionales según sea necesario para su organización.  

    5. Cuando haya terminado, seleccione **revisión** en la esquina superior derecha. Revise la configuración y, a continuación, seleccione **enviar**.  

4. Seleccione **Siguiente**. En el **implementación** página, seleccione **n** implementarla ahora. (El procedimiento siguiente usa el plan de implementación de análisis de escritorio para la implementación). Seleccione **siguiente** y complete el asistente.  


### <a name="bkmk_deploy-app"></a> Implementar Office 365 con el plan de implementación de análisis de escritorio

1. En la consola de Configuration Manager, vaya a la **biblioteca de Software**, expanda **Desktop Analytics mantenimiento**y seleccione el **planes de implementación** nodo.  

2. Seleccione el plan de implementación piloto de Office 365 y, a continuación, seleccione **detalles del Plan de implementación** en la cinta de opciones.  

3. En el **piloto estado** icono, elija **aplicación** desde la lista desplegable y, a continuación, seleccione **implementar**.  

4. En el **General** página del Asistente para implementar Software, seleccione **examinar** junto a la **Software** campo. Seleccione la aplicación de Office 365, por ejemplo, **Office 365 ProPlus**. Seleccione **Siguiente**.  

    > [!Note]  
    > Con la integración de análisis de escritorio, Configuration Manager crea automáticamente una colección para el plan de implementación piloto. Puede tardar hasta 10 minutos para sincronizar antes de que se puede usar esta colección.<!-- 3887891 -->
    >
    > Esta colección está reservada para los dispositivos de plan de implementación de escritorio Analytics. No se admiten los cambios manuales a esta colección.<!-- 3866460, SCCMDocs-pr 3544 -->  

5. En el **contenido** página, seleccione **agregar**y, a continuación, seleccione **punto de distribución**. Seleccione un punto de distribución disponibles para hospedar el contenido de instalación y seleccione **Aceptar**. A continuación, seleccione **Siguiente**.  

6. En el **configuración de implementación** página, seleccione **siguiente** para aceptar la configuración predeterminada. (Una instalación disponible).  

7. En el **programación** página, seleccione **siguiente** para aceptar la configuración predeterminada. (Disponible tan pronto como sea posible).  

8. En el **experiencia del usuario** página, seleccione **siguiente** para aceptar la configuración predeterminada. (Mostrar en el centro de Software y mostrar solo las notificaciones para reinicios del equipo).  

9. En el **alertas** página, seleccione **siguiente** para aceptar la configuración predeterminada.  

10. Complete el asistente.  


### <a name="bkmk_install-app"></a> Instalar Office 365 desde el centro de Software

1. Inicie sesión en un dispositivo que sea miembro del plan de implementación piloto.  

2. Abra **centro de Software** e instalar la aplicación disponible para Office 365.  


<!--
### <a name="bkmk_monitor-app"></a> Monitor status in Configuration Manager
-->


## <a name="next-steps"></a>Pasos siguientes

Avance al siguiente artículo para obtener más información sobre los planes de implementación de análisis de escritorio.
> [!div class="nextstepaction"]  
> [Planes de implementación](/sccm/desktop-analytics/about-deployment-plans)
