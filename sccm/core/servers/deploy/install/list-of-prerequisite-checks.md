---
title: Comprobaciones de requisitos previos | System Center Configuration Manager
description: Revise las comprobaciones de requisitos previos disponibles para System Center Configuration Manager. Incluye comprobaciones para derechos de seguridad.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6a279624-ffc9-41aa-8132-df1809708dd5
caps.latest.revision: 12
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 96787d5c4ad92d86ad9172fcfacb92fe4138c7ba


---
# <a name="list-of-prerequisite-checks-for-system-center-configuration-manager"></a>Lista de comprobaciones previas de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

En las secciones siguientes se detallan las comprobaciones de requisitos previos disponibles.  


 Para obtener más información sobre el Comprobador de requisitos previos, consulte [Comprobador de requisitos previos ](prerequisite-checker.md).  

##  <a name="a-namebkmksecuritya-prerequisite-checks-for-security-rights"></a><a name="BKMK_Security"></a> Comprobaciones de requisitos previos para los derechos de seguridad  
 A continuación se enumeran las comprobaciones de requisitos previos que el Comprobador de requisitos previos realiza para los derechos de seguridad.  

 **Derechos de administrador en el sitio de administración central**: comprueba que la cuenta de usuario que ejecuta el programa de instalación de Configuration Manager tiene derechos de **administrador** local en el equipo del sitio de administración central.  

-   **Gravedad:** error  

-   **Aplicabilidad:**  
      -   Sitio primario  

**Derechos administrativos en sitio primario de expansión**: comprueba que el usuario que ejecuta el programa de instalación tiene derechos de **administrador** local en el sitio primario independiente que se va a expandir.  

-   **Gravedad:** error  

-   **Aplicabilidad:**  

    -   Sitio de administración central  

**Derechos administrativos en el sistema de sitio**: comprueba que la cuenta de usuario que ejecuta el programa de instalación de Configuration Manager tiene derechos de **administrador** local en el equipo de servidor de sitio.  

-   **Gravedad:** error  

-   **Aplicabilidad:**  

    -   Sitio de administración central  
    -   Sitio primario  
    -   Sitio secundario  

**Derechos administrativos del equipo de CAS en el sitio primario de expansión**: comprueba que la cuenta de equipo del sitio de administración central tiene derechos de **administrador** local en el sitio primario independiente que se va a expandir.  

-   **Gravedad:** error  

-   **Aplicabilidad:**  

    -   Sitio de administración central  

**Conexión a SQL Server en el sitio de administración central**: comprueba que la cuenta de usuario que ejecuta el programa de instalación de Configuration Manager en el sitio primario para unirlo a una jerarquía existente tiene el rol **administrador del sistema** en la instancia de SQL Server para el sitio de administración central.  

-   **Gravedad:** error  

-   **Aplicabilidad:**  

    -   Sitio primario  

**Derechos administrativos de la cuenta de equipo del servidor de sitio**: comprueba que la cuenta de equipo del servidor de sitio tiene derechos administrativos en SQL Server y en equipos de punto de administración.  

-   **Gravedad:** error  

-   **Aplicabilidad:**  

    -   Sitio primario  
    -   SQL Server  

**Sistema de sitio para la comunicación de SQL Server**: comprueba que un nombre válido de entidad de seguridad de servicio (SPN) está registrado en los Servicios de dominio de Active Directory para la cuenta configurada para ejecutar el servicio SQL Server para la instancia de SQL Server utilizada para hospedar la base de datos de sitio de Configuration Manager. Un SPN válido debe estar registrado en los Servicios de dominio de Active Directory para admitir la autenticación Kerberos.  

-   **Gravedad** : advertencia  

-   **Aplicabilidad:**  

    -   Sitio secundario  
    -   Punto de administración  

**Modo de seguridad de SQL Server**: comprueba que SQL Server está configurado para la seguridad de autenticación de Windows.  

-   **Gravedad** : advertencia  

-   **Aplicabilidad:**  

    -   SQL Server  

