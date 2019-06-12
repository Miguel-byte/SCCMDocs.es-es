---
title: Solución de problemas del cliente de Windows Defender o Endpoint Protection
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo solucionar problemas con Windows Defender y Endpoint Protection.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: d837253e-fcc2-422a-9e2c-c78b938dfd8c
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4a8f1ca1484df0480a7923a8d3de64c1670aec6d
ms.sourcegitcommit: a6a6507e01d819217208cfcea483ce9a2744583d
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/06/2019
ms.locfileid: "66748194"
---
# <a name="troubleshooting-windows-defender-or-endpoint-protection-client"></a>Solución de problemas del cliente de Windows Defender o Endpoint Protection

*Se aplica a: System Center Configuration Manager (Rama actual)*


Si tiene problemas con Windows Defender o Endpoint Protection, póngase en contacto con el administrador de seguridad para obtener soporte técnico. También puede intentar solucionar los problemas siguientes:  

-   [Actualizar Windows Defender o Endpoint Protection](#update-windows-defender-or-endpoint-protection)  
-   [Iniciar el servicio de Windows Defender o Endpoint Protection](#starting-windows-defender-or-endpoint-protection-service)  
-   [Problemas de conexión de Internet](#internet-connection-issues)  
-   [No se puede corregir una amenaza detectada](#detected-threat-cant-be-remediated)  
-   [Instalar el cliente de Endpoint Protection](#install-the-endpoint-protection-client)  

##  <a name="update-windows-defender-or-endpoint-protection"></a>Actualizar Windows Defender o Endpoint Protection  
 Windows Defender o Endpoint Protection funciona automáticamente con Microsoft Update para garantizar que las definiciones de virus y spyware se mantengan actualizadas.  

 **Síntomas**  

 Este artículo trata los problemas comunes con las actualizaciones automáticas, incluidas las siguientes situaciones:  

- Ve mensajes de error que indican que se produjeron errores en las actualizaciones.  

- Al buscar actualizaciones, recibe un mensaje de error de que las actualizaciones de definiciones de virus y spyware no se pueden comprobar, descargar o instalar.  

- Incluso si está conectado a Internet, se produce un error en las actualizaciones.  

- Las actualizaciones no se instalan automáticamente según la programación.  

  **Causa**  

  Las causas más comunes de problemas de actualización son problemas con la conectividad a Internet. Sin embargo, si sabe que está conectado a Internet ya que puede ir a otros sitios web, el problema podría deberse a conflictos con la configuración de Windows Internet Explorer.  

> [!IMPORTANT]  
>  Tiene que salir de Internet Explorer para completar estos pasos. Por lo tanto, imprímalos, anótelos, o cópielos en otro archivo y, a continuación, agregue este tema a marcadores para poder acceder a él más adelante.  

### <a name="step-1-reset-your-internet-explorer-settings"></a>Paso 1: restablecer la configuración de Internet Explorer  

1.  Cierre todos los programas abiertos, incluido Internet Explorer.  

    > [!NOTE]  
    >  El restablecimiento de esta configuración en Internet Explorer elimina los archivos temporales, las cookies, el historial de exploración y las contraseñas en línea. Sin embargo, no se eliminan los favoritos.  

2.  Haga clic en **Inicio** , busque **inetcpl.cpl**y luego presione **Entrar**.  

3.  En el cuadro de diálogo de **Opciones de Internet** , haga clic en la ficha **Opciones avanzadas** .  

4.  En **Restablecer configuración de Internet Explorer**, haga clic en **Restablecer**, y, a continuación, haga clic en **Restablecer** nuevamente.  

5.  Espere hasta que Internet Explorer termine de restablecer la configuración y, a continuación, haga clic en **Aceptar**.  

6.  Abra Internet Explorer.  

7.  Abra Microsoft Security Essentials, haga clic en la ficha **Actualizar** , y, a continuación, haga clic en **Actualizar**.  

8.  Si el problema persiste, continúe con el paso siguiente.  

### <a name="step-2-set-internet-explorer-as-the-default-browser"></a>Paso 2: establecer Internet Explorer como el explorador predeterminado  

1.  Cierre todos los programas abiertos, incluido Internet Explorer.  

2.  Haga clic en **Inicio** , busque **inetcpl.cpl**y luego presione **Entrar**.  

3.  En el cuadro de diálogo **Opciones de Internet** , haga clic en la ficha **Programas** .  

4.  En **Explorador web predeterminado**, haga clic en **Predeterminar**.  

5.  Haga clic en **Aceptar**.  

6.  Abrir Windows Defender o Endpoint Protection Haga clic en la ficha **Actualizar** y, a continuación, haga clic en **Actualizar**.  

7.  Si el problema persiste, continúe con el paso siguiente.  

### <a name="step-3-ensure-that-the-date-and-time-are-set-correctly-on-your-computer"></a>Paso 3: asegurarse de que la fecha y la hora están establecidas correctamente en el equipo  

1.  Abrir Windows Defender o Endpoint Protection  

2.  Si el mensaje de error recibido contiene el código 0x80072f8f, el problema se debe probablemente a una fecha incorrecta o al valor de tiempo en el equipo.  

3.  Para restablecer el valor de fecha y hora del equipo, siga los pasos de [Fix broken desktop shortcuts and common system maintenance tasks](http://go.microsoft.com/fwlink/?LinkId=155579) (Corregir accesos directos de escritorio rotos y tareas comunes de mantenimiento del sistema) (http://go.microsoft.com/fwlink/?LinkId=155579).  

### <a name="step-4-rename-the-software-distribution-folder-on-your-computer"></a>Paso 4: cambiar el nombre de la carpeta SoftwareDistribution en el equipo  

1. Detener el servicio de actualizaciones automáticas  

    1.  Haga clic en **Inicio** , busque **services.msc**y luego haga clic en **Aceptar**.  

    2.  Haga clic con el botón secundario en **Servicio de actualizaciones automáticas**, y, a continuación, haga clic en **Detener**.  

    3.  Minimice el complemento Servicios.  

2.  Cambie el nombre del directorio **SoftwareDistribution** de la forma siguiente:  

    1.  Haga clic en **Inicio** , busque  **cmd**y luego haga clic en **Aceptar**.  

    2.  Escriba **cd %windir%** y presione **Entrar**.  

    3.  Escriba **ren SoftwareDistribution SDTemp**y presione **Entrar**.  

    4.  Escriba **exit**y presione **Entrar**.  

3.  Inicie el Servicio de actualizaciones automáticas de la forma siguiente:  

    1.  Minimice el complemento Servicios.  

    2.  Haga clic con el botón secundario en **Servicio de actualizaciones automáticas**, y, a continuación, haga clic en **Iniciar**.  

    3.  Cierre la ventana del complemento Servicios.  

### <a name="step-5-reset-the-microsoft-antivirus-update-engine-on-your-computer"></a>Paso 5: restablecer el motor de actualización de antivirus de Microsoft en el equipo  

1.  Haga clic en **Inicio** , busque  **cmd**y luego haga clic en **Aceptar**. A continuación, haga clic con el botón derecho en **Símbolo del sistema**y seleccione **Ejecutar como administrador**.  

2.  En la ventana del **Símbolo del sistema** , escriba los comandos siguientes y presione **Entrar** después de cada comando:  

     **Cd\\**  

     **Cd program files\windows defender**  

     **Mpcmdrun -RemoveDefinitions -all**  

     **Salir**  

3.  Reinicie su equipo.  

4.  Abra Windows Defender o  
          Endpoint Protection, haga clic en la pestaña **Actualizar** y luego en **Actualizar**.  

5.  Si el problema persiste, continúe con el paso siguiente.  

### <a name="step-6-manually-install-the-virus-and-spyware-definition-updates"></a>Paso 6: instalar manualmente las actualizaciones de definiciones de virus y spyware  

-   [Descargue las últimas actualizaciones manualmente](https://www.microsoft.com/wdsi/definitions/).  


### <a name="step-7-contact-support"></a>Paso 7: ponerse en contacto con el servicio de soporte técnico  

-   Si no se resuelve el problema siguiendo los pasos, póngase en contacto con el soporte técnico. Para obtener más información, consulte la [asistencia al cliente](https://support.microsoft.com/contactus/).  

##  <a name="starting-windows-defender-or-endpoint-protection-service"></a>Iniciar el servicio de Windows Defender o Endpoint Protection  
 **Síntoma**  

 Recibe un mensaje que le notifica que **Windows Defender o Endpoint Protection no está supervisando el equipo porque se detuvo el servicio del programa. Debe reiniciarlo ahora.** 

 **Solución**  

### <a name="step-1-restart-your-computer"></a>Paso 1: reiniciar el equipo.  

-   Cierre todas las aplicaciones y reinicie el equipo.  

### <a name="step-2-make-sure-the-windows-defender-or-endpoint-protection-service-is-set-to-automatic-and-is-started"></a>Paso 2: asegurarse de que el servicio "Windows Defender" o "Endpoint Protection" está establecido en automático y se inicia  

1.  Haga clic en **Inicio** , busque **services.msc**y luego presione **Entrar**.  

2.  Busque **Microsoft Antimalware Service**. Haga clic con el botón secundario y seleccione **Propiedades** o haga doble clic para abrir el servicio.  

3.  Asegúrese de que "**Tipo de inicio**" esté establecido en "**Automático**".  

4.  Haga clic en el botón **Iniciar** para iniciar el servicio. Si el botón **Iniciar** no está disponible, haga clic en el botón **Detener** y, a continuación, en el botón **Iniciar** para reiniciar el servicio.  

5.  Asegúrese de anotar los errores que puedan aparecer durante este proceso, envíe un caso en línea e incluya la información de los errores.  

### <a name="step-3-remove-any-existing-internet-security-programs"></a>Paso 3: Quitar cualquier programa de seguridad de Internet existente  

1.  Haga clic en **Inicio** , busque **appwiz.cpl**y luego presione **Entrar**.  

2.  En la lista de programas instalados, desinstale cualquier programa de seguridad de Internet de otro fabricante.*  

3.  Reinicie el equipo y después intente instalar Windows Defender o  
          Endpoint Protection de nuevo.  

> [!NOTE]  
>  Algunas aplicaciones de seguridad de Internet no se desinstalan completamente. Es posible que tenga que descargar y ejecutar una utilidad de limpieza de la aplicación de seguridad anterior para que se quite por completo.  

> [!CAUTION]  
> Cuando quite programas de seguridad de Internet, el equipo quedará desprotegido. Si tiene problemas para instalar Windows Defender después de quitar los programas de seguridad existentes, póngase en contacto con el [soporte técnico de Microsoft](https://support.microsoft.com/supportforbusiness/productselection) para **Windows Defender** de la familia de productos de **Seguridad**.  

### <a name="step-4-uninstallreinstall-endpoint-protection"></a>Paso 4: desinstalar y reinstalar Endpoint Protection  

1.  Haga clic en **Inicio** , busque **appwiz.cpl**y luego presione **Entrar**.  

2.  En la lista de programas instalados, haga clic en **Endpoint Protection**y desinstálelo.  

3.  Si se le solicita, reinicie el equipo y después intente instalar Endpoint Protection de nuevo.  

##  <a name="internet-connection-issues"></a>Problemas de conexión de Internet  
 Con el fin de asegurarse de que el equipo recibe las actualizaciones más recientes de Windows Update, debe estar conectado a Internet.  

### <a name="step-1-verify-that-your-computer-is-connected-to-the-internet"></a>Paso 1: Comprobar que el equipo está conectado a Internet  

1.  Haga clic en **Inicio**, busque **ncpa.cpl**y luego presione **Entrar**.  

2.  Haga clic con el botón secundario en el nombre de la conexión y, a continuación, haga clic en **Estado**.  

3.  Si el equipo está conectado, en Windows XP el estado de la conexión aparecerá como **Conectado**, **Habilitado**o **Autenticación** se realizó correctamente. En Windows Vista y Windows 7, el estado de **IPv4** aparecerá como **Internet**.  

4.  Si el equipo no parece estar conectado, haga clic en el nombre de la conexión y, a continuación, haga clic en **Conectar**, **Habilitar**, **Autenticar**o **Reparar**.  

### <a name="step-3-restart-your-computer"></a>Paso 3: reiniciar el equipo  

-   Cierre todos los programas abiertos y reinicie el equipo.  

### <a name="step-4-if-you-still-cant-connect-to-the-internet-check-your-connections"></a>Paso 4: Si sigue sin poder conectarse a Internet, comprobar las conexiones  

1.  Si usa una conexión de acceso telefónico, asegúrese de que la conexión del cable telefónico en el conector de la pared y en el módem estén bien conectadas.  

2.  Si usa un módem por cable, asegúrese de que la conexión del cable al módem y la conexión del módem al equipo estén bien conectadas.  

3.  Si usa un módem por cable o un enrutador DSL, asegúrese de que las conexiones con el enrutador y con el equipo estén bien conectadas. Pruebe a desconectar y apagar el enrutador y el módem. Espere unos minutos, conecte el módem en primer lugar, espere un minuto y, a continuación, conecte el enrutador y reinicie el equipo.  

##  <a name="detected-threat-cant-be-remediated"></a>No se puede corregir una amenaza detectada  
 Cuando Windows Defender o Endpoint Protection detecta una posible amenaza que se oculta en un archivo comprimido con la extensión de nombre de archivo .zip o dentro de un recurso compartido de red, intenta hacerle frente a la amenaza poniéndola en cuarentena o eliminándola.  

### <a name="remove-or-scan-the-file"></a>Quitar o examinar el archivo  

-   Si la amenaza detectada estaba en un archivo .zip, busque el archivo y quítelo o examínelo al hacer clic en él con el botón derecho y seleccionar **Examinar con Windows Defender** o **Examinar con Endpoint Protection**. Si Windows Defender o Endpoint Protection detecta amenazas adicionales en el archivo, las notifica y permite elegir una acción apropiada.  

-   Si la amenaza detectada estaba en un recurso compartido de red, búsquelo y examínelo al hacer clic en él con el botón derecho y seleccionar **Examinar con Windows Defender** o **Examinar con Endpoint Protection**. Si Windows Defender o Endpoint Protection detecta amenazas adicionales en el recurso compartido de red, las notifica y permite elegir una acción apropiada.  

-   Si no está seguro del origen del archivo, una de las mejores soluciones es ejecutar un examen completo del equipo. Un examen completo puede tardar tiempo en completarse, pero permite que Windows Defender o Endpoint Protection busque el origen de la infección y la limpie.  

##  <a name="install-the-endpoint-protection-client"></a>Instalar el cliente de Endpoint Protection  

> [!NOTE]  
>  En equipos que ejecutan Windows 10, Windows Defender se instala con el sistema operativo.  

 **Síntomas**  

 La instalación no puede realizarse por una razón desconocida o recibe un mensaje de error con un código de error, como 0x80070643, 0X8007064A, 0x8004FF2E, 0x8004FF01, 0x8004FF07, 0x80070002, 0x8007064C, 0x8004FF00, 0x80070001, 0x80070656, 0x8004FF40, 0xC0000156, 0x8004FF41 0x8004FF0B, 0x8004FF11, 0x80240022, 0x8004FF04, 0x80070660, 0x800106B5, 0x80070715, 0x80070005, 0x8004EE00, 0x8007003, 0x800B0100, 0x8007064E o 0x8007007E.  

 Si se está ejecutando Windows XP Service Pack 2 (SP2) en el equipo, puede aparecer alguno de los siguientes mensajes de error:  

- Falta un paquete acumulativo del administrador de filtros en el Asistente para instalación, necesario para completar la instalación.  

- KB914882 Error de instalación, el programa de instalación no puede actualizar los archivos de Windows XP porque el idioma instalado en su sistema es diferente del idioma de actualización.  

  **Causa**  

  Endpoint Protection no se puede instalar en un equipo que ejecuta otros programas de seguridad. A veces, incluso aunque quite los demás programas de seguridad, no se desinstalan por completo. Para instalar Endpoint Protection, debe contar con una versión original del sistema operativo Windows.  

  **Solución**  

> [!IMPORTANT]  
>  Mientras resuelve este problema, tendrá que reiniciar el equipo. Marque esta página (como Favorita) para que resulte más fácil encontrar este tema de nuevo, o imprímala para facilitar su posterior referencia.  

### <a name="step-1-remove-any-existing-security-programs"></a>Paso 1: quitar cualquier programa de seguridad existente  
**Solo Endpoint Protection**

1.  Desinstale completamente todo programa de seguridad de Internet existente.  

2.  Reinicie su equipo.  

3.  Instale Endpoint Protection de nuevo. Si así no se resuelve el problema continúe en el siguiente paso.  

### <a name="step-2-ensure-that-the-windows-installer-service-is-running"></a>Paso 2: asegurarse de que el servicio Windows Installer está en ejecución  

1.  Haga clic en **Inicio** , busque **services.msc**y luego presione **Entrar**.  

2.  Haga clic con el botón secundario en **Windows Installer**y, a continuación, haga clic en **Iniciar**. Si **Iniciar** no está disponible y las opciones **Detener** y **Reiniciar** sí, esto indica que el servicio ya se ha iniciado.  

3.  En la página **Servicios** , en el menú **Archivo** , haga clic en **Salir**.  

4.  Haga clic en **Inicio** y busque **Símbolo del sistema**. Haga clic con el botón secundario en **Símbolo del sistema**y haga clic en **Ejecutar como administrador**.  

5.  Escriba **MSIEXEC /REGSERVER**, y presione **Entrar**.  

    > [!NOTE]  
    >  No hay ninguna indicación de que este comando ha sido correcto o erróneo.  

6.  Instale Endpoint Protection de nuevo. Si así no se resuelve el problema continúe en el siguiente paso.  

### <a name="step-3-start-windows-in-selective-startup-mode"></a>Paso 3: iniciar Windows en el modo Inicio selectivo  

1.  Haga clic en **Inicio** , busque **msconfig**y luego presione **Entrar**.  

2.  En la pestaña **General** haga clic en **Inicio selectivo**y desactive la casilla **Cargar elementos de inicio** .  

3.  En la ficha **Servicios** , active la casilla **Ocultar todos los servicios de Microsoft** y, a continuación, desactive todas las casillas de los servicios que permanecen en la lista.  

4.  Haga clic en **Aceptar**y, a continuación, haga clic en **Reiniciar** para reiniciar el equipo.  

5.  Trate de instalar Endpoint Protection de nuevo.  



### <a name="see-also"></a>Consulte también  
 [Preguntas más frecuentes sobre el cliente de Endpoint Protection](../../protect/deploy-use/endpoint-protection-client-faq.md)   

 [Ayuda del cliente Endpoint Protection](../../protect/deploy-use/endpoint-protection-client-help.md)
