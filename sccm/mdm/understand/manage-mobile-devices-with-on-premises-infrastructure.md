---
title: "Administración local de dispositivos móviles (MDM) | Microsoft Docs"
description: "Obtenga información acerca de la administración de dispositivos móviles local, una solución de administración de dispositivos en System Center Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 497c05c7-fe9f-4b88-983b-1c5b3d59308e
caps.latest.revision: 8
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 0d6479bcc134103e6005159a8ea295a5f359a436
ms.openlocfilehash: cbd33bf3cf7d623d9ba7a657d4ca7d746d7e79da
ms.lasthandoff: 12/16/2016


---
# <a name="on-premises-mobile-device-management-mdm-in-system-center-configuration-manager"></a>Administración de dispositivos móviles local en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

La administración de dispositivos móviles local de System Center Configuration Manager es una solución de administración de dispositivos que se basa en las características integradas de administración de sistemas operativos de dispositivos (conforme al estándar Open Mobile Alliance Device Management o OMA DM) a la vez que usa la infraestructura local de Configuration Manager de una empresa para administrar y mantener los dispositivos. La administración de dispositivos móviles local requiere Microsoft Intune configurar para la función de administración, pero solo es necesario para la suscripción (y para notificar a los dispositivos que comprueben los cambios de directiva determinados momentos), pero no se utiliza para administrar los dispositivos o almacenar datos acerca de ellos.  

 ![Concepto local](media/On-premises-conceptual.png)  

 La administración de dispositivos móviles local difiere de Microsoft Intune, que también se basa en las características integradas de la administración de dispositivos móviles local, pero todas las funciones de administración se prestan a través de servicios en la nube.  La administración de dispositivos móviles local también difiere de la solución de administración basada en cliente que tradicionalmente ofrece Configuration Manager, ya que se basa en una infraestructura de empresa similar, pero no usa software cliente instalado de forma independiente en los equipos y los dispositivos que administra.  

 En la tabla siguiente se detallan las ventajas y desventajas de la administración de dispositivos móviles local en comparación con la administración basada en cliente tradicional:  

|Ventajas|Desventajas|  
|----------------|-------------------|  
|**Infraestructura simplificada** : se necesitan menos roles de sistema de sitio.<br /><br /> **Mantenimiento más sencillo**: dado que la funcionalidad de administración está integrada en el sistema operativo del dispositivo, no se necesitan nuevas versiones del software cliente cuando se incorporan nuevas características de administración en el sistema de Configuration Manager.<br /><br /> **Local** : todos los datos y la administración se conservan de forma local.|**Menos funciones de administración de clientes** : no se necesita orquestación, medición de software, integración de terceros, secuenciación de tareas ni soporte técnico de Centro de software.<br /><br /> **Compatibilidad de dispositivos limitada**: actualmente la administración de dispositivos móviles local solo admite dispositivos que ejecutan Windows 10 y Windows 10 Mobile.|  

 En los temas siguientes se proporciona información que puede usar para planear, preparar e inscribir dispositivos para la administración de dispositivos móviles local:  

-   [Planeación de la administración de dispositivos móviles (MDM) local con System Center Configuration Manager](../plan-design/plan-on-premises-mdm.md)  

     Conozca los aspectos que debe tener en cuenta al configurar la infraestructura de Configuration Manager y planear la inscripción de dispositivos en la administración de dispositivos móviles (MDM) local.  

-   [Pasos de preparación para la administración de dispositivos móviles local en System Center Configuration Manager](../get-started/preparation-steps-for-on-premises-mdm.md)  

     Aprenda a preparar el sistema de Configuration Manager para que está listo para la administración de dispositivos móviles local mediante la configuración de la suscripción a Microsoft Intune, la configuración de certificados, la instalación de roles de sistema de sitio y la configuración de la inscripción de dispositivos.  

-   [Inscripción de dispositivos para la administración de dispositivos móviles (MDM) local en System Center Configuration Manager](../deploy-use/enroll-devices-on-premises-mdm.md)  

     Descubra cómo inscribir dispositivos, cómo los usuarios pueden inscribir sus dispositivos y cómo se realiza la inscripción masiva con un paquete de inscripción.  

