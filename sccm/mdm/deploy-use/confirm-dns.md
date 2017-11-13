---
title: "Confirmación de los requisitos de nombre de dominio"
titleSuffix: Configuration Manager
description: Confirme los requisitos de nombre de dominio mediante System Center Configuration Manager.
ms.custom: na
ms.date: 03/21/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 522c2e82-20eb-4f38-859b-d55640b24e32
caps.latest.revision: "18"
caps.handback.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 152a93559e8587d096552da800b1b84c7bb8bd28
ms.sourcegitcommit: 1132886e07d0c0a87dcc7eeef4577dd8d8840023
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/01/2017
---
# <a name="confirm-domain-name-requirements-with-system-center-configuration-manager-and-microsoft-intune"></a>Confirmación de los requisitos de nombre de dominio con System Center Configuration Manager y Microsoft Intune

*Se aplica a: System Center Configuration Manager (rama actual)*

Si es necesario, siga estos pasos para satisfacer todas las dependencias externas a Configuration Manager:

1. Cada usuario debe tener una licencia de Intune asignada para inscribir dispositivos. Para asociar licencias de Intune a usuarios, cada usuario debe tener un nombre principal de usuario (UPN) que se pueda resolver públicamente (por ejemplo, johndoe@contoso.com) o un identificador de inicio de sesión alternativo configurado en Azure Active Directory. Configurar un identificador de inicio de sesión alternativo permite a los usuarios iniciar sesión con una dirección de correo, por ejemplo, incluso si su UPN está en un formato de NetBIOS (por ejemplo, CONTOSO\johndoe).

  - Si su compañía usa UPN que se pueden resolver públicamente (por ejemplo, johndoe@contoso.com) no se requiere ninguna configuración adicional.
  - Si su empresa usa un UPN que no se puede resolver (por ejemplo, CONTOSO\johndoe), deberá [configurar un identificador alternativo en Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-aadconnect-get-started-custom/#pages-under-the-section-sync).

2.  Implemente y configure los Servicios de federación de Active Directory (AD FS). (Opcional)

     Al configurar el inicio de sesión único, los usuarios pueden iniciar sesión con sus credenciales corporativas para obtener acceso a los servicios de Intune.

     Para obtener más información, consulte los temas siguientes:
    -   [Preparar el inicio de sesión único](http://go.microsoft.com/fwlink/?LinkID=271124)
    -   [Planear e implementar AD FS 2.0 para su uso con el inicio de sesión único](http://go.microsoft.com/fwlink/?LinkID=271125)

3.  Implementar y configurar la sincronización de directorios.

     La sincronización de directorios permite rellenar Intune con cuentas de usuario sincronizadas. Las cuentas de usuario y los grupos de seguridad sincronizados se agregan a Intune. Los errores al habilitar la sincronización de directorios es una causa común por la que los dispositivos no pueden inscribirse al configurar la MDM de Configuration Manager con Microsoft Intune.

     Para obtener más información, consulte [Integración de directorios](http://go.microsoft.com/fwlink/?LinkID=271120) en la biblioteca de documentación de Active Directory.

4.  Opcional, pero no recomendado: si no se usan los Servicios de federación de Active Directory, restablezca las contraseñas de Microsoft Online de los usuarios.

     Si no utiliza AD FS, debe establecer una contraseña de Microsoft Online para cada usuario.

> [!div class="button"]
[< Paso anterior](create-mdm-collection.md)  [Paso siguiente >](configure-intune-subscription.md)
