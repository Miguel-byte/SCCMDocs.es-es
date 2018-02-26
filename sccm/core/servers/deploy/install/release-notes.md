---
title: "Notas de la versión "
titleSuffix: Configuration Manager
description: "Consulte estas notas relativas a problemas urgentes que aún no se han corregido en el producto o no se han tratado en un artículo de Microsoft Knowledge Base."
ms.custom: na
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 030947fd-f5e0-4185-8513-2397fb2ec96f
caps.latest.revision: 
caps.handback.revision: 
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 53685ef2647cfd87c2fcb603097186360f1c96a5
ms.sourcegitcommit: fbd4a9d2fa8ed4ddd3a0fecc4a2ec4fc0ccc3d0c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/19/2018
---
# <a name="release-notes-for-system-center-configuration-manager"></a>Notas de la versión de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Con Configuration Manager, las notas de la versión del producto se limitan a cuestiones urgentes. Estos problemas aún no se han corregido en el producto o no se han tratado en detalle en un artículo de Microsoft Knowledge Base.  

La documentación específica de características incluye información acerca de los problemas conocidos que afectan a escenarios básicos.  

> [!TIP]  
>  Este tema contiene notas de la versión de la rama actual de Configuration Manager. Para obtener información sobre la rama de Technical Preview, vea [Technical Preview para System Center Configuration Manager](../../../../core/get-started/technical-preview.md).  

Para obtener información sobre las características que presentan las distintas versiones, consulte los siguientes artículos:
- [Novedades de la versión 1710](/sccm/core/plan-design/changes/whats-new-in-version-1710)
- [Novedades de la versión 1706](/sccm/core/plan-design/changes/whats-new-in-version-1706)  
- [Novedades de la versión 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702)



## <a name="setup-and-upgrade"></a>Instalación y actualización  


### <a name="when-installing-a-long-term-service-branch-site-using-version-1606-a-current-branch-site-is-installed"></a>Al instalar un sitio de Rama de mantenimiento a largo plazo mediante la versión 1606, se instala un sitio de Rama actual
<!-- Consider move to core content  -->
Al usar el medio de línea base de la versión 1606 incluido en la versión de octubre de 2016 para instalar un sitio de Rama de mantenimiento a largo plazo (LTSB), el programa de instalación instala en su lugar un sitio de Rama actual. Este comportamiento se da porque no está seleccionada la opción para instalar un punto de conexión de servicio con la instalación del sitio.

 - Aunque no es necesario un punto de conexión de servicio, se debe seleccionar que se instale durante la instalación de un sitio de LTSB.

Una vez completada la instalación, puede desinstalar el punto de conexión de servicio. Pero debe tener un punto de conexión de servicio en modo sin conexión o en línea para enviar datos de telemetría y obtener actualizaciones de seguridad de los sitios de Rama actual y LTSB.

