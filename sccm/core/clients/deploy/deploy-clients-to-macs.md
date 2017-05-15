---
title: Implementar clientes Mac | Microsoft Docs
description: "Obtenga información sobre cómo implementar clientes en equipos Mac en System Center Configuration Manager."
ms.custom: na
ms.date: 05/04/2017
ms.prod: configuration-manager
ms.reviewer: aaroncz
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e46ad501-5d73-44ac-92de-0de14ef72b83
caps.latest.revision: 12
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: c6a6137fa978e1ea28aefea2aea4e29ba661efd6
ms.openlocfilehash: 6ce212c6745b70a47553891e5dbc124b4c4e50fa
ms.contentlocale: es-es
ms.lasthandoff: 05/04/2017


---
# <a name="how-to-deploy-clients-to-macs"></a>How to deploy clients to Macs

*Se aplica a: System Center Configuration Manager (rama actual)*

En este tema se describe cómo implementar y mantener el cliente de Configuration Manager en equipos Mac. Para obtener información sobre qué se debe configurar antes de implementar clientes en equipos Mac, vea [Prepararse para implementar software cliente en equipos Mac](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients).

Cuando instale un nuevo cliente para equipos Mac, es posible que tenga que instalar también actualizaciones de Configuration Manager para reflejar la nueva información de cliente en la consola de Configuration Manager.

