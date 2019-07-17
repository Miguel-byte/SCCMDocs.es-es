---
title: Mensajes de estado
titleSuffix: Configuration Manager
description: Descripciones de los mensajes de estado en las versiones compatibles de Configuration Manager.
ms.date: 02/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: f04c0a71-57bc-4443-a47c-592373050d04
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: a83a7100819718dc8bd5fa74f0e4a317b4b47e44
ms.sourcegitcommit: f9654cd1a3af6d67de52fedaccceb2e22dafc159
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/09/2019
ms.locfileid: "67676736"
---
# <a name="state-messages-in-configuration-manager"></a>Mensajes de estado en Configuration Manager 

*Se aplica a: System Center Configuration Manager (Rama actual)*

Los mensajes de estado contienen información concisa sobre las condiciones en el cliente de Configuration Manager. El sistema de mensajes de estado se usa por componentes específicos de Configuration Manager, como las actualizaciones de software y las opciones de configuración.

Los clientes de Configuration Manager envían mensajes de estado al punto de estado de reserva o los sistemas de sitio de punto de administración para notificar el estado actual de las operaciones. Puede crear informes para ver los mensajes de estado enviados por clientes de Configuration Manager.

Cada característica de Configuration Manager que usa mensajes de estado se identifica mediante el tipo de tema del mensaje de estado. Los tipos de tema de mensaje de estado que aparecen en este artículo pueden usarse para definir la característica de Configuration Manager a la que se refiere un mensaje de estado.

> [!NOTE]  
> Un valor de identificador de mensaje de estado de cero (0) indica normalmente que el tipo de tema se encuentra en un estado desconocido.

## <a name="300-statetopictypesumassignmentcompliance"></a>300 STATE_TOPICTYPE_SUM_ASSIGNMENT_COMPLIANCE

|      Id. del mensaje de estado     |  Descripción del mensaje de estado |
|:-------------|:------|
| 0 | Estado de compatibilidad desconocido|
| 1 | conforme | 
| 2 | No compatible | 

## <a name="301-statetopictypesumassignmentenforcement"></a>301 STATE_TOPICTYPE_SUM_ASSIGNMENT_ENFORCEMENT

|       Id. del mensaje de estado     |  Descripción del mensaje de estado |
|:-------------|:------|
| 0  | Estado de aplicación desconocido |
| 1  | Instalando actualizaciones        | 
| 2  | Esperando reiniciarse          | 
| 3  | Esperando a que se complete otra instalación         | 
| 4  | Actualización instalada correctamente (2)          | 
| 5  | Reinicio del sistema pendiente         | 
| 6  | No se pudieron instalar las actualizaciones         | 
| 7  | Descargando las actualizaciones   | 
| 8  | Actualizaciones descargadas    | 
| 9  | No se pudieron descargar las actualizaciones     | 
| 10 | Esperando a la ventana de mantenimiento antes de la instalación         | 
| 11 | Esperando orquestación         | 

## <a name="302-statetopictypesumassignmentevaluation"></a>302 STATE_TOPICTYPE_SUM_ASSIGNMENT_EVALUATION

|     Id. del mensaje de estado     |  Descripción del mensaje de estado |
|:-------------|:------|      
| 0 | Estado de evaluación desconocido|                 
| 1 |Evaluación activada      |
| 2 |Evaluación con éxito      |
| 3 |Error de evaluación      |


## <a name="400-statetopictypesumcidetection"></a>400 STATE_TOPICTYPE_SUM_CI_DETECTION

|     Id. del mensaje de estado     |  Descripción del mensaje de estado |
|:-------------|:------|
| 0 | Estado de detección desconocido|
| 1 | No se requiere   |
| 2 | No detectado    |
| 3 | Detectado   |

## <a name="401-statetopictypesumcicompliance"></a>401 STATE_TOPICTYPE_SUM_CI_COMPLIANCE

|     Id. del mensaje de estado     |  Descripción del mensaje de estado |
|:-------------|:------|
| 0 | Estado de compatibilidad desconocido|
| 1 |conforme     |
| 2 |No compatible     |
| 3 |Conflicto detectado    |
| 4 |Error      |
| 5 |Desconocida     |
| 6 |Cumplimiento parcial   |
| 7 |Cumplimiento no configurado    |

## <a name="402-statetopictypesumcienforcement"></a>402 STATE_TOPICTYPE_SUM_CI_ENFORCEMENT

