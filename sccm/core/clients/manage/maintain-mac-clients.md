---
title: Mantener clientes Mac | Microsoft Docs
description: Tareas de mantenimiento para clientes Mac de Configuration Manager.
ms.custom: na
ms.date: 01/03/2017
ms.prod: configuration-manager
ms.reviewer: aaroncz
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cf6337a2-700c-47f3-b6f8-5814f9b81e59
caps.latest.revision: 12
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: c74b553ab76a2b77b0d893151351132da05a640d
ms.openlocfilehash: 5b75f3296dc20a6766a894f463e958455ca1d65f


---

# <a name="maintain-mac-clients"></a>Mantenimiento de clientes Mac
*Se aplica a: System Center Configuration Manager (Rama actual)*

A continuación se indican procedimientos para desinstalar clientes Mac y para renovar sus certificados.

##  <a name="uninstalling-the-mac-client"></a>Desinstalar el cliente Mac  

1.  En un equipo Mac, abra una ventana de terminal y navegue hasta la carpeta que contiene **macclient.dmg**.  

2.  Navegue hasta la carpeta Tools, y escriba la siguiente línea de comandos:  

     **./CMUninstall -c**  

    > [!NOTE]  
    >  La propiedad **-c** indica a la desinstalación de cliente que también quite los registros de bloqueo y los archivos de registro del cliente. Se recomienda para evitar confusiones si más adelante se vuelve a instalar el cliente.  

3.  Si es necesario, revoque o elimine manualmente el certificado de autenticación de cliente usado por Configuration Manager. CMUnistall no quita ni revoca este certificado.  

##  <a name="renewing-the-mac-client-certificate"></a>Renovación del certificado de cliente Mac  
 Utilice uno de los métodos siguientes para renovar el certificado de cliente Mac:  

