---
title: "Planear la puerta de enlace de administración en la nube | Microsoft Docs"
description: 
ms.date: 12/19/2016
ms.prod: configuration-manager
ms.technology:
- configmgr-client
ms.assetid: 2dc8c9f1-4176-4e35-9794-f44b15f4e55f
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1df2d8bcd73633ac1d37cc3ef31343be9c5bc95d
ms.openlocfilehash: 6e2895565e868eb80a8f4f4b46b8a28eb4961e28

---

# <a name="plan-for-cloud-management-gateway-in-configuration-manager"></a>Planear la puerta de enlace de administración en la nube para Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

A partir de la versión 1610, la puerta de enlace de administración en la nube proporciona una manera sencilla de administrar clientes de Configuration Manager en Internet. El servicio de puerta de enlace de administración en la nube se implementa en Microsoft Azure y requiere una suscripción de Azure. Se conecta a la infraestructura de Configuration Manager local con un nuevo rol denominado punto de conexión de la puerta de enlace de administración en la nube. Una vez implementado y configurado, los clientes podrán tener acceso a los roles de sistema de sitio locales de Configuration Manager independientemente de si están conectados a la red interna privada o a Internet.

Use la consola de Configuration Manager para implementar el servicio en Azure, agregar el rol de punto de conexión de la puerta de enlace de administración en la nube y configurar roles de sistema de sitio para permitir el tráfico de la puerta de enlace de administración en la nube. La puerta de enlace de administración en la nube de momento solo admite los roles de punto de administración y punto de actualización de software.

Se necesitan certificados de cliente y de capa de sockets seguros (SSL) para autenticar los equipos y cifrar las comunicaciones entre los diferentes niveles del servicio. Los equipos cliente normalmente reciben un certificado de cliente mediante la aplicación de directivas de grupo. Para cifrar el tráfico entre los clientes y el servidor de sistema de sitio que hospeda los roles, tiene que crear un certificado SSL personalizado de la CA. También debe configurar un certificado de administración en Azure que permita a Configuration Manager implementar el servicio de puerta de enlace de administración en la nube.

## <a name="requirements-for-cloud-management-gateway"></a>Requisitos para la puerta de enlace de administración en la nube

-   Equipos cliente y servidor de sistema de sitio que ejecuten el punto de conexión de la puerta de enlace de administración en la nube.

-   Certificados SSL personalizados de la CA interna: se usan para cifrar la comunicación de los equipos cliente y para autenticar la identidad del servicio de puerta de enlace de administración en la nube.

-   Suscripción de Azure para los servicios en la nube.

-   Certificado de administración de Azure: se usa para autenticar Configuration Manager con Azure.

## <a name="specifications-for-cloud-management-gateway"></a>Especificaciones para la puerta de enlace de administración en la nube

- Cada instancia de puerta de enlace de administración en la nube admite 4000 clientes.
- Se recomienda que cree al menos dos instancias de puerta de enlace de administración en la nube para mejorar la disponibilidad.
- La puerta de enlace de administración en la nube solo admite los roles de punto de administración y punto de actualización de software.
-   En estos momentos, las siguientes características de Configuration Manager no son compatibles con la puerta de enlace de administración en la nube:

    -   Actualizaciones e implementaciones de cliente con la inserción de cliente
    -   Asignación automática de sitio
    -   Directivas de usuario
    -   Catálogo de aplicaciones (incluidas las solicitudes de aprobación de software)
    -   Implementación completa de sistema operativo (OSD)
    -   Consola de Configuration Manager
    -   Herramientas remotas
    -   Sitio web de generación de informes
    -   Wake on LAN
    -   Clientes Mac, Linux y UNIX
    -   Azure Resource Manager
    -   Almacenamiento en caché del mismo nivel
    -   Administración local de dispositivos móviles

## <a name="cost-of-cloud-management-gateway"></a>Costo de la puerta de enlace de administración en la nube

>[!IMPORTANT]
>La información de costo que se proporciona a continuación se indica solo con fines de estimación. Su entorno puede tener otras variables que afecten al costo general del uso de la puerta de enlace de administración en la nube.

La puerta de enlace de administración en la nube usa la siguiente característica de Microsoft Azure, que genera gastos en la cuenta de suscripción de Azure:

-   Máquina virtual

    -   En estos momentos, la puerta de enlace de administración en la nube necesita una máquina virtual Standard\_A2. Al crear el servicio, puede seleccionar cuántas máquinas virtuales va a admitir el servicio (una es el valor predeterminado).

    -   Solo con fines de estimación, tenga en cuenta que una única máquina virtual Standard\_A2 de Azure puede admitir aproximadamente 2000 clientes simultáneos basados en Internet.

    -   Vea la [Calculadora de precios de Azure](https://azure.microsoft.com/en-us/pricing/calculator/) para determinar los costos potenciales.

      >[!NOTE]
      >Los costos de máquina virtual varían según la región.

-   Transferencia de datos de salida

    -   Se incurren gastos por el flujo de datos fuera del servicio. Vea [Detalles de precios de ancho de banda de Azure](https://azure.microsoft.com/en-us/pricing/details/bandwidth/) para determinar los costos potenciales.

    -   Solo con fines de estimación, calcule aproximadamente 100 MB por cliente al mes para clientes basados en Internet que realizan actualizaciones de directivas cada hora.

    >[!NOTE]
    > Realizar otras acciones admitidas mediante la puerta de enlace de administración en la nube (por ejemplo, implementar actualizaciones de software o aplicaciones) aumentará la cantidad de transferencia de datos de salida de Azure.

-   Almacenamiento de contenido

    -   Los clientes basados en Internet que se administran con la puerta de enlace de administración en la nube obtendrán contenido de actualización de software desde Windows Update sin ningún costo.

    -   Cualquier otro contenido necesario (por ejemplo, aplicaciones) debe distribuirse a un punto de distribución basado en la nube. En estos momentos, la puerta de enlace de administración en la nube solo admite el punto de distribución de nube para enviar contenido a los clientes.

    - Vea el costo de usar una [distribución basada en la nube](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#cost-of-using-cloud-based-distribution) para obtener más información.

## <a name="next-steps"></a>Pasos siguientes

[Configurar puerta de enlace de administración en la nube](setup-cloud-management-gateway.md)



<!--HONumber=Dec16_HO3-->


