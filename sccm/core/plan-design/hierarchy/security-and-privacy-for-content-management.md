---
title: "Seguridad y privacidad de la administración de contenido"
titleSuffix: Configuration Manager
description: "Optimice la seguridad y la privacidad de la administración de contenido de System Center Configuration Manager."
ms.custom: na
ms.date: 3/1/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5f38b726-dc00-433a-ba05-5b7dbb0d8e99
caps.latest.revision: "8"
author: aaroncz
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 33a4ac18b95fbafeb0451a7ba8c2e1c757866eda
ms.sourcegitcommit: 7fe45ff75f05f7cc03ad021db8119791abe18049
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/01/2017
---
# <a name="security-and-privacy-for-content-management-for-system-center-configuration-manager"></a>Seguridad y privacidad de la administración de contenido de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Este tema contiene información sobre seguridad y privacidad de la administración de contenido en System Center Configuration Manager. Lea este artículo en conjunto con los temas siguientes:  

-   [Seguridad y privacidad de la administración de aplicaciones en System Center Configuration Manager](../../../apps/plan-design/security-and-privacy-for-application-management.md)  

-   [Seguridad y privacidad de las actualizaciones de software en System Center Configuration Manager](/sccm/sum/plan-design/security-and-privacy-for-software-updates)  

-   [Seguridad y privacidad para implementación de sistema operativo en System Center Configuration Manager](../../../osd/plan-design/security-and-privacy-for-operating-system-deployment.md)  

##  <a name="BKMK_Security_ContentManagement"></a> Prácticas recomendadas de seguridad para la administración de contenido  
 Utilice las siguientes prácticas recomendadas de seguridad para la administración de contenido:  

 **Para los puntos de distribución en la intranet, tenga en cuenta las ventajas y desventajas de usar HTTPS y HTTP**: en la mayoría de los escenarios, el uso de HTTP y cuentas de acceso de paquete de autorización proporcionan mayor seguridad que HTTPS con cifrado pero sin autorización. Sin embargo, si tiene datos confidenciales en el contenido que desea cifrar durante la transferencia, utilice HTTPS.  

-   **Cuando usa HTTPS para un punto de distribución**, Configuration Manager no usa cuentas de acceso de paquete para autorizar el acceso al contenido, pero el contenido se cifra cuando se transfiere a través de la red.  

-   **Cuando usa HTTP para un punto de distribución**, puede utilizar cuentas de acceso de paquete para la autorización, pero el contenido no se cifra cuando se transfiere a través de la red.  


**Si utiliza un certificado de autenticación de cliente de PKI en lugar de un certificado autofirmado para el punto de distribución, proteja el archivo de certificado (.pfx) con una contraseña segura. Si almacena el archivo en la red, proteja el canal de red al importar el archivo en Configuration Manager**: si pide una contraseña para importar el certificado de autenticación del cliente que usa el punto de distribución para comunicarse con los puntos de administración, esto ayuda a proteger el certificado contra posibles ataques. Use la firma del Bloque de mensajes del servidor (SMB) o IPsec entre la ubicación de red y el servidor de sitio para impedir que un atacante pueda manipular el archivo del certificado.  

**Quite el rol de punto de distribución del servidor de sitio**: de forma predeterminada, hay un punto de distribución instalado en el mismo servidor que el servidor de sitio. Los clientes no tienen que comunicarse directamente con el servidor de sitio; por eso, para reducir la superficie expuesta a ataques, asigne el rol de punto de distribución a otros sistemas de sitio y quítelo del servidor de sitio.  

**Asegure el contenido en el nivel de acceso del paquete**: el recurso compartido de punto de distribución permite acceso de lectura a todos los usuarios. Para restringir qué usuarios pueden acceder al contenido, utilice cuentas de acceso de paquete si el punto de distribución está configurado para HTTP. Esto no se aplica a puntos de distribución basados en la nube, ya que no admiten cuentas de acceso de paquete. Para obtener más información sobre las cuentas de acceso de paquete, consulte [Administración de cuentas para acceder al contenido](../../../core/plan-design/hierarchy/manage-accounts-to-access-content.md).


**Si Configuration Manager instala IIS cuando se agrega un rol de sistema de sitio de punto de distribución, quite las herramientas y los scripts de administración de IIS o redirección de HTTP una vez terminada la instalación del punto de distribución**: el punto de distribución no requiere herramientas ni scripts de administración de IIS o redirección de HTTP. Para reducir la superficie expuesta a ataques, quite estos servicios de rol del rol de servidor web (IIS).  Para obtener más información sobre los servicios de rol para el rol de servidor web (IIS) para puntos de distribución, consulte [Site and site system prerequisites](/sccm/core/plan-design/configs/site-and-site-system-prerequisites) (Requisitos previos del sitio y del sistema de sitio).  

**Establezca permisos de acceso al crear el paquete**: dado que los cambios que se hagan en las cuentas de acceso en los archivos de paquete entran en vigor solo cuando se redistribuye el paquete, defina los permisos de acceso de paquete cuidadosamente al crearlo. Esto es especialmente importante en caso de que el paquete sea grande, se distribuya a muchos puntos de distribución y se limite la capacidad de ancho de banda de red para la distribución de contenido.  

