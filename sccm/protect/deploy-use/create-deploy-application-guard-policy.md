---
title: Creación e implementación de directivas de Protección de aplicaciones de Windows Defender
titleSuffix: Configuration Manager
description: Creación e implementación de directivas de Protección de aplicaciones de Windows Defender.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 33a6c1d9-4dd8-411c-a748-693a5bd2ea5a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: d6446fed2d48fc6428bdc3fbc7a24f728c206dc7
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56132428"
---
# <a name="create-and-deploy-windows-defender-application-guard-policy"></a>Creación e implementación de directivas de Protección de aplicaciones de Windows Defender 
*Se aplica a: System Center Configuration Manager (rama actual)*
<!-- 1351960 --> puede crear e implementar [Windows Defender Application Guard](https://docs.microsoft.com/windows/threat-protection/windows-defender-application-guard/wd-app-guard-overview) directivas utilizando el punto de conexión de Configuration Manager protección. Estas directivas ayudan a proteger a los usuarios al abrir los sitios web que no sean de confianza en un contenedor aislado seguro al que no puedan tener acceso otras partes del sistema operativo.

## <a name="prerequisites"></a>Requisitos previos

Para crear e implementar una directiva de Protección de aplicaciones de Windows Defender, debe usar la actualización de Windows 10 Fall Creator (1709). Además, los dispositivos Windows 10 en los que implementa la directiva deben configurarse con una directiva de aislamiento de red. Para obtener más información, consulte [Información general de la Protección de aplicaciones de Windows Defender](https://docs.microsoft.com/windows/threat-protection/windows-defender-application-guard/wd-app-guard-overview). 


## <a name="create-a-policy-and-to-browse-the-available-settings"></a>Cree una directiva y examine la configuración disponible:

1. En la consola de Configuration Manager, elija **Activos y compatibilidad**.
2. En el área de trabajo **Activos y compatibilidad**, elija **Introducción** > **Endpoint Protection** > **Protección de aplicaciones de Windows Defender**.
3. En la pestaña **Inicio**, en el grupo **Crear**, haga clic en **Crear directiva de Protección de aplicaciones de Windows Defender**.
4. Con el [artículo](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/configure-wd-app-guard) como referencia, puede examinar y configurar las opciones disponibles. Configuration Manager permite establecer determinadas configuraciones de directiva, vea [configuración de interacción de host](#BKMK_HIS) y [comportamiento de la aplicación](#BKMK_AppB).
5. En la página **Definición de red**, debe especificar la identidad corporativa y definir los límites de la red corporativa.

    > [!NOTE]
    > Los equipos con Windows 10 solo almacenan una lista de aislamiento de red en el cliente. Puede crear dos tipos diferentes de listas de aislamiento de red e implementarlas en el cliente:
    >
    >  - uno de Windows Information Protection
    >  - otro de Protección de aplicaciones de Windows Defender
    >
    > Si implementa ambas directivas, deben coincidir con estas listas de aislamiento de red. Si implementa listas que no coincidan con el mismo cliente, se producirá un error en la implementación. Para obtener más información, consulte la [documentación de Windows Information Protection](https://docs.microsoft.com/windows/threat-protection/windows-information-protection/create-wip-policy-using-sccm).
    > 
    > 

6. Cuando haya terminado, complete el asistente e implemente la directiva en uno o varios dispositivos Windows 10 1709.

### <a name="bkmk_HIS"></a> Configuración de interacción de host
Configura las interacciones entre los dispositivos de host y el contenedor de Protección de aplicaciones. Antes de la versión 1802 de Configuration Manager, la interacción de host y el comportamiento de la aplicación se encontraban en la pestaña **Configuración**.

- **Portapapeles**: en Configuración antes de Configuration Manager 1802
    - Tipo de contenido permitido
        - Texto
        - Imágenes
- **Impresión:**
    - Habilitar impresión en XPS
    - Habilitar impresión en PDF
    - Habilitar impresión en impresoras locales
    - Habilitar impresión en impresoras de red
- **Gráficos:** (a partir de la versión 1802 de Configuration Manager)
    - Acceso al procesador de gráficos virtuales
- **Archivos:** (a partir de la versión 1802 de Configuration Manager)
    - Guardar los archivos descargados que se van a hospedar

### <a name="bkmk_ABS"></a> Configuración de comportamiento de la aplicación
Configura el comportamiento de la aplicación dentro de la sesión de Protección de aplicaciones. Antes de la versión 1802 de Configuration Manager, la interacción de host y el comportamiento de la aplicación se encontraban en la pestaña **Configuración**.

- **Contenido:**
   - Los sitios empresariales pueden cargar contenido no empresarial, como complementos de terceros.
- **Otros:**
    - Conservar datos del explorador generados por el usuario
    - Eventos de auditoría de seguridad en la sesión aislada de Protección de aplicaciones



## <a name="next-steps"></a>Pasos siguientes
Para obtener más sobre Protección de aplicaciones de Windows Defender: [Información general de la Protección de aplicaciones de Windows Defender](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/wd-app-guard-overview).
[Windows Defender Application Guard FAQ](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/faq-wd-app-guard) (Preguntas más frecuentes sobre Protección de aplicaciones de Windows Defender).
