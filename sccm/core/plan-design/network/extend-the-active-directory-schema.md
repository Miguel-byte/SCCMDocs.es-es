---
title: "Publicación y el esquema de Active Directory | Microsoft Docs"
description: Extienda el esquema de Active Directory para System Center Configuration Manager a fin de simplificar el proceso de implementar y configurar clientes.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: bc15ee7e-4d0a-4463-ae2c-f72d8d45d65d
caps.latest.revision: 17
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2083a2ca7a199771f26981cdbe04e4e2ef6e8958
ms.openlocfilehash: 3bd18e2de76d886b275c80d0dce3b824f2598008


---
# <a name="prepare-active-directory-for-site-publishing"></a>Preparar Active Directory para la publicación de sitios

*Se aplica a: System Center Configuration Manager (Rama actual)*

Si extiende el esquema de Active Directory para System Center Configuration Manager, introduce estructuras nuevas en Active Directory que los sitios de Configuration Manager usan para publicar información clave en una ubicación segura donde los clientes pueden acceder fácilmente a ella.  

 Se recomienda que use Configuration Manager con un esquema de Active Directory extendido al administrar los clientes locales. Un esquema extendido puede simplificar el proceso de implementar y configurar clientes, y permite que los clientes localicen de manera eficaz los recursos, como servidores de contenido y servicios adicionales proporcionados por los distintos roles de sistema de sitio de Configuration Manager.  

-   Si no está familiarizado con lo que el esquema extendido proporciona a una implementación de Configuration Manager, puede informarse sobre las [Extensiones de esquema para System Center Configuration Manager](../../../core/plan-design/network/schema-extensions.md) para tomar esta decisión.  

-   Si no usa un esquema extendido, puede configurar otros métodos como DNS y WINS para ubicar los servicios y los servidores de sistema de sitio. Estos métodos de ubicación del servicio requieren configuraciones adicionales y no son el método preferido para la ubicación del servicio de los clientes. Para obtener más información al respecto, lea [Understand how clients find site resources and services for System Center Configuration Manager](../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md) (Comprender cómo los clientes buscan servicios y recursos de sitio para System Center Configuration Manager).  

-   Si su esquema de Active Directory se ha extendido para Configuration Manager 2007 o System Center 2012 Configuration Manager, no necesita hacer nada más. Las extensiones de esquema permanecen sin cambios y ya estarán en su lugar.  

La extensión del esquema es una acción que se realiza una sola vez para cada bosque. Para extender el esquema de Active Directory y después usar el esquema extendido, debe hacer lo siguiente:  

## <a name="step-1-extend-the-schema"></a>Paso 1. Extender el esquema  
Haga lo siguiente a fin de extender el esquema para Configuration Manager:  

-   Use una cuenta que pertenezca al grupo de seguridad Administradores de esquema.  

-   Inicie sesión en el controlador de dominio del maestro del esquema.  

-   Ejecute la herramienta **Extadsch.exe** o use la utilidad de línea de comandos LDIFDE con el archivo **ConfigMgr_ad_schema.ldf** . La herramienta y el archivo se encuentran en la carpeta **SMSSETUP\BIN\X64** en los medios de instalación de Configuration Manager.  

#### <a name="option-a-use-extadschexe"></a>Opción A: usar Extadsch.exe  

1.  Ejecute **extadsch.exe** para agregar las clases y los atributos nuevos al esquema de Active Directory.  

    > [!TIP]  
    >  Ejecute esta herramienta desde una línea de comandos para ver los comentarios mientras se ejecuta.  

2.  Compruebe que la extensión de esquema se realizó correctamente. Para ello, revise el archivo extadsch.log ubicado en la raíz de la unidad del sistema.  

#### <a name="option-b-use-the-ldif-file"></a>Opción B: usar el archivo LDIF  

