---
title: Configuración del análisis de escritorio
titleSuffix: Configuration Manager
description: Guía de procedimientos para configurar y la incorporación para análisis del escritorio.
ms.date: 04/15/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 7ff8d453-f24d-4230-a116-585190a663fc
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: b75b82f632c8bfbbc11a2b11d58ab83116e2180a
ms.sourcegitcommit: d23ccf7b95e6c2a6b156975194ebbc375cb5e6ea
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/22/2019
ms.locfileid: "60124444"
---
# <a name="how-to-set-up-desktop-analytics"></a>Cómo configurar el análisis de escritorio

> [!Note]  
> Esta información se relaciona con un servicio en versión preliminar que puede modificarse sustancialmente antes de su lanzamiento comercial. Microsoft no ofrece ninguna garantía, expresa o implícita, con respecto a la información aquí proporcionada.  

Utilice este procedimiento para iniciar sesión el análisis de escritorio y configurarlo en su suscripción. Este procedimiento es un proceso único para configurar los análisis de escritorio de su organización.  



## <a name="initial-onboarding"></a>Incorporación inicial

1. Abra el portal de análisis de escritorio en administración de dispositivos de Microsoft 365 como un usuario con **Administrador de la compañía** permisos. Seleccione **iniciar**.  

2. En el **acepte el contrato de servicio** página, revise el contrato de servicio y seleccione **Accept**.  

3. En el **confirmar la suscripción** página, revise la lista de requiere licencias aplicables. Cambiar el valor a **Sí** junto a **¿tiene una de las suscripciones compatibles o superiores**y, a continuación, seleccione **siguiente**.  

4. En el **dar acceso a los usuarios** página:

    - **¿Desea que el análisis de escritorio para administrar roles de directorio para los usuarios**: Escritorio Analytics asigna automáticamente el **propietarios del área de trabajo** y **colaboradores del área de trabajo** grupos a la **Desktop Administrator de análisis** rol. Si esos grupos ya están un **administrador Global**, no hay ningún cambio.  

        Si no selecciona esta opción, análisis de escritorio seguirá agregando los usuarios como miembros de dos grupos de seguridad. Un **administrador Global** debe asignar manualmente el **Desktop Analytics Administrator** rol para los usuarios.  

        Para obtener más información acerca de cómo asignar permisos del rol de administrador en Azure Active Directory y los permisos asignados a **Desktop Analytics administradores**, consulte [permisos del rol de administrador en Azure Active Directory](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles).  

    - Análisis de escritorio preconfigura dos grupos de seguridad en Azure Active Directory:  

        - **Los propietarios del área de trabajo**: Un grupo de seguridad para crear y administrar áreas de trabajo. Estas cuentas necesitan acceso de propietario a la suscripción de Azure.  

        - **Los colaboradores del área de trabajo**: Un grupo de seguridad para crear y administrar planes de implementación en esta área de trabajo. No necesitan ningún acceso de Azure adicionales.  

        Para agregar un usuario a cualquier grupo, escriba su dirección de correo electrónico o de nombre en el **escriba la dirección de correo electrónico o nombre** sección del grupo adecuado. Cuando termine, seleccione **siguiente**.