|     Id. del mensaje de estado     |  Descripción del mensaje de estado |
|:-------------|:------|
| 0  | Estado de aplicación desconocido|
| 1  |Aplicación iniciada          |
| 2  |Aplicación esperando contenido         |
| 3  | Esperando a que se complete otra instalación        |
| 4  |Esperando a la ventana de mantenimiento antes de la instalación         |
| 5  |Es necesario reiniciar antes de instalar         |
| 6  |Error general        |
| 7  |Instalación pendiente         |
| 8  |Instalando actualización          |
| 9  |Reinicio del sistema pendiente        |
| 10 |Actualización instalada correctamente         |
| 11 |No se pudo instalar la actualización        |
| 12 |Descargando actualización        |
| 13 | Actualización descargada        |
| 14 |No se pudo descargar la actualización        |

## <a name="500-statetoptctypesumupdatedetection"></a>500 STATE_TOPTCTYPE_SUM_UPDATE_DETECTION

|     Id. del mensaje de estado     |  Descripción del mensaje de estado |
|:-------------|:------|
|0 |Estado de detección desconocido|
| 1 | Actualización no necesaria  |
| 2 | Actualización necesaria   |
| 3 | Actualización instalada  |

## <a name="501-statetopictypesumupdatesourcescan"></a>501 STATE_TOPICTYPE_SUM_UPDATE_SOURCE_SCAN

|     Id. del mensaje de estado     |  Descripción del mensaje de estado |
|:-------------|:------|
| 0 |Estado de examen desconocido|
| 1 | El examen está esperando contenido   |
| 2 | Examen en curso    |
| 3 | Examen completado    |
| 4 | Examen pendiente de reintento   |
| 5 | Error en el examen   |
| 6 | Examen completado con errores |

## <a name="700-statetopictyperesyncstatemsg"></a>700 STATE_TOPICTYPE_RESYNC_STATE_MSG

No hay ningún id. de estado.

## <a name="701-statetopictypesystemheartbeat"></a>701 STATE_TOPICTYPE_SYSTEM_HEARTBEAT

No hay ningún id. de estado.

## <a name="702-statetopictypeckdupdate"></a>702 STATE_TOPICTYPE_CKD_UPDATE
 
No hay ningún id. de estado.

## <a name="800-statetopictypeclientdeployment"></a>800 STATE_TOPICTYPE_CLIENT_DEPLOYMENT

|     Id. del mensaje de estado     |  Descripción del mensaje de estado |
|:-------------|:------|
| 100 |Implementación de cliente iniciada      |       
| 101 |Esperando la descarga       |       
| 102 |Descarga programada       |       
| 103 | Esperando la ventana antes de implementar |
| 104 |Implementación omitida       |       
| 301 |Error desconocido al implementar el cliente |       
| 302 |No se pudo crear el servicio ccmsetup  |       
| 303 |No se pudo eliminar el servicio ccmsetup |       
| 304 |No se puede instalar sobre el SO incrustado con el filtro de escritura basado en archivos (FBWF) habilitado en la unidad del sistema |       
| 305 |El modo de seguridad nativo no es válido en Windows 2000  |       
| 306 |No se pudo iniciar el proceso de descarga de ccmsetup  |       
| 307 |Línea de comandos de ccmsetup no válida |       
| 308 |No se pudo descargar el archivo a través de WINHTTP en la dirección |       
| 309 |No se pudieron descargar archivos a través de BITS en la dirección |       
| 310 |No se pudo instalar la versión de BITS |       
| 311 |No se puede comprobar que el archivo de requisitos previos esté firmado por MS  |       
| 312 |No se pudo copiar el archivo porque el disco está lleno |       
| 313 |No se pudo realizar la instalación de Client.msi y se devolvió un error de MSI |       
| 314 |No se pudo cargar el archivo de manifiesto de ccmsetup.xml |       
| 315 |No se pudo obtener un certificado de cliente  |       
| 316 |El archivo de requisitos previos no está firmado por MS |       
| 317 |Se requiere un reinicio para continuar con la instalación  |       
| 318 |No se puede instalar el cliente en el módulo de administración porque su versión no coincide con la del cliente |       
| 319 |Sistema operativo o Service Pack no admitido  |       
| 320 |No se admite la implementación       |       
| 321 |Faltan bits        |       
| 322 |Carpeta de origen no disponible       |       
| 323 |Aplicación no compatible              |       
| 324 |Versión del sitio incorrecta              |       
| 325 |Error de coincidencia de hash de requisitos previos       |       
| 326 |No se pudo cancelar el registro de MDM      |       
| 327 |Se detectó el registro de MDM      |       
| 328 |Intune detectado       |       
| 329 |Red de uso medido no permitida      |       
| 400 |Implementación de cliente con éxito |  
| 401 |Implementación correcta; es necesario reiniciar     |       
| 402 |Implementación correcta; reinicio correcto     |
| 500 |Se inició la asignación de cliente|
| 601 |Error de asignación de cliente desconocido|
| 602 |El siguiente código de sitio no es válido|
| 603 |No se pudo asignar a MP|
| 604 |No se pudo detectar el punto de administración predeterminado|
| 605 |No se pudo descargar el certificado de firma del sitio|
| 606 |No se pudo detectar automáticamente el código del sitio|
| 607 |Error de asignación del sitio. La versión del cliente es superior a la versión del sitio|
| 608 |No se pudo obtener la versión del sitio de Active Directory Domain Services y SLP|
| 609 |No se pudo obtener la versión del cliente|
| 700 |Asignación de cliente con éxito|

