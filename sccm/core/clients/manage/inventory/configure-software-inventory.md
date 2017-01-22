---
title: Configurar el inventario de software | Microsoft Docs
description: "Configure el inventario de software y una carpeta de exclusión de inventario en System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: cc226259-0e28-410a-94d3-223bdc948818
caps.latest.revision: 4
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: fc392e4440e84614f92218e9c7a09ec1c2c64f53
ms.openlocfilehash: 7ba943bee7faf417099cde0388649e4907525738


---
# <a name="how-to-configure-software-inventory-in-system-center-configuration-manager"></a>Cómo configurar el inventario de software en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Puede crear un archivo oculto denominado **Skpswi.dat** y colocarlo en la raíz de la unidad de disco duro de un cliente para excluirlo del inventario de software de System Center Configuration Manager. También puede colocar este archivo en la raíz de cualquier estructura de carpetas que quiera excluir del inventario de software. Este procedimiento se puede utilizar para deshabilitar el inventario de software de un único cliente de servidor o una estación de trabajo, como un servidor de archivos grandes.  

> [!NOTE]  
>  El inventario de software no inventariará la unidad de cliente de nuevo a menos que este archivo se elimine de la unidad del equipo cliente.  

### <a name="to-exclude-folders-from-software-inventory"></a>Cómo excluir carpetas del inventario de software  

1.  Con Notepad.exe, cree un archivo vacío llamado **Skpswi.dat**.  

2.  Haga clic con el botón derecho en el archivo **Skpswi.dat** y después haga clic en **Propiedades**. En las propiedades de archivo del archivo Skpswi.dat, seleccione el atributo **Oculto** .  

3.  Coloque el archivo **Skpswi.dat** en la raíz de cada estructura de carpeta o unidad de disco duro de cliente que quiera excluir del inventario de software.  



<!--HONumber=Dec16_HO3-->


