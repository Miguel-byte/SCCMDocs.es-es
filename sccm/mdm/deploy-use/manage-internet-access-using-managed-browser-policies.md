---
title: Administrar el acceso a Internet mediante directivas de explorador administrado
titleSuffix: Configuration Manager
description: Implemente Intune Managed Browser para administrar y restringir el acceso a Internet.
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8e25e00c-c9a8-473f-bcb7-ea989f6ca3c5
caps.latest.revision: "6"
caps.handback.revision: "0"
author: dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 3aea2a65733a52ab532d451b21ae98fbc0f122c6
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/12/2017
---
# <a name="manage-internet-access-using-managed-browser-policies-with-system-center-configuration-manager"></a>Administrar el acceso a Internet mediante directivas de explorador administrado con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

En System Center Configuration Manager, puede implementar Intune Managed Browser (una aplicación de exploración web) y asociar la aplicación con una directiva de explorador administrado. La directiva de explorador administrado configura una lista de permitidos o una lista de bloqueados que restringe los sitios web a los que pueden ir los usuarios del explorador administrado.  

 Dado que esta aplicación es una aplicación administrada, también puede aplicarle directivas de administración de aplicaciones móviles, como controlar el uso de cortar, copiar y pegar. Esto impide las capturas de pantalla y también garantiza que los vínculos a contenido solo se abran en otras aplicaciones administradas. Para obtener más información, consulte [Protect apps using mobile application management policies](protect-apps-using-mam-policies.md) (Protección de aplicaciones mediante directivas de administración de aplicaciones locales).  

> [!IMPORTANT]  
>  Si los usuarios instalan el explorador administrado ellos mismos, las directivas especificadas no lo administrarán. Para asegurarse de que el explorador se administra mediante Configuration Manager, estos deben desinstalar la aplicación para que se la pueda implementar como una aplicación administrada.  

 Puede crear directivas de explorador administrado para los siguientes tipos de dispositivo:  

-   Dispositivos que ejecutan Android 4 y versiones posteriores  

-   Dispositivos que ejecutan iOS 7 y versiones posteriores  

> [!NOTE]  
>  Para obtener más información sobre la aplicación Intune Managed Browser y descargarla, consulte [iTunes](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8) para iOS y [Google Play](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser&hl=en) para Android.  

## <a name="create-a-managed-browser-policy"></a>Crear una directiva de explorador administrado  

1.  En la consola de Configuration Manager, seleccione **Biblioteca de software** > **Administración de aplicaciones** > **Directivas de administración de aplicaciones**.  

3.  En la pestaña **Inicio**, en el grupo **Crear**, seleccione **Crear directiva de administración de aplicaciones**.  

4.  En la página **General**, escriba el nombre y la descripción de la directiva y seleccione **Siguiente**.  

5.  En la página **Tipo de directiva**, seleccione la plataforma, elija **Explorador administrado** para el tipo de directiva y seleccione **Siguiente**.  

     En la página **Explorador administrado** , seleccione una de las siguientes opciones:  

    -   **Permitir al explorador administrado abrir únicamente las direcciones URL de la lista siguiente**: especifique una lista de direcciones URL que el explorador administrado podrá abrir.  

    -   **Bloquear el explorador administrado para que no pueda abrir las direcciones URL de la lista siguiente**: especifique una lista de direcciones URL que el explorador administrado no podrá abrir.  

    > [!NOTE]  
    >  No puede incluir direcciones URL permitidas y bloqueadas en la misma directiva de explorador administrado.  

     Para obtener más información sobre los formatos de dirección URL que se pueden especificar, consulte Formato de dirección URL para las direcciones URL permitidas y bloqueadas en este artículo.  

    > [!NOTE]  
    >  El tipo de directiva General permite cambiar la funcionalidad de las aplicaciones que implementa para que se ajusten a los requisitos de cumplimiento y las directivas de seguridad de su empresa. Por ejemplo, puede restringir las operaciones de cortar, copiar y pegar en una aplicación restringida. Para obtener más información sobre el tipo de directiva general, consulte [Proteger aplicaciones mediante directivas de administración de aplicaciones móviles](protect-apps-using-mam-policies.md).  

6.  Finalice el asistente.  

La directiva nueva se muestra en el nodo **Directivas de administración de aplicaciones** del área de trabajo **Biblioteca de software** .  

## <a name="create-a-software-deployment-for-the-managed-browser-app"></a>Crear una implementación de software para la aplicación de explorador administrado  
 Después de crear la directiva de explorador administrado, puede crear un tipo de implementación de software para la aplicación de explorador administrado. Debe asociar una directiva general y una directiva de explorador administrado para la aplicación de explorador administrado.  

 Para obtener más información, consulte [Create applications](create-applications.md) (Creación de aplicaciones).  

## <a name="security-and-privacy-for-the-managed-browser"></a>Seguridad y privacidad del explorador administrado  

-   En dispositivos iOS, no se pueden abrir los sitios web que tienen un certificado expirado o que no es de confianza.  

-   El explorador administrado no usa la configuración que realizan los usuarios para el explorador integrado en sus dispositivos. El explorador administrado no tiene acceso a esta configuración.  

