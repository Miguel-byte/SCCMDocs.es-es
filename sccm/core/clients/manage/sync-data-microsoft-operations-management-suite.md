---
title: "Sincronización de datos | Microsoft Operations Management Suite | System Center Configuration Manager"
description: Sincronice datos de System Center Configuration Manager con Microsoft Operations Management Suite.
ms.custom: na
ms.date: 10/13/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 33bcf8b3-a6b6-4fc9-bb59-70a9621b2b0d
caps.latest.revision: 9
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 0fbce476b8a9b91a88354fb4abfadfd2526ca5e8
ms.openlocfilehash: 5786f0734ce186601f5173003b9b133ed6ae8b11

---
# <a name="sync-data-from-configuration-manager-to-the-microsoft-operations-management-suite"></a>Sincronizar datos de Configuration Manager con Microsoft Operations Management Suite

*Se aplica a: System Center Configuration Manager (rama actual)*

Puede usar el conector de Microsoft Operations Management Suite (OMS) para sincronizar datos como recopilaciones de System Center Configuration Manager con OMS. De este modo, los datos de la implementación de Configuration Manager estarán visibles en OMS.

## <a name="add-an-oms-connection-to-configuration-manager"></a>Agregar una conexión de OMS en Configuration Manager

Para agregar una conexión de OMS, primero, el entorno de Configuration Manager debe configurar un [punto de conexión de servicio](../../../core/servers/deploy/configure/about-the-service-connection-point.md) en un [modo en línea](https://azure.microsoft.com/en-us/documentation/articles/resource-group-create-service-principal-portal/). Al agregar una conexión de OMS en el entorno, también se instala Microsoft Monitoring Agent en el equipo que ejecuta este rol de sistema de sitio.
1.  En el área de trabajo **Administración**, seleccione **Conector de OMS**. En la cinta, haga clic en "Crear conexión con Operations Management Suite". Se abrirá el **Asistente para conexión a Operations Management Suite**. Seleccione **Siguiente**.
2.  En la pantalla **General**, confirme que tiene la siguiente información y después seleccione **Siguiente**.

    * Registró Configuration Manager como una herramienta de administración de "Aplicación web y/o API web" y tiene el [identificador de cliente de este registro](https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/).
    * Creó una clave de cliente para la herramienta de administración registrada en Azure Active Directory.
    * En el Portal de administración de Azure, proporcionó la aplicación web registrada con permiso de acceso a OMS, como se describe en [Concesión de permisos a Configuration Manager para acceder a OMS](https://azure.microsoft.com/en-us/documentation/articles/log-analytics-sccm/#provide-configuration-manager-with-permissions-to-oms).

3.  En la pantalla **Azure Active Directory**, proporcione el **Inquilino**, **Id. de cliente** y la **Clave secreta de cliente** para configurar la conexión con OMS y después seleccione **Siguiente**.
4.  En la pantalla **Configuración de conexión de OMS**, rellene la **Suscripción de Azure**, el **Grupo de recursos de Azure** y el **Área de trabajo de Operations Management Suite** para proporcionar la configuración de la conexión.
5.  Compruebe la configuración de la conexión en la pantalla **Resumen** y luego seleccione **Siguiente**. En la pantalla **Progreso**, se mostrará el estado de la conexión y después debería seleccionar **Completar**.

> [!NOTE]
> Debe conectarse OMS con el sitio de nivel superior de la jerarquía. Si conecta OMS con un sitio primario independiente y después agrega un sitio de administración central al entorno, debe eliminar y volver a crear la conexión de OMS dentro de la nueva jerarquía.

Después de haber vinculado Configuration Manager con OMS, puede agregar o quitar recopilaciones y ver las propiedades de la conexión de OMS.

## <a name="viewing-microsoft-operations-management-suite-connection-properties-in-configuration-manager"></a>Ver propiedades de conexión de Microsoft Operations Management Suite en Configuration Manager

1.  Vaya a **Cloud Services** y después seleccione **Conector de OMS** para abrir la página **Propiedades de conexión a OMS**.
2.  En esta página hay dos pestañas:
  * En la pestaña **Azure Active Directory**, se muestra el **Inquilino**, **Id. de cliente** y la **Expiración de la clave secreta de cliente** y le permite **Comprobar** si ha expirado la **Clave secreta de cliente**.
  * En la pestaña **Propiedades de conexión a OMS**, se muestra la **Suscripción de Azure**, el **Grupo de recursos de Azure**, el **Área de trabajo de Operations Management Suite** y una lista de **recopilaciones de dispositivos de los que Operations Management Suite puede obtener datos**. Use los botones **Agregar** y **Quitar** para modificar las recopilaciones que se admiten.



<!--HONumber=Nov16_HO1-->


