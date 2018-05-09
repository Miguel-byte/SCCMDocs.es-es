---
title: Características y funcionalidades
titleSuffix: Configuration Manager
description: Obtenga información sobre las funcionalidades de administración principales de System Center Configuration Manager.
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 5d388399-07ca-431c-a9b2-56c69771aa87
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fadc93d1977d5d066a6c4c3884bdbaeefb2a0c90
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="features-and-capabilities-of-system-center-configuration-manager"></a>Características y funcionalidades de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

A continuación se indican las funcionalidades de administración principales de System Center Configuration Manager. Cada funcionalidad tiene sus propios requisitos previos, y las funcionalidades que use podrían influir en el diseño y la implementación de su jerarquía de Configuration Manager. Por ejemplo, si desea implementar software en dispositivos de su jerarquía, debe instalar el rol de punto de distribución del sistema de sitio.  

 Para obtener más información sobre cómo planear e instalar Configuration Manager para que admita estas funcionalidades de administración en su entorno, consulte [Get ready for System Center Configuration Manager](../../../core/plan-design/get-ready.md) (Preparación para System Center Configuration Manager).  

 **Administración de aplicaciones**  

 Proporciona un conjunto de herramientas y recursos que pueden ayudar a crear, administrar, implementar y supervisar aplicaciones para una variedad de distintos dispositivos que usted administra. Además, Configuration Manager le proporciona herramientas que le ayudan a proteger los datos de la empresa en las aplicaciones de usuario. Consulte [Introduction to application management](/sccm/apps/understand/introduction-to-application-management) (Introducción a la administración de aplicaciones).

 **Acceso a los recursos de la empresa**  

 Proporciona un conjunto de herramientas y recursos que le permiten proporcionar a los usuarios de su organización acceso a datos y aplicaciones desde ubicaciones remotas. Estas herramientas incluyen perfiles de Wi-Fi, perfiles de VPN, perfiles de certificado y el acceso condicional a Exchange y SharePoint Online. Consulte [Protect data and site infrastructure with System Center Configuration Manager](../../../protect/understand/protect-data-and-site-infrastructure.md) (Proteger la infraestructura de datos y del sitio con System Center Configuration Manager) y [Manage access to services in System Center Configuration Manager](../../../protect/deploy-use/manage-access-to-services.md) (Administrar el acceso a servicios en System Center Configuration Manager).  

 **Configuración de cumplimiento**  

 Proporciona un conjunto de herramientas y recursos que pueden ayudar a evaluar, efectuar un seguimiento y corregir el cumplimiento de la configuración de los dispositivos de cliente de la empresa. Además, puede usar la configuración de cumplimiento para configurar una serie de características y opciones de seguridad en los dispositivos que administra. Consulte [Ensure device compliance with System Center Configuration Manager](../../../compliance/understand/ensure-device-compliance.md) (Garantizar el cumplimiento de dispositivos con System Center Configuration Manager).  

 **Endpoint Protection**  

 Proporciona seguridad, antimalware y administración de Firewall de Windows para los equipos de su empresa. Consulte [Endpoint Protection in System Center Configuration Manager](../../../protect/deploy-use/endpoint-protection.md) (Endpoint Protection en System Center Configuration Manager).  

 **Inventario**  

 Proporciona un conjunto de herramientas que ayudan a identificar y supervisar los activos:  

-   **Inventario de hardware**: Recopila información detallada acerca del hardware de los dispositivos de su empresa. Consulte [Introduction to hardware inventory in System Center Configuration Manager](../../../core/clients/manage/inventory/introduction-to-hardware-inventory.md) (Introducción al inventario de hardware en System Center Configuration Manager).  

-   **Inventario de software**: Recopila y proporciona información acerca de los archivos que se almacenan en los equipos cliente de la organización. Consulte [Introduction to software inventory in System Center Configuration Manager](../../../core/clients/manage/inventory/introduction-to-software-inventory.md) (Introducción al inventario de software en System Center Configuration Manager).  

-   **Asset Intelligence**: Proporciona herramientas para recopilar datos de inventario y supervisar el uso de la licencia de software en su empresa. Consulte [Introduction to Asset Intelligence in System Center Configuration Manager](../../../core/clients/manage/asset-intelligence/introduction-to-asset-intelligence.md) (Introducción a Asset Intelligence en System Center Configuration Manager).  

