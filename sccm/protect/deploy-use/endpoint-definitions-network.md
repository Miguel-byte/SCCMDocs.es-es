---
title: Definiciones de malware de Endpoint Protection desde un recurso compartido de red
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo descargar manualmente las últimas actualizaciones de definiciones de Microsoft y, luego, configurar los clientes para que descarguen estas definiciones.
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: ddef4d2a-f481-4020-9ddd-9cca5f9795cb
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 47c6a046dac7cd4b5d0d16f0342d7e95ba3cc2a0
ms.sourcegitcommit: 4f05517f7b284696a492a1b184cc5f25c5cda5e6
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/09/2018
ms.locfileid: "48891153"
---
# <a name="enable-endpoint-protection-malware-definitions-to-download-from-a-network-share-for-configuration-manager"></a>Habilitar la descarga de definiciones de malware de Endpoint Protection desde un recurso compartido de red para Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

 Puede descargar manualmente las últimas actualizaciones de definiciones de Microsoft y luego configurar los clientes para que descarguen estas definiciones desde una carpeta compartida en la red. Los usuarios también pueden iniciar las actualizaciones de definiciones si se usa este origen de actualización.

> [!NOTE]
>  Los clientes deben tener acceso de lectura a la carpeta compartida para poder descargar actualizaciones de definiciones.

 Para obtener más información sobre cómo descargar las actualizaciones de definiciones y motores para su almacenamiento en el recurso compartido de archivos, consulte [Install the latest Microsoft antimalware and antispyware software](https://www.microsoft.com/wdsi/definitions) (Instalar el software antimalware y antispyware más reciente de Microsoft).

## <a name="to-configure-definition-downloads-from-a-file-share"></a>Para configurar las descargas de definiciones desde un recurso compartido de archivos

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad**.

2.  En el área de trabajo **Activos y compatibilidad** , expanda **Endpoint Protection**y haga clic en **Directivas antimalware**.

3.  Abra la página de propiedades de la **Directiva antimalware predeterminada** o cree una nueva. Para obtener más información sobre cómo crear directivas antimalware, consulte [How to create and deploy antimalware policies for Endpoint Protection in System Center Configuration Manager](endpoint-antimalware-policies.md) (Cómo crear e implementar directivas antimalware para Endpoint Protection en System Center Configuration Manager).

4.  En la sección **Actualizaciones de definiciones** del cuadro de diálogo de propiedades de antimalware, haga clic en **Orígenes**.

5.  En el cuadro de diálogo **Configurar orígenes de actualización de definiciones** , seleccione **Actualizaciones desde recursos compartidos de archivos UNC**.

6.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Configurar orígenes de actualización de definiciones** .

7.  Haga clic en **Rutas de acceso**. A continuación, en el cuadro de diálogo **Configurar rutas de acceso UNC de actualización de definiciones** , agregue una o varias rutas de acceso UNC a la ubicación de los archivos de actualizaciones de definiciones en un recurso compartido de red.

8.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Configurar rutas de acceso UNC de actualización de definiciones** .


> [!div class="button"]
[Paso siguiente >](endpoint-antimalware-policies.md)

> [!div class="button"]
[Atrás >](endpoint-configure-alerts.md)
