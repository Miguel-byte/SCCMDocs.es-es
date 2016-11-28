---
title: Publicar datos del sitio | System Center Configuration Manager
description: "Obtenga información sobre cómo publicar sitios de Configuration Manager en Servicios de dominio de Active Directory."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 17cf034f-eaff-43ce-bc8e-917213c1db74
caps.latest.revision: 8
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: cda87a3bdcbba342f111b68af75369ca14744441


---
# <a name="publish-site-data-for-system-center-configuration-manager"></a>Publicar datos de sitio para System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Después de extender el esquema de Active Directory para System Center Configuration Manager, puede publicar sitios de Configuration Manager en Servicios de dominio de Active Directory (AD DS) para que los equipos de Active Directory puedan recuperar de forma segura la información del sitio desde un origen de confianza. Aunque no es necesario publicar la información del sitio en AD DS para obtener la funcionalidad básica de Configuration Manager, esta configuración puede reducir la carga de trabajo administrativo.  

-   **Cuando hay un sitio configurado para publicar en AD DS**, los clientes de Configuration Manager pueden buscar automáticamente puntos de administración mediante la publicación de Active Directory usando una consulta LDAP en un servidor de catálogo global.  

-   **Cuando un sitio no publica en AD DS**, los clientes deben tener un mecanismo alternativo para buscar su punto de administración predeterminado.  

Para obtener más información sobre cómo pueden buscar los clientes un punto de administración, consulte [Understand how clients find site resources and services for System Center Configuration Manager](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md) (Comprender cómo los clientes buscan servicios y recursos de sitio para System Center Configuration Manager).  

## <a name="configure-sites-to-publish-to-ad-ds"></a>Configurar sitios para publicar en AD DS  
 Estos son los pasos generales:  

-   Debe [extender el esquema de Active Directory para System Center Configuration Manager](../../../../core/plan-design/network/extend-the-active-directory-schema.md) en todos los bosques en los que publicará datos del sitio y garantizar que el contenedor **System Management** está presente.  

-   Debe conceder a la cuenta de equipo de cada sitio principal que publicará datos   **control total** sobre el contenedor **System Management** y todos sus objetos secundarios.  

#### <a name="to-enable-a-configuration-manager-site-to-publish-site-information-to-active-directory-forest"></a>Para habilitar que un sitio de Configuration Manager publique información del sitio en el bosque de Active Directory:  

1.  En la consola de Configuration Manager, haga clic en **Administración**.  

2.  En el área de trabajo **Administración** , expanda **Configuración del sitio** y haga clic en **Sitios**. Seleccione el sitio que desee configurar para que publique sus datos y, a continuación, en la pestaña **Inicio** , en el grupo **Propiedades** , haga clic en **Propiedades**.  

3.  En la pestaña **Publicación** de las propiedades de los sitios, seleccione los bosques en los que este sitio publicará los datos.  

4.  Haga clic en **Aceptar** para guardar la configuración.  

 Use el siguiente procedimiento para configurar un bosque de Active Directory para publicación:  

#### <a name="to-configure-active-directory-forests-for-publishing"></a>Para configurar los bosques de Active Directory para la publicación:  

1.  En la consola de Configuration Manager, haga clic en **Administración**.  

2.  En el área de trabajo **Administración** , haga clic en **Bosques de Active Directory**. Si previamente ejecutó la detección de bosques de Active Directory, verá cada bosque detectado en el panel de resultados. El bosque local y todos los bosques de confianza se detectan cuando se ejecuta la detección de bosques de Active Directory. Sólo deben agregarse manualmente los bosques que no son de confianza.  

    -   Para configurar un bosque detectado previamente, seleccione el bosque en el panel de resultados y, a continuación, en la pestaña **Inicio** , en el grupo **Propiedades** , haga clic en **Propiedades** para abrir las propiedades del bosque. Continúe con el paso 3.  

    -   Para configurar un bosque nuevo que no se muestra, en la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Agregar bosque** para abrir el cuadro de diálogo **Agregar bosques** . Continúe con el paso 3.  

3.  En la pestaña **General** , realice las configuraciones del bosque que desea detectar y especifique la **Cuenta de bosque de Active Directory**.  

    > [!NOTE]  
    >  La detección de bosques de Active Directory requiere una cuenta global para detectar bosques que no son de confianza y publicar en ellos. Si no utiliza la cuenta de equipo del servidor de sitio, solo se puede seleccionar una cuenta global.  

4.  Si planea permitir que los sitios publiquen datos del sitio en este bosque, en la pestaña **Publicación** , realice las configuraciones necesarias para publicar en este bosque.  

    > [!NOTE]  
    >  Si habilita los sitios para que publiquen en un bosque, debe extender el esquema de Active Directory de dicho bosque para Configuration Manager, y la Cuenta de bosque de Active Directory debe tener permisos de control total para el contenedor del sistema en dicho bosque.  

5.  Cuando termine la configuración de este bosque para utilizarlo con la detección de bosques de Active Directory, haga clic en **OK** para guardar la configuración.  



<!--HONumber=Nov16_HO1-->


