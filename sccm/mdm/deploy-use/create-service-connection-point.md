---
title: "Creación de un punto de conexión de servicio mediante System Center Configuration Manager | Microsoft Docs"
description: "Cree un punto de conexión de servicio mediante System Center Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 617abb22-d22f-41fb-a76b-1c4259e419d2
caps.latest.revision: 18
caps.handback.revision: 0
author: mtillman
ms.author: mtillman
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: 9a21d02cb2a50162e5de50481f0f27f2dd7a616c
ms.contentlocale: es-es
ms.lasthandoff: 05/17/2017

---
# <a name="create-a-service-connection-point-with-system-center-configuration-manager-and-microsoft-intune"></a>Creación de un punto de conexión de servicio con System Center Configuration Manager y Microsoft Intune

*Se aplica a: System Center Configuration Manager (rama actual)*

Una vez creada la suscripción, puede instalar el rol de sistema de sitio del punto de conexión de servicio que le permite conectarse al servicio de Intune. Este rol de sistema de sitio insertará configuraciones y aplicaciones en el servicio de Intune.

 El punto de conexión de servicio envía información de configuración e implementación de software a Configuration Manager y recupera mensajes de inventario y estado de dispositivos móviles. El servicio Configuration Manager actúa como una puerta de enlace que se comunica con los dispositivos móviles y almacena la configuración.

> [!NOTE]
>  El rol del sistema de sitio del punto de conexión de servicio solo se debe instalar en un sitio de administración central o en un sitio primario independiente. El punto de conexión de servicio debe tener acceso a Internet.


## <a name="configure-the-service-connection-point-role"></a>Configurar el rol de punto de conexión de servicio

1.  En la consola de Configuration Manager, haga clic en **Administración**.

2.  En el área de trabajo **Administración**, expanda **Sitios** y después haga clic en **Servidores y roles del sistema de sitios**.

3.  Agregue el rol **Punto de conexión de servicio** a un servidor de sistema de sitio nuevo o existente mediante la etapa asociada:

    -   Nuevo servidor de sistema de sitio: en la pestaña **Inicio** , del grupo **Crear** , haga clic en **Crear servidor del sistema de sitio** para iniciar el asistente para creación de servidor de sistema de sitio.

    -   Servidor de sistema de sitio existente: haga clic en el servidor en el que quiere instalar el rol de punto de conexión de servicio. A continuación, en la pestaña **Inicio** , en el grupo **Servidor** , haga clic en **Agregar roles del sistema de sitio** para iniciar el Asistente para agregar roles de sistema de sitio.

4.  En la página **Selección de rol del sistema** , seleccione **Punto de conexión de servicio**y haga clic en **Siguiente**.
![Crear un punto de conexión de servicio](../media/mdm-service-connection-point.png)

* Complete el asistente.

## <a name="how-does-the-service-connection-point-authenticate-with-the-microsoft-intune-service"></a>¿Cómo se autentica el punto de conexión de servicio con el servicio de Microsoft Intune?
 El punto de conexión de servicio amplía Configuration Manager; para ello, establece una conexión con el servicio de Intune basado en la nube, que administra los dispositivos móviles mediante Internet. El punto de conexión de servicio se autentica con el servicio de Intune de la manera siguiente:

1.  Cuando se crea una suscripción a Intune en la consola de Configuration Manager, el administrador de Configuration Manager se autentica mediante la conexión a Azure Active Directory, que lo redirige al servidor de ADFS correspondiente para solicitar el nombre de usuario y la contraseña. Después, Intune emite un certificado para el inquilino.

2.  El certificado de la etapa 1 se instala en el rol de sitio del punto de conexión de servicio, y se usa para autenticar y autorizar la comunicación posterior con el servicio de Microsoft Intune.

> [!div class="button"]
[< Paso anterior](terms-and-conditions.md)  [Paso siguiente >](enable-platform-enrollment.md)

