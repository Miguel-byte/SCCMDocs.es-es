---
title: Creación y ejecución de scripts
titleSuffix: Configuration Manager
description: Cree y ejecute scripts de Powershell en dispositivos cliente.
ms.date: 03/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: cc230ff4-7056-4339-a0a6-6a44cdbb2857
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 007c3b68932a673b5d1971fbcf6919a7ad3adc70
ms.sourcegitcommit: 6f4c2987debfba5d02ee67f6b461c1a988a3e201
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59802621"
---
# <a name="create-and-run-powershell-scripts-from-the-configuration-manager-console"></a>Creación y ejecución de scripts de PowerShell desde la consola de Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

<!--1236459-->
System Center Configuration Manager tiene una funcionalidad integrada para ejecutar scripts de Powershell. PowerShell tiene la ventaja de crear scripts automatizados y sofisticados que entienden y comparten una gran comunidad de usuarios. Los scripts simplifican la compilación de herramientas personalizadas para administrar software y posibilitan la realización de tareas rutinarias rápidamente, lo que permite obtener grandes resultados de forma más sencilla y coherente.  

> [!TIP]  
> Esta característica se introdujo por primera vez en la versión 1706 como una [característica de versión preliminar](/sccm/core/servers/manage/pre-release-features). A partir de la versión 1802, ya no es una característica de versión preliminar.  


