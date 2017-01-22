---

title: "Integración con Windows Update for Business en Windows 10 | Microsoft Docs"
description: "Use Windows Update for Business para mantener actualizados los dispositivos basados en Windows 10 de su organización para los dispositivos conectados al servicio de Windows Update."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: 183315fe-27bd-456f-b2c5-e8d25e05229b
translationtype: Human Translation
ms.sourcegitcommit: e6cf8c799b5be2f7dbb6fadadddf702ec974ae45
ms.openlocfilehash: 8bdbacd54632475ac69a0d0a9a34b2567c3daa13


---
# <a name="integration-with-windows-update-for-business-in-windows-10"></a>Integración con Windows Update for Business en Windows 10

*Se aplica a: System Center Configuration Manager (rama actual)*

Windows Update for Business (WUfB) le permite mantener los dispositivos basados en Windows 10 de su organización siempre actualizados con las características de Windows y las defensas de seguridad más recientes cuando estos dispositivos se conectan directamente al servicio de Windows Update (WU). Configuration Manager tiene la capacidad de diferenciar entre los equipos con Windows 10 que usan WUfB y WSUS para obtener actualizaciones de software.  

 Algunas características de Configuration Manager ya no están disponibles cuando los clientes de Configuration Manager se configuran para recibir actualizaciones de WU, lo que incluye WUfB o Windows Insiders:  

-   Informes de cumplimiento de Windows Update:  

    -   Configuration Manager no tendrá conocimiento de las actualizaciones que se publican en WU. Los clientes de Configuration Manager configurados para recibir actualizaciones de WU mostrarán **desconocido** para estas actualizaciones en la consola de Configuration Manager.  

    -   La solución de problemas de estado de cumplimiento general es difícil porque el estado **desconocido** solía ser solo para los clientes que no habían devuelto su estado de examen a WSUS.  Ahora también incluye los clientes de Configuration Manager que reciben las actualizaciones de WU.  

    -   El acceso condicional (para los recursos corporativos) según el estado de cumplimiento de actualización no funcionará como se espera para los clientes que reciben actualizaciones de WU, ya que nunca cumplirían con la compatibilidad desde Configuration Manager.  

    -   El cumplimiento de las actualizaciones de definición es parte de los informes de cumplimiento general de actualización y no funcionará como sería de esperar.  El cumplimiento de las actualizaciones de definición también forma parte de la evaluación de acceso condicional.  

-   Los informes generales de Endpoint Protection para Defender según el estado del cumplimiento de las actualizaciones no devolverán resultados precisos debido a la pérdida de datos de análisis.  

-   Configuration Manager no podrá implementar las actualizaciones de Microsoft, como Office, Internet Explorer y Visual Studio, en los clientes que están conectados a WUfB para recibir actualizaciones.  

-   Configuration Manager no podrá implementar actualizaciones de terceros publicadas en WSUS y administradas a través de Configuration Manager en los clientes que están conectados a WUfB para recibir actualizaciones.  

-   La implementación del cliente completo de Configuration Manager que usa la infraestructura de actualizaciones de software no funcionará para los clientes que están conectados a WUfB para recibir actualizaciones.  

## <a name="identify-clients-that-use--wufb-for-windows-10-updates"></a>Identificar a los clientes que utilizan WUfB para actualizaciones de Windows 10  
 Utilice el procedimiento siguiente para identificar a los clientes que utilizan WUfB para obtener las actualizaciones de Windows 10, configurar estos clientes para que dejen de usar WSUS para obtener actualizaciones e implementar una configuración de agente cliente para deshabilitar el flujo de trabajo de las actualizaciones de software para estos clientes.  

 **Requisitos previos**  

-   Clientes que ejecutan Windows 10 Desktop Pro o Windows 10 Enterprise Edition versión 1511 o posterior  

-   [Windows Update for Business](https://technet.microsoft.com/library/mt622730\(v=vs.85\).aspx) está implementado y los clientes utilizan WUfB para obtener las actualizaciones de Windows 10.  

#### <a name="to-identify-clients-that-use-wufb"></a>Para identificar los clientes que utilizan WUfB  

1.  Si lo tiene habilitado, deshabilite el agente de Windows Update para que no examine nada con WSUS.   
    La clave del Registro **HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU\UseWUServer** se puede establecer para indicar si el equipo está realizando algún análisis con WSUS o Windows Update.  Cuando el valor es 2, no se realiza el análisis con WSUS.  

2.  Existe un nuevo atributo, **UseWUServer**, que se encuentra en el nodo **Windows Update** del Explorador de recursos de Configuration Manager.  

3.  Cree una colección basada en el atributo **UseWUServer** para todos los equipos que estén conectados a través de WUfB para conseguir actualizaciones.  

4.  Cree una configuración de agente cliente para deshabilitar el flujo de trabajo de la actualización de software e implementar la configuración en la colección de equipos que están conectados directamente a WUfB.  

5.  Los equipos que se administran a través de WUfB, mostrarán el valor **Desconocido** en el estado de cumplimiento y no se tendrán en cuenta como parte del porcentaje total de cumplimiento.  



<!--HONumber=Dec16_HO3-->


