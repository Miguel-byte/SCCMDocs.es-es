---
title: Requisitos previos de los perfiles de correo electrónico
titleSuffix: Configuration Manager
description: Obtenga información sobre los perfiles de correo electrónico de System Center Configuration Manager y sus dependencias internas y externas al producto.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: dccf0b73-43bd-4545-8914-114168ebad36
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 58e1f4b56c99cf29c112773b2a82c70695e58744
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="email-profile-prerequisites"></a>Requisitos previos de los perfiles de correo electrónico

*Se aplica a: System Center Configuration Manager (Rama actual)*

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
