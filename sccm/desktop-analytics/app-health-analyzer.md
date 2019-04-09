---
title: Analizador de mantenimiento de la aplicación
titleSuffix: Configuration Manager
description: Guía de procedimientos para evaluar la compatibilidad con el analizador de mantenimiento de la aplicación en el escritorio de análisis.
ms.date: 04/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 2af150a4-0c18-4b40-8492-c04c5d154596
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 21b4907667e055c9595b31eedf9da0ad516b5fec
ms.sourcegitcommit: 5ee9487c891c37916294bd34a10d04e398f111f7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2019
ms.locfileid: "59069371"
---
# <a name="how-to-assess-compatibility-with-app-health-analyzer"></a>Cómo evaluar la compatibilidad con el analizador de mantenimiento de la aplicación

> [!Note]  
> Esta información se relaciona con un servicio en versión preliminar que puede modificarse sustancialmente antes de su lanzamiento comercial. Microsoft no ofrece ninguna garantía, expresa o implícita, con respecto a la información aquí proporcionada.  

Utilice el Kit de herramientas del analizador de mantenimiento de la aplicación para el análisis de escritorio para evaluar los problemas de compatibilidad de aplicaciones de escritorio. Ayuda a centrar sus esfuerzos de validación para las aplicaciones de escritorio, incluidas las aplicaciones de línea de negocio. La herramienta proporciona una clasificación de riesgo, junto con las acciones correctoras posibles. También incluye un informe de disponibilidad de la aplicación que le ayudarán a evaluar la preparación de la aplicación para las actualizaciones de Windows 10.



## <a name="download"></a>Descargar

