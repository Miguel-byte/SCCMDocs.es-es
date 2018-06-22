---
title: Configure iOS apps with app configuration policies
titleSuffix: Configuration Manager
description: Evite los problemas de configuración en los dispositivos con iOS 8 o posterior mediante la implementación de directivas de configuración de aplicaciones en los usuarios antes de que ejecuten las aplicaciones.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: f0a78038-ea22-4826-9c07-1771b7dd2e8d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e5d00b1efd02d3b096a0b64033b450f0da949eeb
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32349466"
---
# <a name="apply-settings-to-ios-apps-with-app-configuration-policies-in-system-center-configuration-manager"></a>Aplicar configuración a aplicaciones iOS con directivas de configuración de aplicaciones en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*


Puede usar directivas de configuración de aplicaciones en System Center Configuration Manager (Configuration Manager) para distribuir valores de configuración que podrían ser necesarios cuando un usuario ejecuta una aplicación. Por ejemplo, una aplicación puede requerir al usuario que especifique estos detalles:
- Un número de puerto personalizado
- Configuración de idioma
- Configuración de seguridad
- Configuración de marca, como un logotipo de empresa

Si el usuario especifica la configuración de manera incorrecta, la responsabilidad de corregirla recaerá en el departamento de soporte técnico y la implementación de aplicación será lenta.
Para evitar estos problemas, puede usar directivas de configuración de aplicaciones para implementar la configuración necesaria en los usuarios antes de que ejecuten la aplicación. La configuración se asociada con un usuario automáticamente. No es necesario que el usuario realice ninguna acción.
Para usar una directiva de configuración de aplicaciones en Configuration Manager, en lugar de implementar las directivas de configuración directamente en los usuarios y los dispositivos, asocie la directiva con un tipo de implementación al implementar la aplicación. La configuración de directiva se aplica cada vez que la aplicación la compruebe (normalmente, la primera vez que se ejecuta la aplicación).

Actualmente, las directivas de configuración de aplicaciones solo están disponibles en dispositivos con iOS 8 y versiones posteriores, y para estos tipos de aplicaciones:

- **Paquete de aplicación para iOS (archivo *.ipa)**
- **Paquete de aplicación de iOS en App Store**

Para obtener más información sobre los tipos de instalación de aplicaciones, vea [Introducción a la administración de aplicaciones](/sccm/apps/understand/introduction-to-application-management).

## <a name="create-an-app-configuration-policy"></a>Crear una directiva de configuración de aplicaciones

1. En la consola de Configuration Manager, seleccione **Biblioteca de software** > **Administración de aplicaciones** > **Directivas de configuración de aplicaciones**.
2. En el grupo **Directivas de configuración de aplicaciones** de la pestaña**Inicio**, seleccione **Create new Application Configuration Policy** (Crear directiva de configuración de la aplicación).
3. En la página **General** del Asistente para crear directiva de configuración de la aplicación, especifique esta información de la directiva:
  - **Nombre**. Especifique un nombre único para la directiva.
  - **Descripción**. (Opcional) Para facilitar la identificación de la directiva, puede agregar una descripción.
  - **Categorías asignadas para mejorar la búsqueda y el filtrado**. (Opcional) Para crear y asignar categorías a la directiva, seleccione **Categorías**. Las categorías facilitan la ordenación y la búsqueda de elementos en la consola de Configuration Manager.
