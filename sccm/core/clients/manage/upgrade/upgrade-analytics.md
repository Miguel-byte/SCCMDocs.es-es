---
title: Upgrade Readiness | System Center Configuration Manager
description: "Integre Upgrade Readiness con Configuration Manager. Acceda a datos de compatibilidad de actualización en su consola de administración. Seleccione dispositivos para su actualización o corrección."
keywords: 
author: brenduns
ms.author: brenduns
manager: angerobe
ms.date: 3/1/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-client
ms.assetid: 68407ab8-c205-44ed-9deb-ff5714451624
ms.translationtype: Human Translation
ms.sourcegitcommit: dcbcd57b95f304f007e92ebe2b9aeefb4b579662
ms.openlocfilehash: 986d0446209f6e7eac1b681066d1b2e2305e1975
ms.contentlocale: es-es
ms.lasthandoff: 05/17/2017


---

# <a name="integrate-upgrade-readiness-with-system-center-configuration-manager"></a>Integrar Upgrade Readiness con System Center Configuration Manager
Upgrade Readiness (antes Upgrade Analytics) le permite evaluar y analizar la preparación del dispositivo y la compatibilidad con Windows 10 para permitir unas actualizaciones más sencillas y con menos problemas. Integre Upgrade Readiness con Configuration Manager para tener acceso a los datos de compatibilidad de actualización del cliente en la consola de administración de Configuration Manager. Después, podrá seleccionar dispositivos para su actualización o corrección desde la lista de dispositivos.

