---
title: Habilitación del uso compartido de datos
titleSuffix: Configuration Manager
description: Guía de referencia para uso compartido de datos de diagnóstico con análisis de escritorio.
ms.date: 01/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: be680198-4cea-4378-a686-d52f382ba483
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: f1a6ab6fca6650bde69179b71576d1df2e201b92
ms.sourcegitcommit: f38ef9afb0c608c0153230ff819e5f5e0fb1520c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/19/2019
ms.locfileid: "58196745"
---
# <a name="enable-data-sharing-for-desktop-analytics"></a>Habilitar uso compartido para el escritorio de análisis de datos 

> [!Note]  
> Esta información se relaciona con un servicio en versión preliminar que puede modificarse sustancialmente antes de su lanzamiento comercial. Microsoft no ofrece ninguna garantía, expresa o implícita, con respecto a la información aquí proporcionada.  

Para inscribir dispositivos para el análisis de escritorio, que necesitan enviar datos de diagnóstico a Microsoft. Si su entorno usa un servidor proxy, utilice esta información para ayudarle a configurar al proxy. 


## <a name="diagnostic-data-levels"></a>Niveles de datos de diagnóstico

![Diagrama de niveles de datos de diagnóstico para el análisis de escritorio](media/diagnostic-data-levels.png)

Al integrar Configuration Manager con análisis de escritorio, usa también para administrar el nivel de datos de diagnóstico en los dispositivos. Para obtener la mejor experiencia, use Configuration Manager. 

