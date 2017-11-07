---
title: "Seguridad y privacidad de la implementación de sistema operativo"
titleSuffix: Configuration Manager
description: "Obtenga información sobre las prácticas recomendadas de seguridad y privacidad para implementación de sistemas operativos en System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5ee5928f-3d72-4b00-8156-1e0d1030a96c
caps.latest.revision: "6"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: f3286fb0afc5a5023ecd725e74606a585c5fa478
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/12/2017
---
# <a name="security-and-privacy-for-operating-system-deployment-in-system-center-configuration-manager"></a>Seguridad y privacidad para implementación de sistemas operativos en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Este tema contiene información sobre la seguridad y privacidad para la implementación de sistemas operativos en System Center Configuration Manager.  

##  <a name="BKMK_Security_HardwareInventory"></a> Prácticas recomendadas de seguridad para la implementación de sistemas operativos  
 Siga las siguientes prácticas recomendadas de seguridad cuando implemente sistemas operativos con Configuration Manager:  

-   **Implementar controles de acceso para proteger el medio de arranque**  

     Cuando cree medios de arranque, asigne siempre una contraseña para ayudar a proteger el medio. Sin embargo, incluso con una contraseña, solo los archivos que contienen información confidencial se cifran y se pueden sobrescribir todos los archivos.  

     Controle el acceso físico a los medios para impedir que un atacante use ataques criptográficos para obtener el certificado de autenticación del cliente.  

     Para evitar que un cliente instale contenido o una directiva de cliente alterados, se aplica un algoritmo hash al contenido que debe usarse con la directiva original.  Si el hash del contenido produce un error o no se puede comprobar que el contenido coincida con la directiva, el cliente no utilizará el medio de arranque. Solo se aplica un algoritmo hash al contenido, no a la directiva. Sin embargo, la directiva se cifra y se asegura cuando especifica una contraseña, lo que dificulta que un atacante pueda modificarla.  

-   **Usar una ubicación segura al crear los medios para las imágenes de sistema operativo**  

     Si un usuario no autorizado tiene acceso a la ubicación, podrá alterar los archivos creados y podrá usar todo el espacio disponible en disco, por lo que no se podrá crear el medio.  

-   **Proteger los archivos de certificado (.pfx) con una contraseña segura y, si los almacena en la red, asegure el canal de red cuando los importe en Configuration Manager**  

     Cuando necesite una contraseña para importar el certificado de autenticación del cliente que use para medios de arranque, esto ayuda a proteger el certificado de un atacante.  

     Use la firma SMB o IPsec entre la ubicación de red y el servidor de sitio para impedir que un atacante pueda manipular el archivo del certificado.  

-   **Si el certificado de cliente se ve comprometido, bloquee el certificado desde Configuration Manager y revóquelo si se trata de un certificado PKI**  

     Para implementar un sistema operativo mediante el uso de un medio de arranque y un arranque PXE, debe tener un certificado de autenticación del cliente con una clave privada. Si ese certificado se ve comprometido, bloquéelo en el nodo **Certificados** del área de trabajo **Administración** , en el nodo **Seguridad** .  

-   **Cuando el proveedor de SMS esté en un equipo o equipos que no sean el servidor de sitio, asegure el canal de comunicación para proteger las imágenes de arranque**  

     Cuando se modifican las imágenes de arranque y el proveedor de SMS se ejecuta en un servidor que no sea el servidor de sitio, las imágenes de arranque son vulnerables a ataques. Proteja el canal de red entre estos equipos mediante la firma SMB o IPsec.  

-   **Habilitar puntos de distribución para la comunicación de cliente PXE solo en segmentos de red segura**  

     Cuando un cliente envía una solicitud de arranque PXE, no dispone de ninguna manera para asegurarse de que la solicitud es atendida por un punto de distribución habilitado para PXE válido. Este escenario supone los riesgos de seguridad siguientes:  

    -   Un punto de distribución no autorizado que responde a las solicitudes PXE podría proporcionar una imagen modificada a los clientes.  

    -   Un atacante podría lanzar un ataque de tipo "Man in the middle" contra el protocolo TFTP usado por PXE y enviar código malintencionado con los archivos del sistema operativo. También podría crear un cliente no autorizado para enviar solicitudes TFTP directamente al punto de distribución.  

    -   Un atacante podría usar a un cliente malintencionado para lanzar un ataque de denegación de servicio contra el punto de distribución.  

     Utilice una defensa a fondo para proteger los segmentos de red donde los clientes tendrán acceso a los puntos de distribución para solicitudes PXE.  

    > [!WARNING]  
    >  Debido a estos riesgos de seguridad, no habilite un punto de distribución para la comunicación PXE cuando se encuentre en una red que no sea de confianza, como una red perimetral.  

