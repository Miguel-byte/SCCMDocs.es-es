---
title: "Instalar un sitio con el medio de línea base 1606 | System Center Configuration Manager"
description: "Obtenga información sobre cómo usar el medio de línea base 1606 para instalar o actualizar sitios de System Center Configuration Manager."
ms.custom: na
ms.date: 10/12/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f4f9a5fd-f573-4b99-ad93-b2c76812e922
caps.latest.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 5e97fbcdc21022e98b4cbdb198273dfe544a561f
ms.openlocfilehash: 3df46a00f2208ffa687c8c99ce610266e206eef0


---
# <a name="install-and-upgrade-with-the-version-1606-baseline-media-for-system-center-configuration-manager"></a>Instalar y actualizar con el medio de línea base de la versión 1606 para System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual) (rama de mantenimiento a largo plazo)*

Use este tema para obtener información sobre la ejecución del programa de instalación de Configuration Manager cuando use el medio de línea base de la versión 1606 de Microsoft System Center 2016 o de una versión de System Center Configuration Manager (rama actual y rama de mantenimiento a largo plazo 1606). Puede usar este medio para instalar un nuevo sitio, o actualizar desde System Center 2012 Configuration Manager con Service Pack 2 o System Center 2012 R2 Configuration Manager con Service Pack 1. Durante la instalación, puede elegir si instala la rama actual o la rama de mantenimiento a largo plazo (LTSB).

Cuando use el medio de línea base de la versión 1606, el sitio que instala (o al que actualiza) es:
- **Un sitio de rama actual** que es equivalente a un sitio que se instaló primero mediante el medio de línea base 1511 y, después, se actualizó a la versión 1606 además del paquete acumulativo de revisiones 1606: KB3186654.
-   **Un sitio de LTSB** que es equivalente al sitio de rama actual que ejecuta la versión 1606 además del paquete acumulativo de revisiones 1606: KB3186654 (el medio de línea base ya incluye el paquete acumulativo de revisiones).  En cambio, la LTSB no admite todas las características o funcionalidades que están disponibles en la rama actual, como se detalla en [Introduction to the Long-Term Servicing Branch of System Center Configuration Manager (Introducción a la rama de mantenimiento a largo plazo de System Center Configuration Manager)](introduction-to-the-ltsb.md).

Si no está familiarizado con las diferentes ramas de System Center Configuration Manager, consulte [Which branch of Configuration Manager should I use (Qué rama de Configuration Manager debo usar)](which-branch-should-i-use.md).


## <a name="changes-to-setup-with-the-1606-baseline-media"></a>Cambios en la configuración con el medio de línea base 1606
El medio de línea base 1606 presenta los siguientes cambios en la instalación de Configuration Manager.

### <a name="branch-and-edition"></a>Rama y edición
Cuando ejecuta el programa de instalación, se le presenta una página de licencia donde puede seleccionar la rama de Configuration Manager que quiere instalar. Puede elegir la rama actual o la LTSB como una instalación con licencia, o puede elegir una edición de evaluación de la rama actual como una instalación sin licencia.

Para obtener más información, consulte [Licensing and branches for System Center Configuration Manager (Licencias y ramas para System Center Configuration Manager)](learn-more-editions.md).

### <a name="software-assurance-expiration"></a>Expiración de Software Assurance
Durante la instalación, tiene la opción de escribir la **fecha de expiración de Software Assurance**. Este es un valor opcional que puede especificar como un recordatorio útil.

> [!NOTE]
> Microsoft no valida la fecha de expiración que especifique y no la usará para la validación de la licencia.  En su lugar, puede usarla como un recordatorio de la fecha de expiración. Esto es útil porque Configuration Manager busca periódicamente nuevas actualizaciones de software que se ofrecen en línea, y el estado de su licencia de Software Assurance debe ser actual para que pueda usar estas actualizaciones adicionales.    

- Puede especificar el valor en la página **Clave de producto** del Asistente para instalación cuando ejecute el programa de instalación del medio de línea base de la versión 1606 de System Center Configuration Manager.
- También puede especificar esta fecha en la pestaña **Licencia** de **Propiedades de configuración de jerarquía** en la consola de Configuration Manager.

Para obtener más información, consulte *Contratos de Software Assurance* en [Licensing and branches for System Center Configuration Manager (Licencias y ramas para System Center Configuration Manager)](learn-more-editions.md).


### <a name="additional-pre-upgrade-configurations"></a>Configuraciones previas a la actualización adicionales
Antes de iniciar una actualización de System Center 2012 Configuration Manager a la LTSB, debe realizar los siguientes pasos adicionales como parte de la lista de comprobación previa a la actualización.  
Desinstalar los roles de sistema de sitio que no se admiten por la LTSB:
- Punto de sincronización de Asset Intelligence
- Conector de Microsoft Intune
- Puntos de distribución basados en la nube

Para obtener más información, consulte [Upgrade to System Center Configuration Manager (Actualizar a System Center Configuration Manager)](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager).


### <a name="new-scripted-install-options"></a>Nuevas opciones de instalación generadas por script
El medio de línea base de la versión 1606 admite una nueva clave de archivo de script desatendido para las instalaciones generadas por script de un sitio nuevo de nivel superior. Se aplica a la instalación de un nuevo sitio primario independiente o a la adición de un sitio de administración central como parte de un escenario de expansión de sitios.

Al usar un script desatendido para instalar una rama con licencia, debe agregar la siguiente sección, nombres de clave y valores a la sección Opciones de su script (no necesita usar estos valores para generar por script la instalación de una edición de evaluación de la rama actual):  

 **SABranchOptions**
