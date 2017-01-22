---
title: "Seleccionar métodos de detección | Microsoft Docs"
description: "Consulte las consideraciones sobre qué métodos usar y en qué sitios ejecutarlos."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 127ce713-d085-430f-ac7b-2701637fe126
caps.latest.revision: 9
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: 54beff9bc8624d67efda7393db6334ebc96937d7

---
# <a name="select-discovery-methods-to-use-for-system-center-configuration-manager"></a>Selección de los métodos de detección que se usarán para System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Para usar la detección de System Center Configuration Manager de forma correcta y eficaz, debe tener en cuenta qué métodos usar y en qué sitios ejecutarlos.  

 Debido a que la detección puede generar un gran volumen de tráfico de red y los registros de datos de detección (DDR) resultantes pueden conllevar un uso considerable de los recursos de la CPU durante el procesamiento, use solo aquellos métodos de detección que necesite para lograr sus objetivos. Podría comenzar usando solo uno o dos métodos de detección y luego más tarde habilitar métodos adicionales de una manera controlada para ampliar el nivel de detección en su entorno. La información de este tema puede ayudarle a tomar decisiones informadas.  

 Para obtener información sobre los diferentes métodos de detección, consulte [Acerca de los métodos de detección para System Center Configuration Manager](../../../../core/servers/deploy/configure/about-discovery-methods.md).  

## <a name="select-methods-to-discover-different-things"></a>Seleccionar métodos para detectar cosas diferentes  
 Para detectar posibles recursos de usuario o equipos cliente de Configuration Manager, debe habilitar los métodos de detección adecuados. Puede utilizar diferentes combinaciones de métodos de detección para localizar recursos diferentes y detectar información adicional sobre dichos recursos. Los métodos de detección que use determinan el tipo de recursos detectados y los agentes y servicios de Configuration Manager que se usan en el proceso de detección. También determinan el tipo de información acerca de los recursos que puede detectar.  

 **Detectar equipos**   
Cuando desee detectar equipos, puede usar la detección de redes o la detección de sistemas de Active Directory.  

 Como ejemplo, si quiere detectar recursos que puedan instalar el cliente de Configuration Manager antes de usar la instalación de inserción de cliente, puede ejecutar la detección de sistemas de Active Directory. Como alternativa, podría ejecutar la detección de redes y utilizar sus opciones para detectar el sistema operativo de los recursos (necesario para usar después la instalación de inserción de cliente). Sin embargo, mediante el uso de la detección de sistemas de Active Directory, no solo se detecta el recurso, sino que se detecta información básica y se puede detectar información ampliada en Servicios de dominio de Active Directory. Esta información puede ser útil en la creación de consultas complejas y recopilaciones que se utilizarán para la asignación de la configuración del cliente o la distribución de contenido. La detección de redes, por otro lado, proporciona información acerca de la tipología de red que no puede adquirir con otros métodos de detección, pero no proporciona información acerca del entorno de Active Directory.  

 También es posible utilizar únicamente la detección de latidos para forzar la detección de clientes que se instalaron por métodos distintos de la instalación de inserción de cliente. En cambio, a diferencia de otros métodos de detección, la detección de latidos no puede detectar equipos que no tengan un cliente de Configuration Manager activo y devuelve información limitada. Está destinado a mantener un registro de la base de datos existente y no a ser la base de ese registro. La información presentada por la detección de latidos podría no ser suficiente para crear consultas complejas o recopilaciones.  

 Si utiliza la detección de grupos de Active Directory para detectar la pertenencia a un grupo específico, puede detectar información del equipo o sistema limitada. Esto no sustituye a una detección completa de equipos, pero puede proporcionar información básica. Esta información básica no es suficiente para la instalación de inserción de cliente.  

 **Detectar usuarios**   
Cuando desee obtener información sobre los usuarios, puede usar la detección de usuarios de Active Directory. Similar a la detección de sistemas de Active Directory, este método detecta los usuarios de Active Directory e incluye información básica además de información ampliada de Active Directory. Puede utilizar esta información para crear consultas complejas y recopilaciones similares a las de los equipos.  

 **Detectar información de grupo**   
Cuando desee obtener información sobre grupos y pertenencias a grupos, use la detección de grupos de Active Directory. Este método de detección crea registros de recursos para los grupos de seguridad.  

 Puede utilizar este método para buscar un grupo específico de Active Directory para identificar a los miembros de ese grupo, además de los grupos anidados dentro de ese grupo. También puede utilizar este método para buscar una ubicación de Active Directory para grupos y buscar de forma recursiva en cada contenedor secundario de esa ubicación en Servicios de dominio de Active Directory.  

 Este método de detección también puede buscar la pertenencia a grupos de distribución. Esto puede identificar las relaciones de grupo de usuarios y equipos.  

 Cuando se detecta un grupo, también puede detectar información limitada sobre sus miembros. Esto no sustituye la detección de usuarios o de sistemas de Active Directory y suele ser insuficiente para crear consultas complejas y recopilaciones o para servir como base de una instalación de inserción de cliente.  

 **Detectar infraestructura**   
