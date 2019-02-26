---
title: Acceso condicional con administración conjunta
titleSuffix: Configuration Manager
description: Controlar el acceso a recursos de la organización según las reglas de cumplimiento de Intune
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4cf640b3-610c-4c3c-b966-c62e9f5654ff
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2d5e5c7d6075697431f8c537366dc16164fedd1f
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56755540"
---
# <a name="conditional-access-with-co-management"></a>Acceso condicional con administración conjunta

Acceso condicional se asegura de que solo los usuarios de confianza pueden tener acceso a recursos de la organización en dispositivos de confianza con las aplicaciones de confianza. Se crea a partir de cero en la nube. Si está administrando los dispositivos con Intune o ampliar la implementación de Configuration Manager con la administración conjunta, funciona del mismo modo.

En el siguiente vídeo, jefe de programas senior Joey Glocke y Ainley Locky del Administrador de marketing de productos tratan y demostración de acceso condicional con administración conjunta:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/The-Security-Benefits-of-Conditional-Access/player]

Con la administración conjunta, Intune evalúa todos los dispositivos de la red para determinar el nivel de confianza es. Esta evaluación realiza en las dos maneras siguientes:

1. Intune asegura de que un dispositivo o aplicación administrada y configurada de forma segura. Esta comprobación depende de cómo establecer las directivas de cumplimiento de su organización. Por ejemplo, asegúrese de que tienen habilitado el cifrado de todos los dispositivos y no están liberados.  

    - Esta evaluación es la infracción de seguridad anterior y basada en la configuración  

    - Para dispositivos administrados conjuntamente, Configuration Manager también realiza la evaluación de configuración. Por ejemplo, requiere compatibilidad de aplicaciones o actualizaciones. Intune combina esta evaluación junto con su propia evaluación.  