## <a name="801-statetopictypedeviceclientdeployment"></a>801 STATE_TOPICTYPE_DEVICE_CLIENT_DEPLOYMENT

No hay ningún id. de estado.

## <a name="810-statetopictypeclientcomanagement"></a>810 STATE_TOPICTYPE_CLIENT_COMANAGEMENT

|     Id. del mensaje de estado     |  Descripción del mensaje de estado |
|:-------------|:------|
| 100 | Estado de inscripción   |
| 101 | Inscripción programada   |
| 102 | Inscripción cancelada   |
| 105 | Inscripción iniciada   |
| 106 | La inscripción se realizó correctamente pero no está aprovisionada
| 107 | La inscripción se realizó correctamente y está aprovisionada
| 108 | Inscripción sin usuarios activos   |
| 110 | Error en la inscripción   |


## <a name="820--statetopictypeclientwufb"></a>820  STATE_TOPICTYPE_CLIENT_WUFB

|     Id. del mensaje de estado     |  Descripción del mensaje de estado |
|:-------------|:------|
| 1 | Estado de cliente de Windows Update para empresas| 

## <a name="900-statetopictypebranchdp"></a>900 STATE_TOPICTYPE_BRANCH_DP

|     Id. del mensaje de estado     |  Descripción del mensaje de estado |
|:-------------|:------|
| 1 | Espacio en disco   | 

## <a name="901-statetopictyperemotedpmonitoring"></a>901 STATE_TOPICTYPE_REMOTE_DP_MONITORING

No hay ningún id. de estado.

## <a name="902-statetopictypepulldpmonitoring"></a>902 STATE_TOPICTYPE_PULL_DP_MONITORING

No hay ningún id. de estado.

## <a name="903-statetopictypedpusage"></a>903 STATE_TOPICTYPE_DP_USAGE

No hay ningún id. de estado.

## <a name="1000--statetopictypeclientframeworkcomm"></a>1000  STATE_TOPICTYPE_CLIENT_FRAMEWORK_COMM

|     Id. del mensaje de estado     |  Descripción del mensaje de estado |
|:-------------|:------|
| 1 | El cliente se está comunicando correctamente con el punto de administración |
| 2 | El cliente no se pudo comunicar con el punto de administración |

## <a name="1001-statetopictypeclientframeworklocal"></a>1001 STATE_TOPICTYPE_CLIENT_FRAMEWORK_LOCAL

|     Id. del mensaje de estado     |  Descripción del mensaje de estado |
|:-------------|:------|
| 1 |El cliente recuperó correctamente el certificado del almacén de certificados local    |
| 2 |El cliente no pudo recuperar el certificado del almacén de certificados local |

## <a name="1002-statetopictypedeviceclientframeworkcomm"></a>1002 STATE_TOPICTYPE_DEVICE_CLIENT_FRAMEWORK_COMM

No hay ningún id. de estado.

## <a name="1003-statetopictypedeviceclientframeworklocal"></a>1003 STATE_TOPICTYPE_DEVICE_CLIENT_FRAMEWORK_LOCAL

No hay ningún id. de estado.

## <a name="1004-statetopictypedeviceclientframeworkcertificate"></a>1004 STATE_TOPICTYPE_DEVICE_CLIENT_FRAMEWORK_CERTIFICATE

No hay ningún id. de estado.

## <a name="1005-statetopictypedeviceclientwipe"></a>1005 STATE_TOPICTYPE_DEVICE_CLIENT_WIPE

No hay ningún id. de estado.

## <a name="1006-statetopictypedeviceclientretire"></a>1006 STATE_TOPICTYPE_DEVICE_CLIENT_RETIRE

No hay ningún id. de estado.

## <a name="1007-statetopictypedeviceclientwipeintune"></a>1007 STATE_TOPICTYPE_DEVICE_CLIENT_WIPE_INTUNE

No hay ningún id. de estado.

## <a name="1008-statetopictypedeviceclientretireintune"></a>1008 STATE_TOPICTYPE_DEVICE_CLIENT_RETIRE_INTUNE

No hay ningún id. de estado.

## <a name="1009-statetopictypedeviceclientdevicelock"></a>1009 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICELOCK

No hay ningún id. de estado.

