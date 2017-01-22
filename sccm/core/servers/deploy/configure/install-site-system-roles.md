---
title: Instalar roles del sistema de sitio | Microsoft Docs
description: Los asistentes le ayudan a agregar roles de sistema de sitio en un servidor de sistema de sitio nuevo o existente en el sitio.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 61f5c774-7667-44ae-b8e4-a4951318b183
caps.latest.revision: 4
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: 9c930db61139fd089554591f4ca0aa2271fb2289

---
# <a name="install-site-system-roles-for-system-center-configuration-manager"></a>Instalación de roles de sistema de sitio para System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

La consola de System Center Configuration Manager tiene dos asistentes que puede usar para instalar roles de sistema de sitio:  

-   **Asistente para agregar roles de sistema de sitio**: utilice este asistente para agregar roles de sistema de sitio en un servidor de sistema de sitio existente en el sitio.  

-   **Asistente para crear servidor de sistema de sitio**: utilice este asistente para especificar un nuevo servidor como servidor de sistema de sitio y, a continuación, instale uno o varios roles de sistema de sitio en el servidor. Este asistente es el mismo que el **Asistente para agregar roles de sistema de sitio**, excepto que, en la primera página, debe especificar el nombre del servidor para usar y el sitio en que desee instalarlo.  

Cuando instala un rol de sistema de sitio en un equipo remoto (incluida una instancia del proveedor de SMS), la cuenta de equipo del equipo remoto se agrega a un grupo local en el servidor de sitio. Cuando el sitio se instala en un controlador de dominio, el grupo en el servidor de sitio es un grupo de dominio en lugar de un grupo local, y el rol de sistema de sitio remoto no está operativo hasta que se reinicie el equipo del rol de sistema de sitio o se actualice el vale Kerberos para la cuenta de equipos remotos [Cuentas usadas en System Center Configuration Manager](../../../../core/plan-design/hierarchy/accounts.md).  

Justo antes de instalar el rol de sistema de sitio, Configuration Manager comprueba el equipo de destino para asegurarse de que cumple los requisitos previos para los roles de sistema de sitio seleccionados. Al instalar roles de sistema de sitio:  

-   De manera predeterminada, cuando Configuration Manager instala un rol de sistema de sitio, los archivos de instalación se instalan en la primera unidad de disco con formato NTFS disponible que tenga el mayor espacio disponible en disco. Para evitar que Configuration Manager se instale en unidades concretas, cree un archivo vacío denominado **no_sms_on_drive.sms** y cópielo en la carpeta raíz de la unidad antes de instalar el servidor de sistema de sitio.  

-   Configuration Manager usa la **cuenta de instalación del sistema de sitio** para instalar roles de sistemas del sitio. Esta cuenta se especifica cuando se ejecuta el asistente aplicable para crear un nuevo servidor de sistemas del sitio o agregar roles de sistema del sitio a un servidor de sistema de sitio existente. De forma predeterminada, esta cuenta es la cuenta del sistema local del equipo del servidor del sitio, pero puede especificar una cuenta de usuario de dominio para su uso como cuenta de instalación del sistema del sitio. Para obtener más información, consulte la cuenta de instalación del sistema de sitio en el tema [Cuentas usadas en System Center Configuration Manager](../../../../core/plan-design/hierarchy/accounts.md).  

##  <a name="a-namebkmkinstalla-to-install-site-system-roles-on-an-existing-site-system-server"></a><a name="bkmk_Install"></a> Para instalar roles de sistema de sitio en un servidor de sistema de sitio existente  

1.  En la consola de Configuration Manager, haga clic en **Administración**.  

2.  En el área de trabajo **Administración** , expanda **Configuración del sitio**, haga clic en **Servidores y roles del sistema de sitios**y, a continuación, seleccione el servidor que desee usar para los nuevos roles de sistema de sitio.  

3.  En la pestaña **Inicio** , en el grupo **Servidor** , haga clic en **Agregar roles del sistema de sitio**.  

4.  En la página **General** , revise la configuración y, a continuación, haga clic en **Siguiente**.  

    > [!TIP]  
    >  Para tener acceso al rol de sistema de sitio desde Internet, asegúrese de especificar un FQDN de Internet.  

5.  En la página **Proxy** , especifique la configuración de un servidor proxy si los roles de sistema de sitio que se ejecutan en ese servidor de sistema de sitio requieren un servidor proxy para conectarse a ubicaciones en Internet y, a continuación, haga clic en **Siguiente**.  

6.  En la página **Selección de rol del sistema** , seleccione los roles de sistema de sitio que desee agregar y, a continuación, haga clic en **Siguiente**.  

7.  Complete el asistente.  

> [!TIP]  
>  El cmdlet de Windows PowerShell, New-CMSiteSystemServer, realiza la misma función que este procedimiento. Para obtener más información, consulte [New-CMSiteSystemServer](http://go.microsoft.com/fwlink/p/?LinkID=271414) en la documentación de referencia del cmdlet de Microsoft System Center 2012 Configuration Manager SP1.  

## <a name="to-install-site-system-roles-on-a-new-site-system-server"></a>Para instalar roles de sistema de sitio en un servidor de sistema de sitio nuevo  

1.  En la consola de Configuration Manager, haga clic en **Administración**.  

2.  En el área de trabajo **Administración** , expanda **Configuración del sitio**y, a continuación, haga clic en **Servidores y roles del sistema de sitios**.  

3.  en la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear servidor del sistema de sitio**.  

4.  En la página **General** , especifique la configuración general del sistema de sitio y, a continuación, haga clic en **Siguiente**.  

    > [!TIP]  
    >  Para tener acceso al nuevo rol de sistema de sitio desde Internet, asegúrese de especificar un FQDN de Internet.  

5.  En la página **Proxy** , especifique la configuración de un servidor proxy si los roles de sistema de sitio que se ejecutan en ese servidor de sistema de sitio requieren un servidor proxy para conectarse a ubicaciones en Internet y, a continuación, haga clic en **Siguiente**.  

6.  En la página **Selección de rol del sistema** , seleccione los roles de sistema de sitio que desee agregar y, a continuación, haga clic en **Siguiente**.  

7.  Complete el asistente.  

> [!TIP]  
>  El cmdlet de Windows PowerShell, New-CMSiteSystemServer, realiza la misma función que este procedimiento. Para obtener más información, consulte [New-CMSiteSystemServer](http://go.microsoft.com/fwlink/p/?LinkID=271414) en la documentación de referencia del cmdlet de Microsoft System Center 2012 Configuration Manager SP1.  



<!--HONumber=Dec16_HO3-->


