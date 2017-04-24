---
title: Actualizar clientes | Microsoft Docs
description: Actualice clientes en equipos Windows en System Center Configuration Manager.
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6143fd47-48ec-4bca-b53b-5b9b9f067bc3
caps.latest.revision: 11
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: a5b59a1d31d897473262edcd0912ef0fcbedd100
ms.lasthandoff: 03/06/2017


---
# <a name="how-to-upgrade-clients-for-windows-computers-in-system-center-configuration-manager"></a>Actualizar clientes de equipos Windows con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Puede actualizar el cliente en equipos Windows mediante los métodos de instalación de cliente o las características de actualización de cliente automática que ofrece Configuration Manager. Los siguientes métodos de instalación de cliente son mecanismos válidos para actualizar el software cliente en equipos Windows:  

-   Instalación de directiva de grupo  

-   Instalación de script de inicio de sesión  

-   Instalación manual  

-   Instalación de actualización  

 Si está interesado en actualizar el cliente mediante los métodos de instalación de cliente, obtenga más información sobre el uso de tales métodos en [Implementar clientes en equipos Windows con System Center Configuration Manager](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md).

 A partir de la versión 1610, puede excluir clientes de la actualización. Para ello, debe especificar un grupo de exclusión. Para obtener más información, consulte [How to exclude upgrading clients for Windows computers](exclude-clients-windows.md) (Cómo excluir la actualización de clientes para equipos Windows).  


> [!TIP]  
>  Si va a actualizar su infraestructura desde una versión anterior de Configuration Manager \(como Configuration Manager 2007 o System Center 2012 Configuration Manager\), se recomienda que realice las actualizaciones de servidor, incluida la instalación de todas las actualizaciones de la rama actual, antes de actualizar los clientes Configuration Manager.   La última actualización de la rama actual contiene la versión más reciente del cliente, por lo que es mejor realizar las actualizaciones de cliente después de instalar todas las actualizaciones de Configuration Manager que desea utilizar.

> [!NOTE]
> Si piensa volver a asignar el sitio a los clientes durante la actualización, puede especificar el nuevo sitio mediante la propiedad de client.msi SMSSITECODE. Si usa AUTO para la propiedad SMSSITECODE, también debe especificar SITEREASSIGN=TRUE para permitir que se produzca la reasignación de sitio automática durante la actualización. Para obtener más información, consulte [SMSSITECODE](../../deploy/about-client-installation-properties.md#smssitecode).

## <a name="use-automatic-client-upgrade"></a>Usar una actualización de cliente automática  
 También puede configurar Configuration Manager para actualizar de forma automática el software cliente a la versión de cliente de Configuration Manager más reciente cuando Configuration Manager identifique que un cliente que está asignado a la jerarquía de Configuration Manager sea de una versión anterior a la usada en la jerarquía. Este escenario incluye la actualización del cliente a la última versión cuando intenta asignarse a un sitio de Configuration Manager.  

 Un cliente puede actualizarse automáticamente en los siguientes escenarios:  

-   La versión del cliente es inferior a la versión que se utiliza en la jerarquía.  

-   El cliente del sitio de administración central tiene instalado un paquete de idioma mientras que el cliente existente no.  

-   Uno de los requisitos previos del cliente de la jerarquía es de una versión diferente a la instalada en el cliente.  

-   Uno o varios de los archivos de instalación del cliente son de una versión diferente.  

> [!NOTE]  
>  Es posible ejecutar el informe **Recuento de clientes de Configuration Manager por versiones de cliente** de la carpeta de informes **Sitio - Información del cliente** para identificar las diferentes versiones del cliente de Configuration Manager de su jerarquía.  

 Configuration Manager crea un paquete de actualización de manera predeterminada que se envía de forma automática a todos los puntos de distribución en la jerarquía. Si realiza cambios en el paquete de cliente del sitio de administración central, por ejemplo, si agrega un paquete de idioma del cliente, Configuration Manager actualiza de forma automática el paquete y lo distribuye a todos los puntos de distribución de la jerarquía. Si se habilita la actualización automática de cliente, todos los clientes instalarán automáticamente el nuevo paquete de idioma del cliente.  

> [!NOTE]  
>  Configuration Manager no envía de forma automática el paquete de actualización de cliente a los puntos de distribución basados en la nube de Configuration Manager.  

 Se recomienda que habilite las actualizaciones de cliente automáticas en la jerarquía. Esto permitirá que los clientes se mantengan actualizados con una sobrecarga administrativa mínima.  

 Utilice el siguiente procedimiento para configurar la actualización de cliente automática. La actualización de cliente automática debe configurarse en un sitio de administración central y esta configuración se aplica a todos los clientes de la jerarquía.  

### <a name="to-configure-automatic-client-upgrades"></a>Para configurar las actualizaciones automáticas de cliente  

1.  En la consola de Configuration Manager, haga clic en **Administración**.  

2.  En el área de trabajo **Administración** , expanda **Configuración del sitio**y, a continuación, haga clic en **Sitios**.  

3.  En la pestaña **Inicio** , en el grupo **Sitios** , haga clic en **Configuración de jerarquía**.  

4.  En la pestaña **Actualización de cliente** del cuadro de diálogo **Propiedades de configuración de jerarquía** , revise la versión y la fecha del cliente de producción y asegúrese de que sea la versión que quiere usar para actualizar equipos Windows.  Si no es la versión de cliente que esperaba ver, quizá sea necesario promover el cliente de preproducción a producción. Para obtener más información, vea [Cómo probar las actualizaciones de cliente en una recopilación de preproducción en System Center Configuration Manager](../../../../core/clients/manage/upgrade/test-client-upgrades.md).  

5.  Haga clic en **Actualizar todos los clientes en la jerarquía con un cliente de producción** y haga clic en **Aceptar** en el cuadro de diálogo de confirmación.  

6.  Si no quiere que las actualizaciones de cliente se apliquen a los servidores, haga clic en **No actualizar servidores**.  

7.  Especifique el número de días en que los equipos deben actualizar el cliente después de recibir la directiva de cliente. El cliente se actualizará en un intervalo aleatorio dentro de este número de días. Esto impide que se produzcan escenarios donde un gran número de equipos cliente se actualiza simultáneamente.

    > [!NOTE]
    > Un equipo debe estar en ejecución para actualizar el cliente. Si no hay ningún equipo en ejecución cuando se ha programado la recepción de la actualización, esta no se lleva a cabo. En su lugar, cuando se reinicia el equipo, se programa otra actualización para una hora aleatoria dentro del número de días permitidos. Si esto ocurre una vez transcurrido el número de días para actualizar, la actualización se programará para que se produzca a una hora aleatoria en las próximas 24 horas después de reiniciar el equipo.
    >     
    > Debido a este comportamiento, los equipos que habitualmente se apagan al final del día pueden tardar más de lo esperado en actualizarse si la hora de actualización programada de forma aleatoria no se encuentra dentro de las horas normales de trabajo.

7. A partir de la versión 1610, si quiere excluir clientes de la actualización, debe hacer clic en **Exclude specified clients from upgrade** (Excluir los clientes especificados de la actualización) y especificar la recopilación que se va a excluir.

8.  Si quiere que el paquete de instalación de cliente se copie a los puntos de distribución habilitados para contenido preconfigurado, haga clic en **Distribuir automáticamente un paquete de instalación de cliente a los puntos de distribución habilitados para contenido preconfigurado**.  

9. Haga clic en **Aceptar** para guardar la configuración y cerrar el cuadro de diálogo **Propiedades de configuración de jerarquía** . Los clientes reciben esta configuración la próxima vez que descarguen la directiva.  

