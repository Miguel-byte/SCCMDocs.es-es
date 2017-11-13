---
title: "Creación de perfiles de certificado SCEP"
titleSuffix: Configuration Manager
description: "Obtenga información sobre cómo usar perfiles de certificado para aprovisionar dispositivos administrados con los certificados que necesitan en System Center Configuration Manager."
ms.custom: na
ms.date: 03/28/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 634d612c-92d7-4c03-873a-b2e730c9a72d
caps.latest.revision: "16"
caps.handback.revision: "0"
author: Nbigman
ms.author: nbigman
manager: angrobe
ms.openlocfilehash: 827565bd4dac074e8599075b19c9dac678a21948
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/12/2017
---
# <a name="create-certificate-profiles"></a>Crear perfiles de certificado

*Se aplica a: System Center Configuration Manager (rama actual)*


Use perfiles de certificado en Configuration Manager (SCCM) para aprovisionar dispositivos administrados con los certificados que necesitan para obtener acceso a los recursos de empresa. Antes de crear perfiles de certificado, configure la infraestructura de certificados como se describe en [Set up certificate infrastructure for System Center Configuration Manager](certificate-infrastructure.md) (Configurar la infraestructura de certificados para System Center Configuration Manager).  

En este tema, se describe cómo crear perfiles de certificado raíz de confianza y SCEP. Si quiere crear perfiles de certificado PFX, consulte [Create PFX certificate profiles](../../protect/deploy-use/create-pfx-certificate-profiles.md) (Crear perfiles de certificado PFX).

Para crear un perfil de certificado, siga estos pasos:

1.  Inicie el Asistente para crear perfil de certificado.
1.  Proporcione información general sobre el certificado.
1.  Configure un certificado de entidad de certificación (CA) de confianza.  
1.  Configure la información de los certificados SCEP (solo para certificados SCEP).  
1.  Especifique las plataformas admitidas del perfil de certificado.


## <a name="start-the-create-certificate-profile-wizard"></a>Inicio del Asistente para crear perfil de certificado  

1.  En la consola de System Center Configuration Manager, haga clic en **Activos y compatibilidad**.  

2.  En el área de trabajo **Activos y compatibilidad** , expanda **Configuración de cumplimiento**, expanda **Acceso a los recursos de la compañía**y, a continuación, haga clic en **Perfiles de certificado**.  

3.  En la pestaña **Inicio** del grupo **Crear** , haga clic en **Crear perfil de certificado**.  

## <a name="provide-general-information-about-the-certificate-profile"></a>Proporcionar información general sobre el perfil de certificado  

En la página **General** del Asistente para crear perfil de certificado, especifique la información siguiente:  

-   **Nombre**: escriba un nombre único para el perfil de certificado. Puede utilizar un máximo de 256 caracteres.  

-   **Descripción**: facilite una descripción general del perfil de certificado y cualquier otra información adicional pertinente para identificarlo en la consola de System Center Configuration Manager. Puede utilizar un máximo de 256 caracteres.  

-   **Especifique el tipo de perfil de certificado que desea crear**: elija uno de los tipos de perfil de certificado que se indican a continuación.  

-   **Certificado de CA de confianza**: seleccione este tipo de perfil de certificado si desea implementar un certificado de entidad de certificación raíz (CA) de confianza o uno intermedio para formar una cadena de certificados de confianza en los casos en los que el usuario o el dispositivo deban autenticar otro dispositivo. Por ejemplo, el dispositivo puede ser un servidor de Servicio de autenticación remota telefónica de usuario (RADIUS) o un servidor de red privada virtual (VPN). También debe configurar un perfil de certificado de CA de confianza antes de crear un perfil de certificado de SCEP. En este caso, el certificado de CA de confianza debe ser el certificado raíz de confianza de la CA que emitirá el certificado para el usuario o el dispositivo.  

