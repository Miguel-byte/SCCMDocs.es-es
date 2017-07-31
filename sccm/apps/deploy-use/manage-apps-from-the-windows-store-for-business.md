---
title: "Administración de aplicaciones adquiridas en la Tienda Windows para empresas | Microsoft Docs"
description: Administre e implemente aplicaciones desde la Tienda Windows para empresas con System Center Configuration Manager.
ms.custom: na
ms.date: 7/25/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8cdb22a6-72d7-41f5-9bed-c098b1bcf675
caps.latest.revision: 11
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: HT
ms.sourcegitcommit: ef42d1483053e9a6c502f4ebcae5a231aa6ba727
ms.openlocfilehash: 93e767c9a115b30d68871baece670977165f55f4
ms.contentlocale: es-es
ms.lasthandoff: 07/26/2017

---

# <a name="manage-apps-from-the-windows-store-for-business-with-system-center-configuration-manager"></a>Administración de aplicaciones desde la Tienda Windows para empresas con System Center Configuration Manager
La [Tienda Windows para empresas](https://www.microsoft.com/business-store) es el lugar donde puede buscar y adquirir aplicaciones de Windows para su organización, individualmente o por volumen. Si conecta la tienda a Configuration Manager, puede sincronizar la lista de aplicaciones que ha comprado con Configuration Manager. A continuación, puede ver estas aplicaciones en la consola de Configuration Manager e implementarlas como cualquier otra aplicación.


## <a name="online-and-offline-apps"></a>Aplicaciones en línea y sin conexión

La Tienda Windows para empresas admite dos tipos de aplicaciones:

- **En línea**: este tipo de licencia requiere que usuarios y dispositivos se conecten a la tienda para obtener una aplicación y su licencia. Los dispositivos de Windows 10 deben estar unidos a un dominio de Azure Active Directory.
- **Sin conexión**: le permite almacenar en caché las aplicaciones y licencias para implementarlas directamente en su red local, sin necesidad de conectarse a la tienda o tener una conexión a Internet.

[Obtenga más información](https://technet.microsoft.com/itpro/windows/whats-new/windows-store-for-business-overview?f=255&MSPPError=-2147217396) acerca de la Tienda Windows para empresas.

Configuration Manager admite la administración de aplicaciones de la Tienda Windows para empresas tanto en dispositivos de Windows 10 que ejecutan el cliente de Configuration Manager como en los dispositivos de Windows 10 inscritos a Microsoft Intune (en lo que se conoce como configuración híbrida). Configuration Manager ofrece las siguientes funciones para las aplicaciones en línea y sin conexión.

> [!IMPORTANT]
> Para utilizarlas, los dispositivos de Windows 10 deben ejecutar la versión de noviembre de 2015 (1511) o una posterior.


|Capacidad|Aplicaciones sin conexión|Aplicaciones en línea|
|------------|------------|------------|
|Sincronizar datos de la aplicación en Configuration Manager<br>(la sincronización se produce cada 24 horas)|Sí|Sí|
|Crear aplicaciones de Configuration Manager desde las aplicaciones de la tienda|Sí|Sí|
|Compatibilidad con las aplicaciones gratuitas de la tienda|Sí|Sí|
|Compatibilidad con las aplicaciones de pago de la tienda|No|Sí|
|Compatibilidad con las implementaciones necesarias para las colecciones de usuarios o dispositivos|Sí|Sí|
|Compatibilidad con las implementaciones disponibles para las colecciones de usuarios o dispositivos|Sí|Sí|
|Compatibilidad con las aplicaciones de línea de negocio desde la tienda|Sí|Sí|

Para implementar aplicaciones con licencia en línea en equipos con Windows 10 con el cliente de Configuration Manager, deben ejecutar Windows 10 Creators Update o posterior.

## <a name="deploying-online-apps-using-the-windows-store-for-business-with-pcs-that-run-the-configuration-manager-client"></a>Implementación de aplicaciones en línea mediante la Tienda Windows para empresas con equipos que ejecutan el cliente de Configuration Manager
Antes de implementar aplicaciones de la Tienda Windows para empresas en equipos que ejecutan el cliente completo de Configuration Manager, tenga en cuenta lo siguiente:

- Para obtener una funcionalidad completa, los equipos deben ejecutar Windows 10 Creators Update o posterior.
- Los equipos deben estar unidos al área de trabajo de Azure Active Directory y encontrarse en el mismo inquilino de AAD donde ha registrado la Tienda Windows para empresas como una herramienta de administración.
- Si los equipos están registrados con la cuenta predefinida de administrador, no pueden acceder a las aplicaciones de la Tienda Windows para empresas.
- Los equipos deben tener una conexión dinámica a Internet con la Tienda Windows para empresas.

### <a name="notes-for-pcs-running-earlier-versions-of-windows-10"></a>Notas para los equipos que ejecutan versiones anteriores de Windows 10
En equipos que ejecutan una versión de Windows 10 anterior a Creators Update (con el cliente de Configuration Manager), se aplica la siguiente funcionalidad:


- Si la instalación se fuerza porque el usuario la instala, consume la fecha límite de instalación o la reevaluación posterior a la instalación de las implementaciones requeridas:
    - La aplicación se "fuerza" iniciando la aplicación de la Tienda Windows para empresas. 
    - El usuario final después debe completar la instalación desde la tienda antes de que se instale.
    - El estado de la aplicación en la consola de Configuration Manager se notifica con el error "La aplicación de la Tienda Windows se ha abierto en el equipo cliente y está esperando a que el usuario complete la instalación".
- En el siguiente ciclo de evaluación de la aplicación:
    - Si el usuario final instala la aplicación desde la tienda, esta notifica el estado **Correcto**. 
    - Si el usuario final no ha intentado instalar la aplicación desde la tienda:
        - Las implementaciones necesarias intentan iniciar la tienda y volver a forzar la instalación de la aplicación.
        - Las implementaciones disponibles no se vuelven a forzar.

#### <a name="further-notes-for-pcs-running-earlier-versions-of-windows-10"></a>Notas adicionales para los equipos que ejecutan versiones anteriores de Windows 10:

- No puede implementar líneas de aplicaciones empresariales desde la Tienda Windows para empresas.
- Al implementar aplicaciones de pago en la tienda, los usuarios finales deben iniciar sesión y adquirirlas.
- Si ha implementado una directiva de grupo que deshabilita el acceso a la versión de consumo de la Tienda Windows, las implementaciones desde la Tienda Windows para empresas no funcionarán, aunque la Tienda esté habilitada.


## <a name="set-up-windows-store-for-business-synchronization"></a>Configuración de la sincronización de la Tienda Windows para empresas

**En Azure Active Directory, registre Configuration Manager como una herramienta de administración "Aplicación web y/o API web". Esta acción le proporciona un identificador de cliente que necesitará más adelante.**
1. En el nodo de Active Directory de [https://manage.windowsazure.com](https://manage.windowsazure.com), seleccione Azure Active Directory y luego haga clic en **Aplicaciones** > **Agregar**.
2.  Haga clic en **Agregar una aplicación que mi organización está desarrollando**.
3.  Escriba un nombre para la aplicación, seleccione **Aplicación web** y/o **API web** y haga clic en la flecha **Siguiente**.
4.  Escriba la misma dirección URL para **URL de inicio de sesión** y **URI de id. de aplicación**. La dirección URL puede ser cualquiera (no es necesario que se resuelva en una dirección real). Por ejemplo, puede escribir *https://yourdomain/sccm*.
5.  Complete el asistente.

**En Azure Active Directory, cree una clave de cliente para la herramienta de administración registrada.**
1.  Resalte la aplicación que haya creado y haga clic en **Configurar**.
2.  En **Claves**, seleccione una duración de la lista y haga clic en **Guardar**. Esta acción crea una clave de cliente. No salga de esta página hasta que haya incorporado correctamente la Tienda Windows para empresas a Configuration Manager.

**En la Tienda Windows para empresas, configure Configuration Manager como la herramienta de administración de la tienda.**
1.  Abra [https://businessstore.microsoft.com/en-us/managementtools](https://businessstore.microsoft.com/en-us/managementtools) e inicie sesión si se le solicita.
2.  Si se le solicita, acepte los términos de uso.
3.  Bajo **Herramientas de administración**, haga clic en **Add a management tool** (Agregar una herramienta de administración).
4.  En **Buscar la herramienta por nombre**, escriba el nombre de la aplicación que creó anteriormente en AAD y luego haga clic en **Agregar**.
5.  Haga clic en **Activar** junto a la aplicación que haya importado.
6.  En la página **Administrar > Información de la cuenta**, seleccione **Show Offline-Licensed Apps** (Mostrar aplicaciones con licencia sin conexión) si desea permitir la adquisición de aplicaciones con licencias sin conexión.

**Incorporación de la cuenta de la tienda a Configuration Manager**

1. Asegúrese de que ha comprado al menos una aplicación en la Tienda Windows para empresas. En el área de trabajo **Administración** de la consola de Configuration Manager, expanda **Servicios de nube** y luego haga clic en **Tienda Windows para empresas**.
2.  En la pestaña **Inicio**, en el grupo **Tienda Windows para empresas**, haga clic en **Agregar cuenta de la Tienda Windows para empresas**. 
3.  Agregue el identificador de inquilino, el identificador de cliente y la clave de cliente de Azure Active Directory y finalice el asistente.
4. Una vez que haya terminado, verá la cuenta configurada en la lista **Tienda Windows para empresas** en la consola de Configuration Manager.


## <a name="create-and-deploy-a-configuration-manager-application-from-a-windows-store-for-business-app"></a>Cree e implemente una aplicación de Configuration Manager a partir de una aplicación de la Tienda Windows para empresas.
1.  En el área de trabajo **Biblioteca de software** de la consola de Configuration Manager, expanda **Administración de aplicaciones** y luego haga clic en **Información de licencia para las aplicaciones de la Tienda**.
2.  Elija la aplicación que quiere implementar y, luego, en la pestaña **Inicio**, en el grupo **Crear**, haga clic en **Crear aplicación**.
Se crea una aplicación de Configuration Manager que contiene la aplicación de la Tienda Windows para empresas. Luego puede implementar y supervisar esta aplicación como lo haría con cualquier otra aplicación de Configuration Manager.

> [!IMPORTANT]
> En el caso de los dispositivos inscritos en Intune, las aplicaciones implementadas solo están disponibles para el usuario que originalmente haya inscrito el dispositivo. Ningún otro usuario puede tener acceso a la aplicación.

## <a name="next-steps"></a>Pasos siguientes

En el área de trabajo **Biblioteca de software**, expanda **Administración de aplicaciones** y luego haga clic en **Información de licencia para las aplicaciones de la Tienda**.

Para cada aplicación de la tienda que administre, podrá ver información acerca de la aplicación, incluido su nombre, plataforma y número de licencias para la aplicación que posee, así como el número de licencias que tiene disponibles.