1.  Edite el archivo **ConfigMgr_ad_schema.ldf** para definir el dominio raíz de Active Directory que desea extender:  

    -   Todas las instancias del texto **DC=x** del archivo deben reemplazarse por el nombre completo del dominio que se va a extender.  

    -   Por ejemplo, si el nombre completo del dominio que se va a extender es widgets.microsoft.com, cambie todas las instancias de DC=x del archivo a **DC=widgets, DC=microsoft, DC=com**.  

2.  Use la utilidad de línea de comandos LDIFDE para importar el contenido del archivo **ConfigMgr_ad_schema.ldf** en Servicios de dominio de Active Directory:  

    -   Por ejemplo, la siguiente línea de comandos importará las extensiones de esquema en Active Directory Domain Services, activará el registro detallado y creará un archivo de registro durante el proceso de importación: **ldifde -i -f ConfigMgr_ad_schema.ldf -v -j &lt;ubicación para almacenar el archivo de registro\>**  

3.  Para comprobar que la extensión del esquema se realizó correctamente, revise el archivo de registro creado por la línea de comandos usada en el paso anterior.  

## <a name="step-2--create-the-system-management-container-and-grant-sites-permissions-to-the-container"></a>Paso 2.  Crear el contenedor System Management y conceder permisos de sitios al contenedor  
 Después de extender el esquema, debe crear un contenedor denominado **System Management** en Active Directory Domain Services (AD DS):  

-   Debe crear este contenedor una vez en cada dominio que tenga un sitio primario o secundario que vaya a publicar datos en Active Directory.  

-   Para cada contenedor, conceda permisos a la cuenta de equipo de cada servidor de sitio primario y secundario que vaya a publicar datos de ese dominio. Cada cuenta necesita **Control total** en el contenedor con el permiso avanzado **Aplicar en** igual a **Este objeto y todos los descendientes**.  

#### <a name="to-add-the-container"></a>Para agregar el contenedor  

1.  Use una cuenta que tenga el permiso **Crear todos los objetos secundarios** en el contenedor **System** en Servicios de dominio de Active Directory.  

2.  Ejecute **ADSI Edit** (adsiedit.msc) y conéctese al dominio del servidor de sitio.  

3.  Cree el contenedor:  

    -   Expanda **Dominio** &lt;nombre de dominio completo del equipo\>, expanda &lt;nombre distintivo\>, haga clic con el botón derecho en **CN=System**, haga clic en **Nuevo** y, después, haga clic en **Objeto**.  

    -   En el cuadro de diálogo **Crear objeto** , seleccione **Contenedor**y, a continuación, haga clic en **Siguiente**.  

    -   En el cuadro **Valor** , escriba **System Management**y, a continuación, haga clic en **Siguiente**.  

4.  Asignar permisos:  

    > [!NOTE]  
    >  Si lo prefiere, puede utilizar otras herramientas como la herramienta administrativa Usuarios y equipos de Active Directory (dsa.msc) para agregar permisos al contenedor.  

    -   Haga clic con el botón secundario en **CN=System Management**y, a continuación, haga clic en **Propiedades**.  

    -   Seleccione la pestaña **Seguridad**, haga clic en **Agregar** y después agregue la cuenta de equipo del servidor de sitio con el permiso  
        **Control total** .  

    -   Haga clic en **Opciones avanzadas**, seleccione la cuenta de equipo del servidor de sitio y, después, haga clic en **Editar**.  

    -   En la lista **Aplicar en** , seleccione **Este objeto y todos los descendientes**.  

5.  Haga clic en **Aceptar** para cerrar la consola y guardar la configuración.  

## <a name="step-3-configure-sites-to-publish-to-active-directory-domain-services"></a>Paso 3. Configurar sitios para la publicación en Active Directory Domain Services  
 Después de configurar el contenedor, conceder los permisos e instalar un sitio primario de Configuration Manager, puede configurar el sitio para la publicación de datos en Active Directory.  

 Para obtener información sobre la publicación, consulte [Publish site data for System Center Configuration Manager](../../../core/servers/deploy/configure/publish-site-data.md) (Publicar datos de sitio para System Center Configuration Manager).  



<!--HONumber=Dec16_HO3-->


