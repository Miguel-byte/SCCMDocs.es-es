---
title: Preguntas más frecuentes sobre análisis de escritorio
titleSuffix: Configuration Manager
description: Preguntas más frecuentes sobre el análisis de escritorio.
ms.date: 09/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: e0db3311-2303-4013-a906-76b408172d3c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 306c6569551e1068c0e682c893e94b8f1a920ade
ms.sourcegitcommit: 4316bff400ffbde8404f8a2092ec17e3601b8d29
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "70738275"
---
# <a name="desktop-analytics-faq"></a>Preguntas más frecuentes sobre análisis de escritorio

> [!Note]  
> Esta información está relacionada con un servicio de vista previa que se puede modificar sustancialmente antes de que se publique comercialmente. Microsoft no ofrece ninguna garantía, expresa o implícita, con respecto a la información aquí proporcionada.  

## <a name="prerequisites"></a>Requisitos previos

### <a name="can-i-use-desktop-analytics-with-intune-managed-devices"></a>¿Puedo usar el análisis de escritorio con dispositivos administrados por Intune? 

La gran mayoría de los clientes que pueden beneficiarse del flujo de trabajo de análisis de escritorio usan Configuration Manager para implementar Windows. Sabemos que los clientes de Intune adoran la información adicional de los datos de análisis y estamos trabajando en formas de compartir información con ellos también.

### <a name="its-been-over-72-hours-and-the-portal-is-still-processing-data-what-next"></a>Ha transcurrido en más de 72 horas y el portal todavía está procesando datos, ¿qué es lo siguiente? 

La primera vez que se configura el análisis de escritorio, es posible que los informes de Configuration Manager y el portal de análisis de escritorio no muestren los datos completos de inmediato. El servicio puede tardar 2-3 días en procesar los datos. Si ha transcurrido en más de 72 horas y el portal todavía está procesando datos, siga estos pasos:

