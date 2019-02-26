---
title: Escritorio privacidad de datos de análisis
titleSuffix: Configuration Manager
description: Análisis de escritorio se compromete a privacidad de datos de cliente
ms.date: 01/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: b5606f15-f589-485c-a599-cdabf1a9e7ac
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 370bfc26b8a7b6ca0223803a36e765528460d89f
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56755615"
---
# <a name="desktop-analytics-data-privacy"></a>Escritorio privacidad de datos de análisis

Análisis de escritorio se ha comprometido a privacidad de los datos al cliente, se centraban en estos principios:

- **Transparencia:** Se documenta completamente los eventos de diagnóstico de Windows. Revíselos con equipos de cumplimiento y seguridad de su compañía. El Visor de datos de diagnóstico de Windows le permite ver datos de diagnóstico enviados desde un dispositivo determinado. Para obtener más información, consulte [Introducción al Visor de datos de diagnóstico](https://docs.microsoft.com/windows/configuration/diagnostic-data-viewer-overview).  

- **Control:** Controlar el nivel de datos de diagnóstico para compartir con Microsoft. Windows 10, versión 1709, agrega una nueva directiva para limitar los datos de diagnóstico mejorado al mínimo requerido por el análisis de escritorio.  

- **Seguridad:** Microsoft protege los datos con cifrado y seguridad sólida.  

- **Confianza:** Análisis de escritorio es compatible con Microsoft [declaración de privacidad](https://privacy.microsoft.com/privacystatement) y [términos de Online Services](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=46).  



## <a name="diagnostic-data-flow"></a>Flujo de datos de diagnóstico

La siguiente ilustración muestra los datos de diagnóstico cómo fluye desde dispositivos individuales a través del servicio de datos de diagnóstico, almacenamiento de Azure Log Analytics y el área de trabajo de Log Analytics:

![Diagrama que ilustra el flujo de datos de diagnóstico de dispositivos](media/da-data-flow-v1.png)

1. Inicie sesión en Azure portal e incorporarse a análisis de escritorio. Crear la aplicación de Azure AD para conectarse con Configuration Manager. Al configurar el análisis de escritorio, cree un área de trabajo de Azure Log Analytics en la ubicación de su elección.  

2. Conectar Configuration Manager e inscribir dispositivos  

    1. Configurar el servicio de análisis de escritorio en la nube en Configuration Manager con los detalles de la aplicación de Azure AD.  

    2. Dentro de 15 minutos, Configuration Manager sincroniza las recopilaciones de dispositivos y los planes de las implementaciones con análisis de escritorio. Este proceso se repite cada hora.  

    3. Configuration Manager establece el identificador comercial, el nivel de datos de diagnóstico y otras opciones para los dispositivos en la colección de destino. Esta configuración especifica los dispositivos para que aparezca en el área de trabajo de análisis de escritorio.  

    4. Implementar actualizaciones de compatibilidad para todos los dispositivos de destino. Opcionalmente, implementar la aplicación analizador de mantenimiento y Readiness Toolkit de Office a un conjunto representativo de los dispositivos. Estas herramientas proporcionan más información en línea personalizada de aplicaciones empresariales y las macros de Office.  

3. Los dispositivos envían datos de diagnóstico a los servicios de administración de datos de diagnóstico de Microsoft para Windows y Office. Este servicio se hospeda en Estados Unidos.  

4. Cada día, Microsoft genera una instantánea de insights centradas en TI. Esta instantánea combina los datos de diagnóstico de Windows y Office con sus comentarios para los dispositivos inscritos. Este proceso se produce en un almacenamiento transitorio, que solo se usa por el análisis de escritorio. El almacenamiento transitorio se hospeda en centros de datos de Microsoft en Estados Unidos. Las instantáneas se segregan por Id. comercial.  

5. Las instantáneas, a continuación, se copian en el área de trabajo de Azure Log Analytics correspondiente.  

6. Escritorio Analytics almacena su entrada en el almacenamiento de Azure Log Analytics. Estas configuraciones incluyen planes de implementación y las decisiones de recurso para la actualización y de importancia.  


<!-- ![Diagram illustrating flow of diagnostic data from devices](media/wa-data-flow-v1.png)

1. Devices send diagnostic data to the Microsoft Diagnostic Data Management service. This service is hosted in the United States.  

2. Set up and enrollment  

    1. You create an Azure Log Analytics workspace when you set up Desktop Analytics. You choose the location and copy the commercial ID. This ID identifies your workspace.  
    
    2. When you connect Configuration Manager to Desktop Analytics, it sets the commercial ID on the devices in your target collection. This configuration specifies the devices to appear in your workspace.  

3. Each day Microsoft produces a "snapshot" of IT-focused insights for each workspace in the Diagnostic Data Management service.  

4. These snapshots are copied to transient storage, which is only used by Desktop Analytics. The transient storage is hosted in Microsoft data centers in the United States. The snapshots are segregated by commercial ID.  

5. The snapshots are then copied to the appropriate Azure Log Analytics workspace.  

6. Desktop Analytics stores your configurations in Analytics Azure storage. These configurations include deployment plans and asset upgrade decisions.  
-->


## <a name="other-resources"></a>Otros recursos

Para obtener más información sobre los aspectos de privacidad relacionada, consulte los artículos siguientes:

- [Windows 10 y el RGPD para decisiones de TI](https://docs.microsoft.com/windows/privacy/gdpr-it-guidance)  

- [Configurar datos de diagnóstico de Windows en su organización](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization)  

- [Campos y eventos de datos de diagnóstico Windows 7, Windows 8 y Windows 8.1 appraiser](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-8.1-and-8/appraiser-diagnostic-data-events-and-fields)  

- [Windows 10, versión 1809 básica nivel eventos de diagnóstico de Windows y campos](https://docs.microsoft.com/windows/privacy/basic-level-windows-diagnostic-events-and-fields-1809)  

- [Windows 10, versión 1709 mejorado eventos de datos de diagnóstico y los campos utilizados por el análisis de escritorio](https://docs.microsoft.com/windows/privacy/enhanced-diagnostic-data-windows-analytics-events-and-fields)  

- [Introducción al Visor de datos de diagnóstico](https://docs.microsoft.com/windows/privacy/diagnostic-data-viewer-overview)  

- [Los términos de licencia y la documentación](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31)  

- [Seguridad y privacidad en centros de datos de Microsoft Azure](https://azure.microsoft.com/global-infrastructure/)  

- [Confianza en la nube de confianza](https://azure.microsoft.com/overview/trusted-cloud/)  

- [Centro de confianza](https://www.microsoft.com/trustcenter)  



## <a name="faq"></a>Preguntas más frecuentes

### <a name="can-desktop-analytics-be-used-without-a-direct-client-connection-to-the-microsoft-data-management-service"></a>¿Análisis de escritorio se puede usar sin una conexión directa desde el cliente al servicio de administración de datos de Microsoft?
No, todo el servicio funciona con datos de diagnóstico de Windows, lo que requiere que los dispositivos tienen esta conectividad directa.


### <a name="can-i-choose-the-data-center-location"></a>¿Puedo elegir la ubicación del centro de datos?

Para Azure Log Analytics: Sí, al configurar el análisis de escritorio y crear el área de trabajo de Log Analytics.

Para el servicio de administración de datos de Microsoft y análisis de almacenamiento de Azure: No, estos dos servicios se hospedan en los Estados Unidos.

