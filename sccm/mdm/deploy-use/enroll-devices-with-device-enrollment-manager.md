---
title: "Inscribir dispositivos con el administrador de inscripción de dispositivos en Configuration Manager | Microsoft Docs"
description: "Inscriba dispositivos de la empresa con la cuenta del administrador de inscripción de dispositivos con System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2905f26e-7859-497d-b995-5ff48261efa2
caps.latest.revision: 8
author: mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 991eff171dce95590a7f050e0d3b07f98c0224b3
ms.openlocfilehash: b356d2351b8a28bdca78176fdf0ff3c913a36bd3


---
# <a name="enroll-devices-with-device-enrollment-manager-with-configuration-manager"></a>Inscribir dispositivos con el administrador de inscripción de dispositivos con Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Las organizaciones pueden usar System Center Configuration Manager e Intune para administrar un gran número de dispositivos móviles con una sola cuenta de usuario. La cuenta del *administrador de inscripción de dispositivos* es una cuenta especial de Intune con permisos para inscribir más de cinco dispositivos.  

## <a name="enroll-corporate-owned-devices-with-the-device-enrollment-manager"></a>Inscribir dispositivos propiedad de la empresa con el administrador de inscripción de dispositivos  
 Puede asignar un administrador o supervisor de almacén, por ejemplo, una cuenta de usuario de administrador de inscripción de dispositivos que le permita hacer lo siguiente:  

-   Inscribir dispositivos para la administración  

-   Usar la aplicación de portal de empresa para instalar aplicaciones de empresa  

-   Instalar y desinstalar software  

-   Configurar el acceso a los datos de la empresa  


Las limitaciones siguientes se aplican a los dispositivos que se administran mediante una cuenta de administrador de inscripción de dispositivos:

- El administrador del almacén no puede restablecer el dispositivo desde el portal de empresa.  
-  Los dispositivos no pueden estar unidos al área de trabajo ni a Azure Active Directory. Esto impide que estos dispositivos usen el acceso condicional.
-  Para implementar aplicaciones de empresa en dispositivos administrados con el administrador de inscripción de dispositivos, implemente la aplicación de portal de empresa como una **instalación requerida** en la cuenta de usuario del administrador de inscripción de dispositivos. Después, el administrador de inscripción de dispositivos puede iniciar la aplicación de portal de empresa para instalar aplicaciones adicionales.
- Para mejorar el rendimiento, en la aplicación de portal de empresa solo se muestra el dispositivo local. La administración remota de otros dispositivos DEM solo puede llevarla a cabo un administrador desde la consola de Configuration Manager.
- El sitio web del portal de empresa no está disponible para cuentas de administrador de inscripción de dispositivos. Use la aplicación de portal de empresa.

 **Ejemplos de escenario de administrador de inscripción de dispositivos:**   
Un restaurante quiere tabletas de punto de venta para los camareros y monitores de pedidos para el personal de cocina. Los empleados no necesitan nunca acceder a los datos de la empresa ni iniciar sesión como usuario. El administrador de Intune crea una cuenta de administrador de inscripción de dispositivos e inscribe los dispositivos propiedad de la empresa usando esa cuenta. El administrador también podría dar las credenciales de inscripción de dispositivos a un responsable del restaurante, para que pueda inscribir y administrar los dispositivos.  

 El administrador puede implementar aplicaciones específicas de cada rol en los dispositivos del restaurante. Un administrador también puede seleccionar un dispositivo en la consola y retirarlo de la administración de dispositivos móviles.  

#### <a name="add-a-device-enrollment-manager"></a>Agregar un administrador de inscripción de dispositivos  

1.  En la consola de Configuration Manager, haga clic en **Administración**.  

2.  En el área de trabajo **Administración** , expanda **Servicios en la nube**y haga clic en **Suscripciones de Microsoft Intune**. Seleccione la suscripción a Microsoft Intune a la que agregará un administrador de inscripción de dispositivos y, después, haga clic en **Propiedades**.  

3.  En el cuadro de diálogo Propiedades de Suscripción a Microsoft Intune, haga clic en la pestaña **Administrador de inscripción de dispositivos**.  

4.  Haga clic en **Agregar o quitar**.  

5.  En el cuadro de diálogo **Administrador de inscripción de dispositivos**, escriba el nombre de usuario del usuario que quiere agregar como administrador de inscripción de dispositivos y, después, haga clic en **Buscar**. Seleccione el usuario que quiere agregar como administrador de inscripción de dispositivos y haga clic en **Agregar**.  

6.  Confirme la cuenta de usuario que se usará como administrador de inscripción de dispositivos y haga clic en **Agregar o quitar**.  Se requiere una licencia de suscripción para cada usuario que acceda al servicio y el *administrador de inscripción de dispositivos* no puede ser un administrador de Intune. Determine si necesita agregar más licencias antes de usar esta característica.  

7.  El administrador de inscripción de dispositivos puede inscribir ahora dispositivos móviles siguiendo el mismo procedimiento que un usuario final usa para un escenario de BYOD (Bring Your Own Device) en el portal de empresa.  

#### <a name="delete-a-device-enrollment-manager-from-intune"></a>Eliminar un administrador de inscripción de dispositivos de Intune  

1.  En la consola de Configuration Manager, haga clic en **Administración**.  

2.  En el área de trabajo **Administración** , expanda **Servicios en la nube**y haga clic en **Suscripciones de Microsoft Intune**. Seleccione la suscripción a Microsoft Intune a la que agregará un administrador de inscripción de dispositivos y, después, haga clic en **Propiedades**.  

3.  En el cuadro de diálogo Propiedades de Suscripción a Microsoft Intune, haga clic en la pestaña **Administrador de inscripción de dispositivos**.  

4.  **Busque** el administrador de inscripción de dispositivos que quiere eliminar, haga clic en **Quitar** y, luego, en **Aceptar**.  

 La eliminación de un administrador de inscripción de dispositivos no afecta a los dispositivos inscritos. Cuando se elimina un administrador de inscripción de dispositivos:  

-   Ningún dispositivo inscrito se ve afectado  

-   Los dispositivos inscritos se continuarán administrando de manera completa  

-   Las credenciales de la cuenta del administrador de inscripción de dispositivos eliminado siguen siendo válidas para iniciar sesión en el portal de empresa y acceder a las aplicaciones.  

-   Las credenciales de la cuenta del administrador de inscripción de dispositivos eliminado todavía no pueden borrar ni retirar dispositivos  

-   La relación de la cuenta del administrador de inscripción de dispositivos eliminado se mantiene pero no se pueden inscribir dispositivos adicionales



<!--HONumber=Jan17_HO4-->


