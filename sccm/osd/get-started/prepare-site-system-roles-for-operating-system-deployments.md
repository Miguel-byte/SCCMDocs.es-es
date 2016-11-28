---
title: Preparar los roles de sistema de sitio para las implementaciones de sistema operativo | Configuration Manager
description: Configure los roles de sistema de sitio antes de implementar sistemas operativos en System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 0ef5f3ce-b0e4-4775-b5c2-b245e45b4194
caps.latest.revision: 11
caps.handback.revision: 0
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: a9e682c855d5e1fb26f772b2af5066280e01851f


---
# <a name="prepare-site-system-roles-for-operating-system-deployments-with-system-center-configuration-manager"></a>Preparar los roles de sistema de sitio para la implementación de sistemas operativos con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Para implementar sistemas operativos en System Center Configuration Manager, primero debe preparar los siguientes roles de sistema de sitio que requieren configuraciones específicas y consideraciones:

##  <a name="a-namebkmkdistributionpointsa-distribution-points"></a><a name="BKMK_DistributionPoints"></a> Puntos de distribución  
 El rol de sistema de sitio de punto de distribución contiene archivos de origen para que los descarguen los clientes como, por ejemplo, contenido de aplicación, actualizaciones de software, imágenes de sistema operativo e imágenes de arranque. Puede controlar la distribución del contenido mediante las opciones de ancho de banda, limitación y programación.  

 Es importante disponer de suficientes puntos de distribución para admitir la implementación de sistemas operativos en los equipos. También es importante planear la selección de ubicación de dichos puntos de distribución en la jerarquía. Encontrará la mayor parte de esta información de planeación en [Manage content and content infrastructure](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md) (Administración del contenido y de la infraestructura de contenido). Sin embargo, existen algunas consideraciones adicionales de planeación para puntos de distribución específicos de implementación de sistema operativo.  

###  <a name="a-namebkmkadditionalplanninga-additional-planning-considerations-for-distribution-points"></a><a name="BKMK_AdditionalPlanning"></a> Consideraciones de planeación adicionales para puntos de distribución  
 A continuación se detallan aspectos de planeación adicionales que deben tenerse en cuenta para los puntos de distribución:  

-   **¿Cómo puedo impedir las implementaciones de sistema de operativo no deseadas?**  

     Configuration Manager no distingue los servidores de sitio de otros equipos de destino en una recopilación. Si implementa una secuencia de tareas requerida en una recopilación que contiene un servidor de sitio, este ejecuta la secuencia de tareas como los otros equipos de la recopilación. Asegúrese de que la implementación de sistema operativo use una recopilación que contenga a los clientes en los que va a ejecutar la implementación.  

     Puede administrar el comportamiento de las implementaciones de secuencias de tareas de alto riesgo. Una implementación de alto riesgo es una implementación que se instala automáticamente en un cliente y puede provocar resultados no deseados. Por ejemplo, una secuencia de tareas con el propósito Requerido que implementa un sistema operativo. Para reducir el riesgo de una implementación de alto riesgo no deseada, puede configurar opciones de comprobación de la implementación: Para obtener más información, consulte [Settings to manage high-risk deployments](../../protect/understand/settings-to-manage-high-risk-deployments.md) (Configuración para administrar implementaciones de alto riesgo).  

-   **¿Cuántos equipos pueden recibir una imagen de sistema operativo al mismo tiempo desde un único punto de distribución?**  

     Para realizar una estimación de los puntos de distribución necesarios, debe tener en cuenta la velocidad de procesamiento y la entrada/salida de disco del punto de distribución, el ancho de banda disponible de la red y el efecto que el tamaño del paquete de imágenes tiene en estos recursos. Por ejemplo, en una red Ethernet de 100 megabytes (MB), el número máximo de equipos que pueden procesar un paquete de imágenes de 4 gigabytes (GB) en una hora es de 11 equipos si no se tienen en cuenta otros factores de recursos del servidor.  

     `100 Megabits/sec = 12.5 Megabytes/sec = 750 Megabytes/min = 45 Gigabytes/hour = 11 images @ 4GB per image.`  

     Si se debe realizar la implementación de un sistema operativo en varios equipos en un intervalo de tiempo determinado, distribuya la imagen en un número adecuado de puntos de distribución.  

-   **¿Puedo distribuir un sistema operativo en un punto de distribución?**  

     Puede implementar un sistema operativo a un punto de distribución, pero la imagen del sistema operativo se debe recibir desde un punto de distribución distinto.  

