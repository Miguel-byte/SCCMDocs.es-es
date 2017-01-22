---
title: "Introducción a la configuración de cumplimiento | Microsoft Docs"
description: "Obtenga información sobre cómo funciona la configuración de cumplimiento en System Center Configuration Manager. Además, obtenga información sobre los conceptos principales que necesita conocer."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: a2742d52-851e-4abc-b623-d12d91684c0b
caps.latest.revision: 11
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: f9e939d871e95a3248d8e5d96cb73063a81fd5cf
ms.openlocfilehash: f16c87dfd0c4f80d96aedf7f5f7497f2bbd4752a


---
# <a name="get-started-with-compliance-settings-in-system-center-configuration-manager"></a>Introducción a la configuración de cumplimiento en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Antes de empezar a crear elementos de configuración de System Center Configuration Manager, debe revisar este tema para entender cómo funciona la configuración de cumplimiento y para obtener información sobre los conceptos principales que debe conocer.  

## <a name="how-compliance-settings-works"></a>Funcionamiento de la configuración de cumplimiento  
 La configuración de cumplimiento le permite administrar la configuración y el cumplimiento de servidores, portátiles, equipos de escritorio y dispositivos móviles en su organización.  

 Los elementos de configuración se clasifican en dos categorías principales:  

-   **Configuración para dispositivos administrados con el cliente de Configuration Manager**: suelen ser dispositivos en los que ha instalado software de cliente de Configuration Manager para permitirle administrar el dispositivo.  

-   **Configuración para dispositivos administrados sin el cliente de Configuration Manager**: suelen ser dispositivos administrados con Microsoft Intune o con la administración de dispositivo local de Configuration Manager.  

## <a name="what-devices-are-supported"></a>¿Qué dispositivos son compatibles?  


|Tipo de dispositivo|Más información|  
|------------|----------------------|  
|Equipos con Windows (con el cliente de Configuration Manager)|Permite crear elementos de configuración personalizados que permiten evaluar elementos como las claves del registro, los archivos y los atributos de Active Directory.<br /><br /> Si se usa el tipo de elemento de configuración de Windows 10, las opciones deseadas se seleccionan de una lista predefinida.|  
|Equipos con Windows (inscritos con Microsoft Intune)|Seleccione la configuración que quiera de una lista predefinida.|  
|Dispositivos iOS (inscritos con Microsoft Intune)|Seleccione la configuración que quiera de una lista predefinida.|  
|Dispositivos Android (inscritos con Microsoft Intune)|Seleccione la configuración que quiera de una lista predefinida.|  
|Dispositivos Windows Phone (inscritos con Microsoft Intune)|Seleccione la configuración que quiera de una lista predefinida.|  
|Equipos Mac (con el cliente de Configuration Manager)|Permite crear elementos de configuración personalizados que facilitan la evaluación de elementos como los valores de las preferencias de Mac OS X (lista de propiedades) y los resultados devueltos por un script.|  
|Equipos Mac (inscritos con Microsoft Intune)|Seleccione la configuración que quiera de una lista predefinida.|  

## <a name="what-is-a-configuration-item"></a>¿Qué es un elemento de configuración?  
 Un elemento de configuración puede considerarse un contenedor que almacena la información siguiente (la información que se configure dependerá del tipo de elemento de configuración):  

-   **Información de método de detección** (para elementos de configuración de Windows que solo contienen la configuración de la aplicación): permite detectar si una aplicación está instalada mediante la detección del archivo del programa de instalación de Windows para la aplicación o mediante un script personalizado.  

-   **Configuración** : representa las condiciones técnicas o de negocio que se usan para evaluar el cumplimiento en dispositivos cliente. Puede configurar una nueva configuración o ir a una configuración existente en un equipo de referencia.  

-   **Reglas de compatibilidad** : especifican las condiciones que definen el cumplimiento del valor de un elemento de configuración. Para poder evaluar el cumplimiento de una configuración, debe tener al menos una regla de cumplimiento. Algunas configuración permiten corregir los valores que no son conformes. Puede crear nuevas reglas o buscar una configuración existente en cualquier elemento de configuración para seleccionar sus reglas.  