-   **Configurar puntos de distribución habilitados para PXE para responder a solicitudes PXE solo en interfaces de red especificadas**  

     Si permite que el punto de distribución responda a solicitudes PXE en todas las interfaces de red, esta configuración podría exponer el servicio PXE a redes que no son de confianza.  

-   **Solicitar una contraseña para el arranque PXE**  

     Cuando solicite una contraseña para el arranque PXE, esta configuración agregará un nivel de seguridad extra al proceso de arranque PXE, lo que ayuda a evitar que clientes no autorizados se unan a la jerarquía de Configuration Manager.  

-   **No incluir aplicaciones de línea de negocio ni software que contenga datos confidenciales en una imagen que se usara para el arranque PXE o la multidifusión**  

     Debido a los inherentes riesgos de seguridad relacionados con la multidifusión y el arranque PXE, reduzca los riesgos si un equipo no autorizado descarga la imagen de sistema operativo.  

-   **No incluya aplicaciones de línea de negocio ni software que contenga datos confidenciales en paquetes de software que se instalen con variables de secuencias de tareas**  

     Al implementar paquetes de software mediante el uso de variables de secuencias de tareas, se podría instalar software en equipos y para usuarios que no estén autorizados a recibir ese software.  

-   **Al migrar el estado del usuario, se debe proteger el canal de red entre el cliente y el punto de migración de estado mediante la firma SMB o IPsec**  

     Después de la conexión inicial a través de HTTP, los datos de la migración del estado de usuario se transfieren mediante SMB.  Si no se protege el canal de red, un atacante puede leer y modificar estos datos.  

-   **Utilice la versión más reciente de la Herramienta de migración de estado de usuario (USMT) que admita Configuration Manager**  

     La versión más reciente de USMT proporciona mejoras de seguridad y un mayor control al migrar los datos de estado de usuario.  

-   **Eliminar manualmente las carpetas en el punto de migración de estado cuando se retiren**  

     Cuando quite una carpeta del punto de migración de estado en la consola de Configuration Manager en las propiedades del punto de migración de estado, no se elimina la carpeta física. Para impedir la divulgación de los datos de la migración de estado de usuario, debe quitar manualmente el recurso compartido de red y eliminar la carpeta.  

-   **No configurar la directiva de eliminación para eliminar el estado de usuario inmediatamente**  

     Si configura la directiva de eliminación en el punto de migración de estado para quitar inmediatamente los datos marcados para su eliminación y un atacante consigue recuperar los datos de estado de usuario antes de que lo haga un equipo válido, los datos de estado de usuario se eliminarán inmediatamente. Establezca el intervalo **Eliminar después de** para que sea lo suficientemente largo para comprobar la correcta restauración de los datos de estado de usuario.  

-   **Elimine manualmente las asociaciones de equipo cuando la restauración de datos de la migración de estado de usuario se haya comprobado y finalizado**  

     Configuration Manager no quita automáticamente las asociaciones de equipo. Ayude a proteger la identidad de los datos de estado de usuario mediante la eliminación manual de las asociaciones de equipo que ya no son necesarias.  

-   **Hacer manualmente una copia de seguridad de los datos de la migración de estado de usuario en el punto de migración de estado**  

     La copia de seguridad de Configuration Manager no incluye los datos de la migración del estado de usuario.  

-   **No olvide habilitar BitLocker después de instalar el sistema operativo**  

     Si un equipo es compatible con BitLocker, debe deshabilitarlo mediante un paso de secuencia de tareas si desea instalar el sistema operativo desatendido. Configuration Manager no habilita BitLocker después de instalar el sistema operativo, por lo que debe volver a habilitar BitLocker manualmente.  

-   **Implementar controles de acceso para proteger el medio preconfigurado**  

     Controle el acceso físico a los medios para impedir que un atacante use ataques criptográficos para obtener el certificado de autenticación del cliente y datos confidenciales.  

