---
title: Instalar actualizaciones de software
titleSuffix: Configuration Manager
description: Recomendaciones para usar el paso de secuencia de tareas Instalar actualizaciones de software en Configuration Manager.
ms.date: 05/28/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 72d1ccd5-3763-4f88-9273-e1a73e8f4286
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 48cb5d13dc3683a11731937d94d1f84414c3d923
ms.sourcegitcommit: 13ac4f5e600dc1edf69e8566e00968f40e1d1761
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 09/11/2019
ms.locfileid: "70892414"
---
# <a name="install-software-updates"></a>Instalar actualizaciones de software

*Se aplica a: System Center Configuration Manager (Rama actual)*

El paso **Instalar actualizaciones de software** se utiliza habitualmente en las secuencias de tareas de Configuration Manager. Al instalar o actualizar el sistema operativo, desencadena los componentes de las actualizaciones de software para buscar e implementar las actualizaciones. Este paso puede causar problemas para algunos clientes, como tiempos de espera largos o falta de actualizaciones. Use la información de este artículo para ayudar a mitigar los problemas comunes con este paso y para conseguir una mejor solución de problemas de cuando algo va mal.

Para obtener más información sobre el paso, consulte [Instalar actualizaciones de software](/sccm/osd/understand/task-sequence-steps#BKMK_InstallSoftwareUpdates).



## <a name="recommendations"></a>Recomendaciones

Para que este proceso se complete correctamente, siga estas recomendaciones:

- [Uso del mantenimiento sin conexión](#use-offline-servicing)
- [Índice único](#single-index)
- [Reducción del tamaño de la imagen](#bkmk_resetbase)

### <a name="use-offline-servicing"></a>Uso del mantenimiento sin conexión

Use Configuration Manager para instalar periódicamente las actualizaciones de software aplicables a los archivos de imagen. De este modo, se reduce el número de actualizaciones que necesita instalar durante la secuencia de tareas.

Para más información, vea [Aplicar las actualizaciones de software a una imagen](/sccm/osd/get-started/manage-operating-system-images#BKMK_OSImagesApplyUpdates).

### <a name="single-index"></a>Índice único

Muchos de los archivos de imagen incluyen varios índices; por ejemplo, para diferentes ediciones de Windows. Reduzca el archivo de imagen a un índice único que necesite. Esta práctica reduce la cantidad de tiempo para aplicar las actualizaciones de software a la imagen. También posibilita la recomendación siguiente de reducir el tamaño de la imagen.

A partir de la versión 1902, automatice este proceso al agregar una imagen de sistema operativo al sitio. Para obtener más información, vea [Agregar una imagen de sistema operativo](/sccm/osd/get-started/manage-operating-system-images#BKMK_AddOSImages).<!--3719699-->

### <a name="bkmk_resetbase"></a> Reducción del tamaño de la imagen

Al aplicar actualizaciones de software a la imagen, optimice los resultados quitando cualquier actualización reemplazada. Use la herramienta de línea de comandos de DISM, por ejemplo:

``` Command
dism /Mount-Image /ImageFile:C:\Data\install.wim /MountDir:C:\Mountdir
dism /Image:C:\Mountdir /Cleanup-Image /StartComponentCleanup /ResetBase
dism /Unmount-Image /MountDir:C:\Mountdir /Commit  
```

A partir de la versión 1902, hay una nueva opción para automatizar este proceso. Para obtener más información, vea [Servicio de imágenes optimizado](/sccm/osd/get-started/manage-operating-system-images#bkmk_resetbase).<!--3555951-->


## <a name="image-engineering-decisions"></a>Decisiones de ingeniería de imágenes

Al diseñar el proceso de creación de imágenes, hay varias opciones que pueden afectar a la instalación de actualizaciones de software:

- [Nueva captura periódica de la imagen](#bkmk_goldimage)  
- [Uso del mantenimiento sin conexión](#bkmk_offline)  
- [Uso de solo la imagen predeterminada](#bkmk_installwim)

### <a name="bkmk_goldimage"></a> Nueva captura periódica de la imagen

Tiene un proceso automatizado para capturar una imagen personalizada del sistema operativo según una programación periódica. Esta secuencia de tareas de capturas instala las actualizaciones de software más recientes. Estas actualizaciones pueden incluir actualizaciones acumulativas y no acumulativas y otras actualizaciones críticas, como actualizaciones de la pila de servicio (SSU). La secuencia de tareas de implementación instala las actualizaciones adicionales desde la captura.

Para obtener más información sobre este proceso, vea [Crear una secuencia de tareas para capturar un sistema operativo](/sccm/osd/deploy-use/create-a-task-sequence-to-capture-an-operating-system).

#### <a name="advantages"></a>Ventajas

- Menos actualizaciones para aplicar en el tiempo de implementación por cliente, lo que ahorra tiempo y ancho de banda durante la implementación
- Menos actualizaciones de las que preocuparse por causar reinicios
- Imagen personalizada para la organización
- Menos variables en tiempo de implementación

#### <a name="disadvantages"></a>Desventajas

- Tiempo para crear y capturar la imagen, aunque es un proceso automatizado en gran medida
- Más tiempo para distribuir la imagen a los puntos de distribución, lo que puede verse como una interrupción de las implementaciones activas
- El tiempo para probar a través de los entornos de preproducción puede ser mayor que el ciclo de revisión del sistema operativo, lo que puede hacer que la imagen actualizada sea irrelevante


### <a name="bkmk_offline"></a> Uso del mantenimiento sin conexión

Programe Configuration Manager para aplicar actualizaciones de software a las imágenes.

Para más información, vea [Aplicar las actualizaciones de software a una imagen](/sccm/osd/get-started/manage-operating-system-images#BKMK_OSImagesApplyUpdates).

#### <a name="advantages"></a>Ventajas

- Menos actualizaciones para aplicar en el tiempo de implementación por cliente, lo que ahorra tiempo y ancho de banda durante la implementación
- Menos actualizaciones de las que preocuparse por causar reinicios
- Puede programar el proceso de mantenimiento en el sitio

#### <a name="disadvantages"></a>Desventajas

- Selección manual de actualizaciones
- Más tiempo para distribuir la imagen a los puntos de distribución
- Solo es compatible con actualizaciones basadas en CBS No puede aplicar las actualizaciones de Office

> [!Tip]  
> Puede automatizar la selección de las actualizaciones de software con PowerShell. Use el cmdlet [Get CMSoftwareUpdate](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmsoftwareupdate?view=sccm-ps) para obtener una lista de actualizaciones. A continuación, utilice el cmdlet [New-CMOperatingSystemImageUpdateSchedule](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmoperatingsystemimageupdateschedule?view=sccm-ps) para crear la programación del mantenimiento sin conexión. El ejemplo siguiente muestra un método para automatizar esta acción:
>
> ```PowerShell
> # Get the OS image
> $Win10Image = Get-CMOperatingSystemImage -Name "Windows 10 Enterprise"
>
> # Get the latest cumulative update for Windows 10 1809
> $OSBuild = "1809"
> $LatestUpdate = Get-CMSoftwareUpdate -Fast | Where {$_.LocalizedDisplayName -Like "*Cumulative Update for Windows 10 Version $OSBuild for x64*" -and $_.LocalizedDisplayName -notlike "*Dynamic*"} | Sort-Object ArticleID -Descending | Select -First 1
> Write-Host "Latest update for Windows 10 build" $OSBuild "is" $LatestUpdate.LocalizedDisplayName
>
> # Create a new update schedule to apply the latest update
> New-CMOperatingSystemImageUpdateSchedule -Name $Win10Image.Name -SoftwareUpdate $LatestUpdate -RunNow -ContinueOnError $True
> ```


### <a name="bkmk_installwim"></a> Uso de solo la imagen predeterminada

Use el archivo de imagen install.wim de Windows de forma predeterminada en las secuencias de tareas de implementación.

#### <a name="advantages"></a>Ventajas

- Una fuente que se sabe que está en buen estado, lo que reduce el riesgo de una imagen dañada como posible problema
- Elimina las modificaciones en la imagen como un posible problema

#### <a name="disadvantages"></a>Desventajas

- Posibilidad de gran volumen de actualizaciones durante la implementación
- Mayor tiempo de implementación de todos los dispositivos
- Es posible que no tenga las personalizaciones necesarias, requiere pasos de secuencia de tareas adicionales para personalizar



## <a name="flowchart"></a>Diagrama de flujo

Este diagrama de flujo muestra el proceso cuando se incluye el paso Instalar actualizaciones de software en una secuencia de tareas.

[Ver el diagrama en tamaño completo](media/ts-step-install-software-updates.svg)

![Diagrama de flujo para el paso de secuencia de tareas Instalar actualizaciones de software](media/ts-step-install-software-updates.svg)  

1. **Se inicia el proceso en el cliente**: una secuencia de tareas que se ejecuta en un cliente incluye el paso Instalar actualizaciones de software.
2. **Compilar y evaluar directivas**: el cliente compila todas las directivas de actualización de software en el espacio de nombres de WMI RequestedConfigs. (CIAgent.log)
3. *¿Es la primera vez que se llama a esta instancia?*  
    1. **Sí**: vaya a **Examen completo**.  
    2. **No**: *¿el paso está configurado con la opción de [Evaluar actualizaciones de software desde los resultados de análisis en caché](/sccm/osd/understand/task-sequence-steps#evaluate-software-updates-from-cached-scan-results)?*
        1. **Sí**: vaya a **Examen de los resultados almacenados en caché**.
        2. **No**: vaya a **Examen completo**.
4. Proceso de examen: un examen completo o el análisis de los resultados almacenados en caché, con el proceso de supervisión en paralelo.
    1. **Examen completo**: el motor de secuencia de tareas llama al agente de actualización de software a través de la API de actualización de examen para hacer un examen *completo*. (WUAHandler.log, ScanAgent.log)  
        1. **Examen de agente SUM: completo**: proceso de examen normal a través del Agente de Windows Update (WUA), que se comunica con el punto de actualización de software que ejecuta WSUS. Agrega cualquier actualización aplicable al almacén de actualizaciones local. (WindowsUpdate.log, UpdateStore.log)
    2. **Examen de los resultados almacenados en caché**: el motor de secuencia de tareas llama al agente de actualización de software a través de la API de actualización de examen para hacer un examen en relación con los metadatos almacenados en caché. (WUAHandler.log, ScanAgent.log)
        1. **Examen de agente SUM: en caché**: el agente de Windows Update (WUA) comprueba las actualizaciones que ya están en caché en el almacén de actualizaciones local. (WindowsUpdate.log, UpdateStore.log)
    3. **Temporizador de inicio de examen**: el motor de secuencia de tareas inicia un temporizador y espera. (Este proceso se produce en paralelo con el examen completo o el examen del proceso de resultados almacenados en caché).
        1. **Supervisión**: el motor de secuencia de tareas supervisa el estado del agente SUM.
        2. *¿Cuál es la respuesta desde el agente SUM?*
            - **En curso**: ¿ha alcanzado el temporizador el valor en la variable de secuencia de tareas [SMSTSSoftwareUpdateScanTimeout](/sccm/osd/understand/task-sequence-variables#SMSTSSoftwareUpdateScanTimeout)? (El valor predeterminado es 1 hora).
                - **Sí**: error en el paso.
                - **No**: vaya a **Supervisión**.
            - **Erróneo**: error en el paso.
            - **Completo**: vaya a **Enumerar la lista de actualizaciones**.
5. **Enumerar la lista de actualizaciones**: el agente SUM enumera la lista de actualizaciones devueltas por el examen y determina cuáles están disponibles o son obligatorias.
6. *¿Hay alguna actualización en la lista de resultados del examen?*
    - **Sí**: vaya a **Instalar actualizaciones**.
    - **No**: no hay nada que instalar, el paso se completa correctamente.
7. Proceso de implementación: el proceso de actualización de la instalación se produce en paralelo con el proceso de supervisión de la implementación.
    1. **Instalar actualizaciones**: el motor de secuencia de tareas llama al agente SUM a través de la API de actualización de la implementación para instalar todas las actualizaciones disponibles o solo las obligatorias. Este comportamiento se basa en la configuración del paso, tanto si se selecciona **Necesario para la instalación: solo actualizaciones de software obligatorias** o **Disponible para la instalación: todas las actualizaciones de software**. También puede especificar este comportamiento mediante la variable [SMSInstallUpdateTarget](/sccm/osd/understand/task-sequence-variables#SMSInstallUpdateTarget).
        1. **Instalación del agente SUM**: proceso de instalación normal mediante el uso de la lista de actualizaciones en caché existente, con descarga de contenido estándar. Instale la actualización a través del agente de Windows Update. (UpdatesDeployment.log, UpdatesHandler.log, WuaHandler.log, WindowsUpdate.log)
    2. **Iniciar el temporizador de implementación y mostrar el progreso**: el motor de secuencia de tareas inicia un temporizador de instalación, muestra el progreso parcial a intervalos del 10 % en la interfaz de usuario de progreso de TS y espera.
        1. **Supervisión**: el motor de secuencia de tareas sondea el estado del agente SUM.
        2. *¿Cuál es la respuesta desde el agente SUM?*
            - **En curso**: *¿el proceso de instalación ha estado inactivo durante 8 horas?*
                - **Sí**: error en el paso.
                - **No**: vaya a **Supervisión**.
            - **Erróneo**: error en el paso.
            - **Completo**: vaya a *¿El paso está configurado con la opción de **Evaluación de las actualizaciones de software a partir de los resultados del análisis en caché**?*


### <a name="timeouts"></a>Tiempos de espera

El diagrama incluye dos de las variables de tiempo de espera que se aplican a este paso. Hay otros temporizadores estándar de otros componentes que pueden afectar a este proceso.

- Tiempo de espera de actualización del examen: 1 hora (smsts.log)  
- Tiempo de espera de solicitud de ubicación: 1 hora (LocationServices.log, CAS.log)  
- Tiempo de espera de descarga de contenido: 1 hora (DTS.log)  
- Tiempo de espera de punto de distribución inactivo: 1 hora (LocationServices.log, CAS.log)  
- Tiempo de espera inactivo total de la instalación: 8 horas (smsts.log)  



## <a name="troubleshooting"></a>Solución de problemas

Use los siguientes recursos e información adicional para ayudarle a solucionar problemas relacionados con este paso:

- Asegúrese de dirigir las implementaciones de actualización de software a la misma colección que la implementación de la secuencia de tareas.  

- Asegúrese de incluir puntos de actualización de software en los grupos de límites. Para obtener más información, consulte este artículo del [soporte técnico de Microsoft](https://support.microsoft.com/help/4041012/1702-clients-do-not-get-software-updates-from-configuration-manager).  

- Para ayudarle a solucionar problemas del proceso de administración de actualizaciones de software, consulte [Solución de problemas de administración de actualizaciones de software](https://support.microsoft.com/help/10680/software-update-management-troubleshooting-in-configuration-manager).  

- Para ayudar a mejorar el rendimiento general, reduzca el tamaño del catálogo de actualización de software. Por ejemplo:  

    - Quite idiomas, productos y clasificaciones innecesarias. Para más información, vea [Configurar las clasificaciones y los productos que va a sincronizar](/sccm/sum/get-started/configure-classifications-and-products).  

    - Vuelva a indizar la base de datos de sitio y vuelva a compilar las estadísticas. Para obtener más información, consulte [Configuration Manager Perf and Scale Guidance Whitepaper](https://gallery.technet.microsoft.com/Configuration-Manager-ba55428e) (Notas del producto de sobre la guía de rendimiento y escalado de Configuration Manager).  

    - Rechace las actualizaciones innecesarias, por ejemplo:
        - Reemplazadas (a partir de la versión 1810, Configuration Manager realiza esta acción en su lugar. Para obtener más información, vea [WSUS cleanup behavior starting in version 1810](/sccm/sum/deploy-use/software-updates-maintenance#wsus-cleanup-behavior-starting-in-version-1810) [Comportamiento de limpieza de WSUS a partir de la versión 1810]).
        - Itanium
        - Beta
        - Versión siguiente
        - ARM
        - Versiones de Windows que no implementa