-   Si configura las opciones **Requerir PIN sencillo para el acceso** o **Requerir credenciales corporativas para el acceso** en una directiva de administración de aplicaciones móviles asociada con el explorador administrado, un usuario puede hacer clic en Ayuda en la página de autenticación e ir a cualquier sitio, incluso a uno que se haya agregado a una lista de bloqueados en la directiva de explorador administrado.  

-   El explorador administrado solo puede bloquear el acceso a sitios cuando se accede a estos directamente. No puede bloquear el acceso cuando se usan servicios intermedios (por ejemplo, un servicio de traducción) para acceder al sitio.  

## <a name="reference-information"></a>Información de referencia  

###  <a name="url-format-for-allowed-and-blocked-urls"></a>Formato de dirección URL para las direcciones URL permitidas y bloqueadas  

Utilice la siguiente información para conocer los formatos permitidos y los caracteres comodín que puede usar al especificar direcciones URL en las listas de permitidos y bloqueados.  

-   Puede utilizar el carácter comodín '**\***' según las reglas de la siguiente lista de patrones permitidos.  

-   Asegúrese de anteponer **http** o **https** a todas las direcciones URL al introducirlas en la lista.  

-   Puede especificar números de puerto en la dirección. Si no especifica un número de puerto, los valores usados serán:  

    -   Puerto 80 para http  

    -   Puerto 443 para https  

     No se admite el uso de caracteres comodín para el número de puerto como, por ejemplo, **http://www.contoso.com:\*** y **http://www.contoso.com: /\***  

-   Utilice la siguiente tabla para obtener información acerca de los patrones permitidos que puede usar al especificar direcciones URL:  

    |Dirección URL|Coincide|No coincide|  
    |---------|-------------|--------------------|  
    |http://www.contoso.com<br /><br /> Coincide con una sola página|www.contoso.com|host.contoso.com<br /><br /> www.contoso.com/images<br /><br /> contoso.com/|  
    |http://contoso.com<br /><br /> Coincide con una sola página|contoso.com/|host.contoso.com<br /><br /> www.contoso.com/images<br /><br /> www.contoso.com|  
    |http://www.contoso.com/*<br /><br /> Coincide con todas las direcciones URL que comienzan con www.contoso.com|www.contoso.com<br /><br /> www.contoso.com/images<br /><br /> www.contoso.com/videos/tvshows|host.contoso.com<br /><br /> host.contoso.com/images|  
    |http://*.contoso.com/\*<br /><br /> Coincide con todos los subdominios en contoso.com|developer.contoso.com/resources<br /><br /> news.contoso.com/images<br /><br /> news.contoso.com/images|contoso.host.com|  
    |http://www.contoso.com/images<br /><br /> Coincide con una sola carpeta|www.contoso.com/images|www.contoso.com/images/dogs|  
    |http://www.contoso.com:80<br /><br /> Coincide con una sola página, con un número de puerto|http://www.contoso.com:80||  
    |https://www.contoso.com<br /><br /> Coincide con una sola página segura|https://www.contoso.com|http://www.contoso.com|  
    |http://www.contoso.com/images/*<br /><br /> Coincide con una sola carpeta y todas sus subcarpetas|www.contoso.com/images/dogs<br /><br /> www.contoso.com/images/cats|www.contoso.com/videos|  

-   Los siguientes son ejemplos de algunas de las entradas que no se pueden especificar:  

    -   *.com  

    -   *.contoso/\*  

    -   www.contoso.com/*images  

    -   www.contoso.com/*images\*pigs  

    -   www.contoso.com/page*  

    -   Direcciones IP  

    -   https://*  

    -   http://*  

    -   http://www.contoso.com:*  

    -   http://www.contoso.com: /*  

> [!NOTE]  
>  *.microsoft.com siempre se permite.  

### <a name="how-conflicts-between-the-allow-and-block-list-are-resolved"></a>Cómo se resuelven los conflictos entre las listas de permitidos y bloqueados  
 Si se implementan varias directivas de explorador administrado en un dispositivo y la configuración presenta conflictos, tanto el modo (permitir o bloquear) como las listas de direcciones URL se evalúan para detectar conflictos. En caso de conflicto, se aplica el comportamiento siguiente:  

-   Si los modos de cada directiva son iguales, pero las listas de direcciones URL son diferentes, las direcciones URL no se aplicarán en el dispositivo.  

-   Si los modos de cada directiva son diferentes, pero las listas de direcciones URL son iguales, las direcciones URL no se aplicarán en el dispositivo.  

-   Si un dispositivo está recibiendo las directivas de explorador administrado por primera vez y dos directivas están en conflicto, las direcciones URL no se aplicarán en el dispositivo. Utilice el nodo **Conflictos de directivas** del área de trabajo **Directiva** para ver los conflictos.  

-   Si un dispositivo ya ha recibido una directiva de explorador administrado y se implementa una segunda directiva con la configuración en conflicto, la configuración original permanece en el dispositivo. Utilice el nodo **Conflictos de directivas** del área de trabajo **Directiva** para ver los conflictos.  
