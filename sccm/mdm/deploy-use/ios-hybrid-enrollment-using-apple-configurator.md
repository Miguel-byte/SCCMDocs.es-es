---
title: "Inscripción híbrida de iOS híbrido con Apple Configurator con Configuration Manager"
descriptions: Pre-enroll iOS devices by using Apple Configurator with Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 61a19d95-83ff-4ad8-9a67-f304d2ba54f2
caps.latest.revision: 5
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 19f4880d6e7ba3da2e4bcfe725c1c806ee3b3334


---
# <a name="ios-hybrid-enrollment-using-apple-configurator-with-configuration-manager"></a>Inscripción híbrida de iOS híbrido con Apple Configurator con Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Las compañías que compran dispositivos iOS destinados para su uso por los empleados pueden administrarlos mediante Microsoft Intune. Ya puede preinscribir dispositivos iOS conectándolos por USB a un equipo Mac que ejecuta Apple Configurator. Antes de la inscripción, debe preparar un perfil de dispositivo inscrito en empresa de Intune en la consola de administración de Intune y exportarlo al equipo Mac. El proceso de inscripción restaurará el dispositivo a su configuración de fábrica; así pues, siga el proceso del Asistente de configuración para configurar el dispositivo. El siguiente procedimiento está recomendado para dispositivos iOS dedicados que tendrán un único usuario que emplea el dispositivo para tener acceso al correo electrónico de la empresa y a recursos corporativos, como aplicaciones y datos.  

##  <a name="a-namebkmksaea-apple-configurator-enrollment-via-setup-assistant"></a><a name="BKMK_SAE"></a> Inscripción de Apple Configurator mediante el Asistente de configuración  
 Mediante Apple Configurator, puede restablecer los valores de fábrica de los dispositivos iOS y prepararlos para la instalación por el nuevo usuario del dispositivo.  Este método requiere que se conecte el dispositivo iOS a un equipo Mac a través de una conexión USB para configurar la inscripción corporativa. Además, el método supone que se está usando Apple Configurator 2.0.  

 **Requisitos previos**  

-   Acceso físico a dispositivos iOS  

