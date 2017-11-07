---
title: Configurar Endpoint Protection
titleSuffix: Configuration Manager
description: "Obtenga información sobre cómo configurar Configuration Manager para actualizar y distribuir definiciones de malware de Windows Defender."
ms.custom: na
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
caps.latest.revision: "21"
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 5f005e7cd9c396fcf7e02aafefcb34c37ddab901
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/12/2017
---
# <a name="configure-endpoint-protection"></a>Configurar Endpoint Protection

*Se aplica a: System Center Configuration Manager (rama actual)*

Para poder usar Endpoint Protection para administrar la seguridad y el malware en equipos cliente de Configuration Manager, debe realizar los pasos de configuración que se detallan en este tema.  

## <a name="how-to-configure-endpoint-protection-in-configuration-manager"></a>Cómo configurar Endpoint Protection en Configuration Manager  
 Endpoint Protection en Configuration Manager tiene dependencias externas y dependencias en el producto.  

### <a name="steps-to-configure-endpoint-protection-in-configuration-manager"></a>Pasos para configurar Endpoint Protection en Configuration Manager  
 La tabla siguiente proporciona pasos, detalles y más información sobre el procedimiento para configurar Endpoint Protection.  

> [!IMPORTANT]  
>  Si administra Endpoint Protection para equipos Windows 10, debe configurar Configuration Manager para actualizar y distribuir las definiciones de malware de Windows Defender. Windows Defender se incluye en Windows 10, pero aun así se tiene que instalar SCEPInstall y se necesita la configuración de cliente personalizada de Endpoint Protection (consulte el **paso 5** más adelante).  

|Pasos|Detalles|  
|-----------|-------------|  
|**Paso 1:** [crear un rol de sistema de sitio de punto de Endpoint Protection](endpoint-protection-site-role.md)|El rol de sistema de sitio de punto de Endpoint Protection debe estar instalado para poder usar Endpoint Protection. Se debe instalar en un solo servidor de sistema de sitio y en la parte superior de la jerarquía en un sitio de administración central o un sitio primario independiente. |  
|**Paso 2:** [configurar alertas de Endpoint Protection](endpoint-configure-alerts.md)|Las alertas informan al administrador si se han producido eventos específicos, como una infección de malware. Las alertas se muestran en el nodo **Alertas** del área de trabajo **Supervisión** o, de forma alternativa, pueden enviarse por correo electrónico a los usuarios especificados. |  
|**Paso 3:** [configurar orígenes de actualizaciones de definiciones para clientes de Endpoint Protection](endpoint-definition-updates.md)|Es posible configurar Endpoint Protection para que use diversos orígenes para la descarga de actualizaciones de definiciones. |  
|**Paso 4:** [configurar la directiva antimalware predeterminada y crear directivas antimalware personalizadas](endpoint-antimalware-policies.md)|La directiva antimalware predeterminada se aplica si está instalado el cliente de Endpoint Protection. Toda directiva personalizada que haya implementado se aplica de forma predeterminada, en los 60 minutos posteriores a la implementación del cliente. Asegúrese de que configuró las directivas antimalware antes de implementar el cliente de Endpoint Protection. |  
|**Paso 5:** [configurar opciones de cliente personalizadas para Endpoint Protection](endpoint-protection-configure-client.md)|Use las opciones de cliente personalizadas con el fin de configurar las opciones de Endpoint Protection para las recopilaciones de equipos de la jerarquía.<br /><br /> Nota: No configure las opciones de cliente personalizadas de Endpoint Protection a menos que esté seguro de que quiere aplicarlas a todos los equipos de la jerarquía. |  
