---
title: "Instalar la evaluación de actualización | System Center Configuration Manager"
description: "Obtenga información sobre cómo actualizar una instalación de evaluación a una instalación completa de System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9a32f5a3-9917-434f-9811-106170f404be
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 0ad15c0caddeb3c200b8c663631d2993a338c7c8

---
# <a name="upgrade-an-evaluation-install-of-system-center-configuration-manager-to-a-full-install"></a>Actualizar una instalación de evaluación de System Center Configuration Manager a una instalación completa

*Se aplica a: System Center Configuration Manager (rama actual)*



 Si ha instalado System Center Configuration Manager como versión de evaluación, después de 180 días, la consola de Configuration Manager pasará a ser de solo lectura hasta que active el producto desde la página **Mantenimiento del sitio** del programa de instalación. En cualquier momento, antes o después del período de 180 días, tiene la opción de actualizar una instalación de evaluación a una instalación completa.  

> [!NOTE]  
>  Si conecta una consola de Configuration Manager a una instalación de evaluación de Configuration Manager, en la barra de título de la consola se muestra el número de días que quedan para que expire la instalación de evaluación. El número de días no se actualiza automáticamente y solo se actualiza cuando se realiza una nueva conexión a un sitio.  

 **Puede actualizar los siguientes sitios que ejecutan una instalación de evaluación:**  

-   Sitio de administración central  

-   Sitio primario  

Ya que los sitios secundarios no se tratan como instalaciones de evaluación, no es necesario modificar un sitio secundario si su sitio primario principal se actualiza a una instalación completa.  

**Requisitos previos para actualizar una edición de evaluación a una edición completa:**  

-   Debe poder usar un producto válido durante la actualización.  

-   La cuenta debe tener permisos de **administrador** en el equipo en el que va a instalar el sitio.  

### <a name="to-upgrade-an-evaluation-edition-of-configuration-manager-to-a-licensed-edition"></a>Para actualizar de una edición de evaluación de Configuration Manager a una edición con licencia  

1.  En el servidor de sitio, busque y ejecute **SETUP.exe** (programa de instalación de Configuration Manager) en la carpeta de instalación de Configuration Manager (**%path%\BIN\X64**).  Debe ejecutar la copia del programa de instalación que se encuentra en el servidor de sitio, en la carpeta de Configuration Manager, porque las opciones de mantenimiento del sitio no están disponibles si ejecuta el programa de instalación desde medios de instalación.  

2.  En la página **Antes de empezar** , haga clic en **Siguiente**.  

3.  En la página **Introducción** , seleccione **Realizar mantenimiento de sitio o restablecer este sitio**y, a continuación, haga clic en **Siguiente**.  

4.  En la página **Mantenimiento del sitio** , seleccione **Actualizar la edición de evaluación a una edición con licencia**, escriba una clave de producto válida y después haga clic en **Siguiente**.  

5.  En la página **Términos de licencia del software de Microsoft** , lea y acepte los términos de licencia y, a continuación, haga clic en **Siguiente**.  

6.  En la página **Configuración** , haga clic en **Cerrar** para completar el asistente.  

    > [!NOTE]  
    >  La barra de título de las consolas de Configuration Manager que permanecen conectadas al sitio que va a actualizar podría indicar que el sitio es aún una versión de evaluación, hasta que vuelva a conectar la consola al sitio.  



<!--HONumber=Nov16_HO1-->


