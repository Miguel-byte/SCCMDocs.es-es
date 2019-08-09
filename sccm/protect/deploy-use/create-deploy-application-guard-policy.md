---
title: Creación e implementación de directivas de Protección de aplicaciones de Windows Defender
titleSuffix: Configuration Manager
description: Creación e implementación de directivas de Protección de aplicaciones de Windows Defender.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 33a6c1d9-4dd8-411c-a748-693a5bd2ea5a
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: d3859b56b71b7818baaf6f63e068c0dec80bba44
ms.sourcegitcommit: 72faa1266b31849ce1a23d661a1620b01e94f517
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/26/2019
ms.locfileid: "68533597"
---
# <a name="create-and-deploy-windows-defender-application-guard-policy"></a>Creación e implementación de directivas de Protección de aplicaciones de Windows Defender

*Se aplica a: System Center Configuration Manager (Rama actual)*
<!-- 1351960 -->  
Puede crear e implementar directivas de [Protección de aplicaciones de Windows Defender (Protección de aplicaciones)](https://docs.microsoft.com/windows/threat-protection/windows-defender-application-guard/wd-app-guard-overview) utilizando Configuration Manager Endpoint Protection. Estas directivas ayudan a proteger a los usuarios al abrir los sitios web que no sean de confianza en un contenedor aislado seguro al que no puedan acceder otras partes del sistema operativo.

## <a name="prerequisites"></a>Requisitos previos

Para crear e implementar una directiva de Protección de aplicaciones de Windows Defender, debe usar la actualización de Windows 10 Fall Creator (1709). Los dispositivos Windows 10 en los que implementa la directiva deben configurarse con una directiva de aislamiento de red. Para obtener más información, consulte [Información general de la Protección de aplicaciones de Windows Defender](https://docs.microsoft.com/windows/threat-protection/windows-defender-application-guard/wd-app-guard-overview).

## <a name="create-a-policy-and-to-browse-the-available-settings"></a>Cree una directiva y examine la configuración disponible

1. En la consola de Configuration Manager, elija **Activos y compatibilidad**.
2. En el área de trabajo **Activos y compatibilidad**, elija **Introducción** > **Endpoint Protection** > **Protección de aplicaciones de Windows Defender**.
3. En la pestaña **Inicio**, en el grupo **Crear**, haga clic en **Crear directiva de Protección de aplicaciones de Windows Defender**.
4. Con el [artículo](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/configure-wd-app-guard) como referencia, puede examinar y configurar las opciones disponibles. Configuration Manager le permite establecer ciertas opciones de configuración de directiva:
   - [Configuración de interacción de host](#bkmk_HIS)
   - [Comportamiento de la aplicación](#bkmk_ABS)
   - [Administración de archivos](#bkmk_FM)
5. En la página **Definición de red**, debe especificar la identidad corporativa y definir los límites de la red corporativa.

    > [!NOTE]
    > Los equipos con Windows 10 solo almacenan una lista de aislamiento de red en el cliente. Puede crear dos tipos diferentes de listas de aislamiento de red e implementarlas en el cliente:
    >
    >  - uno de Windows Information Protection
    >  - otro de Protección de aplicaciones de Windows Defender
    >
    > Si implementa ambas directivas, deben coincidir con estas listas de aislamiento de red. Si implementa listas que no coincidan con el mismo cliente, se producirá un error en la implementación. Para obtener más información, consulte la [documentación de Windows Information Protection](https://docs.microsoft.com/windows/threat-protection/windows-information-protection/create-wip-policy-using-sccm).

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

### <a name="bkmk_FM"></a> Administración de archivos
<!--3555858-->
A partir de Configuration Manager versión 1906, hay una configuración de directiva que permite a los usuarios confiar en los archivos que normalmente se abren en la protección de aplicaciones. Tras completarse correctamente, los archivos se abrirán en el dispositivo de host en lugar de hacerlo en Protección de aplicaciones. Para más información sobre las directivas de Protección de aplicaciones, vea [Establecer la configuración de la directiva de Protección de aplicaciones de Windows Defender](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/configure-wd-app-guard).

- **Permitir a los usuarios confiar en archivos que se abren en protección de aplicaciones de Windows Defender** : permite al usuario marcar archivos como de confianza. Cuando un archivo es de confianza, se abre en el host en lugar de en la protección de aplicaciones. Se aplica a los clientes de Windows 10 versión 1810 o posterior.
  - **Prohibido**: no se permite que los usuarios marquen los archivos como de confianza (valor predeterminado).
  - **Archivo protegido por antivirus:** Permitir a los usuarios marcar archivos como de confianza después de una comprobación antivirus.
  - **Todos los archivos:** se permite que los usuarios marquen cualquier archivo como de confianza.

Al habilitar la administración de archivos, es posible que vea errores registrados en el DCMReporting. log del cliente. Los errores siguientes no suelen afectar a la funcionalidad: <!--4619457-->

- En dispositivos compatibles:
  - No se ha encontrado FileTrustCriteria_condition
- En dispositivos no compatibles:
  - No se ha encontrado FileTrustCriteria_condition
  - No se ha encontrado FileTrustCriteria_condition en el mapa
  - No se ha encontrado FileTrustCriteria_condition en el resumen

Para editar la configuración de la protección de aplicaciones, expanda **Endpoint Protection** en el área de trabajo **activos y compatibilidad** y, a continuación, haga clic en el nodo **protección de aplicaciones de Windows Defender** . Haga clic con el botón derecho en la directiva que quiera editar y luego seleccione **Propiedades**.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más sobre Protección de aplicaciones de Windows Defender: [Información general de la Protección de aplicaciones de Windows Defender](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/wd-app-guard-overview).
[Windows Defender Application Guard FAQ](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/faq-wd-app-guard) (Preguntas más frecuentes sobre Protección de aplicaciones de Windows Defender).
