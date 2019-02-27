---
title: Windows Autopilot con administración conjunta
titleSuffix: Configuration Manager
description: Usar Windows Autopilot con administración conjunta en Configuration Manager para simplificar el conjunto de copia de nuevos dispositivos Windows 10.
ms.date: 02/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e3e3c97f-5945-49ab-a622-9f6fe6b9737e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 28710b925444d681a161eff184b845a1cdd430b1
ms.sourcegitcommit: ef2960bd91655c741450774e512dd0a9be610625
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/26/2019
ms.locfileid: "56838759"
---
# <a name="windows-autopilot-with-co-management"></a>Windows Autopilot con administración conjunta

Recibir un nuevo dispositivo Windows 10 es emocionante. Sin embargo, puede tardar tiempo a configurar todas las aplicaciones y configuración de modo que puede ser productivo. Administración conjunta soluciona este problema con Windows Autopilot de aprovisionamiento de dispositivos.

AutoPilot proporciona una experiencia simplificada para usted y sus usuarios en las situaciones siguientes:
- Configurar y preconfigurar nuevos dispositivos Windows 10  
- Restablecer, reciclaje y recuperar los dispositivos existentes  

AutoPilot reduce el tiempo, recursos y complejidad asociados con la implementación, administración y retirada de los dispositivos. Al mismo tiempo, la experiencia para los usuarios es simplificada y fácil desde el primer inicio.

Windows Autopilot admite varios escenarios, todos los cuales se maximizarán con administración conjunta:

- Los usuarios pueden impulsar sus propias implementaciones de nuevos dispositivos en Active Directory con combinación de Azure AD híbrido o Azure Active Directory (Azure AD)  

- Puede configurar la implementación automática de nuevas implementaciones de dispositivo en Azure AD para dispositivos compartidos y quioscos  

- Con Windows Autopilot para los dispositivos existentes, utilice el Administrador de configuración para migrar un dispositivo existente de Windows 7 y Active Directory para Windows 10 y Azure AD  

En el siguiente vídeo, jefe de programas senior Danny Guillory y director de programas principal Andrew McMurray discutan y demostración de Windows Autopilot con administración conjunta:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Using-Windows-Autopilot-with-Co-Management/player]



## <a name="benefits"></a>Ventajas

Cuando se usa la administración conjunta y Autopilot juntos, asegúrese de tener que nuevos dispositivos que accedan a la red en el mismo estado de administración. En esta configuración, los dispositivos están inscritos en Intune y tienen un cliente de Configuration Manager.  Le permite usar el nuevo modelo de aprovisionamiento de Windows 10 y le ayuda a eliminar la necesidad de crear, mantener y actualizar las imágenes de sistema operativo personalizadas. 

En todos estos escenarios, puede automáticamente [habilitar la administración conjunta](/sccm/comanage/how-to-prepare-win10) por Intune. Esta automatización le ayuda con el proceso de aprovisionamiento y para la administración continua del dispositivo.

Con Autopilot, no deberá preocuparse por las imágenes y controladores. Se centran en el aprovisionamiento de dispositivos por este proceso automatizado mediante Intune y Configuration Manager a través de la administración conjunta.


Le mostramos cómo usar conjuntamente administración conjunta y Autopilot le permite ahora mismo:

#### <a name="reduce-time-costs-and-complexity"></a>Reducir el tiempo, los costos y complejidad
Windows Autopilot, se usa la versión optimizada para OEM de Windows 10 que está preinstalada en el dispositivo. Esta configuración guarda las organizaciones el esfuerzo de tener que mantener imágenes personalizadas y los controladores para cada modelo de dispositivo en uso. En lugar de restablecer la imagen inicial del dispositivo, transformar la instalación de Windows 10 existente a un estado "listo para el negocio". Se aplica la configuración y las directivas, instala las aplicaciones y cambia la edición de Windows 10. Por ejemplo, actualización de Windows 10 Pro a Windows 10 Enterprise para que pueda admitir características avanzadas.

