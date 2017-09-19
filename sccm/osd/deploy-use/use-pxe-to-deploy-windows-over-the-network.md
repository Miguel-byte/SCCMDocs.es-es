---
title: "Uso de PXE para implementar Windows a través de la red | Microsoft Docs"
description: "Use las implementaciones de sistema operativo iniciadas por el entorno PXE para actualizar el sistema operativo de un equipo o instalar una nueva versión de Windows en un equipo nuevo."
ms.custom: na
ms.date: 06/15/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: da5f8b61-2386-4530-ad54-1a5c51911f07
caps.latest.revision: "19"
caps.handback.revision: "0"
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.openlocfilehash: 57292b1c6f6e8b6be91eace06dbf12d788522e0b
ms.sourcegitcommit: 31c670a4bce74fd64a7d46ebf7702f65b80d4147
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/13/2017
---
# <a name="use-pxe-to-deploy-windows-over-the-network-with-system-center-configuration-manager"></a>Usar PXE para implementar Windows a través de la red con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Las implementaciones de sistema operativo iniciadas por el entorno de ejecución previo al arranque (PXE) en System Center Configuration Manager permiten que los equipos cliente soliciten e implementen sistemas operativos a través de la red. En este escenario de implementación, la imagen de sistema operativo y las imágenes de arranque de Windows PE (versiones x86 y x64) se envían a un punto de distribución que está configurado para aceptar solicitudes de arranque de PXE.

> [!NOTE]  
>  Cuando se crea una implementación de sistema operativo dirigida únicamente a equipos con BIOS para x64, tanto la imagen de arranque para x64 como la imagen de arranque para x86 deben estar disponibles en el punto de distribución.

Puede usar implementaciones de sistema operativo iniciadas por PXE en los siguientes escenarios de implementación de sistema operativo:

