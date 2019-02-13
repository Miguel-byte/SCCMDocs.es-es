---
title: Creación de perfiles de certificado PFX mediante una entidad de certificación
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo usar archivos PFX en System Center Configuration Manager para generar certificados específicos del usuario que admiten el intercambio de datos cifrados.
ms.date: 11/01/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: d240a836-c49b-49ab-a920-784c062d6748
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6bbe52a282db016077cb96144938a0d443955f6c
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56127446"
---
# <a name="how-to-create-pfx-certificate-profiles-using-a-certificate-authority"></a>Creación de perfiles de certificado PFX mediante una entidad de certificación

*Se aplica a: System Center Configuration Manager (Rama actual)*

A continuación, aprenderá a crear un perfil de certificado que utiliza una entidad de certificación para las credenciales.

Los [perfiles de certificado](../../protect/deploy-use/introduction-to-certificate-profiles.md) proporcionan información general sobre la creación y configuración de perfiles de certificado. En este tema se destaca información específica sobre perfiles de certificado relacionados con certificados PFX.

## <a name="pfx-certificate-profiles"></a>Perfiles de certificado PFX
System Center Configuration Manager permite crear un perfil de certificado PFX mediante las credenciales que emite una entidad de certificación.  A partir de la versión 1706, se puede elegir Microsoft o Entrust como entidad de certificación.  Cuando se implementan en dispositivos de usuario, los archivos de intercambio de información personal (.pfx) generan certificados específicos del usuario para poder intercambiar datos cifrados.

Con el objetivo de importar las credenciales de certificado a partir de archivos de certificado existentes, consulte [Creación de perfiles de certificado PFX mediante la importación de detalles de certificado](../../mdm/deploy-use/import-pfx-certificate-profiles.md).

## <a name="create-and-deploy-a-personal-information-exchange-pfx-certificate-profile"></a>Creación e implementación de un perfil de certificado de intercambio de información personal (PFX)  

### <a name="get-started"></a>Introducción

1.  En la consola de System Center Configuration Manager, elija **Activos y compatibilidad**.  
2.  En el área de trabajo **Activos y compatibilidad**, elija **Configuración de cumplimiento** &gt;**Acceso a los recursos de la compañía** &gt; **Perfiles de certificado**.  

3.  En la pestaña **Inicio** del grupo **Crear**, seleccione **Crear perfil de certificado**.

4.  En la página **General** del asistente para **Crear perfil de certificado** , especifique la información siguiente:  

    -   **Nombre**: Escriba un nombre único para el perfil de certificado. Puede utilizar un máximo de 256 caracteres.  

    -   **Descripción**: facilite una descripción general del perfil de certificado y cualquier otra información adicional pertinente para identificarlo en la consola de System Center Configuration Manager. Puede utilizar un máximo de 256 caracteres.  

    -   En **Especifique el tipo de perfil de certificado que desea crear.**, elija **Intercambio de información personal -- Configuración de PKCS #12 (PFX) -- Crear** y, luego, seleccione la entidad de certificación de la lista desplegable.  A partir de la versión 1706, se puede elegir **Microsoft** o **Entrust**.

### <a name="select-supported-platforms"></a>Selección de plataformas compatibles

La página Plataformas admitidas identifica los sistemas operativos y dispositivos que admiten el perfil de certificado.  

Los perfiles de certificado pueden admitir varios sistemas operativos y dispositivos; sin embargo, hay algunas combinaciones de sistemas operativos o dispositivos que pueden requerir otra configuración.  En estos casos, se recomienda crear perfiles distintos para cada configuración.  

A partir de la versión 1710, están disponibles las siguientes opciones:

- Windows 10
    - Todo Windows 10 (64 bits)
    - Todo Windows 10 (32 bits)
    - Todo Windows 10 (ARM64)
    - Todo Windows 10 Holographic Enterprise y posterior
    - Todo Windows 10 Holographic y posterior
    - Todo Windows 10 Team y posterior
    - Todo Windows 10 Mobile y posterior
- iPhone
- iPad
- Android
- Android for Work

> [!Note]  
> En estos momentos, no se admiten dispositivos macOS ni OSX.  

Cuando no se selecciona ninguna otra opción, la casilla **Seleccionar todo** elige todas las que hay disponibles.  Cuando se eligen una o varias opciones, **Seleccionar todo** borra las selecciones que haya hechas. 

1.  Seleccione una o varias plataformas compatibles con el perfil de certificado.

1.  Pulse **Siguiente** para continuar.  


### <a name="configure-certification-authorities"></a>Configuración de entidades de certificación

En Configurar entidades de certificación puede elegir el punto de registro de certificados (CRP) para procesar los certificados PFX.  

1.  En la lista **Sitio primario**, elija el servidor que contenga el rol de CRP para la entidad de certificación.
1.  En la lista de **entidades de certificación**, elija la entidad de certificación pertinente colocando una marca de verificación en la columna izquierda.
1.  Cuando esté listo para continuar, haga clic en **Siguiente**.

Para obtener más información, consulte [Infraestructura de certificados](../../protect/deploy-use/certificate-infrastructure.md).


### <a name="configure-certificate-settings-for-microsoft-ca"></a>Configuración de las opciones de certificación de la entidad de certificación de Microsoft

Para configurar las opciones de certificación cuando se utilice Microsoft como la entidad de certificación, siga estos pasos:

1.  En la lista desplegable **Nombre de plantilla de certificado**, elija la plantilla de certificado.

1.  Active la casilla **Uso de certificado** para usar el perfil de certificado de firma o cifrado S/MIME.

    Al seleccionar esta opción mientras se utiliza Microsoft como la entidad de certificación, todos los certificados PFX asociados al usuario de destino se entregan a todos los dispositivos que haya inscrito el usuario.  Cuando esta casilla está desactivada, cada dispositivo recibe un único certificado.  

