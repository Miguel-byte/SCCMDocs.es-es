---
title: Seguridad y privacidad de la administración de aplicaciones
titleSuffix: Configuration Manager
description: Obtenga información sobre instrucciones y recomendaciones de seguridad y privacidad para la administración de aplicaciones.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 4d26deed-3b16-4116-b640-f618f2c20f5a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 80ae609bccd60e68cfee76878bd7a461b5f61716
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="security-and-privacy-for-application-management-in-system-center-configuration-manager"></a>Seguridad y privacidad de la administración de aplicaciones en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*


##  <a name="security-guidance-for-application-management"></a>Instrucciones de seguridad para la administración de aplicaciones  

|Instrucciones de seguridad|Más información|  
|----------------------------|----------------------|  
|Configurar los puntos del catálogo de aplicaciones para que utilicen conexiones HTTPS y formar a los usuarios acerca de los peligros de los sitios web malintencionados.|Configure el punto de sitios web del catálogo de aplicaciones y el punto de servicio web del catálogo de aplicaciones para aceptar conexiones HTTPS. Con esta configuración, el servidor se autentica a los usuarios y los datos transmitidos se protegen contra la manipulación y la visualización. Forme a los usuarios para que solo se conecten a sitios web de confianza y contribuya a evitar ataques de ingeniería social.<br /><br /> Cuando no se use HTTPS, no use las opciones de la configuración de personalización de marca, en las que se muestra el nombre de la organización en el catálogo de aplicaciones como prueba de identificación.|  
|Utilizar la separación de roles, y no instalar el punto de sitios web y el punto de servicio del catálogo de aplicaciones en el mismo servidor.|Si el punto de sitios web del catálogo de aplicaciones se ve comprometido, instálelo en otro servidor para separarlo del punto del servicio web del catálogo de aplicaciones. Este diseño ayuda a proteger los clientes y la infraestructura de Configuration Manager. Esta configuración es especialmente importante si el punto de sitios web del catálogo de aplicaciones acepta conexiones de cliente desde Internet. Hace que el servidor sea vulnerable a los ataques.|  
|Formar a los usuarios para que cierren la ventana del explorador cuando terminen de utilizar el catálogo de aplicaciones.|Si los usuarios utilizan para visitar un sitio web externo la misma ventana del explorador que utilizaron para el catálogo de aplicaciones, el explorador también utilizará la configuración de seguridad aplicable a los sitios de confianza de la intranet.|  
|Especifique manualmente la afinidad de dispositivo del usuario en lugar de permitir a los usuarios identificar su dispositivo primario. No habilite la configuración basada en el uso.|No considere información de autoridad aquélla recopilada de usuarios o del dispositivo. Si se implementa software mediante afinidad entre usuario y dispositivo no especificada por un administrador de confianza, es posible que el software se instale en equipos y usuarios sin autorización para recibir ese software.|  
|Configurar siempre las implementaciones para que descarguen contenido desde los puntos de distribución, en lugar de ejecutarlo desde los puntos de distribución.|Si configura las implementaciones para que descarguen el contenido desde un punto de distribución para ejecutarlo localmente, el cliente de Configuration Manager comprueba el hash de paquete una vez descargado el contenido. El cliente descarta el paquete si el hash no coincide con el hash de la directiva. Por el contrario, si la implementación se configura para que se ejecute directamente desde un punto de distribución, el cliente de Configuration Manager no comprueba el hash de paquete. Este comportamiento significa que el cliente de Configuration Manager puede instalar software que se ha manipulado.<br /><br /> Si tiene que ejecutar implementaciones directamente desde puntos de distribución, use los mínimos permisos posibles de NTFS en los paquetes de los puntos de distribución. Además, use el protocolo de seguridad de Internet (IPsec) para proteger el canal entre el cliente y los puntos de distribución, y entre los puntos de distribución y el servidor de sitio.|  
|<a name="bkmk_interact"></a>No permita a los usuarios interactuar con las aplicaciones si habilita las opciones **Ejecutar con derechos administrativos** o **Instalar para el sistema**.|Cuando se configura una aplicación, se puede establecer la opción en **Permitir a los usuarios ver la instalación del programa e interactuar con la misma**. Esta configuración permite a los usuarios responder a los mensajes necesarios en la interfaz de usuario. Si también se configura la aplicación con **Ejecutar con derechos administrativos**, o bien con **Instalar para el sistema** a partir de la versión 1802, un atacante en el equipo que ejecute el programa podría usar la interfaz de usuario para escalar privilegios en el equipo cliente.<br /><br /> Use los programas que usan Windows Installer para el programa de instalación y los privilegios elevados por usuario para las implementaciones de software que requieren credenciales administrativas. El programa de instalación se debe ejecutar en el contexto de un usuario que no tiene credenciales administrativas. Los privilegios elevados por usuario de Windows Installer proporcionan el modo más seguro de implementar aplicaciones que tienen este requisito.|  
|Restringir si los usuarios pueden instalar software de forma interactiva mediante la configuración de cliente **Permisos de instalación** .|Utilice la configuración de dispositivo de cliente **Instalar permisos** de **Agente de equipo** para restringir los tipos de usuario que pueden instalar software mediante el catálogo de aplicaciones o el Centro de software. Por ejemplo, cree una configuración de cliente personalizada con **Solo administradores** en **Instalar permisos**. A continuación, aplique esta configuración de cliente a una recopilación de servidores para que los usuarios que no tienen permisos administrativos no puedan instalar software en los equipos.|  
|Para dispositivos móviles, implementar solo aplicaciones que estén firmadas.|En dispositivos móviles, implemente solo aplicaciones de código firmado por una entidad de certificación (CA) que sea de confianza para el dispositivo móvil. Por ejemplo:<br /><ul><li>Una aplicación de un proveedor, que está firmada por una entidad de certificación conocida, como VeriSign.</li><li>Una aplicación interna que firma mediante una entidad de certificación interna, en la que no interviene Configuration Manager.</li><li>Una aplicación interna que firma mediante Configuration Manager cuando crea el tipo de aplicación y utiliza un certificado de firma.</li></ul>|  
|Si firma aplicaciones de dispositivos móviles mediante el **Asistente para crear aplicaciones** de Configuration Manager, proteja la ubicación del archivo de certificado de firma y el canal de comunicación.|Para proteger frente a la elevación de privilegios y ataques de tipo "Man in the middle", almacene el archivo de certificado de firma en una carpeta protegida. Use IPsec entre los equipos siguientes:<br /><ul><li>El equipo que ejecuta la consola de Configuration Manager.</li><li>El equipo que almacena el archivo de firma de certificados.</li><li>El equipo que almacena los archivos de origen de la aplicación.</li></ul> También puede firmar la aplicación sin que intervenga Configuration Manager y antes de ejecutar el **Asistente para crear aplicaciones**.|  
|Para proteger los equipos de referencia, implemente controles de acceso.|Si un usuario administrativo configura el método de detección en un tipo de implementación a través de un equipo de referencia, asegúrese de que no se afectó la seguridad del equipo.|  
|Restrinja y supervise los usuarios administrativos a los que se conceden los siguientes roles de seguridad basados en roles de administración de aplicaciones:<br /><ul><li>**Administrador de aplicaciones**</li><li>**Autor de aplicaciones**</li><li> **Administrador de implementación de aplicaciones**</li></ul>|Aunque configure la administración basada en roles, los usuarios administrativos que creen e implementen aplicaciones podrían tener más permisos que aquellos que se les creían asignados. Por ejemplo, los usuarios administrativos que crean o modifican una aplicación, pueden seleccionar aplicaciones dependientes que no están en su ámbito de seguridad.|  
|Al configurar entornos virtuales de Microsoft Application Virtualization (App-V), seleccione aplicaciones del entorno virtual que tengan el mismo nivel de confianza en el entorno virtual.|Dado que las aplicaciones de un entorno virtual de App-V pueden compartir recursos, como el Portapapeles, configure el entorno virtual de tal modo que las aplicaciones seleccionadas tengan el mismo nivel de confianza.<br /><br /> Para obtener más información, consulte [Create App-V virtual environments](../../apps/deploy-use/create-app-v-virtual-environments.md) (Crear entornos virtuales de App-V).|  
|Si implementa aplicaciones para equipos Mac, asegúrese de que los archivos de origen proceden de una fuente de confianza.|La herramienta CMAppUtil no valida la firma del paquete de origen, por lo que debe asegurarse de que proviene de una fuente de confianza. La herramienta CMAppUtil no puede detectar si los archivos han sido manipulados.|  
|Al implementar aplicaciones para equipos Mac, proteja la ubicación del archivo **.cmmac** y el canal de comunicación al importar este archivo en Configuration Manager.|El archivo **.cmmac** que genera la herramienta CMAppUtil, y que importa en Configuration Manager ya no está firmado o validado. Para ayudar a evitar la alteración de este archivo, almacénelo en una carpeta protegida y utilice IPsec o SMB entre los siguientes equipos:<br /><br /><ul><li>El equipo que ejecuta la consola de Configuration Manager.</li><li>El equipo que almacena el archivo **.cmmac**.</li></ul>|  
|Si configura un tipo de implementación de aplicaciones web, use HTTPS en lugar de HTTP para proteger la conexión.|Si se implementa una aplicación web mediante un vínculo HTTP en lugar de un vínculo HTTPS, el dispositivo se podría redirigir a un servidor malintencionado. Los datos transferidos entre el dispositivo y el servidor se podrían manipular.|  



