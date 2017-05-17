---
title: Configurar el cliente de Endpoint Protection | Microsoft Docs
description: "Obtenga información sobre cómo establecer una configuración de cliente personalizada para Endpoint Protection que se puede implementar en recopilaciones de equipos de la jerarquía."
ms.custom: na
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
caps.latest.revision: 21
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: bff083fe279cd6b36a58305a5f16051ea241151e
ms.openlocfilehash: 2d7ec9cc626f3ccfded990cf8ba392c4979adfee
ms.contentlocale: es-es
ms.lasthandoff: 12/16/2016


---

# <a name="configure-custom-client-settings-for-endpoint-protection"></a>Establecer una configuración de cliente personalizada para Endpoint Protection

*Se aplica a: System Center Configuration Manager (rama actual)*

En este procedimiento se establece una configuración de cliente personalizada para Endpoint Protection que se puede implementar en recopilaciones de equipos de la jerarquía.

> [!IMPORTANT]
>  No establezca la configuración de cliente de Endpoint Protection predeterminada a menos que esté seguro de que quiere aplicarla a todos los equipos de la jerarquía.

## <a name="to-enable-endpoint-protection-and-configure-custom-client-settings"></a>Para habilitar Endpoint Protection y establecer la configuración de cliente personalizada

1.  En la consola de Configuration Manager, haga clic en **Administración**.

2.  En el área de trabajo **Administración** , haga clic en **Configuración de cliente**.

3.  En la pestaña **Inicio** , del grupo **Crear** , haga clic en **Crear configuración de dispositivo de cliente personalizada**.

4.  En el cuadro de diálogo **Crear configuración de dispositivo de cliente personalizada** , proporcione un nombre y una descripción para el grupo de opciones y luego seleccione **Endpoint Protection**.

5.  Configure las opciones de cliente de Endpoint Protection que necesite. Para obtener una lista completa de las opciones de configuración de cliente de Endpoint Protection que puede establecer, consulte la sección Endpoint Protection del tema [About client settings in System Center Configuration Manager](../../core/clients/deploy/about-client-settings.md) (Acerca de la configuración de cliente en System Center Configuration Manager).

   > [!IMPORTANT]
   >  Para configurar las opciones de cliente de Endpoint Protection, primero debe instalar el rol de sistema de sitio de Endpoint Protection.

6.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Crear configuración de dispositivo de cliente personalizada** . Las nuevas opciones de cliente se muestran en el nodo **Configuración de cliente** del área de trabajo **Administración** .

7.  Para poder usar las opciones de cliente personalizadas, primero debe implementarlas en una recopilación. Seleccione las opciones de cliente personalizadas que quiere implementar y luego, en la pestaña **Inicio** del grupo **Configuración de cliente** , haga clic en **Implementar**.

8.  En el cuadro de diálogo **Seleccionar recopilación** , elija la recopilación en la que quiere implementar las opciones de cliente y haga clic en **Aceptar**. La nueva implementación se muestra en la pestaña **Implementaciones** del panel de detalles.

Los equipos cliente se configurarán con estas opciones la próxima vez que descarguen directivas de cliente. Para iniciar la recuperación de directivas para un solo cliente, consulte la sección Initiate Policy Retrieval for a Configuration Manager Client (Iniciar la recuperación de directivas para un cliente de Configuration Manager) en [How to manage clients in System Center Configuration Manager](../../core/clients/manage/manage-clients.md) (Cómo administrar clientes en System Center Configuration Manager).

## <a name="how-to-provision-the-endpoint-protection-client-in-a-disk-image-in-configuration-manager"></a>Aprovisionamiento del cliente de Endpoint Protection en una imagen de disco en Configuration Manager
Puede instalar el cliente de Endpoint Protection en un equipo que planee usar como origen de imagen del disco para la implementación del sistema operativo de Configuration Manager. Este equipo se denomina normalmente el equipo de referencia. Después de crear la imagen del sistema operativo, puede usar la implementación de sistema operativo de Configuration Manager para implementar la imagen que puede contener paquetes de software, incluido Endpoint Protection, en equipos cliente.

Use los procedimientos de este tema para ayudarle a instalar y configurar el cliente de Endpoint Protection en un equipo de referencia.

