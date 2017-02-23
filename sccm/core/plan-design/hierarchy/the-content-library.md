---
title: La biblioteca de contenido | Microsoft Docs
description: "Obtenga información sobre la biblioteca de contenido que usa System Center Configuration Manager para reducir el tamaño total del contenido distribuido."
ms.custom: na
ms.date: 2/14/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 65c88e54-3574-48b0-a127-9cc914a89dca
caps.latest.revision: 4
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: d31fecdb71b498864df2bce7403a4290ea9700ae
ms.openlocfilehash: 0fa9f431c00476d71b2b08f92f914d76636d1a27

---
# <a name="the-content-library-in-system-center-configuration-manager"></a>La biblioteca de contenido en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

La biblioteca de contenido es un almacén de instancia única del contenido que System Center Configuration Manager usa para reducir el tamaño total del cuerpo combinado del contenido que se distribuye. La biblioteca de contenido almacena todos los archivos de contenido de las actualizaciones de software, las aplicaciones, las implementaciones de sistema operativo, etc.

 - En cada **servidor de sitio** y en cada **punto de distribución** se crea y se mantiene automáticamente una copia de la biblioteca de contenido.

 - Antes de que Configuration Manager descargue los archivos de contenido en el servidor de sitio o copie los archivos en los puntos de distribución, Configuration Manager comprueba si cada uno de los archivos de contenido ya se halla en la biblioteca de contenido.
 - Si el archivo de contenido está disponible, Configuration Manager no copia el archivo, sino que asocia el archivo de contenido existente a la aplicación o el paquete.

En los equipos en los que instale un punto de distribución, puede configurar lo siguiente:

- Una o varias unidades de disco en las que quiera crear la biblioteca de contenido.
- Una prioridad para cada unidad que use.

Cuando Configuration Manager copia los archivos de contenido, lo hace en la unidad con la prioridad más alta hasta que esa unidad contenga menos de una cantidad mínima de espacio disponible especificado.
- Las unidades se configuran durante la instalación del punto de distribución.
- No se pueden configurar las opciones de unidades en las propiedades del punto de distribución una vez finalizada la instalación.


Para obtener más información sobre cómo configurar la unidad para el punto de distribución, consulte [Administración del contenido y de la infraestructura de contenido para System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  


>  [!IMPORTANT]  
>  Para mover la biblioteca de contenido a otra ubicación en un punto de distribución después de la instalación, use la **herramienta de transferencia de biblioteca de contenido** del kit de herramientas de System Center 2012 R2 Configuration Manager. Puede descargar el kit de herramientas del [Centro de descarga de Microsoft](http://go.microsoft.com/fwlink/?LinkId=279566).  

## <a name="about-the-content-library-on-the-central-administration-site"></a>Acerca de la biblioteca de contenido en el sitio de administración central  
 De manera predeterminada, Configuration Manager crea una biblioteca de contenido en el sitio de administración central cuando se instala el sitio. La biblioteca de contenido se ubica en la unidad del servidor de sitio que dispone de más espacio libre. Dado que no se puede instalar un punto de distribución en el sitio de administración central, no se puede dar un orden de prioridad al uso de las unidades en la biblioteca de contenido. Al igual que la biblioteca de contenido en otros servidores de sitio y en puntos de distribución, cuando la unidad que contiene la biblioteca de contenido se queda sin espacio disponible en disco, la biblioteca de contenido se distribuye a la siguiente unidad disponible.  

 Configuration Manager usa la biblioteca de contenido en el sitio de administración central en los siguientes escenarios:  

-   Cuando se crea contenido en el sitio de administración central.  

-   Cuando se migra el contenido desde otro sitio de Configuration Manager y se asigna el sitio de administración central como el sitio que administra dicho contenido.  

> [!NOTE]  
>  Cuando crea contenido en un sitio primario y, a continuación, lo distribuye a otro sitio primario o a uno secundario de otro sitio primario, el sitio de administración central almacena temporalmente dicho contenido en la bandeja de entrada del programador del sitio de administración central, pero no lo almacena en su biblioteca de contenido.  

 Utilice las siguientes opciones para administrar la biblioteca de contenido en el sitio de administración central:  

-   Para que la biblioteca de contenido no se instale en una unidad específica, cree un archivo vacío de nombre **no_sms_on_drive.sms** y cópielo en la carpeta raíz de la unidad antes de que se cree la biblioteca de contenido.  

-   Tras la creación de la biblioteca de contenido, use la **herramienta de transferencia de biblioteca de contenido** del kit de herramientas de System Center 2012 R2 Configuration Manager para administrar la ubicación de la biblioteca de contenido. Puede descargar el kit de herramientas del [Centro de descarga de Microsoft](http://go.microsoft.com/fwlink/?LinkId=279566).  



<!--HONumber=Feb17_HO3-->


