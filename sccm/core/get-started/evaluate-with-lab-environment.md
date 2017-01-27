---
title: Evaluar Configuration Manager | Microsoft Docs
description: "Cree un entorno de laboratorio para evaluar System Center Configuration Manager para usarlo en la organización."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 01b30260-f03a-4851-a549-d1b76e8cfc69
caps.latest.revision: 25
caps.handback.revision: 0
author: brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 35e48666f4d1a2363304650f960531fd0630a291
ms.openlocfilehash: ad3c849bd3ebfc6c0aa795e5b49a4850371cda47


---
# <a name="evaluate-system-center-configuration-manager-by-building-your-own-lab-environment"></a>Evalúe System Center Configuration Manager mediante la creación de su propio entorno de laboratorio

*Se aplica a: System Center Configuration Manager (rama actual)*

Aprenda a crear un entorno de laboratorio para evaluar System Center Configuration Manager para usarlo en su organización.  

## <a name="evaluate-system-center-configuration-manager-by-building-your-own-lab-environment"></a>Evalúe System Center Configuration Manager mediante la creación de su propio entorno de laboratorio  
 System Center Configuration Manager es una herramienta eficaz y compleja para administrar usuarios, dispositivos y software. Se recomienda realizar una evaluación exhaustiva de System Center Configuration Manager antes de la implementación completa, para que se puedan combinar ejercicios de comprensión conceptual con ejercicios prácticos.  

 Esta guía está destinada principalmente a los administradores que evalúen el uso de Configuration Manager en entornos corporativos.  

-   Administradores que busquen una solución para administrar totalmente sus equipos, servidores y dispositivos móviles.  

-   Administradores de industrias de alta seguridad que requieran la seguridad de la administración de dispositivos local con la flexibilidad de la administración de dispositivos basada en la nube.  

-   Administradores que quieran administrar el escalado de su arquitectura de servidor local.  

### <a name="what-this-lab-does"></a>Qué pretende este laboratorio  
 El objetivo principal de la creación de este entorno es ofrecerle el conocimiento general para empezar a trabajar con Configuration Manager y para mejorar la comprensión de Configuration Manager de manera práctica. Para ello, le guía a través de un ensamblado rápido de la versión actual de Configuration Manager, con dos servidores:  

-   Active Directory de hospedaje, controlador de dominio y servidor DNS  

-   Un segundo Configuration Manager de hospedaje y todos los componentes de SQL Server asociados.  

-   Las máquinas cliente se instalan en Hyper-V. El laboratorio en sí también puede ejecutarse como un sistema completamente virtualizado en un único servidor.  

### <a name="what-this-lab-does-not-do"></a>Qué no pretende este laboratorio  
 Este laboratorio no le guiará a través de todos los escenarios de Configuration Manager y no está diseñado para migrarse inmediatamente a un entorno activo.  

 Al compilar este laboratorio, tendrá un entorno funcional en el que trabajar. Sin embargo, este entorno no se optimizará para el rendimiento del sistema, la administración del espacio del disco duro, el almacenamiento de SQL Server, etc.  

###  <a name="a-namebkmkevalreca-recommended-reading-prior-to-beginning-the-lab"></a><a name="BKMK_EvalRec"></a> Lectura recomendada antes de comenzar la práctica  
 Hay una gran cantidad de contenido disponible en la [documentación para System Center Configuration Manager](http://docs.microsoft.com/sccm/). Una selección de los temas de esta biblioteca se incluyen a continuación. Se recomienda que todos los administradores que trabajen en laboratorios los lean antes de comenzar estos ejercicios.  

-   Obtenga información sobre los conceptos básicos de la consola de Configuration Manager, los portales de usuario final y los escenarios de ejemplo en [Introduction to System Center Configuration Manager](../../core/understand/introduction.md) (Introducción a System Center Configuration Manager).  

-   Obtenga información sobre las funcionalidades de administración principales de Configuration Manager en [Features and capabilities of System Center Configuration Manager](../../core/plan-design/changes/features-and-capabilities.md) (Características y funcionalidades de System Center Configuration Manager).  

-   Refuerce sus conocimientos con [Fundamentals of System Center Configuration Manager](../../core/understand/fundamentals.md) (Aspectos básicos de System Center Configuration Manager).  

-   Aprenda la importancia de los roles de seguridad en [Fundamentals of role-based administration for System Center Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md) (Conceptos básicos de la administración basada en roles de System Center Configuration Manager).  

-   La lectura de [Concepts for content management](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md) (Conceptos de administración de contenido) puede ilustrarle sobre conceptos específicos relacionados con la administración de contenido.  

-   El tema [Understand how clients find site resources and services for System Center Configuration Manager](../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md) (Comprender cómo los clientes buscan servicios y recursos de sitio para System Center Configuration Manager) le ayudará a admitir correctamente las operaciones diarias de su implementación.  



<!--HONumber=Jan17_HO4-->


