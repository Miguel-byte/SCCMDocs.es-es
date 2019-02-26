---
title: Estado del cliente con la administración conjunta
titleSuffix: Configuration Manager
description: Mantener la visibilidad del estado de cliente de Configuration Manager desde el portal de Intune en Azure
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 5b243aac-8a1a-4f14-ba3f-5446bb483e92
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: d6838371a80530d5ab66abd9d8a976af41513e15
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56755564"
---
# <a name="client-health-with-co-management"></a>Estado del cliente con la administración conjunta

El estado de la red está conectado directamente en el estado de los dispositivos se consideran. Intune puede comunicarse con un cliente en mal estado, incluso cuando no está en la red. Usar la administración conjunta para combinar esta característica con capacidad de Configuration Manager para informar el 98% de los clientes en buen estado conocidos. A continuación, puede detectar, evaluar y proporcionar visibilidad en todos los clientes en tiempo real. Intune también agrega la compatibilidad necesaria para las actualizaciones de cumplimiento a través de todos los clientes conectados.

En el siguiente vídeo, Rob York del Administrador de programas senior y Ainley Locky del Administrador de marketing de productos tratan y demostración de mantenimiento de cliente con la administración conjunta:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Client-Health-Monitoring-with-Co-Management/player]



## <a name="benefits"></a>Ventajas

Evaluar el estado de cliente es una prioridad. System Center 2012 Configuration Manager agrega **CCMeval**. Esta utilidad es externa al cliente de Configuration Manager. Proporciona al cliente corrección automática y supervisión de estado. Sin embargo, este informe se basa en un dispositivo que están físicamente o prácticamente en su red interna. Administración conjunta ayuda a resolver este problema.

Con la administración conjunta, Intune puede informar sobre el estado de mantenimiento del cliente. Proporciona información de marca de tiempo para la validez de los datos. Esta información le indica si los dispositivos están en buen estado, puede conectarse, puede instalar aplicaciones, o pueden actualizar al sistema operativo necesario compilaciones. 

Para obtener una descripción detallada de esta característica, vea este vídeo de la [What ' s New in Configuration Manager](https://myignite.techcommunity.microsoft.com/sessions/64591) sesión en Ignite 2018.

> [!VIDEO https://www.youtube.com/embed/UAW2KBUq7DM?start=518]


Cuando Configuration Manager proporciona el estado del dispositivo que está instalado el cliente, pero no es, Intune puede proporcionar más información sin necesidad de conectarse al cliente. La información de estado del dispositivo en Intune es fácil de entender. Si el estado es distinto **correcto**, ofrece recomendaciones y pasos siguientes para solucionar problemas y corregirlo.

> [!Note]  
> Una versión futura se prevé las siguientes ventajas:
> - Administrador de configuración incluirá una funcionalidad adicional en CCMeval  
> - Le resultará más fácil identificar los equipos en mal estado potencialmente en Configuration Manager e Intune  
> - Puede agrupar los datos de estado de cliente de Intune  



## <a name="value-proposition"></a>Propuesta de valor

Con esta característica, ahora dispone de un origen de datos externo con Intune. Permite determinar los pasos siguientes para solucionar el problema de una amplia variedad de problemas del cliente. Ahora no es necesario crear informes adicionales o usar otras herramientas para extraer datos de cliente.

Cuando haya clientes en buen estado, fácilmente ha actualizado el cumplimiento de las revisiones. Un mejor cumplimiento de las revisiones significa mejorar la seguridad.



## <a name="configure"></a>Configurar

Para empezar a usar esta característica, siga estos pasos:

- Actualizar dispositivos con Windows 10, versión 1709 o posterior  

- [Habilitar la administración conjunta](/sccm/comanage/how-to-enable)  
    - No es necesario cambiar cualquier carga de trabajo a Intune  

- Actualizar el sitio de Configuration Manager y los clientes *versión 1806* o posterior  


### <a name="review-configuration-manager-client-health-in-intune"></a>Revise el estado de cliente de Configuration Manager en Intune

1. Inicie sesión en el [Portal de Azure](https://portal.azure.com/).  

2. Elija **todos los servicios** > **Intune**. Intune se encuentra en la **supervisión y administración** sección.  

3. Una vez que haya abierto el **Microsoft Intune** panel, en el menú en **ayuda y soporte técnico**, vaya a la **Troubleshooting** página.  

4. Use la **Seleccionar usuario** opción, busque el dispositivo específico en el **dispositivos** lista y selecciónela para abrir la página del dispositivo.  

5. Información de administración conjunta se muestra en la parte inferior de la página dispositivos. Esta información incluye los siguientes campos para el estado de cliente:  
    - **Estado del agente de Configuration Manager**  
    - **Última comprobación del agente de Configuration Manager en el tiempo**  

> [!Tip]  
> Dispositivos inscritos en Intune se conectan al servicio de nube tres veces al día, cada ocho horas aproximadamente. 
