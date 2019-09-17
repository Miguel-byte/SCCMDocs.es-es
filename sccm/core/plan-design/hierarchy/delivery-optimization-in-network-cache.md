---
title: Servidor de caché en la red de optimización de distribución
titleSuffix: Configuration Manager
description: Uso del punto de distribución de Configuration Manager como servidor de caché local para la Optimización de distribución
ms.date: 09/10/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: c5cb5753-5728-4f81-b830-a6fd1a3e105c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 070f7ec6f99a9de89c155e756989fb3b5fa4a594
ms.sourcegitcommit: 05a984cf94ea43c392701a389c4eb20bd692847c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/12/2019
ms.locfileid: "70922737"
---
# <a name="delivery-optimization-in-network-cache-in-configuration-manager"></a>Servidor de caché en la red de Optimización de distribución en Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

<!--3555764-->

A partir de la versión 1906, puede instalar un servidor de caché en la red de Optimización de distribución (DOINC) en los puntos de distribución. Al almacenar en caché este contenido de forma local, los clientes pueden beneficiarse de la característica de Optimización de entrega y, además, puede ayudar a proteger los vínculos WAN.

Este servidor de caché actúa como una caché transparente a petición para el contenido descargado mediante la Optimización de entrega. Use la configuración de cliente para asegurarse de que este servidor se ofrezca únicamente a los miembros del grupo de límites de Configuration Manager local.

Esta caché es independiente del contenido del punto de distribución de Configuration Manager. Si elige la misma unidad que el rol de punto de distribución, el contenido se almacenará por separado.

> [!Note]  
> El servidor de caché en la red de optimización de distribución es una aplicación instalada en Windows Server que todavía está en desarrollo. Está marcado con una etiqueta *beta* en la consola de Configuration Manager.  


## <a name="how-it-works"></a>Cómo funciona

Cuando configura los clientes para que usen el servidor de caché en la red de Optimización de distribución, ya no necesitan solicitar contenido administrado por Microsoft Cloud desde Internet. Los clientes solicitan este contenido del servidor de DOINC instalado en el punto de distribución. El servidor de DOINC almacena en caché este contenido mediante la característica de IIS para el Enrutamiento de solicitud de aplicaciones (ARR). Después, el servidor de caché puede responder rápidamente a las solicitudes futuras del mismo contenido. Si el servidor de DOINC no está disponible o el contenido todavía no está almacenado en caché, los clientes descargan el contenido de Internet. Los clientes también usan la Optimización de distribución, por lo que debe descargar partes del contenido de los elementos del mismo nivel en su red.

![Diagrama del funcionamiento de DOINC](media/3555764-delivery-optimization-in-network-cache.png)

1. El cliente comprueba si hay actualizaciones y obtiene la dirección de la red de entrega de contenido (CDN).

2. Configuration Manager configura las opciones de la Optimización de distribución (DO) en el cliente, incluido el nombre del servidor de caché.

3. El cliente A solicita el contenido del servidor de caché de Optimización de distribución.

4. Si la caché no incluye el contenido, el servidor de caché de Optimización de distribución lo obtiene de la red CDN.

5. Si el servidor de caché no responde, el cliente descarga el contenido de la red CDN.

6. Los clientes utilizan la Optimización de distribución para obtener fragmentos del contenido de los elementos del mismo nivel.


## <a name="prerequisites-and-limitations"></a>Requisitos previos y limitaciones

