---
title: "TÍTULO DEL ARTÍCULO | Microsoft Docs"
description: 
keywords: 
author: GITHUB USERNAME
manager: ALIAS
ms.date: 10/06/2016
ms.topic: article
ms.prod: 
ms.service: 
ms.technology: 
ms.assetid: GET ONE FROM guidgenerator.com
ms.openlocfilehash: a218011ded1ff3acc1dbd24471119b701f2cce23
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/07/2017
---
# <a name="metadata-and-markdown-template"></a>Metadatos y plantilla Markdown

Esta plantilla docs.ms contiene ejemplos de sintaxis Markdown, además de una guía para configurar los metadatos. Está disponible en el directorio raíz de cada repositorio de EM Pilot (por ejemplo, ~/Azure-RMSDocs-pr /template.md) y está pensado para leerse como un archivo de Markdown, aunque puede consultar la [versión publicada](https://stage.docs.microsoft.com/en-us/rights-management/template) para ver cómo se representan los ejemplos de Markdown.

Al crear un archivo de Markdown, copie la plantilla en un archivo nuevo, rellene los metadatos como se especifica a continuación, establezca el encabezado H1 anterior para el título del artículo y elimine el contenido.


## <a name="metadata"></a>Metadatos

El bloque de metadatos completo está arriba, dividido entre los campos obligatorios y los opcionales; vea la [hoja de referencia rápida de metadatos de OPS](https://ppe.msdn.microsoft.com/en-us/ce-csi-docs/ops/ops-onboarding/managing-content/content-meta-data) para obtener más información. Algunas notas clave:

- **Debe** haber un espacio entre los dos puntos (:) y el valor de un elemento de metadatos.
- Si un elemento de metadatos opcional no tiene ningún valor, comente el elemento con un símbolo # (no lo deje vacío ni use "na"); si va a agregar un valor a un elemento comentado, asegúrese de quitar el signo #.
- Los dos puntos en un valor (por ejemplo, un título) interrumpen el analizador de metadatos. En su lugar, utilice la codificación HTML de &#58; (p. ej., "title: Azure Rights Management &#58; aspectos básicos | Azure RMS").
- **title**: este título aparecerá en los resultados del motor de búsqueda. El título debe finalizar con una línea vertical (|) seguida del nombre del servicio (por ejemplo, véase el caso anterior). El título no tiene que ser idéntico al título del encabezado H1, y probablemente no lo sea. Debe tener aproximadamente 65 caracteres (incluidos | NOMBRE DEL SERVICIO)
- **author**, **manager** y **reviewer**: el campo author debe contener el **nombre de usuario de GitHub** del autor, no su alias.  Los campos "manager" y "reviewer", por otro lado, deben contener alias. ms.reviewer especifica el nombre del jefe de proyecto asociado con el artículo o servicio.
- **ms.assetid**: se trata del GUID del artículo de CAPS. Al crear un archivo de Markdown, obtenga un GUID en [https://www.guidgenerator.com](https://www.guidgenerator.com).
- **ms.prod**, **ms.service**, **ms.technology**, **ms.devlang**, **ms.topic** y **ms.tgt_pltfrm**: los posibles valores para estos elementos se pueden encontrar [aquí](https://microsoft.sharepoint.com/teams/STBCSI/Insights/_layouts/15/WopiFrame.aspx?sourcedoc=%7b7A321BF1-0611-4184-84DA-A0E964C435FA%7d&file=WEDCS_MasterList_CSIValues.xlsx&action=default).

## <a name="basic-markdown-and-gfm"></a>Markdown de línea base y GFM

Se admiten todos los elementos de Markdown de línea base y de GitHub Flavored Markdown. Para más información relacionada, vea:

- [Sintaxis de Markdown de línea de base](https://daringfireball.net/projects/markdown/syntax)
- [Documentación de GitHub Flavored Markdown (GFM)](https://guides.github.com/features/mastering-markdown)

## <a name="headings"></a>Encabezados

Los ejemplos de los encabezados de primer y segundo nivel se han expuesto anteriormente.

**Debe** haber solo un encabezado de primer nivel en el tema, que se mostrará como el título de la página.  

Los encabezados de segundo nivel generarán la tabla de contenido que aparece en la sección "En este artículo" debajo del título de la página.

### <a name="third-level-heading"></a>Encabezado de tercer nivel
#### <a name="fourth-level-heading"></a>Encabezado de cuarto nivel
##### <a name="fifth-level-heading"></a>Encabezado de quinto nivel
###### <a name="sixth-level-heading"></a>Encabezado de sexto nivel

## <a name="text-styling"></a>Estilo del texto

*Cursiva*

**Negrita**

~~Tachado~~



## <a name="links"></a>Vínculos

Para vincular a un archivo de Markdown en el mismo repositorio, utilice [vínculos relativos](https://www.w3.org/TR/WD-html40-970917/htmlweb.html#h-5.1.2).

- Ejemplo: [¿Qué es Azure Rights Management?](./understand-explore/what-is-azure-rights-management.md)

Para vincular a un encabezado en el mismo archivo de Markdown, vea el origen del artículo publicado, busque el identificador del encabezado (por ejemplo, `id="blockquote"`, y vincúlelo con # + identificador (por ejemplo, `#blockquote`).

- Ejemplo: [Blockquotes](#blockquote)

Para crear un vínculo a un encabezado de un archivo de Markdown en el mismo repositorio, use la vinculación relativa + vinculación hashtag.

- Ejemplo: [información técnica del proceso de inicio de sesión](./understand-explore/rms-for-individuals-user-signup.md#technical-overview-of-the-sign-up-process)

Para crear un vínculo a un archivo externo, use la dirección URL completa como vínculo.

- Ejemplo: [GitHub](http://www.github.com)

Si aparece una dirección URL en un archivo de Markdown, se transformará en un vínculo interactivo.

- Ejemplo: http://www.github.com

## <a name="lists"></a>Listas

### <a name="ordered-lists"></a>Listas ordenadas

1. Esta
1. es
1. una
1. lista
1. ordenada  


#### <a name="ordered-list-with-an-embedded-list"></a>Lista ordenada con una lista insertada

1. Esta
1. es
1. una
1. lista
    1. Miss Scarlett
    1. Professor Plum
1. ordenada
1. insertada


### <a name="unordered-lists"></a>Listas desordenadas

- Esta
- es
- una
- lista
- con viñetas


##### <a name="unordered-list-with-an-embedded-lists"></a>Lista desordenada con una lista insertada

- Esta
- lista
- con viñetas
    - Mrs. Peacock
    - Mr. Green
- contiene  
- otras
    1. Colonel Mustard
    1. Mrs. White
- listas


## <a name="horizontal-rule"></a>Regla horizontal

---

## <a name="tables"></a>Tablas

| Las tablas        | son           | estupendas  |
| ------------- |:-------------:| -----:|
| la col. 3 está      | alineada a la derecha | 1600 USD |
| la col. 2 está      | centrada      |   12 USD |
| La col. 1, de forma predeterminada, está | alineada a la izquierda     |    1 USD |


## <a name="code"></a>Código

### <a name="codeblock"></a>Bloque de código

    function fancyAlert(arg) {
      if(arg) {
        $.docs({div:'#foo'})
      }
    }

### <a name="in-line-code"></a>Código insertado

Este es un ejemplo de `in-line code`.

## <a name="blockquotes"></a>Citas en bloque

> La sequía había durado ya diez millones de años, y el reinado de los terribles saurios tiempo ha que había terminado. Aquí en el ecuador, en el continente que había de ser conocido un día como África, la batalla por la existencia había alcanzado un nuevo clímax de ferocidad, no avistándose aún al victorioso. En este terreno baldío y desecado, sólo podía medrar, o aún esperar sobrevivir, lo pequeño, lo raudo o lo feroz.

## <a name="images"></a>Imágenes

### <a name="static-image"></a>Imagen estática

![se trata del texto alternativo](./media/AzRMS_elements.png)

### <a name="linked-image"></a>Imagen vinculada

[![texto alternativo para la imagen vinculada](./media/AzRMS_elements.png)](https://azure.microsoft.com)

### <a name="animated-gif"></a>Gif animado

![Gif animado](./media/hololens.gif)

## <a name="alerts"></a>Alertas

### <a name="note"></a>Nota

> [!NOTE]
> Se trata de una NOTA.

### <a name="warning"></a>Advertencia

> [!WARNING]
> Se trata de una ADVERTENCIA.

### <a name="tip"></a>Sugerencia

> [!TIP]
> Se trata de una SUGERENCIA.

### <a name="important"></a>Importante

> [!IMPORTANT]
> Se trata de algo IMPORTANTE.

## <a name="videos"></a>Vídeos

### <a name="channel-9"></a>Channel9

<iframe src="http://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-Active-Directory-Connect-Express-Settings/player" width="960" height="540" allowFullScreen frameBorder="0"></iframe>


### <a name="youtube"></a>YouTube

<iframe width="420" height="315" src="https://www.youtube.com/embed/R6_eWWfNB54" frameborder="0" allowfullscreen></iframe>

## <a name="docsms-extentions"></a>Extensiones de docs.ms

### <a name="button"></a>Botón

> [!div class="button"]
[vínculos de botón](/rights-management)

### <a name="selector"></a>Selector

> [!div class="op_single_selector"]
- [foo](/rights-management/template.md)
- [bar](/rights-management/scratch.md)

### <a name="step-by-step"></a>Paso a paso

>[!div class="step-by-step"]
[Anterior](https://www.example.com)
[Siguiente](https://www.example.com)