### <a name="prerequisites-for-installing-the-endpoint-protection-client-on-the-reference-computer"></a>Requisitos previos para instalar al cliente de Endpoint Protection en el equipo de referencia
La lista siguiente contiene los requisitos previos necesarios para la instalación del software cliente de Endpoint Protection en un equipo de referencia.

-   Debe tener acceso al paquete de instalación de cliente de Endpoint Protection, **scepinstall.exe**. Este paquete se encuentra en la carpeta **Cliente** de la carpeta de instalación de Microsoft System Center Configuration Manager en el servidor de sitio.

-   Para asegurarse de que el cliente de Endpoint Protection está implementado con la configuración necesaria en su organización, cree una directiva antimalware y, después, exporte la directiva. Puede especificar la directiva antimalware que se usará al instalar manualmente el cliente de Endpoint Protection. Para obtener más información, consulte [How to create and deploy antimalware policies for Endpoint Protection in System Center Configuration Manager](endpoint-antimalware-policies.md) (Crear e implementar directivas antimalware para Endpoint Protection en System Center Configuration Manager).

   > [!NOTE]
   >  La **directiva antimalware de cliente predeterminada** no se puede exportar.

-   Si quiere instalar el cliente de Endpoint Protection con las definiciones más recientes, debe descargarlas de [Microsoft Malware Protection Center](http://go.microsoft.com/fwlink/?LinkID=200965) (Centro de protección contra malware de Microsoft).

### <a name="how-to-install-the-endpoint-protection-client-software-on-the-reference-computer"></a>Instalación del software cliente de Endpoint Protection en el equipo de referencia
Puede instalar el cliente de Endpoint Protection localmente en el equipo de referencia desde un símbolo del sistema. Para ello, primero debe obtener el archivo de instalación **scepinstall.exe**. También puede instalar el cliente con una directiva antimalware preconfigurada o con una directiva antimalware exportada anteriormente.

## <a name="to-install-the-endpoint-protection-client-from-a-command-prompt"></a>Para instalar el cliente de Endpoint Protection desde un símbolo del sistema

1.  Copie **scepinstall.exe** de la carpeta **Cliente** que se encuentra en el medio de instalación de System Center Configuration Manager en el equipo en el que quiere instalar el software cliente de Endpoint Protection.

2.  Abra un símbolo del sistema con privilegios administrativos, navegue hasta la carpeta en la que se encuentra **scepinstall.exe** y, a continuación, ejecute el comando siguiente, añadiendo las propiedades de línea de comandos adicionales necesarias:

   ```
   scepinstall.exe
   ```

    Puede especificar una de las propiedades de línea de comandos siguientes:

   |Propiedad|Descripción|
   |--------------|-----------------|
   |/s|Especifica que se realizará una instalación silenciosa.|
   |/q|Especifica que se realizará una extracción silenciosa de los archivos de instalación.|
   |/i|Especifica que se debe realizar una instalación normal.|
   |/noreplace|Especifica que el software antimalware de otros fabricantes no se desinstala durante la instalación.|
   |/policy|Especifica la utilización de un archivo de directiva antimalware para configurar el cliente durante la instalación.|
   |/sqmoptin|Especifica que la instalación del software cliente participa en el programa para la mejora de la experiencia del usuario de Microsoft.|

3.  Siga las instrucciones en la pantalla para completar la instalación del cliente.

4.  Si descargó el paquete de definición de actualización más reciente, copie el paquete en el equipo cliente y, a continuación, haga doble clic en el paquete de definición para instalarlo.

   > [!NOTE]
   >  Después de completar la instalación del cliente de Endpoint Protection, el cliente realiza automáticamente una comprobación de actualización de definición. Si esta comprobación de actualización se realiza correctamente, no es necesario instalar manualmente el paquete de actualización de definición más reciente.

## <a name="to-install-the-client-software-with-an-antimalware-policy-from-the-command-prompt"></a>Para instalar el software cliente con una directiva antimalware desde el símbolo del sistema

1.  Copie **scepinstall.exe** y la directiva antimalware exportada o preconfigurada en el equipo en el que quiere instalar el software cliente de Endpoint Protection.

2.  Abra un símbolo del sistema con privilegios administrativos, navegue hasta la carpeta en la que se encuentra **scepinstall.exe** y la directiva antimalware y, a continuación, ejecute el comando siguiente:

   ```
   scepinstall.exe /policy <full path>\<policy file>
   ```

3.  Siga las instrucciones en la pantalla para completar la instalación del cliente.

4.  Si descargó el paquete de definición más reciente, copie el paquete en el equipo cliente y, a continuación, haga doble clic en el paquete de definición para instalarlo.

   > [!NOTE]
   >  Después de completar la instalación del cliente de Endpoint Protection, el cliente realiza automáticamente una comprobación de actualización de definición. Si esta comprobación de actualización se realiza correctamente, no es necesario instalar manualmente el paquete de actualización de definición más reciente.

## <a name="verify-that-the-endpoint-protection-client-is-installed-correctly"></a>Comprobar que el cliente de Endpoint Protection está instalado correctamente
Después de instalar el cliente de Endpoint Protection en el equipo de referencia, compruebe que funciona correctamente.

### <a name="to-verify-that-the-endpoint-protection-client-is-installed-correctly"></a>Para comprobar que el cliente de Endpoint Protection está instalado correctamente

1.  En el equipo de referencia, abra **System Center Endpoint Protection** desde el área de notificaciones de Windows.

2.  En la pestaña **Inicio** del cuadro de diálogo **System Center Endpoint Protection**, compruebe que la opción **Protección en tiempo real** está configurada como **Activa**.

3.  Compruebe que se muestra **Actualizadas** para **Definiciones de virus y spyware**.

4.  Para asegurarse de que su equipo de referencia está listo para crear imágenes, en **Opciones de escaneado**, seleccione **Completa**y, a continuación, seleccione **Escanear ahora**.

### <a name="how-to-prepare-the-endpoint-protection-client-for-imaging"></a>Preparación del cliente de Endpoint Protection para la creación de imágenes
Después de comprobar que el cliente de Endpoint Protection está instalado correctamente en el equipo de referencia, puede preparar el equipo para la creación de imágenes. Realice los pasos siguientes para preparar el cliente de Endpoint Protection para la creación de imágenes.


Para obtener más información sobre la implementación de sistema operativo en Configuration Manager, consulte [Manage operating system images with System Center Configuration Manager](/sccm/osd/get-started/manage-operating-system-images) (Administrar imágenes de sistema operativo con System Center Configuration Manager).

### <a name="to-prepare-the-endpoint-protection-client-for-imaging"></a>Para preparar al cliente de Endpoint Protection para la creación de imágenes

1.  En el equipo de referencia, inicie sesión como usuario con privilegios administrativos.

2.  Descargue e instale **PsTools** del [sitio de Windows SysInternals](http://go.microsoft.com/fwlink/?LinkId=215263) en TechNet.

3.  Abra un símbolo del sistema con privilegios elevados, navegue hasta la carpeta en la que instaló PsTools y, a continuación, escriba el siguiente comando

   ```
   Psexec.exe -s -i regedit.exe
   ```

   > [!IMPORTANT]
   >  Ejecute el Editor del Registro con precaución, ya que la opción -s en PsExec.exe ejecuta el Editor del Registro con privilegios LocalSystem.

4.  En el Editor del Registro, vaya a cada una de las siguientes claves del Registro y elimínelas.

   > [!IMPORTANT]
   >  Debe eliminar las claves del Registro como último paso antes de crear las imágenes en el equipo de referencia. Las claves del Registro se vuelven a crear cuando se inicia el cliente de Endpoint Protection. Si reinicia el equipo de referencia, debe volver a eliminar las claves del Registro.

   -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\InstallTime**

   -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastScanRun**

   -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastScanType**

   -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastQuickScanID**

   -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastFullScanID**

   -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\RemovalTools\MRT\GUID**

Después de completar los pasos anteriores, puede preparar el equipo de referencia para la creación de imágenes. Para obtener más información sobre la implementación de sistema operativo en Configuration Manager, consulte [Manage operating system images with System Center Configuration Manager](/sccm/osd/get-started/manage-operating-system-images) (Administrar imágenes de sistema operativo con System Center Configuration Manager).

Si se implementa una imagen que contiene el software cliente de Endpoint Protection, el cliente de Endpoint Protection automáticamente notificará información al sitio de Configuration Manager al que el equipo está asignado, y se descargará y aplicará la directiva aplicable al equipo cliente.