- Para confirmar que los dispositivos activos están configurados correctamente, use el [Panel de estado](/sccm/desktop-analytics/monitor-connection-health)de la conexión. Este panel no se actualiza en tiempo real.
- Asegúrese de que los dispositivos envían datos de diagnóstico al servicio de análisis de escritorio. Para obtener más información, vea [Habilitar el uso compartido de datos](/sccm/desktop-analytics/enable-data-sharing).
- Aprovisione [Azure ad aplicaciones](/sccm/desktop-analytics/troubleshooting#bkmk_AzureADApps) en el Azure ad.
- Compruebe los dispositivos que ha asociado a su organización en los últimos siete días. En el [portal de análisis de escritorio](https://aka.ms/desktopanalytics), vaya al panel **servicios conectados** . Seleccionar **inscribir dispositivos**y **ver datos recientes**

Si los dispositivos están configurados correctamente y aún no ve los datos en el área de trabajo, [póngase en contacto con el soporte técnico de Microsoft](https://support.microsoft.com/hub/4343728/support-for-business).

## <a name="windows-upgrade"></a>Actualización de Windows

### <a name="can-i-upgrade-windows-and-change-architecture"></a>¿Puedo actualizar Windows y cambiar la arquitectura?

El análisis de escritorio está diseñado para ofrecer una mejor compatibilidad con las actualizaciones en contexto. Las actualizaciones en contexto no admiten migraciones de arquitectura de 32 bits a 64 bits. Si necesita migrar equipos en este escenario, use el escenario de actualización. Desktop Analytics Insights sigue siendo útil en este escenario, pero se pueden omitir las instrucciones específicas de la actualización.

Para obtener más información, consulte [Actualizar un equipo existente con una nueva versión de Windows](/sccm/osd/deploy-use/refresh-an-existing-computer-with-a-new-version-of-windows).

### <a name="can-i-change-from-bios-to-uefi-when-upgrading-windows"></a>¿Puedo cambiar de BIOS a UEFI al actualizar Windows?

Sí. Para obtener más información, consulte [conversión de BIOS a UEFI durante una actualización local](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade).

### <a name="can-i-use-desktop-analytics-with-windows-10-ltsc"></a>¿Puedo usar el análisis de escritorio con Windows 10 LTSC?

Aunque puede usar el análisis de escritorio para ayudar con la actualización de dispositivos desde el canal de mantenimiento a largo plazo (LTSC) de Windows 10 al canal semianual de Windows 10, el análisis de escritorio no es compatible con las actualizaciones de Windows 10 LTSC. Este canal de Windows 10 no está pensado para uso amplio y no recibe actualizaciones de características, por lo que no es un destino compatible con el análisis de escritorio. Para obtener más información, vea [información general de Windows como servicio](https://docs.microsoft.com/windows/deployment/update/waas-overview#long-term-servicing-channel).

### <a name="can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal"></a>¿Se puede reducir la cantidad de tiempo que tardan los datos en actualizarse en el portal de análisis de escritorio?

Hay dos tipos de datos en el portal de análisis de escritorio: Datos de administrador y datos de diagnóstico. Para actualizar los datos de administrador a petición, abra el control flotante de moneda de datos y seleccione **aplicar cambios**. Esta acción desencadena inmediatamente una actualización única de los cambios pendientes de administrador en las áreas de trabajo. Los cambios se propagan y están disponibles con carácter general en 15-60 minutos. El tiempo depende del tamaño del área de trabajo y del ámbito de los cambios pendientes. Puede solicitar una actualización de datos a petición hasta seis veces en un período de 24 horas.

Todos los datos se actualizan automáticamente una vez al día, aunque no solicite una actualización de datos a petición. No hay ninguna manera de desencadenar una actualización a petición de datos de diagnóstico. Para obtener más información sobre los diferentes tipos de datos en el análisis del escritorio, consulte latencia de los [datos](/sccm/desktop-analytics/troubleshooting#data-latency).

## <a name="privacy"></a>Privacidad

### <a name="can-desktop-analytics-be-used-without-a-direct-client-connection-to-the-microsoft-data-management-service"></a>¿Se puede usar el análisis de escritorio sin una conexión de cliente directa con el servicio Microsoft Administración de datos?

No, todo el servicio se basa en los datos de diagnóstico de Windows, lo que requiere que los dispositivos tengan esta conectividad directa.

### <a name="can-i-choose-the-data-center-location"></a>¿Se puede elegir la ubicación del centro de datos?

Para Azure Log Analytics: Sí, al configurar el análisis de escritorio y crear el área de trabajo Log Analytics.

Para la Azure Storage de servicio y análisis de Microsoft Administración de datos: No, estos dos servicios se hospedan en el Estados Unidos.

### <a name="where-is-my-organizations-data-stored"></a>¿Dónde se almacenan los datos de mi organización?

Los datos de diagnóstico de Windows de los equipos están cifrados, enviados y procesados en centros de datos seguros administrados por Microsoft ubicados en el Estados Unidos. El análisis de los datos relacionados con el análisis de escritorio se le proporciona a través de la solución Desktop Analytics en el Azure Portal. El análisis de escritorio es compatible con todas las regiones de Azure. La selección de una región de Azure internacional no impide que los datos de diagnóstico se envíen y se procesen en centros de datos seguros de Microsoft en Estados Unidos.

## <a name="existing-windows-analytics-customers"></a>Clientes existentes de Windows Analytics

### <a name="can-i-migrate-inputs-from-windows-analytics"></a>¿Puedo migrar entradas de Windows Analytics?

Sí, al establecer un área de trabajo de Windows Analytics existente como área de trabajo de análisis de escritorio durante la [incorporación inicial](/sccm/desktop-analytics/set-up#initial-onboarding). Si crea una nueva área de trabajo, o selecciona una que no sea un área de trabajo de Windows Analytics, el análisis de escritorio no migrará las entradas.

#### <a name="migration-scope"></a>Ámbito de migración

| Tipo de entrada | ¿Migrará? |
|------------|---------------|
| Importance | Sí |
| Propietario de la aplicación | Sí |
| Decisión de actualización | Sin |
| Plan de pruebas | Sin |
| Resultado de la prueba | Sin |

#### <a name="importance-mapping"></a>Asignación de importancia

| Windows Analytics | Análisis de escritorio |
|-------------------| ------------------|
| Recuento de instalaciones bajas | (No aplicable) <br> Nota: Análisis de escritorio ejecuta su propia heurística para determinar el número de instalaciones bajas |
| No revisado | No revisado |
| Revisión en curso | No revisado |
| Misión crítica | Crítica |
| Crítico para la empresa | Crítica |
| Aún | Aún |
| Mejor esfuerzo | Aún |
| Ignorar | No es importante |

### <a name="can-i-migrate-from-multiple-windows-analytics-workspaces"></a>¿Puedo migrar desde varias áreas de trabajo de Windows Analytics?

No, solo puede seleccionar un área de trabajo de Windows Analytics desde la que migrar entradas. Si posee varias áreas de trabajo de Windows Analytics, seleccione una que mejor se adapte a su organización.

### <a name="ive-chosen-to-migrate-where-can-i-find-the-inputs-on-desktop-analytics"></a>He elegido la migración, ¿Dónde puedo encontrar las entradas en el análisis de escritorio?

Una vez inscritos los dispositivos, para ver las entradas migradas en el portal de análisis de escritorio, vaya a **Administración de recursos de > > aplicaciones**.

### <a name="when-can-i-see-my-migrated-inputs"></a>¿Cuándo puedo ver las entradas migradas?

El proceso de migración es transaccional. Verá todas las entradas migradas sin daños o sin entradas migradas. Si no ve las entradas migradas en 24 horas, póngase en contacto con Soporte técnico de Microsoft. Inicie el etiquetado de las aplicaciones cuando vea las entradas migradas. Si ya etiquetó algunas aplicaciones, el análisis de escritorio mantiene esas entradas en caso de que entren en conflicto con las entradas de Windows Analytics.

### <a name="im-not-ready-yet-can-i-migrate-after-the-initial-onboarding"></a>Todavía no estoy listo, ¿puedo migrar después de la incorporación inicial?

No, en este momento tiene que decidir si migrar durante la [incorporación inicial](/sccm/desktop-analytics/set-up#initial-onboarding).

### <a name="can-i-use-update-compliance-together-with-desktop-analytics"></a>¿Puedo usar Update Compliance junto con el análisis de escritorio?

Sí. Si usa [Update Compliance](https://docs.microsoft.com/windows/deployment/update/update-compliance-get-started) en el Azure portal hoy, puede seguir haciendo esto ahora y más allá del 2020 de enero.

<!-- For more information, see [blog post]... -->

## <a name="other"></a>Otros

### <a name="can-i-use-desktop-analytics-for-my-office-365-proplus-upgrades"></a>¿Puedo usar el análisis de escritorio para las actualizaciones de Office 365 ProPlus?

No, el análisis de escritorio se centra en Windows. Microsoft desarrolló el análisis del escritorio en estrecha colaboración con muchos clientes. A través del programa de vista previa, los comentarios de los clientes fueron sobre cómo el análisis de escritorio mejoró su capacidad para administrar implementaciones de Windows de forma segura. También nos dijeron que querían que [office 365 ProPlus](/sccm/sum/deploy-use/office-365-dashboard#bkmk_o365_readiness) provienen más estrechamente integrados con las herramientas de administración de office en Configuration Manager e Intune. Microsoft continuará realizando inversiones en esas áreas, mientras se centra en los escenarios de Windows en el análisis del escritorio.

### <a name="how-can-i-provide-feedback-about-desktop-analytics"></a>¿Cómo puedo proporcionar comentarios sobre el análisis de escritorio?

Para compartir sus comentarios sobre el análisis de escritorio, seleccione el icono **enviar una sonrisa** en la parte superior del portal. Incluya una captura de pantalla con su envío para ayudar a Microsoft a comprender mejor sus comentarios. También puede enviar sugerencias de productos y votar otras ideas en [UserVoice](https://configurationmanager.uservoice.com/forums/300492-ideas?category_id=366805).

> [!Note]
> No comparta nunca información privada a través de enviar una sonrisa o UserVoice. Esta información privada incluye el identificador de inquilino o el ID. comercial. Microsoft no proporciona soporte técnico a través de los canales enviar una sonrisa o UserVoice. Para obtener ayuda con el área de trabajo de análisis de escritorio, seleccione el vínculo **ayuda y soporte técnico** en el menú de navegación para abrir una incidencia de soporte técnico.
