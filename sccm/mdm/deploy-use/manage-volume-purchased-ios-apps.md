---
title: Manage volume-purchased iOS apps
titleSuffix: Configuration Manager
description: Implemente, administre y realice el seguimiento de licencias de las aplicaciones que ha adquirido mediante App Store de Apple iOS.
ms.date: 03/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 7c3b9316-247b-490b-a363-8f8553821579
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f94cc80d41eb346cb1d4c2fc314d310005c7b5f2
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="manage-volume-purchased-ios-apps-with-system-center-configuration-manager"></a>Administrar aplicaciones de iOS compradas por volumen con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*



 App Store de Apple iOS le permite comprar varias licencias de una aplicación que quiere ejecutar en su compañía. Esta posibilidad ayuda a reducir la carga administrativa relacionada con el seguimiento de varias copias de las aplicaciones que ha comprado.  

 Configuration Manager le ayuda a implementar y administrar aplicaciones de iOS compradas a través del programa. Puede importar la información de licencia desde App Store y realizar el seguimiento del número de licencias que esté usando.  



## <a name="manage-volume-purchased-apps-for-ios-devices"></a>Administrar aplicaciones compradas por volumen para dispositivos iOS  
 Puede comprar varias licencias para aplicaciones iOS a través del Programa de Compras por Volumen (PCV) de Apple. Este proceso implica en primer lugar configurar una cuenta de PCV de Apple desde el sitio web de Apple. Después, cargue el token de PCV de Apple en Configuration Manager, que ofrece las siguientes funcionalidades:  

-   Sincronización de la información de compras por volumen con Configuration Manager  
 
- Sincronización de aplicaciones del Programa de Compras por Volumen de Apple para empresas y el Programa de Compras por Volumen de Apple para educación  

- Asociación de varios tokens del Programa de Compras por Volumen de Apple a Configuration Manager  

-   Visualización de aplicaciones compradas en la consola de Configuration Manager  

-   Implementación y supervisión de estas aplicaciones  

-   Seguimiento del número de licencias utilizadas para cada aplicación   

-   Configuration Manager puede ayudarle a reclamar licencias cuando sea necesario mediante la desinstalación de aplicaciones compradas por volumen que haya implementado.  



## <a name="before-you-start"></a>Antes de empezar  
 Antes de empezar, tiene que obtener un token de PCV de Apple y cargarlo en Configuration Manager.  

-   Si ha usado anteriormente un token de PCV con un producto MDM diferente en su cuenta de PCV de Apple existente, debe generar un nuevo token para usarlo con Configuration Manager.  
-   La validez de cada token es de un año.  
-   De manera predeterminada, Configuration Manager se sincroniza con el servicio PCV de Apple dos veces al día para garantizar que las licencias estén sincronizadas con Configuration Manager. Solo se sincronizan los cambios en las licencias. Se realiza una sincronización completa una vez cada siete días. Cuando se elige **Sincronizar** para realizar una sincronización manual, esta acción siempre realiza una sincronización completa.  
-   Si tiene que recuperar o restaurar la base de datos de Configuration Manager, se recomienda que después realice una sincronización manual. Este proceso garantiza que los datos de licencia sincronizados están actualizados.  
-   Además, debe haber importado un certificado válido de Apple Push Notification Service (APNs) de Apple. Este certificado le permite administrar dispositivos iOS, incluida la implementación de aplicaciones. Para obtener más información, consulte [Configurar la administración de dispositivos de iOS híbrido](enroll-hybrid-ios-mac.md).  
-   Configuration Manager admite la adición de hasta 3000 tokens de VPP.

Puede implementar aplicaciones con licencia para usuarios y dispositivos. Según la capacidad de las aplicaciones para admitir licencias de dispositivo, se solicitará del siguiente modo una licencia adecuada al realizar la implementación:

|¿La aplicación admite licencias de dispositivo?|Tipo de colección de implementación|Licencia exigida|
|---|---|---|
|Sí|usuario|Licencia de usuario|
|No|usuario|Licencia de usuario|
|Sí|Dispositivo|Licencia de dispositivo|
|No|Dispositivo|Licencia de usuario|



## <a name="step-1---to-get-and-upload-an-apple-vpp-token"></a>Paso 1: obtener y cargar un token de PCV de Apple  

1.  En la consola de Configuration Manager, pulse **Administración** > **Cloud Services** > **Tokens del Programa de Compras por Volumen de Apple**.   

3.  En la pestaña **Inicio**, en el grupo **Tokens del Programa de Compras por Volumen de Apple**, pulse **Agregar token del Programa de Compras por Volumen de Apple**.  