Hay dos métodos que puede usar para detectar la infraestructura de red: la detección de redes y la detección de bosques de Active Directory.  

 Puede utilizar la detección de bosques de Active Directory para buscar un bosque de Active Directory para obtener información acerca de subredes y configuraciones de sitios de Active Directory. Después, estas configuraciones se pueden introducir de forma automática en Configuration Manager como ubicaciones de límite.  

 Cuando desee detectar la topología de red, utilice la detección de redes. Mientras otros métodos de detección devuelven información relacionada con Active Directory Domain Services y pueden identificar la ubicación de red actual de un cliente, no proporcionan información de infraestructura basada en las subredes y la topología del enrutador de la red.  

##  <a name="a-namebkmkshareda-discovery-data-is-shared-between-sites"></a><a name="bkmk_shared"></a> Los datos de detección se comparten entre los sitios  
 Después de que Configuration Manager agregue los datos de detección a una base de datos, estos se comparten rápidamente entre todos los sitios de la jerarquía. Ya que detectar la misma información en varios sitios de la jerarquía no aporta normalmente ningún beneficio, es conveniente configurar una sola instancia de cada método de detección usado para que se ejecute en un único sitio, en lugar de ejecutar varias instancias de un único método en diferentes sitios.  

 En cambio, en algunos entornos, podría resultar útil asignar el mismo método de detección para que se ejecute en varios sitios, cada uno con una programación y una configuración independientes. Esto se debe a que las configuraciones para ejecutar un método de detección son específicas de un único sitio. Esto le permite ejecutar la detección en un sitio y después compartir los resultados con otros sitios o usar el mismo método en dos sitios diferentes en los que la detección se ejecuta en un recurso local y no intenta detectar información de ubicaciones a través de una WAN.  Por ejemplo, esto suele resultar útil al usar la Detección de redes, en la que dirige cada sitio para detectar su red local en lugar de intentar ejecutar una detección de todas las ubicaciones de red a través de una WAN. Si se configuran varias instancias de los mismos métodos de detección para que se ejecuten en diferentes sitios, es necesario planificar detenidamente la configuración de cada uno para evitar que dos o más sitios detecten los mismos recursos de la red o Active Directory. La detección de las mismas ubicaciones y los mismos recursos en varios sitios puede consumir ancho de banda de red adicional, además de crear registros de datos de detección (DDR) duplicados de recursos que no aportan ningún valor, pero que también deben procesar los servidores del sitio.  

 En la tabla siguiente se identifica en qué sitios se pueden configurar los diferentes métodos de detección.  

