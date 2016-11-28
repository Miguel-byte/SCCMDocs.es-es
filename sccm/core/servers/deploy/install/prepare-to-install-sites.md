---
title: "Preparar la instalación de sitios | System Center Configuration Manager"
description: "Lea esta información para ahorrar tiempo durante la instalación de varios sitios y así evitar errores."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9089e1b5-cba4-42bd-a2de-126ef882a3af
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 6f240f1da4561c05bee974b78f43bfcdba591df6

---
# <a name="prepare-to-install-system-center-configuration-manager-sites"></a>Preparar la instalación de sitios de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Para preparar una implementación correcta de uno o varios sitios de System Center Configuration Manager, debe familiarizarse con la información descrita en este artículo. Estos pasos le pueden ahorrar tiempo a la hora de instalar varios sitios y pueden evitar que se lleven a cabo pasos incorrectos, con lo que se tendrían que volver a instalar los sitios.
 > [!TIP]
 >  Aunque se parecen, los siguientes escenarios no son los mismos a la hora de instalar un sitio de rama actual de System Center Configuration Manager:
 > -  **Actualización**: instale System Center Configuration Manager para **actualizar** desde System Center 2012 Configuration Manager; consulte [Upgrade to System Center Configuration Manager](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md) (Actualizar a System Center Configuration Manager).
 > -  **Actualización**: use las actualizaciones integradas en la consola para instalar una nueva **versión de actualización** a un sitio existente de System Center Configuration Manager; consulte [Updates for System Center Configuration Manager](../../../../core/servers/manage/updates.md) (Actualizaciones para System Center Configuration Manager).
 > -  **Migración**: Para **migrar datos** desde otra jerarquía de Configuration Manager a la jerarquía actual de System Center Configuration Manager, consulte [Planning for migration to System Center Configuration Manager](../../../../core/migration/planning-for-migration.md) (Planeación de la migración a System Center Configuration Manager).



## <a name="a-namebkmkoptionsa-options-for-installing-different-types-of-sites"></a><a name="bkmk_options"></a> Opciones para instalar los diferentes tipos de sitios
Al instalar un Configuration Manager nuevo, la versión de los archivos de origen que se pueden usar depende de la versión de los sitios que ya están en la jerarquía (en caso de que haya); asimismo, los métodos de instalación disponibles dependen del tipo de sitio que desee instalar.  

Antes de instalar los sitios, asegúrese de haber planeado la jerarquía y de conocer el tipo de sitio que desea instalar. Para obtener más información, consulte [Design a hierarchy of sites](../../../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md) (Diseñar una jerarquía de sitios).


### <a name="first-site"></a>Primer sitio
El primer sitio que va a instalar para una jerarquía será un sitio primario independiente o un sitio de administración central.