El siguiente paso puede realizarse mediante un **propietario del área de trabajo** o **colaborador**. Consulte [requisitos previos.](/sccm/desktop-analytics/overview#prerequisites) 

5. En la página para **configurar el área de trabajo**:  

    - Para usar un área de trabajo para el análisis de escritorio, selecciónela y continúe con el paso siguiente.  

        > [!Note]  
        > Si ya utiliza Windows Analytics, seleccione esa misma área de trabajo. Deberá volver a inscribir dispositivos para el análisis de escritorio que ya tiene inscritos en Windows Analytics.
        >
        > Solo puede tener un área de trabajo de análisis de escritorio por inquilino de Azure AD. Los dispositivos solo pueden enviar datos de diagnóstico a un área de trabajo.  

    - Para crear un área de trabajo para el análisis de escritorio, seleccione **Agregar área de trabajo**.  

        1. Escriba un **nombre de área de trabajo**.<!--do we have any guidance for this name?-->  

        2. Seleccione la lista desplegable para **seleccione el nombre de la suscripción de Azure para esta área de trabajo**y elija la suscripción de Azure para esta área de trabajo.  

        3. Seleccione el **región** en la lista y, a continuación, seleccione **agregar**.  

6. Seleccione un área de trabajo nueva o existente y, a continuación, seleccione **establecer como área de trabajo de análisis de escritorio**.  A continuación, seleccione **continuar** en el **confirmar y concederle acceso** cuadro de diálogo.  

7. En la nueva pestaña del explorador, elija una cuenta para que use para iniciar sesión. Seleccione la opción de **dar su consentimiento en nombre de su organización** y seleccione **Accept**.  

    > [!Note]  
    > Este consentimiento consiste en asignar el rol de lector de Log Analytics para el área de trabajo de la aplicación de MALogAnalyticsReader. Este rol de aplicación es necesario por el análisis de escritorio. Para obtener más información, consulte [rol de aplicación MALogAnalyticsReader](/sccm/desktop-analytics/troubleshooting#bkmk_MALogAnalyticsReader).  

8. En la página a **configurar el área de trabajo**, seleccione **siguiente**.  

9. En el **últimos pasos** página, seleccione **vaya al escritorio Analytics**.

El portal de Azure muestra el análisis de escritorio **inicio** página.



## <a name="create-app-for-configuration-manager"></a>Crear aplicación de Configuration Manager

Crear una aplicación en Azure AD para Configuration Manager.

1. Abra el [portal Azure](http://portal.azure.com) como un usuario con permisos de administrador de empresa, vaya a **Azure Active Directory**y seleccione **registros de aplicaciones**. A continuación, seleccione **nuevo registro de aplicaciones**.  

2. En el **crear** del panel, configure las siguientes opciones:  

    - **Nombre**: un nombre único que identifica la aplicación, por ejemplo: `Desktop-Analytics-Connection`  

    - **Tipo de aplicación**: **Aplicación Web / API**  

    - **Dirección URL de inicio de sesión**: este valor no se usa Configuration Manager, pero necesario para Azure AD. Escriba una dirección URL válida y única, por ejemplo: `https://configmgrapp`  
  
   Seleccione **crear**.  

3. Seleccione la aplicación y tenga en cuenta la **Id. de aplicación**. Este valor es un GUID que se usa para configurar la conexión de Configuration Manager.  

4. Seleccione **configuración** en la aplicación y, a continuación, seleccione **claves**. En el **contraseñas** sección, especifique un **descripción de la clave**, especifique una fecha de expiración **duración**y, a continuación, seleccione **guardar**. Copia el **valor** de la clave, que se usa para configurar la conexión de Configuration Manager.

    > [!Important]  
    > Esta es la única oportunidad para copiar el valor de clave. Si no copia ahora, deberá crear otra clave.  
    >
    > Guarde el valor de clave en una ubicación segura.  

5. En la aplicación **configuración** panel, seleccione **permisos necesarios**.  

    1. En el **permisos necesarios** panel, seleccione **agregar**.  

    2. En el **agregar acceso de API** panel, **seleccionar una API**.  

    3. Busque el **Microservicio del Administrador de configuración** API. Selecciónelo y, a continuación, elija **seleccione**.  

    4. En el **habilitar acceso** del panel, seleccione los permisos de aplicación: **Escribir datos de colección CM** y **leer datos de colección CM**. A continuación, elija **seleccione**.  

    5. En el **agregar acceso de API** panel, seleccione **realiza**.  

6. En el **permisos necesarios** página, seleccione **concederlos**. Seleccione **Sí**.  

7. Copie el identificador de inquilino de Azure AD. Este valor es un GUID que se usa para configurar la conexión de Configuration Manager. Seleccione **Azure Active Directory** en el menú principal y, a continuación, seleccione **propiedades**. Copia el **Id. de directorio** valor.  



## <a name="next-steps"></a>Pasos siguientes

Avance al siguiente artículo para conectar Configuration Manager con análisis de escritorio.
> [!div class="nextstepaction"]  
> [Conectar Configuration Manager](/sccm/desktop-analytics/connect-configmgr)  
