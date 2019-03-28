---
title: Notificación de cliente
titleSuffix: Configuration Manager
description: Administra clientes al tomar medidas inmediatas desde la consola central de Configuration Manager.
ms.date: 03/19/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: deb8aac8-2bd9-4980-a25b-5f8d93051226
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 39135a1fa548c83e0ba9c7d2a98cf1e925217280
ms.sourcegitcommit: f38ef9afb0c608c0153230ff819e5f5e0fb1520c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/19/2019
ms.locfileid: "58197034"
---
# <a name="client-notification-in-configuration-manager"></a>Notificación de cliente de Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Para tomar medidas inmediatas en clientes remotos, envíe una acción de notificación de cliente desde la consola de Configuration Manager. Tome estas medidas en un dispositivo individual o en una colección de dispositivos. 



## <a name="actions"></a>Acciones

Las siguientes acciones están en la cinta, en el grupo Dispositivo o Colección de la pestaña Inicio. 


### <a name="install-client"></a>Instalar cliente

Se abre el **Asistente para la instalación de cliente**. Este asistente usa la instalación de inserción de cliente para instalar un cliente de Configuration Manager. Para obtener más información, vea [Instalación de inserción de cliente](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientPush).

#### <a name="permissions"></a>Permisos
Esta acción requiere los permisos **Modificar recurso** y **Leer** en el objeto **Colección**. 

Los siguientes roles integrados tienen estos permisos de forma predeterminada:
- Administrador de aplicaciones  
- Administrador total  
- Administrador de infraestructuras  
- Administrador de operaciones  
- Administrador de implementaciones del sistema operativo  

Agregue estos permisos a los roles personalizados que necesitan insertar el cliente.


### <a name="run-script"></a>Ejecutar script

Se abre el Asistente para **ejecutar script** para ejecutar un script de PowerShell en todos los clientes de la recopilación. Para obtener más información, consulte [Creación y ejecución de scripts de PowerShell](/sccm/apps/deploy-use/create-deploy-scripts).

#### <a name="permissions"></a>Permisos
Esta acción requiere el permiso **Ejecutar script** en el objeto **Colección**. 

Los siguientes roles integrados tienen este permiso de forma predeterminada:
- Administrador total  
- Administrador de infraestructuras  
- Administrador de operaciones  

Agregue este permiso a cualquier rol personalizado que deba ejecutar scripts.


### <a name="start-cmpivot"></a>Iniciar CMPivot

Inicia **CMPivot**, que ejecuta consultas en tiempo real en los dispositivos de destino. Para obtener más información, vea [CMPivot](/sccm/core/servers/manage/cmpivot).

