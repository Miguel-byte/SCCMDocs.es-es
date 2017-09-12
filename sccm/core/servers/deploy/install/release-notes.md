---
title: "Notas de la versión en Configuration Manager | Microsoft Docs"
description: "Consulte estas notas relativas a problemas urgentes que aún no se han corregido en el producto o no se han tratado en un artículo de Microsoft Knowledge Base."
ms.custom: na
ms.date: 08/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 030947fd-f5e0-4185-8513-2397fb2ec96f
caps.latest.revision: "41"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 4e818ffd943208eab323b1558f825bd87f3ddc4c
ms.sourcegitcommit: 13599667ea77c16db1aebe64f8a6748c268f0b45
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/11/2017
---
# <a name="release-notes-for-system-center-configuration-manager"></a>Notas de la versión de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Con System Center Configuration Manager, las notas de la versión del producto se limitan a problemas urgentes que aún no se han resuelto en el producto (disponible a través de una actualización en la consola) o problemas detallados en el artículo de Microsoft Knowledge Base.  

La información sobre los problemas conocidos que afectan a los escenarios principales se muestra en la documentación del producto en línea, que se encuentra en la biblioteca de documentación de System Center Configuration Manager.  

> [!TIP]  
>  Este tema contiene notas de la versión de la rama actual de System Center Configuration Manager. Para obtener información sobre la vista previa técnica de System Center Configuration Manager, consulte [Technical Preview for System Center Configuration Manager](../../../../core/get-started/technical-preview.md) (Technical Preview de System Center Configuration Manager).  

Para obtener información sobre las características que presentan las distintas versiones, consulte lo siguiente:
- [Novedades de la versión 1706](/sccm/core/plan-design/changes/whats-new-in-version-1706)  
- [Novedades de la versión 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702)
- [Novedades de la versión 1610](/sccm/core/plan-design/changes/whats-new-in-version-1610)
   


## <a name="setup-and-upgrade"></a>Instalación y actualización  

### <a name="after-you-update-a-configuration-manager-console-using-consolesetupexe-from-the-site-server-folder-recent-language-pack-changes-are-not-available"></a>Después de actualizar una consola de Configuration Manager mediante ConsoleSetup.exe desde la carpeta del servidor de sitio, los cambios recientes del paquete de idioma no están disponibles.
<!--  SMS 486420  Applicability should be 1610 and 1702.  -->
*La información siguiente se aplica a las versiones 1610 y 1702.*   
Después de ejecutar una actualización local en una consola mediante ConsoleSetup.exe desde una carpeta de instalación de servidores de sitio, los paquetes de idioma instalados recientemente pueden no estar disponibles. Esto ocurre cuando:
- El sitio ejecuta la versión 1610 o 1702.
- La consola se actualiza a nivel local mediante ConsoleSetup.exe desde la carpeta de instalación del servidor de sitio.

Cuando se produce este problema, la consola reinstalada no utiliza el conjunto más reciente de los paquetes de idioma que se configuraron. No se devuelve ningún error, pero los paquetes de idioma disponibles en la consola no habrán cambiado.  

**Solución alternativa:** desinstale la consola actual y después vuelva a instalarla como una nueva instalación. Puede utilizar ConsoleSetup.exe desde la carpeta de instalación de servidores de sitio. Durante la instalación, asegúrese de seleccionar los archivos de paquete de idioma que desea utilizar.


### <a name="with-version-1702-the-default-site-boundary-group-is-configured-for-use-for-site-assignment"></a>Con la versión 1702, el grupo de límites del sitio predeterminado está configurado para usarlo en la asignación de sitio.
<!--  SMS 486380   Applicability should only be to 1702. -->
*La información siguiente se aplica a la versión 1702.*  
La pestaña Referencia de los grupos de límite del sitio por defecto está marcada para **Usar este grupo de límites para la asignación de sitio**, muestra el sitio como **Sitio asignado** y está atenuada para que la configuración no se pueda modificar ni borrar.

**Solución:** ninguna. Puede ignorar esta configuración. Aunque el grupo está habilitado para la asignación de sitio, el grupo de límites del sitio predeterminado no se utiliza para la asignación de sitio. Con 1702, esta configuración garantiza que el grupo de límites del sitio predeterminado se asocie al sitio correcto.



