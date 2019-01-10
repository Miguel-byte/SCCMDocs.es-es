---
title: Versión preliminar de UUP
titleSuffix: Configuration Manager
description: Instrucciones para la versión preliminar de la integración de UUP
ms.date: 01/04/2018
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 0b0da585-0096-410b-8035-6b7a312f37f5
author: aczechowski
ms.author: aaroncz
manager: dougeby
robots: noindex,nofollow
ms.openlocfilehash: cfc83f4d076a05ea1847c0d073bd824ad10aa731
ms.sourcegitcommit: 1bf26b83fa7da637d299a21e1d3bc61f2d7d8c10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/07/2019
ms.locfileid: "54060389"
---
# <a name="uup-private-preview-instructions"></a>Instrucciones de la versión preliminar privada de UUP

> [!Note]  
> Esta información está relacionada con una característica en versión preliminar que se puede modificar sustancialmente antes de su lanzamiento comercial. Microsoft no ofrece ninguna garantía, expresa o implícita, con respecto a la información aquí proporcionada.  

## <a name="benefits"></a>Ventajas

### <a name="feature-updates"></a>Actualizaciones de características

Las actualizaciones de características con la Plataforma de actualización unificada de Windows 10 (UUP) están diseñadas para solucionar varios problemas que los clientes tienen con el mantenimiento en la actualidad. Pruebe las actualizaciones de características de UUP, incluida:

- Actualización directa al nivel de cumplimiento de seguridad más reciente; ya no tendrá que instalar las actualizaciones de seguridad inmediatamente después de actualizar para que sea compatible. Cada mes se publicará una nueva actualización de características para incluir la actualización de seguridad acumulativa más reciente. No tendrá que volver a descargar ni distribuir la mayoría del contenido de actualización de características cada mes, solo el componente de actualización de seguridad, que también se comparte con la actualización acumulativa.

- Todas las características bajo demanda (FOD) y los paquetes de idioma se deben conservar y no se pierden durante el proceso de actualización.

- Las actualizaciones de características con UUP admiten archivos de instalación rápida, lo que permite a los clientes reducir la cantidad de contenido que deben descargar.

