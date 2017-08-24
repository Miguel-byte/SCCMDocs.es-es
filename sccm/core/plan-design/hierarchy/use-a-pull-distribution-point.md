---
title: "Punto de distribución de extracción | Microsoft Docs"
description: "Obtenga información sobre las configuraciones y las limitaciones del uso de un punto de distribución de extracción con System Center Configuration Manager."
ms.custom: na
ms.date: 2/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7d8f530b-1a39-4a9d-a2f0-675b516da7e4
caps.latest.revision: "9"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: db5039ff6cb93e3099b096196d49a1f06c315a6b
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/07/2017
---
# <a name="use-a-pull-distribution-point-with-system-center-configuration-manager"></a>Usar un punto de distribución de extracción con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*


Un punto de distribución de extracción para System Center Configuration Manager es un punto de distribución estándar que, para obtener el contenido distribuido, lo descarga de una ubicación de origen, como un cliente, en lugar de hacer que el contenido se inserte desde el servidor de sitio.  

 Cuando implementa contenido en un gran número de puntos de distribución en un sitio, los puntos de distribución de extracción pueden ayudarle a reducir la carga de procesamiento en el servidor del sitio y a acelerar la transferencia del contenido en cada punto de distribución. Esta eficacia se consigue mediante la descarga del proceso de transferencia del contenido en cada punto de distribución desde el proceso administrador de distribución en el servidor de sitio.  

-   Puede configurar distintos puntos de distribución para que sean de extracción.  

-   Para cada punto de distribución de extracción debe especificar uno o varios puntos de distribución de origen de los que puede obtener implementaciones (un punto de distribución de extracción solo puede obtener contenido de un punto de distribución especificado como punto de distribución de origen).  

-   Cuando se distribuye contenido a un punto de distribución de extracción, el servidor de sitio lo notifica al punto de distribución de extracción, el cual inicia la descarga (transferencia) del contenido desde un punto de distribución de origen. Un punto de distribución de extracción administra individualmente la transferencia de contenido mediante la descarga de contenido desde un punto de distribución que ya tiene una copia del contenido.  

Los puntos de distribución de extracción admiten las mismas configuraciones y funcionalidad que los puntos de distribución de Configuration Manager normales. Por ejemplo, un punto de distribución que está configurado como punto de distribución de extracción admite el uso de configuraciones de multidifusión y PXE, validación de contenido y distribución de contenido a petición. Un punto de distribución de extracción admite comunicaciones HTTP o HTTPS desde los clientes, admite las mismas opciones de certificados que otros puntos de distribución, y se puede administrar individualmente o como miembro de un grupo de puntos de distribución.  

> [!IMPORTANT]
> Aunque un punto de distribución de extracción admite comunicaciones a través de HTTP y HTTPS, cuando use Configuration Manager, solo podrá especificar puntos de distribución de origen configurados para HTTP. Puede usar el SDK de Configuration Manager para especificar un punto de distribución de origen configurado para HTTPS.  

 **La secuencia de eventos siguiente se produce al distribuir contenido a un punto de distribución de extracción:**  

-   Cuando se distribuye contenido a un punto de distribución de extracción, el administrador de transferencia de paquetes en el servidor de sitio comprueba la base de datos del sitio para confirmar si el contenido está disponible en un punto de distribución de origen. Si no puede confirmar que el contenido está en un punto de distribución de origen para el punto de distribución de extracción, repite la comprobación cada 20 minutos hasta que el contenido esté disponible.  

-   Cuando el administrador de transferencia de paquetes confirma que el contenido está disponible, envía una notificación al punto de distribución de extracción para descargar el contenido. Cuando el punto de distribución de extracción recibe esta notificación, intenta descargar el contenido de los puntos de distribución de origen.  

-   Después de que el punto de distribución de extracción completa la descarga del contenido, envía este estado a un punto de administración. Pero si el estado no se ha recibido después de 60 minutos, el administrador de transferencia de paquetes se reactiva y comprueba el punto de distribución de extracción para confirmar que haya descargado el contenido. Si la descarga de contenido está en curso, el administrador de transferencia de paquetes se suspende durante 60 minutos antes de comprobar de nuevo el punto de distribución de extracción. Este ciclo continúa hasta que el punto de distribución de extracción completa la transferencia de contenido.  

**Se puede configurar un punto de distribución de extracción** al instalar el punto de distribución o después de instalarlo mediante la edición de las propiedades del rol de sistema de sitio del punto de distribución.  

**Se puede quitar la configuración para que el punto de distribución deje de ser de extracción**, mediante la edición de las propiedades del punto de distribución. Cuando se quita la configuración de punto de distribución de extracción, el punto de distribución vuelve a su funcionamiento normal y el servidor de sitio administra las posteriores transferencias de contenido al punto de distribución.  

## <a name="limitations-for-pull-distribution-points"></a>Limitaciones de los puntos de distribución de extracción  

-   No se pueden configurar puntos de distribución basados en la nube como puntos de distribución de extracción.  

-   No se puede configurar un punto de distribución de un servidor del sitio como un punto de distribución de extracción.  

-   **La configuración del contenido preconfigurado reemplaza la configuración del punto de distribución de extracción**. Un punto de distribución de extracción configurado para contenido preconfigurado espera el contenido. No extrae contenido del punto de distribución de origen y, como punto de distribución estándar con la configuración de contenido preconfigurado, no recibe contenido del servidor de sitio.  