##  <a name="security-issues-for-application-management"></a>Problemas de seguridad para la administración de aplicaciones  

-   Los usuarios con derechos reducidos pueden copiar archivos desde la memoria caché del equipo cliente.  

     Los usuarios pueden leer la caché de cliente pero no pueden escribir en ella. Con permisos de lectura, un usuario puede copiar archivos de instalación de aplicaciones de un equipo a otro.  

-   Los usuarios con derechos reducidos pueden cambiar los archivos que registran el historial de implementaciones de software en el equipo cliente.  

     Como la información de historial de aplicaciones no está protegida, un usuario puede cambiar los archivos que notifican si una aplicación está instalada.  

-   Los paquetes de App-V no están firmados.  

     En Configuration Manager, los paquetes de App-V no admiten firma. Las firmas digitales comprueban que el contenido procede de un origen de confianza y no se modificó en el tránsito. No hay solución para este problema de seguridad. Siga el procedimiento recomendado de seguridad para descargar el contenido desde un origen de confianza y una ubicación segura.  

-   Todos los usuarios del equipo pueden instalar las aplicaciones de App-V publicadas.  

     Cuando se publica una aplicación de App-V en un equipo, todos los usuarios que inician sesión en dicho equipo pueden instalarla. Una vez publicada, no se puede restringir qué usuarios pueden instalar la publicación.  

