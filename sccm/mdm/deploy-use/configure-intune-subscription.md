---
title: "Configuración de su suscripción a Intune mediante System Center Configuration Manager | Microsoft Docs"
description: "Configuración de su suscripción a Intune mediante System Center Configuration Manager."
ms.custom: na
ms.date: 06/02/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 99de8fe7-560e-401a-8ab2-6d87d091be17
caps.latest.revision: 18
caps.handback.revision: 0
author: mtillman
ms.author: mtillman
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 662901e850566756759fcfc61c58f3c0e56bc5aa
ms.openlocfilehash: 22d890c972d3166f9c7b583d8d3fa917c1897880
ms.contentlocale: es-es
ms.lasthandoff: 06/03/2017

---
# <a name="configure-your-intune-subscription-with-system-center-configuration-manager-and-microsoft-intune"></a>Configuración de su suscripción a Intune con System Center Configuration Manager y Microsoft Intune

*Se aplica a: System Center Configuration Manager (rama actual)*

La suscripción de Intune le permite administrar dispositivos a través de Internet. Esto incluye la especificación de qué recopilación de usuarios puede inscribir dispositivos y la definición de la información que se presenta a los usuarios. Al crear la suscripción a Intune, también puede agregar personalización de marca de la compañía al portal de la compañía de Intune con el logotipo de la compañía y combinaciones de colores personalizadas.

La suscripción a Intune hace lo siguiente:

-   Recupera el certificado que el punto de conexión de servicio requiere para establecer la conexión con el servicio de Intune.
-   Define la recopilación de usuarios que permite a los usuarios inscribir dispositivos móviles.
-   Define y configura las plataformas móviles que se quieren admitir.

> [!IMPORTANT]
>  Al crear una suscripción de Microsoft Intune en Configuration Manager, el punto de conexión de servicio del sitio se colocará en "modo en línea". Consulte [Acerca del punto de conexión de servicio en System Center Configuration Manager](../../core/servers/deploy/configure/about-the-service-connection-point.md).

## <a name="to-create-the-microsoft-intune-subscription"></a>Para crear la suscripción a Microsoft Intune

1.  Si aún no lo ha hecho, regístrese para obtener una cuenta de Microsoft Intune en [Microsoft Intune](http://go.microsoft.com/fwlink/?LinkID=258216).  Después de crear la cuenta de Intune, no tiene que agregar usuarios a la cuenta de Intune ni realizar configuraciones adicionales.

2.  En la consola de Configuration Manager, haga clic en **Administración**.

3.  En el área de trabajo **Administración** , expanda **Servicios en la nube**y haga clic en **Suscripciones de Microsoft Intune**. En la pestaña **Inicio** , haga clic en **Agregar suscripción de Microsoft Intune**.

![Crear una suscripción a Intune](../media/mdm-set-intune.png)

4.  En la página **Introducción** del Asistente para crear suscripción de Microsoft Intune, revise el texto y haga clic en **Siguiente**.

5.  En la página **Suscripción** , haga clic en **Iniciar sesión** e inicie sesión con su cuenta profesional o educativa. En el cuadro de diálogo **Establecer entidad de administración de dispositivos móviles**, active la casilla para administrar solo dispositivos móviles mediante Configuration Manager a través de la consola de Configuration Manager. Para continuar con su suscripción, debe seleccionar esta opción.

    > [!IMPORTANT]
    >  Una vez que seleccione Configuration Manager como entidad de administración, solo puede cambiar la entidad de administración a Microsoft Intune en Configuration Manager versión 1610 o posterior y Microsoft Intune versión 1705 sin tener que ponerse en contacto con el soporte técnico de Microsoft y sin tener que anular y volver a crear la inscripción de los dispositivos administrados existentes. Para obtener más información, consulte [Cambio de la entidad de MDM](/sccm/mdm/deploy-use/change-mdm-authority).

6.  Haga clic en los vínculos de privacidad para revisarlos y, a continuación, haga clic en **Siguiente**.

7.  En la página **General** , especifique las opciones siguientes y, a continuación, haga clic en **Siguiente**.

  -   **Recopilación**: especifique una recopilación de usuarios que contenga los usuarios que inscribirán sus dispositivos móviles.

      > [!NOTE]
      >  Si se quita un usuario de la recopilación, el dispositivo del usuario se seguirá administrando durante 24 horas hasta que se quite el registro del usuario de la base de datos de usuarios.

  -   **Nombre de compañía**: especifique el nombre de su compañía.

  -   **Dirección URL a la documentación de privacidad de la compañía**: si publica la información de privacidad de su compañía en un vínculo accesible desde Internet, proporcione un vínculo al que los usuarios puedan acceder desde el portal de empresa, por ejemplo, http://www.contoso.com/CP_privacy.html. La información de privacidad puede aclarar la información que comparten los usuarios con su compañía.

  -   **Combinación de colores del portal de la compañía**: si lo desea, cambie el color predeterminado azul de los portales de la compañía.

  -   **Código de sitio de Configuration Manager**: especifique un código de sitio para un sitio primario para administrar los dispositivos móviles.

    > [!NOTE]
    >  El cambio del código de sitio solo afecta a nuevas inscripciones, y no afecta a dispositivos ya inscritos.

8.  En la página **Información de contacto de la compañía**, especifique la información de contacto de la compañía que se muestra a los usuarios en la aplicación Portal de empresa en **Contactar con TI**. Proporcione la información de contacto de la empresa y luego haga clic en **Siguiente**.

9. En la página **Logotipo de la compañía**, puede elegir si quiere mostrar logotipos en el portal de empresa, después haga clic en **Siguiente**.

10. Complete el asistente.

> [!div class="button"]
[< Paso anterior](confirm-dns.md)  [Paso siguiente >](terms-and-conditions.md)

