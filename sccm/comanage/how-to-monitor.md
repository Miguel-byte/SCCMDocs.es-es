---
title: Supervisión de la administración conjunta
titleSuffix: Configuration Manager
description: Utilice el panel de administración conjunta para revisar información sobre los dispositivos administrados conjuntamente.
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e83a7b0d-b381-4b4a-8eca-850385abbebb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7c731692bc2277cc5ce97e079387b392ca09ff3e
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56755588"
---
# <a name="how-to-monitor-co-management-in-configuration-manager"></a>Cómo supervisar la administración conjunta en Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*


Después de habilitar la administración conjunta, los dispositivos de administración conjunta se supervisan con los métodos siguientes:

- [Panel de administración conjunta](#co-management-dashboard)  

- [Directivas de implementación](#deployment-policies)

- [Datos del dispositivo WMI](#wmi-device-data)



## <a name="co-management-dashboard"></a>Panel de administración conjunta

A partir de la versión 1802, vea un panel con información sobre la administración conjunta. El panel le ayudará a revisar los equipos que se administran conjuntamente en el entorno. Los gráficos ayudan a identificar los dispositivos que podrían requerir atención.<!--1356648-->

En la consola de Configuration Manager, vaya al área de trabajo **Supervisión** y haga clic en el nodo **Administración conjunta**.

A partir de la versión 1810, el panel de administración conjunta se ha mejorado con información más detallada. <!--1358980-->

![Captura de pantalla del panel de administración conjunta](media/co-management-dashboard.png)


### <a name="co-managed-devices"></a>Dispositivos administrados conjuntamente

*Se aplica a las versiones 1802 y 1806*

Muestra el porcentaje de dispositivos administrados conjuntamente en todo el entorno.

![Icono de los dispositivos administrados conjuntamente](media/co-management-dashboard/Percent-Co-managed-graph.PNG)


### <a name="client-os-distribution"></a>Distribución del sistema operativo cliente

*Se aplica a todas las versiones* 

Muestra el número de dispositivos cliente en función del sistema operativo por versión. Se usan las siguientes agrupaciones:  
- Windows 7 y 8.x  
- Windows 10 anterior a la versión 1709  
- Windows 10 1709 y versiones posteriores  

    > [!Tip]  
    > Windows 10, versión 1709 y versiones posteriores, es un requisito previo para la administración conjunta.  

Mantenga el puntero sobre una sección del gráfico para mostrar el porcentaje de dispositivos que forman parte de ese grupo de sistemas operativos.

![Icono de distribución del sistema operativo de cliente](media/co-management-dashboard/Co-management-OS-distribution-graph.PNG)


### <a name="co-management-status-donut"></a>Estado de la administración conjunta (anillo)

*Se aplica a las versiones 1802 y 1806*

Muestra el desglose de los dispositivos que se ejecutan correctamente o con error en las categorías siguientes:
- Se ejecuta correctamente, Unidos a Azure AD híbrido  
- Se ejecuta correctamente, Unido a Azure AD  
- Error: Error de inscripción automática  

Mantenga el puntero sobre una sección del gráfico para ver el porcentaje de los dispositivos en esa categoría. 

![Icono de estado (anillo) de administración conjunta](media/co-management-dashboard/Co-management-status-graph.PNG)

Seleccione una sección del gráfico para ver la lista de dispositivos de esa categoría.

![Lista de dispositivos de error de inscripción](media/co-management-dashboard/Enrollment-Failure_Device-List.PNG)


### <a name="co-management-status-funnel"></a>Estado de la administración conjunta (embudo)

*Se aplica a la versión 1810 y posteriores*

Un gráfico de embudo que muestra el número de dispositivos con los siguientes estados del proceso de inscripción:  
- Dispositivos aptos  
- Programado  
- Inscripción iniciada  
- Inscritos  

![Mosaico del estado de la administración conjunta (embudo)](media/co-management-dashboard/1358980-status-funnel.png)


### <a name="co-management-enrollment-status"></a>Estado de la inscripción de administración conjunta

*Se aplica a la versión 1810 y posteriores*

Muestra un desglose del estado de los dispositivos en las categorías siguientes:
- Se ejecuta correctamente, unido a Azure AD híbrido  
- Se ejecuta correctamente, unido a Azure AD  
- Inscribiendo, unido a Azure AD híbrido  
- Error, unido a Azure AD híbrido  
- Error, unido a Azure AD  
- Inicio de sesión de usuario pendiente  

Seleccione un estado del icono para explorar en profundidad una lista de dispositivos de ese estado.  

![Mosaico del estado de la inscripción de administración conjunta](media/co-management-dashboard/1358980-enrollment-status.png)


### <a name="workload-transition"></a>Transición de la carga de trabajo

*Se aplica a todas las versiones*

Muestra un gráfico de barras con el número de dispositivos que se han pasado a Microsoft Intune para las cargas de trabajo disponibles. 

La lista de las cargas de trabajo varía según la versión de Configuration Manager. Para obtener más información, vea [Cargas de trabajo que se pueden pasar a Intune](/sccm/comanage/workloads).

Mantenga el puntero sobre una sección del gráfico para ver el número de dispositivos que se ha pasado para la carga de trabajo. 

![Gráfico de barras de transición de la carga de trabajo](media/co-management-dashboard/Workload-Transition.PNG)


### <a name="enrollment-errors"></a>Errores de inscripción

*Se aplica a la versión 1810 y posteriores*

Esta tabla es una lista de errores de inscripción de dispositivos. Estos errores pueden proceder de los componentes MDM en Windows, el núcleo del sistema operativo de Windows o el cliente de Configuration Manager. 

Existen cientos de posibles errores. En la tabla siguiente se enumera los errores más comunes.
<!-- SCCMDocs issue 1064, BUG 3158555 -->

| Error | Descripción |
|---------|---------|
| 2147549183 (0x8000FFFF) | Inscripción de MDM no se ha configurado todavía en Azure AD, o la inscripción no se espera la dirección URL.<br><br>[Habilitar la inscripción automática de Windows 10](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment) |
| 2149056536 (0x80180018)<br>MENROLL_E_USERLICENSE | Licencia de usuario está en la inscripción bloqueo de mal estado<br><br>[Asignar licencias a usuarios](https://docs.microsoft.com/intune/licenses-assign) |
| 2149056555 (0x8018002B)<br>MENROLL_E_MDM_NOT_CONFIGURED | Cuando se intenta automáticamente inscribirlo en Intune, pero totalmente no se aplica la configuración de Azure AD. Este problema debe ser transitorio, como los reintentos del dispositivo tras un breve período. |
| 2149056554 (0 x 8018002A)<br>&nbsp; | El usuario canceló la operación<br><br>Si la inscripción de MDM requiere autenticación multifactor y el usuario no ha iniciado sesión con un segundo factor compatible, Windows muestra una notificación al usuario a inscribir. Si el usuario no responde para la notificación del sistema, se produce este error. Este problema debe ser transitorio, como Configuration Manager vuelva a intentar y pedir al usuario. Los usuarios deben utilizar la autenticación multifactor cuando inicie sesión en Windows. También Edúquelos espera este comportamiento y si se le solicita, tomar medidas. | 
| 2149056533 (0x80180015)<br>MENROLL_E_NOTSUPPORTED | Administración de dispositivos móviles que generalmente no se admiten | 
| 2149056514 (0x80180002)<br>MENROLL_E_DEVICE_AUTHENTICATION_ERROR | Servidor no pudo autenticar al usuario<br><br> No hay ningún token de Azure AD para el usuario. Asegúrese de que el usuario puede autenticarse en Azure AD. |
| 2147942450 (0 x 80070032)<br>&nbsp; | Solo se admite la inscripción automática de MDM en Windows RS3 y versiones posteriores.<br><br>Asegúrese de que el dispositivo cumple con la [requisitos mínimos](/sccm/comanage/overview#windows-10) para la administración conjunta. |
| 3400073293 | Respuesta de cuenta de dominio Kerberos ADAL de usuario desconocido<br><br>Compruebe la configuración de Azure AD y asegúrese de que los usuarios pueden autenticarse correctamente. | 
| 3399548929 | Necesita inicio de sesión de usuario<br><br>Este problema debería ser transitorio. Se produce cuando el usuario rápidamente cierra antes de que ocurra la tarea de inscripción. | 
| 3400073236 | Error de solicitud de token de seguridad ADAL.<br><br>Compruebe la configuración de Azure AD y asegúrese de que los usuarios pueden autenticarse correctamente. |
| 2149122477 | Problema HTTP genérico |
| 3400073247 | Solo se admite la autenticación de Windows integrada de ADAL en flujo federado<br><br>[Planee la implementación de hybrid Azure Active Directory join](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan) | 
| 3399942148 | No se encontró el servidor o proxy.<br><br>Este problema debe ser transitorio, cuando el cliente no puede comunicarse con la nube. Si persiste, asegúrese de que el cliente tiene una conectividad coherente y en Azure. | 
| 2149056532 | No se admite la plataforma específica o una versión<br><br>Asegúrese de que el dispositivo cumple con la [requisitos mínimos](/sccm/comanage/overview#windows-10) para la administración conjunta. |
| 2147943568 | No se encontró un elemento<br><br>Este problema debería ser transitorio. Si persiste, póngase en contacto con Microsoft Support. |
| 2192179208 | No hay suficientes recursos de memoria están disponibles para procesar este comando.<br><br>Este problema debería ser transitorio, debe solucionar por sí solo cuando el cliente lo reintenta. |
| 3399614467 | Error de concesión de autorización de ADAL para esta aserción<br><br>Compruebe la configuración de Azure AD y asegúrese de que los usuarios pueden autenticarse correctamente. |
| 2149056517 | Error genérico de servidor de administración, por ejemplo, error de acceso de la base de datos<br><br>Este problema debería ser transitorio. Si persiste, póngase en contacto con Microsoft Support. |
| 2149134055 | No puede resolver el nombre de WinHTTP<br><br>El cliente no puede resolver el nombre del servicio. Compruebe la configuración de DNS. | 
| 2149134050 | tiempo de espera de Internet<br><br>Este problema debe ser transitorio, cuando el cliente no puede comunicarse con la nube. Si persiste, asegúrese de que el cliente tiene una conectividad coherente y en Azure. | 


Para obtener más información, consulte [valores de Error de registro de MDM](https://docs.microsoft.com/windows/desktop/mdmreg/mdm-registration-constants).



## <a name="deployment-policies"></a>Directivas de implementación

en el nodo **Implementaciones** del área de trabajo **Supervisión** se crean dos directivas. Una es para el grupo piloto y otra para producción. Estas directivas solo informan del número de dispositivos donde Configuration Manager ha aplicado la directiva. No tienen en cuenta cuántos están inscritos en Intune, que es un requisito antes de que los dispositivos se puedan administrar conjuntamente.  



## <a name="wmi-device-data"></a>Datos del dispositivo WMI

Consulta el **SMS_Client_ComanagementState** clase WMI. Puede crear colecciones personalizadas en Configuration Manager, que ayudan a determinar el estado de la implementación de administración conjunta. Para obtener más información sobre cómo crear colecciones personalizadas, vea [cómo crear recopilaciones](/sccm/core/clients/manage/collections/create-collections). 

Los campos siguientes están disponibles en la clase WMI:  

- **MachineId**: Un identificador de dispositivo único para el cliente de Configuration Manager  

- **MDMEnrolled**: especifica si el dispositivo está inscrito en MDM.  

- **Authority**: La autoridad para el que el dispositivo está inscrito  

- **ComgmtPolicyPresent**: especifica si la directiva de administración conjunta de Configuration Manager existe en el cliente. Si el valor de **MDMEnrolled** es **0**, el dispositivo no se administra conjuntamente con independencia de si la directiva de administración conjunta existe en el cliente.  

Un dispositivo se administra conjuntamente cuando los campos **MDMEnrolled** y **ComgmtPolicyPresent** tienen un valor de **1**.  