-   No puede restringir los permisos de instalación para el portal de la empresa.  

     Aunque se puede establecer una configuración de cliente para restringir los permisos de instalación, por ejemplo a usuarios primarios de un dispositivo o a administradores locales solo, esta configuración no funciona para el portal de empresa. Este problema podría producir una elevación de privilegios. Los usuarios podrían instalar una aplicación que no deberían poder instalar.  



##  <a name="BKMK_CertificatesSilverlight5"></a> Certificados de Microsoft Silverlight 5 y modo de confianza elevado necesarios para el catálogo de aplicaciones  
 Los clientes de Configuration Manager requieren Microsoft Silverlight 5, que se debe ejecutar en modo de confianza elevado para que los usuarios puedan instalar software del catálogo de aplicaciones. De forma predeterminada, las aplicaciones de Silverlight se ejecutan en modo de confianza parcial para evitar que las aplicaciones accedan a los datos de usuario. Si todavía no está instalado, Configuration Manager instala automáticamente Microsoft Silverlight 5 en los clientes. De forma predeterminada, Configuration Manager establece la configuración de cliente **Permitir que las aplicaciones de Silverlight se ejecuten en modo de confianza elevado** de Agente de equipo en **Sí**. Esta opción permite que las aplicaciones de Silverlight firmadas y de confianza soliciten el modo de confianza elevado.  

 Cuando instala el rol del sistema de sitio del punto de sitios web del catálogo de aplicaciones, el cliente también instala el certificado de firma de Microsoft en el almacén de equipo de editores de confianza de cada equipo cliente de Configuration Manager. Las aplicaciones de Silverlight firmadas por este certificado se ejecutan en modo de confianza elevado, que requiere que los equipos instalen el software desde el catálogo de aplicaciones. Configuration Manager administra automáticamente este certificado de firma. Para garantizar la continuidad del servicio, no elimine ni mueva manualmente este certificado de firma de Microsoft.  

