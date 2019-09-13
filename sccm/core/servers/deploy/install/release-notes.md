---
title: Notas de la versión
titleSuffix: Configuration Manager
description: Obtenga información sobre problemas urgentes que todavía no se han corregido en el producto o no se han tratado en un artículo de Knowledge Base del soporte técnico de Microsoft.
ms.date: 07/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 030947fd-f5e0-4185-8513-2397fb2ec96f
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: a21fcce7d5e8db66a7e85c14c0ef4ad1050b342c
ms.sourcegitcommit: 4316bff400ffbde8404f8a2092ec17e3601b8d29
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "70738431"
---
# <a name="release-notes-for-configuration-manager"></a>Notas de la versión de Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Con Configuration Manager, las notas de la versión del producto se limitan a cuestiones urgentes. Estos problemas todavía no se han corregido en el producto o no se han tratado en detalle en un artículo de Knowledge Base del soporte técnico de Microsoft.  

La documentación específica de características incluye información acerca de los problemas conocidos que afectan a escenarios básicos.  

Este artículo contiene notas de la versión de la rama actual de Configuration Manager. Para obtener más información sobre la rama Technical Preview, vea [Technical Preview](/sccm/core/get-started/technical-preview)  

Para obtener información sobre las características que presentan las distintas versiones, consulte los siguientes artículos:

- [Novedades de la versión 1906](/sccm/core/plan-design/changes/whats-new-in-version-1906)  
- [Novedades de la versión 1902](/sccm/core/plan-design/changes/whats-new-in-version-1902)
- [Novedades de la versión 1810](/sccm/core/plan-design/changes/whats-new-in-version-1810)
- [Novedades de la versión 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806)  

> [!Tip]  
> Para obtener una notificación cuando se actualice esta página, copie y pegue la siguiente dirección URL en su lector de fuentes RSS: `https://docs.microsoft.com/api/search/rss?search=%22release+notes+-+Configuration+Manager%22&locale=en-us`


## <a name="set-up-and-upgrade"></a>Configuración y actualización  

### <a name="setup-prerequisite-warning-on-domain-functional-level-on-server-2019"></a>Configuración de la advertencia de requisitos previos en el nivel funcional del dominio en Server 2019

<!-- 4904376 -->

*Se aplica a la versión 1906*

Al instalar la actualización de la versión 1906 en un entorno con controladores de dominio que ejecutan Windows Server 2019, la comprobación de requisitos previos para el nivel funcional del dominio devuelve la siguiente advertencia:

`[Completed with warning]:Verify that the Active Directory domain functional level is Windows Server 2003 or later`

#### <a name="workaround"></a>Solución alternativa

Ignore la advertencia.

### <a name="azure-ad-user-discovery-and-collection-group-sync-dont-work-after-site-expansion"></a>La detección de usuarios de Azure AD y la sincronización del grupo de colecciones no funcionan después de la expansión del sitio

<!-- 4797313 -->
*Se aplica a la versión 1906*

Después de configurar cualquiera de las siguientes características:

- Detección de grupos de usuarios de Azure Active Directory
- Sincronización de los resultados de pertenencia a recopilaciones con grupos de Azure Active Directory

Si, a continuación, expande un sitio primario independiente a una jerarquía con un sitio de administración central, verá el siguiente error en SMS_AZUREAD_DISCOVERY_AGENT.log:

`Could not obtain application secret for tenant xxxxx. If this is after a site expansion, please run "Renew Secret Key" from admin console.`

#### <a name="workaround"></a>Solución alternativa

