---
title: "Introducción a la administración de aplicaciones | Microsoft Docs"
description: "Obtenga la información básica que necesitará para administrar e implementar las aplicaciones de System Center Configuration Manager."
ms.custom: na
ms.date: 12/23/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 08f711ba-83bf-4b5f-9520-a0778c6ae7eb
caps.latest.revision: 18
author: robstackmsft
ms.author: robstack
manager: angrobe
experimental: true
experiment_id: rob-table-161101
translationtype: Human Translation
ms.sourcegitcommit: 5aef08865b232ff2dacec6906098bebf4e42e6b1
ms.openlocfilehash: 699adb5fac0c625c321db011af6989cc4c0778ec


---
# <a name="introduction-to-application-management-in-system-center-configuration-manager"></a>Introducción a la administración de aplicaciones en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

En este tema, aprenderá los conceptos básicos que necesita saber antes de empezar a trabajar con aplicaciones de System Center Configuration Manager.  

> [!TIP]  
>  Si ya está familiarizado con la administración de aplicaciones en Configuration Manager, puede omitir este tema y pasar a la creación de una aplicación de ejemplo. Consulte [Crear e implementar una aplicación con System Center Configuration Manager](../../apps/get-started/create-and-deploy-an-application.md).  

## <a name="what-is-an-application"></a>¿Qué es una aplicación?  
 Aunque el término *aplicación* es un término ampliamente usado en informática, en Configuration Manager, significa algo distinto. Piense en una aplicación como en una caja. Dicha caja contiene uno o varios conjuntos de archivos de instalación de un paquete de software (conocidos como **tipo de implementación**) más instrucciones acerca de la implementación del software.  

 Cuando la aplicación se implementa en dispositivos, los **requisitos** deciden qué tipo de implementación se instala en el dispositivo.  

 Por supuesto, hay muchas más cosas que puede hacer con una aplicación y obtendrá información sobre estas a medida que lea esta guía. La tabla siguiente presenta algunos conceptos que debe saber antes de empezar a investigar un poco más. No necesitará todos estos conceptos en cada aplicación que cree:  

