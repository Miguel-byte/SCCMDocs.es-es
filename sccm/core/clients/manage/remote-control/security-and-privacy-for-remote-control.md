---
title: Seguridad y privacidad del control remoto | Microsoft Docs
description: "Obtenga información sobre seguridad y privacidad del control remoto en System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 272ee86b-d3d9-4fd9-b5c4-73e490e1a1e4
caps.latest.revision: 6
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: fc392e4440e84614f92218e9c7a09ec1c2c64f53
ms.openlocfilehash: 342a58d2b7439f721381beb43188594b5278043d


---
# <a name="security-and-privacy-for-remote-control-in-system-center-configuration-manager"></a>Seguridad y privacidad del control remoto en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Este tema contiene información sobre la seguridad y privacidad del control remoto en System Center 2012 Configuration Manager.  

##  <a name="a-namebkmksecurityhardwareinventorya-security-best-practices-for-remote-control"></a><a name="BKMK_Security_HardwareInventory"></a> Procedimientos recomendados de seguridad para el control remoto  
 Use los siguientes procedimientos recomendados de seguridad para administrar los equipos cliente mediante control remoto.  

|Práctica recomendada de seguridad|Más información|  
|----------------------------|----------------------|  
|Cuando se conecte a un equipo remoto, no continúe si se usa NTLM en lugar de la autenticación Kerberos.|Cuando Configuration Manager detecta que la sesión de control remoto se autentica mediante NTLM en lugar de hacerlo mediante Kerberos, aparece un mensaje que advierte de que no se puede comprobar la identidad del equipo remoto. No continúe con la sesión de control remoto. La autenticación NTLM es un protocolo de autenticación más débil que Kerberos y es vulnerable a la reproducción y la suplantación.|  
|No habilite el uso compartido del Portapapeles en el visor de control remoto.|El Portapapeles admite objetos como archivos ejecutables y texto, y el usuario podría usarlo en el equipo host durante la sesión de control remoto para ejecutar un programa en el equipo de origen.|  
|No introduzca contraseñas para cuentas con privilegios cuando administre de forma remota un equipo.|El software que observa la entrada de teclado podría capturar la contraseña. O bien, si el programa que se está ejecutando en el equipo cliente no es el programa que supone el usuario de control remoto, el programa podría capturar la contraseña. Cuando se necesitan cuentas y contraseñas, el usuario final debe escribirlas.|  
|Bloquee el teclado y el mouse durante una sesión de control remoto.|Si Configuration Manager detecta que ha finalizado la conexión de control remoto, bloquea automáticamente el teclado y el mouse para que ningún usuario pueda tomar el control de la sesión abierta de control remoto. Sin embargo, puede que esta detección no se produzca inmediatamente y no se produce si se finaliza el servicio de control remoto.<br /><br /> Seleccione la acción **Bloquear teclado y mouse remotos** en la ventana **Control remoto de ConfigMgr** .|  
|No permita a los usuarios configurar el control remoto en el Centro de software.|No habilite **Los usuarios pueden cambiar la directiva o la configuración de notificaciones en el Centro de software** en la configuración de cliente para ayudar a impedir que se espíe a los usuarios.<br /><br /> Esta configuración es para el equipo, no para el usuario que inició sesión.|  
|Habilite el perfil **Dominio** de Firewall de Windows.|Habilite **Habilitar control remoto en clientes Perfiles de excepción de firewall** en la configuración de cliente y, a continuación, seleccione el Firewall de Windows **Dominio** para los equipos de la intranet.|  
|Si cierra la sesión durante una sesión de control remoto e inicia la sesión como un usuario diferente, asegúrese de que cierra la sesión antes de desconectar la sesión de control remoto.|Si no cierra la sesión en este escenario, la sesión permanece abierta.|  
|No conceda a los usuarios derechos de administrador local.|Al proporcionar a los usuarios derechos de administrador local, pueden hacerse cargo de la sesión de control remoto o poner en peligro sus credenciales.|  
|Use la directiva de grupo o Configuration Manager para configurar la Asistencia remota, pero no ambos.|Puede usar Configuration Manager y la directiva de grupo para efectuar cambios en la configuración de la Asistencia remota. Cuando se actualiza la directiva de grupo en el cliente, de forma predeterminada, optimiza el proceso cambiando únicamente las directivas que han cambiado en el servidor. Configuration Manager cambia la configuración de la directiva de seguridad local, que no se puede sobrescribir a menos que se fuerce la actualización de la directiva de grupo.<br /><br /> La configuración de la directiva en ambos lugares podría producir resultados incoherentes. Elija uno de estos métodos para configurar la Asistencia remota.|  
|Habilite **Solicitar al usuario permiso de control remoto**en la configuración de cliente.|Aunque hay formas de esta configuración de cliente que piden al usuario que una sesión de control remoto, habilite esta opción para reducir la posibilidad de que se espíe a los usuarios mientras trabajan en tareas confidenciales.<br /><br /> Además, enseñe a los usuarios a que comprueben el nombre de cuenta que se muestra durante la sesión de control remoto y desconecten la sesión si sospechan que la cuenta no está autorizada.|  
|Limite la lista de visores permitidos.|Los derechos de administrador local no son necesarios para que un usuario pueda usar el control remoto.|  

### <a name="security-issues-for-remote-control"></a>Problemas de seguridad para el control remoto  
 La administración de equipos cliente mediante el control remoto tiene los siguientes problemas de seguridad:  

-   No considere confiables los mensajes de auditoría de control remoto.  

     Si inicia una sesión de control remoto y, a continuación, inicia sesión con unas credenciales alternativas, la cuenta original envía los mensajes de auditoría, no la cuenta que usó las credenciales alternativas.  

     No se envían mensajes de auditoría si se copian los archivos binarios para el control remoto en lugar de instalar la consola de Configuration Manager y, luego, ejecutar el control remoto en el símbolo del sistema.  

##  <a name="a-namebkmkprivacyhardwareinventorya-privacy-information-for-remote-control"></a><a name="BKMK_Privacy_HardwareInventory"></a> Información de privacidad para el control remoto  
 El control remoto le permite ver las sesiones activas en los equipos cliente de Configuration Manager y le ofrece la posibilidad de consultar toda la información almacenada en estos equipos. De forma predeterminada, no está habilitado el control remoto.  

 Aunque puede configurar el control remoto para proporcionar un aviso notorio y obtener el consentimiento de un usuario antes de iniciar una sesión de control remoto, también puede supervisar a los usuarios sin su permiso o conocimiento. Puede configurar el nivel de acceso como solo vista para que no se pueda cambiar nada en el control remoto o como control total. La cuenta del administrador de conexión se muestra en la sesión de control remoto, para ayudar a los usuarios a identificar quién se conecta a su equipo.  

 De forma predeterminada, Configuration Manager concede permisos de control remoto al grupo de administradores locales.  

 Antes de configurar el control remoto, tenga en cuenta sus requisitos de privacidad.  



<!--HONumber=Dec16_HO3-->


