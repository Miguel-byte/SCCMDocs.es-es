---
title: Tutorial&#58; Habilitación de la administración conjunta para clientes existentes de Configuration Manager
titleSuffix: Configuration Manager
description: Configure la administración conjunta con Microsoft Intune cuando ya administra dispositivos Windows 10 con Configuration Manager.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: tutorial
ms.assetid: 140c522f-d09a-40b6-a4b0-e0d14742834a
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: ec46fb91e862c8d835b88a7ca859fcbfd8e4d339
ms.sourcegitcommit: 72faa1266b31849ce1a23d661a1620b01e94f517
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/26/2019
ms.locfileid: "68535337"
---
# <a name="tutorial-enable-co-management-for-existing-configuration-manager-clients"></a>Tutorial: Habilitación de la administración conjunta para clientes existentes de Configuration Manager

Con la administración conjunta, puede mantener sus procesos estandarizados para el uso de Configuration Manager para administrar los equipos de su organización. Al mismo tiempo, está invirtiendo en la nube mediante el uso de Intune para la seguridad y el aprovisionamiento moderno.  

En este tutorial, va a configurar la administración conjunta de dispositivos Windows 10 que ya están inscritos en Configuration Manager. Este tutorial comienza con la premisa de que ya usa Configuration Manager para administrar los dispositivos Windows 10.

Use este tutorial cuando:  

- Tiene una instancia de Active Directory local que puede conectar a Azure Active Directory (Azure AD) en una configuración de Azure AD híbrida.

  Si no puede implementar una instancia híbrida de Azure Active Directory (AD) que se une a su AD local con Azure AD, se recomienda seguir nuestro tutorial complementario para la [habilitación de la administración conjunta para los nuevos dispositivos Windows 10 basados en Internet](/sccm/comanage/tutorial-co-manage-new-devices).
- Tiene clientes existentes en Configuration Manager que desea asociar a la nube.

**En este tutorial aprenderá a:**  
> [!div class="checklist"]
> * Revisar los requisitos previos para su entorno local y Azure
> * Configuración de Azure AD híbrido  
> * Configurar los agentes de cliente de Configuration Manager para registrarse con Azure AD  
> * Configurar Intune para la inscripción automática de dispositivos  
> * Asignar licencias de Intune a los usuarios  
> * Habilitar la administración conjunta en Configuration Manager  

## <a name="prerequisites"></a>Requisitos previos  

### <a name="azure-services-and-environment"></a>Entorno y servicios de Azure

