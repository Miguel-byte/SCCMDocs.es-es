---
title: Búsqueda de ayuda
titleSuffix: Configuration Manager
description: Busque recursos para obtener más información sobre Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 86810629-cf2a-43e8-86a2-847444119fc1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9440a4873b6011ed4a7394c335531afc72ac5d97
ms.sourcegitcommit: deb28cdc95a456d4a38499ef1bc71e765ef6dc13
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/03/2019
ms.locfileid: "58901407"
---
# <a name="find-help-for-using-configuration-manager"></a>Buscar ayuda para usar Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

En este artículo se proporcionan las siguientes secciones con varios recursos para buscar ayuda sobre el uso de Configuration Manager:  

- [Documentación del producto](#bkmk_Info)  

- [Compartir comentarios sobre el producto](#product-feedback)  

- [Seguir el blog del equipo de Configuration Manager](#BKMK_ProductGroupBlog)  

- [Opciones de soporte técnico y recursos de la comunidad](#BKMK_SupportOptions)  

Para obtener ayuda sobre la accesibilidad del producto, vea [Características de accesibilidad](/sccm/core/understand/accessibility-features).  



##  <a name="bkmk_Info"></a> Documentación del producto  

Para acceder a la documentación más reciente del producto, comience en el [índice de biblioteca](https://docs.microsoft.com/sccm/).  

<a name="BKMK_SearchTips"></a>  

Para obtener sugerencias sobre cómo buscar, proporcionar comentarios y obtener más información sobre el uso de la documentación del producto, vea [Cómo usar los documentos](/sccm/core/understand/use-docs).  



<a name="product-feedback"></a>

## <a name="BKMK_1806Feedback"></a> Comentarios sobre el producto a partir de la versión 1806

A partir de la versión 1806 de Configuration Manager, puede enviar comentarios sobre el producto directamente desde la consola. Si tiene que adjuntar registros, use [Concentrador de comentarios](#BKMK_FeedbackHub). Puede hacer lo siguiente: <!--1357542-->

  - **Enviar una sonrisa**: envíe comentarios sobre lo que le ha gustado.
  - **Enviar una desaprobación**: envíe comentarios sobre lo que no le ha gustado.
  - **Enviar una sugerencia**: se abre el [Sitio web de UserVoice](https://configurationmanager.uservoice.com/) para que pueda compartir su idea.

    ![Enviar comentarios en Configuration Manager 1806](media/1806-send-a-smile.png)


### <a name="send-a-smile"></a>Enviar una sonrisa

Para enviar comentarios sobre algo que le gustó siga las siguientes instrucciones: 
1. En la esquina superior derecha de la consola, haga clic en la cara sonriente. 
2. En el menú desplegable, seleccione **Enviar una sonrisa**.
3. Utilice el cuadro de texto para explicar lo que le gustó. 
4. Elija si quiere compartir su dirección de correo electrónico y una captura de pantalla. 
5. Haga clic en **Enviar comentarios**
     - Si no tiene conectividad a Internet, haga clic en **Guardar** en la parte inferior. Siga las instrucciones de la sección [Enviar comentarios que ha guardado para enviarlos más tarde](#BKMK_NoInternet) para enviarlo a Microsoft. 

![Formulario de envío de comentarios en Configuration Manager 1806](media/1806-feedback-form.png)


### <a name="send-a-frown"></a>Enviar una desaprobación

Para enviar comentarios sobre algo que no le gustó siga las siguientes instrucciones:

1. En la esquina superior derecha de la consola, haga clic en la cara sonriente. 
2. En el menú desplegable, seleccione **Enviar una desaprobación**.
3. Utilice el cuadro de texto para explicar lo que no le gustó. 
4. Elija si quiere compartir su dirección de correo electrónico y una captura de pantalla. 
5. Haga clic en **Enviar comentarios**
     - Si no tiene conectividad a Internet, haga clic en **Guardar** en la parte inferior. Siga las instrucciones de la sección [Enviar comentarios que ha guardado para enviarlos más tarde](#BKMK_NoInternet) para enviarlo a Microsoft.  

### <a name="send-a-suggestion"></a>Enviar una sugerencia

Cuando **envía una sugerencia**, se le redirige a [UserVoice](https://configurationmanager.uservoice.com/), un sitio web de terceros, para que comparta su idea. El equipo de producto de Configuration Manager usa los siguientes valores de estado en UserVoice:

- **Anotado**: entendemos la solicitud y tiene sentido. La hemos agregado a nuestro trabajo pendiente.
- **Planeado**: hemos empezado a escribir código para esta característica y esperamos que aparezca en una compilación de versión preliminar técnica dentro de los próximos meses.
- **Iniciado**: la característica se encuentra actualmente en una versión preliminar técnica. Pruébela y envíenos sus comentarios para hacernos saber si va por buen camino. Incluya comentarios adicionales en la sección de comentarios de la solicitud original para que otros usuarios puedan verlos y escribir su opinión. Nosotros también los consultaremos y nos basaremos en ellos para intentar mejorar la característica.
- **Completado**: la primera versión de la característica se encuentra en una compilación de producción. Este estado no significa que hayamos completado la característica al 100 % y que no vayamos a mejorarla más, sino que la primera versión de la característica se encuentra en una compilación de producción y puede empezar a usarse. La hemos marcado como completada por las razones siguientes:
  - Queremos que sepa que la característica está lista para la producción.
  - Queremos devolverle sus votos de UserVoice para que pueda usarlos en otros elementos.
  - Puede presentar nuevas solicitudes de cambio de diseño para esta característica, a fin de hacernos saber cuál es la siguiente mejora más importante para la característica.

### <a name="information-sent-with-feedback"></a>Información enviada con comentarios

Cuando **envíe una sonrisa** o **envíe una desaprobación**, se incluirá la información siguiente con los comentarios:
 
   - Información de compilación del sistema operativo
   - Id. de jerarquía de Configuration Manager
   - Información de compilación del producto
   - Información de idioma
   - Identificador de dispositivo 
       - HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SQMClient:MachineId



### <a name="BKMK_NoInternet"></a> Enviar comentarios que ha guardado para enviarlos más tarde

1. Haga clic en **Guardar** en la parte inferior de la ventana **Proporcionar comentarios**. 
2. Guarde el archivo .zip. Si el equipo local no tiene acceso a Internet, copie el archivo en una máquina conectada a Internet. 
3. Si es necesario, copie UploadOfflineFeedback.exe ubicado en `cd.latest\SMSSETUP\Tools\UploadOfflineFeedback\UploadOfflineFeedback.exe`
    - Para obtener más información sobre la carpeta CD.Latest, vea [La carpeta CD.Latest](../servers/manage/the-cd.latest-folder.md)

4. En una máquina conectada a Internet, abra un símbolo del sistema. 
5. Ejecute el comando siguiente: `UploadOfflineFeedback.exe -f c:\folder\location_of.zip`.
    
    - Si quiere, puede especificar los parámetros siguientes:
        -  `-t, --timeout` Tiempo de espera en segundos para enviar los datos. 0 es ilimitado. El valor predeterminado es 30.
        - `-s --silent` Ningún registro en la consola (no se puede combinar con --verbose)
        - `-v, --verbose` Registro detallado de salida en la consola (no se puede combinar con --silent)
        - `--help` Muestra la pantalla de ayuda

## <a name="bkmk_feedbackid"></a> Confirmación de comentarios de la consola

<!--3556010-->
A partir de la versión 1902, al enviar comentarios a través de la consola de Configuration Manager o UploadOfflineFeedback.exe, aparecerá un mensaje de confirmación. Este mensaje incluye un **identificador de comentario** que puede enviar a Microsoft como identificador de seguimiento.

- Para copiar el **identificador de comentario**, seleccione el icono de copia situado junto al identificador o use las teclas de método abreviado **CTRL** + **C**.
  - Este identificador no se almacena en el equipo, así que asegúrese de copiarlo antes de cerrar la ventana.
- Si hace clic en **No volver a mostrar este mensaje**, suprimirá el cuadro de diálogo y evitará que aparezca en el futuro.

   ![Confirmación de comentarios de la consola en Configuration Manager 1902](media/1902-feedback-id-example.png)
- La herramienta de comando **UploadOfflineFeedback** escribe el **FeedbackID** en la consola, a menos que se use -s o --silent.

  ![Confirmación de comentarios de UploadOfflineFeedback.exe en Configuration Manager 1902](media/1902-offline-feedback-id-example.png)

##  <a name="BKMK_FeedbackHub"></a> Comentarios sobre el producto para la versión 1802 y anteriores

Notifique los posibles defectos del producto a través de la [aplicación Centro de opiniones](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app) integrada en Windows 10. Cuando **agregue nuevos comentarios**, no olvide seleccionar la categoría **Enterprise Management** y, después, elija una de las subcategorías siguientes:
 - Cliente de Configuration Manager
 - Consola de Configuration Manager
 - Implementación del sistema operativo de Configuration Manager
 - Servidor de Configuration Manager

Siga usando la [página de UserVoice](https://configurationmanager.uservoice.com/) para votar por nuevas ideas de características en Configuration Manager. El equipo de producto de Configuration Manager usa los siguientes valores de estado en UserVoice:

- **Anotado**: entendemos la solicitud y tiene sentido. La hemos agregado a nuestro trabajo pendiente.
- **Planeado**: hemos empezado a escribir código para esta característica y esperamos que aparezca en una compilación de versión preliminar técnica dentro de los próximos meses.
- **Iniciado**: la característica se encuentra actualmente en una versión preliminar técnica. Pruébela y envíenos sus comentarios para hacernos saber si va por buen camino. Incluya comentarios adicionales en la sección de comentarios de la solicitud original para que otros usuarios puedan verlos y escribir su opinión. Nosotros también los consultaremos y nos basaremos en ellos para intentar mejorar la característica.
- **Completado**: la primera versión de la característica se encuentra en una compilación de producción. Este estado no significa que hayamos completado la característica al 100 % y que no vayamos a mejorarla más, sino que la primera versión de la característica se encuentra en una compilación de producción y puede empezar a usarse. La hemos marcado como completada por las razones siguientes:
  - Queremos que sepa que la característica está lista para la producción.
  - Queremos devolverle sus votos de UserVoice para que pueda usarlos en otros elementos.
  - Puede presentar nuevas solicitudes de cambio de diseño para esta característica, a fin de hacernos saber cuál es la siguiente mejora más importante para la característica.

##  <a name="BKMK_ProductGroupBlog"></a> Blog del equipo de Configuration Manager  

El equipo de ingeniería de Configuration Manager y los equipos asociados usan el [blog Enterprise Mobility + Security](https://cloudblogs.microsoft.com/enterprisemobility/?product=system-center-configuration-manager) para ofrecer información técnica y otras noticias sobre Configuration Manager y tecnologías relacionadas. Nuestras entradas de blog complementan la documentación del producto y la información de soporte técnico.  


##  <a name="BKMK_SupportOptions"></a> Opciones de soporte técnico y recursos de la comunidad  

Los siguientes vínculos proporcionan información sobre las opciones de soporte técnico y los recursos de la comunidad:  

-   [Soporte técnico de Microsoft](https://aka.ms/cmcbsupport)  

-   [Comunidad de Configuration Manager: guía de supervivencia de System Center Configuration Manager (rama actual)](https://social.technet.microsoft.com/wiki/contents/articles/33035.system-center-configuration-manager-current-branch-survival-guide.aspx )  

-   [Página de foros de Configuration Manager](https://social.technet.microsoft.com/Forums/en-US/home?category=ConfigMgrCB)  
    <!-- NOTE: the above URL requires "en-US" for the category to work -->