-   **Plataformas admitidas** : son las plataformas de dispositivo que define en las que se evaluará el elemento de configuración para determinar su cumplimiento. Si implementa un elemento de configuración en un dispositivo que no está en la lista de plataformas admitidas, no se evaluará su cumplimiento.  

## <a name="what-is-a-configuration-baseline"></a>¿Qué es una línea base de configuración?  
 El cumplimiento se evalúa mediante la definición de una línea base de configuración que contiene los elementos de configuración que quiere evaluar, y las configuraciones y reglas que describen el nivel de cumplimiento que debe tener. Puede importar estos datos de configuración desde el sitio web en paquetes de configuración de Microsoft System Center Configuration Manager como procedimientos recomendados que se definen por Microsoft y otros proveedores en Configuration Manager y, después, importarlos a Configuration Manager. O bien, puede crear elementos de configuración y líneas base de configuración.  

 Después de definir una línea base de configuración, puede implementarla para usuarios y dispositivos a través de las recopilaciones y evaluar su configuración de cumplimiento en una programación. Los dispositivos pueden tener varias líneas base de configuración implementados. Esto le proporciona un alto nivel de control.  

 Los dispositivos cliente evalúan su cumplimiento con cada línea base de configuración implementadas y notifican inmediatamente los resultados al sitio mediante mensajes de estado. Si un dispositivo cliente no está conectado actualmente a la red, pero descargó los elementos de configuración a los que se hace referencia en una línea base de configuración implementada, se evaluará la compatibilidad de la línea base de configuración. La información de cumplimiento se envía cuando se vuelve a establecer la conexión.  

 Puede supervisar los resultados de la evaluación de cumplimiento de la línea base de configuración desde el nodo **Implementaciones** del área de trabajo **Supervisión** en la consola de Configuration Manager para ver las causas más comunes de incumplimiento, los errores y el número de usuarios y dispositivos afectados. También puede ejecutar informes de configuración de cumplimiento para conocer los detalles adicionales, como los dispositivos conformes o no conformes, y el elemento de la línea base de configuración que provoca el incumplimiento de un equipo. También puede ver los resultados de la evaluación de cumplimiento desde equipos Windows que ejecuten el software de cliente de Configuration Manager mediante la pestaña **Configuraciones** en **Configuration Manager** en el Panel de control.  

## <a name="user-data-and-profiles-configuration-items"></a>Elementos de configuración de perfiles y datos de usuario  
 Los elementos de configuración de perfiles y datos de usuario contienen opciones para controlar cómo los usuarios de la jerarquía administran el redireccionamiento de carpetas, los archivos sin conexión y los perfiles móviles en equipos que ejecutan Windows 8 y versiones posteriores. Puede implementarlos en recopilaciones de usuarios y, después, supervisar su cumplimiento desde el nodo **Supervisión** de la consola de Configuration Manager. A diferencia de otros elementos de configuración, estos no se agregan a las líneas base de configuración antes de implementarlos. Se pueden implementar directamente con el cuadro de diálogo **Implementar elemento de configuración de perfiles y datos de usuario** .  

 Para obtener más información, consulte [Create user data and profiles configuration items (Crear elementos de configuración de perfiles y datos de usuario)](/sccm/compliance/deploy-use/create-user-data-and-profiles-configuration-items).  

## <a name="remote-connection-profiles"></a>Perfiles de conexión remota  
 Los perfiles de conexión remota proporcionan un conjunto de herramientas y recursos para ayudarle a crear, implementar y supervisar la configuración de conexión remota en dispositivos de su organización. Mediante la implementación de estas opciones, se minimiza la intervención del usuario final para conectarse a sus equipos en la red corporativa.  

Para obtener más información, consulte [Create remote connection profiles (Crear perfiles de conexión remota)](/sccm/compliance/deploy-use/create-remote-connection-profiles).  

## <a name="windows-edition-upgrade"></a>Actualización de edición de Windows
La directiva de actualización de edición le permite actualizar dispositivos automáticamente que ejecutan determinadas versiones de Windows 10 a una versión más reciente proporcionando una nueva clave de producto o archivo de licencia.

Para obtener más información, consulte [Upgrade Windows devices with the edition upgrade policy (Actualizar dispositivos de Windows con la directiva de actualización de edición)](/sccm/compliance/deploy-use/upgrade-windows-version).



<!--HONumber=Dec16_HO3-->


