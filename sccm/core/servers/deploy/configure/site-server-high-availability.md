---
title: Alta disponibilidad de servidor de sitio
titleSuffix: Configuration Manager
description: Cómo configurar la alta disponibilidad del servidor de sitio de Configuration Manager mediante la adición de un servidor de sitio de modo pasivo.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 6dcef836-c0d1-40af-ad30-cd8d864b09a9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 912bdb93db05091ff756c51ee9f951a17a76ff5d
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/31/2018
ms.locfileid: "39385976"
---
# <a name="site-server-high-availability-in-configuration-manager"></a>Alta disponibilidad de servidor de sitio en Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

<!--1128774-->

A partir de la versión 1806 de Configuration Manager, la alta disponibilidad del rol de servidor de sitio es una solución basada en Configuration Manager para instalar un servidor de sitio adicional en modo *pasivo*. El servidor de sitio en modo pasivo se suma al servidor de sitio existente que está en modo *activo*. Un servidor de sitio en modo pasivo está disponible para uso inmediato, cuando sea necesario. Incluya este servidor de sitio adicional como parte del diseño general para que el servicio de Configuration Manager sea de [alta disponibilidad](/sccm/core/servers/deploy/configure/high-availability-options).  

Un servidor de sitio en modo pasivo:
- Utiliza la misma base de datos de sitio que el servidor de sitio en modo activo.
- No escribe datos en la base de datos de sitio cuando está en modo pasivo.
- Utiliza la misma biblioteca de contenido que el servidor de sitio en modo activo.

Para activar el servidor de sitio en modo pasivo, se *promueve* manualmente. Esta acción cambia el servidor de sitio en modo activo para que sea el servidor de sitio en modo pasivo. Los roles de sistema de sitio que están disponibles en el servidor de modo activo original siguen estando disponibles, siempre y cuando sea posible tener acceso a ese equipo. Solo el rol de servidor de sitio cambia entre los modos activo y pasivo.

> [!Note]  
> Configuration Manager no habilita esta característica opcional de forma predeterminada. Deberá habilitarla para poder usarla. Para obtener más información, consulte [Habilitar características opcionales de las actualizaciones](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).



## <a name="prerequisites"></a>Requisitos previos

