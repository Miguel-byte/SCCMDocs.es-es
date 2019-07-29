---
title: Solución de problemas de CMPivot
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo solucionar problemas de CMPivot en Configuration Manager.
ms.date: 04/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 36385bea-f05e-4300-947f-cb3927b3bac5
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: e1614327bbea6ecb92d37e1ca89d9ee430b74f2f
ms.sourcegitcommit: 79c51028f90b6966d6669588f25e8233cf06eb61
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/19/2019
ms.locfileid: "68338125"
---
# <a name="troubleshooting-cmpivot"></a>Solución de problemas de CMPivot

CMPivot es una utilidad en la consola que ahora proporciona acceso al estado en tiempo real de los dispositivos del entorno. Esta utilidad ejecuta una consulta inmediatamente en todos los dispositivos conectados actualmente en la colección de destino y devuelve los resultados. Es posible que en algún momento necesite solucionar problemas de CMPivot. Por ejemplo, podría ver que un cliente ha enviado un mensaje de estado a CMPivot, pero que el servidor de sitio no lo ha procesado porque estaba dañado. Este artículo le ayudará a comprender el flujo de información de CMPivot.

## <a name="get-information-from-the-site-server"></a>Obtención de información del servidor de sitio

De forma predeterminada, los archivos de registro del servidor de sitio se encuentran en C:\Archivos de programa\Microsoft Configuration Manager\logs. Esta ubicación podría cambiar en función de lo que haya especificado para el directorio de instalación o de si ha descargado elementos como el proveedor de SMS en otro servidor.

Consulte en **smsprov.log** esta línea:

```
Auditing: User <username> initiated client operation 135 to collection <CollectionId>.
```

Busque el identificador en la ventana de CMPivot. Este identificador es el **ClientOperationID**.

![Ventana de CMPivot con ClientOperationID resaltado](media/cmpivot-clientoperationid.png)

Busque el **TaskID** en la tabla ClientAction. El **TaskID** se corresponde con el **UniqueID** en la tabla ClientAction. 

```SQL
select * from ClientAction where ClientOperationId=<id>
```

En el archivo **BgbServer.log**, busque el **TaskID** que ha recopilado de SQL. En Bgbserver.log, estará etiquetado como **TaskGUID**. Por ejemplo: 


- Starting to send push task (PushID: 260 TaskID: 258 TaskGUID: **F8C7C37F-B42B-4C0A-B050-2BB44DF1098A** TaskType: 15 TaskParam:   PFNjcmlwdEhhc2ggU2NyaXB0SGFzaEFsZz0nU0hBMjU2Jz42YzZmNDY0OGYzZjU3M2MyNTQyNWZiNT   g2ZDVjYTIwNzRjNmViZmQ1NTg5MDZlMWI5NDRmYTEzNmFiMDE0ZGNjPC9TY3JpcHRIYXNoPjxTY3Jp   cHRQYXJhbWV0ZXJzPjxTY3JpcHRQYXJhbWV0ZXIgUGFyYW1ldGVyR3JvdXBHdWlkPSIiIFBhcmFtZX   Rlckdyb3VwTmFtZT0iUEdfIiBQYXJhbWV0ZXJOYW1lPSJzZWxlY3QiIFBhcmFtZXRlckRhdGFUeXBlP   SJTeXN0ZW0uU3RyaW5nIiBQYXJhbWV0ZXJWaXNpYmlsaXR5PSIwIiBQYXJhbWV0ZXJUeXBlPSIwIiBQ   YXJhbWV0ZXJWYWx1ZT0iRGV2aWNlI2tEZXZpY2UjY05hbWUja1N0cmluZyNjTWFudWZhY3R1cmVyI2tTd   HJpbmcjY1ZlcnNpb24ja1N0cmluZyNjUmVsZWFzZURhdGUja1N0cmluZyNjU2VyaWFsTnVtYmVyI2tTdH   JpbmcjY0J1aWxkTnVtYmVyI2tTdHJpbmcjY1NNQklPU0JJT1NWZXJzaW9uI2tTdHJpbmciLz48U2NyaXB0   UGFyYW1ldGVyIFBhcmFtZXRlckdyb3VwR3VpZD0iIiBQYXJhbWV0ZXJHcm91cE5hbWU9IlBHXyIgUGFyYW   1ldGVyTmFtZT0id21pcXVlcnkiIFBhcmFtZXRlckRhdGFUeXBlPSJTeXN0ZW0uU3RyaW5nIiBQYXJhbWV0ZX   JWaXNpYmlsaXR5PSIwIiBQYXJhbWV0ZXJUeXBlPSIwIiBQYXJhbWV0ZXJWYWx1ZT0iU0VMRUNUI3NOYW1lI2N   NYW51ZmFjdHVyZXIjY1ZlcnNpb24jY1JlbGVhc2VEYXRlI2NTZXJpYWxOdW1iZXIjY0J1aWxkTnVtYmVyI2   NTTUJJT1NCSU9TVmVyc2lvbiNzRlJPTSNzV2luMzJfQmlvcyIvPjwvU2NyaXB0UGFyYW1ldGVycz48UGFyYW   1ldGVyR3JvdXBIYXNoIFBhcmFtZXRlckhhc2hBbGc9J1NIQTI1NicOTE5NmEwNzNlOTljY2U4MzEyMWE3ZmFi   ODE5N2M4M2QxMjhjNDRmNTdlMWI0NGU1NWQwNmU4YTA5NGI5ZGRkNTwvUGFyYW1ldGVyR3JvdXBIYXNoPjwvU   2NyaXB0Q29udGVudD4=-) para cinco clientes con limitación (estrategia: 1 param: 42) Se ha finalizado el envío de la tarea de inserción (id. de inserción: 260 TaskID: 258) to 5 clients

