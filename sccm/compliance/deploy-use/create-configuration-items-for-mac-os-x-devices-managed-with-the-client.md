---
title: "Cómo crear elementos de configuración para dispositivos Mac OS X administrados con el cliente de System Center Configuration Manager | System Center Configuration Manager"
description: "Use el elemento de configuración de Mac OS X de System Center Configuration Manager para administrar la configuración de los dispositivos Mac OS X."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 722d5bf5-bedc-4dfc-b324-6eeb773874e9
caps.latest.revision: 8
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 4e5eb84fcbde7797a68a713b30ef809ed26d0210


---
# <a name="create-configuration-items-for-mac-os-x-devices-managed-with-the-system-center-configuration-manager-client"></a>Crear elementos de configuración para dispositivos Mac OS X administrados con el cliente de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Use el elemento de configuración de **Mac OS X (personalizado)** de System Center Configuration Manager para administrar la configuración de los dispositivos Mac OS X que administra el cliente de Configuration Manager.  

 El sistema operativo Mac OS X usa archivos de lista de propiedades (o plist) para almacenar la configuración de la aplicación. Use la configuración de cumplimiento para evaluar y corregir la configuración en un archivo de lista de propiedades. También puede administrar la configuración de Mac OS X escribiendo un script de shell que devuelva un valor que pueda evaluar y corregir para el cumplimiento.  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad** > **Configuración de cumplimiento** > **Elementos de configuración**.  

3.  En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear elemento de configuración**.  

4.  En la página **General** del **Asistente para crear elemento de configuración**, escriba un nombre y, opcionalmente, una descripción para el elemento de configuración.  

5.  En **Especifique el tipo de elemento de configuración que desea crear**, seleccione **Mac OS X (custom)**.  

6.  Haga clic en **Categorías** si crea y asigna categorías para ayudarle a buscar y filtrar elementos de configuración en la consola de Configuration Manager.  

7.  En la página **Plataformas admitidas**, seleccione las versiones de Mac OS X específicas que evaluarán el elemento de configuración.  

8.  En la página **Configuración**, agregará nuevas configuraciones cuyo cumplimiento se evaluará en equipos Mac. Haga clic en **Nuevo** para abrir el cuadro de diálogo **Crear configuración** .  

9. En el cuadro de diálogo **Crear configuración** , escriba un nombre único y una descripción para la configuración.  

10. Elija el **Tipo de configuración** que quiera y después proporcione la información necesaria como se muestra en la tabla siguiente:  

    -   **Preferencias de Mac OS X** -  

        -   **Id. de la aplicación** : especifique el id. de la aplicación del archivo de lista de propiedades de la que quiere evaluar el cumplimiento de una clave.  

             Por ejemplo, si desea editar la configuración para el explorador Web Safari, podría usar **com.apple.Safari.plist**.  

        -   **Clave** : especifique el nombre de la clave que se va a evaluar para el cumplimiento en equipos Mac. Use la siguiente sintaxis: */<diccionario\>/<nombreClave\>*.  

            > [!IMPORTANT]  
            >  El nombre de clave distingue mayúsculas de minúsculas y no se evaluará si difiere del nombre de clave en el equipo Mac. Además, no podrá modificar el nombre de clave después de especificarlo. Si necesita modificar el nombre de clave, elimine y vuelva a crear la configuración.  

    -   **Script** -  

        -   **Script de detección** : haga clic en **Agregar script**y, a continuación, escriba un script de shell para evaluar el cumplimiento de la configuración en el equipo Mac. Use el comando **echo** en el script de shell para que devuelva valores a Configuration Manager para el cumplimiento. Configuration Manager usa los resultados devueltos en **STDOUT** para evaluar el cumplimiento.  

            > [!IMPORTANT]  
            >  No incluya el comando **reboot** en el script de detección. Dado que el script de detección se ejecuta cada vez que se reinicia el cliente, esto hará que el equipo Mac se reinicie continuamente.  

        -   **Script de corrección (opcional)** : si quiere, haga clic en **Agregar script** y, a continuación, escriba un script de shell que se usará para corregir cualquier configuración no conforme que se encuentre en los equipos cliente de Mac.  

            > [!IMPORTANT]  
            >  Para asegurarse de que no se introducen caracteres de formato que el equipo Mac no pueda interpretar, no debe usar copiar y pegar sino escribir el script.  

11. Elija el **Tipo de datos** que es el formato en el que la condición devuelve los datos antes de que se usen para evaluar la configuración.  

    > [!NOTE]  
    >  El tipo de datos **Punto flotante** admite solo 3 dígitos después del separador decimal.  
    >   
    >  Configuration Manager no admite el uso del tipo de datos **booleano** para la configuración de scripts de elementos de configuración de Mac. En su lugar, establezca el tipo de datos en **Entero** y asegúrese de que el script devuelve un valor entero.  

12. Haga clic en **Aceptar** para guardar la configuración y cerrar el cuadro de diálogo **Crear configuración** ; a continuación, continúe agregando tantos valores como sea necesario.  

