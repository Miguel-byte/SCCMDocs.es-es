---
title: Extensiones de esquema | Microsoft Docs
description: Extienda el esquema de Active Directory para admitir System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 95c13c00-909f-4fbb-bbaa-1eba9d54d8c5
caps.latest.revision: 8
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: noindex
translationtype: Human Translation
ms.sourcegitcommit: 6ed317d45d90758832d4157985dd95d5e253c6fc
ms.openlocfilehash: f230b6cbe97b72fee4f5d2e45260e6217ef2cec0


---
# <a name="schema-extensions-for-system-center-configuration-manager"></a>Extensiones de esquema para System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Puede extender el esquema de Active Directory para admitir Configuration Manager. De este modo, se edita un esquema de Active Directory de bosques para agregar un nuevo contenedor y varios atributos que los sitios de Configuration Manager usan para publicar información de claves de Active Directory a la que los clientes puedan acceder de forma segura.  Esta información puede simplificar la implementación y configuración de clientes, y ayuda a los clientes a localizar los recursos del sitio, como servidores con contenido implementado o que proporcionen varios servicios a los clientes.  

-   No es necesario extender el esquema de Active Directory, pero se recomienda.  

Antes de [extender el esquema de Active Directory](https://msdnstage.redmond.corp.microsoft.com/en-US/library/mt345589\(TechNet.10\).aspx), debe estar familiarizado con los Servicios de dominio de Active Directory y sentirse cómodo con la [modificación del esquema de Active Directory](https://technet.microsoft.com/library/cc759402\(v=ws.10\).aspx).  

## <a name="considerations-for-extending-the-active-directory-schema-for-configuration-manager"></a>Consideraciones para extender el esquema de Active Directory para Configuration Manager  

-   Las extensiones de esquema de Active Directory para System Center Configuration Manager son iguales que las que se usan en Configuration Manager 2007 y Configuration Manager 2012. Si extendió el esquema anteriormente para cualquiera de las versiones, no tiene que volver a hacerlo.  

-   La extensión del esquema es una acción irreversible que tiene lugar en todo el bosque y una sola vez.  

-   La extensión del esquema solo puede realizarla un usuario que pertenezca al grupo Administradores de esquema o que tenga delegados permisos suficientes para modificar el esquema.  

-   Aunque puede extender el esquema antes o después de ejecutar el programa de instalación de Configuration Manager, se recomienda hacerlo antes de empezar a configurar los sitios y la jerarquía.  Esto puede simplificar muchos de los pasos de configuración posteriores.  

-   Después de extender el esquema, el catálogo global de Active Directory se replica en todo el bosque. Por tanto, planee extender el esquema cuando no esté previsto que el tráfico de replicación vaya a afectar negativamente a otros procesos que dependen de la red:  

    -   En los bosques de Windows 2000, la extensión del esquema produce una sincronización total de todo el catálogo global.  

    -   A partir de los bosques de Windows 2003, solo se replican los nuevos atributos agregados.  

**Dispositivos y clientes que no usan el esquema de Active Directory:**  

-   Dispositivos móviles que administra el conector de Exchange Server  

-   El cliente para equipos Mac  

-   El cliente para servidores Linux y UNIX  

-   Dispositivos móviles inscritos por Configuration Manager  

-   Dispositivos móviles que están inscritos por Microsoft Intune  

-   Clientes heredados de dispositivo móvil  

-   Clientes de Windows que están configurados para la administración de clientes solo de Internet  

-   Los clientes de Windows que Configuration Manager detecta que están en Internet  

## <a name="capabilities-that-benefit-from-extending-the-schema"></a>Capacidades que se benefician de la extensión del esquema  
**Asignación de sitio e instalación de equipo cliente:** cuando se instala un nuevo cliente en un equipo Windows, el cliente busca las propiedades de instalación en Active Directory Domain Services.  

-   **Soluciones alternativas:** si no extiende el esquema, use una de las siguientes opciones para proporcionar detalles de configuración que los equipos requieren para la instalación:  

    -   **Use la instalación de inserción de cliente**. Antes de utilizar el método de instalación de cliente, asegúrese de que se cumplen todos los requisitos previos. Para obtener más información, consulte la sección "Dependencias de los métodos de instalación" del tema Requisitos previos de los equipos cliente.  

    -   **Instale manualmente los clientes** y defina las propiedades de instalación de cliente mediante las propiedades de línea de comandos de instalación de CCMSetup. Esto debe incluir lo siguiente:  

        -   Especifique un punto de administración o ruta de acceso de origen desde donde el equipo puede descargar los archivos de instalación usando la propiedad de CCMSetup **/mp:=&lt;nombre de equipo de nombre de punto de administración\>** o **/source:&lt;ruta de acceso de los archivos de origen del cliente\>** en la línea de comandos de CCMSetup durante la instalación del cliente.  

        -   Especifique una lista de los puntos de administración iniciales que el cliente puede utilizar para asignar al sitio y, a continuación, descargue la configuración del sitio y la directiva de cliente. Utilice la propiedad SMSMP de CCMSetup Client.msi para hacer esto.  

    -   **Publique el punto de administración en DNS o WINS** y configure los clientes para que usen este método de ubicación del servicio.  

**Configuración de puerto para la comunicación cliente a servidor**: cuando se instala un cliente, se configura con la información del puerto almacenada en Active Directory. Si posteriormente se cambia el puerto de comunicación entre cliente y servidor para un sitio, un cliente puede obtener esta nueva configuración de puerto de Active Directory Domain Services.  

-   **Soluciones alternativas:** si no extiende el esquema, use una de las opciones siguientes para proporcionar nuevas configuraciones de puerto para los clientes existentes:  

    -   **Reinstale los clientes** con las opciones que configuren el puerto nuevo  

    -   **Implemente un script personalizado para los clientes que actualice la información de puerto**. Si los clientes no pueden comunicarse con un sitio debido a un cambio de puerto, no puede usar Configuration Manager para implementar este script. Por ejemplo, podría utilizar una directiva de grupo.  

**Escenarios de implementación de contenido**: cuando crea contenido en un sitio y, a continuación, implementa ese contenido en otro sitio de la jerarquía, el sitio receptor debe poder verificar la firma de los datos del contenido firmado. Esto requiere acceso a la clave pública del sitio de origen en el que crea estos datos. Al extender el esquema de Active Directory para Configuration Manager, la clave pública de un sitio estará disponible para todos los sitios de la jerarquía.  

-   **Soluciones alternativas:** si no extiende el esquema, use la herramienta de mantenimiento de la jerarquía, **preinst.exe**, para intercambiar la información de clave segura entre sitios.  

     Por ejemplo, si piensa crear contenido en un sitio primario e implementar ese contenido en un sitio secundario ubicado debajo de un sitio primario diferente, debe extender el esquema de Active Directory para permitir que el sitio secundario obtenga la clave pública de los sitios primarios de origen, o debe usar preinst.exe para compartir las claves entre los dos sitios directamente.  

## <a name="active-directory-attributes-and-classes"></a>Atributos y clases de active Directory  
Si extiende el esquema para System Center Configuration Manager, las clases y los atributos siguientes se agregan al esquema y están disponibles para todos los sitios de Configuration Manager de ese bosque de Active Directory.  

-   Atributos:  

    -   cn=mS-SMS-Assignment-Site-Code  

    -   cn=mS-SMS-Capabilities  

    -   cn=MS-SMS-Default-MP  

    -   cn=mS-SMS-Device-Management-Point  

    -   cn=mS-SMS-Health-State  

    -   cn=MS-SMS-MP-Address  

    -   cn=MS-SMS-MP-Name  

    -   cn=MS-SMS-Ranged-IP-High  

    -   cn=MS-SMS-Ranged-IP-Low  

    -   cn=MS-SMS-Roaming-Boundaries  
        en  

    -   cn=MS-SMS-Site-Boundaries  

    -   cn=MS-SMS-Site-Code  

    -   cn=mS-SMS-Source-Forest  

    -   cn=mS-SMS-Version  

-   Clases:  

    -   cn=MS-SMS-Management-Point  

    -   cn=MS-SMS-Roaming-Boundary-Range  

    -   cn=MS-SMS-Server-Locator-Point  

    -   cn=MS-SMS-Site  

> [!NOTE]  
>  Las extensiones de esquema podrían incluir atributos y clases que provienen de versiones anteriores del producto, pero que Configuration Manager 2015 no usa. Por ejemplo:  
>   
>  -   Atributo: cn=MS-SMS-Site-Boundaries  
> -   Clase: cn=MS-SMS-Server-Locator-Point  

Para asegurarse de que las listas anteriores están actualizadas, consulte el archivo **ConfigMgr_ad_schema.LDF** de la carpeta **\SMSSETUP\BIN\x64** del medio de instalación de System Center Configuration Manager.  



<!--HONumber=Dec16_HO3-->


