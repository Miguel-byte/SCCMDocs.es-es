---
title: "Procedimientos recomendados para la implementación de clientes | Microsoft Docs"
description: "Conozca procedimientos recomendados para la implementación de clientes en System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: a933d69c-5feb-4b2b-84e8-56b3b64d5947
caps.latest.revision: 11
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 55c953f312a9fb31e7276dde2fdd59f8183b4e4d
ms.openlocfilehash: 49b2520a82614bedc7bcc077604e0b89885119c2


---
# <a name="best-practices-for-client-deployment-in-system-center-configuration-manager"></a>Procedimientos recomendados para la implementación de clientes en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Use los siguientes procedimientos recomendados como ayuda para implementar clientes en equipos en System Center Configuration Manager.  

## <a name="use-software-update-based-client-installation-for-active-directory-computers"></a>Utilice la instalación de clientes basada en actualizaciones de software para equipos de Active Directory  
 Este método de implementación de clientes tiene la ventaja de usar tecnologías de Windows existentes, se integra con la infraestructura de Active Directory, necesita una configuración mínima en Configuration Manager, es el más fácil de configurar para los firewalls y es el más seguro. Al usar los grupos de seguridad y el filtrado WMI para la configuración de la directiva de grupo, dispone también de una gran flexibilidad para controlar en qué equipos se instala el cliente de Configuration Manager.  

 Para más información, vea [How to Install Configuration Manager Clients by Using Software Update-Based Installation (Cómo instalar clientes de Configuration Manager mediante una instalación basada en software)](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientSUP).  

## <a name="extend-the-active-directory-schema-and-publish-the-site-so-that-you-can-run-ccmsetup-without-command-line-options"></a>Extienda el esquema de Active Directory y publique el sitio para que pueda ejecutar CCMSetup sin opciones de línea de comandos  
 Cuando extiende el esquema de Active Directory para Configuration Manager y el sitio se publica en Active Directory Domain Services, muchas propiedades de instalación de cliente se publican en Active Directory Domain Services. Si un equipo puede ubicar estas propiedades de instalación de cliente, puede usarlas durante la implementación de cliente de Configuration Manager. Dado que esta información se genera automáticamente, se elimina el riesgo de error humano asociado con escribir manualmente las propiedades de la instalación.  

 Para más información, vea [Acerca de las propiedades de instalación de cliente publicadas en Servicios de dominio de Active Directory en Configuration Manager](../../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md).  

## <a name="when-you-have-many-clients-to-deploy-plan-a-phased-rollout-outside-business-hours"></a>Cuando hay que implementar muchos clientes, planee una implementación en fases fuera del horario comercial  
 Minimice el efecto de los requisitos de procesamiento de la CPU en el servidor del sitio mediante la planeación una implementación por fases de los clientes durante un período de tiempo. Implemente los clientes fuera del horario comercial, para que los servicios críticos del negocio dispongan de más ancho de banda durante el día y los usuarios no se vean afectados si su equipo se ralentiza o necesita reiniciarse para completar la instalación.  

## <a name="enable-automatic-upgrade-after-your-main-client-deployment-has-finished"></a>Habilite la actualización automática una vez finalizada la implementación principal de clientes  
 Las actualizaciones automáticas de cliente son útiles cuando desea actualizar un número reducido de equipos cliente que puede que su método de instalación principal de cliente haya omitido. Por ejemplo, cuando se ha completado una actualización de cliente inicial, pero algunos clientes estaban sin conexión durante la implementación de la actualización. A continuación, utilice este método para actualizar el cliente en estos equipos la próxima vez que estén activos.  

