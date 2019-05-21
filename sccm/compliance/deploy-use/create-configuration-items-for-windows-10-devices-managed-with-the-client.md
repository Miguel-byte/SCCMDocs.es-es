---
title: 'Creación de elementos de configuración para Windows 10 administrado por el cliente '
titleSuffix: Configuration Manager
description: Use el elemento de configuración de Windows 10 de System Center Configuration Manager para administrar la configuración de los equipos con Windows 10 que administra el cliente de Configuration Manager.
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 14226fbe-dd07-4432-910b-130790624a4e
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6a26ffcb0d88f50902e82049102825af956a4027
ms.sourcegitcommit: 99dfe4fb9e9cfd20c44380ae442b3a5b895a0d9b
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 05/07/2019
ms.locfileid: "65214925"
---
# <a name="how-to-create-configuration-items-for-windows-10-devices-managed-with-the-system-center-configuration-manager-client"></a>Cómo crear elementos de configuración para dispositivos Windows 10 administrados con el cliente de System Center Configuration Manager
Use el elemento de configuración de **Windows 10** de System Center Configuration Manager para administrar la configuración de los equipos con Windows 10 que administra el cliente de Configuration Manager.  
  
> [!IMPORTANT]  
>  En esta versión, si creó una configuración de **Contraseña** como parte de un elemento de configuración del tipo **Windows 10** (para un dispositivo administrado con el cliente de Configuration Manager), si la configuración no existe o no se ha configurado en el dispositivo Windows 10, se evaluará de forma incorrecta como compatible.  
>   
>  Como alternativa, cuando cree una configuración para estos dispositivos, asegúrese de que **Corregir configuraciones no compatibles** se ha seleccionado en las páginas del Asistente para crear elemento de configuración. Además, al implementar una línea base de configuración que incluye un elemento de configuración de Windows 10 que contiene la configuración de contraseña, seleccione **Corregir las reglas no compatibles cuando se admita** en el cuadro de diálogo Implementar líneas de base de configuración. Con esta solución alternativa, la configuración se supervisará y corregirá si se detecta que no es conforme. Después de la corrección, se informará correctamente que la configuración es **Conforme** (a menos que se encuentre un problema, en cuyo caso informará de **Error**).  
  
### <a name="to-create-a-windows-10-configuration-item"></a>Para crear un elemento de configuración de Windows 10  
  
1. En la consola de Configuration Manager, haga clic en **Activos y compatibilidad**.  
  
2. En el área de trabajo **Activos y compatibilidad** , expanda **Configuración de cumplimiento**y, a continuación, haga clic en **Elementos de configuración**.  
  
3. En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear elemento de configuración**.  
  
4. En la página **General** del **Asistente para crear elemento de configuración**, escriba un nombre y, opcionalmente, una descripción para el elemento de configuración.  
  
5. En **Especifique el tipo de elemento de configuración que quiere crear**, seleccione **Windows 10**.  
  
6. Haga clic en **Categorías** si crea y asigna categorías para ayudarle a buscar y filtrar elementos de configuración en la consola de Configuration Manager.  
  
7. En la página **Plataformas admitidas** del asistente, seleccione las plataformas de Windows 10 específicas que evaluarán el elemento de configuración.  
  
