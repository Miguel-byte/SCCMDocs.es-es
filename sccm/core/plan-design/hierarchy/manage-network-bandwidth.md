---
title: Administración del ancho de banda de red para contenido
titleSuffix: Configuration Manager
description: Configure la programación, el límite y el contenido preconfigurado para System Center Configuration Manager.
ms.date: 2/6/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: e80d1151-91db-4a27-8411-a957297b67d0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 03d85a55e51125e40e1df766382b0a074d865a51
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56141626"
---
# <a name="manage-network-bandwidth-for-content"></a>Administración del ancho de banda de red para contenido
Para ayudarle a administrar el ancho de banda de red que se usa para el proceso de administración de contenido de System Center Configuration Manager, puede usar los controles integrados para la programación y el límite. También puede usar contenido preconfigurado. En las secciones siguientes se describen estas opciones con más detalle.

##  <a name="BKMK_PlanningForThrottling"></a> Programación y el límite  

 Al crear un paquete, cambie la ruta de acceso de origen para el contenido, o actualice el contenido del punto de distribución; los archivos se copian desde la ruta de acceso de origen a la biblioteca de contenido del servidor del sitio. A continuación, el contenido se copia desde la biblioteca de contenido del servidor del sitio a la biblioteca de contenido de los puntos de distribución. Una vez actualizados los archivos de origen de contenido, y distribuidos los archivos de origen, Configuration Manager solo recupera los archivos nuevos o actualizados y, a continuación, los envía al punto de distribución.

 Puede usar los controles de límite y programación para la comunicación de sitio a sitio y para la comunicación entre un servidor de sitio y un punto de distribución remoto. Si el ancho de banda de red está limitado incluso después de configurar los controles de límite y programación, puede preconfigurar el contenido en el punto de distribución.  

 En Configuration Manager, puede configurar una programación y especificar opciones de límite en puntos de distribución remotos para determinar cómo y cuándo se distribuye el contenido. Cada punto de distribución remoto puede tener diferentes configuraciones que ayudan a abordar las limitaciones de ancho de banda de red desde el servidor del sitio hasta el punto de distribución remoto. Los controles para programar y limitar el punto de distribución remoto son similares a la configuración para una dirección de remitente estándar. En este caso, usará la configuración un nuevo componente (denominado administrador de transferencia de paquetes).

 El administrador de transferencia de paquetes distribuye contenido desde un servidor de sitio, como un sitio primario o un sitio secundario, a un punto de distribución que está instalado en un sistema de sitio. El límite se configura en la pestaña **Límites de frecuencia** y la programación se especifica en la pestaña **Programación** (para un punto de distribución que no esté en un servidor de sitio). La configuración de hora se basa en la zona horaria del sitio de envío, no del punto de distribución.  

> [!IMPORTANT]  
>  Las pestañas **Límites de frecuencia** y **Programación** solo se muestran en las propiedades de los puntos de distribución que no están instalados en un servidor del sitio.  

Para obtener más información, consulte [Instalación y configuración de puntos de distribución de System Center Configuration Manager](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points).  

##  <a name="BKMK_PrestagingContent"></a> Contenido preconfigurado  
 Puede preconfigurar contenido para agregar archivos de contenido a la biblioteca de contenido de un servidor de sitio o un punto de distribución antes de distribuir el contenido. Como los archivos de contenido ya están en la biblioteca de contenido, no se transfieren por la red al distribuir el contenido. Puede preconfigurar los archivos de contenido para aplicaciones y paquetes.  

En la consola de Configuration Manager, seleccione el contenido que quiera preconfigurar y, después, use el **Asistente para crear archivos de contenido preconfigurados**. El asistente creará un archivo de contenido preconfigurado comprimido que contiene los archivos y los metadatos asociados al contenido. A continuación, puede importar manualmente el contenido a un servidor de sitio o un punto de distribución. Tenga en cuenta los puntos siguientes:  

-   Cuando se importa el archivo de contenido preconfigurado en un servidor de sitio, los archivos de contenido se agregan a la biblioteca de contenido del servidor de sitio y, a continuación, se registran en la base de datos del servidor de sitio.  

