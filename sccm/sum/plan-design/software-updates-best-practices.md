---

title: Procedimientos recomendados para las actualizaciones de software | Microsoft Docs
description: Use estos procedimientos recomendados para las actualizaciones de software en System Center Configuration Manager.
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: 6d20389a-9de2-4a64-bced-9fc4fa519174
translationtype: Human Translation
ms.sourcegitcommit: d94acac84f052a01de9d9c9f65f237c0006c45b8
ms.openlocfilehash: 5df20f3703442de1be6220ca2770e182e330c036
ms.lasthandoff: 04/26/2017



---
# <a name="best-practices-for-software-updates-in-system-center-configuration-manager"></a>Procedimientos recomendados para las actualizaciones de software en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

En este tema, se incluyen procedimientos recomendados para las actualizaciones de software en System Center Configuration Manager. La información se ordena en prácticas recomendadas para la instalación inicial y prácticas recomendadas para las operaciones en curso.  

## <a name="installation-best-practices"></a>Procedimientos recomendados de instalación  
 Use los procedimientos recomendados siguientes cuando instale actualizaciones de software en Configuration Manager.  

### <a name="use-a-shared-wsus-database-for-software-update-points"></a>Usar una base de datos WSUS compartida para los puntos de actualización de software  
 Cuando instale más de un punto de actualización de software en un sitio primario, utilice la misma base de datos de WSUS para cada punto de actualización de software del mismo bosque de Active Directory. Al compartir la misma base de datos, puede mitigar considerablemente el impacto en el rendimiento del cliente y de la red que se puede producir cuando los clientes cambian a un nuevo punto de actualización de software. Cuando un cliente cambia a un nuevo punto de actualización de software que comparte una base de datos con el punto de actualización de software anterior, se sigue produciendo un examen de diferencias, pero es mucho menor que si el servidor WSUS tuviera su propia base de datos.  

> [!IMPORTANT]  
>  Cuando se utiliza una base de datos WSUS compartida para los puntos de actualización de software, también se deben compartir las carpetas locales de contenido de WSUS.  

 Para obtener más información sobre el intercambio de puntos de actualización de software, consulte la sección [Cambio de punto de actualización de software](../../sum/plan-design/plan-for-software-updates.md#BKMK_SUPSwitching) del tema [Planear las actualizaciones de software en System Center Configuration Manager](../../sum/plan-design/plan-for-software-updates.md).  

### <a name="when-configuration-manager-and-wsus-use-the-same-sql-server-configure-one-of-these-to-use-a-named-instance-and-the-other-to-use-the-default-instance-of-sql-server"></a>Cuando Configuration Manager y WSUS usan el mismo servidor SQL Server, configure uno de ellos para que use una instancia con nombre y el otro para que use la instancia predeterminada de SQL Server  
 Cuando las bases de datos de Configuration Manager y WSUS usan el mismo servidor SQL Server y comparten la misma instancia de SQL Server, no podrá determinar fácilmente el uso de recursos entre las dos aplicaciones. Cuando se usa una instancia de SQL Server diferente para Configuration Manager y WSUS, es más sencillo diagnosticar y solucionar problemas del uso de recursos que pudieran producirse en cada aplicación.  

### <a name="specify-the-store-updates-locally-setting-for-the-wsus-installation"></a>Especificar la configuración de "Guardar actualizaciones localmente" para la instalación de WSUS  
 Cuando instale WSUS, seleccione la opción de **Guardar actualizaciones localmente**. Cuando se selecciona esta opción, los términos de la licencia asociados a las actualizaciones de software se descargan durante el proceso de sincronización y se almacenan en el disco duro local para el servidor WSUS. Cuando esta opción no esté seleccionada, los equipos cliente podrían no examinar el cumplimiento de las actualizaciones de software que tengan términos de licencia. Cuando se instala el punto de actualización de software, el administrador de sincronización de WSUS comprueba que esta configuración se habilita cada 60 minutos, de forma predeterminada.  

## <a name="operational-best-practices"></a>Prácticas recomendadas de uso  
 Siga las recomendaciones siguientes al usar las actualizaciones de software:  

### <a name="limit-software-updates-to-1000-in-a-single-software-update-deployment"></a>Limitar las actualizaciones de software a 1000 en una única implementación de actualización de software  
 Debe limitar el número de actualizaciones de software a 1.000 por cada implementación de actualización de software. Cuando se crea una regla de implementación automática, compruebe que los criterios que especifique no dan como resultado más de 1000 actualizaciones de software. Al implementar manualmente las actualizaciones de software, no seleccione más de 1.000 actualizaciones para implementar.  

### <a name="create-a-new-software-update-group-each-time-an-automatic-deployment-rule-runs-for-patch-tuesday-and-for-general-deployment"></a>Crear un nuevo grupo de actualizaciones de software cada vez que se ejecuta una regla de implementación automática para "Patch Tuesday" y para la implementación general  
 Hay un límite de 1000 actualizaciones de software para una implementación de actualización de software. Cuando cree una regla de implementación automática, especifique si desea utilizar un grupo de actualización existente o crear un nuevo grupo de actualización cada vez que se ejecute la regla. Cuando especifique criterios en una regla de implementación automática que resulte en varias actualizaciones de software y la regla se ejecute en una programación recurrente, especifique la creación de un nuevo grupo de actualizaciones de software cada vez que se ejecute la regla. Esto evitará que se sobrepase el límite de 1000 actualizaciones de software por implementación.  

### <a name="use-an-existing-software-update-group-for-automatic-deployment-rules-for-endpoint-protection-definition-updates"></a>Usar un grupo de actualizaciones de software existente para las reglas de implementación automática para actualizaciones de definiciones de Endpoint Protection  
 Utilice siempre un grupo de actualizaciones de software existente cuando use una regla de implementación automática para implementar las actualizaciones de definiciones de Endpoint Protection con frecuencia. De lo contrario, es posible que se creen con el tiempo cientos de grupos de actualizaciones de software. Por lo general, los publicadores de actualizaciones de definición establecerán la caducidad de estas actualizaciones cuando sean reemplazadas por cuatro actualizaciones más recientes. Por lo tanto, el grupo de actualizaciones de software que se crea mediante la regla de implementación automática nunca contendrá más de cuatro actualizaciones de definiciones para el publicador: una activa y tres obsoletas.  

## <a name="see-also"></a>Véase también  
 [Planear las actualizaciones de software en System Center Configuration Manager](../../sum/plan-design/plan-for-software-updates.md)

