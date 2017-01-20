---
title: Crear aplicaciones de Windows Embedded | System Center Configuration Manager
description: Consulte las consideraciones que debe tener en cuenta al crear e implementar aplicaciones para dispositivos de Windows Embedded.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 16acfd63-0c40-424c-82f4-8c63f7f1c30b
caps.latest.revision: 7
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: b329978126a205a1e790b58465f011c51d4fd171


---
# <a name="create-windows-embedded-applications-with-system-center-configuration-manager"></a>Crear aplicaciones de Windows Embedded con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Además de los otros requisitos y procedimientos de System Center Configuration Manager para crear una aplicación, también debe tener en cuenta las consideraciones siguientes al crear e implementar aplicaciones para dispositivos de Windows Embedded.  

## <a name="general-considerations"></a>Consideraciones generales  

-   Cuando se implementan aplicaciones en dispositivos de Windows Embedded con filtros de escritura habilitados, se puede especificar si se desea deshabilitar el filtro de escritura en el dispositivo durante la implementación y luego reiniciar el dispositivo después de la misma. Si no se deshabilita el filtro de escritura, el software se implementa en una superposición temporal y, a menos que otra implementación fuerce la conservación de los cambios, no estará instalado cuando el dispositivo se reinicie.  

-   Cuando implemente una aplicación en un dispositivo de Windows Embedded, asegúrese de que el dispositivo es miembro de una recopilación que tenga una ventana de mantenimiento configurada. Esto le permite administrar cuándo se deshabilita y habilita el filtro de escritura, y cuándo se reinicia el dispositivo.  

-   La opción de la experiencia del usuario que permite controlar el comportamiento de los filtros de escritura es la casilla **Confirmar cambios dentro de la fecha límite o en una ventana de mantenimiento (reinicio necesario)**.  

## <a name="tips-for-deploying-applications"></a>Sugerencias para la implementación de aplicaciones  

### <a name="use-required-applications-rather-than-available-applications-for-windows-embedded-devices-that-have-write-filters-enabled"></a>Utilice las aplicaciones necesarias en lugar de las aplicaciones disponibles para dispositivos de Windows Embedded que tengan habilitados filtros de escritura  
 Dado que los usuarios no pueden instalar aplicaciones del Centro de software de un dispositivo de Windows Embedded con filtros de escritura habilitados, implemente siempre las aplicaciones con el propósito de implementación de requerida en lugar de disponible en estos dispositivos. Por lo general, esto no significa un problema porque los equipos que ejecutan un sistema operativo Windows Embedded suelen ejecutar una sola aplicación que debe ejecutarse del mismo modo para varios usuarios. Por este motivo, estos dispositivos están bloqueados y altamente administrados por el departamento de TI. Las aplicaciones necesarias son adecuadas para este escenario. Sin embargo, si los usuarios deben ejecutar más de una aplicación en dispositivos incrustados que tienen habilitados filtros de escritura, informe a estos usuarios sobre las siguientes limitaciones:  

-   Los usuarios no pueden instalar el software necesario desde el Centro de software.  

-   Los usuarios no pueden cambiar su horario comercial en la pestaña Opciones del Centro de software.  

-   Los usuarios no pueden posponer la instalación de una aplicación necesaria.  

 Además, los usuarios que tienen derechos reducidos no pueden iniciar sesión durante un período de mantenimiento si Configuration Manager está realizando cambios en las instalaciones y actualizaciones de software. Durante este período, los usuarios ven un mensaje que les informa que el dispositivo no está disponible porque se le están realizando tareas de mantenimiento.  

### <a name="do-not-deploy-applications-to-windows-embedded-devices-that-have-write-filters-enabled-if-the-applications-require-the-user-to-accept-the-license-terms"></a>No implemente aplicaciones en dispositivos de Windows Embedded que tienen habilitados filtros de escritura si las aplicaciones requieren que el usuario acepte los términos de licencia  
 Cuando los filtros de escritura se deshabilitan para que Configuration Manager pueda instalar software en dispositivos incrustados, los usuarios con derechos reducidos no pueden iniciar sesión en esos dispositivos. Si la instalación requiere que el usuario acepte los términos de licencia, esto no será posible y la instalación producirá un error. Asegúrese de no implementar software para dispositivos de Windows Embedded si la instalación requiere la interacción del usuario. Puede usar la lista Plataformas aplicables para filtrar estos sistemas operativos.  



<!--HONumber=Nov16_HO1-->


