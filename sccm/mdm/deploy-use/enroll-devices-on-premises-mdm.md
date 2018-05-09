---
title: 'Inscribir dispositivos '
titleSuffix: Configuration Manager
description: Obtenga información sobre los métodos para inscribir dispositivos para la administración de dispositivos móviles local en System Center Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: b58472e3-31a5-4305-8eb6-2522befebe02
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7e3254fdad766260e3e162378894526e9b4a7249
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="enroll-devices-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>Inscribir dispositivos para la administración local de dispositivos móviles en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Para administrar equipos y dispositivos con la administración de dispositivos móviles local de System Center Configuration Manager, los dispositivos deben estar inscritos para que Configuration Manager pueda comunicarse con ellos para las tareas de administración. Configuration Manager proporciona dos métodos para la inscripción de dispositivos:  

-   **Inscripción de usuario** : en este método, los usuarios inician el proceso de inscripción en sus dispositivos. Para que la inscripción de usuario se realice correctamente, el dispositivo debe tener un certificado raíz de confianza instalado y Configuration Manager debe aprovisionar el usuario para la inscripción.  Para inscribir el dispositivo, el usuario solo tiene que proporcionar las credenciales de trabajo y el dispositivo se inscribirá para su administración.  

     Para obtener más información, consulte [How users enroll devices with On-premises Mobile Device Management in System Center Configuration Manager](../../mdm/deploy-use/user-enroll-devices-on-premises-mdm.md) (Cómo inscriben dispositivos los usuarios mediante la administración de dispositivos móviles (MDM) local en System Center Configuration Manager).  

-   **Inscripción masiva** : en este método, no es necesario que el usuario del dispositivo inicie la inscripción. En su lugar, se crea un paquete de inscripción masiva en Configuration Manager, que luego se coloca y se abre en el dispositivo. Una vez abierto, el paquete proporciona la información necesaria para inscribir el dispositivo.  

     Para obtener más información, consulte [How to bulk-enroll devices with On-premises Mobile Device Management in System Center Configuration Manager](../../mdm/deploy-use/bulk-enroll-devices-on-premises-mdm.md) (Cómo inscribir dispositivos en masa con la administración local de dispositivos móviles en System Center Configuration Manager).  

 > [!NOTE]  
>  La rama actual de Configuration Manager admite la inscripción en la administración local de dispositivos móviles para dispositivos con los sistemas operativos siguientes:  
>   
>  -   Windows 10 Enterprise  
> -   Windows 10 Pro  
> -   Windows 10 Team 
> -   Windows 10 Mobile  
> -   Windows 10 Mobile Enterprise   
