---
title: Configuración de Azure AD híbrido
titleSuffix: Configuration Manager
description: Si el entorno tiene actualmente los dispositivos Windows 10 unido al dominio, configurar híbrida de Azure AD antes de habilitar la administración conjunta
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 27dd26d1-e99c-4431-b2f8-60406394b6db
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: ec02f740485d3f8b466cde0a644aaaa8885b91f2
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56755542"
---
# <a name="set-up-hybrid-azure-ad-for-co-management"></a>Configurar híbrida de Azure AD para la administración conjunta

Si tiene dispositivos de Windows 10 Unidos a un entorno local de Active Directory, antes de habilitar la administración conjunta en Configuration Manager, unir estos dispositivos a Azure Active Directory (Azure AD). Este proceso se denomina combinación de Azure AD híbrido. 

En el siguiente vídeo, jefe de programas senior Sandeep Deo y director de marketing de productos Adam Harbour discutan y demostración de la configuración de dispositivos en Azure AD:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Configuring-Devices-in-Azure-Active-Directory/player]

El híbrido de Azure AD proceso de unión automáticamente registros de los dispositivos Unidos a un dominio de en el entorno local con Azure AD. Para más información sobre este proceso, vea los siguientes artículos:
- [Introducción a la administración de dispositivos en Azure Active Directory](https://docs.microsoft.com/azure/active-directory/device-management-introduction) 
- [Cómo planear la combinación de Azure AD híbrido](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan)

Combinación de Azure AD híbrido es uno de los aspectos básicos de clave para la administración conjunta. Este proceso puede resultar complicado para algunos clientes, por ejemplo:
- Su organización usa una solución de identidad de terceros 
- Las complejidades de la configuración de seguridad de Active Directory Federation Services (ADFS)

Resolver estos desafíos puede tardar algunas instrucciones. En este artículo ayuda a mitigar los retrasos.


## <a name="how-to-do-it"></a>Para saber cómo hacerlo

Los dispositivos son similares a los usuarios cuando se crea una identidad que desea proteger. Para proteger la identidad de un dispositivo en cualquier momento y en cualquier ubicación, deberá introducir la identidad del dispositivo en Azure AD.

Según el tipo de dominio que está usando, hay dos métodos principales para hacerlo. Configurar la combinación de Azure AD híbrido para uno de los siguientes tipos de dominio:  
- [Dominios federados](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-federated-domains)  
- [Dominios administrados](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-managed-domains)  

Los dos métodos anteriores proporcionan la mejor experiencia. Para obtener más información, incluido el proceso totalmente manual, consulte los artículos siguientes:
- [Configurar manualmente los dispositivos Unidos a Azure AD híbrido](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup)  
- [Autenticación de paso a través de AD FS para Azure AD híbrido](https://docs.microsoft.com/windows-server/identity/ad-fs/ad-fs-overview), que incluye la detección de Azure AD  

Pautas para solucionar problemas, consulte el [10 de Windows Azure AD híbrido Guía de solución](https://docs.microsoft.com/azure/active-directory/devices/troubleshoot-hybrid-join-windows-current).



## <a name="case-study"></a>Caso práctico

Una compañía de software Europeo de gran tamaño con más de 100.000 usuarios en su red tardó un enfoque por fases y detallado para habilitar Azure AD híbrido.

Durante la fase de planeación, puesto que la combinación de Azure AD híbrido es un elemento clave que admiten la administración conjunta, los administradores de Configuration Manager trabajaron con el equipo de identidad. Esta empresa de software tenía muchas reglas de AD FS, y algunas de ellas eran complejas. Para abordar este reto, el equipo de identidad revisado las reglas ADFS existentes antes de habilitar la combinación de Azure AD híbrido. El equipo de TI también ha elegido actualizar Azure AD Connect a la versión más reciente. Ahora, Azure AD Connect proporciona un flujo de proceso automatizado para habilitar Azure AD híbrido.

Después de una implementación correcta y probar en su entorno de preproducción, este cliente habilita la combinación de Azure AD híbrido para el espacio de producción completa. Dentro de una semana, tenían que todos los dispositivos Windows 10 administrados conjuntamente.



## <a name="contact-fasttrack"></a>Póngase en contacto FastTrack

Si necesita recibir ayuda para configurar Azure AD en cualquier momento en el proceso, vaya a [Microsoft FastTrack](https://Microsoft.com/FastTrack/), inicie sesión y solicitar asistencia. 

Para obtener más información, consulte [obtener ayuda de FastTrack](/sccm/comanage/quickstart-fasttrack). 

