---
title: Configuración del análisis de escritorio
titleSuffix: Configuration Manager
description: Guía de procedimientos para la configuración y la incorporación de análisis de escritorio.
ms.date: 09/03/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 7ff8d453-f24d-4230-a116-585190a663fc
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: ae1bbbd6a8482ea5008eeb87c30a4e35a26e06d0
ms.sourcegitcommit: 84a6f31797490eeda73bd4f3656ba27741df3030
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/27/2019
ms.locfileid: "71343804"
---
# <a name="how-to-set-up-desktop-analytics"></a>Cómo configurar el análisis de escritorio

> [!Note]  
> Esta información está relacionada con un servicio de vista previa que se puede modificar sustancialmente antes de que se publique comercialmente. Microsoft no ofrece ninguna garantía, expresa o implícita, con respecto a la información aquí proporcionada.  

Use este procedimiento para iniciar sesión en análisis de escritorio y configurarlo en su suscripción. Este procedimiento es un proceso único para configurar el análisis de escritorio de su organización.  


> [!Important]  
> Para obtener información sobre los requisitos previos generales para el análisis de escritorio con Configuration Manager, consulte [requisitos previos](/sccm/desktop-analytics/overview#prerequisites).  

## <a name="initial-onboarding"></a>Incorporación inicial

1. Abra el [portal de análisis de escritorio](https://aka.ms/desktopanalytics) en Microsoft 365 administración de dispositivos como usuario con el rol de **administrador global** . Seleccione **iniciar**. Como alternativa, en la consola de Configuration Manager, vaya al área de trabajo **biblioteca de software** , seleccione el nodo servicio de **análisis de escritorio** y seleccione **planear implementaciones**.

2. En la página **aceptar el contrato de servicio** , revise el contrato de servicio y seleccione **Aceptar**.  

3. En la página **confirmar la suscripción** , revise la lista de licencias aptas necesarias. Cambie la configuración a **sí** junto a **¿tiene una o más**suscripciones admitidas y, a continuación, seleccione **siguiente**.  

4. En la página **conceder acceso a los usuarios** :

    - **Permita que el análisis de escritorio administre los roles de directorio en su nombre**: El análisis de escritorio asigna automáticamente a los **propietarios del área de trabajo** el rol de **Administrador de análisis de escritorio** . Si esos grupos ya son **administradores globales**, no hay ningún cambio.

        Si no selecciona esta opción, el análisis de escritorio todavía agrega usuarios como miembros del grupo de seguridad. Un **administrador global** debe asignar manualmente el rol de **Administrador de análisis de escritorio** para los usuarios.   

        Para obtener más información sobre la asignación de permisos de rol de administrador en Azure Active Directory y los permisos asignados a **los administradores de análisis de escritorio**, consulte [permisos de rol de administrador en Azure Active Directory](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles).  

    - Análisis de escritorio configura previamente el grupo de seguridad **propietarios del área de trabajo** en Azure Active Directory para crear y administrar áreas de trabajo y planes de implementación. 

        Para agregar un usuario al grupo, escriba su nombre o dirección de correo electrónico en la sección **escribir el nombre o la dirección de correo electrónico** . Cuando termine, seleccione **siguiente**.

5. En la página para **configurar el área de trabajo**:  

    - Para usar un área de trabajo existente para el análisis de escritorio, selecciónela y continúe con el siguiente paso.  

        > [!Note]  
        > Solo puede tener un área de trabajo de análisis de escritorio por inquilino de Azure AD. Los dispositivos solo pueden enviar datos de diagnóstico a un área de trabajo.  

        Si ya está usando Windows Analytics, seleccione la misma área de trabajo. Debe volver a inscribir dispositivos en el análisis de escritorio que se inscribió anteriormente en Windows Analytics.

        Para migrar entradas del área de trabajo de Windows Analytics seleccionada, establezca **¿desea ver las entradas de Windows Analytics?** en **sí**. Si no desea migrar, cambie esta configuración a **no**. Para obtener más información, consulte las preguntas más frecuentes sobre [los clientes existentes de Windows Analytics](/sccm/desktop-analytics/faq#existing-windows-analytics-customers).

    - Para crear un área de trabajo para el análisis de escritorio, seleccione **Agregar área de trabajo**.  

        1. Escriba un **nombre de área de trabajo**único global.<!--do we have any guidance for this name?-->  

        2. Seleccione la lista desplegable para **seleccionar el nombre de la suscripción de Azure para esta área de trabajo**y elija la suscripción de Azure para esta área de trabajo.  

        3. **Crear nuevo** Grupo de recursos o **usar existente**.

        4. Seleccione la **región** en la lista y, a continuación, seleccione **Agregar**.  

6. Seleccione un área de trabajo nueva o existente y, a continuación, seleccione **establecer como área de trabajo de análisis de escritorio**.  Después, seleccione **continuar** en el cuadro de diálogo **confirmar y conceder acceso** .  

7. En la pestaña nuevo explorador, seleccione una cuenta para iniciar sesión. Seleccione la opción para dar **su consentimiento en nombre de su organización** y seleccione **Aceptar**.  

    > [!Note]  
    > Este consentimiento es asignar a la aplicación MALogAnalyticsReader el rol lector Log Analytics para el área de trabajo. El análisis de escritorio requiere este rol de aplicación. Para obtener más información, vea [rol de aplicación MALogAnalyticsReader](/sccm/desktop-analytics/troubleshooting#bkmk_MALogAnalyticsReader).  

8. De nuevo en la página para **configurar el área de trabajo**, seleccione **siguiente**.  

9. En la página **últimos pasos** , seleccione **ir a análisis de escritorio**.

En el Azure Portal se muestra la página **principal** de análisis de escritorio.


## <a name="next-steps"></a>Pasos siguientes

Continúe con el siguiente artículo para conectarse Configuration Manager con análisis de escritorio.
> [!div class="nextstepaction"]  
> [Conectar Configuration Manager](/sccm/desktop-analytics/connect-configmgr)  
