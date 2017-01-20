---
title: "Seguridad y privacidad de la administración de aplicaciones | System Center Configuration Manager"
description: "Prácticas recomendadas sobre seguridad y privacidad de la administración de aplicaciones en System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4d26deed-3b16-4116-b640-f618f2c20f5a
caps.latest.revision: 8
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 2c954d2e0244536d74fe85ab98b0d581f7a8167f


---
# <a name="security-and-privacy-for-application-management-in-system-center-configuration-manager"></a>Seguridad y privacidad de la administración de aplicaciones en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*


##  <a name="security-best-practices-for-application-management"></a>Prácticas recomendadas de seguridad para la administración de aplicaciones  

|Práctica recomendada de seguridad|Más información|  
|----------------------------|----------------------|  
|Configurar los puntos del catálogo de aplicaciones para que utilicen conexiones HTTPS y formar a los usuarios acerca de los peligros de los sitios web malintencionados.|Configure el punto de sitios web y el punto de servicio web del catálogo de aplicaciones para que acepte conexiones HTTPS, de tal modo que el servidor se autentique a los usuarios y los datos que se transmiten estén protegidos contra manipulación y visualización. Forme a los usuarios para que solo se conecten a sitios web de confianza y contribuya, de este modo, a evitar ataques de ingeniería social.<br /><br /> No utilice las opciones de la configuración de personalización de marca que muestran el nombre de la organización en el catálogo de aplicaciones como prueba de identificación cuando no se utiliza HTTPS.|  
|Utilizar la separación de roles, y no instalar el punto de sitios web y el punto de servicio del catálogo de aplicaciones en el mismo servidor.|Si el punto de sitios web del catálogo de aplicaciones se ve comprometido, instálelo en otro servidor para separarlo del punto del servicio web del catálogo de aplicaciones. Esto le ayudará a proteger los clientes y la infraestructura de Configuration Manager. Esto es especialmente importante si el punto de sitios web del catálogo de aplicaciones acepta conexiones de cliente desde Internet, porque esta configuración hace que el servidor sea vulnerable a ataques.|  
|Formar a los usuarios para que cierren la ventana del explorador cuando terminen de utilizar el catálogo de aplicaciones.|Si los usuarios utilizan para visitar un sitio web externo la misma ventana del explorador que utilizaron para el catálogo de aplicaciones, el explorador también utilizará la configuración de seguridad aplicable a los sitios de confianza de la intranet.|  
|Especificar manualmente la afinidad entre usuario y dispositivo en lugar de permitir a los usuarios identificar su dispositivo primario; y no habilitar la configuración basada en el uso.|No considere información de autoridad aquélla recopilada de usuarios o del dispositivo. Si implementa software mediante afinidad entre usuario y dispositivo no especificada por un usuario administrativo de confianza, el software podría instalarse en equipos y usuarios sin autorización para recibir dicho software.|  
|Configurar siempre las implementaciones para que descarguen contenido desde los puntos de distribución, en lugar de ejecutarlo desde los puntos de distribución.|Si configura las implementaciones para que descarguen el contenido desde un punto de distribución para ejecutarlo localmente, el cliente de Configuration Manager comprueba el hash de paquete una vez descargado el contenido, y descarta el paquete si el hash no coincide con el hash de la directiva. En comparación, si configura la implementación para que se ejecute directamente desde un punto de distribución, el cliente de Configuration Manager no comprueba el hash de paquete, lo cual significa que el cliente de Configuration Manager puede instalar software que pudo ser objeto de manipulación.<br /><br /> Si tiene que ejecutar implementaciones directamente desde puntos de distribución, utilice los mínimos permisos posibles de NTFS en los paquetes de los puntos de distribución, y utilice IPsec para proteger el canal entre el cliente y los puntos de distribución y entre los puntos de distribución y el servidor de sitio.|  
|No permitir a los usuarios interactuar con programas si se requiere la opción **Ejecutar con derechos administrativos** .|Cuando configura un programa, puede utilizar la opción **Permitir a los usuarios interactuar con este programa** de tal modo que los usuarios puedan responder las solicitudes que reciban en la interfaz de usuario. Si el programa también está configurado para **Ejecutar con derechos administrativos**, un atacante en el equipo que ejecute el programa podría utilizar la interfaz de usuario para escalar privilegios en el equipo cliente.<br /><br /> Utilice programas de instalación basados en Windows Installer con privilegios elevados por usuario para aquellas implementaciones que requieran credenciales administrativas, pero que deban ejecutarse en el contexto de un usuario que no tenga tales credenciales. Los privilegios elevados por usuario de Windows Installer proporcionan el modo más seguro para implementar aplicaciones que tengan este requisito.|  
|Restringir si los usuarios pueden instalar software de forma interactiva mediante la configuración de cliente **Permisos de instalación** .|Utilice la configuración de dispositivo de cliente **Instalar permisos** de **Agente de equipo** para restringir los tipos de usuario que pueden instalar software mediante el catálogo de aplicaciones o el Centro de software. Por ejemplo, cree una configuración de cliente personalizada con **Solo administradores** en **Instalar permisos**. A continuación, aplique esta configuración de cliente a una recopilación de servidores para que los usuarios que no tienen permisos administrativos no puedan instalar software en los equipos.|  
|Para dispositivos móviles, implementar solo aplicaciones que estén firmadas|En dispositivos móviles, implemente solo aplicaciones de código firmado por una entidad de certificación (CA) que sea de confianza para el dispositivo móvil. Por ejemplo:<br /><br /> - Una aplicación de un proveedor, que está firmada por una entidad de certificación conocida, como VeriSign.<br /><br /> - Una aplicación interna que firma mediante una entidad de certificación interna, en la que no interviene Configuration Manager.<br /><br /> - Una aplicación interna que firma mediante Configuration Manager cuando crea el tipo de aplicación y utiliza un certificado de firma.|  
|Si firma aplicaciones de dispositivos móviles mediante el **Asistente para crear aplicaciones** de Configuration Manager, proteja la ubicación del archivo de certificado de firma y el canal de comunicación.|Para proteger frente a la elevación de privilegios y ataques de tipo "Man in the middle", almacene el archivo de certificado de firma en una carpeta protegida, y utilice IPsec o SMB entre los siguientes equipos:<br /><br /> - El equipo que ejecuta la consola de Configuration Manager.<br /><br /> - El equipo que almacena el archivo de firma de certificados.<br /><br /> - El equipo que almacena los archivos de origen de la aplicación.<br /><br /> También puede firmar la aplicación sin que intervenga Configuration Manager y antes de ejecutar el **Asistente para crear aplicaciones**.|  
|Implementar controles de acceso para proteger los equipos de referencia.|Si un usuario administrativo configura el método de detección en un tipo de implementación a través de un equipo de referencia, asegúrese de que no se afectó la seguridad del equipo.|  
|Restringir y supervisar los usuarios administrativos a los que se conceden roles de seguridad basada en roles que estén relacionados con la administración de aplicaciones:<br /><br /> - **Administrador de aplicaciones**<br>- **Autor de aplicaciones**<br>- **Administrador de implementación de aplicaciones**|Aunque configure la administración basada en roles, los usuarios administrativos que creen e implementen aplicaciones podrían tener más permisos que aquellos que se les creían asignados. Por ejemplo, cuando los usuarios administrativos crean o modifican una aplicación, pueden seleccionar las aplicaciones dependientes que no están en su ámbito de seguridad.|  
|Al configurar entornos virtuales de Microsoft Application Virtualization (App-V), seleccionar aplicaciones del entorno virtual que tengan el mismo nivel de confianza.|Dado que las aplicaciones de un entorno virtual de App-V pueden compartir recursos, como el Portapapeles, configure el entorno virtual de tal modo que las aplicaciones seleccionadas tengan el mismo nivel de confianza.<br /><br /> Para obtener más información, consulte [Create App-V virtual environments](../../apps/deploy-use/create-app-v-virtual-environments.md) (Crear entornos virtuales de App-V).|  
|Si implementa aplicaciones para equipos Mac, asegúrese de que los archivos de origen proceden de una fuente de confianza.|La herramienta CMAppUtil no valida la firma del paquete de origen, por lo que debe asegurarse de que proviene de una fuente de confianza. La herramienta CMAppUtil no puede detectar si los archivos han sido manipulados.|  
|Al implementar aplicaciones para equipos Mac, proteja la ubicación del archivo **.cmmac** y el canal de comunicación al importar este archivo en Configuration Manager.|Dado que el archivo **.cmmac** que genera la herramienta CMAppUtil, y que importa en Configuration Manager no está firmado ni validado, para evitar su manipulación, almacénelo en una carpeta protegida, y utilice IPsec o SMB entre los siguientes equipos:<br /><br /> - El equipo que ejecuta la consola de Configuration Manager.<br /><br /> - El equipo que almacena el archivo **.cmmac**.|  
|Si configura un tipo de implementación de aplicaciones web, use HTTPS en lugar de HTTP para proteger la conexión|Si implementa una aplicación web utilizando un vínculo HTTP en lugar de un vínculo HTTPS, el dispositivo se podría redirigir a un servidor malintencionado y los datos transferidos entre el dispositivo y el servidor se podrían manipular.|  

