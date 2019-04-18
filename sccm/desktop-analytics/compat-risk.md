---
title: Riesgo de compatibilidad con aplicaciones Windows
titleSuffix: Configuration Manager
description: Obtenga información sobre los riesgos de compatibilidad para aplicaciones de Windows en el análisis de escritorio.
ms.date: 04/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: ea78f726-b1b3-49b0-8141-d916be48c458
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: bf2114ac77a75fedc18c38a8d373b9c0a1ada591
ms.sourcegitcommit: 6f4c2987debfba5d02ee67f6b461c1a988a3e201
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/17/2019
ms.locfileid: "59673418"
---
# <a name="compatibility-risk-for-windows-apps-in-desktop-analytics"></a>Riesgos de compatibilidad para aplicaciones de Windows en el análisis de escritorio

> [!Note]  
> Esta información se relaciona con un servicio en versión preliminar que puede modificarse sustancialmente antes de su lanzamiento comercial. Microsoft no ofrece ninguna garantía, expresa o implícita, con respecto a la información aquí proporcionada.  

Las evaluaciones de actualización de Windows Analytics eran genéricas, por ejemplo: Atención necesitado o la solución disponible. No ofrece ningún indicador visual para dar prioridad a las aplicaciones con problemas o actualizar la información. Análisis de escritorio reemplaza esta característica con **compatibilidad riesgo**. Escritorio Analytics muestra la evaluación de riesgos de la aplicación para las aplicaciones solo en la vista de implementación para un escenario previas a la actualización. Clasifica las aplicaciones basadas en información detallada que Microsoft obtiene de los equipos incluidos en un plan de implementación actual.

Análisis de escritorio usa las siguientes categorías de riesgo de compatibilidad:

- **Bajo**: Se encontró el servicio no actualización ningún señales de poner en peligro un Windows esta aplicación. Es probable que funcione en el sistema operativo de destino como-es.  

- **Medio**: Análisis indica que la aplicación puede deficiencias funcionalidad, aunque la corrección es probable que posible.  

- **Alta**: La aplicación es casi seguro que producirá un error durante o después de la actualización. Puede que necesite una corrección.  

- **Desconocido**: La aplicación no se ha evaluado por el analizador de mantenimiento de la aplicación. Como no hay ninguna otra información útil *problemas conocidos de MS* o *listos para Windows*.  



## <a name="risk-assessment-engine"></a>Motor de evaluación de riesgos

Hay varios orígenes que el analizador de mantenimiento de la aplicación se usa para generar la clasificación de riesgo.

![Diagrama de áreas de motor de evaluación de riesgo de analizador de mantenimiento de la aplicación](media/aha-risk-assessment-engine.png)


### <a name="ms-known-issues"></a>Problemas conocidos de MS

El analizador de mantenimiento de la aplicación examina la base de datos de compatibilidad de aplicaciones de Microsoft para todos los problemas conocidos. Esta base de datos usa para determinar los bloques existentes de compatibilidad para las aplicaciones disponibles públicamente desde Microsoft o de otros editores. Esta comprobación sólo se aplica para el sistema operativo de destino para el plan de implementación que seleccione.


### <a name="ready-for-windows"></a>Listo para Windows