13. En la página **Reglas de compatibilidad**, especificará las condiciones que definen el cumplimiento de un elemento de configuración. Para poder evaluar el cumplimiento de una configuración, debe tener al menos una regla de cumplimiento. Haga clic en **Nueva** para agregar una nueva regla.  

14. En el cuadro de diálogo **Crear regla** , proporcione la siguiente información:  

    -   **Nombre:** Escriba un nombre para la regla de cumplimiento.  

    -   **Descripción:** Escriba una descripción para la regla de cumplimiento.  

    -   **Configuración seleccionada:** Haga clic en **Examinar** para abrir el **Seleccione configuración** cuadro de diálogo. Seleccione la configuración que desea definir una regla de, o haga clic en **nueva configuración**. Cuando haya terminado, haga clic en **seleccione**.  

        > [!TIP]  
        >  También puede hacer clic en **propiedades** para ver información acerca de la configuración seleccionada actualmente.  

    -   **Tipo de regla:** seleccione el tipo de regla de cumplimiento que quiere usar:  

        -   **Valor:** cree una regla que compare el valor devuelto por el elemento de configuración con un valor que especifique.  

        -   **Existencial** : cree una regla que se evalúe la configuración en función de si existe en un dispositivo.  

    -   Para un tipo de regla **Valor**, especifique la siguiente información:  

        -   La configuración debe cumplir la siguiente regla: seleccione un operador y un valor cuyo cumplimiento se evalúa con la configuración seleccionada. Puede usar los operadores siguientes:  

            -   **Igual a**  

            -   **No es igual a**  

            -   **Mayor que**  

            -   **Menor que**  

            -   **Entre**  

            -   **Mayor o igual que**  

            -   **Menor o igual que**  

            -   **Uno de** : en el cuadro de texto, especifique una entrada en cada línea.  

            -   **Ninguno de** : en el cuadro de texto, especifique una entrada en cada línea.  

        -   **Corregir las reglas no compatibles cuando se admita** : seleccione esta opción si quiere que Configuration Manager corrija automáticamente las reglas no conformes.  

            > [!IMPORTANT]  
            >  Solo puede corregir reglas no conformes cuando el operador de regla se establece en **es igual a**.  

        -   **Notificar la no compatibilidad si no se encuentra la instancia de esta configuración** : el elemento de configuración notifica el incumplimiento si esta configuración no se encuentra en el equipo Mac.  

    -   **Gravedad de no compatibilidad para informes** : especifique el nivel de gravedad que se notifica si esta regla de cumplimiento falla. Los niveles de gravedad disponibles (que se muestran en los informes de Configuration Manager) son:  

        -   **Ninguno**: los equipos que no cumplan esta regla de cumplimiento no notifican una gravedad de error.  

        -   **Información**: los equipos que no cumplan esta regla de cumplimiento notifican una gravedad de error de **Información**.  

        -   **Advertencia**: los equipos que no cumplan esta regla de compatibilidad notifican una gravedad de error de **Advertencia**.  

        -   **Crítico**: los equipos que no cumplan esta regla de compatibilidad notifican una gravedad de error de **Crítico**.  

        -   **Crítico con evento**: los equipos que no cumplan esta regla de cumplimiento notifican una gravedad de error de **Crítico**. Este nivel de gravedad también se registra para el equipo cliente de Mac.  

    -   Para un tipo de regla **Existencial**, especifique la siguiente información:  

        -   Elija una de las siguientes:  

            -   **La configuración debe existir en dispositivos cliente**  

            -   **La configuración no debe existir en dispositivos cliente**  

        -   **Gravedad de no conformidad para los informes:** Especificar el nivel de gravedad se indica si se produce un error en esta regla de compatibilidad. Los niveles de gravedad disponibles (que se muestran en los informes de Configuration Manager) son:  

            -   **Ninguno**: los equipos que no cumplan esta regla de cumplimiento no notifican una gravedad de error.  

            -   **Información**: los equipos que no cumplan esta regla de cumplimiento notifican una gravedad de error de **Información**.  

            -   **Advertencia**: los equipos que no cumplan esta regla de compatibilidad notifican una gravedad de error de **Advertencia**.  

            -   **Crítico**: los equipos que no cumplan esta regla de compatibilidad notifican una gravedad de error de **Crítico**.  

            -   **Crítico con evento**: los equipos que no cumplan esta regla de cumplimiento notifican una gravedad de error de **Crítico**. Este nivel de gravedad también se registra para el equipo cliente de Mac.  

        > [!NOTE]  
        >  Las opciones mostradas pueden variar según el tipo de configuración para la que configura una regla.  

    -   Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Crear regla** .  

15. En la página **Resumen** , confirme la configuración para el nuevo elemento de configuración y, a continuación, complete el asistente.  

El nuevo elemento de configuración se muestra en el nodo **Elementos de configuración** del área de trabajo **Activos y compatibilidad** .  

Si quiere agregar este elemento de configuración a una línea base de configuración, consulte [Crear líneas base de configuración](../../compliance/deploy-use/create-configuration-baselines.md).  



<!--HONumber=Nov16_HO1-->


