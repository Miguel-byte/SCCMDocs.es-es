---
title: "Asistente para la instalación | Microsoft Docs"
ms.custom: na
ms.date: 7/24/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1f703376-5f2c-4fd2-8209-7028c931ddc7
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: HT
ms.sourcegitcommit: 5945abb49fe06c59355805aa94b04d0d445ecbc3
ms.openlocfilehash: 678f1b35fe6f7649dacb766f7c671f4ec8ea1435
ms.contentlocale: es-es
ms.lasthandoff: 07/24/2017

---
# <a name="use-the-setup-wizard-to-install-system-center-configuration-manager-sites"></a>Use el Asistente para instalación si quiere instalar sitios de System Center Configuration Manager.

*Se aplica a: System Center Configuration Manager (rama actual)*


Para instalar un nuevo sitio de System Center Configuration Manager mediante una interfaz de usuario interactiva, use el Asistente para instalación de Configuration Manager (setup.exe). El asistente admite la instalación de un sitio primario o un sitio de administración central. También se usa para [actualizar una instalación de evaluación](../../../../core/servers/deploy/install/upgrade-an-evaluation-install-to-a-full-install.md) de Configuration Manager a una instalación con licencia completa. Si no quiere usar el asistente, puede usar en su lugar un [script de instalación](../../../../core/servers/deploy/install/use-a-command-line-to-install-sites.md) y ejecutar una instalación desatendida de línea de comandos.

Para instalar un sitio secundario, debe instalar el sitio desde la consola de Configuration Manager. Los sitios secundarios no admiten una instalación de línea de comandos por script.

## <a name="bkmk_primary"></a> Instalar un sitio de administración central o un sitio primario
Use el procedimiento siguiente para instalar un sitio de administración central o un sitio primario, o para actualizar un sitio de evaluación a un sitio de Configuration Manager con licencia completa.   

Antes de iniciar la instalación del sitio, debe familiarizarse con los detalles que se incluyen en los artículos siguientes:
 -  [Preparar la instalación de sitios](../../../../core/servers/deploy/install/prepare-to-install-sites.md)
 -  [Requisitos previos para instalar sitios](../../../../core/servers/deploy/install/prerequisites-for-installing-sites.md)

Si va a instalar un sitio de administración central como parte de un escenario de expansión del sitio, revise la sección [Expandir un sitio primario independiente](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_expand) de este tema antes de usar el procedimiento siguiente.

### <a name="bkmk_installpri"></a> Para instalar un sitio primario o de administración central

1.  En el equipo donde quiere instalar el sitio, ejecute **&lt;InstallationMedia\>\SMSSETUP\BIN\X64\Setup.exe** para iniciar el **Asistente para instalación de System Center Configuration Manager**.  

    > [!NOTE]  
    > Al instalar un sitio de administración central para expandir un sitio primario independiente, o al instalar un nuevo sitio primario secundario en una jerarquía existente, debe usar medios de instalación (archivos de origen) que coincidan con la versión de los sitios existentes. Si ha instalado actualizaciones en la consola que han cambiado la versión de los sitios instalados previamente, no use los medios de instalación originales. En su lugar, use archivos de origen de la [carpeta CD.Latest](../../../../core/servers/manage/the-cd.latest-folder.md) de un sitio actualizado. Configuration Manager requiere el uso de archivos de origen que coincidan con la versión del sitio existente al que se conectará el nuevo sitio.  

2.  En la página **Antes de comenzar**, seleccione **Siguiente**.  