-   **Configuración de Protocolo de inscripción de certificados simple (SCEP)**: seleccione este tipo de perfil de certificado si desea solicitar un certificado para un dispositivo o usuario mediante el Protocolo de inscripción de certificados simple y el servicio de rol Servicio de inscripción de dispositivos de red.

-   **Intercambio de información personal: configuración de PKCS #12 (PFX): importar**: seleccione esta opción para importar un certificado PFX. Para obtener más información sobre la creación de certificados PFX, consulte el artículo sobre cómo [importar perfiles de certificado PFX](/sccm/mdm/deploy-use/import-pfx-certificate-profiles.md).

-   **Intercambio de información personal -- Configuración de PKCS #12 (PFX) -- Crear**: seleccione esta opción para procesar certificados PFX con una entidad de certificación. Para obtener más información sobre la creación de certificados PFX, consulte [Create PFX certificate profiles](/sccm/mdm/deploy-use/create-pfx-certificate-profiles.md) (Crear perfiles de certificado PFX).


## <a name="configure-a-trusted-ca-certificate"></a>Configurar un certificado de CA de confianza  

> [!IMPORTANT]  
>  También debe configurar al menos un perfil de certificado de CA de confianza antes de crear un perfil de certificado de SCEP.    
>  
>  Si cambia cualquiera de estos valores después de implementar el certificado, se solicita un nuevo certificado:
>  -  Proveedor de almacenamiento de claves
>  -  Nombre de plantilla de certificado
>  -  Tipo de certificado
>  -  Formato de nombre del sujeto
>  -  Nombre alternativo del firmante
>  -  Período de validez del certificado
>  -  Uso de claves
>  -  Tamaño de la clave
>  -  Uso mejorado de clave
>  -  Certificado de CA raíz

1.  En la página **Certificado de CA de confianza** del Asistente para crear perfil de certificado, especifique la información siguiente:  

 -   **Archivo de certificado**: haga clic en **Importar** y luego busque el archivo de certificado que quiera usar.  

 -   **Almacén de destino**: para los dispositivos que tienen más de un almacén de certificados, seleccione dónde quiere almacenar el certificado. Para los dispositivos que solo tienen un almacén, este valor se omite.  

2.  Utilice el valor de **Huella digital de certificado** para comprobar que importó el certificado correcto.  


## <a name="configure-scep-certificate-information-only-for-scep-certificates"></a>Configurar la información de certificado SCEP (solo para certificados SCEP)  

1.  En la página **SCEP Servers** del Asistente para crear perfil de certificado, especifique las direcciones URL para los servidores de NDES que emitirán certificados a través de SCEP. Puede elegir asignar automáticamente una dirección URL de NDES según la configuración del servidor del sistema de sitios del punto de registro de certificados, o bien agregar direcciones URL manualmente.  