-   **Implementar controles de acceso para proteger el proceso de creación de imágenes del equipo de referencia**  

     Asegúrese de que el equipo de referencia que use para capturar imágenes de sistema operativo esté en un entorno seguro con controles de acceso apropiados para que no se pueda instalar ni incluir accidentalmente software inesperado o malintencionado en la imagen capturada. Cuando capture la imagen, asegúrese de que la ubicación del recurso compartido de archivos de red de destino es segura para que no se pueda manipular la imagen después de capturarla.  

-   **Instalar siempre las actualizaciones de seguridad más recientes en el equipo de referencia**  

     Cuando el equipo de referencia tiene las actualizaciones de seguridad más recientes, se reduce la ventana de vulnerabilidad para los nuevos equipos cuando se inician por primera vez.  

-   **Si debe implementar sistemas operativos en un equipo desconocido, implemente controles de acceso para impedir que equipos no autorizados se conecten a la red**  

     Aunque el aprovisionamiento de equipos desconocidos suponga un método práctico para implementar equipos nuevos a petición, también puede permitir que un atacante se convierta eficientemente en un cliente de confianza en la red. Restrinja el acceso físico a la red y supervise los clientes para detectar equipos no autorizados. Asimismo, los equipos que respondan a la implementación de sistema operativo iniciada por PXE pueden sufrir la destrucción de datos durante la implementación del sistema operativo, lo que podría resultar en una pérdida de disponibilidad de sistemas que se reformatearon de forma inadvertida.  

-   **Habilitar el cifrado de paquetes de multidifusión**  

     Por cada paquete de implementación de sistema operativo, tiene la opción de habilitar el cifrado cuando Configuration Manager transfiera el paquete mediante la multidifusión. Esta configuración ayuda a evitar que los equipos no autorizados se unan a la sesión de multidifusión y ayuda a evitar que los atacantes alteren la transmisión.  

-   **Supervisar los puntos de distribución habilitados para la multidifusión no autorizados**  

     Si algún atacante puede obtener acceso a la red, podrá configurar servidores de multidifusión no autorizados para suplantar la implementación del sistema operativo.  

-   **Al exportar las secuencias de tareas a una ubicación de red, se debe proteger la ubicación y el canal de red**  

     Restrinja quién puede tener acceso a la carpeta de red.  

     Utilice la firma SMB o IPsec entre el servidor de sitio y la ubicación de red para impedir que un atacante manipule la secuencia de tareas exportada.  

-   **Proteja el canal de comunicación al cargar un disco duro virtual a Virtual Machine Manager.**  

     Para evitar la manipulación de los datos cuando se transfieren por la red, utilice la seguridad del protocolo de Internet (IPsec) o el bloque de mensajes de servidor (SMB) entre el equipo que ejecuta la consola de Configuration Manager y el equipo que ejecuta Virtual Machine Manager.  

-   **Si se debe usar la cuenta de ejecución de secuencia de tareas, se deben tomar precauciones de seguridad adicionales**  

     Si utiliza la cuenta de ejecución de secuencia de tareas, tenga en cuenta las siguientes precauciones:  

    -   Utilice una cuenta con los mínimos permisos posibles.  

    -   No utilice la cuenta de acceso de red para esta cuenta.  

    -   Nunca convierta la cuenta en administrador de dominio.  

     Además:  

    -   No configure nunca perfiles móviles para esta cuenta. Cuando se ejecuta la secuencia de tareas, descargará el perfil móvil de la cuenta y se podrá acceder al perfil en el equipo local.  

    -   Limite el ámbito de la cuenta. Por ejemplo, cree diferentes cuentas de ejecución de secuencia de tareas para cada secuencia de tareas, de forma que si una cuenta se ve comprometida, solo se verán comprometidos los equipos cliente a los que ha tenido acceso dicha cuenta. Si la línea de comandos requiere acceso administrativo en el equipo, considere la creación de una cuenta de administrador local únicamente para la cuenta de ejecución de secuencia de tareas en todos los equipos que vayan a ejecutar la secuencia de tareas y elimine la cuenta en cuanto deje de ser necesaria.  

-   **Restringir y controlar los usuarios administrativos a los que se concede el rol de seguridad de Administrador de implementaciones de sistema operativo**  

     Los usuarios administrativos a los que se concede el rol de seguridad de Administrador de implementaciones de sistema operativo pueden crear certificados autofirmados que se podrán usar después para suplantar a un cliente y obtener la directiva de cliente desde Configuration Manager.  

### <a name="security-issues-for-operating-system-deployment"></a>Problemas de seguridad en la implementación de sistemas operativos  
 Aunque la implementación de un sistema operativo puede ser una forma conveniente de implementar las configuraciones y los sistemas operativos más seguros en la red, supone los siguientes riesgos para la seguridad:  

