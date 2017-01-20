---
title: Comprobador de requisitos previos | System Center Configuration Manager
description: "Obtenga información sobre cómo usar el comprobador de requisitos previos para identificar y corregir problemas que bloquearían un sitio real o la instalación del rol de sistema de sitio."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aaf13bb8-4ba2-4bd7-9fac-d36a9d88a1b6
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 4c2322ed0805b5f087409ec487ebec9d7c4f10d5

---
# <a name="prerequisite-checker-for-system-center-configuration-manager"></a>Comprobador de requisitos previos para System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*


 Antes de ejecutar el programa de instalación para instalar o actualizar un sitio de System Center Configuration Manager, o antes de instalar un rol de sistema de sitio en un servidor nuevo, puede usar esta aplicación independiente (**Prereqchk.exe**) de la versión de Configuration Manager que desea usar para comprobar la disponibilidad del servidor. El uso del Comprobador de requisitos previos permite identificar y corregir problemas que bloquearían un sitio real o la instalación del rol de sistema de sitio.  

> [!NOTE]  
>  La comprobación de requisitos previos siempre se ejecuta como parte del programa de instalación.  

De forma predeterminada, cuando se ejecuta el Comprobador de requisitos previos:  

-   Se valida el servidor en el que se ejecuta  

-   Se analiza el equipo local para detectar un servidor de sitio existente, y solo se ejecutan las comprobaciones aplicables al sitio  

-   Si no se detecta ningún sitio existente, se ejecutan todas las reglas de requisitos previos  

-   Comprueba las reglas para asegurarse de que el software y la configuración necesarios para la instalación están instalados. Es posible que el software necesario requiera configuraciones adicionales o actualizaciones de software que el Comprobador de requisitos previos no comprobó  

-   Se registran los resultados en el archivo de **ConfigMgrPrereq.log** en la unidad del sistema del equipo. El archivo de registro puede contener información adicional que no se muestra en la interfaz de usuario.  

Al ejecutar el Comprobador de requisitos previos en el símbolo del sistema y especificar opciones de línea de comandos determinadas:  

-   El Comprobador de requisitos previos solo realiza las comprobaciones que están asociadas con el servidor de sitio o los sistemas de sitio que especificó en la línea de comandos  

-   Para comprobar un equipo remoto, la cuenta de usuario debe tener derechos administrativos en el equipo remoto  

Para obtener más información sobre las comprobaciones que lleva a cabo el Comprobador de requisitos previos, consulte [List of Prerequisite Checks for System Center Configuration Manager](../../../../core/servers/deploy/install/list-of-prerequisite-checks.md) (Lista de comprobaciones de requisitos previos de System Center Configuration Manager).  

## <a name="copy-prerequisite-checker-files-to-another-computer"></a>Copiar los archivos del Comprobador de requisitos previos a otro equipo  

1.  En el Explorador de Windows, examine una de las siguientes ubicaciones:  

    -   **&lt;ConfigMgrInstallationMedia\>\SMSSETUP\BIN\X64**  

    -   **&lt;ConfigMgrInstallationPath\>\BIN\X64**  

2.  Copie los archivos siguientes a la carpeta de destino del otro equipo:  

    -   Prereqchk.exe  

    -   Prereqcore.dll  

    -   Basesql.dll  

    -   Basesvr.dll  

    -   Baseutil.dll  

##  <a name="run-prerequisite-checker-with-default-checks"></a>Ejecute el Comprobador de requisitos previos con las comprobaciones predeterminadas  

1.  En el Explorador de Windows, examine una de las siguientes ubicaciones:  

    -   **&lt;ConfigMgrInstallationMedia\>\SMSSETUP\BIN\X64**  

    -   **&lt;ConfigMgrInstallationPath\>\BIN\X64**  

2.  Abra **prereqchk.exe** para iniciar el Comprobador de requisitos previos.   
    El Comprobador de requisitos previos detecta los sitios existentes y, si los encuentra, realiza comprobaciones de preparación para la actualización. En cambio, si no encuentra ningún sitio, se realizan todas las comprobaciones. En la columna **Tipo de sitio** se ofrece información sobre el servidor de sitio o el sistema de sitio con que está asociada la regla.  

##  <a name="run-prerequisite-checker-from-a-command-prompt-for-all-default-checks"></a>Ejecute el Comprobador de requisitos previos desde el símbolo del sistema para todas las comprobaciones predeterminadas  

1.  Abra una ventana del símbolo del sistema y cambie los directorios a una de las siguientes ubicaciones:  

    -   **&lt;ConfigMgrInstallationMedia\>\SMSSETUP\BIN\X64**  

    -   **&lt;ConfigMgrInstallationPath\>\BIN\X64**  

2.  Escriba  **prereqchk.exe /LOCAL** para iniciar el Comprobador de requisitos previos y ejecutar todas las comprobaciones de requisitos previos en el servidor.  

## <a name="run-prerequisite-checker-from-a-command-prompt-for-specified-options"></a>Ejecute el Comprobador de requisitos previos desde el símbolo del sistema para todas las opciones especificadas  

1.  Abra una ventana del símbolo del sistema y cambie los directorios a una de las siguientes ubicaciones:  

    -   **&lt;ConfigMgrInstallationMedia\>\SMSSETUP\BIN\X64**  

    -   **&lt;ConfigMgrInstallationPath\>\BIN\X64**  

