---
title: Selección de Intune independiente o MDM híbrida
titleSuffix: Configuration Manager
description: Elija si quiere implementar la administración de dispositivos móviles híbrida con Intune y Configuration Manager o ejecutar Intune de forma independiente.
ms.date: 07/18/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 73ff9bb9-e605-4b68-92a1-487684fed42d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2a7cd26fde23c560295117edcc148835b1397a55
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32347297"
---
# <a name="choose-between-microsoft-intune-standalone-and-hybrid-mobile-device-management-with-system-center-configuration-manager"></a>Elegir entre Microsoft Intune independiente y administración de dispositivos móviles híbrida con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Una de las preguntas más frecuentes relacionadas con la administración de dispositivos móviles (MDM) con Microsoft Intune es "¿Debo integrar Intune con Configuration Manager (MDM híbrida) o ejecutar Intune independiente en la configuración de solo en la nube?". Para responder a esa pregunta, debe comparar cuidadosamente ambas opciones.
 
## <a name="intune-standalone"></a>Intune independiente
Intune independiente es la topología de implementación recomendada de Microsoft. Intune independiente es una solución de MDM solo en la nube que se administra mediante una consola web a la que se puede acceder desde cualquier lugar del mundo. Los centros de datos de Intune se hospedan en Norteamérica, Europa y Asia. Como Intune es un servicio en la nube, puede implementar la administración de Intune en sus dispositivos en un período de tiempo relativamente corto.

Generalmente, los clientes consideran que es más rápido y fácil implementar la topología independiente porque no hay independencia para los componentes locales. Intune independiente está disponible ahora en la plataforma de nube de Microsoft Azure y proporciona muchas características avanzadas, como las siguientes:
- Plataforma integrada de Enterprise Mobility Management: una experiencia de administración y plataforma de nube integrada en Azure Portal para Intune, Azure AD Premium y Azure Information Protection.
- Administración de dispositivos móviles: funcionalidades enriquecidas de protección de la información y administración de dispositivos móviles.
- Escala: implemente y administre dispositivos móviles sin preocuparse de la escala.
- Control de acceso basado en rol: restrinja el acceso a las funciones administrativas en función de los ámbitos y roles asignados.
- Acceso mediante programación (API): opciones de administración de PowerShell y SDK, además de compatibilidad con Microsoft Graph API.
- Consola web: una consola basada en HTML 5 basada en estándares web con compatibilidad con exploradores web más modernos.
- Generación de informes avanzada: capacidad de crear informes personalizados.
- Agilidad: configuración sencilla y entrega rápida de funcionalidades nuevas.


## <a name="hybrid-mdm-with-configuration-manager"></a>MDM híbrida con Configuration Manager
MDM híbrida es una solución que integra las funcionalidades de administración de dispositivos móviles de Intune en Configuration Manager. Usa Intune como el canal de entrega de directivas, perfiles y aplicaciones a los dispositivos, pero usa infraestructura local de Configuration Manager para administrar contenido y los dispositivos. Una implementación híbrida proporciona un control desde "una sola ubicación".  Esto significa que puede usar la misma infraestructura local y consola administrativa para administrar dispositivos móviles con Intune así como equipos y servidores con el cliente tradicional de Configuration Manager. Puede elegir MDM híbrida por los siguientes motivos:  
- Desea administrar tanto los dispositivos móviles inscritos en Intune como los dispositivos administrados con el cliente de Configuration Manager desde la misma consola administrativa
- La infraestructura requiere que tenga varios servidores SCEP para la entrega de certificados a los dispositivos móviles
- La infraestructura requiere que tenga varios conectores de Exchange
- Necesita compatibilidad con el cifrado S/MIME


## <a name="changing-the-mdm-authority-setting"></a>Cambio de configuración de la entidad MDM
Si necesita cambiar la configuración de la entidad MDM, puede hacerlo usted mismo sin tener que ponerse en contacto con Soporte técnico de Microsoft ni tener que anular la inscripción de los dispositivos administrados existentes y luego volver a inscribirlos. Para obtener más información, consulte [Cambio de la entidad de MDM](../deploy-use/change-mdm-authority.md).

> [!NOTE]    
> Debe tener la versión 1610 o posterior de Configuration Manager para cambiar la entidad MDM a Intune independiente. Si tiene una versión anterior de Configuration Manager, puede cambiar la entidad MDM pero requiere ayuda de operaciones y Soporte técnico de Microsoft. También necesita anular la inscripción de todos los dispositivos y volver a inscribirlos una vez que se cambia la entidad MDM.  