**Medio de instalación**: para instalar un sitio de administración central o un sitio primario independiente como primer sitio de una nueva jerarquía, debe [usar una versión de línea de base](../../../../core/servers/manage/updates.md#bkmk_Baselines) de Configuration Manager. No instale el primer sitio de una jerarquía nueva con los archivos de origen actualizados desde la [carpeta CD.Latest](../../../../core/servers/manage/the-cd.latest-folder.md) de cualquier sitio.

**Método de instalación**: puede instalar cualquier tipo de sitio mediante el [Asistente para instalación de Configuration Manager](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md); también puede configurar un script para usarlo con una [instalación de línea de comandos generada por scripts](../../../../core/servers/deploy/install/use-a-command-line-to-install-sites.md).


### <a name="additional-sites"></a>Sitios adicionales
Una vez instalado el sitio inicial, puede agregar más sitios en cualquier momento. Existen las siguientes opciones para agregar sitios adicionales (hasta los [límites admitidos](../../../../core/plan-design/configs/size-and-scale-numbers.md)):

Sitio que tiene          |Sitios adicionales que puede instalar  
---------                   |---------
Sitio de administración central |   Instalar un sitio primario secundario            
Sitio primario secundario          |   Instalar un sitio secundario        
Sitio primario independiente    |   Instalar un sitio secundario<br />Expandir el sitio primario, lo cual convierte el sitio primario independiente en un sitio primario secundario

**Medios de instalación**: al instalar un sitio de administración central para expandir un sitio primario independiente, o al instalar un nuevo sitio primario secundario en una jerarquía existente, debe usar medios de instalación (archivos de origen) que coincidan con la versión de los sitios existentes.
> [!IMPORTANT]
> Si ha instalado actualizaciones en la consola que han cambiado la versión de los sitios previamente instalados, no use los medios de instalación originales. Use en su lugar los archivos de origen de la [carpeta CD.Latest](../../../../core/servers/manage/the-cd.latest-folder.md) de un sitio actualizado.  Configuration Manager requiere el uso de archivos de origen que coincidan con la versión del sitio existente al que se conectará el nuevo sitio.


Se debe instalar un sitio secundario desde la consola de Configuration Manager y, por lo tanto, siempre se instala con los archivos de origen del sitio primario principal.

**Método de instalación**: el método empleado para instalar sitios adicionales depende del tipo de sitio que desee instalar.
-   **Agregar un sitio de administración central**:  
Puede usar el Asistente para instalación de Configuration Manager o una línea de comandos generada por scripts para instalar el nuevo sitio de administración central como sitio primario en el sitio primario independiente existente.  Para obtener más información, consulte [Expandir un sitio primario independiente](../../../../core/servers/deploy/install/prerequisites-for-installing-sites.md#bkmk_expand).
-   **Agregar un sitio primario secundario**:  
Puede usar el Asistente para instalación de Configuration Manager o una instalación de línea de comandos para agregar un sitio primario secundario debajo de un sitio de administración central.
-   **Agregar un sitio secundario**:   
Use la consola de Configuration Manager para instalar un sitio secundario debajo de un sitio primario. No se admiten otros métodos para los sitios secundarios.



## <a name="a-namebkmktasksa-common-tasks-to-complete-before-starting-an-install"></a><a name="bkmk_tasks"></a>  Tareas comunes por efectuar antes de iniciar una instalación
-   Analice la topología de la jerarquía que se usará para la implementación    
     (consulte [Design a hierarchy of sites for System Center Configuration Manager](../../../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md) (Diseñar una jerarquía de sitios para System Center Configuration Manager))  

-   Prepare y configure servidores para cumplir los requisitos previos y las configuraciones admitidas para usarlos con Configuration Manager (consulte [Site and site system prerequisites](../../../../core/plan-design/configs/site-and-site-system-prerequisites.md) [Requisitos previos de sitio y sistema de sitio]).  

-   Instale y configure SQL Server para hospedar la base de datos del sitio (consulte    
    [Support for SQL Server versions for System Center Configuration Manager](../../../../core/plan-design/configs/support-for-sql-server-versions.md) [Compatibilidad con versiones de SQL Server para System Center Configuration Manager]).  

-   Prepare el entorno de red para admitir Configuration Manager (consulte [Configure firewalls, ports, and domains to prepare for Configuration Manager](/sccm/core/plan-design/network/configure-firewalls-ports-domains) [Configurar firewalls, puertos y dominios para preparar Configuration Manager]).  

-   Si va a usar una PKI, prepare la infraestructura y los certificados (consulte [PKI certificate requirements for Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md) [Requisitos de certificados PKI para Configuration Manager]).

-   Instale las actualizaciones de seguridad más recientes en los equipos que va a usar como servidores de sitio o servidores del sistema de sitio y, si es necesario, reinícielos.



## <a name="a-namebkmksitecodesa-about-site-names-and-site-codes"></a><a name="bkmk_sitecodes"></a> Acerca de los nombres de sitio y los códigos de sitio
Para identificar y administrar los sitios en una jerarquía de Configuration Manager se usan códigos y nombres de sitio. En la consola de Configuration Manager, el código y el nombre de sitio se muestran con el formato &lt;código de sitio\> - &lt;nombre de sitio\>. Los códigos de sitio que use en su jerarquía deben ser únicos. Si el esquema de Active Directory se extiende para Configuration Manager y los sitios publican datos, los códigos de sitio que se usan en un bosque de Active Directory deben ser únicos incluso si se usan en otra jerarquía de Configuration Manager o si se han usado en instalaciones previas de Configuration Manager. Asegúrese de planear cuidadosamente sus códigos y nombres de sitio antes de implementar su jerarquía.

### <a name="specify-a-site-code-and-site-name"></a>Especificar un nombre y un código de sitio
Durante el programa de instalación de Configuration Manager, se solicita que proporcione un código de sitio y un nombre de sitio para el sitio de administración central y para la instalación de los sitios secundarios y primarios. El código de sitio debe identificar de manera única cada sitio en la jerarquía. Dado que el código de sitio se usa en nombres de carpetas, nunca use los siguientes nombres para el código de sitio, que incluyen nombres reservados para Configuration Manager y nombres reservados para Windows:
  -  AUX
  -  CON
  -  NUL
  -  PRN
  -  SMS

> [!NOTE]
> El programa de instalación de Configuration Manager no comprueba si el código de sitio especificado ya se usa.



Para especificar el código de sitio de un sitio durante el programa de instalación de Configuration Manager, debe escribir tres caracteres alfanuméricos. Para especificar códigos de sitio solo se admiten letras de la A a la Z, números del 0 al 9 o combinaciones de estos elementos. La secuencia de letras o números no tiene ningún efecto en la comunicación entre sitios. Por ejemplo, no es necesario asignar el nombre ABC a un sitio primario y el nombre DEF a un sitio secundario.

El nombre del sitio es un identificador de nombre descriptivo del sitio. Utilice solo caracteres estándar (A - Z, a - z, 0 - 9 y el guión "-") para los nombres de sitio.
> [!IMPORTANT]
> No se admite el cambio del código de sitio o del nombre de sitio después la instalación.

### <a name="reuse-a-site-code"></a>Volver a usar un código de sitio
Los códigos de sitio no se pueden usar más de una vez en una jerarquía de Configuration Manager para un sitio de administración central o para sitios primarios, aunque se hayan desinstalado el código de sitio y el sitio original. Si vuelve a usar un código de sitio, corre el riesgo de que se produzcan conflictos de identificador de objeto en su jerarquía. Puede volver a usar el código de sitio de un sitio secundario si ninguno de estos se usan más en la jerarquía de Configuration Manager o en el bosque de Active Directory.


## <a name="limits-and-restrictions-for-installed-sites"></a>Límites y restricciones de los sitios instalados
Antes de instalar sitios, debe comprender las siguientes limitaciones que se aplican a los sitios y a las jerarquías:
-   Una vez finalizada la instalación, no podrá cambiar las siguientes propiedades del sitio sin desinstalarlo y luego volver a instalarlo con los nuevos valores:  
    -   El directorio de instalación de archivos de programa  
    -   Código de sitio  
    -   Descripción del sitio  
-   Si la jerarquía incluye un sitio de administración central:  
    -   Configuration Manager no admite mover un sitio primario secundario fuera de una jerarquía para crear un sitio primario independiente o para adjuntarlo a otra jerarquía. En su lugar, desinstale el sitio principal secundario y, luego, vuelva a instalarlo como un nuevo sitio primario independiente o como sitio secundario del sitio de administración central de otra jerarquía.  


## <a name="a-namebkmkoptionalstepsa-optional-steps-to-run-before-starting-setup"></a><a name="bkmk_optionalsteps"></a>  Pasos opcionales para ejecutar antes de iniciar el programa de instalación
**Puede ejecutar manualmente el [descargador del programa de instalación](../../../../core/servers/deploy/install/setup-downloader.md)** para descargar los archivos de instalación actualizados de Configuration Manager.

Si el equipo en el que se ejecutará el programa de instalación no está conectado a Internet, o bien si tiene previsto instalar varios servidores de sitio, le recomendamos que use el descargador del programa de instalación para descargar las actualizaciones necesarias para los archivos de instalación:

-  De forma predeterminada, el programa de instalación se conectará a Internet para descargar archivos de instalación actualizados.
-  De forma predeterminada, los archivos se almacenan en una carpeta denominada Redist.
-  Puede dirigir el programa de instalación a una ubicación de red en la que haya almacenado previamente una copia de estos archivos.


**Puede ejecutar manualmente el [comprobador de requisitos previos](../../../../core/servers/deploy/install/prerequisite-checker.md)** para identificar y corregir problemas antes de ejecutar el programa de instalación. Antes de iniciar el programa de instalación para instalar un sitio, y antes de instalar un rol de sistema de sitio en un servidor, puede ejecutar el Comprobador de requisitos previos para asegurarse de que el equipo cumple los requisitos necesarios para hospedar el sitio o el rol de sistema de sitio.
 -  De forma predeterminada, el programa de instalación ejecutará el Comprobador de requisitos previos.
 -  Si se detectan errores, el programa de instalación se detendrá hasta que se solucione el problema.


**Identifique los puertos opcionales** que los sistemas de sitio y clientes pueden usar.
 -  De forma predeterminada, los clientes y los sistemas de sitio usan puertos predefinidos para comunicarse.
 -  Durante la instalación, puede configurar puertos alternativos.
 -  Para obtener más información, consulte [Ports used in System Center Configuration Manager](../../../../core/plan-design/hierarchy/ports.md) (puertos utilizados en System Center Configuration Manager).



<!--HONumber=Nov16_HO1-->