**Derechos de administrador del sistema de SQL Server**: comprueba que la cuenta de usuario que ejecuta el programa de instalación de Configuration Manager tiene el rol **administrador del sistema** en la instancia de SQL Server seleccionada para la instalación de base de datos de sitio. También se producen errores en esta comprobación cuando el programa de instalación no puede tener acceso a la instancia de SQL Server para comprobar los permisos.  

-   **Gravedad:** error  

-   **Aplicabilidad:**  

    -   SQL Server  

**Derechos de administrador del sistema de SQL Server para el sitio de referencia**: comprueba que la cuenta de usuario que ejecuta el programa de instalación de Configuration Manager tiene el rol **administrador del sistema** en la instancia de rol de SQL Server seleccionada como la base de datos de sitio de referencia.  Se requieren los permisos del rol **administrador del sistema** de SQL Server para modificar la base de datos de sitio.  

-   **Gravedad:** error  

-   **Aplicabilidad:**  

    -   SQL Server  

##  <a name="a-namebkmkdependenciesa-prerequisite-checks-for-configuration-manager-dependencies"></a><a name="BKMK_Dependencies"></a> Comprobaciones de requisitos previos para las dependencias de Configuration Manager  
 A continuación se enumeran las comprobaciones de requisitos previos que el Comprobador de requisitos previos realiza para las dependencias de Configuration Manager.  

**Asignaciones de migración activas en el sitio primario de destino**  

 Comprueba que no hay ninguna asignación de migración activa en los sitios primarios.  

-   **Gravedad:** error  

-   **Aplicabilidad:**  

    -   Sitio de administración central  

**Punto de administración de réplica activo**: comprueba la presencia de una réplica de punto de administración activo.  

-   **Gravedad:** error  

-   **Aplicabilidad:**  

    -   Sitio primario  

**Derechos administrativos en el punto de distribución**: comprueba que el usuario que ejecuta el programa de instalación tiene derechos de **administrador** local en el equipo de puntos de distribución.  

-   **Gravedad** : advertencia  

-   **Aplicabilidad:**  

    -   Punto de distribución  

**Derechos administrativos en el punto de administración**: comprueba que la cuenta de equipo del servidor de sitio tiene derechos de **administrador** en el equipo de puntos de administración y distribución.  

-   **Gravedad** : advertencia  

-   **Aplicabilidad:**  

    -   Punto de administración  

**Recurso compartido administrativo (sistema de sitio)**: comprueba que los recursos compartidos administrativos necesarios se encuentran en el equipo de sistema de sitio.  

-   **Gravedad** : advertencia  

-   **Aplicabilidad:**  

    -   Punto de administración  

**Compatibilidad de aplicaciones**: comprueba que las aplicaciones actuales son compatibles con el esquema de la aplicación.  

-   **Gravedad** : advertencia  

-   **Aplicabilidad:**  

    -   Sitio de administración central    
    -   Sitio primario  

**BITS habilitado**: comprueba que el Servicio de transferencia inteligente en segundo plano (BITS) está instalado en el equipo de sistemas de sitio de punto de administración. Cuando se produce algún error en esta comprobación, significa que BITS no está instalado, que el componente de compatibilidad con WMI de IIS 6 para IIS7 no está instalado en el equipo o en el host de IIS remoto, o el programa de instalación no pudo comprobar la configuración de IIS remoto porque los componentes comunes de IIS no estaban instalados en el equipo del servidor de sitio.  

-   **Gravedad:** error  

-   **Aplicabilidad:**  

    -   Punto de administración  

**BITS instalado**: comprueba que el Servicio de transferencia inteligente en segundo plano (BITS) está instalado en Internet Information Services (IIS).  

-   **Gravedad** : advertencia  

-   **Aplicabilidad:**  

    -   Punto de administración  

**Intercalación que diferencia entre mayúsculas y minúsculas en SQL Server**: comprueba que la instalación de SQL Server utiliza una intercalación que diferencia entre mayúsculas y minúsculas, como SQL_Latin1_General_CP1_CI_AS.  

-   **Gravedad:** error  

-   **Aplicabilidad:**  

    -   SQL Server  

**Comprobar la versión y el código de sitio del sitio primario independiente existente**: compruebe que el sitio primario que planea expandir es un sitio primario independiente cuya versión coincide con la de Configuration Manager, pero que tiene un código de sitio distinto al del sitio de administración central que se va a instalar.  

