---
title: "Buscar un nombre de familia de paquete (PFN) para VPN por aplicación | Microsoft Docs"
description: "Obtenga información sobre las dos maneras de buscar un nombre de familia de paquete para poder configurar una VPN por aplicación."
ms.custom: na
ms.date: 10/06/2016
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 47118499-3d26-4c25-bfde-b129de7eaa59
caps.latest.revision: "3"
author: Nbigman
ms.author: nbigman
manager: angrobe
ms.openlocfilehash: ce50645155ecb14a82d8b982aa69c0f87dd15fbf
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/07/2017
---
# <a name="find-a-package-family-name-pfn-for-per-app-vpn"></a>Buscar un nombre de familia de paquete (PFN) para VPN por aplicación

*Se aplica a: System Center Configuration Manager (rama actual)*


Hay dos maneras de buscar un PFN para poder configurar una VPN por aplicación.

## <a name="find-a-pfn-for-an-app-thats-installed-on-a-windows-10-computer"></a>Buscar un PFN para una aplicación que está instalada en un equipo Windows 10

Si la aplicación con la que trabaja ya está instalada en un equipo Windows 10, puede usar el cmdlet [Get-AppxPackage](https://technet.microsoft.com/library/hh856044.aspx) de PowerShell para obtener el PFN.

La sintaxis de Get-AppxPackage es la siguiente:

` Parameter Set: __AllParameterSets`
` Get-AppxPackage [[-Name] <String> ] [[-Publisher] <String> ] [-AllUsers] [-User <String> ] [ <CommonParameters>]`

> [!NOTE]
> Es posible que deba ejecutar PowerShell como administrador para poder recuperar el PFN.

Por ejemplo, para obtener información sobre todas las aplicaciones universales instaladas en el equipo, use `Get-AppxPackage`.

Para obtener información sobre una aplicación cuyo nombre conoce, o parte de él, use `Get-AppxPackage *<app_name>`. Observe el uso del carácter comodín, que resulta especialmente útil si no está seguro del nombre completo de la aplicación. Por ejemplo, para obtener información sobre OneNote, use `Get-AppxPackage *OneNote`.


Esta es la información que se recupera para OneNote:

`Name                   : Microsoft.Office.OneNote`

`Publisher              : CN=Microsoft Corporation, O=Microsoft Corporation, L=Redmond, S=Washington, C=US`

`Architecture           : X64`

`ResourceId             :`

`Version                : 17.6769.57631.0`

`PackageFullName        : Microsoft.Office.OneNote_17.6769.57631.0_x64__8wekyb3d8bbwe`

`InstallLocation        : C:\Program Files\WindowsApps`

`\Microsoft.Office.OneNote_17.6769.57631.0_x64__8wekyb3d8bbwe`

`IsFramework            : False`

**`PackageFamilyName      : Microsoft.Office.OneNote_8wekyb3d8bbwe`**

`PublisherId            : 8wekyb3d8bbwe`



## <a name="find-a-pfn-if-the-app-is-not-installed-on-a-computer"></a>Buscar un PFN si la aplicación no está instalada en un equipo

1.  Vaya a https://www.microsoft.com/es-es/store/apps.
2.  En la barra de búsqueda, escriba el nombre de la aplicación. En nuestro ejemplo, busque OneNote.
3.  Haga clic en el vínculo de la aplicación. Observe que la dirección URL a la que tiene acceso contiene una serie de letras al final. En nuestro ejemplo, la dirección URL tiene el siguiente aspecto: `https://www.microsoft.com/en-us/store/apps/onenote/9wzdncrfhvjl`
4.  En otra pestaña, pegue la dirección URL `https://bspmts.mp.microsoft.com/v1/public/catalog/Retail/Products/<app id>/applockerdata`, pero sustituya `<app id>` por el identificador de la aplicación que obtuvo en https://www.microsoft.com/es-es/store/apps, que es esa serie de letras que se incluye al final de la dirección URL en el paso 3. En nuestro ejemplo de OneNote, pegaría lo siguiente: `https://bspmts.mp.microsoft.com/v1/public/catalog/Retail/Products/9wzdncrfhvjl/applockerdata`.

En Microsoft Edge, se muestra la información que le interesa. En Internet Explorer, debe hacer clic en **Abrir** para verla. El valor PFN se muestra en la primera línea. Este es el aspecto de los resultados de nuestro ejemplo:


`{`
`  "packageFamilyName": "Microsoft.Office.OneNote_8wekyb3d8bbwe",`
`  "packageIdentityName": "Microsoft.Office.OneNote",`
`  "windowsPhoneLegacyId": "ca05b3ab-f157-450c-8c49-a1f127f5e71d",`
`  "publisherCertificateName": "CN=Microsoft Corporation, O=Microsoft Corporation, L=Redmond, S=Washington, C=US"`
`}`
