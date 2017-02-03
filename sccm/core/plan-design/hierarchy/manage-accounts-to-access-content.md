---
title: Cuentas para acceder al contenido | Microsoft Docs
description: "Obtenga información acerca de las cuentas donde los clientes obtienen acceso a contenido de System Center Configuration Manager."
ms.custom: na
ms.date: 1/4/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a7df9d0f-fbde-47eb-97e7-3d29536424fa
caps.latest.revision: 4
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 4d34a272a93100426cccd2308c5b3b0b0ae94a60
ms.openlocfilehash: ee83aa6fdbd1a82384a4684055ed72620a3f474e

---
# <a name="manage-accounts-to-access-content-in-system-center-configuration-manager"></a>Administración de cuentas para acceder al contenido en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Antes de implementar el contenido en System Center Configuration Manager, tómese un tiempo para pensar en cómo tendrán acceso los clientes a dicho contenido desde los puntos de distribución.  

-   **Cuenta de acceso a la red** : la usan los clientes para conectarse a un punto de distribución y acceder al contenido. De forma predeterminada, los clientes primero probarán con su cuenta de equipo.  

     Esta cuenta también la usan los puntos de distribución de extracción para obtener el contenido de un punto de distribución de origen en un bosque remoto.  

-   **Cuenta de acceso de paquete**: de manera predeterminada, Configuration Manager concede acceso al contenido en un punto de distribución a las cuentas integradas denominadas **Usuarios** y **Administradores**. Puede configurar permisos adicionales para restringir el acceso.  

-   **Cuenta de conexión de multidifusión** : se usa para implementaciones de sistema operativo.  

##  <a name="a-namebkmknaaa-network-access-account"></a><a name="bkmk_NAA"></a> Cuenta de acceso a la red  
 Los equipos cliente usan la cuenta de acceso de red cuando no pueden usar su cuenta de equipo local para acceder al contenido en los puntos de distribución. Esto se aplica, por ejemplo, a equipos y clientes del área de trabajo de dominios que no son de confianza. Esta cuenta también se puede utilizar durante la implementación de un sistema operativo cuando el equipo que instala el sistema operativo no tiene aún una cuenta de equipo en el dominio.  

-   Los clientes solo usan la cuenta de acceso a la red para tener acceso a recursos de la red.  

-   Puede configurar varias cuentas para su uso como una cuenta de acceso a la red en cada sitio primario.  

-   Los clientes intentan primero tener acceso al contenido de un punto de distribución mediante su cuenta *nombreDeEquipo*. Si se produce un error en esta cuenta, intentan usar una cuenta de acceso a la red. A continuación, los clientes siguen intentando usar la cuenta de acceso a la red, incluso si antes generó un error.  

**Permisos**: conceda a esta cuenta los permisos adecuados mínimos para tener acceso al software en busca del contenido que requiere el cliente.  

-   La cuenta debe tener el permiso **Tener acceso a este equipo desde la red** en el punto de distribución.  

-   Cree la cuenta en cualquier dominio que proporcione el acceso necesario a los recursos. La cuenta de acceso de red debe incluir siempre un nombre de dominio. No se admite la seguridad de paso a través para esta cuenta. Si tiene puntos de distribución en varios dominios, cree la cuenta en un dominio de confianza.  

> [!TIP]  
>  Para evitar bloqueos de cuentas, no cambie la contraseña de una cuenta de acceso de red existente. En su lugar, cree una cuenta nueva y configúrela en Configuration Manager. Cuando transcurra el tiempo suficiente para que todos los clientes reciban los detalles de la cuenta nueva, quite la cuenta antigua de las carpetas compartidas de red y elimine la cuenta.  

> [!IMPORTANT]  
>  No conceda a esta cuenta derechos de inicio de sesión interactivo.  
>   
>  No conceda a esta cuenta el derecho de unir equipos al dominio. Si debe unir equipos al dominio durante una secuencia de tareas, utilice la cuenta de unión al dominio del editor de secuencia de tareas.  

### <a name="to-configure-the-network-access-account"></a>Para configurar la cuenta de acceso de red  

1.  En la consola de Configuration Manager, haga clic en **Administración** >   **Configuración del sitio** >  **Sitios** y seleccione el sitio.  

2.  En el grupo **Configuración** , haga clic en **Configurar componentes de sitio** > **Distribución de software**.  

3.  Haga clic en la ficha **Cuenta de acceso de red** . Configure una o más cuentas y después haga clic en **Aceptar**.  