-   **Gravedad:** error  

-   **Aplicabilidad:**  

    -   Sitio de administración central    
    -   Sitio primario  

**Comprobar referencias a colecciones no compatibles**: durante una actualización, esta comprobación verifica que las colecciones solo hagan referencia a otras colecciones del mismo tipo.  

-   **Gravedad:** error  

-   **Aplicabilidad:**  

    -   Sitio de administración central  

**Versión de cliente en el equipo de punto de administración**: comprueba que se va a instalar el punto de administración en un equipo cuya versión no difiere de la del cliente instalado de Configuration Manager.  

-   **Gravedad:** error  

-   **Aplicabilidad:**  

    -   Punto de administración  

**Configuración de uso de memoria de SQL Server**: comprueba si SQL Server está configurado para un uso ilimitado de memoria. Debe configurar la memoria de SQL Server para que tenga un límite máximo.  

-   **Gravedad** : advertencia  

-   **Aplicabilidad:**  

    -   SQL Server  

**Instancia de SQL Server dedicada**: comprueba si una instancia de SQL Server dedicada está configurada para hospedar la base de datos de sitio de Configuration Manager. Si otro sitio utiliza la instancia, debe seleccionar una instancia diferente para el nuevo sitio que se va a utilizar. Como alternativa, puede desinstalar el otro sitio o mover su base de datos a una instancia diferente de SQL Server.  

-   **Gravedad:** error  

-   **Aplicabilidad:**  

    -   Sitio de administración central    
    -   Sitio primario    
    -   Sitio secundario  

**Componentes existentes del servidor de Configuration Manager en el servidor**: comprueba que un servidor de sitio o el rol de sistema de sitio aún no están instalados en el equipo seleccionado para la instalación del sitio.  

-   **Gravedad:** error  

-   **Aplicabilidad:**  

    -   Sitio de administración central    
    -   Sitio primario    
    -   Sitio secundario  

**Excepción de firewall para SQL Server**: comprueba si el Firewall de Windows está deshabilitado o si existe una excepción de Firewall de Windows correspondiente para SQL Server. Se debe permitir el acceso remoto a sqlservr.exe o a los puertos TCP necesarios. De forma predeterminada, SQL Server escucha en el puerto TCP 1433 y SQL Broker Service usa el puerto TCP 4022.  

-   **Gravedad:** error  

-   **Aplicabilidad:**  

    -   Sitio de administración central    
    -   Sitio primario    
    -   Sitio secundario    
    -   Punto de administración  

**Excepción de firewall para SQL Server (sitio primario independiente)**: comprueba si el Firewall de Windows está deshabilitado o si existe una excepción de Firewall de Windows correspondiente para SQL Server. Se debe permitir el acceso remoto a sqlservr.exe o a los puertos TCP necesarios. De forma predeterminada, SQL Server escucha en el puerto TCP 1433 y SQL Broker Service usa el puerto TCP 4022.  

-   **Gravedad** : advertencia  

-   **Aplicabilidad:**  

    -   Sitio primario (sólo independiente)  

**Excepción de firewall para SQL Server para punto de administración**: comprueba si el Firewall de Windows está deshabilitado o si existe una excepción de Firewall de Windows correspondiente para SQL Server.  

-   **Gravedad** : advertencia  

-   **Aplicabilidad:**  

    -   Punto de administración  

**Configuración HTTPS de IIS**: comprueba los enlaces del sitio web de Internet Information Services (IIS) para el protocolo de comunicación HTTPS. Si opta por instalar roles de sitio que requieran el protocolo HTTPS, debe configurar los enlaces del sitio de IIS en el servidor especificado con un certificado PKI válido.  

-   **Gravedad** : advertencia  

-   **Aplicabilidad:**  

    -   Punto de administración    
    -   Punto de distribución  

**Ejecución del servicio IIS**: comprueba si Internet Information Services (IIS) está instalado y en ejecución en el equipo para instalar los puntos de administración o distribución.  

-   **Gravedad:** error  

-   **Aplicabilidad:**  

    -   Punto de administración    
    -   Punto de distribución  

