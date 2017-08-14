---
title: Accesibilidad | Microsoft Docs
description: "Conozca las características que hacen que System Center Configuration Manager sea accesible para personas con discapacidades."
ms.custom: na
ms.date: 7/31/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1cb96666-98bf-49a9-85ca-dbb53f0655e9
caps.latest.revision: 6
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: HT
ms.sourcegitcommit: 3c75c1647954d6507f9e28495810ef8c55e42cda
ms.openlocfilehash: ca518796477dda149a9f4c0ebd65f0a082eab806
ms.contentlocale: es-es
ms.lasthandoff: 07/29/2017

---
# <a name="accessibility-features-in-system-center-configuration-manager"></a>Características de accesibilidad de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*


System Center Configuration Manager incluye características que ayudan a que sea accesible para personas con discapacidades.


## <a name="bkmk_aconsole"></a> Características de accesibilidad para la consola de Configuration Manager  

**Accesos directos y mejoras con la versión 1706 y posteriores**

|Método abreviado de teclado|  Finalidad|
|--------|--------|  
|Ctrl+M|Establece el foco en el panel principal (central).|
|Ctrl+T|Establece el foco en el nodo superior del panel de navegación. Si el foco ya estaba en dicho panel, este se establece en el último nodo que visitó.|
|Ctrl+I|Establece el foco en la barra de ruta de navegación, debajo de la cinta de opciones.|
|Ctrl+L|Establece el foco en el campo **Búsqueda**, si está disponible.|
|Ctrl+D|Establece el foco en el panel Detalles, si está disponible.|
|Alt     |Cambia el foco dentro y fuera de la cinta de opciones.|


- Navegación mejorada en el panel de navegación al escribir las letras de un nombre de nodo.
- La navegación con el teclado a través de la vista principal y la cinta de opciones ahora es circular.
- La navegación con el teclado en el panel de detalles ahora es circular. Para volver al objeto o panel anterior, utilice Ctrl + D y luego Mayús + Tab.
- Después de actualizar una vista del área de trabajo, se establece el foco en el panel principal de esa área de trabajo.
- Solución de un problema para permitir que los lectores de pantalla anuncien los nombres de elementos de lista.
- Incorporación de nombres accesibles para varios controles en la página que permite a los lectores de pantalla anunciar información importante.


**Los siguientes métodos abreviados de teclado están disponibles**

- Para tener acceso a un área de trabajo, utilice los siguientes métodos abreviados de teclado:  

|Método abreviado de teclado| Área de trabajo|
|--------|--------|  
|Ctrl + 1| Activos y compatibilidad|
|Ctrl+2|  Biblioteca de software|
|Ctrl+3|  monitoring|
|Ctrl+4|  Administración|


-   Para acceder a un menú del área de trabajo, presione la tecla TAB hasta que el foco esté en el icono Expandir o contraer. Después, presione la tecla de flecha abajo para acceder al menú del área de trabajo.  

-   Para navegar por un menú de área de trabajo, utilice las teclas de dirección.  

-   Para acceder a diferentes áreas del área de trabajo, utilice las teclas Tab y Mayús+Tab. Para navegar dentro de un área de trabajo, como la cinta, utilice las teclas de dirección.  

-   Para acceder a la barra de direcciones cuando el foco está en el nodo de árbol, presione tres veces Mayús+TAB.  

-   En una página de asistente o de propiedades, puede desplazarse entre los diferentes cuadros utilizando los métodos abreviados de teclado. Presione la tecla Alt y el carácter subrayado (Alt+_) para seleccionar un cuadro específico.     

-  Para desplazarse a los diferentes nodos de un área de trabajo, escriba la primera letra del nombre de un nodo. Cada presión de tecla mueve el cursor al siguiente nodo que comience con esa letra. Para los usuarios que tengan un lector de pantalla, el lector leerá el nombre del nodo.

