---
title: Extensiones de Security Content Automation Protocol (SCAP)
titleSuffix: Configuraton Manager
description: Conozca las extensiones de Security Content Automation Protocol (SCAP)
ms.date: 03/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: a315489d-5e12-46d6-903e-3a35235b72c5
author: aczechowski
ms.author: aaroncz
manager: dougeby
robots: noindex,nofollow
ms.openlocfilehash: 18463e4f87c60135bdc29d0f7ce4cb2f80a0eea7
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32336194"
---
# <a name="about-the-security-content-automation-protocol-scap-extensions"></a>Extensiones de Security Content Automation Protocol (SCAP)

*Se aplica a: System Center Configuration Manager (Rama actual)*

> [!Tip]  
> Esta característica se introdujo por primera vez en la versión preliminar técnica 1803 como una [característica de versión preliminar](/sccm/core/servers/manage/pre-release-features). Esta versión preliminar de las extensiones SCAP puede instalarse en cualquier versión admitida de Rama actual de Configuration Manager y LTSB 1606. El archivo de instalación se encuentra en cd.latest\SMSSETUP\TOOLS\ConfigMgrSCAPExtension\ConfigMgrExtensionsForSCAP.msi a partir de 1803 Technical Preview. 

Con las extensiones SCAP para Microsoft System Center Configuration Manager es más fácil analizar y evaluar el entorno de red para garantizar el cumplimiento con el Protocolo de automatización de contenido de seguridad (SCAP). El Instituto Nacional de Estándares y Tecnología (NIST) de EE. UU. es el encargado de definir SCAP y de realizar su mantenimiento.

Las extensiones SCAP para Microsoft System Center Configuration Manager usan la característica Configuración de cumplimiento de Microsoft System Center Configuration Manager para analizar los equipos de su entorno y documentar su nivel de compatibilidad con las exigencias de la Línea base de configuración del gobierno de los Estados Unidos (USGCB).

Las extensiones permiten que Configuration Manager consuma los flujos de datos del Protocolo de automatización de contenido de seguridad (SCAP), evalúe el cumplimiento de los sistemas y genere resultados de informe en formato SCAP. De este modo, la organización puede aprovechar la infraestructura actual de Configuration Manager para garantizar que los equipos que administra cumplan este requisito de cumplimiento de normas federales y generen los informes USGCB necesarios para el Instituto Nacional de Estándares y Tecnología (NIST) de Estados Unidos. Oficina de administración y presupuesto (OMB).

En esta guía se ofrece información con la que podrá instalar, configurar y ejecutar las extensiones SCAP en su infraestructura de System Center Configuration Manager.



# <a name="what39s-new-in-scap-extensions-prerelease-for-microsoft-system-center-configuration-manager"></a>Novedades en la versión preliminar de las extensiones SCAP para Microsoft System Center Configuration Manager

Con esta sección aprenderá cuáles son las novedades de la versión más reciente.

Versión preliminar de extensiones SCAP para System Center Configuration Manager:

- Incluye una extensión de la consola de Configuration Manager totalmente compatible con conversiones de contenido de SCAP a líneas base de configuración de cumplimiento para la versión Rama actual de System Center Configuration Manager.
- Admite SCAP versión 1.2 y es compatible con las versiones 1.1 y 1.0 de SCAP.


  - Admite la versión 1.2 de Extensible Configuration Checklist Description Format (Formato de descripción de listas de comprobación de configuración extensible, XCCDF).
  - Admite hasta la versión 5.10 de Open Vulnerability and Assessment Language (Lenguaje abierto de evaluación y vulnerabilidad, OVAL).
  - Admite la generación de informes con Asset Reporting Format (Formato de informes de activos, ARF) 1.1.
  - Admite Common Platform Enumeration (Enumeración de plataforma común, CPE) 2.3
  - Admite Common Vulnerabilities and Exposures (Vulnerabilidades y exposiciones comunes, CVE)
  - Admite Common Configuration Enumeration (Enumeración de configuración común, CCE) versión 5
  - Admite USGCB Internet Explorer 8, USGCB Windows 7 y USGCB Windows 7 Firewall.

- Incluye un Asistente para la interfaz de usuario con el que se puede importar contenido de SCAP 1.2/1.1/1.0 y de OVAL para convertirlo en líneas base de configuración.


  - Permite la selección de secuencias de datos de origen SCAP, así como de bancos de pruebas XCCDF y perfiles para la conversión.

- Incluye un Asistente para la interfaz de usuario para exportar los resultados de la evaluación de configuración a informes XML con formato de SCAP.


  - Muestra el archivo de código fuente, el flujo de datos de SCAP, la prueba comparativa y el perfil de XCCDF usados para generar la línea base.
  - Admite la generación del informe Lightweight Asset Summary Results (LASR) de Cyberscope.

- Admite la generación de informes de SCAP basados en la implementación de la línea base de configuración. Incluye un nuevo panel para visualizar la conformidad del cliente, así como el cumplimiento de reglas de XCCDF. Con el panel se puede profundizar en informes más detallados donde puede buscar y filtrar.
- Mejora el rendimiento de varios tipos de elementos de configuración convertidos a partir de pruebas de OVAL, lo que permite una evaluación más rápida.