## <a name="client-logs"></a>Registros de cliente

Una vez que haya reunido la información del servidor de sitio, compruebe los registros de cliente. De forma predeterminada, los registros de cliente se encuentran en C:\Windows\CCM\Logs.

Consulte **CCMNotificationAgent.log**. Encontrará registros similares a la entrada siguiente:  

- **Error! No se ha definido ningún marcador.** +PFNjcmlwdEhhc2ggU2NyaXB0SGFzaEFsZz0nU0hBMjU2Jz42YzZmNDY0OGYzZjU3M2MyNTQyNWZiNT   g2ZDVjYTIwNzRjNmViZmQ1NTg5MDZlMWI5NDRmYTEzNmFiMDE0ZGNjPC9TY3JpcHRIYXNoPjxTY3Jp   cHRQYXJhbWV0ZXJzPjxTY3JpcHRQYXJhbWV0ZXIgUGFyYW1ldGVyR3JvdXBHdWlkPSIiIFBhcmFtZX   Rlckdyb3VwTmFtZT0iUEdfIiBQYXJhbWV0ZXJOYW1lPSJzZWxlY3QiIFBhcmFtZXRlckRhdGFUeXBlP   SJTeXN0ZW0uU3RyaW5nIiBQYXJhbWV0ZXJWaXNpYmlsaXR5PSIwIiBQYXJhbWV0ZXJUeXBlPSIwIiBQ   YXJhbWV0ZXJWYWx1ZT0iRGV2aWNlI2tEZXZpY2UjY05hbWUja1N0cmluZyNjTWFudWZhY3R1cmVyI2tTd   HJpbmcjY1ZlcnNpb24ja1N0cmluZyNjUmVsZWFzZURhdGUja1N0cmluZyNjU2VyaWFsTnVtYmVyI2tTdH   JpbmcjY0J1aWxkTnVtYmVyI2tTdHJpbmcjY1NNQklPU0JJT1NWZXJzaW9uI2tTdHJpbmciLz48U2NyaXB0   UGFyYW1ldGVyIFBhcmFtZXRlckdyb3VwR3VpZD0iIiBQYXJhbWV0ZXJHcm91cE5hbWU9IlBHXyIgUGFyYW   1ldGVyTmFtZT0id21pcXVlcnkiIFBhcmFtZXRlckRhdGFUeXBlPSJTeXN0ZW0uU3RyaW5nIiBQYXJhbWV0ZX   JWaXNpYmlsaXR5PSIwIiBQYXJhbWV0ZXJUeXBlPSIwIiBQYXJhbWV0ZXJWYWx1ZT0iU0VMRUNUI3NOYW1lI2N   NYW51ZmFjdHVyZXIjY1ZlcnNpb24jY1JlbGVhc2VEYXRlI2NTZXJpYWxOdW1iZXIjY0J1aWxkTnVtYmVyI2   NTTUJJT1NCSU9TVmVyc2lvbiNzRlJPTSNzV2luMzJfQmlvcyIvPjwvU2NyaXB0UGFyYW1ldGVycz48UGFyYW   1ldGVyR3JvdXBIYXNoIFBhcmFtZXRlckhhc2hBbGc9J1NIQTI1NicOTE5NmEwNzNlOTljY2U4MzEyMWE3ZmFi   ODE5N2M4M2QxMjhjNDRmNTdlMWI0NGU1NWQwNmU4YTA5NGI5ZGRkNTwvUGFyYW1ldGVyR3JvdXBIYXNoPjwvU   2NyaXB0Q29udGVudD4=-