2.  Escriba **prereqchk.exe** agregando una o varias de las siguientes opciones de línea de comandos.  

    Por ejemplo, para comprobar un sitio principal podría usar lo siguiente:  

    -   **prereqchk.exe [/NOUI] /PRI /SQL &lt;FQDN de SQL Server\> /SDK &lt;FQDN del proveedor de SMS\> [/JOIN &lt;FQDN del sitio de administración central\>] [/MP &lt;FQDN del punto de administración\>] [/DP &lt;FQDN del punto de distribución\>]**  

    **Servidor del sitio de administración central:**  

    -   **/NOUI**  

         No requerido: inicia el Comprobador de requisitos previos sin mostrar la interfaz de usuario. Debe especificar esta opción antes que cualquier otra opción en la línea de comandos.  

    -   **/CAS**  

         Requerido: comprueba que el equipo local cumple los requisitos para el sitio de administración central.  

    -   **/SQL &lt;*FQDN de SQL Server*>**  

         Necesario: comprueba que el equipo especificado cumple los requisitos de SQL Server para hospedar la base de datos del sitio de Configuration Manager.  

    -   **/SDK &lt;*FQDN de proveedor de SMS*>**  

         Requerido: comprueba que el equipo especificado cumple los requisitos del proveedor de SMS.  

    -   **/Ssbport**  

         No requerido: comprueba que existe una excepción de firewall para permitir la comunicación en el puerto de SSB. El número de puerto predeterminado es 4022.  

    -   **InstallDir &lt;*ConfigMgrInstallationPath*>**  

         No requerido: comprueba el espacio mínimo en disco requerido para la instalación del sitio.  

    **Servidor de sitio primario:**  

    -   **/NOUI**  

        No requerido: inicia el Comprobador de requisitos previos sin mostrar la interfaz de usuario. Debe especificar esta opción antes que cualquier otra opción en la línea de comandos.  

    -   **/PRI**  

         Requerido: comprueba que el equipo local cumple los requisitos del sitio principal.  

    -   **/SQL &lt;*FQDN de SQL Server*>**  

         Necesario: comprueba que el equipo especificado cumple los requisitos de SQL Server para hospedar la base de datos del sitio de Configuration Manager.  

    -   **/SDK &lt;*FQDN de proveedor de SMS*>**  

         Requerido: comprueba que el equipo especificado cumple los requisitos del proveedor de SMS.  

    -   **/JOIN &lt;*FQDN del sitio de administración central*>**  

         No requerido: comprueba que el equipo local cumple los requisitos para la conexión al servidor de sitio de administración central.  

    -   **/MP &lt;*FQDN del punto de administración*>**  

         No requerido: comprueba que el equipo especificado cumple los requisitos del rol de sistema de sitio de punto de administración. Esta opción solo se admite cuando se usa la opción **/PRI** .  

    -   **/DP &lt;*FQDN del punto de distribución*>**  

         No requerido: comprueba que el equipo especificado cumple los requisitos del rol de sistema de sitio de punto de distribución. Esta opción solo se admite cuando se usa la opción **/PRI** .  

    -   **/Ssbport**  

         No requerido: comprueba que existe una excepción de firewall para permitir la comunicación en el puerto de SSB. El número de puerto predeterminado es 4022.  

    -   **InstallDir &lt;*ConfigMgrInstallationPath*>**  

         No requerido: comprueba el espacio mínimo en disco requerido para la instalación del sitio.  

    **Servidor de sitio secundario:**  

    -   **/NOUI**  

         No requerido: inicia el Comprobador de requisitos previos sin mostrar la interfaz de usuario. Debe especificar esta opción antes que cualquier otra opción en la línea de comandos.  

    -   **/SEC &lt;*FQDN del servidor de sitio secundario*>**  

         Requerido: comprueba que el equipo especificado cumple los requisitos del sitio secundario.  

    -   **/INSTALLSQLEXPRESS**  

         No requerido: comprueba que SQL Server Express puede instalarse en el equipo especificado.  

    -   **/Ssbport**  

         No es necesario:      
        Comprueba que existe una excepción de firewall para permitir la comunicación del puerto de SQL Server Service Broker (SSB). El número de puerto predeterminado es 4022.  

    -   **/Sqlport**  

         No requerido: comprueba que existe una excepción de firewall para permitir la comunicación del puerto de servicio de SQL Server y que ninguna otra instancia con nombre de SQL Server utiliza el puerto. El puerto predeterminado es 1433.  

    -   **InstallDir &lt;*ConfigMgrInstallationPath*>**  

         No requerido: comprueba el espacio mínimo en disco requerido para la instalación del sitio.  

    -   **/SourceDir**  

         No requerido: comprueba que la cuenta de equipo del sitio secundario puede tener acceso a la carpeta que hospeda los archivos de origen del programa de instalación.  

     **Consola de Configuration Manager:**  

    -   **/Adminui**  

         Requerido: comprueba que el equipo local cumple los requisitos para instalar el Configuration Manager.  

3.  En la interfaz de usuario del Comprobador de requisitos previos, el Comprobador de requisitos previos crea una lista de los problemas detectados en la sección **Resultado de requisitos previos** .  

    -   Haga clic en un elemento de la lista para obtener más información acerca de cómo resolver el problema.  

    -   Debe resolver todos los elementos de la lista que tengan un estado de **Error** antes de instalar el servidor de sitio, el sistema de sitio o la consola de Configuration Manager.  

    -   También puede abrir el archivo **ConfigMgrPrereq.log** en la raíz de la unidad del sistema para revisar los resultados del Comprobador de requisitos previos. El archivo de registro puede contener información adicional que no se muestra en la interfaz de usuario.  



<!--HONumber=Nov16_HO1-->