-   Divulgación de información y denegación de servicio  

     Si un atacante puede obtener el control de su infraestructura de Configuration Manager, podría ejecutar cualquier secuencia de tareas, lo que puede incluir el formateo de los discos duros de todos los equipos cliente. Las secuencias de tareas pueden configurarse para contener información confidencial, como las cuentas que tienen permisos para unir el dominio y las claves de licencias por volumen.  

-   Suplantación y elevación de privilegios  

     Las secuencias de tareas pueden unir un equipo al dominio, lo que puede proporcionar acceso autenticado a la red a un equipo no autorizado. Otra consideración de seguridad importante para la implementación de un sistema operativo es proteger el certificado de autenticación del cliente que se utiliza para los medios de secuencias de tareas de arranque y para la implementación del arranque PXE. Cuando capture un certificado de autenticación del cliente, le estará dando a un atacante la oportunidad de obtener la clave privada en el certificado y suplantar luego a un cliente válido en la red.  

     Si un atacante obtiene el certificado del cliente usado para los medios de secuencia de tareas de arranque y la implementación de arranque PXE, este arranque se puede usar para suplantar a un cliente válido en Configuration Manager. En este escenario, el equipo no autorizado podrá descargar la directiva, que puede contener datos confidenciales.  

     Si los clientes usan la cuenta de acceso a la red para obtener acceso a datos en el punto de migración de estado, comparten la misma identidad y podrán obtener acceso a datos de migración de estado de otros clientes que usen la cuenta de acceso de red. Los datos se cifran de manera que solo el cliente original puede leerlos, pero se podrían alterar o eliminar.  

-   La autenticación de cliente en el punto de migración de estado se consigue mediante un token de Configuration Manager emitido por el punto de administración.  

     Además, Configuration Manager no limita o administra la cantidad de datos almacenados en el punto de migración de estado. Un atacante podría llenar el espacio en disco disponible y provocar una denegación de servicio.  

-   Si se usan variables de recopilación, los administradores locales pueden leer información potencialmente confidencial  

     Aunque las variables de recopilación ofrecen un método flexible para implementar sistemas operativos, pueden provocar la divulgación de información.  

##  <a name="BKMK_Privacy_HardwareInventory"></a> Información de privacidad para la implementación de sistemas operativos  
 Además de implementar sistemas operativos en equipos sin sistema operativo, Configuration Manager puede usarse para migrar configuraciones y archivos de los usuarios de un equipo a otro. El administrador configura la información que se va a transferir, como los archivos de datos personales, las opciones de configuración y las cookies del explorador.  

 La información se almacena en un punto de migración de estado y se cifra durante la transmisión y el almacenamiento. El nuevo equipo asociado a la información de estado puede recuperar la información. Si el nuevo equipo pierde la clave para recuperar la información, un administrador de Configuration Manager con el derecho Ver información de recuperación en objetos de instancia de asociación de equipo puede obtener acceso a la información y asociarla a un nuevo equipo. Cuando el nuevo equipo restaura la información de estado, de forma predeterminada, elimina los datos después de un día. Puede configurar cuándo el punto de migración de estado quitará los datos marcados para su eliminación. La información de migración de estado no se almacena en la base de datos del sitio y no se envía a Microsoft.  

 Si usa medios de arranque para implementar imágenes de sistema operativo, use siempre la opción predeterminada para proteger con contraseña el medio de arranque. La contraseña cifra todas las variables almacenadas en la secuencia de tareas, pero la información no almacenada en una variable puede ser vulnerable a la divulgación.  

 La implementación de sistema operativo puede usar secuencias de tareas para realizar varias tareas durante el proceso de implementación, como la instalación de aplicaciones y actualizaciones de software. Al configurar las secuencias de tareas, también debe tener en cuenta las implicaciones de privacidad de la instalación de software.  

 Si carga un disco duro virtual en Virtual Machine Manager sin usar primero Sysprep para limpiar la imagen, el disco duro virtual cargado podría contener datos personales de la imagen original.  

 Configuration Manager no lleva a cabo la implementación de sistemas operativos de manera predetermina: requiere varios pasos de configuración para poder recopilar información de estado de usuario o crear secuencias de tareas o imágenes de arranque.  

 Antes de configurar la implementación de sistema operativo, tenga en cuenta los requisitos de privacidad.  