**Administración de dispositivos móviles con Microsoft Intune**  

 Puede usar Configuration Manager para administrar dispositivos iOS, Android (Samsung KNOX Standard incluido), Windows Phone y Windows mediante el servicio de Microsoft Intune a través de Internet.

 Aunque use el servicio de Intune, las tareas de administración se completan mediante el uso del rol de sistema de sitio del punto de conexión de servicio, disponible a través de la consola de Configuration Manager. Consulte [Hybrid mobile device management (MDM) with System Center Configuration Manager and Microsoft Intune](../../../mdm/understand/hybrid-mobile-device-management.md) (Administración híbrida de dispositivos móviles (MDM) con System Center Configuration Manager y Microsoft Intune).  

 **Administración local de dispositivos móviles**  

 Inscribe y administra equipos y dispositivos móviles mediante la infraestructura local de Configuration Manager y la característica de administración integrada en las plataformas de dispositivo (en lugar de depender de un cliente de Configuration Manager instalado por separado). Actualmente admite la administración de dispositivos Windows 10 Enterprise y Windows 10 Mobile. Consulte [Manage mobile devices with on-premises infrastructure in System Center Configuration Manager](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) (Administrar dispositivos móviles con la infraestructura local en System Center Configuration Manager).  

 **Implementación de sistema operativo**  

 Proporciona una herramienta para crear imágenes del sistema operativo. Así, puede usar estas imágenes para implementar los sistemas operativos en los equipos, mediante arranque de PXE o un medio de arranque, como un conjunto de CD, DVD o unidades flash de USB. Tenga en cuenta que esto se aplica a equipos que se administran con Configuration Manager, así como a equipos no administrados. Consulte [Introduction to operating system deployment in System Center Configuration Manager](../../../osd/understand/introduction-to-operating-system-deployment.md) (Introducción a la implementación de sistema operativo en System Center Configuration Manager).  

 **Administración de energía**  

 Proporciona un conjunto de herramientas y recursos que puede utilizar para administrar y supervisar el consumo de energía de los equipos cliente de la empresa. Consulte [Introduction to power management in System Center Configuration Manager](../../../core/clients/manage/power/introduction-to-power-management.md) (Introducción a la administración de energía en System Center Configuration Manager).  

 **Consultas**  

 Proporciona una herramienta para recuperar información acerca de los recursos de la jerarquía y la información acerca de los mensajes de datos y estado de inventario. Así, puede usar esta información para generar informes o definir recopilaciones de dispositivos o usuarios para la configuración de la implementación y las opciones de software. Consulte [Introduction to queries in System Center Configuration Manager](../../../core/servers/manage/introduction-to-queries.md) (Introducción a las consultas en System Center Configuration Manager).  

 **Perfiles de conexión remota**  

 Proporciona un conjunto de herramientas y recursos para ayudarle a crear, implementar y supervisar la configuración de conexión remota a los dispositivos de su organización. Mediante la implementación de estas opciones, se minimiza la intervención que necesitan los usuarios para conectarse a sus equipos en la red corporativa. Consulte [Working with remote connection profiles in System Center Configuration Manager](/sccm/compliance/deploy-use/create-remote-connection-profiles) (Uso de perfiles de conexión remota en System Center Configuration Manager).  

 **Elementos de configuración de perfiles y datos de usuario**  

 Los elementos de configuración de perfiles y datos de usuario de Configuration Manager contienen opciones que pueden administrar el redireccionamiento de carpetas, los archivos sin conexión y los perfiles móviles en equipos que ejecutan Windows 8 y versiones posteriores para los usuarios de la jerarquía. Consulte [Working with user data and profiles configuration items in System Center Configuration Manager](/sccm/compliance/deploy-use/create-user-data-and-profiles-configuration-items) (Uso de elementos de configuración de perfiles y datos de usuario en System Center Configuration Manager).  

 **Control remoto**  

 Proporciona herramientas para administrar de forma remota los equipos cliente desde la consola de Configuration Manager. Consulte [Introduction to remote control in System Center Configuration Manager](../../../core/clients/manage/remote-control/introduction-to-remote-control.md) (Introducción al control remoto en System Center Configuration Manager).  

 **Generación de informes**  

 Proporciona un conjunto de herramientas y recursos para usar funciones avanzadas de informes de SQL Server Reporting Services desde la consola de Configuration Manager. Consulte [Introduction to reporting in System Center Configuration Manager](../../../core/servers/manage/introduction-to-reporting.md) (Introducción a los informes en System Center Configuration Manager).  

 **Medición de software**  

 Proporciona herramientas para supervisar y recopilar datos de uso de software de los clientes de Configuration Manager. Consulte [Supervisar el uso de aplicaciones a través de la medición de software en System Center Configuration Manager](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).  

 **Actualizaciones de software**  

 Proporciona un conjunto de herramientas y recursos que pueden ayudar a administrar, implementar y supervisar las actualizaciones de la empresa. Consulte [Introduction to software updates in System Center Configuration Manager](/sccm/sum/understand/software-updates-introduction) (Introducción a las actualizaciones de software en System Center Configuration Manager).  
