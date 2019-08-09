---
title: Panel de administración de clientes de Office 365
titleSuffix: Configuration Manager
description: Revisión de la información de los clientes de Office 365 en el panel de administración de clientes de Office 365
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 07/26/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 69f234a2-b04b-445a-b81f-6b4acfc00eaf
ms.collection: M365-identity-device-management
ms.openlocfilehash: cf18203d4b6d4c8858e3547671b7bf63a2250db7
ms.sourcegitcommit: 72faa1266b31849ce1a23d661a1620b01e94f517
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/26/2019
ms.locfileid: "68537288"
---
# <a name="office-365-client-management-dashboard"></a>Panel de administración de clientes de Office 365

A partir de la versión 1802 de Configuration Manager, puede revisar la información del cliente de Office 365 en el panel de administración de clientes de Office 365. En el panel de administración de clientes de Office 365 se muestra una lista de los dispositivos correspondientes al seleccionar las secciones de un gráfico. <!--1357281 -->

## <a name="prerequisites"></a>Requisitos previos

Los datos que se muestran en el panel de administración de clientes de Office 365 proceden de inventario de hardware. Habilite el inventario de hardware y seleccione la clase de inventario de hardware **Configuraciones de Office 365 ProPlus** antes de que los datos aparezcan en el panel.
 
1. Habilite el inventario de hardware, si aún no está habilitado. Para obtener más información, consulte [Configurar el inventario de hardware](/sccm/core/clients/manage/inventory/configure-hardware-inventory).
2. En la consola de Configuration Manager, navegue a **Administración** > **Configuración de cliente** > **Configuración de cliente predeterminada**.  
3. En la pestaña **Inicio** , en el grupo **Propiedades** , haga clic en **Propiedades**.  
4. En el **configuración de cliente predeterminada** cuadro de diálogo, haga clic en **de inventario de Hardware**.  
5. En el **configuración de dispositivo** lista, haga clic en **establecer clases**.  
6. En el cuadro de diálogo **Clases de inventario de hardware**, seleccione **Configuración de Office 365 ProPlus**.  
7. Haga clic en **Aceptar** para guardar los cambios y cerrar la **clases de inventario de Hardware** cuadro de diálogo. 

El panel de administración de clientes de Office 365 comenzará a mostrar los datos a medida que se informe del inventario de hardware.

## <a name="viewing-the-office-365-client-management-dashboard"></a>Visualización del panel de administración de clientes de Office 365

Para ver el panel de administración de clientes de Office 365 en la consola de Configuration Manager, vaya a **Biblioteca de software** > **Información general** > **Administración de clientes de Office 365**. En la parte superior del panel, use la opción desplegable **Colección** para filtrar los datos del panel por miembros de una colección determinada. A partir de Configuration Manager versión 1802, en el panel de administración de clientes de Office 365 se muestra una lista de los dispositivos correspondientes al seleccionar las secciones de un gráfico.

El panel de administración de clientes de Office 365 proporciona una serie de gráficos con la siguiente información:

- Número de clientes de Office 365
- Versiones de cliente de Office 365
- Idiomas de cliente de Office 365
- Canales de cliente de Office 365. Para más información, consulte [Información general de los canales de actualización para Office 365 ProPlus](/DeployOffice/overview-of-update-channels-for-office-365-proplus).


## <a name="bkmk_o365_readiness"></a> Integración para la preparación de Office 365 ProPlus
<!--3735402-->
Desde la versión 1902 de Configuration Manager, se puede usar el panel para identificar los dispositivos con una confianza alta que estén listos para actualizar a Office 365 ProPlus. Esta integración proporciona conclusiones sobre los posibles problemas de compatibilidad con los complementos y las macros de Office usados en su entorno. Después, use Configuration Manager para implementar Office en los dispositivos que estén listos.

El panel de administración de clientes de Office365 incluye un nuevo icono, **Office 365 ProPlus Upgrade Readiness**. Este icono es un gráfico de barras de los dispositivos con los siguientes estados:
- No evaluado
- Preparado para la actualización
- Necesita revisión