> [!Note]  
> Configuration Manager no habilita esta característica opcional de forma predeterminada. Deberá habilitarla para poder usarla. Para obtener más información, consulte [Habilitar características opcionales de las actualizaciones](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  


Gracias a esta integración con System Center Configuration Manager, puede usar la funcionalidad *Ejecutar scripts* para hacer lo siguiente:

- Crear y editar scripts para usarlos con System Center Configuration Manager.
- Administrar el uso de los scripts a través de roles y ámbitos de seguridad. 
- Ejecutar scripts en recopilaciones o equipos Windows administrados locales
- Obtener resultados agregados y rápidos de scripts desde dispositivos cliente
- Supervisar la ejecución de scripts y ver los resultados de los informes desde la salida de los scripts

>[!WARNING]
>Dada la eficacia de los scripts, le recordamos que los utilice de forma intencionada y cautelosa. Hemos integrado medidas de seguridad adicionales para ayudarlo: los ámbitos y roles separados. Asegúrese de validar la precisión de los scripts antes de ejecutarlos y confirme que provienen de un origen de confianza, para así evitar que se ejecuten scripts involuntariamente. Tenga cuidado con los caracteres extendidos u otra ofuscación, e Infórmese sobre la protección de scripts. [Más información sobre la seguridad del script de PowerShell](/sccm/apps/deploy-use/learn-script-security)

## <a name="prerequisites"></a>Requisitos previos

- Para ejecutar los scripts de PowerShell, el cliente debe ejecutar la versión 3.0 o posterior de PowerShell. Sin embargo, si se ejecuta un script que contiene la funcionalidad de una versión posterior de PowerShell, el cliente en el que se ejecuta dicho script debe ejecutar esa misma versión de PowerShell.
- Los clientes de Configuration Manager deben ejecutar al cliente de la versión 1706 o posterior para poder ejecutar scripts.
- Para utilizar scripts, debe ser miembro del rol de seguridad de Configuration Manager adecuado.
- Para importar y crear scripts: la cuenta debe tener permisos de tipo **Crear** para **scripts SMS**.
- Para aprobar o denegar scripts: la cuenta debe tener permisos de tipo **Aprobar** para **scripts SMS**.
- Para ejecutar scripts: la cuenta debe tener permisos de tipo **Ejecutar script** para las **colecciones**.

Para obtener más información sobre los roles de seguridad de Configuration Manager:</br>
[Ámbitos de seguridad para ejecutar scripts](#BKMK_Scopes)</br>
[Roles de seguridad para ejecutar scripts](#BKMK_ScriptRoles)</br>
[Conceptos básicos de la administración basada en roles](/sccm/core/understand/fundamentals-of-role-based-administration)

## <a name="limitations"></a>Limitaciones

La funcionalidad de ejecución de scripts actualmente admite lo siguiente:

- Lenguajes de scripting: PowerShell
- Tipos de parámetro: entero, cadena y lista


>[!WARNING]
>Tenga en cuenta que, cuando se usan parámetros, se abre un área expuesta para el posible riesgo de ataque por inyección de código de PowerShell. Existen varias formas de mitigar esto y buscar soluciones alternativas, como usar expresiones regulares para validar la entrada de parámetros o usar parámetros predefinidos. Un procedimiento recomendado muy habitual consiste en no incluir los secretos en los scripts de PowerShell (contraseñas, etc). [Más información sobre la seguridad del script de PowerShell](/sccm/apps/deploy-use/learn-script-security) <!--There are external tools available to validate your PowerShell scripts such as the [PowerShell Injection Hunter](https://www.powershellgallery.com/packages/InjectionHunter/1.0.0) tool. -->


## <a name="run-script-authors-and-approvers"></a>Autores y aprobadores de la funcionalidad de ejecución de scripts

La funcionalidad de ejecución de scripts utiliza el concepto de *autores de scripts* y *aprobadores de scripts* como roles independientes para implementar y ejecutar un script. La separación de los roles de autor y aprobador permite una importante comprobación del proceso en la eficaz funcionalidad de ejecución de scripts. Hay un rol adicional de *ejecutores de scripts* que permite la ejecución de scripts, pero no la creación ni la aprobación de scripts. Vea [Crear roles de seguridad para scripts](#BKMK_ScriptRoles).

### <a name="scripts-roles-control"></a>Control de los roles de scripts

De forma predeterminada, los usuarios no pueden aprobar un script que hayan creado. Dado que los scripts son eficaces y versátiles, y se pueden implementar en varios dispositivos, podrá separar los roles de la persona que los crea y la persona que los aprueba. Esto proporciona un nivel adicional de seguridad frente a la ejecución de un script sin supervisión. Puede desactivar esta aprobación secundaria para facilitar las pruebas.

### <a name="approve-or-deny-a-script"></a>Aprobación o denegación de un script

Los scripts deben aprobarse, mediante el rol de *aprobador de scripts*, antes de que se pueden ejecutar. Para aprobar un script:

1. En la consola de Configuration Manager, haga clic en **Biblioteca de software**.
2. En el área de trabajo **Biblioteca de software**, haga clic en **Scripts**.
3. En la lista **Script**, elija el script que desea aprobar o rechazar y, a continuación, en la pestaña **Inicio**, en el grupo **Script**, haga clic en **Aprobar o denegar**.
4. En el cuadro de diálogo **Approve or deny script** (Aprobar o denegar script), seleccione **Aprobar** o **Denegar** el script. Si lo desea, escriba un comentario sobre su decisión.  Si se deniega un script, este no se puede ejecutar en los dispositivos cliente. <br>
![Scripts: aprobación](./media/run-scripts/RS-approval.png)
1. Complete el asistente. En la lista **Script**, podrá ver el cambio de la columna **Estado de la aprobación** en función de la acción llevada a cabo.

### <a name="allow-users-to-approve-their-own-scripts"></a>Procedimiento para permitir que los usuarios aprueben sus propios scripts

Esta aprobación se utiliza principalmente para la fase de pruebas de desarrollo de scripts.

1. En la consola de Configuration Manager, haga clic en **Administración**.
2. En el área de trabajo **Administración** , expanda **Configuración del sitio**y, a continuación, haga clic en **Sitios**.
3. En la lista de sitios, elija el sitio y, a continuación, en la pestaña **Inicio** del grupo **Sitios**, haga clic en **Configuración de jerarquía**.
4. En la pestaña **General** del cuadro de diálogo **Propiedades de configuración de jerarquía**, desactive la casilla **Los autores necesitan un aprobador adicional del script**.

>[!IMPORTANT]
>Como práctica recomendada, no debe permitir que el autor de un script apruebe sus propios scripts. Solo se debe permitir en entornos de laboratorio. Piense en el impacto que puede implicar modificar esta configuración en un entorno de producción.

## <a name="security-scopes"></a>Ámbitos de seguridad
*(Se introdujo con la versión 1710)*  
La funcionalidad de ejecución de scripts utiliza ámbitos de seguridad, una característica existente de Configuration Manager, para controlar la ejecución y creación de scripts mediante la asignación de etiquetas que representan grupos de usuarios. Para obtener más información, consulte [Configuración de la administración basada en roles de System Center Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md).

## <a name="bkmk_ScriptRoles"></a> Crear roles de seguridad para scripts
Los tres roles de seguridad usados para ejecutar scripts no se crean de forma predeterminada en Configuration Manager. Para crear los ejecutores de scripts, los autores de scripts y los roles aprobadores de scripts, siga los pasos indicados.

1. En la consola de Configuration Manager, vaya a **Administración** >**Seguridad** >**Roles de seguridad**
2. Haga clic con el botón derecho en un rol y haga clic en **Copiar**. El rol que copie tendrá permisos ya asignados. Asegúrese de que solo toma los permisos que le interesan. 
3. Asigne al rol personalizado un **nombre** y una **descripción**. 
4. Asigne al rol de seguridad los permisos que se describen a continuación.  

### <a name="security-role-permissions"></a>Permisos de rol de seguridad  

**Nombre de rol**: ejecutores de scripts  
- **Descripción**: estos permisos permiten a este rol ejecutar únicamente los scripts creados y aprobados por otros roles.  
- **Permisos:** asegúrese de que los permisos siguientes están establecidos en **Sí**.  

|Categoría|Permiso|Estado|
|---|---|---|
|Colección|Ejecutar script|Sí|
|Sitio|Lectura|Sí|
|Scripts SMS|Lectura|Sí|


**Nombre de rol**: autores de scripts  
- **Descripción**: estos permisos permiten a este rol crear scripts, pero no puede aprobarlos ni ejecutarlos.  
- **Permisos:** asegúrese de que están establecidos los permisos siguientes.
 
|Categoría|Permiso|Estado|
|---|---|---|
|Colección|Ejecutar script|No|
|Sitio|Lectura|Sí|
|Scripts SMS|Crear|Sí|
|Scripts SMS|Lectura|Sí|
|Scripts SMS|Eliminar|Sí|
|Scripts SMS|Modificar|Sí|


**Nombre de rol**: aprobadores de scripts  
- **Descripción**: estos permisos permiten a este rol aprobar scripts, pero no puede crearlos ni ejecutarlos.  
- **Permisos:** asegúrese de que están establecidos los permisos siguientes.  

|Categoría|Permiso|Estado|
|---|---|---|
|Colección|Ejecutar script|No|
|Sitio|Lectura|Sí|
|Scripts SMS|Lectura|Sí|
|Scripts SMS|Aprobar|Sí|
|Scripts SMS|Modificar|Sí|

     
**Ejemplo de permisos de scripts SMS para el rol de autores de scripts**  

 ![Ejemplo de permisos de scripts SMS para el rol de autores de scripts](./media/run-scripts/script_authors_permissions.png)


## <a name="create-a-script"></a>Creación de un script

1. En la consola de Configuration Manager, haga clic en **Biblioteca de software**.
2. En el área de trabajo **Biblioteca de software**, haga clic en **Scripts**.
3. En la pestaña **Inicio**, en el grupo **Crear**, haga clic en **Crear script**.
4. En la página **Script** del Asistente para **crear scripts**, configure lo siguiente:
    - **Nombre de script**: escriba un nombre para el script. Aunque puede crear varios scripts con el mismo nombre, esto dificultará la búsqueda del script que necesite en la consola de Configuration Manager.
    - **Lenguaje de script**: actualmente, solo se admiten scripts de PowerShell.
    - **Importar**: se importa un script de PowerShell en la consola. El script se muestra en el campo **Script**.
    - **Borrar**: se quita el script actual del campo Script.
    - **Script**: se muestra el script importado actualmente. Puede editar el script en este campo según sea necesario.
5. Complete el asistente. El nuevo script se muestra en la lista **Script** con el estado **En espera de aprobación**. Para poder ejecutar este script en los dispositivos cliente, debe aprobarlo. 

> [!IMPORTANT]
> Evite la aplicación de scripts al reinicio de un dispositivo o de un agente de Configuration Manageral utilizar la característica Ejecutar scripts. Si lo hace, podría provocar un estado de reinicio continuo. Si es necesario, existen mejoras en la característica de notificación de clientes que permiten reiniciar dispositivos, a partir de la versión 1710 de Configuration Manager. La [columna Reinicio pendiente](/sccm/core/clients/manage/manage-clients#Restart-clients) puede ayudar a identificar los dispositivos que necesitan un reinicio. 
> <!--SMS503978  -->

## <a name="script-parameters"></a>Parámetros de script
*(Se introdujo con la versión 1710)*  
Al agregar parámetros a un script, dotará de más flexibilidad a su trabajo. Puede incluir hasta 10 parámetros. A continuación, se describe la funcionalidad actual de la característica de ejecución de scripts con parámetros de script para los tipos de datos *Cadena* y *Entero*. También hay disponibles listas de valores preestablecidos. Si el script tiene tipos de datos no compatibles, recibirá una advertencia.

En el cuadro de diálogo **Crear script**, haga clic en **Parámetros de script**, bajo **Script**.

Cada uno de los parámetros de script tiene su propio cuadro de diálogo para agregar más detalles y la validación. Si hay un parámetro predeterminado en el script, se enumerará en la interfaz de usuario del parámetro y podrá configurarlo. Configuration Manager no sobrescribirá el valor predeterminado, ya que nunca modificará el script directamente. Puede pensar que en la interfaz de usuario se proporcionan "valores sugeridos rellenados previamente", pero Configuration Manager no proporciona acceso a los valores "predeterminados" en entorno de ejecución. Esto se puede solucionar mediante la edición del script para que tenga los valores predeterminados correctos. <!--17694323-->

>[!IMPORTANT]
> Los valores de parámetro no pueden contener un apóstrofo. </br></br>
> Hay un problema conocido en Configuration Manager versión 1802 donde los parámetros con espacios no se pasan correctamente al script. Si se usa un espacio en el parámetro, solo se pasa al script el primer elemento del parámetro, pero no lo que sigue al espacio. Los administradores pueden crear scripts de solución alternativa sustituyendo los espacios por caracteres alternativos y convertirlos, o con otros métodos.


### <a name="parameter-validation"></a>Validación de parámetros

Cada parámetro de script tiene un cuadro de diálogo **Script Parameter Properties** (Propiedades de parámetros de script) con el objetivo de agregar validación para ese parámetro. Después de agregar la validación, debería obtener errores si va a especificar un valor para un parámetro que no cumple su validación.

#### <a name="example-firstname"></a>Ejemplo: *FirstName*

En este ejemplo, es posible establecer las propiedades del parámetro de cadena *FirstName*.

![Parámetros de scripts: cadena](./media/run-scripts/RS-parameters-string.png)


La sección de validación del cuadro de diálogo **Propiedades de parámetros de script** contiene los siguientes campos:

- **Longitud mínima**: número mínimo de caracteres del campo *FirstName*.
- **Longitud máxima**: número máximo de caracteres del campo *FirstName*.
- **RegEx**: abreviatura de *expresión regular*. Para más información sobre el uso de la expresión regular, vea la sección siguiente, *Uso de la validación de expresión regular*.
- **Error personalizado**: este campo resulta útil para agregar su propio mensaje de error personalizado que reemplazará a los mensajes de error de validación del sistema.

#### <a name="using-regular-expression-validation"></a>Uso de la validación de expresión regular

Una expresión regular es una forma compacta de programación para comprobar una cadena de caracteres en una validación codificada. Por ejemplo, podría comprobar la ausencia de un carácter alfabético en mayúsculas en el campo *FirstName* colocando `[^A-Z]` en el campo *RegEx*.

.NET Framework admite el procesamiento de la expresión regular para este cuadro de diálogo. Para obtener instrucciones sobre el uso de expresiones regulares, vea [Expresiones regulares de .NET](https://docs.microsoft.com/dotnet/standard/base-types/regular-expressions). 


## <a name="script-examples"></a>Ejemplos de scripts

Estos son un par de ejemplos que ilustran los scripts que recomendamos utilizar con esta funcionalidad.

### <a name="create-a-new-folder-and-file"></a>Creación de una nueva carpeta y archivo

Este script crea una carpeta y un archivo dentro de ella según la entrada de nomenclatura.

``` powershell
Param(
[Parameter(Mandatory=$True)]
[string]$FolderName,
[Parameter(Mandatory=$True)]
[string]$FileName
)

New-Item $FolderName -type directory
New-Item $FileName -type file
```

### <a name="get-os-version"></a>Obtención de versión de SO

Este script usa WMI para consultar a la máquina la versión que tiene de SO.

``` powershell
Write-Output (Get-WmiObject -Class Win32_operatingSystem).Caption
```

## <a name="run-a-script"></a>Ejecutar un script

Una vez que se ha aprobado un script, podrá ejecutarse en un solo dispositivo o colección. Una vez que comienza la ejecución del script, se inicia rápidamente a través de un sistema de alta prioridad cuyo tiempo de espera es de una hora. Después, los resultados del script se devuelven utilizando un sistema de mensaje de estado.

Para seleccionar una colección de destinos para el script:

1. En la consola de Configuration Manager, haga clic en **Activos y compatibilidad**.
2. En el área de trabajo Activos y compatibilidad, haga clic en **Recopilaciones de dispositivos**.
3. En la lista **Recopilaciones de dispositivos**, haga clic en la recopilación de dispositivos en la que desea ejecutar el script.
4. Seleccione la colección que prefiera y haga clic en **Ejecutar script**.
5. En la página **Script** del Asistente para **ejecutar script**, elija un script de la lista. Se muestran solo los scripts aprobados.
6. Haga clic en **Siguiente** y complete el asistente.

> [!IMPORTANT]
> Si un script no se ejecuta, por ejemplo, porque un dispositivo de destino se ha desactivado durante un período de tiempo de una hora, debe ejecutarlo de nuevo.

### <a name="target-machine-execution"></a>Ejecución de la máquina objetivo

El script se ejecuta como cuenta de *sistema* o de *equipo* en los clientes objetivo. Esta cuenta tiene un acceso a la red limitado. El acceso a sistemas y ubicaciones remotos por parte del script se debe aprovisionar teniendo en cuenta este aspecto.

## <a name="script-monitoring"></a>Supervisión de scripts

Una vez iniciada la ejecución de un script en una recopilación de dispositivos, utilice el procedimiento siguiente para supervisar la operación. A partir de la versión 1710, puede supervisar un script en tiempo real en cuanto se ejecuta, así como volver a un informe de una ejecución determinada de la funcionalidad Ejecutar scripts. Los datos de estado del script se limpian como parte de la [tarea de mantenimiento Eliminar operaciones cliente antiguas](../../core/servers/manage/reference-for-maintenance-tasks.md) o eliminar el script.<br>

![Supervisión de scripts: estado de ejecución de scripts](./media/run-scripts/RS-monitoring-three-bar.png)

1. En la consola de Configuration Manager, haga clic en **Supervisión**.
2. En el área de trabajo **Supervisión**, haga clic en **Estado de script**.
3. En la lista **Estado de script** aparecen los resultados de cada script ejecutado en los dispositivos cliente. Un código de salida de script de **0** suele indicar que el script se ejecutó correctamente.
    - A partir de Configuration Manager 1802, la salida del script se trunca en 4 KB para permitir una mejor experiencia de visualización.  <!--510013-->
   
   ![Monitor de script (script truncado)](./media/run-scripts/Script-monitoring-truncated.png)

## <a name="script-output-in-1810"></a>Salida del script en 1810

Puede ver una salida de script detallada sin formato o con formato JSON estructurado. Este formato permite leer y analizar la salida de manera más sencilla. Si el script devuelve texto válido con formato JSON, podrá ver la salida detallada como **salida JSON** o **salida sin formato**. En caso contrario, la única opción es **Salida de script**.

### <a name="example-script-output-is-valid-json"></a>Ejemplo: La salida de script es un archivo JSON válido
Comando: `$PSVersionTable.PSVersion`  

Salida:  
```
Major  Minor  Build  Revision
-----  -----  -----  --------
5      1      16299  551
```

### <a name="example-script-output-isnt-valid-json"></a>Ejemplo: La salida de script no es un archivo JSON válido
Comando: `Write-Output (Get-WmiObject -Class Win32_OperatingSystem).Caption`  

Salida:  
```
Microsoft Windows 10 Enterprise
```

- Los clientes de 1810 devuelven resultados inferiores a 80 KB al sitio a través de un canal de comunicación rápido. Este cambio aumenta el rendimiento de la visualización de resultados del script o la consulta.  

  - Si el resultado del script o la consulta es mayor que 80 KB, el cliente envía los datos a través de un mensaje de estado.  
  - Los clientes anteriores a 1802 siguen utilizando los mensajes de estado.

## <a name="script-output-pre-1810"></a>Salida del script anterior a 1810

- A partir de Configuration Manager versión 1802, la salida del script realiza la devolución con el formato JSON. Este formato devuelve de manera uniforme una salida de script legible. 
- Los scripts que obtengan un resultado desconocido o en los que el cliente estaba sin conexión no se mostrarán en los gráficos ni en el conjunto de datos. <!--507179-->
- Evite devolver una salida de script grande, ya que se trunca en 4 KB. <!--508488-->
- Algunas funciones con el formato de salida de script no están disponibles cuando se ejecuta Configuration Manager versión 1802 o posterior con una versión de nivel inferior del cliente. <!--508487-->
    - Si tiene un cliente de Configuration Manager anterior a la versión 1802, obtendrá una cadena de salida.
    -  Para clientes de Configuration Manager con versión 1802 y versiones posteriores, se obtiene el formato JSON.
        - Por ejemplo, podría obtener resultados que indican TEXTO en una versión de cliente y "TEXTO" (incluido entre comillas dobles) en otra versión, y se colocarán en el gráfico como dos categorías diferentes.
        - Si tiene que solucionar este comportamiento, considere la posibilidad de ejecutar un script en dos colecciones diferentes; Uno con clientes anteriores a la versión 1802 y otro con clientes de la versión 1802 y posteriores. O, si lo prefiere, puede convertir un objeto de enumeración en un valor de cadena en los scripts para que se muestren correctamente en formato JSON. 
- Convierta un objeto de enumeración en un valor de cadena en los scripts para que se muestren correctamente en formato JSON. <!--508377-->

   ![Conversión de un objeto de enumeración en un valor de cadena](./media/run-scripts/enum-tostring-JSON.png)

## <a name="log-files"></a>Archivos de registro

A partir de la versión 1810, se ha agregado un registro adicional para la resolución de problemas.

- En el cliente, de forma predeterminada en C:\Windows\CCM\logs:  
  - **Scripts.log**  
  - **CcmMessaging.log**  

- En el punto de administración, de forma predeterminada en C:\SMS_CCM\Logs:
  - **MP_RelayMsgMgr.log**  

- En el servidor de sitio, de forma predeterminada en C:\Archivos de programa\Configuration Manager\Logs:
  - **SMS_Message_Processing_Engine.log**

## <a name="see-also"></a>Véase también

- [Configuración de la administración basada en roles en System Center Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md)
- [Aspectos básicos de la administración basada en roles](/sccm/core/understand/fundamentals-of-role-based-administration)