> [!NOTE]  
>  Las mejoras de rendimiento de Configuration Manager permiten usar las actualizaciones automáticas como método principal de actualización de clientes. Sin embargo, el rendimiento dependerá de la infraestructura de la jerarquía como, por ejemplo, el número de clientes.  

 Para más información sobre el método automático de actualización de clientes, vea [How to upgrade clients for Windows computers in System Center Configuration Manager (Cómo actualizar clientes de equipos Windows en System Center Configuration Manager)](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

## <a name="use-smsmp-and-fsp-if-you-install-the-client-with-clientmsi-properties"></a>Utilice SMSMP y FSP si instala el cliente con propiedades de client.msi  
 La propiedad SMSMP especifica el punto de administración inicial con el que el cliente se comunica y elimina la dependencia de soluciones de ubicación de servicios como Servicios de dominio de Active Directory, DNS o WINS.  

 Utilice la propiedad FSP e instale un punto de estado de reserva, de modo que pueda supervisar la instalación y asignación del cliente, e identificar los problemas de comunicación.  

 Para más información sobre estas opciones, vea [Acerca de las propiedades de instalación de cliente de Configuración Manager](../../../../core/clients/deploy/about-client-installation-properties.md).  

## <a name="if-you-want-to-use-client-languages-other-than-english-install-the-client-language-packs-before-you-install-the-clients"></a>Si desea utilizar otros idiomas de cliente que no sean el inglés, instale los paquetes de idioma de cliente antes de instalar los clientes  
 Si instala los paquetes de idioma de cliente en un sitio después de instalar los clientes, debe volver a instalar los clientes para poder utilizar los idiomas adicionales. Para los clientes de dispositivos móviles, esto significa que debe borrar el dispositivo móvil e inscribirlo otra vez.  

 Para más información sobre cómo agregar compatibilidad con idiomas de cliente adicionales, vea [Language Packs in System Center Configuration Manager (Paquetes de idioma en System Center Configuration Manager)](../../../../core/servers/deploy/install/language-packs.md).  

## <a name="plan-and-prepare-any-required-pki-certificates-in-advance"></a>Planificación y preparación anticipadas de los certificados PKI necesarios  
 Para administrar dispositivos en Internet, dispositivos móviles inscritos y equipos Mac, debe tener los certificados PKI en sistemas del sitio (puntos de administración y distribución) y los dispositivos cliente. Para muchos usuarios, esto requiere un plan y preparación avanzados, especialmente si se dispone de un equipo independiente que administra las PKI. En redes de producción, es posible que necesite aprobación de administración de cambios para utilizar los nuevos certificados y reiniciar los servidores del sistema de sitio, o los usuarios tendrán que cerrar e iniciar sesión para la nueva pertenencia a grupos. Además, tendría que dejar tiempo suficiente para la replicación de los permisos de seguridad y las nuevas plantillas de certificado.  

 Para más información sobre los certificados PKI necesarios, vea [Requisitos de certificados PKI para System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

## <a name="before-you-install-clients-configure-any-required-client-settings-and-maintenance-windows"></a>Antes de instalar clientes, configure las opciones de cliente y las ventanas de mantenimiento requeridas  
 Aunque puede configurar los ajustes del cliente y las ventanas de mantenimiento antes o después de instalar los clientes, configure los ajustes necesarios antes de instalar los clientes para que estos valores se empleen tan pronto como el cliente esté instalado. Para más información, vea [Cómo establecer la configuración del cliente en Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md)  

 Configure ventanas de mantenimiento para servidores y dispositivos de Windows Embedded, a fin de garantizar la continuidad del funcionamiento de dichos equipos, que a menudo son críticos para el negocio. Por ejemplo, las ventanas de mantenimiento garantizan que las actualizaciones de software y el software antimalware requeridos no reinician el equipo durante el horario comercial.  

> [!IMPORTANT]  
>  Para equipos de Windows 10 que se van a proteger con el filtro de escritura unificado (UWF), debe configurar el dispositivo para UWF antes de instalar el cliente. Esto permite a Configuration Manager instalar el cliente con un proveedor de credenciales personalizadas que evita que los usuarios con pocos derechos inicien sesión en el dispositivo durante el modo de mantenimiento.  

## <a name="for-mac-computers-and-mobile-devices-that-are-enrolled-by-configuration-manager-plan-your-user-enrollment-experience"></a>Para los equipos Mac y dispositivos móviles inscritos por Configuration Manager, planee su experiencia de inscripción de usuario  
 Si los usuarios inscriben sus propios equipos y dispositivos móviles Mac mediante Configuration Manager, planee y preparare la experiencia del usuario. Por ejemplo, es posible que cree un script para la instalación y la inscripción mediante el uso de una página web para que los usuarios especifiquen la cantidad mínima de información necesaria y les envíe las instrucciones con un vínculo por correo electrónico.  

## <a name="when-you-manage-windows-embedded-devices-use-file-based-write-filters-fbwf-rather-than-enhanced-write-filters-ewf-for-higher-scalability"></a>Si administra dispositivos de Windows Embedded, use filtros de escritura basados en archivo (FBWF) en lugar de filtros de escritura mejorados (EWF) para una mayor escalabilidad  
 Los dispositivos incrustados que utilizan filtros de escritura mejorados (EWF) son propensos a experimentar resincronizaciones de mensaje de estado. Si tiene pocos dispositivos incrustados que utilizan filtros de escritura mejorados, es posible que no perciba este comportamiento. Sin embargo, si cuenta con una gran cantidad de dispositivos incrustados que resincronizan su información, tales como el envío del inventario completo del lugar de un inventario diferencial, esto puede generar un incremento notable en los paquetes de red y un mayor procesamiento de la CPU en el servidor de sitio.  

 Si puede elegir qué tipo de filtro de escritura habilitar, elija los filtros de escritura basados ​​en archivo y configure excepciones para conservar el estado del cliente y los datos de inventario entre los reinicios del dispositivo por motivos de eficiencia de la red y la CPU en el cliente de Configuration Manager. Para más información sobre los filtros de escritura, vea [Planning for client deployment to Windows Embedded devices in System Center Configuration Manager (Planeación de implementación de cliente en dispositivos de Windows Embedded en System Center Configuration Manager)](../../../../core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md).  

 Para más información sobre el número máximo de clientes de Windows Embedded que un sitio primario puede admitir, vea [Supported operating systems for clients and devices (Sistemas operativos compatibles con clientes y dispositivos)](../../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md).  



<!--HONumber=Dec16_HO3-->


