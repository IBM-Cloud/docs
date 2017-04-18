---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-27" 

---

# Acceso de autorización con Touch ID
{: #before-you-begin}

Touch ID es una función de reconocimiento de huellas dactilares para dispositivos iOS. Puede utilizar Touch ID con el servicio the {{site.data.keyword.amafull}} para proteger automáticamente la información de autorización para su uso futuro. 

**Nota:** El ID de Touch solo está disponible desde el SDK de Objective-C de {{site.data.keyword.amashort}}.

Para configurar la fortaleza de la seguridad, establezca una de las siguientes políticas de persistencia con el método `IMFAuthorizationManager.setAuthorizationPersistencePolicy()`.

* **IMFAuthorizationPersistencePolicyNever** (más segura): nunca persiste la información de la autorización en el dispositivo. La cabecera de autorización es válida durante una única sesión de aplicación. La información de la autorización persiste en la cadena de claves de iOS.

* **IMFAuthorizationPersistencePolicyAlways** (menos segura): siempre persiste la información de la autorización en el dispositivo, independientemente de que Touch ID esté presente, se admita o esté habilitado. No se necesita ni Touch ID ni la autenticación con código de acceso de dispositivo.

* **IMFAuthorizationPersistencePolicyWithTouchBiometrics**: utilice Touch ID para captar la información de la autorización desde la cadena de claves de iOS. Esta opción equilibra la seguridad y la facilidad de uso. La información de la autorización persiste solo si Touch ID está presente, se admite y está habilitado. Se necesita Touch ID o la autenticación mediante código de acceso de dispositivo para acceder a la información de autorización persistente una vez en cada sesión de la aplicación. Una vez se haya configurado esta política y no haya acceso a Touch ID porque, por ejemplo, el hardware necesario no esté disponible o haya sido inhabilitado, la reserva será **IMFAuthorizationPersistancePolicyNever**.