**Hacer coincidir la intercalación del sitio primario de expansión**: comprueba que la base de datos de sitio para el sitio primario independiente que se va a expandir tiene la misma intercalación que la base de datos de sitio en el sitio de administración central.  

-   **Gravedad:** error  

-   **Aplicabilidad:**  

    -   Sitio de administración central  

**Biblioteca registrada de compresión diferencial remota (RDC) de Microsoft**: comprueba que la Biblioteca de compresión diferencial remota (RDC) de Microsoft está registrada en el servidor de sitio de Configuration Manager.  

-   **Gravedad:** error  

-   **Aplicabilidad:**  

    -   Sitio de administración central    
    -   Sitio primario    
    -   Sitio secundario  

**Microsoft Windows Installer**: comprueba la versión de Windows Installer. Cuando se produce un error en esta comprobación, significa que el programa de instalación no pudo comprobar la versión o que la versión instalada no cumple el requisito mínimo de Windows Installer 4.5.  

-   **Gravedad:** error  

-   **Aplicabilidad:**  

    -   Sitio de administración central    
    -   Sitio primario    
    -   Sitio secundario  

**Microsoft XML Core Services 6.0 (MSXML60)**: comprueba que la versión Microsoft Core XML Services (MSXML) 6.0, u otra posterior, está instalada en el equipo.  

-   **Gravedad** : advertencia  

-   **Aplicabilidad:**  

    -   Sitio de administración central    
    -   Sitio primario    
    -   Sitio secundario    
    -   Consola de Configuration Manager    
    -   Punto de administración    
    -   Punto de distribución  

**Versión mínima de .NET Framework para la consola de Configuration Manager**: comprueba si Microsoft .NET Framework 4.0 está instalado en el equipo de la consola de Configuration Manager. Puede descargar Microsoft .NET Framework versión 4.0 del [Centro de descarga de Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=189149).  

-   **Gravedad:** error  

-   **Aplicabilidad:**  

    -   Consola de Configuration Manager  

**Versión mínima de .NET Framework para el servidor de sitio de Configuration Manager**: comprueba si Microsoft .NET Framework 3.5 está instalado en el servidor de sitio de Configuration Manager. Para Windows Server 2008, puede descargar Microsoft .NET Framework versión 3.5 del [Centro de descarga de Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=185604). Para Windows Server 2008 R2, puede habilitar Microsoft .NET Framework 3.5 como una característica del Administrador de servidores.  

-   **Gravedad:** error  

-   **Aplicabilidad:**  

    -   Sitio de administración central    
    -   Sitio primario    
    -   Sitio secundario  

**Versión mínima de .NET Framework para la instalación de SQL Server Express Edition para el sitio secundario de Configuration Manager**: comprueba que Microsoft .NET Framework versión 4.0 se haya instalado en equipos del sitio secundario de Configuration Manager para instalar SQL Server Express Edition.  

-   **Gravedad:** error  

-   **Aplicabilidad:**  

    -   Sitio secundario  

**Intercalación de base de datos primaria/secundaria**: comprueba que la intercalación de base de datos de sitio coincide con la intercalación de base de datos de sitio primario. Todos los sitios de una jerarquía deben utilizar la misma intercalación de base de datos.  

-   **Gravedad:** error  

-   **Aplicabilidad:**  

    -   Sitio primario    
    -   Sitio secundario  

