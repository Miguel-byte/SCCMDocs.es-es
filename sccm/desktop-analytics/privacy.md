---
title: Privacidad de datos de análisis de escritorio
titleSuffix: Configuration Manager
description: El análisis de escritorio se compromete a la privacidad de los datos del cliente
ms.date: 06/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: b5606f15-f589-485c-a599-cdabf1a9e7ac
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: aef08fb2d4c404ea66ded3d1a49d30af68fe4a95
ms.sourcegitcommit: 9648ce8a8b5c82518e7c8b6a7668e0e9b076cae6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/05/2019
ms.locfileid: "70379734"
---
# <a name="desktop-analytics-data-privacy"></a>Privacidad de datos de análisis de escritorio

El análisis del escritorio está totalmente confirmada para la privacidad de los datos del cliente y se centra en estos principios:

- **Transparencia** Hemos documentado por completo los eventos de diagnóstico de Windows. Revíselos con los equipos de cumplimiento y seguridad de su empresa. El visor de datos de diagnóstico de Windows le permite ver los datos de diagnóstico enviados desde un dispositivo determinado. Para obtener más información, vea [información general del visor de datos de diagnóstico](https://docs.microsoft.com/windows/configuration/diagnostic-data-viewer-overview).  

- **Control** Puede controlar el nivel de los datos de diagnóstico que se van a compartir con Microsoft. Windows 10, versión 1709, agrega una nueva Directiva para limitar los datos de diagnóstico mejorados al mínimo requerido por el análisis de escritorio.  

- **Bursátil** Microsoft protege los datos con seguridad y cifrado seguros.  

- **Transitiv** Análisis de escritorio es compatible con la [declaración de privacidad](https://privacy.microsoft.com/privacystatement) de Microsoft y los términos de [servicio en línea](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=46).  



## <a name="diagnostic-data-flow"></a>Flujo de datos de diagnóstico

En la ilustración siguiente se muestra cómo fluyen los datos de diagnóstico de dispositivos individuales a través del servicio de datos de diagnóstico, Azure Log Analytics Storage y el área de trabajo de Log Analytics:

![Diagrama que ilustra el flujo de datos de diagnóstico de dispositivos](media/da-data-flow.png)

1. Inicie sesión en el Azure Portal e incorpore al análisis de escritorio. Cree la aplicación Azure AD para conectarse con Configuration Manager. Al configurar el análisis de escritorio, se crea un área de trabajo de Log Analytics de Azure en la ubicación de su elección.  

2. Conecta Configuration Manager e inscribe dispositivos  

    1. Configure el servicio en la nube de análisis de escritorio en Configuration Manager con los detalles de la aplicación Azure AD.  

    2. En un plazo de 15 minutos, Configuration Manager sincroniza las recopilaciones de dispositivos y los planes de implementaciones con el análisis de escritorio. Este proceso se repite cada hora.  

    3. Configuration Manager establece el ID. comercial, el nivel de datos de diagnóstico y otras opciones de configuración de los dispositivos de la recopilación de destino. Esta configuración especifica los dispositivos que aparecen en el área de trabajo de análisis de escritorio.  

    4. Las actualizaciones de compatibilidad se implementan en todos los dispositivos de destino.  

3. Los dispositivos envían datos de diagnóstico al servicio Microsoft Diagnostic Administración de datos para Windows. Este servicio se hospeda en el Estados Unidos.  

4. Cada día, Microsoft genera una instantánea de información centrada en ti. Esta instantánea combina los datos de diagnóstico de Windows con la entrada para los dispositivos inscritos. Este proceso se produce en el almacenamiento transitorio, que solo se usa en el análisis de escritorio. El almacenamiento transitorio se hospeda en centros de datos de Microsoft en el Estados Unidos. Las instantáneas se segregan por ID. comercial.  

5. Después, las instantáneas se copian en el área de trabajo de Azure Log Analytics adecuada.  

6. El análisis de escritorio almacena la entrada en Azure Log Analytics Storage. Estas configuraciones incluyen planes de implementación y decisiones de activos para la actualización y la importancia.  



## <a name="other-resources"></a>Otros recursos:

Para ver las preguntas más frecuentes relacionadas con la privacidad de análisis de escritorio, consulte [preguntas más frecuentes sobre privacidad](/sccm/desktop-analytics/faq#privacy).

Para obtener más información sobre los aspectos relacionados con la privacidad, consulte los siguientes artículos:

- [Windows 10 y RGPD para responsables de la toma de decisiones de ti](https://docs.microsoft.com/windows/privacy/gdpr-it-guidance)  

- [Configuración de datos de diagnóstico de Windows en su organización](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization)  

- [Campos y eventos de datos de diagnóstico del evaluador de Windows 7, Windows 8 y Windows 8.1](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-8.1-and-8/appraiser-diagnostic-data-events-and-fields)  

- [Campos y eventos de diagnóstico de Windows de nivel básico de Windows 10, versión 1809](https://docs.microsoft.com/windows/privacy/basic-level-windows-diagnostic-events-and-fields-1809)  

- [Eventos y campos de datos de diagnóstico mejorados de Windows 10, versión 1709 usados por el análisis de escritorio](https://docs.microsoft.com/windows/privacy/enhanced-diagnostic-data-windows-analytics-events-and-fields)  

- [Información general del visor de datos de diagnóstico](https://docs.microsoft.com/windows/privacy/diagnostic-data-viewer-overview)  

- [Términos de licencia y documentación](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31)  

- [Seguridad y privacidad en centros de datos de Microsoft Azure](https://azure.microsoft.com/global-infrastructure/)  

- [Confianza en la nube de confianza](https://azure.microsoft.com/overview/trusted-cloud/)  

- [Centro de confianza](https://www.microsoft.com/trustcenter)  
