---
title: Actualizar Windows 10
titleSuffix: Configuration Manager
description: Actualizar dispositivos a Windows 10 versión 1709 o versiones posteriores, lo cual es necesario para la administración conjunta
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 561eb5b6-f90c-485a-91c2-e45bb0ce7877
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0815a974f3b1f29f664a2948eed33de24c6ecff3
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56755559"
---
# <a name="upgrade-windows-10-for-co-management"></a>Actualizar Windows 10 para la administración conjunta

Cuando se trabaja hacia la incorporación de su organización para la administración conjunta, obtener actual es un obstáculo importante para algunos clientes. Requiere la administración conjunta [Windows 10 versión 1709](https://docs.microsoft.com/windows/whats-new/whats-new-windows-10-version-1709) o una versión posterior. Una vez que actualice a Windows y configurar la inscripción automática, los clientes se inscriben automáticamente para la administración conjunta.

En el siguiente vídeo, Rob York del Administrador de programas senior y Ainley Locky del Administrador de marketing de productos tratan y actualizar a Windows 10 para la administración conjunta de demostración:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Upgrading-to-Windows-10-to-Enable-Co-Management/player]



## <a name="why-upgrade"></a>¿Por qué actualizar?

Entre otros avances de plataforma, versión 1709 y versiones posterior de Windows 10 admite la inscripción automática. Este comportamiento hace que un dispositivo inscribir automáticamente a Intune cuando se ha unido a Azure Active Directory (Azure AD). 

Para obtener más información, consulte [Windows 10 de habilitar la inscripción automática](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment).


## <a name="how-to-do-it"></a>Para saber cómo hacerlo

Estas son algunas sugerencias que hemos aprendido de ayudar a miles de clientes a obtener actual rápidamente:

- Use las implementaciones por fases para implementar esta actualización a las personas adecuadas a la derecha veces. Para más información, vea [Crear implementaciones por fases](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence).  

- Usar almacenamiento en caché previa para reducir los tiempos de espera del usuario. Para obtener más información, vea [Configuración del contenido de la caché previa](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content).  

- Use la plantilla de secuencia de tareas de actualización en contexto de forma predeterminada. A continuación, configure los pasos anteriores y posteriores a la actualización y acciones de error. Para obtener más información, consulte [recomienda pasos de secuencia de tareas para su procesamiento posterior](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#recommended-task-sequence-steps-for-post-processing).  

- Si el entorno tiene una gran movilidad, Configuration Manager admite la actualización en contexto a través de cloud management gateway (CMG). Esta característica permite actualizar a los clientes de Windows 10 cuando están basados en internet. Para obtener más información sobre la instancia de CMG, consulte [ ](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway).  

- Ofrecen una participación en la administración conjunta para los usuarios que quiere que los usuarios pioneros. Este enfoque acelera la adopción inicial. Mediante la identificación de antemano estas personas, puede hacer que buena cobertura en los comienzos de una implementación. También recibir comentarios y validación de los usuarios que están interesados en las versiones más frecuentes y contento con el cambio. Programas de adopción temprana generan interés en las nuevas tecnologías y aumentan de tamaño con el tiempo.  


## <a name="case-studies"></a>Casos prácticos

Microsoft IT implementó Windows 10 a 96,000 usuarios distribuidos en Microsoft. La implementación incluye los usuarios remotos y los usuarios de la red corporativa. La implementación completada en nueve semanas. Para obtener más información sobre su experiencia, consulte [implementar Windows 10 en Microsoft como una actualización en contexto](https://www.microsoft.com/download/details.aspx?id=50377).  

Un fabricante de software Europeo de gran tamaño utiliza correctamente un grupo de adopción temprana. Después de las pruebas iniciales y piloto grupos, aproximadamente 2.000 empleados recibirán la primera actualización, actualizaciones y software. Este grupo incluye personal de TI y participar en voluntarios. Este nivel de compromiso con sus usuarios les proporciona un mayor nivel de confianza cuando se prueba y más credibilidad, cuando empieza a lanzamientos masivos.



## <a name="contact-fasttrack"></a>Póngase en contacto FastTrack

Si necesita ayuda con la actualización de Windows 10 en cualquier momento en el proceso, vaya a [Microsoft FastTrack](https://Microsoft.com/FastTrack/), inicie sesión y solicitar asistencia. 

Para obtener más información, consulte [obtener ayuda de FastTrack](/sccm/comanage/quickstart-fasttrack). 

