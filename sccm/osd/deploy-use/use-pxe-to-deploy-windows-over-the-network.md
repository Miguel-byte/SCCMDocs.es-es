---
title: Usar PXE para OSD a través de la red
titleSuffix: Configuration Manager
description: Use las implementaciones de SO iniciadas por PXE para actualizar el sistema operativo de un equipo o instalar una versión nueva de Windows en un equipo nuevo.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: da5f8b61-2386-4530-ad54-1a5c51911f07
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 75e463d27475e82677e91b00bfba4c4287d463ee
ms.sourcegitcommit: f2a1fa59fb3870a6bebca61daf15c0c157e9fdd6
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/04/2019
ms.locfileid: "54030995"
---
# <a name="use-pxe-to-deploy-windows-over-the-network-with-configuration-manager"></a>Usar el entorno PXE para implementar Windows a través de la red con Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Las implementaciones de SO iniciadas por el entorno de ejecución previo al arranque (PXE) en Configuration Manager permiten que los clientes soliciten e implementen sistemas operativos a través de la red. En este escenario de implementación, se envía la imagen de SO y las imágenes de arranque a un punto de distribución habilitado para PXE.

> [!NOTE]  
>  Cuando se crea una implementación de SO dirigida únicamente a equipos con BIOS para x64, tanto la imagen de arranque para x64 como la imagen de arranque para x86 deben estar disponibles en el punto de distribución.

Se pueden usar las implementaciones de SO iniciadas por PXE en los escenarios siguientes:

-   [Actualizar un equipo existente con una nueva versión de Windows](/sccm/osd/deploy-use/refresh-an-existing-computer-with-a-new-version-of-windows)  

-   [Instalar una nueva versión de Windows en un equipo nuevo (sin sistema operativo)](/sccm/osd/deploy-use/install-new-windows-version-new-computer-bare-metal)  

Complete los pasos de uno de los escenarios de implementación de SO y luego use las secciones de este artículo para prepararse para las implementaciones iniciadas por PXE.



##  <a name="BKMK_Configure"></a> Configure al menos un punto de distribución para aceptar solicitudes PXE

Para implementar sistemas operativos en clientes de Configuration Manager que efectúan solicitudes de arranque PXE, debe configurar uno o varios puntos de distribución para que acepten las solicitudes PXE. Una vez configurado el punto de distribución, responde a las solicitudes de arranque de PXE y determina las acciones de implementación adecuadas que se van a llevar a cabo. Para obtener más información, consulte [Instalar o modificar un punto de distribución](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).  

> [!NOTE]  
>  Al configurar un único punto de distribución habilitado con PXE para admitir varias subredes, no se permite usar las opciones de DHCP. Configure aplicaciones auxiliares de IP en los enrutadores para permitir que las solicitudes PXE se reenvíen a los puntos de distribución habilitados con PXE.

> [!NOTE]  
>  No se puede usar el respondedor del entorno PXE sin WDS en servidores que también estén ejecutando un servidor DHCP.

## <a name="prepare-a-pxe-enabled-boot-image"></a>Preparar una imagen de arranque habilitada para PXE

Para usar PXE para implementar un sistema operativo, debe distribuir imágenes de arranque x86 y x64 habilitadas para PXE a uno o varios puntos de distribución habilitados para PXE. Use la información para habilitar PXE en una imagen de arranque y distribuirla a los puntos de distribución:

-   Para habilitar PXE en una imagen de arranque, seleccione **Implementar esta imagen de arranque desde el punto de distribución habilitado con PXE** en la pestaña **Origen de datos** de las propiedades de la imagen de arranque.

-   Si cambia las propiedades de la imagen de arranque, actualice dicha imagen y vuelva a distribuirla a los puntos de distribución. Para obtener más información, consulte [Distribute content (Distribución del contenido)](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_distribute).



##  <a name="BKMK_PXEExclusionList"></a> Crear una lista de exclusión para las implementaciones de PXE