-   Al importar el archivo de contenido preconfigurado en un punto de distribución, los archivos de contenido se agregan a la biblioteca de contenido en el punto de distribución. Se enviará un mensaje de estado al servidor de sitio para informar al sitio de que el contenido está disponible en el punto de distribución.  

Opcionalmente puede configurar el punto de distribución como **preconfigurado** para facilitar la administración de la distribución de contenido. Después, cuando se distribuya el contenido, puede elegir si quiere:  

-   Preconfigurar siempre el contenido en el punto de distribución.  

-   Preconfigurar el contenido inicial del paquete y, después, usar el proceso de distribución de contenido estándar cuando haya actualizaciones en el contenido.  

-   Usar siempre el proceso de distribución de contenido estándar para el contenido del paquete.  

###  <a name="BKMK_DetermineToPrestageContent"></a> Determinación de si se debe preconfigurar el contenido  
 Considere la preconfiguración de contenido para aplicaciones y paquetes en los escenarios siguientes:  

-   **Para solucionar el problema del ancho de banda de red limitado desde el servidor de sitio a un punto de distribución.** Si la programación y el límite no son suficientes para solucionar sus problemas relacionados con el ancho de banda, puede preconfigurar el contenido en el punto de distribución. Los puntos de distribución tienen la opción **Habilitar este punto de distribución para contenido preconfigurado**, que puede seleccionar en las propiedades del punto de distribución. Cuando se habilita esta opción, el punto de distribución se identifica como un punto de distribución preconfigurado, y puede elegir cómo administrar el contenido en una instalación por paquete.  

    Las opciones siguientes están disponibles en las propiedades de una aplicación, paquete, paquete de controladores, imagen de arranque, instalador de sistema operativo e imagen. Esta configuración le permite seleccionar cómo se administra la distribución de contenido en los puntos de distribución remotos identificados como preconfigurados:  

    -   **Descargar contenido automáticamente cuando los paquetes se asignen a puntos de distribución**: use esta opción cuando haya paquetes más pequeños, y la configuración de programación y limitación proporcione control suficiente para la distribución de contenido.  

    -   **Descargar solo los cambios de contenido en el punto de distribución**: use esta opción cuando espere que las actualizaciones futuras del contenido sean en general más pequeñas que el paquete inicial. Por ejemplo, puede preconfigurar una aplicación como Microsoft Office, ya que el tamaño del paquete inicial es superior a 700 MB y es demasiado grande para enviarlo por la red. Pero las actualizaciones de contenido de este paquete pueden ser inferiores a 10 MB y se pueden distribuir por la red. Otro ejemplo podrían ser paquetes de controladores, donde el tamaño del paquete inicial es grande, pero las adiciones incrementales de controladores al paquete podrían ser reducidas.  

    -   **Copiar manualmente el contenido de este paquete en el punto de distribución**: use esta opción cuando tenga paquetes de gran tamaño (por ejemplo, un sistema operativo) y no quiera usar la red para distribuir el contenido al punto de distribución. Al seleccionar esta opción, debe preconfigurar el contenido del punto de distribución.  

    > [!IMPORTANT]  
    >  Las opciones anteriores se pueden aplicar por paquete y solo se usan cuando un punto de distribución esté identificado como preconfigurado. Los puntos de distribución que no se han identificado como preconfigurados omiten esta configuración. En ese caso, el contenido siempre se distribuye a través de la red desde el servidor de sitio a los puntos de distribución.  

-   **Para restaurar la biblioteca de contenido en un servidor de sitio.** cuando se produce un error en el servidor de sitio, la información sobre paquetes y aplicaciones en la biblioteca de contenido se restaura en la base de datos del sitio como parte del proceso de restauración, pero los archivos de la biblioteca de contenido no se restauran como parte del proceso. Si no tiene una copia de seguridad del sistema de archivos para restaurar la biblioteca de contenido, puede crear un archivo de contenido preconfigurado de otro sitio que contenga los paquetes y aplicaciones que necesita. Después, puede extraer el archivo de contenido preconfigurado en el servidor de sitio recuperado. Para obtener más información sobre la copia de seguridad y recuperación de un servidor de sitio, consulte [Copia de seguridad y recuperación de System Center Configuration Manager](/sccm/protect/understand/backup-and-recovery).  
