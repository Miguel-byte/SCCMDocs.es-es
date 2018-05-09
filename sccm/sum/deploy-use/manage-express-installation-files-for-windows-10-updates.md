---
title: Administración de archivos de instalación rápida para actualizaciones de Windows 10
titleSuffix: Configuration Manager
description: Configuration Manager admite archivos de instalación rápida para Windows 10, que proporciona descargas más pequeñas y tiempos de instalación más rápidos en los clientes.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/24/2017
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: b8d8af88-e8ac-4deb-921b-975e2d2afd80
ms.openlocfilehash: 4ca7a6c37137e266d719b76532b4131a6c43d4de
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="manage-express-installation-files-for-windows-10-updates"></a>Administración de archivos de instalación rápida para actualizaciones de Windows 10
A partir de la versión 1702, Configuration Manager admite archivos de instalación rápida para las actualizaciones de Windows 10. Cuando use una versión compatible con Windows 10, puede usar las opciones de cliente de Configuration Manager para configurar el cliente de manera que descargue solo los cambios entre la actualización acumulativa de Windows 10 del mes actual y la actualización del mes anterior. Sin los archivos de instalación rápida, los clientes de Configuration Manager descargan cada mes la actualización acumulativa completa de Windows 10 (incluidas todas las actualizaciones de los meses anteriores). Usar los archivos de instalación rápida proporciona descargas más pequeñas y tiempos de instalación más rápidos en los clientes.

> [!IMPORTANT]
> Aunque la configuración para admitir el uso de los archivos de instalación rápida está disponible en la versión 1702 de Configuration Manager, la compatibilidad con clientes del sistema operativo está disponible en la versión 1607 de Windows 10 con una actualización del Agente de Windows Update. Esta actualización se incluye con las actualizaciones publicadas el 11 de abril de 2017, Patch Tuesday (segundo martes de cada mes). Para obtener más información sobre estas actualizaciones, vea el [artículo de soporte técnico 4015217](http://support.microsoft.com/kb/4015217). Las actualizaciones futuras se beneficiarán de la instalación rápida para descargas más pequeñas. La versión 1607 de Windows 10 sin la actualización y las versiones anteriores no admiten los archivos de instalación rápida.


### <a name="to-enable-the-download-of-express-installation-files-for-windows-10-updates"></a>Para habilitar la descarga de archivos de instalación rápida para las actualizaciones de Windows 10
Para iniciar la sincronización de los metadatos de los archivos de instalación rápida de Windows 10, debe habilitarlos en las propiedades de punto de actualización de software.
1.  En la consola de Configuration Manager, vaya a **Administración** > **Configuración del sitio** > **Sitios**.
2.  Seleccione el sitio de administración central o el sitio primario independiente.
3.  En la pestaña **Inicio** , en el grupo **Configuración** , haga clic en **Configurar componentes de sitio**y, a continuación, haga clic en **Punto de actualización de software**. En la pestaña **Archivos de actualización**, seleccione **Download both full files for all approved updates and express installation files for Windows 10** (Descargar archivos completos para todas las actualizaciones aprobadas y archivos de instalación rápida de Windows 10).

> [!NOTE]    
> El componente Punto de actualización de software no se puede configurar para descargar solo actualizaciones rápidas.  La descarga de archivos de instalación rápida se realizará aparte de la de archivos completos y, por tanto, aumentará la cantidad de contenido que se distribuye y almacena en los puntos de distribución.

### <a name="to-enable-support-for-clients-to-download-and-install-express-installation-files"></a>Para habilitar la compatibilidad para que los clientes descarguen e instalen archivos de instalación rápida
Para habilitar la compatibilidad de los archivos de instalación rápida en los clientes, debe habilitar los archivos de instalación rápida en la sección Actualizaciones de software de la configuración de cliente. Esto crea una nueva escucha HTTP que escucha las solicitudes para descargar los archivos de instalación rápida en el puerto que especifique.

> [!NOTE]    
> Se trata de un puerto local que los clientes usarán para escuchar solicitudes de Optimización de distribución (DO) o Servicio de transferencia inteligente en segundo plano (BITS) para descargar contenido rápido desde el punto de distribución. No es necesario abrir este puerto en firewalls, pues todo el tráfico se encuentra en el equipo local.

Una vez que implemente la configuración de cliente para habilitar esta característica en el cliente, intentará descargar la diferencia entre la actualización acumulativa de Windows 10 del mes actual y la actualización del mes anterior (los clientes deben ejecutar una versión de Windows 10 que admita los archivos de instalación rápida).
1.  Habilite la compatibilidad para los archivos de instalación rápida en las propiedades de componente de punto de actualización de software (procedimiento anterior).
2.  En la consola de Configuration Manager, vaya a **Administración** > **Configuración de cliente**.
3.  Seleccione la configuración de cliente adecuada y, después, en la pestaña **Inicio**, haga clic en **Propiedades**.
4.  Seleccione la página **Actualizaciones de software**, configure **Sí** para la opción **Enable installation of Express Updates on clients (Habilitar la instalación de actualizaciones rápidas en clientes)** y configure el puerto que ha usado la escucha HTTP en el cliente para la opción **Port used to download content for Express Updates (Puerto usado para descargar el contenido de las actualizaciones rápidas)**.
