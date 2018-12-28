---
title: Configuración de aplicaciones de Android for Work con directivas de configuración de aplicaciones
titleSuffix: Configuration Manager
description: Evite los problemas de configuración en los dispositivos con Android for Work mediante la implementación de directivas de configuración de aplicaciones en los usuarios antes de que ejecuten las aplicaciones.
ms.date: 09/12/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 9126d188-7780-45a4-b21d-7fcf4fad7da2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6f83f26f746c54e3d1defe31df47b3c7c8a7e117
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2018
ms.locfileid: "53417955"
---
# <a name="apply-settings-to-android-for-work-apps-with-app-configuration-policies-in-system-center-configuration-manager"></a>Aplicación de configuración a aplicaciones Android for Work con directivas de configuración de aplicaciones en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Puede usar directivas de configuración de aplicaciones en System Center Configuration Manager para distribuir valores de configuración que podrían ser necesarios cuando un usuario ejecuta una aplicación. Por ejemplo, una aplicación puede requerir al usuario que especifique estos detalles:
- Un número de puerto personalizado
- Configuración de idioma
- Configuración de seguridad
- Configuración de marca, como un logotipo de empresa

Si el usuario especifica la configuración de manera incorrecta, la responsabilidad de corregirla recaerá en el departamento de soporte técnico y la implementación de aplicación será lenta. Para evitar estos problemas, puede usar directivas de configuración de aplicaciones para implementar la configuración necesaria en los usuarios antes de que ejecuten la aplicación. La configuración se asociada con un usuario automáticamente. No es necesario que el usuario realice ninguna acción.
En lugar de implementar las directivas de configuración directamente en los usuarios y los dispositivos, asocie la directiva con un tipo de implementación al implementar la aplicación. La configuración de directiva se aplica cada vez que la aplicación la compruebe (normalmente, la primera vez que se ejecuta la aplicación).

Las directivas de configuración de aplicaciones Android solo están disponibles en los dispositivos que ejecutan Android for Work, y se aplican a las aplicaciones aprobadas en la tienda Play for Work. Para obtener información acerca de las aplicaciones compradas por volumen de Android, vea [Implementación de aplicaciones para dispositivos Android for Work](https://docs.microsoft.com/intune/deploy-use/android-for-work-apps).

Para obtener más información sobre los tipos de instalación de aplicaciones, vea [Introducción a la administración de aplicaciones](/sccm/apps/understand/introduction-to-application-management).

## <a name="create-an-app-configuration-policy"></a>Crear una directiva de configuración de aplicaciones

1. En la consola de Configuration Manager, seleccione **Biblioteca de software** > **Administración de aplicaciones** > **Directivas de configuración de aplicaciones**.
2. En el grupo **Directivas de configuración de aplicaciones** de la pestaña**Inicio**, seleccione **Crear directiva de configuración de aplicaciones**.
3. En la página **General** del Asistente para crear directiva de configuración de la aplicación, especifique esta información de la directiva:
   - **Nombre**. Especifique un nombre único para la directiva.
   - **Descripción**. (Opcional) Para facilitar la identificación de la directiva, puede agregar una descripción.
   -  **Seleccionar un tipo de directiva de configuración**. Especifique la plataforma de destino de la directiva de configuración de aplicación: **Directiva de configuración para Android for Work las aplicaciones**.
   -  **Categorías asignadas para mejorar la búsqueda y el filtrado**. (Opcional) Para crear y asignar categorías a la directiva, seleccione **Categorías**. Las categorías facilitan la ordenación y la búsqueda de elementos en la consola de Configuration Manager.
4. En la página **Directiva de Android for Work**, seleccione cómo especificar la información de la directiva de configuración:
   - **Specify name and value pairs** (Especificar pares de nombre y valor). Puede usar esta opción para los archivos de lista de propiedades que no usan el anidamiento. Para especificar un par de nombre y valor:
        1. Para agregar un nuevo par JSON, seleccione **Nuevo**.
        2. En el cuadro de diálogo **Add Name/Value Pair** (Agregar par de nombre y valor), especifique la siguiente información:
            - **Tipo**. En la lista, seleccione el tipo de valor que quiere especificar.
            - **Nombre**. Escriba el nombre de la clave de la lista de propiedades para la que quiere especificar un valor.
            - **Valor**. Escriba el valor que se aplicará a la clave especificada.

   - **Browse to a property list JSON file** (Examinar un archivo JSON de la lista de propiedades). Use esta opción si ya tiene un archivo JSON de configuración de aplicaciones, o para archivos más complejos que usen anidamiento. En el campo **Directiva de configuración de aplicaciones**, especifique la información de la lista de propiedades en el formato JSON correcto.
5. Para importar un archivo JSON ya creado, haga clic en **Seleccionar archivo**.
6. Elija **Siguiente**. Si el código JSON contiene errores, corríjalos antes de continuar.
7. Finalice los pasos que se muestran en el asistente.

La nueva directiva de configuración de aplicaciones se muestra en el área de trabajo **Biblioteca de software**, en el nodo **Directivas de configuración de aplicaciones**.

## <a name="associate-an-app-configuration-policy-with-a-configuration-manager-application"></a>Asociar una directiva de configuración de aplicaciones a una aplicación de Configuration Manager

Para asociar una directiva de configuración de aplicaciones a la implementación de una aplicación de Android for Work, implemente la aplicación del modo habitual con el procedimiento indicado en el tema [Implementar aplicaciones](/sccm/apps/deploy-use/deploy-applications).

En el Asistente para implementar software, en la página **Directivas de configuración de aplicaciones**, seleccione **Nuevo**. En el cuadro de diálogo **Select App Configuration Policy** (Seleccionar directiva de configuración de la aplicación), elija un tipo de implementación de aplicaciones y la directiva de configuración de aplicaciones con la que quiere asociarlo.
Cuando se instala el tipo de implementación, se aplican automáticamente los valores de la directiva de configuración de aplicaciones.