4.  En la página **General** del Asistente para **agregar token del Programa de Compras por Volumen de Apple**, configure las siguientes opciones:   

    -   **Nombre**: escriba un nombre para este token (así aparecerá en la consola de Configuration Manager).  

    -   **Token**: pulse **Examinar** y, después, seleccione el token de PCV que ha descargado desde el sitio web de Apple.  

         Haga clic en el vínculo **Ver cuenta de PCV de Apple**. Si no lo ha hecho todavía, regístrese en el programa de compras por volumen para empresas o para educación. Una vez que se registre, descargue el token de PCV de Apple para la cuenta.  

    -   **Descripción**: si quiere, escriba una descripción que le ayude a identificar este token en la consola de Configuration Manager.  

    -   **Categorías asignadas para mejorar la búsqueda y el filtrado**: si lo desea, puede asignar categorías al token de PCV para que sea más fácil encontrarlo en la consola de Configuration Manager.  
    -   **Id. de Apple**: escriba el identificador de correo electrónico de Apple asociado con el token de VPP.
    -   **Tipo de token**: seleccione el tipo de token de VPP que desea utilizar. Puede elegir los tipos de token **Empresa** y **EDU**.

5.  Pulse **Siguiente** y, después, finalice el asistente.  

En el nodo **Tokens del Programa de Compras por Volumen de Apple**, ahora puede ver información sobre el token de PCV de Apple. Esta vista incluye la fecha de la última actualización, cuando expira y cuando se sincronizó por última vez.

Puede sincronizar por completo los datos mantenidos en Apple con Configuration Manager siempre que quiera pulsando **Sincronizar** en la cinta.  



## <a name="step-2---deploy-a-volume-purchased-app"></a>Paso 2: implementar una aplicación comprada por volumen  

1.  En la consola de Configuration Manager, pulse **Biblioteca de software** > **Administración de aplicaciones** > **Información de licencia para las aplicaciones de la Tienda**.  

3.  Seleccione la aplicación que quiere implementar y, después, en la pestaña **Inicio**, en el grupo **Crear**, pulse **Crear aplicación**.
La aplicación de Configuration Manager que se crea contiene la aplicación Microsoft Store para Empresas. Luego puede implementar y supervisar esta aplicación como lo haría con cualquier otra aplicación de Configuration Manager.  

    > [!IMPORTANT]  
    > Debe elegir un propósito de implementación del tipo **Requerido**. Actualmente no se admiten las instalaciones disponibles.

 Al implementar la aplicación, cada usuario que instala dicha aplicación usa una licencia, o bien en el caso de las instalaciones de dispositivo, cada dispositivo que instala la aplicación. Si el destino es una recopilación de dispositivos con una aplicación que admite licencias de dispositivo, se reclama una licencia de dispositivo. Si el destino es una colección de dispositivos con una aplicación que no admite licencias de dispositivo, se reclama una licencia de usuario. 

 Cuando se crea una aplicación a partir del nodo **Información de licencia para las aplicaciones de la Tienda**, la aplicación está asociada con licencias del token para la aplicación que ha seleccionado. Por ejemplo, puede ver dos versiones de la misma aplicación en el nodo. Este comportamiento se debe a que cada versión de la aplicación está asociada a un token de PCV de Apple distinto. Luego puede crear aplicaciones a partir de cada token e implementarlas por separado.

 Para reclamar una licencia, debe crear una nueva implementación para la aplicación con una acción de implementación de **Desinstalar**. No se puede cambiar la acción de implementación en la implementación original. La licencia se reclamará una vez que se desinstale la aplicación.  



## <a name="step-3---monitor-ios-vpp-apps"></a>Paso 3: supervisar aplicaciones de PCV de iOS  
 El nodo **Información de licencia para las aplicaciones de la Tienda** del área de trabajo **Biblioteca de software** muestra información sobre sus aplicaciones iOS compradas por volumen. La información incluye el número total de licencias que tiene para cada aplicación y el número que se ha implementado. Además, en la vista se muestra con qué token de VPP está asociada la aplicación, así como el tipo de token.

 También puede supervisar el uso de las licencias de todas las aplicaciones de PCV que ha comprado mediante el informe **Número de aplicaciones del Programa de Compras por Volumen de Apple para iOS con licencias**.  

 En este informe se muestra el nombre de cada aplicación junto con el número total de licencias que ha comprado y el número de licencias disponibles, entre otros datos.  

 Para obtener ayuda con la ejecución de los informes de Configuration Manager, consulte [Reporting in System Center Configuration Manager](../../core/servers/manage/reporting.md) (Generación de informes en System Center Configuration Manager).  



## <a name="delete-an-apple-vpp-token"></a>Eliminación de un token de PCV de Apple  
<!--505268-->

Siga este procedimiento para eliminar un token de Configuration Manager:  

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**. Expanda **Cloud Services** y seleccione **Tokens del Programa de Compras por Volumen de Apple**.  

2. Seleccione los tokens que quiere eliminar.  

3. Haga clic en la opción **Eliminar** de la cinta.  

