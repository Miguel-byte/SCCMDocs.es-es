---
title: Administrar imágenes de sistema operativo
titleSuffix: Configuration Manager
description: En Configuration Manager, obtenga información sobre los métodos que puede usar para administrar las imágenes del sistema operativo que se almacenan en archivos de Windows Imaging (WIM).
ms.date: 12/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: fab13949-371c-4a4c-978e-471db1e54966
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3b0931671c05604a0115c14a5e7fc5d9c6767b7c
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32350109"
---
# <a name="manage-operating-system-images-with-system-center-configuration-manager"></a>Administrar imágenes de sistema operativo con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Las imágenes de sistema operativo de Configuration Manager se almacenan en el archivo de formato de archivo Windows Imaging (WIM) y representan una recopilación comprimida de carpetas y archivos de referencia que se necesitan para instalar y configurar correctamente un sistema operativo en un equipo. Para todos los escenarios de implementación de sistema operativo, debe seleccionar una imagen de sistema operativo.   Puede usar la imagen de sistema operativo predeterminada o crearla desde un equipo de referencia que configure. Si crea el equipo de referencia, puede agregar archivos de sistema operativo, controladores, archivos de compatibilidad técnico, actualizaciones de software, herramientas y otras aplicaciones de software para el sistema operativo antes de capturarlo para crear el archivo de imagen. A continuación se ofrece información sobre cada método.  

 **Imagen predeterminada**  

 La imagen de sistema operativo predeterminada (install.wim) se incluye en los archivos de instalación del sistema operativo Windows. Se trata de una imagen de sistema operativo básica que contiene un conjunto estándar de controladores. Si usa la imagen de sistema operativo predeterminada, puede instalar aplicaciones y realizar otras configuraciones después de que el sistema operativo se instale mediante el uso de pasos de secuencia de tareas.  La imagen de sistema operativo predeterminada se encuentra en <*ruta de acceso de origen del sistema operativo*>\Sources\install.wim.  

-   **Ventajas**  

    -   El tamaño de la imagen es menor que una imagen capturada.  

    -   La instalación de aplicaciones y configuraciones con pasos de secuencia de tareas es más dinámica. Por ejemplo, puede cambiar las aplicaciones que se instalarán y las configuraciones de la secuencia de tareas sin necesidad de volver a crear la imagen del sistema operativo.  

-   **Desventajas**  

    -   La instalación del sistema operativo puede tardar más tiempo porque la instalación de aplicaciones y otras configuraciones se realiza cuando finaliza la instalación del sistema operativo.  

 **Imagen capturada**  

 Para crear una imagen personalizada del sistema operativo, es necesario crear un equipo de referencia con el sistema operativo deseado e instalar aplicaciones, configurar opciones, etc. A continuación, se captura la imagen de sistema operativo del equipo de referencia para crear el archivo WIM. Puede generar el equipo de referencia de forma manual o utilizar una secuencia de tareas para automatizar algunos o todos los pasos de generación.   
Si quiere conocer los pasos necesarios para crear una imagen personalizada del sistema operativo, vea [Personalizar imágenes de sistema operativo](customize-operating-system-images.md).  

-   **Ventajas**  

    -   La instalación puede resultar más rápida que el uso de la imagen predeterminada. Por ejemplo, las aplicaciones se pueden instalar previamente con la imagen de sistema operativo capturada, por lo que no necesitará instalar aplicaciones más adelante mediante el uso de pasos de secuencia de tareas.  

-   **Desventajas**  

    -   La instalación del sistema operativo puede tardar más tiempo porque la instalación de aplicaciones y otras configuraciones se realiza cuando finaliza la instalación del sistema operativo.  


##  <a name="BKMK_AddOSImages"></a> Incorporación de imágenes de sistema operativo a Configuration Manager  
 Para usar una imagen de sistema operativo, primero debe agregarla un sitio de Configuration Manager. Use el procedimiento siguiente para agregar una imagen de sistema operativo a un sitio.  