3.  En la página **Introducción**, seleccione el tipo de sitio que quiera instalar:  

    -   **Sitio de administración central**, como primer sitio de una nueva jerarquía o al expandir un sitio primario independiente:  

        Seleccione **Instalar un sitio de administración central de Configuration Manager**.  

         En un paso posterior de este procedimiento, se le ofrecerá la opción de instalar un sitio de administración central como primer sitio de una jerarquía nueva, o bien de instalar un sitio de administración central para ampliar un sitio primario independiente.  

    -    **Sitio primario**, como sitio primario independiente que es el primer sitio de una jerarquía nueva, o como sitio primario secundario:  

        Seleccione **Instalar un sitio primario de Configuration Manager**.  

        > [!TIP]  
        > Normalmente, solo se selecciona la opción **Usar opciones de instalación típica para un sitio primario independiente** para instalar un sitio primario independiente en un entorno de prueba. Cuando se selecciona esta opción, el programa de instalación hace lo siguiente:  

        > -   Configura automáticamente el sitio como un sitio primario independiente.  
        > -   Usa una ruta de instalación predeterminada.  
        > -   Usa una instalación local de la instancia predeterminada de SQL Server para la base de datos del sitio.  
        > -   Instala un punto de administración y un punto de distribución en el equipo de servidor de sitio.  
        > -   Configura el sitio con el inglés y el idioma de visualización del sistema operativo en el servidor de sitio primario, si coincide con uno de los idiomas que admite Configuration Manager.  

4.  En la página **Clave de producto**:
    - Elija si quiere instalar Configuration Manager como edición de evaluación o como edición con licencia.  

      -   Si selecciona una edición con licencia, escriba la clave de producto y seleccione **Siguiente**.  

      -   Si selecciona una edición de evaluación, seleccione **Siguiente** (más adelante puede actualizar una instalación de evaluación a una instalación completa).  
    - A partir de la versión de octubre de 2016 de los medios de línea base de la versión 1606 para System Center Configuration Manager, puede especificar la fecha de expiración de su contrato de Software Assurance. En esta página puede especificar la **fecha de expiración de Software Assurance** de su contrato de licencia como un cómodo recordatorio de esa fecha. Si no la especifica durante la instalación, puede especificarla más tarde desde la consola de Configuration Manager.

      > [!NOTE]   
      > Microsoft no valida la fecha de expiración especificada y no la usará para la validación de la licencia, pero usted puede usarla como un recordatorio de la fecha de expiración. Esto es útil porque Configuration Manager busca de forma periódica nuevas actualizaciones de software que se ofrecen en línea y el estado de su licencia de Software Assurance debe ser actual para poder usar estas actualizaciones adicionales.    

      Para obtener más información, consulte [Licensing and branches for System Center Configuration Manager](/sccm/core/understand/learn-more-editions) (Licencias y ramas para System Center Configuration Manager).

5.  En la página **Términos de licencia del software de Microsoft** , lea y acepte los términos de licencia.  

6.  En la página **Licencias de requisitos previos** , lea y acepte los términos de licencia del software necesario. El programa de instalación descarga e instala automáticamente el software en los sistemas de sitio o los clientes cuando sea necesario. Debe activar todas las casillas antes de continuar a la página siguiente.  

7.  En la página **Descargas de requisitos previos** , especifique si el programa de instalación debe descargar los archivos redistribuibles necesarios más recientes desde Internet o si debe usar archivos descargados previamente:  

    -   Si desea que el programa de instalación descargue los archivos en este momento, seleccione **Descargar archivos requeridos** y especifique una ubicación para almacenar los archivos.  

    -   Si previamente descargó los archivos con el [descargador del programa de instalación](../../../../core/servers/deploy/install/setup-downloader.md), seleccione **Usar archivos descargados anteriormente** y especifique la carpeta de descarga.  

        > [!TIP]  
        > Si usa archivos descargados previamente, compruebe que la ruta de acceso a la carpeta de descarga contenga la versión más reciente de los archivos.  

8.  En la página **Selección de idioma de servidor**, seleccione los idiomas que están disponibles para la consola de Configuration Manager y para los informes (el inglés está seleccionado de forma predeterminada y no se puede quitar).  

