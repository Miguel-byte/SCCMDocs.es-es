---
title: Notas de la versión de MDT
description: Conozca las plataformas compatibles, los requisitos previos y las limitaciones de Microsoft Deployment Toolkit.
ms.date: 06/04/2018
ms.prod: configuration-manager
ms.technology:
- configmgr-osd
ms.topic: article
ms.assetid: 6e32ce6d-585d-4801-a345-ff0f6f2d90ad
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7cb287a17322af8069708268a18d638bd04dddcf
ms.sourcegitcommit: 10b3a571e2a822bbd7b58a25840ee1e6f703a7a2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/06/2018
ms.locfileid: "34814287"
---
# <a name="microsoft-deployment-toolkit-release-notes"></a>Notas de la versión de Microsoft Deployment Toolkit  

En este artículo se proporciona información sobre la versión más reciente de Microsoft Deployment Toolkit (MDT). La información incluye las plataformas admitidas, los requisitos previos y las limitaciones. Se da por supuesto que está familiarizado con los conceptos, las características y las capacidades de la versión de MDT.



## <a name="latest-release"></a>Versión más reciente

**MDT compilación 8450** es la versión más reciente disponible en el [Centro de descarga de Microsoft](https://aka.ms/mdtdownload). 

Esta actualización comienza la compatibilidad con Windows Assessment and Deployment Kit (ADK) para Windows 10, versión 1709. 

***Actualización***: a partir de mayo de 2018, esta compilación también es compatible con Windows 10, versión 1803.

Para obtener más información, consulte la sección de [plataformas compatibles](#supported-platforms).


### <a name="significant-changes"></a>Cambios importantes
Este es un resumen de los cambios importantes incluidos en esta compilación de MDT.

#### <a name="supported-configuration-updates"></a>Actualizaciones de configuración admitidas
- Windows ADK para Windows 10, versión 1709
- Windows 10, versión 1709
- Configuration Manager, versión 1710

#### <a name="quality-updates"></a>Actualizaciones de calidad
Estos son los títulos de los errores corregidos en esta versión:
- Las dependencias y la licencia de la aplicación instalada como prueba de Win10 no se han instalado.
- La secuencia de tareas CaptureOnly no permite capturar una imagen.
- Error recibido al iniciar una secuencia de tareas de MDT: se especificó un valor de DeploymentType "" no válido. La implementación no continuará.
- ZTIMoveStateStore busca la carpeta de almacenamiento del estado en la ubicación incorrecta, por lo que no puede moverla.
- xml contiene un error de escritura simple que produjo un comportamiento no deseado.
- Instalar Roles y características no funciona para la característica Consola de administración de IIS de Windows Server 2016.
- Exploración de imágenes del sistema operativo en la secuencia de tareas de actualización no funciona al usar carpetas.
- La herramienta de MDT aprovisiona incorrectamente el TPM en un estado de funcionalidad reducida. Para obtener más información, consulte [KB 4018657](https://support.microsoft.com/help/4018657/tpm-is-in-reduced-functionality-mode-after-successful-deployment-of-wi).
- Actualizaciones en la lógica de detección de tipos de chasis ZTIGather.
- El paso de actualización de sistema operativo omite SetupComplete.cmd, lo que interrumpe las implementaciones futuras.
- Problema de arranque de UEFI en Windows 10 ADK 1607 y versiones posteriores en algunos tipos de hardware.
- Incluye los archivos binarios actualizados de secuencia de tareas de Configuration Manager.



## <a name="supported-platforms"></a>Plataformas admitidas

Las versiones de MDT ya no se etiquetan con la versión de actualización o el año. Para adaptarse mejor a las ramas de Windows 10 y Configuration Manager, así como para simplificar la personalización de marca y el proceso de publicación, ahora se denomina simplemente **Microsoft Deployment Toolkit**. El número de compilación se utiliza para distinguir las versiones. Por ejemplo, la compilación más reciente disponible para descargar es la 8450.

A diferencia de Configuration Manager, que cuenta con una programación de publicación de versiones predeterminada, MDT solo publica compilaciones según sea necesario para admitir las nuevas versiones de Windows 10, Windows ADK o la rama actual de Configuration Manager. Todos los problemas conocidos con estos componentes se documentarán en este artículo según sea necesario.

Estas son las versiones de sistema operativo que pueden implementarse con MDT:
- Windows 10, versión 1803
- Windows 10, versión 1709
- Otras [versiones compatibles](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet) de Windows 10
- Windows 8.1
- Windows 7
- Windows Server 2016
- Windows Server 2012 R2
- Windows Server 2012
- Windows Server 2008 R2



## <a name="prerequisites"></a>Requisitos previos

MDT requiere los siguientes componentes, que están incluidos en Windows:
- Microsoft .NET Framework 4.0
- Windows PowerShell versión 3.0

Use la versión más reciente de [Windows ADK para Windows 10](https://docs.microsoft.com/windows-hardware/get-started/adk-install). 

> [!Note]  
> Windows recomienda el uso de la versión de Windows ADK que coincida con la de Windows que va a implementar. Por ejemplo, use la versión 1703 de Windows ADK para Windows 10 al implementar Windows 10 versión 1703. Para obtener más información sobre la compatibilidad del componente Windows ADK, consulte [DISM supported platforms](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-supported-platforms) (Plataformas compatibles con DISM) y [USMT requirements](https://docs.microsoft.com/windows/deployment/usmt/usmt-requirements#bkmk-1) (Requisitos de USMT).

Al integrar MDT con Configuration Manager en escenarios de ZTI y UDI, utilice la versión más reciente de la rama actual de Configuration Manager.



## <a name="upgrading-mdt"></a>Actualización de MDT

El proceso de instalación de MDT quita las instancias existentes de MDT que haya instaladas en el mismo equipo. Los recursos compartidos de implementación, los puntos de distribución y las bases de datos existentes se conservan durante este proceso. Deberán actualizarse una vez que se haya completado la instalación.

Es posible actualizar a la versión actual de MDT desde las siguientes versiones de MDT:
- MDT, compilación 8443

> [!Tip]  
> Crear una copia de seguridad de la infraestructura existente de MDT antes de intentar una actualización.

### <a name="lti"></a>LTI
Después de instalar MDT, actualizar un recurso compartido de implementación existente mediante la ejecución de la **el Asistente para abrir compartir implementación** desde el nodo de recursos compartidos de implementación de Deployment Workbench. Especifique la ruta de acceso del directorio del recurso compartido de implementación existente y, a continuación, active la casilla **Actualizar**. Este proceso también actualiza los recursos compartidos de implementación de red existentes y los recursos compartidos de implementación de medios, por lo que debería poder accederse a esos recursos compartidos. No lleve a cabo esta actualización si está realizando implementaciones, dado que los archivos en uso pueden causar problemas en la actualización.

### <a name="zti"></a>ZTI
Las secuencias de tareas de MDT presentes en Configuration Manager no se modifican durante el proceso de instalación de MDT. Deberían seguir funcionando sin ningún problema. No se proporciona ningún mecanismo para actualizar estas secuencias de tareas. Si quiere utilizar cualquiera de las nuevas capacidades de MDT, cree nuevas secuencias de tareas integradas de MDT en Configuration Manager.

Cuando el proceso de actualización se haya completado:  

- Ejecute el asistente de configuración de la integración de ConfigMgr (**Configure ConfigMgr Integration**) después de la actualización. El asistente registra los componentes nuevos e instala las plantillas de secuencia de tareas de ZTI actualizadas.  

- Cree un paquete nuevo de **archivos de Microsoft Deployment Toolkit** para las nuevas secuencias de tareas ZTI que cree. Puede usar el paquete Microsoft Deployment Toolkit Files existente para las secuencias de tareas ZTI creadas antes de la actualización, pero deberá crear otro paquete para las nuevas secuencias de tareas ZTI.



<!--
## Known issues
-->



## <a name="frequently-asked-questions"></a>Preguntas más frecuentes

#### <a name="whats-the-mdt-support-life-cycle"></a>¿Qué es el ciclo de vida de soporte técnico de MDT?  
Para obtener información, consulte [Ciclo de vida de soporte técnico de Microsoft Deployment Toolkit](https://support.microsoft.com/help/2872000/microsoft-deployment-toolkit-support-life-cycle).

#### <a name="is-this-release-only-supported-with-windows-10-windows-adk-or-configuration-manager-version-x"></a>¿Esta versión se admite solo con Windows 10, Windows ADK o Configuration Manager versión *X*?
Hemos probado principalmente esta compilación de MDT con la configuración mencionada anteriormente. A menos que haya problemas conocidos explícitos, cualquier otra configuración distinta de la anterior también tiene una alta probabilidad de funcionar. El resultado puede variar dado que no hemos probado de manera explícita otras combinaciones.

#### <a name="how-do-i-get-help-with-mdt"></a>¿Cómo se puede obtener ayuda con MDT?
Utilice uno de los métodos siguientes para obtener ayuda con MDT (por orden de prioridad):

1. Publicar en el [foro de MDT](https://social.technet.microsoft.com/Forums/en/home?forum=mdt). Los MVP y otros usuarios de la comunidad revisan las entradas que se publican y responden a ellas. Probablemente sea la manera más eficaz de obtener ayuda.
2. Ponerse en contacto con el Soporte técnico de Microsoft. Abra un caso de soporte técnico y obtenga ayuda profesional.
3. Si puede reproducir constantemente un problema y cree que se trata de un error del producto, notifíquelo en el [centro de opiniones](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app) de Windows 10. El equipo del producto investiga todo lo que se notifica. Use la categoría **Administración empresarial** y la subcategoría **Implementación de sistema operativo** al enviar los comentarios. Esta categorización ayuda a clasificar y dirigir sus comentarios al equipo de MDT.
     - El centro de opiniones también se puede utilizar para enviar sugerencias (solicitudes de cambio de diseño o DCR) sobre el producto.
     - Si previamente ha registrado los comentarios a través de Connect, no es necesario vuelva a hacerlo en el centro de opiniones.