## <a name="1010-statetopictypedeviceclientdevicelockintune"></a>1010 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICELOCK_INTUNE

No hay ningún id. de estado.

## <a name="1011-statetopictypedeviceclientdevicepinreset"></a>1011 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEPINRESET

No hay ningún id. de estado.

## <a name="1012-statetopictypedeviceclientdevicepinresetintune"></a>1012 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEPINRESET_INTUNE

No hay ningún id. de estado.

## <a name="1013-statetopictypedeviceclientdevicepinresetonprem"></a>1013 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEPINRESET_ONPREM

No hay ningún id. de estado.

## <a name="1014-statetopictypedeviceclientdevicealbypass"></a>1014 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEALBYPASS

No hay ningún id. de estado.

## <a name="1015-statetopictypedeviceclientdevicealbypassintune"></a>1015 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEALBYPASS_INTUNE

No hay ningún id. de estado.

## <a name="1100-statetopictypeclientframeworkmodereadiness"></a>1100 STATE_TOPICTYPE_CLIENT_FRAMEWORK_MODEREADINESS

|     Id. del mensaje de estado     |  Descripción del mensaje de estado |
|:-------------|:------|
| 1 |El cliente no está listo para el modo nativo  |
| 2 |El cliente está listo para el modo nativo     |


## <a name="1300-statetopictypeclienthealth"></a>1300 STATE_TOPICTYPE_CLIENT_HEALTH

|     Id. del mensaje de estado     |  Descripción del mensaje de estado |
|:-------------|:------|
| 1 | Correcto|
| 2 | Incorrecto |

## <a name="1401-statetopictypestatereport"></a>1401 STATE_TOPICTYPE_STATE_REPORT

No hay ningún id. de estado.

## <a name="1500-statetopictypecaltrackut"></a>1500 STATE_TOPICTYPE_CAL_TRACK_UT

No hay ningún id. de estado.

## <a name="1502-statetopictypecaltrackmt"></a>1502 STATE_TOPICTYPE_CAL_TRACK_MT

No hay ningún id. de estado.

## <a name="1503-statetopictypecaltrackml"></a>1503 STATE_TOPICTYPE_CAL_TRACK_ML

No hay ningún id. de estado. 

## <a name="1600-statetopictypeuseraffinity"></a>1600 STATE_TOPICTYPE_USER_AFFINITY

|     Id. del mensaje de estado     |  Descripción del mensaje de estado |
|:-------------|:------|
| 1 |Conjunto de afinidad de usuario       |
| 2 |Afinidad de usuario quitada       |

## <a name="1700-statetopictypeappciscan"></a>1700 STATE_TOPICTYPE_APP_CI_SCAN

No hay ningún id. de estado.

## <a name="1701-statetopictypeappcicompliance"></a>1701 STATE_TOPICTYPE_APP_CI_COMPLIANCE

No hay ningún id. de estado.

## <a name="1702-statetopictypeappcienforcement"></a>1702 STATE_TOPICTYPE_APP_CI_ENFORCEMENT

|     Id. del mensaje de estado     |  Descripción del mensaje de estado |
|:-------------|:------|
| 1000  |Elemento de configuración correcto           |
| 1001 |Elemento de configuración correcto ya instalado         |
| 1002 |Elemento de configuración ha realizado correctamente las comprobaciones          |
| 1003 |El estado rápido del elemento configuración se realizó correctamente          |
| 2000 |Elemento de configuración en curso           |
| 2001 |Elemento de configuración en curso esperando contenido         |
| 2002 |Elemento de configuración en curso instalándose          |
| 2003 |Elemento de configuración en curso esperando reinicio         |
| 2004 |Elemento de configuración en curso esperando ventana de mantenimiento        |
| 2005 |Elemento de configuración en curso esperando programación         |
| 2006 |Elemento de configuración en curso descargando contenido dependiente     |
| 2007 |Elemento de configuración en curso instalando dependencias        |
| 2008 |Elemento de configuración en curso pendiente de reinicio         |
| 2009 |Elemento de configuración en curso con contenido descargado         |
| 2010 |Elemento de configuración en curso pendiente de actualización         |
| 2011 |Elemento de configuración en curso esperando reconexión de usuario        |
| 2012 |Elemento de configuración en curso esperando cierre de sesión de usuario         |
| 2013 |Elemento de configuración en curso esperando inicio de sesión de usuario         |
| 2014 |Elemento de configuración en curso esperando instalación         |
| 2015 |Elemento de configuración en curso esperando reintento         |
| 2016 |Elemento de configuración en curso esperando presmode         |
| 2017 |Elemento de configuración en curso esperando orquestación        |
| 2018 |Elemento de configuración en curso esperando red         |
| 2019 |Elemento de configuración en curso pendiente de actualización VE         |
| 2020 |Elemento de configuración en curso actualizando VE         |
| 3000 |No se cumplen los requisitos del elemento de configuración           |
| 3001 |No se cumplen los requisitos del elemento de configuración; host no aplicable        |
| 4000 |Elemento de configuración desconocido           |
| 5000 |Error de elemento de configuración            |
| 5001 |Error al evaluar el elemento de configuración          |
| 5002 |Error al instalar el elemento de configuración          |
| 5003 |Error al recuperar el contenido del elemento de configuración         |
| 5004 |Error al instalar la dependencia del elemento de configuración         |
| 5005 |Error al recuperar la dependencia de contenido del elemento de configuración        |
| 5006 |Error del elemento de configuración; reglas en conflicto          |
| 5007 |Error del elemento de configuración; esperando reintento          |
| 5008 |Error del elemento de configuración al desinstalar la sustitución        |
| 5009 |Error del elemento de configuración; descarga sustituida         |
| 5010 |Error del elemento de configuración al actualizar VE          |
| 5011 |Error del elemento de configuración al instalar licencia         |
| 5012 |Error de elemento de configuración al recuperar el permiso de todas las aplicaciones de confianza       |
| 5013 |Error de elemento de configuración; no hay licencias disponibles         |
| 5014 |Error de elemento de configuración; SO no compatible          |
| 6000 |Inicio del elemento de configuración correcto            |
| 6010 |Error de inicio del elemento de configuración            |
| 6020 |Inicio desconocido del elemento de configuración|

