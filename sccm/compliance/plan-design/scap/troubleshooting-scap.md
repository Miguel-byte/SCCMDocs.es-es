---
title: Solución de problemas de SCAP
titleSuffix: Configuraton Manager
description: Importar la configuración de cumplimiento de SCAP como líneas base de configuración y exportar los resultados
ms.date: 03/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 27261853-1641-4826-98c6-afbb73a1209d
author: aczechowski
ms.author: aaroncz
manager: dougeby
robots: noindex,nofollow
ms.openlocfilehash: 05010d73916ac4c012c157a470ed98dce47fc747
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="troubleshoot-the-scap-extensions-for-microsoft-system-center-configuration-manager"></a>Solucionar problemas de extensiones SCAP para Microsoft System Center Configuration Manager.

*Se aplica a: System Center Configuration Manager (Rama actual)*

> [!Tip]  
> Esta característica se introdujo por primera vez en la versión preliminar técnica 1803 como una [característica de versión preliminar](/sccm/core/servers/manage/pre-release-features). Esta versión preliminar de las extensiones SCAP puede instalarse en cualquier versión admitida de Rama actual de Configuration Manager y LTSB 1606. El archivo de instalación se encuentra en cd.latest\SMSSETUP\TOOLS\ConfigMgrSCAPExtension\ConfigMgrExtensionsForSCAP.msi a partir de 1803 Technical Preview. 

Las extensiones SCAP de Microsoft System Center Configuration Manager están diseñadas para que funcionen con los flujos de datos SCAP que están diseñados para la herramienta SCAP validada con capacidad ACS para admitir USGCB. Normalmente, no tendrá problemas con estos flujos de datos de SCAP de USGCB que se descargan desde el sitio web de NIST.

Pero puede diagnosticar y solucionar problemas que puedan surgir mediante estos métodos:

- Asegúrese de que los componentes de cliente de las extensiones SCAP (scmdcm.msi) están instalados en todos los equipos de destino.
- Revise la salida del archivo de registro de la herramienta Microsoft.Sces.ScapToDcm.exe.
- Revise los problemas y soluciones comunes al usar extensiones SCAP.
- Póngase en contacto con Microsoft para hacer preguntas o comentarios sobre las extensiones SCAP.



## <a name="review-microsoftscesscaptodcmexe-tool-log"></a>Revisar el registro de la herramienta Microsoft.Sces.ScapToDcm.exe

La herramienta Microsoft.Sces.ScapToDcm.exe crea un archivo de registro con nombre personalizado cuando se especifica el parámetro –log. El archivo de registro contiene información sobre los resultados obtenidos al ejecutar la herramienta Microsoft.Sces.ScapToDcm.exe. Por ejemplo, el archivo de registro tiene el número de elementos en el archivo de entrada XCCDF/DataStream que se quitaron o se omitieron durante la ejecución de la herramienta Microsoft.Sces.ScapToDcm.exe.

La tabla siguiente muestra parte de la información que aparece en el archivo de registro y una descripción de cada tipo de información.

### <a name="description-of-information-found-in-microsoftscesscaptodcmexe-log-files"></a>Descripción de la información encontrada en los archivos de registro de Microsoft.Sces.ScapToDcm.exe

| Información | Descripción |
| --- | --- |
| Quitar | Se puede quitar cualquier elemento porque el tipo de prueba no es un tipo de prueba compatible. |
| Skip |El identificador de definición OVAL es para una plataforma no válida. </br> </br> El archivo de entrada XCCDF/DataStream no hace referencia al identificador de definición OVAL.</br> </br> El archivo de entrada XCCDF/DataStream no hace referencia al identificador de prueba OVAL. </br> </br> El identificador de perfil XCCDF no contiene ninguna instrucción @select igual a 1. </br> </br> El identificador de perfil XCCDF incluye un atributo abstracto que es true. </br> </br> El identificador de perfil XCCDF no contiene una regla de calificación.|

## <a name="common-problems-and-solutions"></a>Problemas y soluciones comunes

En la tabla siguiente se enumeran algunos problemas y soluciones comunes para ayudarle a solucionar problemas.

Tabla 1.6. Problemas y soluciones comunes

| Problema | Solución posible |
| --- | --- |
| Si ve los estados **Error** o **Desconocido** de una línea de base e IE no puede mostrar correctamente el informe. IE muestra el mensaje &quot;El informe está vacío o no es válido&quot;. | Seleccione la línea de base y haga clic en **Evaluar** para volver a ejecutar la línea de base. Después, espere para supervisar el **Estado conforme**/**Actualización de la última evaluación**. Después de que se actualiza la fecha de la última evaluación a la fecha y hora actuales (significa que se ha completado la evaluación), seleccione la línea de base y vea el informe de nuevo. Si IE aún no puede ver el informe, tal vez significa que la línea de base es demasiado grande. Vuelva a generar el contenido usando un tamaño de lote más pequeño para crear líneas de base secundarias más pequeñas. Si se produce este problema en las líneas de base primarias, intente implementar en su lugar las líneas de base secundarias. |
| He creado objetos de directiva de grupo (GPO) que incluyen la configuración recomendada de USGCB y los he vinculado a las unidades organizativas (OU) que contienen equipos que ejecutan Windows 7, pero los informes de cumplimiento indican que algunos de los valores no están configurados correctamente. | Es posible que los permisos de directiva de grupo sean incorrectos o no se hayan vinculado a la unidad organizativa correcta. Sin embargo, es más probable que la nueva configuración no haya surtido efecto todavía. De manera predeterminada, la directiva de grupo en equipos cliente que pertenecen a un dominio de Active Directory busca actualizaciones de directiva de grupo cada 90 minutos. Esto puede ser uno de los motivos por los que parece que la configuración no se ha aplicado, aunque haya configurado correctamente las directivas. Otro factor que hay que recordar es que muchas configuraciones de equipo requieren un reinicio para que surtan efecto. Por ejemplo, el valor denominado **Criptografía de sistema: usar algoritmos que cumplan FIPS para cifrado, firma y operaciones hash requiere reiniciar el equipo para que Windows pueda usar los algoritmos de cifrado especificados. Puede omitir el intervalo de actualización de la directiva de grupo. Para ello, escriba el comando gpupdate /force en un símbolo del sistema con privilegios de administrador. Después de completarse la actualización de la directiva de grupo, reinicie el equipo para asegurarse de que toda la configuración surta efecto. Para más información, vea el artículo 298444 de la Base de conocimientos: [Una descripción de la utilidad de actualización de la directiva de grupo](http://support.microsoft.com/kb/298444). |
| Tengo problemas para proporcionar la conexión de base de datos con la información de la organización. | Para obtener información de procedimientos para configurar la información de conexión de base de datos, vea el artículo [Install and configure SCAP](/sccm/compliance/plan-design/scap/install-configure-scap) (Instalar y configurar SCAP). 

## <a name="next-step"></a>Paso siguiente
> [!div class="nextstepaction"]
> [Instalar y configurar extensiones SCAP](/sccm/compliance/plan-design/scap/install-configure-scap)