- Un punto de distribución *local*, con las siguientes configuraciones:

    - Ejecución de Windows Server 2012, Windows Server 2012 R2, Windows Server 2016 o Windows Server 2019

    - Sitio web predeterminado habilitado en el puerto 80

    - No preinstale la característica [Enrutamiento de solicitud de aplicaciones](https://docs.microsoft.com/iis/extensions/planning-for-arr/application-request-routing-version-2-overview) (ARR). DOINC instala ARR y configura sus valores. Microsoft no puede garantizar que la configuración de ARR de DOINC no entre en conflicto con otras aplicaciones del servidor que también usan esta característica.

    - El punto de distribución requiere acceso a la nube de Microsoft a través de Internet. Las direcciones URL concretas pueden variar según el contenido específico habilitado para la nube. Para más información, consulte los [requisitos de acceso a Internet](/sccm/core/plan-design/network/internet-endpoints).

- Clientes que ejecutan Windows 10 versión 1709 y posteriores


## <a name="enable-doinc"></a>Habilitar DOINC

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración** y seleccione el nodo **Puntos de distribución**.

1. Seleccione un punto de distribución local y, a continuación, en la cinta de opciones, seleccione **Propiedades**.

1. En las propiedades del rol de punto de distribución, en la pestaña **General**, configure las opciones siguientes:  

    1. Active la opción **Habilitar este punto de distribución para usarlo como servidor de caché en la red de optimización de distribución**.  

        Lea y acepte los términos de licencia.

    2. **Unidad local que se usará**: seleccione el disco que se usará para la memoria caché. El valor predeterminado es **Automático**, que usa el disco con más espacio libre.<sup>[Nota 1](#bkmk_note1)</sup>  

        > [!Note]  
        > Puede cambiar esta unidad más adelante. Se pierde todo el contenido almacenado en caché, a menos que lo copie en la nueva unidad.

    3. **Espacio en disco**: seleccione la cantidad de espacio en disco que se va a reservar en GB o un porcentaje del espacio en disco total. De forma predeterminada, este valor es 100 GB.

        > [!Note]  
        > El tamaño de caché predeterminado debe ser suficiente para la mayoría de los clientes. Puede ajustar el tamaño de la memoria caché más adelante.

    4. **Conservar la caché al deshabilitar el servidor de caché en la red**: si quita el servidor de caché y habilita esta opción, el servidor mantiene el contenido de la caché en el disco.  

1. En la configuración de cliente, en el grupo **Optimización de distribución**, configure el valor **Permita que los dispositivos administrados por Configuration Manager usen servidores de caché en la red de optimización de distribución (Beta) para la descarga de contenido**.  

### <a name="bkmk_note1"></a> Nota 1: Acerca de la selección de unidades

Si selecciona **Automático**, cuando Configuration Manager instala el componente DOINC, respeta el archivo **no_sms_on_drive.sms**. Por ejemplo, el punto de distribución tiene el archivo `C:\no_sms_on_drive.sms`. Incluso si la unidad C: es la que tiene más espacio disponible, Configuration Manager configura DOINC para usar otra unidad para su caché.

Si selecciona una unidad específica que ya tenga el archivo **no_sms_on_drive.sms**, Configuration Manager ignora el archivo. La configuración de DOINC para usar esa unidad es una intención explícita. Por ejemplo, el punto de distribución tiene el archivo `F:\no_sms_on_drive.sms`. Cuando se configuran explícitamente las propiedades del punto de distribución para usar la unidad **F:**, Configuration Manager configura DOINC para que use la unidad F: para su memoria caché.

Para cambiar la unidad después de instalar DOINC:

- Configure manualmente las propiedades del punto de distribución para usar una letra de unidad específica.

- Si se establece en Automático, cree primero el archivo **no_sms_on_drive.sms**. Después, realice algún cambio en las propiedades del punto de distribución para desencadenar un cambio de configuración.

## <a name="verify"></a>Comprobar

Cuando los clientes descargan contenido administrado en la nube, usan la Optimización de distribución del servidor de caché instalado en el punto de distribución. El contenido administrado en la nube incluye los tipos siguientes:

- Aplicaciones de Microsoft Store
- Características de Windows a petición, como idiomas
- Si habilita [directivas de Windows Update para empresas](/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10): actualizaciones de características y de calidad de Windows 10
- Para las [cargas de trabajo de administración conjunta](/sccm/comanage/workloads):
    - Windows Update para empresas: actualizaciones de características y de calidad de Windows 10
    - Aplicaciones de Office Hacer clic y ejecutar: aplicaciones y actualizaciones de Office
    - Aplicaciones cliente: aplicaciones y actualizaciones de Microsoft Store
    - Endpoint Protection: actualizaciones de definiciones de Windows Defender

En Windows 10 versión 1809 o posteriores, compruebe este comportamiento con el cmdlet **Get-DeliveryOptimizationStatus** de Windows PowerShell. En la salida del cmdlet, revise el valor **BytesFromCacheServer**. Para más información, vea [Supervisar la optimización de distribución](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization-setup#monitor-delivery-optimization).

Si el servidor de caché devuelve algún error HTTP, el cliente de Optimización de distribución recurre al origen inicial en la nube.

Para obtener información detallada, vea [Solución de problemas de la caché en la red de optimización de distribución en Configuration Manager](/sccm/core/servers/deploy/configure/troubleshoot-delivery-optimization-in-network-cache).

## <a name="see-also"></a>Consulte también

[Optimización de la distribución de actualizaciones de Windows 10 con Configuration Manager](/sccm/sum/deploy-use/optimize-windows-10-update-delivery)

[Solución de problemas de la caché en la red de optimización de distribución en Configuration Manager](/sccm/core/servers/deploy/configure/troubleshoot-delivery-optimization-in-network-cache)
