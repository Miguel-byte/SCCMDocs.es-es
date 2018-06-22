---
title: 'Inscripción de dispositivos con el Administrador de inscripción de dispositivos '
titleSuffix: Configuration Manager
description: Inscriba dispositivos de la empresa con la cuenta del administrador de inscripción de dispositivos con System Center Configuration Manager.
ms.date: 09/08/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 2905f26e-7859-497d-b995-5ff48261efa2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9a691bc98a26cdf56d22c03840997d9e0a380b7b
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32347627"
---
# <a name="enroll-devices-with-device-enrollment-manager-with-configuration-manager"></a>Inscribir dispositivos con el administrador de inscripción de dispositivos con Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Las organizaciones pueden usar Intune para administrar un gran número de dispositivos móviles con una sola cuenta de usuario. La cuenta del *administrador de inscripción de dispositivos* (DEM) es una cuenta de usuario especial utilizada para inscribir dispositivos. Agregue usuarios existentes a la cuenta de DEM para ofrecerles funcionalidades DEM especiales. Cada dispositivo inscrito usa una sola licencia. Se recomienda que use dispositivos inscritos a través de esta cuenta como dispositivos compartidos sin afinidad de usuario, en lugar de dispositivos dedicados personales.  

## <a name="enroll-corporate-owned-devices-with-the-device-enrollment-manager"></a>Inscribir dispositivos propiedad de la empresa con el administrador de inscripción de dispositivos  
 Puede asignar un administrador o supervisor de almacén, por ejemplo, una cuenta de usuario de administrador de inscripción de dispositivos que le permita hacer lo siguiente:  

-   Inscribir hasta 1000 dispositivos para la administración  
-   Usar la aplicación de portal de empresa para instalar aplicaciones de empresa  
-   Configurar el acceso a los datos de la empresa  

Las limitaciones siguientes se aplican a los dispositivos que se administran mediante una cuenta de administrador de inscripción de dispositivos:

- El administrador del almacén no puede restablecer el dispositivo desde el portal de empresa.  
- Los dispositivos no pueden estar unidos al área de trabajo ni a Azure Active Directory. Esto impide que estos dispositivos usen el acceso condicional.
-  Para implementar aplicaciones de empresa en dispositivos administrados con el administrador de inscripción de dispositivos, implemente la aplicación de portal de empresa como una **instalación requerida** en la cuenta de usuario del administrador de inscripción de dispositivos. Después, el administrador de inscripción de dispositivos puede iniciar la aplicación de portal de empresa para instalar aplicaciones adicionales.
- Para mejorar el rendimiento, en la aplicación de portal de empresa solo se muestra el dispositivo local. La administración remota de otros dispositivos DEM solo puede llevarla a cabo un administrador desde la consola de Configuration Manager.
- El sitio web del portal de empresa no está disponible para cuentas de administrador de inscripción de dispositivos. Use la aplicación de portal de empresa.
- Si usa DEM para inscribir dispositivos iOS, no puede usa Apple Configurator ni el Programa de inscripción de dispositivos (DEP) de Apple para inscribir dispositivos. (Solo iOS) 

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
La eliminación de un administrador de inscripción de dispositivos no afecta a los dispositivos inscritos. Cuando se elimina un administrador de inscripción de dispositivos:  
- No se ha anulado la inscripción de ningún dispositivo inscrito  
- Los dispositivos inscritos se continuarán administrando de manera completa  
- Las credenciales de la cuenta del administrador de inscripción de dispositivos eliminado siguen siendo válidas para iniciar sesión en el portal de empresa y acceder a las aplicaciones.  
- Las credenciales de la cuenta del administrador de inscripción de dispositivos eliminado todavía no pueden borrar ni retirar dispositivos  
- La relación de la cuenta del administrador de inscripción de dispositivos eliminado se mantiene pero no se pueden inscribir dispositivos adicionales

1.  En la consola de Configuration Manager, haga clic en **Administración**.  
2.  En el área de trabajo **Administración** , expanda **Servicios en la nube**y haga clic en **Suscripciones de Microsoft Intune**. Seleccione la suscripción a Microsoft Intune a la que agregará un administrador de inscripción de dispositivos y, después, haga clic en **Propiedades**.  
3.  En el cuadro de diálogo Propiedades de Suscripción a Microsoft Intune, haga clic en la pestaña **Administrador de inscripción de dispositivos**.  
4.  **Busque** el administrador de inscripción de dispositivos que quiere eliminar, haga clic en **Quitar** y, luego, en **Aceptar**.  