### <a name="when-installing-a-long-term-service-branch-site-using-version-1606-a-current-branch-site-is-installed"></a>Al instalar un sitio de Rama de mantenimiento a largo plazo mediante la versión 1606, se instala un sitio de Rama actual
<!-- Consider move to core content  -->
Al usar el medio de línea base de la versión 1606 incluido en la versión de octubre de 2016 para instalar un sitio de Rama de mantenimiento a largo plazo (LTSB), el programa de instalación instala en su lugar un sitio de Rama actual. Esto ocurre porque no está seleccionada la opción para instalar un punto de conexión de servicio con la instalación del sitio.

 - Aunque no es necesario un punto de conexión de servicio, se debe seleccionar que se instale durante la instalación de un sitio de LTSB.

Una vez completada la instalación, puede desinstalar el punto de conexión de servicio.  Pero debe tener un punto de conexión de servicio en modo sin conexión o en línea para enviar datos de telemetría y obtener actualizaciones de seguridad de los sitios de Rama actual y LTSB.

Si su sitio se instaló como un sitio de Rama actual pero quería instalar la LTSB, puede desinstalarlo y volver a instalarlo. También puede llamar a [Ayuda y soporte de Microsoft](http://go.microsoft.com/fwlink/?LinkId=243064) para obtener ayuda.  

Para confirmar qué rama está instalada, en la consola, vaya a **Administración** > **Configuración de sitio** > **Sitios** y abra **Configuración de jerarquía**. La opción para convertir el sitio a un sitio de Rama actual solo está disponible cuando el sitio ejecuta la LTSB.  

**Solución alternativa:**  ninguna.   


### <a name="an-update-is-stuck-with-a-state-of-downloading-in-the-updates-and-servicing-node-of-the-configuration-manager-console"></a>Una actualización está detenida con un estado Descargando en el nodo Actualizaciones y mantenimiento de la consola de Configuration Manager  
<!-- Source bug pending. Consider move to core content.  8/15 Seeking validation of issue from Dev.  -->
Durante la descarga automática de actualizaciones por un punto de conexión de servicio en línea, una actualización puede bloquearse con un estado Descargando. Cuando se detiene la descarga de una actualización, aparecen entradas similares a las siguientes en los archivos de registro indicados:  

Registro de DMPdownloader:  

-   ERROR: No se pudo descargar el paquete redistribuible para 037cd17e-4d7b-40e1-802b-14bb682364c7 con el comando /RedistUrl http://go.microsoft.com/fwlink/?LinkID=724436 /LnManifestUrl http://go.microsoft.com/fwlink/?LinkID=724434 RedistVersion 112015/NoUI "D:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist"  

ConfigMgrSetup.log:  

-   Error: Error al comprobar 'd: firma de código de autenticación de \ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist\sqlncli.msi'.  

-   Error: Error de comprobación de la forma de archivo para 'd:\ConfigMgr\EasySetupPayload\037cd17e-4d7b-40e1-802b-14bb682364c7\redist\sqlncli.msi  

**Solución alternativa**: en el servidor de sitio, modifique la siguiente clave del Registro para que coincida con la siguiente y, luego, reinicie el servicio SMS_Executive o espere 24 horas al próximo ciclo de descarga automática.  

-   **Clave para editar**: HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\WinTrust\Trust Providers\Software Publishing  

-   **Valor para estado**: establecido en **146944** decimal o **0x00023e00** hexadecimal  


###  <a name="setup-fails-when-using-redist-files-from-the-cdlatest-folder-with-a-manifest-verification-error"></a>Se produce un error en el programa de instalación cuando se usan archivos de redistribución de la carpeta CD.Latest con un error de comprobación de manifiesto
<!-- Source bug pending    8/15 Seeking validation of issue from Dev.   -->

Al ejecutar el programa de instalación desde la carpeta CD.Latest creada para la versión 1606 y usar los archivos de redistribución incluidos en dicha carpeta, se produce un error en el programa de instalación. Aparecen los siguientes errores en el registro de instalación de Configuration Manager:

  - ERROR: File hash check failed for defaultcategories.dll
  - ERROR: Manifest verification failed. Wrong version of manifest?

**Solución alternativa:** use uno de los siguientes métodos:
 - Durante la instalación, descargue los archivos de redistribución más recientes de Microsoft, en lugar de usar los que se incluyen en la carpeta CD.Latest.
 - Elimine manualmente la carpeta *cd.latest\redist\languagepack\zhh* y, luego, vuelva a ejecutar la instalación.


### <a name="service-connection-tool-throws-an-exception-when-sql-server-is-remote-or-when-shared-memory-is-disabled"></a>La herramienta de conexión de servicio produce una excepción cuando SQL Server está instalado en una ubicación remota o cuando la memoria compartida está deshabilitada
<!-- 479223   Fixed in 1702 and later   -->
*La información siguiente se aplica a la versión 1610 y a versiones anteriores.*  
La herramienta de conexión de servicio genera una excepción cuando se cumple una de las condiciones siguientes:  
 -  La base de datos del sitio está instalada en una ubicación remota con respecto al equipo que hospeda el punto de conexión de servicio y usa un puerto no estándar (un puerto distinto de 1433).
 -  La base de datos del sitio está en el mismo servidor que el punto de conexión de servicio, pero la **memoria compartida** del protocolo de SQL está deshabilitada.

La excepción es similar a la siguiente:
 - *Excepción no controlada: System.Data.SqlClient.SqlException: Error relacionado con la red o específico de la instancia mientras se establecía una conexión con el servidor SQL Server. No se encontró el servidor o éste no estaba accesible. Compruebe que el nombre de la instancia es correcto y que SQL Server está configurado para admitir conexiones remotas. (proveedor: Proveedor de canalizaciones con nombre, error: 40 - No se pudo abrir una conexión con SQL Server) --*

**Solución alternativa**: mientras usa la herramienta, debe modificar el registro del servidor que hospeda el punto de conexión de servicio para que incluya información sobre el puerto de SQL Server:

   1.   Antes de usar la herramienta, edite la siguiente clave del Registro y agregue el número del puerto que está en uso con el nombre de SQL Server:
    - Clave: HKLM\Microsoft\SMS\COMPONENTS\SMS_DMP_UPLOADER\
      - Valor: &lt;nombre de SQL Server>
    - Agregue: **,&lt;PUERTO>**

    Por ejemplo, para agregar el puerto *15001* a un servidor denominado *testserver.test.net*, la clave resultante sería la siguiente: ***HKLM\Software\Microsoft\SMS\COMPONENTS\SMS_DMP_UPLOADER\testserver.test.net,15001***

   2.   Después de agregar el puerto al registro, la herramienta debería funcionar con normalidad.  

   3.   Una vez que haya acabado de usar la herramienta, cambie la clave del Registro al valor original para los pasos **-import** y **-connect**.  


<!-- ## Backup and recovery  -->


## <a name="client-deployment-and-upgrade"></a>Actualizaciones e implementaciones de cliente  

### <a name="client-installation-fails-with-error-code-0x8007064c"></a>Se produce un error en la instalación del cliente con el código de error 0x8007064c
<!--- SMS 486973  applies 1606 to 1706. Not yet fixed. -->
*La información siguiente se aplica a todas las versiones activas de Configuration Manager.*   
Al implementar el cliente en equipos Windows, se produce un error en la instalación. El archivo ccmsetup.log contiene la entrada "File 'C:\WINDOWS\ccmsetup\Silverlight.exe' returned failure exit code 1612. Fail the installation" followed by "InstallFromManifest failed 0x8007064c".

**Solución** Esto se debe a una versión de Silverlight previamente instalada que está dañada. Puede intentar ejecutar la herramienta siguiente en el equipo afectado para solucionar este problema: [https://support.microsoft.com/help/17588/fix-problems-that-block-programs-from-being-installed-or-removed](https://support.microsoft.com/help/17588/fix-problems-that-block-programs-from-being-installed-or-removed)

## <a name="operating-system-deployment"></a>Implementación de sistema operativo  

### <a name="servicing-plans-create-a-lot-of-duplicate-software-update-groups-and-deployments-by-default"></a>Los planes de mantenimiento crean de forma predeterminada muchos grupos de actualizaciones e muchas implementaciones de software duplicadas  
De forma predeterminada, el asistente para Crear un plan de mantenimiento se ejecuta actualmente después de cada sincronización de actualizaciones de software. Cada vez que se ejecuta el asistente, se crea un nuevo grupo de actualizaciones e implementaciones de software. Si tiene una programación de sincronización de actualizaciones de software que se ejecuta varias veces al día, por ejemplo, el asistente para Crear un plan de mantenimiento creará varios grupos de actualizaciones y varias implementaciones de software, probablemente idénticos, cada día.  

**Solución alternativa**:    
Después de crear un plan de mantenimiento, abra las propiedades, vaya a la pestaña **Programación de evaluación**, seleccione **Ejecutar la regla en una programación**, haga clic en **Personalizar** y cree una programación personalizada. Por ejemplo, puede hacer que el plan de mantenimiento se ejecute cada 60 días.  


### <a name="when-a-high-risk-deployment-dialog-is-visible-to-a-user-subsequent-high-risk-dialogs-with-a-sooner-deadline-are-not-displayed"></a>Cuando un cuadro de diálogo de implementación de alto riesgo es visible para un usuario, no se muestran cuadros de diálogo de alto riesgo posteriores con una fecha límite anterior.
<!-- Fixed in 1702 and later -->
*La información siguiente se aplica a la versión 1610 y a versiones anteriores.*   
Después de crear e implementar una implementación de tareas de alto riesgo para los usuarios, se muestra un cuadro de diálogo de alto riesgo al usuario. Si el usuario cierra el cuadro de diálogo, cree e implemente otra implementación de alto riesgo con una fecha límite anterior a la del primero, y el usuario no recibirá un cuadro de diálogo actualizado hasta que haya cerrado el cuadro de diálogo original. Las implementaciones seguirán ejecutándose en las fechas límite configuradas.

**Solución alternativa**:  
El usuario debe cerrar el cuadro de diálogo de la primera implementación de alto riesgo para ver el cuadro de diálogo de la siguiente implementación de alto riesgo.



## <a name="software-updates"></a>Actualizaciones de software

### <a name="importing-an-office-365-client-settings-from-a-configuration-file-fails-when-it-contains-unsupported-languages"></a>La importación de una configuración de cliente de Office 365 desde un archivo de configuración genera un error cuando contiene idiomas no admitidos
<!-- 489258  Fixed in 1706  -->
*La información siguiente se aplica a la versión 1702 y a versiones anteriores.*   
Al importar la configuración de cliente de Office 365 desde un archivo de configuración XML existente, si el archivo contiene idiomas que no son compatibles con el cliente de Office 365 ProPlus, se producirá un error. Para obtener más información, consulte [Para implementar aplicaciones de Office 365 en clientes desde el panel Administración de clientes de Office 365](/sccm/sum/deploy-use/manage-office-365-proplus-updates#to-deploy-office-365-apps-to-clients-from-the-office-365-client-management-dashboard).

**Solución alternativa**:    
Use solo los [idiomas admitidos por el cliente de Office 365 ProPlus](https://technet.microsoft.com/library/cc179219&#40;v=office.16&#41;.aspx) en el archivo de configuración XML.  



## <a name="mobile-device-management"></a>Administración de dispositivos móviles  

### <a name="full-wipe-disables-windows-10-devices-with-less-than-4-gb-ram"></a>El borrado completo deshabilita los dispositivos de Windows 10 con menos de 4 GB de RAM
Realizar un borrado completo en dispositivos de Windows 10 RTM (versiones anteriores a la 1511) con menos de 4 GB de RAM puede inutilizar el dispositivo. Después de intentar borrar el dispositivo, este no se puede iniciar y no responde.

**Solución alternativa**: asegúrese de que los equipos con Windows 10 RTM tienen al menos 4 GB de RAM disponibles antes de realizar un borrado completo en el dispositivo. Para ver el número de versión de los dispositivos de Windows 10, escriba 'winver' en un símbolo del sistema. Si el dispositivo ya se ha borrado y ya no responde, use una unidad USB de Windows 10 de arranque para iniciar y recuperar el acceso al dispositivo.


### <a name="when-a-user-belongs-to-two-or-more-user-collections-that-a-terms-and-conditions-policy-is-deployed-to-the-user-sees-multiple-sets-of-the-same-terms"></a>Cuando un usuario pertenece a dos o más recopilaciones de usuarios en las que se implementa una directiva de términos y condiciones, el usuario ve varios conjuntos de los mismos términos  
<!-- 454394    -->
Si un administrador implementa un conjunto de términos en varias recopilaciones de usuarios, y un usuario es miembro de más de una de estas recopilaciones, ese usuario verá varias copias de los mismos términos al abrir el portal de empresa.  Por ejemplo, si un usuario llamado "SampleUser" es miembro de dos recopilaciones de usuarios diferentes, denominadas "CompanyEmployeesFTE" y "CompanyEmployeesNA", y los términos y condiciones denominados "CompanyTerms" se implementan en CompanyEmployeesFTE y CompanyEmployeesNA, SampleUser verá dos conjuntos idénticos de CompanyTerms en la página de aceptación de términos. Puesto que los usuarios solo pueden aceptar o rechazar todos los términos, no existe riesgo de estar en un estado de aceptación ambigua (donde el usuario ha aceptado y rechazado los términos al mismo tiempo). El informe de aceptación de términos y condiciones solo incluirá una fila para cada conjunto de términos de cada usuario, de modo que no hay ningún error en el informe. La única consecuencia es que el usuario verá dos conjuntos de términos en la página de aceptación.  

**Solución alternativa**: asegúrese de que cada usuario solo se incluya en una colección para la que se implementan los términos.  


### <a name="android-for-work-email-profiles-that-use-certificate-authentication-are-not-applied-to-devices"></a>Los perfiles de correo electrónico de Android for Work que usen autenticación de certificado no se aplican a los dispositivos.
<!--  487657      -->
Cuando se crea un perfil de correo electrónico de Android for Work, hay dos opciones de autenticación. Una es el nombre de usuario y la contraseña y la otra es certificados. En este momento, no funciona la opción de certificados. Si el perfil se crea con el método de autenticación establecido en **certificados**, el perfil no se aplica al dispositivo y se le pedirá al usuario que especifique manualmente los detalles de la cuenta de correo electrónico.

**SOLUCIÓN ALTERNATIVA**: ninguna. Los administradores deben usar la opción de **nombre de usuario y contraseña** o esperar a que este problema se resuelva.



<!-- ## Reports and monitoring    -->
<!-- ## Conditional access   -->


## <a name="endpoint-protection"></a>Endpoint Protection

### <a name="antimalware-policy-fails-to-apply-on-windows-server-2016-core"></a>La directiva antimalware no se puede aplicar en Windows Server 2016 Core
<!--  Product Studio bug 485370 added 04 19 2017   Fixed in 1702 -->
*La información siguiente se aplica a la versión 1610 y a versiones anteriores.*  
La directiva antimalware no se puede aplicar en Windows Server 2016 Core.  El código de error es 0x80070002.  Falta una dependencia para ConfigSecurityPolicy.exe.

**Solución:** Este problema se resuelve por el [artículo 4019472 de Knowledge Base](https://support.microsoft.com/help/4019472/windows-10-update-kb4019472) distribuido el 9 de mayo de 2017.


### <a name="windows-defender-advanced-threat-protection-policies-fail-on-older-client-agents"></a>Las directivas de Protección contra amenazas avanzada de Windows Defender dan error en agentes cliente antiguos
<!-- Product Studio bug 462286 added  05 25 2017 and valid until July 2017 GA release      Fixed in 1610 -->
Las directivas de Protección contra amenazas avanzada de Windows Defender creadas desde una versión 1610 de Configuration Manager o un servidor de sitio posterior no pueden aplicarse en la versión 1606 de Configuration Manager y clientes anteriores.  Los clientes no se incorporan y la evaluación de directivas informa de un error. El **Estado de implementación** en la configuración de Protección contra amenazas avanzada de Windows Defender se muestra como **Error**.

**Solución**: actualice el cliente de Configuration Manager a la versión 1610 o posterior.
