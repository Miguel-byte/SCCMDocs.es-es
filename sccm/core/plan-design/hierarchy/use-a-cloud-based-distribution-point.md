---
title: "Punto de distribución basado en la nube | Microsoft Docs"
description: "Obtenga información sobre las configuraciones y las limitaciones del uso de un punto de distribución basado en la nube con System Center Configuration Manager."
ms.custom: na
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3cd9c725-6b42-427d-9191-86e67f84e48c
caps.latest.revision: 9
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: f9097014c7e988ec8e139e518355c4efb19172b3
ms.openlocfilehash: 489f38d3f88391e42b5271c03151203d22b26d9e
ms.lasthandoff: 03/04/2017


---
# <a name="use-a-cloud-based-distribution-point-with-system-center-configuration-manager"></a>Use punto de distribución basado en la nube con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Un punto de distribución basado en la nube de System Center Configuration Manager es un punto de distribución hospedado en Microsoft Azure. La información siguiente está pensada para ayudarle a aprender sobre las configuraciones y las limitaciones del uso de un punto de distribución basado en la nube.

Después de instalar un sitio primario y cuando esté preparado para instalar un punto de distribución basado en la nube, vea [Instalar puntos de distribución basados en la nube en Microsoft Azure para System Center Configuration Manager](../../../core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md).


## <a name="plan-to-use-a-cloud-based-distribution-point"></a>Planeamiento para usar un punto de distribución basado en la nube
Cuando se usa un punto de distribución basado en la nube, es posible:  

-   **Configurar el cliente** para habilitar usuarios y dispositivos de modo que tengan acceso al contenido.  

-   **Especificar un sitio primario para administrar la transferencia de contenido** al punto de distribución.  

-   **Especificar umbrales** para la cantidad de contenido que desea almacenar en el punto de distribución y la cantidad de contenido que desea permitir que los clientes transfieran desde el punto de distribución.  


En función de los umbrales que configure, Configuration Manager puede generar alertas para avisarle cuando la cantidad combinada de contenido que ha almacenado en el punto de distribución se aproxime a la cantidad de almacenamiento especificada, o cuando las transferencias de datos por parte de los clientes estén cerca de los umbrales definidos.  

Los puntos de distribución basados en la nube admiten varias características que también se ofrecen en puntos de distribución locales:  

-   Es posible administrar puntos de distribución basados en la nube individualmente o como miembros de grupos de puntos de distribución.  

-   Puede utilizar un punto de distribución basado en la nube como ubicación de contenido de reserva.  

-   Dispone de soporte para clientes basados en intranet y en Internet.  


Los puntos de distribución basados en la nube ofrecen las siguientes ventajas adicionales:  

-   Configuration Manager cifra el contenido enviado a un punto de distribución basado en la nube antes de que Configuration Manager lo envíe a Azure.  

-   En Azure, es posible escalar manualmente el servicio en la nube para satisfacer las cambiantes exigencias de solicitud de contenido por parte de los clientes, sin necesidad de instalar y aprovisionar otros puntos de distribución.  

-   El punto de distribución basado en la nube es compatible con la descarga de contenido por parte de clientes configurados para Windows BranchCache.  


Un punto de distribución basado en la nube tiene las siguientes limitaciones:  

-  Antes de usar la versión 1610 con la revisión KB4010155, no se puede usar un punto de distribución basado en la nube para hospedar paquetes de actualización de software. Este problema está corregido a partir de la versión 1702.  

-   No se puede usar un punto de distribución basado en la nube con implementaciones habilitadas para PXE o multidifusión.  

-   Los clientes no tienen un punto de distribución basado en la nube como ubicación de contenido para una secuencia de tareas implementada mediante la opción **Descargar el contenido localmente cuando sea necesario mediante la ejecución de una secuencia de tareas**. Sin embargo, las secuencias de tareas implementadas mediante la opción de implementación **Descargar todo el contenido localmente antes de iniciar la secuencia de tareas** pueden usar un punto de distribución basado en la nube como ubicación de contenido válida.  

