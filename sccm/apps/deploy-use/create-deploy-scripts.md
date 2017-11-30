---
title: "Creación y ejecución de scripts"
titleSuffix: Configuration Manager
description: Cree y ejecute scripts de Powershell en dispositivos cliente.
ms.custom: na
ms.date: 11/20/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cc230ff4-7056-4339-a0a6-6a44cdbb2857
caps.latest.revision: "14"
caps.handback.revision: "0"
author: BrucePerlerMS
ms.author: bruceper
manager: angrobe
ms.openlocfilehash: 964f6d39c4c1afc82ff4336821740923d27cd569
ms.sourcegitcommit: 12d0d53e47bbf1a0bbd85015b8404a44589d1e14
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="create-and-run-powershell-scripts-from-the-configuration-manager-console"></a>Creación y ejecución de scripts de PowerShell desde la consola de Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Ahora hemos integrado de forma más eficaz la capacidad de ejecutar scripts de Powershell con System Center Configuration Manager. PowerShell tiene la ventaja de crear scripts automatizados y sofisticados que entienden y comparten una gran comunidad de usuarios. Los scripts simplifican la creación de herramientas personalizadas para administrar software y permiten realizar tareas rutinarias rápidamente, lo que permite obtener grandes resultados de forma más sencilla y coherente.

Gracias a esta integración con System Center Configuration Manager, puede usar la funcionalidad de *ejecución de scripts* para hacer lo siguiente:

- Crear y editar scripts para usarlos con Configuration Manager
- Administrar el uso de los scripts a través de roles y ámbitos de seguridad  
- Ejecutar scripts en recopilaciones o equipos Windows administrados locales
- Obtener resultados agregados y rápidos de scripts desde dispositivos cliente
- Supervisar la ejecución de scripts y ver los resultados de los informes desde la salida de los scripts

>[!IMPORTANT]
>Dada la eficacia de los scripts, le recordamos que los utilice de forma intencionada y cautelosa. Hemos integrado medidas de seguridad adicionales para ayudarlo: los ámbitos y roles separados. Asegúrese de validar la precisión de los scripts antes de ejecutarlos y confirme que provienen de un origen de confianza, para así evitar que se ejecuten scripts involuntariamente. Tenga cuidado con los caracteres extendidos u otra ofuscación, e Infórmese sobre la protección de scripts.

>[!TIP]
>Los scripts de PowerShell son una característica de versión preliminar que se introdujo en la 1706. Para habilitarlos, consulte [Características de versión preliminar en System Center Configuration Manager](/sccm/core/servers/manage/pre-release-features).

## <a name="prerequisites"></a>Requisitos previos

- Para ejecutar los scripts de PowerShell, el cliente debe ejecutar la versión 3.0 o posterior de PowerShell. Sin embargo, si se ejecuta un script que contiene la funcionalidad de una versión posterior de PowerShell, el cliente en el que se ejecuta dicho script debe ejecutar esa misma versión de PowerShell.
- Los clientes de Configuration Manager deben ejecutar al cliente de la versión 1706 o posterior para poder ejecutar scripts.
- Para utilizar scripts, debe ser miembro del rol de seguridad de Configuration Manager adecuado.
- Para importar y crear scripts: la cuenta debe tener permisos **Crear** para **scripts SMS** en el rol de seguridad **Administrador total**.
- Para aprobar o denegar scripts: la cuenta debe tener permisos **Aprobar** para **scripts SMS** en el rol de seguridad **Administrador total**.
- Para ejecutar scripts: la cuenta debe tener permisos **Ejecutar script** para las **colecciones** en el rol de seguridad **Administrador de configuración de cumplimiento**.

Para obtener más información sobre los roles de seguridad de Configuration Manager, consulte [Conceptos básicos de la administración basada en roles](/sccm/core/understand/fundamentals-of-role-based-administration).

## <a name="limitations"></a>Limitaciones

La funcionalidad de ejecución de scripts actualmente admite lo siguiente:

- Lenguajes de scripting: PowerShell
- Tipos de parámetro: entero y cadena

## <a name="run-script-authors-and-approvers"></a>Autores y aprobadores de la funcionalidad de ejecución de scripts

La funcionalidad de ejecución de scripts utiliza el concepto de *autores de scripts* y *aprobadores de scripts* como roles independientes para implementar y ejecutar un script. La separación de los roles de autor y aprobador permite una importante comprobación del proceso en la eficaz funcionalidad de ejecución de scripts.

