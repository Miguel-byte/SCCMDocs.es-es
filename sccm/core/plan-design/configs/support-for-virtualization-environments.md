---
title: Compatibilidad con la virtualización
titleSuffix: Configuration Manager
description: Los requisitos para instalar los roles de sistema de sitio y el cliente de Configuration Manager en un entorno de virtualización.
ms.date: 01/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 1098e8c5-9676-4c2b-841b-ec88bd04e495
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 792e9e34f67ad0dc2a12df0905578effaf1f79aa
ms.sourcegitcommit: 3f791918c5dd87d8968ae9977d761dd97909398c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/10/2019
ms.locfileid: "54196321"
---
# <a name="support-for-virtualization-environments-with-configuration-manager"></a>Compatibilidad con entornos de virtualización con Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Configuration Manager admite la instalación de los roles de sistema de sitio y clientes en sistemas operativos compatibles que se ejecutan como una máquina virtual en los entornos de virtualización de este artículo. Esta compatibilidad existe incluso cuando el host de máquina virtual (entorno de virtualización) no se admita como un servidor de sitio o cliente.  

Por ejemplo, puede usar Microsoft Hyper-V Server 2012 para hospedar una máquina virtual que ejecuta Windows Server 2012. Puede instalar los roles de sistema de sitio y el cliente en la máquina virtual que ejecuta Windows Server 2012. El cliente no se puede instalar en el host que ejecuta Microsoft Hyper-V Server 2012.  


## <a name="virtualization-environments"></a>Entornos de virtualización

- Windows Server 2019  
- Windows Server 2016 <sup>[Note 1](#bkmk_note1)</sup>  
- Microsoft Hyper-V Server 2016 <sup>[Note 1](#bkmk_note1)</sup>  
- Windows Server 2012 R2  
- Microsoft Hyper-V Server 2012  
- Windows Server 2012  
- Microsoft Hyper-V Server 2008 R2  
- Windows Server 2008 R2  

#### <a name="bkmk_note1"></a> Nota 1: Virtualización anidada
Configuration Manager no admite la [virtualización anidada](https://docs.microsoft.com/windows-server/virtualization/hyper-v/What-s-new-in-Hyper-V-on-Windows#BKMK_nested), que es nueva en Windows Server 2016.


### <a name="virtualization-environment-support"></a>Compatibilidad del entorno de virtualización

Cada equipo virtual tiene los mismos o mayores requisitos de hardware y software que se usarían para un equipo de Configuration Manager físico.  

Para validar que el entorno de virtualización es compatible con Configuration Manager, use el Programa de validación de virtualización del servidor. Incluye un Asistente para directivas de compatibilidad del programa de virtualización en línea. Para más información, consulte [Windows Server Virtualization Validation Program](https://www.windowsservercatalog.com/svvp.aspx) (Programa de validación de virtualización del servidor de Windows).  

> [!NOTE]  
> Configuration Manager no es compatible con sistemas operativos invitados de Virtual PC o Virtual Server que se ejecuten en equipos Mac.  

Configuration Manager no puede administrar máquinas virtuales si están sin conexión. No se puede actualizar una imagen de máquina virtual sin conexión ni se puede recopilar un inventario mediante el cliente de Configuration Manager en el equipo host.  

Las máquinas virtuales no reciben ninguna consideración especial. Por ejemplo, Configuration Manager no puede determinar si una actualización se debe volver a aplicar a una imagen de máquina virtual si la máquina virtual se ha detenido y reiniciado sin guardar el estado de la máquina virtual a la que se ha aplicado la actualización.  



##  <a name="bkmk_Azure"></a> Máquinas virtuales de Microsoft Azure  

Configuration Manager puede ejecutarse en máquinas virtuales de Azure y localmente dentro del centro de datos. Puede usar Configuration Manager con máquinas virtuales de Azure en los escenarios siguientes:  

- **Escenario 1**: Ejecutar Configuration Manager en una máquina virtual de Azure. Úselo para administrar clientes en otras máquinas virtuales de Azure.  

- **Escenario 2**: Ejecutar Configuration Manager en una máquina virtual de Azure. Úselo para administrar clientes que no se ejecuten en Azure.  

- **Escenario 3**: Ejecutar distintos roles de sistema de sitio de Configuration Manager en máquinas virtuales de Azure. Ejecute otros roles en el centro de datos local que está conectado correctamente a Azure.  

Los mismos requisitos de Configuration Manager para redes, configuraciones admitidas y los requisitos de hardware que se aplican para instalarlo en el entorno local también se aplican a la instalación en máquinas virtuales de Azure.  

Para más información, consulte [Configuration Manager en Azure](/sccm/core/understand/configuration-manager-on-azure).

> [!IMPORTANT]  
> Los sitios y clientes de Configuration Manager que se ejecutan en máquinas virtuales de Azure están sujetos a los mismos requisitos de licencia que las instalaciones locales.  