Cuando implementa sistemas operativos con PXE, puede crear una lista de exclusión en cada punto de distribución. Agregue las direcciones MAC a la lista de exclusión de los equipos que quiere que el punto de distribución ignore. Los equipos indicados no reciben las secuencias de tareas de implementación que Configuration Manager usa para la implementación de PXE.

#### <a name="to-create-the-exclusion-list"></a>Para crear la lista de exclusión

1.  Cree un archivo de texto en el punto de distribución que está habilitado para PXE. Por ejemplo, puede llamar a este archivo de texto **pxeExceptions.txt**.  

2.  Utilice un editor de texto sin formato, como el Bloc de notas, y agregue las direcciones MAC de los equipos que el punto de distribución habilitado para PXE debe ignorar. Separar los valores de dirección MAC por dos puntos y escriba cada dirección en una línea independiente. Por ejemplo: `01:23:45:67:89:ab`  

3.  Guarde el archivo de texto en el servidor de sistema de sitio del punto de distribución habilitado por PXE. El archivo de texto se puede guardar en cualquier ubicación en el servidor.  

4.  Edite el Registro del punto de distribución habilitado para PXE para crear una clave del Registro **MACIgnoreListFile**. Agregue el valor de cadena de la ruta de acceso completa para el archivo de texto en el servidor de sistema de sitio del punto de distribución habilitado para PXE. Utilice la siguiente ruta de acceso para el Registro:  

     `HKLM\Software\Microsoft\SMS\DP`  

    > [!WARNING]  
    >  Si utiliza incorrectamente el Editor del Registro, podría causar problemas graves que quizás requieran volver a instalar el sistema operativo. Microsoft no puede garantizar que pueda resolver problemas ocasionados por un uso incorrecto del Editor del Registro. Utilice el Editor del Registro bajo su responsabilidad.  

5. Reinicie el servicio WDS o el servicio del respondedor PXE después de realizar este cambio de registro. No es necesario reiniciar el servidor.<!--512129-->  



## <a name="manage-duplicate-hardware-identifiers"></a>Administrar identificadores de hardware duplicados