**Implementar controles de acceso para proteger los medios con contenido preconfigurado**: el contenido preconfigurado está comprimido pero no cifrado. Un atacante podría leer y modificar los archivos que luego se descargarán a los dispositivos. Los clientes de Configuration Manager rechazan el contenido que se haya alterado, pero igualmente lo descargarán.  

**Importe el contenido preconfigurado usando únicamente la herramienta de línea de comandos ExtractContent (ExtractContent.exe) suministrada con Configuration Manager y asegúrese de que esté firmada por Microsoft**: para evitar que alguien pueda manipular y elevar los privilegios, use solo la herramienta de línea de comandos autorizada que se suministra con Configuration Manager.  

**Proteja el canal de comunicación entre el servidor de sitio y la ubicación de origen del paquete**: use la firma SMB o IPsec entre el servidor de sitio y la ubicación de origen del paquete al crear aplicaciones y paquetes. Esto ayuda a evitar que un atacante pueda manipular los archivos de origen.  

**Si cambia la opción de configuración de sitio para usar un sitio web personalizado en lugar del predeterminado, una vez instalados los roles de punto de distribución, quite los directorios virtuales predeterminados**: cuando se pasa del sitio web predeterminado a uno personalizado, Configuration Manager no quita los directorios virtuales antiguos. Quite los directorios virtuales que Configuration Manager ha creado originalmente en el sitio web predeterminado:  

-   SMS_DP_SMSPKG$  

-   SMS_DP_SMSSIG$  

-   NOCERT_SMS_DP_SMSPKG$  

-   NOCERT_SMS_DP_SMSSIG$  

**Para los puntos de distribución basados en la nube, proteja los detalles de la suscripción y los certificados**: si usa puntos de distribución basados en la nube, proteja artículos de gran valor, incluido el nombre de usuario y la contraseña para la suscripción a Azure, el certificado de administración de Azure y el certificado del servicio de punto de distribución basado en la nube. Almacene los certificados en forma segura y, si llega hasta ellos a través de la red al configurar el punto de distribución basado en la nube, use la firma SMB o IPsec entre el servidor de sitio y la ubicación de origen.  

**Para los puntos de distribución basada en la nube: a fin de minimizar las interrupciones del servicio, supervise la fecha de expiración de los certificados**: Configuration Manager no le avisa cuando los certificados importados para administrar el servicio de punto de distribución basado en la nube están a punto de expirar. Debe supervisar las fechas de expiración independientemente de Configuration Manager y asegurarse de renovar e importar los nuevos certificados antes de la fecha de expiración. Esto es especialmente importante si el certificado de servicio de punto de distribución basado en la nube para Configuration Manager lo compró a una autoridad de certificación (CA) externa, porque podría necesitar tiempo adicional para obtener la renovación del certificado.  

 Si el certificado expira, el Administrador de servicios de nube genera el identificador de mensaje de estado **9425** y el archivo CloudMgr.log contiene una entrada para indicar que el certificado **está en estado expirado**, con la fecha de expiración también registrada en UTC.  

## <a name="security-considerations-for-content-management"></a>Consideraciones de seguridad para la administración de contenido  
Al planear la administración de contenido, tenga en cuenta lo siguiente:  

-   Los clientes no validan el contenido hasta después de descargarlo.  

     Los clientes de Configuration Manager validan el hash de contenido solo después de descargarlo en la memoria caché del cliente. Si un atacante manipula la lista de archivos que se van a descargar o el contenido en sí, el proceso de descarga puede ocupar un ancho de banda considerable hasta que el cliente después vea que debe desechar el contenido al detectar un hash no válido.  

-   Si usa puntos de distribución basados en la nube, el acceso al contenido se restringe automáticamente a la empresa y no puede restringirse aún más a usuarios o grupos determinados.  

-   Si usa puntos de distribución basados en la nube, los clientes son autenticados por el punto de administración y luego emplean un token de Configuration Manager para acceder a los puntos de distribución basados en la nube. El token es válido durante ocho horas. Esto significa que, si se bloquea un cliente porque deja de ser de confianza, igualmente puede seguir descargando contenido desde un punto de distribución basado en la nube hasta que expire el período de validez de este token. En ese momento, el punto de administración no emitirá otro token para el cliente porque el cliente está bloqueado.  

     Para evitar que un cliente bloqueado descargue contenido en este período de ocho horas, puede detener el servicio de nube desde el nodo **Nube**, **Configuración de jerarquía**, en el área de trabajo **Administración** de la consola de Configuration Manager.  

##  <a name="BKMK_Privacy_ContentManagement"></a> Información de privacidad para la administración de contenido  
 Configuration Manager no incluye ningún dato de usuario en los archivos de contenido, aunque un usuario administrativo podría optar por incluirlos.  

 Antes de configurar la administración de contenido, tenga en cuenta los requisitos de privacidad.  