Upgrade Readiness es una solución de Microsoft Operations Management Suite (OMS). Puede leer más sobre Upgrade Readiness en [Get started with Upgrade Readiness (Introducción a Upgrade Readiness)](https://technet.microsoft.com/itpro/windows/deploy/manage-windows-upgrades-with-upgrade-readiness).

## <a name="configure-clients"></a>Configurar clientes

Existen varios pasos de configuración que tiene que realizar para asegurarse de que sus clientes pueden proporcionar datos a Upgrade Readiness:

-  Configure las opciones de telemetría de cliente como se describe en [Configurar la telemetría de Windows en la organización](https://technet.microsoft.com/itpro/windows/manage/configure-windows-telemetry-in-your-organization).
-  Instale los artículos de KB que se describen en la sección *Implementar la actualización de compatibilidad y los artículos de KB relacionados* del tema [Get started with Upgrade Readiness (Introducción a Upgrade Readiness)](https://technet.microsoft.com/itpro/windows/deploy/manage-windows-upgrades-with-upgrade-readiness).

    > [!NOTE]
    > Puede descargar un script para automatizar muchas de las tareas de configuración del cliente. Vea la sección *Run the Upgrade Readiness deployment script* (Ejecutar el script de implementación de Upgrade Readiness) del tema [Get started with Upgrade Readiness (Introducción a Upgrade Readiness)](https://technet.microsoft.com/itpro/windows/deploy/manage-windows-upgrades-with-upgrade-readiness) para obtener información sobre el script.

## <a name="create-a-connection-to-upgrade-readiness"></a>Crear una conexión con Upgrade Readiness

### <a name="prerequisites"></a>Requisitos previos

- Para agregar la conexión, el entorno de Configuration Manager debe configurar primero un [punto de conexión de servicio](/sccm/core/servers/deploy/configure/about-the-service-connection-point) en un [modo en línea](https://azure.microsoft.com/en-us/documentation/articles/resource-group-create-service-principal-portal/). Al agregar la conexión en el entorno, también se instala Microsoft Monitoring Agent en el equipo que ejecuta este rol de sistema de sitio.
- Registre Configuration Manager como una herramienta de administración de "Aplicación web o API web" y obtenga el [identificador de cliente de este registro](https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/).
- Cree una clave de cliente para la herramienta de administración registrada en Azure Active Directory.
- En el Portal de administración de Azure, proporcione la aplicación web registrada con permiso de acceso a OMS, como se describe en [Concesión de permisos a Configuration Manager para acceder a OMS](https://azure.microsoft.com/en-us/documentation/articles/log-analytics-sccm/#provide-configuration-manager-with-permissions-to-oms).

    > [!IMPORTANT]
    > Al configurar el permiso para acceder a OMS, asegúrese de elegir el rol **Colaborador** y asignarle permisos al grupo de recursos de la aplicación registrada.

### <a name="create-the-connection"></a>Crear la conexión

1.  En la consola de Configuration Manager, pulse **Administración** > **Cloud Services** > **Upgrade Readiness Connector (Conector de Upgrade Readiness)** > **Create Connection to Upgrade Analytics (Crear conexión para Upgrade Analytics)** para iniciar el **Asistente para agregar una conexión a Upgrade Analytics**.
3.  En la pantalla **Azure Active Directory**, proporcione el **Inquilino**, **Id. de cliente** y **Clave secreta de cliente** y, después, seleccione **Siguiente**.
4.  En la pantalla **Upgrade Readiness**, rellene la **Suscripción de Azure**, el **Grupo de recursos de Azure** y el **Área de trabajo de Operations Management Suite** para proporcionar la configuración de la conexión.
5.  Compruebe la configuración de la conexión en la pantalla **Resumen** y luego seleccione **Siguiente**.

    > [!NOTE]
    > Debe conectar Upgrade Readiness con el sitio de nivel superior de la jerarquía. Si conecta Upgrade Readiness con un sitio primario independiente y después agrega un sitio de administración central al entorno, debe eliminar y volver a crear la conexión de OMS dentro de la nueva jerarquía.

### <a name="complete-upgrade-readiness-tasks"></a>Completar tareas de Upgrade Readiness  

Después de crear la conexión en Configuration Manager, realice estas tareas como se describe en [Get started with Upgrade Readiness (Introducción a Upgrade Readiness)](https://technet.microsoft.com/itpro/windows/deploy/manage-windows-upgrades-with-upgrade-readiness).  

1. Agregue el servicio UpgradeReadiness al área de trabajo de OMS.  
2. Genere un id. comercial.  
3. Suscríbase a Upgrade Readiness.   

## <a name="use-the-upgrade-readiness-deployment-script"></a>Usar el script de implementación de Upgrade Readiness  

Puede automatizar muchas de las tareas de Upgrade Readiness y solucionar los problemas de uso compartido de datos con el **script de implementación de Upgrade Readiness** de Microsoft.  
El script de implementación de Upgrade Readiness hace lo siguiente:  

- Establece la clave de id. comercial + la clave CommercialDataOptIn + la clave RequestAllAppraiserVersions.  
- Comprueba que los equipos de los usuarios pueden enviar datos a Microsoft.  
- Comprueba si el equipo tiene un reinicio pendiente.   
- Comprueba que esté instalada la última versión del paquete de KB 10.0.x (se necesita la versión 10.0.14913 u otras posteriores).  
- Si está habilitado, activa el modo detallado para la solución de problemas.  
- Inicia la recopilación de datos de telemetría que Microsoft necesita para evaluar la preparación de actualización de su organización.  
- Si está habilitado, muestra el progreso del script en una ventana cmd, proporcionándole visibilidad ante los problemas (acierto o error de cada paso) o escribe en el archivo de registro.  

### <a name="to-run-the-upgrade-readiness-deployment-script"></a>Para ejecutar el script de implementación de Upgrade Readiness:  

1. Descargue el [script de implementación de Upgrade Readiness](https://go.microsoft.com/fwlink/?LinkID=822966&clcid=0x409) y extraiga el archivo UpgradeReadiness.zip. Los archivos de la carpeta **Diagnósticos** son necesarios solo si planea ejecutar el script en el modo de solución de problemas.  
2. Edite estos parámetros en RunConfig.bat:  
- Almacene la ubicación de la información de registro. Ejemplo: %SystemDrive%\URDiagnostics. Puede almacenar la información de registro en un directorio local o en un recurso compartido de archivos remoto. Si el script no puede crear el archivo de registro para la ruta de acceso especificada, crea los archivos de registro en la unidad con el directorio de Windows.  
- Clave de id. comercial.  
- De manera predeterminada, el script envía información de registro a la consola y al archivo de registro. Para cambiar el comportamiento predeterminado, use una de las siguientes opciones:  
    - logMode = 0 envío de registro solo a la consola  
    - logMode = 1 envío de registro al archivo y a la consola  
    - logMode = 2 envío de registro solo al archivo  
    - Para solucionar problemas, establezca **isVerboseLogging** en **$true** para generar información de registro que pueda ayudarle a diagnosticar los problemas. De manera predeterminada, **isVerboseLogging** se establece en **$false**. Asegúrese de que la carpeta Diagnósticos está instalada en el mismo directorio que el script para usar este modo.  
    - Indique a los usuarios si necesitan reiniciar sus equipos. De manera predeterminada, esta opción está desactivada.  

3. Después de que termine de editar los parámetros en RunConfig.bat, ejecute el script como un administrador.  


## <a name="view-microsoft-upgrade-readiness-properties-in-configuration-manager"></a>Ver las propiedades de Microsoft Upgrade Readiness en Configuration Manager  

1.  En la consola de Configuration Manager, vaya a **Cloud Services** y después seleccione **Conector de OMS** para abrir la página **Propiedades de conexión de OMS**.  

2.  En esta página hay dos pestañas:
  * En la pestaña **Azure Active Directory**, se muestra el **Inquilino**, **Id. de cliente** y la **Expiración de la clave secreta de cliente** y le permite **Comprobar** si ha expirado la **Clave secreta de cliente**.
  * La pestaña **Upgrade Readiness** muestra la **Suscripción de Azure**, el **Grupo de recursos de Azure** y el **Área de trabajo de Operations Management Suite**.

## <a name="view-and-use-the-upgrade-information"></a>Ver y usar la información de actualización

Después de integrar Upgrade Readiness con Configuration Manager, puede ver el análisis de la preparación de actualización de los clientes y, después, tomar medidas al respecto.

1. En la consola de Configuration Manager, pulse **Supervisión** > **Información general** > **Upgrade Readiness**.
2. Revise los datos, que incluyen el estado de preparación de actualización y el porcentaje de dispositivos Windows que están generando informes de telemetría.
3. Puede filtrar el panel para ver los datos de los dispositivos de colecciones determinadas.
4. Puede ver los dispositivos en un estado de preparación determinado y crear una colección dinámica para estos, de manera que pueda actualizar estos dispositivos si están listos o tomar medidas para que se encuentren en un estado de preparación.