2. Intune detecta los incidentes de seguridad activas en un dispositivo. Utiliza la seguridad inteligente de [protección contra amenazas avanzada de Windows Defender](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/get-started) y otros [proveedores de defensa contra amenazas móviles](https://www.lookout.com/about/partners/microsoft). Estos asociados ejecutan análisis de comportamiento en curso en los dispositivos. Este análisis detecta incidentes activos y, a continuación, pasa esta información a Intune para la evaluación de cumplimiento en tiempo real.  

    - Esta evaluación es de seguridad posteriores a la infracción y basado en incidentes  

Microsoft vicepresidente corporativo de Brad Anderson analiza el acceso condicional en profundidad con demostraciones en vivo durante el discurso de apertura de Ignite de 2018. 

> [!VIDEO https://www.youtube.com/embed/7tDbUhVCX_I?start=1071]

Acceso condicional también proporciona un lugar centralizado para ver el estado de todos los dispositivos conectados en red. Obtenga las ventajas de escala de nube, lo que resulta especialmente útil para pruebas de las instancias de producción de Configuration Manager.


## <a name="benefits"></a>Ventajas

Cada equipo de TI está obsesionado con la seguridad de red. Es obligatorio para asegurarse de que todos los dispositivos con sus requisitos empresariales y de seguridad antes de acceder a la red. Con el acceso condicional, puede determinar los factores siguientes: 
- Si se cifran todos los dispositivos  
- Si se instala un malware  
- Si se actualiza su configuración  
- Si lo está liberado o modificado  

Acceso condicional combina un control granular sobre los datos de la organización con una experiencia de usuario que se maximice la productividad de los trabajadores en cualquier dispositivo desde cualquier ubicación.

El siguiente vídeo muestra cómo [protección avanzada de subproceso](https://www.microsoft.com/windowsforbusiness/windows-atp) (ATP) se integra en escenarios comunes que suelen producirse:

> [!VIDEO https://www.youtube.com/embed/A7IrxAH87wc?start=178]

Con la administración conjunta, Intune puede incorporar las responsabilidades del Administrador de configuración para evaluar el cumplimiento de estándares de seguridad de aplicaciones o actualizaciones necesarias. Este comportamiento es importante para cualquier organización de TI que desea continuar usando el Administrador de configuración de aplicación compleja y la administración de revisiones.

Acceso condicional también es una parte fundamental del desarrollo de su [cero Trust Network](https://cloudblogs.microsoft.com/microsoftsecure/2018/06/14/building-zero-trust-networks-with-microsoft-365/) arquitectura. Con acceso condicional, los controles de acceso de dispositivo compatible cubren los niveles básicos de red de confianza de cero. Esta funcionalidad es una gran parte del modo de proteger su organización en el futuro.

Para obtener más información, consulte la entrada de blog en [mejora del acceso condicional con los datos de riesgo de la máquina de la protección de amenazas avanzada de Windows Defender](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/Enhancing-conditional-access-with-machine-risk-data-from-Windows/ba-p/250559).



## <a name="case-studies"></a>Casos prácticos

La TI consulting Wipro firme usa acceso condicional para proteger y administrar los dispositivos usados por todos los 91,000 empleados. En un estudio de caso reciente, el vicepresidente de TI en Wipro se indica:

> *Lograr el acceso condicional es un gran logro para Wipro. Ahora, todos los empleados tienen acceso móvil a información a petición. * 
>  *Hemos mejorado nuestra productividad del empleado y postura de seguridad. Ahora 91,000 empleados beneficiarán del acceso altamente seguro a más de 100 aplicaciones desde cualquier dispositivo, en cualquier lugar.*

<!-- waiting for the case study to be public
For more information, see [Wipro drives mobile productivity with Microsoft cloud security tools to improve customer engagements](https://customers.microsoft.com/story/446f72f9-2f50-4697-b688-6d279786e010)
-->

Otros ejemplos incluyen: 

- Nestle, que usa acceso condicional basado en aplicaciones de más de 150.000 empleados  

- La compañía de software de automatización, cadencia, quién puede ahora Asegúrese de que "solo los dispositivos administrados tengan acceso a aplicaciones de Office 365, como los equipos y de la intranet de la empresa." También pueden ofrecer a sus recursos humanos "acceso más seguro a otras aplicaciones basadas en la nube, como Workday y Salesforce." Para obtener más información acerca de la experiencia de la cadencia con Intune, consulte [cadencia aumenta el ritmo de negocios con herramientas de colaboración móviles en Microsoft 365](https://customers.microsoft.com/story/cadence-partner-professional-services-microsoft-365).

También es totalmente, Intune se integra con partners como Cisco ISE, Aruba Clear Pass y Citrix NetScaler. Con estos asociados, puede mantener los controles de acceso en función de la inscripción de Intune y el estado de cumplimiento de dispositivos en estas otras plataformas.

Para obtener más información, consulte los siguientes vídeos:
- [Acceso condicional de demostraciones de Brad Anderson en detalle](https://youtu.be/8321obNofgM?t=547)  
- [Detalles adicionales de punto de conexión de zona 1805](https://youtu.be/f-ILlEuBFZg?t=196)  


## <a name="value-proposition"></a>Propuesta de valor

Con acceso condicional y la integración de ATP, está refuerzo un componente fundamental de todas las organizaciones de TI: proteger el acceso a la nube.

En más del 63% de todas las infracciones de datos, los atacantes obtienen acceso a la red de la organización a través de las credenciales de usuario débiles, predeterminadas o lo roban. Acceso condicional se centra en la protección de la identidad del usuario, ya que restringe el robo de credenciales. Acceso condicional administra y protege las identidades, ya sea con privilegios o sin privilegios. No hay ninguna manera mejor para proteger los dispositivos y los datos en ellos.

Puesto que el acceso condicional es un componente principal de Enterprise Mobility + Security (EMS), no hay ninguna instalación local o la arquitectura necesaria. Con Intune y Azure Active Directory (Azure AD), puede configurar rápidamente el acceso condicional en la nube. Si actualmente está usando Configuration Manager, puede ampliar su entorno a la nube con la administración conjunta fácilmente y empezar a usarlo ahora mismo.

Para obtener más información acerca de la integración de ATP, vea esta entrada de blog [puntuación de riesgo del dispositivo de Windows Defender ATP expone cyberattack nueva, controla el acceso condicional para proteger redes](https://cloudblogs.microsoft.com/microsoftsecure/2018/11/28/windows-defender-atp-device-risk-score-exposes-new-cyberattack-drives-conditional-access-to-protect-networks/). Explica cómo un grupo de hackers avanzada utilizado nunca antes vistas herramientas. La nube de Microsoft detectado y había detenido debido a que los usuarios de destino tenían acceso condicional. La intrusión activa la directiva de acceso condicional en función del riesgo del dispositivo. Aunque el atacante ha establecido un punto de apoyo en la red, las máquinas aprovechadas se restringieron automáticamente contra el acceso a los servicios organizativos y datos administrados por Azure AD.



## <a name="configure"></a>Configurar

Acceso condicional es fácil de usar cuando se [habilitar la administración conjunta](/sccm/comanage/how-to-enable). Requiere mover la **las directivas de cumplimiento** carga de trabajo a Intune. Para más información, consulte [Cambiar las cargas de trabajo de Configuration Manager a Intune](/sccm/comanage/how-to-switch-workloads). 

Para obtener más información sobre el uso de acceso condicional, consulte los artículos siguientes: 

- [Acceso condicional en Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)  

- [Directivas de cumplimiento de dispositivos de Intune](https://docs.microsoft.com/intune/device-compliance)  

- [Acceso condicional basado en aplicación con Intune](https://docs.microsoft.com/intune/app-based-conditional-access-intune)  

> [!Note]  
> Características de acceso condicional están disponibles inmediatamente para Azure híbrido dispositivos Unidos a AD. Estas características incluyen la autenticación multifactor y control de acceso de combinación de Azure AD híbrido. Este comportamiento es porque están basados en las propiedades de Azure AD. Para sacar provecho de evaluación basada en la configuración de Intune y Configuration Manager, habilite la administración conjunta. Esta configuración permite que control de acceso directamente desde Intune para dispositivos compatibles. También ofrece característica de evaluación de directivas de cumplimiento de Intune.  

