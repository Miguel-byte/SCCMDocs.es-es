---
title: "Configurar aplicaciones iOS con directivas de configuración de aplicaciones | System Center Configuration Manager"
description: "Evite los problemas de configuración en los dispositivos con iOS 8 o posterior mediante la implementación de directivas de configuración de aplicaciones en los usuarios antes de que ejecuten las aplicaciones."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology:
- configmgr-app
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 74d5d776-e37d-45de-bdba-43541b03d12c
caps.latest.revision: 10
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 9cbf28afbbe69f9a027ffad2a699b9d6b625e690


---
# <a name="configure-ios-apps-with-app-configuration-policies-in-system-center-configuration-manager"></a>Configure iOS apps with app configuration policies in System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*


Use directivas de configuración de aplicaciones en System Center Configuration Manager para proporcionar valores de configuración que podrían ser necesarios cuando el usuario ejecuta una aplicación. Por ejemplo, una aplicación puede requerir al usuario que especifique:
- Un número de puerto personalizado
- Configuración de idioma
- Configuración de seguridad
- Configuración de marca, como un logotipo de empresa

Si el usuario ha introducido esta configuración incorrectamente, puede aumentar la carga del servicio de asistencia técnica y ralentizar la adopción de nuevas aplicaciones.
Las directivas de configuración de aplicaciones pueden ayudarle a eliminar estos problemas al permitirle implementar esta configuración para los usuarios en una directiva antes de ejecutar la aplicación. A continuación, la configuración se proporciona de forma automática y el usuario tiene que realizar ninguna acción.
No implemente estas directivas directamente en usuarios y dispositivos. En su lugar, asocie la directiva a un tipo de implementación cuando implemente la aplicación. La configuración de directiva se usará cada vez que la aplicación la compruebe (normalmente, la primera vez que se ejecuta).

De momento las directivas de configuración de aplicaciones solo están disponibles en dispositivos con iOS 8 y versiones posteriores, y admiten los siguientes tipos de aplicaciones:

- **Paquete de aplicación de iOS (archivo *.ipa)**
- **Paquete de aplicación de iOS en App Store**

Para más información sobre los tipos de instalación de aplicaciones, vea [Introducción a la administración de aplicaciones](/sccm/apps/understand/introduction-to-application-management).

## <a name="create-an-app-configuration-policy"></a>Crear una directiva de configuración de aplicaciones

1. En la consola de Configuration Manager, haga clic en **Biblioteca de software** > **Administración de aplicaciones** > **Directivas de configuración de aplicaciones**.
3. En el grupo **Directivas de configuración de aplicaciones** de la pestaña**Inicio**, haga clic en **Crear una nueva directiva de configuración de la aplicación**.
4. En la página **General** de **Crear el asistente de directiva de configuración de la aplicación**, especifique la siguiente información:
    - **Nombre**: especifique un nombre exclusivo para la directiva.
    - **Descripción**: si quiere, especifique una descripción para la directiva que le ayude a identificarla.
    - **Categorías asignadas para mejorar la búsqueda y el filtrado**: opcionalmente, haga clic en **Categorías** para crear y asignar categorías a la directiva. Esto facilita la ordenación y la búsqueda de elementos en la consola de Configuration Manager.
5. En la página **Directiva de iOS**, elija cómo especificar la información de la directiva de configuración:
    - **Especificar pares de nombre y valor**: puede usar esta opción para los archivos de lista de propiedades que no usan el anidamiento.
    Para especificar pares de nombre y valor
        - Para agregar un nuevo par, haga clic en **Nuevo**.
        - En el cuadro de diálogo **Agregar nombre o par de valor**, especifique lo siguiente:
            - **Tipo**: en la lista, elija el tipo de valor que quiere especificar.
            - **Nombre**: escriba el nombre de la clave de la lista de propiedades para la que quiere especificar un valor.
            - **Valor**: escriba el valor que se aplicará a la clave especificada.
        - Examinar un archivo de lista de propiedades: use esta opción si ya tiene un archivo XML de configuración de aplicaciones, o para archivos más complejos que usen anidamiento.
        Para ir a un archivo de lista de propiedades
            - En el campo **Directiva de configuración de aplicaciones**, especifique la información de la lista de propiedades en el formato XML correcto.
            Para más información sobre las listas de propiedades XML, vea [Understanding XML Property Lists](https://developer.apple.com/library/ios/documentation/Cocoa/Conceptual/PropertyLists/UnderstandXMLPlist/UnderstandXMLPlist.html) (Descripción de las listas de propiedades XML) en la biblioteca de desarrolladores de iOS.
            El formato de la lista de propiedades XML variará según la aplicación que configure. Para obtener más información sobre el formato exacto que debe usar, póngase en contacto con el proveedor de la aplicación.
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
            Además, Intune admite los siguientes tipos de token en la lista de propiedades:
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

            The {{ and }} characters are used by token types only and must not be used for other purposes.
            ```
            También puede hacer clic en **Seleccionar archivo** para importar un archivo XML que haya creado previamente.
6. Haga clic en **Siguiente**. Si el código XML contiene errores, tendrá que corregirlos antes de continuar.
6. Complete el asistente.

La nueva directiva de configuración de aplicaciones se muestra en el nodo **Directivas de configuración de aplicaciones** del área de trabajo **Biblioteca de software**.

## <a name="associate-an-app-configuration-policy-with-a-configuration-manager-application"></a>Asociar una directiva de configuración de aplicaciones a una aplicación de Configuration Manager

Para asociar una directiva de configuración de aplicaciones a la implementación de una aplicación iOS, implemente la aplicación del modo habitual con el procedimiento del tema [Implementar aplicaciones](/sccm/apps/deploy-use/deploy-applications).
En la página **Directivas de configuración de aplicaciones** del **Asistente para implementar software**, haga clic en **Nuevo**. Luego, en el cuadro de diálogo **Seleccionar directiva de configuración de la aplicación**, elija un tipo de implementación de aplicaciones y una directiva de configuración de aplicaciones para asociarlos.
Cuando se instala el tipo de implementación, se aplica automáticamente la opción de directiva de configuración de aplicaciones.

## <a name="example-format-for-the-mobile-app-configuration-xml-file"></a>Ejemplo de formato del archivo XML de configuración de aplicaciones móviles

Cuando crea un archivo de configuración de aplicaciones móviles, puede especificar uno o varios de los siguientes valores con este formato:

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



<!--HONumber=Nov16_HO1-->