### <a name="scripts-roles-control"></a>Control de los roles de scripts

De forma predeterminada, los usuarios no pueden aprobar un script que hayan creado. Dado que los scripts son eficaces y versátiles, y se pueden implementar en varios dispositivos, podrá separar los roles de la persona que los crea y la persona que los aprueba. Esto proporciona un nivel adicional de seguridad frente a la ejecución de un script sin supervisión. Puede desactivar esta aprobación secundaria para facilitar las pruebas.

### <a name="approve-or-deny-a-script"></a>Aprobación o denegación de un script

Los scripts deben aprobarse, mediante el rol de *aprobador de scripts*, antes de que se pueden ejecutar. Para aprobar un script:

1. En la consola de Configuration Manager, haga clic en **Biblioteca de software**.
2. En el área de trabajo **Biblioteca de software**, haga clic en **Scripts**.
3. En la lista **Script**, elija el script que desea aprobar o rechazar y, a continuación, en la pestaña **Inicio**, en el grupo **Script**, haga clic en **Aprobar o denegar**.
4. En el cuadro de diálogo **Aprobar o denegar script**, seleccione **Aprobar** o **Denegar** el script y, opcionalmente, escriba un comentario sobre su decisión.  Si se deniega un script, este no se puede ejecutar en los dispositivos cliente. <br>
![Scripts: aprobación](./media/run-scripts/RS-approval.png)
5. Complete el asistente. En la lista **Script**, podrá ver el cambio de la columna **Estado de la aprobación** en función de la acción llevada a cabo.

### <a name="allow-users-to-approve-their-own-scripts"></a>Procedimiento para permitir que los usuarios aprueben sus propios scripts

Esta aprobación se utiliza principalmente para la fase de pruebas de desarrollo de scripts.

1. En la consola de Configuration Manager, haga clic en **Administración**.
2. En el área de trabajo **Administración** , expanda **Configuración del sitio**y, a continuación, haga clic en **Sitios**.
3. En la lista de sitios, elija el sitio y, a continuación, en la pestaña **Inicio** del grupo **Sitios**, haga clic en **Configuración de jerarquía**.
4. En la pestaña **General** del cuadro de diálogo **Propiedades de configuración de jerarquía**, desactive la casilla **Do not allow script authors to approve their own scripts** (No permitir que los autores de scripts aprueben sus propios scripts).

>[!IMPORTANT]
>Como práctica recomendada, no debe permitir que el autor de un script apruebe sus propios scripts. Solo se puede permitir en entornos de laboratorio. Piense en el impacto que puede implicar modificar esta configuración en un entorno de producción.

## <a name="security-scopes"></a>Ámbitos de seguridad
*(Se introdujo con la versión 1710)*  
La funcionalidad de ejecución de scripts utiliza ámbitos de seguridad, una característica existente de Configuration Manager, para controlar la ejecución y creación de scripts mediante la asignación de etiquetas que representan grupos de usuarios. Para obtener más información, consulte [Configuración de la administración basada en roles de System Center Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md).

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
1. Complete el asistente. El nuevo script se muestra en la lista **Script** con el estado **En espera de aprobación**. Para poder ejecutar este script en los dispositivos cliente, debe aprobarlo.

## <a name="script-parameters"></a>Parámetros de script
*(Se introdujo con la versión 1710)*  
Al agregar parámetros a un script, dotará de más flexibilidad a su trabajo. A continuación, se describe la funcionalidad actual de la característica de ejecución de scripts con parámetros de script para los tipos de datos *Cadena* y *Entero*. También hay disponibles listas de valores preestablecidos. Si el script tiene tipos de datos no compatibles, recibirá una advertencia.

En el cuadro de diálogo **Crear script**, haga clic en **Parámetros de script**, bajo **Script**.

Cada uno de los parámetros de script tiene su propio cuadro de diálogo para agregar más detalles y la validación.

### <a name="parameter-validation"></a>Validación de parámetros

Cada parámetro de script tiene un cuadro de diálogo **Script Parameter Properties** (Propiedades de parámetros de script) con el objetivo de agregar validación para ese parámetro. Después de agregar la validación, debería obtener errores si va a especificar un valor para un parámetro que no cumple su validación.

