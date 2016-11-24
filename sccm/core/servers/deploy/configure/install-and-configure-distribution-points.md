---
title: "Administrar puntos de distribución | System Center Configuration Manager"
description: "Hospede el contenido (archivos y software) que implementa en dispositivos y usuarios mediante el uso de los puntos de distribución. Aquí se muestra cómo instalarlos y configurarlos."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aebafaf9-b3d5-4a0f-9ee5-685758c037a1
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: dedfcc77cb94ede1abfd65e22f9d3d116b9ed68e

---
# <a name="install-and-configure-distribution-points-for-system-center-configuration-manager"></a>Instalación y configuración de puntos de distribución de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Instale puntos de distribución de System Center Configuration Manager para hospedar el contenido (archivos y software) que implementa en dispositivos y usuarios. También puede crear grupos de puntos de distribución que simplifican la manera en que administra los puntos de distribución, y cómo distribuye el contenido en puntos de distribución.  

 Cuando **instala un nuevo punto de distribución** (mediante el asistente de instalación) o **administra las propiedades de un punto de distribución existente** (editando las propiedades del punto de distribución), tiene la oportunidad de configurar la mayoría de la configuración del punto de distribución. En cambio, existen algunas opciones de configuración que solo están disponibles al instalar o editar, pero no en ambas:  

-   **Opciones que solo están disponibles cuando se instala un punto de distribución:**  

    -   Permitir que el administrador de configuración instale IIS en el equipo del punto de distribución  

    -   Configurar el espacio de la unidad para el punto de distribución  

-   **Pasos de configuración que solo están disponibles cuando se editan las propiedades de un punto de distribución:**  

    -   Administrar relaciones de grupo de puntos de distribución  

    -   Ver el contenido implementado en el punto de distribución  

    -   Configurar los límites de frecuencia de las transferencias de datos a los puntos de distribución  

    -   Configurar las programaciones de las transferencias de datos a los puntos de distribución  

##  <a name="a-namebkmkinstalla-install-a-distribution-point"></a><a name="bkmk_install"></a> Instalar un punto de distribución  
 Debe designar un servidor de sistema de sitio como punto de distribución antes de que el contenido puede estar disponible en los equipos cliente. Puede agregar el rol de sitio de punto de distribución a un nuevo servidor de sistema de sitio o puede agregar el rol de sitio a un servidor de sistema de sitio existente.  

 Cuando instala un nuevo punto de distribución, usa un asistente de instalación que le guía a través de la configuración disponible. Antes de comenzar, tenga en cuenta lo siguiente:  

-   Debe tener los siguientes permisos de seguridad para crear y configurar un punto de distribución:  

    -   **Leer** en el objeto **Punto de distribución**  

    -   **Copiar en punto de distribución** en el objeto **Punto de distribución**  

    -   **Modificar** en el objeto **Sitio**  

    -   **Administrar certificados para implementación de sistema operativo** en el objeto **Sitio**  

-   IIS debe estar instalado en el servidor que hospedará el punto de distribución. Cuando se instala el rol de sistema de sitio, Configuration Manager puede instalar y configurar IIS automáticamente.  

