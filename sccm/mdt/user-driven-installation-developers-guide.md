---
title: Instalación controlada por el usuario
titleSuffix: Microsoft Deployment Toolkit
description: 'Guía para desarrolladores para la instalación controlada por el usuario de Microsoft Deployment Toolkit 2013. '
ms.date: 09/09/2016
ms.prod: configuration-manager
ms.technology:
- configmgr-osd
ms.topic: article
ms.assetid: a2b3a3a0-7b81-4191-b1f9-c618e59347c3
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 434178f100c32a4188ecf5283066f9332035f761
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2018
---
# <a name="user-driven-installation---developers-guide"></a>Instalación controlada por el usuario: guía para desarrolladores
La instalación controlada por el usuario (UDI) ayuda a simplificar la implementación de sistemas operativos cliente Windows®, como Windows 8.1, en equipos con la característica de implementación de sistema operativo (OSD) de Microsoft® System Center 2012 R2 Configuration Manager. UDI forma parte de Microsoft Deployment Toolkit (MDT).  

## <a name="introduction"></a>Introducción  
 Normalmente, al implementar sistemas operativos mediante la característica OSD, se debe proporcionar toda la información necesaria para implementar el sistema operativo. La información se configura en archivos de configuración o en bases de datos (por ejemplo, el archivo CustomSettings.ini o la base de datos de MDT [MDT DB]). Se deben proporcionar todos los valores de configuración antes de iniciar la implementación.  

 UDI proporciona una interfaz controlada por un asistente que permite proporcionar la información de configuración inmediatamente antes de realizar la implementación. Este comportamiento permite crear secuencias de tareas OSD genéricas y, después, proporcionar información específica del equipo en el momento de la implementación, lo que ofrecer mayor flexibilidad en el proceso de implementación.  

### <a name="target-audience"></a>Público de destino  
 Esta guía está escrita para los desarrolladores que crean páginas del asistente personalizadas para el Asistente para UDI y editores de páginas del asistente personalizados para el diseñador del Asistente para UDI. En esta guía se da por supuesto que está familiarizado con el desarrollo de aplicaciones Windows mediante:  

-   C++, que se usa para crear páginas del asistente personalizadas.  

-   Microsoft .NET Framework, que se usa para crear editores de páginas del asistente personalizados.  

-   Windows Presentation Foundation (WPF), que se usa para crear editores de páginas del asistente personalizados.  

-   Los lenguajes que admite WPF, como C#, C++ o Microsoft Visual Basic® .NET, que se usan para crear editores de páginas del asistente personalizados.  

### <a name="about-this-guide"></a>Acerca de esta guía  
 En esta guía se proporciona la información de referencia necesaria para ayudar a personalizar UDI para la organización. En esta guía no se describen temas administrativos ni operativos, como la instalación de MDT (que incluye UDI), la configuración de UDI para implementar sistemas operativos y aplicaciones o realizar implementaciones mediante el Asistente para UDI. Para obtener más información sobre estos temas, vea los temas de UDI en *Uso de Microsoft Deployment Toolkit*, que se incluye con MDT.  

## <a name="udi-development-overview"></a>Introducción al desarrollo de UDI  
 El desarrollo de UDI permite ampliar las características que proporciona UDI. Por lo general, el desarrollo de UDI es necesario cuando se quiere recopilar información adicional que el proceso de implementación de UDI consume. Esta información adicional se guarda normalmente como variables de secuencia de tareas que los pasos de secuencia de tareas en una secuencia de tareas de UDI de Configuration Manager leen.  

### <a name="udi-architecture"></a>Arquitectura de UDI  
 El objetivo general del desarrollo de UDI consiste en crear páginas del asistente personalizadas que se puedan mostrar en el Asistente para UDI. Mediante la creación de páginas del asistente personalizadas, se pueden ampliar las características existentes de UDI para responder a las necesidades empresariales y los requisitos técnicos de la organización. Una página del asistente personalizada recopila información además o en lugar de las páginas del asistente que proporciona UDI.  

 En la ilustración 1 se muestra la relación entre el diseñador del Asistente para UDI y el Asistente para UDI.  

 ![UDIDevelopersGuide1](media/UDIDevelopersGuide1.jpg "UDIDevelopersGuide1")  
Ilustración 1. Relación entre el Asistente para UDI y el diseñador del Asistente para UDI  

 **Ilustración 1. Relación entre el Asistente para UDI y el diseñador del Asistente para UDI**  

 En un nivel conceptual, el desarrollo de UDI incluye la creación de lo siguiente:  

-   **Páginas del asistente personalizadas**. Las páginas del asistente se muestran en el Asistente para UDI y recopilan la información necesaria para completar el proceso de implementación. Las páginas del asistente se crean mediante C++ en Microsoft Visual Studio®. Las páginas del asistente personalizadas se implementan como archivos DLL que lee el Asistente para UDI. En el kit de desarrollo de software (SDK) de UDI se incluye un ejemplo de cómo crear páginas del asistente personalizadas.  