Consulte en **Scripts.log** el **TaskID**. En el ejemplo siguiente, vemos **Task ID {F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}** :

```
Sending script state message: 7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14 Scripts 7/3/2018 11:44:47 AM 5036 (0x13AC)
State message: Task Id {F8C7C37F-B42B-4C0A-B050-2BB44DF1098A} Scripts 7/3/2018 11:44:47 AM 5036 (0x13AC)
```

Consulte **StateMessage.log**. Nuestro **TaskID** de ejemplo se encuentra hacia el final del mensaje situado junto a &lt;Param>. Verá líneas parecidas a la siguiente:

```xml
StateMessage body: <?xml version="1.0" encoding="UTF-16"?>
<Report><ReportHeader><Identification><Machine><ClientInstalled>1</ClientInstalled><ClientType>1
</ClientType><ClientID>GUID:DBAC52C9-57E6-47D7-A8D6-E0A5A64B57E6</ClientID><ClientVersion>5.00.8670.1000</ClientVersion>
<NetBIOSName>R613924</NetBIOSName><CodePage>437</CodePage>
<SystemDefaultLCID>1033</SystemDefaultLCID><Priority>0</Priority></Machine></Identification>
<ReportDetails><ReportContent>State Message Data</ReportContent><ReportType>Full</ReportType>
<Date>20180703184447.673000+000</Date><Version>1.0</Version><Format>1.0</Format>
</ReportDetails></ReportHeader><ReportBody><StateMessage MessageTime="20180703184447.517000+000"><Topic ID="7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14" Type="9003" IDType="0" User="" UserSID=""/><State ID="1" Criticality="0"/>
<StateDetails Type="1"><![CDATA["PAA/AHgAbQBsACAAdgBlAHIAcwBpAG8AbgA9ACIAMQAuADAAIgAgAGUAbgBjAG8AZABpAG4AZwA9ACIAdQB0AGYALQAxADYAIgA/AD4APAByAGUAcwB1AGwAdAAgAFIAZQBzAHUAbAB0AEMAbwBkAGUAPQAiADAAIgA+ADwAZQAgAE4AYQBtAGUAPQAiAEkAbgB0AGUAbAAoAFIAKQAgAFgAZQBvAG4AKABSACkAIABDAFAAVQAgAEUANQAtADIANgA3ADMAIAB2ADQAIABAACAAMgAuADMAMABHAEgAegAiACAATQBhAG4AdQBmAGEAYwB0AHUAcgBlAHIAPQAiAEEAbQBlAHIAaQBjAGEAbgAgAE0AZQBnAGEAdAByAGUAbgBkAHMAIABJAG4AYwAuACIAIABWAGUAcgBzAGkAbwBuAD0AIgBWAFIAVABVAEEATAAgAC0AIAA2ADAAMAAxADcAMAAyACIAIABSAGUAbABlAGEAcwBlAEQAYQB0AGUAPQAiADIAMAAxADcALQAwADYALQAwADIAIAAwADAAOgAwADAAOgAwADAAIgAgAFMAZQByAGkAYQBsAE4AdQBtAGIAZQByAD0AIgAwADAAMAAwAC0AMAAwADEAOAAtADMANgA4ADIALQA0ADcAMAA4AC0ANwA2ADQAMAAtADcANgAwADAALQAzADMAIgAgAFMATQBCAEkATwBTAEIASQBPAFMAVgBlAHIAcwBpAG8AbgA9ACIAMAA5ADAAMAAwADcAIAAiACAALwA+ADwALwByAGUAcwB1AGwAdAA+AA=="~~]]></StateDetails><UserParameters Flags="0" Count="2">
<Param>{F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}</Param><Param>0</Param></UserParameters></StateMessage></ReportBody></Report>
StateMessage 7/3/2018 11:44:47 AM 5036 (0x13AC)
Successfully forwarded State Messages to the MP StateMessage 7/3/2018 11:44:47 AM 5036 (0x13AC)
```

