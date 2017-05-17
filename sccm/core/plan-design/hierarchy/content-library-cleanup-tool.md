---
title: Content Library Cleanup Tool | Microsoft Docs
description: "Utilice Content Library Cleanup Tool para quitar contenido huérfano que ya no está asociado con una implementación de System Center Configuration Manager."
ms.custom: na
ms.date: 4/7/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 226cbbb2-9afa-4e2e-a472-be989c0f0e11
caps.latest.revision: 4
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 32f7fc4ef9c8e8d3c2ec8eeaf9a3174bad992ffb
ms.openlocfilehash: 76e6772bdd5cbd32d525e728f6ebc988b045da78
ms.contentlocale: es-es
ms.lasthandoff: 05/17/2017

---
# <a name="the-content-library-cleanup-tool-for-system-center-configuration-manager"></a>Content Library Cleanup Tool para System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

 A partir de la versión 1702, puede usar una herramienta de línea de comandos (**ContentLibraryCleanup.exe**) para quitar contenido que ya no está asociado con ningún paquete o aplicación de un punto de distribución (contenido huérfano). Esta herramienta se denomina Content Library Cleanup Tool y sustituye a las versiones anteriores de herramientas similares publicadas para productos anteriores de Configuration Manager.  

La herramienta solo afecta al contenido del punto de distribución que especifique al ejecutar la herramienta. La herramienta no puede quitar el contenido de la biblioteca de contenido en el servidor de sitio.

Puede encontrar **ContentLibraryCleanup.exe** en la carpeta *%CM_Installation_Path%\cd.latest\SMSSETUP\TOOLS\ContentLibraryCleanup\* del servidor de sitio de un sitio primario o de un sitio de administración central.

## <a name="requirements"></a>Requisitos  
 La herramienta solo puede ejecutarse en un único punto de distribución a la vez.  
 - Puede ejecutarse directamente en el equipo que hospeda el punto de distribución que desea limpiar o de manera remota desde otro servidor.
 - La cuenta de usuario que ejecuta la herramienta debe tener directamente los permisos de administración basada en roles que son iguales a los de Administrador total en la jerarquía de Configuration Manager. La herramienta no funciona cuando la cuenta de usuario recibe permisos como un miembro de un grupo de seguridad de Windows que tiene los permisos de Administrador total.

## <a name="modes-of-operation"></a>Modos de operación
Puede ejecutar la herramienta en los dos modos siguientes. Se recomienda ejecutar la herramienta en el modo *What-If*, para que pueda revisar los resultados antes de ejecutar la herramienta en el *modo de eliminación*:
  1.    **Modo de hipótesis**:   
      Si no especifica el modificador **/delete**, la herramienta se ejecuta en el modo de hipótesis e identifica el contenido que se eliminaría del punto de distribución.
   - Cuando se ejecuta en este modo, la herramienta no elimina ningún dato.
   - La información sobre el contenido que se eliminaría se escribe en el archivo de registro de herramientas y no se le pide que confirme cada eliminación posible.  
      </br>   

  2. **Modo de eliminación**:   
    Cuando ejecuta la herramienta con el modificador **/delete**, la herramienta se ejecuta en el modo de eliminación.

     - Cuando se ejecuta en este modo, el contenido huérfano que se ha detectado en el punto de distribución especificado puede eliminarse de la biblioteca de contenido del punto de distribución.
     -     Antes de eliminar cada archivo, debe confirmar que el archivo debe eliminarse.  Puede seleccionar **S** para sí, **N** para no o **Sí a todo** para omitir mensajes adicionales y eliminar todo el contenido huérfano.  
     </br>

Cuando la herramienta se ejecuta en cualquier modo, crea automáticamente un registro con un nombre que incluye el modo en el que se ejecuta la herramienta, el nombre del punto de distribución, la fecha y la hora de la operación. El archivo de registro se abre automáticamente cuando finaliza la herramienta.

De forma predeterminada, el archivo de registro se escribe en la carpeta temporal de la cuenta de usuario que ejecuta la herramienta en el equipo donde se ejecuta la herramienta. Puede usar el modificador **/log** para remitir el archivo de registro a otra ubicación, incluido un recurso compartido de red.


