---
title: Uso de datos de diagnóstico
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo Microsoft usa los datos de uso y diagnóstico que System Center Configuration Manager recopila.
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a8021bc8-2799-41f4-83c2-e27d1242028c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fac92818a56b9ef7c7e8e6b923fb0d833f9053c2
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="how-diagnostics-and-usage-data-is-used-for-system-center-configuration-manager"></a>Cómo se usan los datos de uso y diagnóstico para System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Los datos de uso y diagnóstico recopilados por System Center Configuration Manager proporcionan información casi inmediata a Microsoft sobre cómo funciona el producto y se usa para ajustar las actualizaciones futuras. También podemos ver datos de configuración que nos ayudan a diseñar y probar las configuraciones que están en producción. Por ejemplo:  

-   Las versiones de servidor de Windows que usan los servidores de sitio  

-   Los paquetes de idioma instalados  

-   Las diferencias entre el esquema SQL y el valor predeterminado del producto  

Estos datos ayudan al equipo de ingeniería a planear futuras pruebas para garantizar la mejor experiencia con las configuraciones más comunes. Como las actualizaciones a Configuration Manager se publican a un ritmo más rápido (para admitir mejor tecnologías que cambian rápidamente, como Windows 10 y Microsoft Intune), estos datos son cruciales para ajustarse y adaptarse rápidamente.  

Reviste la misma importancia la forma en que no se usan los datos de uso y diagnóstico. Microsoft no utiliza estos datos para:  

-   Auditorías de licencias, como comparar el uso del cliente con respecto a los contratos de licencia  

-   Auditoría de los productos que están fuera del soporte técnico  

-   Publicidad basada en los datos disponibles, como el uso de características o la ubicación geográfica (zona horaria)  

##  <a name="bkmk_improve"></a> Ejemplos de cómo los datos de uso y diagnóstico mejoran el producto  
Microsoft utiliza los datos disponibles para mejorar el producto. Estos son algunos ejemplos:  

-   **Compatibilidad revisada con sistemas operativos de servidor anteriores:**  

     La compatibilidad inicial que ofrecía la rama actual de System Center Configuration Manager limitaba la escala de tiempo del soporte técnico para Windows Server 2008 R2. Después de examinar los datos de uso de los clientes que habían actualizado a la rama actual de Configuration Manager, se identificó la necesidad de revisar y extender esta escala de tiempo para dar soporte a los clientes que aún usan este sistema operativo del servidor para hospedar servidores de sitio y roles de sistema de sitio.  

-   **Comprobaciones mejoradas de requisitos previos:**  

     En función de los datos de uso, se han mejorado las comprobaciones de requisitos previos para instalar una actualización, a fin de quitar reglas obsoletas, incorporar casos adicionales y, en casos adicionales, corregir algunos problemas de forma automática.  