4. En la página **Directiva de iOS**, seleccione cómo especificar la información de la directiva de configuración:
  - **Specify name and value pairs** (Especificar pares de nombre y valor). Puede usar esta opción para los archivos de lista de propiedades que no usan el anidamiento.

      *Para especificar un par de nombre y valor*
        1. Para agregar un nuevo par, seleccione **Nuevo**.
        2. En el cuadro de diálogo **Agregar nombre o par de valor**, especifique lo siguiente:
            - **Tipo**. En la lista, seleccione el tipo de valor que quiere especificar.
            - **Nombre**. Escriba el nombre de la clave de la lista de propiedades para la que quiere especificar un valor.
            - **Valor**. Escriba el valor que se aplicará a la clave especificada.

  - **Browse to a property list file** (Examinar un archivo de lista de propiedades). Use esta opción si ya tiene un archivo XML de configuración de aplicaciones, o para archivos más complejos que usen anidamiento.

    *Para examinar un archivo de lista de propiedades*

      1.  En el campo **Directiva de configuración de aplicaciones**, especifique la información de la lista de propiedades en el formato XML correcto.

      Para más información sobre las listas de propiedades XML, vea [Understanding XML Property Lists](https://developer.apple.com/library/ios/documentation/Cocoa/Conceptual/PropertyLists/UnderstandXMLPlist/UnderstandXMLPlist.html) (Descripción de las listas de propiedades XML) en la biblioteca de desarrolladores de iOS.

El formato de la lista de propiedades XML varía según la aplicación que configure. Póngase en contacto con el proveedor de la aplicación para obtener información sobre el formato que debe usar.
Intune admite los siguientes tipos de datos en una lista de propiedades:
            
            ```
            <integer>
            <real>
            <string>
            <array>
            <dict>
            <true /> or <false />
            ```
Para más información sobre los tipos de datos, vea [About Property Lists](https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/PropertyLists/AboutPropertyLists/AboutPropertyLists.html) (Acerca de las listas de propiedades) en la biblioteca de desarrolladores de iOS.
Intune también admite los siguientes tipos de token en la lista de propiedades:
            
            ```
            {{userprincipalname}} - (Example: John@contoso.com)
            {{mail}} - (Example: John@contoso.com)
            {{partialupn}} - (Example: John)
            {{accountid}} - (Example: fc0dc142-71d8-4b12-bbea-bae2a8514c81)
            {{deviceid}} - (Example: b9841cd9-9843-405f-be28-b2265c59ef97)
            {{userid}} - (Example: 3ec2c00f-b125-4519-acf0-302ac3761822)
            {{username}} - (Example: John Doe)
            {{serialnumber}} - (Example: F4KN99ZUG5V2) for iOS devices
            {{serialnumberlast4digits}} - (Example: G5V2) for iOS devices
            ```

Los caracteres {{ y }} solo los usan los tipos de token, por lo que no deben utilizarse para otros fines.
            
5. Para importar un archivo XML ya creado, haga clic en **Seleccionar archivo**.
6. Elija **Siguiente**. Si el código XML contiene errores, tendrá que corregirlos antes de continuar.
7. Finalice los pasos que se muestran en el asistente.

La nueva directiva de configuración de aplicaciones se muestra en el área de trabajo **Biblioteca de software**, en el nodo **Directivas de configuración de aplicaciones**.

## <a name="associate-an-app-configuration-policy-with-a-configuration-manager-application"></a>Asociar una directiva de configuración de aplicaciones a una aplicación de Configuration Manager

Para asociar una directiva de configuración de aplicaciones a la implementación de una aplicación iOS, implemente la aplicación del modo habitual con el procedimiento indicado en el tema [Implementar aplicaciones](/sccm/apps/deploy-use/deploy-applications).

En el Asistente para implementar software, en la página **Directivas de configuración de aplicaciones**, seleccione **Nuevo**. En el cuadro de diálogo **Select App Configuration Policy** (Seleccionar directiva de configuración de la aplicación), elija un tipo de implementación de aplicaciones y la directiva de configuración de aplicaciones con la que quiere asociarlo.
Cuando se instala el tipo de implementación, se aplican automáticamente los valores de la directiva de configuración de aplicaciones.

## <a name="example-format-for-the-mobile-app-configuration-xml-file"></a>Ejemplo de formato del archivo XML de configuración de aplicaciones móviles

Cuando crea un archivo de configuración de aplicaciones móviles, puede usar este formato para especificar uno o varios de los siguientes valores:

```
<dict>
  <key>userprincipalname</key>
  <string>{{userprincipalname}}</string>
  <key>mail</key>
  <string>{{mail}}</string>
  <key>partialupn</key>
  <string>{{partialupn}}</string>
  <key>accountid</key>
  <string>{{accountid}}</string>
  <key>deviceid</key>
  <string>{{deviceid}}</string>
  <key>userid</key>
  <string>{{userid}}</string>
  <key>username</key>
  <string>{{username}}</string>
  <key>serialnumber</key>
  <string>{{serialnumber}}</string>
  <key>serialnumberlast4digits</key>
  <string>{{serialnumberlast4digits}}</string>
  <key>udidlast4digits</key>
  <string>{{udidlast4digits}}</string>
</dict>
```