-   **Un punto de distribución de extracción no usa las configuraciones de los límites de frecuencia** al transferir el contenido. Si configura un punto de distribución instalado previamente para que sea un punto de distribución de extracción, las configuraciones de los límites de frecuencia se guardan, pero no se utilizan. Si después quita la configuración del punto de distribución de extracción, las configuraciones de límite de frecuencia se implementan como se configuraron anteriormente.  

    > [!NOTE]  
    >  Cuando un punto de distribución se configura como punto de distribución de extracción, la pestaña **Límites de frecuencia** no estará visible en las propiedades del punto de distribución.  

-   Un punto de distribución de extracción no usa la **configuración de reintento** para la distribución de contenido. **Configuración de reintento** puede configurarse como parte de las **Propiedades del componente de distribución de software** de cada sitio. Para ver o configurar estas propiedades, en el espacio de trabajo **Administración** de la consola de Configuration Manager, expanda **Configuración del sitio** y, después, seleccione **Sitios**. Después seleccione un sitio en el panel de resultados y, en la pestaña **Inicio**, seleccione **Configurar componentes de sitio**. Por último, seleccione **Distribución de software**.  

-   Para transferir contenido de un punto de distribución de origen en un bosque remoto, el equipo que hospeda el punto de distribución de extracción debe tener instalado un cliente de Configuration Manager. Debe configurarse el uso de una cuenta de acceso de red con acceso al punto de distribución de origen.  

-   En un equipo configurado como punto de distribución de extracción y que ejecuta un cliente de Configuration Manager, la versión del cliente debe ser la misma que la del sitio de Configuration Manager que instala el punto de distribución de extracción. Un requisito del punto de distribución de extracción es usar CCMFramework, que es común al punto de distribución de extracción y al cliente de Configuration Manager.  

## <a name="about-source-distribution-points"></a>Acerca de los puntos de distribución de origen  
 Al configurar el punto de distribución de extracción, debe especificar uno o varios puntos de distribución de origen:  

-   Solo se muestran los puntos de distribución que pueden ser puntos de distribución de origen.  

-   Un punto de distribución de extracción puede especificarse como punto de distribución de origen para otro punto de distribución de extracción.  

-   Solo los puntos de distribución compatibles con HTTP pueden especificarse como puntos de distribución de origen cuando use Configuration Manager.  

-   Puede usar el SDK de Configuration Manager para especificar un punto de distribución de origen configurado para HTTPS. Para usar un punto de distribución de origen configurado para HTTPS, el punto de distribución de extracción debe compartir ubicación con un equipo que ejecute el cliente de Configuration Manager.  

Se puede asignar una prioridad a cada punto de distribución en una lista de puntos de distribución de origen de los puntos de distribución de extracción:  

-   Puede asignar una prioridad diferente a cada punto de distribución de origen o asignar varios puntos de distribución de origen a la misma prioridad.  

-   La prioridad determina el orden en que el punto de distribución de extracción solicita contenido de sus puntos de distribución de origen.  

-   Los puntos de distribución de extracción establecen contacto inicialmente con el punto de distribución de origen que tenga la prioridad más baja.  Si hay varios puntos de distribución de origen con la misma prioridad, el punto de distribución de extracción selecciona de forma no determinista uno de esos puntos de distribución de origen con la misma prioridad.  

-   Si el contenido no está disponible en el origen seleccionado, el punto de distribución de extracción intenta descargar el contenido desde otro punto de distribución con la misma prioridad.  

-   Si ninguno de los puntos de distribución con una prioridad determinada tiene el contenido, el punto de distribución de extracción intenta descargar el contenido desde un punto de distribución que tenga asignada una prioridad con el siguiente valor superior, y así sucesivamente hasta que se encuentre el contenido o el punto de distribución de extracción se suspenda durante 30 minutos antes de comenzar el proceso de nuevo.  

Cuando un punto de distribución de extracción descarga contenido desde un punto de distribución de origen, ese punto de distribución de extracción se cuenta como un cliente en la columna **Cliente accedido (único)** del informe **Resumen de uso de los puntos de distribución** .  

 De forma predeterminada, un punto de distribución de extracción usa su **cuenta de equipo** para transferir contenido desde un punto de distribución de origen. Pero cuando el punto de distribución de extracción transfiere contenido desde un punto de distribución de origen que se encuentra en un bosque remoto, el punto de distribución de extracción siempre utiliza la cuenta de acceso de red. Este proceso requiere que el equipo tenga instalado el cliente de Configuration Manager y que se configure una cuenta de acceso de red con acceso al punto de distribución de origen.  

## <a name="about-content-transfers"></a>Acerca de las transferencias de contenido  
 Para administrar la transferencia de contenido, los puntos de distribución de extracción usan el componente **CCMFramework** del software de cliente de Configuration Manager.  

-   Este marco se instala mediante el archivo **Pulldp.msi** al configurar el punto de distribución como punto de distribución de extracción. El marco no requiere el cliente de Configuration Manager.  

-   Una vez instalado el punto de distribución de extracción, el servicio CCMExec del equipo del punto de distribución debe estar operativo para que el punto de distribución de extracción funcione.  

-   Cuando el punto de distribución de extracción transfiere contenido, lo hace mediante el **Servicio de transferencia inteligente en segundo plano** (BITS) y registra su funcionamiento en los registros **datatransferservice.log** y **pulldp.log** del equipo del punto de distribución.  

## <a name="see-also"></a>Consulte también  
 [Fundamental concepts for content management in System Center Configuration Manager (Aspectos básicos de la administración de contenido en System Center Configuration Manager)](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management)   
