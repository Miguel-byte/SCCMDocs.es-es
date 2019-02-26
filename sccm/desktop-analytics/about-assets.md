---
title: Recursos de análisis de escritorio
titleSuffix: Configuration Manager
description: Obtenga información sobre los dispositivos, aplicaciones, aplicaciones de Office, complementos de Office y las macros de Office en el escritorio de análisis.
ms.date: 01/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d07198cf-49bb-4712-8c63-063b4302cc11
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 149c5f2a4469a353c6dce6fde86527ca95518484
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56755557"
---
# <a name="assets-in-desktop-analytics"></a>Recursos de análisis de escritorio 

> [!Note]  
> Esta información se relaciona con un servicio en versión preliminar que puede modificarse sustancialmente antes de su lanzamiento comercial. Microsoft no ofrece ninguna garantía, expresa o implícita, con respecto a la información aquí proporcionada.  

Después de que los dispositivos notificarán datos a Analytics de escritorio, proporciona un inventario de los recursos siguientes:
- Dispositivos  
- Controladores de hardware  
- Aplicaciones instaladas  
- Aplicaciones de Office  
- Complementos de Office  
- Macros de Office  

En el portal de servicios, seleccione **activos** en el menú de análisis de escritorio.


## <a name="devices"></a>Dispositivos

El **dispositivos** ficha muestra información esencial sobre todos los dispositivos de su organización que se inscribe a análisis de escritorio. Se puede ordenar cualquier columna o filtrar determinados valores.

> [!NOTE]  
> Si el panel no notifica el número de dispositivos que espera para su entorno, consulte [solución de problemas de análisis de escritorio](/sccm/desktop-analytics/troubleshooting).  



## <a name="apps"></a>Aplicaciones

El **aplicaciones** pestaña aplicaciones muestra todos los instalada que detecta el servicio de los dispositivos de Windows.

**Merece la pena comentar** aplicaciones están instaladas en más de 2% de los dispositivos inscritos. <!--You can change the threshold of "noteworthy" by {doing something}.--> 

Configurar la **importancia** de aplicaciones si se establece alguna de las siguientes categorías:

- Crítica
- Importante
- Ignorar
- No se ha revisado

Seleccione la aplicación en la lista y seleccione **editar**. Esta acción muestra los detalles de la aplicación. Seleccione el **importancia** menú desplegable y establezca un valor. También puede asignar un **propietario**. Si realiza cambios, seleccione **guardar**. 


## <a name="office-apps"></a>Aplicaciones de Office

El **aplicaciones de Office** ficha es similar a la pestaña aplicaciones. Solo muestra las aplicaciones como Microsoft Word o Excel, y hay ninguna categorización o recuento de interés. Establecer la importancia y el propietario de las aplicaciones de Office en la misma manera que con otras aplicaciones.


## <a name="office-add-ins"></a>Complementos de Office

El **complementos de Office** pestaña se muestra en herramientas, por ejemplo, Microsoft Azure Information Protection o las herramientas de análisis de compatibilidad. Esta ficha es similar a la pestaña aplicaciones, e incluye el recuento de interés. Al igual que con las aplicaciones, establezca la importancia y el propietario. 


## <a name="office-macros"></a>Macros de Office

El **macros de Office** pestaña se muestra si los dispositivos recientemente han tenido acceso a los archivos que pueden incluir macros. 

<!-- (For a detailed list of these file types, see [File formats supported in the 2007 Office system (corrected)](https://blogs.technet.microsoft.com/office_resource_kit/2009/04/04/file-formats-supported-in-the-2007-office-system-corrected/) at the Office IT Pro blog.)
 -->

> [!NOTE]  
> Si también usa el [Readiness Toolkit](https://aka.ms/readinesstoolkit) para complementos de Office y Visual Basic para las macros de aplicaciones (VBA), esta pestaña también muestra datos adicionales de esos dispositivos. 
> 
> No es necesario usar el Kit de herramientas de preparación para usar análisis de escritorio.  



## <a name="next-steps"></a>Pasos siguientes

- [Obtenga información acerca de los planes de implementación de análisis de escritorio](/sccm/desktop-analytics/about-deployment-plans)  

- [Obtenga información acerca de las actualizaciones de seguridad y la característica](/sccm/desktop-analytics/about-updates)  