Use los siguientes procedimientos básicos para instalar o modificar un punto de distribución y consulte la sección [Configuraciones del punto de distribución](#bkmk_configs) de este tema para obtener más información sobre las opciones de configuración disponibles.  

#### <a name="to-install-a-distribution-point"></a>Para instalar un punto de distribución  

1.  En la consola de Configuration Manager, haga clic en **Administración** >  **Configuración de sitio** > **Servidores y roles del sistema de sitios**.  

2.  Agregue el rol de sistema de sitio del punto de distribución a un servidor de sistema de sitio nuevo o existente:  

    -   **Nuevo servidor de sistema de sitio**: en la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear servidor de sistema de sitio**. Se abre el Asistente para crear servidor de sistema de sitio.  

    -   **Servidor de sistema de sitio existente**: haga clic en el servidor en el que desea instalar el rol de sistema de sitio del punto distribución. Al hacer clic en un servidor, se muestra en el panel de resultados una lista de los roles de sistema de sitio que ya están instalados en el servidor.  

         En la pestaña **Inicio** , en el grupo **Servidor** , haga clic en **Agregar rol de sistema de sitio**. Se abre el Asistente para agregar roles de sistema de sitio.  

3.  En la página **General** , especifique la configuración general para el servidor de sistema de sitio. Cuando se agrega el punto de distribución a un servidor de sistema de sitio existente, compruebe los valores configurados previamente.  

4.  En la página **Selección de rol del sistema** , seleccione **Punto de distribución** en la lista de roles disponibles y, a continuación, haga clic en **Siguiente**.  

5.  En lo que respecta a las páginas posteriores del asistente, consulte la información de la sección [Configuraciones del punto de distribución](#bkmk_configs) para completar cada página del asistente cuando se le solicite.  

     Por ejemplo, si quiere instalar el punto de distribución como punto de distribución de extracción, debe seleccionar **Habilitar este punto de distribución para extraer contenido desde otros puntos de distribución** y después configurar los valores adicionales que requieren los puntos de distribución de extracción.  

6.  Después de completar al asistente, se agrega el rol del sitio del punto de distribución al servidor de sistema del sitio.  

#### <a name="to-modify-a-distribution-point"></a>Para modificar un punto de distribución  

1.  En la consola de Configuration Manager, haga clic en **Administración** >  **Puntos de distribución** y, después, seleccione el punto de distribución que quiere configurar.  

2.  En la pestaña **Inicio** , en el grupo **Propiedades** , haga clic en **Propiedades**.  

3.  Use la información de la sección [Configuraciones del punto de distribución](#bkmk_configs) al editar las propiedades del punto de distribución.  

4.  Tras realizar los cambios que desee, guarde la configuración y cierre las propiedades del punto de distribución.  

##  <a name="a-namebkmkmanagea-manage-distribution-point-groups"></a><a name="bkmk_manage"></a> Administrar grupos de puntos de distribución  
 Los grupos de puntos de distribución proporcionan una agrupación lógica de los puntos de distribución para la distribución de contenido. Puede usar estos grupos para administrar y supervisar el contenido desde una ubicación central para los puntos de distribución que abarcan varios sitios.  

-   Puede agregar uno o varios puntos de distribución desde cualquier sitio de la jerarquía a un grupo de puntos de distribución.  

-   Puede agregar un punto de distribución a más de un grupo de puntos de distribución.  

-   Cuando distribuye contenido a un grupo de puntos de distribución, el administrador de configuración distribuye el contenido a todos los puntos de distribución que son miembros del grupo de puntos de distribución.  

-   Si agrega un punto de distribución al grupo de puntos de distribución después de la primera distribución de contenido, el administrador de configuración distribuye automáticamente el contenido al miembro nuevo del punto de distribución.  

-   Puede asociar una recopilación con un grupo de puntos de distribución. A continuación, cuando distribuya contenido a dicha recopilación, el administrador de configuración determina los grupos de puntos de distribución asociados con la recopilación y, después, el contenido se distribuye a todos los puntos de distribución que son miembros de esos grupos de puntos de distribución.  

    > [!NOTE]  
    >  Después de distribuir contenido a una recopilación, si asocia la recopilación a un nuevo grupo de puntos de distribución, debe redistribuir el contenido a la recopilación antes de distribuirlo al nuevo grupo de puntos de distribución.  

#### <a name="to-create-and-configure-a-new-distribution-point-group"></a>Para crear y configurar un grupo de puntos de distribución nuevo  

1.  En la consola de Configuration Manager, haga clic en **Administración** > **Grupos de puntos de distribución**.  

2.  En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear grupo**.  

3.  Escriba el nombre y una descripción para el grupo de puntos de distribución.  

4.  En la pestaña **Recopilaciones** , haga clic en **Agregar**, seleccione las recopilaciones que va a asociar al grupo de puntos de distribución y, a continuación, haga clic en **Aceptar**.  

5.  En la pestaña **Miembros** , haga clic en **Agregar**, seleccione los puntos de distribución que va a agregar como miembros del grupo de puntos de distribución y, a continuación, haga clic en **Aceptar**.  

6.  Haga clic en **Aceptar** para crear el grupo de puntos de distribución.  

#### <a name="to-add-distribution-points-and-associate-collections-to-an-existing-distribution-point-group"></a>Para agregar puntos de distribución y asociar recopilaciones a un grupo de puntos de distribución existente  

1.  En la consola de Configuration Manager, haga clic en **Administración** > **Grupos de puntos de distribución**.  

2.  En la pestaña **Inicio** , en el grupo **Propiedades** , haga clic en **Propiedades**.  

3.  En la pestaña **Recopilaciones** , haga clic en **Agregar** , seleccione las recopilaciones que desee asociar al grupo de puntos de distribución y, a continuación, haga clic en **Aceptar**.  

4.  En la pestaña **Miembros** , haga clic en **Agregar** , seleccione los puntos de distribución que desee agregar como miembros del grupo de puntos de distribución y, a continuación, haga clic en **Aceptar**.  

5.  Haga clic en **Aceptar** para guardar los cambios en el grupo de puntos de distribución.  

#### <a name="to-add-selected-distribution-points-to-a-new-distribution-point-group"></a>Para agregar puntos de distribución seleccionados a un grupo de puntos de distribución nuevo  

1.  En la consola de Configuration Manager, haga clic en **Administración** > **Puntos de distribución** y, después, seleccione los puntos de distribución que quiera agregar al grupo de puntos de distribución nuevo.  

2.  En la pestaña **Inicio** , en el grupo **Punto de distribución** , expanda **Agregar elementos seleccionados**y, a continuación, haga clic en **Agregar elementos seleccionados a grupo de puntos de distribución**.  

3.  Escriba el nombre y una descripción para el grupo de puntos de distribución.  

4.  En la pestaña **Recopilaciones** , haga clic en **Agregar** , seleccione las recopilaciones que desee asociar al grupo de puntos de distribución y, a continuación, haga clic en **Aceptar**.  

5.  En la pestaña **Miembros**, compruebe que quiere que Configuration Manager agregue los puntos de distribución incluidos en la lista como miembros del grupo de puntos de distribución. Haga clic en **Agregar** para modificar los puntos de distribución que desee agregar como miembros del grupo de puntos de distribución y, a continuación, haga clic en **Aceptar**.  

6.  Haga clic en **Aceptar** para crear el grupo de puntos de distribución.  

#### <a name="to-add-selected-distribution-points-to-existing-distribution-point-groups"></a>Para agregar puntos de distribución seleccionados a grupos de puntos de distribución existentes.  

1.  En la consola de Configuration Manager, haga clic en **Administración** > **Puntos de distribución** y, después, seleccione los puntos de distribución que quiera agregar al grupo de puntos de distribución nuevo.  

2.  En la pestaña **Inicio** , en el grupo **Punto de distribución** , expanda **Agregar elementos seleccionados**y, a continuación, haga clic en **Agregar elementos seleccionados a grupos de puntos de distribución existentes**.  

3.  En **Grupos de puntos de distribución disponibles**, seleccione los grupos de puntos de distribución en los que se agregarán los puntos de distribución seleccionados como miembros y, a continuación haga clic en **Aceptar**.  

##  <a name="a-namebkmkconfigsa-distribution-point-configurations"></a><a name="bkmk_configs"></a> Configuraciones de punto de distribución  
 Los puntos de distribución individuales admiten varias configuraciones. Sin embargo, no todos los tipos de puntos de distribución son compatibles con todas las configuraciones. Por ejemplo, los puntos de distribución basados en la nube no admiten las implementaciones de contenido que están habilitadas para PXE o multidifusión. Puede encontrar información sobre las limitaciones específicas en los temas siguientes:  

-   [Usar un punto de distribución basado en la nube con System Center Configuration Manager](../../../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md)  

-   [Usar un punto de distribución de extracción con System Center Configuration Manager](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point)  

En las secciones siguientes se describen las configuraciones que puede seleccionar al instalar un punto de distribución nuevo o modificar las propiedades de un punto de distribución existente:  

### <a name="general"></a>General  
 Configure los valores generales del punto de distribución:  

-   **Instalar y configurar IIS si Configuration Manager lo requiere:** seleccione esta opción para permitir que Configuration Manager instale y configure Internet Information Services (IIS) en el servidor, si no está instalado ya. IIS se debe instalar en todos los puntos de distribución. Si IIS no está instalado en el servidor y no se selecciona esta opción, se debe instalar IIS para poder instalar correctamente el punto de distribución.  

    > [!NOTE]  
    >  Esta opción solo está disponible cuando se instala un punto de distribución nuevo.  

-   **Configurar la manera en que los dispositivos cliente se comunican con el punto de distribución:** existen ventajas y desventajas para usar HTTP y HTTPS. Para obtener más información, consulte *Procedimientos recomendados de seguridad para la administración de contenido* en [Fundamental concepts for content management in System Center Configuration Manager (Conceptos básicos de la administración de contenido en System Center Configuration Manager)](../../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md).  

-   **Permitir a los clientes conectarse de forma anónima**: esta opción permite especificar si el punto de distribución va a permitir conexiones anónimas de los clientes de Configuration Manager con la biblioteca de contenido.  

    > [!IMPORTANT]  
    >  La reparación de una aplicación de Windows Installer puede producir un error en un cliente si no se usa esta configuración.  
    >   
    >  -   Cuando se implementa una aplicación de Windows Installer en un cliente de Configuration Manager, este descarga el archivo en la caché local del cliente y los archivos se quitarán una vez finalizada la instalación.  
    > -   El cliente de Configuration Manager actualiza la lista de origen de Windows Installer de las aplicaciones instaladas de Windows Installer con la ruta de contenido de la biblioteca de contenido de los puntos de distribución asociados.  
    > -   Más adelante, si inicia la acción Reparar en Agregar o quitar programas en un cliente de Configuration Manager, MSIExec intentará tener acceso a la ruta de contenido con un usuario anónimo.  
    >   
    >  En cambio, puede instalar la actualización descrita en el artículo de Microsoft Knowledge Base [2619572](http://go.microsoft.com/fwlink/?LinkId=279699) y después modificar una clave del Registro para cambiar este comportamiento.  
    >   
    >  -   Después de instalar la actualización en los clientes, MSIExec tendrá acceso a la ruta de contenido mediante la cuenta del usuario conectado cuando seleccione la opción **Permitir a los clientes conectarse de forma anónima**.  

-   **Crear un certificado autofirmado o importar un certificado de cliente de infraestructura de clave pública (PKI) para el punto de distribución:** El certificado tiene los siguientes fines:  

    -   Autentica el punto de distribución en un punto de administración antes de que el punto de distribución envíe mensajes de estado.  

    -   Si activa la casilla **Habilitar compatibilidad de PXE para clientes** de la página **Configuración PXE** , el certificado se envía a los equipos que realizan un arranque PXE para que puedan conectarse a un punto de administración durante la implementación del sistema operativo.  

    Cuando se configuran todos los puntos de administración del sitio para HTTP, debe crear un certificado autofirmado. Cuando se configuran los puntos de administración para HTTPS, debe importar un certificado de cliente PKI.  

    Para importar el certificado, busque un archivo de estándar de criptografía de clave pública (PKCS #12) que contenga un certificado PKI con los requisitos siguientes para Configuration Manager:  

    -   El uso previsto debe incluir autenticación de cliente.  

    -   La clave privada debe habilitarse para ser exportada.  

    > [!TIP]  
    >  No hay requisitos específicos para el nombre del firmante o el nombre alternativo del firmante (SAN) del certificado, y puede utilizar el mismo certificado para varios puntos de distribución.  

     Para obtener más información sobre los requisitos de certificados, consulte [Requisitos de certificados PKI para System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

     Para ver una implementación de ejemplo de este certificado, consulte la sección *Implementación del certificado de cliente para puntos de distribución* del tema [Ejemplo paso a paso de implementación de los certificados PKI para System Center Configuration Manager: Entidad de certificación de Windows Server 2008](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  

-   **Habilitar este punto de distribución para contenido preconfigurado:** seleccione esta opción para habilitar el punto de distribución para contenido preconfigurado. Cuando se selecciona esta opción, puede configurar el comportamiento de la distribución a la hora de distribuir contenido. Puede elegir entre preconfigurar siempre el contenido en el punto de distribución, preconfigurar el contenido inicial para el paquete, pero usar el proceso de distribución de contenido normal cuando haya actualizaciones en el contenido, o usar siempre el proceso de distribución de contenido normal para el contenido del paquete.  

### <a name="drive-settings"></a>Configuración de unidad  

> [!NOTE]  
>  Estas opciones solo están disponibles cuando se instala un punto de distribución nuevo.  

Especifique la configuración de unidad para el punto de distribución. Se pueden configurar hasta dos unidades de disco para la biblioteca de contenido y dos unidades de disco para el recurso compartido de paquete, aunque Configuration Manager puede usar unidades adicionales cuando las dos primeras alcancen el valor de la reserva de espacio de unidad configurada. La página **Configuración de unidad** permite configurar la prioridad de las unidades de disco y la cantidad de espacio libre en disco que debe quedar en cada unidad de disco.  

-   **Reserva de espacio de unidad (MB):** el valor que se configura en esta opción determina la cantidad de espacio libre de una unidad antes de que Configuration Manager elija una unidad diferente y continúe con el proceso de copia en esa unidad. Los archivos de contenido pueden ocupar varias unidades.  

-   **Ubicaciones de contenido:** especifique las ubicaciones de contenido de la librería de contenido y el recurso compartido de paquete. Configuration Manager copia el contenido en la ubicación primaria de contenido hasta que la cantidad de espacio libre alcance el valor especificado en **Reserva de espacio de unidad (MB)**. De forma predeterminada, las ubicaciones de contenido se establecen como **Automático**. La ubicación del contenido primario se establece en la unidad de disco que tiene más espacio en disco en la instalación. La ubicación secundaria se asigna a la unidad de disco que tiene más espacio disponible en segundo lugar. Cuando las unidades primaria y secundaria alcanzan el valor de la reserva de espacio de unidad, Configuration Manager selecciona otra unidad que esté disponible y que tenga la mayor cantidad de espacio disponible en disco, y continúa con el proceso de copia.  

> [!NOTE]  
>  Para evitar que Configuration Manager se instale en una unidad específica, cree un archivo vacío llamado **no_sms_on_drive.sms** y cópielo en la carpeta raíz de la unidad antes de instalar el punto de distribución.  

### <a name="pull-distribution-point"></a>Punto de distribución de extracción  
Si selecciona **Habilitar este punto de distribución para extraer contenido desde otros puntos de distribución**, cambiará la manera en que ese equipo obtiene el contenido que se distribuye al punto de distribución. Se convertirá en un punto de distribución de extracción.  

Para cada punto de distribución que configure, debe especificar uno o más puntos de distribución de origen de los cuales el punto de distribución de extracción obtiene el contenido.  

-   Haga clic en **Agregar** y, después, seleccione uno o varios de los puntos de distribución disponibles para que sean puntos de distribución de origen.  

-   Haga clic en **Quitar** para quitar el punto de distribución seleccionado como punto de distribución de origen.  

-   Utilice los botones de flecha para ajustar el orden en que el punto de distribución de extracción contacta con los puntos de distribución de origen cuando el punto de distribución de extracción intenta transferir contenido. Se establece contacto con los puntos de distribución con el valor más bajo en primer lugar.  

### <a name="pxe"></a>PXE  
Especifique si desea habilitar PXE en el punto de distribución. Cuando se habilita PXE, Configuration Manager instala Servicios de implementación de Windows en el servidor si es necesario. Servicios de implementación de Windows es el servicio que realiza el arranque PXE para instalar sistemas operativos. Después de completar el asistente para crear el punto de distribución, Configuration Manager instala un proveedor en Servicios de implementación de Windows que usa funciones de arranque PXE.  

Cuando se seleccione **Habilitar compatibilidad de PXE para clientes**, configure las siguientes opciones:  

-   **Permitir que este punto de distribución responda a solicitudes de PXE entrantes**: especifica si se habilita Servicios de implementación de Windows para que responda a las solicitudes de servicio de PXE. Use esta casilla para habilitar y deshabilitar el servicio sin quitar la funcionalidad de PXE del punto de distribución.  

-   **Habilitar compatibilidad de equipos desconocida**: especifique si quiere habilitar la compatibilidad con equipos que no están administrados por Configuration Manager.  

-   **Requerir una contraseña cuando los equipos usen PXE**: para proporcionar seguridad adicional para sus implementaciones de PXE, especifique una contraseña segura.  

-   **Afinidad de dispositivo del usuario**: especifique cómo desea que el punto de distribución asocie usuarios al equipo de destino para las implementaciones de PXE. Seleccione una de las siguientes opciones:  

    -   **Permitir afinidad de dispositivo de usuario con autoaprobación**: seleccione esta opción para asociar automáticamente los usuarios al equipo de destino sin tener que esperar aprobación.  

    -   **Permitir afinidad de dispositivo de usuario pendiente de la aprobación del administrador**: seleccione esta opción para esperar aprobación por parte de un usuario administrativo antes de asociar usuarios al equipo de destino.  

    -   **No permitir afinidad de dispositivo de usuario**: seleccione esta opción para especificar que los usuarios no están asociados al equipo de destino.  

     Para obtener más información sobre la afinidad entre usuario y dispositivo, consulte [Vincular usuarios y dispositivos con afinidad entre usuario y dispositivo en System Center Configuration Manager](../../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).  

-   **Interfaces de red**: especifique que el punto de distribución responda a las solicitudes PXE desde todas las interfaces de red o desde interfaces de red específicas. Si el punto de distribución responde a interfaces de red específicas, debe proporcionar la dirección MAC de cada interfaz de red.  

-   **Especificar retraso en la respuesta del servidor PXE (segundos)**: especifica, en segundos, el tiempo que se demora el punto de distribución antes de responder a las solicitudes de equipo cuando se utilizan varios puntos de distribución habilitados para PXE. De manera predeterminada, el punto de servicio PXE de Configuration Manager responde primero a solicitudes PXE de red.  

> [!NOTE]  
>  Puede usar el protocolo PXE para iniciar implementaciones del sistema operativo en equipos cliente de Configuration Manager. Configuration Manager usa el rol de sitio del punto de distribución habilitado con PXE para iniciar el proceso de implementación del sistema operativo. El punto de distribución habilitado para PXE debe estar configurado para responder a solicitudes de arranque PXE que realizan clientes de Configuration Manager en la red y, después, interactuar con la infraestructura de Configuration Manager para determinar las acciones de implementación apropiadas que se deben llevar a cabo.  

### <a name="multicast"></a>Multidifusión  
Especifique si desea habilitar la multidifusión en el punto de distribución. Cuando se habilita la multidifusión, Configuration Manager instala Servicios de implementación de Windows en el servidor si es necesario.  

Cuando se active la casilla **Habilitar multidifusión para enviar datos simultáneamente a varios clientes** , configure las opciones siguientes:  

-   **Cuenta de conexión de multidifusión**: especifique la cuenta que se debe usar al configurar conexiones de base de datos de Configuration Manager para la multidifusión.  

-   **Configuración de dirección de multidifusión**: especifique las direcciones IP usadas para enviar datos a los equipos de destino. De forma predeterminada, se obtiene la dirección IP de un servidor DHCP que esté habilitado para distribuir direcciones de multidifusión. Dependiendo del entorno de red, puede especificar un intervalo de direcciones IP entre 239.0.0.0 y 239.255.255.255.  

    > [!IMPORTANT]  
    >  Las direcciones IP que se configuran deben ser accesibles para los equipos de destino que solicitan la imagen de sistema operativo. Compruebe que los enrutadores y firewalls permiten tráfico de multidifusión entre el equipo de destino y el servidor del sitio.  

-   **Intervalo de puertos UDP para multidifusión**: especifique el intervalo de puertos de protocolo de datagramas de usuario (UDP) que se utilizaron para enviar datos a los equipos de destino.  

    > [!IMPORTANT]  
    >  Los puertos UDP deben ser accesibles para los equipos de destino que soliciten la imagen de sistema operativo. Compruebe que los enrutadores y firewalls permiten tráfico de multidifusión entre el equipo de destino y el servidor del sitio.  

-   **Velocidad de transferencia de cliente**: seleccione la velocidad de transferencia que se utiliza para descargar datos en los equipos de destino.  

-   **Número máximo de clientes**: especifique el número máximo de equipos de destino que pueden descargar el sistema operativo desde este punto de distribución.  

-   **Habilitar multidifusión programada**: especifique cómo Configuration Manager controla cuándo se debe iniciar la implementación de sistemas operativos en los equipos de destino. Una vez seleccionado, configure las siguientes opciones:  

    -   **Retraso de inicio de sesión (minutos)**: especifique el número de minutos que Configuration Manager espera antes de responder a la primera solicitud de implementación.  

    -   **Tamaño de sesión mínimo (clientes)**: especifique cuántas solicitudes deben recibirse para que Configuration Manager inicie la implementación del sistema operativo.  

> [!NOTE]  
>  Las implementaciones de multidifusión ahorran ancho de banda de red al enviar datos simultáneamente a varios clientes de Configuration Manager, en lugar de enviar una copia de los datos a cada cliente a través conexiones independientes. Para obtener más información sobre el uso de la multidifusión para implementar sistemas operativos, consulte [Use multicast to deploy Windows over the network with System Center Configuration Manager (Usar la multidifusión para implementar Windows a través de la red con System Center Configuration Manager)](../../../../osd/deploy-use/use-multicast-to-deploy-windows-over-the-network.md).  

### <a name="group-relationships"></a>Relaciones de grupo  

> [!NOTE]  
>  Estas opciones solo están disponibles cuando se editan las propiedades de un punto de distribución previamente instalado.  

Administre los grupos de puntos de distribución de los que es miembro este punto de distribución.  

Para agregar este punto de distribución como miembro a un grupo de puntos de distribución existente, haga clic en **Agregar**. Seleccione un grupo de puntos de distribución existente en la lista del cuadro de diálogo **Agregar grupos de puntos de distribución** y, a continuación, haga clic en **Aceptar**.  

Para quitar este punto de distribución de un grupo de puntos de distribución, seleccione el grupo en la lista y, a continuación, haga clic en **Quitar**.  

### <a name="content"></a>Content  

> [!NOTE]  
>  Estas opciones solo están disponibles cuando se editan las propiedades de un punto de distribución previamente instalado.  

Administre el contenido distribuido en el punto de distribución. La sección Paquetes de implementación proporciona una lista de los paquetes distribuidos en este punto de distribución. Puede seleccionar un paquete de la lista y realizar las siguientes acciones:  

-   **Validar**: se inicia el proceso de validar la integridad de los archivos de contenido en el paquete. Para ver los resultados del proceso de validación de contenido, en el área de trabajo **Supervisión** , expanda **Estado de distribución**y, a continuación, haga clic en el nodo **Estado de contenido** .  

-   **Redistribuir**: se copian todos los archivos de contenido del paquete en el punto de distribución y se sobrescriben los archivos existentes. Esta operación se suele usar para reparar archivos de contenido en el paquete.  

-   **Quitar**: se quitan archivos de contenido del punto de distribución para el paquete.  

### <a name="content-validation"></a>Validación de contenido  
Especifique si desea establecer una programación para validar la integridad de los archivos de contenido en el punto de distribución. Si habilita la validación de contenido de forma programada, Configuration Manager inicia el proceso a la hora programada y se comprueba todo el contenido del punto de distribución. También puede configurar la prioridad de la validación de contenido. De forma predeterminada, la prioridad está establecida en **La más baja**.  

Para ver los resultados del proceso de validación de contenido, en el área de trabajo **Supervisión** , expanda **Estado de distribución**y, a continuación, haga clic en el nodo **Estado de contenido** . Se muestra el contenido de cada tipo de paquete (por ejemplo, Aplicación, Paquete de actualización de software e Imagen de arranque).  

> [!WARNING]  
>  Aunque la programación de la validación de contenido se especifica mediante la hora local del equipo, la programación se muestra en la consola de Configuration Manager mediante UTC.  

### <a name="boundary-group"></a>Grupo de límites  
Administre los grupos de límites a los que se asigna este punto de distribución. Puede asociar grupos de límites a un punto de distribución. Durante la distribución de contenido, los clientes deben estar en un grupo de límites que esté asociado con el punto de distribución para utilizarlo como una ubicación de origen para el contenido. Puede activar la casilla **Permitir a los clientes utilizar este sistema del sitio como ubicación de origen de reserva para contenido** para permitir a los clientes que están fuera de estos grupos de límites que reserven y usen el punto de distribución como una ubicación de origen para el contenido cuando no estén disponibles otros puntos de distribución.  

Para obtener más información sobre los puntos de distribución preferidos, consulte [Fundamental concepts for content management in System Center Configuration Manager (Conceptos básicos de la administración de contenido en System Center Configuration Manager)](../../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md).  

### <a name="schedule"></a>Programa  

> [!NOTE]  
>  Estas opciones solo están disponibles cuando se editan las propiedades de un punto de distribución previamente instalado.  

> [!TIP]  
>  Esta ficha solo está disponible al editar las propiedades de un punto de distribución que es remoto desde el equipo de servidor del sitio.  

 Especifique si quiere configurar una programación que limite cuándo puede Configuration Manager transferir datos al punto de distribución.  

> [!IMPORTANT]  
>  La programación se basa en la zona horaria del sitio de envío, no del punto de distribución.  

Para restringir datos, seleccione el período de tiempo y, a continuación, seleccione una de las siguientes opciones para **Disponibilidad**:  

-   **Abrir para todas las prioridades**: especifica que Configuration Manager envíe datos al punto de distribución sin restricciones.  

-   **Permitir alta y media prioridad**: especifica que Configuration Manager envíe solo los datos de prioridad media y alta al punto de distribución.  

-   **Permitir solo prioridad alta**: especifica que Configuration Manager envíe solo los datos de prioridad alta al punto de distribución.  

-   **Cerrado**: especifica que Configuration Manager no envíe datos al punto de distribución.  

Puede restringir los datos por prioridad o cerrar la conexión durante períodos de tiempo seleccionados.  

### <a name="rate-limits"></a>Límites de frecuencia  

> [!NOTE]  
>  Estas opciones solo están disponibles cuando se editan las propiedades de un punto de distribución previamente instalado.  

> [!TIP]  
>  Esta ficha solo está disponible al editar las propiedades de un punto de distribución que es remoto desde el equipo de servidor del sitio.  

Especifique si desea configurar límites de velocidad para controlar el ancho de banda de red que se usa al transferir contenido al punto de distribución. Puede elegir entre las siguientes opciones:  

-   **Ilimitado en los envíos a este destino**: especifica que Configuration Manager envíe contenido al punto de distribución sin restricciones de velocidad.  

-   **Modo por pulsos**: especifica el tamaño de los bloques de datos que se envían al punto de distribución. También puede especificar un retraso de tiempo entre el envío de cada bloque de datos. Utilice esta opción cuando tenga que enviar datos a través de una conexión de red con un ancho de banda muy bajo al punto de distribución. Por ejemplo, podría tener limitaciones al enviar 1 KB de datos cada cinco segundos, independientemente de la velocidad del vínculo o su uso en un momento dado.  

-   **Limitado al máximo especificado de velocidades de transferencia por hora**: especifique esta opción para que un sitio envíe datos a un punto de distribución usando solo el porcentaje de tiempo que configure. Cuando use esta opción, Configuration Manager no identifica el ancho de banda disponible de las redes, sino que divide el tiempo en que puede enviar datos en intervalos de tiempo. A continuación, se envían datos durante un corto periodo de tiempo, seguido de periodos de tiempo en que no se envían datos. Por ejemplo, si la velocidad máxima se establece en **50 %**, Configuration Manager transmitirá datos durante un periodo de tiempo seguido de un periodo de tiempo igual en que no se enviarán datos. La cantidad real de datos, o el tamaño del bloque de datos, no se administra. En su lugar, solo se administra la cantidad de tiempo durante la cual se envían datos.  



<!--HONumber=Nov16_HO1-->