## <a name="run-the-tool"></a>Ejecutar la herramienta
Para ejecutar la herramienta:
1. Abra un símbolo del sistema administrativo en una carpeta que contenga **ContentLibraryCleanup.exe**.  
2. Después, escriba una línea de comandos que incluya los modificadores de línea de comandos necesarios y modificadores opcionales que quiera usar.

**Problema conocido** Cuando se ejecuta la herramienta, se podría devolver un error similar al siguiente cuando se produce cualquier error en algún paquete o implementación, o bien cuando está en progreso:
-  *System.InvalidOperationException: esta biblioteca de contenido no puede limpiarse ahora porque el paquete <packageID> no está totalmente instalado.*

**Solución:** ninguna. La herramienta no puede identificar archivos huérfanos con confianza cuando la implementación del contenido está en curso o si se ha producido algún error en dicho proceso. Por lo tanto, la herramienta no le permitirá limpiar contenido hasta que se solucione el problema.

### <a name="command-line-switches"></a>Modificadores de línea de comandos  
Los siguientes modificadores de línea de comandos se pueden usar en cualquier orden.   

|Modificador|Detalles|
|---------|-------|
|**/delete**  |**Opcional** </br> Use este modificador cuando quiera eliminar contenido del punto de distribución. Se le preguntará antes de que se elimine el contenido. </br></br> Cuando este modificador no se usa, la herramienta registra los resultados del contenido que se habría eliminado, pero no elimina contenido del punto de distribución. </br></br> Ejemplo: ***ContentLibraryCleanup.exe /dp server1.contoso.com /delete*** |
| **/q**       |**Opcional** </br> Este modificador ejecuta la herramienta en el modo silencioso que suprime todos los mensajes (como los avisos cuando está eliminando contenido) y no abre automáticamente el archivo de registro. </br></br> Ejemplo: ***ContentLibraryCleanup.exe /q /dp server1.contoso.com*** |
| **/dp &lt;FQDN del punto de distribución>**  | **Requerido** </br> Especifique el nombre de dominio completo (FQDN) del punto de distribución que quiere limpiar. </br></br> Ejemplo: ***ContentLibraryCleanup.exe /dp server1.contoso.com***|
| **/ps &lt;FQDN del sitio primario>**       | **Opcional** al limpiar contenido de un punto de distribución en un sitio primario.</br>**Requerido** al limpiar contenido de un punto de distribución en un sitio secundario. </br></br>La herramienta se conecta al sitio primario principal para ejecutar consultas en SMS_Provider. Estas consultas permiten a la herramienta determinar qué contenido debe estar en el punto de distribución, de modo que pueda identificar el contenido huérfano que se puede quitar. Esta conexión con el sitio primario principal debe realizarse para los puntos de distribución de un sitio secundario, ya que los detalles necesarios no están disponibles directamente en el sitio secundario.</br></br> Especifique el FQDN del sitio primario al que pertenece el punto de distribución, o del primario principal cuando el punto de distribución se encuentra en un sitio secundario. </br></br> Ejemplo: ***ContentLibraryCleanup.exe /dp server1.contoso.com /ps siteserver1.contoso.com*** |
| **/sc &lt;código del sitio primario>**  | **Opcional** al limpiar contenido de un punto de distribución en un sitio primario.</br>**Requerido** al limpiar contenido de un punto de distribución en un sitio secundario. </br></br> Especifique el código del sitio del sitio primario al que pertenece el punto de distribución, o del sitio primario principal cuando el punto de distribución se encuentra en un sitio secundario.</br></br> Ejemplo: ***ContentLibraryCleanup.exe /dp server1.contoso.com /sc ABC*** |
| **/log <log file directory>**       |**Opcional** </br> Especifique la ubicación donde la herramienta escribe el archivo de registro. Puede ser una unidad local o un recurso compartido de red.</br></br> Cuando no se usa este modificador, el archivo de registro se coloca en la carpeta temporal del usuario, en el equipo donde se ejecuta la herramienta.</br></br> Ejemplo de unidad local: ***ContentLibraryCleanup.exe /dp server1.contoso.com /log C:\Users\Administrator\Desktop*** </br></br>Ejemplo de recurso compartido de red: ***ContentLibraryCleanup.exe /dp server1.contoso.com /log \\&lt;recurso compartido>\&lt;carpeta>***|