-   [Actualizar un equipo existente con una nueva versión de Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [Instalar una nueva versión de Windows en un equipo nuevo (sin sistema operativo)](install-new-windows-version-new-computer-bare-metal.md)  

Complete las etapas de uno de los escenarios de implementación de sistema operativo y luego use las secciones siguientes para prepararse para las implementaciones iniciadas por PXE.

##  <a name="BKMK_Configure"></a> Configure al menos un punto de distribución para aceptar solicitudes PXE
Para implementar sistemas operativos en clientes que realizan solicitudes de arranque PXE, debe usar uno o más puntos de distribución configurados para responder a las solicitudes de arranque PXE. Para conocer los pasos para habilitar el entorno PXE en un punto de distribución, consulte [Configuring distribution points to accept PXE requests](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint) (Configuración de puntos de distribución para aceptar solicitudes del entorno PXE).

## <a name="prepare-a-pxe-enabled-boot-image"></a>Preparar una imagen de arranque habilitada para PXE
Si quiere usar PXE para implementar un sistema operativo, debe distribuir imágenes de arranque x86 y x64 habilitadas para PXE a uno o varios puntos de distribución habilitados para PXE. Use la información para habilitar PXE en una imagen de arranque y distribuirla a los puntos de distribución:

-   Para habilitar PXE en una imagen de arranque, seleccione **Implementar esta imagen de arranque desde el punto de distribución habilitado con PXE** en la pestaña **Origen de datos** de las propiedades de la imagen de arranque.

-   Si cambia las propiedades de la imagen de arranque, vuelva a distribuir dicha imagen a los puntos de distribución. Para obtener más información, consulte [Distribute content (Distribución del contenido)](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).

##  <a name="BKMK_PXEExclusionList"></a> Crear una lista de exclusión para las implementaciones de PXE
Cuando implementa sistemas operativos con PXE, puede crear una lista de exclusión en cada punto de distribución. Agregue las direcciones MAC a la lista de exclusión de los equipos que quiere que el punto de distribución ignore. Los equipos de la lista no recibirán las secuencias de tareas de implementación que Configuration Manager usa para la implementación del entorno PXE.

#### <a name="to-create-the-exclusion-list"></a>Para crear la lista de exclusión

1.  Cree un archivo de texto en el punto de distribución que está habilitado para PXE. Por ejemplo, puede llamar a este archivo de texto **pxeExceptions.txt**.

2.  Utilice un editor de texto sin formato, como el Bloc de notas, y agregue las direcciones MAC de los equipos que el punto de distribución habilitado para PXE debe ignorar. Separar los valores de dirección MAC por dos puntos y escriba cada dirección en una línea independiente. Por ejemplo: `01:23:45:67:89:ab`

3.  Guarde el archivo de texto en el servidor de sistema de sitio del punto de distribución habilitado por PXE. El archivo de texto se puede guardar en cualquier ubicación en el servidor.

4.  Edite el Registro del punto de distribución habilitado para PXE para crear una clave del Registro **MACIgnoreListFile**. Agregue el valor de cadena de la ruta de acceso completa para el archivo de texto en el servidor de sistema de sitio del punto de distribución habilitado para PXE. Utilice la siguiente ruta de acceso para el Registro:

     **HKLM\Software\Microsoft\SMS\DP**  

    > [!WARNING]  
    >  Si utiliza incorrectamente el Editor del Registro, podría causar problemas graves que quizás requieran volver a instalar el sistema operativo. Microsoft no puede garantizar que pueda resolver problemas ocasionados por un uso incorrecto del Editor del Registro. Utilice el Editor del Registro bajo su responsabilidad.

     No es necesario reiniciar el servidor después de realizar este cambio en el Registro.

##  <a name="BKMK_RamDiskTFTP"></a> Tamaño de bloque de TFTP de RamDisk y tamaño de ventana
Puede personalizar el tamaño de bloque de TFTP de RamDisk y, a partir de Configuration Manager versión 1606, el tamaño de ventana de los puntos de distribución habilitados con el entorno PXE. El hecho de haber personalizado su red podría provocar que se produjera un error de tiempo de espera en la descarga de la imagen de arranque porque el tamaño del bloque o la ventana es demasiado grande. La personalización tanto del tamaño del bloque como del de la ventana de TFTP de RamDisk le permiten optimizar el tráfico de TFTP al utilizar PXE para cumplir los requisitos de red específicos. Pruebe la configuración personalizada en su entorno para determinar el método más eficaz. Para obtener más información, consulte [Customize the RamDisk TFTP block size and window size on PXE-enabled distribution points](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_RamDiskTFTP) (Personalización del tamaño de bloque de TFTP de RamDisk y el tamaño de la ventana de puntos de distribución habilitados con el entorno PXE).

## <a name="configure-deployment-settings"></a>Configurar la implementación
Para usar una implementación de sistema operativo iniciada por PXE, debe configurar la implementación para que el sistema operativo esté disponible para las solicitudes de arranque de PXE. Puede configurar los sistemas operativos disponibles en la página **Configuración de implementación** del Asistente para implementar software o en la pestaña **Configuración de implementación** en las propiedades de la implementación. Para la opción de configuración **Estar disponible para** , configure uno de los siguientes:

-   Clientes de Configuration Manager, medios y PXE

-   Solo medios y PXE

-   Sólo medios y PXE (ocultos)

##  <a name="BKMK_Deploy"></a> Implementar la secuencia de tareas
Implemente el sistema operativo en una recopilación de destino. Para obtener más información, vea [Deploy a task sequence](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS). Al implementar sistemas operativos mediante PXE, puede configurar que la implementación sea necesaria o esté disponible.

-   **Implementación requerida**: este tipo de implementación usa PXE sin intervención del usuario. El usuario no podrá omitir el arranque de PXE. Sin embargo, si el usuario cancela el arranque de PXE antes de que responda el punto de distribución, no se implementará el sistema operativo.

-   **Implementación disponible**: este tipo de implementación requiere que el usuario esté presente en el equipo de destino para que presione la tecla F12 y permitir, así, la continuación del proceso de arranque de PXE. Si el usuario no está presente para presionar F12, el equipo arrancará en el sistema operativo actual, o desde el siguiente dispositivo de arranque disponible.

Puede realizar de nuevo una implementación del entorno PXE requerida. Para ello, borre el estado de la última implementación del entorno PXE asignada a un equipo o a una recopilación de Configuration Manager. Esta acción restablece el estado de la implementación, y vuelve a instalar las implementaciones requeridas más recientes.

> [!IMPORTANT]
> El protocolo PXE no es seguro. Asegúrese de que el servidor PXE y el cliente de PXE se encuentran en una red físicamente segura, como, por ejemplo, en un centro de datos, para evitar accesos no autorizados al sitio.

##  <a name="how-is-the-boot-image-selected-for-clients-booting-with-pxe"></a>¿Cómo se selecciona la imagen de arranque para los clientes que arrancan con el entorno PXE?
Cuando un cliente arranca con el entorno PXE, Configuration Manager ofrece al cliente una imagen de arranque. A partir de Configuration Manager versión 1606, Configuration Manager usa una imagen de arranque con una coincidencia de arquitectura exacta. Si no hay disponible una imagen de arranque con la arquitectura exacta, Configuration Manager usa una imagen de arranque con una arquitectura compatible. En la lista siguiente se proporciona información sobre cómo se selecciona una imagen de arranque para los clientes que arrancan con el entorno PXE.
1. Configuration Manager busca en la base de datos de sitio un registro del sistema que coincida con la dirección MAC o SMBIOS del cliente que está intentando arrancar.  

    > [!NOTE]
    > Si un equipo que se asigna a un sitio se arranca en PXE para un sitio diferente, las directivas no son visibles para el equipo. Por ejemplo, si un cliente ya está asignado al sitio A, el punto de administración y punto de distribución en el sitio B no podrán acceder a las directivas de sitio A y el cliente no arrancará correctamente PXE.

2. Configuration Manager busca secuencias de tareas que estén implementadas en el registro del sistema que se encontró en el paso 1.

3. En la lista de las secuencias de tareas que se encontraron en el paso 2, Configuration Manager busca una imagen de arranque que coincida con la arquitectura del cliente que está intentando arrancar. Si se encuentra una imagen de arranque con la misma arquitectura, se usa esa imagen.

4. Si no se encuentra una imagen de arranque con la misma arquitectura, Configuration Manager busca una imagen de arranque que sea compatible con la arquitectura del cliente. Busca en la lista de secuencias de tareas que se encuentra en el paso 2. Por ejemplo, un cliente de 64 bits es compatible con imágenes de arranque de 32 bits y 64 bits. Un cliente de 32 bits solo es compatible con imágenes de arranque de 32 bits. Un cliente UEFI solo es compatible con imágenes de arranque de 64 bits.
