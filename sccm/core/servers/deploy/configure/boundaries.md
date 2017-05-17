---
title: "Definición de límites | Microsoft Docs"
description: "Obtenga información sobre cómo definir ubicaciones de red de la intranet que pueden contener los dispositivos que quiere administrar."
ms.custom: na
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 4a9dc4d9-e114-42ec-ae2b-73bee14ab04f
caps.latest.revision: 10
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: bed70809008fde5e2b0215f4dce049402edf83ba
ms.contentlocale: es-es
ms.lasthandoff: 05/17/2017


---
# <a name="define-network-locations-as-boundaries-for-system-center-configuration-manager"></a>Definición de las ubicaciones de red como límites para System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Los límites de Configuration Manager son ubicaciones de red que contienen dispositivos que desea administrar. El límite en que un dispositivo se encuentra es equivalente al sitio de Active Directory, o bien la dirección IP de red identificada por el cliente de Configuratoin Manager que está instalado en el dispositivo.
 - Puede crear límites independientes manualmente. No obstante, Configuration Manager no es compatible con la entrada directa de una superred como un límite. En su lugar, utilice el tipo de límite de intervalo de direcciones IP.
 - Puede configurar el método de [detección de bosques de Active Directory](../../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutForest) para que detecte automáticamente y cree límites para las subredes IP y el sitio de Active Directory que detecta. Cuando la detección de bosques de Active Directory identifica una superred asignada a un sitio de Active Directory, Configuration Manager convierte la superred en un límite de intervalo de direcciones IP.  

No es raro que un dispositivo use una dirección IP de la que el administrador de Configuration Manager no tiene constancia. Si tiene dudas sobre la ubicación de red de un dispositivo, confirme lo que el dispositivo notifica como su ubicación mediante el comando **IPCONFIG** en el dispositivo.  

Al crear un límite, este recibe automáticamente un nombre basado en el tipo y ámbito del límite. No se puede modificar este nombre. En su lugar, puede especificar una descripción que ayude a identificar el límite en la consola de Configuration Manager.  

Cada límite está disponible para que lo use cada sitio de la jerarquía. Después de haber creado un límite, puede modificar sus propiedades para hacer lo siguiente:  
-   Agregar el límite a uno o varios grupos de límites.  
-   Cambiar el tipo o el ámbito del límite.  
-   Ver la pestaña **Sistemas de sitio** del límite para ver qué servidores de sistema de sitio (puntos de distribución, puntos de migración de estado y puntos de administración) están asociados con el límite.  

## <a name="to-create-a-boundary"></a>Para crear un límite  

1.  En la consola de Configuration Manager, haga clic en **Administración** > **Configuración de jerarquía** > **Límites**.  

2.  En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear Boundary.**.  

3.  En la pestaña **General** del cuadro de diálogo Crear límite, puede especificar una **Descripción** para identificar el límite con un nombre o referencia fácil de reconocer.  

4.  Seleccione un **Tipo** para este límite:  

    -   Si selecciona **Subred de IP**, debe especificar un **Id. de subred** para este límite.  
        > [!TIP]  
        >  Puede especificar la **Red** y la **Máscara de subred** para que el **Id. de subred** se especifique automáticamente. Cuando se guarda el límite, se guarda solo el valor de Id. de subred.  

    -   Si selecciona **Sitio de Active Directory**, debe especificarlo o **Examinar** para buscar un sitio de Active Directory en el bosque local del servidor de sitio.  

        > [!IMPORTANT]  
        >  Cuando se especifica un sitio de Active Directory para un límite, el límite incluye cada subred de IP que sea miembro de ese sitio de Active Directory. Si cambia la configuración del sitio de Active Directory en Active Directory, también cambiarán las ubicaciones de red incluidas en este límite.  

    -   Si selecciona **Prefijo IPv6**, debe especificar un **Prefijo** en el formato de prefijo IPv6.  

    -   Si selecciona **Intervalo de direcciones IP**, debe especificar una **Dirección IP inicial** y una **Dirección IP final** que incluya parte de una subred de IP o que incluya múltiples subredes de IP.    

5.  Haga clic en **Aceptar** para guardar el nuevo límite.  

## <a name="to-configure-a-boundary"></a>Para configurar un límite  

1.  En la consola de Configuration Manager, haga clic en **Administración** > **Configuración de jerarquía** > **Límites**.  

2.  Seleccione el límite que desea modificar.  

3.  En la pestaña **Inicio** , en el grupo **Propiedades** , haga clic en **Propiedades**.  

4.  En el cuadro de diálogo **Propiedades** para el límite, seleccione la pestaña **General** para editar la **Descripción** o el **Tipo** para el límite. También puede cambiar el ámbito de un límite mediante la edición de las ubicaciones de red para el límite. Por ejemplo, para un límite de sitio de Active Directory, puede especificar un nuevo nombre de sitio de Active Directory.  

5.  Seleccione la pestaña **Sistemas de sitio** para ver los sistemas de sitio que están asociados con este límite. No puede cambiar esta configuración desde las propiedades de un límite.  

    > [!TIP]  
    >  Para que un servidor de sistema de sitio se muestre como sistema de sitio para un límite, el servidor de sistema de sitio debe estar asociado como servidor de sistema de sitio para, al menos, un grupo de límites que incluya este límite. Esto se configura en la pestaña **Referencias** de un grupo de límites.  

6.  Seleccione la pestaña **Grupos de límites** para modificar la pertenencia al grupo de límites de este límite:  

    -   Para agregar este límite a uno o más grupos de límites, haga clic en **Agregar**, seleccione la casilla para uno o más grupos de límites y, a continuación, haga clic en **Aceptar**.  

    -   Para quitar este límite de un grupo de límites, seleccione el grupo de límites y haga clic en **Quitar**.  

7.  Haga clic en **Aceptar** para cerrar las propiedades de límite y guardar la configuración.  