|Método de detección|Ubicaciones admitidas|  
|----------------------|-------------------------|  
|Detección de bosques de Active Directory|Sitio de administración central<br /><br /> Sitio primario|  
|Detección de grupos de Active Directory|Sitio primario|  
|Detección de sistemas de Active Directory|Sitio primario|  
|Detección de usuario de Active Directory|Sitio primario|  
|Detección de latidos<sup>1</sup>|Sitio primario|  
|Detección de redes|Sitio primario<br /><br /> Sitio secundario|  

 <sup>1</sup> Los sitios secundarios no pueden configurar el método de detección de latidos, pero pueden recibir el DDR de latido de un cliente.  

 Cuando los sitios secundarios ejecutan la detección de redes o reciben DDR de detección de latidos, transfieren el DDR mediante la replicación basada en archivos a su sitio primario principal. Esto se debe a que solo los sitios primarios y los sitios de administración central pueden procesar los DDR. Para obtener más información sobre cómo se procesan los DDR, consulte [Acerca de los registros de datos de detección](../../../../core/servers/deploy/configure/run-discovery.md#BKMK_DDRs).  

## <a name="considerations-for-different-discovery-methods"></a>Consideraciones de los diferentes métodos de detección  
 Ya que todos los servidores de sitio y entornos de red son diferentes, limite las configuraciones de detección iniciales y después supervise de cerca la capacidad de cada servidor de sitio para procesar los datos de detección que se han generado.  

-   Cuando se utiliza un método de detección de Active Directory para sistemas, usuarios o grupos:  

    -   Ejecute la detección en un sitio que tiene una conexión de red rápida con los controladores de dominio.  

    -   Tenga en cuenta la topología de replicación de Active Directory para garantizar que la detección puede tener acceso a la información más reciente.  

    -   Tenga en cuenta el ámbito de la configuración de detección y limite la detección únicamente a las ubicaciones y los grupos de Active Directory que se deban detectar.  

-   Si utiliza la detección de redes:  

    -   Utilice una configuración inicial limitada para identificar la topología de la red.  

    -   Después de identificar la topología de la red, configure la detección de redes para ejecutarse en sitios específicos que son fundamentales para las áreas de la red que desea detectar plenamente.  

-   Habida cuenta de que la detección de latidos no se ejecuta en un sitio específico, no es necesario considerarla en la planificación general de dónde ejecutar la detección.  

-   Como cada servidor de sitio y entorno de red son diferentes, cabe limitar las configuraciones de detección inicial y supervisar de cerca la capacidad de cada servidor de sitio para procesar los datos de detección que se han generado.  

##  <a name="a-namebkmkbesta-best-practices-for-discovery"></a><a name="bkmk_best"></a> Procedimientos recomendados para la detección  
 **Ejecución de la detección de sistemas de Active Directory y la detección de usuarios de Active Directory antes de ejecutar la detección de grupos de Active Directory:**  

 Cuando la detección de grupos de Active Directory identifica un usuario o equipo no detectado previamente como miembro de un grupo, trata de detectar los detalles básicos del usuario o el equipo. Habida cuenta de que la detección de grupos de Active Directory no está optimizada para este tipo de detección, este proceso puede dar lugar a que la detección de grupos de Active Directory se ejecute con lentitud. Además, la detección de grupos de Active Directory identifica sólo los detalles básicos sobre los usuarios y equipos que detecta, y no crea un registro de detección completo del usuario o el equipo. Al ejecutar la detección de sistemas de Active Directory y la detección de usuarios de Active Directory, se encontrarán disponibles también los atributos adicionales de Active Directory para cada tipo de objeto y, como resultado, la detección de grupos de Active Directory se ejecuta de manera más eficaz.  

 **Al configurar la detección de grupos de Active Directory, especifique solo los grupos que usa con Configuration Manager:**  

 Para controlar el uso que la detección de grupos de Active Directory hace de los recursos, especifique solo los grupos que use con Configuration Manager. Esto se debe a que la detección de grupos de Active Directory busca usuarios, equipos y grupos anidados de forma recursiva en cada grupo que detecta. La búsqueda de cada grupo anidado puede ampliar el ámbito de la detección de grupos de Active Directory y reducir el rendimiento. Además, al configurar la detección de diferencias para la detección de grupos de Active Directory, el método de detección supervisa los cambios de cada grupo. Esto reduce aún más el rendimiento cuando el método debe buscar grupos innecesarios.  

 **Configuración de métodos de detección con un intervalo más largo entre la detección completa y un período más frecuente de detección de diferencias:**  

 Habida cuenta de que la detección de diferencias consume menos recursos que un ciclo de detección completa, además de poder identificar recursos nuevos o modificados en Active Directory, al utilizar la detección de diferencias se puede reducir la frecuencia de los ciclos de detección completa a una ejecución por semana o incluso menos. La detección de diferencias para la detección de sistemas de Active Directory, la detección de usuarios de Active Directory y la detección de grupos de Active Directory identifica casi todos los cambios de los objetos de Active Directory y puede mantener datos de detección precisos sobre los recursos.  

 **Ejecución de métodos de detección de Active Directory en el sitio primario que tiene una ubicación de red más cercana al controlador de dominio de Active Directory:**  

 Para mejorar el rendimiento de la detección de Active Directory, se recomienda ejecutar la detección en un sitio primario que tiene una conexión de red rápida a los controladores de dominio. Si se ejecuta el mismo método de detección de Active Directory en varios sitios, se recomienda configurar cada método de detección para evitar superposiciones. A diferencia de las versiones anteriores de Configuration Manager, los datos de detección se comparten entre los sitios. Por lo tanto, no es necesario detectar la misma información en varios sitios. Para obtener más información, consulte [Los datos de detección se comparten entre los sitios](../../../../core/servers/deploy/configure/select-discovery-methods-to-use.md#bkmk_shared).  

 **Ejecución de la detección de bosques de Active Directory en un solo sitio cuando planee crear de forma automática los límites de los datos de detección:**  

 Si se ejecuta la detección de bosques de Active Directory en más de un sitio de una jerarquía, se recomienda habilitar sólo las opciones para crear automáticamente los límites en un solo sitio. Esto se debe a que, cuando la detección de bosques de Active Directory se ejecuta en cada sitio y crea límites, Configuration Manager no puede combinar esos límites en un objeto de un solo límite. Al configurar la detección de bosques de Active Directory para crear de forma automática los límites en varios sitios, el resultado pueden ser objetos con límites duplicados en la consola de Configuration Manager.  



<!--HONumber=Dec16_HO3-->