-   Un punto de distribución basado en la nube no admite paquetes que se ejecutan desde el punto de distribución. Todo el contenido debe descargarlo el cliente y ejecutarse localmente.  

-   Los puntos de distribución basados en la nube no admiten aplicaciones de transmisión por secuencias mediante Application Virtualization o programas similares.  

-   Los puntos de distribución basados en la nube no admiten contenido preconfigurado. El administrador de la distribución del sitio primario que administra el punto de distribución transfiere todo el contenido al punto de distribución.  

-   No se pueden configurar puntos de distribución basados en la nube como puntos de distribución de extracción.  

##  <a name="BKMK_PrereqsCloudDP"></a> Requisitos previos para puntos de distribución basados en la nube  
 Los puntos de distribución basados en la nube requieren los siguientes requisitos previos para su uso:  

-   Una suscripción a Azure (vea [Acerca de las suscripciones y los certificados](#BKMK_CloudDPCerts) en este tema).

-   Un certificado autofirmado o de administración de infraestructura de clave pública (PKI) para la comunicación desde un servidor de sitio primario de Configuration Manager con el servicio en la nube de Microsoft Azure (vea [Acerca de las suscripciones y los certificados](#BKMK_CloudDPCerts) en este tema).

-   Un certificado de servicio (PKI) que los clientes de Configuration Manager usan para conectarse a los puntos de distribución basados en la nube y descargar contenido de los mismos mediante HTTPS.  

-  Para poder acceder al contenido desde un punto de distribución en la nube, un dispositivo o usuario debe tener la opción **Permitir acceso al punto de distribución de nube** establecida en **Sí** en la configuración de cliente de **Cloud Services**. De forma predeterminada, este valor está establecido como **No**.  

-   Los clientes deben poder resolver el nombre del servicio en la nube, lo que requiere un alias de Sistema de nombres de dominio (DNS) y un registro CNAME en el espacio de nombres DNS.  

-   Los clientes deben poder acceder a Internet para utilizar el punto de distribución basado en la nube.  

##  <a name="BKMK_CloudDPCost"></a> Costo de la utilización la distribución basada en la nube  
 Cuando use un punto de distribución basado en la nube, planee el costo del almacenamiento de datos y las transferencias de descarga que realizan los clientes de Configuration Manager.  

 Configuration Manager incluye opciones para ayudar a controlar los costos y supervisar el acceso a datos:  

-   Puede controlar y supervisar la cantidad de contenido que se almacena en un servicio en la nube.  

-   Puede configurar Configuration Manager para que le alerte cuando los **umbrales** de las descargas de cliente alcancen o superen el límite mensual.  

-   Además, puede usar el almacenamiento en caché de sistemas de mismo nivel (Windows BranchCache) para contribuir a reducir el número de transferencias de datos desde puntos de distribución basados en la nube por parte de los clientes. Los clientes de Configuration Manager configurados para BranchCache pueden transferir contenido mediante puntos de distribución basados en la nube.  


**Opciones**  

-   **Configuración de cliente para la nube**: el acceso a todos los puntos de distribución basados en la nube de una jerarquía se controla mediante **Configuración de cliente**.  

     En **Configuración de cliente**, la categoría **Configuración de nube** admite la opción **Permitir acceso a puntos de distribución en la nube**. De forma predeterminada, esta opción está establecida en **No**. Puede habilitar esta opción para usuarios y para dispositivos.  

-   **Umbrales para transferencias de datos**: puede configurar umbrales para la cantidad de datos que desea almacenar en el punto de distribución y para la cantidad de datos que los clientes pueden descargar desde el punto de distribución.  

     Los umbrales para los puntos de distribución basados en la nube son los siguientes:  

    -   **Umbral de alerta de almacenamiento**: un umbral de alerta de almacenamiento, establece un límite superior para la cantidad de datos o de contenido que se desea almacenar en el punto de distribución basado en la nube. Configuration Manager puede generar una advertencia cuando se alcance el nivel de espacio libre restante que se haya especificado.  

    -   **Umbral de alerta de transferencia**: un umbral de alerta de transferencia permite supervisar la cantidad de contenido que se transfiere desde el punto de distribución a los clientes durante un período de 30 días. El umbral de alerta de transferencia supervisa la transferencia de datos que se ha realizado durante los últimos 30 días y puede generar una alerta de advertencia y una alerta crítica cuando se alcanzan los valores que se definieron.  

        > [!IMPORTANT]  
        >  Configuration Manager supervisa la transferencia de datos, pero no detiene la transferencia cuando se supera el valor establecido en el umbral de alerta de transferencia.  

 Los umbrales de cada punto de distribución basado en la nube se pueden especificar durante la instalación del punto de distribución, aunque, una vez instalado, también se pueden editar sus propiedades.  

-   **Alertas**: se puede configurar Configuration Manager para que genere alertas basadas en las transferencias de datos que se realizan a cada punto de distribución basado en la nube, y desde este, en función de los umbrales de transferencia de datos que especifique. Estas alertas son útiles para supervisar las transferencias de datos y permiten decidir cuándo se debe detener el servicio en la nube, ajustar el contenido que se almacena en el punto de distribución o modificar los clientes que pueden utilizar los puntos de distribución basados en la nube.  

     En un ciclo de una hora, el sitio primario que supervisa el punto de distribución basado en la nube descarga los datos de transacciones desde Azure y los almacena en CloudDP-&lt;nombreDelServicio\>.log en el servidor de sitio. Configuration Manager evalúa esta información teniendo en cuenta las cuotas de transferencia y almacenamiento de cada punto de distribución basado en la nube. Si la transferencia de datos alcanza o supera el volumen especificado de alertas de advertencia o de alertas críticas, Configuration Manager generará la alerta correspondiente.  

    > [!WARNING]  
    >  Dado que la información de transferencias de datos se descarga desde Azure cada hora, el uso de datos podría superar el valor establecido en un umbral de alerta de advertencia o de alerta crítica antes de que Configuration Manager tenga acceso a los datos y genere una alerta.  

    > [!NOTE]  
    >  Las alertas para un punto de distribución basado en la nube dependen de las estadísticas de uso de Azure, que pueden tardar hasta 24 horas en estar disponibles. Para obtener información sobre el análisis de almacenamiento de Azure y su frecuencia de actualización de estadísticas de uso, vea [Storage Analytics](http://go.microsoft.com/fwlink/p/?LinkID=275111) (Análisis de almacenamiento) en MSDN Library.  


-   **Detener o iniciar el servicio de nube a petición**: se puede utilizar la opción de detener un servicio de nube en cualquier momento para que los clientes no puedan utilizarlo de forma continuada. Una vez detenido el servicio de nube, los clientes no podrán descargar contenido adicional desde él. También puede reiniciar el servicio de nube para restaurar el acceso para los clientes. Por ejemplo, suponga que desea detener un servicio de nube cuando se alcancen los umbrales de datos.  

     Cuando se detiene un servicio de nube, éste no elimina el contenido del punto de distribución; por lo tanto, el servidor del sitio puede continuar con la transferencia de contenido adicional al punto de distribución basado en la nube.  

     Para detener un servicio en la nube, en la consola de Configuration Manager, seleccione el punto de distribución del nodo **Puntos de distribución de nube** en **Servicios en la nube**, en el área de trabajo **Administración**. Después elija **Detener servicio** para detener el servicio en la nube que se ejecuta en Azure.  

##  <a name="BKMK_CloudDPCerts"></a> Acerca de las suscripciones y los certificados para puntos de distribución basados en la nube  
 Los puntos de distribución basados en la nube requieren certificados para permitir que Configuration Manager administre el servicio en la nube que hospeda el punto de distribución, y para que los clientes obtengan acceso al contenido del punto de distribución. A continuación se proporciona información general acerca de estos certificados. Para más información, consulte [Requisitos de certificados PKI para System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md).  

 **Certificados**  

-   **Certificado de administración para la comunicación desde el servidor de sitio al punto de distribución**: el certificado de administración establece confianza entre la API de administración de Azure y Configuration Manager. Esta autenticación permite a Configuration Manager llamar a la API de Azure cuando se realizan tareas como la implementación de contenido o el inicio y la detención del servicio en la nube. Con Azure, puede crear sus propios certificados de administración, que pueden ser certificados autofirmados o certificados emitidos por una entidad de certificación (CA):  

    -   Proporcione el archivo .cer del certificado de administración a Azure durante la configuración de Azure para Configuration Manager. El archivo .cer contiene la clave pública para el certificado de administración. Debe cargar el certificado en Azure antes de instalar un punto de distribución basado en la nube. Este certificado permite a Configuration Manager acceder a la API de Azure.  

    -   Proporcione el archivo .pfx del certificado de la administración a Configuration Manager al instalar el punto de distribución basado en la nube. El archivo .pfx contiene la clave privada para el certificado de administración. Configuration Manager almacena este certificado en la base de datos del sitio. Dado que el archivo .pfx contiene la clave privada, debe proporcionar la contraseña para importar este archivo de certificado en la base de datos de Configuration Manager.  

    Si crea un certificado autofirmado, debe exportar primero el certificado como archivo .cer y luego exportarlo de nuevo como archivo .pfx.  

    También puede especificar un archivo **.publishsettings** de versión uno desde el SDK 1.7 de Azure. Para obtener información sobre los archivos publishsettings, consulte la documentación de Azure.  

    Para obtener más información, consulte [Crear un certificado de administración para Windows Azure](http://go.microsoft.com/fwlink/p/?LinkId=220281) y [Agregar un certificado de administración a una suscripción de Windows Azure](http://go.microsoft.com/fwlink/p/?LinkId=241722) en la sección Plataforma Windows Azure de MSDN Library.  

-   **Certificado de servicio para la comunicación del cliente con el punto de distribución**: el certificado de servicio de punto de distribución basado en la nube de Configuration Manager establece confianza entre los clientes de Configuration Manager y el punto de distribución basado en la nube y protege los datos que los clientes descargan del mismo mediante la capa de sockets seguros (SSL) a través de HTTPS.  

    > [!IMPORTANT]  
    >  El nombre común en el cuadro del sujeto del certificado del certificado de servicio debe ser único en el dominio y no debe coincidir con ningún dispositivo unido a un dominio.  

   Para ver una implementación de ejemplo de este certificado, vea la sección **Implementación del certificado de servicio para puntos de distribución basados en la nube** en el tema [Ejemplo paso a paso de la implementación de los certificados PKI para System Center Configuration Manager: entidad de certificación de Windows Server 2008](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  

##  <a name="bkmk_Tasks"></a> Tareas de administración comunes para puntos de distribución basados en la nube  

-   **Comunicación entre servidor de sitio y el punto de distribución basado en la nube**: cuando se instala un punto de distribución basado en la nube, es necesario asignar un sitio primario para administrar la transferencia de contenido al servicio en la nube. Esta acción es equivalente a la instalación del rol del sistema de sitio de punto de distribución en un determinado sitio.  

-   **Comunicación entre cliente y punto de distribución basado en la nube**: cuando un dispositivo o un usuario de un dispositivo tienen una configuración de cliente que habilita el uso de un punto de distribución basado en la nube, el dispositivo puede recibir el punto de distribución basado en la nube como una ubicación de contenido válida:  

    -   El punto de distribución basado en la nube se considera un punto de distribución remoto cuando un cliente evalúa las ubicaciones de contenido disponibles.  

    -   Los clientes de la intranet solo utilizan puntos de distribución basados en la nube como una opción de reserva si no están disponibles los puntos de distribución locales.  

    Aunque se instalen puntos de distribución basados en la nube en determinadas regiones de Azure, los clientes que usan puntos de distribución basados en la nube no tienen en cuenta dichas regiones y seleccionan puntos de distribución basados en la nube de manera no determinista.

Por lo tanto, si instala puntos de distribución basados en la nube en varias regiones y un cliente recibe varios puntos de distribución basados en la nube como ubicaciones de contenido, es posible que el cliente no use un punto de distribución basado en la nube de la misma región de Azure.  

Los clientes que usan puntos de distribución basados en la nube utilizan la siguiente secuencia para solicitudes de ubicación del contenido:  

1.  Un cliente que está configurado para utilizar puntos de distribución basados en la nube siempre intenta obtener contenido de un punto de distribución preferido en primer lugar.  

2.  Si un punto de distribución preferido no está disponible, el cliente utiliza un punto de distribución remoto, si la implementación es compatible con esta opción y si hay un punto de distribución remoto disponible.  

3.  Si no está disponible un punto de distribución preferido o un punto de distribución remoto, el cliente puede entonces intentar obtener el contenido de un punto de distribución basado en la nube.  



  Cuando un cliente usa un punto de distribución basado en la nube como una ubicación de contenido, el cliente se autentica a sí mismo en el punto de distribución basado en la nube mediante un token de acceso de Configuration Manager. Si el cliente confía en el certificado de punto de distribución basado en la nube de Configuration Manager, el cliente puede entonces descargar el contenido solicitado.  

-   **Supervisar puntos de distribución basados en la nube**: puede supervisar el contenido que se implementa en cada punto de distribución y el servicio en la nube que hospeda el punto de distribución.  

    -   **Contenido**: el contenido que se implementa en un punto de distribución basado en la nube se supervisa del mismo modo que el contenido que se implementa en puntos de distribución locales.  

    -   **Servicio en la nube**: Configuration Manager comprueba periódicamente el servicio de Azure y genera una alerta si no está activo o si existe algún problema con las suscripciones o los certificados. Los detalles del punto de distribución también se pueden ver en el nodo **Puntos de distribución de nube** en **Servicios en la nube** en el área de trabajo **Administración** de la consola de Configuration Manager. Desde esta ubicación, puede verse información de alto nivel sobre el punto de distribución. Puede seleccionar también un punto de distribución y editar sus propiedades.  

    Al editar las propiedades de un punto de distribución basado en la nube, es posible realizar lo siguiente:  

    -   Ajustar los umbrales de datos para el almacenamiento y las alertas.  

    -   Administrar el contenido tal y como se haría con un punto de distribución local.  

    Por último, se puede ver, pero no editar, el identificador de suscripción o el nombre del servicio, entre otros detalles, especificados cuando se instaló el punto de distribución basado en la nube.  

-   **Copia de seguridad y recuperación de puntos de distribución basados en la nube**: si usa un punto de distribución basado en la nube en la jerarquía, utilice la siguiente información para planear la copia de seguridad o la recuperación del punto de distribución:  

    -   Si usa la tarea de mantenimiento **Copia de seguridad del servidor del sitio**, Configuration Manager incluye de forma automática las configuraciones para el punto de distribución basado en la nube.  

    -   Como procedimiento recomendado, haga una copia de seguridad del certificado de administración y del certificado de servicio utilizados con un punto de distribución basado en la nube, y guárdela. Si restaura en otro equipo el sitio primario de Configuration Manager que administra el punto de distribución basado en la nube, tendrá que volver a importar los certificados para poder seguir usándolos.  

-   **Desinstalar un punto de distribución basado en la nube**: para desinstalar un punto de distribución basado en la nube, seleccione el punto de distribución en la consola de Configuration Manager y luego seleccione **Eliminar**.  

    Cuando se elimina un punto de distribución basado en la nube de una jerarquía, Configuration Manager quita el contenido del servicio en la nube en Azure.  