Seleccione un estado para obtener los detalles en una lista de dispositivos. En este informe de preparación se muestran más detalles sobre los dispositivos. Se incluyen columnas para el estado de compatibilidad de los complementos y las macros de Office.

### <a name="prerequisites-for-office-365-proplus-readiness-integration"></a>Requisitos previos para la integración de la preparación de Office 365 ProPlus

- Habilite el inventario de hardware en la configuración de cliente. Para más información, consulte la sección [Requisitos previos](#prerequisites).  

- El dispositivo necesita disponer de conectividad a la red de entrega de contenido (CDN) de Office para poder descargar el archivo de preparación de un complemento. Para obtener más información, vea [Redes de entrega de contenido](https://docs.microsoft.com/office365/enterprise/content-delivery-networks). Si el dispositivo no puede descargar el archivo, el estado de los complementos será *Necesita revisión*.  

    > [!Note]  
    > No se envía ningún dato a Microsoft en relación con esta característica.  

### <a name="bkmk_ort"></a> Preparación de la macro detallada

De manera predeterminada, el agente de detección busca en la lista de archivos usados más recientemente (MRU por sus siglas en inglés) de cada dispositivo. Cuenta los archivos de la lista que admiten macros. Estos archivos pueden ser de los siguientes tipos:
- Formatos de archivos de Office habilitados para macros, como libros habilitados para macros de Excel (.xlsm) o documentos habilitados para macros de Word (.docm).  
- Formatos de Office más antiguos que no indican si hay contenido de macro, como un libro de Excel 97-2003 (.xls).

Si necesita una evaluación más detallada, implemente **Office Readiness Toolkit**. Esta herramienta analiza el código de un archivo de macro. Comprueba si hay cualquier posible problema de compatibilidad. Por ejemplo, que un archivo use una función que pueda cambiar en una versión más reciente de Office. Después de ejecutar Office Readiness Toolkit, Configuration Manager podrá usar los resultados obtenidos. Estos datos adicionales permiten mejorar el cálculo de la preparación del dispositivo. Para obtener más información, vea [Usar Readiness Toolkit para evaluar la compatibilidad de aplicaciones de Office 365 ProPlus](http://aka.ms/readinesstoolkit).

## <a name="office-365-proplus-upgrade-readiness-dashboard"></a>Panel de Upgrade Readiness para Office 365 ProPlus

*(Se introdujo en la versión 1906)*

<!--4021125-->
Para ayudarle a determinar qué dispositivos están listos para actualizar a Office 365 ProPlus, hay un panel de preparación a partir de la versión 1906. Incluye el icono de **Upgrade Readiness para Office 365 ProPlus** que se publicó en la versión 1902 de la rama actual de Configuration Manager. Los siguientes iconos nuevos de este panel le ayudan a evaluar la preparación de las macros y los complementos de Office:

- Implementación
- Preparación del dispositivo
- Preparación de complementos
- Instrucciones de compatibilidad de complementos
- Complementos principales por número de versión
- Número de dispositivos que tienen macros
- Preparación de las macros
- Avisos de macros

### <a name="using-the-office-365-proplus-upgrade-readiness-dashboard"></a>Uso del panel de Upgrade Readiness para Office 365 ProPlus
 
1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software** y expanda **Administración de clientes de Office 365**.
1. Seleccione el nodo **Office 365 ProPlus upgrade Readiness** .
1. Cambie la arquitectura de **Office** de **colección** y destino para cambiar la información retransmitida en el panel.

![Panel de Upgrade Readiness para Office 365 ProPlus](./media/4021125-office-365-upgrade-readiness-dashboard.png)

![Panel de Upgrade Readiness para Office 365 ProPlus](./media/4021125-office-365-to-add-ins.png)

![Panel de Upgrade Readiness para Office 365 ProPlus](./media/4021125-office-365-macro-advisories.png)

## <a name="next-steps"></a>Pasos siguientes

[Administración de Office 365 ProPlus con Configuration Manager](/sccm/sum/deploy-use/manage-office-365-proplus-updates)