-   [Asistente para renovar certificado](#renew-certificate-wizard)  

-   [Renovar el certificado manualmente](#renew-certificate-manually)  

###  <a name="renew-certificate-wizard"></a>Asistente para renovar certificado  

1.  Configure los valores siguientes como *cadenas* en el archivo ccmclient.plist que controla la apertura del Asistente para renovar certificado:  

 -   **RenewalPeriod1**: especifica, en segundos, el primer período de renovación en el que los usuarios pueden renovar el certificado. El valor predeterminado es 3.888.000 segundos (45 días). No configure un valor inferior a 300, ya que el período volverá al valor predeterminado. 

 -   **RenewalPeriod2**: especifica, en segundos, el segundo período de renovación en el que los usuarios pueden renovar el certificado. El valor predeterminado es 259.200 segundos (3 días). Si este valor se configura y es mayor o igual que 300 segundos y menor o igual que **RenewalPeriod1**, se usará el valor. Si **RenewalPeriod1** es mayor que 3 días, se usará un valor de 3 días para **RenewalPeriod2**.  Si **RenewalPeriod1** es menor que 3 días, **RenewalPeriod2** se establecerá en el mismo valor que **RenewalPeriod1**.  

 -   **RenewalReminderInterval1**: especifica, en segundos, la frecuencia con la que se mostrará el Asistente para renovación de certificados a los usuarios durante el primer período de renovación. El valor predeterminado es 86.400 segundos (1 día). Si **RenewalReminderInterval1** es mayor que 300 segundos y menor que el valor configurado para **RenewalPeriod1**, se usará el valor configurado. De lo contrario, se utilizará el valor predeterminado de 1 día.  

 -   **RenewalReminderInterval2**: especifica, en segundos, la frecuencia con la que se mostrará el Asistente para renovación de certificados a los usuarios durante el segundo período de renovación. El valor predeterminado es 28.800 segundos (8 horas). Si **RenewalReminderInterval2** es mayor que 300 segundos y menor o igual que **RenewalReminderInterval1** , y menor o igual que **RenewalPeriod2**, se usará el valor configurado. De lo contrario, se usará un valor de 8 horas.  

     **Ejemplo** : si se mantienen los valores predeterminados, 45 días antes de que expire el certificado, el asistente se abrirá cada 24 horas.  A los 3 días de que expire el certificado, el asistente se abrirá cada 8 horas.  

     **Ejemplo** : use la siguiente línea de comandos, o un script, para establecer el valor del primer período de renovación en 20 días.  

     `sudo defaults write com.microsoft.ccmclient RenewalPeriod1 1728000`  

2.  Habitualmente, cuando se abre el Asistente para renovar certificado, los campos **Nombre de usuario** y **Nombre de servidor** se rellenan automáticamente y el usuario solo puede escribir la contraseña para renovar el certificado.  

    > [!NOTE]  
    >  Si el asistente no se inicia, o si cierra el asistente involuntariamente, haga clic en **Renovar** en la página de preferencias de **Configuration Manager** para iniciarlo.  

###  <a name="renew-certificate-manually"></a>Renovar el certificado manualmente  
 El período de validez normal de un certificado de cliente de Mac es 1 año Configuration Manager no renueva automáticamente el certificado de usuario que solicita durante la inscripción, por lo que deberá realizar el siguiente procedimiento para renovarlo manualmente.  

> [!IMPORTANT]  
>  Si el certificado expira, debe desinstalarlo, reinstalarlo y, a continuación, volver a inscribir el cliente Mac.  

 Este procedimiento quita el SMSID, lo cual es necesario para solicitar un nuevo certificado para el mismo equipo Mac. Cuando quita y reemplaza el SMSID del cliente, todo el historial del cliente almacenado, como el inventario, se elimina después de eliminar el cliente de la consola de Configuration Manager.  

1.  Cree y rellene una recopilación de dispositivos para los equipos Mac que deben renovar los certificados de usuario.  

    > [!WARNING]  
    >  Configuration Manager no supervisa el periodo de validez del certificado que inscribe para los equipos Mac. Debe supervisarlo independientemente de Configuration Manager para identificar los equipos Mac que se van a agregar a esta recopilación.  

2.  En el área de trabajo **Activos y compatibilidad** , inicie el **Asistente para crear elemento de configuración**.  

3.  En la página **General** , especifique la siguiente información:  

    -   **NombreQuitar SMSID para Mac**:  

    -   **TipoMac OS X**:  

4.  En la página **Plataformas admitidas**, asegúrese de que están seleccionadas todas las versiones de Mac OS X.  

5.  En la página **Configuración**, seleccione **Nueva** y, después, en el cuadro de diálogo **Crear configuración**, especifique la información siguiente:  

    -   **NombreQuitar SMSID para Mac**:  

    -   **Tipo de configuraciónscript**:  

    -   **Tipo de datoscadena**:  

6.  En el cuadro de diálogo **Crear configuración**, en **Script de detección**, seleccione **Agregar script** para especificar un script que detecta equipos Mac con el SMSID configurado.  

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

12. En la página **Reglas de compatibilidad** del asistente, haga clic en **Nueva**y, a continuación, en el cuadro de diálogo **Crear regla** , especifique la información siguiente:  

    -   **NombreQuitar SMSID para Mac**:  

    -   **Configuración seleccionada**: seleccione **Examinar** y, luego, seleccione el script de detección especificado previamente.  

    -   En el campo **los siguientes valores** escriba **The domain/default pair of (com.microsoft.ccmclient, SMSID) does not exist**.  

    -   Habilite la opción **Ejecutar el script de corrección especificado cuando esta configuración no sea compatible**.  

13. Complete el Asistente para crear elemento de configuración.  

14. Cree una línea base de configuración que contenga el elemento de configuración que acaba de crear e impleméntela en la recopilación de dispositivos que creó en el paso 1.  

     Para obtener más información sobre cómo crear e implementar líneas de base de configuración, consulte [How to create configuration baselines in System Center Configuration Manager](../../../compliance/deploy-use/create-configuration-baselines.md) (Cómo crear líneas base de configuración en System Center Configuration Manager) y [How to deploy configuration baselines in System Center Configuration Manager](../../../compliance/deploy-use/deploy-configuration-baselines.md) (Cómo implementar líneas base de configuración en System Center Configuration Manager).  

15. En equipos Mac que tienen el SMSID quitado, ejecute el comando siguiente para instalar un certificado nuevo:  

    ```  
    sudo ./CMEnroll -s <enrollment_proxy_server_name> -ignorecertchainvalidation -u <'user name'>  
    ```  

     Cuando se le solicite, proporcione la contraseña de la cuenta de superusuario para ejecutar el comando y, a continuación, la contraseña de la cuenta de usuario de Active Directory.  

16. Para limitar el certificado inscrito a Configuration Manager, en el equipo Mac, abra una ventana de terminal y realice los cambios siguientes:  

    a.  Escriba el comando **sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access**  

    b.  En el cuadro de diálogo **Keychain Access** (Acceso a cadenas de claves), en la sección **Keychains** (Cadenas de claves), seleccione **Sistema** y, después, en la sección **Categoría**, seleccione **Claves**.  

    c.  Expanda los llaveros para ver los certificados de cliente. Una vez identificado el certificado con la clave privada que acaba de instalar, haga doble clic en dicha clave.  

    d.  En la pestaña **Control de acceso**, seleccione **Confirm before allowing access** (Confirmar antes de permitir el acceso).  

    e.  Vaya a **/Library/Application Support/Microsoft/MCC**, elija **CCMClient** y, después, seleccione **Agregar**.  

    f.  Seleccione **Guardar cambios** y cierre el cuadro de diálogo **Keychain Access** (Acceso a cadenas de claves).  

17. Reinicie el equipo Mac.  




<!--HONumber=Jan17_HO1-->