9. En la página **Selección de idioma de cliente**, seleccione los idiomas que están disponibles para los equipos cliente y especifique si quiere habilitar todos los idiomas de cliente para los clientes de dispositivos móviles (el inglés está seleccionado de forma predeterminada y no se puede quitar).  

    > [!IMPORTANT]  
    > Si usa un sitio de administración central, asegúrese de que los idiomas de cliente que configure en el sitio de administración central incluyen todos los idiomas de cliente que configure en cada sitio primario secundario. El motivo es que los clientes que realizan la instalación desde un punto de distribución tienen acceso a los idiomas de cliente desde el sitio de nivel superior, mientras que los clientes que realizan la instalación desde un punto de administración tienen acceso a los idiomas de cliente desde su sitio primario asignado.  

10. En la página **Configuración de sitio e instalación**, especifique lo siguiente para el nuevo sitio que va a instalar:  

    -   **Código de sitio:** [todos los códigos de sitio de una jerarquía deben ser únicos](../../../../core/servers/deploy/install/prepare-to-install-sites.md#bkmk_sitecodes) y deben constar de tres dígitos alfanuméricos (de la A a la Z y del 0 al 9). Dado que el código de sitio se usa en nombres de carpeta, no use nombres reservados para Windows en el código de sitio, como los siguientes:    
        -   AUX  
        -   CON    
        -   NUL    
        -   PRN    
        -   SMS  

        > [!NOTE]  
        > El programa de instalación no comprueba si el código de sitio especificado ya está en uso o si tiene un nombre reservado.  

    -   **Nombre de sitio:** todos los sitios requieren este nombre descriptivo, que le facilitará la identificación del sitio.  

    -   **Carpeta de instalación:** es la ruta de acceso a la carpeta de instalación de Configuration Manager. No se puede cambiar la ubicación después de instalar el sitio. Además, la ruta de acceso no puede contener caracteres Unicode ni espacios finales.  

11. En la página **Instalación del sitio**, use la opción que coincida con su escenario:  

    -   **Voy a instalar un sitio de administración central:**  

         En la página **Instalación de sitio de administración central**, seleccione **Instalar como primer sitio en una jerarquía nueva** y, después, seleccione **Siguiente** para continuar.  

    -   **Voy a expandir un sitio primario independiente en una jerarquía con un sitio de administración central:**  

         En la página **Instalación de sitio de administración central**, seleccione **Expandir un sitio primario independiente existente en una jerarquía**, especifique el FQDN del servidor de sitio primario independiente y, después, seleccione **Siguiente** para continuar.  

         Los medios que use para instalar el nuevo sitio de administración central deben coincidir con la versión del sitio primario.  

    -   **Voy a instalar un sitio primario independiente:**  

         En la página **Instalación de sitio primario**, seleccione**Instalar el sitio primario como un sitio independiente** y, luego, seleccione **Siguiente**.  

    -   **Voy a instalar un sitio primario secundario:**  

         En la página **Instalación de sitio primario**, seleccione **Unir el sitio primario a una jerarquía existente**, especifique el FQDN del sitio de administración central y después seleccione **Siguiente**.  

12. En la página **Información de base de datos**, especifique la siguiente información:  

    -   **Nombre de SQL Server (FQDN):** de forma predeterminada, este se establece como el equipo de servidor de sitio.

     Si usa un puerto personalizado, agréguelo al FQDN del servidor SQL Server. Para ello, escriba el FQDN seguido de una coma y el número de puerto.   Por ejemplo, para el servidor *SQLServer1.fabrikam.com*, use este formato para especificar el puerto *1551*: **SQLServer1.fabrikam.com,1551**

    -   **Nombre de instancia:** de forma predeterminada, está en blanco. Usa la instancia predeterminada de SQL en el equipo del servidor de sitio.  

    -   **Nombre de la base de datos:** de forma predeterminada, se establece en CM_&lt;código del sitio\>. Puede usar un nombre diferente, si lo prefiere.  

    -   **Puerto de Service Broker:** de forma predeterminada, se establece para usar el puerto predeterminado de SQL Server Service Broker (SSB), que es el 4022. SQL lo usa para comunicarse directamente con la base de datos del sitio en otros sitios.  

13. En la segunda página de **Información de base de datos** puede especificar ubicaciones no predeterminadas para el archivo de datos de SQL Server y el archivo de registro de SQL Server para la base de datos del sitio:  

    -   Se proporcionan las ubicaciones predeterminadas de archivos para SQL Server.  

    -   La opción de especificar ubicaciones de archivos no predeterminadas no está disponible cuando se usa un clúster de SQL Server.  

    -   El comprobador de requisitos previos no ejecuta una comprobación del espacio libre en disco de ubicaciones de archivos no predeterminadas.  

14. En la página **Configuración de proveedor de SMS** , especifique el FQDN del servidor en el que desee instalar el proveedor de SMS.  

    -   De forma predeterminada, se especifica el servidor de sitio.  

    -   Después de haber instalado el sitio, puede configurar proveedores de SMS adicionales.  

15. En la página **Configuración de comunicación de equipos cliente** , elija entre configurar todos los sistemas de sitio para que acepten solo la comunicación HTTPS de los clientes y configurar el método de comunicación para cada rol de sistema de sitio.  

    Si selecciona **Los roles de sistema de sitio aceptan solo comunicación HTTPS de los clientes**, el equipo cliente debe tener un certificado PKI válido para la autenticación de cliente. Para obtener más información sobre los requisitos de certificados PKI, consulte [Requisitos de certificados PKI para Configuration Manager](https://technet.microsoft.com/library/gg699362.aspx).  

    > [!NOTE]  
    > Este paso se aplica solo cuando se instala un sitio primario. Si va a instalar un sitio de administración central, omita este paso.  

16. En la página **Roles del sistema de sitio** , elija si desea instalar un punto de administración o un punto de distribución. Para cada rol que decida instalar con el programa de instalación:  

    -   Debe especificar el **FQDN** para el equipo que hospedará el rol y elegir el método de conexión de cliente que el servidor admitirá (HTTP o HTTPS).  

    -   Si ha seleccionado **Los roles de sistema de sitio aceptan solo comunicación HTTPS de los clientes** en la página anterior, la conexión de cliente se configura automáticamente para HTTPS y no se puede cambiar a menos que retroceda y cambie la configuración.  

    > [!NOTE]  
    > Este paso se aplica solo cuando se instala un sitio primario. Si va a instalar un sitio de administración central, omita este paso.  

    > [!NOTE]  
    > Para instalar roles de sistema de sitio, el programa de instalación usa la **cuenta de instalación de sistema de sitio**. De forma predeterminada, se usa la cuenta del equipo del sitio primario. Esta cuenta debe tener un administrador local en un equipo remoto para instalar el rol de sistema de sitio. Si esta cuenta no tiene los permisos necesarios, desactive los roles de sistema de sitio e instálelos más tarde desde la consola de Configuration Manager, después de configurar las cuentas adicionales que va a usar como cuentas de instalación de sistema de sitio.  

17. En la página **Datos de uso**, revise la información sobre los datos que Microsoft recopila y, después, seleccione **Siguiente**.  

18. La página **Configuración de punto de conexión de servicio** solo está disponible durante la instalación:  

    -   Si va a instalar un sitio primario independiente.  

    -   Si va a instalar un sitio de administración central.  

    > [!NOTE]  
    > Si va a instalar un sitio primario secundario, omita este paso (esta página no está disponible).  

     Si va a instalar un sitio de administración central como parte de un escenario de expansión del sitio y este rol ya está instalado en el sitio primario independiente, debe desinstalar el rol del sitio primario independiente. Se permite solo una instancia de este rol en una jerarquía, y solo en el sitio de nivel superior de la jerarquía.  

     Después de seleccionar una configuración para el **Punto de conexión de servicio**, seleccione **Siguiente**. (Una vez completada la instalación, puede cambiar esta configuración desde la consola de Configuration Manager).  

19. En la página **Resumen de configuración**, revise la configuración seleccionada. Cuando esté listo, seleccione **Siguiente** para iniciar el Comprobador de requisitos previos.  

20. En la página **Comprobar requisitos previos de instalación** aparecen todos los problemas que puedan identificarse.  

    -   Cuando el Comprobador de requisitos previos encuentre un problema, seleccione un elemento de la lista para obtener más información sobre cómo resolverlo.  

    -   Debe resolver todos los elementos en estado de **error** antes de seguir instalando el sitio. Los elementos que tienen el estado **Advertencia** deben resolverse, pero no impiden la instalación del sitio.  

    -   Después de solucionar los problemas, seleccione **Ejecutar comprobación** para volver a ejecutar el Comprobador de requisitos previos.  

     Si al ejecutar el Comprobador de requisitos previos, ninguno de los elementos comprobados recibe el estado **Error**, puede seleccionar **Empezar la instalación** para iniciar la instalación del sitio.  

    > [!TIP]  
    > Además de la información proporcionada en el asistente, puede encontrar información adicional sobre los problemas de los requisitos previos al consultar el archivo **ConfigMgrPrereq.log** en la raíz de la unidad del sistema del equipo en el que va a efectuar la instalación. Para obtener una lista de las reglas y descripciones de los requisitos previos de instalación, consulte [List of Prerequisite Checks for System Center Configuration Manager](../../../../core/servers/deploy/install/list-of-prerequisite-checks.md) (Lista de comprobación de requisitos previos para System Center Configuration Manager).  

21. En la página **Instalación** , el programa de instalación muestra el estado general de la instalación. Una vez finalizada la instalación del servidor de sitio básica, tendrá la opción de **Cerrar** el asistente de instalación. Al cerrar el asistente, continúan la instalación y las configuraciones de sitio inicial en segundo plano.  

    -   Puede conectar una consola de Configuration Manager al sitio antes de que finalice la instalación. Esta consola se conecta como de solo lectura y le permite ver objetos y configuraciones, pero no efectuar modificaciones.  

    -   Cuando el programa de instalación haya finalizado, podrá conectar una consola en la que puede editar objetos y configuraciones.  


## <a name="bkmk_expand"></a> Expandir un sitio primario independiente
Cuando haya instalado un sitio primario independiente como primer sitio, después tendrá la opción de expandir dicho sitio en una jerarquía más grande, instalando un sitio de administración central.   

Al expandir un sitio primario independiente, instale un sitio de administración central nuevo que use la base de datos del sitio primario independiente existente como referencia. Después de instalar un nuevo sitio de administración central, el sitio primario independiente hace la función de sitio primario secundario.

-   Solo se puede expandir un sitio primario independiente en una nueva jerarquía.  

-   Solo se puede expandir un único sitio primario independiente en una jerarquía determinada. No se puede usar esta opción para incorporar otros sitios primarios independientes a la misma jerarquía. En lugar de eso, use la migración para migrar datos de una jerarquía a otra.  

-   Después de expandir un sitio independiente en una jerarquía con un sitio de administración central, puede agregar sitios secundarios primarios secundarios adicionales.  

-   Para quitar un sitio primario de una jerarquía con un sitio de administración central, debe desinstalar el sitio primario.  

Para expandir el sitio, use el Asistente para instalación de System Center Configuration Manager para instalar un nuevo sitio de administración central con las siguientes observaciones:  

-   Debe instalar el sitio de administración central usando la misma versión de Configuration Manager que el sitio primario independiente.  

-   En la página **Introducción** del Asistente para la instalación, seleccione la opción para instalar un sitio de administración central. En una fase posterior del programa de instalación, deberá elegir una opción para expandir un sitio primario independiente existente.  

-   Al configurar la página **Selección del idioma de cliente** para el nuevo sitio de administración central, debe seleccionar los mismos idiomas de cliente que están configurados para el sitio primario independiente que va a expandir.  

-   En la página **Instalación del sitio**, seleccione la opción de expandir el sitio primario independiente.  

Para expandir un sitio primario independiente, primero vea los [requisitos previos para expandir un sitio](/sccm/core/servers/deploy/install/prerequisites-for-installing-sites#bkmk_expand) y luego use el procedimiento *[Para instalar un sitio primario o de administración central](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_installpri)*, que aparece más arriba en este artículo.


## <a name="bkmk_secondary"></a> Instalar un sitio secundario
 Use la consola de Configuration Manager para instalar un sitio secundario.  

-   Si la consola que usa no está conectada al sitio primario que será el sitio primario del nuevo sitio secundario, el comando para instalar el sitio se replicará en el sitio primario correcto.  

-   Antes de iniciar la instalación del sitio, asegúrese de que su cuenta de usuario tiene los permisos necesarios y de que el equipo que hospedará el nuevo sitio secundario cumple todos los requisitos previos para poder usarse como servidor de sitio secundario.  

-   Al instalar el sitio secundario, Configuration Manager configura el nuevo sitio secundario para que pueda usar los puertos de comunicación de cliente que están configurados en el sitio primario principal.  

### <a name="bkmk_installsecondary"></a> Para instalar un sitio secundario  


1.  En la consola de Configuration Manager, vaya a **Administración** > **Configuración del sitio** > **Sitios**. Seleccione el sitio que será el sitio primario principal del nuevo sitio secundario.  

2.  Seleccione **Crear sitio secundario** para iniciar el **Asistente para crear sitio secundario**.  

3.  En la página **Antes de comenzar**, confirme que el sitio primario que aparece es el sitio que quiere como sitio primario del nuevo sitio secundario. Después, haga clic en **Siguiente**.  

4.  En la página **General** , especifique lo siguiente:  

    -   **Código de sitio:** todos los códigos de sitio de una jerarquía deben ser únicos y deben constar de tres dígitos alfanuméricos (de la A a la Z y del 0 al 9). Dado que el código de sitio se usa en nombres de carpeta, no use nombres reservados para Windows en el código de sitio, como los siguientes:  

        -   AUX    
        -   CON    
        -   NUL    
        -   PRN  
        -   SMS  

       > [!NOTE]  
       > El programa de instalación no comprueba si el código de sitio especificado ya está en uso o si tiene un nombre reservado.  

    -   **Nombre del servidor de sitio**: este es el FQDN del servidor en el que se instalará el nuevo sitio secundario.  

    -   **Nombre de sitio:** todos los sitios requieren este nombre descriptivo, que le facilitará la identificación del sitio.  

    -   **Carpeta de instalación:**esta es la ruta a la carpeta de instalación de Configuration Manager. No se puede cambiar la ubicación después de instalar el sitio. La ruta de acceso no puede contener caracteres Unicode ni espacios finales.  

    > [!IMPORTANT]  
    > Después de especificar los detalles en esta página, seleccione **Resumen** para usar la configuración predeterminada para el resto de las opciones del sitio secundario, y para ir directamente a la página **Resumen** del asistente.  

    > -   Use esta opción solo si está familiarizado con la configuración predeterminada de este asistente y estos son los valores que quiere usar.  
    > -   Cuando se usa la configuración predeterminada no se asocian grupos de límites al punto de distribución. Por lo tanto, hasta que configure grupos de límites que incluyan el servidor de sitio secundario, los clientes no usarán el punto de distribución que está instalado en este sitio secundario como ubicación de origen de contenido.  

5.  En la página **Archivos de origen de instalación** , elija el modo en el que el equipo del sitio secundario obtendrá los archivos de origen para instalar el sitio.  

     Al usar archivos de origen almacenados en la red o almacenados en el equipo del sitio secundario:  

    -   La ubicación del archivo de origen debe incluir una carpeta denominada **Redist** que contiene todos los archivos descargados anteriormente con el descargador del programa de instalación.  

    -   Si alguno de los archivos de **Redist** no está disponible, el programa de instalación no podrá instalar el sitio secundario.  

    -   La cuenta de equipo del equipo de sitio secundario debe tener permisos de **lectura** en la carpeta de origen y el recurso compartido de los archivos.  

6.  En la página **Configuración de SQL Server** , especifique la versión de SQL Server que se va a usar y después configure los valores relacionados.  

    > [!NOTE]  
    > El programa de instalación no valida la información que se escriba en esta página hasta que inicia la instalación. Antes de continuar, compruebe esta configuración.  

     **Instalar y configurar una copia local de SQL Express en el equipo del sitio secundario**  

    -   **Puerto del servicio de SQL Server**: especifique el puerto de servicio de SQL Server que SQL Server Express debe usar. Normalmente, el puerto de servicio está configurado para utilizar el puerto TCP 1433, pero se puede configurar otro puerto.  

    -   **Puerto de SQL Server Broker**: especifique el puerto de SQL Server Service Broker (SSB) que SQL Server Express debe usar. Normalmente, Service Broker está configurado para utilizar el puerto TCP 4022, pero se puede configurar otro puerto. Debe especificar un puerto válido que no use ningún otro sitio o servicio y que no esté bloqueado por restricciones de firewall.  

    > [!IMPORTANT]  
    > Cuando Configuration Manager instala SQL Server Express, instala SQL Server Express 2012 sin ningún Service Pack:  

    > -   Para que el sitio secundario se admita, después de instalarlo, debe actualizar SQL Server Express 2012 a [una versión compatible](/sccm/core/plan-design/configs/support-for-sql-server-versions#bkmk_SQLVersions).
    > -   Además, si la instalación del nuevo sitio secundario no puede finalizar, pero primero completa la instalación de SQL Server Express 2012, debe actualizar esa instancia de SQL Server Express antes de que Configuration Manager pueda volver a intentar correctamente la instalación del sitio secundario.  

     **Usar una instancia existente de SQL Server**  

    -   **FQDN de SQL Server**: revise el FQDN del equipo que ejecuta SQL Server. Debe usar un servidor local que ejecute SQL Server para hospedar la base de datos del sitio secundario; esta configuración no se puede modificar.  

    -   **Instancia de SQL Server**: especifique la instancia de SQL Server que se usará como base de datos del sitio secundario. Deje esta opción en blanco para utilizar la instancia predeterminada.  

    -   **Nombre de base de datos de sitio de ConfigMgr**: especifique el nombre que se usará para la base de datos del sitio secundario.  

    -   **Puerto de SQL Server Broker**: especifique el puerto de SQL Server Service Broker (SSB) que SQL Server debe usar. Debe especificar un puerto válido que no utilice ningún otro sitio o servicio y que no esté bloqueado por restricciones de firewall.  

    > [!TIP]  
    > Consulte [Versiones de SQL Server compatibles con System Center Configuration Manager](../../../../core/plan-design/configs/support-for-sql-server-versions.md) para obtener una lista de las versiones de SQL Server compatibles con System Center Configuration Manager.  

7.  En la página **Punto de distribución** , configure las opciones para el punto de distribución que se instalará en el servidor de sitio secundario.  

     **Configuración requerida:**  

    -   **Especifique cómo se comunican los dispositivos cliente con el punto de distribución**: elija entre HTTP y HTTPS.  

    -   **Crear un certificado autofirmado o importar un certificado de cliente PKI**: elija entre usar un certificado autofirmado (que también le permitirá establecer conexiones anónimas de clientes de Configuration Manager a la biblioteca de contenido) o importar un certificado de la PKI.  

         El certificado se usa para autenticar el punto de distribución en un punto de administración antes de que el punto de distribución envíe mensajes de estado.  

         Para obtener información sobre los requisitos de certificado, consulte [Requisitos de certificados PKI para Configuration Manager](https://technet.microsoft.com/library/gg699362.aspx).  

    **Configuración opcional:**  

    -   **Instalar y configurar IIS si Configuration Manager lo requiere:** seleccione esta opción para permitir que Configuration Manager instale y configure Internet Information Services (IIS) en el servidor, si no está instalado ya. IIS se debe instalar en todos los puntos de distribución.  

        > [!NOTE]  
        > Aunque este valor es opcional, IIS se debe instalar en el servidor antes de poder instalar correctamente un punto de distribución.  

    -   **Habilitar y configurar BranchCache para este punto de distribución**.  

    -   **Descripción**. Se trata de una descripción detallada para que el punto de distribución le facilite su reconocimiento.  

    -   **Habilitar este punto de distribución para contenido preconfigurado**.  

8.  En la página **Configuración de unidad** , especifique la configuración del punto de distribución del sitio secundario.  

     Puede configurar hasta dos unidades de disco para la biblioteca de contenido y dos unidades de disco para el recurso compartido de paquete. En cambio, Configuration Manager puede usar otras unidades cuando las dos primeras alcancen la reserva de espacio de unidad configurada. La página **Configuración de unidad** le permite configurar la prioridad de las unidades de disco y la cantidad de espacio libre en disco que debe quedar en cada unidad de disco.  

    -   **Reserva de espacio de unidad (MB)**: el valor que se configura en esta opción determina la cantidad de espacio libre de una unidad antes de que Configuration Manager elija una unidad diferente y continúe con el proceso de copia en esa unidad. Los archivos de contenido pueden ocupar varias unidades.  

    -   **Ubicaciones de contenido**: Especifique las ubicaciones de contenido de la librería de contenido y el recurso compartido de paquete. Configuration Manager copia el contenido en la ubicación primaria de contenido hasta que la cantidad de espacio libre alcance el valor especificado en **Reserva de espacio de unidad (MB)**.

     De forma predeterminada, las ubicaciones de contenido se establecen como **Automático**. La ubicación del contenido principal se establece en la unidad de disco que tenga más espacio en disco en el momento de efectuar la instalación. La ubicación secundaria se establece en la unidad de disco que tenga el máximo espacio libre en disco después de la unidad principal. Cuando las unidades primaria y secundaria alcanzan el valor de la reserva de espacio de unidad, Configuration Manager selecciona otra unidad que esté disponible y que tenga la mayor cantidad de espacio disponible en disco, y continúa con el proceso de copia.  

9. En la página **Validación de contenido** , especifique si desea validar la integridad de los archivos de contenido en el punto de distribución.  

    -   Si habilita la validación de contenido de forma programada, Configuration Manager inicia el proceso a la hora programada, y se verifica todo el contenido del punto de distribución.  

    -   También puede configurar la **Prioridad de validación de contenido**.  

    -   Para ver los resultados del proceso de validación de contenido, en la consola de Configuration Manager, vaya a **Supervisión** > **Estado de distribución** > **Estado de contenido**. Se muestra el contenido de cada tipo de paquete (por ejemplo, Aplicación, Paquete de actualización de software e Imagen de arranque).  

10. En la página **Grupos de límites**, administre los grupos de límites a los que está asignado este punto de distribución:  

    -   Durante la distribución de contenido, los clientes deben estar en un grupo de límites que esté asociado con el punto de distribución para utilizarlo como una ubicación de origen para el contenido.  

    -   Puede seleccionar la opción **Permitir ubicación de origen de reserva para contenido** para permitir a los clientes que están fuera de estos grupos de límites que reviertan y usen el punto de distribución como una ubicación de origen para el contenido cuando no estén disponibles otros puntos de distribución preferidos.  

     Para obtener información sobre los puntos de distribución preferidos, consulte el tema [Conceptos básicos de la administración de contenido en System Center Configuration Manager](../../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md).  

11. En la página **Resumen**, compruebe la configuración y seleccione **Siguiente** para instalar el sitio secundario. Cuando el asistente muestre la página **Finalización**, puede cerrarlo. La instalación del sitio secundario continúa en segundo plano.  


### <a name="bkmk_verify"></a> Para comprobar el estado de instalación del sitio secundario  

1.  En la consola de Configuration Manager, vaya a **Administración** > **Configuración del sitio** > **Sitios**.  

2.  Seleccione el servidor de sitio secundario que va a instalar y, después, seleccione **Mostrar estado de instalación**.  

    > [!TIP]  
    > Si se instala más de un sitio secundario a la vez, el Comprobador de requisitos previos se ejecuta en los distintos sitios de uno en uno y debe finalizar un sitio antes de empezar a comprobar el siguiente.  