#### <a name="improve-the-user-experience"></a>Mejorar la experiencia del usuario
La mejor experiencia de usuario hace que la menor interrupción y les ayuda a regresar a centrarse en su trabajo. Windows Autopilot ofrece un enfoque sencillo para ayudar a los usuarios configurar rápidamente con unos pocos clics y sus credenciales de Azure AD. Para muchas organizaciones con un campo de gran tamaño de los empleados remotos, use Windows Autopilot para el envío de nuevos dispositivos directamente desde el fabricante.

#### <a name="use-autopilot-and-configuration-manager-to-migrate-existing-windows-7-devices-to-windows-10"></a>Usar Autopilot y Configuration Manager para migrar los dispositivos existentes de Windows 7 a Windows 10
Con Windows Autopilot para los dispositivos existentes, crea un archivo de configuración e implementarlo con una secuencia de tareas de Configuration Manager. Este proceso migra fácilmente los dispositivos existentes de Windows 7 a Windows 10. Usar una imagen de la firma de Windows 10 en Configuration Manager y, a continuación, se aplican a los dispositivos existentes de Windows 7 con la configuración de Autopilot. Cuando el usuario arranca el dispositivo, usan el proceso de incorporación controlado por el usuario de Autopilot.

Estos son los pasos de Autopilot para los dispositivos existentes:

![Información general del proceso de Windows Autopilot para los dispositivos existentes](media/autopilot-for-existing-devices.png)

1. Implementar Directiva de grupo para redirigir las carpetas conocidas a OneDrive
2. Generar archivo de configuración de Autopilot
3. Implementar secuencia de tareas para actualizar a Windows 10
4. Equipo Windows 10 recorre Autopilot en el primer arranque

#### <a name="modernizing-device-provisioning-for-all-types-of-workers"></a>Modernización de aprovisionamiento de dispositivos para todos los tipos de trabajos
Con Autopilot, ahora puede proporcionar una implementación de sistema operativo manos libres en dispositivos sin personal de operación o dispositivos compartidos con el modo de implementación automática. Esta configuración satisface las necesidades de todos los distintos tipos de trabajos. Además, la función de restablecimiento de Windows Autopilot asegura que el reaprovisionamiento de un dispositivo a un nuevo usuario se simple y fácil. Este proceso simplifica lo que tradicionalmente era una tarea difícil cuando se tienen estacionales o contrato de los trabajadores. 



## <a name="case-study"></a>Caso práctico

La compañía de transporte ferroviario y logística alemán Shenker DB usa Autopilot para aumentar la productividad de los empleados y liberar sus equipos de TI puedan trabajar en tareas de soporte técnico habituales. Shenker tiene alejado de creación de imágenes tradicional y se ha reemplazado con el aprovisionamiento a través de la nube. Ahora usan Azure AD join e Intune para obtener nuevos dispositivos en marcha rápidamente. 

En lugar de tener su tiempo de residuos de trabajadores remotos viaja a una ubicación con servicios de TI, Shenker utiliza ahora Windows Autopilot. Su hardware de los trabajadores se incluyen directamente desde el fabricante para su oficina local. El trabajo conecta con el nuevo dispositivo a internet e inicie sesión con sus credenciales de Azure AD. El dispositivo, a continuación, se conecta a las aplicaciones y servicios que Schenker asigna el departamento de TI para el perfil de usuario individuales.

Para obtener más información, consulte [centraliza la empresa Global logística TI, une los empleados con modernas al área de trabajo digital](https://customers.microsoft.com/story/db-schenker-travel-transportation-windows-10).



## <a name="value-proposition"></a>Propuesta de valor

Cree la satisfacción de su organización mediante la creación de una mejor experiencia de usuario para los usuarios. Usar Windows Autopilot para reducir los costos. Libere tiempo para centrarse en otros proyectos para impulsar el mayor valor y el impacto para su organización.



## <a name="configure"></a>Configurar

Vea los siguientes artículos para más información:

[Usar Intune para crear perfiles de Windows Autopilot](https://docs.microsoft.com/intune/enrollment-autopilot)

[Windows Autopilot para los dispositivos existentes](/sccm/osd/deploy-use/windows-autopilot-for-existing-devices) secuencia de tareas

