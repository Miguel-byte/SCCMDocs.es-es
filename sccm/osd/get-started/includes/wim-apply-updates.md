---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.topic: include
ms.date: 11/27/2018
ms.openlocfilehash: f6e46f8b0bf985eae87cd5157f8a82af5fa0b849
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56142585"
---
##  <a name="BKMK_OSImagesApplyUpdates"></a> Aplicar las actualizaciones de software a una imagen  

> [!Note]  
> Esta sección se aplica a las **imágenes de sistema operativo** y a los **paquetes de actualización del sistema operativo**. Utiliza el término general "imagen" para hacer referencia al archivo de imagen de Windows (WIM). Estos dos objetos tienen un archivo WIM, que contiene los archivos de instalación de Windows. Las actualizaciones de software son aplicables a estos archivos en los dos objetos. El comportamiento de este proceso es el mismo en los dos objetos.  

Todos los meses hay nuevas actualizaciones de software aplicables a la imagen. Para poder aplicar las actualizaciones de software, necesita los siguientes requisitos previos: 

- Infraestructura de actualizaciones de software  
- Actualizaciones de software sincronizadas correctamente  
- Actualizaciones de software descargadas a la biblioteca de contenido en el servidor del sitio  

Para obtener más información, consulte [Deploy software updates](/sccm/sum/deploy-use/deploy-software-updates) (Implementación de actualizaciones de software).  

Aplique las actualizaciones de software pertinentes a una imagen según una programación especificada. Este proceso se conoce como *instalación sin conexión*. En esta programación, Configuration Manager aplica las actualizaciones de software seleccionadas a la imagen. Después, también puede redistribuir la imagen actualizada a los puntos de distribución. 

La base de datos del sitio almacena información sobre la imagen, incluyendo las actualizaciones de software que se aplicaron en el momento de la importación. Las actualizaciones de software que aplique a la imagen desde que se agregó inicialmente también se almacenan en la base de datos del sitio. Al iniciar el asistente para aplicar las actualizaciones de software, se recuperará la lista de actualizaciones de software aplicables que el sitio aún no haya aplicado a la imagen. Configuration Manager copiará las actualizaciones de software que seleccione en la biblioteca de contenido del servidor de sitio. Después aplica las actualizaciones de software a la imagen.  


### <a name="servicing-process"></a>Proceso de mantenimiento  

1.  En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y después seleccione **Imágenes de sistema operativo** o **Paquetes de actualización del sistema operativo**.  

2.  Seleccione el objeto al que va a aplicar las actualizaciones de software.  

3.  En la cinta de opciones, haga clic en **Programar actualizaciones** para iniciar el asistente.  

4.  En la página **Elegir actualizaciones**, seleccione las actualizaciones de software que quiera aplicar a la imagen. La lista de actualizaciones puede tardar un rato en aparecer en el asistente. Use el **filtro** para buscar cadenas en los metadatos. Use la lista desplegable **Arquitectura del sistema** para filtrar por **X86**, **X64** o **Todas**. Puede seleccionar una actualización de la lista, muchas o todas. Cuando haya terminado de seleccionar las actualizaciones, haga clic en **Siguiente**.  

5.  En la página **Establecer programación** , especifique la siguiente configuración y, a continuación, haga clic en **Siguiente**.  

    a.  **Programación**: especifique la programación para cuando el sitio aplique las actualizaciones de software a la imagen.  

    b.  **Continuar después de un error**:  seleccione esta opción para continuar con la aplicación de las actualizaciones de software a la imagen, incluso cuando se produzca un error.  

    c.  **Actualizar puntos de distribución con la imagen:** seleccione esta opción para actualizar la imagen en puntos de distribución después de que el sitio aplique las actualizaciones de software.  

6.  Finalice el asistente para programar actualizaciones.  

> [!NOTE]  
>  Para minimizar el tamaño de carga, el mantenimiento de los paquetes de actualización del sistema operativo y de imágenes del sistema operativo quita la versión anterior.  


### <a name="servicing-operations"></a>Operaciones de mantenimiento

En el nodo **Imágenes de sistema operativo** o **Paquetes de actualización del sistema operativo** de la consola de Configuration Manager, agregue las siguientes columnas a la vista:
- **Fecha de actualizaciones programadas**: esta propiedad muestra la siguiente programación que haya definido.  
- **Estado de actualizaciones programadas**: esta propiedad muestra el estado. Por ejemplo, **Correcto** o **En proceso**.  

Seleccione un objeto de imagen específico y después cambie a la pestaña **Estado de actualización** en el panel de detalles. En esta pestaña se muestra la lista de actualizaciones de la imagen. 

Seleccione un objeto de imagen específico y haga clic en **Propiedades** en la cinta de opciones. En la pestaña **Actualizaciones instaladas** se muestra la lista de actualizaciones de la imagen. La pestaña **Mantenimiento** es una vista de solo lectura de la programación de mantenimiento actual y de las actualizaciones programadas para aplicarse. 

Cuando el estado es **En proceso**, puede seleccionar **Cancelar actualizaciones programadas** en la cinta de opciones. Esta acción cancela el proceso de mantenimiento activo. 

Para solucionar este proceso, vea los archivos **OfflineServicingMgr.log** y **dism.log** en el servidor de sitio. Para obtener más información, vea [Archivos de registro](/sccm/core/plan-design/hierarchy/log-files).


### <a name="bkmk_servicing-drive"></a> Especificación de la unidad para la instalación sin conexión de imágenes de SO  
<!--1358924-->

A partir de la versión 1810, especifique la unidad que Configuration Manager usa durante la instalación sin conexión de imágenes de SO. Este proceso puede consumir una gran cantidad de espacio en disco con los archivos temporales. Esta opción le ofrece la flexibilidad de seleccionar la unidad que se va a usar. 

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Configuración del sitio** y seleccione el nodo **Sitios**. En la cinta, haga clic en **Configurar componentes de sitio** y seleccione **Implementación de sistema operativo**.  

2. En la pestaña **Instalación sin conexión**, especifique la opción para **Una unidad local que se usará en la instalación de imágenes sin conexión**.  

De manera predeterminada, esta configuración es **Automática**. Con este valor, Configuration Manager selecciona la unidad donde está instalado. 

Si selecciona una unidad que no existe en el servidor de sitio, Configuration Manager se comportará igual que si selecciona **Automática**. 

Durante la instalación sin conexión, Configuration Manager almacena los archivos temporales en la carpeta, `<drive>:\ConfigMgr_OfflineImageServicing`. También monta la imagen del SO en esta carpeta. 