> [!NOTE]
> La entrada del registro anterior en StateSys.log solo está visible cuando el registro detallado está habilitado para el componente SMS_STATE_SYSTEM, lo que puede realizarse mediante la modificación de esta clave del Registro: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\COMPONENTS\SMS_STATE_SYSTEM\Verbose logging = 1 (el valor predeterminado es 0)

## <a name="review-messages-on-the-site-server"></a>Revisión de los mensajes en el servidor de sitio

Abra **statesys.log** para ver si el mensaje se ha recibido y procesado. Nuestro **TaskID** de ejemplo se encuentra hacia el final del mensaje situado junto a &lt;Param>.

```xml
CMessageProcessor - the cmdline to DB exec dbo.spProcessStateReport N'?<?xml version="1.0" encoding="UTF-
16"?>~~<Report><ReportHeader><Identification><Machine><ClientInstalled>1</ClientInstalled><ClientType>1
</ClientType><ClientID>GUID:DBAC52C9-57E6-47D7-A8D6-E0A5A64B57E6</ClientID><ClientVersion>5.00.8670.1000</ClientVersion>
<NetBIOSName>R613924</NetBIOSName><CodePage>437</CodePage>
<SystemDefaultLCID>1033</SystemDefaultLCID><Priority>0</Priority></Machine></Identification>
<ReportDetails><ReportContent>State Message Data</ReportContent><ReportType>Full</ReportType>
<Date>20180703184447.673000+000</Date><Version>1.0</Version><Format>1.0</Format>
</ReportDetails></ReportHeader><ReportBody><StateMessage MessageTime="20180703184447.517000+000"><Topic ID="7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14" Type="9003" IDType="0" User="" UserSID=""/><State ID="1" Criticality="0"/>
<StateDetails Type="1"><![CDATA["PAA/AHgAbQBsACAAdgBlAHIAcwBpAG8AbgA9ACIAMQAuADAAIgAgAGUAbgBjAG8AZABpAG4AZwA9ACIAdQB0AGYALQAxADYAIgA/AD4APAByAGUAcwB1AGwAdAAgAFIAZQBzAHUAbAB0AEMAbwBkAGUAPQAiADAAIgA+ADwAZQAgAE4AYQBtAGUAPQAiAEkAbgB0AGUAbAAoAFIAKQAgAFgAZQBvAG4AKABSACkAIABDAFAAVQAgAEUANQAtADIANgA3ADMAIAB2ADQAIABAACAAMgAuADMAMABHAEgAegAiACAATQBhAG4AdQBmAGEAYwB0AHUAcgBlAHIAPQAiAEEAbQBlAHIAaQBjAGEAbgAgAE0AZQBnAGEAdAByAGUAbgBkAHMAIABJAG4AYwAuACIAIABWAGUAcgBzAGkAbwBuAD0AIgBWAFIAVABVAEEATAAgAC0AIAA2ADAAMAAxADcAMAAyACIAIABSAGUAbABlAGEAcwBlAEQAYQB0AGUAPQAiADIAMAAxADcALQAwADYALQAwADIAIAAwADAAOgAwADAAOgAwADAAIgAgAFMAZQByAGkAYQBsAE4AdQBtAGIAZQByAD0AIgAwADAAMAAwAC0AMAAwADEAOAAtADMANgA4ADIALQA0ADcAMAA4AC0ANwA2ADQAMAAtADcANgAwADAALQAzADMAIgAgAFMATQBCAEkATwBTAEIASQBPAFMAVgBlAHIAcwBpAG8AbgA9ACIAMAA5ADAAMAAwADcAIAAiACAALwA+ADwALwByAGUAcwB1AGwAdAA+AA=="~~]]></StateDetails><UserParameters Flags="0" Count="2">
<Param>{F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}</Param><Param>0</Param></UserParameters></StateMessage></ReportBody></Report>~~'
```

Compruebe la bandeja de entrada de mensajes de estado si ve que el mensaje no se ha procesado. La ubicación predeterminada de la bandeja de entrada es C:\Archivos de programa\Microsoft Configuration Manager\inboxes\auth\statesys.box\. Los archivos tendrán uno de los siguientes estados:
  
- Entrante
- Dañado
- Proceso

Compruebe la vista de supervisión para CMPivot desde SQL mediante el **TaskID**.

```SQL
select * from vSMS_CMPivotStatus where TaskID='{F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}'
```

## <a name="next-steps"></a>Pasos siguientes

[Uso de CMPivot](/sccm/core/servers/manage/cmpivot)

[Crear y ejecutar scripts de PowerShell](/sccm/apps/deploy-use/create-deploy-scripts)
