---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-27" 

---

# 通过 Touch 标识授予访问权
{: #before-you-begin}

Touch 标识是 iOS 设备的一种指纹识别功能。可以对 {{site.data.keyword.amafull}} 服务使用 Touch 标识来自动保护授权信息以供未来使用。 

**注：**只有通过 {{site.data.keyword.amashort}} Objective-C SDK，才能使用 Touch 标识。

要配置安全强度，请通过 `IMFAuthorizationManager.setAuthorizationPersistencePolicy()` 方法设置下列其中一个持久存储策略。

* **IMFAuthorizationPersistencePolicyNever**（最安全）：永不在设备上持久存储授权信息。Authorization 头在单个应用程序会话期间有效。授权信息在 iOS 密钥链中持久存储。

* **IMFAuthorizationPersistencePolicyAlways**（最不安全）：始终在设备上持久存储授权信息，不管 Touch 标识是否存在、是否受支持或是否已启用。从不需要 Touch 标识和设备数字密码认证。

* **IMFAuthorizationPersistencePolicyWithTouchBiometrics**：使用 Touch 标识从 iOS 密钥链中访存授权信息。此选项兼顾安全性和易用性。仅当 Touch 标识存在、受支持且已启用时，授权信息才会持久存储。需要 Touch 标识或设备数字密码认证才能访问持久存储的授权信息，并且每个应用程序会话只能访问一次。设置了此策略，但没有对 Touch 标识的访问权时（例如，由于必需的硬件不存在或已禁用），替代策略为 **IMFAuthorizationPersistancePolicyNever** 策略。
