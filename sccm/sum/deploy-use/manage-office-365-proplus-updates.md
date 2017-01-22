---
title: Administrar las actualizaciones de Office 365 ProPlus | Microsoft Docs
description: "Configuration Manager sincroniza las actualizaciones de cliente de Office 365 desde el catálogo WSUS en el servidor de sitio para que las actualizaciones estén disponibles para su implementación en los clientes."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 11/10/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: eac542eb-9aa1-4c63-b493-f80128e4e99b
translationtype: Human Translation
ms.sourcegitcommit: 5415bfa0ac4af14891a9445cdeab6a4509fffc38
ms.openlocfilehash: 630ccdf7b7f45a88586c9ab530c164985267bec9

---

# <a name="manage-office-365-proplus-updates-with-configuration-manager"></a>Administración de actualizaciones de Office 365 ProPlus con Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

A partir de la versión 1602, Configuration Manager tiene la capacidad de administrar las actualizaciones del cliente de Office 365 mediante el flujo de trabajo de administración de actualizaciones de software. Cuando Microsoft publica una nueva actualización de cliente de Office 365 en Content Delivery Network (CDN) de Office, Microsoft también publica un paquete de actualización para Windows Server Update Services (WSUS). Después de que Configuration Manager sincroniza la actualización de cliente de Office 365 desde el catálogo WSUS en el servidor de sitio, la actualización está disponible para implementarla en los clientes.

## <a name="office-365-client-management-dashboard"></a>Panel de administración de clientes de Office 365  
A partir de Configuration Manager versión 1610, el panel de administración de clientes de Office 365 está disponible en la consola de Configuration Manager. Para ver el panel, vaya a **Biblioteca de software** > **Información general** > **Administración de clientes de Office 365**.

<!--- >[!NOTE]
>In the **What's New** workspace in the Configuration Manager console, the new dashboard is incorrectly named **Office 365 Servicing dashboard**. --->

El panel muestra gráficos para lo siguiente:

- Número de clientes de Office 365
- Versiones de cliente de Office 365
- Idiomas de cliente de Office 365
- Canales de cliente de Office 365     
Para más información, vea [Información general de los canales de actualización para Office 365 ProPlus](https://technet.microsoft.com/library/mt455210.aspx).
<!--- - Automatic deployment rules with Office 365 apps (have Office 365 Client selected in the set of available products). --->

<!---You can take the following actions on the dashboard:
- --->

En la parte superior del panel, use la opción desplegable **Colección** para filtrar los datos del panel por miembros de una colección determinada.

<!---
 On the upper-right side of the dashboard, click **Office 365 Installer** to start the Office 365 Client Installation Wizard to deploy Office 365 apps to clients. For details, see [Deploy Office 365 apps to clients](#deploy-office-365-apps-to-clients).
- On the middle-right side of the dashboard, click **Create an ADR** to open the Automatic Deployment Rule Wizard to create a new automatic deployment rule (ADR). To create an ADR for Office 365 apps, select **Office 365 Client** when you choose the product. For more information, see [Automatically deploy software updates](/sccm/sum/deploy-use/automatically-deploy-software-updates).
- On the lower-right side of the dashboard, click **Create Client Agent Settings** to open Client Agent settings. For more information, see [About client settings](/sccm/core/clients/deploy/about-client-settings).
--->

#### <a name="to-deploy-office-365-updates-with-configuration-manager"></a>Para implementar actualizaciones de Office 365 con Configuration Manager
Siga estos pasos para implementar actualizaciones de Office 365 con Configuration Manager:

1.  [Compruebe los requisitos](https://technet.microsoft.com/library/mt628083.aspx) para usar Configuration Manager para administrar las actualizaciones de cliente de Office 365 en la sección **Requisitos para usar Configuration Manager para administrar las actualizaciones de cliente de Office 365** del tema.  

2.  [Configurar puntos de actualización de software](../get-started/configure-classifications-and-products.md) para sincronizar las actualizaciones de cliente de Office 365. Definir las **actualizaciones** para la clasificación y seleccionar el **cliente de Office 365** para el producto. Es posible que deba sincronizar actualizaciones de software al menos una vez antes de que el producto Office 365 Client esté disponible para elegirlo. Debe sincronizar las actualizaciones de software después de configurar los puntos de actualización de software para usar la clasificación **Actualizaciones**.  

3.  Permita que los clientes de Office 365 reciban actualizaciones de Configuration Manager. Puede hacerlo mediante la configuración de cliente de Configuration Manager o la directiva de grupo. Utilice uno de los métodos siguientes para habilitar el cliente:  
    - Método 1: a partir de Configuration Manager versión 1606, puede usar la configuración de cliente de Configuration Manager para administrar el agente cliente de Office 365. Después de configurar esta opción e implementar las actualizaciones de Office 365, el agente cliente de Configuration Manager se comunica con el de Office 365 para descargar las actualizaciones de Office 365 desde un punto de distribución e instalarlas. Configuration Manager realiza un inventario de la configuración de cliente de Office 365 ProPlus.
      1.  En la consola de Configuration Manager, haga clic en **Administración** > **Información general** > **Configuración de cliente**.  

      2.  Abra la configuración de dispositivo adecuada para habilitar el agente cliente. Para más información sobre las configuraciones de cliente personalizada y predeterminada, vea [Cómo establecer la configuración del cliente en Configuration Manager](../../core/clients/deploy/configure-client-settings.md).  

      3.  Haga clic en **Actualizaciones de software** y seleccione **Sí** para el valor **Habilitar administración del Agente cliente de Office 365**.  

    - Método 2: [permitir a los clientes de Office 365 recibir actualizaciones](https://technet.microsoft.com/library/mt628083.aspx#BKMK_EnableClient) de Configuration Manager mediante la herramienta de implementación de Office o la directiva de grupo.  

4. [Implemente actualizaciones de Office 365](deploy-software-updates.md) en los clientes.  

<!--- ## Next steps
Use the Office 365 Client Management dashboard in Configuration Manager to review Office 365 client information and deploy Office 365 apps. For details, see [Manage Office 365 apps](manage-office-365-apps.md). --->



<!--HONumber=Dec16_HO3-->


