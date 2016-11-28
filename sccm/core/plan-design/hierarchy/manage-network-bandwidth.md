---
title: "Administración del ancho de banda de red para el contenido | System Center Configuration Manager"
description: "Configure la programación, el límite y el contenido preconfigurado para System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e80d1151-91db-4a27-8411-a957297b67d0
caps.latest.revision: 15
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 92a08908f284abb02ce8000122b0839c474616d7


---

##  <a name="a-namebkmkplanningforthrottlingascheduling-and-throttling"></a><a name="BKMK_PlanningForThrottling"></a> Programación y el límite  
 Para ayudarle a administrar el ancho de banda de red que se usa para el proceso de administración de contenido, puede usar los controles integrados de Configuration Manager para la programación y el límite, o bien usar contenido preconfigurado.  

 Al crear un paquete, cambie la ruta de acceso de origen del contenido o actualice el contenido del punto de distribución; los archivos se copian desde la ruta de acceso de origen a la biblioteca de contenido del servidor de sitio. A continuación, el contenido se copia desde la biblioteca de contenido del servidor del sitio a la biblioteca de contenido de los puntos de distribución. Una vez actualizados los archivos de origen de contenido, y distribuidos los archivos de origen, Configuration Manager solo recupera los archivos nuevos o actualizados y, a continuación, los envía al punto de distribución. Los controles de la limitación y la programación pueden configurarse para la comunicación de sitio a sitio y para la comunicación entre un servidor de sitio y un punto de distribución remoto. Cuando se limita el ancho de banda de red entre el servidor del sitio y el punto de distribución remoto incluso después de configurar la programación y la limitación, puede considerar la preconfiguración del contenido en el punto de distribución.  

 En Configuration Manager, puede configurar una programación y especificar opciones de limitación en puntos de distribución remotos para determinar cómo y cuándo se realiza la distribución del contenido. Cada punto de distribución remoto puede tener diferentes configuraciones que ayudan a abordar las limitaciones de ancho de banda de red desde el servidor del sitio hasta el punto de distribución remoto. Los controles utilizados para programar y limitar el punto de distribución remoto son similares a la configuración de una dirección de remitente estándar pero, en este caso, un nuevo componente denominado administrador de transferencia de paquetes utiliza la configuración. El administrador de transferencia de paquetes distribuye contenido desde un servidor de sitio, como un sitio primario o un sitio secundario, a un punto de distribución que está instalado en un sistema de sitio. La limitación se configura en la pestaña **Límites de frecuencia** , y la programación se configura en la pestaña **Programación** para un punto de distribución que no está en un servidor del sitio. La configuración de hora se basa en la zona horaria del sitio de envío, no del punto de distribución.  

> [!WARNING]  
>  Las pestañas **Límites de frecuencia** y **Programación** solo se muestran en las propiedades de los puntos de distribución que no están instalados en un servidor del sitio.  

Para obtener más información acerca de cómo configurar la programación y limitación de un punto de distribución remoto, consulte [Install and configure distribution points for System Center Configuration Manager](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points) (Instalación y configuración de puntos de distribución para System Center Configuration Manager).  

##  <a name="a-namebkmkprestagingcontentaprestaged-content"></a><a name="BKMK_PrestagingContent"></a>Contenido preconfigurado  
 Puede preconfigurar el contenido para agregar archivos de contenido a la biblioteca de contenido de un servidor de sitio o un punto de distribución antes de distribuir el contenido.  

-   Los archivos de contenido no se transfieren a través de la red cuando se distribuye el contenido porque ya figuran en la biblioteca de contenido.  

-   Puede preconfigurar los archivos de contenido para aplicaciones y paquetes.  

En la consola de Configuration Manager, seleccione el contenido que necesita preconfigurar y, a continuación, utilice el **Asistente para crear archivos de contenido preconfigurados** para crear un archivo de contenido preconfigurado comprimido que contenga los archivos y los metadatos asociados del contenido. A continuación, puede importar manualmente el contenido a un servidor de sitio o un punto de distribución.  

-   Cuando se importa el archivo de contenido preconfigurado en un servidor de sitio, los archivos de contenido se agregan a la biblioteca de contenido del servidor de sitio y después se registran en la base de datos del servidor de sitio.  

-   Cuando se importa el archivo de contenido preconfigurado en un punto de distribución, los archivos de contenido se agregan a la biblioteca de contenido del punto de distribución y se envía un mensaje de estado al servidor de sitio para notificar al sitio que el contenido está disponible en el punto de distribución.  

