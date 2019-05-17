---
title: 'Sincronización de actualizaciones sin conexión a Internet '
titleSuffix: Configuration Manager
description: Ejecute la sincronización de actualizaciones de software en el punto de actualización de software de nivel superior que está desconectado de Internet.
ms.date: 01/23/2017
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 1a997c30-8e71-4be5-89ee-41efb2c8d199
manager: dougeby
author: mestew
ms.author: mstewart
ms.collection: M365-identity-device-management
ms.openlocfilehash: 67b284e369268b184067e33d2a505585618795e5
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 05/09/2019
ms.locfileid: "65493978"
---
# <a name="synchronize-software-updates-from-a-disconnected-software-update-point"></a>Sincronizar actualizaciones de software desde un punto de actualización de software desconectado  

*Se aplica a: System Center Configuration Manager (Rama actual)*

 Cuando un punto de actualización de software en el sitio de nivel superior se desconecta de Internet, debe usar las funciones de exportación e importación de la herramienta WSUSUtil para sincronizar los metadatos de las actualizaciones de software. Puede elegir un servidor WSUS existente que no se incluya en su jerarquía de Configuration Manager como origen de la sincronización. En este tema, se proporciona información sobre cómo usar las funciones de exportación e importación de la herramienta WSUSUtil.  

 Para exportar e importar metadatos de actualizaciones de software, debe exportar los metadatos de actualizaciones de software desde la base de datos WSUS en un servidor de exportación especificado, copiar los archivos de los términos de licencia almacenados localmente en el punto de actualización de software desconectado y, a continuación, importar los metadatos de actualizaciones de software en la base de datos WSUS en el punto de actualización de software desconectado.  

 Utilice la siguiente tabla para identificar el servidor de exportación al que se van a exportar los metadatos de las actualizaciones de software.  

|Punto de actualización de software|Origen de la actualización del canal de subida para puntos de actualización de software conectados|Servidor de exportación para un punto de actualización de software desconectado|  
|---------------------------|-----------------------------------------------------------------|------------------------------------------------------------|  
|Sitio de administración central|Microsoft Update (Internet)<br /><br /> Servidor WSUS existente|Elija un servidor WSUS sincronizado con Microsoft Update mediante las clasificaciones de actualizaciones de software, los productos y los idiomas que necesite en su entorno de Configuration Manager.|  
|Sitio primario independiente|Microsoft Update (Internet)<br /><br /> Servidor WSUS existente|Elija un servidor WSUS sincronizado con Microsoft Update mediante las clasificaciones de actualizaciones de software, los productos y los idiomas que necesite en su entorno de Configuration Manager.|  

 Antes de iniciar el proceso de exportación, compruebe que se ha completado la sincronización de las actualizaciones de software en el servidor de exportación seleccionado para asegurarse de que se sincronizan los metadatos de las actualizaciones de software más recientes. Para comprobar que la sincronización de las actualizaciones de software ha finalizado correctamente, utilice el procedimiento siguiente.  

#### <a name="to-verify-that-software-updates-synchronization-has-completed-successfully-on-the-export-server"></a>Para comprobar que la sincronización de las actualizaciones de software se realizó correctamente en el servidor de exportación  

1.  Abra la consola Administración de WSUS y conéctese a la base de datos WSUS en el servidor de exportación.  

2.  En la consola Administración de WSUS, haga clic en **Sincronizaciones**. Se muestra una lista de los intentos de sincronización de actualizaciones de software en el panel de resultados.  

3.  En el panel de resultados, busque el intento de sincronización de actualizaciones de software más reciente y compruebe que se realizó correctamente.  

> [!IMPORTANT]  
>  La herramienta WSUSUtil debe ejecutarse localmente en el servidor de exportación para exportar los metadatos de las actualizaciones de software, y también debe ejecutarse en el servidor del punto de actualización de software desconectado para importar los metadatos de las actualizaciones de software. Además, el usuario que ejecuta la herramienta WSUSUtil debe ser un miembro del grupo de administradores local en cada servidor.  

## <a name="export-process-for-software-updates"></a>Proceso de exportación de actualizaciones de software  
 El proceso de exportación de las actualizaciones de software consta de dos pasos principales: copiar los archivos de los términos de licencia almacenados localmente en el punto de actualización de software desconectado y exportar los metadatos de las actualizaciones de software de la base de datos WSUS en el servidor de exportación.  

 Utilice el siguiente procedimiento para copiar los metadatos de los términos de licencia locales en el punto de actualización de software desconectado.  