##  <a name="a-namebkmkpaaa-package-access-accounts"></a><a name="bkmk_Paa"></a> Cuentas de acceso de paquetes  
 Las cuentas de acceso de paquete le permiten establecer permisos del sistema de archivos NTFS para especificar los usuarios y los grupos de usuarios que pueden acceder al contenido del paquete en puntos de distribución. De forma predeterminada, Configuration Manager solo concede acceso a las cuentas genéricas **Usuarios** y **Administradores**, aunque puede controlar el acceso de los equipos cliente mediante el empleo de otras cuentas o grupos de Windows. Los dispositivos móviles siempre recuperan el contenido del paquete de forma anónima, por lo que no utilizan cuentas de acceso de paquete.  

 De forma predeterminada, cuando Configuration Manager copia los archivos de contenido de un paquete en un punto de distribución, este concede acceso de **Lectura** al grupo local **Usuarios** y **Control total** al grupo de **Administradores** local. Los permisos reales que se requieren dependen del paquete. Si tiene clientes en grupos de trabajo o en bosques que no son de confianza, estos clientes utilizan la cuenta de acceso de red para acceder al contenido del paquete. Asegúrese de que la cuenta de acceso de red tiene permisos para acceder al paquete mediante el uso de las cuentas de acceso de paquete definidas.  

 Utilice las cuentas en un dominio que pueda acceder a los puntos de distribución. Si crea o modifica la cuenta después de que se cree el paquete, deberá redistribuirlo. La actualización del paquete no modifica los permisos del sistema de archivos NTFS en el paquete.  

 No es necesario que agregue la cuenta de acceso de red como una cuenta de acceso de paquete, ya que la pertenencia al grupo **Usuarios** la agrega automáticamente. Restringir la cuenta de acceso de paquetes a solo la cuenta de acceso a la red no impide que los clientes accedan al paquete.  

### <a name="to-manage-access-accounts"></a>Para administrar cuentas de acceso  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

2.  En el área de trabajo **Biblioteca de software** , seleccione uno de los siguientes pasos para el tipo de contenido para el que desea administrar cuentas de acceso:  

    -   **Aplicaciones**: expanda **Administración de aplicaciones**, haga clic en **Aplicaciones**y, a continuación, seleccione las aplicaciones para las que desea administrar cuentas de acceso.  

    -   **Paquetes**: expanda **Administración de aplicaciones**, haga clic en **Paquetes**y, a continuación, seleccione los paquetes para los que desea administrar cuentas de acceso.  

    -   **Paquetes de implementación**: expanda **Actualizaciones de software**, haga clic en **Paquetes de implementación**y, a continuación, seleccione los paquetes de implementación para los que desea administrar cuentas de acceso.  

    -   **Paquetes de controladores**: expanda **Sistemas operativos**, haga clic en **Paquetes de controladores**y, a continuación, seleccione los paquetes de controladores para los que desea administrar cuentas de acceso.  

    -   **Imágenes de sistema operativo**: expanda **Sistemas operativos**, haga clic en **Imágenes de sistema operativo**y, a continuación, seleccione las imágenes de sistema operativo para que las que desea administrar cuentas de acceso.  

    -   **Instaladores de sistema operativo**: expanda **Sistemas operativos**, haga clic en **Instaladores de sistema operativo**y, a continuación, seleccione los instaladores de sistema operativo para que los que desea administrar cuentas de acceso.  

    -   **Imágenes de arranque**: expanda **Sistemas operativos**, haga clic en **Imágenes de arranque**y, a continuación, seleccione las imágenes de arranque para las que desea administrar cuentas de acceso.  

3.  Haga clic con el botón secundario en el objeto seleccionado y, a continuación, haga clic en **Administrar cuentas de acceso**.  

4.  En el cuadro de diálogo **Agregar cuenta** , especifique el tipo de cuenta al que se le concederá acceso al contenido y, a continuación, especifique los derechos de acceso asociados a la cuenta.  

    > [!NOTE]  
    >  Cuando se agrega un nombre de usuario para la cuenta y Configuration Manager encuentra una cuenta de usuario local y una cuenta de usuario de dominio con ese nombre, Configuration Manager establece derechos de acceso para la cuenta de usuario de dominio.  

##  <a name="a-namebkmkmultia-multicast-connection-account"></a><a name="bkmk_multi"></a> Cuenta de conexión de multidifusión  
 Los puntos de distribución, que están configurados para multidifusión, utilizan la cuenta de conexión de multidifusión para leer información en la base de datos del sitio.  

-   Especifique la cuenta que se debe usar al configurar conexiones de base de datos del administrador de configuración para la multidifusión.  

-   De forma predeterminada, se usa la cuenta de equipo del punto de distribución, pero puede configurar una cuenta de usuario en su lugar.  

-   Debe especificar una cuenta de usuario cada vez que la base de datos del sitio esté en un bosque que no sea de confianza.  

-   La cuenta debe tener permisos de **Lectura** para la base de datos del sitio.  

Por ejemplo, si el centro de datos tiene una red perimetral en un bosque que no sea ni el servidor del sitio ni la base de datos del sitio, puede utilizar esta cuenta para leer información de multidifusión desde la base de datos del sitio.  
Si crea esta cuenta, créela como una cuenta local con derechos reducidos en el equipo que ejecuta Microsoft SQL Server.  

> [!IMPORTANT]  
>  No conceda a esta cuenta derechos de inicio de sesión interactivo.  



<!--HONumber=Jan17_HO1-->


