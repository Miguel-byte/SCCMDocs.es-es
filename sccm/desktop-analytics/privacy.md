---
title: Escritorio privacidad de datos de análisis
titleSuffix: Configuration Manager
description: Análisis de escritorio se compromete a privacidad de datos de cliente
ms.date: 06/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: b5606f15-f589-485c-a599-cdabf1a9e7ac
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 08c8837bf71e0f3ff2a19290880d33ac28eed039
ms.sourcegitcommit: 659976b943226c5124057429ac7444989f98433f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2019
ms.locfileid: "67159011"
---
# <a name="desktop-analytics-data-privacy"></a>Escritorio privacidad de datos de análisis

Análisis de escritorio se ha comprometido a privacidad de los datos al cliente, se centraban en estos principios:

- **Transparencia:** Se documenta completamente los eventos de diagnóstico de Windows. Revíselos con equipos de cumplimiento y seguridad de su compañía. El Visor de datos de diagnóstico de Windows le permite ver datos de diagnóstico enviados desde un dispositivo determinado. Para obtener más información, consulte [Introducción al Visor de datos de diagnóstico](https://docs.microsoft.com/windows/configuration/diagnostic-data-viewer-overview).  

- **Control:** Controlar el nivel de datos de diagnóstico para compartir con Microsoft. Windows 10, versión 1709, agrega una nueva directiva para limitar los datos de diagnóstico mejorado al mínimo requerido por el análisis de escritorio.  

- **Seguridad:** Microsoft protege los datos con cifrado y seguridad sólida.  

- **Confianza:** Análisis de escritorio es compatible con Microsoft [declaración de privacidad](https://privacy.microsoft.com/privacystatement) y [términos de Online Services](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=46).  



## <a name="diagnostic-data-flow"></a>Flujo de datos de diagnóstico

La siguiente ilustración muestra los datos de diagnóstico cómo fluye desde dispositivos individuales a través del servicio de datos de diagnóstico, almacenamiento de Azure Log Analytics y el área de trabajo de Log Analytics:

![Diagrama que ilustra el flujo de datos de diagnóstico de dispositivos](media/da-data-flow.png)

1. Inicie sesión en Azure portal e incorporarse a análisis de escritorio. Crear la aplicación de Azure AD para conectarse con Configuration Manager. Al configurar el análisis de escritorio, cree un área de trabajo de Azure Log Analytics en la ubicación de su elección.  

2. Conectar Configuration Manager e inscribir dispositivos  

    1. Configurar el servicio de análisis de escritorio en la nube en Configuration Manager con los detalles de la aplicación de Azure AD.  

    2. Dentro de 15 minutos, Configuration Manager sincroniza las recopilaciones de dispositivos y los planes de las implementaciones con análisis de escritorio. Este proceso se repite cada hora.  

    3. Configuration Manager establece el identificador comercial, el nivel de datos de diagnóstico y otras opciones para los dispositivos en la colección de destino. Esta configuración especifica los dispositivos para que aparezca en el área de trabajo de análisis de escritorio.  

    4. Implementar actualizaciones de compatibilidad para todos los dispositivos de destino.  

3. Los dispositivos envían datos de diagnóstico para el servicio de administración de datos de diagnóstico de Microsoft para Windows. Este servicio se hospeda en Estados Unidos.  

4. Cada día, Microsoft genera una instantánea de insights centradas en TI. Esta instantánea combina los datos de diagnóstico de Windows con sus comentarios para los dispositivos inscritos. Este proceso se produce en un almacenamiento transitorio, que solo se usa por el análisis de escritorio. El almacenamiento transitorio se hospeda en centros de datos de Microsoft en Estados Unidos. Las instantáneas se segregan por Id. comercial.  

5. Las instantáneas, a continuación, se copian en el área de trabajo de Azure Log Analytics correspondiente.  

6. Escritorio Analytics almacena su entrada en el almacenamiento de Azure Log Analytics. Estas configuraciones incluyen planes de implementación y las decisiones de recurso para la actualización y de importancia.  



## <a name="other-resources"></a>Otros recursos

Para privacidad relacionadas con las preguntas más frecuentes para el análisis de escritorio, consulte [preguntas más frecuentes de privacidad](/sccm/desktop-analytics/faq#privacy).

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
