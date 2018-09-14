---
title: Selección de Intune independiente o MDM híbrida
titleSuffix: Configuration Manager
description: Elija si quiere implementar la administración de dispositivos móviles híbrida con Intune y Configuration Manager o ejecutar Intune de forma independiente.
ms.date: 08/14/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 73ff9bb9-e605-4b68-92a1-487684fed42d
author: aczechowski
ms.author: aaroncz
manager: dougeby
robots: noindex,nofollow
ms.openlocfilehash: 153c1208cef8a940cc06412322e8112d53d17e58
ms.sourcegitcommit: 98c3f7848dc9014de05541aefa09f36d49174784
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/14/2018
ms.locfileid: "42584449"
---
# <a name="choose-between-microsoft-intune-standalone-and-hybrid-mdm-with-configuration-manager"></a>Selección de Microsoft Intune independiente y MDM híbrida con Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Una de las preguntas más frecuentes relacionadas con la administración de dispositivos móviles (MDM) con Microsoft Intune es "¿Debo integrar Intune con Configuration Manager (MDM híbrida) o ejecutar Intune independiente en la configuración de solo en la nube?". 

Intune en Azure es la solución de MDM recomendada por Microsoft.     


> [!Important]  
> Desde el 14 de agosto de 2018, la administración híbrida de dispositivos móviles es una [característica en desuso](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). Para más información, vea [¿Qué es la Administración híbrida de dispositivos móviles (MDM)?](/sccm/mdm/understand/hybrid-mobile-device-management). <!--Intune feature 2683117-->  


 
## <a name="intune-standalone"></a>Intune independiente

Intune independiente es la topología de implementación recomendada de Microsoft. Intune independiente es una solución de MDM solo en la nube que se administra mediante una consola web a la que se puede acceder desde cualquier lugar del mundo. Los centros de datos de Intune se hospedan en Norteamérica, Europa y Asia. Como Intune es un servicio en la nube, puede implementar la administración de Intune en sus dispositivos rápidamente.

Generalmente, los clientes consideran que es más rápido y fácil implementar la topología independiente porque no hay independencia para los componentes locales. Intune independiente está disponible ahora en la plataforma de nube de Microsoft Azure y proporciona muchas características avanzadas, como las siguientes:  

- Plataforma integrada de Enterprise Mobility Management: una experiencia de administración y plataforma de nube integrada en Azure Portal para Intune, Azure AD Premium y Azure Information Protection  

- Administración de dispositivos móviles: funcionalidades enriquecidas de protección de la información y administración de dispositivos móviles  

- Escala: implemente y administre dispositivos móviles sin preocuparse de la escala.  

- Control de acceso basado en rol: restrinja el acceso a las funciones administrativas en función de los ámbitos y roles asignados.  

- Acceso mediante programación (API): opciones de administración de PowerShell y SDK, además de compatibilidad con Microsoft Graph API.  

- Consola web: una consola basada en HTML 5 basada en estándares web con compatibilidad con exploradores web más modernos.  

- Generación de informes avanzada: capacidad de crear informes personalizados.  

- Agilidad: configuración sencilla y entrega rápida de funcionalidades nuevas.  



## <a name="hybrid-mdm-with-configuration-manager"></a>MDM híbrida con Configuration Manager

> [!Important]  
> Desde el 14 de agosto de 2018, la administración híbrida de dispositivos móviles es una [característica en desuso](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). Para más información, vea [¿Qué es la Administración híbrida de dispositivos móviles (MDM)?](/sccm/mdm/understand/hybrid-mobile-device-management).  

MDM híbrida es una solución que integra las funcionalidades de administración de dispositivos móviles de Intune en Configuration Manager. Usa Intune como el canal de entrega de directivas, perfiles y aplicaciones a los dispositivos, pero usa infraestructura local de Configuration Manager para administrar contenido y los dispositivos. Una implementación híbrida proporciona un control desde "una sola ubicación". Esto significa que puede usar la misma infraestructura local y consola administrativa para administrar dispositivos móviles con Intune así como equipos y servidores con el cliente tradicional de Configuration Manager. 

Puede elegir MDM híbrida por los siguientes motivos:  

- Desea administrar tanto los dispositivos móviles inscritos en Intune como los dispositivos administrados con el cliente de Configuration Manager desde la misma consola administrativa  

- La infraestructura requiere que tenga varios servidores SCEP para la entrega de certificados a los dispositivos móviles  

- La infraestructura requiere que tenga varios conectores de Exchange  

- Necesita compatibilidad con el cifrado S/MIME

> [!Note]  
> Si configura MDM híbrida en Configuration Manager para el acceso condicional con Exchange local, los usuarios seguirán con la posibilidad de acceder al correo electrónico en Outlook para iOS y Android. Esta misma configuración con Intune independiente bloquea el correo electrónico para estos clientes.<!--Intune bug 2285890-->  



## <a name="change-the-mdm-authority"></a>Cambio de la entidad de MDM

Si necesita cambiar la configuración de la entidad MDM, puede hacerlo usted mismo sin tener que ponerse en contacto con Soporte técnico de Microsoft ni tener que anular la inscripción de los dispositivos administrados existentes y luego volver a inscribirlos. Para obtener más información, consulte [Cambio de la entidad de MDM](/sccm/mdm/deploy-use/change-mdm-authority).