#### <a name="to-add-an-operating-system-image-to-a-site"></a>Para agregar una imagen de sistema operativo a un sitio  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

2.  En el área de trabajo **Biblioteca de software** , expanda **Sistemas operativos**y, a continuación, haga clic en **Imágenes de sistema operativo**.  

3.  En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Agregar imagen de sistema operativo** para iniciar el Asistente para agregar imagen de sistema operativo.  

4.  En la página **Origen de datos** , especifique la ruta de acceso de red para la imagen de sistema operativo. Por ejemplo, especifique **\\\servidor\rutaDeAcceso\OS.WIM**.  

5.  En la página **General** , especifique la información siguiente y, a continuación, haga clic en **Siguiente**. Esta información es útil para propósitos de identificación cuando se agregan varias imágenes de sistema operativo al mismo sitio.  

    -   **Nombre**: especifique el nombre de la imagen. De forma predeterminada, se toma el nombre de la imagen del archivo WIM.  

    -   **Versión**: especifique la versión de la imagen.  

    -   **Comentario**: especifique una breve descripción de la imagen.  

6.  Complete el asistente.  

 Puede distribuir la imagen de sistema operativo a puntos de distribución.  

##  <a name="BKMK_DistributeBootImages"></a> Distribución de imágenes de sistema operativo a puntos de distribución  
 Las imágenes de sistema operativo se distribuyen a los puntos de distribución de la misma forma que se distribuye otro tipo de contenido. En la mayoría de los casos, debe distribuir la imagen de sistema operativo a un punto de distribución, como mínimo, antes de implementar el sistema operativo. Para conocer los pasos de distribución de una imagen de sistema operativo, vea [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute) (Distribuir contenido).  

##  <a name="BKMK_OSImagesApplyUpdates"></a> Aplicación de actualizaciones de software a una imagen de sistema operativo  
 Periódicamente, se publican nuevas actualizaciones de software que son aplicables al sistema operativo contenido en la imagen de sistema operativo. Por supuesto, antes de aplicar las actualizaciones de software a una imagen debe contar con la infraestructura de actualizaciones de software, haber sincronizado correctamente dichas actualizaciones y haber descargado las actualizaciones de software en la biblioteca de contenido en el servidor del sitio. Para obtener más información, consulte [Deploy software updates](../../sum/deploy-use/deploy-software-updates.md) (Implementación de actualizaciones de software).  

 Puede aplicar las actualizaciones de software que sean aplicables a una imagen según una programación especificada. En función de la programación que especifique, Configuration Manager aplica las actualizaciones de software que seleccione a la imagen del sistema operativo y, a continuación, opcionalmente, distribuye la imagen actualizada a los puntos de distribución. La información sobre la imagen de sistema operativo se almacena en la base de datos del sitio, incluyendo las actualizaciones de software que se aplicaron en el momento de la importación. Las actualizaciones de software que se hayan aplicado a la imagen desde que se agregó inicialmente también se almacenan en la base de datos del sitio. Cuando inicia el asistente para aplicar actualizaciones de software a la imagen de sistema operativo, el asistente recupera una lista de actualizaciones de software aplicables aún no aplicadas a la imagen para que usted seleccione las que desea. Configuration Manager copia las actualizaciones de software de la biblioteca de contenido que se encuentra en el servidor de sitio y las aplica a la imagen de sistema operativo.  

 Utilice el siguiente procedimiento para aplicar las actualizaciones de software a una imagen de sistema operativo.  

#### <a name="to-apply-software-updates-to-an-operating-system-image"></a>Para aplicar actualizaciones de software a una imagen de sistema operativo  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

2.  En el área de trabajo **Biblioteca de software** , expanda **Sistemas operativos**y, a continuación, haga clic en **Imágenes de sistema operativo**.  

3.  Seleccione la imagen de sistema operativo a la que desea aplicar actualizaciones de software.  

