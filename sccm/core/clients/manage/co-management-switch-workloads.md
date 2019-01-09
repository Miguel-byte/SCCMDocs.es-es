---
title: Cambiar las cargas de trabajo de Configuration Manager a Intune
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo cambiar las cargas de trabajo que administra actualmente Configuration Manager a Microsoft Intune.
ms.prod: configuration-manager
ms.technology: configmgr-client
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 12/10/2018
ms.topic: conceptual
ms.assetid: 60e2022f-a4f9-40dd-af01-9ecb37b43878
ms.openlocfilehash: e3bd3bfda92fb877bac3ca68dbecf8b4a4078d4d
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2018
ms.locfileid: "53416952"
---
# <a name="switch-configuration-manager-workloads-to-intune"></a>Cambiar las cargas de trabajo de Configuration Manager a Intune

Después de [preparar los dispositivos Windows 10 para la administración conjunta](/sccm/core/clients/manage/co-management-prepare), el paso siguiente consiste en habilitar la inscripción de cliente automática en Intune. Después, cuando esté listo, empiece a trasladar cargas de trabajo específicas de Configuration Manager a Intune. 


## <a name="setup-co-management"></a>Configuración de la administración conjunta

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Servicios en la nube** y seleccione el nodo **Administración conjunta**.  

2. En la pestaña **Inicio** de la cinta, en el grupo **Administrar**, haga clic en  **Configurar administración conjunta**. Esta acción abre al Asistente para la configuración de administración conjunta.  

3. En la página de suscripción, seleccione **Iniciar sesión**. Inicie sesión en su inquilino de Intune y después haga clic en **Siguiente**.  

