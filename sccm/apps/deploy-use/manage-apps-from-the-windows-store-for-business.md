---
title: Administración de aplicaciones desde Microsoft Store para Empresas
titleSuffix: Configuration Manager
description: Administre e implemente aplicaciones desde Microsoft Store para Empresas con System Center Configuration Manager.
ms.date: 12/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 8cdb22a6-72d7-41f5-9bed-c098b1bcf675
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4999784140ece9df49a28063e8660566f7206df0
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32336126"
---
# <a name="manage-apps-from-the-microsoft-store-for-business-with-system-center-configuration-manager"></a>Administrar aplicaciones desde Microsoft Store para Empresas con System Center Configuration Manager
[Microsoft Store para Empresas](https://www.microsoft.com/business-store) es el lugar donde puede buscar y comprar aplicaciones de Windows para su organización, individualmente o por volumen. Si conecta la tienda a Configuration Manager, puede sincronizar la lista de aplicaciones que ha comprado con Configuration Manager. A continuación, puede ver estas aplicaciones en la consola de Configuration Manager e implementarlas como cualquier otra aplicación.


## <a name="online-and-offline-apps"></a>Aplicaciones en línea y sin conexión

Microsoft Store para Empresas admite dos tipos de aplicaciones:

- **En línea**: este tipo de licencia requiere que usuarios y dispositivos se conecten a la tienda para obtener una aplicación y su licencia. Los dispositivos de Windows 10 deben estar unidos a un dominio de Azure Active Directory.
- **Sin conexión**: permite almacenar en caché aplicaciones y licencias para implementarlas directamente en la red local. No es necesario que los dispositivos se conecten a la tienda o tengan una conexión a Internet.

[Obtenga más información](https://docs.microsoft.com/microsoft-store/microsoft-store-for-business-overview) sobre Microsoft Store para Empresas.

Configuration Manager admite la administración de aplicaciones de Microsoft Store para Empresas tanto en dispositivos con Windows 10 con el cliente de Configuration Manager como en los dispositivos con Windows 10 inscritos con Microsoft Intune. Configuration Manager ofrece las siguientes funciones para las aplicaciones en línea y sin conexión.

> [!IMPORTANT]
> Para usar Microsoft Store para Empresas, los dispositivos Windows 10 deben ejecutar la versión de noviembre de 2015 (1511) o una versión posterior.


|Capacidad|Aplicaciones sin conexión|Aplicaciones en línea|
|------------|------------|------------|
|Sincronizar datos de la aplicación en Configuration Manager<br>(la sincronización se produce cada 24 horas)|Sí|Sí|
|Crear aplicaciones de Configuration Manager desde las aplicaciones de la tienda|Sí|Sí|
|Compatibilidad con las aplicaciones gratuitas de la tienda|Sí|Sí|
|Compatibilidad con las aplicaciones de pago de la tienda|No|Sí<sup>1</sup>|
|Compatibilidad con las implementaciones necesarias para las colecciones de usuarios o dispositivos|Sí|Sí|
|Compatibilidad con las implementaciones disponibles para las colecciones de usuarios o dispositivos|Sí|Sí|
|Compatibilidad con las aplicaciones de línea de negocio desde la tienda|Sí|Sí|

<sup>1</sup>Para implementar aplicaciones con licencia en línea en equipos con Windows 10 con el cliente de Configuration Manager, deben ejecutar Windows 10 Creators Update o posterior.

### <a name="deploying-online-apps-using-the-microsoft-store-for-business-with-pcs-that-run-the-configuration-manager-client"></a>Implementación de aplicaciones en línea mediante Microsoft Store para Empresas con equipos que ejecutan el cliente de Configuration Manager
Antes de implementar aplicaciones de Microsoft Store para Empresas en equipos que ejecutan el cliente completo de Configuration Manager, tenga en cuenta lo siguiente:

- Para obtener una funcionalidad completa, los equipos deben ejecutar Windows 10 Creators Update o posterior.
- Los PC deben estar unidos a Azure Active Directory en el mismo inquilino donde registró Microsoft Store para Empresas como una herramienta de administración.
- Si los equipos están registrados con la cuenta predefinida de administrador, no pueden obtener acceso a las aplicaciones de Microsoft Store para Empresas.
- Los equipos deben tener una conexión dinámica a Internet con Microsoft Store para Empresas.

### <a name="notes-for-pcs-running-earlier-versions-of-windows-10"></a>Notas para los equipos que ejecutan versiones anteriores de Windows 10
En equipos que ejecutan una versión de Windows 10 anterior a Creators Update (con el cliente de Configuration Manager), se aplica la siguiente funcionalidad:


- Al forzar la instalación porque el usuario instala la aplicación, la aplicación alcanza su fecha límite de instalación o la reevaluación posterior a la instalación de las implementaciones requeridas:
    - La aplicación se "fuerza" iniciando la aplicación de Microsoft Store para Empresas. 
    - El usuario final después debe completar la instalación desde la tienda antes de que se instale.
    - En la consola de Configuration Manager, el estado de la aplicación se notifica con el error "La aplicación de Microsoft Store se abrió en el equipo cliente y está esperando a que el usuario complete la instalación".
- En el siguiente ciclo de evaluación de la aplicación:
    - Si el usuario final instala la aplicación desde la tienda, esta notifica el estado **Correcto**. 
    - Si el usuario final no ha intentado instalar la aplicación desde la tienda:
        - Las implementaciones necesarias intentan iniciar la tienda y volver a forzar la instalación de la aplicación.
        - Las implementaciones disponibles no se vuelven a forzar.

#### <a name="further-notes-for-pcs-running-earlier-versions-of-windows-10"></a>Notas adicionales para los equipos que ejecutan versiones anteriores de Windows 10:

- No puede implementar aplicaciones de línea de negocio desde Microsoft Store para Empresas
- Al implementar aplicaciones de pago en la tienda, los usuarios finales deben iniciar sesión y adquirirlas.
- Si implementa una directiva de grupo para deshabilitar el acceso a la versión de consumo de Microsoft Store, las implementaciones desde Microsoft Store para Empresas no funcionarán, aunque Microsoft Store para Empresas esté habilitada.


## <a name="set-up-microsoft-store-for-business-synchronization"></a>Configurar la sincronización de Microsoft Store para Empresas
La sincronización de la lista de aplicaciones compradas por la organización permite ver estas aplicaciones en la consola de Configuration Manager.

<!-- Remove below after 1802... -->
### <a name="for-configuration-manager-versions-prior-to-1706"></a>Para versiones de Configuration Manager anteriores a la 1706

**En Azure Active Directory, registre Configuration Manager como una herramienta de administración "Aplicación web y/o API web". Esta acción le proporciona un identificador de cliente que necesitará más adelante.**
1. En el nodo de Active Directory de [https://manage.windowsazure.com](https://manage.windowsazure.com), seleccione Azure Active Directory y, luego, haga clic en **Aplicaciones** > **Agregar**.
2.  Haga clic en **Agregar una aplicación que mi organización está desarrollando**.
3.  Escriba un nombre para la aplicación, seleccione **Aplicación web** y/o **API web** y haga clic en la flecha **Siguiente**.
4.  Escriba la misma dirección URL para **URL de inicio de sesión** y **URI de id. de aplicación**. La dirección URL puede ser cualquiera (no es necesario que se resuelva en una dirección real). Por ejemplo, puede escribir *https://yourdomain/sccm*.
5.  Complete el asistente.

**En Azure Active Directory, cree una clave de cliente para la herramienta de administración registrada.**
1.  Resalte la aplicación que haya creado y haga clic en **Configurar**.
2.  En **Claves**, seleccione una duración de la lista y haga clic en **Guardar**. Esta acción crea una clave de cliente. No salga de esta página hasta que haya incorporado correctamente Microsoft Store para Empresas a Configuration Manager.

**En Microsoft Store para Empresas, configure Configuration Manager como la herramienta de administración de la tienda**
1.  Abra [https://businessstore.microsoft.com/managementtools](https://businessstore.microsoft.com/managementtools) e inicie sesión si se le solicita.
2.  Si se le solicita, acepte los términos de uso.
3.  Bajo **Herramientas de administración**, haga clic en **Add a management tool** (Agregar una herramienta de administración).
4.  En **Buscar la herramienta por nombre**, escriba el nombre de la aplicación que creó anteriormente en AAD y luego haga clic en **Agregar**.
5.  Haga clic en **Activar** junto a la aplicación que haya importado.
6.  En la página **Administrar > Información de la cuenta**, seleccione **Show Offline-Licensed Apps** (Mostrar aplicaciones con licencia sin conexión) si desea permitir la adquisición de aplicaciones con licencias sin conexión.

**Incorporación de la cuenta de la tienda a Configuration Manager**

1. Asegúrese de que ha comprado al menos una aplicación en Microsoft Store para Empresas. En el área de trabajo **Administración** de la consola de Configuration Manager, expanda **Servicios de nube** y luego haga clic en **Microsoft Store para Empresas**.
2.  En la pestaña **Inicio**, en el grupo **Microsoft Store para Empresas**, haga clic en **Agregar cuenta de Microsoft Store para Empresas**. 
3.  Agregue el identificador de inquilino, el identificador de cliente y la clave de cliente de Azure Active Directory y finalice el asistente.
4. Cuando haya terminado, puede ver la cuenta configurada bajo **Microsoft Store para Empresas** en la consola de Configuration Manager.

### <a name="for-configuration-manager-version-1706-and-later"></a>Para la versión 1706 de Configuration Manager y posteriores
<!-- ...remove above after 1802 -->

1. En la consola, vaya a **Administración** > **Cloud Services** > **Azure Services** y, después, seleccione **Configurar servicios de Azure** para iniciar el **Asistente para servicios de Azure**.
2. En la página **Servicios de Azure**, seleccione el servicio que quiera configurar y, después, haga clic en **Siguiente**.
3. En la página **General**, proporcione un nombre descriptivo para el nombre del servicio de Azure y una descripción opcional y, después, haga clic en **Siguiente**.
4. En la página **Aplicación**, especifique el entorno de Azure y, después, haga clic en **Examinar** para abrir la ventana **Aplicación del servidor**.
5. En la ventana **Aplicación del servidor**, seleccione la aplicación de servidor que quiera usar y, después, haga clic en **Aceptar**. Las aplicaciones de servidor son las aplicaciones web de Azure que contienen las configuraciones de la cuenta de Azure, incluidos el identificador de inquilino, el identificador de cliente y una clave secreta para los clientes. Si no tiene una aplicación de servidor disponible, realice una de las acciones siguientes:
    - **Crear**: para crear una nueva aplicación de servidor haga clic en **Crear**. Proporcione un nombre descriptivo para la aplicación y el inquilino. Después, una vez que inicie sesión en Azure, Configuration Manager crea automáticamente la aplicación web en Azure, incluidos el identificador de cliente y la clave secreta para su uso con la aplicación web. Más adelante, puede ver estos valores desde Azure Portal.
    - **Importar**: para usar una aplicación web que ya existe en su suscripción de Azure, haga clic en **Importar**. Proporcione un nombre descriptivo para la aplicación y el inquilino. Después, especifique el identificador del inquilino, el identificador de cliente y la clave secreta de la aplicación web de Azure que quiere que use Configuration Manager. Después de **Comprobar** la información, haga clic en **Aceptar** para continuar. 
6. Revise la página **Información** y complete los pasos y configuraciones adicionales tal como se indica. Estas configuraciones son necesarias para usar el servicio con Configuration Manager. Por ejemplo, para configurar Microsoft Store para Empresas:
    - En Azure, debe registrar Configuration Manager como una aplicación web o API web, y registrar el identificador de cliente. Especifique también una clave de cliente para su uso con la herramienta de administración (que es Configuration Manager).
    - En el portal de Microsoft Store para Empresas debe configurar Configuration Manager como la herramienta de administración de la tienda, habilitar la compatibilidad de aplicaciones con licencia sin conexión y, después, comprar al menos una aplicación. 
7. Haga clic en **Siguiente** cuando esté listo para continuar.
8. En la página **Configuraciones de aplicación**, realice las configuraciones del catálogo de aplicaciones y el idioma para este servicio y, después, haga clic en **Siguiente**.
9. Cuando finalice el asistente, la consola de Configuration Manager muestra que ha configurado **Microsoft Store para Empresas** como un **Tipo de servicio de nube**.




## <a name="create-and-deploy-a-configuration-manager-application-from-a-microsoft-store-for-business-app"></a>Creación e implementación de una aplicación de Configuration Manager a partir de una aplicación de Microsoft Store para Empresas
Después de la sincronización, cree e implemente las aplicaciones de la tienda como lo haría con cualquier otra aplicación.

1.  En el área de trabajo **Biblioteca de software** de la consola de Configuration Manager, expanda **Administración de aplicaciones** y luego haga clic en **Información de licencia para las aplicaciones de la Tienda**.
2.  Elija la aplicación que quiere implementar y, luego, en la pestaña **Inicio**, en el grupo **Crear**, haga clic en **Crear aplicación**.
Se crea una aplicación de Configuration Manager que contiene la aplicación de Microsoft Store para Empresas. Luego puede implementar y supervisar esta aplicación como lo haría con cualquier otra aplicación de Configuration Manager.

> [!IMPORTANT]
> En el caso de los dispositivos inscritos en Microsoft Intune, las aplicaciones implementadas solo están disponibles para el usuario que originalmente haya inscrito el dispositivo. Ningún otro usuario puede tener acceso a la aplicación.

## <a name="next-steps"></a>Pasos siguientes

En el área de trabajo **Biblioteca de software**, expanda **Administración de aplicaciones** y luego haga clic en **Información de licencia para las aplicaciones de la Tienda**.

Para cada aplicación de la tienda que administre, puede ver información sobre la aplicación. Esta información incluye el nombre de la aplicación, la plataforma, el número de licencias para la aplicación que posee y el número de licencias que tiene disponibles.

Después de implementar aplicaciones en línea, las actualizaciones de esa aplicación provendrán directamente de Microsoft Store. Además, Configuration Manager no comprueba la compatibilidad de versión de las aplicaciones en línea, al igual que Windows informa de la aplicación como instalada.  

Al implementar aplicaciones sin conexión en dispositivos Windows 10 con el cliente de Configuration Manager, no permita a los usuarios actualizar aplicaciones externas en implementaciones de Configuration Manager. El control de las actualizaciones de las aplicaciones sin conexión es especialmente importante en entornos de varios usuarios como clases. Una opción para deshabilitar Microsoft Store es mediante la [directiva de grupo](https://docs.microsoft.com/windows/configuration/stop-employees-from-using-microsoft-store#a-href-idblock-store-group-policyablock-microsoft-store-using-group-policy). 

Después de que el administrador de Microsoft Store para Empresas compre una aplicación sin conexión, no publique la aplicación a los usuarios a través de la tienda. Esta configuración garantiza que los usuarios no puedan instalar o actualizar en línea. Los usuarios solo recibirán actualizaciones de aplicaciones sin conexión a través de Configuration Manager. 