Renueve la clave asociada al registro de la aplicación en Azure AD. Para más información, vea [Renovar clave secreta](/sccm/core/servers/deploy/configure/azure-services-wizard#bkmk_renew).


### <a name="setup-command-line-option-joinceip-must-be-specified"></a>Se debe especificar la opción de línea de comandos JoinCEIP de la instalación

<!--510806-->
*Se aplica a: Configuration Manager, versión 1802*

A partir de la versión 1802 de Configuration Manager, la característica Programa para la mejora de la experiencia del usuario (CEIP) se ha quitado del producto. Cuando se [automatiza la instalación](/sccm/core/servers/deploy/install/command-line-options-for-setup) de un sitio nuevo desde un script de línea de comandos o un script desatendido, el programa de instalación devuelve un error de que falta un parámetro necesario.

#### <a name="workaround"></a>Solución alternativa

Aunque no tiene ningún efecto en el resultado del proceso de instalación, incluya el parámetro **JoinCEIP** en la línea de comandos de instalación.

> [!Note]  
> El parámetro EnableSQM para el [programa de instalación de la consola](/sccm/core/servers/deploy/install/install-consoles) no es necesario.

### <a name="cloud-service-manager-component-stopped-on-site-server-in-passive-mode"></a>Componente de administrador de servicio en la nube detenido en el servidor de sitio en modo pasivo

<!--VSO 2858826, SCCMDocs issue 772-->
*Se aplica a: Configuration Manager, versión 1806*

Si el [punto de conexión de servicio](/sccm/core/servers/deploy/configure/about-the-service-connection-point) se coloca con un [servidor de sitio en modo pasivo](/sccm/core/servers/deploy/configure/site-server-high-availability), la implementación y supervisión de una instancia de [Cloud Management Gateway](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway) no se inicia. El componente de administrador de servicio en la nube (SMS_CLOUD_SERVICES_MANAGER) está en estado detenido.

#### <a name="workaround"></a>Solución alternativa

Mueva el rol del punto de conexión de servicio a otro servidor.


<!-- ## Backup and recovery  -->

<!--## Client deployment and upgrade-->


## <a name="os-deployment"></a>Implementación del sistema operativo

### <a name="after-passive-site-server-is-promoted-the-default-boot-image-packages-still-have-package-source-on-the-previous-active-server"></a>Tras promover el servidor de sitio pasivo, los paquetes de imágenes de arranque predeterminadas todavía tendrán el paquete de origen en el servidor activo anterior.

<!--3453224, SCCMDocs-pr issue 3097-->
*Se aplica a: Configuration Manager, versión 1810*

Si tiene un servidor de sitio en modo pasivo (servidor B), cuando lo promueva a activo, la ubicación del contenido para las imágenes de arranque predeterminadas continuará haciendo referencia al servidor activo anterior (servidor A). Si el servidor A tiene un error de hardware, no podrá actualizar ni cambiar las imágenes de arranque predeterminadas.

#### <a name="workaround"></a>Solución alternativa

Ninguno


## <a name="software-updates"></a>Actualizaciones de software

### <a name="security-roles-are-missing-for-phased-deployments"></a>Roles de seguridad que faltan para las implementaciones por fases

<!--3479337, SCCMDocs-pr issue 3095-->
*Se aplica a: Configuration Manager, versiones 1810, 1902*

El rol de seguridad integrado **Administrador de implementaciones del sistema operativo** tiene permisos para las [implementaciones por fases](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence). En los roles siguientes faltan estos permisos:  

- **Administrador de aplicaciones**  
- **Administrador de implementación de aplicaciones**  
- **Administrador de actualizaciones de software**  

El rol **Autor de la aplicación** puede parecer que tiene algunos permisos para las implementaciones por fases, pero no debería ser capaz de crear implementaciones.

Un usuario con uno de estos roles puede iniciar el asistente Crear una implementación por fases y puede ver las implementaciones por fases para una aplicación o actualización de software. No puede completar al asistente ni realizar cambios en una implementación existente.

#### <a name="workaround"></a>Solución alternativa

Cree un rol de seguridad personalizado. Copie un rol de seguridad existente y agregue los permisos siguientes a la clase de objeto **Implementación por fases**:

- Crear  
- Eliminar  
- Modificar  
- Lectura  

Para obtener más información, vea [Crear roles de seguridad personalizados](/sccm/core/servers/deploy/configure/configure-role-based-administration#BKMK_CreateSecRole).

### <a name="changing-office-365-client-setting-doesnt-apply"></a>No se aplica la configuración cliente de cambios de Office 365

<!--511551-->
*Se aplica a: Configuration Manager, versión 1802*  

Implemente una [configuración de cliente](/sccm/core/clients/deploy/about-client-settings#enable-management-of-the-office-365-client-agent) con **Habilitar administración del Agente cliente de Office 365** configurado en `Yes`. Cambie luego esa configuración a `No` o `Not Configured`. Después de actualizar la directiva en los clientes de destino, las actualizaciones de Office 365 se siguen administrando mediante Configuration Manager.

#### <a name="workaround"></a>Solución alternativa

Cambie el valor del Registro siguiente a `0` y reinicie el **Servicio Hacer clic y ejecutar de Microsoft Office** (ClickToRunSvc):

```Registry
[HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\office\16.0\Common\officeupdate]
"OfficeMgmtCOM"=dword:00000000
```

## <a name="desktop-analytics"></a>Análisis de escritorio

### <a name="if-you-use-hardware-inventory-for-distributed-views-you-cant-onboard-to-desktop-analytics"></a>Si usa el inventario de hardware para las vistas distribuidas, no puede realizar incorporaciones al Análisis de escritorio

<!-- 4950335 -->
*Se aplica a: la versión 1902 de Configuration Manager con el paquete acumulativo de actualizaciones y a la versión 1906*

Si tiene una jerarquía y habilita los datos del sitio **Inventario de hardware** para las [vistas distribuidas](/sccm/core/plan-design/hierarchy/database-replication#bkmk_distviews) en cualquier vínculo de replicación del sitio, después de configurar la conexión del Análisis de escritorio en Configuration Manager, verá el siguiente error en M365UploadWorker.log:

`Unexpected exception 'System.Data.SqlClient.SqlException' Remote access is not supported for transaction isolation level "SNAPSHOT".:    at System.Data.SqlClient.SqlConnection.OnError(SqlException exception, Boolean breakConnection, Action'1 wrapCloseInAction)`

#### <a name="workaround"></a>Solución alternativa

Deshabilite los datos del sitio **Inventario de hardware** para las vistas distribuidas en cada vínculo de replicación del sitio.


### <a name="console-unexpectedly-closes-when-removing-collections"></a>La consola se cerra inesperadamente al quitar colecciones

<!-- 4749443 -->
*Se aplica a: Versión 1902 de Configuration Manager con el paquete acumulativo de actualizaciones*

Después de conectar el sitio a [Análisis de escritorio](/sccm/desktop-analytics/connect-configmgr), puede **seleccionar colecciones específicas para sincronizar con Análisis de escritorio**. Si quita una colección y aplica los cambios, agregar inmediatamente una colección nueva provoca una excepción no controlada. La consola se cierra inesperadamente.

#### <a name="workaround"></a>Solución alternativa

Cuando quite una colección, seleccione **Aceptar** para cerrar la ventana de propiedades. Luego, vuelva a abrir las propiedades para agregar una colección nueva en la pestaña **Desktop Analytics Connection** (Conexión de Análisis de escritorio).

### <a name="pilot-status-tile-shows-some-devices-as-undefined"></a>El icono Estado piloto muestra algunos dispositivos como "no definidos"

<!-- 4547783 -->
*Se aplica a: Versión 1902 de Configuration Manager con el paquete acumulativo de actualizaciones*

Al usar la consola de Configuration Manager para supervisar el estado de la implementación piloto, los dispositivos piloto actualizados en la versión de destino de Windows de ese plan de implementación se muestran como **no definidos** en el icono Estado piloto.  

Estos dispositivos **no definidos** están **actualizados** con la versión de destino del sistema operativo de ese plan de implementación. No es necesario realizar ninguna acción.


## <a name="mobile-device-management"></a>Administración de dispositivos móviles  

### <a name="validation-for-ios-app-link-sometimes-fails-on-valid-link"></a>A veces se produce un error de validación para el vínculo de la aplicación de iOS en un vínculo válido

*Se aplica a: Configuration Manager, versión 1810 y anteriores*

<!-- LSI 106004348 -->
Cuando se crea una nueva aplicación de tipo **Paquete de aplicación para iOS en App Store**, el validador no acepta algunas direcciones URL válidas para **Ubicación**. En concreto, la App Store de iOS no requiere un valor para la sección de nombre de la aplicación de la dirección URL. Por ejemplo, ambos de los siguientes vínculos son válidos y apuntan a la misma aplicación, pero el **Asistente para crear aplicaciones** acepta solo el primero:

- `https://itunes.apple.com/us/app/app-name/id123456789?mt=8`
- `https://itunes.apple.com/us/app//id123456789?mt=8`

#### <a name="workaround"></a>Solución alternativa

Cuando se crea una aplicación de iOS a la que le falta el nombre de la aplicación en la dirección URL, agregue cualquier valor como si fuera el nombre de la aplicación a la dirección URL. Por ejemplo:

- `https://itunes.apple.com/us/app/any-string/id123456789?mt=8`

Esta acción permite completar al asistente. La aplicación se implementa correctamente en dispositivos iOS. La cadena que agrega a la dirección URL aparece como el **Nombre** en la pestaña **Información general** del asistente. También es la etiqueta de la aplicación en el Portal de empresa.




<!-- ## Reports and monitoring    -->
<!-- ## Conditional access   -->

<!-- ## Endpoint Protection -->
