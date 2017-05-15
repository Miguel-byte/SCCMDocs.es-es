---
title: Administrar aplicaciones iOS compradas por volumen | Microsoft Docs
description: Implemente, administre y supervise licencias para las aplicaciones que ha adquirido mediante el App Store de iOS.
ms.custom: na
ms.date: 05/03/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7c3b9316-247b-490b-a363-8f8553821579
caps.latest.revision: 18
caps.handback.revision: 0
author: mtillman
ms.author: mtillman
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: c6a6137fa978e1ea28aefea2aea4e29ba661efd6
ms.openlocfilehash: 55f1204b088a7b636a90561f20aa41c7de72bc05
ms.contentlocale: es-es
ms.lasthandoff: 05/04/2017

---
# <a name="manage-volume-purchased-ios-apps-with-system-center-configuration-manager"></a>Administrar aplicaciones de iOS compradas por volumen con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*



 El App Store de iOS le permite comprar varias licencias de una aplicación que quiere ejecutar en su empresa. Esto ayuda a reducir la carga administrativa relacionada con el seguimiento de varias copias de las aplicaciones que ha comprado.  

 System Center Configuration Manager le ayuda a implementar y administrar aplicaciones iOS que ha adquirido a través del programa mediante la importación de la información de licencia desde el App Store y la supervisión de la cantidad de licencias que se van a usar.  

## <a name="manage-volume-purchased-apps-for-ios-devices"></a>Administrar aplicaciones compradas por volumen para dispositivos iOS  
 Puede comprar varias licencias para aplicaciones iOS a través del Programa de Compras por Volumen (PCV) de Apple. Esto implica configurar una cuenta de PCV de Apple en el sitio web de Apple y cargar el token de PCV de Apple en Configuration Manager, que proporciona las siguientes características:  

-   Sincronice la información de la compra por volumen con Configuration Manager. 
 
- Sincronice aplicaciones desde el Programa de compras por volumen de Apple para Empresas y el Programa de compras por volumen de Apple para educación.

- Asocie varios tokens del Programa de compras por volumen de Apple con Configuration Manager.

-   Las aplicaciones que ha comprado se muestran en la consola de Configuration Manager.  

-   Puede implementar y supervisar estas aplicaciones, y también realizar un seguimiento del número de licencias para cada aplicación que se ha usado.  

-   Configuration Manager puede ayudarle a recuperar licencias cuando sea necesario mediante la desinstalación de aplicaciones compradas por volumen que haya implementado.  

## <a name="before-you-start"></a>Antes de empezar  
 Antes de empezar, es necesario obtener un token de PCV de Apple y cargarlo en Configuration Manager.  

-   Si ha usado anteriormente un token de PCV con un producto MDM diferente en su cuenta de PCV de Apple existente, debe generar un nuevo token para usarlo con Configuration Manager.  
-   La validez de cada token es de un año.  
-   De manera predeterminada, Configuration Manager se sincroniza con el servicio PCV de Apple dos veces al día para garantizar que las licencias estén sincronizadas con Configuration Manager.  
      Solo se sincronizan los cambios en las licencias. Pero, una vez cada siete días, se realiza una sincronización completa.  
      Cuando pulse **Sincronizar** para realizar una sincronización manual, siempre se realizará una sincronización completa.  
-   Si necesita recuperar o restaurar la base de datos de Configuration Manager, se recomienda que realice una sincronización manual posteriormente para garantizar que los datos de licencia sincronizados estén actualizados.  
-   Además, debe haber importado un certificado válido de Apple Push Notification Service (APNs) de Apple que le permita administrar dispositivos iOS, incluida la implementación de la aplicación. Para obtener más información, consulte [Configurar la administración de dispositivos de iOS híbrido](enroll-hybrid-ios-mac.md).  

A partir de la versión 1702 de System Center Configuration Manager, ahora puede implementar aplicaciones con licencia en dispositivos y usuarios. Dependiendo de la capacidad de las aplicaciones para admitir licencias de dispositivo, se solicitará una licencia adecuada al realizar la implementación, como sigue:

|||||
|-|-|-|-|
|Versión de Configuration Manager|¿La aplicación admite licencias de dispositivo?|Tipo de colección de implementación|Licencia exigida|
|Anterior a 1702|Sí|usuario|Licencia de usuario|
|Anterior a 1702|No|usuario|Licencia de usuario|
|Anterior a 1702|Sí|Dispositivo|Licencia de usuario|
|Anterior a 1702|No|Dispositivo|Licencia de usuario|
|1702 y versiones posteriores|Sí|usuario|Licencia de usuario|
|1702 y versiones posteriores|No|usuario|Licencia de usuario|
|1702 y versiones posteriores|Sí|Dispositivo|Licencia de dispositivo|
|1702 y versiones posteriores|No|Dispositivo|Licencia de usuario|

## <a name="step-1---to-get-and-upload-an-apple-vpp-token"></a>Paso 1: obtener y cargar un token de PCV de Apple  

