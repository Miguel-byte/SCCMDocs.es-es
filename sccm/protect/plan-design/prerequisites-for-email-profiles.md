---
title: "Requisitos previos de los perfiles de correo electrónico | Microsoft Docs"
description: "Obtenga información sobre los perfiles de correo electrónico de System Center Configuration Manager y sus dependencias internas y externas al producto."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: dccf0b73-43bd-4545-8914-114168ebad36
caps.latest.revision: 5
caps.handback.revision: 0
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 0fa837c68eb073d2ceaf48c938137a94141a102e
ms.openlocfilehash: bdb7f78480f73bc4559c4ff49ecb7b047581780a


---
# <a name="email-profile-prerequisites"></a>Requisitos previos de los perfiles de correo electrónico

*Se aplica a: System Center Configuration Manager (rama actual)*

Los perfiles de correo electrónico de System Center Configuration Manager tienen dependencias internas y externas al producto.  

## <a name="configuration-manager-dependencies"></a>Dependencias de Configuration Manager  

|Dependencia|Más información|  
|----------------|----------------------|  
|Para administrar perfiles de correo electrónico se deben conceder determinados permisos de seguridad.|Debe tener los siguientes permisos de seguridad para poder administrar la configuración del acceso a los recursos de empresa, como los perfiles de correo electrónico:<br /><br /> - Para ver y administrar alertas e informes de perfiles de correo electrónico: permisos **Crear**, **Eliminar**, **Modificar**, **Modificar informe**, **Leer** y **Ejecutar informe** para el objeto **Alertas**.<br /><br /> - Para crear y administrar perfiles de certificado: permisos **Directiva de autor**, **Modificar informe**, **Leer** y **Ejecutar informe** para el objeto **Perfil de certificado**.<br /><br /> - Para administrar implementaciones de perfiles de correo electrónico: permisos **Implementar directivas de configuración**, **Modificar alerta de estado de cliente**, **Leer** y **Leer recurso** para el objeto **Recopilación**.<br /><br /> - Para administrar todas las directivas de configuración: permisos **Crear**, **Eliminar**, **Modificar**, **Leer** y **Establecer ámbito de seguridad** para el objeto **Directiva de configuración**.<br /><br /> - Para ejecutar consultas relacionadas con los perfiles de correo electrónico: permiso **Leer** para el objeto **Consulta**.<br /><br /> - Para consultar información de los perfiles de correo electrónico en la consola de System Center Configuration Manager: permiso **Leer** para el objeto **Sitio**.<br /><br /> - Para ver los mensajes de estado de los perfiles de correo electrónico: permiso **Leer** para el objeto **Mensajes de estado**.<br /><br /> - Para crear y administrar perfiles de correo electrónico: permisos **Directiva de autor**, **Modificar informe**, **Leer** y **Ejecutar informe** para el objeto **Perfil de aprovisionamiento de comunicaciones**.<br /><br /> El rol de seguridad **Administrador de acceso de recursos de la compañía** incluye estos permisos necesarios para administrar los perfiles de correo electrónico en System Center Configuration Manager. Para obtener más información, consulte [Configurar la seguridad en System Center Configuration Manager](../../core/plan-design/security/configure-security.md).|  
|Atributo mail en Active Directory|Si quiere usar la dirección SMTP principal de los usuarios para crear la dirección de correo electrónico de dichos usuarios en un perfil de correo electrónico, la detección de usuarios de System Center Configuration Manager debe estar configurada para poder detectar el atributo **mail** de Active Directory (esto está configurado de forma predeterminada).|  

## <a name="external-dependencies"></a>Dependencias externas  

|Dependencia|Más información|  
|----------------|----------------------|  
|Atributo mail en Active Directory|Si quiere usar la dirección SMTP principal de los usuarios para crear la dirección de correo electrónico de dichos usuarios en un perfil de correo electrónico, esta dirección debe existir en el atributo **mail** de Active Directory.<br /><br /> Para obtener más información, consulte la documentación de Windows Server.|



<!--HONumber=Jan17_HO4-->