## <a name="1703-statetopictypeappciassignmentevaluatio"></a>1703 STATE_TOPICTYPE_APP_CI_ASSIGNMENT_EVALUATIO

No hay ningún id. de estado.

## <a name="1704-statetopictypeappcilaunch"></a>1704 STATE_TOPICTYPE_APP_CI_LAUNCH

No hay ningún id. de estado.

## <a name="1800-statetopictypeeventintrinsic"></a>1800 STATE_TOPICTYPE_EVENT_INTRINSIC

No hay ningún id. de estado.

## <a name="1801-statetopictypeeventextrinsic"></a>1801 STATE_TOPICTYPE_EVENT_EXTRINSIC

No hay ningún id. de estado.

## <a name="1900-statetopictypeepaminfection"></a>1900 STATE_TOPICTYPE_EP_AM_INFECTION

No hay ningún id. de estado.

## <a name="1901-statetopictypeepamhealth"></a>1901 State_Topictype_Ep_Am_Health

No hay ningún id. de estado.

## <a name="1902-statetopictypeepmalware"></a>1902 STATE_TOPICTYPE_EP_MALWARE

No hay ningún id. de estado.

## <a name="1950-statetopictypeatphealthstatus"></a>1950 STATE_TOPICTYPE_ATP_HEALTH_STATUS

No hay ningún id. de estado.

## <a name="2001-statetopictypeepclientdeployment"></a>2001 STATE_TOPICTYPE_EP_CLIENT_DEPLOYMENT

|     Id. del mensaje de estado     |  Descripción del mensaje de estado |
|:-------------|:------|
| 1 |Endpoint Protection no administrado   |
| 2 |Endpoint Protection esperando instalación  |
| 3 |Endpoint Protection administrado   |
| 4 |Error de instalación de Endpoint Protection  |
| 5 |Reinicio pendiente de Endpoint Protection  |
| 6 |Endpoint Protection no compatible   |
| 7 |Endpoint Protection coadministrado   |

## <a name="2002-statetopictypeepclientpolicyapplication"></a>2002 STATE_TOPICTYPE_EP_CLIENT_POLICYAPPLICATION

|     Id. del mensaje de estado     |  Descripción del mensaje de estado |
|:-------------|:------|
| 0 |Estado de la aplicación de directiva de Endpoint Protection desconocido    |
| 1 |Aplicación de directiva de Endpoint Protection correcta    |
| 2 |Aplicación de directiva de Endpoint Protection con error    |

## <a name="2003-statetopictypeclientaction"></a>2003 STATE_TOPICTYPE_CLIENT_ACTION

|     Id. del mensaje de estado     |  Descripción del mensaje de estado |
|:-------------|:------|
| 0 |  Desconocida    |
| 1 |  Activo    |
| 2 |  Inactivo    |

## <a name="2100-statetopictypewpclientdeployment"></a>2100 STATE_TOPICTYPE_WP_CLIENT_DEPLOYMENT