##  <a name="security-issues-for-application-management"></a>Problemas de seguridad para la administración de aplicaciones  

-   Los usuarios con derechos reducidos pueden copiar archivos desde la memoria caché del equipo cliente.  

     Los usuarios pueden leer la memoria caché del cliente, pero no pueden escribir en ella. Con permisos de lectura, un usuario puede copiar archivos de instalación de aplicaciones de un equipo a otro.  

-   Los usuarios con derechos reducidos pueden modificar los archivos que registran el historial de implementaciones de software en el equipo cliente.  

     Dado que la información de historial de aplicaciones no está protegida, un usuario puede modificar archivos que notifican si una aplicación está instalada.  

-   Los paquetes de App-V no están firmados.  

     Los paquetes de App-V de Configuration Manager no admiten la firma para comprobar que el contenido procede de un origen de confianza, y si se modificó en tránsito. No hay solución para este problema de seguridad; asegúrese de que sigue la práctica de seguridad para descargar el contenido desde un origen de confianza y una ubicación segura.  

-   Todos los usuarios del equipo pueden instalar las aplicaciones de App-V publicadas.  

     Cuando se publica una aplicación de App-V en un equipo, todos los usuarios que inician sesión en dicho equipo pueden instalarla. Esto significa que, una vez publicada, no se podrá restringir qué usuarios podrán instalar la publicación.  