#### <a name="permissions"></a>Permisos
Esta acción requiere los mismos permisos que la acción [Ejecutar script](#run-script). 



## <a name="client-notification"></a>Notificación de cliente

Las siguientes acciones están en el menú **Notificación de cliente**, en la cinta, en el grupo Dispositivo o Colección de la pestaña Inicio.

En la versión 1806 o anterior, la opción **Notificación de cliente** solo está disponible en el nodo Colección de dispositivos o cuando veía la pertenencia de una colección de dispositivos. A partir de la versión 1810, puede iniciar una **Notificación de cliente** directamente desde el nodo **Dispositivos**. Ya no es requisito estar dentro de la vista de la pertenencia a una colección. <!--SCCMDocs-pr issue 2972-->

#### <a name="permissions"></a>Permisos
<!--SCCMDocs-pr issue #2972-->
A partir de la versión 1810, las acciones de notificación de cliente requieren el permiso **Notificar al recurso** en el objeto Colección. Este permiso se aplica a todas las acciones del menú **Notificación de cliente**. 

Los siguientes roles integrados tienen este permiso de forma predeterminada:
- Administrador total  
- Administrador de infraestructuras  

Agregue este permiso a cualquier rol personalizado que deba usar acciones de notificación de cliente.


### <a name="download-computer-policy"></a>Descargar directiva de equipo

Actualiza la directiva de dispositivo. Para obtener más información, vea [Iniciar la recuperación de directivas para un cliente de Configuration Manager](/sccm/core/clients/manage/manage-clients#BKMK_PolicyRetrieval).  


### <a name="download-user-policy"></a>Descargar directiva de usuario

Actualiza la directiva de usuario.  


### <a name="collect-discovery-data"></a>Recopilar datos de detección

Desencadena clientes para enviar un registro de datos de detección (DDR). Para obtener más información, vea [Heartbeat Discovery](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutHeartbeat) (Detección de latidos).  


### <a name="collect-software-inventory"></a>Recopilar inventario de software

Desencadena clientes para ejecutar un ciclo de inventario de software. Para obtener más información, vea [Introducción al inventario de software](/sccm/core/clients/manage/inventory/introduction-to-software-inventory).  


### <a name="collect-hardware-inventory"></a>Recopilar información de inventario de hardware

Desencadena clientes para ejecutar un ciclo de inventario de hardware. Para obtener más información, vea [Introducción al inventario de hardware](/sccm/core/clients/manage/inventory/introduction-to-hardware-inventory).  


### <a name="evaluate-application-deployments"></a>Evaluar implementaciones de aplicaciones

Desencadena clientes para ejecutar un ciclo de evaluación de implementación de aplicaciones. Para obtener más información, vea [Programar la reevaluación para implementaciones](/sccm/core/clients/deploy/about-client-settings#schedule-re-evaluation-for-deployments).  


### <a name="evaluate-software-update-deployments"></a>Evaluar implementaciones de actualizaciones de software

Desencadena clientes para ejecutar un ciclo de evaluación de implementación de actualizaciones de software. Para obtener más información, vea [Introducción a las actualizaciones de software](/sccm/sum/understand/software-updates-introduction).  


### <a name="switch-to-the-next-software-update-point"></a>Cambiar al siguiente punto de actualización de software

Desencadena clientes para cambiar al siguiente punto de actualización de software disponible. Para obtener más información, vea [Cambio de punto de actualización de software](/sccm/sum/plan-design/plan-for-software-updates#BKMK_SUPSwitching).  


### <a name="evaluate-device-health-attestation"></a>Evaluar Atestación de estado de dispositivo

Desencadena clientes de Windows 10 para comprobar y enviar su estado de dispositivo más reciente. Para más información, vea [Atestación de estado](/sccm/core/servers/manage/health-attestation).  


### <a name="check-conditional-access-compliance"></a>Comprobar cumplimiento de acceso condicional

Desencadena clientes para comprobar su cumplimiento con el acceso condicional. Para obtener más información, consulte [Administrar el acceso a servicios de Office 365 para equipos administrados por System Center Configuration Manager](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm).  


### <a name="wake-up"></a>Reactivar

A partir de la versión 1810, desencadena dispositivos en modo suspensión para volver al estado de potencia completa.


### <a name="restart"></a>Reiniciar

Desencadena los dispositivos seleccionados para que se reinicien. 



## <a name="endpoint-protection"></a>Endpoint Protection

Las siguientes acciones están en el menú **Endpoint Protection**. Este menú se encuentra en la cinta, en el grupo Colección de la pestaña Inicio. Cuando se seleccionan uno o más dispositivos, estas acciones pasan a la pestaña **Objeto seleccionado** de la cinta.

Para obtener más información, vea [Endpoint Protection en Configuration Manager](/sccm/protect/deploy-use/endpoint-protection).

#### <a name="permissions"></a>Permisos
Esta acción requiere el permiso **Aplicar seguridad** en el objeto **Colección**. 

Los siguientes roles integrados tienen este permiso de forma predeterminada:
- Administrador total  
- Endpoint Protection Manager  
- Administrador de operaciones  

Agregue este permiso a cualquier rol personalizado que deba desencadenar acciones de Endpoint Protection.


### <a name="full-scan"></a>Examen completo

Desencadena Endpoint Protection o Windows Defender para ejecutar un examen antimalware *completo*.  


### <a name="quick-scan"></a>Examen rápido

Desencadena Endpoint Protection o Windows Defender para ejecutar un examen antimalware *rápido*.  


### <a name="download-definition"></a>Descargar definición

Desencadena Endpoint Protection o Windows Defender para descargar las últimas definiciones de antimalware.  



## <a name="see-also"></a>Consulte también

- [Cómo administrar clientes](/sccm/core/clients/manage/manage-clients)
- [Cómo administrar recopilaciones](/sccm/core/clients/manage/collections/manage-collections)