4. En la página Habilitación, elija **Piloto** o **Todo**.  

    Esta acción permite la inscripción de cliente automática en Intune. Si elige **Piloto**, solo los clientes de Configuration Manager que sean miembros de la colección piloto se inscribirán de forma automática en Intune. Esta opción permite habilitar la administración conjunta en un subconjunto de los clientes para probarla inicialmente e implementarla con un enfoque por fases.  

    Use la línea de comandos que se muestra para implementar el cliente de Configuration Manager como una aplicación en Intune para los dispositivos ya inscritos en Intune. Para obtener más información, vea [Dispositivos de Windows 10 inscritos en Intune](/sccm/core/clients/manage/co-management-prepare#windows-10-devices-enrolled-in-intune).  

5. En la página Cargas de trabajo, elija si quiere cambiar las cargas de trabajo de Configuration Manager para que las administre Intune. Puede habilitar la inscripción en la página anterior sin tener que cambiar las cargas de trabajo en este momento. 

    El valor **Intune piloto** cambia la carga de trabajo asociada solo para los dispositivos de la colección Piloto. La configuración **Intune** cambia la carga de trabajo asociada para todos los dispositivos Windows 10 administrados conjuntamente.  

    > [!Important] 
    > Antes de cambiar las cargas de trabajo, asegúrese de que la carga de trabajo correspondiente en Intune se ha configurado e implementado correctamente. Asegúrese de que las cargas de trabajo siempre se administren mediante una de las herramientas de administración para los dispositivos.  

6. En la página Almacenamiento provisional, configure las opciones siguientes:  

    - **Piloto**: el grupo piloto contiene una o varias colecciones que seleccione. Use este grupo como parte de la implementación por fases de la administración conjunta. Comience con una colección de prueba pequeña y, luego, agregue más colecciones al grupo piloto a medida que implemente la administración conjunta en más usuarios y dispositivos. Puede cambiar las colecciones del grupo piloto en cualquier momento.  

    - **Production**: Configure el **grupo de exclusión** con una o varias colecciones. Los dispositivos que forman parte de cualquiera de las colecciones de este grupo se excluyen del uso de la administración conjunta.  

7. Para habilitar la administración conjunta, siga los pasos del asistente.  

<!--1357377--> A partir de la versión 1806 de Configuration Manager, cuando se cambia una carga de trabajo de administración compartida, los dispositivos administrados conjuntamente sincronizan automáticamente la directiva MDM de Microsoft Intune. Esta sincronización también se produce al iniciar la acción **Descargar directiva de equipo** desde Notificaciones de cliente en la consola de Configuration Manager. Para obtener más información, vea [Iniciar la recuperación de directivas de cliente mediante la notificación de cliente](/sccm/core/clients/manage/manage-clients#initiate-client-policy-retrieval-using-client-notification).



## <a name="modify-your-co-management-settings"></a>Modificación de la configuración de administración conjunta

Después de habilitar la administración conjunta con el asistente, modifique la configuración en las propiedades de administración conjunta. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Servicios en la nube** y seleccione el nodo **Administración conjunta**. Seleccione el objeto de administración conjunta y, después, haga clic en **Propiedades** en la cinta. 



## <a name="supported-workloads"></a>Cargas de trabajo compatibles

Las cargas de trabajo siguientes están disponibles actualmente para cambiar de Configuration Manager a Intune:

- **Directivas de cumplimiento de dispositivos**  

- **Directivas de acceso a recursos**: Para obtener más información sobre estas directivas de Intune, vea [Perfiles de dispositivo de Microsoft Intune](https://docs.microsoft.com/intune/device-profiles).
    - Perfil de correo electrónico  
    - Perfil de Wi-Fi  
    - Perfil de VPN  
    - Perfil de certificado  

- **Directivas de Windows Update**  

- **Endpoint Protection**: A partir de la versión 1802 de Configuration Manager, esta carga de trabajo incluye las características siguientes:  
    - Protección de aplicaciones de Windows Defender  
    - Firewall de Windows Defender  
    - SmartScreen de Windows Defender  
    - Cifrado de Windows  
    - Windows Defender Exploit Guard  
    - Control de aplicaciones de Windows Defender  
    - Centro de seguridad avanzada de Windows Defender  
    - Protección contra amenazas avanzada de Windows Defender  
    - Windows Information Protection  

- **Configuración del dispositivo**: A partir de la versión 1806 de Configuration Manager<!--1357903-->:  

    - al mover la carga de trabajo de configuración de dispositivo también se mueven las cargas de trabajo **Acceso a los recursos** y **Endpoint Protection**.  

    - Todavía puede implementar la configuración de Configuration Manager en los dispositivos administrados conjuntamente, aunque Intune sea la autoridad de configuración de dispositivos. Esta excepción podría utilizarse para definir la configuración que necesita su organización, pero aún no está disponible en Intune. Especifique esta excepción en una [línea de base de configuración de Configuration Manager](/sccm/compliance/deploy-use/create-configuration-baselines). Habilite la opción **Always apply this baseline even for co-managed clients** (Aplicar siempre esta línea de base incluso para los clientes conjuntamente administrados) al crear la línea de base, o en la pestaña **General** de las propiedades de una línea de base existente.  

- **Aplicaciones Hacer clic y ejecutar de Office 365**: A partir de la versión 1806 de Configuration Manager<!--1357841-->:  

    - Después de mover la carga de trabajo, la aplicación se muestra en el **Portal de empresa** en el dispositivo.  

    - Las actualizaciones de Office pueden tardar aproximadamente 24 horas en aparecer en el cliente a menos que se reinicien los dispositivos.  

    - Hay una nueva condición global, **¿Las aplicaciones de Office 365 están administradas por Intune en este dispositivo?** Esta condición se agrega de forma predeterminada como requisito a las nuevas aplicaciones de Office 365. Cuando se realiza la transición de esta carga de trabajo, los clientes con administración conjunta no cumplen el requisito en la aplicación. Por tanto, no instalan Office 365 implementado a través de Configuration Manager.  

- **Aplicaciones cliente**: A partir de la versión 1806 de Configuration Manager como una [característica de versión preliminar](/sccm/core/servers/manage/pre-release-features))<!--1357892-->:  

    - después de realizar la transición de esta carga de trabajo, las aplicaciones disponibles implementadas desde Intune están disponibles en el Portal de empresa.  

    - Las aplicaciones implementadas desde Configuration Manager están disponibles en el Centro de software.  



## <a name="monitor-co-management"></a>Supervisión de la administración conjunta

Después de habilitar la administración conjunta, los dispositivos de administración conjunta se supervisan con los métodos siguientes:

- [Panel de administración conjunta](/sccm/core/clients/manage/co-management-dashboard)  

- **Vista SQL y clase WMI**: consulte la vista SQL **v_ClientCoManagementState** en la base de datos de sitio de Configuration Manager o en la clase WMI **SMS_Client_ComanagementState**. Con la información de la clase WMI, puede crear recopilaciones personalizadas en Configuration Manager para ayudar a determinar el estado de la implementación de la administración compartida. Para obtener más información, consulte [Cómo crear recopilaciones](/sccm/core/clients/manage/collections/create-collections). Los campos siguientes están disponibles en la vista SQL y la clase WMI:  
  - **MachineId**: especifica un identificador de dispositivo único para el cliente de Configuration Manager.  
  - **MDMEnrolled**: especifica si el dispositivo está inscrito en MDM.  
  - **Authority**: especifica la entidad para la que el dispositivo está inscrito.  
  - **ComgmtPolicyPresent**: especifica si la directiva de administración conjunta de Configuration Manager existe en el cliente. Si el valor de **MDMEnrolled** es **0**, el dispositivo no se administra conjuntamente con independencia de si la directiva de administración conjunta existe en el cliente.  

    > [!Note]  
    > Un dispositivo se administra conjuntamente cuando los campos **MDMEnrolled** y **ComgmtPolicyPresent** tienen un valor de **1**.  

- **Directivas de implementación**: en el nodo **Implementaciones** del área de trabajo **Supervisión** se crean dos directivas. Una es para el grupo piloto y otra para producción. Estas directivas solo informan del número de dispositivos donde Configuration Manager ha aplicado la directiva. No tienen en cuenta cuántos están inscritos en Intune, que es un requisito antes de que los dispositivos se puedan administrar conjuntamente.  



## <a name="check-compliance-for-co-managed-devices"></a>Comprobación del cumplimiento para los dispositivos administrados conjuntamente

Los usuarios pueden usar el Centro de software para comprobar el cumplimiento de sus dispositivos Windows 10 administrados conjuntamente, ya se administre el acceso condicional mediante Intune o Configuration Manager. Los usuarios también pueden comprobar el cumplimiento mediante la aplicación de Portal de empresa cuando se administra el acceso condicional mediante Intune.



## <a name="next-steps"></a>Pasos siguientes

Use los siguientes recursos para ayudarlo a administrar las cargas de trabajo que cambie a Intune:
- [Directivas de cumplimiento de dispositivos](https://docs.microsoft.com/intune/device-compliance-get-started)
- [Directivas de acceso a recursos](https://docs.microsoft.com/intune/device-profiles)
- [Directivas de Windows Update para empresas](https://docs.microsoft.com/intune/windows-update-for-business-configure)
- [Endpoint Protection para Microsoft Intune](https://docs.microsoft.com/intune-classic/deploy-use/help-secure-windows-pcs-with-endpoint-protection-for-microsoft-intune)