###  <a name="a-namebkmkpxedistributionpointa-configuring-distribution-points-to-accept-pxe-requests"></a><a name="BKMK_PXEDistributionPoint"></a> Configuración de puntos de distribución para aceptar solicitudes PXE  
 Para implementar sistemas operativos en clientes de Configuration Manager que efectúan solicitudes de arranque PXE, debe configurar uno o varios puntos de distribución para que acepten las solicitudes PXE. Una vez configurado el punto de distribución, puede responder a la solicitud de arranque de PXE y determinar las acciones de implementación que se deberán llevar a cabo.

> [!IMPORTANT]  
>  [Servicios de implementación de Windows](../plan-design/infrastructure-requirements-for-operating-system-deployment.md#BKMK_WDS) debe estar instalado en todos los puntos de distribución habilitados con PXE.  

 Utilice el siguiente procedimiento para modificar un punto de distribución existente para que pueda aceptar solicitudes de PXE. Para obtener información sobre cómo instalar un nuevo punto de distribución, consulte [Install or modify a distribution point](../../core/servers/deploy/configure/install-and-configure-distribution-points.md) (Instalar o modificar un punto de distribución).  

#### <a name="to-modify-an-existing-distribution-point-to-accept-pxe-requests"></a>Para modificar un punto de distribución existente para aceptar solicitudes de PXE  

1.  En la consola de Configuration Manager, haga clic en **Administración**, expanda **Introducción** y haga clic en **Puntos de distribución**.  

2.  Seleccione el punto de distribución que desee configurar y, en la pestaña **Inicio** , en el grupo **Propiedades** , haga clic en **Propiedades**.  

3.  En la página de propiedades para el punto de distribución, haga clic en la pestaña **PXE** . y seleccione **Habilitar compatibilidad de PXE para clientes** para habilitar PXE en este punto de distribución.  

4.  Haga clic en **Sí** en el cuadro de diálogo **Revisar los puertos necesarios para PXE** para confirmar que desea habilitar PXE. Configuration Manager configura automáticamente los puertos predeterminados en un firewall de Windows. Debe configurar los puertos manualmente si usa un firewall diferente.  

    > [!NOTE]  
    >  Si WDS y DHCP están instalados en el mismo servidor, debe configurar WDS para que escuche en un puerto diferente (ya que DHCP escucha en el mismo puerto). Para obtener más información, consulte [Considerations when you have WDS and DHCP on the same server](../plan-design/infrastructure-requirements-for-operating-system-deployment.md#BKMK_WDSandDHCP) (Consideraciones si se tiene WDS y DHCP en el mismo servidor).  

5.  Seleccione **Permitir que este punto de distribución responda a solicitudes de PXE entrantes** para habilitar WDS para que responda a las solicitudes de servicio de PXE entrantes. Puede utilizar esta configuración para habilitar y deshabilitar el servicio sin quitar la funcionalidad de PXE del punto de distribución.  

6.  Para implementar sistemas operativos en un equipo no administrado por Configuration Manager, seleccione **Habilitar compatibilidad de equipos desconocida**.  

7.  Seleccione **Requerir una contraseña cuando los equipos usen PXE**y, a continuación, especifique una contraseña segura para proporcionar seguridad adicional para sus implementaciones de PXE.  

8.  In the **Afinidad entre usuario y dispositivo** elija cómo desea que el punto de distribución para asociar los usuarios con el equipo de destino para implementaciones de PXE.  

    -   Seleccione **No usar afinidad entre usuario y dispositivo** para no asociar usuarios al equipo de destino.  

    -   Seleccione **Permitir afinidad de dispositivo del usuario con aprobación manual** para esperar la aprobación de un usuario administrativo antes de que los usuarios queden asociados con el equipo de destino.  

    -   Seleccione **Permitir afinidad de dispositivo del usuario con aprobación automática** para asociar automáticamente a los usuarios con el equipo de destino sin tener que esperar aprobación.  

     Para obtener más información, consulte [Associate users with a destination computer](../get-started/associate-users-with-a-destination-computer.md) (Asociar usuarios a un equipo de destino).  

9. especifique que el punto de distribución responda a las solicitudes PXE desde todas las interfaces de red o desde interfaces de red específicas. Si elige que el punto de distribución responda a interfaces de red específicas, debe proporcionar la dirección MAC de cada interfaz de red.  

10. Especifique, en segundos, la duración de la demora antes de que el punto de distribución responda a las solicitudes del equipo cuando se utilizan varios puntos de distribución habilitados por PXE.  

11. Haga clic en **Aceptar** para actualizar las propiedades del punto de distribución.  

###  <a name="a-namebkmkramdisktftpa-customize-the-ramdisk-tftp-block-size-and-window-size-on-pxe-enabled-distribution-points"></a><a name="BKMK_RamDiskTFTP"></a> Personalización del tamaño de bloque de TFTP de RamDisk y el tamaño de la ventana de puntos de distribución habilitados con PXE  
Puede personalizar el tamaño de bloque de TFTP de RamDisk y, a partir de Configuration Manager versión 1606, el tamaño de ventana de los puntos de distribución habilitados con el entorno PXE. El hecho de haber personalizado su red podría provocar que se produjera un error de tiempo de espera en la descarga de la imagen de arranque porque el tamaño del bloque o la ventana es demasiado grande. La personalización tanto del tamaño del bloque como del de la ventana de TFTP de RamDisk le permiten optimizar el tráfico de TFTP al utilizar PXE para cumplir los requisitos de red específicos.   
Debe probar la configuración personalizada en su entorno para determinar lo que es más eficaz.  

-   **Tamaño del bloque de TFTP**: el tamaño de bloque es el tamaño de los paquetes de datos enviados por el servidor al cliente que está descargando el archivo (como se describe en RFC 2347). Un tamaño de bloque mayor permite que el servidor envíe menos paquetes, por lo que habrá menos demoras por los recorridos de ida y vuelta entre el servidor y el cliente. Sin embargo, un tamaño de bloque grande genera fragmentación en los paquetes, lo cual no se admite en la mayoría de implementaciones de cliente de PXE.  

-   **Tamaño de la ventana de TFTP**: TFTP requiere un paquete de confirmación para cada bloque de datos que se envía. El servidor no envía el siguiente bloque de la secuencia hasta que reciba el paquete de confirmación del bloque anterior. La característica basada en ventanas de TFTP forma parte de Servicios de implementación de Windows y permite definir cuántos bloques de datos son necesarios para completar una ventana. El servidor envía los bloques de datos sucesivamente hasta que se completa la ventana; en ese momento, el cliente envía un paquete de confirmación. Al aumentar el tamaño de la ventana se reduce el número de demoras por los recorridos de ida y vuelta entre el cliente y el servidor y se disminuye el tiempo global necesario para descargar una imagen de arranque.  


#### <a name="to-modify-the-ramdisk-tftp-window-size"></a>Para modificar el tamaño de la ventana de TFTP de RamDisk  

-   Agregue la siguiente clave del Registro en puntos de distribución habilitados con PXE para personalizar el tamaño de la ventana de TFTP de RamDisk:  

     **Ubicación**: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP  
    Nombre: RamDiskTFTPWindowSize  

     **Tipo**: REG_DWORD  

     **Valor**: <tamaño de ventana personalizado\>  

 El valor predeterminado es 1 (1 bloque de datos completa la ventana)  

#### <a name="to-modify-the-ramdisk-tftp-block-size"></a>Para modificar el tamaño de bloque de TFTP de RamDisk  

-   Agregue la siguiente clave del Registro en puntos de distribución habilitados con PXE para personalizar el tamaño de la ventana de TFTP de RamDisk:  

     **Ubicación**: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP  
    Nombre: RamDiskTFTPBlockSize  

     **Tipo**: REG_DWORD  

     **Valor**: <tamaño de bloque personalizado\>  

 El valor predeterminado es 4096 (4k).  


###  <a name="a-namebkmkdpmulticasta-configure-distribution-points-to-support-multicast"></a><a name="BKMK_DPMulticast"></a> Configuración de puntos de distribución para admitir la multidifusión  
 La multidifusión es un método de optimización de red que puede usar en puntos de distribución si es probable que varios clientes descarguen la misma imagen de sistema operativo al mismo tiempo. Cuando se usa multidifusión, varios equipos pueden descargar la imagen de sistema operativo de forma simultánea a medida que el punto de distribución la reparte mediante multidifusión, en lugar de que el punto de distribución envíe una copia de los datos a cada cliente a través de una conexión separada. Debe configurar al menos un punto de distribución para admitir la multidifusión: Para obtener más información, consulte [Use multicast to deploy Windows over the network](../deploy-use/use-multicast-to-deploy-windows-over-the-network.md) (Usar multidifusión para implementar Windows a través de la red).  

 Antes de implementar el sistema operativo, debe configurar un punto de distribución para admitir la multidifusión. Utilice el siguiente procedimiento para modificar un punto de distribución existente para que admita la multidifusión. Para obtener información sobre cómo instalar un punto de distribución nuevo, consulte [Install and configure distribution points](../../core/servers/deploy/configure/install-and-configure-distribution-points.md) (Instalar y configurar puntos de distribución).

#### <a name="to-enable-multicast-for-a-distribution-point"></a>Para habilitar la multidifusión para un punto de distribución  

1.  En la consola de Configuration Manager, haga clic en **Administración**.  

2.  En el área de trabajo **Administración** , expanda **Introducción**y seleccione el nodo **Puntos de distribución** .  

3.  Seleccione el punto de distribución que desee utilizar para la multidifusión de la imagen de sistema operativo.  

4.  En la pestaña **Inicio** , en el grupo **Propiedades** , haga clic en **Propiedades**.  

5.  Seleccione la pestaña **Multidifusión** y configure las siguientes opciones:  

    -   **Habilitar multidifusión**: debe seleccionar esta opción para que el punto de distribución admita la multidifusión.  

    -   **Cuenta de conexión de multidifusión**: especifique una cuenta para conectarse a la base de datos del sitio.  

    -   **Configuración de dirección de multidifusión**: especifique las direcciones IP usadas para enviar datos a los equipos de destino. De forma predeterminada, se obtiene la dirección IP de un servidor DHCP que esté habilitado para distribuir direcciones de multidifusión. Dependiendo del entorno de red, puede especificar un intervalo de direcciones IP entre 239.0.0.0 y 239.255.255.255.  

        > [!IMPORTANT]  
        >  Estas direcciones IP deben ser accesibles para los equipos de destino que soliciten la imagen de sistema operativo. Esto significa que los enrutadores y firewalls que hay entre el equipo de destino y el servidor de sitio deben configurarse para permitir el tráfico de multidifusión.  

    -   **Intervalo de puertos UDP**: especifique el intervalo de puertos UDP para enviar datos a los equipos de destino.  

        > [!IMPORTANT]  
        >  Estos puertos deben ser accesibles para los equipos de destino que soliciten la imagen de sistema operativo. Esto significa que los enrutadores y firewalls que hay entre el equipo de destino y el servidor de sitio deben configurarse para permitir el tráfico de multidifusión.  

    -   **Habilitar multidifusión programada**: especifique cómo Configuration Manager controla cuándo se debe iniciar la implementación de sistemas operativos en los equipos de destino. Haga clic en **Habilitar multidifusión programada**y, a continuación, seleccione las opciones siguientes.  

         En el cuadro **Retraso de inicio de sesión**, especifique cuántos minutos debe esperar Configuration Manager para responder la primera solicitud de implementación.  

         En el cuadro **Tamaño de sesión mínimo**, especifique cuántas solicitudes deben recibirse para que Configuration Manager inicie la implementación del sistema operativo.  

    -   **Velocidad de transferencia de clientes**: seleccione la velocidad de transferencia para descargar datos en los equipos de destino.  

    -   **Número máximo de clientes**: especifique el número máximo de equipos de destino que pueden descargar el sistema operativo desde este punto de distribución.  

6.  Haga clic en **Aceptar**.  

##  <a name="a-namebkmkstatemigrationpointsa-state-migration-point"></a><a name="BKMK_StateMigrationPoints"></a> Punto de migración de estado  
 El punto de migración de estado almacena los datos de estado de usuario que se capturan en un equipo y se restauran en otro. Sin embargo, cuando se captura la configuración de usuario para la implementación de sistema operativo en el mismo equipo, como una implementación que actualice el sistema operativo en el equipo de destino, puede elegir si quiere almacenar los datos en el mismo equipo mediante el uso de vínculos físicos o usar un punto de migración de estado. En algunas implementaciones, al crear el almacén de estado, Configuration Manager crea automáticamente una asociación entre el almacén de estado y el equipo de destino. Tenga en cuenta los siguientes factores al planear el punto de migración de estado.  

### <a name="user-state-size"></a>Tamaño de estado de usuario  
 El tamaño de estado de usuario afecta directamente al almacenamiento en disco en el punto de migración de estado y al rendimiento de la red durante la migración. Tenga en cuenta el tamaño de estado de usuario y el número de equipos que desea migrar. También es preciso tener en cuenta la configuración que desea migrar desde el equipo. Por ejemplo, si se realiza una copia de seguridad de **Mis documentos** en un servidor, tal vez no sea necesario migrar Mis documentos como parte de la implementación de imagen. Evite la realización de migraciones innecesarias para reducir el tamaño total del estado de usuario y para minimizar el efecto que podría tener en el rendimiento de la red y en el almacenamiento en disco en el punto de migración de estado.  

### <a name="user-state-migration-tool"></a>Herramienta de migración de estado de usuario  
 Para capturar y restaurar el estado de usuario durante la implementación de sistemas operativos, es preciso usar el paquete de la Herramienta de migración de estado de usuario (USMT) que apunta a los archivos de origen de USMT. Configuration Manager crea automáticamente este paquete en la consola de Configuration Manager en **Biblioteca de software** > **Administración de aplicaciones** > **Paquetes**. Configuration Manager usa USMT 10.0, que se distribuye en Windows Assessment and Deployment Kit (Windows ADK), para capturar el estado de usuario de un sistema operativo y luego restaurarlo en otro sistema operativo.  

 Para obtener una descripción de escenarios de migración diferentes para USMT 10.0, consulte [Escenarios comunes de migración](https://technet.microsoft.com/library/mt299169\(v=vs.85\).aspx).  

### <a name="retention-policy"></a>Directiva de retención  
 Al configurar el punto de migración de estado, puede especificar el intervalo de tiempo durante el que desea mantener los datos de estado de usuario almacenados en el mismo. El periodo de tiempo para mantener los datos en el punto de migración de estado depende de dos factores:  

-   El efecto de los datos almacenados en el almacenamiento en disco.  

-   La posibilidad de que sea necesario mantener los datos durante un tiempo por si fuera preciso migrarlos de nuevo.  

 La migración de estado se produce en dos fases: captura y restauración de los datos. Al capturar los datos, se recopilan los datos de estado de usuario y se guardan en el punto de migración de estado. Al restaurar los datos, los datos de estado de usuario se recuperan del punto de migración de estado, se escriben en el equipo de destino y, a continuación, la secuencia de tareas **Liberar almacén de estado** los libera. Al realizar la liberación de los datos, se inicia el temporizador de retención. Si selecciona la opción de eliminar inmediatamente los datos migrados, los datos de estado de usuario se eliminan después de liberarse. Si selecciona la opción de mantener los datos durante un determinado periodo de tiempo, los datos se eliminan al finalizar dicho periodo, después de la liberación de los datos de estado. El espacio en disco potencialmente necesario aumentará en función del periodo de retención establecido.  

### <a name="select-drive-to-store-user-state-migration-data"></a>Seleccionar una unidad para el almacenamiento de datos de migración de estado de usuario  
 Al configurar el punto de migración de estado, debe especificar la unidad del servidor en la que desea almacenar los datos de migración de estado. Debe seleccionar una unidad de una determinada lista de unidades. Sin embargo, algunas de estas unidades pueden representar unidades que no permiten la escritura, como unidades de CD o unidades de recursos compartidos que no son de red. Además, es posible que algunas letras de unidad no estén asignadas a las unidades del equipo. Al configurar el punto de migración de estado debe especificar una unidad compartida y que permita la escritura.  

### <a name="configure-a-state-migration-point"></a>Configurar un punto de migración de estado  
 Puede utilizar los métodos siguientes para configurar un punto de migración de estado para almacenar los datos de estado de usuario:  

-   Use el **Asistente para crear servidor de sistema de sitio** para crear un nuevo servidor de sistema de sitio para el punto de migración de estado.  

-   Use el **Asistente para agregar roles de sistema de sitio** para agregar un punto de migración de estado a un servidor existente.  

 Al utilizar estos asistentes, deberá proporcionar la siguiente información para el punto de migración de estado:  

-   Las carpetas para almacenar los datos de estado de usuario.  

-   El número máximo de clientes que pueden almacenar datos en el punto de migración de estado.  

-   Seleccione el espacio libre mínimo para que el punto de migración de estado almacene datos de estado de usuario.  

-   La directiva de eliminación para el rol. Puede especificar que los datos de estado de usuario se eliminen inmediatamente después de ser restaurados en un equipo o después de un número específico de días tras haber sido restaurados en un equipo.  

-   Si el punto de migración de estado responde solo a solicitudes de restauración de datos de estado de usuario. Cuando se habilita esta opción, no se puede utilizar el punto de migración de estado para almacenar datos de estado de usuario.  

 Para consultar los pasos necesarios para instalar un rol de sistema de sitio, consulte [Add site system roles](../../core/servers/deploy/configure/add-site-system-roles.md) (Agregar roles de sistema de sitio).  



<!--HONumber=Nov16_HO1-->


