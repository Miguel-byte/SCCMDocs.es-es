---
title: "Creación y ejecución de scripts con Configuration Manager | Microsoft Docs"
description: Cree y ejecute scripts en los dispositivos cliente con Configuration Manager.
ms.custom: na
ms.date: 09/15/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cc230ff4-7056-4339-a0a6-6a44cdbb2857
caps.latest.revision: "14"
caps.handback.revision: "0"
author: lleonard-msft
ms.author: alleonar
manager: angrobe
ms.openlocfilehash: e6b29cd85504742e8638a55db2f6c4ecc8ab3e55
ms.sourcegitcommit: 5ca89204716750eaaceb01bba40b35b85c7122ba
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/18/2017
---
# <a name="create-and-run-powershell-scripts-from-the-configuration-manager-console"></a>Creación y ejecución de scripts de PowerShell desde la consola de Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

En Configuration Manager, además de usar paquetes y programas para implementar scripts, puede utilizar la siguiente funcionalidad para realizar las siguientes acciones:

- Importar scripts de PowerShell en Configuration Manager.
- Editar los scripts desde la consola de Configuration Manager (solo para scripts sin firmar).
- Marcar scripts como aprobados o denegados, para mejorar la seguridad.
- Ejecutar scripts en recopilaciones de equipos cliente de Windows y equipos de Windows administrados locales. No se implementan los scripts, sino que se ejecutan casi en tiempo real en los dispositivos cliente.
- Examine los resultados devueltos por el script en la consola de Configuration Manager.

>[!TIP]
>En esta versión de Configuration Manager, los scripts son una característica de versión preliminar. Para habilitarlos, consulte [Características de versión preliminar en System Center Configuration Manager](/sccm/core/servers/manage/pre-release-features).

## <a name="prerequisites"></a>Requisitos previos

Para ejecutar los scripts de PowerShell, el cliente debe ejecutar la versión 3.0 o posterior de PowerShell. Sin embargo, si se ejecuta un script que contiene la funcionalidad de una versión posterior de PowerShell, el cliente en el que se ejecuta dicho script debe ejecutar esa misma versión.

Los clientes de Configuration Manager deben ejecutar al cliente de la versión 1706 o posterior para poder ejecutar scripts.

Para utilizar scripts, debe ser miembro del rol de seguridad de Configuration Manager adecuado.

- Para importar y crear scripts: la cuenta debe tener permisos **Crear** para **scripts SMS** en el rol de seguridad **Administrador total**.
- Para aprobar o denegar scripts: la cuenta debe tener permisos **Aprobar** para **scripts SMS** en el rol de seguridad **Administrador total**.
- Para ejecutar scripts: la cuenta debe tener permisos **Ejecutar script** para las **colecciones** en el rol de seguridad **Administrador de configuración de cumplimiento**.

Para obtener más información sobre los roles de seguridad de Configuration Manager, consulte [Conceptos básicos de la administración basada en roles](/sccm/core/understand/fundamentals-of-role-based-administration).

De forma predeterminada, los usuarios no pueden aprobar un script que hayan creado. Dado que los scripts son eficaces y versátiles, y se pueden implementar en varios dispositivos, podrá separar los roles de la persona que los crea y la persona que los aprueba. Esto proporciona un nivel adicional de seguridad frente a la ejecución de un script sin supervisión. Puede desactivar esta aprobación secundaria para facilitar las pruebas.

## <a name="allow-users-to-approve-their-own-scripts"></a>Procedimiento para permitir que los usuarios aprueben sus propios scripts

1. En la consola de Configuration Manager, haga clic en **Administración**.
2. En el área de trabajo **Administración** , expanda **Configuración del sitio**y, a continuación, haga clic en **Sitios**.
3. En la lista de sitios, elija el sitio y, a continuación, en la pestaña **Inicio** del grupo **Sitios**, haga clic en **Configuración de jerarquía**.
4. En la pestaña **General** del cuadro de diálogo **Propiedades de configuración de jerarquía**, desactive la casilla **Do not allow script authors to approve their own scripts** (No permitir que los autores de scripts aprueben sus propios scripts).

## <a name="import-and-edit-a-script"></a>Importación y modificación de un script

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

### <a name="script-examples"></a>Ejemplos de scripts

Estos son algunos ejemplos que ilustran los scripts que recomendamos utilizar con esta funcionalidad.

#### <a name="create-a-folder"></a>Crea una carpeta

*New-Item "c:\scripts" -nombre de la carpeta*


#### <a name="create-a-file"></a>Creación de un archivo

*New-Item c:\scripts\new_file.txt -nombre del archivo*


## <a name="approve-or-deny-a-script"></a>Aprobación o denegación de un script

Para ejecutar un script, es necesario aprobarlo. Para aprobar un script:

1. En la consola de Configuration Manager, haga clic en **Biblioteca de software**.
2. En el área de trabajo **Biblioteca de software**, haga clic en **Scripts**.
3. En la lista **Script**, elija el script que desea aprobar o rechazar y, a continuación, en la pestaña **Inicio**, en el grupo **Script**, haga clic en **Aprobar o denegar**.
4. En el cuadro de diálogo **Approve or deny script** (Aprobar o denegar script), **apruebe** o **deniegue** el script y, opcionalmente, escriba un comentario sobre su decisión. Si se deniega un script, este no se puede ejecutar en los dispositivos cliente.
5. Complete el asistente. En la lista **Script**, podrá ver el cambio de la columna **Estado de la aprobación** en función de la acción llevada a cabo.

## <a name="run-a-script"></a>Ejecutar un script
Una vez que se ha aprobado un script, podrá ejecutarse en la colección que elija.

1. En la consola de Configuration Manager, haga clic en **Activos y compatibilidad**.
2. En el área de trabajo Activos y compatibilidad, haga clic en **Recopilaciones de dispositivos**.
3. En la lista **Recopilaciones de dispositivos**, haga clic en la recopilación de dispositivos en la que desea ejecutar el script.
4. En la pestaña **Inicio**, en el grupo **Todos los sistemas**, haga clic en **Ejecutar script**.
5. En la página **Script** del Asistente para **ejecutar script**, elija un script de la lista. Se muestran solo los scripts aprobados.
6. Haga clic en **Siguiente** y complete el asistente.

>[!IMPORTANT]
>El script tiene un período de una hora durante el cual se ejecutará. Si no ejecuta (por ejemplo, si el equipo se ha apagado) en este período, debe volver a ejecutarlo.

## <a name="next-steps"></a>Pasos siguientes

Después de ejecutar un script en los dispositivos cliente, siga este procedimiento para supervisar si la operación se ha completado correctamente.

1. En la consola de Configuration Manager, haga clic en **Supervisión**.
2. En el área de trabajo **Supervisión**, haga clic en **Estado de script**.
3. En la lista **Estado de script** aparecen los resultados de cada script ejecutado en los dispositivos cliente. Un código de salida de script de **0** suele indicar que el script se ejecutó correctamente.
