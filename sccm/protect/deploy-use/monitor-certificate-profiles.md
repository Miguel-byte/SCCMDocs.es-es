---
title: "Creación de perfiles de certificado | System Center Configuration Manager"
description: Aprenda a supervisar el estado de cumplimiento de los perfiles de certificado de System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 98feaa06-64b1-4e86-a122-93017c97cd4f
caps.latest.revision: 7
caps.handback.revision: 0
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: bb72571596e77ce3069c1f6526fb3ba00fc9ecdc


---
# <a name="how-to-monitor-certificate-profiles-in-system-center-configuration-manager"></a>Cómo supervisar perfiles de certificado en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*


Después de implementar los perfiles de certificado de System Center Configuration Manager en los usuarios de la jerarquía, puede usar los procedimientos siguientes para supervisar el estado de compatibilidad del perfil de certificado:  

-   [Ver los resultados de compatibilidad en la consola de Configuration Manager](#BKMK_console)  

-   [Ver los resultados de compatibilidad mediante informes](#BKMK_Reports)  

##  <a name="a-namebkmkconsolea-how-to-view-compliance-results-in-the-configuration-manager-console"></a><a name="BKMK_console"></a> Ver los resultados de compatibilidad en la consola de Configuration Manager  
 Use este procedimiento para ver los detalles sobre el cumplimiento de los perfiles de certificado implementados en la consola de System Center Configuration Manager.  

> [!NOTE]  
>  No use la consola de Configuration Manager para supervisar el cumplimiento del certificado SCEP. En su lugar, use los informes, tal como se describe en [How to View Compliance Results by Using Reports](#BKMK_Reports). En concreto, debe usar los informes de certificado que se encuentran en el nodo de informes **Acceso a los recursos de la compañía**.  
>   
>  -   Historial de certificados emitidos  
> -   Lista de activos con certificados a punto de expirar  
> -   Lista de activos por estado de emisión de certificado  

#### <a name="to-view-compliance-results-in-the-configuration-manager-console"></a>Para ver los resultados de compatibilidad en la consola de Configuration Manager  

1.  En la consola de System Center Configuration Manager, haga clic en **Supervisión**.  

2.  En el área de trabajo **Supervisión** , haga clic en **Implementaciones**.  

3.  En la lista **Implementaciones** , seleccione la implementación del perfil de certificado para el que desea revisar la información de compatibilidad.  

4.  Puede revisar la información de resumen sobre la compatibilidad del perfil de certificado en la página principal. Para ver información más detallada, seleccione el perfil de certificado y, a continuación, en la pestaña **Inicio** , en el grupo **Implementación** , haga clic en **Ver estado** para abrir la página **Estado de implementación** .  

     La página **Estado de implementación** contiene las siguientes pestañas:  

    -   **Compatible**: muestra la compatibilidad del perfil de certificado en función del número de recursos afectados. Puede hacer doble clic en una regla para crear un nodo temporal en el nodo **Usuarios** , en el área de trabajo **Activos y compatibilidad** . Este nodo contiene todos los usuarios que son compatibles con el perfil de certificado. El panel **Detalles del activo** muestra los usuarios que son compatibles con el perfil. Haga doble clic en un usuario de la lista para mostrar información adicional.  

        > [!IMPORTANT]  
        >  Un perfil de certificado no se evalúa si no es aplicable en un dispositivo cliente. Sin embargo, se devuelve como compatible.  

    -   **Error**: muestra una lista de todos los errores de la implementación de perfil de certificado seleccionada en función del número de recursos afectados. Puede hacer doble clic en una regla para crear un nodo temporal en el nodo **Usuarios** del área de trabajo **Activos y compatibilidad** . Este nodo contiene todos los usuarios que generaron errores con este perfil. Cuando se selecciona un usuario, el panel **Detalles del activo** muestra los usuarios afectados por el problema seleccionado. Haga doble clic en un usuario de la lista para mostrar información adicional sobre el problema.  

    -   **No compatible**: muestra una lista de todas las reglas no compatibles en el perfil de certificado en función del número de recursos afectados. Puede hacer doble clic en una regla para crear un nodo temporal en el nodo **Usuarios** del área de trabajo **Activos y compatibilidad** . El nodo contiene todos los usuarios que no son compatibles con este perfil. Cuando se selecciona un usuario, el panel **Detalles del activo** muestra los usuarios afectados por el problema seleccionado. Haga doble clic en un usuario de la lista para mostrar información adicional sobre el problema.  

    -   **Desconocido**: muestra una lista de todos los usuarios que no han notificado la compatibilidad de la implementación de perfil de certificado seleccionada y el estado de cliente actual de los dispositivos.  

5.  En la página **Estado de implementación** , puede revisar información detallada sobre la compatibilidad del perfil de certificado implementado. Se crea un nodo temporal en el nodo **Implementaciones** que le permite encontrar esta información rápidamente.  

     El estado de inscripción del certificado se muestra como un número. Utilice la tabla siguiente para determinar el significado de cada número:  

    |Estado de inscripción|Descripción|  
    |-----------------------|-----------------|  
    |0x00000001|La inscripción se realizó correctamente y el certificado se emitió.|  
    |0x00000002|La solicitud se envió y la inscripción está pendiente, o la solicitud se emitió fuera de banda.|  
    |0x00000004|La inscripción debe aplazarse.|  
    |0x00000010|Error.|  
    |0x00000020|Se desconoce el estado de la inscripción.|  
    |0x00000040|Se ha omitido la información de estado. Esto puede ocurrir si una entidad de certificación HYPERLINK "http://msdn.microsoft.com/en-us/windows/ms721572" \l "_security_certification_authority_gly" no es válida o no se ha seleccionado para la supervisión.|  
    |0x00000100|Se ha denegado la inscripción.|  

##  <a name="a-namebkmkreportsa-how-to-view-compliance-results-by-using-reports"></a><a name="BKMK_Reports"></a> Ver los resultados de compatibilidad mediante informes

 La configuración de cumplimiento en System Center Configuration Manager incluye informes integrados que se pueden utilizar para supervisar la información de perfiles de certificado. Estos informes tienen la categoría de informe de **Administración de compatibilidad y configuración**.  

> [!IMPORTANT]  
>  Debe usar un carácter comodín (%) para utilizar los parámetros **Filtro del dispositivo** y **Filtro de usuarios** en los informes de configuración de cumplimiento.  

 Para obtener más información sobre cómo configurar la generación de informes en Configuration Manager, vea [Reporting in System Center Configuration Manager](../../core/servers/manage/reporting.md) (Generación de informes en System Center Configuration Manager).  



<!--HONumber=Nov16_HO1-->