1.  En la consola de Configuration Manager, pulse **Administración** > **Cloud Services** > **Tokens del Programa de Compras por Volumen de Apple**.   

3.  En la pestaña **Inicio**, en el grupo **Tokens del Programa de Compras por Volumen de Apple**, pulse **Agregar token del Programa de Compras por Volumen de Apple**.  

4.  En la página **General** del Asistente para **agregar token del Programa de Compras por Volumen de Apple**, configure lo siguiente:   

    -   **Nombre:** escriba un nombre para este token (así aparecerá en la consola de Configuration Manager).  

    -   **Token**: pulse **Examinar** y, después, seleccione el token de PCV que ha descargado desde el sitio web de Apple.  

         Pulse el vínculo **Ver cuenta de PCV de Apple** y, si no lo ha hecho todavía, regístrese en el programa de compras por volumen profesional o educativo. Una vez que se registre, descargue el token de PCV de Apple para la cuenta.  

    -   **Descripción**: si lo desea, escriba una descripción que le ayude a identificar este token de PCV en la consola de Configuration Manager.  

    -   **Categorías asignadas para mejorar la búsqueda y el filtrado**: si lo desea, puede asignar categorías al token de PCV para que sea más fácil encontrarlo en la consola de Configuration Manager.  
    -   **Id. de Apple**: escriba el identificador de correo electrónico de Apple asociado con el token de VPP.
    -   **Tipo de token**: seleccione el tipo de token de VPP que desea utilizar. Puede elegir los tipos de token **Empresa** y **EDU**.

5.  Pulse **Siguiente** y, después, finalice el asistente.  

En el nodo **Tokens del Programa de Compras por Volumen de Apple**, ahora puede ver información sobre el token de PCV de Apple, que incluye la fecha de la última actualización, la fecha de vencimiento y la fecha de la última sincronización.

Puede sincronizar por completo los datos mantenidos en Apple con Configuration Manager en cualquier momento pulsando **Sincronizar** en la pestaña **Inicio** del grupo **Sincronizar**.  

## <a name="step-2---deploy-a-volume-purchased-app"></a>Paso 2: implementar una aplicación comprada por volumen  

1.  En la consola de Configuration Manager, pulse **Biblioteca de software** > **Administración de aplicaciones** > **Información de licencia para las aplicaciones de la Tienda**.  

3.  Seleccione la aplicación que quiere implementar y, después, en la pestaña **Inicio**, en el grupo **Crear**, pulse **Crear aplicación**.
La aplicación de Configuration Manager que se crea contiene la aplicación de la Tienda Windows para empresas. Luego puede implementar y supervisar esta aplicación como lo haría con cualquier otra aplicación de Configuration Manager.

    > [!IMPORTANT]  
    > Debe elegir un propósito de implementación del tipo **Requerido**. Actualmente no se admiten las instalaciones disponibles.

 Al implementar la aplicación, cada usuario que instala dicha aplicación usa una licencia, o bien en el caso de las instalaciones de dispositivo, cada dispositivo que instala la aplicación.  Si el destino es una recopilación de dispositivos con una aplicación que admite licencias de dispositivo, se reclama una licencia de dispositivo.  Si el destino es una recopilación de dispositivos con una aplicación que no admite licencias de dispositivo, se reclama una licencia de usuario. 

 Cuando se crea una aplicación a partir del nodo **Información de licencia para las aplicaciones de la Tienda**, la aplicación está asociada con licencias del token para la aplicación que ha seleccionado.  Por ejemplo, puede ver dos versiones de la misma aplicación en el nodo. Esto se debe a que cada versión de la aplicación está asociada a un token de VPP de Apple distinto.  A continuación, podría crear aplicaciones de cada token e implementarlas por separado.

 Para reclamar una licencia, debe crear una nueva implementación para la aplicación con una acción de implementación de **Desinstalar**. No se puede cambiar la acción de implementación en la implementación original. La licencia se recuperará una vez que se desinstale la aplicación.  

## <a name="step-3---monitor-ios-vpp-apps"></a>Paso 3: supervisar aplicaciones de PCV de iOS  
 El nodo **Información de licencia para las aplicaciones de la Tienda** del área de trabajo **Biblioteca de software** muestra información sobre sus aplicaciones iOS compradas por volumen. La información incluye el número total de licencias que tiene para cada aplicación y el número que se ha implementado. Además, en la vista se muestra con qué token de VPP está asociada la aplicación, así como el tipo de token.

 También puede supervisar el uso de las licencias de todas las aplicaciones de PCV que ha comprado mediante el informe **Número de aplicaciones del Programa de Compras por Volumen de Apple para iOS con licencias**.  

 En este informe se muestra el nombre de cada aplicación junto con el número total de licencias que ha comprado y el número de licencias disponibles, entre otros datos.  

 Para obtener ayuda con la ejecución de los informes de Configuration Manager, consulte [Reporting in System Center Configuration Manager](../../core/servers/manage/reporting.md) (Generación de informes en System Center Configuration Manager).  