|Concepto|Descripción|    
|-|-|  
|**Requirements**|En versiones anteriores de Configuration Manager, a menudo se creaba una recopilación que contenía los dispositivos que quería implementar en una aplicación. Aunque es posible crear dicha recopilación, los requisitos hacen que no sea tan necesaria su creación, ya que permiten especificar criterios mucho más granulares para la instalación de una aplicación.<br /><br /> Por ejemplo, puede especificar que una aplicación se instale solo en dispositivos que ejecutan Windows 10. A continuación, puede implementar la aplicación en todos los dispositivos, pero solo se instalará en los dispositivos que ejecuten Windows 10.<br /><br /> Configuration Manager evalúa los requisitos para determinar si se instalará una aplicación y cualquiera de sus tipos de implementación. A continuación, determina el tipo de implementación correcto mediante el que debe instalarse una aplicación. Cada siete días, de forma predeterminada, las reglas de requisitos se vuelven a evaluar para garantizar su cumplimiento conforme a la configuración de cliente **Programar la reevaluación para implementaciones**.<br /><br /> Para obtener más información, consulte [Crear e implementar una aplicación](../../apps/get-started/create-and-deploy-an-application.md).|  
|**Condiciones globales**|Cuando se utilicen los requisitos con un tipo de implementación específico en una única aplicación, también podrá crear condiciones globales. Son una biblioteca de requisitos predefinidos que puede usar con cualquier aplicación y tipo de implementación.<br /><br /> Configuration Manager contiene un conjunto de condiciones globales integradas y también permite crear las suyas propias.<br /><br /> Para obtener más información, consulte [Crear condiciones globales](../../apps/deploy-use/create-global-conditions.md).|  
|**Implementación simulada**|Evalúa los requisitos, el método de detección y las dependencias de una aplicación. Informa de los resultados sin instalar realmente la aplicación.<br /><br /> Para obtener más información, consulte [Simular implementaciones de aplicaciones](../../apps/deploy-use/simulate-application-deployments.md).|  
|**Acción de implementación**|Especifica si desea instalar o desinstalar (si se admite) la aplicación que se va a implementar.<br /><br /> Para obtener más información, consulte [Implementar aplicaciones](../../apps/deploy-use/deploy-applications.md).|  
|**Propósito de implementación**|Especifica si la aplicación de la implementación tendrá el estado **Requerido**o **Disponible**.<br /><br /> **Requerido** significa que la aplicación se implementa automáticamente según la programación configurada. Sin embargo, un usuario puede realizar un seguimiento del estado de la implementación de la aplicación si no está oculto y puede instalar la aplicación antes de la fecha límite mediante el Centro de software.<br /><br /> **Disponible** significa que si la aplicación se implementa en un usuario, este la verá en el Centro de software y la podrá solicitar a petición.<br /><br /> Para obtener más información, consulte [Implementar aplicaciones](../../apps/deploy-use/deploy-applications.md).|  
|**Revisiones**|Si se hacen revisiones en una aplicación o en un tipo de implementación contenido en una aplicación, Configuration Manager crea una versión nueva de la aplicación. También puede ver el historial de cada revisión de aplicación, ver sus propiedades, restaurar una versión anterior de una aplicación o eliminar una versión anterior.<br /><br /> Para obtener más información, consulte [Actualizar y retirar aplicaciones](../../apps/deploy-use/update-and-retire-applications.md).|  
|**Método de detección**|Los métodos de detección se usan para detectar si ya está instalada una aplicación implementada. Si el método de detección indica que la aplicación está instalada, Configuration Manager no intenta instalarla de nuevo.<br /><br /> Para obtener más información, consulte [Crear aplicaciones](../../apps/deploy-use/create-applications.md).|  
|**Dependencias**|Las dependencias definen uno o más tipos de implementación de otra aplicación que se deben instalar antes de que se instale un tipo de implementación. Puede configurar los tipos de implementación dependientes para que se instalen automáticamente antes de la instalación de un determinado tipo de implementación.<br /><br /> Para obtener más información, consulte [Crear aplicaciones](../../apps/deploy-use/create-applications.md).|  
|**Sustitución**|Configuration Manager le permite actualizar o reemplazar las aplicaciones existentes mediante una relación de sustitución. Cuando se sustituye una aplicación, puede especificar un nuevo tipo de implementación para reemplazar el tipo de implementación de la aplicación sustituida. También puede decidir si desea actualizar o desinstalar la aplicación sustituida antes de que se instale la aplicación sustituida.<br /><br /> Para obtener más información, consulte [Crear aplicaciones](../../apps/deploy-use/create-applications.md).|  
|**Administración centrada en el usuario**|Las aplicaciones de Configuration Manager admiten la administración centrada en el usuario, por lo que permiten asociar usuarios específicos con dispositivos concretos. En lugar de tener que recordar el nombre del dispositivo de un usuario, ahora puede implementar aplicaciones para el usuario y el dispositivo. Esta funcionalidad puede ayudarle a asegurarse de que las aplicaciones más importantes siempre estén disponible en todos los dispositivos a los que accede un usuario específico. Si un usuario adquiere un nuevo equipo, puede instalar automáticamente las aplicaciones del usuario en el dispositivo antes de que inicie sesión.<br /><br /> Para obtener información, consulte [Vincular usuarios y dispositivos con la afinidad entre usuario y dispositivo](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).|  

## <a name="what-application-types-can-you-deploy"></a>¿Qué tipos de aplicación puede implementar?  
 Configuration Manager le permite implementar los siguientes tipos de aplicaciones:  

- Windows Installer (archivo *.msi)
- Paquete de aplicación de Windows (*.appx, *.appxbundle)
- Paquete de aplicación de Windows (en la Tienda Windows)
- Microsoft Application Virtualization 4
- Microsoft Application Virtualization 5
- Archivo .CAB de Windows Mobile
- macOS  


Además, al administrar dispositivos a través de la administración de dispositivos locales de Microsoft Intune o Configuration Manager, puede administrar estos tipos de aplicación adicionales:

- Paquete de aplicación de Windows Phone (archivo *.xap)
- Paquete de aplicación iOS (archivo *.ipa)
- Paquete de aplicación de Android (archivo *.apk)
- Paquete de aplicación para Android en Google Play
- Paquete de aplicación de Windows Phone (en la Tienda Windows Phone)
- Windows Installer a través de MDM
- Aplicación web