|     Id. del mensaje de estado     |  Descripción del mensaje de estado |
|:-------------|:------|
| 1 | No está instalado el proxy de reactivación    |
| 2 | El proxy de reactivación está esperando la instalación   |
| 3 | Está instalado el proxy de reactivación    |
| 4 | Error en la instalación del proxy de reactivación   |
| 5 | El proxy de reactivación está esperando el reinicio   |
| 6 | El proxy de reactivación no se admite en este SO  |
| 7 | El servidor del proxy de reactivación no puede participar   |
| 8 | No se pudo desinstalar el proxy de reactivación   |
| 9 | Entorno de ejecución del proxy de reactivación no compatible   |

## <a name="2200-statetopictypefdm"></a>2200 STATE_TOPICTYPE_FDM

No hay ningún id. de estado.

## <a name="2201-statetopictypeccmcertbinding"></a>2201 STATE_TOPICTYPE_CCM_CERT_BINDING

No hay ningún id. de estado.

## <a name="2202-statetopictypeserverstatistic"></a>2202 STATE_TOPICTYPE_SERVER_STATISTIC

No hay ningún id. de estado.

## <a name="3000-statetopictypedmwnschannel"></a>3000 STATE_TOPICTYPE_DM_WNS_CHANNEL

|     Id. del mensaje de estado     |  Descripción del mensaje de estado |
|:-------------|:------|
|0 | Conjunto de canales del servicio de notificaciones de inserción de Windows|

## <a name="4000-statetopictypemdmdeviceproperty"></a>4000 STATE_TOPICTYPE_MDM_DEVICE_PROPERTY

No hay ningún id. de estado.

## <a name="4002-statetopictypemdmclientidenitity"></a>4002 STATE_TOPICTYPE_MDM_CLIENT_IDENITITY

No hay ningún id. de estado.

## <a name="4003-statetopictypemdmapplicationrequest"></a>4003 STATE_TOPICTYPE_MDM_APPLICATION_REQUEST

No hay ningún id. de estado.

## <a name="4004-statetopictypemdmapplicationstate"></a>4004 STATE_TOPICTYPE_MDM_APPLICATION_STATE

No hay ningún id. de estado.

## <a name="4005-statetopictypemdmlicensedevicerelation"></a>4005 STATE_TOPICTYPE_MDM_LICENSE_DEVICE_RELATION

No hay ningún id. de estado.

## <a name="4006-statetopictypemdmlicensekeys"></a>4006 STATE_TOPICTYPE_MDM_LICENSE_KEYS

No hay ningún id. de estado.

## <a name="4007-statetopictypemdmpolicyassignment"></a>4007 STATE_TOPICTYPE_MDM_POLICY_ASSIGNMENT

No hay ningún id. de estado.

## <a name="4008-statetopictypemdmandroidcount"></a>4008 STATE_TOPICTYPE_MDM_ANDROID_COUNT

No hay ningún id. de estado.

## <a name="4009-statetopictypemdmslkstatus"></a>4009 STATE_TOPICTYPE_MDM_SLK_STATUS

No hay ningún id. de estado.

## <a name="4010-statetopictypemdmusercompanytermacceptance"></a>4010 STATE_TOPICTYPE_MDM_USER_COMPANY_TERM_ACCEPTANCE

No hay ningún id. de estado.

## <a name="4022-statetopictypemdmdepsyncnowstatus"></a>4022 STATE_TOPICTYPE_MDM_DEP_SYNCNOW_STATUS

No hay ningún id. de estado.

## <a name="4023-statetopictypemdmmamstoreappsync"></a>4023 STATE_TOPICTYPE_MDM_MAM_STORE_APP_SYNC

No hay ningún id. de estado.

## <a name="5000-statetopictypecertificateenrollment"></a>5000 STATE_TOPICTYPE_CERTIFICATE_ENROLLMENT

|     Id. del mensaje de estado     |  Descripción del mensaje de estado |
|:-------------|:------|
| 1 |Desafío emitido         |
| 2 |Error de emisión de desafío        |
| 3 |Error al crear la solicitud        |
| 4 |Error de envío de solicitud        |
| 5 |Validación del desafío correcta       |
| 6 |Error de validación del desafío       |
| 7 |Error de emisión         |
| 8 |Emisión pendiente         |
| 9 |Emitido          |
| 10 |Error al procesar la respuesta       |
| 11 |Respuesta pendiente         |
| 12 |Inscripción realizada correctamente         |
| 13 |Inscripción no necesaria         |
| 14 |Revocado          |
| 15 |Se ha quitado de la colección        |
| 16 |Renovar comprobado         |
| 17 |No se pudo realizar la instalación        |
| 18 |Instalado         |
| 19 |Error de eliminación         |
| 20 |Eliminado         |
| 21 |Renovación solicitada        |


## <a name="5001-statetopictypecertificatecrp"></a>5001 STATE_TOPICTYPE_CERTIFICATE_CRP