- El servidor de sitio en modo pasivo puede ser local o estar basado en la nube de Azure.  
    > [!Note]  
    > Un servidor de sitio en modo pasivo basado en la nube utiliza la infraestructura como servicio (IaaS) de Azure. Vea los siguientes artículos para más información:  
    > - [Máquinas virtuales de Azure (para infraestructuras basadas en la nube)](/sccm/core/understand/use-cloud-services#azure-virtual-machines-for-cloud-based-infrastructure)
    > - [Preguntas más frecuentes sobre Configuration Manager en Azure](/sccm/core/understand/configuration-manager-on-azure)  

- Ambos servidores de sitio deben estar unidos al mismo dominio de Active Directory.  

- El sitio es un sitio primario independiente. 

- Ambos servidores de sitio deben utilizar la misma base de datos de sitio, que debe ser remota para cada servidor de sitio.  

     - Ambos servidores de sitio necesitan permisos de **sysadmin** en la instancia de SQL Server que hospeda la base de datos de sitio.

     - El servidor SQL Server que hospeda la base de datos de sitio puede utilizar una instancia predeterminada, una instancia con nombre, el [clúster de SQL Server](/sccm/core/servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database) o un [grupo de disponibilidad de SQL Server AlwaysOn](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database).  

     - El servidor de sitio en modo pasivo está configurado para utilizar la misma base de datos de sitio que el servidor de sitio en modo activo. El servidor de sitio en modo pasivo solo lee en la base de datos. No escribe en la base de datos hasta que se promueva al modo activo.  

- La biblioteca de contenido de sitio debe estar en un recurso compartido de red remoto. Ambos servidores de sitio necesitan permisos de control total en el recurso compartido y su contenido. Para más información, vea [Manage content library](/sccm/core/plan-design/hierarchy/the-content-library#manage-content-library) (Administrar la biblioteca de contenido).<!--1357525-->  

    - El servidor de sitio no puede tener el rol de punto de distribución. El punto de distribución también usa la biblioteca de contenido, y este rol no admite una biblioteca de contenido remota. Después de mover la biblioteca de contenido, no se puede agregar el rol de punto de distribución al servidor de sitio.  

- El servidor de sitio en modo pasivo:  

     - Debe cumplir los [requisitos previos para instalar un sitio primario](/sccm/core/servers/deploy/install/prerequisites-for-installing-sites#primary-sites-and-the-central-administration-site).  

     - Su cuenta de equipo debe estar en el grupo de administradores locales del servidor de sitio en modo activo.<!--516036-->

     - Se instala con archivos de origen que coinciden con la versión del servidor de sitio en modo activo.  

     - No puede tener un rol de sistema de sitio de ningún sitio antes de instalar el rol de servidor de sitio en modo pasivo.  

- Ambos servidores de sitio pueden ejecutar distintas versiones del sistema operativo o del Service Pack, siempre que ambos sean [compatibles con Configuration Manager](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers).  



## <a name="limitations"></a>Limitaciones
- En cada sitio primario se admite un solo servidor de sitio en modo pasivo.  

- No se admite un servidor de sitio en modo pasivo en una jerarquía. Una jerarquía incluye un sitio de administración central y un sitio primario secundario. Solo puede crear un servidor de sitio en modo pasivo en un sitio primario independiente.<!--1358224-->

- No se admite un servidor de sitio en modo pasivo en un sitio secundario.<!--SCCMDocs issue 680-->  

- La promoción del servidor de sitio en modo pasivo al modo activo es manual. No hay ninguna conmutación automática por error.  

- No se pueden instalar roles de sistema de sitio en el nuevo servidor antes de agregar el servidor de sitio en modo pasivo.  

    > [!Note]  
    > Cuando instale el servidor de sitio en modo pasivo, puede agregar roles adicionales según sea necesario. Por ejemplo, el proveedor de SMS o un punto de administración en un sitio primario.  

- En el caso de roles como el punto de notificación que utilizan una base de datos, hospede la base de datos en un servidor que sea remoto para los dos servidores de sitio.  

- El proveedor de SMS no se instala en el servidor de sitio en modo pasivo. Conéctese a un proveedor del sitio para promover manualmente el servidor de sitio en modo pasivo al modo activo. Instale al menos una instancia adicional del proveedor en otro servidor. Para más información, vea [Plan for the SMS Provider](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider) (Planear el proveedor de SMS).  

- La consola de Configuration Manager no se instala automáticamente en el servidor de sitio en modo pasivo.  



## <a name="add-a-site-server-in-passive-mode"></a>Adición de un servidor de sitio en el modo pasivo

Para más información sobre el proceso general de la adición de roles, vea [Install site system roles](/sccm/core/servers/deploy/configure/install-site-system-roles) (Instalar roles de sistema de sitio).

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Configuración del sitio**, seleccione el nodo **Sitios** y, en la cinta, haga clic en **Crear servidor del sistema de sitio**.   

2. En la página **General** del Asistente para crear servidor de sistema de sitio, especifique el servidor que va a hospedar el servidor de sitio en modo pasivo. El servidor que especifique no puede hospedar ningún rol de sistema de sitio para que se pueda instalar un servidor de sitio en modo pasivo.  

3. En la página **Selección de rol del sistema**, seleccione únicamente **Site server in passive mode** (Servidor de sitio en modo pasivo).  

    > [!Note]  
    > El asistente realiza las siguientes comprobaciones de requisitos previos iniciales en esta página:  
    > - El servidor seleccionado no es un servidor de sitio secundario
    > - El servidor seleccionado no es ya un servidor de sitio en modo pasivo
    > - La biblioteca de contenido del sitio se encuentra en una ubicación remota  
    >  
    > Si las comprobaciones de requisitos previos iniciales no se realizan, no podrá continuar más allá de esta página del asistente.  

4. En la página **Servidor de sitio en modo pasivo**, especifique la siguiente información, que sirve para ejecutar el programa de instalación e instalar el rol de servidor de sitio, en el servidor especificado:

     - Elija una de las siguientes opciones:  

         - **Copy installation source files over the network from the site server in active mode** (Copiar los archivos de origen de instalación a través de la red desde el servidor de sitio en modo activo): esta opción crea un paquete comprimido y lo envía al nuevo servidor de sitio.  

         - **Use the source files at the following location on the site server in passive mode** (Usar los archivos de origen en la siguiente ubicación del servidor de sitio en modo pasivo): por ejemplo, una ruta de acceso local en la que ya ha copiado los archivos de origen. Asegúrese de que este contenido tiene la misma versión que el servidor de sitio en modo activo.  

         - (*Recomendado*) **Use the source files at the following network location** (usar los archivos de origen en la siguiente ubicación de red): especifique la ruta de acceso directamente al contenido de la carpeta **CD.Latest** del servidor de sitio en modo activo. Por ejemplo, `\\Server\SMS_ABC\CD.Latest`, donde "*Server*" es el nombre del servidor de sitio en modo activo y "*ABC*" es el código de sitio.  

     - Especifique la ruta de acceso local en el nuevo servidor de sitio donde se va a instalar Configuration Manager. Por ejemplo: `C:\Program Files\Configuration Manager`  

5. Complete el asistente. Configuration Manager instala entonces el servidor de sitio en modo pasivo en el servidor especificado.

Para obtener información detallada sobre el estado de la instalación, vaya al área de trabajo **Supervisión** de la consola y seleccione el nodo **Estado del servidor de sitio**. El estado del servidor de sitio en modo pasivo aparece como **Instalando**. Para más información, seleccione el servidor y haga clic en **Mostrar estado**. Esta acción abre la ventana de estado de instalación del servidor de sitio. Una vez completado el proceso, se muestra el estado **Correcto** para ambos servidores.   

Para más información sobre el proceso de instalación, vea [Diagrama de flujo: configuración de un servidor de sitio en modo pasivo](/sccm/core/servers/deploy/configure/passive-site-server-flowchart).

Después de agregar un servidor de sitio en modo pasivo, vea ambos servidores de sitio en la pestaña **Nodos** del nodo **Sitios** de la consola. 

Todos los componentes del servidor de sitio de Configuration Manager se encuentran en modo de espera en el servidor de sitio en modo pasivo. Los servicios de Windows siguen ejecutándose.



## <a name="site-server-promotion"></a>Promoción del servidor de sitio  

Del mismo modo que con copia de seguridad y recuperación, planee y practique el proceso para cambiar los servidores de sitio. Plantéese los siguientes puntos en el plan de promoción:  

- Practique una promoción planeada, donde ambos servidores de sitio están en línea. Practique también una conmutación por error no planificada, desconectando o apagando de manera forzada el servidor del sitio en modo activo.  

- Determine los procesos operativos durante la conmutación por error y lo que se comunica a otros administradores de Configuration Manager.  

- Antes de una promoción planeada:  

    - Compruebe el estado general del sitio y los componentes del sitio. Asegúrese de que todo está correcto como de costumbre en su entorno.  

    - Compruebe el estado de contenido de los paquetes que se repliquen activamente entre sitios.  

    - No inicie nuevos trabajos de distribución de contenido. 

        > [!Note]  
        > Si durante la conmutación por error hay una replicación de archivos entre sitios en curso, el nuevo servidor de sitio no puede recibir el archivo replicado. Si esto ocurre, redistribuya el contenido de software cuando el nuevo servidor de sitio esté activo.<!--515436-->  


### <a name="process-to-promote-the-site-server-in-passive-mode-to-active-mode"></a>Proceso de promoción del servidor de sitio en modo pasivo al modo activo

En esta sección se describe cómo cambiar el servidor de sitio en modo pasivo al modo activo. Para tener acceso al sitio y realizar este cambio, ha de tener acceso a una instancia del proveedor de SMS. Para más información, vea [Use multiple SMS Providers](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider#BKMK_MultiSMSProv) (Usar varios proveedores de SMS).  

> [!Important]  
> De forma predeterminada, solo el servidor de sitio original tiene el rol de proveedor de SMS. Si este servidor está sin conexión, no podrá conectarse al sitio porque no hay ningún proveedor disponible. Al agregar el servidor de sitio en modo pasivo, el proveedor de SMS no se agrega automáticamente. Agregue al menos un rol de proveedor de SMS adicional al sitio para tener un servicio de alta disponibilidad.  

> [!Tip]  
> La consola de Configuration Manager solicita la lista de proveedores de SMS de WMI disponibles en el servidor de sitio. Cuando se instalan varios proveedores de SMS en un sitio, el sitio asigna de forma aleatoria cada nueva solicitud de conexión para que use un proveedor de SMS instalado. No se puede especificar la ubicación del proveedor de SMS para utilizarla con una sesión de conexión específica. Si la consola no puede conectarse al sitio porque el servidor de sitio actual está sin conexión, especifique el otro servidor del sitio en la ventana de conexión de sitio.  

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Configuración del sitio** y seleccione el nodo **Sitios**. Seleccione el sitio y luego cambie a la pestaña **Nodos**. Seleccione el servidor de sitio en modo pasivo y luego, en la cinta, haga clic en **Promover a activo**. Haga clic en **Sí** para confirmar y continuar.   
  
2. Actualice el nodo de la consola. La columna **Estado** del servidor que se promueve aparece en la pestaña **Nodos** como **Promoviendo**.  

3. Una vez completada la promoción, la columna **Estado** muestra el estado **Correcto** tanto para el nuevo servidor de sitio en modo activo como para el nuevo servidor de sitio en modo pasivo. La columna **Nombre del servidor** del sitio muestra ahora el nombre del nuevo servidor de sitio en modo activo.

Para obtener información detallada sobre el estado, vaya al área de trabajo **Supervisión** y seleccione el nodo **Estado del servidor de sitio**. La columna **Modo** identifica qué servidor está *Activo* o *Pasivo*. Al promover un servidor en modo pasivo a modo activo, seleccione el servidor de sitio que va a promover y, en la cinta, elija **Mostrar estado**. Se abrirá la ventana Site Server Promotion Status (Estado de promoción del servidor de sitio), que muestra otros detalles sobre el proceso.

Cuando un servidor de sitio en modo activo cambia a modo pasivo, únicamente el rol de sistema de sitio pasa a pasivo. Todos los demás roles de sistema de sitio instalados en ese equipo permanecen activos y accesibles para los clientes.

Para más información sobre el proceso de promoción *planeada*, vea [Diagrama de flujo: promoción del servidor de sitio (planeada)](/sccm/core/servers/deploy/configure/promote-site-server-flowchart).


### <a name="unplanned-failover"></a>Conmutación por error no planeada

Si el servidor de sitio en modo activo actual está sin conexión, el servidor de sitio en promoción intenta ponerse en contacto con él durante 30 minutos. Si el servidor sin conexión se recupera antes de ese tiempo, se notifica correctamente y el cambio se realiza sin problemas. En caso contrario, el servidor de sitio en promoción actualiza de manera forzada la configuración del sitio para que esté activo. Si el servidor sin conexión se recupera después de este tiempo, comprueba primero el estado actual de la base de datos del sitio. Luego continúa con las disminución de su nivel al servidor de sitio en modo pasivo.

Durante este período de espera de 30 minutos, el sitio no tiene ningún servidor de sitio en modo activo. Los clientes todavía se comunican con los roles de cara al cliente, tales como puntos de administración, puntos de actualización de software y puntos de distribución. Los usuarios pueden instalar software que ya se ha implementado. No es posible ninguna administración de sitios en este período de tiempo. Para más información, vea [Impactos de errores de sitio](/sccm/core/servers/manage/site-failure-impacts).  

Si el servidor sin conexión está dañado, de tal forma que no puede recuperarse, elimine este servidor de sitio de la consola. Cree luego un nuevo servidor de sitio en modo pasivo para restaurar un servicio de alta disponibilidad. 

Para más información sobre el proceso de conmutación por error *no planeada*, vea [Diagrama de flujo: promoción del servidor de sitio (no planeada)](/sccm/core/servers/deploy/configure/promote-site-server-unplanned-flowchart).


### <a name="additional-tasks-after-site-server-promotion"></a>Tareas adicionales después de la promoción del servidor de sitio  

Después de cambiar de servidor de sitio, no tiene que realizar la mayoría de las demás tareas necesarias al [recuperar un sitio](/sccm/core/servers/manage/recover-sites#post-recovery-tasks). Por ejemplo, no es necesario restablecer las contraseñas ni volver a conectarse a su suscripción a Microsoft Intune.

Puede que se requieran los siguientes pasos si es necesario en su entorno:  

- Si importa certificados PKI de puntos de distribución, vuelva a importar el certificado de los servidores afectados. Para más información, vea [Regeneración de los certificados para puntos de distribución](/sccm/core/servers/manage/recover-sites#regenerate-the-certificates-for-distribution-points).  

- Si Configuration Manager se integra con Microsoft Store para Empresas, vuelva a configurar esa conexión. Para más información, vea [Manage apps from the Microsoft Store for Business](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business) (Administrar aplicaciones desde Microsoft Store para Empresas).  



## <a name="daily-monitoring"></a>Supervisión diaria

Cuando haya un servidor de sitio en modo pasivo, supervíselo diariamente. Asegúrese de que su estado sigue siendo Correcto y está listo para su uso. En la consola de Configuration Manager, vaya al área de trabajo **Supervisión** y seleccione el nodo **Estado del servidor de sitio**. Vea ambos servidores de sitio y su estado actual. Vea también el estado en el área de trabajo **Administración**. Expanda **Configuración del sitio** y seleccione el nodo **Sitios**. Seleccione el sitio y luego cambie a la pestaña **Nodos**. 