- Suscripción de Azure ([evaluación gratuita](https://azure.microsoft.com/free))
- Azure Active Directory Premium
- Suscripción a Microsoft Intune
  > [!TIP]  
  > Una suscripción a Enterprise Mobility + Security (EMS) incluye Azure Active Directory Premium y Microsoft Intune. Una suscripción a EMS ([evaluación gratuita](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-trial)).  

Si no está ya presente en su entorno, durante este tutorial, necesitará:

- Asignar a los usuarios una licencia para *Intune* y para *Azure Active Directory Premium*.
- Configurar [Azure AD Connect](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-install-select-installation) entre su instancia de Active Directory local y su inquilino de Azure Active Directory (AD).

### <a name="on-premises-infrastructure"></a>Infraestructura local

- Una [versión compatible](https://docs.microsoft.com/sccm/core/servers/manage/updates#supported-versions) de la rama actual de System Center Configuration Manager
- La [entidad de administración de dispositivos móviles (MDM)](https://docs.microsoft.com/sccm/mdm/deploy-use/change-mdm-authority) se debe establecer en Intune.  

### <a name="permissions"></a>Permisos

A lo largo de este tutorial, use los siguientes permisos para completar las tareas:

- Una cuenta que sea un *administrador global* en Azure  
- Una cuenta que sea un *administrador de dominio* en su infraestructura local  
- Una cuenta que sea un *administrador total* para *todos* los ámbitos en Configuration Manager

## <a name="set-up-hybrid-azure-ad"></a>Configuración de Azure AD híbrido

Cuando configura un entorno híbrido de Azure AD, realmente está configurando la integración de una instancia local de AD con Azure AD mediante Azure AD Connect y Servicios de federación de Active Directory (AD FS). Con una configuración correcta, los trabajadores pueden perfectamente iniciar sesión en sistemas externos mediante sus credenciales de AD locales.

> [!IMPORTANT]  
> Este tutorial detalla un proceso básico para configurar Azure AD híbrido para un dominio administrado. Se recomienda estar familiarizado con el proceso y no basarse en este tutorial como guía para comprender e implementar el entorno de Azure AD híbrido.
>
> Para obtener más información acerca de Azure AD híbrido, comience con los siguientes artículos en la documentación de Azure Active Directory:
>
> - [Planeación de la implementación de la unión a Azure AD](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan)
> - [Planeamiento de la implementación de la unión a Azure Active Directory híbrido](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan)
> - [Control de la unión a Azure AD híbrido de los dispositivos](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-control)
> - [Configuración de dispositivos híbridos unidos a Azure Active Directory para dominios federados](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-federated-domains)  

### <a name="set-up-azure-ad-connect"></a>Configuración de Azure AD Connect

Azure AD híbrido requiere la configuración de Azure AD Connect para mantener sincronizadas las cuentas del equipo en su Active Directory (AD) local y el objeto del dispositivo en Azure AD.

A partir de la versión 1.1.819.0, Azure AD Connect proporciona un asistente para configurar la unión a Azure AD híbrido. El uso de dicho asistente simplifica el proceso de configuración.  

Para configurar Azure AD Connect, necesita credenciales de administrador global para el inquilino de Azure AD.  

> [!TIP]  
> El siguiente procedimiento no debe considerarse autoritativo para la configuración de Azure AD Connect, pero se proporciona aquí para ayudar a simplificar la configuración de la administración conjunta entre Intune y Configuration Manager. Para ver el contenido autoritativo sobre este y otros procedimientos relacionados para la configuración de Azure AD, consulte [Configuración de dispositivos híbridos unidos a Azure Active Directory para dominios administrados](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-managed-domains) en la documentación de Azure AD.  

#### <a name="configure-a-hybrid-azure-ad-join-using-azure-ad-connect"></a>Configuración de una unión a Azure AD híbrida con Azure AD Connect

1. Obtenga e instale la [versión más reciente de Azure AD Connect](https://www.microsoft.com/download/details.aspx?id=47594) (1.1.819.0 o superior).  
2. Inicie Azure AD Connect y, a continuación, seleccione **Configurar**.
3. En la página **Tareas adicionales**, seleccione **Configurar opciones de dispositivo** y, a continuación, seleccione **Siguiente**.
4. En la página **Información general**, seleccione **Siguiente**.
5. En la página **Conectarse a Azure AD**, escriba las credenciales de administrador global para el inquilino de Azure AD.
6. En la página **Opciones de dispositivo**, seleccione **Configurar la combinación de Azure AD híbrido** y, a continuación, seleccione **Siguiente**.
7. En la página **Sistemas operativos de dispositivos**, seleccione los sistemas operativos que usan los dispositivos en su entorno de Active Directory y, a continuación, seleccione **Siguiente**.  

   Puede seleccionar la opción para admitir los dispositivos unidos al dominio de nivel inferior de Windows, pero tenga en cuenta que la administración conjunta de dispositivos solo se admite para Windows 10.
8. En la página **SCP**, para cada bosque local que desee que Azure AD Connect configure para el punto de conexión de servicio (SCP), realice los siguientes pasos y luego seleccione **Siguiente**:  
   1. Seleccione el bosque.  
   2. Seleccione el servicio de autenticación.  Si tiene un dominio federado, seleccione el servidor de AD FS, a menos que su organización tenga exclusivamente clientes de Windows 10 y haya configurado la sincronización de equipo o dispositivo o su organización use [SeamlessSSO](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso).  
   3. Haga clic en **Agregar** para escribir las credenciales de administrador de empresa.  
9. Si tiene un dominio administrado, omita este paso.  

   En la página **Configuración de federación**, escriba las credenciales del administrador de AD FS y, a continuación, seleccione **Siguiente**.
10. En la página **Listo para configurar**, seleccione **Configurar**.
11. En la página **Configuración completada**, seleccione **Salir**.

Si experimenta problemas con la finalización de la unión a Azure AD híbrido para dispositivos Windows unidos a dominio, vea [Solución de problemas de dispositivos híbridos de Windows 10 y Windows Server 2016 unidos a Azure Active Directory](https://docs.microsoft.com/azure/active-directory/devices/troubleshoot-hybrid-join-windows-current).

## <a name="configure-client-settings-to-direct-clients-register-with-azure-ad"></a>Configuración del cliente para dirigir a los clientes al registro con Azure AD

Use la configuración de cliente para configurar los clientes de Configuration Manager para que se registren automáticamente con Azure AD.  

1. Abra la **Consola de Configuration Manager** > **Administración** > **Información general** > **Configuración de cliente** y, luego, edite la **Configuración de cliente predeterminada**.  

2. Seleccione **Cloud Services**.  

3. En la página **Configuración predeterminada**, establezca **Registrar automáticamente los nuevos dispositivos de Windows 10 unidos a un dominio con Azure Active Directory** en = **Sí**.  

4. Haga clic en **Aceptar** para guardar esta configuración.  

## <a name="configure-auto-enrollment-of-devices-to-intune"></a>Configuración de la inscripción automática de dispositivos en Intune

A continuación, configuraremos la inscripción automática de dispositivos con Intune. Con la inscripción automática, los dispositivos administrados con Configuration Manager se inscriben automáticamente en Intune.

La inscripción automática también permite a los usuarios inscribir sus dispositivos Windows 10 en Intune. Inscriba dispositivos cuando un usuario agregue su cuenta profesional a su dispositivo personal, o cuando un dispositivo corporativo esté unido a Azure Active Directory.  

1. Inicie sesión en [Azure Portal](https://portal.azure.com/) y seleccione **Azure Active Directory** > **Movilidad (MDM y MAM)**  > **Microsoft Intune** .  

2. Configure el **ámbito de usuario de MDM**. Especifique una de las opciones siguientes para configurar qué dispositivos de usuarios se administran por Microsoft Intune y acepte la configuración predeterminada para los valores de la dirección URL.  

   - **Algunos**: seleccione los **grupos** que pueden inscribir automáticamente sus dispositivos Windows 10  

   - **Todos**: todos los usuarios pueden inscribir automáticamente sus dispositivos Windows 10; cuando está configurados en **Ninguno**, se deshabilita la inscripción automática de la administración de dispositivos móviles (MDM)

   > [!IMPORTANT]  
   > Si **ámbito de usuario de MAM** y la inscripción automática de MDM (el **ámbito de usuario de MDM**) están habilitados para un grupo, solo se habilitará MAM. Solo se agrega la administración de aplicaciones móviles (MAM) para los usuarios de ese grupo cuando conectan su dispositivo personal al área de trabajo. Los dispositivos no se inscriben automáticamente en MDM.  

3. Seleccione **Guardar** para completar la configuración de la inscripción automática.  

4. Vuelva a **Movilidad (MDM y MAM)** y, a continuación, seleccione **Inscripción a Microsoft Intune**.  

5. Para el ámbito de usuario de MDM, seleccione **Todos** y, a continuación, **Guardar**.  

## <a name="assign-intune-licenses-to-users"></a>Asignación de licencias de Intune a los usuarios

Una acción de gran importancia que suele pasarse por alto es la asignación de una licencia de Intune a cada usuario que use un dispositivo que sea administrado conjuntamente.  

Para asignar licencias a grupos de usuarios, utilice Azure Active Directory.  

1. Inicie sesión en [Azure Portal](https://portal.azure.com/) con una cuenta de administrador. Para administrar las licencias, la cuenta debe tener un rol de administrador global o administrador de cuentas de usuario.  

2. Seleccione **Todos los servicios** en el panel de navegación izquierdo y, a continuación, seleccione **Azure Active Directory**.  

3. En el panel **Azure Active Directory**, seleccione **Licencias** para abrir un panel donde puede ver y administrar todos los productos con licencia en el inquilino.  

4. En **Todos los productos**, seleccione la opción de producto que incluye la licencia de Intune y, a continuación, seleccione **Asignar** en la parte superior del panel.  

   Por ejemplo, puede seleccionar **Enterprise Mobility + Security E5** si es así como obtiene Intune.  

5. En el panel **Asignar licencias**, haga clic en **Usuarios y grupos** para abrir el panel **Usuarios y grupos**. Seleccione los grupos y usuarios individuales a los que desee asignar una licencia.  A continuación, haga clic en **Seleccionar** en la parte inferior del panel para confirmar la selección.  

6. En el panel **Asignar licencias**, haga clic en **Opciones de asignación** para mostrar todos los planes de servicio incluidos en el producto que seleccionó anteriormente. Si ha seleccionado un solo producto, como Intune, se muestra solo ese producto.  
   - Establezca **Microsoft Intune** en **Activado**.  
   - Asigne a cada usuario una licencia para **Azure Active Directory Premium**.  

   Cuando se hayan asignado las licencias correspondientes, seleccione **Aceptar**.  

7. Para completar la asignación, en el panel **Asignar licencia**, haga clic en **Asignar** en la parte inferior del panel.

8. Se muestra una notificación en la esquina superior derecha que muestra el estado y el resultado del proceso. Si no se pudo completar la asignación al grupo (por ejemplo, porque ya existían licencias en el grupo), haga clic en la notificación para ver los detalles del error.

Para obtener más información sobre la asignación de licencias de Intune a los usuarios, consulte [Asignar licencias](https://docs.microsoft.com/intune/licenses-assign).

## <a name="enable-co-management-in-configuration-manager"></a>Habilitación de la administración conjunta en Configuration Manager

Con Azure AD configurado, las configuraciones del cliente de Configuration Manager establecidas y las licencias de producto asignadas a los usuarios, está listo para cambiar el conmutador y habilitar la administración conjunta de los dispositivos Windows 10.  

> [!TIP]
> - Cuando habilite la administración conjunta, asignará una recopilación como un *grupo piloto*. Se trata de un grupo que contiene un número pequeño de clientes para probar sus configuraciones de administración conjunta. Se recomienda crear una colección adecuada antes de iniciar el procedimiento. A continuación, puede seleccionar esa colección sin salir del procedimiento para ello.
> - A partir de la versión 1906 de Configuration Manager, es posible que necesite varias recopilaciones, porque puede asignar un *grupo piloto* distinto para cada carga de trabajo.

### <a name="enable-co-management-starting-in-version-1906"></a>Habilitación de la administración conjunta a partir de la versión 1906

Para habilitar la administración conjunta a partir de la versión 1906 de Configuration Manager, siga estas instrucciones:

[!INCLUDE [Enable Co-management in version 1906 and later](includes/enable-co-management-1906-and-higher.md)]

### <a name="enable-co-management-in-version-1902-and-earlier"></a>Habilitación de la administración conjunta en la versión 1902 y versiones anteriores

Para habilitar la administración conjunta para la versión 1902 y versiones anteriores de Configuration Manager, siga estas instrucciones:

[!INCLUDE [Enable Co-management in version 1902 and earlier](includes/enable-co-management-1902-and-earlier.md)]

## <a name="next-steps"></a>Pasos siguientes

- Revise el estado de los dispositivos administrados conjuntamente con el [panel de administración conjunta](/sccm/comanage/how-to-monitor).
- Empiece a recibir [valor inmediato](quickstarts.md#immediate-value) de la administración conjunta.
- Use el [acceso condicional](quickstart-conditional-access.md) y las reglas de cumplimiento de Intune para administrar el acceso de los usuarios a los recursos corporativos.