Descargue el Kit de herramientas desde el [Microsoft Download Center](http://download.microsoft.com/download/3/7/D/37D7E378-D805-4822-A712-4EADBF50FC08/AppHealthAnalyzer.zip)<!-- (https://www.microsoft.com/download/details.aspx?id=57276) -->. Use siempre la versión más reciente.

La descarga es un archivo de Windows Installer (MSI). Instalar el Kit de herramientas del analizador de mantenimiento de la aplicación en el equipo del usuario. Al ejecutar el Kit de herramientas, un asistente le guía a través del proceso de creación de un informe de preparación para la aplicación.

El Kit de herramientas incluye scripts de muestra. Si necesita automatizar la recopilación de información de preparación de los dispositivos en toda la organización, puede usar Configuration Manager para implementar estos scripts. Para obtener más información, consulte [automatización](#automation).



## <a name="how-it-works"></a>Cómo funciona

La herramienta realiza un análisis estático de las aplicaciones que ya están instalados en un dispositivo. No hace un análisis de un instalador de aplicación del paquete. Un usuario no necesita ejecutar la aplicación. La herramienta evalúa todas las aplicaciones instaladas registradas con Windows en el dispositivo.

Analizador de mantenimiento de la aplicación no requiere mantener instaladores para aplicaciones heredadas que no administra activamente. Identifica los problemas de compatibilidad con la aplicación en su estado instalado. Todas las aplicaciones se evalúan para reglas de compatibilidad predefinidos. Estas señales son problemas frecuentes comunes que se notifican a Microsoft cuando los clientes actualicen a Windows 10. La información de compatibilidad también incluye las acciones correctoras posibles o correcciones. Si tiene aplicaciones con problemas, comience con las acciones sugeridas.

> [!Important]  
> El Kit de herramientas no es compatible con las características para reparar o resolver las aplicaciones. Si crea un informe de preparación para la aplicación, proporciona información y orientación que le ayudarán a corregir las aplicaciones antes de actualizar a Windows 10.  



## <a name="prerequisites"></a>Requisitos previos

Antes de instalar y usar el Kit de herramientas, asegúrese de que el dispositivo cumple los requisitos siguientes:  

- Windows 7 Service Pack 1 o posterior  

- Tener privilegios de administrador en el dispositivo  

- Microsoft .NET Framework 4.5.1 o posterior  

- Inscritos en el servicio de análisis de escritorio, que incluye los siguientes requisitos:  

    - Actualizaciones más recientes. Para obtener más información, consulte [actualizar dispositivos](/sccm/desktop-analytics/enroll-devices#update-devices).  

    - Nivel de datos de diagnóstico. Para obtener más información, consulte [niveles de datos de diagnóstico](/sccm/desktop-analytics/enable-data-sharing#diagnostic-data-levels).  



## <a name="analyze"></a>Analizar

1. Instalar el analizador de mantenimiento de la aplicación en el dispositivo de destino. De forma predeterminada, se instala en la ruta de acceso siguiente: `C:\Program Files\Microsoft Corporation\Microsoft App Health Analyzer`  

2. Vaya a la Windows **iniciar** menú, expanda el **analizador de mantenimiento de aplicación de Microsoft** y abra el **analizador de mantenimiento de la aplicación** como administrador. Puede tardar varios minutos en generar el informe.  

    > [!Note]  
    > Si cualquiera de los valores de datos de diagnóstico requeridos no están configurado, verá un error. Asegúrese de que configurar correctamente la configuración de requisitos previos. Para obtener más información, consulte [niveles de datos de diagnóstico](/sccm/desktop-analytics/enable-data-sharing#diagnostic-data-levels).  

3. Cuando se abre el informe de preparación de la aplicación, se inicia la evaluación de las aplicaciones. Espere a que el Kit de herramientas hasta el final, lo que puede tardar tiempo en función del número de aplicaciones en el dispositivo.  

![Captura de pantalla del informe de preparación para la aplicación del analizador de mantenimiento de aplicación](media/app-readiness-report-evaluating.png)

Puede minimizar la ventana y continuar con otras tareas mientras se ejecuta el Kit de herramientas en segundo plano.


### <a name="app-readiness-report-features"></a>Características de informe de preparación de aplicaciones

#### <a name="get-started"></a>Introducción

Esta ficha proporciona una visión general de las señales admitidas en esta versión actual. También incluye las acciones correctoras posibles.

#### <a name="insights"></a>Insights

Esta ficha proporciona una vista de todas las aplicaciones de la herramienta evalúa. Muestra la evaluación de riesgos y diversas señales que se usan para identificar problemas de compatibilidad.

- **Las señales** menú: Filtrar estas aplicaciones mediante señales mediante el menú de la izquierda  

- **Exportar a CSV**: Exportar esta información como un archivo de valores separados por comas (CSV)  

- **Volver a examinar aplicaciones**: Si instala las aplicaciones nuevas, use esta opción para volver a ejecutar la herramienta  

- **Id. de la solución de problemas**: Si el dispositivo ha instalado las aplicaciones y no ver ninguna información en el informe, proporcione este Id. para admitir  

#### <a name="desktop-analytics"></a>Análisis de escritorio

Esta pestaña proporciona información general de cómo usar el analizador de mantenimiento de aplicación para proporcionar información de disponibilidad para las aplicaciones en toda la organización.



## <a name="automation"></a>Automation

Para obtener esta información de la aplicación en varios dispositivos, implemente la versión de línea de comandos del analizador de mantenimiento de la aplicación con Configuration Manager. Implementar en un pequeño conjunto de dispositivos representativos dentro de su organización. Por ejemplo, utilice los análisis de escritorio *piloto* colección. El mismo [requisitos previos](#prerequisites) se aplican a estos dispositivos.

Antes de realizar una implementación más amplia, compruebe en primer lugar una ejecución correcta. Asegúrese de que se muestren los datos en análisis de escritorio.

El Kit de herramientas del analizador de mantenimiento de la aplicación incluye un script de ejemplo, run_silent.cmd. De forma predeterminada, esta secuencia de comandos es la ruta de acceso: `C:\Program Files\Microsoft Corporation\Microsoft App Health Analyzer`. Use este script para automatizar el proceso con el Administrador de configuración.


### <a name="tips"></a>Sugerencias

- Antes de actualizar para el sistema operativo de destino, implemente el analizador de mantenimiento de la aplicación en todos los dispositivos de la prueba piloto. Para obtener información de disponibilidad efectiva, ejecute al menos una vez en el grupo piloto para un plan de implementación.  

- Análisis de escritorio tiene funcionalidad integrada para recomendar grupos piloto de los planes de implementación. Ejecutar el Kit de herramientas en todos los dispositivos pilotos para obtener una cobertura completa de las aplicaciones importantes.  

- Programar la herramienta para ejecutar cuando un usuario no se ha iniciado sesión, o cuando no se usa el dispositivo.  

- Configurar una programación periódica. Por ejemplo, ejecútelo cada 30 días. Esta programación Obtiene la información más reciente de la preparación de los dispositivos que les ayuden a mantenerse al día.  



## <a name="desktop-analytics-integration"></a>Integración de análisis de escritorio

La siguiente captura de pantalla de escritorio Analytics muestra los detalles de la versión 1.15.25 ContosoApp.

- Tiene un **medio** evaluación de riesgos  
- Está disponible una versión aprobada  
- Tiene una dependencia del controlador  

![Análisis de escritorio que muestra los factores de riesgo de compatibilidad de una aplicación](media/aha-desktop-analytics-compat-risk-factors.png)



## <a name="troubleshooting"></a>Solución de problemas

En esta sección se trata los pasos para solucionar problemas y problemas operativos más comunes que puede aparecer con el analizador de mantenimiento de la aplicación. Por ejemplo:

- No ve la pantalla de bienvenida en el analizador de mantenimiento de aplicación  

- Hay aplicaciones instaladas en el dispositivo, pero no ve ninguna información en el informe de preparación de la aplicación  

- No ocurre nada al ejecutar la herramienta  

### <a name="diagnostic-data-settings"></a>Configuración de datos de diagnóstico

Vuelva a comprobar las configuraciones para los valores de datos de diagnóstico de Windows. Administrador de configuración debe establecer estos valores cuando el incorpora dispositivos a análisis de escritorio. Puede usar otros métodos como la directiva de secuencia de comandos o un grupo como solución alternativa. Para obtener más información, consulte [niveles de datos de diagnóstico](/sccm/desktop-analytics/enable-data-sharing#diagnostic-data-levels).  

### <a name="verbose-mode"></a>Modo detallado

Ejecute la herramienta en modo detallado con el script run_verbose.cmd. De forma predeterminada, el script está en la ruta de acceso siguiente: `C:\Program Files\Microsoft Corporation\Microsoft App Health Analyzer\run_verbose.cmd`

El modo detallado genera registros adicionales, que pueden ayudarle a solucionar los problemas potenciales. Guarda los registros para el `LogCollection` carpeta en la ubicación de instalación. Por ejemplo, la ruta de acceso de colección de registro predeterminada es: `C:\Program Files\Microsoft Corporation\Microsoft App Health Analyzer\LogCollection\`


## <a name="see-also"></a>Consulte también

La ventaja de centro de FastTrack para Windows 10 proporciona acceso a **asegurar aplicaciones de escritorio**. Esta ventaja es un nuevo servicio diseñado para solucionar problemas con Windows 10 y compatibilidad de aplicaciones de Office 365 ProPlus. Para obtener más información, consulte [asegurar aplicaciones de escritorio](https://docs.microsoft.com/fasttrack/win-10-desktop-app-assure).
