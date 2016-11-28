---
title: "Administración de aplicaciones desde la Tienda Windows para empresas | System Center Configuration Manager"
description: Administre e implemente aplicaciones desde la Tienda Windows para empresas con System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
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
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 1e293b2ec4debf7a8513f1e3544ac234616f04d7

---
# <a name="manage-apps-from-the-windows-store-for-business-with-system-center-configuration-manager"></a>Administración de aplicaciones desde la Tienda Windows para empresas con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

La [Tienda Windows para empresas](https://www.microsoft.com/business-store) es el lugar donde puede buscar y adquirir aplicaciones de Windows para su organización, individualmente o por volumen. Al conectar el almacén a Configuration Manager, puede sincronizar la lista de aplicaciones que haya adquirido con Configuration Manager, verlas en la consola de Configuration Manager e implementarlas como lo haría con cualquier otra aplicación.


## <a name="online-and-offline-apps"></a>Aplicaciones en línea y sin conexión

La Tienda Windows para empresas admite dos tipos de aplicaciones:

- **En línea**: este tipo de licencia requiere que usuarios y dispositivos se conecten a la tienda para obtener una aplicación y su licencia. Los dispositivos de Windows 10 deben estar unidos a un dominio de Azure Active Directory.
- **Sin conexión**: las organizaciones pueden almacenar en caché las aplicaciones y licencias para implementarlas directamente en su red local, sin necesidad de conectarse a la tienda o tener una conexión a Internet.

[Obtenga más información](https://technet.microsoft.com/itpro/windows/whats-new/windows-store-for-business-overview) acerca de la Tienda Windows para empresas.

Configuration Manager admite la administración de aplicaciones de la Tienda Windows para empresas tanto en dispositivos de Windows 10 que ejecutan el cliente de Configuration Manager como en los dispositivos de Windows 10 inscritos a Microsoft Intune (en lo que se conoce como configuración híbrida). Configuration Manager ofrece las siguientes funciones para las aplicaciones en línea y sin conexión.

> [!IMPORTANT]
> Para utilizarlas, los dispositivos de Windows 10 deben ejecutar la versión de noviembre de 2015 (1511) o una posterior.

|Capacidad|Aplicaciones sin conexión|Aplicaciones en línea|
|------------|------------|------------|
|Sincronizar datos de la aplicación en Configuration Manager<br>(la sincronización se produce cada 24 horas)|Sí|Sí|
|Crear aplicaciones de Configuration Manager desde las aplicaciones de la tienda|Sí|Sí|
|Compatibilidad con las aplicaciones gratuitas de la tienda|Sí|Sí|
|Compatibilidad con las aplicaciones de pago de la tienda|No|No|
|Compatibilidad con las implementaciones necesarias para las colecciones de usuarios o dispositivos|Sí|Sí<sup>1</sup>|
|Compatibilidad con las implementaciones disponibles para las colecciones de usuarios o dispositivos|Sí<sup>3</sup>|No<sup>2</sup>|

<sup>1</sup>Admite solo dispositivos administrados por Intune. Aunque no se le impide la creación de una aplicación en línea en la consola de Configuration Manager y su implementación en un dispositivo administrado por el cliente de Configuration Manager, esto no funcionará. Se dirigirá al usuario final a la página correspondiente de la tienda de aplicaciones desde donde debe instalar la aplicación manualmente.

<sup>2</sup>Las aplicaciones en línea se pueden implementar como disponibles para las colecciones de usuarios o dispositivos solo para los dispositivos administrados por Configuration Manager, pero si el usuario final selecciona la aplicación en el Centro de software, se le dirigirá a la Tienda Windows para empresas, donde tendrá que instalar la aplicación manualmente. No se admiten las implementaciones disponibles para dispositivos inscritos con Microsoft Intune.

<sup>3</sup>No se admite para los dispositivos administrados por Intune.

> [!IMPORTANT]
> En esta versión, si tiene una jerarquía de Configuration Manager que contiene un sitio de administración central y al menos un sitio primario, se producirá un error en la implementación de aplicaciones sin conexión de la Tienda Windows para empresas en dispositivos administrados por Intune.


## <a name="activate-the-windows-store-for-business-capability"></a>Activación de la función de la Tienda Windows para empresas
Dado que esta es una característica de la versión preliminar, antes de conectar Configuration Manager con la Tienda de Windows para empresas, debe realizar los pasos siguientes:

**Dar su consentimiento para utilizar las características de la versión preliminar**
1. En el área de trabajo **Administración** de la consola de Configuration Manager, haga clic en **Configuración del sitio** > **Sitios**.
2. Seleccione el sitio de nivel superior en la jerarquía y, a continuación, abra **Configuración de jerarquía**.
3. En el cuadro de diálogo **Propiedades de configuración de jerarquía** diálogo cuadro, active la casilla **Consentimiento para usar características de versiones preliminares**.
4. Haga clic en **Aceptar**.

**Activación de la función de la Tienda Windows para empresas**
1. En el área de trabajo **Administración** de la consola de Configuration Manager, haga clic en **Servicios de nube** > **Actualizaciones y mantenimiento** > **Características**.
2. Seleccione **Integración con la Tienda Windows para empresas**, luego, en la pestaña **Inicio**, en el grupo **Características**, haga clic en **Activar**.
3. Cierre y abra la consola de Configuration Manager de nuevo.
4. Ahora verá el nodo **Tienda Windows para empresas** en el área de trabajo **Administración** bajo **Servicios de nube**.

## <a name="set-up-windows-store-for-business-synchronization"></a>Configuración de la sincronización de la Tienda Windows para empresas

**En Azure Active Directory, registre Configuration Manager como una herramienta de administración "Aplicación web y/o API web". De este modo, obtendrá un identificador de cliente que necesitará más adelante.**
1. En el nodo de Active Directory de [https://manage.windowsazure.com](https://manage.windowsazure.com), seleccione Azure Active Directory y luego haga clic en **Aplicaciones** > **Agregar**.
2.  Haga clic en **Agregar una aplicación que mi organización está desarrollando**.
3.  Escriba un nombre para la aplicación, seleccione **Aplicación web** y/o **API web** y haga clic en la flecha **Siguiente**.
4.  Escriba la misma dirección URL para **URL de inicio de sesión** y **URI de id. de aplicación**. La dirección URL puede ser cualquiera (no es necesario que se resuelva en una dirección real). Por ejemplo, puede escribir *https://yourdomain/sccm*.
5.  Complete el asistente.

**En Azure Active Directory, cree una clave de cliente para la herramienta de administración registrada.**
1.  Resalte la aplicación que acaba de crear y haga clic en **Configurar**.
2.  En **Claves**, seleccione una duración de la lista y haga clic en **Guardar**. De este modo, se creará una nueva clave de cliente. No salga de esta página hasta que haya incorporado correctamente la Tienda Windows para empresas a Configuration Manager.

**En la Tienda Windows para empresas, configure Configuration Manager como la herramienta de administración de la tienda.**
1.  Abra [https://businessstore.microsoft.com/en-us/managementtools](https://businessstore.microsoft.com/en-us/managementtools) e inicie sesión si se le solicita.
2.  Si se le solicita, acepte los términos de uso.
3.  Bajo **Herramientas de administración**, haga clic en **Add a management tool** (Agregar una herramienta de administración).
4.  En **Buscar la herramienta por nombre**, escriba el nombre de la aplicación que creó anteriormente en AAD y luego haga clic en **Agregar**.
5.  Haga clic en **Activar** junto a la aplicación que acaba de importar.
6.  En la página **Administrar > Información de la cuenta**, seleccione **Show Offline-Licensed Apps** (Mostrar aplicaciones con licencia sin conexión) si desea permitir la adquisición de aplicaciones con licencias sin conexión.

**Incorporación de la cuenta de la tienda a Configuration Manager**

1. Asegúrese de que dispone de al menos una aplicación de la Tienda Windows para empresas. En el área de trabajo **Administración** de la consola de Configuration Manager, expanda **Servicios de nube** y, a continuación, haga clic en **Tienda Windows para empresas**.
2.  En la pestaña **Inicio**, en el grupo **Tienda Windows para empresas**, haga clic en **Agregar cuenta de la Tienda Windows para empresas**.
3.  Agregue el identificador de inquilino, el identificador de cliente y la clave de cliente de Azure Active Directory y finalice el asistente.
4. Una vez que haya terminado, verá la cuenta configurada en la lista **Tienda Windows para empresas** en la consola de Configuration Manager.


## <a name="create-and-deploy-a-configuration-manager-application-from-a-windows-store-for-business-app"></a>Cree e implemente una aplicación de Configuration Manager a partir de una aplicación de la Tienda Windows para empresas.
1.  En el área de trabajo **Biblioteca de software** de la consola de Configuration Manager, expanda **Administración de aplicaciones** y luego haga clic en **Información de licencia para las aplicaciones de la Tienda**.
2.  Elija la aplicación que quiere implementar y, luego, en la pestaña **Inicio**, en el grupo **Crear**, haga clic en **Crear aplicación**.
Se crea una aplicación de Configuration Manager que contiene la aplicación de la Tienda Windows para empresas. Luego puede implementar y supervisar esta aplicación como lo haría con cualquier otra aplicación de Configuration Manager.

> [!IMPORTANT]
> En el caso de los dispositivos inscritos en Intune, las aplicaciones implementadas solo están disponibles para el usuario que originalmente haya inscrito el dispositivo. Ningún otro usuario puede tener acceso a la aplicación.

## <a name="monitor-windows-store-for-business-apps"></a>Supervisión de las aplicaciones de la Tienda Windows para empresas

En el área de trabajo **Biblioteca de software**, expanda **Administración de aplicaciones** y luego haga clic en **Información de licencia para las aplicaciones de la Tienda**.

Para cada aplicación de la tienda que administre, podrá ver información acerca de la aplicación, incluido su nombre, plataforma y número de licencias para la aplicación que posee, así como el número de licencias que tiene disponibles.



<!--HONumber=Nov16_HO1-->