- Corrige varios problemas que se encuentran en el contenido de Windows 10 DISA v1r3.

# <a name="scap-extensions-for-microsoft-system-center-configuration-manager-deployment-process"></a>Proceso de implementación de extensiones SCAP para Microsoft System Center Configuration Manager

En esta guía se describe cómo analizar, evaluar e informar sobre el cumplimiento de SCAP mediante SCAP Extensions para Microsoft System Center Configuration Manager. Aquí se describen brevemente los procedimientos que debe seguir:

- Preparar la infraestructura de requisitos previos para aprovechar las extensiones.
- Instalar y configurar SCAP Extensions para Microsoft System Center Configuration Manager.
- Descargar, instalar y configurar los archivos de flujo de datos de SCAP desde la [Base de datos nacional de vulnerabilidad](http://nvd.nist.gov) (NVD).
- Convertir e importar los archivos de flujo de datos de SCAP directamente en una línea base de configuración de cumplimiento de System Center Configuration Manager, mediante el Asistente para importación **o** a través de un archivo contenedor (.cab) mediante la herramienta de línea de comandos de Microsoft.Sces.ScapToDcm.exe.
- Exportar los resultados de cumplimiento al formato de SCAP mediante el Asistente para exportación o la herramienta de línea de comandos de Microsoft.Sces.DcmToScap.exe.

# <a name="terms"></a>Términos

**Identificador de OVAL:** Identificador para una definición de OVAL específica que se ajusta al formato para identificadores de OVAL.

**Flujo de datos de resultados de SCAP:** Agrupación de componentes de SCAP, junto con las asignaciones de referencias entre componentes de SCAP, que incluyen contenido de salida (resultados).

**Flujo de datos de origen de SCAP:** agrupación de componentes de SCAP, junto con las asignaciones de referencias entre componentes de SCAP, que incluyen contenido de entrada (origen).

# <a name="prepare-the-prerequisite-infrastructure"></a>Preparar la infraestructura de requisitos previos

Asegúrese de que se cumplen los siguientes requisitos de hardware y software para aprovechar las ventajas de las extensiones SCAP para Microsoft System Center Configuration Manager.

## <a name="software-requirements"></a>Requisitos de software

Para instalar, configurar y ejecutar las extensiones SCAP para Microsoft System Center Configuration Manager, necesita un equipo con el software siguiente:

- Una [versión compatible](/sccm/core/servers/manage/current-branch-versions-supported) de la consola de la rama actual de System Center Configuration Manager.
- Un sistema operativo compatible con la consola de System Center Configuration Manager. Para obtener una lista de sistemas operativos compatibles, vea el artículo [Sistemas operativos compatibles con consolas de System Center Configuration Manager](/sccm/core/plan-design/configs/supported-operating-systems-consoles).

Además del equipo que ejecute las extensiones SCAP, también necesitará lo siguiente:

- Una infraestructura de rama actual de System Center Configuration Manager. Para saber más sobre los requisitos de una implementación de Configuration Manager, vea el artículo [Configuraciones admitidas para System Center Configuration Manager](/sccm/core/plan-design/configs/supported-configurations).

Los equipos cuyo cumplimiento de normas SCAP desea evaluar necesitan el software y las configuraciones siguientes:

- El componente de administración de configuración y cumplimiento habilitado en el cliente de Configuration Manager.
- Windows PowerShell 2.0 o superior.
- La directiva de ejecución de PowerShell de Configuration Manager definida en **Omitir**. Para saber más, vea el apartado [Directiva de ejecución de PowerShell](/sccm/core/clients/deploy/about-client-settings#computer-agent).
- Uno de los siguientes sistemas operativos:
  - Versión preliminar de Windows 7 o Sp1, 32 bits o 64 bits
  - Windows 10 (32 o 64 bits)
  - Windows Server 2012 R2

## <a name="hardware-requirements"></a>Requisitos de hardware

En este artículo se describen los requisitos mínimos del sistema:

[Planeación de las configuraciones de hardware en Configuration Manager](/sccm/core/plan-design/configs/recommended-hardware)



## <a name="accessibility-features"></a>Características de accesibilidad

Las extensiones SCAP para System Center Configuration Manager incluyen herramientas de línea de comandos de Windows que pueden aprovechar las características de accesibilidad y las herramientas de Windows.

- Los parámetros de línea de comandos se documentan en este manual del usuario para Microsoft.Sces.ScapToDcm.exe y Microsoft.Sces.DcmToScap.exe.
- -help y -? imprimirá el uso de la herramienta en la pantalla, donde estará disponible para los lectores de pantalla y otras tecnologías de asistencia.
- [Accesibilidad](http://windows.microsoft.com/windows/help/accessibility) de Windows

Las extensiones SCAP también usan las características de System Center Configuration Manager.  Configuration Manager incluye características que ayudan a que el producto sea más accesible para personas con discapacidades.

- [Características de accesibilidad de System Center Configuration Manager](/sccm/core/understand/accessibility-features)

Para obtener información general sobre los productos y servicios de accesibilidad de Microsoft, visite el sitio web [Accesibilidad de Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=9212).

## <a name="next-step"></a>Paso siguiente
> [!div class="nextstepaction"]
> [Instalar y configurar extensiones SCAP](/sccm/compliance/plan-design/scap/install-configure-scap)
