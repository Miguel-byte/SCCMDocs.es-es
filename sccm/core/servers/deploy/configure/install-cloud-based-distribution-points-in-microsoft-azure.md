---
title: Instalación de puntos de distribución basados en la nube
titleSuffix: Configuration Manager
description: Obtenga información sobre lo que necesita para empezar a usar los puntos de distribución basados en la nube en Microsoft Azure.
ms.date: 2/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: bb83ac87-9914-4a35-b633-ad070031aa6e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2c9c79c5e635a50fecf02c46e2a134df87c2d784
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="install-cloud-based-distribution-points-in-microsoft-azure-for-system-center-configuration-manager"></a>Instalar puntos de distribución basados en la nube en Microsoft Azure para System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Puede instalar puntos de distribución basados en la nube de System Center Configuration Manager en Microsoft Azure. Si no está familiarizado con los puntos de distribución basados en la nube, vea [Usar un punto de distribución basado en la nube](../../../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md) antes de continuar.

 Antes de comenzar la instalación,asegúrese de que tiene los archivos de certificado necesarios:  

-   Un certificado de administración de Microsoft Azure que se exporta a un archivo .cer y a un archivo .pfx.  

-   Un certificado de servicio de punto de distribución basado en la nube de Configuration Manager que se exporta a un archivo .pfx.  

    > [!TIP]
    >   Para obtener más información sobre estos certificados, consulte la sección de puntos de distribución basados en la nube en el tema [Requisitos de certificados PKI para System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md). Para obtener un ejemplo de implementación del certificado de servicio de punto de distribución basado en la nube, consulte la sección "Implementación del certificado de servicio para puntos de distribución basados en la nube" del tema [Ejemplo paso a paso de la implementación de los certificados PKI para System Center Configuration Manager: entidad de certificación de Windows Server 2008](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  


 Después de instalar el punto de distribución basado en la nube, Azure genera automáticamente un GUID para el servicio y lo anexa al sufijo DNS de **cloudapp.net**. Con este GUID, debe configurar DNS con un alias DNS (registro CNAME). De este modo, puede asignar el nombre de servicio definido en el certificado de servicio de punto de distribución basado en la nube de Configuration Manager al GUID generado automáticamente.  

 Si utiliza un servidor proxy web, es posible que tenga que configurar el servidor proxy para habilitar la comunicación con el servicio de nube que hospeda el punto de distribución.  

##  <a name="BKMK_ConfigWindowsAzureandInstallDP"></a> Configurar Azure e instalar puntos de distribución basados en la nube  
 Use los procedimientos siguientes para configurar Azure para admitir puntos de distribución y, después, instale el punto de distribución basado en la nube en Configuration Manager.  

### <a name="to-set-up-a-cloud-service-in-azure-for-a-distribution-point"></a>Para configurar un servicio de nube en Azure para un punto de distribución  

1.  Abra un explorador web para Azure Portal, en https://manage.windowsazure.com, y acceda a la cuenta.  

2.  Haga clic en **Servicios hospedados, cuentas de almacenamiento y CDN** y, después, seleccione **Certificados de administración**.  

3.  Haga clic con el botón secundario en su suscripción y, a continuación, seleccione **Agregar certificado**.  

4.  En **Archivo de certificado**, especifique el archivo .cer que contiene el certificado de administración de Azure para usar con este servicio en la nube y, después, haga clic en **Aceptar**.  

El certificado de administración se carga en Azure y podrá instalar un punto de distribución basado en la nube.  

### <a name="to-install-a-cloud-based-distribution-point-for-configuration-manager"></a>Para instalar un punto de distribución basado en la nube para Configuration Manager  

1.  Complete los pasos del procedimiento anterior para configurar un servicio en la nube en Azure con un certificado de administración.  

2.  En el área de trabajo **Administración** de la consola de Configuration Manager, expanda **Cloud Services** y seleccione **Puntos de distribución de nube**. En la pestaña **Inicio**, haga clic en **Crear punto de distribución de nube**.  

3.  En la página **General** del Asistente para crear punto de distribución de nube, configure lo siguiente:  

    -   Especifique el **Id. de suscripción** de su cuenta de Azure.  

        > [!TIP]  
        >  Encontrará el identificador de la suscripción de Azure en Azure Portal.  

    -   Especifique el **Certificado de administración**. Haga clic en **Examinar** para especificar el archivo .pfx que contiene el certificado de administración de Azure exportado y, después, escriba la contraseña del certificado. Opcionalmente, puede especificar un archivo .publishsettings de versión 1 desde Azure SDK 1.7.  

4.  Haga clic en **Siguiente**. Configuration Manager se conectará a Azure para validar el certificado de administración.  

5.  En la página **Configuración**, complete las opciones siguientes y, después, haga clic en **Siguiente**:  

    -   En **Región**, seleccione la región de Azure donde quiera crear el servicio en la nube que hospeda este punto de distribución.  

    -   En **Archivo de certificado**, especifique el archivo .pfx que contiene el certificado exportado para el servicio de punto de distribución basado en la nube de Configuration Manager. Después, escriba la contraseña.  

        > [!NOTE]  
        >  El cuadro **FQDN de servicio** se rellena automáticamente con el nombre del firmante del certificado. En la mayoría de los casos, no es necesario modificarlo. La excepción es si se usa un certificado comodín en un entorno de prueba. Por ejemplo, en este caso podría no especificar el nombre de host, de modo que varios equipos que tienen el mismo sufijo DNS puedan usar el certificado. En este caso, el firmante del certificado es un valor similar a **CN=\*.contoso.com** y Configuration Manager muestra un mensaje que indica que debe especificar el FQDN correcto. Haga clic en **Aceptar** para cerrar el mensaje y, a continuación, escriba un nombre específico antes del sufijo DNS para proporcionar un FQDN completo. Por ejemplo, puede agregar **clouddp1** para especificar el FQDN del servicio completo de **clouddp1.contoso.com**. El FQDN del servicio debe ser exclusivo en su dominio y no debe coincidir con el de ningún dispositivo unido al dominio.  
        >   
        >  Los certificados comodín solo se admiten en entornos de prueba.  

6.  En la página **Alertas**, configure cuotas de almacenamiento, cuotas de transferencia y el porcentaje de estas cuotas en el que quiere que Configuration Manager genere alertas. A continuación, haga clic en **Siguiente**.  

7.  Complete el asistente.  

El asistente crea un nuevo servicio hospedado para el punto de distribución basado en la nube. Después de cerrar el asistente, puede supervisar el progreso de instalación del punto de distribución basado en la nube en la consola de Configuration Manager. También puede supervisar el archivo **CloudMgr.log** en el servidor de sitio primario. Puede supervisar el aprovisionamiento del servicio en la nube en Azure Portal.  

> [!NOTE]  
>  Se puede tardar hasta 30 minutos en aprovisionar un nuevo punto de distribución en Azure. El siguiente mensaje se repite en el archivo **CloudMgr.log** hasta que se aprovisione la cuenta de almacenamiento: **Esperando para comprobar si existe contenedor. Se comprobará otra vez en 10 segundos**. A continuación, el servicio se crea y se configura.  

 Puede identificar que se ha completado la instalación del punto de distribución basado en la nube mediante los métodos siguientes:  

-   En Azure Portal, la **Implementación** del punto de distribución basado en la nube muestra un estado de **Listo**.  

-   En la consola de Configuration Manager, en el área de trabajo **Administración**, en **Configuración de jerarquía**, en el nodo **Nube**, el punto de distribución basado en la nube muestra un estado de **‎Listo**.  

-   Configuration Manager muestra un identificador de mensaje de estado **9409** para el componente SMS_CLOUD_SERVICES_MANAGER.  

##  <a name="BKMK_ConfigDNSforCloudDPs"></a> Configurar la resolución de nombres para puntos de distribución basados en la nube  
 Antes de que los clientes puedan tener acceso al punto de distribución basado en la nube, deben ser capaces de resolver el nombre del punto de distribución basado en la nube en una dirección IP que administra Azure. Los clientes hacen esto en dos fases:  

1.  Asignan el nombre del servicio que se ha proporcionado con el certificado del servicio de punto de distribución basado en la nube de Configuration Manager a su FQDN de servicio de Azure. Este FQDN contiene un GUID y el sufijo DNS de **cloudapp.net**. El GUID se genera automáticamente después de instalar el punto de distribución basado en la nube. Para ver el FDQN completo en Azure Portal, haga referencia a la **DIRECCIÓN URL DEL SITIO** en el panel del servicio en la nube. Una dirección URL del sitio de ejemplo es **http://d1594d4527614a09b934d470.cloudapp.net**.  

2.  Resuelven el FQDN de servicio de Azure en la dirección IP que Azure asigna. Esta dirección IP también puede identificarse en el panel del servicio en la nube en Azure Portal y recibe el nombre de **DIRECCIÓN IP VIRTUAL PÚBLICA (VIP)**.  

Para asignar el nombre de servicio proporcionado con el certificado de servicio de punto de distribución basado en la nube de Configuration Manager (por ejemplo, **clouddp1.contoso.com**) a su FQDN de servicio de Azure (por ejemplo, **d1594d4527614a09b934d470.cloudapp.net**), los servidores DNS de Internet deben tener un alias DNS (registro CNAME). Los clientes pueden entonces resolver el FQDN de servicio de Azure en la dirección IP mediante el uso de servidores DNS en Internet.  

##  <a name="BKMK_ConfigProxyforCloud"></a> Configurar parámetros proxy para sitios primarios que administran servicios en la nube  
 Cuando usa servicios en la nube con Configuration Manager, el sitio primario que administra el punto de distribución basado en la nube debe poder conectarse a Azure Portal. El sitio se conecta mediante la cuenta de **sistema** del equipo de sitio primario. Esta conexión se realiza mediante el explorador web predeterminado del equipo del servidor de sitio primario.  

 En el servidor de sitio primario que administra el punto de distribución basado en la nube, es posible que tenga que configurar parámetros proxy para habilitar el acceso del sitio primario a Internet y Azure.  

 Use el procedimiento siguiente para configurar los parámetros proxy para el servidor de sitio primario en la consola de Configuration Manager.  

> [!TIP]  
>  También puede configurar el servidor proxy al instalar nuevos roles de sistema de sitio en el servidor de sitio primario mediante el **Asistente para agregar roles de sistema de sitio**.  

#### <a name="to-set-up-proxy-settings-for-the-primary-site-server"></a>Para configurar parámetros proxy para el servidor de sitio primario  

1.  En la consola de Configuration Manager, haga clic en **Administración**.  

2.  En el área de trabajo **Administración** , expanda **Configuración del sitio**y, a continuación, haga clic en **Servidores y roles del sistema de sitios**. Después, seleccione el servidor de sitio primario que administra el punto de distribución basado en la nube.  

3.  En el panel de detalles, haga clic con el botón secundario en **Sistema de sitio**y, a continuación, haga clic en **Propiedades**.  

4.  En **Propiedades de sistema de sitio**, seleccione la pestaña **Proxy** y, después, establezca la configuración de proxy para este servidor de sitio primario.  

5.  Haga clic en **Aceptar** para guardar la configuración.  
