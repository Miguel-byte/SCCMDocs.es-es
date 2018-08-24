---
title: Extensiones SCAP
titleSuffix: Configuraton Manager
description: Conozca las extensiones de Security Content Automation Protocol (SCAP) para Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: a315489d-5e12-46d6-903e-3a35235b72c5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0992b3853776cc487c6c0a88d80cbce21bf79782
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/31/2018
ms.locfileid: "39384861"
---
# <a name="about-the-security-content-automation-protocol-scap-extensions"></a>Extensiones de Security Content Automation Protocol (SCAP)

*Se aplica a: System Center Configuration Manager (Rama actual)*

Con las extensiones SCAP para Configuration Manager es más fácil analizar y evaluar el entorno de red para garantizar el cumplimiento con el Protocolo de automatización de contenido de seguridad (SCAP). El Instituto Nacional de Normas y Tecnología (NIST) de los Estados Unidos se encarga de definir y mantener el protocolo SCAP. Para obtener más información, vea la [SCAP Project Overview (Información general del proyecto SCAP)](https://csrc.nist.gov/projects/security-content-automation-protocol).

Las extensiones SCAP para Configuration Manager usan la característica de configuración de cumplimiento para analizar primero los equipos de su entorno. Después documenta su nivel de compatibilidad con línea de base de configuración del gobierno de los Estados Unidos (USGCB).

Las extensiones permiten que Configuration Manager consuma los flujos de datos del SCAP, evalúe el cumplimiento de los sistemas y genere resultados de informe en formato SCAP. Su organización puede utilizar la infraestructura existente de Configuration Manager para ayudar a garantizar que los equipos que administra cumplan este requisito de cumplimiento de normas federales. También puede usar Configuration Manager para generar los informes USGCB que necesitan NIST y la Oficina de administración y presupuesto (OMB).

Este artículo ofrece información con la que podrá instalar, configurar y ejecutar las extensiones SCAP en su infraestructura de Configuration Manager.



## <a name="whats-new"></a>Novedades

Esta versión de las extensiones SCEP para Configuration Manager incluye y admite las siguientes características:  

- Una extensión de consola de Configuration Manager, que es compatible con convertir contenido SCAP a líneas de base de configuración de cumplimiento.  

- SCAP versión 1.2, que incluye los siguientes componentes:  

  - la versión 1.2 de Extensible Configuration Checklist Description Format (XCCDF)
  - la versión 5.10 de Open Vulnerability and Assessment Language (OVAL)
  - la generación de informes con Asset Reporting Format (ARF) 1.1
  - Common Platform Enumeration (CPE) 2.3
  - Common Vulnerabilities and Exposures (CVE)
  - la versión 5 de Common Configuration Enumeration (CCE)
  - USGCB Internet Explorer 8, USGCB Windows 7 y USGCB Windows 7 Firewall  

- Compatible con las versiones 1.0 y 1.1 de SCAP.  

- Un asistente para la consola con el que se puede importar contenido de SCAP 1.2/1.1/1.0 y de OVAL para convertirlo en líneas base de configuración.  

  - Permite la selección de secuencias de datos de origen SCAP, así como de bancos de pruebas XCCDF y perfiles para la conversión.

- Un asistente para la interfaz de usuario para exportar los resultados de la evaluación de configuración a informes XML con formato de SCAP.  

  - Muestra el archivo de código fuente, el flujo de datos de SCAP, la prueba comparativa y el perfil de XCCDF usados para generar la línea base.
  - Generar el informe Lightweight Asset Summary Results (LASR) de Cyberscope.  

- Generar informes de SCAP basados en la implementación de la línea base de configuración. Este componente incluye un nuevo panel para visualizar la conformidad del cliente, así como el cumplimiento de reglas de XCCDF. Con el panel se puede profundizar en informes más detallados donde puede buscar y filtrar.  

- Rendimiento mejorado de varios tipos de elementos de configuración convertidos a partir de pruebas de OVAL, lo que permite una evaluación más rápida.  

- Corrige varios problemas que se encuentran en el contenido de Windows 10 DISA v1r3.  



## <a name="terms"></a>Términos

- **Identificador de OVAL:** un identificador para una definición de OVAL específica que se ajusta al formato para identificadores de OVAL.  

- **Flujo de datos de resultados de SCAP:** una agrupación de componentes de SCAP, junto con las asignaciones de referencias entre componentes de SCAP, que incluyen contenido de salida (resultados).  

- **Flujo de datos de origen de SCAP:** una agrupación de componentes de SCAP, junto con las asignaciones de referencias entre componentes de SCAP, que incluyen contenido de entrada (origen).



## <a name="deployment-process"></a>Proceso de implementación

Este es un resumen del proceso de implementación general:  

- [Preparar la infraestructura](#bkmk_prepare) para utilizar las extensiones  

- [Instalar y configurar extensiones SCAP](/sccm/compliance/plan-design/scap/install-configure-scap#bkmk_install) para Configuration Manager  

- [Descargar e instalar los archivos de flujo de datos de SCAP](/sccm/compliance/plan-design/scap/install-configure-scap#bkmk_scap-data-stream-files) de NIST  

- Convierta e importe los archivos de flujo de datos de SCAP en una línea de base de configuración de cumplimiento de Configuration Manager. Use uno de los dos métodos siguientes:   

    - [Proceso manual](/sccm/compliance/plan-design/scap/install-configure-scap#bkmk_convert-and-import) mediante el Asistente para la importación de la consola de Configuration Manager  

    - [Proceso automatizado](/sccm/compliance/plan-design/scap/install-configure-scap#bkmk_auto-convert-and-import) con la herramienta de línea de comandos de Microsoft.Sces.ScapToDcm.exe  

- [Implementar](/sccm/compliance/plan-design/scap/deploy-monitor-export#bkmk_deploy) las líneas de base de configuración para colecciones  

- [Supervisar](/sccm/compliance/plan-design/scap/deploy-monitor-export#bkmk_monitor) los datos de cumplimiento  

- Exporte los resultados de cumplimiento al formato de SCAP mediante uno de los dos métodos siguientes:  

    - [Proceso manual](/sccm/compliance/plan-design/scap/deploy-monitor-export#bkmk_export) mediante el Asistente para exportación de la consola  

    - [Proceso automatizado](/sccm/compliance/plan-design/scap/deploy-monitor-export#bkmk_auto-export) con la herramienta de línea de comandos de Microsoft.Sces.DcmToScap.exe  



## <a name="bkmk_prepare"></a> Preparar la infraestructura

### <a name="software-requirements"></a>Requisitos de software

Para instalar, configurar y ejecutar las extensiones SCAP para Configuration Manager, necesita un equipo con el software siguiente:

- Una [versión compatible](/sccm/core/servers/manage/current-branch-versions-supported) de la consola de la rama actual de Configuration Manager.  

- Una versión de SO compatible con la consola de Configuration Manager. Para obtener más información, vea [Sistemas operativos compatibles con las consolas de Configuration Manager](/sccm/core/plan-design/configs/supported-operating-systems-consoles).  

Además del equipo que ejecute las extensiones SCAP, también necesitará lo siguiente:

- Una infraestructura de rama actual de Configuration Manager. Para saber más sobre los requisitos de una implementación de Configuration Manager, vea el artículo [Configuraciones admitidas para System Center Configuration Manager](/sccm/core/plan-design/configs/supported-configurations).  

Los equipos cuyo cumplimiento de normas SCAP desea evaluar necesitan el software y las configuraciones siguientes:

- El cliente de Configuration Manager.  

- Windows PowerShell 2.0 o superior.  

- La directiva de ejecución de PowerShell de Configuration Manager definida en **Omitir**. Para saber más, vea el apartado [Directiva de ejecución de PowerShell](/sccm/core/clients/deploy/about-client-settings#computer-agent).  

- Uno de los siguientes sistemas operativos:  
  - Windows 7 SP1 32 o 64 bits
  - Windows 10 32 o 64 bits
  - Windows Server 2012 R2

### <a name="hardware-requirements"></a>Requisitos de hardware

Para saber más sobre los requisitos del sistema mínimos de Configuration Manager, vea [Planificar configuraciones de hardware para Configuration Manager](/sccm/core/plan-design/configs/recommended-hardware).



## <a name="accessibility-features"></a>Características de accesibilidad

Las extensiones SCAP para Configuration Manager incluyen herramientas de línea de comandos de Windows. Estas herramientas pueden aprovechar las ventajas de las características de accesibilidad y herramientas de Windows.

- Los parámetros de línea de comandos se documentan para Microsoft.Sces.ScapToDcm.exe y Microsoft.Sces.DcmToScap.exe. Para obtener más información, consulte [Microsoft.Sces.ScapToDcm.exe. Parámetros de la línea de comandos](/sccm/compliance/plan-design/scap/install-configure-scap#microsoftscesscaptodcmexe-command-line-parameters) y [Parámetros de la línea de comandos de Microsoft.Sces.DcmToScap.exe](/sccm/compliance/plan-design/scap/import-scap-compliance-settings#microsoftscesdcmtoscapexe-command-line-parameters).  

- Los parámetros de la línea de comandos `-help` y `-?` para cada herramienta imprimen el uso en la pantalla. Estos detalles de uso después están disponibles para los lectores de pantalla y otras tecnologías de asistencia.  

- Para obtener más información, consulte [Windows Update](http://windows.microsoft.com/windows/help/accessibility).

Las extensiones SCAP también usan las características de accesibilidad de Configuration Manager. Para obtener la información, vea [Características de accesibilidad de Configuration Manager](/sccm/core/understand/accessibility-features).

Para obtener más información sobre los productos y servicios de accesibilidad de Microsoft, vea el sitio web [Accesibilidad de Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=9212).



## <a name="next-step"></a>Paso siguiente
> [!div class="nextstepaction"]
> [Instalación y configuración de extensiones SCAP](/sccm/compliance/plan-design/scap/install-configure-scap)
