---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-27" 

---

# Touch ID によるアクセスの許可
{: #before-you-begin}

Touch ID は、iOS デバイス向けの指紋認証機能です。{{site.data.keyword.amafull}} で Touch ID を使用することで、将来の使用のために許可情報を自動的に保護できます。 

**注:** Touch ID は、{{site.data.keyword.amashort}} Objective-C SDK からのみ使用可能です。

セキュリティー強度を構成するため、`IMFAuthorizationManager.setAuthorizationPersistencePolicy()` メソッドを使用して以下のいずれかのパーシスタンス・ポリシーを設定します。

* **IMFAuthorizationPersistencePolicyNever** (最高のセキュリティー強度): 許可情報をデバイスに保持することは決してありません。許可ヘッダーは単一アプリケーション・セッション中のみ有効です。許可情報は iOS keychain 内で保持されます。

* **IMFAuthorizationPersistencePolicyAlways** (最低のセキュリティー強度): Touch ID があるか、サポートされているか、有効になっているかに関わらず、許可情報は常にデバイスに保持されます。Touch ID およびデバイスのパスコード認証が必要とされることはありません。

* **IMFAuthorizationPersistencePolicyWithTouchBiometrics**: Touch ID を使用して、iOS keychain から許可情報を取り出します。このオプションはセキュリティーと使用しやすさのバランスを取ったオプションです。Touch ID があり、サポートされていて、有効になっている場合にのみ、許可情報が保持されます。保持された許可情報にアクセスするには、アプリケーション・セッションごとに 1 回ずつ、Touch ID またはデバイス・パスコード認証が必要です。このポリシーが設定されていても、必要なハードウェアがない、または使用不可になっているなどの理由で Touch ID にアクセスできない場合は、**IMFAuthorizationPersistancePolicyNever** ポリシーにフォールバックします。
