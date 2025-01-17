---
title: Coexistencia de MDM de terceros
titleSuffix: Configuration Manager
description: Obtenga información sobre el uso de un servicio de MDM de terceros con Configuration Manager
ms.date: 05/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: ed4dc65e-e5d5-4f75-88ac-f4849ec8fc10
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5fbb2d4a902c21ac2fa2186bba70f58d66e50c48
ms.sourcegitcommit: 18ad7686d194d8cc9136a761b8153a1ead1cdc6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66176857"
---
# <a name="third-party-mdm-coexistence-with-configuration-manager"></a>Coexistencia de MDM de terceros con Configuration Manager

Al administrar simultáneamente dispositivos Windows 10 mediante Configuration Manager y Microsoft Intune, esta funcionalidad se denomina [administración conjunta](/sccm/comanage/overview). Al administrar dispositivos con Configuration Manager e inscribirse a un servicio de MDM de terceros, esta funcionalidad se denomina *coexistencia*. Tener dos autoridades de administración para un único dispositivo puede ser complicado si no hay una orquestación correcta entre los dos. Con la administración conjunta, Configuration Manager e Intune equilibran las [cargas de trabajo](/sccm/comanage/workloads) para asegurarse de que no hay ningún conflicto. Esta interacción no existe con los servicios de terceros, por lo que hay limitaciones con las funcionalidades de administración de coexistencia.

El cliente de Configuration Manager puede coexistir con un servicio de MDM de terceros en un dispositivo en el que se ejecute Windows 10 versión 1709 o posterior, y que esté unido a Azure Active Directory. El dispositivo puede ser de cualquiera de los siguientes tipos:

- Solo [Unido a Azure AD](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan). (Este tipo se conoce a veces como "unido al dominio en la nube")  

- [Unido a un dominio híbrido](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan), en el que el dispositivo está unido a Active Directory local y registrado con Azure Active Directory.  

> [!Note]  
> No es compatible con [dispositivos personales](https://docs.microsoft.com/windows/client-management/mdm/mdm-enrollment-of-windows-devices#connecting-personally-owned-devices-bring-your-own-device).  

Cuando el cliente de Configuration Manager detecta que un servicio de MDM de terceros también está administrando el dispositivo, este desactiva automáticamente determinadas cargas de trabajo en Configuration Manager. Este comportamiento permite al servicio de MDM ocuparse de estas funciones. También evita las configuraciones en conflicto en el cliente que podrían afectar negativamente a la experiencia del usuario y al dispositivo. Las cargas de trabajo siguientes de Configuration Manager se desactivan en este caso:

- Directivas de acceso a recursos para la configuración de VPN, Wi-Fi, correo electrónico y certificados
- Administración de aplicaciones, incluidos los paquetes heredados
- Instalación y análisis de actualizaciones de software
- Endpoint Protection, el conjunto de características de protección antimalware de Windows Defender
- Directiva de cumplimiento para el acceso condicional
- Configuración del dispositivo
- Administración con Hacer clic y ejecutar de Office

El cliente de Configuration Manager evita conflictos con la entidad de administración de terceros mediante la ejecución de las siguientes operaciones de solo lectura:

- Inventario de hardware y software
- Asset Intelligence
- Disponibilidad de software
- Informes de administración de energía

Para obtener más información sobre las ventajas de la administración conjunta con Configuration Manager e Intune, vea las [ventajas de la administración conjunta](/sccm/comanage/overview#benefits).