**PowerShell 2.0 en el servidor de sitio**: comprueba que la versión Windows PowerShell 2.0, u otra posterior, está instalada en el servidor de sitio para Configuration Manager Exchange Connector. Para obtener más información acerca de PowerShell 2.0, consulte el [Artículo 968930](http://go.microsoft.com/fwlink/p/?LinkId=226450) en Microsoft Knowledge Base.  

-   **Gravedad** : advertencia  

-   **Aplicabilidad:**  

    -   Sitio primario  

**FQDN primario**: comprueba que el nombre NETBIOS del equipo coincide con el nombre de host local (primera etiqueta del FQDN) del equipo.  

-   **Gravedad:** error  

-   **Aplicabilidad:**  

    -   Sitio de administración central    
    -   Sitio primario    
    -   Sitio secundario    
    -   SQL Server  

**Conexión remota con WMI en el sitio secundario**: comprueba si el programa de instalación puede establecer una conexión remota con WMI en el servidor de sitio secundario.  

-   **Gravedad** : advertencia  

-   **Aplicabilidad:**  

    -   Sitio secundario  

**Intercalación de SQL Server requerida**: comprueba que la instancia de SQL Server y la base de datos de sitio de Configuration Manager, si están instaladas, están configuradas para utilizar la intercalación SQL_Latin1_General_CP1_CI_AS, a menos que utilice un sistema operativo chino y requiera compatibilidad para GB18030.  

 Para obtener información acerca de cómo cambiar las intercalaciones de base de datos y la instancia de SQL Server, consulte [Establecer y cambiar intercalaciones](http://go.microsoft.com/fwlink/p/?LinkID=234541) en los Libros en pantalla de SQL Server 2008 R2.  Para obtener información acerca de cómo habilitar la compatibilidad para GB18030, consulte [Compatibilidad internacional en System Center Configuration Manager](../../../../core/plan-design/hierarchy/international-support.md).  

-   **Gravedad:** error  

-   **Aplicabilidad:**  

    -   Sitio de administración central    
    -   Sitio primario    
    -   Sitio secundario  

**Carpeta del origen de la instalación**: comprueba que la cuenta de equipo del sitio secundario tiene el permiso **Lectura** para el sistema de archivos NTFS y el permiso **Lectura** del recurso compartido para el recurso compartido y la carpeta de origen del programa de instalación.  

> [!NOTE]  
>  La cuenta de equipo del sitio secundario debe ser un administrador del equipo si se utilizan recursos compartidos administrativos (por ejemplo, C$ y D$).  

-   **Gravedad:** error  

-   **Aplicabilidad:**  

    -   Sitio secundario  

**Versión de origen de programa de instalación**: comprueba que la versión de Configuration Manager de la carpeta de origen especificada para la instalación del sitio secundario debe coincidir con la versión de Configuration Manager del sitio primario.  

-   **Gravedad:** error  

-   **Aplicabilidad:**  

    -   Sitio secundario  

**Código de sitio en uso**: comprueba que el código de sitio que ha especificado aún no se utiliza en la jerarquía de Configuration Manager. Debe especificar un código de sitio único para este sitio.  

-   **Gravedad:** error  

-   **Aplicabilidad:**  

    -   Sitio primario  

**El equipo del proveedor de SMS tiene el mismo dominio que el servidor de sitio**: comprueba si un equipo que ejecuta una instancia del proveedor de SMS tiene el mismo dominio que el servidor de sitio.  

-   **Gravedad:** error  

-   **Aplicabilidad:**  

    -   proveedor de SMS  

**Edición de SQL Server**: comprueba que la edición de SQL Server del sitio no es SQL Server Express.  

-   **Gravedad:** error  

-   **Aplicabilidad:**  

    -   SQL Server  

**SQL Server Express en el sitio secundario** comprueba que SQL Server Express puede instalarse correctamente en el equipo de servidor de sitio para un sitio secundario.  

-   **Gravedad:** error  

-   **Aplicabilidad:**  

    -   Sitio secundario  

**SQL Server en el equipo de sitio secundario**: comprueba que SQL Server está instalado en el equipo de sitio secundario. No se permite instalar SQL Server en el sistema de sitio remoto.  

> [!WARNING]  
>  Esta comprobación sólo se aplica cuando se selecciona que el programa de instalación utilice una instancia existente de SQL Server.  

-   **Gravedad:** error  

-   **Aplicabilidad:**  

    -   Sitio secundario  

**Asignación de memoria de proceso de SQL Server**: comprueba que SQL Server reserva un mínimo de 8 GB de memoria para el sitio de administración central y el sitio primario, y un mínimo de 4 GB de memoria para el sitio secundario. Para obtener más información acerca de cómo establecer una cantidad fija de memoria usando SQL Server Management Studio, consulte [Cómo: establecer una cantidad fija de memoria (SQL Server Management Studio)](http://go.microsoft.com/fwlink/p/?LinkId=233759).  

> [!NOTE]  
>  Esta comprobación no es aplicable a SQL Server Express en un sitio secundario, ya que está limitado a 1 GB de memoria reservada.  

-   **Gravedad** : advertencia  

-   **Aplicabilidad:**  

    -   SQL Server  

**Cuenta de ejecución de servicio SQL Server**: comprueba que la cuenta de inicio de sesión del servicio SQL Server no es una cuenta de usuario local ni SERVICIO LOCAL. Debe configurar el servicio SQL Server para utilizar una cuenta de dominio válida, SERVICIO DE RED o SISTEMA LOCAL.  

-   **Gravedad:** error  

-   **Aplicabilidad:**  

    -   Sitio de administración central    
    -   Sitio primario    
    -   Sitio secundario  

**Puerto TCP de SQL Server**: comprueba que TCP está habilitado para SQL Server y está configurado para utilizar un puerto estático.  

-   **Gravedad:** error  

-   **Aplicabilidad:**  

    -   SQL Server  

**Versión de SQL Server**: comprueba que una versión compatible de SQL Server está instalada en el servidor de base de datos de sitio especificado. Para más información, consulte [Compatibilidad con versiones de SQL Server para System Center Configuration Manager](../../../../core/plan-design/configs/support-for-sql-server-versions.md).  

-   **Gravedad:** error  

-   **Aplicabilidad:**  

    -   SQL Server  

**Versión de sistema operativo de sistema de sitio no admitida para la actualización**: durante una actualización, esta regla comprueba si los roles de sistema de sitio, excepto los puntos de distribución, se instalan en equipos que ejecutan Windows Server 2008 o anterior.  

> [!NOTE]  
>  Dado que esta comprobación no puede resolver el estado de los roles de sistema de sitio que se instalan en Azure o el almacenamiento en la nube utilizado por Microsoft Intune al integrar Intune con Configuration Manager, puede omitir las advertencias para estos roles de falsos positivos.  

-   **Gravedad** : advertencia  

-   **Aplicabilidad:**  

    -   Sitio primario    
    -   Sitio secundario  

**Rol de sistema de sitio "Punto de sincronización de Asset Intelligence" no admitido en el sitio primario expandido**: comprueba que el rol de sistema de sitio de punto de sincronización de Asset Intelligence no está instalado en el sitio primario independiente que se va a expandir.  

-   **Gravedad:** error  

-   **Aplicabilidad:**  

    -   Sitio de administración central  

**Rol de sistema de sitio "Punto de Endpoint Protection" no admitido en el sitio primario expandido**: comprueba que el rol de sistema de sitio Punto de Endpoint Protection no está instalado en el sitio primario independiente que se va a expandir.  

-   **Gravedad:** error  

-   **Aplicabilidad:**  

    -   Sitio de administración central  

<a name="-head"></a><<<<<<< HEAD
=======

>>>>>>> 5e8e486ea74f66a92696c65e3367aec2e592b001 **Rol del sistema de sitio "Conector de Microsoft Intune" no admitido en el sitio primario expandido**: comprueba que el rol del sistema de sitio "Conector de Microsoft Intune" no está instalado en el sitio primario independiente que se va a expandir.  

-   **Gravedad:** error  

-   **Aplicabilidad:**  

    -   Sitio de administración central  

**La Herramienta de migración de estado de usuario (USMT) está instalada**: comprueba que el componente Herramienta de migración de estado de usuario (USMT) de Windows Assessment and Deployment Kit (ADK) para Windows 8.1 está instalado.  

-   **Gravedad:** error  

-   **Aplicabilidad:**  

    -   Sitio de administración central    
    -   Sitio primario (sólo independiente)  

**Validar el FQDN del equipo con SQL Server**: comprueba que el FQDN que ha especificado para el equipo con SQL Server es válido.  

-   **Gravedad:** error  

-   **Aplicabilidad:**  

    -   SQL Server  

**Comprobar la versión del sitio de administración central**: comprueba que el sitio de administración central tiene la misma versión que Configuration Manager.  

-   **Gravedad:** error  

-   **Aplicabilidad:**  

    -   Sitio primario  

**Comprobar los permisos de servidor de sitio para publicar en Active Directory**: comprueba que la cuenta de equipo del servidor de sitio tiene permisos de **Control total** en el contenedor **System Management** en el dominio de Active Directory. Para más información acerca de las opciones para configurar los permisos necesarios, consulte [Extender el esquema de Active Directory para System Center Configuration Manager](../../../../core/plan-design/network/extend-the-active-directory-schema.md).  

> [!NOTE]  
>  Puede omitir esta advertencia si ha comprobado manualmente los permisos.  

-   **Gravedad** : advertencia  

-   **Aplicabilidad:**  

    -   Sitio de administración central    
    -   Sitio primario    
    -   Sitio secundario  

**Las herramientas de implementación de Windows están instaladas**: comprueba si el componente de herramientas de implementación de Windows Assessment and Deployment Kit (ADK) para Windows 10 está instalado.  

-   **Gravedad:** error  

-   **Aplicabilidad:**  

    -   proveedor de SMS  

**Clúster de conmutación por error de Windows**: comprueba que los equipos que tienen un punto de administración o un punto de distribución no forman parte de un clúster de Windows.  

-   **Gravedad:** error  

-   **Aplicabilidad:**  

    -   Punto de administración    
    -   Punto de distribución  

**El Entorno de preinstalación de Windows está instalado**: comprueba si el componente de entorno de preinstalación de Windows de Windows Assessment and Deployment Kit (ADK) para Windows 10 está instalado.  

-   **Gravedad:** error  

-   **Aplicabilidad:**  

    -   proveedor de SMS  

**Administración remota de Windows (WinRM) v1.1**: comprueba que WinRM v1.1 está instalado en el servidor de sitio primario o en el equipo de la consola de Configuration Manager para ejecutar la consola de administración desde un origen externo. Para obtener más información acerca de cómo descargar WinRM 1.1, consulte el [Artículo 936059](http://go.microsoft.com/fwlink/p/?LinkId=247166) en Microsoft Knowledge Base.  

-   **Gravedad** : advertencia  

-   **Aplicabilidad:**  

    -   Sitio primario    
    -   Consola de Configuration Manager  

**WSUS en servidor de sitio**: comprueba que Windows Server Update Services (WSUS) 3.0 Service Pack 2 está instalado en el servidor de sitio. Cuando se utiliza un punto de actualización de software en un equipo distinto al servidor del sitio, debe instalar la consola de administración de WSUS en el servidor de sitio. Para obtener más información acerca de WSUS, consulte la página web de [Windows Server Update Services](http://go.microsoft.com/fwlink/p/?LinkID=79477) .  

-   **Gravedad** : advertencia  

-   **Aplicabilidad:**  

    -   Sitio de administración central    
    -   Sitio primario  

##  <a name="a-namebkmkrequirementsa-prerequisite-checks-for-system-requirements"></a><a name="BKMK_Requirements"></a> Comprobaciones de requisitos previos para requisitos del sistema  
 A continuación se enumeran las comprobaciones de requisitos previos que el Comprobador de requisitos previos realiza para los requisitos del sistema.  

**Comprobación de nivel funcional de dominio de Active Directory**: comprueba que el nivel funcional de dominio de Active Directory es como mínimo Windows Server 2008 R2.  

-   **Gravedad** : advertencia  

-   **Aplicabilidad:**  

    -   Sitio de administración central    
    -   Sitio primario  

**Comprobación de si el servicio de servidor se está ejecutando**: comprueba que se ha iniciado el servicio del servidor.  

-   **Gravedad:** error  

-   **Aplicabilidad:**  

    -   Sitio de administración central    
    -   Sitio primario    
    -   Sitio secundario  

**Pertenencia a dominio**: comprueba que el equipo de Configuration Manager pertenece a un dominio de Windows.  

-   **Gravedad:** error  

-   **Aplicabilidad:**  

    -   Sitio de administración central    
    -   Sitio primario    
    -   Sitio secundario    
    -   Proveedor de SMS    
    -   SQL Server  

**Pertenencia a dominio**: comprueba que el equipo de Configuration Manager pertenece a un dominio de Windows.  

-   **Gravedad** : advertencia  

-   **Aplicabilidad:**  

    -   Punto de administración    
    -   Punto de distribución  

**Unidad FAT en servidor de sitio**: comprueba si la unidad de disco está formateada con el sistema de archivos FAT. Instale los componentes de servidor de sitio en unidades de disco formateadas con el sistema de archivos NTFS para mejorar la seguridad.  

-   **Gravedad** : advertencia  

-   **Aplicabilidad:**  

    -   Sitio primario  

**Espacio libre en disco en el servidor de sitio**: el equipo de servidor de sitio debe tener al menos 5 GB de espacio libre en disco para instalar el servidor de sitio. Debe contar con 1 GB de espacio libre adicional si instala el rol de sistema de sitio del proveedor de SMS en el mismo equipo.  

-   **Gravedad:** error  

-   **Aplicabilidad:**  

    -   Sitio de administración central    
    -   Sitio primario    
    -   Sitio secundario  

**Reinicio del sistema pendiente**: comprueba si otro programa requiere que el servidor se reinicie antes de ejecutar el programa de instalación.  

-   **Gravedad:** error  

-   **Aplicabilidad:**  

    -   Sitio de administración central    
    -   Sitio primario    
    -   Sitio secundario  
    -   Consola de Configuration Manager    
    -   proveedor de SMS    
    -   SQL Server    
    -   Punto de administración    
    -   Punto de distribución  

**Controlador de dominio de solo lectura**: los servidores de base de datos de sitio y servidores de sitio secundario no se admiten en un controlador de dominio de solo lectura (RODC). Para obtener más información, consulte [Puede encontrar problemas al instalar a SQL Server en un controlador de dominio](http://go.microsoft.com/fwlink/p/?LinkId=264856) en Microsoft Knowledge Base.  

-   **Gravedad:** error  

-   **Aplicabilidad:**  

    -   Sitio de administración central    
    -   Sitio primario    
    -   Sitio secundario  

**Extensiones de esquema**: determina si se ha ampliado el esquema de Servicios de dominio de Active Directory y, si es así, la versión de las extensiones de esquema que se han utilizado. Las extensiones de esquema de Configuration Manager Active Directory no son necesarias para la instalación del servidor de sitio, pero se recomiendan para poder admitir todas las características de Configuration Manager. Para más información acerca de las ventajas de la extensión de esquema, consulte [Extender el esquema de Active Directory para System Center Configuration Manager](../../../../core/plan-design/network/extend-the-active-directory-schema.md).  

-   **Gravedad** : advertencia  

-   **Aplicabilidad:**  

    -   Sitio de administración central    
    -   Sitio primario  

**Longitud del FQDN del servidor de sitio**: comprueba la longitud del FQDN del equipo de servidor de sitio.  

-   **Gravedad:** error  

-   **Aplicabilidad:**  

    -   Sitio de administración central    
    -   Sitio primario    
    -   Sitio secundario  

**Sistema operativo de consola de Configuration Manager no admitido**: comprueba que las consolas de Configuration Manager pueden instalarse en equipos que ejecutan una versión de sistema operativo compatible. Para obtener más información, consulte [Supported operating systems for System Center Configuration Manager consoles](/sccm/core/plan-design/configs/supported-operating-systems-consoles) (Sistemas operativos compatibles para consolas de System Center Configuration Manager).  

-   **Gravedad:** error  

-   **Aplicabilidad:**  

    -   Consola de Configuration Manager  

**Versión no compatible del sistema operativo de servidor de sitio para el programa de instalación**: comprueba si se está ejecutando un sistema operativo compatible en el servidor. Para más información, consulte [Sistemas operativos compatibles con sitios y clientes de System Center Configuration Manager](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers).  

-   **Gravedad:** error  

-   **Aplicabilidad:**  

    -   Sitio de administración central    
    -   Sitio primario    
    -   Sitio secundario    
    -   Consola de Configuration Manager    
    -   Punto de administración    
    -   Punto de distribución  

**Comprobar la coherencia de la base de datos**: a partir de la versión 1602, este proceso comprueba la coherencia de la base de datos.  

-   **Gravedad:** error  

-   **Aplicabilidad:**  

    -   Sitio de administración central    
    -   Sitio primario  



<!--HONumber=Nov16_HO1-->