> [!WARNING]  
>  Cuando se habilita, la configuración de cliente **Permitir que las aplicaciones de Silverlight se ejecuten en modo de confianza elevado** permite que todas las aplicaciones de Silverlight, firmadas por certificados del almacén de certificados de editores de confianza del almacén del equipo o el almacén del usuario, se ejecuten en modo de confianza elevado. La configuración de cliente no puede habilitar el modo de confianza elevado específicamente para el catálogo de aplicaciones de Configuration Manager ni para el almacén de certificados de editores de confianza del almacén del equipo. Si el malware agrega un certificado no autorizado en el almacén de editores de confianza, el malware que use su propia aplicación de Silverlight ahora también se puede ejecutar en modo de confianza elevado.  

 Si establece la opción **Permitir que las aplicaciones de Silverlight se ejecuten en modo de confianza elevado** en **No**, los clientes no quitan el certificado de firma de Microsoft.  

 Para más información acerca de las aplicaciones de confianza en Silverlight, vea [Aplicaciones de confianza](https://go.microsoft.com/fwlink/p/?LinkId=252842).  

 > [!NOTE]
 > A partir de Configuration Manager 1802, Silverlight ya no se instala de manera automática. La funcionalidad principal del Catálogo de aplicaciones ahora se incluye en el Centro de software. La compatibilidad con el sitio web del Catálogo de aplicaciones finaliza con la primera actualización publicada después del 1 de junio de 2018.



##  <a name="privacy-information-for-application-management"></a>Información de privacidad para la administración de aplicaciones  
 La administración de aplicaciones permite ejecutar cualquier aplicación, programa o script en cualquier cliente de la jerarquía. Configuration Manager no tiene control acerca de los tipos de aplicaciones, programas o scripts que se ejecutan, ni acerca de el tipo de información que transmiten. Durante el proceso de implementación de aplicaciones, es posible que Configuration Manager transmita información que identifique el dispositivo y las cuentas de inicio de sesión entre clientes y servidores.  

 Configuration Manager mantiene información de estado sobre el proceso de implementación de software. La información del estado de la implementación de software no se cifra durante la transmisión, a menos que el cliente se comunique mediante HTTPS. La información de estado no se almacena en un formato cifrado en la base de datos.  

 El uso de la instalación de la aplicación de Configuration Manager para instalar software de forma remota, interactiva y silenciosa en el cliente podría estar sujeto a términos de licencia para dicho software. Este uso es independiente de los términos de licencia de software para System Center Configuration Manager. Revise y acepte siempre los términos de licencia de software antes de implementar software mediante Configuration Manager.  

 La implementación de la aplicación no se efectúa de forma predeterminada y requiere varios pasos de configuración.  

 Dos características opcionales que permiten una implementación eficaz del software son la afinidad entre usuario y dispositivo y el catálogo de aplicaciones:  

-   La afinidad entre usuario y dispositivo asigna un usuario a dispositivos. Un administrador de Configuration Manager implementa software en un usuario. El cliente instala automáticamente el software en uno o más equipos que el usuario usa con más frecuencia.  

-   El catálogo de aplicaciones es un sitio web que permite a los usuarios solicitar el software que van a instalar.  

 Consulte las secciones siguientes para obtener información sobre la privacidad en la afinidad entre usuario y dispositivo y el catálogo de aplicaciones.  

 Para configurar la administración de aplicaciones, tenga en cuenta los requisitos de privacidad.  



##  <a name="user-device-affinity"></a>Afinidad de dispositivo de usuario  
-  Configuration Manager puede transmitir información entre clientes y sistemas del sitio del punto de administración. La información puede identificar al equipo y a la cuenta de inicio de sesión, y el uso resumido de cuentas de inicio de sesión.  
-  La información que se transmite entre el cliente y el servidor no se cifra, a menos que el punto de administración esté configurado para requerir que los clientes se comuniquen mediante HTTPS.  
-  La información de uso del equipo y la cuenta de inicio de sesión, que se usa para asignar un usuario a un dispositivo, se almacena en los equipos cliente, se envía a los puntos de administración y, después, se almacena en la base de datos de Configuration Manager. La información antigua se elimina de la base de datos de manera predeterminada después de 90 días. Se puede configurar la eliminación mediante la tarea de mantenimiento de sitio **Eliminar datos antiguos de afinidad entre usuario y dispositivo** .
-  Configuration Manager conserva la información de estado sobre la afinidad entre usuario y dispositivo. La información de estado no se cifra durante la transmisión a menos que los clientes estén configurados para comunicarse con los puntos de administración mediante HTTPS. La información de estado no se almacena en un formato cifrado en la base de datos.  
-  La información de uso de la cuenta de inicio de sesión y del equipo, y la información de estado no se envían a Microsoft.  
-  La información de uso de inicio de sesión y de equipo que se usa para establecer la afinidad entre usuario y dispositivo siempre está habilitada. Además, los usuarios y los usuarios administrativos pueden proporcionar información de afinidad de dispositivo de usuario.  



##  <a name="application-catalog"></a>Catálogo de aplicaciones  
-  El catálogo de aplicaciones permite al administrador de Configuration Manager publicar aplicaciones, programas o scripts para que los ejecuten los usuarios. Configuration Manager no ejerce ningún control acerca de los tipos de programas o scripts que se publican en el catálogo, o acerca de el tipo de información que transmiten.    
-  Configuration Manager puede transmitir información entre clientes y los roles de sistema de sitio del catálogo de aplicaciones. La información permite identificar las cuentas de equipo y de inicio de sesión. La información que se transmite entre el cliente y los servidores no se cifra, a menos que se configuren los roles de sistema de sitio para requerir que los clientes se conecten mediante HTTPS.  
-  La información acerca de las solicitudes de aprobación de aplicaciones se almacena en la base de datos de Configuration Manager. Las solicitudes que se cancelan o se deniegan se eliminan de forma predeterminada después de 30 días, junto con las entradas del historial de solicitudes correspondientes. Se puede configurar la eliminación mediante la tarea de mantenimiento de sitio **Eliminar datos antiguos de solicitud de la aplicación** . Las solicitudes de aprobación de aplicaciones que están en estados aprobados y pendientes no se eliminan nunca.  
-  La información que se envía a y desde el catálogo de aplicaciones no se envía a Microsoft.  
-  El catálogo de aplicaciones no se instala de forma predeterminada. La instalación requiere varios pasos de configuración.  