-   No puede restringir los permisos de instalación para el portal de la empresa  

     Aunque puede configurar la configuración de un cliente para restringir permisos de instalación, por ejemplo, a usuarios primarios de un dispositivo o a administradores locales solo, esta configuración no funciona para el portal de la compañía. Esto podría resultar en una elevación de privilegios porque un usuario podría instalar una aplicación que no debería poder instalar.  

##  <a name="certificates-for-microsoft-silverlight-5-and-elevated-trust-mode-required-for-the-application-catalog"></a>Certificados de Microsoft Silverlight 5 y modo de confianza elevado necesarios para el catálogo de aplicaciones  
 Los clientes de Configuration Manager requieren Microsoft Silverlight 5, que se debe ejecutar en modo de confianza elevado para que los usuarios puedan instalar software del catálogo de aplicaciones. De forma predeterminada, las aplicaciones de Silverlight se ejecutan en modo de confianza parcial para evitar que las aplicaciones accedan a los datos de usuario. Configuration Manager instala Microsoft Silverlight 5 automáticamente en los clientes (si no está ya instalado) y establece de forma predeterminada en **Sí** la configuración de cliente **Permitir que las aplicaciones de Silverlight se ejecuten en modo de confianza elevado** del Agente de equipo. Esta opción permite que las aplicaciones de Silverlight firmadas y de confianza soliciten el modo de confianza elevado.  

 Cuando instala el rol del sistema de sitio del punto de sitios web del catálogo de aplicaciones, el cliente también instala el certificado de firma de Microsoft en el almacén de equipo de editores de confianza de cada equipo cliente de Configuration Manager. Este certificado permite que las aplicaciones de Silverlight firmadas por este certificado se ejecuten en el modo de confianza elevado que requieren los equipos para instalar software desde el catálogo de aplicaciones. Configuration Manager administra automáticamente este certificado de firma. Para garantizar la continuidad del servicio, no elimine ni mueva manualmente este certificado de firma de Microsoft.  

