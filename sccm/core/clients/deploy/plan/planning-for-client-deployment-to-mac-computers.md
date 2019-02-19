---
title: Planeamiento de la implementación del cliente en equipos Mac
titleSuffix: Configuration Manager
description: Planee la implementación de cliente en equipos Mac en System Center Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 8d15ae3f-de42-461f-a907-c43873da22d2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: fe9c5a22f1c3a17737ccfb452b3cd4dd418bf9a9
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56142466"
---
# <a name="planning-for-client-deployment-to-mac-computers-in-system-center-configuration-manager"></a>Planeamiento de la implementación de cliente en equipos Mac en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Puede instalar el cliente de Configuration Manager en equipos Mac que ejecuten el sistema operativo Mac OS X y usen las siguientes capacidades de administración:  

- **Inventario de hardware**  

   Es posible usar el inventario de hardware de Configuration Manager para recopilar información sobre el hardware y las aplicaciones instaladas en los equipos Mac. Entonces, esta información puede verse en el explorador de recursos de la consola de Configuration Manager y usarse para crear recopilaciones, consultas e informes. Para obtener más información, consulte [Cómo usar el Explorador de recursos para ver el inventario de Hardware en Configuration Manager](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md).  

   Configuration Manager recopila la siguiente información de hardware de los equipos Mac:  

  -   Procesador  

  -   Sistema de equipo  

  -   Unidad de disco  

  -   Partición de disco  

  -   Adaptador de red  

  -   Sistema operativo  

  -   Servicio  

  -   Proceso  

  -   Software instalado  

  -   Producto de sistema del equipo  

  -   Controladora USB  

  -   Dispositivo USB  

  -   Unidad de CD-ROM  

  -   Controladora de vídeo  

  -   Monitor de escritorio  

  -   Batería portátil  

  -   Memoria física  

  -   Impresora  

  > [!IMPORTANT]  
  >  No se puede extender la información del hardware que se recopila de equipos Mac durante el inventario de hardware.  

- **Configuración de cumplimiento**  

   Puede usar la configuración de cumplimiento de Configuration Manager para ver la compatibilidad y corregir la configuración de preferencias (.plist) de Mac OS X. Por ejemplo, puede aplicar la configuración para la página principal en el explorador web Safari o asegurarse de que el firewall de Apple está habilitado. También puede utilizar scripts de shell para supervisar y corregir la configuración en MAC OS X.  

- **Administración de aplicaciones**  

   Configuration Manager puede implementar software en equipos Mac. Es posible implementar los siguientes formatos de software en equipos Mac:  

  -   Imagen de disco Apple (.DMG)  

  -   Archivo de paquete Meta (.MPKG)  

  -   Paquete de instalador de Mac OS X (.PKG)  

  -   Aplicación de Mac OSX (.APP)  

  Al instalar el cliente de Configuration Manager en equipos Mac, no se pueden usar las siguientes capacidades de administración admitidas por el cliente de Configuration Manager en equipos basados en Windows:  

- Instalación de inserción de cliente  

- Implementación de sistema operativo  

- Actualizaciones de software  

  > [!NOTE]  
  >  Puede usar la administración de aplicaciones de Configuration Manager para implementar las actualizaciones de software de Mac OS X necesarias en equipos Mac. Además, puede utilizar la configuración de compatibilidad para asegurarse de que los equipos tengan las actualizaciones de software necesarias.  

- Ventanas de mantenimiento  

- Control remoto  

- Administración de energía  

- Comprobación y corrección de cliente del estado de cliente  

  Para obtener más información sobre cómo instalar y configurar el cliente Mac de Configuration Manager, consulte [Cómo implementar clientes en equipos Mac con System Center Configuration Manager](../../../../core/clients/deploy/deploy-clients-to-macs.md).