|     Id. del mensaje de estado     |  Descripción del mensaje de estado |
|:-------------|:------|
| 1 |Desafío emitido         |
| 2 |Error de emisión de desafío        |
| 3 |Error al crear la solicitud        |
| 4 |Error de envío de solicitud        |
| 5 |Validación del desafío correcta       |
| 6 |Error de validación del desafío       |
| 7 |Error de emisión         |
| 8 |Emisión pendiente         |
| 9 |Emitido          |
| 10 |Error al procesar la respuesta       |
| 11 |Respuesta pendiente         |
| 12 |Inscripción realizada correctamente         |
| 13 |Inscripción no necesaria         |
| 14 |Revocado          |
| 15 |Se ha quitado de la colección        |
| 16 |Renovar comprobado         |
| 17 |No se pudo realizar la instalación        |
| 18 |Instalado         |
| 19 |Error de eliminación         |
| 20 |Eliminado         |
| 21 |Renovación solicitada        |

## <a name="5200-statetopictyperesourceaccessstatus"></a>5200 STATE_TOPICTYPE_RESOURCE_ACCESS_STATUS

|     Id. del mensaje de estado     |  Descripción del mensaje de estado |
|:-------------|:------|
| 1 | La configuración del pin de estado se realizó correctamente       |
| 2 | Error en la configuración del pin de estado       |
| 3 | Configuración del pin de estado no admitida      |
| 4 | Configuración del pin de estado en curso      |

## <a name="6000-statetopictyperemoteappsubscriptionstatus"></a>6000 STATE_TOPICTYPE_REMOTEAPP_SUBSCRIPTION_STATUS

No hay ningún id. de estado.

## <a name="6001-statetopictyperemoteappsubscriptionsyncstatus"></a>6001 STATE_TOPICTYPE_REMOTEAPP_SUBSCRIPTION_SYNC_STATUS

No hay ningún id. de estado.

## <a name="6002-statetopictyperemoteappauthcookiessyncstatus"></a>6002 STATE_TOPICTYPE_REMOTEAPP_AUTHCOOKIES_SYNC_STATUS

No hay ningún id. de estado.

## <a name="6003-statetopictyperemoteapplicationssyncstatus"></a>6003 STATE_TOPICTYPE_REMOTEAPPLICATIONS_SYNC_STATUS

No hay ningún id. de estado.

## <a name="6004-statetopictyperemoteapplockresult"></a>6004 STATE_TOPICTYPE_REMOTEAPP_LOCK_RESULT

No hay ningún id. de estado.

## <a name="7000-statetopictypeusercompanytermacceptance"></a>7000 STATE_TOPICTYPE_USER_COMPANY_TERM_ACCEPTANCE

No hay ningún id. de estado.

## <a name="7001-statetopictypepfxcertificate"></a>7001 STATE_TOPICTYPE_PFX_CERTIFICATE

|     Id. del mensaje de estado     |  Descripción del mensaje de estado |
|:-------------|:------|
| 1 |Desafío emitido    |
| 2 |Error de emisión de desafío   |
| 3 |Error al crear la solicitud   |
| 4 |Error de envío de solicitud   |
| 5 |Validación del desafío correcta  |
| 6 |Error de validación del desafío  |
| 7 |Error de emisión    |
| 8 |Emisión pendiente    |
| 9 |Emitido     |
| 10 |Error al procesar la respuesta  |
| 11 |Respuesta pendiente    |
| 12 |Inscripción realizada correctamente    |
| 13 |Inscripción no necesaria    |
| 14 |Revocado     |
| 15 |Se ha quitado de la colección   |
| 16 |Renovar comprobado    |
| 17 |No se pudo realizar la instalación   |
| 18 |Instalado    |
| 19 |Error de eliminación    |
| 20 |Eliminado    |
| 21 |Renovación solicitada   |

## <a name="7010-statetopictypeconditionalaccesscompliance"></a>7010 STATE_TOPICTYPE_CONDITIONAL_ACCESS_COMPLIANCE

|     Id. del mensaje de estado     |  Descripción del mensaje de estado |
|:-------------|:------|
|| 1 | Cumplimiento correcto    |
| 2 | Error de cumplimiento en el módulo de administración   |
| 3 | Error de cumplimiento en el cliente   |
| 4 | Error de cumplimiento en Intune   |
| 5 | Error de cumplimiento en AAD   |
| 6 | Coadministración de cumplimiento en Intune   |

## <a name="7200-statetopictypesuperpeerupdatecachemap"></a>7200 STATE_TOPICTYPE_SUPER_PEER_UPDATE_CACHE_MAP

|     Id. del mensaje de estado     |  Descripción del mensaje de estado |
|:-------------|:------|
| 1 |Origen de la caché del mismo nivel agregado       |
| 2 |Origen de la caché del mismo nivel eliminado      |