4.  En la pestaña **Inicio** , en el grupo **Imagen de sistema operativo** , haga clic en **Programar actualizaciones** para iniciar el asistente.  

5.  En la página **Elija las actualizaciones** , seleccione las actualizaciones de software que desea aplicar a la imagen de sistema operativo y, a continuación, haga clic en **Siguiente**.  

6.  En la página **Establecer programación** , especifique la siguiente configuración y, a continuación, haga clic en **Siguiente**.  

    1.  **Programación**: especifique la programación para el momento en el que deben aplicarse las actualizaciones de software a la imagen de sistema operativo.  

    2.  **Continuar después de un error**: seleccione esta opción para continuar con la aplicación de las actualizaciones de software a la imagen incluso cuando se produzca un error.  

    3.  **Distribuir la imagen a los puntos de distribución**: seleccione esta opción para actualizar la imagen de sistema operativo en los puntos de distribución después de que se apliquen las actualizaciones de software.  

7.  En la página **Resumen** , compruebe la información y, a continuación, haga clic en **Siguiente**.  

8.  En la página **Finalización** , compruebe que las actualizaciones de software se aplicaron correctamente a la imagen de sistema operativo.  

##  <a name="BKMK_OSImageMulticast"></a> Preparación de la imagen de sistema operativo para implementaciones de multidifusión  
 Use las implementaciones de multidifusión para permitir que varios equipos descarguen una imagen de sistema operativo simultáneamente. El punto de distribución envía la imagen mediante multidifusión a los clientes en vez de enviar una copia de la imagen a cada cliente a través de una conexión independiente. Al elegir el método de implementación de sistema operativo [Usar multidifusión para implementar Windows a través de la red](../deploy-use/use-multicast-to-deploy-windows-over-the-network.md), debe configurar el paquete de imágenes de sistema operativo para que admita la multidifusión antes de distribuir la imagen de sistema operativo a un punto de distribución habilitado para multidifusión. Utilice el siguiente procedimiento para establecer las opciones de multidifusión para un paquete de imágenes de sistema operativo existente.  

#### <a name="to-modify-an-operating-system-image-package-to-use-multicast"></a>Para modificar un paquete de imágenes de sistema operativo para que use la multidifusión  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

2.  En el área de trabajo **Biblioteca de software** , expanda **Sistemas operativos**y, a continuación, haga clic en **Imágenes de sistema operativo**.  

3.  Seleccione la imagen de sistema operativo que se va a distribuir en el punto de distribución habilitado para multidifusión.  

4.  En la pestaña **Inicio** , en el grupo **Propiedades** , haga clic en **Propiedades**.  

5.  Seleccione la pestaña **Configuración de distribución** y configure las siguientes opciones:  

    -   **Permitir que este paquete se transfiera mediante multidifusión (solo WinPE)**: debe seleccionar esta opción para que Configuration Manager implemente imágenes del sistema operativo simultáneamente.  

    -   **Cifrar paquetes de multidifusión**: especifique si la imagen se cifrará antes de enviarse al punto de distribución. Utilice esta opción si el paquete contiene información confidencial. Si la imagen no está cifrada, el contenido del paquete será visible en texto sin cifrar en la red y podría ser leído por un usuario no autorizado.  

    -   **Transferir este paquete solo mediante multidifusión**: especifique si desea que el punto de distribución implemente la imagen solamente durante una sesión de multidifusión.  

         Si selecciona **Transferir este paquete solo mediante multidifusión**, también deberá especificar **Descargar el contenido localmente cuando sea necesario mediante la ejecución de una secuencia de tareas** como la opción de implementación para la imagen de sistema operativo. Puede especificar las opciones de implementación de la imagen cuando implemente la imagen de sistema operativo o más tarde mediante la modificación de las propiedades de la implementación. Las opciones de implementación se encuentran en la pestaña **Puntos de distribución** de la página **Propiedades** del objeto de implementación.  

6.  Haga clic en **Aceptar**.  
