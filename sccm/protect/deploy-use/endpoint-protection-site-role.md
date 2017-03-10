---
title: Crear un rol de sistema de sitio de punto de Endpoint Protection | Microsoft Docs
description: Aprenda a configurar Endpoint Protection para administrar la seguridad y el malware en equipos cliente de Configuration Manager.
defintion: 
definition: 
ms.custom: na
ms.date: 02/14/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 0a9dc0fe-a942-40a2-bab1-7eeee4d95380
caps.latest.revision: 21
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 017bd5b899b364fc832c721d63cc7dbad0a11671
ms.openlocfilehash: 884b5f2ec3f1aa273128dfeaaf88d969c9d8669d
ms.lasthandoff: 02/15/2017


---
# <a name="create-an-endpoint-protection-point-site-system-role"></a>Crear un rol de sistema de sitio de punto de Endpoint Protection

*Se aplica a: System Center Configuration Manager (rama actual)*

 El rol de sistema de sitio de punto de Endpoint Protection debe estar instalado para poder usar Endpoint Protection. Se debe instalar en un solo servidor de sistema de sitio y en la parte superior de la jerarquía en un sitio de administración central o un sitio primario independiente.

 Use uno de los procedimientos que se describen a continuación, según si quiere instalar un nuevo servidor de sistema de sitio para Endpoint Protection o usar un servidor de sistema de sitio existente:
 - [Instalar en un servidor de sistema de sitio nuevo](#new-site-system-server)
 - [Instalar en un servidor de sistema de sitio existente](#existing-site-system-server)

> [!IMPORTANT]
>  Cuando se instala un punto de Endpoint Protection, se instala un cliente de Endpoint Protection en el servidor que hospeda el punto de Endpoint Protection. Los servicios y los exámenes están deshabilitados en este cliente para que pueda coexistir con cualquier solución antimalware existente que esté instalada en el servidor. Si posteriormente habilita este servidor para la administración mediante Endpoint Protection y selecciona la opción para quitar cualquier solución antimalware de terceros, no se quitará el producto de terceros. Es necesario desinstalar este producto manualmente.

## <a name="new-site-system-server"></a>nuevo servidor de sistema de sitio

1.  En la consola de Configuration Manager, haga clic en **Administración**.

2.  En el área de trabajo **Administración** , expanda **Configuración del sitio**y, a continuación, haga clic en **Servidores y roles del sistema de sitios**.

3.  En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear servidor del sistema de sitio**.

4.  En la página **General** , especifique la configuración general del sistema de sitio y, a continuación, haga clic en **Siguiente**.

5.  En la página **Selección de rol del sistema** , seleccione **Punto de Endpoint Protection** en la lista de roles disponibles y luego haga clic en **Siguiente**.

6.  En la página **Endpoint Protection** , seleccione **Acepto los términos de licencia de Endpoint Protection** y luego haga clic en **Siguiente**.

    > [!IMPORTANT]
    >  No puede usar Endpoint Protection en Configuration Manager a menos que acepte los términos de licencia.

7.  En la página de **Cloud Protection Service**, seleccione el nivel de información que quiere enviar a Microsoft para ayudar a desarrollar nuevas definiciones y, luego, haga clic en **Siguiente**.

    > [!NOTE]
    >  Esta opción configura las opciones de Cloud Protection Service (antes conocido como Microsoft Active Protection Service o MAPS) que se usan de forma predeterminada. Por lo tanto, puede configurar opciones personalizadas para cada directiva antimalware que cree. Únase a Cloud Protection Service para ayudar a proteger los equipos al suministrar a Microsoft ejemplos de malware que pueden ayudar a que Microsoft mantenga las definiciones de antimalware más actualizadas. Además, si se une a Cloud Protection Service, el cliente de Endpoint Protection puede usar el servicio de firmas dinámicas para descargar nuevas definiciones antes de que se publiquen en Windows Update. Para obtener más información, consulte [How to create and deploy antimalware policies for Endpoint Protection in System Center Configuration Manager](endpoint-antimalware-policies.md) (Crear e implementar directivas antimalware para Endpoint Protection en System Center Configuration Manager).

8.  Complete el asistente.


## <a name="existing-site-system-server"></a>servidor de sistema de sitio existente

1.  En la consola de Configuration Manager, haga clic en **Administración**.

2.  En el área de trabajo **Administración**, expanda **Configuración del sitio**, haga clic en **Servidores y roles del sistema de sitios** y, luego, seleccione el servidor que quiere usar para Endpoint Protection.

3.  En la pestaña **Inicio** , en el grupo **Servidor** , haga clic en **Agregar roles del sistema de sitio**.

4.  En la página **General** , especifique la configuración general del sistema de sitio y, a continuación, haga clic en **Siguiente**.

5.  En la página **Selección de rol del sistema** , seleccione **Punto de Endpoint Protection** en la lista de roles disponibles y luego haga clic en **Siguiente**.

6.  En la página **Endpoint Protection** , seleccione **Acepto los términos de licencia de Endpoint Protection** y luego haga clic en **Siguiente**.

    > [!IMPORTANT]
    >  No puede usar Endpoint Protection en Configuration Manager a menos que acepte los términos de licencia.

7.  En la página de **Cloud Protection Service**, seleccione el nivel de información que quiere enviar a Microsoft para ayudar a desarrollar nuevas definiciones y, luego, haga clic en **Siguiente**.

    > [!NOTE]
    >  Esta opción configura las opciones de Cloud Protection Service (antes conocido como MAPS) que se usan de forma predeterminada. Puede configurar opciones personalizadas para cada directiva antimalware que configure. Para obtener más información, consulte [How to create and deploy antimalware policies for Endpoint Protection in System Center Configuration Manager](endpoint-antimalware-policies.md) (Crear e implementar directivas antimalware para Endpoint Protection en System Center Configuration Manager).

8.  Complete el asistente.