-   Números de serie del dispositivo: [cómo obtener un número de serie de iOS](https://support.apple.com/en-us/HT204308)  

-   Cables de conexión USB  

-   Equipo Mac con [Apple Configurator 2.0](http://go.microsoft.com/fwlink/?LinkId=518017)  

#### <a name="enable-setup-assistant-enrollment-with-configuration-manager-and-intune"></a>Habilitación de la inscripción con el Asistente de configuración con Configuration Manager y Intune  

1.  **Incorporación de un perfil de inscripción de dispositivos corporativos**   
    En la consola de Configuration Manager, en el área de trabajo **Activos y compatibilidad**, expanda **Introducción**, expanda **Todos los dispositivos corporativos**, expanda **iOS** y haga clic en **Perfiles de inscripción**. Haga clic en **Crear perfil** en la pestaña **Inicio** para abrir el Asistente para crear el perfil. Establezca la configuración en las siguientes páginas:  

    1.  On the **General** , especifique la información siguiente y, a continuación, haga clic en **Siguiente**.  

        -   **Nombre** : nombre del perfil de inscripción de dispositivo. (No es visible para los usuarios)  

        -   **Descripción** : descripción del perfil de inscripción de dispositivo. (No es visible para los usuarios)  

        -   **Afinidad de usuario** : especifica cómo se inscriben los dispositivos. En la mayoría de los escenarios del Asistente de configuración, use **Solicitar afinidad de usuarios**.  

            -   **Solicitar afinidad de usuario**: el dispositivo debe estar afiliado a un usuario durante la instalación inicial y, a continuación, se le puede permitir el acceso a los datos y al correo electrónico de la compañía como dicho usuario.  

            -   **Sin afinidad de usuario**: el dispositivo no está afiliado a ningún usuario. Utilice esta afiliación para dispositivos que realizan tareas sin tener acceso a datos de usuario local. Las aplicaciones que requieren la afiliación de un usuario no funcionarán.  

    2.  En la página **Programa de inscripción de dispositivos**, deje la casilla **Configurar ajustes del programa de inscripción de dispositivos de este perfil** desactivada y haga clic en **Siguiente**.  

    3.  Revise el resumen y, a continuación, haga clic en Siguiente.  

2.  **Incorporación de dispositivos de iOS para su inscripción con el Asistente para configuración**   
    En la consola de Configuration Manager, en el área de trabajo **Activos y compatibilidad**, expanda **Introducción**, expanda **Todos los dispositivos propiedad de la empresa**, expanda **iOS** y haga clic en **Información del dispositivo**. A continuación, haga clic en **Agregar dispositivos**. Puede agregar dispositivos de dos maneras:  

    - Puede **cargar un archivo CSV que contiene números de serie**: cree una lista de valores separados por comas (.csv) con dos columnas sin encabezado, limitada a 5000 dispositivos o 5 MB por archivo csv. Para cada fila, la primera celda es el número de serie del dispositivo y la segunda celda son los detalles del dispositivo (opcional).

  Este archivo .csv, cuando se ve en un editor de texto, aparece como:  

    ```  
    0000000,PO 1234  
    111111111,PO 1234  
    ```  

    - También puede **agregar manualmente números de serie y detalles**: especifique el número de serie y los detalles de hasta cinco dispositivos.  

    A continuación, haga clic en **Siguiente**.  

3.  **Selección de dispositivos para inscribir**   
    Confirme los dispositivos que desea inscribir. No se pueden importar los números de serie ya inscritos o inscritos por otros medios. Haga clic en **Siguiente** para continuar.  

4.  **Asignación de perfil**   
    Especifique el perfil que se va a asignar a los dispositivos agregados desde la lista de perfiles disponibles, consulte los **detalles del perfil de inscripción** y, a continuación, haga clic en **Finalizar**. Los dispositivos agregados manualmente pueden asignarse a cualquier perfil de inscripción, pero los dispositivos sincronizados por DEP deben asignarse a un perfil habilitado para DEP.  

5.  **Selección de un perfil para implementar en dispositivos iOS**   
    En la consola de Configuration Manager, en el área de trabajo **Activos y compatibilidad**, expanda sucesivamente **Información general**, **Todos los dispositivos propiedad de empresa** y **iOS**; haga clic en **Perfiles de inscripción** y luego seleccione el perfil de dispositivo para implementar en los dispositivos móviles. Haga clic en **Exportar…** en la barra de tareas. Copie y guarde el valor de **Dirección URL del perfil**. Se cargará en Apple Configurator más tarde para definir el perfil de Intune utilizado por los dispositivos iOS.  La dirección URL del perfil de inscripción es válida durante dos semanas desde que se exporta. Después de dos semanas, debe exportar un nuevo archivo de dirección URL para inscribir dispositivos iOS.  

     Para admitir Apple Configurator 2, se debe editar la URL de perfil 2.0. Reemplace:  

    ```  
    https://manage.microsoft.com/EnrollmentServer/Discovery.svc/iOS/ESProxy?id=  

    ```  

     por  

    ```  
    https://appleconfigurator2.manage.microsoft.com/MDMServiceConfig?id=  

    ```  

6.  **Preparación del dispositivo con Apple Configurator**   
    Los dispositivos iOS están conectados al equipo Mac e inscritos para la administración de dispositivos móviles.  

    > [!WARNING]  
    >  Los dispositivos se restablecerán en la configuración de fábrica durante el proceso de inscripción.  

    1.  En un equipo Mac, abra **Apple Configurator 2**.  En la barra de menús, haga clic en **Apple Configurator 2** y luego en **Preferences** (Preferencias).  

    2.  En el panel de preferencias, seleccione **Servers** (Servidores) y haga clic en el símbolo "+" debajo del panel izquierdo para iniciar el asistente del servidor MDM. Haga clic en **Siguiente**.  

    3.  Escriba el **nombre** y la **URL de inscripción** del servidor MDM del paso 5 anterior. Haga clic en **Siguiente**.  

         Si recibe una advertencia sobre los requisitos de perfil de confianza para Apple TV, puede cancelar con seguridad la opción de **Trust Profile** (Perfil de confianza) haciendo clic en la "X" de color gris. También de forma segura, puede omitir cualquier advertencia de marcador de certificado. Para continuar, haga clic en **Next** (Siguiente) hasta que finalice el asistente.  

    4.  En el panel **Servers** (Servidores), haga clic en "Edit" (Editar) junto a perfil del nuevo servidor. Asegúrese de que la dirección URL de inscripción coincide exactamente con la dirección URL exportada de Intune. Vuelva a escribir la dirección URL original si es diferente y **guarde** el perfil de inscripción exportado desde Intune.  

    5.  Conecte los dispositivos móviles iOS al equipo Apple con un adaptador USB.  

        > [!WARNING]  
        >  Los dispositivos se restablecerán en la configuración de fábrica durante el proceso de inscripción. Como procedimiento recomendado, restablezca el dispositivo y enciéndalo. Como procedimiento recomendado, los dispositivos deben estar en la pantalla de bienvenida al iniciar el Asistente para la instalación.  

    6.  Haga clic en **Prepare** (Preparar). En el panel **Prepare iOS Device** (Preparar dispositivo iOS), haga clic en **Manual** y luego en **Next** (Siguiente).  

    7.  En el panel **Enroll in MDM Server** (Inscribir en servidor MDM), seleccione el nombre del servidor que ha creado y haga clic en **Next** (Siguiente).  

    8.  En el panel **Enroll in MDM Server** (Inscribir en servidor MDM), seleccione el nombre del servidor que ha creado y haga clic en **Next** (Siguiente).  

    9. En el panel **Create an Organization** (Crear una organización), elija la **organización** o cree una nueva y luego haga clic en **Next** (Siguiente).  

    10. En el panel **Configure iOS Setup Assistant** (Configurar el Asistente para la instalación de iOS), elija los pasos presentados al usuario y haga clic en **Prepare** (Preparar). Si se le solicita, autentíquese para actualizar la configuración de confianza.  

    11. Cuando el dispositivo iOS termine de prepararse, puede desconectar el cable USB.  

7.  **Distribución de los dispositivos**   
    Los dispositivos ya están listos para la inscripción corporativa. Apague los dispositivos y distribúyalos a los usuarios. Cuando el dispositivo se encienda, se iniciará el asistente de configuración y pedirá al usuario su cuenta profesional o educativa.



<!--HONumber=Nov16_HO1-->


