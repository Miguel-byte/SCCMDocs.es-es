---
title: "Administración de aplicaciones iOS adquiridas por volumen | System Center Configuration Manager"
description: Implemente, administre y supervise licencias para las aplicaciones que ha adquirido mediante el App Store de iOS.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b5e7cead-e257-405b-a2aa-b0130e48dc40
caps.latest.revision: 23
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 4289f4853f77392df420e44e179961609f83683f


---
# <a name="manage-volume-purchased-ios-apps-with-system-center-configuration-manager"></a>Manage volume-purchased iOS apps with System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*



 El App Store de iOS le permite comprar varias licencias de una aplicación que desea ejecutar en su empresa. Esto ayuda a reducir la carga administrativa relacionada con el seguimiento de varias copias compradas de las aplicaciones.  

 System Center Configuration Manager ayuda a implementar y administrar aplicaciones de iOS adquiridas a través del programa mediante la importación de la información de licencia desde el App Store y la supervisión de la cantidad de licencias utilizadas.  

## <a name="manage-volume-purchased-apps-for-ios-devices"></a>Administrar aplicaciones compradas por volumen para dispositivos iOS  
 Puede comprar varias licencias para aplicaciones de iOS a través del Programa de Compras por Volumen (PCV) de Apple. Esto implica configurar una cuenta de PCV de Apple en el sitio web de Apple y cargar el token de PCV de Apple en Configuration Manager, con lo que obtendrá las siguientes funcionalidades:  

-   Sincronice la información de la compra por volumen con Configuration Manager.  

-   Las aplicaciones que ha comprado se muestran en la consola de Configuration Manager.  

-   Puede implementar y supervisar estas aplicaciones y también supervisar el número de licencias para cada aplicación que se han utilizado.  

-   Configuration Manager puede ayudarle a recuperar licencias cuando sea necesario mediante la desinstalación de aplicaciones adquiridas por volumen que haya implementado a los usuarios.  

## <a name="before-you-start"></a>Antes de empezar  
 Antes de empezar, es necesario obtener un token de PCV de Apple y cargarlo en Configuration Manager.  

> [!IMPORTANT]  
>  -   Cada organización puede tener una sola cuenta de PCV y un solo token.  
> -   Se admite solo el Programa de Compras por Volumen para Empresas de Apple.  
> -   Una vez asociada una cuenta de PCV a Intune, no se puede asociar posteriormente una cuenta diferente. Por este motivo, es muy importante que varias personas tengan los detalles de la cuenta que se usa.  
> -   Si usó anteriormente un token de PCV con otro producto MDM en su cuenta de PCV existente, debe generar un nuevo token para usar con Configuration Manager.  
> -   La validez de cada token es de un año.  
> -   De forma predeterminada, Configuration Manager se sincroniza con el servicio PCV de Apple dos veces por día para garantizar que las licencias estén sincronizadas con Configuration Manager.  
>   
>      Solo se sincronizan los cambios en las licencias. Sin embargo, una vez cada 7 días, se realiza una sincronización completa.  
>   
>      Al hacer clic en **Sincronizar** para realizar una sincronización manual, siempre se realizará una sincronización completa.  
> -   Si necesita recuperar o restaurar la base de datos de Configuration Manager, se recomienda que realice una sincronización manual posteriormente para garantizar que los datos de licencia sincronizados estén actualizados.  
> -   Aunque puede implementar aplicaciones adquiridas por volumen de iOS en colecciones de usuario o dispositivo, las aplicaciones de PCV que implemente en un dispositivo sin un usuario (por ejemplo, un dispositivo inscrito sin afinidad de usuario mediante el Programa de inscripción de dispositivos o Apple Configurator) no se instalarán.  

 Además, debe haber importado un certificado válido de Apple Push Notification Service de Apple que le permita administrar dispositivos iOS, incluida la implementación de la aplicación. Para obtener más información, consulte [Configurar la administración de dispositivos de iOS híbrido](../../mdm/deploy-use/set-up-ios-hybrid-device-management.md).  

