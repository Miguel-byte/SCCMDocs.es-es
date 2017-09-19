---
title: "Métodos de instalación de clientes | Microsoft Docs"
description: "Conozca los métodos de instalación de cliente para System Center Configuration Manager."
ms.custom: na
ms.date: 04/25/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 51b5964b-374d-4abc-8619-414a9fffad2d
caps.latest.revision: "9"
caps.handback.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 23dcf515b12cc91b25bedf8b42397cc815f901eb
ms.sourcegitcommit: b438515490e04fb09c82a8af642d38e9a0605178
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/15/2017
---
# <a name="client-installation-methods-in-system-center-configuration-manager"></a>Métodos de instalación de cliente en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Puede usar diferentes métodos para instalar el software cliente de Configuration Manager. Puede usar un método o una combinación de ellos. En este tema puede obtener información sobre cada método para saber cuál de ellos funcionará mejor en su organización.  

## <a name="client-push-installation"></a>Instalación de inserción de cliente  

 **Plataforma de cliente admitida:** Windows  

 **Ventajas**  

-   Se puede utilizar para instalar el cliente en un solo equipo, en una recopilación de equipos o en los resultados de una consulta.  

-   Se puede utilizar para instalar automáticamente el cliente en todos los equipos detectados.  

-   Usa automáticamente las propiedades de instalación de cliente definidas en la pestaña **Cliente** del cuadro de diálogo **Propiedades de instalación de inserción de cliente**.  

 **Desventajas**  

-   Puede causar mucho tráfico de red si se realiza la inserción en recopilaciones de gran volumen.  

-   Solo se puede usar en equipos detectados por Configuration Manager.  

-   No se puede utilizar para instalar clientes en un grupo de trabajo.  

-   Debe especificar una cuenta de instalación de inserción de cliente que tenga derechos administrativos en el equipo cliente especificado.  

-   Se deben configurar excepciones en el Firewall de Windows en los equipos cliente para que se pueda completar la instalación de inserción de cliente.  

-   La instalación de inserción de cliente no se puede cancelar. Cuando usa este método de instalación de cliente para un sitio, Configuration Manager intenta instalar el cliente en todos los recursos detectados y vuelve a intentar las instalaciones erróneas durante siete días como máximo.  

 Para más información sobre este método de instalación, vea [How to deploy clients to Windows computers in System Center Configuration Manager (Cómo implementar clientes en equipos Windows con System Center Configuration Manager)](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md).  

## <a name="software-update-point-based-installation"></a>Instalación basada en el punto de actualización de software  
 **Plataforma de cliente admitida:** Windows  

 **Ventajas:**  

-   Puede utilizar la infraestructura existente de actualizaciones de software para administrar el software cliente.  

-   Puede instalar automáticamente el software cliente en nuevos equipos si se configuraron correctamente las opciones de Windows Server Update Services (WSUS) y las opciones de directiva de grupo en Servicios de dominio de Active Directory.  

-   No requiere la detección de equipos para instalar el cliente.  

-   Los equipos pueden leer las propiedades de instalación de cliente publicadas en Servicios de dominio de Active Directory.  

-   El software cliente se volverá a instalar si se quita.  

-   No requiere la configuración y el mantenimiento de una cuenta de instalación para el equipo cliente especificado.  

 **Desventajas:**  

-   Requiere una infraestructura de actualizaciones de software operativa como requisito previo.  

-   Debe usar el mismo servidor para la instalación de cliente y las actualizaciones de software. El servidor debe residir en un sitio primario.  

-   Para instalar nuevos clientes, debe configurar un objeto de directiva de grupo (GPO) en Active Directory Domain Services con el puerto y el punto de actualización de software activo del cliente.  

-   Si el esquema de Active Directory no se extiende para Configuration Manager, debe usar la configuración de directiva de grupo para aprovisionar equipos con propiedades de instalación de cliente.  

 Para más información sobre este método de instalación, vea [How to deploy clients to Windows computers in System Center Configuration Manager (Cómo implementar clientes en equipos Windows con System Center Configuration Manager)](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md).  

## <a name="group-policy-installation"></a>Instalación de directiva de grupo  
 **Plataforma de cliente admitida:** Windows  

 **Ventajas:**  

-   No requiere la detección de equipos para instalar el cliente.  

-   Se puede utilizar para nuevas instalaciones o actualizaciones de cliente.  

-   Los equipos pueden leer las propiedades de instalación de cliente publicadas en Servicios de dominio de Active Directory.  

-   No requiere la configuración y el mantenimiento de una cuenta de instalación para el equipo cliente especificado.  

 **Desventajas:**  

-   Puede causar mucho tráfico de red si se instala un gran número de clientes.  

-   Si el esquema de Active Directory no se extiende para Configuration Manager, debe usar la configuración de directiva de grupo para agregar propiedades de instalación de cliente a los equipos del sitio.  

 Para más información sobre este método de instalación, vea [How to deploy clients to Windows computers in System Center Configuration Manager (Cómo implementar clientes en equipos Windows con System Center Configuration Manager)](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md).  

## <a name="logon-script-installation"></a>Instalación de script de inicio de sesión  
 **Plataforma de cliente admitida:** Windows  

 **Ventajas:**  

-   No requiere la detección de equipos para instalar el cliente.  

-   Admite el uso de propiedades de línea de comandos para CCMSetup.  

 **Desventajas:**  

-   Puede causar mucho tráfico de red si se instala un gran número de clientes en un breve periodo de tiempo.  

-   Puede tardar bastante tiempo en realizar la instalación en todos los equipos cliente si los usuarios no inician sesión en la red con frecuencia.  

 Para más información sobre este método de instalación, vea [How to deploy clients to Windows computers in System Center Configuration Manager (Cómo implementar clientes en equipos Windows con System Center Configuration Manager)](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md).  

## <a name="manual-installation"></a>Instalación manual  
 **Plataforma de cliente admitida**: Windows, UNIX/Linux, Mac OS X  

 **Ventajas:**  

-   No requiere la detección de equipos para instalar el cliente.  

-   Puede ser útil para realizar pruebas.  

-   Admite el uso de propiedades de línea de comandos para CCMSetup.  

 **Desventajas:**  

-   Carece de automatización y es, por lo tanto, un proceso lento.  

 Para más información acerca de cómo instalar manualmente el cliente en cada plataforma, vea lo siguiente:  

-   [How to deploy clients to Windows computers in System Center Configuration Manager (Cómo implementar clientes en equipos Windows con System Center Configuration Manager)](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md)  

-   [How to deploy clients to UNIX and Linux servers in System Center Configuration Manager (Cómo implementar clientes en servidores UNIX y Linux en System Center Configuration Manager)](../../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md)  

-   [How to deploy clients to Macs in System Center Configuration Manager (Cómo implementar clientes en dispositivos Mac en System Center Configuration Manager)](../../../../core/clients/deploy/deploy-clients-to-macs.md)  