Para obtener más información sobre la UUP, consulte la entrada de blog de Windows [An update on our Unified Update Platform (UUP)](https://blogs.windows.com/windowsexperience/2017/03/02/an-update-on-our-unified-update-platform-uup/) (Actualización de nuestra Plataforma de actualización unificada).


### <a name="cumulative-updates"></a>Actualizaciones acumulativas

Las actualizaciones acumulativas con UUP permiten que el contenido para los paquetes de idioma y FOD se distribuya sin conexión para que los usuarios finales las consigan a petición sin necesidad de ir a Internet ni de que los administradores tengan que realizar tediosos esfuerzos de almacenamiento provisional.



## <a name="set-up-instructions"></a>Instrucciones de configuración

### <a name="1-send-your-wsus-id-to-your-uup-preview-contact-at-microsoft"></a>1. Envíe el identificador de WSUS a su contacto de la versión preliminar de UUP en Microsoft.

Para participar en la versión preliminar privada de UUP, debe compartir su identificador de WSUS con Microsoft para que su entorno se pueda incluir en la lista de permitidos de la versión preliminar. Sin este identificador, no podrá ver las actualizaciones de UUP hasta que la versión preliminar sea pública.

Para recuperar el identificador de WSUS:

```PowerShell
$server = Get-WsusServer
$config = $server.GetConfiguration()
$config.ServerId
```

### <a name="2-update-configmgr-to-a-supported-version"></a>2. Actualice Configuration Manager a una versión admitida.

Si va a sincronizar archivos de instalación rápida en su entorno, necesitará la rama actual de Configuration Manager, 1810, para los entornos de producción, o bien la rama de versión preliminar técnica, 1812, para entornos de laboratorio.

De lo contario, también necesitará la revisión KB4482615 de Configuration Manager, 1810, para los entornos de producción, o bien la rama de versión preliminar técnica, 1812, para los de laboratorio.


#### <a name="configmgr-1810-uup-hotfix-kb4482615"></a>Revisión de ConfigMgr 1810 de la UUP (KB4482615)

> [!Important]  
> El siguiente proceso se aplica a los sitios de la rama actual actualizados a la versión 1810, disponible de forma general después del 19 de diciembre de 2018.
>
> Si optó por recibir la actualización 1810 ejecutando un script de PowerShell a finales de noviembre o principios de diciembre de 2018, la revisión aún no estará disponible. 


1. Actualización del sitio

    1. Descargue la revisión KB4482615 del [Centro de descarga de Microsoft]<!--(https://download.microsoft.com/download/0/9/0/09081E12-A2CF-40B6-82D8-9B8914A1C2D3/KB4482615/CM1810-KB4482615.ConfigMgr.Update.exe)-->. Esta revisión permite usar la UUP en escenarios que no sean rápidos.  

    2. [Uso de la herramienta de registro de actualizaciones para importar revisiones](/sccm/core/servers/manage/use-the-update-registration-tool-to-import-hotfixes)  

2. Actualice los clientes.  

    - Para simplificar el proceso, considere la posibilidad de usar la actualización automática del cliente. Para obtener más información, vea [Actualizar clientes](/sccm/core/clients/manage/upgrade/upgrade-clients#automatic-client-upgrade).  

    - Todos los clientes a los que destine las actualizaciones de UUP se deben actualizar para evitar **la descarga innecesaria de unos 6 GB** de contenido no usado al cliente.


#### <a name="1812-technical-preview"></a>Technical Preview 1812
En escenarios de UUP admitidos, Technical Preview 1812 es equivalente a la revisión de UUP de Configuration Manager 1810 (KB4482615).

El único aspecto a tener en cuenta es que la actualización de cliente de Technical Preview 1812 se separa de TP 1810.1 o TP 1811. Para solucionar este problema, tendrá que desinstalar los clientes TP 1811 y TP 1810.1, y después instalar el cliente TP 1812 de forma limpia. Todos los clientes a los que destine las actualizaciones de UUP deben estar en Technical Preview 1812 (o una versión posterior) para evitar **la descarga innecesaria de unos 6 GB** de contenido no usado al cliente.


### <a name="3-update-windows-clients-to-supported-versions"></a>3. Actualizar los clientes de Windows a las versiones compatibles

#### <a name="for-express-installation-file-sync"></a>Para la sincronización de archivos de instalación rápida
Para contenido rápido, las versiones de Windows admitidas incluyen las siguientes:

- **Windows 10, versión 1709** con [KB4338825](https://support.microsoft.com/help/4338825) (actualización de seguridad acumulativa de julio de 2017) o posterior  

- **Windows 10, versión 1803** con [KB4284835](https://support.microsoft.com/help/4284835) (actualización de seguridad acumulativa de junio de 2017) o posterior  

- **Windows 10, versión 1809** con la actualización acumulativa que no es de seguridad de enero, pendiente de publicación (o la siguiente actualización de seguridad acumulativa de febrero) o posterior

#### <a name="for-non-express-installation-file-sync"></a>Para la sincronización de archivos de instalación que no son rápidos
Para el contenido que no es rápido, se debe aplicar una revisión adicional. Esta ruta de acceso empezó a estar disponible en un formato no acumulativo en el catálogo 12/20 y estará disponible en el formato acumulativo normal a finales de enero.

**Windows 10, versión 1709** y **Windows 10, versión 1803** con:
- Diciembre-Enero: los clientes deben tener un nivel base de actualización acumulativa además de la actualización no acumulativa  
    - Actualización acumulativa  
        - 1709: [KB4338825](https://support.microsoft.com/help/4338825) (actualización de seguridad acumulativa de julio de 2017) hasta la actualización acumulativa de seguridad de enero de 2019, inclusive  
        - 1803: [KB4284835](https://support.microsoft.com/help/4284835) (actualización de seguridad acumulativa de junio de 2017) hasta la actualización acumulativa de seguridad de enero de 2019, inclusive  
    - Actualización no acumulativa: esta actualización solo está disponible en el catálogo y no se sincroniza directamente con WSUS. Para importar la actualización al entorno con el fin de implementarla, vea [Importar actualizaciones desde el catálogo de Microsoft Update](/sccm/sum/get-started/synchronize-software-updates#import-updates-from-the-microsoft-update-catalog).  
        - 1709: [KB4483530](https://support.microsoft.com/help/4483530)  
        - 1803: [KB4483541](https://support.microsoft.com/help/4483541)  
- Febrero y meses posteriores: para la actualización acumulativa, solo la actualización acumulativa que no es de seguridad de enero, pendiente de publicación (o la siguiente actualización de seguridad acumulativa de febrero) o posterior   

**Windows 10, versión 1809** con la actualización acumulativa que no es de seguridad de enero, pendiente de publicación (o la siguiente actualización de seguridad acumulativa de febrero) o posterior


### <a name="4-enable-express-installation-on-clients-in-client-settings"></a>4. Habilitar la instalación rápida en los clientes en la configuración de cliente

Para las actualizaciones UUP, se debe establecer la configuración de cliente para habilitar la instalación rápida, con independencia de que el contenido rápido se sincronice o no. Esta configuración permite que Configuration Manager deje al Agente de Windows Update (WUA) determinar el contenido necesario para descargar en los clientes, en lugar de que Configuration Manager tenga que descargar todo el contenido asociado a la actualización de UUP. Esta configuración es necesaria incluso para los escenarios que no son rápidos porque hay contenido opcional de FOD y paquetes de idioma, lo que genera una cantidad no significativa de datos adicionales que no son necesarios para todos los clientes asociados con la actualización.

La habilitación de esta configuración no afectará a las descargas de contenido del servidor, solo a los comportamientos de descarga de cliente. Es importante que las versiones de cliente de Configuration Manager y Windows estén articuladas antes de habilitar esta opción si todavía no la ha habilitado, ya que esas versiones corregirán algunos problemas de compatibilidad con la aprobación de actualizaciones directamente en WSUS y permitirán que Configuration Manager use este canal para las actualizaciones de UUP incluso si el contenido rápido no se sincroniza.

Para habilitar la instalación rápida en los clientes:

1. En la consola de Configuration Manager, vaya a **Administración** \ **Configuración de cliente**.  

2. Abra las propiedades de la configuración de cliente que quiera usar o cree una para la implementación según corresponda.  

3. En el grupo **Actualizaciones de software**, establezca **Habilitar instalación de archivos de instalación rápida en los clientes** en **Sí**

![Resaltado de la configuración de cliente en el grupo Actualizaciones de software](../media/uup-preview-client-settings.png)


### <a name="5-make-sure-your-adrs-are-set-as-desired"></a>5. Asegurarse de que las ADR se establecen según corresponda 

Antes de habilitar la sincronización de las actualizaciones de UUP, tenga en cuenta sus reglas de implementación automática (ADR) y cualquier otra infraestructura de actualización que tenga instalada. Si no quiere que estas actualizaciones se implementen de forma automática como parte de las ADR existentes y los planes de mantenimiento, asegúrese de actualizar las ADR para filtrarlas. Vea [Cómo buscar actualizaciones de UUP sincronizadas](#how-to-find-synced-uup-updates). Los planes de mantenimiento existentes no implementarán UUP de forma predeterminada, pero puede actualizarlos para cambiar este comportamiento.

Considere también si estas actualizaciones afectarán a alguno de los informes de cumplimiento u otra infraestructura; para ello, sincronícelos y realice las modificaciones deseadas con antelación. Por ejemplo, si mide el cumplimiento de todos los productos, ahora verá la actualización acumulativa de Windows 10 de UUP y no UUP como no compatible o compatible, con lo que los números estarán distorsionados.



## <a name="enable-uup-and-start-testing"></a>Habilitar UUP e iniciar las pruebas

### <a name="select-products-and-classifications-to-sync"></a>Selección de productos y clasificaciones para sincronizar

Cuando esté listo para iniciar la sincronización de las actualizaciones UUP y probarlas, y desde Microsoft se le haya notificado que se ha habilitado su instancia de WSUS para ver el proyecto piloto, habilite los productos nuevos.

1. [Sincronizar actualizaciones de software](/sccm/sum/get-started/synchronize-software-updates) para permitir que se rellenen los productos nuevos  

2. En la consola de Configuration Manager, vaya a **Administración** \ **Configuración de sitio** \ **Sitios**.  

3. Seleccione el sitio de nivel superior, que será un sitio de administración central (CAS) o uno primario independiente.  

4. Abra **Configurar componentes de sitio** \ **Punto de actualización de software**  

5. En la pestaña **Productos**, una vez que el servidor WSUS se haya agregado a la versión preliminar, deberían aparecer dos productos nuevos. Estos productos contienen el contenido de la versión preliminar de UUP.  

    - **Piloto UUP de Windows 10**: actualizaciones de UUP para estaciones de trabajo de Windows  
    - **UUP de Windows Server 2016**: actualizaciones de UUP para Windows Server  

6. En la pestaña **Clasificaciones**, asegúrese de seleccionar:  

    - **Actualizaciones de seguridad**: Para ver las actualizaciones acumulativas de UUP  
    - **Actualizaciones**: Para ver las actualizaciones de características de UUP  

7. Sincronizar actualizaciones de software para ver las nuevas actualizaciones de UUP


### <a name="how-to-find-synced-uup-updates"></a>Cómo buscar actualizaciones de UUP sincronizadas

Después de sincronizar las actualizaciones UUP en el entorno, querrá buscarlas para realizar pruebas. Hay dos métodos sencillos para encontrar las actualizaciones de versión preliminar en la consola de Configuration Manager.

- Como estas actualizaciones de versión preliminar se encuentran en productos independientes, siempre puede usar el producto para filtrarlas o buscarlas. El filtro de producto se ha agregado a los planes de mantenimiento para que pueda seleccionar si quiere implementar actualizaciones de características de UUP o que no sean de UUP.  

- Hay una nueva columna opcional, **Etiqueta**, en los nodos **Todas las actualizaciones de software** y **Todas las actualizaciones de Windows 10** de la Biblioteca de software, así como un filtro de los ADR. Este campo se establece en **UUP** para las actualizaciones de UUP y está en blanco para las que no son de UUP.  


### <a name="updates-available-during-preview"></a>Actualizaciones disponibles durante la versión preliminar

- Actualizaciones acumulativas de Windows 10 1709
    - Actualización de seguridad de diciembre (11/12)
    - Actualización de seguridad de enero (8/1)
    - Actualización que no es de seguridad de enero (15/1)
    - Actualización de seguridad de febrero (12/2)  

- Actualizaciones acumulativas de Windows 10 1803
    - Actualización de seguridad de diciembre (11/12)
    - Actualización de seguridad de enero (8/1)
    - Actualización que no es de seguridad de enero (15/1)
    - Actualización de seguridad de febrero (12/2)  

- Actualizaciones acumulativas de Windows 10 1809
    - Actualización de seguridad de febrero (12/2)  

- Actualizaciones de características de Windows 10 1803 (desde 1709 o 1803)   
    - Cumplimiento de actualizaciones de seguridad de diciembre (11/12)
    - Cumplimiento de actualizaciones de seguridad de enero (8/1)
    - Cumplimiento de actualizaciones de seguridad de febrero (12/2)  

- Actualizaciones de características de Windows 10 1809 (desde 1709 o 1803)
    - Cumplimiento de actualizaciones de seguridad (11/12) de diciembre
    - Cumplimiento de actualizaciones de seguridad (8/1) de enero
    - Cumplimiento de actualizaciones de seguridad de febrero (12/2)  

Si es necesario, las actualizaciones de seguridad de marzo y futuras se seguirán publicando en todas estas áreas siempre y cuando UUP siga en versión preliminar (privada o pública). Cuando se complete la versión preliminar, en producción solo se admitirán las actualizaciones acumulativas y las actualizaciones de características de Windows 10, versión 1809 (a partir de Windows 10, versión 1803).


### <a name="scenarios-to-try"></a>Escenarios para pruebas

#### <a name="feature-updates"></a>Actualizaciones de características
- Actualización directa al nivel de cumplimiento de seguridad elegido  

- Actualización con los paquetes de idioma y FOD instalados antes de la actualización, que se conservan durante la actualización  

- Opcionalmente, habilite la sincronización de los archivos de instalación rápida para las actualizaciones de características para reducir la cantidad de contenido que debe descargar cada cliente.  

    > [!Note]  
    > Esta ventaja de cliente se obtiene a costa de una mayor descarga y distribución en el servidor, como sucede con los archivos de instalación rápida para las actualizaciones acumulativas.  

#### <a name="cumulative-updates"></a>Actualizaciones acumulativas
Durante la versión preliminar, mantenga el cumplimiento normativo de los clientes con la actualización de tipo de UUP durante varias actualizaciones consecutivas para hacerse una idea de las expectativas en curso.

#### <a name="content"></a>Content
La primera actualización para cada combinación de versión principal (1709, 1803, 1809), arquitectura e idioma parecerá ser grande (en número de archivos y espacio en disco) en comparación con lo que habría visto antes en las actualizaciones que no son de UUP. Este contenido adicional es principalmente para todos los paquetes de idioma y FOD para las actualizaciones acumulativas. Para las actualizaciones de características, especialmente si está habilitado el modo rápido, hay contenido adicional de gran tamaño para esa primera actualización. 

Pero en las actualizaciones posteriores (las acumulativas y las actualizaciones de características mensuales en niveles de cumplimiento superiores), la cantidad de contenido nuevo que se debe descargar y distribuir será mucho menor, ya que todo el contenido de FOD y paquetes de idioma se comparte inteligentemente entre todas las actualizaciones en lugar de volverlo a descargar o distribuir. Durante la versión preliminar, en 1709 y 1803, esta descarga mensual será aproximadamente equivalente al tamaño de las actualizaciones acumulativas que se ven en los escenarios que no son de UUP. Pero en la versión 1809, todo mejora considerablemente ya que la descarga incremental de la actualización acumulativa es mucho menor de mes a mes. 

Si examina el contenido total descargado y distribuido en un período de 12 meses para las actualizaciones que no son rápidas, la versión 1803 sin UUP debería ser aproximadamente equivalente a la versión 1809 con UUP, y después de ese punto crítico, el contenido total descargado y distribuido por toda la duración de la versión es más pequeño en la versión 1809 con UUP. Para las actualizaciones rápidas, el punto crítico aparece igual que con la versión 1809, la modalidad rápida solo es para la actualización acumulativa y no las actualizaciones de características y, por tanto, el gran coste del contenido de servidor de modalidad rápida es una sola vez por versión, en lugar de cada mes.

#### <a name="supported-content-channels"></a>Canales de contenido admitidos
Para la versión preliminar, pruebe con lo que usa en entornos empresariales reales. UUP será compatible con todos los canales de contenido, incluidos:
- Optimización de distribución de Windows
- Caché del mismo nivel de Configuration Manager
- Windows BranchCache
- Implementación sin descargas en el servidor (sin paquete de implementación) para efectuar la descarga directamente desde Microsoft Update; en este caso, se recomienda usarlo junto con la optimización de distribución
- Proveedores de contenido alternativos de terceros

Para obtener más información, vea [Optimización de la distribución de actualizaciones de Windows 10](/sccm/sum/deploy-use/optimize-windows-10-update-delivery).