## <a name="7201-statetopictypesuperpeerupdateconfig"></a>7201 STATE_TOPICTYPE_SUPER_PEER_UPDATE_CONFIG

|     Id. del mensaje de estado     |  Descripción del mensaje de estado |
|:-------------|:------|
| 1 |Origen de la caché del mismo nivel desactivado       |
| 2 |El origen de la caché del mismo nivel está activo       |

## <a name="7202-statetopictypedownloadaggregatedata"></a>7202 STATE_TOPICTYPE_DOWNLOAD_AGGREGATE_DATA
|     Id. del mensaje de estado     |  Descripción del mensaje de estado |
|:-------------|:------|
| 1 |Descargar la carga de datos agregados       |

## <a name="7203-statetopictypepeersourcereqrejectionstats"></a>7203 STATE_TOPICTYPE_PEERSOURCE_REQ_REJECTION_STATS

|     Id. del mensaje de estado     |  Descripción del mensaje de estado |
|:-------------|:------|
| 1 |Carga de datos de rechazo de origen del mismo nivel     |

## <a name="7300-statetopictypeproxytraffic"></a>7300 STATE_TOPICTYPE_PROXY_TRAFFIC

No hay ningún id. de estado.

## <a name="7301-statetopictypeproxyconnection"></a>7301 STATE_TOPICTYPE_PROXY_CONNECTION

No hay ningún id. de estado.

## <a name="7302-statetopictypesrsusagedata"></a>7302 STATE_TOPICTYPE_SRS_USAGE_DATA

No hay ningún id. de estado.

## <a name="7303-statetopictypeproxytrafficidentity"></a>7303 STATE_TOPICTYPE_PROXY_TRAFFIC_IDENTITY

No hay ningún id. de estado.

## <a name="8001-statetopictypehasreport"></a>8001 STATE_TOPICTYPE_HAS_REPORT

|     Id. del mensaje de estado     |  Descripción del mensaje de estado |
|:-------------|:------|
| 1 |Se admite la atestación de estado      |
| 2 |No se admite la atestación de estado      |

## <a name="statetopictypedeviceclientedplog"></a>STATE_TOPICTYPE_DEVICE_CLIENT_EDPLOG

No hay ningún id. de estado.

## <a name="8003-statetopictypeenablelostmode"></a>8003 STATE_TOPICTYPE_ENABLE_LOSTMODE

No hay ningún id. de estado.

## <a name="8004-statetopictypedisablelostmode"></a>8004 STATE_TOPICTYPE_DISABLE_LOSTMODE

No hay ningún id. de estado.

## <a name="8005-statetopictypelocatedevice"></a>8005 STATE_TOPICTYPE_LOCATE_DEVICE

No hay ningún id. de estado.

## <a name="8006-statetopictyperebootdevice"></a>8006 STATE_TOPICTYPE_REBOOT_DEVICE

No hay ningún id. de estado.

## <a name="8007-statetopictypelogoutuser"></a>8007 STATE_TOPICTYPE_LOGOUTUSER

No hay ningún id. de estado.

## <a name="8008-statetopictypeuserslist"></a>8008 STATE_TOPICTYPE_USERSLIST

No hay ningún id. de estado.

## <a name="8009-statetopictypedeleteuser"></a>8009 STATE_TOPICTYPE_DELETEUSER

No hay ningún id. de estado.

## <a name="8010-statetopictypecleanpcretaininguserdata"></a>8010 STATE_TOPICTYPE_CLEANPCRETAININGUSERDATA

No hay ningún id. de estado.

## <a name="8011-statetopictypecleanpcwithoutretaininguserdata"></a>8011 STATE_TOPICTYPE_CLEANPCWITHOUTRETAININGUSERDATA

No hay ningún id. de estado.

## <a name="8012-statetopictypesetdevicename"></a>8012 STATE_TOPICTYPE_SETDEVICENAME

No hay ningún id. de estado.

## <a name="9000-statetopictypebookcicompliance"></a>9000 STATE_TOPICTYPE_BOOK_CI_COMPLIANCE

No hay ningún id. de estado.

## <a name="9001-statetopictypebookcienforcement"></a>9001 STATE_TOPICTYPE_BOOK_CI_ENFORCEMENT

No hay ningún id. de estado.

## <a name="next-steps"></a>Pasos siguientes

- [Descripción del estado de mensajería en Configuration Manager](https://support.microsoft.com/help/4459394/description-of-state-messaging-in-system-center-configuration-manager)
- [Software updates management whitepaper for Configuration Manager](https://www.microsoft.com/download/details.aspx?id=44578) (Notas del producto de administración de actualizaciones de software de Configuration Manager)
