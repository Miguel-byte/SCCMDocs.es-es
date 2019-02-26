---
title: Tutorial&#58; ruta de acceso de administración conjunta 1
titleSuffix: Configuration Manager
description: Configurar administración conjunta con Microsoft Intune cuando ya administra dispositivos Windows 10 con Configuration Manager.
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: tutorial
ms.assetid: 140c522f-d09a-40b6-a4b0-e0d14742834a
author: brenduns
ms.author: brenduns
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1aecb2c33c874717f1da979f1316d1b46b785071
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56755552"
---
# <a name="tutorial-enable-co-management-for-existing-configuration-manager-clients"></a>Tutorial: Habilitar la administración conjunta para los clientes existentes de Configuration Manager
Con la administración conjunta, puede conservar sus procesos estandarizados para el uso de Configuration Manager para administrar los equipos de su organización. Al mismo tiempo, se invierten en la nube mediante el uso de Intune para la seguridad y aprovisionamiento modernas.  

En este tutorial, configuró la administración conjunta de los dispositivos Windows 10 que ya estén inscritos en Configuration Manager. Este tutorial comienza con la premisa de que ya usa Configuration Manager para administrar los dispositivos Windows 10.

Use este tutorial cuando:  

- Tiene un Active Directory local que se puede conectar a Azure Active Directory (Azure AD) en una configuración de Azure AD híbrido
- Tener los clientes de Configuration Manager existentes que desea asociar a la nube


**En este tutorial aprenderá a:**  
> [!div class="checklist"]  
> * Revisar los requisitos previos para su entorno local y Azure  
> * Configuración de Azure AD híbrido  
> * Configurar los agentes de cliente de Configuration Manager para registrar con Azure AD  
> * Configurar Intune para dispositivos con inscripción automática  
> * Asignar licencias de Intune a los usuarios  
> * Habilitar la administración conjunta en Configuration Manager  


## <a name="prerequisites"></a>Requisitos previos  

