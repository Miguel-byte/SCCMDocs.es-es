---
title: Evaluación de compatibilidad
titleSuffix: Configuration Manager
description: Obtenga información acerca de la evaluación de compatibilidad de aplicaciones de Windows y controladores en el escritorio de análisis.
ms.date: 06/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: ea78f726-b1b3-49b0-8141-d916be48c458
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: bef2c11732177dfb842f0961dc2d5d5a69edd55e
ms.sourcegitcommit: d47d2f03482e48d343e2139a341e61022331e6c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/14/2019
ms.locfileid: "67148102"
---
# <a name="compatibility-assessment-in-desktop-analytics"></a>Evaluación de compatibilidad de análisis de escritorio

> [!Note]  
> Esta información se relaciona con un servicio en versión preliminar que puede modificarse sustancialmente antes de su lanzamiento comercial. Microsoft no ofrece ninguna garantía, expresa o implícita, con respecto a la información aquí proporcionada.  

Las evaluaciones de actualización de Windows Analytics eran genéricas, por ejemplo: Atención necesitado o la solución disponible. No ofrece ningún indicador visual para dar prioridad a las aplicaciones o controladores con problemas o actualizar la información. Análisis de escritorio reemplaza esta característica con **compatibilidad riesgo**. Análisis de escritorio muestran la valoración de las aplicaciones solo en la vista de implementación para un escenario de actualización previa. Clasifica las aplicaciones basadas en información detallada que Microsoft obtiene de los equipos incluidos en un plan de implementación actual.

Análisis de escritorio usa las siguientes categorías de evaluación de compatibilidad:

- **Bajo**: Se encontró el servicio no actualización ningún señales de poner en peligro un Windows esta aplicación. Es probable que funcione en el sistema operativo de destino como-es.  

- **Medio**: Análisis indica que la aplicación puede deficiencias funcionalidad, aunque la corrección es probable que posible.  

- **Alta**: La aplicación es casi seguro que producirá un error durante o después de la actualización. Puede que necesite una corrección.  

- **Desconocido**: No se ha evaluado la aplicación. Como no hay ninguna otra información útil *problemas conocidos de MS* o *listos para Windows*.  

En la lista de aplicaciones o controladores activos en un plan de implementación, podrá ver este valor para cada activo en el **compatibilidad riesgo** columna.


## <a name="app-risk-assessment"></a>Evaluación de riesgos de la aplicación

Hay varios orígenes que análisis de escritorio que se usa para generar la clasificación de evaluación para las aplicaciones:

