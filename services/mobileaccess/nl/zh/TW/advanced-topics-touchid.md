---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-27" 

---

# 使用 Touch ID 授權存取
{: #before-you-begin}

Touch ID 是 iOS 裝置的指紋辨識特性。您可以使用 Touch ID 與 {{site.data.keyword.amafull}} 搭配，自動保護授權資訊的安全，以供未來使用。 

**附註：**Touch ID 只能從 {{site.data.keyword.amashort}} Objective-C SDK 取得。

若要配置安全強度，請使用 `IMFAuthorizationManager.setAuthorizationPersistencePolicy()` 方法來設定下列其中一個持續性原則。

* **IMFAuthorizationPersistencePolicyNever**（最安全）：永不在裝置上持續保存授權資訊。授權標頭在單一應用程式階段作業期間有效。授權資訊會持續保存在 iOS 金鑰鏈中。

* **IMFAuthorizationPersistencePolicyAlways**（最不安全）：一律在裝置上持續保存授權資訊（不論 Touch ID 是否存在、受支援或已啟用）。永不需要 Touch ID 和裝置密碼鑑別。

* **IMFAuthorizationPersistencePolicyWithTouchBiometrics**：使用 Touch ID，從 iOS 金鑰鏈提取授權資訊。此選項兼顧安全和容易使用的特點。只有在 Touch ID 存在、受支援或已啟用時，才會持續保存授權資訊。需要有 Touch ID 或裝置密碼鑑別，才能在每個應用程式階段作業內存取一次持續保存的授權資訊。如果已經設定此原則，但沒有 Touch ID 的存取權（例如，因為必要的硬體不存在或已遭停用），則替代原則為 **IMFAuthorizationPersistancePolicyNever** 原則。
