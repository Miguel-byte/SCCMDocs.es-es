---
title: Solución de problemas de SCAP
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo solucionar problemas de extensiones SCAP para Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 27261853-1641-4826-98c6-afbb73a1209d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bb3bcd0e7301ff2ef7baeff29de038cbd8476525
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/31/2018
ms.locfileid: "39383286"
---
# <a name="troubleshoot-the-scap-extensions-for-configuration-manager"></a>Solucionar problemas de extensiones SCAP para Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Las extensiones SCAP de Configuration Manager están diseñadas para que funcionen con los flujos de datos SCAP que están diseñados para la herramienta SCAP validada con capacidad ACS para admitir USGCB. Normalmente, no tendrá problemas con estos flujos de datos de SCAP de USGCB que se descargan desde el sitio web de NIST.

Diagnosticar y solucionar problemas mediante los siguientes métodos:  

- Asegúrese de que los componentes de cliente de las extensiones SCAP (scmdcm.msi) están instalados en todos los equipos de destino.  

- Revise la salida del archivo de registro de la herramienta Microsoft.Sces.ScapToDcm.exe.  

- Revise los problemas y soluciones comunes al usar extensiones SCAP.  

- Póngase en contacto con Microsoft para hacer preguntas o comentarios sobre las extensiones SCAP.



## <a name="review-microsoftscesscaptodcmexe-log"></a>Revisar el registro de Microsoft.Sces.ScapToDcm.exe

La herramienta Microsoft.Sces.ScapToDcm.exe crea un archivo de registro con nombre personalizado cuando especifica el parámetro `–log`. El archivo de registro contiene información sobre los resultados obtenidos al ejecutar la herramienta Microsoft.Sces.ScapToDcm.exe. Por ejemplo, incluye el número de elementos en el archivo de entrada XCCDF/DataStream que se quitaron o se omitieron durante la ejecución de la herramienta Microsoft.Sces.ScapToDcm.exe.

La tabla siguiente muestra parte de la información que aparece en el archivo de registro y una descripción de cada tipo de información.

### <a name="information-found-in-the-microsoftscesscaptodcmexe-log-file"></a>Información encontrada en el archivo de registro de Microsoft.Sces.ScapToDcm.exe

| Información | Descripción |
| --- | --- |
| **Quitar** | Se puede quitar cualquier elemento porque el tipo de prueba no es un tipo de prueba compatible. |
| **Omitir** | El identificador de definición OVAL es para una plataforma no válida. </br> </br> El archivo de entrada XCCDF/DataStream no hace referencia al identificador de definición OVAL.</br> </br> El archivo de entrada XCCDF/DataStream no hace referencia al identificador de prueba OVAL. </br> </br> El identificador de perfil XCCDF no contiene ninguna instrucción `@select` igual a 1. </br> </br> El identificador de perfil XCCDF incluye un atributo abstracto que es true. </br> </br> El identificador de perfil XCCDF no contiene una regla de calificación.|



## <a name="common-problems-and-solutions"></a>Problemas y soluciones comunes

Aquí encontrará algunos problemas y soluciones comunes para ayudarle a solucionar problemas.

- Ve un estado **Error** o **Desconocido** para una línea de base e Internet Explorer no puede mostrar correctamente el informe. El error del explorador es “El informe está vacío o no es válido”.  

     - Vuelva a ejecutar la línea base. Seleccione la línea base y haga clic en **Evaluar**. Después, espere para supervisar el **Estado conforme**/**Actualización de la última evaluación**. Después de que se actualice la fecha de la última evaluación a la fecha y hora actuales, lo que significa que se ha completado la evaluación, seleccione la línea de base y vea el informe de nuevo.  

     - Si Internet Explorer aún no puede ver el informe, tal vez significa que la línea de base es demasiado grande. Vuelva a generar el contenido usando un tamaño de lote más pequeño para crear líneas de base secundarias más pequeñas.  

     - Si se produce este problema en las líneas de base primarias, intente implementar en su lugar las líneas de base secundarias.  

- He creado objetos de directiva de grupo (GPO) que incluyen la configuración recomendada de USGCB. Los he vinculado a las unidades organizativas (OU) que contienen equipos que ejecutan Windows 7. Los informes de cumplimiento indican que algunos de los valores no están configurados correctamente.  

     - Es posible que los permisos de directiva de grupo sean incorrectos o no se hayan vinculado a la unidad organizativa correcta.  

     - Es más probable que la nueva configuración no haya surtido efecto todavía. De forma predeterminada, los clientes de Active Directory comprueban las actualizaciones de directiva de grupo cada 90 minutos. Este ciclo puede ser uno de los motivos por los que parece que la configuración no se ha aplicado, aunque haya configurado correctamente las directivas.  

     - Muchas configuraciones de equipo requieren un reinicio para que surtan efecto. Por ejemplo, el valor para **Criptografía de sistema: usar algoritmos que cumplan FIPS para cifrado, firma y operaciones hash** requiere reiniciar el equipo para que Windows pueda usar los algoritmos de cifrado especificados. Omita el intervalo de actualización de directiva de grupo escribiendo el siguiente comando en un símbolo del sistema con privilegios de administrador: `gpupdate /force`. Una vez completada la actualización de la directiva de grupo, reinicie el equipo para asegurarse de que toda la configuración surta efecto. Para obtener más información, vea [Descripción de la utilidad para actualizar Directiva de grupo](https://support.microsoft.com/help/298444).

- Tengo problemas para proporcionar la conexión de base de datos con la información de la organización.  

     - Para obtener información sobre cómo configurar la conexión de base de datos, vea [Install and configure SCAP](/sccm/compliance/plan-design/scap/install-configure-scap) (Instalar y configurar SCAP).  
