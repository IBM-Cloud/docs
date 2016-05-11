---

copyright:
  years: 2015, 2016
  
---

# Touch ID로 권한 보안 설정
{: #before-you-begin}

Touch ID는 iOS 디바이스의 지문 인식 기능입니다. Touch ID를 사용하여 이후 사용을 위해 권한 정보를
자동으로 보안 설정할 수 있습니다. 보안 강도를 구성하려면 `IMFAuthorizationManager.setAuthorizationPersistencePolicy()`
메소드를 사용하여 다음 지속성 정책 중 하나를 설정하십시오. 

* **IMFAuthorizationPersistencePolicyNever**(가장 안전): 권한 정보를 디바이스에
보존하지 않습니다. 권한 헤더는 단일 애플리케이션 세션 동안 유효합니다. 권한 정보는 iOS 키체인에 보존됩니다. 

* **IMFAuthorizationPersistencePolicyAlways**(가장 취약): Touch ID가 있거나,
지원되거나 사용하도록 설정되었는지와 상관없이 권한 정보를 항상 디바이스에 보존합니다. Touch ID 및 디바이스 패스코드 인증이
필요하지 않습니다. 

* **IMFAuthorizationPersistencePolicyWithTouchBiometrics**: Touch ID를 사용하여
iOS 키체인에서 권한 정보를 페치합니다. 이 옵션은 보안과 사용 편이성 간에 균형을 맞춥니다.
Touch ID가 있고 지원되며 사용하도록 설정된 경우에만 권한 정보가 보존됩니다. 보존된 권한 정보에 애플리케이션 세션당 한 번 액세스하려면 Touch ID 또는 디바이스 패스코드 인증이
필요합니다. 이 정책이 설정되었지만 Touch ID에 액세스할 수 없습니다. 예를 들어 필요한 하드웨어가 없거나 사용 안함으로 설정되어 있으므로
**IMFAuthorizationPersistancePolicyNever**
정책을 대신 사용하십시오. 