#### <a name="example-firstname"></a>Ejemplo: FirstName

En este ejemplo, es posible establecer las propiedades del parámetro de cadena *FirstName*. Observe el campo opcional de **Error personalizado**. Este campo es útil para agregar instrucciones de usuario sobre el campo específico e instrucciones para el usuario sobre su interacción con el parámetro de cadena (*FirstName* en este caso).

![Parámetros de scripts: cadena](./media/run-scripts/RS-parameters-string.png)

## <a name="script-examples"></a>Ejemplos de scripts

Estos son un par de ejemplos que ilustran los scripts que recomendamos utilizar con esta funcionalidad.

### <a name="create-a-folder"></a>Crea una carpeta

``` powershell
New-Item "c:\scripts" -type folder name
```

### <a name="create-a-file"></a>Creación de un archivo

```powershell
New-Item "c:\scripts\new_file.txt" -type file name
```

### <a name="ping-a-given-computer"></a>Ping a un equipo determinado

Este script toma una cadena y se utiliza como un parámetro de una operación de *ping*.

``` powershell
Param
(
 [String][Parameter(Mandatory=$True, Position=1)] $Computername
)

Ping $Computername
```

### <a name="get-battery-status"></a>Obtención del estado de la batería

Este script usa WMI para consultar a la máquina el estado de batería.

``` powershell
Write-Output (Get-WmiObject -Class Win32_Battery).BatteryStatus

```

## <a name="run-a-script"></a>Ejecutar un script

Una vez que se ha aprobado un script, podrá ejecutarse en la colección que elija. Una vez que comienza la ejecución del script, se inicia rápidamente a través de un sistema de alta prioridad y se ejecuta dentro de una hora. Los resultados del script se devuelven utilizando un sistema de mensaje de estado más lento.

1. En la consola de Configuration Manager, haga clic en **Activos y compatibilidad**.
2. En el área de trabajo Activos y compatibilidad, haga clic en **Recopilaciones de dispositivos**.
3. En la lista **Recopilaciones de dispositivos**, haga clic en la recopilación de dispositivos en la que desea ejecutar el script.
4. En la pestaña **Inicio**, en el grupo **Todos los sistemas**, haga clic en **Ejecutar script**.
5. En la página **Script** del Asistente para **ejecutar script**, elija un script de la lista. Se muestran solo los scripts aprobados.
6. Haga clic en **Siguiente** y complete el asistente.

>[!IMPORTANT]
>Si un script no se ejecuta, por ejemplo, porque un cliente de destino se ha desactivado, en el período de tiempo de una hora, debe ejecutarlo de nuevo.

### <a name="target-machine-execution"></a>Ejecución de la máquina objetivo
El script se ejecuta como cuenta de *sistema* o de *equipo* en los clientes objetivo. Esta cuenta tiene un acceso a la red limitado. El acceso a sistemas y ubicaciones remotos por parte del script se debe aprovisionar teniendo en cuenta este aspecto.

## <a name="work-flow-and-monitoring"></a>Supervisión y flujo de trabajo

Este es el aspecto que tiene un flujo de trabajo de la funcionalidad de ejecución de scripts: creación, aprobación, ejecución y supervisión.

![Funcionalidad de ejecución de scripts: flujo de trabajo](./media/run-scripts/RS-run-scripts-work-flow.png)

### <a name="script-monitoring"></a>Supervisión de scripts

Una vez iniciada la ejecución de un script en una recopilación de dispositivos, utilice el procedimiento siguiente para supervisar la operación. A partir de la versión 1710, puede supervisar un script en tiempo real en cuanto se ejecuta, así como volver a un informe de una ejecución determinada de la funcionalidad de ejecución de scripts.

1. En la consola de Configuration Manager, haga clic en **Supervisión**.
2. En el área de trabajo **Supervisión**, haga clic en **Estado de script**. ![Supervisión de scripts: estado de ejecución de scripts](./media/run-scripts/RS-monitoring-three-bar.png)
3. En la lista **Estado de script** aparecen los resultados de cada script ejecutado en los dispositivos cliente. Un código de salida de script de **0** suele indicar que el script se ejecutó correctamente.

## <a name="see-also"></a>Véase también

- [Configuración de la administración basada en roles en System Center Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md)
- [Aspectos básicos de la administración basada en roles](/sccm/core/understand/fundamentals-of-role-based-administration)