8. En la página **Configuración del dispositivo** del asistente, seleccione el grupo de configuración que quiere configurar. Consulte [Referencia a configuración de elemento de configuración de Windows 10](#BKMK_Ref) en este artículo para más información y, luego, haga clic en **Siguiente**.  
  
   > [!TIP]  
   >  Si el valor que quiere no aparece, seleccione la casilla **Configurar opciones adicionales que no se encuentran en los grupos de configuración predeterminados**.  
  
9. En cada página de configuración, configure las opciones que necesita y si quiere corregirlas cuando no sean conformes en los dispositivos (si se admite).  
  
10. Para cada grupo de configuración, también puede elegir la gravedad que se notificará cuando se encuentre que un elemento de configuración no es conforme entre las siguientes:  
  
    -   **Ninguna**: los dispositivos que no sigan esta regla de cumplimiento no notificarán ninguna gravedad de error en los informes de Configuration Manager.  
  
    -   **Información**: los dispositivos que no cumplan esta regla de compatibilidad notificarán una gravedad de error de **Información** en los informes de Configuration Manager.  
  
    -   **Advertencia**: los dispositivos que no cumplan esta regla de compatibilidad notificarán una gravedad de error de **Advertencia** en los informes de Configuration Manager.  
  
    -   **Crítico**: los dispositivos que no cumplan esta regla de compatibilidad notificarán una gravedad de error de **Crítico** en los informes de Configuration Manager.  
  
    -   **Crítico con evento**: los dispositivos que no cumplan esta regla de compatibilidad notificarán una gravedad de error de **Crítico** en los informes de Configuration Manager. Este nivel de gravedad también se registra como evento de Windows en el registro de eventos de la aplicación.  
  
11. En la página **Aplicabilidad de plataforma** del asistente, revise cualquier configuración que no sea compatible con las plataformas admitidas que seleccionó anteriormente. Puede regresar y eliminar esta configuración o puede continuar.  
  
    > [!TIP]  
    >  No se evalúa el cumplimiento de la configuración no admitida.  
  
12. Complete el asistente.  
  
    Puede ver el nuevo elemento de configuración en el nodo **Elementos de configuración** del área de trabajo **Activos y compatibilidad** .  
  
## <a name="BKMK_Ref"></a> Windows 10 configuration item settings reference  
  
### <a name="password"></a>Contraseña  
  
|Configuración|Detalles|  
|-------------|-------------|  
|**Requerir configuración de contraseña en dispositivos**|Se requiere una contraseña en dispositivos compatibles.|  
|**Longitud de contraseña mínima (caracteres)**|La longitud mínima en caracteres de la contraseña.|  
|**Caducidad de la contraseña en días**|El número de días antes de que se deba cambiar la contraseña.|  
|**Número de contraseñas recordadas**|Impide que se vuelvan a usar contraseñas anteriores.|  
|**Número de intentos de inicio de sesión incorrectos antes de que se borre un dispositivo**|Borra el dispositivo si hay este número de intentos de inicio de sesión incorrectos.|  
|**Tiempo de inactividad antes de que se bloquee el dispositivo**|Especifica cuántos minutos el dispositivo debe estar inactivo antes de se bloquee automáticamente.|  
|**Complejidad de la contraseña**|Elija si se puede especificar un PIN como "1234" o si se debe proporcionar una contraseña segura.|
|**Número de conjuntos de caracteres complejos que se requieren para la contraseña**|Si ha seleccionado una contraseña **segura**, use esta opción para configurar el número de conjuntos de caracteres complejos necesarios. Para una contraseña segura, este valor se debe establecer en al menos **3, lo que significa que se requieren tanto números como letras. Seleccione **4** si quiere exigir una contraseña que, además, requiera caracteres especiales como **($%**.<br>(Solo Windows 10)  |
  
###  <a name="device"></a>Dispositivo  
  
|Nombre de la configuración|Detalles|  
|------------------|-------------|  
|**Bluetooth**|Permite el uso de la característica Bluetooth en el dispositivo.|  
  
### <a name="cloud"></a>Nube  
  
|Nombre de la configuración|Detalles|  
|------------------|-------------|  
|**Sincronización de la configuración**|Permite la sincronización de configuraciones entre diferentes dispositivos.|  
|**Sincronización de credenciales**|Permite la sincronización de credenciales entre diferentes dispositivos.|  
|**Sincronización de configuraciones a través de conexión de uso medido**|Permite la sincronización de configuraciones cuando se mide la conexión a Internet.|  
  
### <a name="roaming"></a>Movilidad  
  
|Nombre de la configuración|Detalles|  
|------------------|-------------|  
|**Itinerancia de datos**|Permite movilidad entre redes al obtener acceso a datos.|  
  
### <a name="encryption"></a>Cifrado  
  
|Nombre de la configuración|Detalles|  
|------------------|-------------|  
|**Cifrado de archivo en el dispositivo**|Requiere el cifrado de los archivos en el dispositivo.|  
  
### <a name="system-security"></a>Seguridad del sistema  
  
|Nombre de la configuración|Detalles|  
|------------------|-------------|  
|**Control de cuentas de usuario**|Configura cómo funciona el Control de cuentas de usuario de Windows en el dispositivo.<br />Por ejemplo, puede deshabilitarlo o establecer el nivel en el que le notifica.|  
|**Firewall de red**|Habilita o deshabilita el Firewall de Windows.|  
|**SmartScreen**|Habilita o deshabilita Windows SmartScreen.|  
|**Protección antivirus**|Requiere que el software antivirus esté instalado y configurado.|  
|**Las firmas de protección antivirus están actualizadas**|Requiere que los archivos de firma para el software antivirus en el dispositivo estén actualizados.|  
  
### <a name="windows-information-protection-wip"></a>Windows Information Protection (WIP)

Con el aumento de los dispositivos propiedad de los empleados en la empresa, también aumenta el riesgo de pérdidas de datos accidentales a través de aplicaciones y servicios, como el correo electrónico, las redes sociales y la nube pública, que están fuera del control de la empresa. Por ejemplo, cuando un empleado envía imágenes de su último proyecto de ingeniería desde su cuenta de correo electrónico personal, copia y pega información de producto en un tweet o guarda un informe de ventas en curso para su almacenamiento en nube pública.

Windows Information Protection (anteriormente, Protección de datos de empresa) ayuda a protegerse contra esta pérdida potencial de datos sin interferir en la experiencia de empleado. WIP también ayuda a proteger los datos y aplicaciones de la empresa de pérdidas accidentales de datos en dispositivos tanto propiedad de la empresa como personales que los empleados llevan al trabajo sin necesidad de realizar cambios en su entorno ni en otras aplicaciones.

 Los elementos de configuración de Windows Information Protection de Configuration Manager administran la lista de aplicaciones protegidas por WIP, las ubicaciones de red de la empresa, el nivel de protección y la configuración de cifrado.
  

Para obtener información sobre cómo configurar Windows Information Protection con Configuration Manager, vea [Protege los datos de tu empresa con Windows Information Protection (WIP)](https://technet.microsoft.com/itpro/windows/keep-secure/protect-enterprise-data-using-wip).
  
## <a name="see-also"></a>Véase también  
 [Elementos de configuración para dispositivos administrados con el cliente de System Center Configuration Manager](../../compliance/deploy-use/create-configuration-items.md)