Si su sitio se instaló como un sitio de Rama actual pero quería instalar la LTSB, puede desinstalarlo y volver a instalarlo. También puede llamar a [Ayuda y soporte de Microsoft](http://go.microsoft.com/fwlink/?LinkId=243064) para obtener ayuda.  

Para confirmar qué rama está instalada, en la consola, vaya a **Administración** > **Configuración de sitio** > **Sitios** y abra **Configuración de jerarquía**. La opción para convertir el sitio a un sitio de Rama actual solo está disponible cuando el sitio ejecuta la LTSB.  

**Solución:** ninguna.   


### <a name="an-update-persists-in-downloading-state-in-the-updates-and-servicing-node-of-the-console"></a>Una actualización persiste en el estado Descargando en el nodo Actualizaciones y mantenimiento de la consola  
<!-- Source bug pending. Consider move to core content.  8/15 Seeking validation of issue from Dev.  -->
Durante la descarga automática de actualizaciones por un punto de conexión de servicio en línea, una actualización puede bloquearse con un estado Descargando. Cuando se detiene la descarga de una actualización, aparecen entradas similares a las siguientes en los archivos de registro indicados:  

Registro de DMPdownloader:  
`ERROR: Failed to download redist for 037cd17e-4d7b-40e1-802b-14bb682364c7 with command  /RedistUrl http://go.microsoft.com/fwlink/?LinkID=724436 /LnManifestUrl http://go.microsoft.com/fwlink/?LinkID=724434 /RedistVersion 112015 /NoUI  "D:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist"`  

ConfigMgrSetup.log:  
`Error: failed to verify 'd:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist\sqlncli.msi' authenticode signature.`  
`Error: file signature check failed for 'd:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist\sqlncli.msi`  

**Solución**: en el servidor de sitio, modifique la siguiente clave del Registro para que coincida con el valor siguiente:  

-   **Clave para editar**: HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\WinTrust\Trust Providers\Software Publishing  

-   **Valor para estado**: establecido en **146944** decimal o **0x00023e00** hexadecimal  

A continuación, reinicie el servicio SMS_Executive o espere 24 horas al próximo ciclo de descarga automática.

### <a name="when-using-redistributable-files-from-the-cdlatest-folder-setup-fails-with-a-manifest-verification-error"></a>Cuando se usan archivos de redistribución de la carpeta CD.Latest, se produce un error de comprobación de manifiesto en la instalación
<!-- Source bug pending    8/15 Seeking validation of issue from Dev.   -->

Al ejecutar el programa de instalación desde la carpeta CD.Latest creada para la versión 1606 y usar los archivos de redistribución incluidos en dicha carpeta, se produce un error en el programa de instalación. Aparecen los siguientes errores en el registro de instalación de Configuration Manager:

  `ERROR: File hash check failed for defaultcategories.dll`  
  `ERROR: Manifest verification failed. Wrong version of manifest?`

**Solución:** use una de las siguientes opciones:
 - Durante la instalación, elija descargar los archivos redistribuibles más recientes de Microsoft. Utilice los archivos redistribuibles más recientes en lugar de los archivos incluidos en la carpeta CD.Latest.
 - Elimine manualmente la carpeta *cd.latest\redist\languagepack\zhh* y, luego, vuelva a ejecutar la instalación.



<!-- ## Backup and recovery  -->


## <a name="client-deployment-and-upgrade"></a>Actualizaciones e implementaciones de cliente  

### <a name="client-installation-fails-with-error-code-0x8007064c"></a>Se produce un error en la instalación del cliente con el código de error 0x8007064c
<!--- SMS 486973  applies 1606 to 1706. Not yet fixed. -->
*La siguiente cuestión se aplica a todas las versiones activas de Configuration Manager.*  

Al implementar el cliente en equipos con Windows, se produce un error en la instalación. El archivo ccmsetup.log contiene las entradas siguientes: 

`File 'C:\WINDOWS\ccmsetup\Silverlight.exe' returned failure exit code 1612. Fail the installation`  
`InstallFromManifest failed 0x8007064c`

**Solución**: una versión de Silverlight previamente instalada que está dañada provoca este problema. Para solucionarlo, ejecute la herramienta siguiente en el equipo afectado: [Solucionar problemas que impiden la instalación o desinstalación de programas](https://support.microsoft.com/help/17588/fix-problems-that-block-programs-from-being-installed-or-removed).

## <a name="operating-system-deployment"></a>Implementación de sistema operativo  

### <a name="servicing-plans-create-many-duplicate-software-update-groups-and-deployments-by-default"></a>Los planes de mantenimiento crean de forma predeterminada muchos grupos de actualizaciones e muchas implementaciones de software duplicadas  
De forma predeterminada, el asistente para Crear un plan de mantenimiento se ejecuta actualmente después de cada sincronización de actualizaciones de software. Cada vez que se ejecuta el asistente, se crea un nuevo grupo de actualizaciones e implementaciones de software. Si tiene una programación de sincronización de actualizaciones de software que se ejecuta varias veces al día, el Asistente para crear un plan de mantenimiento crea varios grupos de actualizaciones de software e implementaciones cada día.  

**Solución**: después de crear un plan de mantenimiento, abra las propiedades, vaya a la pestaña **Programación de evaluación**, seleccione **Ejecutar la regla en una programación**, haga clic en **Personalizar** y cree una programación personalizada. Por ejemplo, puede hacer que el plan de mantenimiento se ejecute cada 60 días.  



## <a name="software-updates"></a>Actualizaciones de software

### <a name="importing-an-office-365-client-settings-from-a-configuration-file-fails-when-it-contains-unsupported-languages"></a>La importación de una configuración de cliente de Office 365 desde un archivo de configuración genera un error cuando contiene idiomas no admitidos
<!-- 489258  Fixed in 1706  -->
*El siguiente problema se aplica a la versión 1702 y a versiones anteriores.*   

Al importar la configuración de cliente de Office 365 desde un archivo de configuración XML existente, si el archivo contiene idiomas que no son compatibles con el cliente de Office 365 ProPlus, se produce un error. Para obtener más información, consulte [Para implementar aplicaciones de Office 365 en clientes desde el panel Administración de clientes de Office 365](/sccm/sum/deploy-use/manage-office-365-proplus-updates#to-deploy-office-365-apps-to-clients-from-the-office-365-client-management-dashboard).

**Solución**: use solo los [idiomas admitidos por el cliente de Office 365 ProPlus](https://technet.microsoft.com/library/cc179219&#40;v=office.16&#41;.aspx) en el archivo de configuración XML.  



## <a name="mobile-device-management"></a>Administración de dispositivos móviles  

### <a name="beginning-with-version-1710-you-can-no-longer-deploy-windows-phone-81-vpn-profiles-to-windows-10------503274--should-be-fixed-by-1802-if-not-sooner---"></a>A partir de la versión 1710, ya no se pueden implementar perfiles de VPN de Windows Phone 8.1 en Windows 10   <!-- 503274  Should be fixed by 1802, if not sooner -->
En 1710 ya no es posible crear un perfil de VPN mediante el flujo de trabajo de Windows Phone 8.1 que también se aplica a dispositivos Windows 10. Para estos perfiles, la página Plataformas compatibles ya no se muestra en el asistente para la creación. Windows Phone 8.1 se selecciona automáticamente en el back-end. La página Plataformas compatibles está disponible en las propiedades del perfil, pero no muestra las opciones de Windows 10.

**Solución alternativa**: use el flujo de trabajo del perfil de VPN de Windows 10 para dispositivos Windows 10. Si esta opción no es factible para su entorno, póngase en contacto con el soporte técnico. El soporte técnico puede ayudarle a agregar los destinos de Windows 10.


### <a name="full-wipe-disables-windows-10-devices-with-less-than-4-gb-of-memory"></a>El borrado completo deshabilita los dispositivos de Windows 10 con menos de 4 GB de memoria
Realizar un borrado completo en dispositivos que ejecutan Windows 10, versión 1507, con mejos de 4 GB de RAM puede dejar el dispositivo inutilizable. Después de intentar borrar el dispositivo, este no se puede iniciar y no responde.

**Solución**: asegúrese de que los dispositivos con Windows 10 tienen al menos 4 GB de memoria disponible antes de realizar un borrado completo. Para ver el número de versión de los dispositivos de Windows 10, escriba 'winver' en un símbolo del sistema. Si ya ha borrado el dispositivo y ha dejado de responder, use una unidad USB de arranque de Windows 10 para recuperar el dispositivo.


### <a name="when-a-user-belongs-to-two-or-more-user-collections-to-which-you-deploy-a-terms-and-conditions-policy-the-user-sees-multiple-sets-of-the-same-terms"></a>Cuando un usuario pertenece a dos o más recopilaciones de usuarios en las que implementa una directiva de términos y condiciones, el usuario ve varios conjuntos de los mismos términos  
<!-- 454394    -->
Si implementa un conjunto de términos en varias recopilaciones de usuarios, y un usuario es miembro de más de una de estas recopilaciones, ese usuario verá varias copias de los mismos términos en el portal de empresa. Por ejemplo:
- Un usuario llamado "SampleUser" es un miembro de dos coleccioness de usuario diferentes: "CompanyEmployeesFTE" y "CompanyEmployeesNA".
- Implementa los términos y condiciones "CompanyTerms" en CompanyEmployeesFTE y CompanyEmployeesNA.
- El usuario SampleUser verá dos conjuntos idénticos de CompanyTerms en la página de aceptación de términos en el Portal de empresa. 

Los usuarios solo pueden aceptar o rechazar todos los términos. Por lo tanto, no hay ningún riesgo de estado de aceptación ambigua (este estado ambiguo es en el que el usuario acepta y rechaza los mismos términos). El informe de aceptación de términos y condiciones solo incluye una fila para cada conjunto de términos de cada usuario, de modo que no hay ningún error en el informe. La única consecuencia es que el usuario ve dos conjuntos de términos en la página de aceptación.  

**Solución alternativa**: asegúrese de que cada usuario solo se incluya en una colección para la que se implementan los términos.  


<!-- ## Reports and monitoring    -->
<!-- ## Conditional access   -->
<!-- ## Endpoint Protection -->