En estos procedimientos, tiene dos opciones para instalar los certificados de cliente. Obtenga más información sobre los certificados de cliente para equipos Mac en [Prepararse para implementar software cliente en equipos Mac](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients#certificate-requirements).  

-   Usar la inscripción de Configuration Manager mediante la [herramienta CMEnroll](#install-the-client-and-then-enroll-the-client-certificate-on-the-mac). El proceso de inscripción no admite la renovación automática de certificados por lo que debe volver a inscribir los equipos Mac antes de que expire el certificado instalado.    

-   [Usar una solicitud de certificado y un método de instalación independiente de Configuration Manager](#use-a-certificate-request-and-installation-method-that-is-independent-from-configuration-manager). 

>[!IMPORTANT]
>  Para implementar el cliente en dispositivos que ejecutan macOS Sierra, el nombre de asunto del certificado de punto de administración se debe configurar correctamente mediante, por ejemplo, el FQDN del servidor de punto de administración.


## <a name="configure-client-settings-for-enrollment"></a>Configurar las opciones del cliente para la inscripción  
 Debe usar la [configuración de cliente predeterminada](../../../core/clients/deploy/about-client-settings.md) para configurar la inscripción para equipos Mac; no puede usar una configuración de cliente personalizada.  

 Esto es necesario para que Configuration Manager solicite e instale el certificado en el equipo Mac.  

### <a name="to-configure-the-default-client-settings-for-configuration-manager-to-enroll-certificates-for-macs"></a>Para configurar las opciones de cliente predeterminadas para que Configuration Manager inscriba los certificados para los equipos Mac  

1.  En la consola de Configuration Manager, elija **Administración** >  **Configuración de cliente** > **Configuración de cliente predeterminada**.  

4.  En la pestaña **Inicio**, en el grupo **Propiedades**, elija **Propiedades**.  

5.  Seleccione la sección **Inscripción** y, después, configure estas opciones:  

    1.  **Permitir a los usuarios inscribir dispositivos móviles y equipos Mac: Sí**  

    2.  **Perfil de inscripción:** seleccione **Establecer perfil**.  

6.  En el cuadro de diálogo **Perfil de inscripción de dispositivo móvil**, seleccione **Crear**.  

7.  En el cuadro de diálogo **Crear perfil de inscripción** , escriba un nombre para este perfil de inscripción y, a continuación, configure el **Código del sitio de administración**. Seleccione el sitio primario de Configuration Manager que contiene los puntos de administración que administrarán los equipos Mac.  

    > [!NOTE]  
    >  Si no puede seleccionar el sitio, compruebe que como mínimo un punto de administración en el sitio está configurado para admitir dispositivos móviles.  

8.  Seleccione **Agregar**.  

9. En el cuadro de diálogo **Agregar entidad de certificación para dispositivos móviles**, seleccione el servidor de la entidad de certificación (CA) que emitirá certificados a equipos Mac.  

10. En el cuadro de diálogo **Crear perfil de inscripción**, seleccione la plantilla de certificado del equipo Mac que ha creado en el paso 3.  

11. Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Perfil de inscripción** y el cuadro de diálogo **Configuración de cliente predeterminada**.  

    > [!TIP]  
    >  Si quiere cambiar el intervalo de directivas de cliente, use el **Intervalo de sondeo de directiva de cliente** en el grupo de configuración de cliente **Directiva de cliente**.  

 Todos los usuarios se configurarán con estas opciones la próxima vez que descarguen directivas de cliente. Para iniciar la recuperación de directivas para un solo cliente, consulte [Initiate Policy Retrieval for a Configuration Manager Client](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval) (Iniciar la recuperación de directivas para un cliente de Configuration Manager).  

 Además de la configuración de cliente de inscripción, asegúrese de que configuró la siguiente configuración de dispositivo de cliente:  

-   **Inventario de hardware**: habilite y configure esta opción si quiere recopilar el inventario de hardware de los equipos cliente Mac y Windows. Para obtener más información, consulte [How to extend hardware inventory in System Center Configuration Manager](../../../core/clients/manage/inventory/extend-hardware-inventory.md) (Cómo ampliar el inventario de hardware en System Center Configuration Manager).  

-   **Configuración de cumplimiento**: habilite y configure esta opción si quiere evaluar y corregir la configuración de los equipos cliente Mac y Windows. Para obtener más información, consulte [Plan for and configure compliance settings](../../../compliance/plan-design/plan-for-and-configure-compliance-settings.md) (Planear y configurar la configuración de cumplimiento).  

> [!NOTE]  
>  Para obtener más información sobre la configuración de cliente de Configuration Manager, consulte [How to configure client settings in System Center Configuration Manager](../../../core/clients/deploy/configure-client-settings.md) (Cómo configurar el cliente en System Center Configuration Manager).  

## <a name="download-the-client-source-files-for-macs"></a>Descargar los archivos de origen de cliente para equipos Mac  

1.  Descargue el paquete de archivos de cliente de Mac OS X **ConfigmgrMacClient.msi**y guárdelo en un equipo donde se ejecute Windows.  

     Este archivo no se incluye en los medios de instalación de Configuration Manager. Puede descargar este archivo desde el [Centro de descarga de Microsoft](http://go.microsoft.com/fwlink/?LinkID=525184).  

2.  En el equipo Windows, ejecute **ConfigmgrMacClient.msi** para extraer el paquete de cliente Mac, Macclient.dmg, en una carpeta del disco local (de manera predeterminada **C:\Archivos de programa (x86)\Microsoft\System Center 2012 Configuration Manager Mac Client\\**).  

3.  Copie el archivo Macclient.dmg en una carpeta del equipo Mac.  

4.  En el equipo Mac, ejecute el archivo Macclient.dmg para extraer los archivos en una carpeta del disco local.  

5.  En la carpeta, asegúrese de que se extraen los archivos Ccmsetup y CMClient.pkg, y que se creó una carpeta denominada Tools que contiene las herramientas CMDiagnostics, CMUninstall, CMAppUtil y CMEnroll.

    -  **Ccmsetup**: instala el cliente de Configuration Manager en los equipos Mac.  

    -   **CMDiagnostics**: recopila información de diagnóstico relacionada con el cliente de Configuration Manager en los equipos Mac.  

    -   **CMUninstall**: desinstala el cliente de los equipos Mac.  

    -   **CMAppUtil**: convierte paquetes de aplicaciones de Apple en un formato que se pueda implementar como una aplicación de Configuration Manager.  

    -   **CMEnroll**: solicita e instala el certificado de cliente para un equipo Mac, de modo que pueda instalar después el cliente de Configuration Manager.   

## <a name="install-the-client-and-then-enroll-the-client-certificate-on-the-mac"></a>Instalar el cliente e inscribir el certificado de cliente en el equipo Mac  

Puede inscribir clientes individuales con el [Asistente para inscripción de equipos Mac](#enroll-the-client-with-the-mac-computer-enrollment-wizard).

Para la automatización que habilita la inscripción de muchos clientes, use la [herramienta CMEnroll](#client-and-certificate-automation-with-cmenroll).   


###  <a name="enroll-the-client-with-the-mac-computer-enrollment-wizard"></a>Inscribir el cliente mediante el Asistente para inscripción de equipos Mac  

1.  Cuando la instalación del cliente finaliza, se abre el Asistente para inscripción de equipos. Si el asistente no se inicia, o si cierra el asistente involuntariamente, haga clic en **Inscribir** en la página de preferencias de **Configuration Manager** para abrirlo.  

2.  En la segunda página del asistente, proporcione lo siguiente:  

    -   **Nombre de usuario** : el nombre de usuario puede adoptar los siguientes formatos:  

        -   'dominio\nombre'. Por ejemplo: 'contoso\mnorth'  

        -   "user@domain". Por ejemplo: "mnorth@contoso.com"  

            > [!IMPORTANT]  
            >  Si usa una dirección de correo electrónico para rellenar el campo **Nombre de usuario**, Configuration Manager automáticamente usa el nombre de dominio de la dirección de correo electrónico y el nombre predeterminado del servidor de punto de proxy de inscripción para rellenar el campo **Nombre de servidor**. Si el nombre de dominio y el nombre de servidor no coinciden con el nombre del servidor de punto de proxy de inscripción, notifique a los usuarios el nombre correcto que deben usar al realizar la inscripción de equipos Mac.  

         El nombre de usuario y la contraseña correspondiente deben coincidir con una cuenta de usuario de Active Directory a la que se haya concedido permisos de lectura e inscripción en la plantilla de certificado de cliente de Mac.  

    -   **Contraseña**: escriba la contraseña correspondiente del nombre de usuario especificado.  

    -   **Nombre de servidor**: escriba el nombre del servidor de punto de proxy de inscripción.  


### <a name="client-and-certificate-automation-with-cmenroll"></a>Automatización del cliente y el certificado con CMEnroll  

Use este procedimiento para automatizar la instalación del cliente y solicitar e inscribir certificados de cliente con la herramienta CMEnroll. Para ejecutar la herramienta debe tener una cuenta de usuario de Active Directory.

1.  En el equipo Mac, vaya a la carpeta en la que ha extraído el contenido del archivo Macclient.dmg file.  

2.  Escriba la siguiente línea de comandos: **sudo ./ccmsetup**  

3.  Espere hasta que vea el mensaje de **instalación completada** . Aunque el instalador muestra un mensaje que indica que debe reiniciar ahora, no lo haga y continúe con el paso siguiente.  

4.  En la carpeta de herramientas en el equipo Mac, escriba lo siguiente: **sudo ./CMEnroll -s &lt;nombre_de_servidor_proxy_de_inscripción> -ignorecertchainvalidation -u &lt;nombre de usuario'>**  

    Una vez instalado del cliente, se abrirá el asistente para inscripción de equipos Mac que lo ayudará a inscribir el equipo Mac. Para inscribir el cliente mediante este método, consulte [To enroll the client by using the Mac Computer Enrollment Wizard](#BKMK_EnrollR2) en este tema.  

5. Escriba la contraseña de la cuenta de usuario de Active Directory.  Cuando escriba este comando, se le pedirán dos contraseñas: la primera solicitud es para que la cuenta de superusuario ejecute el comando. La segunda es para la cuenta de usuario de Active Directory. Los mensajes de solicitud son idénticos, así que asegúrese de especificar las credenciales en la secuencia correcta.  

    El nombre de usuario puede adoptar los siguientes formatos:  

    -   'dominio\nombre'. Por ejemplo: 'contoso\mnorth'  

    -   "user@domain". Por ejemplo: "mnorth@contoso.com"  

     El nombre de usuario y la contraseña correspondiente deben coincidir con una cuenta de usuario de Active Directory a la que se haya concedido permisos de lectura e inscripción en la plantilla de certificado de cliente de Mac.  

     Ejemplo: si el servidor de punto de proxy de inscripción se denomina **server02.contoso.com** y se concedieron permisos para la plantilla de certificado de cliente Mac a un nombre de usuario de **contoso\mnorth**, escriba lo siguiente: **sudo ./CMEnroll -s server02.contoso.com -ignorecertchainvalidation -u 'contoso\mnorth'**  

    > [!NOTE]  
    >  La inscripción no se llevará a cabo si el nombre de usuario contiene cualquiera de los siguientes caracteres: **&lt;>"+=,**. Obtenga un certificado de fuera de banda con un nombre de usuario que no contenga estos caracteres.  
    >  
    >  Para lograr una perfecta experiencia de usuario, puede crear scripts con los comandos y pasos de la instalación para que los usuarios solo tengan que proporcionar su nombre de usuario y contraseña.  

5.  Espere hasta que vea el mensaje de **inscripción correcta** .  

6.  Para limitar el certificado inscrito a Configuration Manager, en el equipo Mac, abra una ventana de terminal y realice los cambios siguientes:  

    a.  Escriba el comando **sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access**  

    b.  En el cuadro de diálogo **Keychain Access** (Acceso a cadenas de claves), en la sección **Keychains** (Cadenas de claves), seleccione **Sistema** y, después, en la sección **Categoría**, seleccione **Claves**.  

    c.  Expanda los llaveros para ver los certificados de cliente. Una vez identificado el certificado con la clave privada que acaba de instalar, haga doble clic en dicha clave.  

    d.  En la pestaña **Control de acceso**, seleccione **Confirm before allowing access** (Confirmar antes de permitir el acceso).  

    e.  Vaya a **/Library/Application Support/Microsoft/MCC**, elija **CCMClient** y, después, seleccione **Agregar**.  

    f.  Seleccione **Guardar cambios** y cierre el cuadro de diálogo **Keychain Access** (Acceso a cadenas de claves).  

7.  Reinicie el equipo Mac.  

 Compruebe que la instalación de cliente se realizó correctamente. Para ello, abra el elemento **Configuration Manager** en **Preferencias del sistema** en el equipo Mac. También puede actualizar y ver la recopilación **Todos los sistemas** para confirmar que el equipo Mac ahora aparece en esta recopilación como un cliente administrado.  

> [!TIP]  
>  Para resolver problemas con el cliente Mac, puede usar el programa CMDiagnostics que se incluye con el paquete de cliente Mac OS X para recopilar la siguiente información de diagnóstico:  
>   
>  -   Una lista de procesos en ejecución  
> -   La versión del sistema operativo Mac OS X  
> -   Informes de bloqueo de Mac OS X relacionados con el cliente de Configuration Manager, incluidos **CCM\*.crash** y **System Preference.crash**.  
> -   El archivo de lista de materiales (L. Mat) y el archivo de lista de propiedades (.plist) creados por la instalación de cliente de Configuration Manager.  
> -   El contenido de la carpeta /Library/Application Support/Microsoft/CCM/Logs.  
>   
>  La información recopilada por CmDiagnostics se agrega a un archivo ZIP que se guarda en el escritorio del equipo con el nombre cmdiag-*<nombre de host\>***-***&gt;fecha y hora\>*.zip.***


##  <a name="use-a-certificate-request-and-installation-method-that-is-independent-from-configuration-manager"></a>Utilizar una solicitud de certificado y un método de instalación independiente de Configuration Manager  

En primer lugar, realice estas tareas específicas de [Prepararse para implementar software cliente en equipos Mac](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients):

1. [Implementar un certificado de servidor web en servidores del sistema de sitio](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients#deploy-a-web-server-certificate-to-site-system-servers)

2. [Implementar un certificado de autenticación de cliente en servidores del sistema de sitio](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients#deploy-a-client-authentication-certificate-to-site-system-servers)

3. [Configurar el punto de administración y el punto de distribución](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients#configure-the-management-point-and-distribution-point)

4. [Opcional: instalar el punto de servicios de informes](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients#install-the-reporting-services-point)

Después, realice estas tareas:

5. [Descargar los archivos de origen de cliente para equipos Mac](#download-the-client-source-files-for-macs)  
6. Use las instrucciones que acompañan al método de implementación del certificado elegido para solicitar e instalar el certificado de cliente en el equipo Mac.  
7.  Navegue a la carpeta en la que extrajo el contenido del archivo macclient.dmg que descargó desde el Centro de descarga de Microsoft.  

3.  Escriba la siguiente línea de comandos: **sudo ./ccmsetup -MP <FQDN de Internet del punto de administración\> -SubjectName <valor de asunto del certificado\>**.  El valor de asunto del certificado distingue mayúsculas de minúsculas, por tanto escríbalo tal como aparece en los detalles del certificado.  

     Ejemplo: si en las propiedades del sistema de sitio el valor de FQDN de Internet es **server03.contoso.com** y el certificado de cliente de Mac tiene el FQDN de **mac12.contoso.com** como nombre común en el asunto del certificado, escriba: **sudo ./ccmsetup -MP server03.contoso.com -SubjectName mac12.contoso.com**.  

4.  Espere hasta que vea el mensaje de que se **completó la instalación** y, a continuación, reinicie el equipo Mac.  

5.  Para asegurarse de que Configuration Manager tiene acceso a este certificado, en el equipo Mac, abra una ventana de terminal y realice estos cambios:  

    a.  Escriba el comando **sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access**  

    b.  En el cuadro de diálogo **Keychain Access** (Acceso a cadenas de claves), en la sección **Keychains** (Cadenas de claves), seleccione **Sistema** y, después, en la sección **Categoría**, seleccione **Claves**.  

    c.  Expanda los llaveros para ver los certificados de cliente. Una vez identificado el certificado con la clave privada que acaba de instalar, haga doble clic en dicha clave.  

    d.  En la pestaña **Control de acceso**, seleccione **Confirm before allowing access** (Confirmar antes de permitir el acceso).  

    e.  Vaya a **/Library/Application Support/Microsoft/MCC**, elija **CCMClient** y, después, seleccione **Agregar**.  

    f.  Seleccione **Guardar cambios** y cierre el cuadro de diálogo **Keychain Access** (Acceso a cadenas de claves).  

6.  Si tiene más de un certificado que contiene el mismo asunto, debe especificar el número de serie de certificado para identificar el certificado que quiere usar para el cliente de Configuration Manager. Para ello, use el siguiente comando: **sudo defaults write com.microsoft.ccmclient SerialNumber -data "<número de serie\>"**.  

     Por ejemplo: **sudo defaults write com.microsoft.ccmclient SerialNumber -data "17D4391A00000003DB"**  

 Compruebe que la instalación de cliente se ha realizado correctamente. Para ello, abra el elemento **Configuration Manager** en **Preferencias del sistema** en el equipo Mac. También puede actualizar y ver la recopilación **Todos los sistemas** para confirmar que el equipo Mac aparece en esta recopilación como un cliente administrado.  

## <a name="renewing-the-mac-client-certificate"></a>Renovación del certificado de cliente Mac  
 Utilice el siguiente procedimiento antes de renovar el certificado de equipo en los equipos Mac.  

 Este procedimiento quita el SMSID, lo cual es necesario para que el cliente utilice un certificado nuevo o renovado en el equipo Mac.  

> [!IMPORTANT]  
>  Cuando quita y reemplaza el SMSID del cliente, todo el historial del cliente almacenado, como el inventario, se elimina después de eliminar el cliente de la consola de Configuration Manager.  

### <a name="to-renew-the-mac-client-certificate"></a>Para renovar el certificado de cliente Mac  

1.  Cree y rellene una recopilación de dispositivos para los equipos Mac que deben renovar los certificados de equipo.  

2.  En el área de trabajo **Activos y compatibilidad** , inicie el **Asistente para crear elemento de configuración**.  

3.  En la página **General** del asistente, especifique la siguiente información:  

    -   **NombreQuitar SMSID para Mac**:  

    -   **TipoMac OS X**:  

4.  En la página **Plataformas admitidas** del asistente, asegúrese de que se seleccionan todas las versiones de Mac OS X.  

5.  En la página **Configuración** del asistente, haga clic en **Nueva** y, a continuación, en el cuadro de diálogo **Crear configuración** , especifique la información siguiente:  

    -   **NombreQuitar SMSID para Mac**:  

    -   **Tipo de configuraciónscript**:  

    -   **Tipo de datoscadena**:  

6.  En el cuadro de diálogo **Crear configuración** , en **Script de detección**, haga clic en **Agregar script** para especificar un script que detecta equipos Mac con el SMSID configurado.  

7.  En el cuadro de diálogo **Editar script de detección** , escriba el siguiente script de shell:  

    ```  
    defaults read com.microsoft.ccmclient SMSID  
    ```  

8.  Seleccione **Aceptar** para cerrar el cuadro de diálogo **Editar script de detección**.  

9. En el cuadro de diálogo **Crear configuración**, en **Script de corrección (opcional)**, seleccione **Agregar script** para especificar un script que quita el SMSID cuando se encuentra en equipos Mac.  

10. En el cuadro de diálogo **Crear script de corrección** , escriba el siguiente script de shell:  

    ```  
    defaults delete com.microsoft.ccmclient SMSID  
    ```  

11. Seleccione **Aceptar** para cerrar el cuadro de diálogo **Crear script de corrección**.  

12. En la página **Reglas de compatibilidad** del asistente, seleccione **Nueva** y, después, en el cuadro de diálogo **Crear regla**, especifique la información siguiente:  

    -   **NombreQuitar SMSID para Mac**:  

    -   **Configuración seleccionada**: seleccione **Examinar** y, luego, seleccione el script de detección especificado previamente.  

    -   En el campo **los siguientes valores** escriba **El dominio/par predeterminado (com.microsoft.ccmclient, SMSID) no existe**.  

    -   Habilite la opción **Ejecutar el script de corrección especificado cuando esta configuración no sea compatible**.  

13. Complete el Asistente para crear elemento de configuración.  

14. Cree una línea de base de configuración que contenga el elemento de configuración que acaba de crear e impleméntela en la recopilación de dispositivos que creó en el paso 1.  

     Para obtener más información sobre cómo crear e implementar líneas de base de configuración, consulte [How to create configuration baselines in System Center Configuration Manager](../../../compliance/deploy-use/create-configuration-baselines.md) (Cómo crear líneas base de configuración en System Center Configuration Manager).  

15. Después de instalar un nuevo certificado en los equipos Mac a los que se ha quitado el SMSID, ejecute el siguiente comando para configurar el cliente para usar el nuevo certificado:  

    ```  
    sudo defaults write com.microsoft.ccmclient SubjectName -string <Subject_Name_of_New_Certificate>  
    ```  

16. Si tiene más de un certificado que contiene el mismo asunto, debe especificar el número de serie de certificado para identificar el certificado que quiere usar para el cliente de Configuration Manager. Para ello, use el siguiente comando: **sudo defaults write com.microsoft.ccmclient SerialNumber -data "<número de serie\>"**.  

     Por ejemplo: **sudo defaults write com.microsoft.ccmclient SerialNumber -data "17D4391A00000003DB"**  

17. Reiniciar.  


## <a name="see-also"></a>Consulte también

[Mantenimiento de clientes Mac](/sccm/core/clients/manage/maintain-mac-clients)