Opcionalmente puede configurar el punto de distribución como **preconfigurado** para facilitar la administración de la distribución de contenido. A continuación, cuando se distribuya el contenido, puede elegir si desea:  

-   Preconfigurar siempre el contenido en el punto de distribución.  

-   Preconfigurar el contenido inicial para el paquete y después usar el proceso de distribución de contenido estándar cuando haya actualizaciones del contenido.  

-   Usar siempre el proceso de distribución de contenido estándar para el contenido del paquete.  

###  <a name="a-namebkmkdeterminetoprestagecontentadetermine-whether-to-prestage-content"></a><a name="BKMK_DetermineToPrestageContent"></a>Determinación de si se debe preconfigurar el contenido  
 Considere la preconfiguración de contenido para aplicaciones y paquetes en los escenarios siguientes:  

-   **Ancho de banda de red limitado desde el servidor del sitio al punto de distribución**: si la programación y la limitación pueden resultar insuficientes para distribuir contenido a través de la red a un punto de distribución remoto, considere la posibilidad de preconfigurar el contenido en el punto de distribución. Los puntos de distribución tienen la configuración **Habilitar este punto de distribución para contenido preconfigurado** que se puede configurar en las propiedades del punto de distribución. Cuando se habilita esta opción, el punto de distribución se identifica como un punto de distribución preconfigurado, y puede elegir cómo administrar el contenido en una instalación por paquete.  

     Las siguientes opciones están disponibles en las propiedades para una aplicación, paquete, paquete de controlador, imagen de arranque, instalador de sistema operativo e imagen, y le permiten configurar la administración de la distribución del contenido de puntos de distribución remotos que identificados como preconfigurados:  

    -   **Descargar contenido automáticamente cuando los paquetes se asignen a puntos de distribución**: utilice esta opción cuando haya paquetes más reducidos donde la configuración de programación y limitación proporcione control suficiente para la distribución de contenido.  

    -   **Descargar solo los cambios de contenido en el punto de distribución**: use esta opción si tiene un paquete inicial que puede considerar grande y espera que las actualizaciones futuras al contenido del paquete sean, por lo general, más reducidas. Por ejemplo, puede preconfigurar una aplicación como Microsoft Office porque el tamaño de paquete inicial supera los 700 MB y es demasiado grande para enviarlo a través de la red. Sin embargo, las actualizaciones de contenido de este paquete pueden ser inferiores a 10 MB y se pueden distribuir a través de la red. Otro ejemplo podrían ser paquetes de controladores donde el tamaño de paquete inicial es grande, pero las adiciones incrementales de controladores al paquete podrían ser reducidas.  

    -   **Copiar manualmente el contenido de este paquete en el punto de distribución**: utilice esta opción cuando tenga paquetes grandes, como por ejemplo, un sistema operativo, y no desee usar la red para distribuir el contenido al punto de distribución. Al seleccionar esta opción, debe preconfigurar el contenido del punto de distribución.  

    > [!WARNING]  
    >  Las opciones anteriores son aplicables a una instalación por paquete, y solo se utilizan cuando un punto de distribución está identificado como preconfigurado. Los puntos de distribución que no se han identificado como preconfigurados omiten esta configuración. En ese caso, el contenido siempre se distribuye a través de la red desde el servidor de sitio a los puntos de distribución.  

-   **Restaurar la biblioteca de contenido en un servidor del sitio**: cuando se produce un error en el servidor de sitio, la información sobre paquetes y aplicaciones en la biblioteca de contenido se restaura en la base de datos del sitio como parte del proceso de restauración, pero los archivos de la biblioteca de contenido no se restauran como parte del proceso. Si no dispone de una copia de seguridad del sistema de archivos para restaurar la biblioteca de contenido, puede crear un archivo de contenido preconfigurado desde otro sitio que contiene los paquetes y aplicaciones que debe tener y, a continuación, extraer el archivo de contenido preconfigurado en el servidor de contenido recuperado. Para obtener más información sobre la recuperación y copia de seguridad de un servidor de sitio, vea [Backup and recovery for System Center Configuration Manager](/sccm/protect/understand/backup-and-recovery) (Copia de seguridad y recuperación para System Center Configuration Manager).  



<!--HONumber=Nov16_HO1-->