## <a name="state-based-applications"></a>Aplicaciones basadas en estado  
 Las aplicaciones de Configuration Manager usan la supervisión basada en estado, lo cual permite hacer un seguimiento del último estado de implementación de aplicación para usuarios y dispositivos. Los mensajes de estado muestran información acerca de dispositivos individuales. Por ejemplo, si una aplicación se implementa en una recopilación de usuarios, puede ver el estado de cumplimiento de la implementación y el propósito de la implementación en la consola de Configuration Manager. Puede supervisar la implementación de todo el software mediante el área de trabajo **Supervisión** en la consola de Configuration Manager. Las implementaciones de software incluyen actualizaciones de software, configuración de cumplimiento, aplicaciones, secuencias de tareas, y paquetes y programas. Para obtener más información, consulte [Supervisión de aplicaciones](/sccm/apps/deploy-use/monitor-applications-from-the-console).  

 Configuration Manager vuelve a evaluar las implementaciones de aplicaciones con determinada frecuencia. Por ejemplo:  

-   El usuario final desinstala una aplicación implementada. En el siguiente ciclo de evaluación, Configuration Manager detecta que la aplicación no está presente y vuelve a instalarla.  

-   Una aplicación no se instaló en un dispositivo porque no cumple los requisitos. Posteriormente, se realiza un cambio en el dispositivo y cumple los requisitos. Configuration Manager detecta este cambio y la aplicación se instala.  


 Puede establecer la configuración de cliente **Programar reevaluación de implementaciones** para configurar el intervalo de reevaluación de las implementaciones de aplicaciones. Para más información, vea [Acerca de la configuración de cliente](../../core/clients/deploy/about-client-settings.md).  

## <a name="get-started-creating-an-application"></a>Empezar a crear una aplicación  
 Si quiere comenzar de inmediato a crear una aplicación, encontrará un tutorial para crear una aplicación sencilla en el tema [Crear e implementar una aplicación con System Center Configuration Manager](../../apps/get-started/create-and-deploy-an-application.md).  

 Si está familiarizado con los aspectos básicos y quiere obtener más información de referencia sobre las opciones disponibles, empiece por [Crear aplicaciones](/sccm/apps/deploy-use/create-applications).  

## <a name="software-center-and-the-application-catalog"></a>Centro de software y Catálogo de aplicaciones  
 En versiones anteriores de Configuration Manager, el Centro de software se usaba para instalar y programar las instalaciones de software, configurar las opciones de control remoto y configurar la administración de energía. Los usuarios podían conectarse al catálogo de aplicaciones para buscar y solicitar software, configurar algunas opciones de preferencia y borrar remotamente sus dispositivos móviles.  

 Aunque estas opciones siguen estando disponibles en System Center Configuration Manager, ahora hay una nueva versión del Centro de software disponible que permite buscar aplicaciones. No tiene que usar el catálogo de aplicaciones, que requiere un explorador web habilitado para Silverlight. Sin embargo, los roles de sistema de sitio de punto de sitios web del catálogo de aplicaciones y de punto de servicio web del catálogo de aplicaciones siguen siendo necesarios para que las aplicaciones disponibles para el usuario aparezcan en el Centro de software.  

 Para obtener más información, consulte [Planear y configurar la administración de aplicaciones en Configuration Manager](../../apps/plan-design/plan-for-and-configure-application-management.md).  

## <a name="configuration-manager-packages-and-programs"></a>Paquetes y programas de Configuration Manager  
 Configuration Manager mantiene la compatibilidad de los paquetes y programas usados en versiones anteriores del producto. Una implementación que utilice paquetes y programas podría ser más adecuada que una implementación que use una aplicación cuando se implementa algo de lo siguiente:  

-   Scripts que no instalan una aplicación en un equipo, como un script para desfragmentar la unidad de disco del equipo.  

-   Secuencias de comandos "Uso único" que no es necesario supervisar de forma constante.  

-   Scripts que se ejecutan según una programación periódica y no pueden usar evaluación global.

 Para obtener más información, consulte [Paquetes y programas](../../apps/deploy-use/packages-and-programs.md).  



<!--HONumber=Dec16_HO5-->


