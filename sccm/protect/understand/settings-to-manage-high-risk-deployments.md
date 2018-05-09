---
title: Administración de implementaciones de alto riesgo
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo configurar el sitio en System Center Configuration Manager para advertir a los administradores si crean una implementación de alto riesgo.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 8d37b983-a964-402c-819d-2512ed2d463b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 44c7c805baedde820bc230dc25a3186762ecc8dc
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="settings-to-manage-high-risk-deployments-for-system-center-configuration-manager"></a>Configuración para administrar implementaciones de alto riesgo para System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*


Con System Center Configuration Manager, puede configurar un sitio de modo que avise a los administradores si crean una implementación de una secuencia de tareas de alto riesgo. Se consideran implementaciones de alto riesgo las siguientes:  

-   Una implementación que se instala automáticamente  

-   Una implementación que tiene el potencial de provocar resultados no deseados  

 Por ejemplo, una secuencia de tareas con el propósito **Requerido** que implementa un sistema operativo se considera de alto riesgo.  

 Para reducir el riesgo de una implementación de alto riesgo no deseada, puede configurar límites de tamaño en estas opciones de comprobación de la implementación:  

-   **Límites de tamaño de la recopilación**: oculta las recopilaciones que contienen más clientes que el límite al crear una implementación.  

    -   **Tamaño predeterminado**: esta opción oculta, de manera predeterminada, las recopilaciones que contienen más clientes que el límite al crear una implementación. Puede ver igualmente estas recopilaciones al crear la implementación, pero están ocultas de manera predeterminada. El valor predeterminado es 100. Escriba un valor de 0 para omitir esta configuración.  

    -   **Tamaño máximo**: esta opción siempre oculta las recopilaciones que contienen más clientes que el límite al crear una implementación. El valor predeterminado es 0, que omite esta configuración. El valor del **Tamaño máximo** debe ser mayor que el valor del **Tamaño predeterminado** .  

     Por ejemplo, establezca el **Tamaño predeterminado** en 100 y el **Tamaño máximo** en 1000. Al crear una implementación de alto riesgo, la ventana **Seleccionar recopilación** solo mostrará las recopilaciones que contengan menos de 100 clientes. Si desactiva la configuración **Ocultar recopilaciones con un número de miembros superior a la configuración de tamaño mínimo del sitio**, la ventana mostrará las recopilaciones que contengan menos de 1000 clientes.  

-   **Recopilaciones con servidores del sistema de sitio**: bloquea las implementaciones, o bien solicita una comprobación antes de crear la implementación, cuando la recopilación de destino contiene un equipo con un rol de sistema de sitio. Cuando se bloquea una implementación, debe seleccionar una recopilación diferente que cumpla los criterios de comprobación de la implementación.  

> [!NOTE]  
>  Las implementaciones de alto riesgo siempre se limitan a las recopilaciones personalizadas, las recopilaciones que cree y la recopilación integrada **Equipos desconocidos** . Cuando cree una implementación de alto riesgo, no puede seleccionar una recopilación integrada como **Todos los sistemas**.  

### <a name="to-configure-deployment-verification-for-a-site"></a>Para configurar la comprobación de la implementación de un sitio  

1.  En la consola de Configuration Manager, elija **Administración** >**Configuración del sitio** > **Sitios** y después seleccione el sitio primario que se va a configurar.  

2.  En la pestaña **Inicio**, en el grupo **Propiedades**, elija **Propiedades** y después elija la pestaña **Verificación de la implementación**.  

3.  Después de establecer la configuración que quiere usar, elija **Aceptar** para guardar la configuración.  

### <a name="see-also"></a>Consulte también  
 [Configurar sitios y jerarquías para System Center Configuration Manager](../../core/servers/deploy/configure/configure-sites-and-hierarchies.md)
