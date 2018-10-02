---
title: Notas de la versión
titleSuffix: Configuration Manager
description: Obtenga información sobre problemas urgentes que todavía no se han corregido en el producto o no se han tratado en un artículo de Knowledge Base del soporte técnico de Microsoft.
ms.date: 08/21/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 030947fd-f5e0-4185-8513-2397fb2ec96f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 939ab4b97a1a62eeae834873dd39e2f0d435527d
ms.sourcegitcommit: 4e4b71227309bee7e9f1285971f8235c67a9c502
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/25/2018
ms.locfileid: "42590104"
---
# <a name="release-notes-for-configuration-manager"></a>Notas de la versión de Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Con Configuration Manager, las notas de la versión del producto se limitan a cuestiones urgentes. Estos problemas todavía no se han corregido en el producto o no se han tratado en detalle en un artículo de Knowledge Base del soporte técnico de Microsoft.  

La documentación específica de características incluye información acerca de los problemas conocidos que afectan a escenarios básicos.  

> [!TIP]  
>  Este tema contiene notas de la versión de la rama actual de Configuration Manager. Para obtener más información sobre la rama Technical Preview, vea [Technical Preview](/sccm/core/get-started/technical-preview)  

Para obtener información sobre las características que presentan las distintas versiones, consulte los siguientes artículos:
- [Novedades de la versión 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806)  
- [Novedades de la versión 1802](/sccm/core/plan-design/changes/whats-new-in-version-1802)
- [Novedades de la versión 1710](/sccm/core/plan-design/changes/whats-new-in-version-1710)



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


### <a name="cloud-service-manager-component-stopped-on-site-server-in-passive-mode"></a>Componente de administrador de servicio en la nube detenido en el servidor de sitio en modo pasivo
<!--VSO 2858826, SCCMDocs issue 772-->
*Se aplica a: Configuration Manager, versión 1806*

Si el [punto de conexión de servicio](/sccm/core/servers/deploy/configure/about-the-service-connection-point) coexiste con un [servidor de sitio en modo pasivo](/sccm/core/servers/deploy/configure/site-server-high-availability), la implementación y supervisión de una instancia de [Cloud Management Gateway](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway) no se inicia. El componente de administrador de servicio en la nube (SMS_CLOUD_SERVICES_MANAGER) está en estado detenido.

#### <a name="workaround"></a>Solución alternativa
Mueva el rol del punto de conexión de servicio a otro servidor.



<!-- ## Backup and recovery  -->


## <a name="client-deployment-and-upgrade"></a>Actualizaciones e implementaciones de cliente

### <a name="azure-ad-enabled-clients-cant-communicate-with-management-point"></a>Los clientes habilitados para Azure AD no se pueden comunicar con el punto de administración
<!--501089-->
*Se aplica a: Configuration Manager, versión 1706*
<!--also fixed in 1710 HFRU--> En el escenario [Instalación y asignación de clientes Windows 10 para Configuration Manager mediante la autenticación basada en Azure AD](/sccm/core/clients/deploy/deploy-clients-cmg-azure), se produce un error en la comunicación de cliente cuando el punto de administración habilitado para HTTPS usa credenciales de base de datos alternativas. 

#### <a name="workaround"></a>Solución alternativa
Solucione este problema con una de las acciones siguientes:
- Actualice el sitio a la última versión y aplique la revisión más reciente.
- Cambie las credenciales que usa el punto de administración.


<!-- ## Operating system deployment  -->



## <a name="software-updates"></a>Actualizaciones de software

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