### <a name="azure-services-and-environment"></a>Entorno y los servicios de azure
- Suscripción de Azure ([gratuita](https://azure.microsoft.com/free))
- Azure Active Directory Premium
- Suscripción a Microsoft Intune
  > [!TIP]  
  > Una Enterprise Mobility + Security (EMS) suscripción incluye Azure Active Directory Premium y Microsoft Intune. Suscripción de EMS ([gratuita](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-trial)).  

Si no está ya presente en su entorno, durante este tutorial, necesitará:
- Asignar a los usuarios una licencia para *Intune* y para *Azure Active Directory Premium*
- Configurar [Azure AD Connect](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-install-select-installation) entre su Active Directory local y su Azure Active Directory (AD) de inquilinos


### <a name="on-premises-infrastructure"></a>Infraestructura local
- Un [versión admitida](https://docs.microsoft.com/sccm/core/servers/manage/updates#supported-versions) de rama actual de System Center Configuration Manager
- El [entidad de MDM](https://docs.microsoft.com/sccm/mdm/deploy-use/change-mdm-authority) debe establecerse en Intune  


### <a name="permissions"></a>Permisos
A lo largo de este tutorial, use los siguientes permisos para completar las tareas:  
- Una cuenta que sea un *administrador global* en Azure  
- Una cuenta que sea un *Administrador de dominio* en su infraestructura local  
- Una cuenta que sea un *Administrador total* para *todas* ámbitos en Configuration Manager   

## <a name="set-up-hybrid-azure-ad"></a>Configuración de Azure AD híbrido
Cuando configura un híbrido de Azure AD, realmente está configurando la integración de un uso local de AD con Azure AD mediante Azure AD Connect y servicios federados de Active Directory (ADFS). Con una configuración correcta, entre los trabajadores de pueden perfectamente iniciar sesión en sistemas externos mediante sus localmente las credenciales de AD.

> [!IMPORTANT]  
> Este tutorial detalla un proceso básica para configurar Azure AD para un dominio administrado híbrido. Se recomienda, estar familiarizado con el proceso y no confiar en este tutorial como guía para comprender e implementar Azure AD híbrido.
>
> Para obtener más información acerca de Azure AD híbrido, comience con los siguientes artículos en la documentación de Azure Active Directory:
> - [Planee la implementación de Azure AD join](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan)
> -  [Planee la implementación de combinación de Azure AD híbrido](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan)
> -  [Controlar la combinación de Azure AD híbrido de los dispositivos](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-control)
> -  [Configurar la combinación de Azure AD híbrido para dominios federados](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-federated-domains)  


### <a name="set-up-azure-ad-connect"></a>Configurar Azure AD Connect  
Azure AD híbrido requiere la configuración de Azure AD Connect para sincronizar las cuentas de equipo en local Active Directory (AD) y el objeto de dispositivo en Azure AD.

Desde la versión 1.1.819.0, Azure AD Connect proporciona un Asistente para configurar la combinación de Azure AD híbrido. Uso de dicho asistente simplifica el proceso de configuración.  

Para configurar Azure AD Connect, necesita credenciales de administrador global para el inquilino de Azure AD.  

> [!TIP]  
> El procedimiento siguiente no se consideran autoritativo para la configuración de Azure AD Connect, pero se proporciona aquí para ayudar a simplificar la configuración de la administración conjunta entre Intune y Configuration Manager. Para el contenido autoritativo sobre esto y procedimientos relacionados para la configuración de Azure AD, consulte [configurar Azure AD híbrido para dominios administrados](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-managed-domains) en la documentación de Azure AD.  


#### <a name="configure-a-hybrid-azure-ad-join-using-azure-ad-connect"></a>Configurar una combinación de Azure AD híbrido con Azure AD Connect

1. Obtenga e instale el [versión más reciente de Azure AD Connect](https://www.microsoft.com/download/details.aspx?id=47594) (1.1.819.0 o superior).  
2. Inicie Azure AD Connect y, a continuación, seleccione **configurar**.
3. En el **tareas adicionales** página, seleccione **configurar opciones de dispositivo**y, a continuación, seleccione **siguiente**.
4. En el **Introducción** página, seleccione **siguiente**.
5. En el **conectar con Azure AD** , escriba las credenciales de administrador global para el inquilino de Azure AD.
6. En el **opciones de dispositivo** página, seleccione **configurar Azure AD híbrido**y, a continuación, seleccione **siguiente**.
7. En el **SCP** página, para cada bosque local que desea que Azure AD Connect para configurar el punto de conexión de servicio (SCP), realice los pasos siguientes y, a continuación, seleccione **siguiente**:  
   1. Seleccione el bosque.  
   2. Seleccione el servicio de autenticación.  Si tiene un dominio federado, seleccione el servidor de AD FS, a menos que su organización tiene exclusivamente los clientes de Windows 10 y ha configurado la sincronización de equipo o dispositivo o su organización usa [SeamlessSSO](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso).  
   3. Haga clic en **agregar** que escriba las credenciales de administrador de empresa.  
8. En el **sistemas operativos de dispositivos** , seleccione los sistemas operativos que usan los dispositivos en su entorno de Active Directory y, a continuación, seleccione **siguiente**.  

   Puede seleccionar la opción para admitir los dispositivos Unidos al dominio de nivel inferior de Windows, pero tenga en cuenta que la administración conjunta de dispositivos solo se admite para Windows 10.

9. Si tiene un dominio administrado, omita este paso.  

   En el **configuración de federación** página, escriba las credenciales del Administrador de AD FS y, a continuación, seleccione **siguiente**.
10. En el **listo para configurar** página, seleccione **configurar**.
11. En el **completar configuración** página, seleccione **Exit**.

Si experimenta problemas con la finalización de Azure AD híbrido unión de dominio unido dispositivos de Windows, vea [Troubleshooting Azure AD híbrido para dispositivos de Windows actuales](https://docs.microsoft.com/azure/active-directory/devices/troubleshoot-hybrid-join-windows-current).


## <a name="configure-client-settings-to-direct-clients-register-with-azure-ad"></a>Configurar el cliente para dirigir los clientes se registran con Azure AD  
Usar la configuración de cliente para configurar los clientes de Configuration Manager para registrar automáticamente con Azure AD.  

1. Abra el **consola de Configuration Manager** > **administración** > **Introducción** > **configuración de cliente** y, a continuación, edite el **configuración de cliente predeterminada**.  

2. Seleccione **servicios en la nube**.  

3. En el **la configuración predeterminada de** , establezca **registrar automáticamente nuevos dispositivos Unidos a un dominio de Windows 10 con Azure Active Directory** a = **Sí**.  

4. Haga clic en **Aceptar** para guardar esta configuración.  

## <a name="configure-auto-enrollment-of-devices-to-intune"></a>Configurar la inscripción automática de dispositivos a Intune   
A continuación, configuraremos la inscripción automática de dispositivos con Intune. Con la inscripción automática, los dispositivos administrados con Configuration Manager automáticamente se inscriban en Intune.

La inscripción automática también permite a los usuarios inscribir sus dispositivos Windows 10 en Intune. Inscribir dispositivos cuando un usuario agrega su cuenta profesional a sus dispositivos personales, o cuando un dispositivo corporativo está unido a Azure Active Directory.  

1. Inicie sesión en el [portal Azure](https://portal.azure.com/) y seleccione **Azure Active Directory** > **movilidad (MDM y MAM)** > **Microsoft Intune** .  

2. Configurar **el ámbito de usuario MDM**. Especifique uno de los procedimientos siguientes para configurar los dispositivos que los usuarios administrados por Microsoft Intune y aceptar los valores predeterminados para los valores de dirección URL.  

   - **Algunos** : seleccione el **grupos** que pueden inscribir automáticamente sus dispositivos Windows 10  

   - **Todos los** -todos los usuarios pueden inscribir automáticamente sus dispositivos Windows 10 cuando se establece en **ninguno**, se deshabilita la inscripción automática de administración de dispositivos móviles (MDM)

   > [!IMPORTANT]  
   > Si ambos **el ámbito de usuario MAM** y la inscripción automática de MDM (**el ámbito de usuario MDM**) están habilitadas para un grupo, solo se habilitará MAM. Solo aplicaciones móviles Management (MAM) se agrega para los usuarios de ese grupo al que conectar su dispositivo personal al área de trabajo. Dispositivos no son automáticamente inscriben en MDM.  

3. Seleccione **guardar** para completar la configuración de la inscripción automática.  

4. Vuelva a **movilidad (MDM y MAM)** y, a continuación, seleccione **inscripción a Microsoft Intune**.  

5. Para el ámbito de usuario MDM, seleccione **todas**y, a continuación, **guardar**.  


## <a name="assign-intune-licenses-to-users"></a>Asignar licencias de Intune a los usuarios   
Es una acción normalmente se pasa por alto pero crítica asignar una licencia de Intune a cada usuario que se van a usar un dispositivo que se administra conjuntamente.  

Para asignar licencias a grupos de usuarios, utilice Azure Active Directory.  

1. Inicie sesión en el [portal Azure](https://portal.azure.com/) con una cuenta de administrador. Para administrar las licencias, la cuenta debe ser un administrador de cuenta de usuario o rol de administrador global.  

2. Seleccione **todos los servicios** en el panel de navegación izquierdo y, a continuación, seleccione **Azure Active Directory**.  

3. En el **Azure Active Directory** panel, seleccione **licencias** para abrir un panel donde puede ver y administrar todos los productos con licencia en el inquilino.  

4. En **todos los productos**, seleccione la opción de producto que incluye la licencia de Intune y, a continuación, seleccione **asignar** en la parte superior del panel.  

   Por ejemplo, puede seleccionar **Enterprise Mobility + Security E5** si eso es cómo obtener Intune.  

5. En el **asignar licencias** panel, haga clic en **usuarios y grupos** para abrir el **usuarios y grupos** panel. Seleccione los grupos y usuarios individuales a los que desee asignan una licencia.  A continuación, haga clic en **seleccione** en la parte inferior del panel para confirmar la selección.  

6. En el **asignar licencias** panel, haga clic en **opciones de asignación** para mostrar todos los planes de servicio incluidos en el producto que seleccionó anteriormente. Si ha seleccionado un solo producto, como Intune, se muestra solo para ese producto.  
   - Establecer **Microsoft Intune** a **en**.  
   - Asignar a cada usuario una licencia para **Azure Active Directory Premium**.  

   Cuando se asignan las licencias aplicables, seleccione **Aceptar**.  

7. Para completar la asignación, en el **asignar licencias** panel, haga clic en **asignar** en la parte inferior del panel.

8. Se muestra una notificación en la esquina superior derecha que muestra el estado y el resultado del proceso. Si no se pudo completar la asignación al grupo (por ejemplo, porque ya existían licencias en el grupo), haga clic en la notificación para ver los detalles del error.

Para obtener más información sobre la asignación de licencias de Intune a los usuarios, consulte [asignar licencias](https://docs.microsoft.com/intune/licenses-assign).


## <a name="enable-co-management-in-configuration-manager"></a>Habilitar la administración conjunta en Configuration Manager
Con el conjunto de Azure AD híbrido, seguridad de las configuraciones de cliente de Configuration Manager en su lugar y licencias de producto asignadas a los usuarios, está listo para cambiar el conmutador y habilitar la administración conjunta de los dispositivos Windows 10.  

> [!TIP]  
>  En el paso seis del siguiente procedimiento, deberá asignar una colección como un *grupo piloto* para la administración conjunta. Se trata de un grupo que contenga un número pequeño de clientes para probar sus configuraciones de administración conjunta. Se recomienda que crear una colección adecuada antes de iniciar el procedimiento. A continuación, puede seleccionar esa colección sin salir del procedimiento para realizar esta acción.  

1. En la consola de Configuration Manager, vaya a **Administración** > **Información general** > **Servicios de nube** > **Co-management** (Administración conjunta).

2. En la pestaña Inicio, en el grupo de administración, seleccione **Configurar administración conjunta** para abrir el Asistente para configuración de administración conjunta.

3. En la página de suscripción, seleccione **sesión** inicie sesión en su inquilino de Intune y, a continuación, seleccione **siguiente**.

4. En la página de habilitación de la *la inscripción automática en Intune* lista desplegable, seleccione una de las siguientes opciones:  

   - **Piloto**  - *(recomendado)* los miembros de la colección que especifique se inscriban automáticamente en Intune y, a continuación, administrarlos de forma conjunta. Especifique la recopilación piloto en el *ensayo* página de este asistente. Esta opción permite la administración conjunta en un subconjunto de los clientes de prueba. A continuación, puede desplegar administración conjunta a clientes adicionales con un enfoque por fases.  

   - **Todos los** -habilitar la administración conjunta para todos los clientes.  

5. En la página de las cargas de trabajo puede cambiar las cargas de trabajo de **Configuration Manager** a uno de los siguientes valores y, a continuación, cuando esté listo para continuar, seleccione **siguiente**.  

   - **Definir un programa piloto de Intune** -cambia una carga de trabajo solo para los dispositivos del grupo piloto. Asignación de una colección como el grupo piloto en la siguiente página del asistente.  

   - **Intune** -cambia la carga de trabajo asociada para todos los dispositivos Windows 10 administrados conjuntamente.  

   No es necesario cambiar las cargas de trabajo en el momento de que habilitar la administración conjunta. Puede volver a visitar esta configuración desde la consola de Configuration Manager más adelante, después de configura la administración conjunta.  

   Antes de cambiar una carga de trabajo, asegúrese de que se configuran e implementan la carga de trabajo correspondiente en Intune. Realizar por lo que mantiene las cargas de trabajo administrados.  

6. En la página de almacenamiento provisional, especifique una colección que se usará para la **recopilación piloto**y, a continuación, haga clic en **siguiente**. La colección que especifique se usa como parte de la implementación por fases de la administración conjunta. Puede cambiar las colecciones del grupo piloto en cualquier momento desde las propiedades de la administración conjunta.  

7. En la página Resumen, seleccione **siguiente**y, a continuación, **cerrar** para completar el asistente.  


## <a name="next-steps"></a>Pasos siguientes
- Revisar el estado de los dispositivos administrados conjuntamente con el [panel de administración conjunta](/sccm/comanage/how-to-monitor)
- Empezar a recibir [valor inmediato](quickstarts.md#immediate-value) de la administración conjunta
- Use [acceso condicional](quickstart-conditional-access.md) y las reglas de cumplimiento de Intune para administrar el acceso de usuario a los recursos corporativos