La funcionalidad básica de escritorio de análisis funciona en el **básica** nivel de datos de diagnóstico. No obtendrá los datos de uso o de mantenimiento para los dispositivos actualizados sin habilitar la **mejorado (limitado)** nivel. Microsoft recomienda que habilite el **mejorado (limitado)** nivel de datos de diagnóstico. Para obtener más información, consulte [mejorada de Windows 10 eventos de datos de diagnóstico y los campos que usa Windows Analytics](https://docs.microsoft.com/windows/privacy/enhanced-diagnostic-data-windows-analytics-events-and-fields)). 

Para obtener más información, consulte [privacidad escritorio Analytics](/sccm/desktop-analytics/privacy).

Los artículos siguientes también son buenos recursos para mejor descripción de los niveles de datos de diagnóstico de Windows: 

- [Windows 10 y el RGPD para decisiones de TI](https://docs.microsoft.com/windows/privacy/gdpr-it-guidance)  

- [Configurar datos de diagnóstico de Windows en su organización](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization)  


> [!Note]  
> En el nivel mejorado (limitado), cuando cada cliente realiza el examen inicial, envía aproximadamente 2 MB de datos en la nube de Microsoft. El delta diario varía entre 400-250 KB por día. 
> 
> Se produce el examen de diferencias diaria a 3:00 A.M. (hora local del dispositivo). Algunos eventos se envían a la primera vez disponible durante todo el día. Estos tiempos no son configurables.
> 
> Para obtener más información, consulte [Configurar los datos de diagnóstico de Windows en la organización](https://aka.ms/enterprisetelemetry).  



## <a name="endpoints"></a>Puntos de conexión

Para habilitar el uso compartido de datos, configure el servidor proxy en la lista blanca los siguientes extremos:

| punto de conexión  | Función  |
|-----------|-----------|
| `https://v10c.events.data.microsoft.com` | Experiencia del usuario conectado y el punto de conexión de diagnóstico del componente. Utilizado por los dispositivos que ejecutan Windows 10, versión 1703 o posterior, con 2018-09 acumulativa update o posterior instalado. |
| `https://v10.events.data.microsoft.com` | Experiencia del usuario conectado y el punto de conexión de diagnóstico del componente. Utilizado por los dispositivos que ejecutan Windows 10, versión 1803 o posterior, _sin_ instalada la actualización acumulativa de 2018-09. |
| `https://v10.vortex-win.data.microsoft.com` | Experiencia del usuario conectado y el punto de conexión de diagnóstico del componente. Utilizado por dispositivos que ejecutan Windows 10, versión 1709 o versiones anterior. |
| `https://vortex-win.data.microsoft.com` | Experiencia del usuario conectado y el punto de conexión de diagnóstico del componente. Utilizado por los dispositivos que ejecutan Windows 7 y Windows 8.1 |
| `https://settings-win.data.microsoft.com` | Permite la actualización de compatibilidad enviar datos a Microsoft. |
| `http://adl.windows.com` | Permite la actualización de compatibilidad recibir los datos de compatibilidad más recientes de Microsoft. |
| `https://watson.telemetry.microsoft.com` | Windows Error Reporting (WER). Se requiere para supervisar el estado de implementación de Windows 10, versión 1803 o una versión anterior. |
| `https://umwatsonc.events.data.microsoft.com` | Windows Error Reporting (WER). Se requiere para los informes de estado dispositivo Windows 10, versión 1809 o posterior. |
| `https://ceuswatcab01.blob.core.windows.net`<br> `https://ceuswatcab02.blob.core.windows.net`<br> `https://eaus2watcab01.blob.core.windows.net`<br> `https://eaus2watcab02.blob.core.windows.net`<br> `https://weus2watcab01.blob.core.windows.net`<br> `https://weus2watcab02.blob.core.windows.net` | Windows Error Reporting (WER). Se requiere para supervisar el estado de implementación de Windows 10, versión 1809 o posterior. |
| `https://www.msftncsi.com` | Windows Error Reporting (WER). Se requiere para que el estado del dispositivo comprobar la conectividad. |
| `https://www.msftconnecttest.com` | Windows Error Reporting (WER). Se requiere para que el estado del dispositivo comprobar la conectividad. | 
| `https://kmwatsonc.events.data.microsoft.com` | Análisis de bloqueos en línea. Se requiere para los informes de estado dispositivo Windows 10, versión 1809 o posterior. |
| `https://oca.telemetry.microsoft.com`  | Análisis de bloqueos en línea (OCA). Se requiere para supervisar el estado de implementación de Windows 10, versión 1803 o una versión anterior. |
| `https://login.live.com` | Debe para proporcionar una identidad de dispositivo más confiable para el análisis de escritorio. <br> <br>Para deshabilitar el acceso de cuenta de Microsoft del usuario final, use la configuración de directiva en lugar de bloquear este punto de conexión. Para obtener más información, consulte [cuenta Microsoft en la empresa](https://docs.microsoft.com/windows/security/identity-protection/access-control/microsoft-accounts#block-all-consumer-microsoft-account-user-authentication). |
| `https://nexusrules.officeapps.live.com` | Se usa para solicitar los eventos de diagnóstico de datos dinámicos desde clientes de Office. Estos datos son útiles para fines de exploración en profundidad y el diagnóstico en el portal de análisis de escritorio |
| `https://nexus.officeapps.live.com` | Usado por los clientes de Office para enviar eventos de datos de diagnóstico desde Office 14, 15 de Office y las versiones anteriores a 16.0.8702 de Office 16. Se usa para recopilar el uso y confiabilidad señales de eventos para el análisis de escritorio. |
| `https://office.pipe.aria.microsoft.com` | Utilizado por los clientes de Office para enviar eventos de datos de diagnóstico de aplicaciones de Office universal/moderno y las versiones de Win32 Office 16 16.0.8702 posterior. Se usa para recopilar el uso y confiabilidad señales de eventos para el análisis de escritorio. |
| `https://graph.windows.net` | Se usa para recuperar automáticamente la configuración como CommercialId al adjuntar la jerarquía para el análisis de escritorio (en función de servidor de Configuration Manager). |
| `https://fef.msua06.manage.microsoft.com` | Se utiliza para sincronizar miembros de la colección de dispositivo, los planes de implementación y estado de preparación del dispositivo con análisis de escritorio (en función de servidor de Configuration Manager). |


### <a name="ssl-inspection"></a>Inspección de SSL

Para privacidad e integridad de datos, Windows busca un certificado SSL de Microsoft al comunicarse con los puntos de conexión de datos de diagnóstico. Inspección e intercepción de SSL no son posibles. Para utilizar el análisis de escritorio, excluir los puntos de conexión anteriores de la inspección de SSL.



## <a name="proxy-server-authentication"></a>Autenticación del servidor proxy

Asegúrese de que un servidor proxy no bloquea los datos de diagnóstico debido a la autenticación. Si su organización usa la autenticación del servidor proxy para el tráfico saliente, utilice uno o varios de los métodos siguientes:

- **Omisión** (recomendado): Configure los servidores proxy que no se requiere autenticación proxy para el tráfico a los puntos de conexión de datos de diagnóstico. Esta opción es la solución más completa. Funciona con todas las versiones de Windows 10.  

- **Autenticación del usuario proxy**: Configurar dispositivos para usar el contexto del usuario que inició sesión para la autenticación proxy. Este método requiere que los dispositivos que ejecutan Windows 10, versión 1703 o posterior. Asegúrese de que los usuarios tienen permiso de proxy para llegar a los puntos de conexión de datos de diagnóstico. Esta opción requiere que los dispositivos tienen los usuarios de la consola con permisos de servidor proxy, por lo que no puede usar este método con dispositivos sin periféricos.  

- **Autenticación de proxy de dispositivo**: 
    - Configurar un servidor proxy de nivel de sistema en los dispositivos.  
    - Configurar estos dispositivos para usar la autenticación de proxy de salida basado en dispositivos.  
    - Configure los servidores proxy para permitir que las cuentas de equipo tener acceso a los puntos de conexión de datos de diagnóstico.  



