---
title: Privacidad y seguridad de la migración
titleSuffix: Configuration Manager
description: Obtenga información sobre la privacidad y los procedimientos recomendados de seguridad para la migración al entorno de System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 6893fce1-7ad5-4151-9ba9-3096871e8e4a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8cc6c1cee04e815c8a34f24236333fb927ed44fc
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32337914"
---
# <a name="security-and-privacy-for-migration-to-system-center-configuration-manager"></a>Seguridad y privacidad de la migración a System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Este tema contiene información sobre la privacidad y los procedimientos recomendados de seguridad para la migración al entorno de System Center Configuration Manager.  

## <a name="security-best-practices-for-migration"></a>Prácticas recomendadas de seguridad para la migración  
 Utilice la siguiente práctica de seguridad para la migración.  

|Práctica recomendada de seguridad|Más información|  
|----------------------------|----------------------|  
|Use la cuenta de equipo para la cuenta de proveedor de SMS de sitio de origen y la cuenta de SQL Server de sitio de origen, en lugar de una cuenta de usuario.|Si se debe utilizar una cuenta de usuario para la migración, quite los detalles de la cuenta cuando se haya completado la migración.|  
|Utilice IPsec al migrar contenido desde un punto de distribución en un sitio de origen a un punto de distribución en el sitio de destino.|Aunque al contenido migrado se le aplica un algoritmo hash para detectar posibles manipulaciones, si se modifican los datos mientras se transfiere, se producirá un error en la migración.|  
|Restrinja y controle los usuarios administrativos que pueden crear trabajos de migración.|La integridad de la base de datos de la jerarquía de destino depende de la integridad de datos que elige el usuario administrativo para importar desde la jerarquía de origen. Además, este usuario administrativo puede leer todos los datos de la jerarquía de origen.|  

### <a name="security-issues-for-migration"></a>Problemas de seguridad para la migración  
La migración tiene los siguientes problemas de seguridad:  

-   Los clientes que están bloqueados en un sitio de origen podrían asignarse con éxito a la jerarquía de destino antes de migrar su registro de cliente.  

     Aunque Configuration Manager conserva el estado bloqueado de los clientes que se migran, el cliente puede asignarse correctamente a la jerarquía de destino si la asignación se produce antes de que se complete la migración del registro de cliente.  

-   Los mensajes de auditoría no se migran.  

Al migrar datos desde un sitio de origen a un sitio de destino, perderá cualquier información de auditoría de la jerarquía de origen.  

## <a name="privacy-information-for-migration"></a>Información de privacidad para la migración  
 La migración detecta la información de las bases de datos del sitio que se identifican en una infraestructura de origen y almacena estos datos en la base de datos de la jerarquía de destino. La información que System Center Configuration Manager pueda detectar de un sitio o una jerarquía de origen depende de las características habilitadas en el entorno de origen, así como de las operaciones de administración efectuadas en ese entorno de origen.  

 Para obtener más información acerca de la información de seguridad y privacidad, consulte uno de los siguientes temas:  

-   Para obtener más información sobre la información de privacidad de Configuration Manager 2007, consulte [Security and Privacy for Configuration Manager 2007](http://go.microsoft.com/fwlink/p/?LinkId=216450) (Seguridad y privacidad para Configuration Manager 2007) en la biblioteca de documentación de Configuration Manager 2007.  

-   Para obtener más información sobre la información de privacidad de System Center 2012 Configuration Manager, consulte [Seguridad y privacidad en System Center 2012 Configuration Manager](https://technet.microsoft.com/library/gg682033.aspx) en la biblioteca de documentación de System Center 2012 Configuration Manager.  

-   Para obtener más información sobre la información de privacidad de System Center Configuration Manager, consulte [Security and privacy for System Center Configuration Manager](../../core/plan-design/security/security-and-privacy.md) (Seguridad y privacidad de System Center Configuration).  

Puede migrar algunos o todos los datos admitidos desde un sitio de origen a una jerarquía de destino.  

La migración no está habilitada de forma predeterminada y requiere varios pasos de configuración. La información de migración no se envía a Microsoft.  

Antes de migrar datos de una jerarquía de origen, tenga en cuenta los requisitos de privacidad.  
