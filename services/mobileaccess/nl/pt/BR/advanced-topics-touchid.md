---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-27" 

---

# Autorizando acesso com o Touch ID
{: #before-you-begin}

Touch ID é um recurso de reconhecimento de impressão digital para dispositivos iOS. É possível usar o Touch ID com o serviço {{site.data.keyword.amafull}} para proteger automaticamente informações de autorização para uso futuro. 

**Nota:** o ID de toque está disponível somente a partir do {{site.data.keyword.amashort}} Objective-C SDK.

Para configurar a intensidade de segurança, defina uma das políticas de persistência a seguir com o método `IMFAuthorizationManager.setAuthorizationPersistencePolicy()`:

* **IMFAuthorizationPersistencePolicyNever** (Mais seguro): nunca persistir informações de autorização no dispositivo. Um cabeçalho de autorização é válido durante uma única sessão de aplicativo. As informações de autorização são persistidas no keychain do iOS.

* **IMFAuthorizationPersistencePolicyAlways** (Menos seguro): sempre persistir informações de autorização no dispositivo, independentemente de o Touch ID estar presente, ser suportado ou estar ativado. O Touch ID e a autenticação da senha do dispositivo
nunca são necessários.

* **IMFAuthorizationPersistencePolicyWithTouchBiometrics**: Use Touch ID para buscar as informações de autorização do keychain do iOS. Essa opção equilibra segurança e facilidade de uso. As informações de autorização persistirão somente se o Touch ID estiver presente, ser suportado e estar ativado. Touch ID ou autenticação de senha do dispositivo é necessária para acessar as informações de autorização persistidas uma vez por sessão de aplicativo. Quando essa política tiver sido configurada, mas não houver acesso ao Touch ID, por exemplo, porque o hardware necessário não está presente ou foi desativado, o fallback será a política **IMFAuthorizationPersistancePolicyNever**.