#### <a name="to-copy-local-files-from-the-export-server-to-the-disconnected-software-update-point-server"></a>Para copiar archivos locales desde el servidor de exportación en el servidor del punto de actualización de software desconectado  

1. En el servidor de exportación, vaya a la carpeta donde se almacenan las actualizaciones de software y los términos de licencia para las actualizaciones de software. De forma predeterminada, el servidor WSUS almacena los archivos en <*UnidadInstalaciónWSUS*>\WSUS\WSUSContent\\, donde *UnidadInstalaciónWSUS* es la unidad en la que está instalado WSUS.  

2. Copie todos los archivos y carpetas desde esta ubicación a la carpeta WSUSContent en el servidor del punto de actualización de software desconectado.  

   Utilice el siguiente procedimiento para exportar los metadatos de las actualizaciones de software desde la base de datos WSUS al servidor de exportación.  

#### <a name="to-export-software-updates-metadata-from-the-wsus-database-on-the-export-server"></a>Para exportar metadatos de actualizaciones de software desde la base de datos WSUS al servidor de exportación  

1.  En el símbolo del sistema del servidor de exportación, vaya a la carpeta que contiene WSUSutil.exe. De forma predeterminada, la herramienta se encuentra en %*ProgramFiles*%\Update Services\Tools. Por ejemplo, si la herramienta se encuentra en la ubicación predeterminada, escriba **cd %ProgramFiles%\Update Services\Tools**.  

2.  Escriba lo siguiente para exportar los metadatos de las actualizaciones de software a un archivo de paquete:  

     **wsusutil.exe export**  *nombreDePaquete*  *archivoDeRegistro*  

     Por ejemplo:  

     **wsusutil.exe export export.cab export.log**  

     El formato se puede definir de la siguiente manera: WSUSutil.exe va seguido de la opción de exportación, el nombre del archivo .cab de exportación creado durante la operación de exportación y el nombre de un archivo de registro. WSUSutil.exe exporta los metadatos desde el servidor de exportación y crea un archivo de registro de la operación.  

    > [!NOTE]  
    >  Los nombres del paquete (archivo .cab) y del archivo de registro deben ser únicos en la carpeta actual.  

3.  Mueva el paquete de exportación a la carpeta que contiene WSUSutil.exe en el servidor WSUS de importación.  

    > [!NOTE]  
    >  Si mueve el paquete a esta carpeta, la experiencia de importación puede ser más fácil. Puede mover el paquete a cualquier ubicación que sea accesible al servidor de importación y, a continuación, especificar la ubicación cuando ejecute WSUSutil.exe.  

## <a name="import-software-updates-metadata"></a>Importar metadatos de actualizaciones de software  
 Utilice el siguiente procedimiento para importar metadatos de las actualizaciones de software desde el servidor de exportación hasta el punto de actualización de software desconectado.  

> [!IMPORTANT]  
>  No importe nunca datos exportados desde un origen que no sea de confianza. Si importa contenido desde un origen que no es de confianza, podría poner en peligro la seguridad de su servidor WSUS.  

#### <a name="to-import-metadata-to-the-database-of-the-import-server"></a>Para importar metadatos en la base de datos del servidor de importación  

1.  En el símbolo del sistema del servidor WSUS de importación, vaya a la carpeta que contiene WSUSutil.exe. De forma predeterminada, la herramienta se encuentra en %*ProgramFiles*%\Update Services\Tools.  

2.  Escriba lo siguiente:  

     **wsusutil.exe import**  *nombreDePaquete*  *archivoDeRegistro*  

     Por ejemplo:  

     **wsusutil.exe import export.cab import.log**  

     El formato se puede resumir de la siguiente manera: WSUSutil.exe va seguido del comando de importación, el nombre del archivo del paquete (.cab) creado durante la operación de exportación, la ruta de acceso del archivo del paquete si se encuentra en una carpeta diferente y el nombre de un archivo de registro. WSUSutil.exe importa los metadatos desde el servidor de exportación y crea un archivo de registro de la operación.  

## <a name="next-steps"></a>Pasos siguientes
Después de sincronizar las actualizaciones de software por primera vez o después de que haya clasificaciones o productos nuevos, debe [configurar los productos y clasificaciones nuevos](configure-classifications-and-products.md) para sincronizar las actualizaciones de software con los nuevos criterios.

Después de sincronizar las actualizaciones de software con los criterios que necesite, [administre la configuración de las actualizaciones de software](manage-settings-for-software-updates.md).  
