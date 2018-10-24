---
title: Utilizar una secuencia de tareas para administrar discos duros virtuales
titleSuffix: Configuration Manager
description: Puede crear y modificar un VHD, agregar aplicaciones y actualizaciones de software, y publicar el VHD en System Center Virtual Machine Manager (VMM) desde Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 0212b023-804a-4f84-b880-7a59cdb49c67
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 49de1e2f94d1016f3c0139ccf534b85a718bf7e0
ms.sourcegitcommit: 3dfe3f4401651afa9dc65d14a8944ae4e4198b3e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/08/2018
ms.locfileid: "48862505"
---
# <a name="use-a-task-sequence-to-manage-virtual-hard-disks-in-system-center-configuration-manager"></a>Utilizar una secuencia de tareas para administrar discos duros virtuales en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*


   > [!NOTE] 
   >  La compatibilidad con esta característica está en desuso en la versión 1710. Para más información, vea [Características en desuso y eliminadas de Configuration Manager](https://docs.microsoft.com/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).

En System Center Configuration Manager, puede administrar discos duros virtuales (VHD) e integrar los VHD que cree en el centro de datos desde la consola de Configuration Manager. De forma específica, puede crear y modificar un VHD, agregar aplicaciones y actualizaciones de software al VHD, y publicar el VHD en System Center Virtual Machine Manager (VMM) desde la consola de Configuration Manager.  

 Use las secciones siguientes para administrar los VHD en Configuration Manager.

## <a name="prerequisites"></a>Requisitos previos  
 Antes de empezar, compruebe los siguientes requisitos previos:  

-   El equipo desde donde se administran los VHD debe ejecutar uno de los siguientes sistemas operativos:  

    -   Windows 8.1 x64  

    -   Windows 8 x64  

    -   Windows Server 2008 R2  

    -   Windows Server 2012  

    -   Windows Server 2012 R2  

-   Debe estar habilitada la virtualización en el BIOS e Hyper-V debe estar instalado en el equipo desde el que ejecuta la consola de Configuration Manager para administrar los VHD. También se recomienda instalar las herramientas de administración de Hyper-V para ayudarlo a probar y solucionar problemas en los discos duros virtuales. Por ejemplo, para supervisar el archivo smsts.log para realizar un seguimiento del progreso de la secuencia de tareas en Hyper-V, debe tener instaladas las herramientas de administración de Hyper-V. Para obtener más información acerca de los requisitos de Hyper-V, consulte [Hyper-V Installation Prerequisites (Requisitos previos para la instalación de Hyper-V)](http://technet.microsoft.com/library/cc731898.aspx).  

    > [!IMPORTANT]  
    >  El proceso para crear un disco duro virtual consume memoria y tiempo de procesador. Por tanto, se recomienda que administre los VHD desde una consola de Configuration Manager que no esté instalada en el servidor de sitio.  

-   El servidor del sitio debe tener permiso de acceso para **Escribir** en la carpeta que contendrá el archivo del VHD cuando administre VHD desde un equipo que sea remoto del servidor del sitio.  

-   Compruebe que dispone de suficiente espacio libre en disco en el equipo desde donde se administran los VHD. Los requisitos de espacio en disco duro del VHD varían según el sistema operativo y las aplicaciones que instale.  

-   Compruebe que dispone de suficiente memoria en el equipo desde donde se administran los VHD. Durante el proceso de crear el VHD, la máquina virtual está configurada para consumir 2 GB de memoria.  

-   Instale la consola de System Center Virtual Machine Manager (VMM) en el equipo desde el que se cargue el VHD a VMM. Puede instalar la consola de VMM en un equipo diferente desde el que administrará los VHD, lo que significa que no necesita tener instalado Hyper-V para importar el VHD a VMM.  

    > [!NOTE]  
    >  Si instala la consola de VMM mientras la consola de Configuration Manager está abierta, debe reiniciar la consola de Configuration Manager una vez finalizada la instalación de la consola de VMM. De lo contrario, Configuration Manager no se conectará correctamente al servidor de administración de VMM para cargar un VHD.  

##  <a name="BKMK_CreateVHDSteps"></a> Pasos para crear un disco duro virtual  
 Para crear un disco duro virtual debe crear una secuencia de tareas que contenga los pasos para crear el disco duro virtual y, a continuación, usar la secuencia de tareas en el Asistente para crear disco duro virtual para crear el disco duro virtual. Las secciones siguientes proporcionan los pasos para crear el disco duro virtual.  

###  <a name="BKMK_CreateTS"></a> Crear una secuencia de tareas para el disco duro virtual  
 Debe crear una secuencia de tareas con los pasos para crear el VHD. En el Asistente para crear secuencia de tareas, cuenta con la opción **Instalar un paquete de imagen existente en un disco duro virtual** , que crea los pasos para crear el VHD. Por ejemplo, el asistente agrega los pasos necesarios siguientes: Reiniciar en Windows PE, Formatear y crear particiones en el disco, Aplicar el sistema operativo y Apagar el equipo. No se puede crear el VHD mientras esté en el sistema operativo completo. Además, Configuration Manager debe esperar hasta que se apague la máquina virtual para poder completar el paquete. De manera predeterminada, el asistente espera 5 minutos antes del cierre de la máquina virtual. Después de crear la secuencia de tareas, puede agregar pasos adicionales en caso necesario.  

> [!IMPORTANT]  
>  El proceso siguiente crea la secuencia de tareas mediante la opción **Instalar un paquete de imagen existente en un disco duro virtual** , que incluye automáticamente los pasos necesarios para crear el VHD correctamente. Si elige usar una secuencia de tareas existente o crear manualmente una secuencia de tareas nueva, asegúrese de agregar el paso Apagar el equipo al final de la secuencia. Sin este paso, no se elimina la máquina virtual temporal y no se completa el proceso de creación del VHD. Sin embargo, el asistente finaliza e indica que todo se ha realizado correctamente.  

 Utilice el procedimiento siguiente para crear la secuencia de tareas para crear el disco duro virtual:  

#### <a name="to-create-the-task-sequence-to-create-the-vhd"></a>Para crear la secuencia de tareas para crear el VHD  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

2.  En el área de trabajo **Biblioteca de software** , expanda **Sistemas operativos**y, a continuación, haga clic en **Secuencias de tareas**.  

3.  En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear secuencia de tareas** para iniciar el Asistente para crear secuencia de tareas.  

4.  En la página **Crear nueva secuencia de tareas** , haga clic en **Instalar un paquete de imagen existente en un disco duro virtual**y, a continuación, haga clic en **Siguiente**.  

5.  En la página **Información de secuencia de tareas** , especifique la siguiente configuración y, a continuación, haga clic en **Siguiente**.  

    -   **Nombre de secuencia de tareas**: especifique un nombre que identifique la secuencia de tareas.  

    -   **Descripción**: especifique una descripción de la secuencia de tareas.  

    -   **Imagen de arranque**: especifique la imagen de arranque que instala el sistema operativo en el equipo de destino. Para más información, vea [Manage boot images (Administrar imágenes de arranque)](../get-started/manage-boot-images.md).  

6.  En la página **Instalar Windows** , especifique la siguiente configuración y, a continuación, haga clic en **Siguiente**.  

    -   **Paquete de imágenes**: especifique el paquete que contiene la imagen de sistema operativo que desea instalar.  

    -   **Imagen**: si el paquete de imágenes de sistema operativo contiene varias imágenes, especifique el índice de la imagen de sistema operativo que desea instalar.  

    -   **Clave de producto**: especifique la clave de producto para el sistema operativo Windows que quiere instalar. Puede especificar claves de licencia por volumen codificadas y claves de producto estándar. Si utiliza una clave de producto no codificada, cada grupo de 5 caracteres debe estar separado por un guión (-). Por ejemplo: *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX*  

    -   **Modo de licencia de servidor**: especifique que la licencia de servidor sea **Por puesto**, **Por servidor**o que no se especifica ninguna licencia. Si la licencia de servidor es **Por servidor**, especifique también el número máximo de conexiones de servidor.  

    -   Especifique cómo administrar la cuenta de administrador que se utiliza cuando se implementa la imagen de sistema operativo.  

        -   **Generar la contraseña de administrador local aleatoriamente y deshabilitar la cuenta en todas las plataformas admitidas (recomendado)**: utilice esta opción para que el asistente cree una contraseña para la cuenta de administrador local aleatoriamente y deshabilite la cuenta cuando se implemente la imagen de sistema operativo.  

        -   **Habilitar la cuenta y especificar la contraseña de administrador local**: utilice esta opción para utilizar una contraseña específica para la cuenta de administrador local en todos los equipos donde se implemente la imagen del sistema operativo.  

7.  En la página **Configurar red** , especifique la siguiente configuración y, a continuación, haga clic en **Siguiente**.  

    -   **Unirse a un grupo de trabajo**: especifique si desea agregar el equipo de destino a un grupo de trabajo.  

    -   **Unirse a un dominio**: especifique si desea agregar el equipo de destino a un dominio. En **Dominio**, especifique el nombre del dominio.  

        > [!IMPORTANT]  
        >  Puede examinar para localizar los dominios del bosque local, pero debe especificar el nombre de dominio para un bosque remoto.  

         También puede especificar una unidad organizativa (OU). Es una configuración opcional que especifica el nombre distintivo LDAP X.500 de la unidad organizativa en la que se va a crear la cuenta de equipo si aún no existe.  

    -   **Cuenta**: especifique el nombre de usuario y la contraseña de la cuenta que tenga permisos para unirse al dominio especificado. Por ejemplo: *dominio\usuario* o *%variable%*.  

8.  En la página **Instalar Configuration Manager**, especifique el paquete de cliente de Configuration Manager que quiere instalar en el equipo de destino y, después, haga clic en **Siguiente**.  

9. En la página **Instalar aplicaciones** , especifique las aplicaciones que desee instalar en el equipo de destino y, a continuación, haga clic en **Siguiente**. Si especifica varias aplicaciones, también puede especificar que la secuencia de tareas continúe si se produce un error en la instalación de una aplicación específica.  

10. Complete el asistente.  

###  <a name="BKMK_CreateVHD"></a> Crear un disco duro virtual  
 Después de crear una secuencia de tareas para el disco duro virtual, use el Asistente para crear disco duro virtual para crear el disco duro virtual.  

> [!IMPORTANT]  
>  Antes de ejecutar este procedimiento, compruebe que cumple los requisitos previos que se enumeran al principio de este tema.  

 Utilice el procedimiento siguiente para crear un VHD.  

#### <a name="to-create-a-vhd"></a>Para crear un disco duro virtual  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

2.  En el área de trabajo **Biblioteca de software** , expanda **Sistemas operativos**y, a continuación, haga clic en **Discos duros virtuales**.  

3.  En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear disco duro virtual** para iniciar el Asistente para crear disco duro virtual.  

    > [!NOTE]  
    >  Hyper-V debe estar instalado en el equipo que ejecuta la consola de Configuration Manager desde el que administra los VHD o la opción **Crear disco duro virtual** no está habilitada. Para obtener más información acerca de los requisitos de Hyper-V, consulte [Hyper-V Installation Prerequisites (Requisitos previos para la instalación de Hyper-V)](http://technet.microsoft.com/library/cc731898.aspx).  

    > [!TIP]  
    >  Para organizar sus VHD, cree una nueva carpeta o seleccione una existente en el nodo **Discos duros virtuales** . A continuación, haga clic en **Crear disco duro virtual** desde la carpeta.  

4.  En la página **General** , especifique las opciones siguientes y, a continuación, haga clic en **Siguiente**.  

    -   **Nombre**: especifique un nombre exclusivo para el VHD.  

    -   **Versión**: especifique un número de versión para el VHD. Se trata de un parámetro opcional.  

    -   **Comentario**: especifique una descripción para el VHD.  

    -   **Ruta de acceso**: especifique la ruta de acceso y el nombre de archivo donde el asistente creará el archivo del VHD.  

         Debe especificar una ruta de red válida en el formato UNC. Por ejemplo: **\\\nombreDeServidor\\<nombreDeRecursoCompartido\>\\<nombreDeArchivo\>.vhd**.  

        > [!WARNING]  
        >  Configuration Manager debe tener permiso de acceso de **Escritura** en la ruta de acceso especificada para crear el VHD. Cuando Configuration Manager no puede tener acceso a la ruta de acceso, registra el error asociado en el archivo distmgr.log en el servidor de sitio.  

5.  En la página **Secuencia de tareas** , especifique la secuencia de tareas indicada en la sección anterior y, a continuación, haga clic en **Siguiente**.  

6.  En la página **Puntos de distribución** , seleccione uno o varios puntos de distribución que contengan el contenido que necesita la secuencia de tareas y, a continuación, haga clic en **Siguiente**.  

7.  En la página **Personalización** , haga clic en **Siguiente**. El proceso para crear el disco duro virtual omite la configuración especificada en esta página.  

8.  Compruebe la configuración y, a continuación, haga clic en **Siguiente**. El asistente crea el disco duro virtual.  

    > [!TIP]  
    >  El tiempo para completar el proceso de creación del VHD puede variar. Aunque el asistente funciona a través de este proceso, puede supervisar los siguientes archivos de registro para realizar un seguimiento del progreso. De forma predeterminada, los registros se ubican en el equipo que ejecuta la consola de Configuration Manager en %*ProgramFiles(x86)*%\Microsoft Configuration Manager\AdminConsole\AdminUILog.  
    >   
    >  -   **CreateTSMedia.log**: el asistente escribe información en este archivo mientras crea el medio de la secuencia de tareas. Revise este archivo de registro para realizar un seguimiento del progreso del asistente al crear los medios independientes.  
    > -   **DeployToVHD.log**: el asistente escribe información en este archivo mientras lleva a cabo el proceso de creación del VHD. Revise este archivo de registro para realizar un seguimiento del progreso del asistente por todos los pasos después de crear los medios independientes.  
    >   
    >  Asimismo, cuando se inicie la instalación del sistema operativo, podrá abrir el Administrador de Hyper-V (si instaló las herramientas de administración de Hyper-V en el equipo) y conectarse a la máquina virtual temporal creada por el asistente para ver la ejecución de la secuencia de tareas. Desde el equipo virtual, puede supervisar el archivo smsts.log para realizar un seguimiento del progreso de la secuencia de tareas. Cuando haya problemas con la finalización de un paso de la secuencia de tareas, puede utilizar este archivo de registro para ayudar a solucionar el problema. El archivo smsts.log se encuentra en x: \windows\temp\smstslog\smsts.log antes de formatear el disco duro, y en c:\\_SMSTaskSequence\Logs\Smstslog\ después de formatearlo. Una vez finalizados los pasos de la secuencia de tareas, la máquina virtual se apaga después de 5 minutos (de forma predeterminada) y se elimina.  

 Después de que Configuration Manager cree el disco duro virtual, este se ubica en el nodo **Discos duros virtuales** en la consola de Configuration Manager, en el nodo **Implementación de sistema operativo** del área de trabajo **Biblioteca de software**.  

> [!NOTE]  
>  Configuration Manager recupera el tamaño del disco duro virtual mediante la conexión a la ubicación de origen del disco duro virtual. Si Configuration Manager no puede acceder al archivo de disco duro virtual, se muestra **0** en la columna **Tamaño (KB)** del disco duro virtual.  

##  <a name="BKMK_ModifyVHDSteps"></a> Pasos para modificar un disco duro virtual existente  
 Para modificar un disco duro virtual, debe crear una secuencia de tareas con los pasos necesarios para modificar el disco duro virtual. A continuación, seleccione la secuencia de tareas en el Asistente para modificar disco duro virtual. El Asistente conecta el disco duro virtual a la máquina virtual, ejecuta la secuencia de tareas en el disco duro virtual y, a continuación, actualiza el archivo de disco duro virtual. Las secciones siguientes proporcionan los pasos para modificar el disco duro virtual.  

###  <a name="BKMK_ModifyTS"></a> Crear una secuencia de tareas para modificar el disco duro virtual  
 Para modificar un disco duro virtual existente, primero debe crear una secuencia de tareas. Elija solo los pasos necesarios para modificar la secuencia de tareas. Por ejemplo, si desea agregar una aplicación al disco duro virtual, cree una secuencia de tareas personalizada y, a continuación, agregue solo el paso Instalar aplicación.  

 Utilice el procedimiento siguiente para crear la secuencia de tareas para modificar el disco duro virtual.  

#### <a name="to-create-a-custom-task-sequence-to-modify-the-vhd"></a>Para crear una secuencia de tareas personalizada para modificar el disco duro virtual  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

2.  En el área de trabajo **Biblioteca de software** , expanda **Sistemas operativos**y, a continuación, haga clic en **Secuencias de tareas**.  

3.  En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear secuencia de tareas** para iniciar el Asistente para crear secuencia de tareas.  

4.  En la página **Crear una nueva secuencia de tareas** , seleccione **Crear una nueva secuencia de tareas personalizada**y, a continuación haga clic en **Siguiente**.  

5.  En la página **Información de secuencia de tareas** , especifique la siguiente configuración y, a continuación, haga clic en **Siguiente**.  

    -   **Nombre de secuencia de tareas**: especifique un nombre que identifique la secuencia de tareas.  

    -   **Descripción**: especifique una descripción de la secuencia de tareas.  

    -   **Imagen de arranque**: especifique la imagen de arranque que instala el sistema operativo en el equipo de destino. Para obtener más información, consulte [Manage boot images](../get-started/manage-boot-images.md) (Administrar imágenes de arranque).  

6.  Complete el asistente.  

 Utilice el procedimiento siguiente para agregar los pasos de secuencia de tareas a la secuencia de tareas personalizada.  

#### <a name="to-add-task-sequence-steps-to-the-custom-task-sequence"></a>Para agregar los pasos de secuencia de tareas a la secuencia de tareas personalizada  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

2.  En el área de trabajo **Biblioteca de software** , expanda **Sistemas operativos**, haga clic en **Secuencias de tareas**y, a continuación, seleccione la secuencia de tareas personalizada que creó en el procedimiento anterior.  

3.  En la pestaña **Inicio** , en el grupo **Secuencia de tareas** , haga clic en **Editar** para iniciar el Editor de secuencia de tareas.  

4.  Agregue los pasos de la secuencia de tareas que desea utilizar para modificar el disco duro virtual.  

5.  Haga clic en **Aceptar** para salir del Editor de secuencia de tareas.  

###  <a name="BKMK_ModifyVHD"></a> Modificar un disco duro virtual  
 Después de crear una secuencia de tareas para el disco duro virtual, use el Asistente para modificar disco duro virtual para modificar el disco duro virtual.  

 Utilice el procedimiento siguiente para modificar un disco duro virtual.  

#### <a name="to-modify-a-vhd"></a>Para modificar un disco duro virtual  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

2.  En el área de trabajo **Biblioteca de software** , expanda **Sistemas operativos**, haga clic en **Discos duros virtuales**y, a continuación, seleccione el disco duro virtual que desea modificar.  

3.  En la pestaña **Inicio** , en el grupo **Disco duro virtual** , haga clic en **Modificar disco duro virtual** para iniciar el Asistente para modificar disco duro virtual.  

    > [!NOTE]  
    >  Hyper-V debe estar instalado en el equipo que ejecuta la consola de Configuration Manager desde el que administra los VHD o la opción **Modificar disco duro virtual** no está habilitada. Para obtener más información acerca de los requisitos de Hyper-V, consulte [Hyper-V Installation Prerequisites (Requisitos previos para la instalación de Hyper-V)](http://technet.microsoft.com/library/cc731898.aspx).  

4.  En la página **General** , confirme las opciones siguientes y, a continuación, haga clic en **Siguiente**.  

    -   **Nombre**: especifica el nombre exclusivo para el VHD.  

    -   **Versión**: especifica el número de versión del VHD. Se trata de un parámetro opcional.  

    -   **Comentario**: especifica la descripción del VHD.  

    -   **Ruta de acceso**: especifica la ruta de acceso y el nombre del archivo de la ubicación del archivo del VHD. Esta configuración no se puede modificar.  

        > [!WARNING]  
        >  Configuration Manager debe tener permiso de acceso de **Escritura** en la ruta de acceso especificada para crear el VHD. Cuando Configuration Manager no puede tener acceso a la ruta de acceso, registra el error asociado en el archivo distmgr.log en el servidor de sitio.  

5.  En la página **Secuencia de tareas** , especifique la secuencia de tareas personalizada que se creó en la sección anterior y, a continuación, haga clic en **Siguiente**.  

6.  En la página **Puntos de distribución** , seleccione uno o varios puntos de distribución que contengan el contenido que necesita la secuencia de tareas y, a continuación, haga clic en **Siguiente**.  

7.  En la página **Personalización** , haga clic en **Siguiente**. El proceso para modificar el disco duro virtual omite la configuración especificada en esta página.  

8.  Compruebe la configuración y, a continuación, haga clic en **Siguiente**. El asistente crea el disco duro virtual modificado.  

    > [!TIP]  
    >  El tiempo para completar el proceso de modificación del disco duro virtual puede variar. Aunque el asistente funciona a través de este proceso, puede supervisar los siguientes archivos de registro para realizar un seguimiento del progreso. De forma predeterminada, los registros se ubican en el equipo que ejecuta la consola de Configuration Manager en %*ProgramFiles(x86)*%\Microsoft Configuration Manager\AdminConsole\AdminUILog.  
    >   
    >  -   **CreateTSMedia.log**: el asistente escribe información en este archivo mientras crea el medio de la secuencia de tareas. Revise este archivo de registro para realizar un seguimiento del progreso del asistente al crear los medios independientes.  
    > -   **DeployToVHD.log**: el asistente escribe información en este archivo mientras lleva a cabo el proceso de modificación del VHD. Revise este archivo de registro para realizar un seguimiento del progreso del asistente por todos los pasos después de crear los medios independientes.  
    >   
    >  Además, podrá abrir el Administrador de Hyper-V (si instaló las herramientas de administración de Hyper-V en el equipo) y conectarse a la máquina virtual temporal creada por el asistente para visualizar la ejecución de la secuencia de tareas. Desde el equipo virtual, puede supervisar el archivo smsts.log para realizar un seguimiento del progreso de la secuencia de tareas. Cuando haya problemas con la finalización de un paso de la secuencia de tareas, puede utilizar este archivo de registro para ayudar a solucionar el problema. El archivo smsts.log se encuentra en x: \windows\temp\smstslog\smsts.log antes de formatear el disco duro, y en c:\\_SMSTaskSequence\Logs\Smstslog\ después de formatearlo. Una vez finalizados los pasos de la secuencia de tareas, la máquina virtual se apaga después de 5 minutos (de forma predeterminada) y se elimina.  

##  <a name="BKMK_ApplyUpdates"></a> Aplicar actualizaciones de software a un disco duro virtual  
 Periódicamente, se publican nuevas actualizaciones de software que son aplicables al sistema operativo de su VHD. Puede aplicar las actualizaciones de software que sean aplicables a un VHD según una programación especificada. En la programación que especifique, Configuration Manager aplica en el VHD las actualizaciones de software que seleccione.  

 La información sobre el VHD se almacena en la base de datos del sitio, incluyendo las actualizaciones de software que se aplicaron en el momento en que creó el VHD. Las actualizaciones de software que se hayan aplicado al VHD desde que se creó inicialmente también se almacenan en la base de datos del sitio. Cuando inicia el asistente para aplicar actualizaciones de software al VHD, el asistente recupera una lista de actualizaciones de software aplicables aún no aplicadas al VHD para que usted seleccione las que desee.  

 Puede seleccionar la opción **Continuar después de un error** para que Configuration Manager siga aplicando las actualizaciones de software aunque se produzca un error al aplicar una o más de las actualizaciones de software seleccionadas.  

> [!NOTE]  
>  Las actualizaciones de software se copian desde la biblioteca de contenido en el servidor del sitio.  

 Utilice el siguiente procedimiento para aplicar las actualizaciones de software al VHD.  

#### <a name="to-apply-software-updates-to-a-vhd"></a>Para aplicar las actualizaciones de software a un disco duro virtual  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

2.  En el área de trabajo **Biblioteca de software** , expanda **Sistemas operativos**y, a continuación, haga clic en **Discos duros virtuales**.  

3.  Seleccione el VHD para aplicar las actualizaciones de software.  

4.  En la pestaña **Inicio** , en el grupo **Disco duro virtual** , haga clic en **Programar actualizaciones** para iniciar el asistente.  

5.  En la página **Elija las actualizaciones** , seleccione las actualizaciones de software que desea aplicar al VHD y, a continuación, haga clic en **Siguiente**.  

6.  En la página **Establecer programación** , especifique la siguiente configuración y, a continuación, haga clic en **Siguiente**.  

    1.  **Programación**: especifique la programación para cuándo aplicar las actualizaciones de software en el VHD.  

    2.  **Continuar después de un error**: seleccione esta opción para continuar con la aplicación de las actualizaciones de software a la imagen incluso cuando se produzca un error.  

7.  En la página **Resumen** , compruebe la información y, a continuación, haga clic en **Siguiente**.  

8.  En la página **Finalización** , compruebe que las actualizaciones de software se aplicaron correctamente a la imagen de sistema operativo.  

##  <a name="BKMK_ImportToVMM"></a> Importar el disco duro virtual en System Center Virtual Machine Manager  
 System Center VMM es una solución de administración para el centro de datos virtualizado que le permite configurar y administrar su host de virtualización, redes y recursos de almacenamiento para poder crear e implementar máquinas virtuales y servicios para las nubes privadas que cree. Después de crear un VHD en Configuration Manager, puede importar y administrar el VHD con VMM.  

> [!TIP]  
>  Antes de cargar un VHD a VMM, compruebe que la consola de VMM se conecta correctamente al servidor de administración de VMM.  

 Utilice el siguiente procedimiento para importar un disco duro virtual en VMM.  

#### <a name="to-import-a-vhd-to-vmm"></a>Para importar un VHD en VMM  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

2.  En el área de trabajo **Biblioteca de software** , expanda **Sistemas operativos**y, a continuación, haga clic en **Discos duros virtuales**.  

3.  En la pestaña **Inicio** , en el grupo **Disco duro virtual** , haga clic en **Cargar a Virtual Machine Manager** para iniciar el Asistente para cargar a Virtual Machine Manager.  

4.  En la página **General** , configure las opciones siguientes y, a continuación, haga clic en **Siguiente**.  

    -   **Nombre del servidor VMM**: especifique el FQDN del equipo donde está instalado el servidor de administración de VMM. El asistente se conecta al servidor de administración de VMM para descargar los recursos compartidos de biblioteca para el servidor.  

    -   **Recurso compartido de biblioteca VMM**: especifique el recurso compartido de biblioteca VMM en la lista desplegable.  

    -   **Usar transferencia sin cifrar**: seleccione esta opción para transferir el archivo del VHD al servidor de administración de VMM sin el uso del cifrado.  

5.  En la página Resumen, compruebe la configuración y, a continuación, complete el asistente. El tiempo que se tarda en cargar el VHD puede variar según el tamaño del archivo del VHD y el ancho de banda de red del servidor de administración de VMM.  