## <a name="step-1---to-get-and-upload-an-apple-vpp-token"></a>Paso 1: obtener y cargar un token de PCV de Apple  
  
1.  En la consola de Configuration Manager, haga clic en **Administración** > **Servicios de nube** > **Tokens del Programa de Compras por Volumen de Apple**.   
  
3.  En la pestaña **Inicio**, en el grupo **Tokens del Programa de Compras por Volumen de Apple**, haga clic en **Agregar token del Programa de Compras por Volumen de Apple**.  

4.  En la página **General** del Asistente para **agregar token del Programa de Compras por Volumen de Apple**, configure lo siguiente:   

    -   **Nombre:** escriba un nombre para este token (así aparecerá en la consola de Configuration Manager).  

    -   **Token**: haga clic en **Examinar** y, a continuación, seleccione el token de PCV que descargó desde el sitio web de Apple.  

         Haga clic en el vínculo **Cuenta de PCV de Apple** y, si no lo ha hecho todavía, regístrese en el programa de compras por volumen para la empresa o la educación. Una vez que se registre, descargue el token de PCV de Apple para la cuenta.  

    -   **Descripción**: si lo desea, escriba una descripción que le ayude a identificar este token de PCV en la consola de Configuration Manager.  

    -   **Categorías asignadas para mejorar la búsqueda y el filtrado**: si lo desea, puede asignar categorías al token de PCV para que sea más fácil encontrarlo en la consola de Configuration Manager.  

5.  Haga clic en **Siguiente** y complete el asistente.  
  
En el nodo **Tokens del Programa de Compras por Volumen de Apple**, ahora puede ver información sobre el token de PCV de Apple, que incluye la fecha de la última actualización, la fecha de vencimiento y la fecha de la última sincronización. 
  
Puede sincronizar por completo los datos mantenidos en Apple con Configuration Manager en cualquier momento haciendo clic en **Sincronizar** en la pestaña **Inicio**, en el grupo **Sincronizar**.  
  
## <a name="step-2---deploy-a-volume-purchased-app"></a>Paso 2: implementar una aplicación comprada por volumen  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software** > **Administración de aplicaciones** > **Información de licencia para las aplicaciones de la Tienda**.  

3.  Elija la aplicación que quiere implementar y, luego, en la pestaña **Inicio**, en el grupo **Crear**, haga clic en **Crear aplicación**.
Se crea una aplicación de Configuration Manager que contiene la aplicación de la Tienda Windows para empresas. Luego puede implementar y supervisar esta aplicación como lo haría con cualquier otra aplicación de Configuration Manager.

    > [!IMPORTANT]  
    > Debe elegir un propósito de implementación del tipo **Requerido**. Actualmente no se admiten las instalaciones disponibles.

 Al implementar la aplicación, cada usuario que instala dicha aplicación usa una licencia.  

 Para recuperar una licencia, se debe cambiar la acción de implementación a **Desinstalar**. La licencia se recupera cuando se desinstala la aplicación.  

## <a name="step-3---monitor-ios-vpp-apps"></a>Paso 3: supervisar aplicaciones de PCV de iOS  
 El nodo **Información de licencia para las aplicaciones de la Tienda	** del área de trabajo **Biblioteca de software** muestra información sobre las aplicaciones de iOS adquiridas por volumen, incluido el número total de licencias que posee para cada aplicación y cuántas se han implementado.

 También puede supervisar el uso de las licencias de todas las aplicaciones de PCV que ha comprado mediante el informe **Número de aplicaciones del Programa de Compras por Volumen de Apple para iOS con licencias**.  

 Este informe muestra el nombre de cada aplicación junto con el número total de licencias que se compraron, el número de licencias disponibles, entre otros datos.  

 Para obtener ayuda con la ejecución de los informes de Configuration Manager, consulte [Reporting in System Center Configuration Manager](../../core/servers/manage/reporting.md) (Generación de informes en System Center Configuration Manager).  



<!--HONumber=Nov16_HO1-->


