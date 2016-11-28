---
title: "Preparar el almacenamiento en caché del mismo nivel de Windows PE para reducir el tráfico WAN | Configuration Manager"
description: "Almacenamiento en caché del mismo nivel de Windows PE funciona en Windows PE para obtener contenido de un elemento local de mismo nivel y minimizar el tráfico WAN cuando no hay ningún punto de distribución local."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 6c64f276-b88c-4b1e-8073-331876a03038
caps.latest.revision: 11
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: dc21868f99e17070b25c8b490e86477227a96c8e


---
# <a name="prepare-windows-pe-peer-cache-to-reduce-wan-traffic-in-system-center-configuration-manager"></a>Preparar el almacenamiento en caché del mismo nivel de Windows PE para reducir el tráfico WAN en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Al implementar un nuevo sistema operativo en System Center Configuration Manager, los equipos que ejecutan la secuencia de tareas pueden usar Almacenamiento en caché del mismo nivel de Windows PE para obtener contenido de un elemento local del mismo nivel (un origen de almacenamiento en caché del mismo nivel), en lugar de descargar el contenido de un punto de distribución. Esto ayuda a minimizar el tráfico de red de área extensa (WAN) en escenarios de sucursales donde no hay ningún punto de distribución local.  

 Almacenamiento en caché del mismo nivel en Windows PE es similar a [Windows BranchCache](http://technet.microsoft.com/library/mt617255\(TechNet.10\).aspx#bkmk_branchcache), pero funciona en el entorno de preinstalación de Windows (Windows PE). Si inicia la secuencia de tareas desde el contexto del sistema operativo, por ejemplo, desde el Centro de software en el cliente, no se usa Almacenamiento en caché del mismo nivel en Windows PE. Los siguientes términos se usan para describir a los clientes que usan Almacenamiento en caché del mismo nivel en Windows PE:  

-   Un **cliente de caché del mismo nivel** es un equipo que está configurado para usar Almacenamiento en caché del mismo nivel en Windows PE.  

-   Un **origen de caché del mismo nivel** es un cliente que está configurado para la caché del mismo nivel y que pone contenido a disposición de otros clientes de la caché del mismo nivel que lo solicitan.  

Use las siguientes secciones para administrar Almacenamiento en caché del mismo nivel.

##  <a name="a-namebkmkpeercacheobjectsa-objects-stored-on-a-peer-cache-source"></a><a name="BKMK_PeerCacheObjects"></a> Objetos almacenados en un origen de Almacenamiento en caché del mismo nivel  
 Una secuencia de tareas configurada para usar Almacenamiento en caché del mismo nivel en Windows PE puede obtener los siguientes objetos de contenido mientras se ejecuta en Windows PE:  

-   Imagen de sistema operativo  

-   Paquete de controladores  

-   Paquetes y programas (cuando el cliente continúa ejecutando la secuencia de tareas en el sistema operativo completo, el cliente obtiene este contenido desde un origen de la caché del mismo nivel si la secuencia de tareas se configuró originalmente para la caché del mismo nivel cuando se ejecuta en Windows PE).  

-   Imágenes de arranque adicionales  

 Los siguientes objetos de contenido nunca transfieren mediante almacenamiento en caché del mismo nivel. En su lugar, lo hacen desde un punto de distribución o mediante Windows BranchCache si configuró Windows BranchCache en su entorno:  

-   Aplicaciones  

-   Actualizaciones de software  

##  <a name="a-namebkmkpeercacheworka-how-does-windows-pe-peer-cache-work"></a><a name="BKMK_PeerCacheWork"></a> ¿Cómo funciona Almacenamiento en caché del mismo nivel en Windows PE?  
 Considere un escenario con una sucursal que no tiene ningún punto de distribución, pero sí varios clientes habilitados para usar Almacenamiento en caché del mismo nivel en Windows PE. Implemente la secuencia de tareas configurada para usar el almacenamiento en caché del mismo nivel en varios clientes configurados como parte del origen del almacenamiento en caché del mismo nivel. El primer cliente que ejecuta la secuencia de tareas emite una solicitud para un elemento del mismo nivel con el contenido. Si no encuentra uno, obtiene el contenido desde un punto de distribución a través de la WAN. El cliente instala la nueva imagen y, a continuación, almacena el contenido en su caché de cliente de Configuration Manager, por lo que puede funcionar como origen de caché del mismo nivel para otros clientes. Cuando el cliente siguiente ejecuta la secuencia de tareas, emite una solicitud en la subred para un origen de caché del mismo nivel. El primer cliente responde y pone a disposición su contenido almacenado en caché.  

##  <a name="a-namebkmkpeercachedeterminea-determine-what-clients-will-be-part-of-the-windows-pe-peer-cache-source"></a><a name="BKMK_PeerCacheDetermine"></a> Determinar qué clientes formarán parte del origen de Almacenamiento en caché del mismo nivel en Windows PE  
 Para ayudarle a determinar qué equipos seleccionar como origen de Almacenamiento en caché del mismo nivel en Windows PE, hay varios aspectos que debe considerar:  

-   El origen del Almacenamiento en caché del mismo nivel en Windows PE debe ser un equipo de escritorio que siempre esté encendido y disponible para los clientes de Almacenamiento en caché del mismo nivel.  

-   El Almacenamiento en caché del mismo nivel tiene un tamaño de caché de cliente suficiente para almacenar las imágenes.  

##  <a name="a-namebkmkpeercacherequirementsa-requirements-for-a-client-to-use-a-windows-pe-peer-cache-source"></a><a name="BKMK_PeerCacheRequirements"></a> Requisitos para que un cliente use un origen de Almacenamiento en caché del mismo nivel en Windows PE  
 Para que los clientes usen un origen de Almacenamiento en caché del mismo nivel en Windows PE, deben cumplir los siguientes requisitos:  

-   El cliente de Configuration Manager debe poder comunicarse a través de los siguientes puertos de la red:  

    -   Puerto para la difusión de red inicial para buscar un origen de caché del mismo nivel. De forma predeterminada, este puerto es 8004.  

    -   Puerto para el contenido que se descarga de un origen de caché del mismo nivel (HTTP y HTTPS). De forma predeterminada, este puerto es 8003.  

        > [!TIP]  
        >  Los clientes usarán HTTPS para descargar contenido cuando esté disponible. Sin embargo, se usará el mismo número de puerto para HTTP o HTTPS.  

-   [Configure the Client Cache for Configuration Manager Clients](../../core/clients/manage/manage-clients.md#BKMK_ClientCache) en los clientes para asegurarse de que tienen espacio suficiente para contener y almacenar las imágenes que implemente. Almacenamiento en caché del mismo nivel en Windows PE no afecta a la configuración o el comportamiento de la caché del cliente.  

-   Las opciones de implementación para la implementación de la secuencia de tareas deben configurarse como Descargar el contenido localmente cuando sea necesario mediante la ejecución de una secuencia de tareas.  

##  <a name="a-namebkmkpeercacheconfigurea-configure-windows-pe-peer-cache"></a><a name="BKMK_PeerCacheConfigure"></a> Configurar Almacenamiento en caché del mismo nivel en Windows PE  
 Puede usar los siguientes métodos para aprovisionar un cliente con contenido de la caché del mismo nivel, para que pueda servir como origen de caché del mismo nivel:  

-   Un cliente de caché del mismo nivel que no puede encontrar un origen de caché del mismo nivel con el contenido usará un punto de distribución para descargarlo.  Si el cliente recibe la configuración de cliente que habilita la memoria caché del mismo nivel y la secuencia de tareas está configurada para conservar el contenido almacenado en caché, el cliente se convierte en un origen de caché del mismo nivel.  

-   Un cliente de caché del mismo nivel puede obtener contenido de otro cliente de caché del mismo nivel (un origen de caché del mismo nivel).  Dado que el cliente está configurado para el almacenamiento en caché del mismo nivel, cuando ejecuta la secuencia de tareas que está configurada para conservar el contenido almacenado en caché, el cliente se convierte en un origen de caché del mismo nivel.  

-   Un cliente ejecuta una secuencia de tareas que incluye el paso opcional, [Download Package Content](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent), que se usa para preconfigurar el contenido relevante que se incluye en la secuencia de tareas Almacenamiento en caché del mismo nivel en Windows PE. Al usar este método:  

    -   El cliente no necesita instalar la imagen que se va a implementar.  

    -   Además de la opción **Descargar contenido de paquete** , la secuencia de tareas también debe usar la opción **Caché de cliente de Configuration Manager** . Usa esta opción para almacenar el contenido en la caché de los clientes, por lo que el cliente puede actuar como un origen de caché del mismo nivel para otros clientes de caché del mismo nivel.  

 Los procedimientos siguientes le ayudarán a configurar Almacenamiento en caché del mismo nivel en Windows PE en clientes y las secuencias de tareas que admiten el almacenamiento en caché del mismo nivel.  

### <a name="to-configure-the-windows-pe-peer-cache-source-computers"></a>Para configurar los equipos de origen de Almacenamiento en caché del mismo nivel en Windows PE  

1.  En la consola de Configuration Manager, vaya a **Administración** > **Configuración de cliente** y, después, cree una **Configuración de dispositivo de cliente personalizada** nueva o edite un objeto de configuración existente. También puede establecer esta configuración para el objeto **Configuración de cliente predeterminada** .  

    > [!TIP]  
    >  Use un objeto de configuración personalizada para administrar qué clientes deben recibir esta configuración. Por ejemplo, puede desear evitar establecer esta configuración en los equipos portátiles de los usuarios que se desplazan con frecuencia. Un sistema de alta movilidad puede ser un origen deficiente para proporcionar contenido a otros clientes de caché del mismo nivel.  
    >   
    >  Recuerde también que cuando se establece esta configuración como parte de la **Configuración de cliente predeterminada**, la configuración se aplica a todos los clientes de su entorno.  

2.  En **Almacenamiento en caché del mismo nivel en Windows PE**, establezca **Habilitar el cliente Administrador de configuración en el sistema operativo completo para compartir contenido** en **Sí**.  

    -   De forma predeterminada, solo está habilitado HTTP. Si desea que los clientes puedan descargar contenido a través de HTTPS, establezca **Enable HTTPS for client peer communication** en **Sí**.  

    -   De forma predeterminada, se establece el puerto para las difusiones en 8004 y el puerto para descargas de contenido en 8003, pero puede cambiar ambos ajustes.  

3.  Guarde e implemente la Configuración de cliente para los clientes que seleccionó para que fueran el origen del almacenamiento en caché del mismo nivel.  

 Después de aplicar este objeto de configuración a un objeto, el dispositivo está configurado para actuar como origen de caché del mismo nivel. Esta configuración debe implementarse en clientes potenciales de caché del mismo nivel para ajustar los protocolos y puertos necesarios.  

###  <a name="a-namebkmkpeercacheconfiguretsa-configure-a-task-sequence-for-windows-pe-peer-cache"></a><a name="BKMK_PeerCacheConfigureTS"></a> Configurar una secuencia de tareas para Almacenamiento en caché del mismo nivel en Windows PE  
 Al configurar la secuencia de tareas, use las siguientes variables de secuencia de tareas como Variables de la recopilación en la recopilación en la que se implementa la secuencia de tareas:  

-   **SMSTSPeerDownload**  

     Valor: TRUE  

     Esto permite al cliente usar Almacenamiento en caché del mismo nivel en Windows PE.  

-   **SMSTSPeerRequestPort**  

     Valor: <Número de puerto\>  

     Si no usa los puertos predeterminados configurados en Configuración de cliente (8004), debe configurar esta variable con un valor personalizado del puerto de red que se usará para la difusión inicial.  

-   **SMSTSPreserveContent**  

     Valor: TRUE  

     Esta variable marca la conservación del contenido de la secuencia de tareas en la memoria caché del cliente de Configuration Manager después de la implementación. Esta acción es diferente a usar SMSTSPersisContent, que solo conserva el contenido el tiempo que dure la secuencia de tareas y usa la memoria caché de la secuencia de tareas, no la memoria caché del cliente de Configuration Manager.  

 Para obtener más información, consulte [Task sequence built-in variables](../understand/task-sequence-built-in-variables.md) (Variables integradas de la secuencia de tareas).  

###  <a name="a-namebkmkpeercachevalidatea-validate-the-success-of-using-windows-pe-peer-cache"></a><a name="BKMK_PeerCacheValidate"></a> Validar el éxito del uso de Almacenamiento en caché del mismo nivel en Windows PE  
 Después de usar Almacenamiento en caché del mismo nivel en Windows PE para implementar e instalar una secuencia de tareas, puede confirmar que ese almacenamiento en caché del mismo nivel se empleó correctamente en el proceso observando el **smsts.log** en el cliente que ejecutó la secuencia de tareas.  

 En el registro, busque una entrada similar a la siguiente, donde <*NombreServidorOrigen*> identifica el equipo desde el que el cliente obtuvo el contenido. Este equipo debe ser un origen de caché del mismo nivel y no un servidor de punto de distribución. Otros detalles varían en función de su entorno local y sus configuraciones.  

-   *<![LOG[Downloaded file from http:// <NombreServidorOrigen\>:8003/SCCM_BranchCache$/SS10000C/sccm?/install.wim to C:\\_SMSTaskSequence\Packages\SS10000C\install.wim ]LOG]!><time="14:24:33.329+420" date="06-26-2015" component="ApplyOperatingSystem" context="" type="1" thread="1256" file="downloadcontent.cpp:1626">*  



<!--HONumber=Nov16_HO1-->