1.  Establezca **Formato de nombre de sujeto** en **Nombre común** o **Nombre completo**.  Si sabe con seguridad cuál usar, póngase en contacto con el administrador de su entidad de certificación.

1.  En **Nombre alternativo del firmante**, habilite **Dirección de correo electrónico** y **Nombre principal del usuario (UPN)** según cuál sea la entidad de certificación.

1.  **Umbral de renovación** determina si los certificados se renuevan automáticamente, en función del porcentaje de tiempo que quede antes de la expiración.

1.  Establezca **Período de validez del certificado** en la duración del certificado.  El período se especifica estableciendo un número (1-100) y un período (años, meses o días).

1.  **Publicación de Active Directory** se habilita cuando el punto de registro de certificados especifica las credenciales de Active Directory.  Habilite la opción para publicar el perfil de certificado en Active Directory.

1.  Si ha seleccionado una o varias plataformas Windows 10 al especificar las plataformas admitidas, siga estos pasos:

    1.  Establezca **Almacén de certificados de Windows** en **Usuario**  (la opción **Equipo local** no implementa certificados y, por tanto, no debe seleccionarse).
    1.  Seleccione el **proveedor de almacenamiento de claves (KSP)** de una de las siguientes opciones:

        - **Instalar en Módulo de plataforma segura (TPM) si está presente**  
        - **Instalar en Módulo de plataforma segura (TPM) o se producirá un error** 
        - **Instalar en Windows Hello para empresas o generar un error** 
        - **Instalar en Proveedor de almacenamiento de claves de software** 

1.  Cuando termine, elija **Siguiente** o **Resumen**.

### <a name="configure-certificate-settings-for-entrust-ca"></a>Configuración de las opciones de certificación de la entidad de certificación de Entrust

Para configurar las opciones de certificación cuando se utilice Entrust como la entidad de certificación, siga estos pasos:

1.  En la lista desplegable **Configuración de identificador digital**, elija el perfil de configuración.  Las opciones de configuración de identificador digital se crean con el administrador de Entrust.

1.  Cuando se activa la casilla **Uso de certificado**, se utiliza el perfil de certificado de firma o cifrado S/MIME.

    Al utilizar Entrust como la entidad de certificación, todos los certificados PFX asociados al usuario de destino se entregan a todos los dispositivos que haya inscrito el usuario.    Cuando esta opción *no* está activada, cada dispositivo recibe un único certificado  (el comportamiento será distinto según la entidad emisora; para obtener más información, consulte la sección correspondiente).

1.  Use el botón **Formatear** para asignar los tokens de **Formato de nombre del firmante** de Entrust a los campos de ConfigMgr.  

    El cuadro de diálogo **Formato de nombre de sujeto de certificado** enumera las variables de configuración de identificador digital de Entrust.  En cada variable de Entrust, elija la variable adecuada de LDAP de la lista desplegable asociada.

1.  Use el botón **Formatear** para asignar los tokens de **Nombre alternativo del firmante** de Entrust a las variables admitidas de LDAP.  

    El cuadro de diálogo **Formato de nombre de sujeto de certificado** enumera las variables de configuración de identificador digital de Entrust.  En cada variable de Entrust, elija la variable adecuada de LDAP de la lista desplegable asociada.

1.  **Umbral de renovación** determina si los certificados se renuevan automáticamente, en función del porcentaje de tiempo que quede antes de la expiración.

1.  Establezca **Período de validez del certificado** en la duración del certificado.  El período se especifica estableciendo un número (1-100) y un período (años, meses o días).

1.  **Publicación de Active Directory** se habilita cuando el punto de registro de certificados especifica las credenciales de Active Directory.  Habilite la opción para publicar el perfil de certificado en Active Directory.

1.  Si ha seleccionado una o varias plataformas Windows 10 al especificar las plataformas admitidas, siga estos pasos:

    1.  Establezca **Almacén de certificados de Windows** en **Usuario**  (la opción **Equipo local** no implementa certificados y, por tanto, no debe seleccionarse).
    1.  Seleccione el **proveedor de almacenamiento de claves (KSP)** de una de las siguientes opciones:

        - **Instalar en Módulo de plataforma segura (TPM) si está presente**  
        - **Instalar en Módulo de plataforma segura (TPM) o se producirá un error** 
        - **Instalar en Windows Hello para empresas o generar un error** 
        - **Instalar en Proveedor de almacenamiento de claves de software** 

1.  Cuando termine, elija **Siguiente** o **Resumen**.


### <a name="finish-up"></a>Finalizar

1.  En la página Resumen, revise las selecciones y compruebe las opciones.

1.  Cuando esté listo, elija **Siguiente** para crear el perfil.  

1.  El perfil de certificado que contiene el archivo PFX ya está disponible en el área de trabajo **Perfiles de certificado** . 

1.  Para implementar el perfil, siga estos pasos:

    1. Abra el área de trabajo **Activos y compatibilidad**.
    1. Elija **Configuración de cumplimiento** > **Acceso a los recursos de la compañía** > **Perfiles de certificado**
    1. Haga clic con el botón derecho en el perfil de certificado que desee y, luego, elija **Implementar**. 


## <a name="see-also"></a>Consulte también
[Crear un nuevo perfil de certificado](../../protect/deploy-use/create-certificate-profiles.md) le guiará a través del Asistente para crear perfil de certificado.

[Creación de perfiles de certificado PFX mediante la importación de detalles de certificado](../../mdm/deploy-use/import-pfx-certificate-profiles.md).

[Implementación de perfiles de Wi-Fi, VPN, correo electrónico y certificado](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md) describe cómo implementar perfiles de certificado.