2.  Complete la página **Inscripción de SCEP** del Asistente para crear perfil de certificado.

 -  **Reintentos**: especifique el número de veces que el dispositivo intenta enviar automáticamente la solicitud de certificado al servidor que ejecuta el Servicio de inscripción de dispositivos de red. Esta configuración es compatible con el escenario en el que un administrador de CA debe aprobar una solicitud de certificado para que sea aceptada. Esta opción se utiliza normalmente en entornos de alta seguridad o si tiene una CA emisora independiente en vez de una CA empresarial. También puede utilizar este valor para realizar pruebas, de forma que pueda examinar las opciones de la solicitud de certificado antes de que la CA emisora procese la solicitud de certificado. Utilice esta opción con el valor **Intervalo entre reintentos (minutos)** .  

 -   **Intervalo entre reintentos (minutos)**: especifique el intervalo en minutos entre cada intento de inscripción cuando se usa la aprobación del administrador de CA antes de que la CA emisora procese la solicitud de certificado. Si utiliza la aprobación del administrador para realizar pruebas, es probable que desee especificar un valor bajo para no tener que esperar mucho tiempo a que el dispositivo reintente la solicitud de certificado después de aprobarla. Sin embargo, si utiliza la aprobación del administrador en una red de producción, es probable que desee especificar un valor mayor para otorgar al administrador de CA tiempo suficiente para comprobar y aprobar o denegar aprobaciones pendientes.  

 -   **Umbral de renovación (%)**: especifique qué porcentaje de la duración del certificado tiene que quedar para que el dispositivo solicite la renovación del certificado.  

 -   **Proveedor de almacenamiento de claves (KSP)**: especifique donde se almacenará la clave del certificado. Elija uno de los siguientes valores:  

   -   **Instalar en Módulo de plataforma segura (TPM) si está presente**: instala la clave en el TPM. Si el TPM no está presente, la clave se instalará en el proveedor de almacenamiento de la clave de software.  

   -   **Instalar en Módulo de plataforma segura (TPM); de lo contrario, generar error**: instala la clave en el TPM. Si el módulo TPM no está presente, se producirá un error en la instalación.  

   -   **Instalar en Windows Hello para empresas; de lo contrario, generar error**: esta opción está disponible para dispositivos Windows 10 Desktop y Windows 10 Mobile. Inscribe la clave en **Windows Hello para empresas**, que se describe en [Windows Hello for Business settings in System Center Configuration Manager](../../protect/deploy-use/windows-hello-for-business-settings.md) (Configuración de Windows Hello para empresas en System Center Configuration Manager). Esta opción también le permite **Requerir autenticación multifactor** durante la inscripción de dispositivos antes de emitir certificados a esos dispositivos. Vea [Proteger dispositivos Windows con la autenticación multifactor](https://technet.microsoft.com/library/dn889751.aspx) para obtener más información.

   > [!NOTE]  
   > 
   > Cuando un usuario crea un PIN de Windows Hello para empresas, Windows envía una notificación que escucha Configuration Manager. De este modo, Configuration Manager puede conocer rápidamente qué usuarios han creado un PIN de Windows Hello. Configuration Manager puede entonces emitir nuevos certificados a esos usuarios si Windows Hello se usa como proveedor de almacenamiento de claves en un perfil de certificado.  

   -   **Instalar en el proveedor de almacenamiento de claves de software**: instala la clave en el proveedor de almacenamiento de la clave de software.  

 -   **Dispositivos para la inscripción de certificados**: si el perfil de certificado se implementa en una recopilación de usuario, seleccione si quiere permitir la inscripción de certificados solo en el dispositivo primario del usuario o en todos los dispositivos en los que el usuario inicia sesión. Si el perfil de certificado se implementa en una recopilación de dispositivos, elija si desea permitir la inscripción de certificado solo al usuario primario del dispositivo o a todos los usuarios que inicien sesión en el dispositivo.  

3.  En la página **Propiedades de certificado** del Asistente para crear perfil de certificado, especifique la información siguiente:  

 -   **Nombre de plantilla de certificado**: haga clic en **Examinar** para seleccionar el nombre de una plantilla de certificado cuya utilización está configurada en el Servicio de inscripción de dispositivos de red y que se haya agregado a una CA emisora. Para examinar correctamente las plantillas de certificado, la cuenta de usuario usada para ejecutar la consola de System Center Configuration Manager debe tener permisos de lectura en la plantilla de certificado. Como alternativa, si no puede usar **Examinar**, escriba el nombre de la plantilla de certificado.  

 > [!IMPORTANT]
 >   
 >  Si el nombre de la plantilla de certificado contiene caracteres no ASCII (por ejemplo, los caracteres del alfabeto chino), el certificado no se implementará. Para asegurarse de que el certificado se implementa, cree primero una copia de la plantilla de certificado en la CA y cambie el nombre de la copia mediante el uso de caracteres ASCII.  

   Tenga en cuenta las observaciones siguientes, en función de si busca la plantilla de certificado o escribe el nombre del certificado:  

 -   Si examina para seleccionar el nombre de la plantilla de certificado, algunos campos de la página se rellenan automáticamente mediante la información de la plantilla de certificado. En algunos casos, estos valores no se pueden cambiar a menos que elija otra plantilla de certificado.  

 -   Si escribe el nombre de la plantilla de certificado, asegúrese de que el nombre coincide exactamente con una de las plantillas de certificado que se muestran en el Registro del servidor que ejecuta el Servicio de inscripción de dispositivos de red. Asegúrese de que especifica el nombre de la plantilla de certificado y no el nombre para mostrar de la plantilla de certificado.  

   Para buscar los nombres de las plantillas de certificado, vaya a la siguiente clave: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Cryptography\MSCEP. Verá las plantillas de certificado como los valores de **EncryptionTemplate**, **GeneralPurposeTemplate**y **SignatureTemplate**. De forma predeterminada, el valor de las tres plantillas de certificado es **IPSECIntermediateOffline**, que se asigna al nombre de plantilla para mostrar **IPSEC (solicitud sin conexión)**.  

   > [!WARNING]  
   > 
   >  Debido a que System Center Configuration Manager no puede comprobar el contenido de la plantilla de certificado cuando escribe el nombre de la plantilla de certificado en lugar de examinar para buscarlo, es posible que pueda seleccionar opciones no compatibles con la plantilla de certificado y que producirán un error en la solicitud de certificado. Cuando esto sucede, verá un mensaje de error de w3wp.exe en el archivo CPR.log que indica que el nombre de la plantilla en la solicitud de firma de certificado (CSR) y el desafío no coinciden.  
   >   
   >  Cuando escriba el nombre de la plantilla de certificado especificado para el valor de **GeneralPurposeTemplate** , debe seleccionar las opciones **Cifrado de clave** y **Firma digital** para este perfil de certificado. No obstante, si desea habilitar solamente la opción **Cifrado de clave** en este perfil de certificado, especifique el nombre de la plantilla de certificado para la clave de **EncryptionTemplate** . De igual forma, si desea habilitar solamente la opción **Firma digital** en este perfil de certificado, especifique el nombre de la plantilla de certificado para la clave de **SignatureTemplate** .  

 -   **Tipo de certificado**: seleccione si el certificado se va a implementar en un dispositivo o en un usuario.  
 -   **Formato de nombre del sujeto**: en la lista, seleccione cómo crea System Center Configuration Manager de forma automática el nombre del sujeto en la solicitud de certificado. Si el certificado es para un usuario, también puede incluir la dirección de correo electrónico del usuario en el nombre del sujeto. 
    
   > [!NOTE]  
   > 
   > Seleccionar **Número IMEI** o **Número de serie** le permite diferenciar entre distintos dispositivos que pertenecen al mismo usuario. Por ejemplo, esos dispositivos pueden compartir un nombre común, pero no un número IMEI o número de serie. Si el dispositivo no notifica un número de serie o IMEI, el certificado se emitirá con el nombre común.

 -   **Nombre alternativo del firmante**: especifique cómo crea System Center Configuration Manager de forma automática los valores del nombre alternativo del firmante (SAN) en la solicitud de certificado. Por ejemplo, si seleccionó un tipo de certificado de usuario, puede incluir el nombre principal de usuario (UPN) en el nombre alternativo del sujeto.  Si el certificado de cliente se utilizará para autenticar un servidor de directivas de redes, debe establecer el nombre alternativo del sujeto en el UPN.  

   > [!NOTE]  
   >  - La compatibilidad de dispositivos iOS con formatos de nombre del sujeto y nombres alternativos del sujeto está limitada en los certificados de SCEP. Si especifica un formato que no es compatible, los certificados no se inscribirán en dispositivos iOS. Cuando configure un perfil de certificado de SCEP para que se implemente en dispositivos iOS, utilice el **nombre común** para el **formato de nombre de sujeto**y el **nombre DNS**, la **dirección de correo electrónico** o el **UPN** para el **nombre alternativo del sujeto**.  

 -   **Período de validez del certificado**: si ha ejecutado en la CA emisora el comando - setreg Policy\EditFlags +EDITF_ATTRIBUTEENDDATE, que permite un período de validez personalizado, puede especificar el tiempo restante hasta la expiración del certificado. Para obtener más información sobre este comando, consulte [Certificate infrastructure in System Center Configuration Manager](../../protect/deploy-use/certificate-infrastructure.md) (Infraestructura de certificados en System Center Configuration Manager).  

   Puede especificar un valor inferior al período de validez de la plantilla de certificado especificada, pero no superior. Por ejemplo, si el período de validez del certificado en la plantilla de certificado es de dos años, puede especificar un valor de un año, pero no un valor de cinco años. El valor también debe ser menor que el período de validez restante del certificado de la CA emisora.  

 -   **Uso de la clave**: especifique las opciones de uso de claves para el certificado. Puede elegir entre las siguientes opciones:  

        -   **Cifrado de clave**: permite el intercambio de claves solo si la clave está cifrada.  

        -   **Firma digital**: permite el intercambio de claves solo cuando una firma digital ayuda a proteger la clave.  

   Si se seleccionó una plantilla de certificado mediante **Examinar**, es posible que no pueda cambiar esta configuración a menos que seleccione otra plantilla de certificado.  

   La plantilla de certificado seleccionada debe configurarse con como mínimo una de las dos opciones de uso de clave anteriores. En caso contrario, se mostrará el mensaje **Key usage in CSR and challenge do not match (El uso de la clave en la CSR y en el desafío no coinciden)** en el archivo de registro del punto de registro de certificado ( **Crp.log**).  


   -   **Tamaño de la clave (bits)**: seleccione el tamaño de la clave, en bits.  

   -   **Uso de clave mejorado**: haga clic en **Seleccionar** para agregar valores para la finalidad prevista del certificado. En la mayoría de los casos, el certificado requerirá **Autenticación de cliente** para que el usuario o dispositivo pueda autenticarse en un servidor. Sin embargo, puede agregar otros usos de clave según sea necesario.  


   -   **Algoritmo hash**: seleccione uno de los tipos de algoritmos hash disponibles para usarlo con este certificado. Seleccione el nivel máximo de seguridad que admiten los dispositivos de conexión.  

   > [!NOTE]  
   > 
   >  **SHA-2** admite SHA-256, SHA-384 y SHA-512. **SHA-3** solo admite SHA-3.  

   -   **Certificado de CA raíz**: haga clic en **Seleccionar** para elegir un perfil de certificado de CA raíz que previamente ha configurado e implementado para el usuario o dispositivo. Este certificado de CA debe ser el certificado raíz para la entidad de certificación que emitirá el certificado que va a configurar en este perfil de certificado.  

   > [!IMPORTANT]  
   >  Si especifica un certificado de CA raíz que no se ha implementado en el usuario o dispositivo, System Center Configuration Manager no iniciará la solicitud de certificado que está configurando en este perfil de certificado.  


##  <a name="specify-supported-platforms-for-the-certificate-profile"></a>Especificar las plataformas admitidas del perfil de certificado  

1. En la página **Plataformas admitidas** del Asistente para crear perfil de certificado, seleccione los sistemas operativos en los que desea instalar el perfil de certificado. O bien, haga clic en **Seleccionar todo** para instalar el perfil de certificado en todos los sistemas operativos disponibles.
2. Revise la página **Resumen** del asistente y elija **Finalizar**. 
 
 
Se muestra el nuevo perfil de certificado en el nodo **Perfiles de certificado** del área de trabajo **Activos y compatibilidad** y está listo para su implementación en usuarios o dispositivos, tal y como se describe en [How to deploy profiles in System Center Configuration Manager](deploy-wifi-vpn-email-cert-profiles.md) (Cómo implementar perfiles en System Center Configuration Manager).  