> [!NOTE]  
>  Es posible que la información de esta sección solo sea válida para usuarios con licencia de productos de Microsoft en Estados Unidos. Si ha obtenido este producto fuera de los Estados Unidos, puede usar la tarjeta de información de filiales incluida en el paquete de software o visitar el [sitio web de accesibilidad de Microsoft](http://go.microsoft.com/fwlink/?LinkId=8431) para obtener la información de contacto de los servicios de soporte técnico de Microsoft. Puede ponerse en contacto con su distribuidor para conocer si el tipo de productos y servicios que se describen en esta sección están disponibles en su área. La información sobre accesibilidad está disponible en otros idiomas, incluidos japonés y francés.  

##  <a name="bkmk_ahelp"></a> Características de accesibilidad para la Ayuda de Configuration Manager  
 La Ayuda de Configuration Manager incluye características que la hacen accesible a más usuarios, incluidos aquellos con una destreza manual limitada, problemas de visión o alguna otra discapacidad.  

|Para|Utilice este método abreviado de teclado|  
|----------------|--------------------------------|  
|Mostrar la ventana de Ayuda.|F1|  
|Mover el cursor entre el panel de temas de Ayuda y el panel de navegación (las pestañas **Contenido**, **Búsqueda**e **Índice** ).|F6|  
|Cambiar entre las pestañas (por ejemplo, **Contenido**, **Búsqueda** e **Índice**) del panel de navegación.|Alt + letra subrayada de la ficha|  
|Seleccionar el siguiente texto oculto o hipervínculo.|Pestaña|  
|Seleccionar el hipervínculo o texto oculto anterior.|Mayús+Tabulador|  
|Realizar la acción seleccionada: Mostrar todo, Ocultar todo, texto oculto o hipervínculo.|INTRO|  
|Mostrar el menú **Opciones** para tener acceso a los comandos de la barra de herramientas de la Ayuda.|Alt+O|  
|Ocultar o mostrar el panel que contiene las pestañas **Contenido**, **Búsqueda** e **Índice**.|Alt+O y, después, seleccione T|  
|Mostrar el tema consultado anteriormente.|Alt+O y, después, seleccione B|  
|Mostrar el tema siguiente en una secuencia de temas mostrados anteriormente.|Alt+O y, después, seleccione F|  
|Volver a la página principal especificada.|Alt+O y, después, seleccione H|  
|Impedir que la ventana de Ayuda abra un tema de Ayuda (por ejemplo, para detener la descarga de una página web).|Alt+O y, después, seleccione S|  
|Abrir el cuadro de diálogo **Opciones de Internet** de Windows Internet Explorer, donde puede cambiar la configuración de accesibilidad.|Alt+O y, después, seleccione I|  
|Actualizar el tema, por ejemplo, una página web vinculada.|Alt+O y, después, seleccione R|  
|Imprimir todos los temas de un libro o solo un tema seleccionado.|Alt+O y, después, seleccione P|  
|Cerrar la ventana de Ayuda.|Alt+F4|  

#### <a name="to-change-the-appearance-of-a-help-topic"></a>Para cambiar la apariencia de un tema de Ayuda  

1.  Para prepararse para personalizar los colores, estilos de fuente y tamaños de fuente en la Ayuda, abra la ventana de Ayuda.  

2.  Seleccione **Opciones** y, después, **Opciones de Internet**.  

3.  En la pestaña **General**, seleccione **Accesibilidad**. Seleccione **Omitir colores especificados en páginas web**, **Omitir estilos de fuentes especificados en páginas web** y **Omitir tamaños de fuentes especificados en páginas web**. También puede usar la configuración especificada en su propia hoja de estilos.  

#### <a name="to-change-the-color-of-the-background-or-text-in-help"></a>Para cambiar el color de fondo o el texto de la Ayuda  

1.  Abra la ventana de Ayuda.  

2.  Seleccione **Opciones** y, después, **Opciones de Internet**.  

3.  En la pestaña **General**, seleccione **Accesibilidad**. Después, seleccione **Omitir colores especificados en páginas web**. También puede usar la configuración especificada en su propia hoja de estilos.  

4.  Para personalizar los colores que se usan en la Ayuda, en la pestaña **General**, seleccione **Colores**. Desactive la casilla **Usar colores de Windows** y, después, seleccione los colores de fondo y fuente que quiera usar.  

    > [!NOTE]  
    >  Si cambia el color de fondo de los temas de Ayuda en la ventana de Ayuda, el cambio también afectará el color de fondo de las páginas web en Windows Internet Explorer.  

#### <a name="to-change-the-font-in-help"></a>Para cambiar la fuente en la Ayuda  

1.  Abra la ventana de Ayuda.  

2.  Seleccione **Opciones** y, después, **Opciones de Internet**.  

3.  En la pestaña **General**, seleccione **Accesibilidad**. Para usar la misma configuración que en su instancia de Windows Internet Explorer, seleccione **Omitir estilos de fuentes especificados en páginas web** y **Omitir tamaños de fuentes especificados en páginas web**. También puede usar la configuración especificada en su propia hoja de estilos.  

4.  Para personalizar el estilo de fuente que se usa en la ayuda, en la pestaña **General**, seleccione **Fuentes** y, después, seleccione el estilo de fuente que prefiera.  

    > [!NOTE]  
    >  Si cambia la fuente de los temas de Ayuda en la ventana de Ayuda, el cambio también afecta las fuentes de las páginas web en Windows Internet Explorer.  

