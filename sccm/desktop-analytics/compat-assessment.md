---
title: Evaluación de compatibilidad
titleSuffix: Configuration Manager
description: Obtenga información sobre la evaluación de compatibilidad para aplicaciones y controladores de Windows en análisis de escritorio.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: ea78f726-b1b3-49b0-8141-d916be48c458
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: f6181f0e1a502d701ca7337641013a18b03251f9
ms.sourcegitcommit: 72faa1266b31849ce1a23d661a1620b01e94f517
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/26/2019
ms.locfileid: "68535977"
---
# <a name="compatibility-assessment-in-desktop-analytics"></a>Evaluación de compatibilidad en análisis de escritorio

> [!Note]  
> Esta información está relacionada con un servicio de vista previa que se puede modificar sustancialmente antes de que se publique comercialmente. Microsoft no ofrece ninguna garantía, expresa o implícita, con respecto a la información aquí proporcionada.  

Las evaluaciones de actualización en Windows Analytics eran genéricas, por ejemplo: Atención necesaria o corrección disponible. No proporciona ningún indicador visual sobre cómo priorizar aplicaciones o controladores con problemas o actualizar información. El análisis de escritorio reemplaza esta característica por el **riesgo de compatibilidad**. Análisis de escritorio muestra la evaluación de las aplicaciones solo en la vista de implementación para un escenario anterior a la actualización. Clasifica las aplicaciones en función de la información que Microsoft obtiene de las máquinas incluidas en un plan de implementación actual.

Análisis de escritorio usa las siguientes categorías de evaluación de compatibilidad:

- **Bajo**: El servicio no encontró señales para poner en peligro esta aplicación para una actualización de Windows. Es probable que funcione en el sistema operativo de destino tal cual.  

- **Medio**: Analytics indica que la aplicación puede tener una funcionalidad dispares, aunque es probable que la corrección sea posible.  

- **Alto**: La aplicación está casi seguro de que se produce un error durante o después de la actualización. Es posible que necesite una corrección.  

- **Desconocido**: No se evaluó la aplicación. No hay ninguna otra información, como *problemas conocidos de MS* o *listas para Windows*.  

En la lista de recursos de aplicación o de controlador de un plan de implementación, verá este valor para cada activo en la columna **riesgo de compatibilidad** .


## <a name="app-risk-assessment"></a>Evaluación del riesgo de la aplicación

![Diagrama de orígenes de evaluación del riesgo de la aplicación](media/app-risk-assessment-sources.png)

Hay varios orígenes que el análisis de escritorio usa para generar la clasificación de evaluación para las aplicaciones:

- [Problemas conocidos de Microsoft](#microsoft-known-issues)
- [Listo para Windows Catalog](#ready-for-windows)
- [Información avanzada](#advanced-insights)

Puede encontrar la evaluación de cada origen en la aplicación en análisis de escritorio. En la lista de activos de la aplicación de un plan de implementación, seleccione una aplicación individual para abrir el panel de control flotante propiedades. Verá una recomendación general y un nivel de evaluación. En la sección **factores de riesgo de compatibilidad** se muestran los detalles de estas evaluaciones.


## <a name="microsoft-known-issues"></a>Problemas conocidos de Microsoft

El análisis de escritorio examina la base de datos de compatibilidad de aplicaciones de Microsoft en busca de cualquier problema conocido. Utiliza esta base de datos para determinar los bloques de compatibilidad existentes para las aplicaciones disponibles públicamente de Microsoft o de otros publicadores. Esta comprobación solo se aplica al SO de destino para el plan de implementación que seleccione.

Verá los siguientes problemas en el panel de propiedades de la aplicación como **problemas conocidos de MS**:

### <a name="application-is-removed-during-upgrade"></a>La aplicación se quita durante la actualización

Windows detectó problemas de compatibilidad. La aplicación no se migrará a la nueva versión del sistema operativo. No es necesario realizar ninguna acción para que la actualización continúe.

### <a name="blocking-upgrade"></a>Bloqueo de la actualización

Windows detectó problemas de bloqueo y no puede quitar la aplicación durante la actualización. Es posible que no funcione en la nueva versión del sistema operativo. Antes de actualizar, quite la aplicación. Vuelva a instalarlo y pruébelo en la nueva versión del sistema operativo.

### <a name="blocking-upgrade-but-can-be-reinstalled-after-upgrading"></a>Bloqueo de la actualización, pero se puede reinstalar después de la actualización

La aplicación es compatible con la nueva versión del sistema operativo, pero no se migrará. Quite la aplicación antes de actualizar Windows. Vuelva a instalarlo en la nueva versión del sistema operativo.

### <a name="blocking-upgrade-update-application-to-newest-version"></a>Bloquear la actualización, actualizar la aplicación a la versión más reciente

La versión existente de la aplicación no es compatible con la nueva versión del sistema operativo y no se migrará. Hay disponible una versión compatible de la aplicación. Actualice la aplicación antes de actualizar.

### <a name="disk-encryption-blocking-upgrade"></a>Actualización de bloqueo de disco

Las características de cifrado de la aplicación bloquean la actualización. Deshabilite la característica de cifrado antes de actualizar Windows y habilítela después de la actualización.

### <a name="does-not-work-with-new-os-but-wont-block-upgrade"></a>No funciona con el nuevo sistema operativo, pero no bloqueará la actualización

La aplicación no es compatible con la nueva versión del sistema operativo, pero no bloqueará la actualización. No es necesario realizar ninguna acción para que la actualización continúe. Instale una versión compatible de la aplicación en la nueva versión del sistema operativo.

### <a name="does-not-work-with-new-os-and-will-block-upgrade"></a>No funciona con el nuevo sistema operativo y bloqueará la actualización

La aplicación no es compatible con la nueva versión del sistema operativo y bloqueará la actualización. Quite la aplicación antes de actualizar. Puede que haya disponible una versión compatible de la aplicación.

### <a name="evaluate-application-on-new-os"></a>Evaluación de la aplicación en el nuevo sistema operativo

Windows migrará la aplicación, pero detectó problemas que pueden afectar al rendimiento de la aplicación en la nueva versión del sistema operativo. No es necesario realizar ninguna acción para que la actualización continúe. Pruebe la aplicación en la nueva versión del sistema operativo.

### <a name="may-block-upgrade-test-application"></a>Puede bloquear la actualización, probar la aplicación

Windows detectó problemas que pueden interferir con la actualización, pero que necesitan más investigación. Probar el comportamiento de la aplicación durante la actualización. Si bloquea la actualización, quítela antes de actualizar. A continuación, vuelva a instalarlo y pruebe la nueva versión del sistema operativo.

### <a name="multiple"></a>Múltiple

Varios problemas afectan a la aplicación. Seleccione **consulta** para ver los detalles de los problemas detectados por Windows.

### <a name="reinstall-application-after-upgrading"></a>Reinstalar la aplicación después de la actualización

La aplicación es compatible con la nueva versión del sistema operativo, pero debe volver a instalarla después de actualizar Windows. El proceso de actualización quita la aplicación. No es necesario realizar ninguna acción para que la actualización continúe. Vuelva a instalar la aplicación en la nueva versión del sistema operativo.


## <a name="ready-for-windows"></a>Listo para Windows

El catálogo [de aplicaciones preparado para Windows](https://www.readyforwindows.com) correlaciona los siguientes orígenes de datos:

- Datos de diagnóstico de otros clientes que informan de las mismas aplicaciones
- Comprobaciones adicionales de Microsoft como bloques de compatibilidad en un dispositivo

Las categorías posibles son:

- **Muy adoptado**: Al menos 100.000 dispositivos comerciales de Windows 10 tienen instalada esta aplicación.  

- **Adopción**: Al menos 10.000 dispositivos comerciales de Windows 10 tienen instalada esta aplicación.  

- **Datos**insuficientes: Pocos dispositivos comerciales de Windows 10 están compartiendo información de esta aplicación para que Microsoft Clasifique su adopción.

- **Póngase en contacto con Developer**: Puede haber problemas de compatibilidad con esta versión de la aplicación. Microsoft recomienda ponerse en contacto con el proveedor de software para obtener más información. Para obtener más información, vea [listo para Windows](https://www.readyforwindows.com/).  

- **Desconocido**: No hay disponible ninguna información de Windows para esta versión de esta aplicación. Puede haber información disponible para otras versiones de la aplicación en [preparado para Windows](https://www.readyforwindows.com/).  

### <a name="support-statement"></a>Instrucción de soporte técnico

Si el proveedor de software admite una o varias versiones de esta aplicación en Windows 10, verá esta instrucción en el panel de propiedades de la aplicación. En la sección factores de riesgo de compatibilidad, consulte la **declaración de soporte técnico**.



## <a name="advanced-insights"></a>Información avanzada

El análisis de escritorio también puede detectar problemas con la siguiente información adicional:

### <a name="adopted-version-available"></a>Versión aprobada disponible

Hay otra versión de esta aplicación muy adoptada por otros clientes. Esta señal usa datos de listos para Windows. Si hay algún bloque de actualización con la versión actual, considere la posibilidad de implementar la versión alternativa en su lugar.

### <a name="driver-dependency"></a>Dependencia del controlador

La aplicación depende de un controlador. El análisis de escritorio recomienda la aplicación para realizar pruebas piloto y detectar cualquier regresión. Si tiene algún problema, póngase en contacto con el editor para solicitar una versión compatible con Windows 10.

### <a name="additional-insights"></a>Información adicional

<!-- 4021225 -->
Al actualizar el sitio de Configuration Manager y los clientes a la versión 1906, los clientes también informan de esta información adicional:

> [!Important]  
> Para aprovechar al máximo las nuevas características de Configuration Manager, después de actualizar el sitio, actualice también los clientes a la versión más reciente. Este escenario no funciona hasta que la versión del cliente sea también la más reciente.

#### <a name="16-bit-apps"></a>aplicaciones de 16 bits

Quite todos los componentes de 16 bits de las aplicaciones y reemplace por los equivalentes de 32 o 64 bits. Para obtener más información, [vea el artículo para desarrolladores de Windows Vista y Windows Server 2008: Guía](https://docs.microsoft.com/previous-versions/aa480152\(v=msdn.10\))de compatibilidad de aplicaciones.

La otra opción consiste en habilitar NT virtual DOS Machine (NTVDM) para la compatibilidad con Windows 10.

#### <a name="requires-admin-privileges"></a>Requiere privilegios de administrador

La aplicación requiere que el usuario tenga acceso administrativo al dispositivo. Use un manifiesto de aplicación para estas aplicaciones que requieran permisos de administrador. Para obtener más información, vea [crear e insertar un manifiesto de aplicación](https://docs.microsoft.com/previous-versions/bb756929\(v=msdn.10\)).

El análisis de escritorio recomienda la aplicación para realizar pruebas piloto y detectar cualquier regresión.

#### <a name="java-dependency"></a>Dependencia de Java

Muchas aplicaciones Java dependen de un Java Runtime Environment instalado por separado (JRE). Aunque es posible que las versiones anteriores de JRE sigan funcionando en Windows 10, Oracle solo admite las últimas versiones de JRE. El uso de una versión anterior de JRE no compatible puede tener vulnerabilidades de seguridad. Compruebe que la aplicación se ejecuta en las versiones más recientes de JRE.

#### <a name="not-dpi-aware"></a>No compatible con PPP

Es posible que la aplicación tenga problemas de visualización con las resoluciones de pantalla avanzadas en Windows 10. Use un manifiesto de aplicación para evitar problemas con resoluciones de PPP altas. Para obtener más información, consulte manifiestos de [aplicación](https://docs.microsoft.com/windows/desktop/SbsCs/application-manifests).

El análisis de escritorio recomienda la aplicación para realizar pruebas piloto y detectar cualquier regresión.

#### <a name="silverlight-framework"></a>Marco de Silverlight

Microsoft recomienda que las aplicaciones no basadas en explorador no usen Silverlight. La fecha de finalización del soporte técnico para Silverlight 5 es 2021 de octubre.

La mayoría de los exploradores Web actuales no admiten Silverlight.

| Browser | Soporte técnico |
|---------|---------|
| Google Chrome | Fin del soporte técnico: 2015 de septiembre |
| Firefox | Fin del soporte técnico: Marzo de 2017 |
| Microsoft Edge | No hay complementos disponibles |

El análisis de escritorio recomienda la aplicación para realizar pruebas piloto y detectar cualquier regresión.

#### <a name="net-framework-1011"></a>.NET Framework 1.0/1.1

La versión 1,0 de .NET Framework no es compatible con Windows 10. La versión 1,1 no es compatible con Windows 10. Si la aplicación es de un publicador de terceros, póngase en contacto con el proveedor para solicitar una versión compatible con Windows 10. De lo contrario, redesarrolle la aplicación para usar una versión compatible de .NET.

#### <a name="net-framework-2030"></a>.NET Framework 2.0/3.0

Los marcos de .NET 2,0 y 3,5 se admiten en Windows 10. Es posible que tenga que habilitar la característica de Windows. Para obtener más información, consulte [instalación del .NET Framework 3,5 en Windows 10](https://docs.microsoft.com/dotnet/framework/install/dotnet-35-windows-10).

#### <a name="ui-access"></a>Acceso a la interfaz de usuario

Las aplicaciones con acceso a la interfaz de usuario pueden omitir los niveles de control de la interfaz de usuario para impulsar la entrada en ventanas de privilegios superiores en el escritorio. Use esta opción solo para aplicaciones de tecnología de asistencia de la interfaz de usuario.

Si no usa las características de accesibilidad en la aplicación, establezca la marca de acceso a la interfaz de usuario en el manifiesto de la aplicación en false. Para obtener más información, vea [crear e insertar un manifiesto de aplicación](https://docs.microsoft.com/previous-versions/bb756929\(v=msdn.10\)).

El análisis de escritorio recomienda la aplicación para realizar pruebas piloto y detectar cualquier regresión.


## <a name="driver-risk-assessment"></a>Evaluación de riesgos de controladores

El análisis de escritorio también enumera y agrupa por disponibilidad los controladores que no se migren a la versión del sistema operativo.

Puede encontrar la evaluación en el controlador en el análisis de escritorio. En la lista de recursos de controlador de un plan de implementación, seleccione un controlador individual para abrir el panel de control flotante propiedades. Verá una recomendación general y un nivel de evaluación. En la sección **factores de riesgo de compatibilidad** se muestran los detalles de estas evaluaciones.

| Disponibilidad del controlador | ¿Se requiere acción? | Qué significa | Guía |
|---------------------|------------------|---------------|----------|
| Disponible | No, solo para el reconocimiento | La versión instalada actualmente de una aplicación o un controlador no se migrará a la nueva versión del sistema operativo. Se instala una versión compatible con la nueva versión del sistema operativo. | No es necesario realizar ninguna acción para que la actualización continúe. |
| Importar desde Windows Update | Sí | La versión instalada actualmente de un controlador no se migra a la nueva versión del sistema operativo. Una versión compatible está disponible en Windows Update. | Si el equipo recibe automáticamente las actualizaciones de Windows Update, no es necesario realizar ninguna acción. De lo contrario, importe un nuevo controlador desde Windows Update después de actualizar Windows. |
| Disponible y desde Windows Update | Sí | La versión instalada actualmente de un controlador no se migra a la nueva versión del sistema operativo. Aunque un nuevo controlador se instala durante la actualización, la versión más reciente está disponible en Windows Update. | Si el equipo recibe automáticamente las actualizaciones de Windows Update, no es necesario realizar ninguna acción. De lo contrario, importe un nuevo controlador desde Windows Update después de actualizar Windows. |
| Consultar con el proveedor | Sí | El controlador no se migrará a la nueva versión del sistema operativo y el análisis de escritorio no puede encontrar una versión compatible. | En el caso de una solución, consulte con el fabricante de hardware independiente (IHV) que fabrica el controlador o con el fabricante de equipos originales (OEM) que proporcionó el dispositivo. |


## <a name="see-also"></a>Consulte también

El beneficio del centro de FastTrack para Windows 10 proporciona acceso a la **aplicación de escritorio**. Esta ventaja es un nuevo servicio diseñado para solucionar problemas con la compatibilidad de aplicaciones de Windows 10 y Office 365 ProPlus. Para obtener más información, vea el apartado sobre la [aplicación de escritorio](https://docs.microsoft.com/fasttrack/win-10-desktop-app-assure).
