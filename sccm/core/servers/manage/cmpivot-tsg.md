---
title: Solución de problemas de CMPivot
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo solucionar problemas de CMPivot en Configuration Manager.
ms.date: 09/19/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 36385bea-f05e-4300-947f-cb3927b3bac5
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 09c748e563ea6410b7f2ebc842c77707cf29494a
ms.sourcegitcommit: 013596de802ac0eb416118169ad049733b5a63e5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/23/2019
ms.locfileid: "71198200"
---
# <a name="troubleshooting-cmpivot"></a>Solución de problemas de CMPivot

CMPivot es una utilidad que proporciona acceso al estado en tiempo real de los dispositivos de su entorno. Esta utilidad ejecuta una consulta inmediatamente en todos los dispositivos conectados actualmente en la colección de destino y devuelve los resultados. Es posible que en algún momento necesite solucionar problemas de CMPivot. Por ejemplo, podría ver que un cliente ha enviado un mensaje de estado a CMPivot, pero que el servidor de sitio no lo ha procesado porque estaba dañado. Este artículo le ayudará a comprender el flujo de información de CMPivot.

## <a name="bkmk_CMPivot-1902"></a> Solución de problemas de CMPivot en la versión 1902 y posteriores

A partir de Configuration Manager versión 1902, puede ejecutar CMPivot desde el sitio de administración central (CAS) en una jerarquía. El sitio primario sigue controlando la comunicación con el cliente. Al ejecutar CMPivot desde el sitio de administración central, se comunica con el sitio primario a través del canal de suscripción de mensajes de alta velocidad. Esta comunicación no depende de la replicación SQL estándar entre sitios. Si la instancia de SQL Server o el proveedor son remotos, o si usa SQL Always On, tendrá un "escenario de salto doble" para CMPivot. Para obtener información sobre cómo definir la delegación restringida para un "escenario de salto doble", consulte [CMPivot a partir de la versión 1902](/sccm/core/servers/manage/cmpivot#bkmk_cmpivot1902).

>[!IMPORTANT]
> Para solucionar problemas de CMPivot, habilite el registro detallado en los módulos de administración y en el componente SMS_MESSAGE_PROCESSING_ENGINE del servidor de sitio para más información. Si el resultado del cliente es superior a 80 KB, habilite el registro detallado en el módulo de administración y el componente SMS_STATE_SYSTEM del servidor de sitio. Para más información acerca de cómo habilitar el registro detallado, consulte las [opciones de registro de servidor de sitio](/sccm/core/plan-design/hierarchy/about-log-files#bkmk_reg-site).

### <a name="get-information-from-the-site-server"></a>Obtención de información del servidor de sitio

De forma predeterminada, los archivos de registro del servidor de sitio se encuentran en C:\Archivos de programa\Microsoft Configuration Manager\logs. Esta ubicación podría cambiar en función de lo que haya especificado para el directorio de instalación o de si ha descargado elementos como el proveedor de SMS en otro servidor. Si está ejecutando, CMPivot desde un CAS, los registros estarán en el servidor del sitio principal.

Consulte el archivo **smsprov.log** para estas líneas:

- Configuration Manager, versión 1906:
  <pre><code lang="Log">Auditing: User &ltusername> initiated client operation 145 to collection &ltCollectionId>. </code></pre>

- Configuration Manager, versión 1902:
  <pre><code lang="Log">Type parameter is 135.
  Auditing: User &ltusername> ran script 7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14 with hash dc6c2ad05f1bfda88d880c54121c8b5cea6a394282425a88dd4d8714547dc4a2 on collection &ltCollectionId>. </code></pre>



**7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14** es el GUID de script para CMPivot. También puede ver este GUID en los [mensajes de estado de auditoría de CMPivot](/sccm/core/servers/manage/cmpivot#cmpivot-audit-status-messages).

A continuación, busque el identificador en la ventana de CMPivot. Este identificador es el **ClientOperationID**.

![Ventana de CMPivot con ClientOperationID resaltado](media/cmpivot-client-operationid-1902.png)

Busque el **TaskID** en la tabla ClientAction. El **TaskID** se corresponde con el **UniqueID** en la tabla ClientAction.

``` SQL
select * from ClientAction where ClientOperationId=<id>
```

En el archivo **BgbServer.log**, busque la propiedad **TaskID** que ha recopilado de SQL y anote el valor de **PushID**. En el archivo Bgbserver.log, la propiedad **TaskID** estará etiquetada como **TaskGUID**. Por ejemplo:

<pre><code lang="Log">Starting to send push task (<b>PushID: 9</b> TaskID: 12 <b>TaskGUID: 9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0</b> TaskType: 15 TaskParam: PFNjcmlwdENvbnRlbnQgU2NyaXB0R3VpZD0nN0RDNkI2RjEtRTdGNi00M0MxL (truncated log entry)
Finished sending push task (<b>PushID: 9</b> TaskID: 12) to 2 clients
</code></pre>

### <a name="client-logs"></a>Registros de cliente

Una vez que haya reunido la información del servidor de sitio, compruebe los registros de cliente. De forma predeterminada, los registros de cliente se encuentran en C:\Windows\CCM\Logs.

Consulte **CCMNotificationAgent.log**. Encontrará registros similares a las líneas siguientes:  

<pre><code lang="Log">Receive task from server with <b>pushid=9</b>, taskid=12, <b>taskguid=9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0</b>, tasktype=15 and taskParam=PFNjcmlwdEhhc2ggU2NyaXB0SGF (truncated log entry)
Send Task response message &ltBgbResponseMessage TimeStamp="2019-09-13T17:29:09Z"><b>&ltPushID>5</b>&lt/PushID>&ltTaskID>4&lt/TaskID>&ltReturnCode>1&lt/ReturnCode>&lt/BgbResponseMessage> successfuly.
 </code></pre>

Consulte en **Scripts.log** el **TaskID**. En el ejemplo siguiente, vemos el **identificador de tarea {9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0}** :

<pre><code lang="Log">Sending script state message (fast): <b>{9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0}</b>
Result are sent for ScriptGuid: 7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14 and <b>TaskID: {9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0}</b>
</code></pre>

> [!NOTE]
> Si no ve "(fast)" en el archivo **scripts.log**, es probable que los datos superen los 80 KB. En este caso, la información se envía al servidor de sitio como un mensaje de estado. Utilice el archivo **StateMessage.log** del cliente y el archivo **Statesys.log** del servidor de sitio.

### <a name="review-messages-on-the-site-server"></a>Revisión de los mensajes en el servidor de sitio

Cuando el [registro detallado](/sccm/core/plan-design/hierarchy/about-log-files#bkmk_reg-client) está habilitado en el punto de administración, puede ver cómo se administran los mensajes de cliente entrantes. En el archivo **MP_RelayMsgMgr.log**, busque la propiedad **TaskID**.

En el ejemplo **MP_RelayMsgMgr.log**, vemos el identificador del cliente (GUID:83F67728-2E6D-4E4F-8075-ED035C31B783) y el **identificador de tarea {9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0}** . Un identificador de mensaje se asigna a la respuesta del cliente antes de enviarse al motor de procesamiento de mensajes:

<pre><code lang="Log">MessageKey: GUID:83F67728-2E6D-4E4F-8075-ED035C31B783<b>{9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0}</b>
Create message succeeded for <b>message id 22f00adf-181e-4bad-b35e-d18912f39f89</b>
Add message payload succeeded for message id 22f00adf-181e-4bad-b35e-d18912f39f89
Put message succeeded for message id 22f00adf-181e-4bad-b35e-d18912f39f89
CRelayMsgMgrHandler::HandleMessage(): ExecuteTask() succeeded
</code></pre>

Cuando el [registro detallado](/sccm/core/plan-design/hierarchy/about-log-files#bkmk_logoptions) está habilitado en **SMS_MESSAGE_PROCESSING_ENGINE.log**, verá que se procesan los resultados del cliente. Use el identificador del mensaje que encontró en **MP_RelayMsgMgr.log**. Las entradas del registro de procesamiento similares a las siguientes entradas de ejemplo:

<pre><code lang="Log">Processing 2 messages with type Instant and IDs <b>22f00adf-181e-4bad-b35e-d18912f39f89[19]</b>, 434d80ae-09d4-4d84-aebf-28a4a29a9852[20]...
Processed 2 messages with type Instant. Failed to process 0 messages. All message IDs <b>22f00adf-181e-4bad-b35e-d18912f39f89[19]</b>, 434d80ae-09d4-4d84-aebf-28a4a29a9852[20]
</code></pre>

  - Si obtiene una excepción durante el procesamiento, puede revisarla con la ejecución de la siguiente consulta SQL y el examen de la columna de excepciones. Una vez procesado el mensaje, ya no estará en la tabla MPE_RequestMessages_Instant.

    ```SQL
    select * from MPE_RequestMessages_Instant where MessageID=<ID from SMS_MESSAGE_PROCESSING_ENGINE.log>
    ```

En **BgbServer.log**, busque el valor de **PushID** para ver el número de clientes que se han comunicado o que tienen errores.

<pre><code lang="Log">Generated BGB task status report c:\ConfigMgr\inboxes\bgb.box\Bgb5c1db.BTS at 09/16/2019 16:46:39. (<b>PushID: 9</b> ReportedClients: 2 FailedClients: 0)
</code></pre>

Compruebe la vista de supervisión para CMPivot desde SQL mediante el **TaskID**.

``` SQL
select * from vSMS_CMPivotStatus where TaskID='{9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0}'
```

![Consultas SQL de CMPivot para solucionar problemas en la versión 1902](media/cmpivot-sql-queries-1902.png)

## <a name="bkmk_CMPivot-1810"></a> Solución de problemas de CMPivot en la versión 1810 y versiones anteriores

### <a name="get-information-from-the-site-server"></a>Obtención de información del servidor de sitio

De forma predeterminada, los archivos de registro del servidor de sitio se encuentran en C:\Archivos de programa\Microsoft Configuration Manager\logs. Esta ubicación podría cambiar en función de lo que haya especificado para el directorio de instalación o de si ha descargado elementos como el proveedor de SMS en otro servidor.

Consulte en **smsprov.log** esta línea:

<pre><code lang="Log">Auditing: User <username> initiated client operation 135 to collection &ltCollectionId>.
</code></pre>

Busque el identificador en la ventana de CMPivot. Este identificador es el **ClientOperationID**.

![Ventana de CMPivot con ClientOperationID resaltado](media/cmpivot-clientoperationid.png)

Busque el **TaskID** en la tabla ClientAction. El **TaskID** se corresponde con el **UniqueID** en la tabla ClientAction. 

``` SQL
select * from ClientAction where ClientOperationId=<id>
```

En el archivo **BgbServer.log**, busque el **TaskID** que ha recopilado de SQL. En Bgbserver.log, estará etiquetado como **TaskGUID**. Por ejemplo:

<pre><code lang="Log">Starting to send push task (PushID: 260 TaskID: 258 TaskGUID: <b>F8C7C37F-B42B-4C0A-B050-2BB44DF1098A</b> TaskType: 15
TaskParam: PFNjcmlwdEhhc2ggU2NyaXB0SGF...truncated...to 5 clients with throttling (strategy: 1 param: 42)
Finished sending push task (PushID: 260 TaskID: 258) to 5 clients
</code></pre>

### <a name="client-logs"></a>Registros de cliente

Una vez que haya reunido la información del servidor de sitio, compruebe los registros de cliente. De forma predeterminada, los registros de cliente se encuentran en C:\Windows\CCM\Logs.

Consulte **CCMNotificationAgent.log**. Encontrará registros similares a la entrada siguiente:  

<pre><code lang="Log"><b>Error! Bookmark not defined.</b>+PFNjcmlwdEhhc2ggU2NyaXB0SGFzaEFsZz0nU0hBMjU2Jz42YzZmNDY0OGYzZjU3M2MyNTQyNWZiNT
g2ZDVjYTIwNzRjNmViZmQ1NTg5MDZlMWI5NDRmYTEzNmFiMDE0ZGNjPC9TY3JpcHRIYXNoPjxTY3Jp (truncated log entry)
</code></pre>

Consulte en **Scripts.log** el **TaskID**. En el ejemplo siguiente, vemos **Task ID {F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}** :

<pre><code lang="Log">Sending script state message: 7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14
State message: Task Id <b>{F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}</b>
</code></pre>

Consulte **StateMessage.log**. Nuestro **TaskID** de ejemplo se encuentra hacia el final del mensaje situado junto a \<Param>. Verá líneas parecidas a la siguiente:

``` XML
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

Successfully forwarded State Messages to the MP StateMessage 7/3/2018 11:44:47 AM 5036 (0x13AC)
```

### <a name="review-messages-on-the-site-server"></a>Revisión de los mensajes en el servidor de sitio

Abra **statesys.log** para ver si el mensaje se ha recibido y procesado. Nuestro **TaskID** de ejemplo se encuentra hacia el final del mensaje situado junto a \<Param>. Debe habilitar el [registro detallado](/sccm/core/plan-design/hierarchy/about-log-files#bkmk_logoptions) en el componente SMS_STATE_SYSTEM para ver estas entradas de registro.  

``` XML
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

``` SQL
select * from vSMS_CMPivotStatus where TaskID='{F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}'
```

>[!NOTE]
>En el caso de los clientes que usan la versión 1810 o posterior, no se utiliza la mensajería de estado a menos que la salida sea superior a 80 KB. A la hora de solucionar problemas de CMPivot en estos casos, habilite el registro detallado en los módulos de detección y la SMS_MESSAGE_PROCESSING_ENGINE del servidor de sitio para más información. Para más información acerca de cómo habilitar el registro detallado, consulte las [opciones de registro de servidor de sitio](/sccm/core/plan-design/hierarchy/about-log-files#bkmk_reg-site).
> 
> Use los siguientes registros para solucionar problemas:
> - MP_Relay.log
> - SMS_MESSAGE_PROCESSING_ENGINE.log

## <a name="next-steps"></a>Pasos siguientes

[Uso de CMPivot](/sccm/core/servers/manage/cmpivot)

[Crear y ejecutar scripts de PowerShell](/sccm/apps/deploy-use/create-deploy-scripts)
