---
title: Notas de la versión
titleSuffix: Configuration Manager
description: Obtenga información sobre problemas urgentes que todavía no se han corregido en el producto o no se han tratado en un artículo de Microsoft Knowledge Base.
ms.custom: na
ms.date: 04/18/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 030947fd-f5e0-4185-8513-2397fb2ec96f
caps.latest.revision: 41
caps.handback.revision: 0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2eabcba6e56bd2a0a9977ab31610a9d747ab6207
ms.sourcegitcommit: e23350fe65ff99228274e465b24b5e163769f38f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/20/2018
---
# <a name="release-notes-for-system-center-configuration-manager"></a>Notas de la versión de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Con Configuration Manager, las notas de la versión del producto se limitan a cuestiones urgentes. Estos problemas todavía no se han corregido en el producto o no se han tratado en detalle en un artículo de Microsoft Knowledge Base.  

La documentación específica de características incluye información acerca de los problemas conocidos que afectan a escenarios básicos.  

> [!TIP]  
>  Este tema contiene notas de la versión de la rama actual de Configuration Manager. Para obtener información sobre la rama de Technical Preview, vea [Technical Preview para System Center Configuration Manager](../../../../core/get-started/technical-preview.md).  

Para obtener información sobre las características que presentan las distintas versiones, consulte los siguientes artículos:
- [Novedades de la versión 1802](/sccm/core/plan-design/changes/whats-new-in-version-1802)
- [Novedades de la versión 1710](/sccm/core/plan-design/changes/whats-new-in-version-1710)
- [Novedades de la versión 1706](/sccm/core/plan-design/changes/whats-new-in-version-1706)  



## <a name="setup-and-upgrade"></a>Instalación y actualización  


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



<!-- ## Backup and recovery  -->


## <a name="client-deployment-and-upgrade"></a>Actualizaciones e implementaciones de cliente

### <a name="azure-ad-enabled-clients-cant-communicate-with-management-point"></a>Los clientes habilitados para Azure AD no se pueden comunicar con el punto de administración
<!--501089-->
*Se aplica a: Configuration Manager, versión 1706*
<!--also fixed in 1710 HFRU-->
En el escenario [Instalación y asignación de clientes Windows 10 para Configuration Manager mediante la autenticación basada en Azure AD](/sccm/core/clients/deploy/deploy-clients-cmg-azure), se produce un error en la comunicación de cliente cuando el punto de administración habilitado para HTTPS usa credenciales de base de datos alternativas. 

#### <a name="workaround"></a>Solución alternativa
Solucione este problema con una de las acciones siguientes:
- Actualice el sitio a la última versión y aplique la revisión más reciente.
- Cambie las credenciales que usa el punto de administración.


<!-- ## Operating system deployment  -->



## <a name="software-updates"></a>Actualizaciones de software

### <a name="servicing-plans-create-many-duplicate-software-update-groups-and-deployments-by-default"></a>Los planes de mantenimiento crean de forma predeterminada muchos grupos de actualizaciones e muchas implementaciones de software duplicadas  
<!-- 474326 -->
De forma predeterminada, el asistente para Crear un plan de mantenimiento se ejecuta actualmente después de cada sincronización de actualizaciones de software. Cada vez que se ejecuta el asistente, se crea un nuevo grupo de actualizaciones e implementaciones de software. Si tiene una programación de sincronización de actualizaciones de software que se ejecuta varias veces al día, el Asistente para crear un plan de mantenimiento crea varios grupos de actualizaciones de software e implementaciones cada día.  

#### <a name="workaround"></a>Solución alternativa
 Después de crear un plan de mantenimiento, abra las propiedades, vaya a la pestaña **Programación de evaluación**, seleccione **Ejecutar la regla en una programación**, haga clic en **Personalizar** y cree una programación personalizada. Por ejemplo, puede hacer que el plan de mantenimiento se ejecute cada 60 días.  


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

### <a name="you-can-no-longer-deploy-windows-phone-81-vpn-profiles-to-windows-10"></a>Ya no se pueden implementar perfiles de VPN de Windows Phone 8.1 en Windows 10
<!-- 503274  -->
*Se aplica a: Configuration Manager, versión 1710*

No se puede crear un perfil de VPN mediante el flujo de trabajo de Windows Phone 8.1, lo que también se aplica a los dispositivos Windows 10. Para estos perfiles, la página Plataformas compatibles ya no se muestra en el asistente para la creación. Windows Phone 8.1 se selecciona automáticamente en el back-end. La página Plataformas compatibles está disponible en las propiedades del perfil, pero no muestra las opciones de Windows 10.

#### <a name="workaround"></a>Solución alternativa
 Use el flujo de trabajo del perfil de VPN de Windows 10 para los dispositivos Windows 10. Si esta opción no es factible para el entorno, póngase en contacto con el soporte técnico. El soporte técnico puede ayudarle a agregar los destinos de Windows 10.



<!-- ## Reports and monitoring    -->
<!-- ## Conditional access   -->
<!-- ## Endpoint Protection -->