- [Problemas conocidos de Microsoft](#microsoft-known-issues)
- [Listo para el catálogo de Windows](#ready-for-windows)
- [Información avanzada](#advanced-insights)

Puede encontrar la evaluación para cada origen de la aplicación de escritorio de análisis. En la lista de recursos de la aplicación en un plan de implementación, seleccione una aplicación para abrir su panel de control flotante de propiedades individual. Verá un nivel general de evaluación y recomendación. El **factores de riesgo de compatibilidad** sección muestra los detalles de estas evaluaciones.


## <a name="microsoft-known-issues"></a>Problemas conocidos de Microsoft

Escritorio análisis examinan la base de datos de compatibilidad de aplicaciones de Microsoft para todos los problemas conocidos. Esta base de datos usa para determinar los bloques existentes de compatibilidad para las aplicaciones disponibles públicamente desde Microsoft o de otros editores. Esta comprobación sólo se aplica para el sistema operativo de destino para el plan de implementación que seleccione.

Verá lo siguiente en el panel de propiedades de la aplicación como **problemas conocidos de MS**:

### <a name="application-is-removed-during-upgrade"></a>Se quita la aplicación durante la actualización

Windows ha detectado problemas de compatibilidad. La aplicación no migra a la nueva versión del sistema operativo. Se requiere para la actualización continuar ninguna acción.

### <a name="blocking-upgrade"></a>Bloqueo de actualización

Windows detectan problemas de bloqueo y no pueden quitar la aplicación durante la actualización. No puede funcionar en la nueva versión del sistema operativo. Antes de actualizar, quitar la aplicación. Vuelva a instalar y probarla en la nueva versión del sistema operativo.

### <a name="blocking-upgrade-but-can-be-reinstalled-after-upgrading"></a>Bloqueo de actualización, pero puede volver a instalar después de actualizar

La aplicación es compatible con la nueva versión del sistema operativo, pero no se migrará. Quitar la aplicación antes de actualizar Windows. Vuelva a instalarlo en la nueva versión del sistema operativo.

### <a name="blocking-upgrade-update-application-to-newest-version"></a>Bloqueo de actualización, actualice la aplicación a la versión más reciente

La versión existente de la aplicación no es compatible con la nueva versión del sistema operativo y no se migrará. Hay disponible una versión compatible de la aplicación. Actualizar la aplicación antes de actualizar.

### <a name="disk-encryption-blocking-upgrade"></a>Actualización bloquea de cifrado de disco

Características de cifrado de la aplicación bloquean la actualización. Deshabilitar la característica de cifrado antes de actualizar a Windows y habilitarlo después de la actualización.

### <a name="does-not-work-with-new-os-but-wont-block-upgrade"></a>No funciona con el nuevo sistema operativo, pero no bloquear la actualización

La aplicación no es compatible con la nueva versión del sistema operativo, pero no puede bloquear la actualización. Se requiere para la actualización continuar ninguna acción. Instale una versión compatible de la aplicación en la nueva versión del sistema operativo.

### <a name="does-not-work-with-new-os-and-will-block-upgrade"></a>No funciona con el nuevo sistema operativo y bloqueará la actualización

La aplicación no es compatible con la nueva versión del sistema operativo y bloqueará la actualización. Quitar la aplicación antes de actualizar. Una versión compatible de la aplicación puede estar disponible.

### <a name="evaluate-application-on-new-os"></a>Evaluar la aplicación en el nuevo sistema operativo

Windows migrará la aplicación, pero detectó problemas que pueden afectar al rendimiento de la aplicación en la nueva versión del sistema operativo. Se requiere para la actualización continuar ninguna acción. Probar la aplicación en la nueva versión del sistema operativo.

### <a name="may-block-upgrade-test-application"></a>Puede bloquear la actualización, probar la aplicación

Windows ha detectado problemas que pueden interferir con la actualización, pero necesita más investigación. Probar el comportamiento de la aplicación durante la actualización. Si bloquea la actualización, quite antes de actualizar. A continuación, vuelva a instalarlo y prueba en la nueva versión del sistema operativo.

### <a name="multiple"></a>Varios

Varios problemas afectan a la aplicación. Seleccione **consulta** para ver detalles sobre los problemas detectados por Windows.

### <a name="reinstall-application-after-upgrading"></a>Vuelva a instalar la aplicación después de actualizar

La aplicación es compatible con la nueva versión del sistema operativo, pero deberá volver a instalarlo después de actualizar Windows. El proceso de actualización quita la aplicación. Se requiere para la actualización continuar ninguna acción. Volver a instalar la aplicación en la nueva versión del sistema operativo.


## <a name="ready-for-windows"></a>Listo para Windows

El [listos para Windows](https://www.readyforwindows.com) catálogo de aplicaciones correlaciona los orígenes de datos siguientes:

- Datos de diagnóstico desde otros clientes que informan de las mismas aplicaciones
- Comprobaciones adicionales de Microsoft, como bloques de compatibilidad en un dispositivo

Las categorías posibles son:

- **Alta adopción**: Al menos 100 000 dispositivos comerciales de Windows 10 han instalado esta aplicación.  

- **Adoptado**: Al menos 10 000 dispositivos comerciales de Windows 10 han instalado esta aplicación.  

- **Datos insuficientes**: Demasiado pocos dispositivos comerciales de Windows 10 están compartiendo información para esta aplicación para que Microsoft pueda clasificar su adopción.

- **Póngase en contacto con el desarrollador**: Puede haber problemas de compatibilidad con esta versión de la aplicación. Microsoft recomienda ponerse en contacto con el proveedor de software para obtener más información. Para obtener más información, consulte [listos para Windows](https://www.readyforwindows.com/).  

- **Desconocido**: No hay ninguna información listos para Windows disponibles para esta versión de esta aplicación. Información puede estar disponible para otras versiones de la aplicación en [listos para Windows](https://www.readyforwindows.com/).  

### <a name="support-statement"></a>Declaración de soporte técnico

Si el proveedor de software es compatible con una o varias versiones de esta aplicación en Windows 10, podrá ver esta instrucción en el panel de propiedades de la aplicación. En la sección de factores de riesgo de compatibilidad, examine el **admite instrucción**.



## <a name="advanced-insights"></a>Información avanzada

Escritorio Analytics también puede detectar problemas con la información adicional siguiente:

### <a name="adopted-version-available"></a>Versión aprobada disponible

Hay otra versión de la aplicación que es alta adopción con otros clientes. Esta señal utiliza datos de listo para Windows. Si hay algún Bloqueador de actualización con su versión actual, considere la posibilidad de implementar la versión alternativa en su lugar.

### <a name="driver-dependency"></a>Dependencia del controlador

La aplicación es dependiente de un controlador. Análisis de escritorio, recomienda la aplicación para las pruebas piloto. Debería funcionar bien para piloto, pero encontrará las regresiones. Si tiene problemas, póngase en contacto con el publicador para solicitar una versión que sea compatible con Windows 10.



## <a name="driver-risk-assessment"></a>Evaluación de riesgos de controlador

Análisis de escritorio también se enumeran y grupos de disponibilidad de todos los controladores que no se migrarán a la versión del sistema operativo.

Puede encontrar la evaluación en el controlador en el análisis de escritorio. En la lista de recursos de controlador en un plan de implementación, seleccione un controlador individual para abrir su panel de control flotante de propiedades. Verá un nivel general de evaluación y recomendación. El **factores de riesgo de compatibilidad** sección muestra los detalles de estas evaluaciones.

| Disponibilidad del controlador | ¿Acción requerida? | Lo que significa | Guía |
|---------------------|------------------|---------------|----------|
| Disponible de forma predeterminada | No, para que el reconocimiento solo | La versión instalada actualmente de una aplicación o el controlador no se migrará a la nueva versión del sistema operativo. Hay instalada una versión compatible con la nueva versión del sistema operativo. | Se requiere para la actualización continuar ninguna acción. |
| Importar desde Windows Update | Sí | La versión instalada actualmente de un controlador no se migrará a la nueva versión del sistema operativo. Una versión compatible está disponible desde Windows Update. | Si el equipo recibe automáticamente las actualizaciones desde Windows Update, se requiere ninguna acción. En caso contrario, debe importar un nuevo controlador desde Windows Update después de actualizar Windows. |
| Disponible de forma predeterminada y de Windows Update | Sí | La versión instalada actualmente de un controlador no se migrará a la nueva versión del sistema operativo. Aunque un controlador nuevo se instala durante la actualización, una versión más reciente está disponible desde Windows Update. | Si el equipo recibe automáticamente las actualizaciones desde Windows Update, se requiere ninguna acción. En caso contrario, debe importar un nuevo controlador desde Windows Update después de actualizar Windows. |
| Póngase en contacto con el proveedor | Sí | El controlador no se migrará a la nueva versión del sistema operativo y el análisis de escritorio no puede encontrar una versión compatible. | Para una solución, póngase en contacto con el fabricante independiente de hardware (IHV) que se fabrica el controlador o el fabricante de equipos originales (OEM) que ha proporcionado el dispositivo. |


## <a name="see-also"></a>Consulte también

La ventaja de centro de FastTrack para Windows 10 proporciona acceso a **asegurar aplicaciones de escritorio**. Esta ventaja es un nuevo servicio diseñado para solucionar problemas con Windows 10 y compatibilidad de aplicaciones de Office 365 ProPlus. Para obtener más información, consulte [asegurar aplicaciones de escritorio](https://docs.microsoft.com/fasttrack/win-10-desktop-app-assure).