Configuration Manager puede reconocer varios equipos como el mismo dispositivo si tienen atributos SMBIOS duplicados o si se usa un adaptador de red compartido. Puede mitigar estos problemas mediante la administración de los identificadores de hardware duplicados en la configuración de la jerarquía. Para obtener más información, vea [Administrar identificadores de hardware duplicados](/sccm/core/clients/manage/manage-clients#manage-duplicate-hardware-identifiers).



##  <a name="BKMK_RamDiskTFTP"></a> Tamaño de bloque de TFTP de RamDisk y tamaño de ventana

Se pueden personalizar los tamaños de bloque de TFTP de RamDisk y de ventana para los puntos de distribución habilitados con PXE. Si ha personalizado la red, un tamaño de bloque o ventana grande podría provocar que se produjera un error de tiempo de espera en la descarga de la imagen de arranque. Las personalizaciones del tamaño del bloque y la ventana de TFTP de RamDisk permiten optimizar el tráfico de TFTP al usar PXE para cumplir los requisitos de red específicos. Para determinar la configuración más eficaz, pruebe la configuración personalizada en el entorno. Para obtener más información, consulte [Customize the RamDisk TFTP block size and window size on PXE-enabled distribution points](/sccm/osd/get-started/prepare-site-system-roles-for-operating-system-deployments#BKMK_RamDiskTFTP) (Personalización del tamaño de bloque de TFTP de RamDisk y el tamaño de la ventana de puntos de distribución habilitados con el entorno PXE).



## <a name="configure-deployment-settings"></a>Configurar la implementación

Para usar una implementación de SO iniciada por PXE, configure la implementación para que el sistema operativo esté disponible para las solicitudes de arranque de PXE. Configure los sistemas operativos disponibles en la pestaña **Configuración de implementación** de las propiedades de implementación. Para el valor **Estar disponible para**, seleccione una de las opciones siguientes:

-   Clientes de Configuration Manager, medios y PXE

-   Solo medios y PXE

-   Sólo medios y PXE (ocultos)



##  <a name="BKMK_Deploy"></a> Implementar la secuencia de tareas

Implemente el sistema operativo en una recopilación de destino. Para obtener más información, vea [Deploy a task sequence](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS). Al implementar sistemas operativos mediante PXE, puede configurar que la implementación sea necesaria o esté disponible.

-   **Implementación requerida**: las implementaciones requeridas utilizarán el entorno PXE sin intervención del usuario. El usuario no puede omitir el arranque de PXE. Pero si el usuario cancela el arranque de PXE antes de que responda el punto de distribución, el sistema operativo no se implementa.

-   **Implementación disponible**: las implementaciones disponibles requieren que el usuario esté presente en el equipo de destino. El usuario debe presionar la tecla **F12** para continuar el proceso de arranque de PXE. Si el usuario no está presente para presionar **F12**, el equipo arrancará en el sistema operativo actual o desde el siguiente dispositivo de arranque disponible.

Puede realizar de nuevo una implementación del entorno PXE requerida. Para ello, borre el estado de la última implementación del entorno PXE asignada a un equipo o a una recopilación de Configuration Manager. Para obtener más información sobre la acción **Borrar implementaciones de PXE requeridas**, vea [Administrar clientes](/sccm/core/clients/manage/manage-clients#BKMK_ManagingClients_DevicesNode) o [Administrar recopilaciones](/sccm/core/clients/manage/collections/manage-collections#how-to-manage-device-collections). Esta acción restablece el estado de la implementación, y vuelve a instalar las implementaciones requeridas más recientes.

> [!IMPORTANT]  
> El protocolo PXE no es seguro. Asegúrese de que el servidor PXE y el cliente de PXE se encuentran en una red físicamente segura, como, por ejemplo, en un centro de datos, para evitar accesos no autorizados al sitio.



##  <a name="how-is-the-boot-image-selected-for-clients-booting-with-pxe"></a>¿Cómo se selecciona la imagen de arranque para los clientes que arrancan con el entorno PXE?

Cuando un cliente arranca con el entorno PXE, Configuration Manager ofrece al cliente una imagen de arranque. Configuration Manager usa una imagen de arranque con una coincidencia de arquitectura exacta. Si no hay disponible una imagen de arranque con la arquitectura exacta, Configuration Manager usa una imagen de arranque con una arquitectura compatible. 

En la lista siguiente se proporciona información sobre cómo se selecciona una imagen de arranque para los clientes que arrancan con el entorno PXE:  

1. Configuration Manager busca en la base de datos de sitio un registro del sistema que coincida con la dirección MAC o SMBIOS del cliente que está intentando arrancar.  

    > [!NOTE]  
    > Si un equipo que se asigna a un sitio se arranca en PXE para un sitio diferente, las directivas no son visibles para el equipo. Por ejemplo, si un cliente ya está asignado al sitio A, el punto de administración y el punto de distribución para el sitio B no pueden tener acceso a las directivas del sitio A y el cliente no arranca PXE correctamente.  

2. Configuration Manager busca secuencias de tareas que estén implementadas en el registro del sistema que se encontró en el paso 1.  

3. En la lista de las secuencias de tareas que se encontraron en el paso 2, Configuration Manager busca una imagen de arranque que coincida con la arquitectura del cliente que está intentando arrancar. Si se encuentra una imagen de arranque con la misma arquitectura, se usa esa imagen.  

4. Si no se encuentra una imagen de arranque con la misma arquitectura, Configuration Manager busca una imagen de arranque que sea compatible con la arquitectura del cliente. Busca en la lista de secuencias de tareas que se encuentra en el paso 2. Por ejemplo, un cliente de 64 bits es compatible con imágenes de arranque de 32 bits y 64 bits. Un cliente de 32 bits solo es compatible con imágenes de arranque de 32 bits. Un cliente UEFI solo es compatible con imágenes de arranque de 64 bits.  