-   **Nombre de clave: SSActive**
  - Valores: 0 o 1  
  - Detalles: 0 instala una edición de evaluación sin licencia de la rama actual y 1 instala una edición con licencia.   

- **CurrentBranch**
  - Valores: 0 o 1  
  - Detalles: 0 instala la rama de mantenimiento a largo plazo y 1 instala la rama actual.  

Por ejemplo, para instalar una edición de rama actual con licencia, usará:

  **Nombre de clave: SABranchOptions**
   -    **SSActive = 1**
   - **CurrentBranch = 1**
 

> [!IMPORTANT]  
> **SABranchOptions** solo funciona con el programa de instalación desde el medio de línea base. No se aplica cuando ejecuta el programa de instalación desde la carpeta CD.Latest de un sitio que ha instalado previamente mediante el medio de línea base de la versión 1606.
>
> **SABranchOptions** no se aplica a actualizaciones generadas por script de System Center 2012 Configuration Manager y siempre da como resultado la rama actual.

Para obtener más información, consulte [Usar una línea de comandos para instalar sitios de System Center Configuration Manager](/sccm/core/servers/deploy/install/use-a-command-line-to-install-sites).


## <a name="install-a-new-site"></a>Instalar un nuevo sitio
Cuando usa el medio de línea base 1606 para instalar un nuevo sitio de cualquier rama, use los procedimientos de instalación, preparación y planeación de sitios que se documentan en el tema [Installing System Center Configuration Manager sites (Instalación de sitios de System Center Configuration Manager)](/sccm/core/servers/deploy/install/installing-sites) además de las siguientes consideraciones sobre el programa de instalación:

- Durante la instalación, debe elegir la rama de Configuration Manager que quiere instalar, y puede especificar la información de su contrato de Software Assurance.
-   Nuevas opciones de instalación generadas por script

## <a name="expand-a-stand-alone-primary-site"></a>Expandir un sitio primario independiente
Puede expandir un sitio primario independiente que ejecuta la LTSB.  El proceso no es diferente del que se usó para un sitio de rama actual con una salvedad:

- Al instalar el nuevo sitio de administración central, debe usar el programa de instalación del medio de origen original que usó para instalar el sitio de LTSB. (No se admite para ejecutar el programa de instalación de la carpeta CD.Latest para este escenario).

Para obtener más información sobre la expansión de un sitio, consulte *Expandir un sitio primario independiente* en [Install a site using the Setup Wizard (Instalar un sitio mediante el asistente para instalación)](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites).

## <a name="upgrade-from-system-center-2012-configuration-manager"></a>Actualización desde System Center 2012 Configuration Manager
Cuando actualiza desde System Center 2012 Configuration Manager, usa los procedimientos de preparación y planeación del sitio como se documenta en el tema [Upgrade to System Center Configuration Manager (Actualizar a System Center Configuration Manager)](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager), pero con los siguientes cambios:

**Actualizar a la rama actual:**
- Durante el programa de instalación, debe elegir la rama actual, y puede especificar la información de su contrato de Software Assurance.
-   Nuevas opciones de instalación generadas por script

**Actualizar a la LTSB:**  
- Pasos adicionales para seguir en la lista de comprobación previa a la actualización
- Durante el programa de instalación, debe elegir la LTSB, y puede especificar la información de su contrato de Software Assurance.
- Solo puede actualizar un sitio que ejecute System Center 2012 Configuration Manager con Service Pack 2 o System Center 2012 R2 Configuration Manager con Service Pack 1.

### <a name="in-place-upgrade-paths-for-the-1606-baseline-media"></a>Rutas de actualización local para el medio de línea base 1606
Puede usar el medio de línea base 1606 para actualizar lo siguiente a una edición con licencia de System Center Configuration Manager:
- System Center 2012 Configuration Manager con Service Pack 2
- System Center 2012 R2 Configuration Manager con Service Pack 1

También puede usar este medio para actualizar una edición de evaluación sin licencia de la rama actual a una versión de licencia completa de la rama actual.

Este medio no admite la actualización de:
- Otras versiones de System Center 2012 Configuration Manager
- Configuration Manager 2007 o versiones anteriores
- Una instalación de versión candidata de System Center Configuration Manager

## <a name="about-the-cdlatest-folder-and-the-ltsb"></a>Sobre la carpeta CD.Latest y la LTSB
Lo siguiente son advertencias para usar el medio que Configuration Manager crea en la carpeta CD.Latest del servidor de sitio. Estas se aplican a sitios que ejecutan la LTSB: el medio de la carpeta CD.Latest es compatible con:
- Recuperación del sitio
- Mantenimiento del sitio
- Instalación de sitios primarios secundarios adicionales

El medio de la carpeta CD.Latest no es compatible con:  
- Instalación de un sitio de administración central como parte de un escenario de expansión de sitios.

Para obtener más información, consulte [la carpeta CD.Latest](/sccm/core/servers/manage/the-cd.latest-folder).

## <a name="backup-recovery-and-site-maintenance-for-the-ltsb"></a>Copia de seguridad, recuperación y mantenimiento de sitio para la LTSB
Para realizar una copia de seguridad, recuperar o ejecutar el mantenimiento de sitio que ejecuta la LTSB, use la guía y los procedimientos de [Backup and recovery for System Center Configuration Manager (Copia de seguridad y recuperación de System Center Configuration Manager)](/sccm/protect/understand/backup-and-recovery).  

Use el programa de instalación de Configuration Manager de la carpeta CD.Latest de la copia de seguridad de su sitio de LTSB.



<!--HONumber=Nov16_HO1-->