> [!WARNING]  
>  Si está habilitada, la opción de cliente **Permitir que las aplicaciones de Silverlight se ejecuten en modo de confianza elevado** permite que todas las aplicaciones de Silverlight firmadas por certificados del almacén de certificados de editores de confianza del almacén del equipo o el almacén del usuario se ejecuten en modo de confianza elevado. La opción de cliente no puede habilitar el modo de confianza elevado específicamente para el catálogo de aplicaciones de Configuration Manager ni para el almacén de certificados de editores de confianza del almacén del equipo. Si una aplicación de malware agrega un certificado no autorizado en el almacén de editores de confianza, en el almacén del usuario, por ejemplo, el malware que utilice su propia aplicación de Silverlight podrá ejecutarse en modo de confianza elevado.  

 Si configura la opción de cliente **Permitir que las aplicaciones de Silverlight se ejecuten en modo de confianza elevado** en **No**, no se quitará el certificado de firma de Microsoft de los clientes.  

 Para obtener más información acerca de las aplicaciones de confianza en Silverlight, consulte [Trusted Applications (Aplicaciones de confianza)](http://go.microsoft.com/fwlink/p/?LinkId=252842).  

##  <a name="privacy-information-for-application-management"></a>Información de privacidad para la administración de aplicaciones  
 La administración de aplicaciones permite ejecutar cualquier aplicación, programa o script en cualquier equipo cliente o dispositivo móvil cliente de la jerarquía. Configuration Manager no tiene control sobre los tipos de aplicaciones, programas o scripts que se ejecutan, ni sobre el tipo de información que transmiten. Durante el proceso de implementación de aplicaciones, es posible que Configuration Manager transmita información entre clientes y servidores que permite identificar las cuentas de dispositivo y de inicio de sesión.  

 Configuration Manager mantiene información de estado sobre el proceso de implementación de software. La información del estado de la implementación de software no se cifra durante la transmisión, a menos que el cliente se comunique mediante HTTPS. La información de estado no se almacena en un formato cifrado en la base de datos.  

 El uso de la instalación de la aplicación de Configuration Manager para instalar software de forma remota, interactiva y silenciosa en el cliente podría estar sujeto a términos de licencia específicos para dicho software, independientes de los términos de licencia de software para System Center Configuration Manager. Revise y acepte siempre los términos de licencia de software antes de implementar software mediante Configuration Manager.  

 La implementación de la aplicación no se efectúa de forma predeterminada. Requiere varios pasos de configuración.  

 Dos características opcionales que permiten una implementación eficaz del software son la afinidad entre usuario y dispositivo y el catálogo de aplicaciones:  

-   La afinidad entre usuario y dispositivo asigna un usuario a los dispositivos de tal modo que un administrador de Configuration Manager pueda, así, implementar software en un usuario, y este software se instale automáticamente en el equipo, o los equipos, que el usuario utiliza con más frecuencia.  

-   El catálogo de aplicaciones es un sitio web que permite a los usuarios solicitar el software que van a instalar.  

 Consulte las secciones siguientes para obtener información sobre la privacidad en la afinidad entre usuario y dispositivo y el catálogo de aplicaciones.  

 Para configurar la administración de aplicaciones, tenga en cuenta los requisitos de privacidad.  

##  <a name="user-device-affinity"></a>Afinidad de dispositivo de usuario  
-  Configuration Manager puede transmitir información entre clientes y sistemas de sitios de punto de administración que permite identificar las cuentas de equipo y de inicio de sesión, y el resumen de uso de cuentas de inicio de sesión.  
-  La información que se transmite entre el cliente y el servidor no se cifra a menos que el punto de administración esté configurado para requerir que los clientes se comuniquen mediante HTTPS.  
-  La información de uso del equipo y la cuenta de inicio de sesión que se usa para asignar un usuario a un dispositivo se almacena en equipos cliente, se envía a puntos de administración y, a continuación, se almacena en la base de datos de Configuration Manager. La información antigua se elimina de la base de datos de manera predeterminada después de 90 días. Se puede configurar la eliminación mediante la tarea de mantenimiento de sitio **Eliminar datos antiguos de afinidad entre usuario y dispositivo** .
-  Configuration Manager conserva la información de estado sobre la afinidad entre usuario y dispositivo. La información de estado no se cifra durante la transmisión a menos que los clientes estén configurados para comunicarse con los puntos de administración mediante HTTPS. La información de estado no se almacena en un formato cifrado en la base de datos.  
-  La información de uso de la cuenta de inicio de sesión y del equipo y la información de estado no se envían a Microsoft.  
-  La información de uso de inicio de sesión y de equipo que se usa para establecer la afinidad entre usuario y dispositivo siempre está habilitada. Además, los usuarios y los usuarios administrativos pueden proporcionar información de afinidad de dispositivo de usuario.  

##  <a name="application-catalog"></a>Catálogo de aplicaciones  
-  El catálogo de aplicaciones permite al administrador de Configuration Manager publicar aplicaciones, programas o scripts para que los ejecuten los usuarios. Configuration Manager no ejerce ningún control sobre los tipos de programas o scripts que se publican en el catálogo, o sobre el tipo de información que transmiten.    
-  Configuration Manager puede transmitir información entre clientes y los roles de sistema de sitio del catálogo de aplicaciones que permite identificar las cuentas de equipo y de inicio de sesión. La información que se transmite entre el cliente y los servidores no se cifra a menos que los roles de sistema de sitio estén configurados para requerir que los clientes se comuniquen mediante HTTPS.  
-  La información acerca de las solicitudes de aprobación de aplicaciones se almacena en la base de datos de Configuration Manager. Las solicitudes que se cancelan o se deniegan se eliminan de forma predeterminada después de 30 días, junto con las entradas del historial de solicitudes correspondientes. Se puede configurar la eliminación mediante la tarea de mantenimiento de sitio **Eliminar datos antiguos de solicitud de la aplicación** . Las solicitudes de aprobación de aplicaciones que están en estados aprobados y pendientes no se eliminan nunca.  
-  La información que se envía a y desde el catálogo de aplicaciones no se envía a Microsoft.  
-  El catálogo de aplicaciones no se instala de forma predeterminada. La instalación requiere varios pasos de configuración.  



<!--HONumber=Nov16_HO1-->


