---
title: Notas de la versión
titleSuffix: Configuration Manager
description: Obtenga información sobre problemas urgentes que todavía no se han corregido en el producto o no se han tratado en un artículo de Knowledge Base del soporte técnico de Microsoft.
ms.date: 03/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 030947fd-f5e0-4185-8513-2397fb2ec96f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 33ef7020e1b9312717919a9dda8ce189c8db533c
ms.sourcegitcommit: f3dd8405018fe1043434386be15c16752c1a4a3c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/07/2019
ms.locfileid: "57558191"
---
# <a name="release-notes-for-configuration-manager"></a>Notas de la versión de Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Con Configuration Manager, las notas de la versión del producto se limitan a cuestiones urgentes. Estos problemas todavía no se han corregido en el producto o no se han tratado en detalle en un artículo de Knowledge Base del soporte técnico de Microsoft.  

La documentación específica de características incluye información acerca de los problemas conocidos que afectan a escenarios básicos.  

Este tema contiene notas de la versión de la rama actual de Configuration Manager. Para obtener más información sobre la rama Technical Preview, vea [Technical Preview](/sccm/core/get-started/technical-preview)  

Para obtener información sobre las características que presentan las distintas versiones, consulte los siguientes artículos:
- [Novedades de la versión 1810](/sccm/core/plan-design/changes/whats-new-in-version-1810)
- [Novedades de la versión 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806)  
- [Novedades de la versión 1802](/sccm/core/plan-design/changes/whats-new-in-version-1802)

> [!Tip]  
> Para obtener una notificación cuando se actualice esta página, copie y pegue la siguiente dirección URL en su lector de fuentes RSS: `https://docs.microsoft.com/api/search/rss?search=%22release+notes+-+Configuration+Manager%22&locale=en-us`



## <a name="set-up-and-upgrade"></a>Configuración y actualización  


### <a name="when-using-redistributable-files-from-the-cdlatest-folder-setup-fails-with-a-manifest-verification-error"></a>Cuando se usan archivos de redistribución de la carpeta CD.Latest, se produce un error de comprobación de manifiesto en la instalación
<!-- 510080, 490569  -->

Al ejecutar el programa de instalación desde la carpeta CD.Latest creada para la versión 1606 y usar los archivos de redistribución incluidos en esa carpeta, se produce un error en el programa de instalación y aparecen los errores siguientes en el registro de instalación de Configuration Manager:

  `ERROR: File hash check failed for defaultcategories.dll`  
  `ERROR: Manifest verification failed. Wrong version of manifest?`

#### <a name="workaround"></a>Solución alternativa
Use una de las opciones siguientes:
 - Durante la instalación, elija descargar los archivos redistribuibles más recientes de Microsoft. Utilice los archivos redistribuibles más recientes en lugar de los archivos incluidos en la carpeta CD.Latest.
 - Elimine manualmente la carpeta *cd.latest\redist\languagepack\zhh* y, luego, vuelva a ejecutar la instalación.


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
*Se aplica a: Configuration Manager, versión 1810*

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

```
[HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\office\16.0\Common\officeupdate]
"OfficeMgmtCOM"=dword:00000000
```



## <a name="mobile-device-management"></a>Administración de dispositivos móviles  

### <a name="validation-for-ios-app-link-sometimes-fails-on-valid-link"></a>A veces se produce un error de validación para el vínculo de la aplicación de iOS en un vínculo válido
<!-- LSI 106004348 --> Cuando se crea una nueva aplicación del tipo **Paquete de aplicación para iOS en App Store**, el validador no acepta algunas direcciones URL válidas para la **Ubicación**. En concreto, la App Store de iOS no requiere un valor para la sección de nombre de la aplicación de la dirección URL. Por ejemplo, ambos de los siguientes vínculos son válidos y apuntan a la misma aplicación, pero el **Asistente para crear aplicaciones** acepta solo el primero:
- `https://itunes.apple.com/us/app/app-name/id123456789?mt=8`
- `https://itunes.apple.com/us/app//id123456789?mt=8`

#### <a name="workaround"></a>Solución alternativa
Cuando se crea una aplicación de iOS a la que le falta el nombre de la aplicación en la dirección URL, agregue cualquier valor como si fuera el nombre de la aplicación a la dirección URL. Por ejemplo:
- `https://itunes.apple.com/us/app/any-string/id123456789?mt=8`

Esta acción permite completar al asistente. La aplicación se implementa correctamente en dispositivos iOS. La cadena que agrega a la dirección URL aparece como el **Nombre** en la pestaña **Información general** del asistente. También es la etiqueta de la aplicación en el Portal de empresa.


### <a name="you-can-no-longer-deploy-windows-phone-81-vpn-profiles-to-windows-10"></a>Ya no se pueden implementar perfiles de VPN de Windows Phone 8.1 en Windows 10
<!-- 503274  -->
*Se aplica a: Configuration Manager, versión 1710*

No se puede crear un perfil de VPN mediante el flujo de trabajo de Windows Phone 8.1, lo que también se aplica a los dispositivos Windows 10. Para estos perfiles, la página Plataformas compatibles ya no se muestra en el asistente para la creación. Windows Phone 8.1 se selecciona automáticamente en el back-end. La página Plataformas compatibles está disponible en las propiedades del perfil, pero no muestra las opciones de Windows 10.

#### <a name="workaround"></a>Solución alternativa
 Use el flujo de trabajo del perfil de VPN de Windows 10 para los dispositivos Windows 10. Si esta opción no es factible para el entorno, póngase en contacto con el soporte técnico. El soporte técnico puede ayudarle a agregar los destinos de Windows 10.



<!-- ## Reports and monitoring    -->
<!-- ## Conditional access   -->
<!-- ## Endpoint Protection -->