El [listos para Windows](https://www.readyforwindows.com) catálogo de aplicaciones pone en correlación datos de diagnóstico desde otros clientes que informan de las mismas aplicaciones con comprobaciones adicionales de Microsoft como bloques de compatibilidad en un dispositivo. 

Las categorías posibles son:

- **Datos insuficientes** significa muy pocos dispositivos comerciales de Windows 10 están compartiendo información para esta aplicación para que Microsoft pueda clasificar su adopción.

- **Adoptado** significa que la aplicación se ha instalado en al menos 10 000 dispositivos comerciales de Windows 10.  

- **Alta adopción** significa que la aplicación se ha instalado en al menos 100 000 dispositivos comerciales de Windows 10.  

- **Póngase en contacto con el desarrollador** significa que puede haber problemas de compatibilidad con esta solución y, por tanto, Microsoft recomienda ponerse en contacto con el proveedor de software para obtener más información.  

### <a name="app-health-analyzer-signals-for-compatibility-assessment"></a>Analizador de mantenimiento de la aplicación se señala para su evaluación de compatibilidad

Usar el Kit de herramientas del analizador de mantenimiento de la aplicación para recopilar señales adicionales para la compatibilidad de aplicaciones. Para obtener más información, consulte [analizador de mantenimiento de la aplicación](/sccm/desktop-analytics/app-health-analyzer).

Las señales siguientes están disponibles actualmente:

#### <a name="adopted-version-available"></a>Versión aprobada disponible

Hay otra versión de la aplicación que es alta adopción con otros clientes. Esta señal utiliza datos de listo para Windows. Si hay algún Bloqueador de actualización con su versión actual, considere la posibilidad de implementar la versión alternativa en su lugar.

#### <a name="16-bit"></a>16 bits

Quitar todos los componentes de 16 bits de las aplicaciones y reemplace por sus equivalentes de 32 bits o 64 bits. Para obtener más información, consulte [historias de desarrolladores de Windows Server 2008 y de la Vista de Windows: Guía de compatibilidad de aplicaciones](https://msdn.microsoft.com/library/aa480152.aspx).

La otra opción es permitirle NT Virtual DOS Machine (NTVDM) para obtener soporte técnico en Windows 10.

#### <a name="requires-admin-privileges"></a>Requiere privilegios de administrador

La aplicación requiere que el usuario tenga acceso administrativo al dispositivo. Use un manifiesto de aplicación para estas aplicaciones que requieren permisos de administrador. Para obtener más información, consulte [crear e incrustar un manifiesto de aplicación](https://msdn.microsoft.com/library/bb756929.aspx).
<!--Is this a better, more current link? https://docs.microsoft.com/windows/desktop/sbscs/application-manifests-->

Análisis de escritorio, recomienda la aplicación para las pruebas piloto. Debería funcionar bien para piloto, pero encontrará las regresiones.

#### <a name="java-dependency"></a>Dependencia de Java

Muchas aplicaciones de Java se basan en un entorno de tiempo de ejecución de Java (JRE) instalado por separado. Mientras que las versiones JRE anteriores pueden continuar trabajando en Windows 10, Oracle sólo admite las últimas versiones JRE. El uso de un JRE no admitida anterior puede tener vulnerabilidades de seguridad. Compruebe que la aplicación se ejecuta en las últimas versiones JRE.

#### <a name="not-dpi-aware"></a>Reconocimiento de PPP no

La aplicación puede tener problemas de visualización con resoluciones de pantalla avanzada en Windows 10. Use un manifiesto de aplicación para evitar cualquier problema con altas resoluciones de PPP. Para obtener más información, consulte [manifiestos de aplicación](https://docs.microsoft.com/windows/desktop/SbsCs/application-manifests).

Análisis de escritorio, recomienda la aplicación para las pruebas piloto. Debería funcionar bien para piloto, pero encontrará las regresiones.

#### <a name="visual-basic-version-6-vb6"></a>Visual Basic versión 6 (VB6)

Análisis de escritorio, recomienda la aplicación para las pruebas piloto. Aplicaciones de VB6 a menudo son compatibles. Si la aplicación retrocede durante la prueba piloto debido a las dependencias adicionales y los widgets, debe actualizar la aplicación a Visual Basic .NET

#### <a name="os-version-dependency"></a>Dependencia de la versión del sistema operativo

Considere la posibilidad de volver a desarrollar la aplicación para usar la API de las aplicaciones auxiliares de versión o manifiesto de la aplicación de destino Windows 10.

Análisis de escritorio, recomienda la aplicación para las pruebas piloto. Debería funcionar bien para piloto, pero encontrará las regresiones.

#### <a name="silverlight-framework"></a>Marco de Silverlight

Microsoft recomienda que las aplicaciones no basadas en explorador no usar Silverlight. La fecha de finalización del soporte técnico de Silverlight 5 es de 2021 de octubre.

Los exploradores web más actuales no admiten Silverlight.

| Explorador | Compatibilidad |
|---------|---------|
| Google Chrome | Finalización del soporte técnico: Septiembre de 2015 |
| Firefox | Finalización del soporte técnico: Marzo de 2017 |
| Microsoft Edge | Ningún complemento disponible |

Análisis de escritorio, recomienda la aplicación para las pruebas piloto. Debería funcionar bien para piloto, pero encontrará las regresiones.

#### <a name="net-framework-1011"></a>.NET framework 1.0/1.1

La versión de .NET framework 1.0 no es compatible con Windows 10. Versión 1.1 no es compatible en Windows 10. Si la aplicación procede de un editor de terceros, póngase en contacto con el proveedor para solicitar una versión que sea compatible con Windows 10. En caso contrario, rediseñar la aplicación para usar una versión compatible de. NET.

#### <a name="net-framework-2030"></a>.NET framework 2.0 y 3.0

.NET 2.0 y 3.5 marcos se admiten en Windows 10. Es posible que deba habilitar la característica de Windows. Para obtener más información, consulte [instalar .NET Framework 3.5 en Windows 10](https://docs.microsoft.com/dotnet/framework/install/dotnet-35-windows-10).

#### <a name="ui-access"></a>Acceso de interfaz de usuario

Las aplicaciones con acceso de interfaz de usuario pueden omitir los niveles de control de interfaz de usuario para controlar la entrada a mayor privilegio windows en el escritorio. Utilice esta configuración sólo para las aplicaciones de tecnología de interfaz de usuario.

Si no usa características de accesibilidad en la aplicación, establezca la marca de acceso de la interfaz de usuario en el manifiesto de aplicación en false. Para obtener más información, consulte [crear e incrustar un manifiesto de aplicación](https://msdn.microsoft.com/library/bb756929.aspx).

#### <a name="driver-dependency"></a>Dependencia del controlador

La aplicación es dependiente de un controlador. Análisis de escritorio, recomienda la aplicación para las pruebas piloto. Debería funcionar bien para piloto, pero encontrará las regresiones. Si tiene problemas, póngase en contacto con el publicador para solicitar una versión que sea compatible con Windows 10.



## <a name="app-confidence-simulation-for-a-sample-population"></a>Simulación de confianza de aplicación para una población de muestra

Los gráficos siguientes provienen de un caso práctico de ejemplo. Estos datos resaltan el uso del analizador de mantenimiento de aplicación con análisis de escritorio para adoptar un enfoque controlado por datos para la validación de la aplicación. Este enfoque puede ayudar a reducir el tiempo y esfuerzo en las pruebas de las aplicaciones durante la actualización de Windows 10.

Estos datos muestran las métricas de confianza para dispositivos de 60 con 899 aplicaciones, incluidas las aplicaciones de línea de negocio.

![Antes y después de gráficos que muestran la confianza de la aplicación](media/aha-app-confidence-simulation.png)


## <a name="see-also"></a>Consulte también

La ventaja de centro de FastTrack para Windows 10 proporciona acceso a **asegurar aplicaciones de escritorio**. Esta ventaja es un nuevo servicio diseñado para solucionar problemas con Windows 10 y compatibilidad de aplicaciones de Office 365 ProPlus. Para obtener más información, consulte [asegurar aplicaciones de escritorio](https://docs.microsoft.com/fasttrack/win-10-desktop-app-assure).
