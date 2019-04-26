---
title: Configuración del inventario de hardware para dispositivos móviles
titleSuffix: Configuration Manager
description: Configure el inventario de hardware para dispositivos móviles inscritos mediante Microsoft Intune y System Center Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 78a0aecc-f775-451e-aa05-56377ec91b1f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: d1a208b3bac5d0b12a9fd395506f02d283a0b55f
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62228253"
---
# <a name="how-to-configure-hardware-inventory-for-mobile-devices-enrolled-by-microsoft-intune-and-system-center-configuration-manager"></a>Cómo configurar el inventario de hardware en dispositivos móviles inscritos mediante Microsoft Intune y System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

En Configuration Manager, puede recopilar el inventario de hardware en dispositivos Windows, Android e iOS mediante el conector de Microsoft Intune. Para obtener más información sobre cómo configurar el inventario de hardware, consulte [How to extend hardware inventory in System Center Configuration Manager](../../core/clients/manage/inventory/extend-hardware-inventory.md) (Ampliación del inventario de hardware en System Center Configuration Manager).  

 Para más información sobre cómo inscribir dispositivos en Microsoft Intune, vea [Inscribir dispositivos para administrarlos en Intune](https://technet.microsoft.com/library/dn646962.aspx).  

## <a name="hardware-inventory-for-mobile-devices"></a>Inventario de hardware para dispositivos móviles  
 Las tablas siguientes enumeran las clases de inventario disponibles para el inventario de hardware en plataformas móviles utilizadas.  

 **iOS**  

|Clase de inventario de hardware|iOS|  
|------------------------------|---------|  
|Nombre|Device_ComputerSystem.DeviceName|  
|Id. de dispositivo único|Device_ComputerSystem.UDID|  
|Número de serie|Device_ComputerSystem.SerialNumber|  
|Dirección de correo electrónico|Device_Email.OwnerEmailAddress|  
|Tipo de sistema operativo|No aplicable|  
|Versión de sistema operativo|Device_OSInformation.OSVersion|  
|Versión de compilación|No aplicable|  
|Versión principal de Service Pack|No aplicable|  
|Versión secundaria de Service Pack|No aplicable|  
|Idioma del sistema operativo|No aplicable|  
|Espacio de almacenamiento total|Device_Memory.DeviceCapacity|  
|Espacio de almacenamiento libre|Device_Memory.AvailableDeviceCapacity|  
|Identidad de equipo móvil internacional o IMEI (IMEI)|Device_ComputerSystem.IMEI|  
|Identificador de equipo móvil (MEID)|Device_ComputerSystem.MEID|  
|Fabricante|No aplicable|  
|Modelo|ModelName|  
|Número de teléfono<sup>1</sup>|Device_ComputerSystem.PhoneNumber|  
|Operador del suscriptor|Device_ComputerSystem.SubscriberCarrierNetwork|  
|Tecnología de datos móviles|Device_ComputerSystem.CellularTechnology|  
|MAC Wi-Fi|Device_WLAN.WiFiMAC|  

 **Android**  

> [!NOTE]  
>  **NOTA:** Clases de inventario de Android están disponibles cuando se usa la aplicación de Portal de empresa Android.  

|Clase de inventario de hardware|Android|  
|------------------------------|-------------|  
|Nombre|No aplicable|  
|Id. de dispositivo único|No aplicable|  
|Número de serie|Device_ComputerSystem.SerialNumber|  
|Dirección de correo electrónico|No aplicable|  
|Tipo de sistema operativo|Device_OSInformation.Platform|  
|Versión de sistema operativo|Device_OSInformation.Version|  
|Versión de compilación|No aplicable|  
|Versión principal de Service Pack|No aplicable|  
|Versión secundaria de Service Pack|No aplicable|  
|Idioma del sistema operativo|No aplicable|  
|Espacio de almacenamiento total|Device_Memory.StorageTotal|  
|Espacio de almacenamiento libre|Device_Memory.StorageFree|  
|Identidad de equipo móvil internacional o IMEI (IMEI)|Device_ComputerSystem.IMEI|  
|Identificador de equipo móvil (MEID)|No aplicable|  
|Fabricante|Device_Info.Manufacturer|  
|Modelo|Device_Info.Model|  
|Número de teléfono<sup>1</sup>|Device_ComputerSystem.PhoneNumber|  
|Operador del suscriptor|Device_ComputerSystem.SubscriberCarrierNetwork|  
|Tecnología de datos móviles|Device_ComputerSystem.CellularTechnology|  
|MAC Wi-Fi|Device_WLAN.WiFiMAC|  

 **Windows Phone 8/8.1**  

|Clase de inventario de hardware|Windows Phone 8 y Windows Phone 8.1|  
|------------------------------|-------------------------------------------|  
|Nombre|Device_ComputerSystem.DeviceName|  
|Id. de dispositivo único|Device_ComputerSystem.DeviceClientID|  
|Número de serie|No aplicable|  
|Dirección de correo electrónico|Device_Email.OwnerEmailAddress|  
|Tipo de sistema operativo|Device_OSInformation.Platform|  
|Versión de sistema operativo|Device_ComputerSystem.SoftwareVersion|  
|Versión de compilación|No aplicable|  
|Versión principal de Service Pack|No aplicable|  
|Versión secundaria de Service Pack|No aplicable|  
|Idioma del sistema operativo|Device_OSInformation.Language|  
|Espacio de almacenamiento total|No aplicable|  
|Espacio de almacenamiento libre|No aplicable|  
|Identidad de equipo móvil internacional o IMEI (IMEI)|No aplicable|  
|Identificador de equipo móvil (MEID)|No aplicable|  
|Fabricante|Device_ComputerSystem.DeviceManufacturer|  
|Modelo|Device_ComputerSystem.DeviceModel|  
|Número de teléfono<sup>1</sup>|No aplicable|  
|Operador del suscriptor|No aplicable|  
|Tecnología de datos móviles|No aplicable|  
|MAC Wi-Fi|No aplicable|  

 **Windows RT**  

|Clase de inventario de hardware|Windows RT|  
|------------------------------|----------------|  
|Nombre|Device_ComputerSystem.DeviceName|  
|Id. de dispositivo único|Device_ComputerSystem.DeviceName|  
|Número de serie|No aplicable|  
|Dirección de correo electrónico|Device_Email.OwnerEmailAddress|  
|Tipo de sistema operativo|CCM_OperatingSystem.SystemType|  
|Versión de sistema operativo|Win32_OperatingSystem.Version|  
|Versión de compilación|Win32_OperatingSystem.BuildNumber|  
|Versión principal de Service Pack|Win32_OperatingSystem.ServicePackMajorVersion|  
|Versión secundaria de Service Pack|Win32_OperatingSystem.ServicePackMinorVersion|  
|Idioma del sistema operativo|No aplicable|  
|Espacio de almacenamiento total|Win32_PhysicalMemory.Capacity|  
|Espacio de almacenamiento libre|Win32_OperatingSystem.FreePhysicalMemory|  
|Identidad de equipo móvil internacional o IMEI (IMEI)|No aplicable|  
|Identificador de equipo móvil (MEID)|No aplicable|  
|Fabricante|Win32_ComputerSystem.Manufacturer|  
|Modelo|Win32_ComputerSystem.Model|  
|Número de teléfono<sup>1</sup>|No aplicable|  
|Operador del suscriptor|No aplicable|  
|Tecnología de datos móviles|No aplicable|  
|MAC Wi-Fi|Win32_NetworkAdapter.MACAddress|  

 <sup>1</sup> El número de teléfono se enmascara con * excepto los cuatro últimos dígitos.  

 Para que el inventario recopile el número de teléfono, el dispositivo debe tener una tarjeta SIM y un número de teléfono proporcionado por el proveedor de esa tarjeta SIM.  
