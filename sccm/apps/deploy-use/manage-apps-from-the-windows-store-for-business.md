---
title: "Administración de aplicaciones adquiridas en la Tienda Windows para empresas | Microsoft Docs"
description: Administre e implemente aplicaciones desde la Tienda Windows para empresas con System Center Configuration Manager.
ms.custom: na
ms.date: 02/14/2017
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
translationtype: Human Translation
ms.sourcegitcommit: f955b5aadfc617e08d5d933dee8e42de838f83c0
ms.openlocfilehash: bf2937f5ba86db19d9cb40e2c98cbb8ba365f7eb

---
# <a name="manage-apps-from-the-windows-store-for-business-with-system-center-configuration-manager"></a>Administración de aplicaciones desde la Tienda Windows para empresas con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

La [Tienda Windows para empresas](https://www.microsoft.com/business-store) es el lugar donde puede buscar y comprar aplicaciones de Windows para su organización, individualmente o por volumen. Al conectar la tienda a Configuration Manager, puede sincronizar la lista de aplicaciones que ha comprado con Configuration Manager, verlas en la consola de Configuration Manager e implementarlas como lo haría con cualquier otra aplicación.


## <a name="online-and-offline-apps"></a>Aplicaciones en línea y sin conexión

La Tienda Windows para empresas admite dos tipos de aplicaciones:

- **En línea**: este tipo de licencia requiere que usuarios y dispositivos se conecten a la tienda para obtener una aplicación y su licencia. Los dispositivos de Windows 10 deben estar unidos a un dominio de Azure Active Directory.
- **Sin conexión**: las organizaciones pueden almacenar en caché las aplicaciones y las licencias para implementarlas directamente en su red local, sin necesidad de conectarse a la tienda o tener una conexión a Internet.

Obtenga más información sobre la [Tienda Windows para empresas](https://technet.microsoft.com/itpro/windows/whats-new/windows-store-for-business-overview).

Configuration Manager admite la administración de aplicaciones de la Tienda Windows para empresas en dispositivos de Windows 10 que ejecutan el cliente de Configuration Manager y en los dispositivos de Windows 10 inscritos con Microsoft Intune (configuración híbrida). Configuration Manager ofrece las siguientes funciones para las aplicaciones en línea y sin conexión.

> [!IMPORTANT]
> Para usarlas, los dispositivos de Windows 10 deben ejecutar la versión de noviembre de 2015 (1511) o una posterior.

|Capacidad|Aplicaciones sin conexión|Aplicaciones en línea|
|------------|------------|------------|
|Sincronizar datos de la aplicación en Configuration Manager<br>(La sincronización se produce cada 24 horas, o bien puede iniciar una sincronización inmediata).|Sí|Sí|
|Crear aplicaciones de Configuration Manager desde las aplicaciones de la tienda|Sí|Sí|
|Compatibilidad con las aplicaciones gratuitas de la tienda|Sí|Sí<sup>1</sup>|
|Compatibilidad con las aplicaciones de pago de la tienda|No|Sí<sup>1</sup>|
|Compatibilidad con las implementaciones necesarias para las colecciones de usuarios o dispositivos|Sí|Sí<sup>1</sup>|
|Compatibilidad con las implementaciones disponibles para las colecciones de usuarios o dispositivos|Sí<sup>2</sup>|No|

<sup>1</sup>Solo hay compatibilidad con dispositivos administrados por Intune. No se le impide la creación de una aplicación en línea en la consola de Configuration Manager y su implementación en un dispositivo administrado por el cliente de Configuration Manager, pero la implementación no funcionará. Se dirigirá a los usuarios a la página correspondiente de la tienda de aplicaciones para que instalen la aplicación manualmente.

<sup>2</sup>Solo hay compatibilidad con dispositivos administrados por el cliente de Configuration Manager.

<!--- ## Activate the Windows Store for Business capability
Because this is a pre-release feature, before you can connect Configuration Manager to the Windows Store for Business, you must take the following steps:

**Give your consent to use pre-release features**
1. In the **Administration** workspace of the Configuration Manager console, choose **Site Configuration** > **Sites**.
2. Select the top-level site in your hierarchy, then, open **Hierarchy Settings**.
3. In the **Hierarchy Settings Properties** dialog box, check the box, **Consent to use Pre-Release** features.
4. Choose **OK**.

**Activate the Windows Store for Business capability**
1. In the **Administration** workspace of the Configuration Manager console, choose **Cloud Services** > **Updates and Servicing** > **Features**.
2. Select **Windows Store for Business Integration**, and then in the **Home** tab, in the **Features** group, choose **Turn on**.
3. Close and re-open the Configuration Manager console.
4. You'll now see the node **Windows Store for Business** in the **Administration** workspace under **Cloud Services**. --->

## <a name="set-up-windows-store-for-business-synchronization"></a>Configuración de la sincronización de la Tienda Windows para empresas

> [!IMPORTANT]
> Cuando establezca una conexión entre Configuration Manager y la Tienda Windows para empresas, deberá proporcionar una carpeta donde se conservará el contenido de la aplicación sincronizado desde la tienda.
Para asegurarse de que esta carpeta sea segura y que su contenido se pueda implementar en dispositivos, compruebe que se hayan aplicado los permisos siguientes:
-    El equipo en el que instale el rol de sistema de sitio del punto de conexión de servicio (el sitio de nivel superior de la jerarquía) debe tener permisos de lectura y escritura en la carpeta que haya especificado al usar la cuenta **Computer$**.
-    El autor de la aplicación debe tener permisos de lectura en la carpeta que haya especificado.
-    La cuenta **Computer$** de cada equipo que hospede una instancia del proveedor de SMS debe poder usar la carpeta que haya especificado.


En Azure Active Directory, registre Configuration Manager como una herramienta de administración de aplicación web o API web. De este modo, obtendrá un identificador de cliente que necesitará más adelante.
1. En el nodo [https://manage.windowsazure.com](https://manage.windowsazure.com) de Active Directory, seleccione Azure Active Directory y **Aplicaciones** > **Agregar**.
2.  Seleccione **Agregar una aplicación que mi organización está desarrollando**.
3.  Escriba un nombre para la aplicación, elija **Aplicación web** y/o **API web** y, después, seleccione **Siguiente**.
4.  Escriba la misma dirección URL para **URL de inicio de sesión** y **URI de id. de aplicación**. La dirección URL puede ser cualquiera (no es necesario que se resuelva en una dirección real). Por ejemplo, puede escribir *https://yourdomain/sccm*.
5.  Finalice el asistente.

En Azure Active Directory, cree una clave de cliente para la herramienta de administración registrada.
1.  Resalte la aplicación que acaba de crear y seleccione **Configurar**.
2.  En **Claves**, elija una duración de la lista y, después, seleccione **Guardar**. De este modo, se creará una nueva clave de cliente. No salga de esta página hasta que haya incorporado correctamente la Tienda Windows para empresas a Configuration Manager.

En la Tienda Windows para empresas, configure Configuration Manager como la herramienta de administración de la tienda.
1.  Abra [https://businessstore.microsoft.com/es-es/managementtools](https://businessstore.microsoft.com/en-us/managementtools) e inicie sesión si se le solicita.
2.  Si se le solicita, acepte los términos de uso.
3.  En **Herramientas de administración**, seleccione **Add a management tool** (Agregar una herramienta de administración).
4.  En **Search for the tool by name** (Buscar la herramienta por nombre), escriba el nombre de la aplicación que creó anteriormente en Azure Active Directory y, luego, seleccione **Agregar**.
5.  Seleccione **Activar** junto a la aplicación que acaba de importar.
6.  En la página **Administrar > Información de la cuenta**, seleccione **Show Offline-Licensed Apps** (Mostrar aplicaciones con licencia sin conexión) si quiere permitir la adquisición de aplicaciones con licencias sin conexión.

> [!Note]
> Si utiliza más de una herramienta de administración para implementar aplicaciones de la Tienda Windows para empresas, anteriormente, solo se podía asociar una de estas con la Tienda Windows para empresas. Ahora puede asociar varias herramientas de administración con la tienda, por ejemplo, Intune y Configuration Manager.

Incorpore la cuenta de la tienda a Configuration Manager.

1. Asegúrese de que ha comprado al menos una aplicación en la Tienda Windows para empresas. En el área de trabajo **Administración** de la consola de Configuration Manager, expanda **Cloud Services** y, luego, seleccione **Tienda Windows para empresas**.
2.  En la pestaña **Inicio**, en el grupo **Tienda Windows para empresas**, seleccione **Add Windows Store for Business Account** (Agregar cuenta de la Tienda Windows para empresas).
3.  Agregue el identificador de inquilino, el identificador de cliente y la clave de secreto de cliente de Azure Active Directory y, después, finalice el asistente.
4. Una vez que haya terminado, verá la cuenta configurada en la lista **Tienda Windows para empresas** en la consola de Configuration Manager.

Cambie los idiomas de aplicación que se mostrarán en el catálogo de aplicaciones para que los descarguen los usuarios.

1.    En el área de trabajo **Administración** de la consola de Configuration Manager, seleccione **Cloud Services** > **Actualizaciones y mantenimiento** > **Tienda Windows para empresas**.
2.    Seleccione su cuenta de la Tienda Windows para empresas y haga clic en **Propiedades**.
3.    Seleccione la pestaña **Idioma**.
4.    Agregue o quite los idiomas que se mostrarán en el catálogo de aplicaciones. Seleccione el idioma del catálogo de aplicaciones predeterminado que estará disponible para los usuarios.

>[!IMPORTANT]
>En esta versión, si cambia los idiomas que se van a sincronizar, debe reiniciar el servicio SMS Executive en el servidor de sitio para que la configuración de idioma surta efecto.


Modifique la clave de secreto de cliente de Azure Active Directory.

1.    En el área de trabajo **Administración** de la consola de Configuration Manager, seleccione **Cloud Services** > **Actualizaciones y mantenimiento** > **Tienda Windows para empresas**.
2.    Seleccione su cuenta de la Tienda Windows para empresas y haga clic en **Propiedades**.
3.    En el cuadro de diálogo **Windows Store for Business Account Properties** (Propiedades de la cuenta de la Tienda Windows para empresas), escriba una nueva clave en el campo **Client secret key** (Clave de secreto de cliente) y seleccione **Comprobar**. Una vez comprobada, seleccione **Aplicar** y cierre el cuadro de diálogo.

## <a name="sync-apps-from-the-store-with-configuration-manager"></a>Sincronizar aplicaciones de la tienda con Configuration Manager

La sincronización se produce cada 24 horas, pero puede iniciar una sincronización inmediata mediante el procedimiento siguiente:

1. En el área de trabajo **Administración** de la consola de Configuration Manager, seleccione **Cloud Services** > **Actualizaciones y mantenimiento** > **Tienda Windows para empresas**.
3.    En la pestaña **Inicio**, en el grupo **Sincronizar**, seleccione **Sincronizar ahora**.
4.    La aplicación que ha comprado aparecerá en el nodo **License Information for Store Apps** (Información de licencia para las aplicaciones de la Tienda) del área de trabajo **Administración de aplicaciones**.


## <a name="create-and-deploy-a-configuration-manager-application-from-a-windows-store-for-business-app"></a>Crear e implementar una aplicación de Configuration Manager a partir de una aplicación de la Tienda Windows para empresas

En este procedimiento se da por supuesto que ha adquirido al menos una aplicación gratuita o ha comprado al menos una aplicación con licencia en línea de pago a través de la Tienda Windows para empresas.

1.  En el área de trabajo **Biblioteca de software** de la consola de Configuration Manager, expanda **Administración de aplicaciones** y, luego, seleccione **License Information for Store Apps** (Información de licencia para las aplicaciones de la Tienda).
2.  Elija la aplicación que quiere implementar y, luego, en la pestaña **Inicio**, en el grupo **Crear**, seleccione **Crear aplicación**.
Se crea una aplicación de Configuration Manager que contiene la aplicación de la Tienda Windows para empresas. Luego puede implementar y supervisar esta aplicación como lo haría con cualquier otra aplicación de Configuration Manager.

> [!IMPORTANT]
> En el caso de los dispositivos inscritos en Intune, las aplicaciones implementadas solo están disponibles para el usuario que originalmente haya inscrito el dispositivo. Ningún otro usuario puede usar la aplicación.

## <a name="monitor-windows-store-for-business-apps"></a>Supervisión de las aplicaciones de la Tienda Windows para empresas

En el área de trabajo **Biblioteca de software**, expanda **Administración de aplicaciones** y, luego, seleccione **License Information for Store Apps** (Información de licencia para las aplicaciones de la Tienda).

Para cada aplicación de la tienda que administre, podrá ver información sobre la aplicación, incluido su nombre, la plataforma y el número de licencias para la aplicación que posee, así como el número de licencias que tiene disponibles.



<!--HONumber=Feb17_HO3-->