-   **Editores de páginas del asistente personalizados**. Los editores de páginas del asistente se usan para configurar el comportamiento de la página del asistente personalizada. Los editores de páginas del asistente personalizados se implementan como archivos DLL que lee el diseñador del Asistente para UDI. Los editores de páginas del asistente se crean mediante:  

    -   [WPF](http://msdn.microsoft.com/library/ms754130.aspx) versión 4.0  

    -   [Microsoft Prism](http://compositewpf.codeplex.com/) versión 4.0  

    -   [Microsoft Unity Application Block](http://unity.codeplex.com/) (Unity) versión 2.1  

     MDT incluye todos los ensamblados necesarios para crear un editor de páginas del asistente personalizado para su uso en el diseñador del Asistente para UDI. En el SDK de UDI se incluye un ejemplo de cómo crear editores de páginas del asistente personalizados.  

 Además, el diseñador del Asistente para UDI consume archivos de configuración auxiliares de editor de páginas del asistente. Los archivos de configuración del editor de páginas del asistente se crean para como parte del proceso de creación de las páginas del asistente personalizadas y los editores de páginas del asistente personalizados. El diseñador del Asistente para UDI crea la información XML necesaria en el archivo de configuración del Asistente para UDI y el archivo .app correspondiente.  

### <a name="preparing-the-udi-development-environment"></a>Preparación del entorno de desarrollo de UDI  
 Antes de comenzar a crear páginas del asistente personalizadas y editores de páginas del asistente propios, siga los pasos siguientes para preparar el entorno de desarrollo de UDI:  

1.  Prepare los requisitos previos del entorno de desarrollo de UDI como se describe en [Preparación de los requisitos previos del entorno de desarrollo de UDI](#PrepareUDIDevelopmentEnvironmentPrerequisites).  

2.  Configure el entorno de desarrollo de UDI como se describe en [Configuración del entorno de desarrollo de UDI](#ConfigureUDIDevelopmentEnvironment).  

3.  Compruebe que el entorno de desarrollo de UDI está configurado correctamente como se describe en [Comprobación del entorno de desarrollo de UDI](#VerifyUDIDeploymentEnvironment).  

####  <a name="PrepareUDIDevelopmentEnvironmentPrerequisites"></a> Preparación de los requisitos previos del entorno de desarrollo de UDI  
 Para preparar los requisitos previos del entorno de desarrollo de UDI, siga estos pasos:  

1.  Prepare los requisitos previos de hardware del entorno de desarrollo de UDI como se describe en [Preparación de los requisitos previos de hardware del entorno de desarrollo de UDI](#PrepareUDIDevelopmentEnvironmentHardwarePrerequisites).  

2.  Prepare los requisitos previos de software del entorno de desarrollo de UDI como se describe en [Preparación de los requisitos previos de software del entorno de desarrollo de UDI](#PrepareUDIDevelopmentEnvironmentSoftwarePrerequisites).  

#####  <a name="PrepareUDIDevelopmentEnvironmentHardwarePrerequisites"></a> Preparación de los requisitos previos de hardware del entorno de desarrollo de UDI  
 Los requisitos de hardware del entorno de desarrollo de UDI son los mismos que para la edición de Microsoft Visual Studio 2010 que usa. Para obtener más información sobre estos requisitos, consulte los requisitos del sistema de cada edición en [Productos de Visual Studio 2010](http://www.microsoft.com/visualstudio/products/2010-editions).  

#####  <a name="PrepareUDIDevelopmentEnvironmentSoftwarePrerequisites"></a> Preparación de los requisitos previos de software del entorno de desarrollo de UDI  
 El entorno de desarrollo de UDI tiene los requisitos previos de software siguientes:  

-   Cualquier sistema operativo Windows compatible con Visual Studio 2010 (se recomienda Windows 7 o Windows Server® 2008 R2).  

     Necesitará un sistema operativo Windows que admita la arquitectura de procesador para la que se va a desarrollar. Puede realizar el desarrollo de UDI de 32 bits y 64 bits con un sistema operativo de 64 bits. El desarrollo de UDI de 32 bits solo se realiza en sistemas operativos de 32 bits. Por este motivo, debe usar un sistema operativo de 64 bits.  

    > [!NOTE]
    >  Las versiones de IntelItanium (IA-64) del sistema operativo Windows no son compatibles con los entornos de desarrollo de UDI.  

     Para obtener más información sobre los sistemas operativos compatibles con Visual Studio 2010, vea los requisitos del sistema de cada edición en [Productos de Visual Studio 2010](http://www.microsoft.com/visualstudio/products/2010-editions).  

-   Microsoft .NET Framework, versión 4.0 (requerido por Visual Studio 2010).  

-   El lenguaje C++ (el lenguaje que se usa para la extensión de páginas del Asistente para UDI).  

-   Otros lenguajes compatibles con WPF, como C#, Visual Basic .NET o C++/Common Language Infrastructure, que se usan para ampliar los editores de páginas del asistente del diseñador del Asistente para UDI.  

    > [!NOTE]
    >  El código fuente de ejemplo para los editores de páginas del asistente del diseñador del Asistente para UDI se escribe en C#. Instale el lenguaje C# si quiere usar el código fuente de ejemplo.  

####  <a name="ConfigureUDIDevelopmentEnvironment"></a> Configuración del entorno de desarrollo de UDI  
 Después de que se cumplan los requisitos previos del entorno de desarrollo de UDI, siga estos pasos para configurarlo:  

1.  Instale Visual Studio 2010.  

     Asegúrese de instalar el lenguaje C++ y cualquier otro compatible con WPF.  

    > [!NOTE]
    >  El código fuente de ejemplo para las páginas del editor del diseñador del Asistente para UDI se escribe en C#. Instale el lenguaje C# si quiere usar el código fuente de ejemplo.  

     Para obtener más información sobre la instalación de Visual Studio 2010, vea [Instalar Visual Studio](http://msdn.microsoft.com/library/e2h7fzkw.aspx).  

2.  Instale MDT.  

     Para obtener más información sobre cómo instalar MDT, vea la sección "Installing or Upgrading to MDT" (Instalación o actualización de MDT), en el documento de MDT *Using the Microsoft Deployment Toolkit* (Uso de Microsoft Deployment Toolkit).  

3.  En el Explorador de Windows, cree *carpeta_local* (donde *carpeta_local* es cualquier carpeta de una unidad local en el equipo de desarrollo).  

4.  Copie la carpeta *carpeta_de_instalación*\SDK en *carpeta_local* (donde *carpeta_de_instalación* es la carpeta en la que instaló MDT y *carpeta_local* es cualquier carpeta de una unidad local en el equipo de desarrollo).  

     La carpeta del SDK se copia en otra ubicación porque MDT se instala en la carpeta Archivos de programa, en la que no se puede escribir sin permisos elevados. Copiar la carpeta del SDK en otra ubicación permite modificar los archivos que contiene sin necesidad de permisos elevados.  

5.  Copie la carpeta *carpeta_de_instalación*\Templates\Distribution\Tools en *carpeta_local* (donde *carpeta_de_instalación* es la carpeta en la que instaló MDT y *carpeta_local* es la carpeta que creó anteriormente).  

6.  Cambie el nombre de la carpeta *carpeta_local* \Tools a *carpeta_local*\OSDSetupWizard (donde *carpeta_local* es la carpeta que creó anteriormente en el proceso).  

     Cuando haya completado, la estructura de carpetas bajo *carpeta_local* debería ser similar a la que se muestra en la ilustración 2 (donde *carpeta_local* es la carpeta que creó anteriormente en el proceso y que se muestra como *UDIDevelopment* en la ilustración).  

     ![UDIDevelopersGuide2](media/UDIDevelopersGuide2.jpg "UDIDevelopersGuide2")  
Ilustración 2. Estructura de carpetas para el desarrollo de UDI  

     **Ilustración 2. Estructura de carpetas para el desarrollo de UDI**  

####  <a name="VerifyUDIDeploymentEnvironment"></a> Comprobación del entorno de desarrollo de UDI  
 Después de configurar el entorno de desarrollo de UDI, compruebe que está configurado correctamente asegurándose de que los proyectos de ejemplo se compilan correctamente en Visual Studio 2010.  

 Compruebe que el entorno de desarrollo de UDI está configurado correctamente mediante la determinación de si:  

-   El proyecto SamplePage se compila correctamente como se describe en [Comprobación de la compilación correcta del proyecto SamplePage](#VerifySamplePageProjectBuildsCorrectly).  

-   El proyecto SampleEditor se compila correctamente como se describe en [Comprobación de la compilación correcta del proyecto SampleEditor](#VerifySampleEditorProjectBuildsCorrectly).  

#####  <a name="VerifySamplePageProjectBuildsCorrectly"></a> Comprobación de la compilación correcta del proyecto SamplePage  
 En el proyecto SamplePage se proporciona un ejemplo de cómo crear una página del asistente personalizada para el Asistente para UDI. Para obtener más información sobre el proyecto SamplePage, vea [Revisión de la solución de Visual Studio SamplePage](#ReviewSamplePageVisualStudioSolution).  

 **Para comprobar la compilación correcta del proyecto SamplePage**  

1.  Inicie Visual Studio 2010.  

2.  Abra el proyecto SamplePage.  

     El proyecto SamplePage se encuentra en la carpeta *carpeta_local*\SDK\UDI\SamplePage (donde *carpeta_local* es la carpeta que creó anteriormente en el proceso).  

3.  En Visual Studio 2010, en el Explorador de soluciones, haga clic con el botón derecho en el proyecto SamplePage y, después, haga clic en **Propiedades**.  

     Aparece el cuadro de diálogo **Páginas de propiedades de SamplePage**.  

4.  En el cuadro de diálogo **Páginas de propiedades de SamplePage**, vaya a Propiedades de configuración/Depuración.  

5.  En las propiedades de depuración, en **Configuración**, haga clic en **Todas las configuraciones**.  

6.  En las propiedades de depuración, en **Comando**, escriba **$(DirectorioDestino)\OSDSetupWizard.exe.**  

7.  En las propiedades de depuración, en **Directorio de trabajo**, escriba **$(DirectorioDestino)**.  

8.  En el cuadro de diálogo **Páginas de propiedades de SamplePage**, vaya a Propiedades de configuración/Eventos de compilación/Evento posterior a la compilación.  

9. En las propiedades de evento posterior a la compilación, en **Línea de comandos**, escriba lo siguiente:  

    ```  
    copy /y "$(ProjectDir)..\..\..\..\OSDSetupWizard\x86\*.*" "$(TargetDir)"  
    xcopy /y /i "$(ProjectDir)..\..\..\..\OSDSetupWizard\x86\en-us" "$(TargetDir)en-us"  
    copy /y "$(ProjectDir)..\..\..\..\OSDSetupWizard\OSDResults\Images\UDI_Wizard_Banner.bmp" "$(ProjectDir)header.bmp"  
    copy /y "$(ProjectDir)Config.xml" "$(TargetDir)”  
    copy /y "$(ProjectDir)header.bmp" "$(TargetDir)header.bmp"  
    ```  

10. En el cuadro de diálogo **Páginas de propiedades de SamplePage**, haga clic en **Aceptar**.  

11. Guarde el proyecto.  

12. Desde el menú **Depuración**, haga clic en **Iniciar depuración**.  

     Aparece el cuadro de diálogo **Microsoft Visual Studio** en el que se indica que el origen no está actualizado y se le pregunta si quiere compilar el proyecto.  

13. En el cuadro de diálogo **Microsoft Visual Studio**, haga clic en **Sí**.  

     Aparece el cuadro de diálogo **No hay información de depuración** en el que se informa de que no hay información de depuración disponible para OSDSetupWizard.exe.  

14. En el cuadro de diálogo **No hay información de depuración**, haga clic en **Sí**.  

     Se abre el Asistente para UDI en el que se muestra la página del asistente personalizada.  

15. Compruebe que puede seleccionar un valor en **Choose your location** (Elegir la ubicación).  

16. En el formulario **Wizard with sample page** (Asistente con página de ejemplo), haga clic en **Cancelar**.  

     Aparece el cuadro de diálogo **Cancelar el asistente**.  

17. En el cuadro de diálogo **Cancelar el asistente**, haga clic en **Sí**.  

18. Cierre Visual Studio 2010.  

#####  <a name="VerifySampleEditorProjectBuildsCorrectly"></a> Comprobación de la compilación correcta del proyecto SampleEditor  
 En el proyecto SampleEditor se proporciona un ejemplo de cómo crear un editor de páginas del asistente personalizado para el diseñador del Asistente para UDI. Para obtener más información sobre el proyecto SampleEditor, vea [Revisión de la solución de Visual Studio SamplePage](#ReviewSamplePageVisualStudioSolution).  

 **Para comprobar que el proyecto SampleEditor se compila correctamente**  

1.  Inicie Visual Studio 2010.  

2.  Abra el proyecto SampleEditor.  

     El proyecto SampleEditor se encuentra en la carpeta *carpeta_local*\SDK\UDI\SampleEditor (donde *carpeta_local* es la carpeta que creó anteriormente en el proceso).  

3.  En Visual Studio 2010, en el Explorador de soluciones, seleccione el proyecto SampleEditor.  

4.  Desde el menú **Proyecto**, haga clic en **Agregar referencia**.  

     Se abre el cuadro de diálogo **Agregar referencia**.  

5.  En el cuadro de diálogo **Agregar referencia**, haga clic en la pestaña **Examinar**.  

6.  En la pestaña **Examinar**, vaya a *carpeta_de_instalación*\Bin (donde *carpeta_de_instalación* es la carpeta en la que instaló MDT). Seleccione los archivos siguientes y, después, haga clic en **Aceptar**:  

    -   Microsoft.Enterprise.UDIDesigner.Common.dll  

    -   Microsoft.Enterprise.UDIDesigner.DataService.dll  

    -   Microsoft.Enterprise.UDIDesigner.Infrastructure.dll  

    -   Microsoft.Practices.Prism.dll  

    -   Microsoft.Practices.ServiceLocation.dll  

    -   Microsoft.Practices.Unity.dll  

    -   RibbonControlsLibrary.dll  

    > [!NOTE]
    >  Puede seleccionar varios archivos en la pestaña **Examinar** si mantiene presionada la tecla CTRL mientras hace clic en los archivos.  

7.  En el Explorador de soluciones, vaya a SampleEditor/Referencias.  

8.  Compruebe que ninguna de las referencias tiene advertencias o errores.  

9. En el Explorador de soluciones, haga clic con el botón derecho en el proyecto SampleEditor y, después, haga clic en **Propiedades**.  

     Aparece el cuadro de diálogo **Páginas de propiedades de SampleEditor**.  

10. En el cuadro de diálogo **Páginas de propiedades de SampleEditor**, haga clic en la pestaña **Depuración**.  

11. En la pestaña **Depuración**, haga clic en **Programa externo de inicio**.  

12. En **Programa externo de inicio**, escriba ***carpeta_de_instalación\Bin\UDIDesigner.exe*** (donde *carpeta_de_instalación* es la carpeta en la que instaló MDT) y, después, haga clic en **Aceptar**.  

    > [!TIP]
    >  Puede hacer clic en el botón de puntos suspensivos (...) para buscar la carpeta y seleccionar UDIDesigner.exe.  

13. En el menú **Archivo**, haga clic en **Guardar todo**.  

14. Copie el archivo *carpeta_local*\SDK\SamplePage\SamplePage.dll.config a la carpeta *carpeta_de_instalación*\Bin\Config (donde *carpeta_local* es la carpeta que creó en el equipo de desarrollo anteriormente en el proceso de configuración y *carpeta_de_instalación* es la carpeta en la que instaló MDT).  

15. En Visual Studio 2010, desde el menú **Depuración**, haga clic en **Iniciar depuración**.  

     Se iniciará el diseñador del Asistente para UDI.  

16. En el diseñador del Asistente para UDI, en la cinta, haga clic en **Abrir**.  

     Aparece el cuadro de diálogo **Abrir**.  

17. En el cuadro de diálogo **Abrir**, abra el archivo *carpeta_local*\SDK\SamplePage\SamplePage\Config.xml (donde *carpeta_local* es la carpeta que creó en el equipo de desarrollo anteriormente en el proceso de configuración).  

     Se abre el archivo Config.xml y se muestra el elemento [StageGroup](#StageGroup) personalizado en el panel de detalles.  

18. En el panel de detalles, haga clic en la pestaña **Configurar**.  

19. Revise la información de configuración del cuadro **Ubicación**, incluido lo siguiente:  

    -   El botón **Desbloquear**, con el que se habilita o deshabilita el cuadro **Ubicación**.  

    -   El cuadro **Valor predeterminado**, en el que se escribe un valor predeterminado que se mostrará en el cuadro **Ubicación**.  

    -   **Friendly display name visible in summary page** (Nombre descriptivo para mostrar visible en la página de resumen), en la que se escribe el título para la información que se muestra en la página **Resumen**.  

    -   El cuadro de lista **Ubicación**, en el que se incluye una lista de las ubicaciones posibles.  

20. Cierre el diseñador del Asistente para UDI.  

21. Cierre Visual Studio 2010.  

## <a name="reviewing-the-udi-sdk-examples"></a>Revisión de los ejemplos del SDK de UDI  
 Antes de comenzar el desarrollo, revise los ejemplos proporcionados en el SDK de UDI. Use la información de esta guía y el código fuente de los ejemplos para crear sus propias páginas de asistente personalizadas y editores de página del Asistente de UDI.  

 Examine los ejemplos del SDK de UDI revisando lo siguiente:  

-   El contenido de la carpeta SDK que copió anteriormente en el proceso de instalación como se describe en [Revisión del contenido de la carpeta SDK](#ReviewContentsofSDKFolder).  

-   El ejemplo de página del Asistente para UDI personalizada, como se describe en [Revisión de la solución de Visual Studio SamplePage](#ReviewSamplePageVisualStudioSolution).  

-   El ejemplo de editor de páginas del Asistente para UDI personalizado, como se describe en [Revisión de la solución de Visual Studio SampleEditor](#ReviewSampleEditorVisualStudioSolution).  

###  <a name="ReviewContentsofSDKFolder"></a> Revisión del contenido de la carpeta SDK  
 Durante la configuración del entorno de desarrollo de UDI, copió la carpeta SDK de la carpeta en la que instaló MDT a otra carpeta que creó. En la tabla 1 se muestran las carpetas situadas inmediatamente debajo de la carpeta SDK y se proporciona una breve descripción de cada una.  

### <a name="table-1-folders-in-the-udi-sdk"></a>Tabla 1. Carpetas en el SDK de UDI  

|**Carpeta**|**Esta carpeta contiene**|  
|-|-|  
|Includes|Los archivos de encabezado de C++ necesarios para crear páginas del asistente personalizadas para el Asistente para UDI.|  
|Libs|Los archivos de biblioteca de C++ que se vincularán a la página personalizada; hay versiones de 32 bits y 64 bits de las bibliotecas de vínculos estáticos. **Nota:** Las versiones de Itanium de las bibliotecas (IA-64) no están disponibles.|  
|SampleEditor|Un proyecto de Visual Studio para crear un editor personalizado que se usa para editar la página SamplePage en el diseñador del Asistente para UDI, que está escrito en C#.|  
|SamplePage|Un proyecto de Visual Studio para crear una página del Asistente para UDI personalizada, que está escrito en Visual C++.|  

###  <a name="ReviewSamplePageVisualStudioSolution"></a> Revisión de la solución de Visual Studio SamplePage  
 Antes de comenzar a crear páginas del asistente personalizadas y editores de página del asistente propios, realice las tareas siguientes para preparar el entorno de desarrollo de UDI:  

-   Revise las fases del ciclo de vida de una página del Asistente para UDI, como se describe en [Revisión del ciclo de vida de la página del asistente](#ReviewWizardPageLifeCycle).  

-   Revise la solución de Visual Studio para el ejemplo SamplePage en el SDK de UDI, como se describe en [Revisión del ejemplo SamplePage](#ReviewSamplePageExample).  

####  <a name="ReviewWizardPageLifeCycle"></a> Revisión del ciclo de vida de la página del asistente  
 Una página del Asistente para UDI tiene métodos que se corresponden a cada fase del ciclo de vida de la página. Como parte de la creación de la página del asistente personalizada, debe invalidar estos métodos con código propio. En la tabla 2 se enumeran los métodos que será necesario invalidar y se proporciona una breve descripción de cada uno, incluido cuándo usar el método en el ciclo de vida de la página del asistente.  

### <a name="table-2-methods-in-a-wizard-page-life-cycle"></a>Tabla 2. Métodos del ciclo de vida de una página del asistente  

|**Método**|**Descripción**|  
|-|-|  
|**OnWindowCreated**|Este método se llama una vez, después de crear la ventana de la página.<br /><br /> Para este método, escriba código que inicialice la página por primera vez y solo tenga que ejecutarse una vez. Por ejemplo, use este método para inicializar los campos o leer información de configuración de los elementos **Setter** del archivo de configuración del Asistente para UDI.|  
|**OnWindowShown**|Este método se llama cada vez que se muestra la página en el Asistente para UDI. Se llama la primera vez que se muestra la página y cada vez que se navega a ella haciendo clic en **Siguiente** o **Atrás** en el asistente.<br /><br /> Para este método, escriba código que prepare la página para mostrarla, por ejemplo, para leer variables de memoria, variables de secuencia de tareas o variables de entorno y, después, actualizar la página en función de los cambios en esas variables.|  
|**OnCommonControlEvent**|Este método se puede llamar cada vez que se muestre la página del asistente y reciba un mensaje WM_NOTIFY de un elemento secundario (normalmente, controles comunes).<br /><br /> Para este método, escriba código que controle WM_NOTIFY en función del mensaje de notificación. Por ejemplo, es posible que le interese responder a los eventos de un control común, como a los eventos de clic o doble clic para un control **TreeView**.|  
|**OnUnhandledEvent**|Este método se llama cada vez que se produce un mensaje de ventana no controlado para la página del asistente. Este método proporciona la oportunidad de interceptar y controlar estos mensajes de ventana que, en caso contrario, no se controlan.<br /><br /> Para este método, escriba código que controle los mensajes de ventana que sean pertinentes para la página del asistente. Por lo general, no es necesario invalidar este método.|  
|**OnNextClicked**|Este método se llama al hacer clic en **Siguiente** en el asistente.<br /><br /> Para este método, escriba código que realice las acciones necesarias antes de pasar a la siguiente página del asistente; por ejemplo, realizar la validación que pueda tardar mucho tiempo. Si se produce un error en la validación, puede cancelar la solicitud de **Siguiente** y mostrar un mensaje.|  
|**OnWindowHidden**|Este método se llama cada vez que la página se oculta cuando se muestra la página del asistente anterior o siguiente.<br /><br /> Para este método, escriba código que realice todas las acciones antes de que se oculte la página, antes de que se muestre otra. Por lo general, no es necesario invalidar este método.|  

####  <a name="ReviewSamplePageExample"></a> Revisión del ejemplo SamplePage  
 Revise el ejemplo SamplePage mediante la lista siguiente, en la que se representa la secuencia de eventos durante el ciclo de vida de la página del asistente del ejemplo SamplePage:  

1.  El Asistente para UDI, OSDSetupWizard.exe, lee la información de configuración desde el archivo de configuración del Asistente para UDI en el ejemplo (el archivo Config.xml) como se describe en [Paso 1: el Asistente para UDI (OSDSetupWizard.exe) lee el archivo Config.xml](#UDIWizardReadstheConfigFile).  

2.  El Asistente para UDI carga los archivos DLL necesarios para cada página del asistente indicada en el archivo de configuración del Asistente para UDI, como se describe en [Paso 2: el Asistente para UDI carga el archivo DLL de la página del asistente personalizada](#UDIWizardLoadstheDLLforCustomWizardPage).  

3.  El Asistente para UDI muestra la página del asistente personalizada y permite la interacción de control deseada, como se describe en [Paso 3: el Asistente para UDI muestra la página del asistente personalizada](#UDIWizardDisplaysCustomWizardPage).  

4.  Cuando la página del asistente personalizada ha recopilado la información, realice las tareas necesarias antes de hacer clic en **Siguiente** para continuar con el asistente siguiente, como se describe en [Paso 4: se hace clic en el botón Siguiente en la página del asistente personalizada](#TheNextButtonisClickedinCustomWizardPage).  

#####  <a name="UDIWizardReadstheConfigFile"></a> Paso 1: el Asistente para UDI (OSDSetupWizard.exe) lee el archivo Config.xml  
 Cuando se inicia el Asistente para UDI (OSDSetupWizard.exe), de forma predeterminada lee el archivo de configuración del Asistente para UDI, que es el archivo UDIWizard_Config.xml (el archivo de configuración principal del Asistente para UDI).  

> [!NOTE]
>  En el ejemplo se usa Config.xml como el archivo de configuración. En MDT, el archivo de configuración predeterminado es UDIWizard_Config.xml, que se encuentra en la carpeta Scripts en el paquete de archivos de MDT para la configuración.  

 Se puede reemplazar el archivo de configuración predeterminado que usa el Asistente para UDI si se modifica el paso de secuencia de tareas del Asistente para UDI para usar el parámetro **/definition**. Para obtener más información sobre cómo invalidar el archivo de configuración predeterminado que usa el Asistente para UDI, vea "Invalidación del archivo de configuración que usa el Asistente para UDI".  

 Los elementos de nivel superior del archivo Config.xml son los siguientes:  

-   Elemento [DLLs](#DLLs)  

-   Elemento [Style](#Style)  

-   Elemento [Pages](#Pages)  

-   Elemento [StageGroups](#StageGroups)  

 Para obtener más información sobre el esquema del archivo de configuración del Asistente para UDI y cada uno de estos elementos, vea [Referencia de esquema del archivo de configuración del Asistente para UDI](#UDIWizardConfigurationFileSchemaReference).  

 El Asistente para UDI examina el elemento **DLLs** para buscar los archivos .dll que se van a cargar. En el ejemplo, se muestran dos archivos .dll: SamplePage.dll y SharedPages.dll. Estos archivos .dll deben estar en la misma carpeta que OSDSetupWizard.exe: la carpeta Tools\\*plataforma* (donde *plataforma* es x86 para la versión de 32 bits o x64 para la de 64 bits).  

 El Asistente para UDI examina el elemento **Pages** para buscar las páginas que se definen. En el ejemplo, se definen dos páginas: **Custom** y **SummaryPage**. El atributo **Tipo** del elemento **Page** se define en el archivo PageClassIDs.h y define de forma inequívoca el tipo de la página personalizada.  

 En el ejemplo, el tipo definido es **Microsoft.SamplePage.LocationPage**. Para la página personalizada, sustituya los elementos siguientes para evitar posibles conflictos con otras páginas que pueda crear en el futuro:  

-   El nombre de la organización en lugar de **Microsoft**.  

-   El nombre del proyecto en lugar de **SamplePage**.  

-   El nombre de la página del asistente personalizada en lugar de **LocationPage**.  

#####  <a name="UDIWizardLoadstheDLLforCustomWizardPage"></a> Paso 2: el Asistente para UDI carga el archivo DLL de la página del asistente personalizada  
 Cuando el Asistente para UDI carga el archivo DLL, llama a la función **RegisterFactories**, que se debe implementar en el archivo .dll. En el ejemplo, esta función se implementa en el archivo dllmain.ccp. Todas las páginas del asistente que se creen deben implementar la función **RegisterFactories**.  

 La función **RegisterFactories** se usa para registrar la clase de generador de la página del asistente con el registro de generadores de clases del Asistente para UDI. Los *generadores de clases* son clases que pueden crear una instancia de otra clase. La función **RegisterFactories** crea una instancia de una clase de generador y la pasa al registro de generadores de clases del Asistente para UDI, que pone esa clase de generador a disposición del asistente. El Asistente para UDI busca una clase de generador registrada con un identificador que coincida con el atributo **Tipo** del elemento **Page** de la página del asistente personalizada.  

 En el ejemplo, el identificador se define como **ID_Location** en el archivo PageClassIds.h como **Microsoft.SamplePage.LocationPage**, que coincide con el atributo **Tipo** del elemento **Page** en el archivo Config.xml. **ID_Location** se pasa como un parámetro en la función **RegisterFactories** implementada en el archivo dllmain.ccp.  

 Se puede crear una función mediante la plantilla de función Register_*nombre* para simplificar la creación de una instancia de generador y registrar la instancia recién creada. El valor **nombre** proporcionado con la plantilla de la función Register debe implementar la interfaz **iClassFactory**. La [clase ClassFactoryImpl](#ClassFactoryImplClass) controla la mayoría de los detalles de implementación de un generador de clases.  

 También se puede usar la función **RegisterFactories** para registrar tipos de tareas y de validador. Para obtener más información, consulte:  

-   [Creación de tareas de UDI personalizadas](#CreatingCustomUDITasks)  

-   [Creación de validadores de UDI personalizados](#CreatingCustomUDIValidators)  

> [!NOTE]
>  En el ejemplo solo se incluye y registra la única página del asistente personalizada. En el ejemplo no se incluyen tareas ni validadores personalizados, por lo que no se registra ninguna tarea o validador personalizado.  

#####  <a name="UDIWizardDisplaysCustomWizardPage"></a> Paso 3: el Asistente para UDI muestra la página del asistente personalizada  
 La página del asistente personalizada del ejemplo se define en el archivo LocationPage.cpp. Las páginas del asistente se derivan las clases de plantilla que proporcionan gran parte de la funcionalidad de una página. Todas las páginas del asistente deben derivarse de la [clase de plantilla WizardPageImpl](#WizardPageImplTemplateClass), que implementa la [interfaz IWizardPage](#IWizardPageInterface). Cada página del asistente puede implementar otras clases de plantilla opcionales y las interfaces correspondientes en función de las necesidades de la página.  

 La [clase de plantilla WizardPageImpl](#WizardPageImplTemplateClass) tiene varias interfaces útiles que pueden ayudar a escribir páginas del asistente personalizadas. Implemente la [clase de plantilla WizardPageImpl](#WizardPageImplTemplateClass) como la clase base para la página del asistente personalizada.  

 Para obtener una lista de:  

-   Las clases de plantilla disponibles para las páginas del asistente, vea [Clases auxiliares de página del asistente](#WizardPageHelperClasses).  

-   Las interfaces disponibles para las clases de plantilla de página del asistente, vea [Interfaces de página del asistente](#WizardPageInterfaces).  

 La página del asistente personalizada del ejemplo se deriva de la [clase de plantilla WizardPageImpl](#WizardPageImplTemplateClass) e implementa la [interfaz IWizardPage](#IWizardPageInterface). Además, la página del asistente personalizada implementa la interfaz **IFieldCallback**. Las dos se implementan en el archivo LocationPage.cpp.  

 En la página del asistente personalizada del ejemplo se invalidan los métodos siguientes:  

-   **OnWindowCreated**. El método **OnWindowCreated** de la página del asistente del ejemplo llama a los métodos siguientes:  

    -   [AddField](#AddField). Este método relaciona el control de cuadro **IDC_COMBO_LOCATION** del recurso **IDD_LOCATION_PAGE** con el elemento [Data](#Data) denominado **Location** en el archivo Config.xml.  

         Además del método **AddField**, se pueden usar los métodos [AddRadioGroup](#AddRadioGroup) y [AddToGroup](#AddToGroup) para admitir otros controles y comportamientos.  

        > [!NOTE]
        >  Asegúrese de que se llama al método [AddField](#AddField), [AddRadioGroup](#AddRadioGroup) o [AddToGroup](#AddToGroup) antes de llamar al método [InitFields](#InitFields).  

    -   [InitFields](#InitFields). Use este método para inicializar los campos (controles) que ha agregado al formulario. El puntero de la página es un parámetro. En el ejemplo, se pasa el puntero **this**, que hace referencia a la página actual.  

        > [!NOTE]
        >  Para admitir el uso del puntero **this**, debe implementar la interfaz **IFieldCallback** además de las que admita la [plantilla de clase WizardPageImpl](#WizardPageImplTemplateClass).  

         La interfaz **IFieldCallback** llama al método **SetFieldDefault**, que se usa para establecer los valores predeterminados para los controles que no son de cuadro de texto y de casilla. En el ejemplo, el método **SetFieldDefault** establece el índice inicial del control de cuadro combinado en función del valor predeterminado especificado en el elemento **Default** para el elemento [Field](#Field) del archivo Config.xml.  

     El método **OnWindowCreated** configura el controlador de formulario mediante la [interfaz IFormController](#IFormController-Interface). Para obtener más información sobre cómo configurar el controlador de formulario, vea [Configuración del formulario](#SettingUptheForm).  

-   **InitLocations**. Este método rellena el cuadro combinado de la lista de ubicaciones del archivo Config.xml. El elemento [Data](#Data) y los elementos secundarios [DataItem](#DataItem) del archivo Confg.xml proporcionan la lista de valores posibles.  

-   **OnNextClicked**. Este método realiza las tareas siguientes:  

    -   Actualiza la variable de secuencia de tareas **TSLocation** con el valor seleccionado en el cuadro combinado mediante el método **SaveFields**.  

    -   Agrega la información que se mostrará en la página **Resumen** con el método **SaveFields**.  

#####  <a name="TheNextButtonisClickedinCustomWizardPage"></a> Paso 4: Se hace clic en el botón Siguiente en la página del asistente personalizada  
 Cuando el usuario completa los campos en la página del asistente personalizada, hace clic en **Siguiente**, lo que llama al método **OnNextClicked**. El método **OnNextClicked** realiza las tareas necesarias antes de continuar con la siguiente página del asistente, como la grabación de los cambios de configuración realizados en la página del asistente personalizada.  

 Para la página del asistente personalizada de ejemplo, la invalidación del método **OnNextClicked** se implementa en el archivo LocationPage.ccp. En el método **OnNextClicked** de la página del asistente personalizada de ejemplo se llama a los métodos siguientes:  

1.  [InitSection](#InitSection). Este método inicializa el encabezado (título de la etiqueta) para los datos de resumen que se muestran en la página **Resumen**. Por lo general, este valor se puede establecer con la función **DisplayName()**. Los datos asociados con este título se guardan con el método [SaveFields](#SaveFields).  

2.  [SaveFields](#SaveFields). Este método guarda los valores de campo en las variables de secuencia de tareas y en los datos que se muestran en la página **Resumen**.  

###  <a name="ReviewSampleEditorVisualStudioSolution"></a> Revisión de la solución de Visual Studio SampleEditor  
 Antes de comenzar a crear páginas del asistente personalizadas y editores de páginas del asistente propios, siga los pasos siguientes para preparar el entorno de desarrollo de UDI:  

-   Revise la arquitectura del diseñador del Asistente para UDI, como se describe en [Revisión de la arquitectura del diseñador del Asistente para UDI](#ReviewUDIWizardDesignerArchitecture).  

-   Revise los componentes de una página del Asistente para UDI que se pueden personalizar mediante el archivo de configuración del Asistente para UDI, como se describe en [Revisión de los componentes configurables de una página del Asistente para UDI](#ReviewConfigurableComponentsofUDIWizardPage).  

-   Revise el ejemplo EditorPage proporcionado en el SDK de UDI, como se describe en [Revisión del ejemplo EditorPage](#ReviewEditorPageExample).  

####  <a name="ReviewUDIWizardDesignerArchitecture"></a> Revisión de la arquitectura del diseñador del Asistente para UDI  
 El diseñador del Asistente para UDI se desarrolló con WPF, Prism y Unity. El diseñador de UDI se usa para editar el archivo de configuración del Asistente para UDI (UDIWizard_Config.xml), que el Asistente para UDI (OSDSetupWizard.exe) lee en tiempo de ejecución. El elemento [Pages](#Pages) del archivo de configuración del Asistente para UDI contiene una lista de páginas con un elemento [Page](#Page) independiente para cada página del asistente.  

 Al editar los valores de configuración de una página del asistente, el diseñador del Asistente para UDI carga el editor de páginas personalizado que se corresponde con el tipo de página del asistente. Los editores de página del asistente personalizado se desarrollan como controles de usuario de WPF. El editor de páginas del asistente personalizado usa el modelo de diseño [Model-View-ViewModel](http://msdn.microsoft.com/magazine/dd419663.aspx) (MVVM) para WPF.  

 El modelo de diseño MVVM ayuda a separar la interfaz de usuario (UI; presentación) de los datos que se presentan. Los datos son una fachada sobre el elemento [Page](#Page) del archivo de configuración del Asistente para UDI (el archivo Config.xml en el ejemplo), al que se tiene acceso mediante la propiedad [CurrentPage](#CurrentPage) de la interfaz [IDataService](#IDataService).  

 En el diseñador del Asistente para UDI se usa **DependencyAttribute** para obtener acceso a la clase **DataService** en función del marco de trabajo de inserción de dependencias de Unity. Para obtener más información sobre el marco de trabajo de inserción de dependencias de Unity, vea [Inject Some Life into Your Applications—Getting to Know the Unity Application Block](http://msdn.microsoft.com/library/ff650806.aspx) (Inserción de vida en las aplicaciones: familiarizarse con el bloque de aplicaciones de Unity).  

####  <a name="ReviewConfigurableComponentsofUDIWizardPage"></a> Revisión de los componentes configurables de una página del Asistente para UDI  
 A medida que se crea la página del asistente personalizada, algunas de las opciones de configuración se pueden establecer en el código y no se pueden cambiar una vez que se compila la página. Pero para otras opciones de configuración será necesario permitir el cambio de esos valores de configuración mediante el diseñador del Asistente para UDI.  

 Normalmente, los valores de configuración que se quieren configurar con el diseñador del Asistente para UDI se guardan en el archivo de configuración del Asistente para UDI (el archivo Config.xml en el ejemplo). Pero también puede crear su propio archivo de configuración independiente, si es necesario. Un ejemplo de uso de un archivo de configuración independiente es el archivo UDIWizard_Config.xml.app, que usan la tarea **Detección de aplicaciones** y el tipo de página del asistente **ApplicationPage**.  

 La siguiente es una lista de las opciones de configuración típicas que se pueden administrar mediante el diseñador del Asistente para UDI:  

-   **Field**. Use los campos para permitir a los usuarios proporcionar entradas. Los campos aparecen como elementos [Field](#Field) en el archivo de configuración del Asistente para UDI (UDIWizard_Config.xml), que contiene los valores de configuración para cada campo. El editor de página del asistente correspondiente debe proporcionar un método para modificar los valores de configuración de campo para el campo mediante [FieldElementControl](#FieldElementControl).  

-   **Propiedades**. Los establecedores ayudan a crear propiedades para las entidades de la página, como las páginas del elemento [Page](#Page), los campos del elemento, [Field](#Field) o los datos de los elementos [Data](#Data) o [DataItem](#DataItem). Las propiedades se configuran en los elementos [Setter](). Agregue un elemento [Setter]() para cada propiedad que quiera definir. Las propiedades se modifican mediante [SetterControl](#SetterControl) y otros elementos [Setter]() se configuran con otros controles.  

-   **Datos**. Los datos se usan para almacenar información para su uso por la página del asistente y otros componentes. Se pueden definir datos para páginas o campos mediante los elementos [Data](#Data) o [DataItem](#DataItem). Los datos se pueden definir en una estructura sin formato o jerárquica mediante el uso correcto de los elementos [Data](#Data) o [DataItem](#DataItem). En el archivo Config.xml del ejemplo del SDK se muestra cómo generar estructuras de datos sin formato.  

 El editor de páginas del asistente personalizado que cree debe ser capaz de administrar estos valores de configuración.  

####  <a name="ReviewEditorPageExample"></a> Revisión del ejemplo EditorPage  
 El ejemplo EditorPage se usa para establecer las opciones de configuración para la página del asistente **SamplePage** en el archivo de configuración del Asistente para UDI. El ejemplo EditorPage tiene los componentes principales siguientes:  

-   Interfaz de usuario para configurar los valores del cuadro combinado **Location**.  

-   Interfaz de usuario para agregar o editar una ubicación de la lista de ubicaciones posibles, que se muestran en el cuadro combinado **Location**.  

-   Las opciones de configuración se leen y se guardan en el archivo de configuración del Asistente para UDI.  

-   Código auxiliar para los demás componentes.  

 Siga estos pasos para revisa el ejemplo EditorPage en Visual Studio:  

1.  Revise cómo se carga e inicializa el editor de páginas del asistente **SampleEditor** en el diseñador del Asistente para UDI, como se describe en [Revisión de la carga e inicialización del editor de páginas del asistente](#ReviewWizardPageEditorLoadingInitialization).  

2.  Revise la interfaz de usuario que se usa para editar el cuadro combinado **Location** en los archivos LocationPageEditor.xaml y LocationPageEditor.xaml.cs, como se describe en [Revisión de la interfaz de usuario que se usa para configurar el cuadro combinado Location](#ReviewUserInterfaceUsedtoConfigureLocationComboBox).  

3.  Revise la interfaz de usuario que se usa para agregar o modificar ubicaciones a la lista de los archivos AddEditLocationView.xaml y AddEditLocationView.xaml.cs, como se describe en [Revisión de la interfaz de usuario que se usa para modificar la lista de ubicaciones posibles](#ReviewUserInterfaceUsedtoModifyListofPossibleLocations).  

4.  Revise el código que se usa para administrar la información de configuración guardada en el archivo de configuración del Asistente para UDI, como se describe en [Revisión del código que se usa para administrar la información de configuración](#ReviewCodeUsedtoManageConfigurationInformation).  

#####  <a name="ReviewWizardPageEditorLoadingInitialization"></a> Revisión de la carga e inicialización del editor de páginas del asistente  
 Los editores de páginas del asistente personalizados se cargan según sea necesario por el diseñador del Asistente para UDI. Los archivos de configuración del diseñador del Asistente para UDI se cargan cuando se inicia el diseñador del Asistente para UDI. El diseñador del Asistente para UDI busca en la carpeta *carpeta_de_instalación*\Bin\Config (donde *carpeta_de_instalación* es el nombre de la carpeta donde se instaló MDT) los archivos que tienen una extensión de archivo de .config.  

 Durante la configuración del entorno de desarrollo de UDI, copió el archivo SamplePage.dll.confg a la carpeta *carpeta_de_instalación*\Bin\Config. Cuando se inicia el diseñador del Asistente para UDI, se localiza y se carga el archivo SamplePage.dll.confg.  

 El diseñador del Asistente para UDI usa los atributos siguientes del elemento [Page](#Page) del archivo SamplePage.dll.confg para cargar e inicializar el ejemplo EditorPage:  

-   **EnsambladoDeDiseñador**. Este atributo determina el nombre del archivo DLL que se va a cargar. Este archivo DLL se debe colocar en la misma carpeta que el archivo UDIDesigner.exe, que es *carpeta_de_instalación*\Bin (donde *carpeta_de_instalación* es el nombre de la carpeta en la que se instaló MDT).  

-   **TipoDeDiseñador**. Este atributo es el nombre de tipo de Microsoft .NET de la clase que contiene el control de usuario de WPF.  

-   **Tipo**. Use este atributo para configurar el tipo de página de la página del asistente personalizada, que el Asistente para UDI carga. El diseñador del Asistente para UDI usa este atributo para localizar el elemento [Page](#Page) correspondiente en el archivo de configuración del Asistente para UDI.  

-   **Dll**. Use este atributo para configurar el elemento [DLL](#DLL) del archivo de configuración del Asistente para UDI, que el diseñador del Asistente para UDI crea.  

-   **Descripción**. Use este atributo para proporcionar información sobre el editor de páginas del asistente. El valor de este atributo se muestra en el cuadro de diálogo **Agregar nueva página** del diseñador del Asistente para UDI, que se usa para agregar la página del asistente a la "Biblioteca de páginas".  

-   **DisplayName**. Use este atributo para proporcionar el nombre de la página del asistente personalizada que se muestra en el diseñador del Asistente para UDI. El valor de este atributo se muestra en el cuadro de diálogo **Agregar nueva página** del diseñador del Asistente para UDI, que se usa para agregar la página del asistente a la "Biblioteca de páginas".  

     En el ejemplo, el tipo de la página del asistente personalizada **SamplePage** es **Microsoft.SamplePage.LocationPage**, que se guarda en el archivo Config.xml. El archivo Config.xml se encuentra en la carpeta *carpeta_local*\SDK\SamplePage\SamplePage (donde *carpeta_local* es la carpeta que creó en el equipo de desarrollo anteriormente en el proceso de configuración).  

#####  <a name="ReviewUserInterfaceUsedtoConfigureLocationComboBox"></a> Revisión de la interfaz de usuario que se usa para configurar el cuadro combinado Location  
 Cuando se carga y se inicializa el editor de páginas de asistente, se carga el editor de páginas del asistente SampleEditor cuando se modifica una página con el tipo de **Microsoft.SamplePage.LocationPage**. La interfaz de usuario para el editor de páginas se almacena en el archivo LocationPageEditor.xaml.  

 Si examina la interfaz de usuario en la pestaña **Diseño** y el código en la pestaña **XAML**, puede ver la relación entre la interfaz gráfica de usuario y los elementos y atributos del lenguaje XAML.  

 Por ejemplo, si examina el elemento **Controls:FieldElementControl** en el código XAML puede ver cómo que se relaciona con el diseño de la interfaz de usuario correspondiente. Use el elemento **Controls:FieldElementControl** para definir el control [FieldElementControl](#FieldElementControl).  

 Los parámetros **Binding** del archivo XAML enlazan los campos del editor de páginas de ejemplo con la información en el archivo de configuración del Asistente para UDI. Por ejemplo, el código siguiente vincula el cuadro de texto **Valor predeterminado** con el elemento [Default](#Default) del archivo de configuración del Asistente para UDI (Config.xml en el ejemplo):  

```  
<TextBox Text="{Binding FieldData.DefaultValue,  
 UpdateSourceTrigger=PropertyChanged,  
 Mode=TwoWay}"/>  
```  

 Para obtener más información, vea [Cómo: Hacer que los datos estén disponibles para el enlace en XAML](http://msdn.microsoft.com/library/ms748857.aspx).  

 Use el elemento **Views:CollectionTControl.ColumnCollectionView** del código XAML para modificar la lista de ubicaciones disponibles en la vista de cuadrícula. El control [CollectionTControl](#CollectionTControl) se usa para mostrar la vista de cuadrícula y enlazarla al elemento [Data](#Data) con el nombre **Location** en el archivo de configuración UDI.  

#####  <a name="ReviewUserInterfaceUsedtoModifyListofPossibleLocations"></a> Revisión de la interfaz de usuario que se usa para modificar la lista de ubicaciones posibles  
 La interfaz de usuario para modificar la lista de ubicaciones posibles consta de lo siguiente:  

-   Un menú contextual y botones de la cinta de opciones que permiten agregar, editar, quitar o cambiar el orden de los elementos de la lista de ubicaciones, como se describe en [Revisión del menú contextual y los botones de la cinta para modificar la lista de ubicaciones](#ReviewContextSensitiveMenuandRibbonButtons).  

-   Un cuadro de diálogo que se inicia cuando se selecciona agregar o editar un elemento en la lista de ubicaciones, como se describe en [Revisión del cuadro de diálogo para agregar o editar ubicaciones](#ReviewDialogBoxforAddingEditingLocations).  

######  <a name="ReviewContextSensitiveMenuandRibbonButtons"></a> Revisión del menú contextual y los botones de la cinta para modificar la lista de ubicaciones  
 Cuando hace clic con el botón derecho en el cuadro de lista que contiene la lista de ubicaciones, se muestra un menú contextual. La cinta tiene botones correspondientes que permiten realizar las mismas tareas. En el elemento de control **Views:CollectionsTControl** del archivo LocationPageEditor.xaml se definen los métodos a los que se llama en función de la acción realizada y las propiedades que se establecen como sigue:  

-   **SelectedItem**. Esta propiedad de enlace a datos se activa cuando el usuario selecciona un elemento en la lista. Esta propiedad está vinculada a la propiedad **CurrentLocation** del modelo de vista, que está ubicada en el archivo LocationPageEditorViewModel.cs y que el control [CollectionTControl](#CollectionTControl) usa para pasar el elemento seleccionado al editar o quitar un elemento existente.  

-   **AddItemAction**. Esta acción se realiza cuando el usuario hace clic en la opción **Agregar elemento** del menú contextual o los botones correspondientes de la cinta. Hay un enlace de datos a una propiedad en el modelo de vista que devuelve el objeto **AddLocationAction**. Este objeto es el método **AddLocationCallback**, que se encuentra en el archivo LocationPageEditorViewModel.cs, y muestra el cuadro de diálogo del archivo AddEditLocationView.xaml.  

-   **EditItemAction**. Esta acción se realiza cuando el usuario hace clic en la opción **Editar elemento** del menú contextual. Hay un enlace de datos a una propiedad en el modelo de vista que devuelve el objeto **EditLocationAction**. Este objeto es el método **EditLocationCallback**, que se encuentra en el archivo LocationPageEditorViewModel.cs, y muestra el cuadro de diálogo del archivo AddEditLocationView.xaml.  

-   **RemoveAction**. Esta acción se realiza cuando el usuario hace clic en la opción **Quitar elemento** del menú contextual. Hay un enlace de datos a una propiedad en el modelo de vista que devuelve el objeto **RemoveAction**. Este objeto es el método **EditLocationCallback**, que se encuentra en el archivo LocationPageEditorViewModel.cs, y muestra un mensaje que confirma la eliminación de la ubicación.  

######  <a name="ReviewDialogBoxforAddingEditingLocations"></a> Revisión del cuadro de diálogo para agregar o editar ubicaciones  
 Si se agrega una ubicación nueva a la lista de ubicaciones o se modifica una ubicación existente, se muestra un mensaje que se encuentra en el archivo AddEditLocationView.xaml. El mensaje se muestra mediante el método de ventana [ShowDialogWindow](#ShowDialogWindow) del archivo LocationPageEditorViewModel.cs.  

 La interfaz de usuario del archivo AddEditLocationView.xaml consta de lo siguiente:  

-   Un marco de cuadro de diálogo denominado **DialogFrame**, que incluye los elementos siguientes:  

    -   Un título, que se configura mediante el atributo **DialogTitle** del marco de cuadro de diálogo.  

    -   Un botón **Aceptar**, que establece el estado devuelto de la propiedad **Approved** en **True** (El estado devuelto se comprueba en el método **AddLocationCallback** del archivo LocationPageEditorViewModel.cs para determinar si el usuario hizo clic en **Aceptar**).  

    -   Un botón **Cancelar**, que establece el estado devuelto de la propiedad **Approved** en **False** (El estado devuelto se comprueba en el método **AddLocationCallback** del archivo LocationPageEditorViewModel.cs para determinar si el usuario hizo clic en **Cancelar**).  

-   Un elemento de WPF que contiene lo siguiente:  

    -   Una etiqueta que se configura mediante el atributo **Contenido**.  

    -   Un cuadro de texto que se enlaza al elemento [Data](#Data) con el nombre **Location** en el archivo de configuración de UDI (el archivo Config.xml en el ejemplo).  

######  <a name="ReviewCodeUsedtoManageConfigurationInformation"></a> Revisión del código que se usa para administrar la información de configuración  
 La información de configuración de la página del asistente personalizada se almacena en el archivo de configuración del Asistente para UDI, que es:  

-   El archivo config.xml en el ejemplo proporcionado con el SDK de UDI (este archivo solo contiene las opciones de configuración para el ejemplo).  

-   El archivo UDIWizard_Config.xml proporcionado con MDT, que se almacena en *carpeta_de_instalación*\Templates\Distribution\Scripts (donde *carpeta_de_instalación* es la carpeta en la que instaló MDT); este archivo contiene las opciones de configuración para todas las páginas y fases del asistente integradas.  

 En el ejemplo SampleEditor, la rutina **Locations** facilita la administración de la información de configuración y se encuentra en el archivo LocationPageEditorViewModel.cs. La rutina **Locations** devuelve una lista de las ubicaciones del archivo de configuración del Asistente para UDI. En concreto, la lista devuelta contiene un elemento para cada elemento [DataItem](#DataItem) del archivo de configuración del Asistente para UDI.  

## <a name="creating-custom-udi-wizard-pages"></a>Creación de páginas personalizadas del Asistente para UDI  
 El proceso general para la creación de páginas personalizadas del Asistente para UDI es el siguiente:  

1.  Realizar una copia de la solución SamplePage como punto de partida.  

2.  Colocar los controles (campos) deseados en el formulario.  

3.  Escribir código para realizar las tareas apropiadas cuando se carga la página del asistente (invalidaciones para el método **OnWindowCreated**), incluidos los pasos siguientes:  

    1.  Inicializar el formulario.  

    2.  Leer variables de memoria, variables de secuencia de tareas, variables de entorno o información de archivos XML (como las propiedades **Setter**).  

4.  Escribir código para realizar las tareas apropiadas cuando se muestra la página (invalidaciones para el método **OnWindowShown**), incluidos los pasos siguientes:  

    1.  Habilitar o deshabilitar controles en función de la información que se lee cuando se carga la página en el paso 3.  

    2.  Actualizar los controles en función de la información que se lee cuando se carga página en el paso 3, por ejemplo, el rellenado de los controles de acuerdo con la información que se ha leído.  

5.  Escribir código para realizar las tareas apropiadas mientras el usuario interactúa con la página del asistente.  

6.  Escribir código para realizar las tareas apropiadas cuando el usuario hace clic en **Siguiente** en el Asistente para UDI (invalidaciones para el método **OnNextClicked**), incluidos los pasos siguientes:  

    1.  Actualizar las variables de memoria, variables de secuencia de tareas, variables de entorno o información de archivos XML.  

    2.  Actualizar la información de la página de resumen (si no lo hacen los campos de la página).  

7.  Compilar la solución.  

     Asegúrese de que la versión del archivo DLL que se crea es la misma plataforma de procesador que en la instalación de MDT, en concreto, la plataforma de procesador para el entorno de preinstalación de Windows (Windows PE). El Asistente para UDI se puede ejecutar en:  

    -   **El sistema operativo existente en el equipo de destino**. Puede ejecutar las versiones de 32 bits de la página del asistente en sistemas operativos Windows de 32 bits o 64 bits. Pero solo se pueden ejecutar las versiones de 64 bits de la página del asistente en sistemas operativos Windows de 64 bits.  

    -   **Windows PE en el equipo de destino**. Windows PE no admite la ejecución de aplicaciones de 32 bits en una versión de 64 bits de Windows PE. Por tanto, tendrá que crear una versión de la página del asistente para cada arquitectura de procesador de Windows PE que se va a usar.  

8.  Copie el archivo DLL de la página del asistente personalizada en *carpeta_de_instalación*\Templates\Distribution\Tools\plataforma (donde *carpeta_de_instalación* es la carpeta en la que instaló MDT y *plataforma* es **x86** para la versión de 32 bits o **x64** para la versión de 64 bits).  

9. Complete los pasos para crear un editor de páginas personalizado.  

## <a name="creating-custom-wizard-page-editors"></a>Creación de editores de páginas del asistente personalizado  
 El proceso general para la creación de editores de páginas personalizado del Asistente para UDI es el siguiente:  

1.  Realizar una copia de la solución SampleEditor como punto de partida.  

2.  Crear la interfaz de usuario principal del editor de páginas en un archivo .xaml.  

3.  Agregar instancias del control [FieldElementControl](#FieldElementControl) según sea necesario para la configuración de la página del asistente.  

4.  Agregar instancias del control [SetterControl](#SetterControl) según sea necesario para la configuración de la página del asistente.  

5.  Agregar instancias del control [CollectionTControl](#CollectionTControl) según sea necesario para la configuración de la página del asistente.  

6.  Agregar la interfaz [IDataService](#IDataService).  

7.  Escribir el código adecuado para actualizar el archivo de configuración del Asistente para UDI en función de los valores de configuración que se van a configurar mediante el editor de páginas del asistente personalizado.  

8.  Crear cuadros de diálogo secundarios en un archivo .xaml y llamarlos desde el editor de páginas principal mediante la interfaz [IMessageBoxService](#IMessageBoxService) según sea necesario para configurar la página del asistente.  

9. Agregar las interfaces adecuadas a la cinta del diseñador del Asistente para UDI según los requisitos de la página del asistente que se va a configurar.  

10. Compilar la solución.  

    > [!NOTE]
    >  Asegúrese de que la versión del archivo DLL que se crea es la misma plataforma de procesador que en la instalación de MDT. Por ejemplo, si instala la versión de 64 bits de MDT, compile una versión de 64 bits del editor de páginas personalizado.  

11. Cree un archivo de configuración del diseñador del Asistente para UDI para cargar los archivos DLL necesarios y asigne el editor de páginas del asistente con la página del asistente correspondiente (el archivo SamplePage.dll.config en el ejemplo).  

     Para obtener más información sobre los elementos necesarios para realizar la asignación entre la página del asistente y el editor de páginas del asistente, vea el elemento [DesignerMappings](#DesignerMappings), los elementos secundarios y los atributos correspondientes.  

12. Copie el archivo de configuración del diseñador del Asistente para UDI que creó en el paso anterior en *carpeta_de_instalación*\Bin\Config (donde *carpeta_de_instalación* es la carpeta en la que instaló la versión de MDT).  

13. Copie el archivo DLL del editor de páginas del asistente personalizado en *carpeta_de_instalación*\Bin (donde *carpeta_de_instalación* es la carpeta en la que instaló MDT).  

##  <a name="CreatingCustomUDITasks"></a> Creación de tareas de UDI personalizadas  
 Las *tareas de UDI* son archivos DLL escritos en C++ que implementan la [interfaz ITask](#ITaskinterface). El archivo DLL se registra con la biblioteca de tareas del diseñador del Asistente para UDI mediante la creación de un archivo de configuración del diseñador del Asistente para UDI (archivo .config) y se coloca en *carpeta_de_instalación*\Bin\Config (donde *carpeta_de_instalación* es la carpeta en la que instaló MDT).  

> [!NOTE]
>  Se puede crear un archivo DLL que contenga las páginas del asistente, las tareas y los validadores dentro del mismo archivo .dll. También se puede crear un único archivo de configuración de diseñador del Asistente para UDI (.config) que contenga los valores de configuración para las páginas del asistente, las tareas y los validadores en el archivo DLL.  

 **Para crear tareas personalizadas de UDI**  

1.  Escriba código que implemente la [interfaz ITask](#ITaskinterface) y los métodos siguientes:  

    -   [Init](#Init). Este método se llama para inicializar la tarea.  

    -   [Execute](#Execute). Este método se llama para ejecutar la tarea.  

2.  Escriba código que registre el generador de clases de tareas personalizado con el registro de fábrica.  

3.  Compile la solución para la tarea personalizada.  

    > [!NOTE]
    >  Asegúrese de que la versión del archivo DLL que se crea es la misma plataforma de procesador que en la instalación de MDT. Por ejemplo, si instala la versión de 64 bits de MDT, compile una versión de 64 bits de la tarea de UDI personalizada.  

4.  Cree un elemento [Task](#Task) bajo el elemento [TaskLibrary](#TaskLibrary) en el archivo de configuración del diseñador del Asistente para UDI similar al fragmento siguiente:  

    ```  
    <Task DLL="OSDRefreshWizard.dll" Description="Discovers supported applications for install." Type="Microsoft.OSDRefresh.AppDiscoveryTask" Name="Application Discovery">  
       <TaskItem Type="Setter" Name="Status Bitmap">  
          <Param Name="BitmapFilename"/>  
       </TaskItem>  
       <TaskItem Type="Setter" Name="Log File">  
          <Param Name="log"/>  
       </TaskItem>  
       <TaskItem Type="Setter" Name="Write Configuration File">  
          <Param Name="writecfg"/>  
       </TaskItem>  
       <TaskItem Type="Setter" Name="Read Configuration File">  
          <Param Name="readcfg"/>  
       </TaskItem>  
    </Task>  
    ```  

    > [!NOTE]
    >  Todos los elementos [Task](#Task) deben incluir el parámetro **BitmapFilename**. Especifique los demás parámetros en función de los requisitos de la tarea. Por ejemplo, en el extracto anterior, el parámetro **log** se usa para especificar un parámetro para la ubicación de un archivo de registro.  

5.  Copie el archivo de configuración del diseñador del Asistente para UDI creado en el paso anterior en *carpeta_de_instalación*\Bin\Config (donde *carpeta_de_instalación* es la carpeta en la que instaló MDT).  

6.  Copie el archivo DLL de la tarea personalizada en *carpeta_de_instalación*\Templates\Distribution\Tools\plataforma (donde *carpeta_de_instalación* es la carpeta en la que instaló MDT y *plataforma* es **x86** para la versión de 32 bits o **x64** para la versión de 64 bits).  

##  <a name="CreatingCustomUDIValidators"></a> Creación de validadores de UDI personalizados  
 Los *validadores de UDI* son archivos DLL escritos en C++ que implementan la interfaz **IValidator**. El archivo DLL se registra con la biblioteca de validadores del diseñador del Asistente para UDI mediante la creación de un archivo de configuración del diseñador del Asistente para UDI (archivo .config) y se coloca en *carpeta_de_instalación*\Bin\Config (donde *carpeta_de_instalación* es la carpeta en la que instaló MDT).  

 **Para crear validadores de UDI personalizados**  

1.  Escriba código que cree una subclase de la clase **BaseValidator** e implemente los métodos siguientes:  

    -   **Init(IControl \*pControl, IWizardPageContainer \*pContainer, IStringProperties \*pProperties)**. El controlador de formulario llama al miembro **Init** para inicializar el validador. Este método debe llamar al método **Init** de la clase **BaseValidator**. Normalmente lee las propiedades establecidas para el validador del archivo de configuración del Asistente para UDI. Por ejemplo, el validador **InvalidCharactersValidator** recupera el valor de la propiedad **InvalidChars** mediante este método.  

    -   **IsValid**. El controlador de formulario llama a este método para ver si el control contiene texto válido. El siguiente es un ejemplo del método **IsValid** de un validador que valida que el campo no está vacío:  

        ```  
        BOOL IsValid(LPBSTR pMessage)  
        {  
            __super::IsValid(pMessage);  

            _bstr_t text;  
            m_pText->GetText(text.GetAddress());  
            return (text.length() > 0);  
        }  
        ```  

    -   **Init(IControl \*pControl, LPCTSTR message)**. El controlador de formulario llama a este miembro para cada pulsación de tecla y otros eventos para que el validador pueda validar el contenido del control y los mensajes actualizados en la parte inferior de la página del asistente (o borrarlos).  

     Normalmente, estos son los únicos métodos que es necesario invalidar. Pero en función del validador, es posible que sea necesario invalidar otros métodos de la subclase de la clase **BaseValidator** que se crea. Para obtener más información sobre estos otros métodos, vea la clase **BaseValidator**.  

2.  Escriba código que registre la clase de tareas personalizada con el generador del registro.  

3.  Compile la solución para la tarea personalizada.  

    > [!NOTE]
    >  Asegúrese de que la versión del archivo DLL que se crea es la misma plataforma de procesador que en la instalación de MDT. Por ejemplo, si instala la versión de 64 bits de MDT, compile una versión de 64 bits de la tarea de UDI personalizada.  

4.  Cree un elemento [Validator](#Validator) bajo el elemento **ValidatorLibrary** en el archivo de configuración del diseñador del Asistente para UDI similar al fragmento siguiente:  

    ```  
    <Validator   
    <Validator DLL="" Description="Must follow a pre-defined pattern" Type="Microsoft.Wizard.Validation.RegEx" Name="NamedPattern">  
       <Param Description="Enter the message you want displayed when the text in this field doesn't match the pattern:" Name="Message" DisplayName="Message"/>  
       <Param Description="The name of a pre-defined regular expression pattern. Must be Username, ComputerName, or Workgroup" Name="NamedPattern" DisplayName="Named Pattern"/>  
    </Validator>  
    ```  

    > [!WARNING]
    >  Todos los elementos [Validator](#Validator) deben incluir el parámetro **Mensaje**. Especifique todos los demás parámetros necesarios para el validador. Por ejemplo, en el extracto anterior, se usa el parámetro **NamedPattern** para especificar un parámetro para el nombre de un patrón de expresión regular predefinido.  

5.  Copie el archivo de configuración del diseñador del Asistente para UDI creado en el paso anterior en *carpeta_de_instalación*\Bin\Config (donde *carpeta_de_instalación* es la carpeta en la que instaló MDT).  

6.  Copie el archivo DLL de la tarea personalizada en *carpeta_de_instalación*\Templates\Distribution\Tools\plataforma (donde *carpeta_de_instalación* es la carpeta en la que instaló MDT y *plataforma* es **x86** para la versión de 32 bits o **x64** para la versión de 64 bits).  

## <a name="udi-wizard-reference"></a>Referencia del Asistente para UDI  

### <a name="wizard-page-components"></a>Componentes de la página del asistente  
 Se pueden usar varios componentes creados previamente para compilar las páginas personalizadas.  

#### <a name="creating-component-instances"></a>Creación de instancias de componente  
 El Asistente para UDI usa generadores de clases para crear instancias de objetos de forma automática. Estos generadores se registran con un registro de fábrica, mediante una cadena como la clave para el generador. Por ejemplo, el componente **WmiRepository** se identifica por la cadena "Microsoft.Wizard.WmiRepository", que está disponible en el archivo de encabezado IWmiRepository como **ID_WmiRepository**.  

 Suponiendo que la página se ha escrito como una subclase de **WizardPageImpl**, se puede crear una instancia de **WmiRepoistory** de esta forma:  

```  
PWmiRepository pWmi;  
CreateInstance(Container(), ID_WmiRepository, &pWmi);  
```  

 **CreateInstance** es una función de plantilla con seguridad de tipos para crear instancias de componentes. **PWmiRepository** es un puntero inteligente, por lo que controla automáticamente el recuento de referencias.  

#### <a name="creatable-components"></a>Componentes que se pueden crear  
 Hay un conjunto de componentes que se pueden registrar con el registro. Siempre se registra el primer conjunto de componentes, porque el archivo ejecutable principal del Asistente para UDI lo proporciona. Los otros dos conjuntos de componentes se proporcionan en archivos DLL "opcionales". Para que estos componentes estén disponibles, el archivo DLL debe indicarse en la sección **DLLs** del archivo XML .config. No es necesario que el código sepa qué archivo ejecutable contiene un componente específico.  

 La lista de identificadores de componente de los componentes (el nombre del componente es el mismo que el identificador pero sin la parte *ID_* inicial) que se registra con el registro de fábrica (definido en OSDSetupWizard) se muestra en la tabla 3.  

### <a name="table-3-component-ids"></a>Tabla 3. Id. de componente  

|**ID**|**Descripción**|  
|-|-|  
|ID_ACPowerTask|(ITask, IWizardComponent) Una tarea preparatoria que asegura que el equipo no se está ejecutando solo con la batería.|  
|ID_AppDiscoveryTask|(ITask, IWizardComponent) Una tarea especializada para detectar los elementos de software que se han instalado en el equipo.|  
|**ID_BackgroundTask**|(**IBackgroundTask**, **IWizardComponent**) Se puede usar para ejecutar una tarea en otro subproceso.|  
|**ID_CopyFilesTask**|(**ITask**, **IWizardComponent**) Una tarea para copiar uno o varios archivos.|  
|**ID_FormController**|(**IFormController**) Es probable que no sea necesario crear una instancia personalmente, dado que la página recibe la suya propia.|  
|**ID_InvalidCharactersValidator**|(**IValidator**) Garantiza que ningún campo de texto contiene caracteres de una lista proporcionada al validador.|  
|**ID_Logger**|(**ILogger**) Es probable que no sea necesario crear una instancia personalmente, dado que la página recibe un puntero a la instancia compartida.|  
|**ID_NonEmptyValidator**|(**IValidator**) Un validador que se asegura de que ningún campo esté vacío.|  
|**ID_PasswordValidator**|(**IValidator**) Un validador que se asegura de que dos campos de texto no tengan el mismo contenido.|  
|**ID_Regex**|(**IRegEx**) Evalúa las expresiones regulares en busca de coincidencias.|  
|**ID_RegExValidator**|(**IValidator**) Un validador que se valida con respecto a una expresión regular o un patrón conocido.|  
|**ID_SimpleStringProperties**|(**IStringProperties**, **ISimpleStringProperties**) Proporciona una manera sencilla de enviar las propiedades a las tareas sin usar XML.|  
|**ID_ShellExecuteTask**|(**ITask**, **IWizardComponent**) Ejecuta un programa externo.|  
|**ID_SummaryBag**|(**ISummaryBag**) Disponible indirectamente desde la página a través del método Form.|  
|**ID_TaskManager**|(**ITaskManager**, **IBackgroundCallback**, **IWizardComponent**) Administra la ejecución de un conjunto de tareas y la interfaz de usuario.|  
|**ID_WmiRepository**|(**IWmiRepository**, **IWizardComponent**) Permite ejecutar consultas de Instrumental de administración de Windows (WMI).|  
|**ID_IXmlDocument**|(**IXmlDocument**) Proporciona una fachada para leer y escribir documentos XML.|  

 El archivo OSDRefreshWizard.dll definido, las páginas compartidas y otros componentes de control se muestran en las tablas 4 y 5.  

### <a name="table-4-directory-controls"></a>Tabla 4. Controles de directorio  

|**ID**|**Descripción**|  
|-|-|  
|**ID_Directory**|(**IDirectory**) Una fachada para obtener la información de los directorios del sistema de archivos.|  

### <a name="table-5-defined-sharedpagesdll"></a>Tabla 5. Archivo SharedPages.dll definido  

|**ID**|**Descripción**|  
|-|-|  
|**ID_ADHelper**|(**IADHelper**) Proporciona una fachada para un conjunto limitado de características de Active Directory® Domain Services (AD DS).|  
|**ID_CpuInfo**|(**ICpuInfo**) Determina si la CPU es de 32 o 64 bits.|  
|**ID_DomainJoinValidator**|(**IDomainJoinValidator**) Tiene algunos métodos para comprobar si se permite a un conjunto de credenciales unirse a un dominio.|  
|**ID_DriveList**|(**IDriveList**, **IBindableList**, **IWizardComponent**) Usa WMI para obtener una lista de las unidades del equipo.|  
|**ID_WiredNetworkTask**|(**ITask**) Una tarea que comprueba si está conectado a la red con un adaptador de red con cable (en lugar de inalámbrico).|  

#### <a name="control-components"></a>Componentes de control  
 Con los controles en la página se interactúa a través de la función de plantilla **GetControlWrapper**, que proporciona acceso a uno de los tipos de componentes enumerados en la tabla 6.  

### <a name="table-6-components"></a>Tabla 6. Componentes  

|**Tipos de controles de cuadro de diálogo**|**Descripción**|  
|-|-|  
|**CONTROL_CHECK_BOX**|(**ICheckBox**) Una fachada para trabajar con controles de casilla.|  
|**CONTROL_COMBO_BOX**|(**IComboBox**) Una fachada para controles de cuadro combinado.|  
|**CONTROL_GENERIC**|(**IControl**) Permite trabajar con la mayoría de los tipos de controles para controlar el estado de habilitación y visibilidad.|  
|**CONTROL_LIST_VIEW**|(**IListView**) Una fachada que proporciona acceso a las características de un control de vista de lista.|  
|**CONTROL_PROGRESS_BAR**|(**IProgressBar**) Una fachada para trabajar con la posición de un control de barra de progreso.|  
|**CONTROL_RADIO_BUTTON**|(**IRadioButton**) Una fachada para trabajar con controles de botón de radio.|  
|**CONTROL_STATIC_TEXT**|(**IStaticText**) Una fachada que proporciona permiso de lectura y escritura para el texto de un control, como una etiqueta o un cuadro de texto.|  
|**CONTROL_TREE_VIEW**|(**ItreeView**) Una fachada para trabajar con un control de vista de árbol.|  

#### <a name="image-list-component"></a>Componente de lista de imágenes  
 Este componente es una fachada para un control **ImageList** de la página. Una lista de imágenes se crea a través de la interfaz **IListView** o **ITreeView**.  

#### <a name="formcontroller-component"></a>Componente FormController  
 El asistente crea automáticamente este componente y lo pasa a la página. Se puede tener acceso a él desde la página mediante el método **Form** que implementa la clase base **WizardPageImpl**.  

#### <a name="invalidcharactervalidator-component"></a>Componente InvalidCharacterValidator  
 Se trata de un tipo de validador que se puede incluir en una página. El identificador es **ID_InvalidCharactersValidator** (definido en IValidator.h), que tiene un valor de texto de "Microsoft.Wizard.Validation.InvalidChars."  

 Este validador busca una sola propiedad (un elemento **Setter** en el archivo .config) llamada **InvalidChars**, que es una lista de los caracteres que no están permitidos. Comprueba los caracteres en un cuadro de texto; si el texto contiene algún carácter de esta lista, el componente notifica el error.  

#### <a name="nonemptyvalidator-component"></a>Componente NonEmptyValidator  
 Se trata de un tipo de validador que se puede incluir en una página. El identificador es **ID_NonEmptyValidator** (definido en IValidator.h), que tiene un valor de texto de "Microsoft.Wizard.Validation.NonEmpty."  

 Este validador notifica el error si el cuadro de texto (o cualquier otro control que admita **IStaticText**) tiene un valor de cadena vacío.  

#### <a name="passwordvalidator-component"></a>Componente PasswordValidator  
 Se trata de un tipo de validador que se puede incluir en una página. El identificador es **ID_PasswordValidator** (definido en IValidator.h), que tiene un valor de texto de "Microsoft.Wizard.Validation.Password."  

 Este validador funciona con dos controles de texto diferentes (controles que admiten **IStaticText**) y notifica el error si no contienen los mismos valores. En otras palabras, se produce un error si los cuadros de texto **Contraseña** y **Confirmar contraseña** no coinciden.  

 Como este validador requiere dos controles, necesita más configuración que los demás validadores. Es posible que la configuración sea similar a la siguiente:  

```  
Form()->AddToGroup(IDC_EDIT_PASSWORD, IDC_EDIT_PASSWORD2);  
PValidator pValidator;  
Form()->AddValidator(IDC_EDIT_PASSWORD, ID_PasswordValidator, pMessage, &pValidator);  
PStaticText pPassword2;  
GetControlWrapper(View(), IDC_EDIT_PASSWORD2, CONTROL_STATIC_TEXT, &pPassword2);  
pValidator->SetProperty(0, pPassword2);  
```  

 En primer lugar, defina el control **Confirmar contraseña** como "secundario" del control **Contraseña**. De ese modo, si el controlador de formulario deshabilita el control **Contraseña**, también deshabilitará el control **Confirmar contraseña**. Después, agregue un validador de contraseña al formulario. Por último, proporcione el validador de contraseña con la interfaz al control **Confirmar contraseña**.  

 Debido al requisito de dos controles, debe usar código para configurar este validador en lugar del archivo XML .config.  

#### <a name="regexvalidator-component"></a>Componente RegExValidator  
 Se trata de un tipo de validador que se puede incluir en una página. El identificador es **ID_RegExValidator** (definido en IValidator.h), que tiene un valor de texto de "Microsoft.Wizard.Validation.RegEx."  

 Este validador compara el contenido de un control de texto (uno que admita **IStaticText**) con una expresión regular y devuelve un error si el texto no coincide con la expresión regular.  

 Como alternativa, se puede usar este validador con un patrón con nombre predefinido. Para usar una expresión regular, el código XML debe contener una propiedad de establecedor denominada **Pattern**. Si en su lugar quiere usar un patrón con nombre, use un establecedor denominado **PatrónConNombre** establecido en uno de los valores de la tabla 7.  

### <a name="table-7-named-pattern-setters"></a>Tabla 7. Establecedores de patrón con nombre  

|**Patrón**|**Descripción**|  
|-|-|  
|Nombre de usuario|Comprueba que el texto está en el formato dominio\usuario o user@domain.|  
|ComputerName|El nombre debe tener entre 1 y 15 caracteres de longitud y no puede incluir un juego de caracteres (por ejemplo : y ?).|  
|Grupo de trabajo|El nombre debe tener entre 1 y 15 caracteres de longitud y no puede incluir un juego de caracteres (por ejemplo =, + y ?).|  

#### <a name="factoryregistry-component"></a>Componente FactoryRegistry  
 Este componente realiza el seguimiento de todos los generadores de clases y servicios. Implementa la interfaz **IFactoryRegistry** y está disponible indirectamente a través del método **Container** de la página. Además, el registro carga los archivos DLL de extensión. Después de cargar un archivo DLL, el registro busca una función exportada denominada **RegisterFactories**. Debe implementar esta función y, en ella, registrar los generadores de clases para las páginas, tareas y validadores (y otros generadores de clases que quiera registrar). Este es un ejemplo del proyecto de ejemplo:  

```  
extern "C" __declspec(dllexport) void RegisterFactories(IFactoryRegistry *factories)  
{  
Register<LocationPageFactory>(ID_LocationPage, factories);  
}  
```  

#### <a name="logger-component"></a>Componente Logger  
 Este componente está disponible en la página a través del método **Logger** (implementado por **WizardPageImpl**). Este método se usa para escribir entradas en el archivo de registro. El contenido del archivo de registro es útil para diagnosticar problemas que los usuarios podrían tener al ejecutar el Asistente para UDI.  

#### <a name="propertybag-component"></a>Componente PropertyBag  
 El *contenedor de propiedades* es un contenedor para las variables de memoria. Está disponible en la página mediante **Container()->Properties()**. Las variables de memoria son útiles para pasar datos temporales entre páginas distintas.  

#### <a name="tsvariablebag-and-tsrepository-components"></a>Componentes TSRepository y TSVariableBag  
 El componente **TSVariableBag** permite leer y escribir variables de secuencia de tareas. Mantiene los valores en la memoria hasta que el usuario hace clic en **Finalizar** (de forma predeterminada). Se puede tener acceso al contenedor **TSVariable** a través del método **TSVariables** de la página (implementado por la clase base **WizardPageImpl**). Estos componentes registran todas las operaciones de lectura y escritura de las variables de secuencia de tareas.  

#### <a name="wmirepository-component"></a>Componente WmiRepository  
 Este componente proporciona una fachada para trabajar con consultas de WMI. Se puede llamar a la función auxiliar **CreateInstance** con **ID_WmiRepository** para obtener una instancia de este componente, que admite la interfaz **IWmiRepository**. Este componente devuelve los registros de resultados a través de la interfaz **IWmiIterator**.  

###  <a name="WizardPageHelperClasses"></a> Clases auxiliares de páginas del asistente  
 Se pueden crear páginas del Asistente para UDI personalizadas mediante las clases auxiliares integradas proporcionadas con el SDK de UDI. En la tabla 8 se muestran las clases auxiliares que se pueden usar para crear páginas del asistente personalizadas.  

### <a name="table-8-helper-classes"></a>Tabla 8. Clases auxiliares  

|**Clase auxiliar**|**Descripción**|  
|-|-|  
|[Clase ClassFactoryImpl](#ClassFactoryImplClass)|Se trata de una clase base útil para crear un generador de clases que después se puede registrar con el registro de fábrica.|  
|[Clase de plantilla Interface](#InterfaceTemplateClass)|Use esta clase de plantilla cuando quiera crear un componente que implemente más de una interfaz.|  
|[Clase de plantilla Path](#PathHelperClass)|Esta clase proporciona las operaciones comunes de archivos o directorios.|  
|[Clase de plantilla Pointer](#PointerTemplateClass)|Esta clase proporciona el recuento de referencias para la administración de la duración de los componentes COM. Es importante liberar las interfaces cuando haya terminado con ellas. Esta clase de plantilla controla automáticamente la duración.|  
|[Clase PUnknown](#PUnkownClass)|Esta clase es un puntero inteligente específicamente para la interfaz IUnknown. Para todas las demás interfaces, use la clase de plantilla Pointer.|  
|[Clase auxiliar StringUtil](#StringUtilHelperClass)|Esta clase proporciona métodos auxiliares que facilitan el trabajo con cadenas.|  
|[Clase de plantilla SubInterface](#SubInterfaceTemplateClass)|Esta clase base facilita la implementación de un componente que admite una interfaz que se hereda de otra interfaz.|  
|[Clase de plantilla UnknownImpl](#UnknownImplTemplateClass)|Esta clase controla la mayoría de los detalles de creación de un componente COM.|  
|[Clase de plantilla WizardComponent](#WizardComponentTemplateClass)|Esta clase base se usa para crear componentes que necesitan tener acceso a los servicios del asistente, como la creación y el registro de componentes.|  
|[Clase de plantilla WizardPageImpl](#WizardPageImplTemplateClass)|Esta clase base se debe usar como clase base para todas las páginas del asistente personalizadas.|  

####  <a name="ClassFactoryImplClass"></a> Clase ClassFactoryImpl  
 Se trata de una clase base útil para crear un generador de clases que después se puede registrar con el registro de fábrica.  

 El siguiente es un extracto del archivo LocationPage.h del proyecto de ejemplo para definir la clase **ClassFactoryImpl**.  

```  
#pragma once  

#include "ClassFactoryImpl.h"  

class LocationPageFactory :public ClassFactoryImpl  
{  
protected:  
    IUnknown *CreateNewInstance();  
};  
```  

 El siguiente es un extracto del archivo LocationPage.cpp de la página del asistente de ejemplo que se usa para definir el generador de clases de la página.  

```  
IUnknown *LocationPageFactory::CreateNewInstance()  
{  
    return static_cast<IWizardPage *>(new LocationPage);  
}  
```  

####  <a name="InterfaceTemplateClass"></a> Clase de plantilla Interface  
 Use esta clase de plantilla cuando quiera crear un componente que implemente más de una interfaz, por ejemplo:  

```  
classLocationPage :public Interface<IFieldCallback, WizardPageImpl<IDD_LOCATION_PAGE>>  
```  

 Este código crea una cadena de clases base que admite tanto **IFieldCalback** como las interfaces que admite **WizardPageImpl** (que resulta ser **IWizardPage**).  

####  <a name="PathHelperClass"></a> Clase de plantilla Path  
 Esta clase proporciona las operaciones comunes de archivos o directorios:  

```  
static inline std::wstring GetModulePath(HINSTANCE hModule)  
```  

 También devuelve la ruta de acceso completa al archivo .exe o .dll con el identificador de instancia que se proporciona a este método:  

```  
static inline std::wstring GetModuleFilename(HINSTANCE hModule)  
```  

 La clase devuelve la ruta de acceso completa y el nombre de archivo del archivo .exe o .dll con el identificador de instancia que se proporciona a este método:  

```  
static inline std::wstring GetDirecotryName(LPCWSTR fullName)  
```  

 . . . o bien la ruta de acceso sin el nombre de archivo:  

```  
static inline std::wstring GetFileName(LPCWSTR fullName)  
```  

 Dada una ruta de acceso con un nombre de archivo, la clase auxiliar Path devuelve solo el nombre de archivo:  

```  
static inline std::wstring Combine(LPCWSTR path, LPCWSTR name)  
```  

 Por último, la clase devuelve una cadena nueva que es la combinación del nombre de archivo y la ruta de acceso (o bien otra ruta de acceso).  

####  <a name="PointerTemplateClass"></a> Clase de plantilla Pointer  
 Esta clase se define en Pointer.h. Como los componentes COM usan el recuento de referencias para la administración de la duración, es importante liberar siempre las interfaces cuando se haya terminado con ellas. Microsoft proporciona una clase de plantilla que automáticamente controla la duración. Por ejemplo, si quiere un puntero inteligente para una interfaz XML, podría escribir algo parecido a esto:  

```  
Pointer<IXMLDOMNode> pNewChild  
pXmlDom->CreateNode(NODE_ELEMENT, L"MyElement", L"", &pNewChild);  
```  

 En la primera línea se define el puntero inteligente. En la segunda línea se muestra cómo recuperar un puntero inteligente a través de otra llamada. El operador **&** siempre libera una interfaz existente si contiene una y devuelve la dirección del puntero interno. Después de recuperar un puntero como este, la instancia de **Pointer** llama automáticamente a **Release** cuando la variable sale del ámbito. Microsoft recomienda el uso de punteros inteligentes en lugar de llamar manualmente a **AddRef** y **Release**.  

 Además, la clase de puntero inteligente **Pointer** llama a **QueryInterface** para recuperar automáticamente otras interfaces. Por ejemplo, cuando el registro de fábrica crea una instancia de un componente, tiene código similar al siguiente:  

```  
PWizardComponent pComp = pUnknown;  
if (pComp != nullptr)  
    pComp->SetContainer(m_pContainer);  
```  

 En la primera línea se llama a **QueryInterface** en segundo plano para solicitar la interfaz **IWizardComponent**. El puntero inteligente resultante será igual a **nullptr** si el componente no admite esa interfaz.  

####  <a name="PUnkownClass"></a> Clase PUnknown  
 Esta clase es un puntero inteligente específicamente para la interfaz **IUnknown**. Para todas las demás interfaces, use la clase de plantilla **Pointer**.  

####  <a name="StringUtilHelperClass"></a> Clase auxiliar StringUtil  
 Esta clase se define en Utilities.h y proporciona métodos auxiliares que facilitan el trabajo con cadenas:  

```  
static inline int CompareIgnore(LPCWSTR first, LPCWSTR second)  
```  

 Este método compara dos cadenas e ignora las mayúsculas y minúsculas (vea la tabla 9).  

### <a name="table-9-stringutil-helper-class"></a>Tabla 9. Clase auxiliar StringUtil  

|**Devuelve**|**Descripción**|  
|-|-|  
|**0**|Las cadenas coinciden, se ignoran las mayúsculas y minúsculas|  
|**<0**|Primera < segunda|  
|**>0**|Primera > segunda|  

 Este es un ejemplo:  

```  
static inline std::wstring Format(LPCWSTR input, int index, LPCWSTR value)  
static inline std::wstring Format(LPCWSTR input, int index, DWORD value)  
```  

 Estos métodos son similares a los métodos **Format** de Microsoft .NET en el sentido de que los parámetros tienen el formato **{0}**. Pero no aplican ningún formato a la entrada, solamente sustitución:  

```  
static inline std::wstring Printf(std::wstring format, I val)  
static inline std::wstring Printf(std::wstring format, I val1, J val2)  
static inline std::wstring Printf(std::wstring format, I val1, J val2, K val3)  
static inline std::wstring Printf(std::wstring format, I val1, J val2, K val3, L val4)  
```  

 Estos son contenedores para **StringCchPrintf** que devuelven una **wstring** de modo que no sea necesario asignar memoria para cadenas o búferes.  

####  <a name="SubInterfaceTemplateClass"></a> Clase de plantilla SubInterface  
 Esta clase base facilita la implementación de un componente que admite una interfaz que se hereda de otra interfaz. Por ejemplo, la interfaz **ICheckBox** se hereda de **IControl**. Aquí se muestra cómo se usa esta clase para definir **CheckBoxWrapper**:  

```  
classCheckBoxWrapper :public SubInterface<IControl, UnknownImpl<ICheckBox> >  
```  

 La interfaz base es el primer parámetro, mientras que la interfaz derivada es el segundo.  

####  <a name="UnknownImplTemplateClass"></a> Clase de plantilla UnknownImpl  
 Esta clase se define en UnknownImpl.h y controla la mayoría de los detalles de creación de un componente COM. Este es un ejemplo de cómo se podría usar esta clase base:  

```  
classDirectory :public UnknownImpl<IDirectory>  
```  

 Este código define una clase que admite la interfaz **IDirectory**.  

####  <a name="WizardComponentTemplateClass"></a> Clase de plantilla WizardComponent  
 Esta clase se define en IWizardComponent.h y es una clase base útil para crear componentes que necesitan tener acceso a los servicios del asistente, como la creación y el registro de componentes.  

 Por ejemplo, aquí se muestra cómo se define el componente **CopyFilesTask**:  

```  
classCopyFilesTask :public WizardComponent<ITask>  
{  
    ...  
```  

 El parámetro para esta clase de plantilla es la interfaz "principal" que se quiere usar para el componente, que en el caso de las tareas es **ITask**. El uso de **WizardComponent** significa que el componente admite la interfaz que se proporciona (**ITask** en este ejemplo) e **IWizardComponent**.  

 Siempre que se use el registro de generador de clases para crear un componente, el registro llama al método **IWizardComponent->SetContainer** del componente para proporcionarle acceso a los servicios del asistente.  

####  <a name="WizardPageImplTemplateClass"></a> Clase de plantilla WizardPageImpl  
 Use esta clase como clase base para las páginas personalizadas, por ejemplo:  

```  
class LocationPage :public WizardPageImpl<IDD_LOCATION_PAGE>  
```  

 El parámetro es el identificador de recurso para la plantilla de cuadro de diálogo.  

###  <a name="WizardPageInterfaces"></a> Interfaces de la página del asistente  
 El Asistente para UDI usa interfaces para tener acceso a los distintos controles en la página. En la página, se usa la función **GetControlWrapper** para recuperar un contenedor de control. Este es un ejemplo:  

```  
PStaticText pFormat;  
GetControlWrapper(View(), IDC_CHECK_PARTITION, CONTROL_STATIC_TEXT, &pFormat);  
```  

 En este caso, **PStaticText** es un puntero inteligente a la interfaz **IStaticText**. Los punteros inteligentes llaman automáticamente al método **Release()** de COM cuando salen del ámbito o se pasa la dirección de una variable (como **&pFormat**) a un método.  

#### <a name="iadhelper-interface"></a>Interfaz IADHelper  

```  
__interfaceIADHelper : IUnknown  
{  
    HRESULT Init(ILogger *pLogger);  
    HRESULT ValidLogon(LPCTSTR userName, LPCTSTR password, LPCTSTR domain);  
    HRESULT HasAccess(LPCTSTR username, LPCTSTR password, LPCTSTR domain, LPCTSTR computerName, LPCTSTR accountDomain);  
};  

```  

##### <a name="hresult-initilogger-plogger"></a>HRESULT Init(ILogger \*pLogger)  
 Inicialice este componente y páselo al registrador para que puede registrar información.  

##### <a name="hresultvalidlogonlpctstr-username-lpctstr-password-lpctstr-domain"></a>HRESULTValidLogon(LPCTSTR userName, LPCTSTR password, LPCTSTR domain)  
 Este método comprueba si un conjunto de credenciales es válido, como se muestra en la tabla 10.  

### <a name="table-10-hresultvalidlogon"></a>Tabla 10. HResultValidLogon  

|**HResult**|**Descripción**|  
|-|-|  
|S_OK|Las credenciales son válidas.|  
|S_FALSE|Las credenciales no son válidas.|  
|E_FAIL|No se pudo encontrar el controlador de dominio; compruebe los registros para obtener más información.|  

##### <a name="hresult-hasaccesslpctstr-username-lpctstr-password-lpctstr-domain-lpctstr-computername-lpctstr-accountdomain"></a>HRESULT HasAccess(LPCTSTR username, LPCTSTR password, LPCTSTR domain, LPCTSTR computerName, LPCTSTR accountDomain)  
 Este método comprueba si un conjunto de credenciales tiene acceso de lectura y escritura al objeto de equipo en AD DS, como se muestra en la tabla 11.  

### <a name="table-11-hresult-hasaccess"></a>Tabla 11. HResult HasAccess  

|**HRESULT**|**Descripción**|  
|-|-|  
|S_OK|El usuario tiene acceso.|  
|E_FAIL|El usuario no tiene acceso. Compruebe el archivo de registro para obtener más información.|  

#### <a name="ibackgroundtask-interface"></a>Interfaz IBackgroundTask  

```  
__interface IBackgroundTask : IUnknown  
{  
    HRESULT Init(ITask *pTask, int id, IBackgroundCallback *pCallback);  
    void Start(void);  
    BOOL Running(void);  
    HRESULT Wait(DWORD waitMilliseconds);  
    HRESULT Terminate(DWORD exitCode);  
    HRESULT GetExitCode(LPDWORD pCode, HRESULT *pHresult);  
    HRESULT Close(void);  
};  
```  

##### <a name="overview"></a>Información general  
 En la página **Progress** se usa esta clase para ejecutar tareas en un subproceso independiente. También se puede usar esta clase siempre que quiera realizar operaciones en un subproceso independiente. Las *tareas* son cualquier clase que admita la interfaz **ITask**.  

 Esta interfaz se implementa mediante el componente **ID_BackgroundTask** ("Microsoft.Wizard.BackgroundTask"), definido en la interfaz IBackgroundTask.h.  

##### <a name="hresult-inititask-ptask-int-id-ibackgroundcallback-pcallback"></a>HRESULT Init(ITask \*pTask, int id, IBackgroundCallback \*pCallback)  
 Esta interfaz inicializa el componente, como se muestra en la tabla 12.  

### <a name="table-12-hresult-init"></a>Tabla 12. HRESULT Init  

|**Parámetro**|**Descripción**|  
|-|-|  
|**pTask**|Puntero a la clase que contiene el código que se quiere ejecutar en otro subproceso.|  
|**Id**|Un número que se puede usar en el método **Finished** de la devolución de llamada para indicar qué tarea se ha terminado de ejecutar; es útil si se inician varias tareas con el mismo método de devolución de llamada.|  
|**pCallback**|Una clase que implementa el método **Finished**, que se llama cada vez que finaliza la ejecución de una tarea; la llamada al método **Finished** se realiza en el subproceso en segundo plano, no en el subproceso de interfaz de usuario.|  

##### <a name="void-startvoid"></a>void Start(void)  
 Este método inicia la tarea en un subproceso en segundo plano y devuelve los elementos que se muestran en la tabla 13.  

### <a name="table-13-return-background-thread"></a>Tabla 13. Devolución del subproceso en segundo plano  

|**Devuelve**|**Descripción**|  
|-|-|  
|**E_INVALIDARG**|La tarea ya se está ejecutando, por lo que se no puede iniciar ahora mismo.|  
|**E_FAIL**|Se produjo un error al iniciar el subproceso.|  
|**S_OK**|Se inició el subproceso.|  

##### <a name="bool-running"></a>BOOL Running()  
 Este método devuelve TRUE si la tarea en segundo plano se está ejecutando actualmente y FALSE si no se está ejecutando.  

##### <a name="hresult-waitdword-waitmilliseconds"></a>HRESULT Wait(DWORD waitMilliseconds)  
 Este método espera hasta que el subproceso deje de ejecutarse o haya transcurrido el número de milisegundos.  

##### <a name="hresult-terminatedword-exitcode"></a>HRESULT Terminate(DWORD exitCode)  
 Este método termina el subproceso que se está ejecutando (vea las tablas 14 y 15). Este proceso puede tardar un tiempo en finalizar después de que vuelva este método.  

### <a name="table-14-hresult-terminate-exit-code"></a>Tabla 14. Código de salida de HRESULT Terminate  

|**Parámetro**|**Descripción**|  
|-|-|  
|**exitCode**|El código de salida que se enviará al método de devolución de llamada Finished, que también estará disponible en el método **GetExitCode**.|  

### <a name="table-15-termination-codes"></a>Tabla 15. Códigos de terminación  

|**Devuelve**|**Descripción**|  
|-|-|  
|**E_FAIL**|No se pudo terminar la llamada.|  
|**S_OK**|La solicitud para terminar el subproceso se realizó correctamente.|  

##### <a name="hresult-getexitcodelpdword-pcode-hresult-phresult"></a>HRESULT GetExitCode(LPDWORD pCode, HRESULT \*pHresult)  
 Use este método para obtener los resultados de la ejecución de la tarea en el subproceso en segundo plano (vea la tabla 16).  

### <a name="table-16-result-codes"></a>Tabla 16. Código de resultado  

|**Parámetro**|**Descripción**|  
|-|-|  
|**pCode**|Puntero a un **DWORD** que se establecerá en la devolución o **nullptr** si no se necesita el valor devuelto. En la salida, este parámetro se establece en **STILL_ACTIVE** si se está ejecutando el subproceso, el código devuelto por el método **Execute** de la tarea o el valor pasado al método **Terminate** si se llamó a ese método.|  
|**pHresult**|Puntero a un **HRESULT** que se establecerá en la devolución o **nullptr** si no se necesita el valor **HRESULT**.|  

##### <a name="hresult-closevoid"></a>HRESULT Close(void)  
 Este método libera el subproceso en segundo plano. Devuelve **E_INVALIDARG** si el subproceso se está ejecutando actualmente y **S_OK** en caso contrario.  

#### <a name="icheckbox-interface"></a>Interfaz ICheckBox  

```  
__interface ICheckBox : IControl  
{  
    void Check(BOOL check);  
    BOOL IsButtonChecked();  
};  
```  

##### <a name="void-checkbool-check"></a>void Check(BOOL check)  
 Establezca el estado de activación de la casilla. Cuando el método es TRUE, la casilla se activa; si el método es FALSE, la casilla se desactiva.  

##### <a name="bool-isbuttonchecked"></a>BOOL IsButtonChecked()  
 Este método notifica el estado de activación actual de una casilla.  

#### <a name="icombobox-interface"></a>Interfaz IComboBox  

```  
__interface IComboBox : IControl  
{  
    HRESULT Bind([in] IBindableList *pList);  
    HRESULT Select(int index);  
    int Selected(void);  
    void Add([in] LPCTSTR caption);  
    HRESULT GetText([out, retval] LPBSTR pText);  
    void Clear();  
};  
```  

##### <a name="overview"></a>Información general  
 Esta interfaz se implementa mediante el componente **CheckBoxWrapper**. Una instancia de este componente se recupera mediante la función auxiliar **GetControlWrapper** con el tipo **CONTROL_COMBO_BOX**.  

##### <a name="hresult-bindin-ibindablelist-plist"></a>HRESULT Bind([in] IBindableList \*pList)  
 Use este método si tiene un origen de datos que implementa la interfaz **IBindableList**. El cuadro de lista inicializa el contenido con los títulos de esta lista.  

##### <a name="hresult-selectint-index"></a>HRESULT Select(int index)  
 Seleccione el elemento del cuadro combinado en el índice.  

##### <a name="int-selectedvoid"></a>int Selected(void)  
 Este método devuelve el índice del elemento seleccionado o **-1** si no se selecciona nada.  

##### <a name="void-addin-lpctstr-caption"></a>void Add([in] LPCTSTR título)  
 Agregar manualmente un elemento al cuadro combinado.  

##### <a name="hresult-gettextout-retval-lpbstr-ptext"></a>HRESULT GetText([out, retval] LPBSTR pText)  
 Recuperar la cadena del elemento seleccionado actualmente en el cuadro combinado.  

##### <a name="void-clear"></a>void Clear()  
 Quitar todos los elementos del cuadro combinado.  

#### <a name="icontrol-interface"></a>Interfaz IControl  

```  
__interface IControl : IUnknown  
{  
    HRESULT SetEnable(BOOL enable);  
    BOOL IsEnabled(void);  
    HRESULT SetVisible(BOOL visible);  
};  
```  

##### <a name="overview"></a>Información general  
 Esta interfaz se implementa mediante el componente **ControlWrapper**. Una instancia de este componente se recupera mediante la función auxiliar **GetControlWrapper** con el tipo **CONTROL_GENERIC**.  

##### <a name="hresult-setenablebool-enable"></a>HRESULT SetEnable(BOOL enable)  
 Habilitar o deshabilitar el control.  

##### <a name="bool-isenabledvoid"></a>BOOL IsEnabled(void)  
 Devuelve TRUE si el control está habilitado, FALSE si no lo está.  

##### <a name="hresult-setvisiblebool-visible"></a>HRESULT SetVisible(BOOL visible)  
 Mostrar u ocultar el control.  

#### <a name="icpuinfo-interface"></a>Interfaz ICpuInfo  

```  
__interface ICpuInfo : IUnknown  
{  
    BOOL Is64Bit(void);  
};  
```  

##### <a name="overview"></a>Información general  
 Esta interfaz se obtiene mediante la creación de un componente **ID_CpuInfo**. El único método notifica si la CPU es de 32 o 64 bits. Tenga en cuenta que si tiene un sistema operativo de 32 bits en un equipo de 64 bits, este método devuelve TRUE, porque solo notifica el ancho de la CPU (no el sistema operativo).  

##### <a name="idirectory-interface"></a>Interfaz IDirectory  

```  
__interface IDirectory : IUnknown  
{  
    BOOL FileExists(LPCWSTR name);  
    BOOL FindFirst([in] LPCWSTR name);  
    HRESULT FoundName([out, retval] LPBSTR name);  
    DWORD FoundAttributes(void);  
    BOOL FindNext(void);  
    void FinishFind(void);  
};  
```  

###### <a name="overview"></a>Información general  
 El componente **Directory**, que se crea con **ID_Directory**, proporciona una fachada para trabajar con directorios del sistema de archivos.  

###### <a name="bool-fileexistslpcwstr-name"></a>BOOL FileExists(LPCWSTR name)  
 Este método devuelve TRUE si existe un archivo con el nombre que se proporciona.  

###### <a name="bool-findfirstin-lpcwstr-name"></a>BOOL FindFirst([in] LPCWSTR name)  
 Este método busca una primera coincidencia para el nombre que se proporcione. Admite los caracteres comodín y devuelve tanto nombres de archivo como de directorio. El método devuelve TRUE si se encuentra una coincidencia, FALSE en caso contrario.  

###### <a name="hresult-foundnameout-retval-lpbstr-name"></a>HRESULT FoundName([out, retval] LPBSTR name)  
 Este método recupera el nombre del archivo encontrado con una llamada a **FindFirst** o **FindNext**.  

###### <a name="dword-foundattributesvoid"></a>DWORD FoundAttributes(void)  
 Este método devuelve el atributo del último directorio o archivo encontrado. Se puede usar código como el siguiente para comprobar si se trata de un directorio:  

```  
pDirectory->FoundAttributes() & FILE_ATTRIBUTE_DIRECTORY  
```  

###### <a name="bool-findnextvoid"></a>BOOL FindNext(void)  
 Buscar el siguiente. Este método devuelve TRUE si se encontró otra coincidencia, FALSE en caso contrario.  

###### <a name="void-finishfindvoid"></a>void FinishFind(void)  
 Este método libera los recursos que se usan para la operación de búsqueda.  

#### <a name="idomainjoinvalidator-interface"></a>Interfaz IDomainJoinValidator  

```  
__interface IDomainJoinValidator : IUnknown  
{  
    HRESULT Init(ILogger *pLogger, IWizardPageContainer *pContainer, IStaticText *pUsername, IStaticText *pPassword, IStaticText *pComputerName);  
    HRESULT IsUsernameValid(LPCWSTR domainName);  
    BOOL CanModifyComputerAdEntry(LPCWSTR domainName);  
};  
```  

##### <a name="overview"></a>Información general  
 Se puede obtener una instancia de esta interfaz mediante el valor **ID_DomainJoinValidator** de la función de plantilla **CreateInstance**.  

##### <a name="hresult-initilogger-plogger-iwizardpagecontainer-pcontainer-istatictext-pusername-istatictext-ppassword-istatictext-pcomputername"></a>HRESULT Init(ILogger \*pLogger, IWizardPageContainer \*pContainer, IStaticText \*pUsername, IStaticText \*pPassword, IStaticText \*pComputerName)  
 Inicialice la instancia, como se muestra en la tabla 17.  

### <a name="table-17-hresult-init---instance-initialization"></a>Tabla 17. HRESULT Init: inicialización de la instancia  

|**Parámetro**|**Descripción**|  
|-|-|  
|**pLogger**|La instancia del registrador, que está disponible en la página a través del método **Logger** de la página.|  
|**pContainer**|Pasa los resultados del método **Container** de la página.|  
|**pUsername**|El cuadro de texto que contiene el nombre de usuario que se va a validar.|  
|**pPassword**|El cuadro de texto que contiene la contraseña que se va a validar.|  
|**PComputerName**|El cuadro de texto que contiene el nombre del equipo que finalmente se unirá al dominio.|  

##### <a name="hresult-isusernamevalidlpcwstr-domainname"></a>HRESULT IsUsernameValid(LPCWSTR domainName)  
 Este método usa el método **IADHelper->ValidLogon** para realizar la operación. Vea ese método para obtener más información.  

##### <a name="bool-canmodifycomputeradentrylpcwstr-domainname"></a>BOOL CanModifyComputerAdEntry(LPCWSTR domainName)  
 Compruebe si el usuario tiene derechos para modificar la entrada del equipo. **IADHelper->HasAccess** realiza la mayor parte del trabajo. Si este método devuelve FALSE, compruebe el archivo de registro para obtener más información.  

#### <a name="idrivelist-interface"></a>Interfaz IDriveList  

```  
__interface IDriveList : IUnknown  
{  
    HRESULT Init(IWmiRepository *pWmi);  
    HRESULT SetWhereClause(LPCTSTR whereClause);  
    HRESULT SetMinimumDriveSize(__int64 size);  
    HRESULT Update(void);  
    HRESULT AddProperty(ENUM_DISK_QUERY_SECTION section, LPCTSTR propName, LPCTSTR propNameReturned);  

    size_t Count(void);  
    HRESULT GetProperty(size_t index, LPCTSTR propName,  LPVARIANT value);  
    HRESULT GetCaption(size_t index,  LPBSTR pCaption);  
}  
```  

##### <a name="hresult-initiwmirepository-pwmi"></a>HRESULT Init(IWmiRepository \*pWmi)  
 Llame a este método antes de llamar a cualquier otro componente. Debe crear un nuevo **WmiRepository** antes de llamar a este método.  

##### <a name="hresult-setwhereclauselpctstr-whereclause"></a>HRESULT SetWhereClause(LPCTSTR whereClause)  
 Este método permite agregar texto que aparecerá como una cláusula "where" en la consulta. Por ejemplo, la línea siguiente devuelve solo las unidades USB:  

```  
pDrives->SetWhereClause(L"WHERE InterfaceType='USB'");  
```  

##### <a name="hresult-setminimumdrivesizeint64-size"></a>HRESULT SetMinimumDriveSize(\__int64 size)  
 Establezca el tamaño de unidad mínimo, en bytes, de las unidades que se devolverán de la consulta.  

##### <a name="hresult-updatevoid"></a>HRESULT Update(void)  
 Ejecute la consulta. La lista de unidades disponibles después de llamar a este método se ordena por la letra de unidad.  

##### <a name="hresult-addpropertyenumdiskquerysection-section-lpctstr-propname-lpctstr-propnamereturned"></a>HRESULT AddProperty(ENUM_DISK_QUERY_SECTION section, LPCTSTR propName, LPCTSTR propNameReturned)  
 Este método agrega los nombres de propiedades adicionales que quiere que estén disponibles en los resultados de la consulta. Llame a este método antes de llamar a **Update**. En la tabla 18 se muestran tres de las propiedades útiles.  

### <a name="table-18-hresult-addproperty-useful-properties"></a>Tabla 18. HRESULT AddProperty: propiedades útiles  

|**Sección**|**Propiedad**|**Descripción**|  
|-|-|-|  
|**DISKQUERY_LOGICALDISK**|**Size**|El tamaño, en bytes, que se representa como una cadena.|  
|**DISKQUERY_DISKPARTITION**|**DiskIndex**|El número de disco como un entero, empezando por 0.|  
|**DISKQUERY_LOGICALDISK**|**VolumeName**|La etiqueta del volumen.|  

##### <a name="sizet-countvoid"></a>size_t Count(void)  
 El número de registros que devuelve la consulta. Llame a **Update** antes de llamar a este método.  

##### <a name="hresult-getpropertysizet-index-lpctstr-propname--lpvariant-value"></a>HRESULT GetProperty(size_t index, LPCTSTR propName,  LPVARIANT value)  
 Este método recupera el valor de una propiedad de los resultados de la consulta, como se muestra en la tabla 19.  

### <a name="table-19-hresult-getproperty"></a>Tabla 19. HRESULT GetProperty  

|**Parámetro**|**Descripción**|  
|-|-|  
|**Index**|Índice de base cero del registro del resultado.|  
|**propName**|Nombre de la propiedad, por ejemplo, "Tamaño".|  
|**Valor**|En la devolución, este parámetro contiene un valor de tipo variant de la propiedad.|  

##### <a name="hresult-getcaptionsizet-index--lpbstr-pcaption"></a>HRESULT GetCaption(size_t index,  LPBSTR pCaption)  
 Este método recupera el título para un registro que es el mismo que la propiedad **Caption**.  

#### <a name="iimagelist-interface"></a>Interfaz IImageList  

```  
__interface IImageList  
{  
    HRESULT CreateImageList(int width, int height, UINT flags);  
    HImageList GetImageList(void);  
    int AddImage(HInstance hInstance, int resourceId);  
};  
```  

##### <a name="overview"></a>Información general  
 Esta interfaz se implementa mediante el componente **ImageList**. Se recupera una instancia de este componente de la interfaz **IListView**.  

##### <a name="hresult-createimagelistint-width-int-height-uint-flags"></a>HRESULT CreateImageList(int width, int height, UINT flags)  
 Crea una lista de imágenes, administrada por este componente. Llame a este método solo una vez.  

##### <a name="himagelist-getimagelistvoid"></a>HImageList GetImageList(void)  
 Este método devuelve el identificador de la lista de imágenes en caso de que se necesiten realizar otras operaciones en la lista de imágenes.  

##### <a name="int-addimagehinstance-hinstance-int-resourceid"></a>int AddImage(HInstance hInstance, int resourceId)  
 Agregar una imagen a la lista de imágenes de un recurso, como se muestra en la tabla 20.  

### <a name="table-20-hresult-iimagelist-interface"></a>Tabla 20. Interfaz HRESULT IImageList  

|**Parámetro**|**Descripción**|  
|-|-|  
|**hInstance**|Identificador de instancia del módulo que contiene el recurso de mapa de bits.|  
|**resourceId**|Identificador del recurso que se va a cargar en la lista de imágenes.|  

#### <a name="ilistview-interface"></a>Interfaz IListView  

```  
__interface IListView : IControl  
{  
    int AddItem([in] LPCTSTR text);  
    int AddColumn(int width, [in] LPCTSTR text);  
    HRESULT SetSubItem(int index, int column, [in] LPCTSTR text);  
    int GetWidth(void);  
    void SetExtendedStyle(DWORD style);  
    int GetSelectedItem(void);  
    HRESULT SelectItem(int index);  
    BOOL IsItemChecked(int index);  
    int GetItemCount(void);  
    HRESULT CreateImageList(int width, int height, UINT flags);  
    int AddImage(HINSTANCE hInstance, int resourceId);  
    HRESULT SetImage(int index, int imageIndex);  
    HRESULT Clear(void);  
};  
```  

##### <a name="overview"></a>Información general  
 Esta interfaz se implementa mediante el componente **ControlWrapper**. Una instancia de este componente se recupera mediante la función auxiliar **GetControlWrapper** con el tipo **CONTROL_LIST_VIEW**.  

##### <a name="int-additemin-lpctstr-text"></a>int AddItem([in] LPCTSTR text)  
 Agregar una fila nueva al cuadro de lista. El método devuelve el índice del elemento recién agregado.  

##### <a name="int-addcolumnint-width-in-lpctstr-text"></a>int AddColumn(int width, [in] LPCTSTR text)  
 Agregar una columna a la vista de lista.  

##### <a name="hresult-setsubitemint-index-int-column-in-lpctstr-text"></a>HRESULT SetSubItem(int index, int column, [in] LPCTSTR text)  
 Establecer el texto en una columna que no sea la primera del cuadro de lista, como se muestra en la tabla 21.  

### <a name="table-21-hresult-setsubitem"></a>Tabla 21. HRESULT SetSubItem  

|**Parámetro**|**Descripción**|  
|-|-|  
|**índice**|El índice del elemento de lista que se quiere modificar.|  
|**columna**|El índice de la columna que se quiere actualizar; la primera columna se establece con **AddItem**, la segunda y las siguientes se establecen con este método.|  
|**texto**|La cadena que se va a mostrar en la columna.|  

##### <a name="int-getwidthvoid"></a>int GetWidth(void)  
 Este método devuelve el ancho del cuadro de texto completo.  

##### <a name="void-setextendedstyledword-style"></a>void SetExtendedStyle(DWORD style)  
 Este método permite establecer estilos extendidos en el cuadro de lista, por ejemplo:  

```  
m_pList->SetExtendedStyle(LVS_EX_FULLROWSELECT);  
```  

##### <a name="int-getselecteditemvoid"></a>int GetSelectedItem(void)  
 Este método devuelve el índice del elemento de vista de lista actualmente seleccionado.  

##### <a name="hresult-selectitemint-index"></a>HRESULT SelectItem(int index)  
 Establecer el elemento seleccionado en la lista en este índice.  

##### <a name="bool-isitemcheckedint-index"></a>BOOL IsItemChecked(int index)  
 Este método devuelve TRUE si se selecciona un elemento de la lista. Este método requiere llamar a **SetExtendedStyle** para establecer el estilo de la casilla.  

##### <a name="int-getitemcountvoid"></a>int GetItemCount(void)  
 Este método devuelve el número de elementos de la vista de lista.  

##### <a name="hresult-createimagelistint-width-int-height-uint-flags"></a>HRESULT CreateImageList(int width, int height, UINT flags)  
 Crear una lista de imágenes y adjuntarla a la vista de lista.  

##### <a name="int-addimagehinstance-hinstance-int-resourceid"></a>int AddImage(HINSTANCE hInstance, int resourceId)  
 Agregar una imagen a la lista de imágenes de la vista de lista. Primero se debe llamar a **CreateImageList**.  

##### <a name="hresult-setimageint-index-int-imageindex"></a>HRESULT SetImage(int index, int imageIndex)  
 Establecer la imagen que se mostrará en el lado izquierdo de un elemento de vista de lista concreto.  

##### <a name="hresult-clearvoid"></a>HRESULT Clear(void)  
 Quitar todos los elementos de la vista de lista.  

#### <a name="iprogressbar-interface"></a>Interfaz IProgressBar  

```  
__interface IProgressBar : IControl  
{  
    HRESULT SetPercentage(int position);  
    int GetPercentage(void);  
};  
```  

##### <a name="overview"></a>Información general  
 Esta interfaz se implementa mediante el componente **ProgressBarWrapper**. Una instancia de este componente se recupera mediante la función auxiliar **GetControlWrapper** con el tipo **CONTROL_PROGRESS_BAR**.  

##### <a name="hresult-setpercentageint-position"></a>HRESULT SetPercentage(int posición)  
 Establezca la posición de la barra de progreso mediante un número comprendido entre 0 y 100. De forma predeterminada, las barras de progreso nuevas de Win32® tienen un intervalo máximo de 100.  

##### <a name="int-getpercentagevoid"></a>int GetPercentage(void)  
 Este método devuelve la posición actual de la barra de progreso.  

#### <a name="iradiobutton-interface"></a>Interfaz IRadioButton  

```  
__interface IRadioButton : IControl  
{  
public:  
    void SetGroup(int firstId, int lastId);  
    void CheckRadio(int id);  
    BOOL IsButtonChecked(int id);  
    void EnableRadio(int id, BOOL enable);  
};  
```  

##### <a name="overview"></a>Información general  
 Esta interfaz se implementa mediante el componente **RadioButtonWrapper**. Una instancia de este componente se recupera mediante la función auxiliar **GetControlWrapper** con el tipo **CONTROL_RADIO_BUTTON**.  

##### <a name="void-setgroupint-firstid-int-lastid"></a>void SetGroup(int primerId, int segundoId)  
 Proporcione al contenedor el intervalo de botones de radio que se deben tratar como un grupo. Llame a este método antes de llamar a **CheckRadio**.  

##### <a name="void-checkradioint-id"></a>void CheckRadio(int id)  
 Establezca el botón de radio específico para que sea el único en el grupo de botones de radio seleccionado. Llame a **SetGroup** antes de llamar a este método.  

##### <a name="bool-isbuttoncheckedint-id"></a>BOOL IsButtonChecked(int id)  
 Este método devuelve TRUE si el botón de radio está seleccionado, FALSE en caso contrario.  

##### <a name="void-enableradioint-id-bool-enable"></a>void EnableRadio(int id, BOOL enable)  
 Este método habilita o deshabilita un botón de radio.  

#### <a name="istatictext-interface"></a>Interfaz IStaticText  

```  
__interface IStaticText : IControl  
{  
    HRESULT SetText([in] LPCTSTR pText);  
    HRESULT GetText([out, retval] LPBSTR pText);  
};  
```  

##### <a name="overview"></a>Información general  
 Esta interfaz se implementa mediante el componente **StaticTextWrapper**. Una instancia de este componente se recupera mediante la función auxiliar **GetControlWrapper** con el tipo **CONTROL_STATIC_TEXT**.  

##### <a name="hresult-settextin-lpctstr-ptext"></a>HRESULT SetText([in] LPCTSTR pText)  
 Establecer el texto del control.  

##### <a name="hresult-gettextout-retval-lpbstr-ptext"></a>HRESULT GetText([out, retval] LPBSTR pText)  
 Este método devuelve el valor actual del texto del control.  

####  <a name="ITaskinterface"></a> Interfaz ITask  

```  
__interface IControl : IUnknown  
{  
    HRESULT Init(IStringProperties *pProperties, ISettingsProperties *pTaskSettings);  
    HRESULT Execute(LPDWORD pReturnCode);  
};  
```  

 Implemente esta interfaz si quiere que el componente esté disponible como una tarea en la página preparatoria o si quiere usar el componente **BackgroundTask** para realizar el trabajo en un subproceso en segundo plano.  

 Estos son los componentes que implementan la interfaz **ITask**:  

-   ID_ShellExecuteTask, L"Microsoft.Wizard.ShellExecuteTask"  

-   ID_CopyFilesTask, L"Microsoft.Wizard.CopyFilesTask"  

-   ID_ACPowerTask, L"Microsoft.OSDRefresh.ACPowerTask"  

-   ID_WiredNetworkTask, L"Microsoft.SharedPages.WiredNetworkTask"  

##### <a name="init"></a>Inicializar  

```  
HRESULT Init(IStringProperties *pProperties, ISettingsProperties *pTaskSettings)  
```  

 Si está escribiendo una tarea para la página preparatoria, llame a este método para inicializar la tarea. El archivo .config contiene XML que podría tener este aspecto:  

```  
<Task DisplayName="Check Windows Scripting Host" Type="Microsoft.Wizard.ShellExecuteTask">  
  <Setter Property="filename">%windir%\system32\cscript.exe</Setter>  
  <Setter Property="parameters">Preflight\OSDCheckWSH.vbs</Setter>  
  <Setter Property="BitmapFilename">images\WinScriptHost.bmp</Setter>  
  <ExitCodes>  
    <ExitCode State="Success" Type="0" Value="0" Text="" />  
    <ExitCode State="Error" Type="-1" Value="*" Text="Windows Scripting Host not installed." />  
  </ExitCodes>  
</Task>  
```  

 El parámetro **pProperties** proporciona acceso a los tres valores de establecedor, mientras que el parámetro **pTaskSettings** proporciona acceso al elemento **Task** y los elementos secundarios. La mayoría de las tareas solo necesitan leer los datos del parámetro **pProperties**.  

#####  <a name="Execute"></a> Execute  

```  
HRESULT Execute(LPDWORD pReturnCode)  
```  

 Aquí es donde se escribe el código que realiza la tarea. Este método debe devolver **S_OK** si no hubo errores y puede devolver otro **HRESULT** si se produjo un error mientras se ejecutaba la tarea. Los valores distintos de **S_OK** que devuelve este método se hacen coincidir hasta los elementos <Error\> de la sección <ExitCodes\> si se usa la página preparatoria.  

 El parámetro **pReturnCode** debe estar actualizado con un número que indique el estado de la tarea. La página preparatoria hace coincidir estos valores con los elementos <ExitCode\>.  

#### <a name="itreeview-interface"></a>Interfaz ITreeView  

```  
__interface ITreeView : IControl  
{  
    void EnableCheckboxes(void);  
    HRESULT CreateImageList(int width, int height, UINT flags);  
    int AddImage(HINSTANCE hInstance, int resourceId);  

    HTREEITEM AddItem(LPCTSTR text, HTREEITEM hParent = NULL);  
    void SetImage(HTREEITEM item, int image, int expandImage);  

    void Clear(void);  
    BOOL SetFirstVisible(HTREEITEM item);  
    BOOL SelectItem(HTREEITEM item);  
    void CheckItem(HTREEITEM item, UINT checkState);  
    HTREEITEM SelectedItem(void);  
    int SetItemHeight(SHORT height);  
    HRESULT EnableItem(HTREEITEM item, BOOL enable);  
    void Expand(HTREEITEM hItem, BOOL expand);  

    HTREEITEM GetChild(HTREEITEM hParent);  
    HTREEITEM GetParent(HTREEITEM hNode);  
    HTREEITEM GetNextItem(HTREEITEM hPrevious);  

    UINT IsChecked(HTREEITEM item);  
    BOOL IsEnabled(HTREEITEM item);  

    INT_PTR CommonControlEvent(WORD controlId, void* pInfo, BOOL *pCancel);  
    HRESULT SetEventHandler(ITreeViewEvent *pEventHandler);  

    void SetSelectedBackColor(COLORREF color);  
};  
```  

##### <a name="overview"></a>Información general  
 Esta interfaz se implementa mediante el componente **TreeViewWrapper**. Una instancia de este componente se recupera mediante la función auxiliar **GetControlWrapper** con el tipo **CONTROL_TREE_VIEW**.  

##### <a name="void-enablecheckboxesvoid"></a>void EnableCheckboxes(void)  
 Este método activa las casillas del control de vista de árbol estableciendo el estilo **TVS_CHECKBOXES**.  

##### <a name="hresult-createimagelistint-width-int-height-uint-flags"></a>HRESULT CreateImageList(int width, int height, UINT flags)  
 Agregar una lista de imágenes nueva al control de vista de árbol. El parámetro **marcas** se pasa en la llamada a la función **ImageList_Create** de Win32.  

##### <a name="int-addimagehinstance-hinstance-int-resourceid"></a>int AddImage(HINSTANCE hInstance, int resourceId)  
 Agregar una imagen a la lista de imágenes de un recurso (**resourceId**) en el módulo con el identificador de instancia **hInstance**.  

##### <a name="htreeitem-additemlpctstr-text-htreeitem-hparent--null"></a>HTREEITEM AddItem(LPCTSTR text, HTREEITEM hParent = NULL)  
 Agregar un nodo a la vista de árbol. El nodo nuevo se agregará en el nivel superior si **hParent** es NULL. En caso contrario, proporcione el identificador al elemento primario donde quiera agregar el elemento nuevo. Este método devuelve el identificador al elemento nuevo.  

##### <a name="void-setimagehtreeitem-item-int-image-int-expandimage"></a>void SetImage(HTREEITEM item, int image, int expandImage)  
 Establezca la imagen que se va a usar para un elemento de vista de árbol. Se puede establecer la imagen normal y la de expansión.  

##### <a name="void-clearvoid"></a>void Clear(void)  
 Quitar todos los elementos de la vista de árbol.  

##### <a name="bool-setfirstvisiblehtreeitem-item"></a>BOOL SetFirstVisible(HTREEITEM item)  
 Asegúrese de que el elemento de vista de árbol es visible. La vista de árbol se desplazará si es necesario para que este elemento sea visible.  

##### <a name="bool-selectitemhtreeitem-item"></a>BOOL SelectItem(HTREEITEM item)  
 Establece el elemento seleccionado actualmente en el elemento que se proporciona. Se puede llamar a **SetFirstVisible** después de esta opción para asegurarse de que el elemento recién seleccionado es visible.  

##### <a name="void-checkitemhtreeitem-item-uint-checkstate"></a>void CheckItem(HTREEITEM item, UINT checkState)  
 Básicamente, el método establece la imagen que se va a mostrar para la casilla en la vista de árbol. Estas imágenes se encuentran en otro control **ImageList** administrado por la vista de árbol. De forma predeterminada, esta lista de imágenes contiene tres imágenes, que se muestran en la tabla 22.  

### <a name="table-22void-checkitem-image-list-default"></a>Tabla 22. Lista predeterminada de imágenes de void CheckItem  

|**checkState**|**Descripción**|  
|-|-|  
|**0**|En blanco|  
|**1**|Desactivado|  
|**2**|Seleccionado|  

##### <a name="htreeitem-selecteditemvoid"></a>HTREEITEM SelectedItem(void)  
 Este método devuelve el identificador del elemento de vista de árbol seleccionado actualmente.  

##### <a name="int-setitemheightshort-height"></a>int SetItemHeight(SHORT height)  
 Este método establece el alto en píxeles de todos los elementos del control de vista de árbol. Devuelve el alto anterior en píxeles.  

##### <a name="hresult-enableitemhtreeitem-item-bool-enable"></a>HRESULT EnableItem(HTREEITEM item, BOOL enable)  
 Este método habilita o deshabilita un único elemento en el árbol. Deshabilitar un elemento con elementos secundarios no deshabilitará los elementos secundarios.  

##### <a name="void-expandhtreeitem-hitem-bool-expand"></a>void Expand(HTREEITEM hItem, BOOL expand)  
 Este método expande o contrae un nodo en el árbol.  

##### <a name="htreeitem-getchildhtreeitem-hparent"></a>HTREEITEM GetChild(HTREEITEM hParent)  
 Este método devuelve el primer elemento secundario de un elemento de vista de árbol o NULL si no hay elementos secundarios.  

##### <a name="htreeitem-getparenthtreeitem-hnode"></a>HTREEITEM GetParent(HTREEITEM hNode)  
 Este método devuelve el identificador del elemento primario de un nodo en la vista de árbol o NULL si el nodo está en el nivel superior.  

##### <a name="htreeitem-getnextitemhtreeitem-hprevious"></a>HTREEITEM GetNextItem(HTREEITEM hPrevious)  
 También se puede llamar a este método con un identificador que **GetChild** devuelve para recorrer en iteración todos los elementos secundarios de un nodo. Este método devuelve el siguiente elemento relacionado en el árbol que comparte al mismo elemento primario.  

##### <a name="uint-ischeckedhtreeitem-item"></a>UINT IsChecked(HTREEITEM item)  
 Este método devuelve **0** si el nodo de la vista de árbol no está seleccionado y **1** si lo está.  

##### <a name="bool-isenabledhtreeitem-item"></a>BOOL IsEnabled(HTREEITEM item)  
 Este método devuelve TRUE si el nodo de la vista de árbol está habilitado, FALSE en caso contrario.  

##### <a name="intptr-commoncontroleventword-controlid-void-pinfo-bool-pcancel"></a>INT_PTR CommonControlEvent(WORD Idcontrol, void* pInfo, BOOL \*pCancel)  
 Este método es solo para uso interno.  

##### <a name="hresult-seteventhandleritreeviewevent-peventhandler"></a>HRESULT SetEventHandler(ITreeViewEvent \*pEventHandler)  
 Llame a este método si quiere recibir una notificación cuando cambie el elemento seleccionado o el usuario cambie el estado de activación de un elemento de vista de árbol. Para recibir estas devoluciones de llamada debe implementar **ITreeViewEvent** en el componente.  

##### <a name="void-setselectedbackcolorcolorref-color"></a>void SetSelectedBackColor(COLORREF color)  
 Establecer el color de fondo que se usa para el elemento seleccionado.  

#### <a name="iwmiiteration-interface"></a>Interfaz IWmiIteration  

```  
__interface IWmiIterator : IUnknown  
{  
    HRESULT Next(void);  
    HRESULT GetProperty(LPCTSTR propertyName, [out] LPVARIANT pValue);  
};  
```  

##### <a name="overview"></a>Información general  
 Esta interfaz se suele usar, junto con **IWmiRepository**, cuando se trabaja con llamadas WMI. La interfaz **IWmiIteration** permite recorrer en iteración los valores que devuelve una consulta.  

##### <a name="hresult-nextvoid"></a>HRESULT Next(void)  
 Desplazarse al elemento siguiente en los resultados de consulta, como se muestra en la tabla 23.  

### <a name="table-23-hresult-nextvoid-query-returns"></a>Tabla 23. Resultados de consulta de HRESULT Next(void)  

|**HRRESULT**|**Descripción**|  
|-|-|  
|**S_OK**|Desplazamiento al siguiente resultado; se puede usar **GetProperty** para recuperar las propiedades de ese resultado.|  
|**S_FALSE**|En la lista no hay más elementos.|  
|**E_NOT_SET**|No hay resultados de consulta.|  

##### <a name="hresult-getpropertylpctstr-propertyname-out-lpvariant-pvalue"></a>HRESULT GetProperty(LPCTSTR propertyName, [out] LPVARIANT pValue)  
 Este método recupera el valor de una propiedad del registro de resultados actual, como se muestra en las tablas 24 y 25.  

### <a name="table-24-hresult-getproperty"></a>Tabla 24. HRESULT GetProperty  

|**Parámetro**|**Descripción**|  
|-|-|  
|**propertyName**|Nombre de la propiedad que se quiere recuperar.|  
|**pValue**|Apunta a una estructura VARIANT que, en la devolución, contiene el valor de propiedad.|  

### <a name="table-25-hresult-getproperty-result"></a>Tabla 25. Resultado de HRESULT GetProperty  

|**HRESULT**|**Descripción**|  
|-|-|  
|**S_OK**|Se ha recuperado el valor de propiedad.|  
|**WBEM_E_NOT_FOUND**|No hay ninguna propiedad con el nombre.|  
|**E_NOT_VALID_STATE**|No hay ningún registro actual.|  

> [!NOTE]
>  El método **GetProperty** puede devolver otros códigos de error de WMI que no aparecen en la tabla 25. Los valores enumerados son los resultados comunes que se devuelven.  

#### <a name="iwmirepository-interface"></a>Interfaz IWmiRepository  

```  
__interface IWmiRepository : IUnknown  
{  
    HRESULT SetNamespace(LPCWSTR namespaceName);  
    HRESULT ExecQuery(LPCWSTR query, [out] IWmiIterator **ppIterator);  
};  
```  

##### <a name="overview"></a>Información general  
 Esta interfaz se implementa mediante el componente **WmiRepository** (**ID_WmiRepository**).  

##### <a name="hresult-setnamespacelpcwstr-namespacename"></a>HRESULT SetNamespace(LPCWSTR namespaceName)  
 Este método establece el espacio de nombres de WMI que se va a usar para la consulta. Llame a este método antes de llamar a **ExecQuery**. Si no se llama a este método, el espacio de nombres será root\cimv2. Este método siempre devuelve **S_OK**.  

##### <a name="hresult-execquerylpcwstr-query-out-iwmiiterator-ppiterator"></a>HRESULT ExecQuery(LPCWSTR consulta, [out] IWmiIterator **ppIterator)  
 Ejecutar una consulta en el espacio de nombres de WMI establecido con una llamada a **SetNamespace**, como se muestra en las tablas 26 y 27.  

### <a name="table-26-hresult-execquery"></a>Tabla 26. HRESULT ExecQuery  

|**Parámetro**|**Descripción**|  
|-|-|  
|**Consulta**|La cadena para la consulta WMI que se quiere ejecutar.|  
|**ppIterator**|Pasar un puntero a un puntero de interfaz, que, en la devolución, se rellenará con una interfaz, lo que proporciona acceso a los resultados de consulta.|  

### <a name="table-27-hresult-query-result"></a>Tabla 27. Resultado de consulta HRESULT  

|**HRESULT**|**Descripción**|  
|-|-|  
|**S_OK**|Consulta correcta.|  
|**Other**|Si la consulta no es correcta, devuelve un **HRESULT** de WMI.|  

#### <a name="iformcontroller-interface"></a>Interfaz IFormController  

```  
__interface IFormController : IUnknown  
{  
    Init(IWizardPageView *pView, IWizardPageContainer *pContainer);  
    SetPageInfo(ISettingsProperties *pPageInfo);  

    Validate(void);  

    AddToGroup(int groupControlId, int controlId);  
    UpdateCheckGroup(int groupControlId);  
    AddValidator(int controlId, IValidator *pValidator, IControl *pCOntrol = 0);  

    AddValidator(int controlId, LPCWSTR validatorId, LPCWSTR message, IValidator **ppValidator = nullptr);  
    DisableValidation(int controlId, BOOL disable);  

    AddField(LPCWSTR fieldName, int controlId, BOOL suppressLog, DialogControlTypes type);  
    AddRadioGroup(LPCWSTR groupName, int radioControlId);  
    EnableRadioGroup(LPCWSTR groupName, BOOL enable);  
    InitFields(IFieldCallback *pFieldCallback = nullptr);  
    SaveFields(IFieldCallback *pFieldCallback = nullptr);  
    BOOL IsFieldDisabled(int controlId);  

    InitSection(LPCWSTR key, LPCWSTR sectionCaption);  
    AddSummaryItem(LPCWSTR first, LPCWSTR second);  
    SuppressLogValue(LPCWSTR tsVariableName);  
    SaveText(int controlId, LPCWSTR tsVariableName, LPCWSTR summaryCaption);  
    LoadText(int controlId, LPCWSTR tsVariableName);  

    void ControlEvent(WORD eventId, WORD controlId);  
    BOOL IsValid(void);  
 };  
```  

##### <a name="overview"></a>Información general  
 Cada página del Asistente para UDI tiene su propio controlador de formulario que implementa esta interfaz. Use este controlador para conectar los datos de campo del archivo .config de XML a los controles de la página. Después, el controlador de formulario controla automáticamente muchos de los detalles.  

#####  <a name="SettingUptheForm"></a> Configuración del formulario  
 Por lo general, el controlador de formulario se configura en el método **OnWindowCreated** de la página. Esto implica normalmente llamar a los métodos que se muestran en la tabla 28.  

### <a name="table-28-onwindowcreated-method"></a>Tabla 28. OnWindowCreated (método)  

|**Método**|**Descripción**|  
|-|-|  
|**Init**|Inicializa el controlador de formulario.|  
|**AddField**|Proporciona una conexión entre un campo del archivo .config de XML que es un nombre de cadena y un control del cuadro de diálogo de la página que es un Id.|  
|**AddRadioGroup**|Se usa para conectar un botón de radio a un grupo y a un control del cuadro de diálogo|  
|**AddToGroup**|Permite "convertir en secundarios" los controles que están habilitados o deshabilitados junto con su elemento primario o en función del botón de radio que está seleccionado|  
|**InitFields**|Se llama después de llamar a todos los métodos **Add** para configurar el formulario.|  
|**Validate**|Realiza la validación inicial.|  

##### <a name="processing-form-events"></a>Procesamiento de eventos de formulario  
 Agregue la llamada siguiente al método **OnControlEvent**:  

```  
Form()->ControlEvent(eventId, controlId);  
```  

 Esta llamada pasa los eventos al controlador de formulario para poder procesar eventos relacionados con el formulario.  

##### <a name="save-form-data"></a>Guardar datos de formulario  
 En el método **OnNextClicked**, llame a los métodos de formulario que se muestran en la tabla 29.  

### <a name="table-29-onnextclicked-method"></a>Tabla 29. OnNextClicked (método)  

|**Método**|**Descripción**|  
|-|-|  
|**InitSection**|Proporciona el nombre de la sección que se mostrará en la página **Resumen** para esta página|  
|**SaveFields**|Guardar los valores de campo en variables de secuencia de tareas y la página **Resumen**.|  

#####  <a name="Init"></a> Init  

```  
HRESULT Init(IWizardPageView *pView, IWizardPageContainer *pContainer)  
```  

 Se suele llamar a este método al principio del método **OnWindowCreated** de la página. El comando debe tener un aspecto similar al siguiente:  

```  
Form()->Init(View(), Container());  
```  

##### <a name="setpageinfo"></a>SetPageInfo  

```  
HRESULT SetPageInfo(ISettingsProperties *pPageInfo)  
```  

 Este método se llama de manera interna y no lo debe llamar usted mismo. Proporciona el XML de la página al controlador de formulario.  

##### <a name="validate"></a>Validate  

```  
HRESULT Validate(void)  
```  

 Este método ejecuta todos los validadores adjuntados a los controles. Si un validador no pasa, el controlador de formulario muestra un mensaje de advertencia y deshabilita el botón **Siguiente** y, después, deja de procesar los validadores. Normalmente, solo se necesita llamar a este método al final del método **OnWindowCreated**; siempre devuelve **S_OK**.  

##### <a name="addtogroup"></a>AddToGroup  

```  
AddToGroup(int groupControlId, int controlId)  
```  

 Este método agrega un control como "secundario" de una casilla o un botón de radio, como se muestra en la tabla 30. Todos los controles secundarios de este tipo se deshabilitarán cuando el control primario no se selecciona. El método siempre devuelve **S_OK**.  

### <a name="table-30-addtogroup"></a>Tabla 30. AddToGroup  

|**Parámetro**|**Descripción**|  
|-|-|  
|**idGrupoControles**|El identificador de la casilla o el botón de radio que va a controlar el estado de habilitación del control secundario.|  
|**idControl**|El identificador del control que se quiere agregar como elemento secundario.|  

##### <a name="updatecheckgroup"></a>UpdateCheckGroup  

```  
HRESULT UpdateCheckGroup(int groupControlId)  
```  

 Este método actualiza el estado de habilitación o deshabilitación de los controles secundarios de un grupo en función del estado del control primario. Por lo general, no es necesario llamar a este método personalmente, porque el controlador de formulario lo llama de manera automática.  

##### <a name="addvalidator"></a>AddValidator  

```  
HRESULT AddValidator(int controlId, IValidator *pValidator, IControl *pControl = 0)  
```  

 Llame a este método solo si tiene un validador que quiere crear en el código en lugar de hacerlo con el código XML. Este método siempre devuelve **S_OK**.  

##### <a name="addvalidator"></a>AddValidator  

```  
HRESULT AddValidator(int controlId, LPCWSTR validatorId, LPCWSTR message, IValidator **ppValidator = nullptr)  
```  

 Llame a este método solo si tiene un validador que quiere crear en el código en lugar de hacerlo con el código XML.  

##### <a name="disablevalidation"></a>DisableValidation  

```  
HRESULT DisableValidation(int controlId, BOOL disable)  
```  

 Llame a este método para deshabilitar explícitamente el validador para un control o restaurar la validación normal, como se muestra en la tabla 31. Este método resulta útil, por ejemplo, cuando hay que habilitar o deshabilitar reglas para los controles que no están cubiertos por la validación del formulario y es necesario deshabilitar la validación de un control. En otras palabras, este método no se llamará normalmente. Este método siempre devuelve **S_OK**.  

### <a name="table-31-hresult-disablevalidation"></a>Tabla 31. HRESULT DisableValidation  

|**Parámetro**|**Descripción**|  
|-|-|  
|**idControl**|El control para el que se quiere habilitar o deshabilitar la validación.|  
|**Deshabilitar**|Se establece en TRUE para deshabilitar la validación y en FALSE para restaurar la validación normal.|  

#####  <a name="AddField"></a> AddField  

```  
HRESULT AddField(LPCWSTR fieldName, int controlId, BOOL suppressLog, DialogControlTypes type)  
```  

 Agregue una asignación de control entre el nombre de un elemento **Field** del archivo .config de XML y el identificador de control del cuadro de diálogo de la página, como se muestra en la tabla 32. Debe llamar a este método antes de llamar a **InitFields**, porque **InitFields** usa esta información. Este método siempre devuelve **S_OK**.  

### <a name="table-32-hresult-addfield"></a>Tabla 32. HRESULT AddField  

|**Parámetro**|**Descripción**|  
|-|-|  
|**Fieldname**|El nombre del campo tal y como aparece en el XML de la página.|  
|**idControl**|El identificador del control en la plantilla de cuadro de diálogo de la página.|  
|**suppressLog**|Establézcalo en TRUE si no quiere que los valores de este campo se escriban en el archivo de registro; establezca siempre este parámetro en TRUE para los campos de contraseña o PIN.|  
|**Tipo**|El tipo de control, que es uno de los siguientes:<br /><br /> -   **CONTROL_STATIC_TEXT**<br />-   **CONTROL_COMBO_BOX**<br />-   **CONTROL_LIST_VIEW**<br />-   **CONTROL_PROGRESS_BAR**<br />-   **CONTROL_GENERIC**<br />-   **CONTROL_RADIO_BUTTON**<br />-   **CONTROL_CHECK_BOX**<br />-   **CONTROL_TREE_VIEW**|  

#####  <a name="AddRadioGroup"></a> AddRadioGroup  

```  
HRESULT AddRadioGroup(LPCWSTR groupName, int radioControlId)  
```  

 Este método agrega un control a un grupo de botones de radio con nombre, como se muestra en la tabla 33. Se debe llamar antes que el método **InitFields**, porque ese método usa los atributos del elemento **RadioGroup** para controlar la configuración de todos los controles de botón de radio del grupo. Los grupos de botón de radio se pueden bloquear, por ejemplo, para deshabilitar todos los botones de radio, pero habilitar o deshabilitar los controles secundarios únicamente en función del botón de radio que esté seleccionado. Este método siempre devuelve **S_OK**.  

### <a name="table-33-hresult-addradiogroup"></a>Tabla 33. HRESULT AddRadioGroup  

|**Parámetro**|**Descripción**|  
|-|-|  
|**groupName**|Una cadena que define un grupo de botones de radio en esta página.|  
|**radioControlId**|El identificador de un solo botón de radio que se va a agregar a este grupo.|  

##### <a name="enableradiogroup"></a>EnableRadioGroup  

```  
HRESULT EnableRadioGroup(LPCWSTR groupName, BOOL enable)  
```  

 Este método permite habilitar o deshabilitar un grupo de botones de radio completo. Al deshabilitar un grupo de botones de radio se deshabilitan todos los controles de botón de radio del grupo, así como los elementos secundarios de esos botones de radio que se han agregado con **AddToGroup**. Vea las tablas 34 y 35.  

### <a name="table-34-enableradiogroup"></a>Tabla 34. EnableRadioGroup  

|**Parámetro**|**Descripción**|  
|-|-|  
|**groupName**|Nombre de un grupo de botones de radio que ya se ha definido con una llamada a **AddRadioGroup**.|  
|**Habilitar**|Se establece en TRUE para habilitar el grupo de botones de radio y FALSE para deshabilitarlo.|  

### <a name="table-35-hresult-enableradiogroup"></a>Tabla 35. HRESULT EnableRadioGroup  

|**HRESULT**|**Descripción**|  
|-|-|  
|**S_OK**|Grupo habilitado o deshabilitado.|  
|**E_INVALIDARG**|No hay ningún grupo de botones de radio con el nombre especificado.|  

#####  <a name="InitFields"></a> InitFields  

```  
HRESULT InitFields(IFieldCallback *pFieldCallback = nullptr)  
```  

 Antes de llamar a este método, llame al método **AddField** para cada campo que se puede controlar con el código XML. Este método siempre devuelve **S_OK**.  

 El parámetro **pFieldCallback** es opcional. Si se proporciona, el controlador de formulario llama a **SetFieldDefault** para los controles que no son **CONTROL_STATIC_TEXT** o **CONTROL_CHECK_BOX**. Este comportamiento permite recuperar un valor predeterminado del código XML y establecerlo en el control.  

#####  <a name="SaveFields"></a> SaveFields  

```  
HRESULT SaveFields(IFieldCallback *pFieldCallback = nullptr)  
```  

 Este método guarda los valores de campo en las variables de secuencia de tareas y en los datos de resumen que se van a mostrar en la página **Resumen**. Proporcionar un puntero en **pFieldCallback** permite administrar los valores que se guardan para los controles que no admiten **CONTROL_STATIC_TEXT**.  

##### <a name="isfielddisabled"></a>IsFieldDisabled  

```  
BOOL IsFieldDisabled(int controlId)  
```  

 Este método permite determinar si un campo se ha deshabilitado en el código XML.  

#####  <a name="InitSection"></a> InitSection  

```  
HRESULT InitSection(LPCWSTR key, LPCWSTR sectionCaption)  
```  

 Este método inicializa los datos de resumen que se van a mostrar en la página **Resumen**, como se muestra en la tabla 36. Llame a este método en el método **OnNextClicked** antes de llamar a **SaveFields**. Este método siempre devuelve **S_OK**.  

### <a name="table-36-hresult-initsection"></a>Tabla 36. HRESULT InitSection  

|**Parámetro**|**Descripción**|  
|-|-|  
|**Clave**|Este parámetro debe ser único en la página. Se usa para asegurarse de que cada página tiene su propia información de resumen.|  
|**sectionCaption**|El encabezado que se va a mostrar en la página **Resumen** de la información de resumen de esta página. Normalmente, se usa **DisplayName()** como el valor de este parámetro.|  

##### <a name="addsummaryitem"></a>AddSummaryItem  

```  
HRESULT AddSummaryItem(LPCWSTR first, LPCWSTR second)  
```  

 Este método permite agregar elementos de resumen a la página **Resumen** además de los que se establecen con el código XML. Vea la tabla 37.  

### <a name="table-37-hresult-addsummaryitem"></a>Tabla 37. HRESULT AddSummaryItem  

|**Parámetro**|**Descripción**|  
|-|-|  
|**Primero**|El título para el elemento de resumen, que se muestra en el lado izquierdo.|  
|**Segundo**|El valor que se va a mostrar en el lado derecho.|  

##### <a name="suppresslogvalue"></a>SuppressLogValue  

```  
HRESULT SuppressLogValue(LPCWSTR tsVariableName)  
```  

 Llame a este método para las variables de secuencia de tareas para las que no quiera que se escriban valores en el archivo de registro. Llame este método para las variables de secuencia de tareas que almacenan contraseñas, PIN u otros valores confidenciales que es posible que escriba un usuario.  

##### <a name="savetext"></a>SaveText  

```  
HRESULT SaveText(int controlId, LPCWSTR tsVariableName, LPCWSTR summaryCaption)  
```  

 Este método guarda el valor de un control de texto en una variable de secuencia de tareas y en la sección de resumen. Normalmente, no será necesario llamar a este método personalmente, porque el controlador de formulario lo hace para todos los campos. Vea la tabla 38.  

### <a name="table-38-hresult-savetext"></a>Tabla 38. HRESULT SaveText  

|**Parámetro**|**Descripción**|  
|-|-|  
|**idControl**|El identificador del cuadro de texto que contiene el valor que se quiere guardar (o cualquier otro control que puede devolver el texto).|  
|**tsVariableName**|Nombre de la variable de secuencia de tareas que se va a modificar.|  
|**summaryCaption**|El título para este valor en la página **Resumen**.|  

##### <a name="loadtext"></a>LoadText  

```  
HRESULT LoadText(int controlId, LPCWSTR tsVariableName)  
```  

 Este método lee el valor de una variable de secuencia de tareas y establece el cuadro de texto en este valor.  

##### <a name="controlevent"></a>ControlEvent  

```  
void ControlEvent(WORD eventId, WORD controlId)  
```  

 Llame a este método en el método **OnControlEvent** para asegurarse de que el controlador de formulario puede procesar eventos de control, lo que debe hacer para funcionar correctamente. Los valores que se pasan a este método son los mismos que se pasan al método **OnControlEvent**.  

##### <a name="isvalid"></a>IsValid  

```  
BOOL IsValid(void)  
```  

 Este método devuelve el estado de la validación más reciente del formulario. Si alguno de los validadores de control notificó un error, este método devuelve FALSE. En otras palabras, devuelve TRUE solo si todos los controles de la página son válidos.  

#### <a name="ivalidator-interface"></a>Interfaz IValidator  

```  
__interface IValidator : IUnknown  
{  
    HRESULT Init(IControl *pControl, LPCTSTR message);  
    HRESULT Init(IControl *pControl, IWizardPageContainer *pContainer, IStringProperties *pProperties);  
    BOOL, IsValid(LPBSTR pMessage);  
    HRESULT SetProperty(int propertyId, LPVARIANT pValue);  
    HRESULT SetProperty(int propertyId, IUnknown *pUnknown);  
    HRESULT SetProperty)(int propertyId, LPCTSTR pValue);  
};  
```  

##### <a name="overview"></a>Información general  
 Los *validadores* son componentes que pueden validar un único control en la página. La manera más fácil de implementar un validador consiste en convertirlo en una subclase de la clase **BaseValidator**, que se define en el archivo de encabezado BaseValidator.h.  

##### <a name="hresult-initicontrol-pcontrol-lpctstr-message"></a>HRESULT Init(IControl \*pControl, LPCTSTR message)  
 Si se crea un control de validación en el código, se puede llamar a este método para inicializar el validador. Vea la tabla 39.  

### <a name="table-39-hresult-init"></a>Tabla 39. HRESULT Init  

|**Parámetro**|**Descripción**|  
|-|-|  
|**pControl**|El control que debe validar el validador.|  
|**Message**|El mensaje que se va a mostrar en la página si el control no es válido.|  

##### <a name="hresult-initicontrol-pcontrol-iwizardpagecontainer-pcontainer-istringproperties-pproperties"></a>HRESULT Init(IControl \*pControl, IWizardPageContainer \*pContainer, IStringProperties \*pProperties)  
 El controlador de formulario llama a este método para inicializar los validadores que crea en función del código XML de la página. Vea la tabla 40.  

### <a name="table-40-hresult-init-method"></a>Tabla 40. HRESULT Init (método)  

|**Parámetro**|**Descripción**|  
|-|-|  
|**pControl**|El control que debe validar el validador.|  
|**pContainer**|En caso de que el validador necesite tener acceso al registrador o crear otros componentes.|  
|**pProperties**|Proporciona acceso a las propiedades (elementos de establecedor) para el validador.|  

##### <a name="bool-isvalidlpbstr-pmessage"></a>BOOL, IsValid(LPBSTR pMessage)  
 Este método devuelve TRUE si el control es válido o FALSE si no lo es. En la devolución, **pMessage** se debe rellenar con un nuevo **BSTR** que contiene el mensaje que se va a mostrar cuando el control no sea válido.  

##### <a name="hresult-setpropertyint-propertyid-lpvariant-pvalue"></a>HRESULT SetProperty(int propertyId, LPVARIANT pValue)  
 Este método se puede implementar si se necesitan valores adicionales que no se proporcionan en el código XML.  

##### <a name="hresult-setpropertyint-propertyid-iunknown-punknown"></a>HRESULT SetProperty(int propertyId, IUnknown \*pUnknown)  
 Este método se puede implementar si se necesitan valores adicionales que no se proporcionan en el código XML.  

##### <a name="hresult-setpropertyint-propertyid-lpctstr-pvalue"></a>HRESULT SetProperty)(int propertyId, LPCTSTR pValue)  
 Este método se puede implementar si se necesitan valores adicionales que no se proporcionan en el código XML.  

#### <a name="iregex-interface"></a>Interfaz IRegEx  

```  
__interface IRegEx : IUnknown  
{  
    BOOL MatchesRegex(LPCTSTR input, LPCTSTR regex);  
    HRESULT GetMatch(size_t index, LPBSTR pValue);  
};  
```  

 Este método lo implementa el componente **ID_Regex** (IRegex.h) y proporciona compatibilidad para el procesamiento de expresiones regulares.  

##### <a name="bool-matchesregexlpctstr-input-lpctstr-regex"></a>BOOL MatchesRegex(LPCTSTR input, LPCTSTR regex)  
 Este método ejecuta la expresión regular con el texto de entrada. Usa la función **regex_match** de la biblioteca estándar de C++ para realizar la operación. El método devuelve TRUE si hay coincidencias, FALSE en caso contrario.  

##### <a name="hresult-getmatchsizet-index-lpbstr-pvalue"></a>HRESULT GetMatch(size_t index, LPBSTR pValue)  
 Este método permite recuperar las coincidencias de la llamada a **MatchesRegex** más reciente. Tenga en cuenta que en este método no hay procesamiento de errores y que devuelve **S_OK** o produce una excepción.  

#### <a name="isummaryinfo-interface"></a>Interfaz ISummaryInfo  

```  
__interface ISummaryInfo : IUnknown  
{  
    size_t Count(void);  
    HRESULT Clear(void);  
    HRESULT AddInfo(LPCTSTR pFirst, LPCTSTR pSecond);  
    HRESULT GetInfo(size_t index, LPBSTR pFirst, LPBSTR pSecond);  
    HRESULT GetCaption(LPBSTR pCaption);  
    HRESULT SetCaption(LPCTSTR caption);  
};  
```  

 No es necesario usar esta interfaz directamente. En su lugar, use **IFormController**.  

#### <a name="isummarybag"></a>ISummaryBag  

```  
__interface ISummaryBag : IUnknown  
{  
    size_t Count(void);  
    HRESULT GetInfoByIndex(size_t index, [out] ISummaryInfo **ppSummary);  
    HRESULT GetInfoByKey(LPCTSTR key, [out] ISummaryInfo **ppSummary);  
};  
```  

 No es necesario usar esta interfaz directamente. En su lugar, use **IFormController**.  

#### <a name="itsvariablebag-interface"></a>Interfaz ITSVariableBag  

```  
__interface ITSVariableBag : IUnknown  
{  
    void GetValue([in] LPCTSTR variableName, [out] LPBSTR pValue);  
    void SetValue([in] LPCTSTR variableName, [in] LPCTSTR pValue);  
    void Clear(void);  
    HRESULT Remove([in] LPCTSTR variableName);  
    HRESULT SuppressLogValue([in] LPCTSTR variableName);  
    void Save(void);  
};  
```  

 Esta interfaz proporciona acceso a las variables de secuencia de tareas. Se puede tener acceso a esta interfaz mediante el método **TSVariables()** de la página.  

##### <a name="void-getvaluein-lpctstr-variablename-out-lpbstr-pvalue"></a>void GetValue([in] LPCTSTR variableName, [out] LPBSTR pValue)  
 Este método lee el valor de una variable de secuencia de tareas.  

> [!NOTE]
>  Los valores se almacenan en caché después de la primera lectura.  

##### <a name="void-setvaluein-lpctstr-variablename-in-lpctstr-pvalue"></a>void SetValue([in] LPCTSTR variableName, [in] LPCTSTR pValue)  
 Este método establece el valor de una variable de secuencia de tareas. Este valor se guarda en la memoria. Los valores de secuencia de tareas se escriben después de hacer clic en **Finalizar** en el Asistente para UDI.  

##### <a name="void-clearvoid"></a>void Clear(void)  
 Este método quita todos los valores de secuencia de tareas que se han guardado en la memoria.  

##### <a name="hresult-removein-lpctstr-variablename"></a>HRESULT Remove([in] LPCTSTR variableName)  
 Este método quita un valor de secuencia de tareas específico de la memoria. La próxima vez que se llame a **GetValue** con el mismo nombre de secuencia de tareas, el método intenta recuperarlo de la secuencia de tareas.  

##### <a name="hresult-suppresslogvaluein-lpctstr-variablename"></a>HRESULT SuppressLogValue([in] LPCTSTR variableName)  
 Cada vez que se escriben variables de secuencia de tareas, por ejemplo al hacer clic en **Finalizar** en el Asistente para UDI, los nombres y valores se escriben en el archivo de registro. Llame a este método para suprimir el registro de los valores confidenciales, como contraseñas o PIN, para una variable de secuencia de tareas específica.  

##### <a name="void-savevoid"></a>void Save(void)  
 Este método guarda todos los valores de secuencia de tareas que se han establecido con llamadas a **SetValue**.  

#### <a name="itsvariablerepository-interface"></a>Interfaz ITSVariableRepository  

```  
__interface ITSVariableRepository : IUnknown  
{  
    void GetValue([in] LPCTSTR variableName, BOOL logValue, [out] LPBSTR pValue);  
    void SetValue([in] LPCTSTR variableName, BOOL logValue, [in] LPCTSTR value);  
};  
```  

 Esta interfaz es para uso interno de **TSVariableBag** para leer y escribir variables de secuencia de tareas.  

#### <a name="iwizardfinish-interface"></a>Interfaz IWizardFinish  

```  
__interface IWizardFinish : IUnknown  
{  
    HRESULT Canceled(void);  
    HRESULT Finished(void);  
};  
```  

 Esta interfaz es útil en escenarios avanzados donde se quiere realizar un procesamiento adicional al hacer clic en **Finalizar** o **Cancelar** en el Asistente para UDI. El Asistente para UDI contiene una tarea **Finalizar** que guarda las variables de secuencia de tareas al hacer clic en **Finalizar**. Si se cancela el asistente, la tarea solo establece la variable de secuencia de tareas **OSDSetupWizCancelled** en TRUE y no guarda los cambios en ninguna otra variable de secuencia de tareas.  

 Si se crea un componente de finalización propio, se debe registrar con código similar al siguiente:  

```  
Register<MyFinishTaskFactory>(ID_MyFinishTask, pRegistry);  

PWizardFinish pFinish;  
CreateInstance(pRegistry, ID_MyFinishTask, &pFinish);  

PWizardFinishService pService;  
GetService<IWizardFinishService>(pRegistry, &pService);  

pService->Register(pFinish);  
```  

#### <a name="ibindablelist-interface"></a>Interfaz IBindableList  

```  
__interface IBindableList : IUnknown  
{  
    size_t Count(void);  
    HRESULT GetCaption(size_t index, LPBSTR pCaption);  
};  
```  

 Implemente esta interfaz si tiene un componente de origen de datos que quiere enlazar a un cuadro combinado mediante una llamada a su método **Bind**.  

##### <a name="sizet-countvoid"></a>size_t Count(void)  
 Este método devuelve el número de elementos de la lista.  

##### <a name="hresult-getcaptionsizet-index-lpbstr-pcaption"></a>HRESULT GetCaption(size_t index, LPBSTR pCaption)  
 Este método devuelve el título del elemento en el índice específico.  

#### <a name="idatanodes-interface"></a>Interfaz IDataNodes  

```  
__interface IDataNodes : IUnknown  
{  
    size_t Count();  
    HRESULT SetCaptionProperty(LPCTSTR captionProperty);  
    HRESULT GetProperty(size_t index, LPCTSTR propertyName, [out] LPBSTR propertyValue);  
    HRESULT GetNode(size_t index, [out] ISettingsProperties **ppNode);  
};  
```  

 Esta interfaz proporciona acceso a los datos jerárquicos que se pueden guardar en una página. Esta interfaz se obtiene a través de los métodos de la interfaz **ISettingsProperties**, que está disponible para la página a través del método **Settings**.  

 Los datos en el código XML de una página pueden ser parecidos a estos:  

```  
      <Data Name="Network">  
        <DataItem>  
          <Setter Property="DisplayName">Public</Setter>  
          <Setter Property="Share">\\servername\Share</Setter>  
        </DataItem>  
        <DataItem>  
          <Setter Property="DisplayName">Dev Team</Setter>  
          <Setter Property="Share">\\servername\DevShare</Setter>  
        </DataItem>  
      </Data>  
```  

 Llamar a **Settings()->GetDataNode(L"Network", &pData)** proporciona una instancia de **IDataNodes** con dos elementos de datos (cada uno con dos propiedades).  

##### <a name="sizet-count"></a>size_t Count()  
 Este método devuelve el número de elementos **DataItem**.  

##### <a name="hresult-setcaptionpropertylpctstr-captionproperty"></a>HRESULT SetCaptionProperty(LPCTSTR captionProperty)  
 El componente que admite esta interfaz también admite **IBindableList**, lo que facilita rellenar un cuadro combinado con datos del código XML de la página. Este método controla qué propiedad (establecedor) de cada elemento **DataItem** se va a usar para este enlace. Por ejemplo, se podría llamar a este método con **DisplayName**, y usar esa propiedad de establecedor para el enlace de datos. El cuadro combinado contendría entonces **Public** y **Dev Team** como elementos.  

##### <a name="hresult-getpropertysizet-index-lpctstr-propertyname-out-lpbstr-propertyvalue"></a>HRESULT GetProperty(size_t index, LPCTSTR propertyName, [out] LPBSTR propertyValue)  
 Este método obtiene una propiedad de uno de los elementos **DataItem**. Vea las tablas 41 y 42.  

### <a name="table-41-dataitem-getproperty"></a>Tabla 41. DataItem GetProperty  

|**Parámetro**|**Descripción**|  
|-|-|  
|**Index**|El valor de índice (empezando por 0) del elemento **DataItem** para el que se quiere recuperar un valor de propiedad.|  
|**propertyName**|Nombre de la propiedad de establecedor para la que se quiere recuperar un valor.|  
|**propertyValue**|En la devolución, contiene el valor de cadena de una propiedad.|  

### <a name="table-42-hresult-getproperty"></a>Tabla 42. HRESULT GetProperty  

|||  
|-|-|  
|**HRESULT**|**Descripción**|  
|**S_OK**|Se recuperó la propiedad.|  
|**E_INVALIDARG**|El índice está más allá del final de la matriz.|  

##### <a name="hresult-getnodesizet-index-out-isettingsproperties-ppnode"></a>HRESULT GetNode(size_t index, [out] ISettingsProperties **ppNode)  
 Este método es similar a **GetProperty**, pero en lugar de devolver un valor de un elemento **DataItem**, devuelve el elemento **DataItem** completo encapsulado en una interfaz **ISettingsProperties**. Vea las tablas 43 y 44.  

### <a name="table-43-hresult-getnode"></a>Tabla 43. HRESULT GetNode  

|**Parámetro**|**Descripción**|  
|-|-|  
|Índice|El valor de índice (empezando por 0) del elemento **DataItem** para el que se quiere recuperar un valor de propiedad.|  
|**ppNode**|En la salida, la interfaz **ISettingsProperties** que encapsula el nodo **DataItem**.|  

### <a name="table-44-hresult-getnode-results"></a>Tabla 44. Resultados de HRESULT GetNode  

|**HRESULT**|**Descripción**|  
|-|-|  
|**S_OK**|Se recuperó el nodo.|  
|**E_INVALIDARG**|El índice está más allá del final de la matriz.|  

#### <a name="ifactoryregistry-interface"></a>Interfaz IFactoryRegistry  

```  
__interface IFactoryRegistry : IUnknown  
{  
    void Register(LPCTSTR type,  IClassFactory *pFactory);  
    HRESULT LoadAndRegister(LPCTSTR dllName, ILogger *pLogger);  
    BOOL Contains(LPCTSTR type);  
    HRESULT GetFactory(LPCTSTR type,  IClassFactory **ppFactory);  
    HRESULT CreateInstance(LPCTSTR type,  IUnknown **ppInstance);  
    HRESULT SetContainer(IWizardPageContainer *pContainer);  
    HRESULT RegisterService(REFGUID iid, IUnknown *pService);  
    HRESULT GetService(REFGUID iid,  IUnknown **ppService);  
};  
```  

##### <a name="overview"></a>Información general  
 Cuando se crea una página personalizada, como mínimo se debe crear un *generador de páginas*: una clase que implementa **IClassFactory**. (Se puede usar **ClassFactoryImpl** como una clase base para el generador).  

##### <a name="void-registerlpctstr-type--iclassfactory-pfactory"></a>void Register(LPCTSTR type,  IClassFactory \*pFactory)  
 Este método registra un generador de clases con el registro. Vea la tabla 45.  

### <a name="table-45-iclassfactory-void-register"></a>Tabla 45. Registro de IClassFactory void  

|**Parámetro**|**Descripción**|  
|-|-|  
|**Tipo**|Una cadena que identifica el generador que se va a registrar; por lo general, este parámetro debe tener el nombre de la empresa en la cadena para asegurarse de que sea única.|  
|**pFactory**|Un puntero a la instancia del generador de clases.|  

##### <a name="hresult-loadandregisterlpctstr-dllname-ilogger-plogger"></a>HRESULT LoadAndRegister(LPCTSTR dllName, ILogger \*pLogger)  
 Este método es solo para uso interno.  

##### <a name="bool-containslpctstr-type"></a>BOOL Contains(LPCTSTR type)  
 Generalmente, este método es para uso interno. Comprueba si se ha registrado un generador de clases para un tipo.  

##### <a name="hresult-getfactorylpctstr-type--iclassfactory-ppfactory"></a>HRESULT GetFactory(LPCTSTR type,  IClassFactory **ppFactory)  
 Este método permite recuperar el generador de clases. Normalmente, se llamaría a **CreateInstance**. Pero si va a crear una gran cantidad del mismo componente, es más eficaz recuperar el generador y, después, solicitarle que cree las instancias automáticamente.  

##### <a name="hresult-createinstancelpctstr-type--iunknown-ppinstance"></a>HRESULT CreateInstance(LPCTSTR type,  IUnknown **ppInstance)  
 Este método crea una instancia de un componente, dado su tipo. Use el método de plantilla **CreateInstance** en su lugar, que permite crear objetos con seguridad de tipos.  

##### <a name="hresult-setcontaineriwizardpagecontainer-pcontainer"></a>HRESULT SetContainer(IWizardPageContainer \*pContainer)  
 Este método es solo para uso interno.  

##### <a name="hresult-registerservicerefguid-iid-iunknown-pservice"></a>HRESULT RegisterService(REFGUID iid, IUnknown \*pService)  
 Los *servicios* son instancias únicas de un componente que se pueden usar en varios lugares. Se puede usar este método para registrar un servicio en una página y, después, recuperar esa misma instancia de otra página.  

##### <a name="hresult-getservicerefguid-iid--iunknown-ppservice"></a>HRESULT GetService(REFGUID iid,  IUnknown **ppService)  
 Este método recupera un servicio que se registró anteriormente con una llamada a RegisterService.  

##### <a name="hresult-setlanguagelangid-languageid"></a>HRESULT SetLanguage(LANGID languageId)  
 Este método establece el idioma del Asistente para UDI en el identificador de idioma que se proporcionó en el parámetro **languageId**.  

##### <a name="langid-getlanguage"></a>LANGID GetLanguage()  
 Este método devuelve el valor del identificador de idioma que se proporcionó con el parámetro de la línea de comandos **/locale** para el Asistente para UDI. El método devuelve uno de los valores siguientes:  

-   Valor del identificador de idioma que se proporcionó con el parámetro de la línea de comandos **/locale**.  

-   0, si no proporcionó el parámetro de la línea de comandos **/locale**.  

#### <a name="ilogger-interface"></a>Interfaz ILogger  

```  
__interface ILogger : IUnknown  
{  
    HRESULT Init(LPCWSTR logFilename);  
    HRESULT MoveLog(LPCWSTR logFilename);  
    HRESULT LogBase(EMessageType messageType, LPCTSTR component, SYSTEMTIME eventTime, LPCTSTR message);  
    HRESULT Log(EMessageType messageType, LPCTSTR component, LPCTSTR message);  
    HRESULT Error(HRESULT error, LPCTSTR component, LPCTSTR message);  
    HRESULT Error2(HRESULT error, LPCTSTR component, LPCTSTR message, LPCTSTR message2);  
    HRESULT Normal(LPCTSTR component, LPCTSTR message);      
    HRESULT Normal2(LPCTSTR component, LPCTSTR message, LPCTSTR message2);  
    HRESULT Verbose(LPCTSTR component, LPCTSTR message);  
    HRESULT Verbose2(LPCTSTR component, LPCTSTR message, LPCTSTR message2);  
    HRESULT Debug(LPCWSTR component, LPCWSTR message);  
    HRESULT EnableDebug(BOOL debug);  
    HRESULT Close(void);  
    HRESULT GetLogFilename(LPBSTR pFilename);  
};  
```  

##### <a name="overview"></a>Información general  
 El Asistente para UDI registra información en un archivo de registro, lo que ayuda a solucionar los problemas encontrados en el campo. Es una buena idea que las páginas registren información. Se puede obtener un puntero a esta interfaz desde dentro de la página mediante el método **Logger()** de la página. Las líneas del archivo de registro contienen un número de "nivel" que representa mensajes de error, normales, detallados o de depuración.  

> [!NOTE]
>  Los mensajes de depuración no se guardan en el archivo de registro a menos que se active la compatibilidad con la depuración. Se puede activar la compatibilidad con la depuración mediante la adición de la línea siguiente al elemento **Style** del archivo .config:  

```  
<Setter Property="debug">true</Setter>  
```  

##### <a name="init"></a>Inicializar  

```  
HRESULT Init(LPCWSTR logFilename)  
```  

 Este método es solo para uso interno.  

##### <a name="movelog"></a>MoveLog  

```  
HRESULT MoveLog(LPCWSTR logFilename)  
```  

 Este método es solo para uso interno.  

##### <a name="logbase"></a>LogBase  

```  
HRESULT LogBase(EMessageType messageType, LPCTSTR component, SYSTEMTIME eventTime, LPCTSTR message)  
```  

 Este método es solo para uso interno.  

##### <a name="log"></a>Registro  

```  
HRESULT Log(EMessageType messageType, LPCTSTR component, LPCTSTR message)  
```  

 Este método es solo para uso interno.  

##### <a name="error"></a>Error  

```  
HRESULT Error(HRESULT error, LPCTSTR component, LPCTSTR message)  
```  

 Llame a este método para registrar información sobre un error. Vea la tabla 46.  

### <a name="table-46-hresult-error"></a>Tabla 46. HRESULT Error  

|**Parámetro**|**Descripción**|  
|-|-|  
|**Error**|El código de error devuelto por una llamada (este código se mostrará en la entrada del registro como un número).|  
|**Componente**|Una cadena que identifica el origen del error, que suele ser la página o el componente que se ha escrito.|  
|**Message**|El mensaje que explica el motivo del error.|  

#####  <a name="Error2"></a> Error2  

```  
HRESULT Error2(HRESULT error, LPCTSTR component, LPCTSTR message, LPCTSTR message2)  
```  

 Este método es similar al método **Error** pero permite proporcionar un mensaje de dos partes. El mensaje final tendrá "mensaje" y, después, "mensaje2" en el archivo de salida. Simplemente es un método cómodo.  

##### <a name="normal"></a>Normal  

```  
HRESULT Normal(LPCTSTR component, LPCTSTR message)  
```  

 Este método registra un mensaje normal. Vea la descripción del método [Error](#Error) para obtener los parámetros.  

##### <a name="normal2"></a>Normal2  

```  
HRESULT Normal2(LPCTSTR component, LPCTSTR message, LPCTSTR message2)  
```  

 Este método registra un mensaje normal. Vea la descripción del método [Error2](#Error2) para obtener los parámetros.  

##### <a name="verbose"></a>Detallado  

```  
HRESULT Verbose(LPCTSTR component, LPCTSTR message)  
```  

 Este método registra un mensaje detallado. Vea la descripción del método [Error](#Error) para obtener los parámetros.  

##### <a name="verbose2"></a>Verbose2  

```  
HRESULT Verbose2(LPCTSTR component, LPCTSTR message, LPCTSTR message2)  
```  

 Este método registra un mensaje detallado. Vea la descripción del método [Error2](#Error2) para obtener los parámetros.  

##### <a name="debug"></a>Depuración  

```  
HRESULT Debug(LPCWSTR component, LPCWSTR message)  
```  

 Este método registra un mensaje de depuración. Vea la descripción del método [Error](#Error) para obtener los parámetros. Los mensajes de depuración no se guardan en el archivo a menos que se habilite. Vea la sección Información general para obtener más detalles.  

##### <a name="enabledebug"></a>EnableDebug  

```  
HRESULT EnableDebug(BOOL debug)  
```  

 Este método es solo para uso interno.  

##### <a name="close"></a>Cerrar  

```  
HRESULT Close(void)  
```  

 Este método es solo para uso interno.  

##### <a name="getlogfilename"></a>GetLogFilename  

```  
HRESULT GetLogFilename(LPBSTR pFilename)  
```  

 Este método recupera el nombre del archivo de registro.  

#### <a name="iorientation-interface"></a>Interfaz IOrientation  

```  
__interface IOrientation : IUnknown  
{  
    void SetController(IWizardDialogController *pController);  
    int AddPage(LPCTSTR name);  
    void SelectPage(int index);  
};  
```  

 Esta interfaz es solo para uso interno.  

#### <a name="isettings-interface"></a>Interfaz ISettings  

```  
__interface ISettings : IUnknown  
{  
    int NumDlls();  
    int NumPages();  

    HRESULT SetStage(LPCWSTR stageName);  
    HRESULT GetDllName(long index, __out LPBSTR pDllName);  
    HRESULT GetPageInfo(long index, __out ISettingsProperties **ppPageInfo);  
    HRESULT GetStyle(__out ISettingsProperties **ppStyleInfo);  
};  
```  

 Esta interfaz es solo para uso interno.  

#### <a name="isettingsproperties-interface"></a>Interfaz ISettingsProperties  

```  
__interface ISettingsProperties : IUnknown  
{  
    HRESULT GetAttribute(LPCTSTR attributeName, __out LPBSTR attributeValue);  
    IStringProperties * Properties();  
   RESULT SelectNodes(LPCTSTR xPath, __out IXMLDOMNodeList **ppList);  
    HRESULT SelectSingleNode(LPCTSTR xPath, __out IXMLDOMNode **ppNode);  
    HRESULT GetDataNode(LPCTSTR name, __out ISettingsProperties **ppNode);  
    HRESULT GetDataNodes(__out IDataNodes **ppNodes);  
    HRESULT GetChildDataNodes(LPCTSTR childeName, __out IDataNodes **ppNodes);  
};  
```  

##### <a name="overview"></a>Información general  
 Esta interfaz proporciona acceso a los datos de la página. Para obtener el nivel superior de datos de la página, use el método **Settings()** de la página.  

##### <a name="hresult-getattributelpctstr-attributename--lpbstr-attributevalue"></a>HRESULT GetAttribute(LPCTSTR attributeName,  LPBSTR attributeValue)  
 Este método permite recuperar los valores de atributos en el nodo principal, que es el nodo **Page** cuando se usa el método **Settings()** de la página.  

##### <a name="istringproperties--properties"></a>IStringProperties * Properties()  
 Este método proporciona acceso a los valores de propiedad de establecedor bajo el nodo principal. Para una página, estas son las propiedades de nivel superior.  

##### <a name="hresult-selectnodeslpctstr-xpath--ixmldomnodelist-pplist"></a>HRESULT SelectNodes(LPCTSTR xPath,  IXMLDOMNodeList **ppList)  
 Llame a este método si quiere obtener directamente una lista de los nodos XML en los que se usa una expresión XPath. Es mejor usar uno de los otros métodos si es posible. Use este método solo si no hay otra manera de llegar a los nodos.  

##### <a name="hresult-selectsinglenodelpctstr-xpath--ixmldomnode-ppnode"></a>HRESULT SelectSingleNode(LPCTSTR xPath,  IXMLDOMNode **ppNode)  
 Llame a este método si quiere obtener directamente un solo nodo XML con una expresión XPath. Es mejor usar uno de los otros métodos si es posible. Use este método solo si no hay otra manera de llegar a un nodo.  

##### <a name="hresult-getdatanodelpctstr-name--isettingsproperties-ppnode"></a>HRESULT GetDataNode(LPCTSTR name,  ISettingsProperties **ppNode)  
 Recuperar un elemento **Data** en función del atributo **Name** de ese elemento.  

##### <a name="hresult-getdatanodesidatanodes-ppnodes"></a>HRESULT GetDataNodes(IDataNodes **ppNodes)  
 Este método recupera una lista de los elementos **DataItem** bajo el nodo actual. Desde el nivel de página, llame al método **GetDataNode** para recuperar una interfaz **ISettingsProperty** para los datos. Después, en esa instancia, llame a **GetDataNodes** para recuperar la lista de registros. Por ejemplo, con este código XML:  

```  
    <Page …>  
      <Data Name="Network">  
        <DataItem>  
          <Setter Property="DisplayName">Public</Setter>  
          <Setter Property="Share">\\servername\Share</Setter>  
        </DataItem>  
        <DataItem>  
          <Setter Property="DisplayName">Dev Team</Setter>  
          <Setter Property="Share">\\servername\DevShare</Setter>  
        </DataItem>  
      </Data>  

PSettingsProperties pData;  
Settings()->GetDataNode(L"Network", &pData);  
PDataNodes pNodes;  
pData->GetDataNodes(&pNodes);  
```  

##### <a name="hresult-getchilddatanodeslpctstr-childename--idatanodes-ppnodes"></a>HRESULT GetChildDataNodes(LPCTSTR childeName,  IDataNodes **ppNodes)  
 Este método proporciona una forma rápida de tener acceso al conjunto de nodos **DataItem** en un nodo **Data** determinado. Con el código XML del ejemplo **GetDataNodes**, el código siguiente hace exactamente lo mismo que las cuatro líneas de código del ejemplo **GetDataNodes** pero con comprobación de errores:  

```  
ISimpleStringProperties Interface  
```  

#### <a name="isimplestringproperties-interface"></a>Interfaz ISimpleStringProperties  

```  
__interface ISimpleStringProperties : IStringProperties  
{  
void Add(LPCTSTR propertyName, LPCTSTR value);  
};  
```  

 Por sí sola, es posible que esta interfaz no sea útil. Pero se implementa mediante el componente **ID_SimpleStringProperties**, que también implementa la interfaz **IStringProperties**. Se puede usar este componente en casos donde es necesario pasar un conjunto de propiedades a otro componente, como una tarea, pero se quieren agregar valores mediante programación en lugar de usar los del código XML. Este es un ejemplo de cómo se podría usar esta interfaz:  

```  
PSimpleStringProperties *pProperties;  
CreateInstance(Container(), ID_SimpleStringProperties, &pProperties);  
pProperties->Add(L"filename", L"%windir%\\system32\\cscript.exe");  
pTask->Init(pProperties, nullptr);  
IStringProperties  
__interface IStringProperties : IUnknown  
{  
    HRESULT Get(LPCTSTR propertyName, [out] LPBSTR pPropValue);  
};  
```  

 Esta interfaz proporciona acceso simple a un conjunto de elementos de establecedor que proceden del código XML. Esta interfaz está disponible para las propiedades de una página mediante **Settings()->Properties()**.  

##### <a name="hresult-getlpctstr-propertyname-out-lpbstr-ppropvalue"></a>HRESULT Get(LPCTSTR propertyName, [out] LPBSTR pPropValue)  
 Este método recupera un solo valor de propiedad. Vea las tablas 47 y 48.  

### <a name="table-47-ihresult-get-property-value"></a>Tabla 47. Valor de la propiedad IHRESULT Get  

|**Parámetro**|**Descripción**|  
|-|-|  
|**propertyName**|Nombre de la propiedad que se quiere leer.|  
|**pPropValue**|En la salida, contiene el valor de propiedad como una cadena (este valor será **nullptr** si no existe esa propiedad).|  

### <a name="table-48-ihresult-get-property-value-results"></a>Tabla 48. Resultados de valor de propiedad de IHRESULT Get  

|||  
|-|-|  
|**HRESULT**|**Descripción**|  
|**S_OK**|Se recupera el valor de propiedad.|  
|**E_INVALIDARG**|No hay ninguna propiedad con el nombre proporcionado.|  

#### <a name="itaskmanager-interface"></a>Interfaz ITaskManager  

```  
__interface ITaskManager : IUnknown  
{  
    HRESULT Init(IWizardPageView *pPageView, int idListView, int idMessage, int idRetryButton, ISettingsProperties *pPageInfo, ITaskManagerCallback *pCallback);  
    HRESULT SetFailMessage(LPCWSTR message);  

    HRESULT Start(void);  

    HRESULT GetTaskMessage(size_t index, LPBSTR message);  
    HRESULT GetResultType)(size_t index, LPBSTR type);  
    HRESULT GetProperty(size_t index, LPCTSTR propertyName, LPBSTR value);  
    int GetSelectedIndex(void);  
    HRESULT Wait(DWORD waitMilliseconds);  
    size_t FailedCount(void);  
    size_t WarningCount(void);  
    size_t SucceedCount(void);  
    size_t RunningCount(void);  

    void OnCommonControlEvent(WORD controlId, LPNMHDR pInfo);  
    void OnControlEvent(WORD eventId, WORD controlId);  
    void EnableButtons(BOOL enable);  
}  
```  

 Esta interfaz se implementa mediante el componente **TaskManager** (**ID_TaskManager** en ITaskManager.h), que es el que ejecuta las tareas en la página preparatoria. Se puede usar la página preparatoria directamente, lo que se hace la mayoría de las veces, o bien crear una página propia y dejar que este componente realice la mayoría del trabajo.  

##### <a name="hresult-initiwizardpageview-ppageview-int-idlistview-int-idmessage-int-idretrybutton-isettingsproperties-ppageinfo-itaskmanagercallback-pcallback"></a>HRESULT Init(IWizardPageView \*pPageView, int idListView, int idMessage, int idRetryButton, ISettingsProperties \*pPageInfo, ITaskManagerCallback \*pCallback)  
 Debe llamar a este método antes de llamar a cualquier otro. Inicializa el componente **TaskManager**. Vea la tabla 49.  

### <a name="table-49-hresult-init"></a>Tabla 49. HRESULT Init  

|**Parámetro**|**Descripción**|  
|-|-|  
|**pPageView**|Proporciona acceso a la página en la que se ejecutarán las tareas (esta página debe tener un conjunto específico de controles, que se describen en los parámetros siguientes).|  
|**idListView**|El identificador de control de un control **ListView** que mostrará la lista de tareas y el estado de esas tareas.|  
|**idMessage**|El identificador de control de un cuadro de texto que se usará para mostrar un mensaje para la tarea seleccionada.|  
|**idRetryButton**|El identificador de control de un botón en el que se puede hacer clic para volver a ejecutar las tareas.|  
|**pPageInfo**|Un contenedor alrededor del código XML de la página (**TaskManager** carga el conjunto de tareas que se van a ejecutar desde este código XML).|  
|**pCallback**|Puede ser NULL (si este parámetro no es NULL, **TaskManager** llama al método **Started** cuando se inicia una tarea y al método **Finished** para cada tarea que termina de ejecutarse).|  

##### <a name="hresult-setfailmessagelpcwstr-message"></a>HRESULT SetFailMessage(LPCWSTR message)  
 Este método establece el mensaje que se mostrará si se produce un error en una o varias tareas.  

##### <a name="hresult-startvoid"></a>HRESULT Start(void)  
 Este método inicia todas las tareas. Cada tarea se inicia en un subproceso independiente.  

##### <a name="hresult-gettaskmessagesizet-index-lpbstr-message"></a>HRESULT GetTaskMessage(size_t index, LPBSTR message)  
 Este método es solo para uso interno. Recupera el mensaje actual de una tarea según su índice en la lista de tareas.  

##### <a name="hresult-getresulttypesizet-index-lpbstr-type"></a>HRESULT GetResultType)(size_t index, LPBSTR type)  
 Este método recupera el "tipo" para una tarea actual. En la tabla 50 se muestran los tipos disponibles.  

### <a name="table-50-hresult-getresulttype"></a>Tabla 50. HRESULT GetResultType  

|**Tipo**|**Descripción**|  
|-|-|  
|**0**|Representa una tarea que se ha realizado correctamente.|  
|**1**|Representa una tarea que devuelve una advertencia.|  
|**-1**|Representa una tarea con error.|  

 Para recuperar el tipo, se examina el código de error o de salida de la tarea y se busca una coincidencia en el elemento XML <ExitCodes\> de la tarea.  

##### <a name="hresult-getpropertysizet-index-lpctstr-propertyname-lpbstr-value"></a>HRESULT GetProperty(size_t index, LPCTSTR propertyName, LPBSTR value)  
 En las páginas de progreso y preparatoria se usa este método para recuperar la propiedad de establecedor **BitmapFilename** para que pueda mostrar una imagen junto al mensaje para la tarea que se resalte. En otras palabras, se puede agregar un establecedor personalizado al código XML de la tarea y, después, recuperarlo con este método.  

##### <a name="int-getselectedindexvoid"></a>int GetSelectedIndex(void)  
 Este método recupera el índice de la tarea seleccionada actualmente, lo que resulta útil si quiere recuperar información adicional sobre la tarea (vea el método **GetProperty**) para mostrar de la tarea seleccionada. En las páginas de progreso y preparatoria se usa este método para mostrar una imagen para la tarea seleccionada.  

##### <a name="hresult-waitdword-waitmilliseconds"></a>HRESULT Wait(DWORD waitMilliseconds)  
 Este método ayuda principalmente con las pruebas unitarias para que la prueba pueda garantizar que las tareas finalizan antes de que la prueba unitaria salga. Este método no se llamará normalmente. Devuelve cuando finalizan todas las tareas en ejecución o el tiempo de espera se ha agotado.  

##### <a name="sizet-failedcountvoid"></a>size_t FailedCount(void)  
 Este método devuelve el número de tareas que actualmente se marcan como erróneas.  

##### <a name="sizet-warningcountvoid"></a>size_t WarningCount(void)  
 Este método devuelve el número de tareas que actualmente se marcan como advertencias.  

##### <a name="sizet-succeedcountvoid"></a>size_t SucceedCount(void)  
 Este método devuelve el número de tareas que actualmente se marcan como correctas.  

##### <a name="sizet-runningcountvoid"></a>size_t RunningCount(void)  
 Este método devuelve el número de tareas actualmente en ejecución.  

##### <a name="void-oncommoncontroleventword-controlid-lpnmhdr-pinfo"></a>void OnCommonControlEvent(WORD idControl, LPNMHDR pInfo)  
 Este método se llama desde **OnCommonControlEvent** de la página para que **TaskManager** pueda procesar los eventos que necesita.  

##### <a name="void-oncontroleventword-eventid-word-controlid"></a>void OnControlEvent(WORD idEvento, WORD idControl)  
 Este método se llama desde **OnControlEvent** de la página para que **TaskManager** pueda procesar los eventos que necesita.  

##### <a name="void-enablebuttonsbool-enable"></a>void EnableButtons(BOOL enable)  
 Este método es solo para uso interno.  

#### <a name="iwizardcomponent-interface"></a>Interfaz IWizardComponent  

```  
__interface IWizardComponent : IUnknown  
{  
    HRESULT SetContainer(IWizardPageContainer *pContainer);  
};  
```  

##### <a name="overview"></a>Información general  
 Normalmente, esta interfaz no se implementará directamente, sino a través de la clase de plantilla **WizardComponent**. Si el componente implementa esta interfaz y se ha registrado un generador de clases con el registro, el componente recibe un puntero a la instancia de **IWizardPageContainer** cuando se crea. Esto facilita, por ejemplo, el acceso al registrador o al registro para crear otros componentes que es posible que el componente necesite.  

#### <a name="iwizarddialogcontroller-interface"></a>Interfaz IWizardDialogController  

```  
__interface IWizardDialogController : IUnknown  
{  
    void Initialize(ISettings *pSettings);  
    void InitPages(void);  
    void Start();  
    void Next();  
    void Finish();  
    void Previous();  
    int NumPages();  
    void Cancel();  

    HRESULT Focus(WizardButtons button);  
    HRESULT SetEnable(WizardButtons button, BOOL enable);  
    void ShowWarningMessage(LPCTSTR message);  
    void HideWarningMessage();  

    void ChangePage(size_t newIndex);  
    IUnknown *CurrentPage(void);  
    HRESULT GetCurrentTitle([out, retval] LPBSTR pDisplayName);  
};  
```  

 Esta interfaz es solo para uso interno.  

#### <a name="iwizarddialogview-interface"></a>Interfaz IWizardDialogView  

```  
__interface IWizardDialogView : IUnknown  
{  
    HRESULT LoadBannerImage(LPCTSTR bannerFilename);  
    HRESULT LoadPage(LPCTSTR pageType, ISettingsProperties *pPageSettings, IWizardPageView **view);  
    HRESULT SetEnable(WizardButtons button, BOOL enable);  
    HRESULT Focus(WizardButtons button);  
    void EnableFinish(BOOL isFinish);  
    void Exit(int exitCode);  
    void ShowWarningMessage(LPCTSTR message);  
    void HideWarningMessage(void);  
    void SetTitle(LPCTSTR title);  
    void SetPageTitle(LPCTSTR title);  
    int ShowMessageBox(LPCTSTR message, LPCTSTR lpCaption, UINT uType);  
    HWND GetHwnd(void);  
    void UpdateFocus(void);  
};  
```  

 Esta interfaz es solo para uso interno.  

####  <a name="IWizardPageInterface"></a> Interfaz IWizardPage  

```  
__interface IWizardPage : IUnknown  
{  
    HRESULT SetPageSettings(ISettingsProperties *pPageSettings);  
    HINSTANCE GetInstanceHandle(void);  
    int GetDialogResourceId(void);  
    void WindowCreated(IWizardPageView *pView, IWizardPageContainer *pContainer);  
    void WindowShown(void);  
    void WindowHidden(void);  

    HRESULT NextClicked(void);  
    void ControlEvent(WORD eventId, WORD controlId);  
    void CommonControlEvent(WORD controlId, LPNMHDR pInfo, LPBOOL pCancel);  
    void UnhandledEvent(HWND hwnd, UINT message, WPARAM wParam, LPARAM lParam);  
};  
```  

##### <a name="overview"></a>Información general  
 Esta interfaz se implementa mediante **WizardPageImpl**, por lo que normalmente no tendrá que implementarla usted mismo. El asistente llama a todos estos métodos automáticamente cuando interactúa con las páginas personalizadas.  

#### <a name="iwizardpagecontainer-interface"></a>Interfaz IWizardPageContainer  

```  
__interface IWizardPageContainer : IUnknown  
{  
    ILogger * Logger(void);  
    IPropertyBag * Properties(void);  
    HRESULT CreateInstance(LPCTSTR type, [out] IUnknown **ppInstance);  
    HRESULT GetService(REFIID iid, [out] IUnknown **ppInstance);  
    HRESULT ReplaceVariables(LPCTSTR source, [out] LPBSTR pDest);  
    HRESULT GotoPage(LPCTSTR pageName);  
    int ShowMessageBox(LPCTSTR message, LPCTSTR lpCaption, UINT uType);  
    BOOL InPreview(void);  
    HWND GetHwnd(void);  
};  
```  

##### <a name="overview"></a>Información general  
 Esta interfaz está disponible en la página a través del método **Container** (implementado por **WizardPageImpl**) y proporciona acceso a diversos servicios del asistente.  

##### <a name="ilogger--loggervoid"></a>ILogger * Logger(void)  
 Use este método para escribir mensajes en el archivo de registro, por ejemplo:  

```  
Logger()->Verbose(s_component, L"Message for log file");  
```  

##### <a name="ipropertybag--propertiesvoid"></a>IPropertyBag * Properties(void)  
 Este método proporciona acceso a las variables de "memoria", que son propiedades que están en memoria solo mientras se ejecuta el Asistente para UDI. Estas propiedades están disponibles para otras páginas en el código o en el XML mediante la sintaxis **$memoryVarName$**.  

##### <a name="hresult-createinstancelpctstr-type-out-iunknown-ppinstance"></a>HRESULT CreateInstance(LPCTSTR type, [out] IUnknown **ppInstance)  
 Este método permite crear una instancia de cualquier componente que se haya registrado. Pero es mejor usar la función de plantilla **CreateInstance**, porque está fuertemente tipada.  

##### <a name="hresult-getservicerefiid-iid-out-iunknown-ppinstance"></a>HRESULT GetService(REFIID iid, [out] IUnknown **ppInstance)  
 Este método permite recuperar un servicio que se ha registrado. Pero es mejor llamar a la función de plantilla **GetService**, que está fuertemente tipada (en lugar de usar **IUnknown**).  

##### <a name="hresult-replacevariableslpctstr-source-out-lpbstr-pdest"></a>HRESULT ReplaceVariables(LPCTSTR source, [out] LPBSTR pDest)  
 Este método controla el trabajo con variables dentro de valores de cadena. Admite los formatos que se muestran en las tablas 51 y 52.  

### <a name="table-51-hresult-replacevariables"></a>Tabla 51. HRESULT ReplaceVariables  

|**Formato**|**Descripción**|  
|-|-|  
|**$Name$**|Reemplaza el valor de una variable de memoria con este nombre (si no hay ninguna variable de memoria con el nombre, se quitará el "token").|  
|**%Name%**|Una variable de secuencia de tareas o una variable de entorno. El orden es como sigue:<br /><br /> 1.  Use el valor de una variable de secuencia de tareas, si existe.<br />2.  Use el valor de una variable de entorno, si existe.<br />3.  En caso contrario, quite este texto de la cadena.|  

### <a name="table-52-hresult-parameter"></a>Tabla 52. HRESULT Parameter  

|**Parámetro**|**Descripción**|  
|-|-|  
|**Origen**|La cadena de entrada, que puede contener cualquier combinación de las variables **$** y **%**, o ninguna.|  
|**pDest**|En la devolución, contiene una cadena nueva con todos los tokens reemplazados según la tabla 51.|  

##### <a name="hresult-gotopagelpctstr-pagename"></a>HRESULT GotoPage(LPCTSTR pageName)  
 Este método no se ha probado totalmente. La idea es que se puede cambiar directamente a una página específica según el nombre de la página como se define en el archivo .config de XML. Llamar a este método omite **OnNextClicked** en la página. Además, el comportamiento de este método está sujeto a cambios, por lo que debe usarlo bajo su responsabilidad.  

##### <a name="int-showmessageboxlpctstr-message-lpctstr-lpcaption-uint-utype"></a>int ShowMessageBox(LPCTSTR message, LPCTSTR lpCaption, UINT uType)  
 Este método muestra un cuadro de mensaje con el texto y el título que se proporcionan. El parámetro **uType** tiene cualquier valor que se pueda proporcionar a la función **MessageBox** de Win32.  

##### <a name="bool-inpreviewvoid"></a>BOOL InPreview(void)  
 Este método devuelve TRUE si el asistente se inició en modo de "vista previa" proporcionando el modificador **/preview**. En el modo de vista previa, el botón **Siguiente** nunca está deshabilitado. Este método permite omitir el código en modo de vista previa, por ejemplo, que podría producir problemas cuando no hay datos válidos en la página.  

##### <a name="hwnd-gethwndvoid"></a>HWND GetHwnd(void)  
 Este método devuelve el **HWND** para el cuadro de diálogo principal. Use este método con cuidado. Por lo general, la interfaz de programación de aplicaciones del Asistente para UDI está diseñada para que nunca se trabaje directamente con los identificadores de ventana.  

#### <a name="iwizardpageview-interface"></a>Interfaz IWizardPageView  

```  
__interface IWizardPageView : IUnknown  
{  
    HRESULT GetControlWrapper(int itemId, DialogControlTypes controlType, IUnknown **ppControl);  
    HWND GetHwnd(void);  
    HWND GetControl(int itemId);  
    HRESULT Show (void);  
    HRESULT Hide(void);  
    HRESULT Focus(int itemId);  
    IWizardPage * Page(void);  
    IFormController * Form(void);  

    HRESULT FocusWizardButton(WizardButtons button);  
    HRESULT SetEnable(WizardButtons button, BOOL enable);  
    void ShowWarningMessage(LPCTSTR message);  
    void HideWarningMessage(void);  
};  
```  

 Esta interfaz está disponible para el código de la página a través del método **View** (implementado por **WizardPageImpl**).  

##### <a name="hresult-getcontrolwrapperint-itemid-dialogcontroltypes-controltype-iunknown-ppcontrol"></a>HRESULT GetControlWrapper(int itemId, DialogControlTypes controlType, IUnknown \*ppControl)  
 El Asistente para UDI usa *contenedores*, que en realidad son fachadas para interactuar con los controles de la página. Al usar estas fachadas en lugar de los controles reales es mucho más fácil escribir pruebas para la página, porque se pueden proporcionar fachadas ficticias desde las pruebas.  

 En lugar de usar este método directamente, es mejor usar el método de plantilla, **GetControlWrapper** que está fuertemente tipado, por ejemplo:  

```  
PComboBox m_pLanguagePackCombo;  
GetControlWrapper(View(), IDC_MY_COMBO, CONTROL_COMBO_BOX, &m_pCombo);  
```  

##### <a name="hwnd-gethwndvoid"></a>HWND GetHwnd(void)  
 Este método devuelve el identificador de ventana de la página. Por lo general, no debería ser necesario el acceso a este identificador de ventana.  

##### <a name="hwnd-getcontrolint-itemid"></a>HWND GetControl(int itemId)  
 Si es necesario, se puede llamar a este método para obtener el identificador de ventana para un control de la página. (Es mejor llamar a la función de plantilla **GetControlWrapper**).  

##### <a name="hresult-show-void"></a>HRESULT Show (void)  
 Este método es solo para uso interno.  

##### <a name="hresult-hidevoid"></a>HRESULT Hide(void)  
 Este método es solo para uso interno.  

##### <a name="hresult-focusint-itemid"></a>HRESULT Focus(int itemId)  
 Establecer el foco de entrada en un control específico.  

##### <a name="iwizardpage--pagevoid"></a>IWizardPage * Page(void)  
 Este método es solo para uso interno.  

##### <a name="iformcontroller--formvoid"></a>IFormController * Form(void)  
 Este método es solo para uso interno.  

##### <a name="hresult-focuswizardbuttonwizardbuttons-button"></a>HRESULT FocusWizardButton(WizardButtons button)  
 Establece el foco en uno de los botones del asistente. **WizardButtons** tiene dos valores: **BackButton** y **NextButton**.  

##### <a name="hresult-setenablewizardbuttons-button-bool-enable"></a>HRESULT SetEnable(WizardButtons button, BOOL enable)  
 Solicitud para habilitar o deshabilitar uno de los botones del asistente. Es posible que el botón no coincida con el estado que se solicita. Por ejemplo, si se ejecuta el Asistente para UDI con el modificador **/preview**, los botones siempre estarán habilitados. **WizardButtons** tiene dos valores: **BackButton** y **NextButton**.  

##### <a name="void-showwarningmessagelpctstr-message"></a>void ShowWarningMessage(LPCTSTR message)  
 Este método muestra un mensaje de advertencia en la parte inferior del área de contenido de la página. Este mensaje puede ser cualquier texto.  

##### <a name="void-hidewarningmessagevoid"></a>void HideWarningMessage(void)  
 Ocultar un mensaje de advertencia que se ha mostrado con una llamada a **ShowWarningMessage**.  

#### <a name="ixmldocument-interface"></a>Interfaz IXmlDocument  

```  
__interface IXmlDocument : IUnknown  
    HRESULT Load(LPCTSTR filename);  
    HRESULT LoadXml(LPCTSTR xml);  
    HRESULT Save(LPCWSTR filename);  
    HRESULT GetParseErrorMessage(LPBSTR pMessage);  
    HRESULT SelectNodes(LPCTSTR xpath, IXMLDOMNodeList **ppNodes);  
    HRESULT SelectSingleNode(LPCTSTR xpath, IXMLDOMNode **ppNode);  
    HRESULT AddSchema(LPCTSTR filename, LPCTSTR ns);  
    HRESULT AddAttribute(IXMLDOMNode *pNode, LPCWSTR name, LPCWSTR value);  
    HRESULT CreateNode(DOMNodeType type, LPCWSTR name, LPCWSTR ns, IXMLDOMNode **ppNode);  
};  
```  

##### <a name="overview"></a>Información general  
 Esta interfaz se implementa mediante el componente **ID_IXmlDocument**, que es una fachada diseñada para que sea más fácil trabajar con documentos XML en C++.  

##### <a name="hresult-loadlpctstr-filename"></a>HRESULT Load(LPCTSTR filename)  
 Este método carga un documento XML desde un archivo externo. Devuelve **S_OK** si el archivo se cargó sin errores o **S_FALSE** si se produjo un error. Cuando se produce un error, se puede obtener el mensaje de error mediante una llamada a **GetParseErrorMessage**.  

##### <a name="hresult-loadxmllpctstr-xml"></a>HRESULT LoadXml(LPCTSTR xml)  
 Este método carga un documento XML desde una cadena en lugar de un archivo externo. Aparte del origen para leer el archivo XML, el comportamiento es el mismo que el del método **Load**.  

##### <a name="hresult-savelpcwstr-filename"></a>HRESULT Save(LPCWSTR filename)  
 Este método guarda en un archivo externo el documento XML que está en la memoria.  

##### <a name="hresult-getparseerrormessagelpbstr-pmessage"></a>HRESULT GetParseErrorMessage(LPBSTR pMessage)  
 Este método devuelve una cadena nueva con el mensaje de error de la carga del documento XML, si existe. Siempre devuelve **S_OK**.  

##### <a name="hresult-selectnodeslpctstr-xpath-ixmldomnodelist-ppnodes"></a>HRESULT SelectNodes(LPCTSTR xpath, IXMLDOMNodeList \**ppNodes)  
 Este método permite usar una expresión XPath para recuperar una colección de nodos del documento. Siempre devuelve **S_OK**.  

##### <a name="hresult-selectsinglenodelpctstr-xpath-ixmldomnode-ppnode"></a>HRESULT SelectSingleNode(LPCTSTR xpath, IXMLDOMNode \**ppNode)  
 Este método permite usar una expresión XPath para recuperar un nodo del documento. Siempre devuelve **S_OK**.  

##### <a name="hresult-addschemalpctstr-filename-lpctstr-ns"></a>HRESULT AddSchema(LPCTSTR filename, LPCTSTR ns)  
 Este método agrega el nombre de un archivo de esquema externo que se usará para validar el esquema del documento XML cuando se cargue. El espacio de nombres que se proporciona es la cadena que se puede usar en las consultas XPath, aunque esto no se ha probado.  

##### <a name="hresult-addattributeixmldomnode-pnode-lpcwstr-name-lpcwstr-value"></a>HRESULT AddAttribute(IXMLDOMNode \*pNode, LPCWSTR name, LPCWSTR value)  
 Este método agrega un atributo nuevo a un nodo existente en el documento XML. Vea la tabla 53.  

### <a name="table-53-hresult-addattribute"></a>Tabla 53. HRESULT AddAttribute  

|**Parámetro**|**Descripción**|  
|-|-|  
|**pNode**|El nodo al que se quiere agregar un atributo.|  
|**Nombre**|El nombre del atributo nuevo.|  
|**Valor**|El valor del atributo nuevo.|  

##### <a name="hresult-createnodedomnodetype-type-lpcwstr-name-lpcwstr-ns-ixmldomnode-ppnode"></a>HRESULT CreateNode(DOMNodeType type, LPCWSTR name, LPCWSTR ns, IXMLDOMNode \**ppNode)  
 Llame a este método para crear un nodo:  

```  
Pointer<IXMLDOMNode> pNewChild  
pXmlDom->CreateNode(NODE_ELEMENT, L"MyElement", L"", &pNewChild);  
```  

 Después de crear un nodo, se puede agregar como un elemento secundario a otro nodo mediante una llamada al método **appendChild** del elemento primario.  

### <a name="helper-functions"></a>Funciones auxiliares  

#### <a name="createinstance-template-function"></a>Función de plantilla CreateInstance  

```  
HRESULT CreateInstance(IWizardPageContainer *pContainer, LPCTSTR type, I **ppObject)  
```  

 Esta función se define en IWizardPageContainer.h y proporciona un contenedor con seguridad de tipos sobre el método **IWizardPageContainer->CreateInstance**, por ejemplo:  

```  
CreateInstance<IDirectory>(Container(), ID_Directory, &pDirectory);  
```  

 Este código crea un componente **ID_Directory** para recuperar la interfaz **IDirectory** de ese componente.  

#### <a name="getservice-template-function"></a>Función de plantilla GetService  

```  
void GetService(IWizardPageContainer *pContainer, I **ppService)  
```  

 Esta función se define en IWizardPageContainer.h y proporciona un contenedor con seguridad de tipos sobre el método **IWizardPageContainer->GetService**, por ejemplo:  

```  
GetService<ITSVariableBag>(Container(), &pTsBag);  
```  

 Esta función recupera el componente de secuencia de tareas, que es compatible con la interfaz **ITSVariableBag**. (Para **ITSVariableBag**, en su lugar se puede usar el método TSVariables de la clase **WizardPageImpl**).  

### <a name="udi-wizard-designer-configuration-file-schema-reference"></a>Referencia de esquema de archivo de configuración del diseñador del Asistente para UDI  
 Este archivo lo usa el diseñador del Asistente para UDI. Se crea un archivo independiente para cada archivo .dll personalizado, que puede contener editores de páginas del asistente personalizados, tareas personalizadas o validadores personalizados. El archivo debe terminar con *.config* y residir en *carpeta_de_instalación*\Bin\Config (donde *carpeta_de_instalación* es la carpeta en la que instaló MDT).  

  En la tabla 54 se enumeran los elementos del archivo de configuración del diseñador del Asistente para UDI y sus descripciones. El elemento **DesignerConfig** es el nodo raíz para esta referencia.  

### <a name="table-54-elements-in-the-udi-wizard-designer-configuration-file-and-their-descriptions"></a>Tabla 54. Elementos del archivo de configuración del diseñador del Asistente para UDI y sus descripciones  

|**Nombre de elemento**|**Descripción**|  
|-|-|  
|[DesignerConfig](#DesignerConfig)|Especifica el directorio raíz para todos los demás elementos.|  
|[DesignerMappings](#DesignerMappings)|Agrupa un conjunto de elementos [Page](#Page).|  
|[Page](#Page)|Especifica un editor de páginas del asistente para cargar en el diseñador del Asistente para UDI, que se usa para editar las opciones de configuración de una página del asistente.|  
|[Param](#Param)|Especifica un parámetro que se pasa al elemento primario [Task](#Task) o [Validator](#Validator), y se corresponde a un elemento [Setter]() del archivo de configuración del Asistente para UDI **Nota:** Los atributos de este elemento son diferentes si el elemento primario es [Task](#Task) o [Validator](#Validator).|  
|[Task](#Task)|Especifica una tarea dentro de la biblioteca de tareas.|  
|[TaskItem](#TaskItem)|Especifica un grupo de parámetros que se pasan a la tarea.|  
|[TaskLibrary](#TaskLibrary)|Agrupa un conjunto de elementos [Task](#Task).|  
|[Validator](#Validator)|Especifica un validador dentro de la biblioteca de validadores.|  
|[ValidatorLibrary](#ValidatorLibrary)|Agrupa un conjunto de elementos [Validator](#Validator).|  

####  <a name="DesignerConfig"></a> DesignerConfig  
 Este elemento especifica el directorio raíz para todos los demás elementos.  

##### <a name="element-information"></a>Información del elemento  
  En la tabla 55 se ofrece información sobre el elemento [DesignerConfig](#DesignerConfig).  

### <a name="table-55-designerconfig-element-information"></a>Tabla 55. Información del elemento DesignerConfig  

|**Atributo**|**Valor**|  
|-|-|  
|Número de repeticiones|Una: este elemento es necesario.|  
|Elementos primarios|Ninguno|  
|Contenido|**DesignerMappings**, **TaskLibrary**, **ValidatorLibrary**|  

##### <a name="element-attributes"></a>Atributos del elemento  
 Este elemento no tiene atributos.  

##### <a name="remarks"></a>Comentarios  
 Ninguna.  

##### <a name="example"></a>Ejemplo  

```  
<DesignerConfig>  
   + <TaskLibrary>  
   + <ValidatorLibrary>  
   + <DesignerMappings>  
</DesignerConfig>  
```  

####  <a name="DesignerMappings"></a> DesignerMappings  
 Este elemento agrupa un conjunto de elementos [Page](#Page).  

##### <a name="element-information"></a>Información del elemento  
  En la tabla 56 se ofrece información sobre el elemento [DesignerMappings](#DesignerMappings).  

### <a name="table-56-designermappings-element-information"></a>Tabla 56. Información del elemento DesignerMappings  

|**Atributo**|**Valor**|  
|-|-|  
|Número de repeticiones|Cero o una dentro del elemento [DesignerConfig](#DesignerConfig) (este elemento es opcional si no hay ninguna página del asistente personalizada en el archivo DLL que se corresponde a este archivo de configuración del diseñador del Asistente para UDI).|  
|Elementos primarios|**DesignerConfig**|  
|Contenido|**Page**|  

##### <a name="element-attributes"></a>Atributos del elemento  
 Este elemento no tiene atributos.  

##### <a name="remarks"></a>Comentarios  
 Ninguna.  

##### <a name="example"></a>Ejemplo  

```  
<DesignerConfig>  
   + <TaskLibrary>  
   + <ValidatorLibrary>  
   - <DesignerMappings>  
        <Page DLL="SharedPages.dll"  
           Description="Used to display text that describes the current stagegroup"  
           Type="Microsoft.SharedPages.WelcomePage"  
           DisplayName="Welcome"   
           Image="Welcome_188.png"  
           DesignerType="Microsoft.Enterprise.UDIDesigner.CoreModules.Views.WelcomePageView"  
           DesignerAssembly="Microsoft.Enterprise.UDIDesigner.CoreModules.dll"/>  
        <Page DLL="OSDRefreshWizard.dll"  
           Description="Captures or restores user state data"  
           Type="Microsoft.OSDRefresh.UserStatePage"  
           DisplayName="User Data"  
           Image="UserState_188.png"  
           DesignerType="Microsoft.Enterprise.UDIDesigner.CoreModules.Views.UserStatePageView"  
           DesignerAssembly="Microsoft.Enterprise.UDIDesigner.CoreModules.dll"/>  
        <Page DLL="OSDRefreshWizard.dll"  
           Description="Allows selecting the image to install, target drive, and whether to format"  
           Type="Microsoft.OSDRefresh.VolumePage"  
           DisplayName="Volume"  
           Image="Volume_188.png"  
           DesignerType="Microsoft.Enterprise.UDIDesigner.CoreModules.Views.VolumePageView"  
           DesignerAssembly="Microsoft.Enterprise.UDIDesigner.CoreModules.dll"/>  
     </DesignerMappings>  
</DesignerConfig>  
```  

####  <a name="Page"></a> Page  
 Este elemento especifica un editor de páginas del asistente para cargar en el diseñador del Asistente para UDI, que se usa para editar las opciones de configuración de una página del asistente.  

##### <a name="element-information"></a>Información del elemento  
En la tabla 57 se proporciona información sobre el elemento [Page](#Page).  

### <a name="table-57-page-element-information"></a>Tabla 57. Información del elemento Page  

|**Atributo**|**Valor**|  
|-|-|  
|Número de repeticiones|Una o varias para cada página del asistente que se define en el elemento [DesignerMappings](#DesignerMappings).|  
|Elementos primarios|**DesignerMappings**|  
|Contenido|Cualquier contenido de XML con formato correcto.|  

##### <a name="element-attributes"></a>Atributos del elemento  
En la tabla 58 se enumeran los atributos del elemento [Page](#Page) y una descripción para cada uno.  

### <a name="table-58-attributes-and-corresponding-values-for-the-page-element"></a>Tabla 58. Atributos y valores correspondientes para el elemento Page  

|**Atributo**|**Descripción**|  
|-|-|  
|**Descripción**|Especifica el texto que proporciona información sobre el parámetro, que se muestra en el diseñador del Asistente para UDI.|  
|**DesignerAssembly**|Especifica el nombre del archivo .dll asociado con el editor de páginas del asistente (el archivo .dll debe existir en *carpeta_de_instalación*\Bin (donde *carpeta_de_instalación* es la carpeta en la que se instaló MDT).|  
|**DesignerType**|Especifica el nombre del editor de páginas del asistente en el archivo .dll especificado en el atributo **DesignerAssembly** (es el tipo de Microsoft .NET para el editor de páginas del asistente, con el espacio de nombres completo de Microsoft .NET).|  
|**DisplayName**|Especifica el nombre descriptivo del editor de página, que se muestra en el diseñador del Asistente para UDI.|  
|**DLL**|Especifica el nombre del archivo .dll asociado con la página del asistente (el archivo debe existir en *carpeta_de_instalación*\Templates\Distribution\Tools\\*plataforma* (donde *carpeta_de_instalación* es la carpeta en la que instaló MDT y *plataforma* es **x86** para la versión de 32 bits o **x64** para la versión de 64 bits). **Nota:** Asegúrese de que la arquitectura de procesador de DLL coincide con la arquitectura de procesador de MDT instalada. Por ejemplo, si instaló una versión de 32 bits de MDT, asegúrese de usar un archivo DLL de 32 bits para la página del asistente.|  
|**Imagen**|Especifica el nombre de una imagen de la página que está en formato PNG (Portable Network Graphics) (El archivo .png debe existir en *carpeta_de_instalación*\Bin\Images (donde *carpeta_de_instalación* es la carpeta en la que instaló MDT).|  
|**Tipo**|Especifica el editor de páginas del asistente y debe coincidir con la instancia con nombre que usó cuando se registró la página personalizada.|  

##### <a name="remarks"></a>Comentarios  
 En el diseñador del Asistente para UDI se usa el elemento [Page](#Page) como una plantilla para crear el código XML inicial para un asistente nuevo. El diseñador del Asistente para UDI realiza la validación de esquema para asegurarse de que el elemento [Page](#Page) y los elementos secundarios tienen un formato válido. Este elemento proporciona una asignación entre el tipo de página del Asistente para UDI y la información que necesita el diseñador del Asistente para UDI para editar y crear páginas de este tipo mediante el editor de páginas personalizado.  

##### <a name="example"></a>Ejemplo  
 Ninguna.  

####  <a name="Param"></a> Param  
 Este elemento especifica un parámetro que se pasa al elemento primario [Task](#Task) o [Validator](#Validator), y se corresponde a un elemento [Setter]() del archivo de configuración del Asistente para UDI.  

> [!NOTE]
>  Los atributos de este elemento son diferentes si el elemento primario es [Task](#Task) o [Validator](#Validator).  

##### <a name="element-information"></a>Información del elemento  
 En la tabla 59 se ofrece información sobre el elemento [Param](#Param).  

### <a name="table-59-param-element-information"></a>Tabla 59. Información del elemento Param  

|**Atributo**|**Valor**|  
|-|-|  
|Número de repeticiones|Una o varias para cada elemento primario [TaskItem](#TaskItem) o [Validator](#Validator).|  
|Elementos primarios|**TaskItem**, **Validator**|  
|Contenido|Cualquier contenido de XML con formato correcto.|  

##### <a name="element-attributes"></a>Atributos del elemento  
  En la tabla 60 se enumeran los atributos del elemento [Param](#Param) y se ofrece una descripción de cada uno.  

### <a name="table-60-attributes-and-corresponding-values-for-the-param-element"></a>Tabla 60. Atributos y valores correspondientes para el elemento Param  

|**Atributo**|**Descripción**|  
|-|-|  
|**Descripción**|Especifica el texto que proporciona información sobre el parámetro, que se muestra en el diseñador del Asistente para UDI. **Nota:** Este atributo solo es válido para el elemento [Validator](#Validator).|  
|**DisplayName**|Especifica el nombre descriptivo del parámetro de validador, que se muestra en la página del Asistente para UDI apropiada en el diseñador del Asistente para UDI (normalmente este nombre es más descriptivo que el atributo **Nombre**). **Nota:** Este atributo solo es válido para el elemento [Validator](#Validator).|  
|**Nombre**|Especifica el nombre del parámetro que se pasa a la tarea o al validador, en función del elemento primario (este atributo se convertirá en el atributo **Propiedad** de un elemento [Setter]() en el archivo de configuración del Asistente para UDI). **Nota:** Este parámetro se usa para los elementos primarios [TaskItem](#TaskItem) y [Validator](#Validator).|  

##### <a name="remarks"></a>Comentarios  
 Ninguna.  

##### <a name="example"></a>Ejemplo  
 Ninguna.  

####  <a name="Task"></a> Task  
 Este elemento especifica una tarea dentro de la biblioteca de tareas.  

##### <a name="element-information"></a>Información del elemento  
 En la tabla 61 se proporciona información sobre el elemento [Task](#Task).  

### <a name="table-61-task-element-information"></a>Tabla 61. Información del elemento Task  

|**Atributo**|**Valor**|  
|-|-|  
|Número de repeticiones|Una o varias en el elemento [TaskLibrary](#TaskLibrary) (este elemento no es opcional si se especifica el elemento **TaskLibrary**).|  
|Elementos primarios|**TaskLibrary**|  
|Contenido|**TaskItem**|  

##### <a name="element-attributes"></a>Atributos del elemento  
  En la tabla 62 se enumeran los atributos del elemento [Task](#Task) y se ofrece una descripción de cada uno.  

### <a name="table-62-attributes-and-corresponding-values-for-the-task-element"></a>Tabla 62. Atributos y valores correspondientes para el elemento Task  

|**Atributo**|**Descripción**|  
|-|-|  
|**Descripción**|Especifica el texto que proporciona información sobre la tarea, que se muestra en el diseñador del Asistente para UDI.|  
|**DLL**|Especifica el nombre del archivo .dll asociado con la tarea (el archivo .dll debe existir en *carpeta_de_instalación*\Templates\Distribution\Tools\\*plataforma* (donde *carpeta_de_instalación* es la carpeta en la que se instaló MDT y *plataforma* es **x86** para la versión de 32 bits o **x64** para la versión de 64 bits).|  
|**Nombre**|Especifica el nombre de la tarea, que se muestra en la página del Asistente para UDI adecuada y en el diseñador del Asistente para UDI.|  
|**Tipo**|Especifica el tipo de tarea, que se registra con el registro de fábrica y se usa para llamar a una tarea específica dentro de un archivo .dll.|  

##### <a name="remarks"></a>Comentarios  
 Ninguna.  

##### <a name="example"></a>Ejemplo  
 Ninguna.  

####  <a name="TaskItem"></a> TaskItem  
 Este elemento especifica un grupo de parámetros que se pasan a la tarea.  

##### <a name="element-information"></a>Información del elemento  
  En la tabla 63 se proporciona información sobre el elemento [TaskItem](#TaskItem).  

### <a name="table-63-taskitem-element-information"></a>Tabla 63. Información del elemento TaskItem  

|**Atributo**|**Valor**|  
|-|-|  
|Número de repeticiones|Una o varias para cada elemento **Task**.|  
|Elementos primarios|**Task**|  
|Contenido|**Param**|  

##### <a name="element-attributes"></a>Atributos del elemento  
 En la tabla 64 se enumeran los atributos del elemento [TaskItem](#TaskItem) y se ofrece una descripción de cada uno.  

### <a name="table-64-attribute-and-corresponding-values-for-the-taskitem-element"></a>Tabla 64. Atributos y valores correspondientes para el elemento TaskItem  

|**Atributo**|**Descripción**|  
|-|-|  
|**Tipo**|Especifica del tipo de elemento que se va a crear en el archivo de configuración del Asistente para UDI. Se creará un elemento XML que se corresponde con el valor de este atributo. Por ejemplo, si el valor de este atributo es [File](#File), se creará un elemento **File** en el archivo de configuración del Asistente para UDI.<br /><br /> Actualmente, los únicos valores admitidos son estos:<br /><br /> -   **File**, que requiere dos elementos secundarios [Param](#Param) (un elemento secundario **Param** con el atributo **Nombre** establecido en **Origen** y otro elemento secundario **Param** con el atributo **Nombre** establecido en **Dest**).<br />-   [Setter](), que requiere un elemento secundario **Param**.|  

##### <a name="remarks"></a>Comentarios  
 Ninguna.  

##### <a name="example"></a>Ejemplo  
 Ninguna.  

####  <a name="TaskLibrary"></a> TaskLibrary  
 Este elemento agrupa un conjunto de elementos [Task](#Task).  

##### <a name="element-information"></a>Información del elemento  
 En la tabla 65 se proporciona información sobre el elemento [TaskLibrary](#TaskLibrary).  

### <a name="table-65-tasklibrary-element-information"></a>Tabla 65. Información del elemento TaskLibrary  

|**Atributo**|**Valor**|  
|-|-|  
|Número de repeticiones|Cero o una dentro del elemento [DesignerConfig](#DesignerConfig) (este elemento es opcional si no hay tareas personalizadas en el archivo DLL que se corresponde a este archivo de configuración del diseñador del Asistente para UDI).|  
|Elementos primarios|**DesignerConfig**|  
|Contenido|**Task**|  

##### <a name="element-attributes"></a>Atributos del elemento  
 Este elemento no tiene atributos.  

##### <a name="remarks"></a>Comentarios  
 Ninguna.  

##### <a name="example"></a>Ejemplo  

```  
<DesignerConfig>  
   - <TaskLibrary>  
        +<Task DLL="" Description="Executes a process with the given command line." Type="Microsoft.Wizard.ShellExecuteTask" Name="Shell Execute Task">  
        +<Task DLL="OSDRefreshWizard.dll" Description="Discovers supported applications for install." Type="Microsoft.OSDRefresh.AppDiscoveryTask" Name="Application Discovery">  
        +<Task DLL="SharedPages.dll" Description="Check to ensure a wired network connection is available." Type="Microsoft.SharedPages.WiredNetworkTask" Name="Wired Network Check">  
        +<Task DLL="OSDRefreshWizard.dll" Description="Check to ensure power source is AC (not battery)." Type="Microsoft.OSDRefresh.ACPowerTask" Name="AC Power Check">  
        +<Task DLL="" Description="Check to ensure power source is AC (not battery)." Type="Microsoft.Wizard.CopyFilesTask" Name="Copy Files Task">  
     </TaskLibrary>  
   + <ValidatorLibrary>  
   + <DesignerMappings>  
</DesignerConfig>  
```  

####  <a name="Validator"></a> Validator  
 Este elemento especifica un validador dentro de la biblioteca de validadores.  

##### <a name="element-information"></a>Información del elemento  
 En la tabla 66 se proporciona información sobre el elemento [Validator](#Validator).  

### <a name="table-66-validator-element-information"></a>Tabla 66. Información del elemento Validator  

|**Atributo**|**Valor**|  
|-|-|  
|Número de repeticiones|Cero o más dentro del elemento [ValidatorLibrary](#ValidatorLibrary) (este elemento es opcional).|  
|Elementos primarios|**ValidatorLibrary**|  
|Contenido|**Param**|  

##### <a name="element-attributes"></a>Atributos del elemento  
En la tabla 67 se enumeran los atributos del elemento [Validator](#Validator) y se ofrece una descripción de cada uno.  

### <a name="table-67-attributes-and-corresponding-values-for-the-validator-element"></a>Tabla 67. Atributos y valores correspondientes para el elemento Validator  

|**Atributo**|**Descripción**|  
|-|-|  
|**Descripción**|Especifica el texto que proporciona información sobre el validador, que se muestra en el diseñador del Asistente para UDI.|  
|**DisplayName**|Especifica el nombre descriptivo del validador que se muestra en el diseñador del Asistente para UDI (normalmente este nombre es más descriptivo que el atributo **Nombre**).|  
|**DLL**|Especifica el nombre del archivo .dll asociado con el validador (el archivo .dll debe existir en *carpeta_de_instalación*\Templates\Distribution\Tools\\*plataforma* (donde *carpeta_de_instalación* es la carpeta en la que se instaló MDT y *plataforma* es **x86** para la versión de 32 bits o **x64** para la versión de 64 bits).|  
|**Nombre**|Especifica el nombre del validador, que se muestra en la página del Asistente para UDI adecuada y en el diseñador del Asistente para UDI.|  
|**Tipo**|Especifica el tipo de validador, que se registra con el generador de registros y se usa para llamar a una tarea específica dentro de un archivo .dll.|  

##### <a name="remarks"></a>Comentarios  
 Ninguna.  

##### <a name="example"></a>Ejemplo  
 Ninguna.  

####  <a name="ValidatorLibrary"></a> ValidatorLibrary  
 Este elemento agrupa un conjunto de elementos [Validator](#Validator).  

##### <a name="element-information"></a>Información del elemento  
 En la tabla 68 se proporciona información sobre el elemento [ValidatorLibrary](#ValidatorLibrary).  

### <a name="table-68-validatorlibrary-element-information"></a>Tabla 68. Información del elemento ValidatorLibrary  

|**Atributo**|**Valor**|  
|-|-|  
|Número de repeticiones|Cero o una dentro del elemento [DesignerConfig](#DesignerConfig) (este elemento es opcional si no hay validadores personalizados en el archivo DLL que se corresponde a este archivo de configuración del diseñador del Asistente para UDI).|  
|Elementos primarios|**DesignerConfig**|  
|Contenido|**Validator**|  

##### <a name="element-attributes"></a>Atributos del elemento  
 Este elemento no tiene atributos.  

##### <a name="remarks"></a>Comentarios  
 Ninguna.  

##### <a name="example"></a>Ejemplo  
 <DesignerConfig\>   + <TaskLibrary\>   - <ValidatorLibrary\>        +<Validator DLL="" Description="Requires text in a field" Type="Microsoft.Wizard.Validation.NonEmpty" Name="NonEmpty"\>        +<Validator DLL="" Description="Doesn't allow certain characters to be in a field" Type="Microsoft.Wizard.Validation.InvalidChars" Name="InvalidChars"\>        +<Validator DLL="" Description="Must follow a pre-defined pattern" Type="Microsoft.Wizard.Validation.RegEx" Name="NamedPattern"\>        +<Validator DLL="" Description="Require the contents match a regular expression" Type="Microsoft.Wizard.Validation.RegEx" Name="RegEx"\>     </ValidatorLibrary\>   + <DesignerMappings\></DesignerConfig\>  

## <a name="udi-wizard-designer-reference"></a>Referencia del diseñador del Asistente para UDI  

### <a name="controls"></a>Controles  
 Los controles que se usan para crear editores de páginas del asistente personalizados para su uso en el diseñador del Asistente para UDI son instancias de **UserControl** de WPF. En la tabla 69 se muestran los controles que se pueden usar para crear editores de páginas del asistente personalizados.  

### <a name="table-69-controls-that-can-be-used-to-create-custom-wizard-page-editors"></a>Tabla 69. Controles que se pueden usar para crear editores de páginas del asistente personalizados  

|Control|Descripción|  
|-|-|  
|[CollectionTControl](#CollectionTControl)|Este control se usa para modificar los datos almacenados en el elemento [Data](#Data) dentro de un elemento [Page](#Page).|  
|[FieldElementControl](#FieldElementControl)|Este control se usa para modificar un campo, que normalmente está vinculado a un control TextBox en la página .xaml.|  
|[SetterControl](#SetterControl)|Este control se usa para modificar el valor de un elemento [setter]() en el archivo de configuración del Asistente para UDI.|  

####  <a name="CollectionTControl"></a> CollectionTControl  
 Este control proporciona muchas funciones para modificar los datos. La mejor manera de obtener información sobre cómo usar este control consiste en examinar el ejemplo, en el que se muestra cómo modificar los datos bajo el elemento **Data** de una página. En concreto, en el ejemplo se muestra cómo agregar, quitar y modificar elementos de este control.  

####  <a name="FieldElementControl"></a> FieldElementControl  
 Use este control para modificar un campo, que normalmente está vinculado a un control **TextBox** en la página .xaml.  

##### <a name="example"></a>Ejemplo  
 En el fragmento siguiente de un archivo .xaml se muestra el uso de **FieldElementControl** para configurar el valor predeterminado para un campo en una página del asistente con un control **TextBox** secundario:  

```  
<Controls:FieldElementControl  
Width="450"  
Margin="0,5"  
FieldData="{Binding DataContext.Location, ElementName=ControlRoot}"  
HeaderText="Location Combo Box"  
InstructionText="Here you can configure the behavior of the location combo box."  
HideValidationTab="True">  

<TextBox Text="{Binding FieldData.DefaultValue,  
 UpdateSourceTrigger=PropertyChanged,  
 Mode=TwoWay}"/>  
</Controls:FieldElementControl>  
```  

##### <a name="properties"></a>Propiedades  

###### <a name="fielddata"></a>FieldData  
 Esta propiedad de cadena contiene información para conectar **FieldElementControl** al código XML subyacente del campo. La conexión se realiza a una propiedad de la interfaz de editor de la página. En el fragmento siguiente de un archivo .xaml se muestra el uso de la propiedad **FieldData**:  

```  
FieldData="{Binding DataContext.Location, ElementName=ControlRoot}"  
```  

 En este fragmento, la interfaz de editor de página se denomina **ControlRoot** y se especifica en el parámetro **ElementName**. El enlace se realiza a la propiedad **DataContext.Location** de la interfaz del editor de página **ControlRoot**. **DataContext** es un modelo de vista que apunta al elemento [Page](#Page) dentro del archivo de configuración del Asistente para UDI. **Location** es una propiedad de la vista que devuelve una lista de las ubicaciones posibles y se define mediante un elemento [Data](#Data) dentro del archivo de configuración del Asistente para UDI. Cada ubicación se define mediante un elemento [DataItem](#DataItem) dentro del archivo de configuración del Asistente para UDI.  

###### <a name="headertext"></a>HeaderText  
 Esta propiedad de cadena permite especificar un encabezado para el control [FieldElementControl](#FieldElementControl). El encabezado actúa como un título para el control y se le da formato como texto de color naranja en negrita que se muestra inmediatamente encima del control.  

###### <a name="instructiontext"></a>InstructionText  
 Esta propiedad de cadena permite especificar texto informativo para el control [FieldElementControl](#FieldElementControl). Por lo general, el texto se usa para proporcionar una breve descripción del campo y explicar cómo la configuración del campo afecta a la correspondiente página del asistente.  

###### <a name="hideenablebutton"></a>HideEnableButton  
 Esta propiedad booleana permite controlar la visibilidad del botón que cambia el estado entre **Desbloqueado** y **Bloqueado** (habilitado o deshabilitado). Si se establece en:  

-   **True**, el botón no es visible.  

-   **False**, el botón es visible (es el valor predeterminado).  

###### <a name="hidedefaulttab"></a>HideDefaultTab  
 Esta propiedad booleana permite controlar la visibilidad de la sección que contiene el control que se usa para establecer el valor predeterminado. Aunque la propiedad hace referencia a una pestaña, no hay ninguna en [FieldElementControl](#FieldElementControl), sino una sección que se puede ocultar. Si se establece en:  

-   **True**, la sección no es visible.  

-   **False**, la sección es visible (es el valor predeterminado).  

###### <a name="hideborder"></a>HideBorder  
 Esta propiedad booleana permite controlar la visibilidad del borde que rodea el control de campo. Si se establece en:  

-   **True**, el borde no es visible.  

-   **False**, el borde es visible (es el valor predeterminado).  

###### <a name="hideimage"></a>HideImage  
 Esta propiedad booleana permite controlar la visibilidad de la imagen configurada por la propiedad **FieldImageSource**. Si se establece en:  

-   **True**, la imagen no es visible.  

-   **False**, la imagen es visible (es el valor predeterminado).  

###### <a name="hidevalidationtab"></a>HideValidationTab  
 Esta propiedad booleana permite controlar la visibilidad de la sección donde se administra la lista de validadores. Aunque la propiedad hace referencia a una pestaña, no hay ninguna en [FieldElementControl](#FieldElementControl), sino una sección que se puede ocultar. Si se establece en:  

-   **True**, la sección no es visible.  

-   **False**, la sección es visible (es el valor predeterminado).  

###### <a name="hidesummarytab"></a>HideSummaryTab  
 Esta propiedad booleana permite controlar la visibilidad de la sección en la que se configura el título de resumen del campo. El título y el valor correspondiente del campo se muestran en un tipo de página del asistente **SummaryPage** en un flujo de fases. Aunque la propiedad hace referencia a una pestaña, no hay ninguna en [FieldElementControl](#FieldElementControl), sino una sección que se puede ocultar. Si se establece en:  

-   **True**, la sección no es visible.  

-   **False**, la sección es visible (es el valor predeterminado).  

###### <a name="hidetasksequencetab"></a>HideTaskSequenceTab  
 Esta propiedad booleana permite controlar la visibilidad de la sección en la que se configura la variable de secuencia de tareas que se corresponde al campo. Aunque la propiedad hace referencia a una pestaña, no hay ninguna en [FieldElementControl](#FieldElementControl), sino una sección que se puede ocultar. Si se establece en:  

-   **True**, la sección no es visible.  

-   **False**, la sección es visible (es el valor predeterminado).  


####  <a name="SetterControl"></a> SetterControl  
 Use este control para modificar el valor de un elemento [Setter]() en el archivo de configuración del Asistente para UDI. Este control contiene un control secundario que se usa para modificar el valor del elemento **setter**.  

##### <a name="example"></a>Ejemplo  
 En el fragmento siguiente de un archivo .xaml se muestra el uso de **SetterControl** para modificar un elemento [Setter]() denominado **KeyLocationSetter** con un control secundario **TextBox**.  

```  
<Controls:SetterControl Margin="5"  
        Width="450"  
        HeaderText="Title text"  
        SetterData="{Binding KeyLocationSetter}"   
        InstructionText="What this means…"  
        HorizontalAlignment="Left">  

    <TextBox  
                   Margin="0,3"  
                   Text="{Binding SetterData.SetterValue, Mode=TwoWay, UpdateSourceTrigger=PropertyChanged}"  
    />  

</Controls:SetterControl>  
```  

##### <a name="properties"></a>Propiedades  

###### <a name="setterdata"></a>SetterData  
 Es necesario enlazarlo con una propiedad de la vista o el modelo de vista que se conecta al establecedor. Esto es similar a cómo se enlazaría a un campo, como se describe para **FieldElementControl**.  

###### <a name="headertext"></a>HeaderText  
 Esta propiedad permite establecer el texto que aparecerá en el encabezado del control. Considere esta propiedad como un título para el control; de forma predeterminada, aparece como texto de color naranja en negrita.  

###### <a name="instructiontext"></a>InstructionText  
 Establezca esta propiedad en el texto que quiere que aparezca debajo del encabezado, normalmente texto de instrucciones que indica al usuario del editor personalizado cuándo y por qué le interesaría modificar el comportamiento del campo.  

### <a name="interfaces"></a>Interfaces  
En la tabla 70 se enumeran las interfaces que se pueden usar para crear editores de páginas del asistente personalizados.  

### <a name="table-70-interfaces-that-can-be-used-to-create-custom-wizard-page-editors"></a>Tabla 70. Interfaces que se pueden usar para crear editores de páginas del asistente personalizados  

|**Interfaz**|**Descripción**|  
|-|-|  
|[IDataService](#IDataService)|Use esta interfaz para conectar los campos a los elementos **Data** del archivo de configuración del Asistente para UDI.|  
|[IMessageBoxService](#IMessageBoxService)|Esta interfaz proporciona acceso a los métodos que se pueden usar para mostrar cuadros de mensaje.|  

####  <a name="IDataService"></a> IDataService  
 Esta interfaz contiene varias propiedades y métodos, pero solo hay una propiedad que probablemente necesite. Esa propiedad es la única que se documenta aquí.  

 Se puede usar la inserción de dependencias para obtener un puntero a esta interfaz mediante código similar al siguiente en la clase:  

```  
[Dependency]  
public IDataService DataService { get; set; }  
```  

##### <a name="properties"></a>Propiedades  
 En la tabla 71 se enumeran las propiedades de la interfaz **IDataService**.  

### <a name="table-71-properties-for-the-idataservice-interface"></a>Tabla 71. Propiedades para la interfaz IDataService  

|**Interfaz**|**Descripción**|  
|-|-|  
|[CurrentPage](#CurrentPage)|Esta propiedad proporciona acceso a los elementos, atributos y valores de XML bajo el contexto de la página actual que se está modificando en el archivo de configuración del Asistente para UDI.|  

######  <a name="CurrentPage"></a> CurrentPage  

```  
XElement CurrentPage { get; set; }  
```  

 Esta propiedad proporciona acceso al código XML para la página actual. Esta propiedad no se debe establecer nunca, pero tiene libertad para modificar el código XML de la página. En el editor de página de ejemplo se muestran ejemplos de cómo modificar el código XML. Use esta propiedad principalmente cuando tenga datos personalizados. Para los campos y propiedades (establecedores), se pueden usar controles creados previamente que se ocupen de todos los detalles.  

####  <a name="IMessageBoxService"></a> IMessageBoxService  
 Esta interfaz proporciona acceso a los métodos que se pueden usar para mostrar cuadros de mensaje. Es posible que se pregunte por qué se necesita una interfaz para mostrar un cuadro de mensaje. En realidad no es necesario: Microsoft usa esta interfaz con el código, ya que ayuda a escribir pruebas automatizadas para las páginas de diseñador.  

 Pero el uso de estos métodos proporciona una ventaja útil: los cuadros de diálogo siempre tienen el "propietario" establecido en el Asistente para UDI, lo que garantiza que el cuadro de diálogo se agrupa correctamente con la ventana principal.  

 Se puede usar la inserción de dependencias para obtener un puntero a esta interfaz mediante código similar al siguiente en la clase:  

```  
[Dependency]  
public IMessageBoxService MessageBoxes { get; set; }  
```  

##### <a name="methods"></a>Métodos  
 En la tabla 72 se enumeran los métodos para la interfaz **IMessageBoxService**.  

### <a name="table-72-methods-for-the-imessageboxservice-interface"></a>Tabla 72. Métodos para la interfaz IMessageBoxService  

|**Método**|**Descripción**|  
|-|-|  
|[ShowMessageBox](#ShowMessageBox)|Este método sobrecargado se usa para mostrar un cuadro de mensaje con los miembros siguientes:<br /><br /> -   [ShowMessageBox(String message, String caption, MessageBoxImage icon)](#ShowMessageBox_Stringmessage_Stringcaption_MessageBoxImage_icon)<br />-   [ShowMessageBox(string message, string caption, MessageBoxButton button, MessageBoxImage icon)](#ShowMessageBox_stringmessage_stringcaption_MessageBoxButtonbutton_MessageBoxImage_icon)<br />-   [ShowMessageBox(Exception exception)](#ShowMessageBox_Exception_exception)|  
|[ShowDialogWindow](#ShowDialogWindow)|Use este método para crear un cuadro de diálogo.|  
|[ShowWizardWindow](#ShowWizardWindow)|Use este método para mostrar un editor personalizado dentro de un cuadro de diálogo que incluya los botones **Siguiente** y **Atrás** para la navegación.|  

######  <a name="ShowMessageBox"></a> ShowMessageBox  
 Este método muestra un cuadro de mensaje que es un elemento secundario del editor de página del asistente personalizado. Este miembro está sobrecargado: en la tabla 73 se incluye una lista de los miembros y una breve descripción de cada uno. Para obtener información completa sobre cada miembro (incluida la sintaxis, el uso y ejemplos), vea la sección correspondiente a cada miembro.  

### <a name="table-73-overloaded-members-for-the-showmessagbox-method"></a>Tabla 73. Miembros sobrecargados para el método ShowMessagBox  

|Miembro|Descripción|  
|-|-|  
|[ShowMessageBox(String message, String caption, MessageBoxImage icon)](#ShowMessageBox_Stringmessage_Stringcaption_MessageBoxImage_icon)|Muestra un cuadro de mensaje con un icono y un botón **Aceptar**.|  
|[ShowMessageBox(string message, string caption, MessageBoxButton button, MessageBoxImage icon)](#ShowMessageBox_stringmessage_stringcaption_MessageBoxButtonbutton_MessageBoxImage_icon)|Muestra un cuadro de mensaje con un icono y otras combinaciones de botones posibles.|  
|[ShowMessageBox(Exception exception)](#ShowMessageBox_Exception_exception)|Muestra un cuadro de mensaje que proporciona información sobre una excepción y tiene un botón **Aceptar**.|  

######  <a name="ShowMessageBox_Stringmessage_Stringcaption_MessageBoxImage_icon"></a> ShowMessageBox(String message, String caption, MessageBoxImage icon)  

```  
void ShowMessageBox(String message, String caption, MessageBoxImage icon);  
```  

 Este método muestra un cuadro de mensaje con un botón **Aceptar**. Vea la tabla 74.  

### <a name="table-74-parameters-for-the-showmessageboxstring-message-string-caption-messageboximage-icon-method"></a>Tabla 74. Parámetros para el método ShowMessageBox(String message, String caption, MessageBoxImage icon)  

|**Parámetro**|**Descripción**|  
|-|-|  
|**message**|El mensaje que se va a mostrar en el área de contenido del cuadro de mensaje.|  
|**caption**|El texto que se va a mostrar en la barra de título del cuadro de diálogo.|  
|**icon**|El tipo de icono que se va a mostrar en el cuadro de mensaje.|  

######  <a name="ShowMessageBox_stringmessage_stringcaption_MessageBoxButtonbutton_MessageBoxImage_icon"></a> ShowMessageBox(string message, string caption, MessageBoxButton button, MessageBoxImage icon)  

```  
MessageBoxResult ShowMessageBox(string message, string caption, MessageBoxButton button, MessageBoxImage icon);  
```  

 Este método muestra un cuadro de mensaje con el conjunto de botones que se quieren mostrar y notifica en qué botón se ha hecho clic. Vea la tabla 75.  

### <a name="table-75-parameters-for-the-showmessageboxstring-message-string-caption-messageboxbutton-button-messageboximage-icon-method"></a>Tabla 75. Parámetros para el método ShowMessageBox(string message, string caption, MessageBoxButton button, MessageBoxImage icon)  

|**Parámetro**|**Descripción**|  
|-|-|  
|**message**|El mensaje que se va a mostrar en el área de contenido del cuadro de mensaje.|  
|**caption**|El texto que se va a mostrar en la barra de título del cuadro de diálogo.|  
|**button**|Los botones que se van a mostrar.|  
|**icon**|El tipo de icono que se va a mostrar en el cuadro de mensaje.|  

######  <a name="ShowMessageBox_Exception_exception"></a> ShowMessageBox(Exception exception)  

```  
void ShowMessageBox(Exception exception);  
```  

 Este método muestra un cuadro de mensaje que contiene información sobre una excepción. Este cuadro de mensaje tiene un único botón **Aceptar**. Vea la tabla 76.  

### <a name="table-76-parameters-for-the-showmessageboxexception-exception-method"></a>Tabla 76. Parámetros para el método ShowMessageBox(Exception exception)  

|**Parámetro**|**Descripción**|  
|-|-|  
|**exception**|La excepción que se quiere notificar (El cuadro de diálogo usa **exception.Message** como el contenido).|  

######  <a name="ShowDialogWindow"></a> ShowDialogWindow  

```  
void ShowDialogWindow(Type viewType, DialogInteraction dialogPayload);  
```  

 Este método crea un cuadro de diálogo, cuyo contenido es el texto proporcionado en el parámetro **viewType**. El diseñador de UDI crea una instancia de este tipo y la encapsula en un cuadro de diálogo que tiene botones **Aceptar** y **Cancelar**.  

 Los datos se pasan al control mediante el parámetro dialogPayload. En la solución **SampleEditor** del directorio del SDK se incluye un ejemplo de cómo usar esta funcionalidad.  

######  <a name="ShowWizardWindow"></a> ShowWizardWindow  

```  
void ShowWizardWindow(Type viewType, DialogInteraction dialogPayload);  
```  

 Este método permite mostrar un editor personalizado dentro de un cuadro de diálogo que incluye los botones **Siguiente** y **Atrás** para la navegación. Microsoft no ha proporcionado un ejemplo de cómo usar este método.  

###  <a name="UDIWizardConfigurationFileSchemaReference"></a> Referencia de esquema de archivo de configuración del Asistente para UDI  
 Este archivo lo usa el Asistente para UDI y lo configura el diseñador del Asistente para UDI. Este archivo se usa para configurar lo siguiente:  

-   Las páginas del asistente que se muestran en el Asistente para UDI.  

-   La secuencia de las páginas del asistente en el Asistente para UDI.  

-   Configuración de los campos de cada página del asistente.  

-   Elementos StageGroup disponibles en el diseñador del Asistente para UDI.  

-   Fases disponibles dentro de cada asistente para la implementación en el diseñador del Asistente para UDI.  

  En la tabla 77 se enumeran los elementos del archivo de configuración del Asistente para UDI y sus descripciones. El elemento **Wizard** es el nodo raíz para esta referencia.  

### <a name="table-77-elements-in-the-udi-wizard-configuration-file-and-their-descriptions"></a>Tabla 77. Elementos del archivo de configuración del Asistente para UDI y sus descripciones  

|**Nombre de elemento**|**Descripción**|  
|-|-|  
|[Data](#Data)|Agrupa los elementos [DataItem](#DataItem) individuales dentro de un elemento [Page](#Page) y se llama mediante el atributo **Nombre**.|  
|[DataItem](#DataItem)|Agrupa los elementos [Setter]() individuales dentro de un elemento [Page](#Page). Se pueden crear datos jerárquicos mediante la inclusión de uno o varios elementos [Data](#Data) dentro de un elemento [DataItem](#DataItem). Cada elemento **DataItem** representa un elemento individual. Por ejemplo, una lista de las unidades de disco disponibles podría tener un elemento **DataItem** para el nombre para mostrar y otro elemento **DataItem** para la letra de unidad correspondiente.|  
|[Predeterminado](#Default)|Especifica un valor predeterminado para el campo especificado en el elemento primario [Field](#Field) o [RadioGroup](#RadioGroup). El valor predeterminado se establece en el valor entre corchetes de este elemento.|  
|[DLL](#DLL)|Especifica un archivo DLL que el Asistente para UDI y el diseñador del Asistente para UDI van a cargar y hacer referencia.|  
|[DLLs](#DLLs)|Agrupa los elementos [DLL](#DLL) individuales.|  
|[Error](#Error)|Especifica el código de error posible que puede devolver una tarea. El **HRESULT** de la tarea devuelve el valor del código de error y este elemento lo captura para proporcionar información de error más específica.|  
|[ExitCode](#ExitCode)|Especifica un código de salida posible para una tarea. Los códigos de salida son códigos de retorno que la tarea espera. Cree un elemento **ExitCode** para cada código de salida posible. En caso contrario, puede especificar un asterisco (\*) en el atributo **Valor** para controlar los códigos de retorno que no se enumeran en otros elementos **ExitCode**.|  
|[ExitCodes](#ExitCodes)|Agrupa un conjunto de elementos [ExitCode](#ExitCode) y [Error](#Error) para un elemento [Task](#Task) o **Error**.|  
|[Field](#Field)|Especifica una instancia de un control en un elemento [Page](#Page) que se usa para proporcionar personalización mediante XML. No todos los controles permiten la personalización con XML, solo los que usan el elemento [Field](#Field).|  
|[Fields](#Fields)|Agrupa los elementos [Field](#Field) individuales dentro de un elemento [Page](#Page).|  
|[File](#File)|Especifica el origen y destino para una operación de copia de archivo mediante el tipo de tarea **Microsoft.Wizard.CopyFilesTask**. Se puede incluir un elemento **File** independiente para copiar más de un archivo en una sola tarea.|  
|[Page](#Page)|Especifica una instancia de una página e incluye todos los valores de configuración de la página.|  
|[PageRef](#PageRef)|Especifica una referencia a una instancia de una página en un elemento [Stage](#Stage) dentro de un elemento [StageGroup](#StageGroup).|  
|[Pages](#Pages)|Agrupa los elementos [Page](#Page) individuales.|  
|[RadioGroup](#RadioGroup)|Especifica un grupo de botones de radio dentro de un elemento [Field](#Field).|  
|[StageGroup](#StageGroup)|Especifica un grupo de una o varias fases.|  
|[StageGroups](#StageGroups)|Agrupa un conjunto de grupos de fase dentro de un archivo de configuración del Asistente para UDI.|  
|[Setter]()|Especifica un valor de propiedad de un valor para una propiedad que se menciona en la propiedad **Property**.|  
|[Stage](#Stage)|Especifica una fase dentro de un elemento [StageGroup](#StageGroup) y contiene uno o varios elementos [PageRef](#PageRef).|  
|[Style](#Style)|Agrupa los elementos [setter]() individuales que configuran la apariencia y el funcionamiento del Asistente para UDI, incluidos el título que aparece en la parte superior del asistente y la imagen de pancarta que se muestra en él.|  
|[Task](#Task)|Especifica una tarea que se va a ejecutar en la página especificada en el elemento [Page](#Page) primario.|  
|[Tareas](#Tasks)|Agrupa un conjunto de tareas para un elemento [Page](#Page).|  
|[Validator](#Validator)|Especifica un validador para el control de campo que se especifica en el elemento primario [Field](#Field).|  
|[Wizard](#Wizard)|Especifica la raíz de todos los demás elementos.|  

####  <a name="Data"></a> Data  
 Este elemento agrupa los elementos [DataItem](#DataItem) individuales dentro de un elemento [Page](#Page) y se denomina mediante el atributo **Nombre**.  

##### <a name="element-information"></a>Información del elemento  
En la tabla 78 se proporciona información sobre el elemento [Data](#Data).  

### <a name="table-78-data-element-information"></a>Tabla 78. Información del elemento Data  

|**Atributo**|**Valor**|  
|-|-|  
|Número de repeticiones|Cero o más dentro del elemento [Page](#Page) (este elemento es opcional).|  
|Elementos primarios|**Page**, **DataItem**|  
|Contenido|**DataItem**, **Setter**|  

##### <a name="element-attributes"></a>Atributos del elemento  
 En la tabla 79 se enumeran los atributos del elemento [Data](#Data) y se ofrece una descripción de cada uno.  

### <a name="table-79-attributes-and-corresponding-values-for-the-data-element"></a>Tabla 79. Atributos y valores correspondientes para el elemento Data  

|**Atributo**|**Descripción**|  
|-|-|  
|**Nombre**|Especifica el nombre del elemento [Data](#Data).|  

##### <a name="remarks"></a>Comentarios  
 El atributo **Name** permite que el código recupere un conjunto específico de datos.  

##### <a name="example"></a>Ejemplo  
 Ninguna.  

####  <a name="DataItem"></a> DataItem  
 Este elemento agrupa los elementos [Setter]() individuales dentro de un elemento [Page](#Page). Se pueden crear datos jerárquicos mediante la inclusión de uno o varios elementos [Data](#Data) dentro de un elemento [DataItem](#DataItem). Cada elemento **DataItem** representa un elemento individual. Por ejemplo, una lista de las unidades de disco disponibles podría tener un elemento **DataItem** para el nombre para mostrar y otro elemento **DataItem** para la letra de unidad correspondiente.  

##### <a name="element-information"></a>Información del elemento  
 En la tabla 80 se ofrece información sobre el elemento [DataItem](#DataItem).  

### <a name="table-80-dataitem-element-information"></a>Tabla 80. Información del elemento DataItem  

|**Atributo**|**Valor**|  
|-|-|  
|Número de repeticiones|Cero o más dentro del elemento [Data](#Data) (este elemento es opcional).|  
|Elementos primarios|**Data**|  
|Contenido|**Data**, **Setter**|  

##### <a name="element-attributes"></a>Atributos del elemento  
 Este elemento no tiene atributos.  

##### <a name="remarks"></a>Comentarios  
 Ninguna.  

##### <a name="example"></a>Ejemplo  
 Ninguna.  

#### <a name="default"></a>Predeterminado  
 Este elemento especifica un valor predeterminado para el campo especificado en el elemento primario [Field](#Field) o [RadioGroup](#RadioGroup). El valor predeterminado se establece en el valor entre corchetes de este elemento.  

##### <a name="element-information"></a>Información del elemento  
En la tabla 81 se proporciona información sobre el elemento [Default](#Default).  

### <a name="table-81-default-element-information"></a>Tabla 81. Información del elemento Default  

|**Atributo**|**Valor**|  
|-|-|  
|Número de repeticiones |Cero o más dentro del elemento [Field](#Field) o [RadioGroup](#RadioGroup). (Este elemento es opcional).|  
|Elementos primarios|**Field**, **RadioGroup**|  
|Contenido|Puede ser cualquier contenido XML con formato correcto pero normalmente es texto estándar.|  

##### <a name="element-attributes"></a>Atributos del elemento  
 Este elemento no tiene atributos.  

##### <a name="remarks"></a>Comentarios  
 Ninguna.  

##### <a name="example"></a>Ejemplo  
 En el ejemplo siguiente, el valor predeterminado para el campo **TimeZone** se establece en "Pacific Standard Time" (Hora estándar del Pacífico):  

```  
<Field Name="TimeZone" Enabled="true" VarName="OSDTimeZone" Summary="Time Zone:">  
  <Default>Pacific Standard Time</Default>  
```  

####  <a name="DLL"></a> DLL  
 Este elemento especifica un archivo DLL para que el Asistente para UDI y el diseñador del Asistente para UDI lo carguen y hagan referencia a él.  

##### <a name="element-information"></a>Información del elemento  
En la tabla 82 se proporciona información sobre el elemento [DLL](#DLL).  

### <a name="table-82-dll-element-information"></a>Tabla 82. Información del elemento DLL  

|**Atributo**|**Valor**|  
|-|-|  
|Número de repeticiones|Una o varias en el elemento [DLLs](#DLLs).|  
|Elemento primario|**DLLs**|  
|Contenido|No se permite contenido para este elemento.|  

##### <a name="element-attributes"></a>Atributos del elemento  
 En la tabla 83 se enumeran los atributos del elemento [DLL](#DLL) y se ofrece una descripción de cada uno.  

### <a name="table-83-attributes-and-corresponding-values-for-the-dll-element"></a>Tabla 83. Atributos y valores correspondientes para el elemento DLL  

|**Atributo**|**Descripción**|  
|-|-|  
|Nombre|Especifica el nombre del archivo DLL para que el Asistente para UDI y el diseñador del Asistente para UDI hagan referencia a él.|  

##### <a name="remarks"></a>Comentarios  
 Ninguna.  

##### <a name="example"></a>Ejemplo  

```  
<DLLs>  
  <DLL Name="OSDRefreshWizard.dll" />   
  <DLL Name="SharedPages.dll" />  
</DLLs>  
```  

####  <a name="DLLs"></a> DLLs  
 Este elemento agrupa los elementos [DLL](#DLL) individuales.  

##### <a name="element-information"></a>Información del elemento  
En la tabla 84 se proporciona información sobre el elemento [DLLs](#DLLs).  

### <a name="table-84-dlls-element-information"></a>Tabla 84. Información del elemento DLLs  

|**Atributo**|**Valor**|  
|-|-|  
|Número de repeticiones|Uno|  
|Elementos primarios|**Wizard**|  
|Contenido|**DLL**|  

##### <a name="element-attributes"></a>Atributos del elemento  
 Este elemento no tiene atributos.  

##### <a name="remarks"></a>Comentarios  
 Ninguna.  

##### <a name="example"></a>Ejemplo  

```  
<DLLs>  
   <DLL Name="OSDRefreshWizard.dll" />  
   <DLL Name="SharedPages.dll" />   
</DLLs>  
```  

####  <a name="Error"></a> Error  
 Este elemento especifica un código de error posible que una tarea puede devolver. El **HRESULT** de la tarea devuelve el valor del código de error para proporcionar información de error más específica.  

##### <a name="element-information"></a>Información del elemento  
 En la tabla 85 se proporciona información sobre el elemento [Error](#Error).  

### <a name="table-85-error-element-information"></a>Tabla 85. Información del elemento Error  

|**Atributo**|**Valor**|  
|-|-|  
|Número de repeticiones|Cero o más dentro del elemento [ExitCode](#ExitCode) (este elemento es opcional).|  
|Elementos primarios|**ExitCodes**|  
|Contenido|Cualquier contenido de XML con formato correcto.|  

##### <a name="element-attributes"></a>Atributos del elemento  
 En la tabla 86 se enumeran los atributos del elemento [Error](#Error) y se ofrece una descripción de cada uno.  

###  

|**Atributo**|**Descripción**|  
|-|-|  
|**Estado**|Especifica el estado de devolución de una tarea que ha encontrado un error. Normalmente, el valor de este atributo se establece en Error. Este valor se muestra en la columna **Estado** en la página del asistente en el Asistente para UDI.|  
|**Texto**|Especifica el texto descriptivo sobre la condición de error que la tarea encontró.|  
|**Tipo**|Especifica si este elemento representa un error, una advertencia o un proceso correcto. El valor especificado en **Tipo** debe ser único dentro de un elemento [ExitCodes](#ExitCodes). Los siguientes son valores válidos para este elemento:<br /><br /> -   **0.** El elemento representa un estado correcto.<br />-   **1.** El elemento representa una advertencia.<br />-   **-1.** El elemento representa un error.|  
|**Valor**|Especifica el valor del código que la tarea devuelve como un valor numérico. Especificar el valor de un asterisco (*) indica el elemento predeterminado para los códigos de retorno que no aparecen en otros elementos [Error](#Error).|  

##### <a name="remarks"></a>Comentarios  
 Ninguna.  

##### <a name="example"></a>Ejemplo  
 Ninguna.  

####  <a name="ExitCode"></a> ExitCode  
 Este elemento especifica un código de salida posible para una tarea. Los códigos de salida son códigos de retorno que la tarea espera. Cree un elemento **ExitCode** para cada código de salida posible. En caso contrario, puede especificar un asterisco (\*) en el atributo **Valor** para controlar los códigos de retorno que no se enumeran en otros elementos **ExitCode**.  

##### <a name="element-information"></a>Información del elemento  
En la tabla 87 se proporciona información sobre el elemento [ExitCode](#ExitCode).  

### <a name="table-87-exitcode-element-information"></a>Tabla 87. Información del elemento ExitCode  

|**Atributo**|**Valor**|  
|-|-|  
|Número de repeticiones|Cero o más dentro del elemento [ExitCodes](#ExitCodes) (este elemento es opcional).|  
|Elementos primarios|**ExitCodes**|  
|Contenido|Al menos un elemento [ExitCode](#ExitCode) y cero o más elementos [Error](#Error).|  

##### <a name="element-attributes"></a>Atributos del elemento  
En la tabla 88 se enumeran los atributos del elemento [ExitCode](#ExitCode) y se ofrece una descripción de cada uno.  

### <a name="table-88-attributes-and-corresponding-values-for-the-exitcode-element"></a>Tabla 88. Atributos y valores correspondientes para el elemento ExitCode  

|**Atributo**|Descripción|  
|-|-|  
|**Estado**|Especifica el estado de devolución de una tarea. El valor de este atributo se muestra en la columna **Estado** de la página del asistente correspondiente del Asistente para UDI. Para este atributo se puede usar cualquier valor que sea significativo para la tarea. Los siguientes son los valores típicos que se usan para este atributo:<br /><br /> -   Success<br />-   Warning<br />-   Error|  
|**Texto**|Especifica el texto descriptivo sobre el código de salida de la tarea.|  
|**Tipo**|Especifica si este elemento representa un error, una advertencia o un proceso correcto. El valor especificado en el tipo debe ser único dentro de un elemento [ExitCodes](#ExitCodes). Los siguientes son valores válidos para este elemento:<br /><br /> -   **0.** El elemento representa un estado correcto.<br />-   **1.** El elemento representa una advertencia.<br />-   **-1.** El elemento representa un error.|  
|**Valor**|Especifica el valor del código que la tarea devuelve como un valor numérico. Especificar el valor de un asterisco (*) indica el elemento predeterminado para los códigos de retorno que no aparecen en otros elementos [ExitCode](#ExitCode).|  

##### <a name="remarks"></a>Comentarios  
 Ninguna.  

##### <a name="example"></a>Ejemplo  
 Ninguna.  

####  <a name="ExitCodes"></a> ExitCodes  
 Este elemento agrupa un conjunto de elementos [ExitCode](#ExitCode) y [Error](#Error) para un elemento [Task](#Task) o **Error**.  

##### <a name="element-information"></a>Información del elemento  
En la tabla 89 se proporciona información sobre el elemento [ExitCodes](#ExitCodes).  

### <a name="table-89-exitcodes-element-information"></a>Tabla 89. Información del elemento ExitCodes  

|**Atributo**|**Valor**|  
|-|-|  
|Número de repeticiones|Una en cada elemento [Task](#Task).|  
|Elementos primarios|**Task**|  
|Contenido|**Error**, **ExitCode**|  

##### <a name="element-attributes"></a>Atributos del elemento  
 Este elemento no tiene atributos.  

##### <a name="remarks"></a>Comentarios  
 Ninguna.  

##### <a name="example"></a>Ejemplo  
 Ninguna.  

####  <a name="Field"></a> Field  
 Este elemento especifica una instancia de un control en un elemento [Page](#Page) que se usa para proporcionar personalización mediante XML. No todos los controles permiten la personalización con XML, solo los que usan el elemento [Field](#Field).  

##### <a name="element-information"></a>Información del elemento  
 En la tabla 90 se proporciona información sobre el elemento [Field](#Field).  

### <a name="table-90-field-element-information"></a>Tabla 90. Información del elemento Field  

|**Atributo**|**Valor**|  
|-|-|  
|Número de repeticiones|Cero o más dentro del elemento [Field](#Field) (este elemento es opcional).|  
|Elementos primarios|**Fields**|  
|Contenido|**Default**, **Validator**|  

##### <a name="element-attributes"></a>Atributos del elemento  
En la tabla 91 se enumeran los atributos del elemento [Field](#Field) y se ofrece una descripción de cada uno.  

### <a name="table-91-attributes-and-corresponding-values-for-the-field-element"></a>Tabla 91. Atributos y valores correspondientes para el elemento Field  

|**Atributo**|**Descripción**|  
|-|-|  
|**Habilitado**|Especifica si el campo está habilitado para la entrada del usuario (el atributo se puede establecer en True o False).|  
|**Nombre**|Especifica el nombre del campo.|  
|**Resumen**|Especifica el texto descriptivo que se muestra en la página **Resumen** del asistente para el valor que establece este campo.|  
|**VarName**|Especifica el nombre de la variable de secuencia de tareas que se lee o configura mediante el campo en el elemento primario [Field](#Field).|  

##### <a name="remarks"></a>Comentarios  
 Este elemento puede contener cero o más elementos [Default](#Default) y cero o más elementos [Validator](#Validator).  

##### <a name="example"></a>Ejemplo  
 Ninguna.  

####  <a name="Fields"></a> Fields  
 Este elemento agrupa los elementos [Field](#Field) individuales dentro de un elemento [Page](#Page).  

##### <a name="element-information"></a>Información del elemento  
En la tabla 92 se proporciona información sobre el elemento [Fields](#Fields).  

### <a name="table-92-fields-element-information"></a>Tabla 92. Información del elemento Fields  

|**Atributo**|**Valor**|  
|-|-|  
|Número de repeticiones|Cero o más dentro del elemento [Page](#Page) (este elemento es opcional).|  
|Elementos primarios|**Page**|  
|Contenido|**Field**, **RadioGroup**|  

##### <a name="element-attributes"></a>Atributos del elemento  
 Este elemento no tiene atributos.  

##### <a name="remarks"></a>Comentarios  
 Ninguna.  

##### <a name="example"></a>Ejemplo  
 Ninguna.  

####  <a name="File"></a> File  
 Este elemento especifica el origen y destino para una operación de copia de archivo mediante el tipo de tarea **Microsoft.Wizard.CopyFilesTask**. Se puede incluir un elemento [File](#File) independiente para copiar más de un archivo en una sola tarea.  

##### <a name="element-information"></a>Información del elemento  
 En la tabla 93 se proporciona información sobre el elemento [File](#File).  

### <a name="table-93-file-element-information"></a>Tabla 93. Información del elemento File  

|**Atributo**|**Valor**|  
|-|-|  
|Número de repeticiones|Una o varias para cada tarea que tiene un tipo de tarea de **Microsoft.Wizard.CopyFilesTask**.|  
|Elementos primarios|**Task**|  
|Contenido|Ninguno|  

##### <a name="element-attributes"></a>Atributos del elemento  
 En la tabla 94 se enumeran los atributos del elemento [File](#File) y se ofrece una descripción de cada uno.  

### <a name="table-94-attributes-and-corresponding-values-for-the-file-element"></a>Tabla 94. Atributos y valores correspondientes para el elemento File  

|**Atributo**|**Descripción**|  
|-|-|  
|**Dest**|Especifica la ruta de acceso completa o relativa a la carpeta de destino para el archivo especificado en el atributo **Source**. Se permiten las variables de entorno como parte de la ruta de acceso.|  
|**Origen**|Especifica la ruta de acceso completa o relativa al archivo de origen que copia el tipo de tarea **Microsoft.Wizard.CopyFilesTask**. Este atributo admite caracteres comodín, por lo que se pueden copiar varios archivos con uno solo elemento [File](#File). Se permiten las variables de entorno como parte de la ruta de acceso.|  

##### <a name="remarks"></a>Comentarios  
 Ninguna.  

##### <a name="example"></a>Ejemplo  
 Ninguna.  

####  <a name="PageElement"></a> Page  
 Este elemento especifica una instancia de una página e incluye todos los valores de configuración de la página.  

##### <a name="element-information"></a>Información del elemento  
En la tabla 95 se proporciona información sobre el elemento [Page](#Page).  

### <a name="table-95-page-element-information"></a>Tabla 95. Información del elemento Page  

|**Atributo**|**Valor**|  
|-|-|  
|Número de repeticiones|Una o varias dentro de cada elemento [Pages](#Pages).|  
|Elementos primarios|**Pages**|  
|Contenido|**Data**, **Fields**, **Setter**, **Tasks**|  

##### <a name="element-attributes"></a>Atributos del elemento  
En la tabla 96 se enumeran los atributos del elemento [Page](#Page) y se ofrece una descripción de cada uno.  

### <a name="table-96-attributes-and-corresponding-values-for-the-page-element"></a>Tabla 96. Atributos y valores correspondientes para el elemento Page  

|**Atributo**|**Descripción**|  
|-|-|  
|**DisplayName**|Especifica el nombre descriptivo de la página del asistente que se muestra en el diseñador del Asistente para UDI. Normalmente este nombre es más descriptivo que el atributo **Nombre**.|  
|**Nombre**|Especifica el nombre de la página del asistente que se muestra en el diseñador del Asistente para UDI.|  
|**Tipo**|Especifica el tipo de página del asistente que se relaciona directamente con una página específica del asistente en un archivo DLL.|  

##### <a name="remarks"></a>Comentarios  
 Ninguna.  

##### <a name="example"></a>Ejemplo  
 Ninguna.  

####  <a name="PageRef"></a> PageRef  
 Este elemento especifica una referencia a una instancia de una página en un elemento [Stage](#Stage) dentro de un elemento [StageGroup](#StageGroup).  

##### <a name="element-information"></a>Información del elemento  
En la tabla 97 se proporciona información sobre el elemento [PageRef](#PageRef).  

### <a name="table-97-pageref-element-information"></a>Tabla 97. Información del elemento PageRef  

|**Atributo**|**Valor**|  
|-|-|  
|Número de repeticiones|Una o varias dentro de un elemento [Stage](#Stage).|  
|Elementos primarios|**Stage**|  
|Contenido|Ninguno|  

##### <a name="element-attributes"></a>Atributos del elemento  
En la tabla 98 se enumera el atributo del elemento [PageRef](#PageRef) y se ofrece su descripción.  

### <a name="table-98-attributes-and-corresponding-values-for-the-pageref-element"></a>Tabla 98. Atributos y valores correspondientes para el elemento PageRef  

|**Atributo**|**Descripción**|  
|-|-|  
|**Página**|Especifica la instancia de una página de un elemento [Stage](#Stage) dentro de un elemento [StageGroup](#StageGroup). Establezca este valor en el atributo Nombre de un elemento [Page](#Page).|  

##### <a name="remarks"></a>Comentarios  
 Ninguna.  

##### <a name="example"></a>Ejemplo  
 Ninguna.  

####  <a name="Pages"></a> Pages  
 Este elemento agrupa los elementos [Page](#Page) individuales.  

##### <a name="element-information"></a>Información del elemento  
En la tabla 99 se proporciona información sobre el elemento [Pages](#Pages).  

### <a name="table-99-pages-element-information"></a>Tabla 99. Información del elemento Pages  

|**Atributo**|**Valor**|  
|-|-|  
|Número de repeticiones|Uno|  
|Elementos primarios|**Wizard**|  
|Contenido|**Página**|  

##### <a name="element-attributes"></a>Atributos del elemento  
 Este elemento no tiene atributos.  

##### <a name="remarks"></a>Comentarios  
 Ninguna.  

##### <a name="example"></a>Ejemplo  

```  
<Pages>  
   + <Page Name="WelcomePage" DisplayName="Welcome" Type="Microsoft.SharedPages.WelcomePage">  
   + <Page Name="ConfigScanPage" DisplayName="Deployment Readiness" Type="Microsoft.OSDRefresh.ConfigScanPage">  
   + <Page Name="ConfigScanBareMetal" DisplayName="Deployment Readiness" Type="Microsoft.OSDRefresh.ConfigScanPage">  
   + <Page Name="RebootPage" DisplayName="Reboot" Type="Microsoft.OSDRefresh.RebootPage">  
   + <Page Name="WelcomePageReplace" DisplayName="Welcome" Type="Microsoft.SharedPages.WelcomePage">  
   + <Page Name="VolumePage" DisplayName="Volume" Type="Microsoft.OSDRefresh.VolumePage">  
   + <Page Name="UserRestorePage" DisplayName="Select Target" Type="Microsoft.OSDRefresh.UserStatePage">  
   + <Page Name="ComputerPage" DisplayName="New Computer Details" Type="Microsoft.OSDRefresh.ComputerPage">  
   + <Page Name="AdminAccounts" DisplayName="Administrator Password" Type="Microsoft.SharedPages.AdminAccountsPage">  
   + <Page Name="UDAPage" DisplayName="User Device Affinity" Type="Microsoft.OSDRefresh.UDAPage">  
   + <Page Name="LanguagePage" DisplayName="Language" Type="Microsoft.OSDRefresh.LanguagePage">  
   + <Page Name="ApplicationPage" DisplayName="Install Programs" Type="Microsoft.OSDRefresh.ApplicationPage">  
     <Page Name="SummaryPage" DisplayName="Summary" Type="Microsoft.Shared.SummaryPage" />   
   + <Page Name="UserCapturePageOldPC" DisplayName="Select Target" Type="Microsoft.OSDRefresh.UserStatePage">  
   + <Page Name="ProgressPage" DisplayName="Capture Data" Type="Microsoft.OSDRefresh.ProgressPage">  
   + <Page Name="RebootAfterCapture" DisplayName="Reboot" Type="Microsoft.OSDRefresh.RebootPage">  
</Pages>  
```  

####  <a name="RadioGroup"></a> RadioGroup  
 Este elemento especifica un grupo de botones de radio dentro de un elemento [Field](#Field).  

##### <a name="element-information"></a>Información del elemento  
En la tabla 100 se proporciona información sobre el elemento [RadioGroup](#RadioGroup).  

### <a name="table-100-radiogroup-element-information"></a>Tabla 100. Información del elemento RadioGroup  

|**Atributo**|**Valor**|  
|-|-|  
|Número de repeticiones|Cero o más dentro de un elemento [Fields](#Fields) (este elemento es opcional).|  
|Elementos primarios|**Fields**|  
|Contenido|**Predeterminado**|  

##### <a name="element-attributes"></a>Atributos del elemento  
 En la tabla 101 se enumeran los atributos del elemento [RadioGroup](#RadioGroup) y se ofrece una descripción de cada uno.  

### <a name="table-101-attributes-and-corresponding-values-for-the-radiogroup-element"></a>Tabla 101. Atributos y valores correspondientes para el elemento RadioGroup  

|**Atributo**|**Descripción**|  
|-|-|  
|**Bloqueado**|Especifica si el grupo de botones de radio está habilitado para la entrada de usuario. El atributo se puede establecer en:<br /><br /> -   **True**. Especifica que los botones de radio están deshabilitados y los usuarios no pueden seleccionar un botón de radio del grupo.<br />-   **False**. Especifica que los botones de radio están habilitados y los usuarios pueden seleccionar un botón de radio del grupo.|  
|**Nombre**|Especifica el nombre del grupo de botones de radio.|  

##### <a name="remarks"></a>Comentarios  
 Ninguna.  

##### <a name="example"></a>Ejemplo  
 Ninguna.  

####  <a name="StageGroup"></a> StageGroup  
 Este elemento especifica un grupo de fases de implementación.  

##### <a name="element-information"></a>Información del elemento  
En la tabla 102 se proporciona información sobre el elemento [StageGroup](#StageGroup).  

### <a name="table-102-stagegroup-element-information"></a>Tabla 102. Información del elemento StageGroup  

|**Atributo**|**Valor**|  
|-|-|  
|Número de repeticiones|Una o varias dentro de un elemento [StageGroups](#StageGroups).|  
|Elementos primarios|**StageGroups**|  
|Contenido|**Stage**|  

##### <a name="element-attributes"></a>Atributos del elemento  
 En la tabla 103 se enumeran los atributos del elemento [StageGroup](#StageGroup) y se ofrece una descripción de cada uno.  

### <a name="table-103-attributes-and-corresponding-values-for-the-stagegroup-element"></a>Tabla 103. Atributos y valores correspondientes para el elemento StageGroup  

|**Atributo**|**Descripción**|  
|-|-|  
|**DisplayName**|Especifica el nombre descriptivo del grupo de fases que se muestra en el diseñador del Asistente para UDI. Normalmente este nombre es más descriptivo que el atributo **Nombre**.|  

##### <a name="remarks"></a>Comentarios  
 Ninguna.  

##### <a name="example"></a>Ejemplo  
 Ninguna.  

####  <a name="StageGroups"></a> StageGroups  
 Este elemento agrupa un conjunto de grupos de fases dentro de un archivo de configuración del Asistente para UDI.  

##### <a name="element-information"></a>Información del elemento  
En la tabla 104 se proporciona información sobre el elemento [StageGroups](#StageGroups).  

### <a name="table-104-stagegroups-element-information"></a>Tabla 104. Información del elemento StageGroups  

|**Atributo**|**Valor**|  
|-|-|  
|Número de repeticiones|Cero o una dentro de un elemento [Wizard](#Wizard).|  
|Elementos primarios|**Wizard**|  
|Contenido|**StageGroup**|  

##### <a name="element-attributes"></a>Atributos del elemento  
 Este elemento no tiene atributos.  

##### <a name="remarks"></a>Comentarios  
 Ninguna.  

##### <a name="example"></a>Ejemplo  
 Ninguna.  

####  <a name="Setter"></a> Setter  
 Este elemento especifica un valor de propiedad de un valor para una propiedad que se menciona en la propiedad **Property**.  

##### <a name="element-information"></a>Información del elemento  
 En la tabla 105 se proporciona información sobre el elemento [Setter]().  

### <a name="table-105-setter-element-information"></a>Tabla 105. Información del elemento Setter  

|**Atributo**|**Valor**|  
|-|-|  
|Número de repeticiones|Cero o más dentro de cada elemento primario (este elemento es opcional).|  
|Elementos primarios|**Data**, **DataItem**, **Page**, **Style**, **Task**, **Validator**|  
|Contenido|Contiene un valor de cadena en el atributo **Propiedad**.|  

##### <a name="element-attributes"></a>Atributos del elemento  
En la tabla 106 se enumera el atributo del elemento [Setter]() y se ofrece su descripción.  

### <a name="table-106-attributes-and-corresponding-values-for-the-setter-element"></a>Tabla 106. Atributos y valores correspondientes para el elemento Setter  

|**Atributo**|**Descripción**|  
|-|-|  
|**Propiedad**|Especifica el nombre de propiedad que se va a establecer. El nombre de propiedad se establece en el valor entre corchetes de este atributo.|  

##### <a name="remarks"></a>Comentarios  
 Ninguna.  

##### <a name="example"></a>Ejemplo  
 Ninguna.  

#### <a name="stage"></a>Fase  
 Este elemento especifica un elemento [Stage](#Stage) dentro de un elemento [StageGroup](#StageGroup) y contiene uno o varios elementos [PageRef](#PageRef).  

##### <a name="element-information"></a>Información del elemento  
En la tabla 107 se proporciona información sobre el elemento [Stage](#Stage).  

### <a name="table-107-stage-element-information"></a>Tabla 107. Información del elemento Stage  

|**Atributo**|**Valor**|  
|-|-|  
|Número de repeticiones|Una o varias dentro de un elemento [StageGroup](#StageGroup).|  
|Elementos primarios|**StageGroup**|  
|Contenido|**PageRef**|  

##### <a name="element-attributes"></a>Atributos del elemento  
En la tabla 108 se enumeran los atributos del elemento [Stage](#Stage) y se ofrece una descripción de cada uno.  

### <a name="table-108-attributes-and-corresponding-values-for-the-stage-element"></a>Tabla 108. Atributos y valores correspondientes para el elemento Stage  

|**Atributo**|**Descripción**|  
|-|-|  
|**DisplayName**|Especifica el nombre descriptivo de la página del asistente que se muestra en el diseñador del Asistente para UDI. Normalmente este nombre es más descriptivo que el atributo **Nombre**.|  
|**Nombre**|Especifica el nombre de la fase. El valor de este elemento se usa al iniciar el Asistente para UDI con el parámetro de la línea de comandos **/fase: nombre**.|  

##### <a name="remarks"></a>Comentarios  
 Ninguna.  

##### <a name="example"></a>Ejemplo  
 Ninguna.  

####  <a name="Style"></a> Style  
 Este elemento agrupa los elementos [Setter]() individuales que configuran la apariencia y el funcionamiento del Asistente para UDI, incluidos el título que aparece en la parte superior del asistente y la imagen de pancarta que se muestra en él.  

##### <a name="element-information"></a>Información del elemento  
En la tabla 109 se proporciona información sobre el elemento Style.  

### <a name="table-109-style-element-information"></a>Tabla 109. Información del elemento Style  

|**Atributo**|**Valor**|  
|-|-|  
|Número de repeticiones|Uno|  
|Elementos primarios|**Wizard**|  
|Contenido|**Setter**|  

##### <a name="element-attributes"></a>Atributos del elemento  
 Este elemento no tiene atributos.  

##### <a name="remarks"></a>Comentarios  
 Ninguna.  

##### <a name="example"></a>Ejemplo  

```  
<Style>  
  <Setter Property="bannerFilename">UDI_Wizard_Banner.bmp</Setter>   
  <Setter Property="title">Operating System Deployment (OSD) Refresh Wizard</Setter>   
</Style>  
```  

####  <a name="TaskElement"></a> Task  
 Este elemento especifica una tarea que se va a ejecutar en la página especificada en el elemento [Page](#Page) primario.  

##### <a name="element-information"></a>Información del elemento  
En la tabla 110 se proporciona información sobre el elemento [Task](#Task).  

### <a name="table-110-task-element-information"></a>Tabla 110. Información del elemento Task  

|**Atributo**|**Valor**|  
|-|-|  
|Número de repeticiones|Una o varias dentro de un elemento [Tasks](#Tasks).|  
|Elementos primarios|**Tareas**|  
|Contenido|**ExitCodes**, **File**, **Setter**|  

##### <a name="element-attributes"></a>Atributos del elemento  
En la tabla 111 se enumeran los atributos del elemento [Task](#Task) y se ofrece una descripción de cada uno.  

### <a name="table-111-attributes-and-corresponding-values-for-the-task-element"></a>Tabla 111. Atributos y valores correspondientes para el elemento Task  

|**Atributo**|**Descripción**|  
|-|-|  
|**DependsOn**|Especifica si la tarea depende de otra. El valor de este atributo se establece en el atributo **Name** de otro elemento [Task](#Task). **Nota:** Este atributo no se puede configurar mediante el diseñador del Asistente para UDI. Pero este atributo se puede agregar manualmente a un elemento [Task](#Task) si se modifica directamente el archivo .xml.|  
|**DisplayName**|Especifica el nombre descriptivo de la tarea que se muestra en el diseñador del Asistente para UDI. Normalmente este nombre es más descriptivo que el atributo **Name**.|  
|**Nombre**|Especifica el nombre de la tarea. Este nombre debe ser único.|  
|Escriba|Especifica el tipo de tarea para la tarea que se va a ejecutar, que se define en el archivo DLL que contiene la tarea.|  

##### <a name="remarks"></a>Comentarios  
 Ninguna.  

##### <a name="example"></a>Ejemplo  
 Ninguna.  

####  <a name="Tasks"></a> Tasks  
 Este elemento agrupa un conjunto de tareas para un elemento [Page](#Page).  

##### <a name="element-information"></a>Información del elemento  
En la tabla 112 se proporciona información sobre el elemento [Tasks](#Tasks).  

### <a name="table-112-tasks-element-information"></a>Tabla 112. Información del elemento Tasks  

|**Atributo**|**Valor**|  
|-|-|  
|Número de repeticiones|Cero o más dentro de cada elemento [Page](#Page) (este elemento es opcional).|  
|Elementos primarios|**Página**|  
|Contenido|**Task**|  

##### <a name="element-attributes"></a>Atributos del elemento  
En la tabla 113 se enumeran los atributos del elemento [Tasks](#Tasks) y se ofrece una descripción de cada uno.  

### <a name="table-113-attributes-and-corresponding-values-for-the-tasks-element"></a>Tabla 113. Atributos y valores correspondientes para el elemento Tasks  

|**Atributo**|**Descripción**|  
|-|-|  
|**NameTitle**|Especifica el título que aparece en la parte superior de la columna que contiene el nombre de las tareas en la página del asistente adecuada.|  
|**StatusTitle**|Especifica el título que aparece en la parte superior de la columna que contiene el estado de las tareas en la página del asistente adecuada.|  

##### <a name="remarks"></a>Comentarios  
 Ninguna.  

##### <a name="example"></a>Ejemplo  
 Ninguna.  

####  <a name="ValidatorElement"></a> Validator  
 Este elemento especifica un validador para el control de campo que se especifica en el elemento primario [Field](#Field).  

##### <a name="element-information"></a>Información del elemento  
En la tabla 114 se proporciona información sobre el elemento [Validator](#Validator).  

### <a name="table-114-validator-element-information"></a>Tabla 114. Información del elemento Validator  

|**Atributo**|**Valor**|  
|-|-|  
|Número de repeticiones|Cero o una dentro de un elemento [Field](#Field).|  
|Elementos primarios|**Field**|  
|Contenido|**Setter**|  

##### <a name="element-attributes"></a>Atributos del elemento  
En la tabla 115 se enumera el atributo del elemento [Validator](#Validator) y se ofrece su descripción.  

### <a name="table-115-attributes-and-corresponding-values-for-the-validator-element"></a>Tabla 115. Atributos y valores correspondientes para el elemento Validator  

|**Atributo**|**Descripción**|  
|-|-|  
|Escriba|Especifica el tipo del validador, que se define en el archivo DLL que contiene el validador.|  

##### <a name="remarks"></a>Comentarios  
 Ninguna.  

##### <a name="example"></a>Ejemplo  
 Ninguna.  

####  <a name="Wizard"></a> Wizard  
 Este elemento especifica el directorio raíz para todos los demás elementos.  

##### <a name="element-information"></a>Información del elemento  
En la tabla 116 se proporciona información sobre el elemento [Wizard](#Wizard).  

### <a name="table-116-wizard-element-information"></a>Tabla 116. Información del elemento Wizard  

|**Atributo**|**Valor**|  
|-|-|  
|Número de repeticiones|Uno|  
|Elementos primarios|Ninguno|  
|Contenido|**DLLs**, **Pages**, **StageGroups**, **Style**|  

##### <a name="element-attributes"></a>Atributos del elemento  
 Este elemento no tiene atributos.  

##### <a name="remarks"></a>Comentarios  
 Ninguna.  

##### <a name="example"></a>Ejemplo  

```  
<Wizard>  
   + <DLLs>  
   + <Style>  
   + <Pages>  
   + <StageGroups>  
</Wizard>  
```
