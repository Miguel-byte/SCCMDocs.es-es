---
title: Policy Spy
titleSuffix: Configuration Manager
description: Use Policy Spy para ver y solucionar problemas del sistema de la directiva en los clientes de Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 1012ec24-27d9-4193-8236-918d283c7448
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 66a9949723e6555ddb72ebfdb845a523fb29bfe5
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/31/2018
ms.locfileid: "39385996"
---
# <a name="policy-spy"></a>Policy Spy

*Se aplica a: System Center Configuration Manager (Rama actual)*

Policy Spy es una de las [herramientas de Configuration Manager](/sccm/core/support/tools). Se trata de una herramienta para ver y solucionar problemas del sistema de la directiva en los clientes de Configuration Manager. Ejecute **PolicySpy.exe** para abrir la interfaz de usuario. Para más información sobre la utilización de la línea de comandos, vea [Sintaxis de línea de comandos](#bkmk_policyspy-syntax).

> [!Important]  
> Ejecute Policy Spy como administrador. Si no lo **ejecuta como administrador**, verá el siguiente error en la información de cliente:  
> `There is no client installed on this machine. Connection to client policy failed with error 80041003`


## <a name="bkmk_policyspy-syntax"></a> Sintaxis de línea de comandos

Policy Spy sirve principalmente para su uso a través de su interfaz de usuario. Ofrece opciones de línea de comandos limitadas que admiten la automatización y el procesamiento por lotes.

`PolicySpy.exe [/export <ExportFilename> [<computername>]]`

### <a name="option-export"></a>Opción: `/export`
Esta opción en modo silencioso exporta la directiva del equipo local o remoto. `<ExportFilename>` es el nombre de archivo con el que la herramienta guarda el archivo XML de la directiva exportada. Si se especifica la opción `<computername>`, Policy Spy exporta la directiva de ese equipo en lugar de la del equipo local.

> [!Note]  
> Esta opción de línea de comandos no ofrece una forma de especificar las credenciales de usuario. Para usar credenciales alternativas de acceso a un equipo remoto, use el comando **runas** para abrir un nuevo símbolo del sistema con las credenciales de seguridad necesarias.  


## <a name="usage"></a>Uso

### <a name="tools-menu"></a>Menú Herramientas

Las acciones siguientes están disponibles en el menú **Herramientas**:  

- **Open Remote**(Abrir remoto): se conecta a la directiva de cliente de Configuration Manager en un equipo remoto. Utilice el cuadro de diálogo Conectar para recuperar el nombre del equipo remoto y las credenciales de usuario opcionales. Si la conexión no se establece, muestra información de error en el panel de información del cliente. Si el error de conexión persiste, intente conectarse seleccionando **Actualizar** en el menú **Edición** o presionando F5.  

- **Abrir archivo**: abre un archivo de exportación de directiva (XML) creado por la opción **Exportar directiva**. La herramienta muestra la directiva exportada exactamente igual que una directiva activa. Deshabilita algunas características que solo se aplican al conectarse a un cliente real.  

- **Request Machine Assignments** (Solicitar asignaciones de máquina): desencadena una solicitud de asignaciones de directiva de equipo en el equipo de destino. Esta característica se deshabilita al visualizar una directiva exportada.  

- **Evaluate Machine Policy** (Evaluar la directiva de equipo): desencadena la evaluación de una directiva de equipo en el equipo de destino. Esta característica se deshabilita al visualizar una directiva exportada.  

- **Request User Assignments** (Solicitar asignaciones de usuario): desencadena una solicitud de asignaciones de directiva de usuario del usuario con sesión iniciada actualmente. Esta característica solo está disponible al visualizar una directiva en el equipo local.  

- **Evaluate User Policy** (Evaluar la directiva de usuario): desencadena la evaluación de una directiva de usuario para el usuario con sesión iniciada actualmente. Esta característica solo está disponible al visualizar una directiva en el equipo local.  

- **Reset Policy** (Restablecer directiva): quita todas las directivas no predeterminadas y restablece las cookies de la directiva para el sitio. Luego desencadena una solicitud de asignaciones de directiva de equipo. Esta característica se deshabilita al visualizar una directiva exportada.  

- **Exportar directiva**: exporta la directiva del equipo de destino a un archivo XML. Vea este archivo en cualquier equipo con Policy Spy. Para abrir el archivo de exportación, seleccione **Abrir archivo** en el menú **Herramientas**. Esta característica se deshabilita al visualizar una directiva exportada.  


### <a name="edit-menu"></a>Menú Edición

Las acciones siguientes están disponibles en el menú **Edición**:  

- **Eliminar**: elimina la instancia seleccionada en el panel de resultados. Esta acción solo se admite con instancias de la directiva. Si se intenta eliminar cualquier otra cosa que no sean instancias de la directiva, la herramienta muestra un mensaje de error. Esta característica se deshabilita al visualizar una directiva exportada.  

- **Actualizar**: actualiza todos los resultados para ver la información más reciente. Todos los nodos de árbol que estaban expandidos antes de actualizar se expanden automáticamente después. Si Policy Spy no se ha conectado correctamente a la directiva del equipo de destino, intenta conectarse de nuevo. Esta característica se deshabilita al visualizar una directiva exportada.  

- **Borrar eventos**: borra todos los elementos de la pestaña Eventos.  



## <a name="results-pane"></a>Panel Resultados

El panel de resultados muestra distintas vistas del sistema de la directiva en el equipo de destino. Obtenga acceso a estas vistas haciendo clic en una de las cuatro pestañas siguientes: 
- [Real](#bkmk_policyspy-actual)
- [Solicitado](#bkmk_policyspy-requested)
- [Predeterminado](#bkmk_policyspy-default)
- [Eventos](#bkmk_policyspy-events)


### <a name="bkmk_policyspy-actual"></a> Real

Esta pestaña muestra la directiva actual del cliente. La directiva actual determina el comportamiento de un cliente y el comportamiento de sus agentes de cliente, como distribución de software e inventario. La pestaña muestra los resultados en formato de árbol con un nodo raíz para el espacio de nombres de equipo y cada espacio de nombres específico del usuario. Expanda un nodo de espacio de nombres para mostrar una lista de clases. Expanda una clase para mostrar una lista de sus instancias. La lista de clases incluye solo las clases que tienen instancias.


### <a name="bkmk_policyspy-requested"></a> Solicitado

Esta pestaña muestra las asignaciones de directiva que el cliente recuperó del sitio asignado. La pestaña muestra los resultados en formato de árbol con un nodo raíz para el espacio de nombres de máquina y cada espacio de nombres específico del usuario. Al expandir un nodo de espacio de nombres, se muestran los nodos siguientes:  

- **Configuración**: muestra una lista de las clases de configuración derivadas de CCM_Policy_Config, que incluye el objeto de directiva, las asignaciones y otros elementos.  

- **Configuración**: muestra todos los ajustes activos generados por las directivas. Los ajustes se muestran en el nodo Configuración. 

> [!Note]   
> Pueden existir varias instancias con el mismo nombre porque el cliente no ha combinado estos ajustes en un conjunto resultante final. Policy Spy muestra instancias en este nodo mediante el uso de las propiedades RealKey en lugar de sus verdaderas claves de directiva. Correlacione estas instancias con el conjunto resultante que aparece en la pestaña Real.  


### <a name="bkmk_policyspy-default"></a> Predeterminado

Esta pestaña muestra la misma información que la pestaña **Solicitado**. También incluye contenido de los espacios de nombres DefaultMachine y DefaultUser.


### <a name="bkmk_policyspy-events"></a> Eventos

Esta pestaña muestra los eventos del agente de directiva cuando se producen. La vista crea una suscripción de eventos WMI de todos los eventos derivados de CCM_PolicyAgent_Event. La vista muestra un máximo de 200 eventos. Quita los eventos más antiguos de la parte superior de la lista según sea necesario. Si selecciona el último elemento en la lista, la lista se desplaza automáticamente hacia abajo a medida que se agregan nuevos eventos. En caso contrario, la vista conserva su posición actual y usted debe desplazarse hacia abajo o presionar la tecla Fin para ver los nuevos eventos. Esta vista siempre está vacía al ver una directiva exportada.



## <a name="client-info-pane"></a>Panel de información del cliente
El panel de información del cliente muestra una lista de propiedades del equipo de destino. Muestra las propiedades siguientes si están disponibles:  
- Nombre
- Id.
- Versión
- Sitio
- Punto de administración asignado
- Punto de administración residente
- Punto de administración de proxy
- Estado del proxy



## <a name="details-pane"></a>Panel de detalles
El panel de detalles muestra información detallada sobre la selección actual. Si no hay ninguna selección activa, muestra información sobre Policy Spy, incluida la versión. En caso contrario, muestra una representación del archivo Managed Object Format (MOF) del elemento seleccionado.

Policy Spy usa su propia rutina de generación del archivo MOF para crear una pantalla HTML más fácil de usar que el archivo MOF de texto sin formato generado por WMI. Este comportamiento permite que Policy Spy agregue las siguientes características para hacer más legible el archivo MOF:  

- Resaltado de sintaxis  

- Matrices y objetos con sangría  

- Las propiedades se organizan en grupos del sistema, heredados y locales. De manera predeterminada, contrae los grupos del sistema y heredados. Inmediatamente pueden verse las propiedades que realmente utiliza la instancia.  

- Copie el archivo MOF o el archivo MOF de texto sin formato en el Portapapeles. Esta característica resulta útil para pegar el archivo MOF en otras aplicaciones llamando directamente a la herramienta MofComp.  

En el caso de las instancias de objetos de directiva derivados de CCM_Policy_Policy, el panel de detalles muestra el cuerpo de la directiva después del archivo MOF que se muestra. Si el cliente no ha descargado el cuerpo de la directiva, Policy Spy muestra un hipervínculo. Haga clic en el vínculo para descargar el cuerpo de la directiva directamente desde el punto de administración del cliente. Si la herramienta descarga correctamente el cuerpo de la directiva, reemplaza el hipervínculo con el contenido de la respuesta. En caso contrario, Policy Spy actualiza la pantalla e indica un error en la solicitud.

