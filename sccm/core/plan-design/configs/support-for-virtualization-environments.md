---
title: "Compatibilidad con la virtualización | Microsoft Docs"
description: "Obtenga los requisitos para instalar los roles de sistema de sitio y el cliente de System Center Configuration Manager en un entorno de virtualización."
ms.custom: na
ms.date: 1/12/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1098e8c5-9676-4c2b-841b-ec88bd04e495
caps.latest.revision: 6
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10192da2633555ab3bae60dbb1156d1926f9a4a0
ms.openlocfilehash: b49bd179da850cee35b2487a353bb1788df03d58


---
# <a name="support-for-virtualization-environments-for-system-center-configuration-manager"></a>Compatibilidad con entornos de virtualización de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Configuration Manager admite la instalación de los roles de sistema de sitio y clientes en sistemas operativos compatibles que se ejecutan como una máquina virtual en los entornos de virtualización que se muestran en este artículo. Esta compatibilidad existe incluso cuando el host de máquina virtual (entorno de virtualización) no se admita como un servidor de sitio o cliente.  

 Por ejemplo, si usa Microsoft Hyper-V Server 2012 para hospedar una máquina virtual que ejecuta Windows Server 2012, puede instalar los roles de sistema de sitio o cliente en la máquina virtual (Windows Server 2012), pero no en el host (Microsoft Hyper-V Server 2012).  

|Entorno de virtualización|  
|--------------------------------|  
|Windows Server 2008 R2|  
|Microsoft Hyper-V Server 2008 R2|  
|Windows Server 2012|  
|Microsoft Hyper-V Server 2012|  
|Windows Server 2012 R2|
|Windows Server 2016 <sup>(Ver *nota 1*)</sup>|
|Microsoft Hyper-V Server 2016 <sup>(Ver *nota 1*)|
-  *Nota 1*: Configuration Manager no admite la [virtualización anidada](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/what-s-new-in-hyper-v-on-windows#a-namebkmknestedanested-virtualization-new), que es nueva en Windows Server 2016.


 Cada equipo virtual que use debe cumplir o superar los mismos requisitos de hardware y software que usaría para un equipo físico de Configuration Manager.  

 Puede validar que el entorno de virtualización es compatible con Configuration Manager mediante el Programa de validación de virtualización del servidor y su Asistente para directivas de compatibilidad del programa de virtualización en línea. Para obtener más información sobre el Programa de validación de virtualización del servidor, consulte [Windows Server Virtualization Validation Program](https://www.windowsservercatalog.com/svvp.aspx) (Programa de validación de virtualización de Windows Server).  

> [!NOTE]  
>  Configuration Manager no es compatible con sistemas operativos invitados de Virtual PC o Virtual Server que se ejecuten en equipos Mac.  

Configuration Manager no puede administrar máquinas virtuales a menos que estén en línea. No se puede actualizar una imagen de máquina virtual sin conexión ni se puede recopilar un inventario mediante el cliente de Configuration Manager en el equipo host.  

Las máquinas virtuales no reciben ninguna consideración especial. Por ejemplo, Configuration Manager no puede determinar si una actualización se debe volver a aplicar a una imagen de máquina virtual si la máquina virtual se ha detenido y reiniciado sin guardar el estado de la máquina virtual a la que se ha aplicado la actualización.  

##  <a name="a-namebkmkazurea-microsoft-azure-virtual-machines"></a><a name="bkmk_Azure"></a> Máquinas virtuales de Microsoft Azure  
 Configuration Manager puede ejecutarse en máquinas virtuales de Azure y localmente dentro de la red corporativa física. Puede usar Configuration Manager con máquinas virtuales de Azure en los escenarios siguientes:  

-   **Escenario 1:** puede ejecutar Configuration Manager en una máquina virtual de Azure y usarlo para administrar clientes instalados en otras máquinas virtuales de Azure.  

-   **Escenario 2:** puede ejecutar Configuration Manager en una máquina virtual de Azure y usarlo para administrar clientes que no se ejecutan en Azure.  

-   **Escenario 3:** puede ejecutar diferentes roles de sistema de sitio de Configuration Manager en máquinas virtuales de Azure mientras ejecuta otros roles en su red corporativa física (con la conectividad de red adecuada para las comunicaciones).  

Los mismos requisitos de System Center Configuration Manager para redes, configuraciones admitidas y requisitos de hardware que se aplican a la instalación de Configuration Manager local en su red corporativa física también se aplican a la instalación en máquinas virtuales de Azure.  

Para obtener más información, vea [Configuration Manager en Azure - Preguntas más frecuentes](/sccm/core/understand/configuration-manager-on-azure).

> [!IMPORTANT]  
>  Los sitios y clientes de Configuration Manager que se ejecutan en máquinas virtuales de Azure están sujetos a los mismos requisitos de licencia que las instalaciones locales.  



<!--HONumber=Jan17_HO2-->


