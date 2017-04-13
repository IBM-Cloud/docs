---

copyright:
  years: 2017
lastupdated: "2017-03-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# HSBN(High Security Business Network) vNext Beta
{: #etn_overview}

**HSBN vNext Beta**는 블록체인 비즈니스 네트워크 생성에 바로 사용 가능한 솔루션을 제공합니다. 이 서비스는 신속하게 네트워크를 공급하고 리소스를 쉽게 관리하고 유지보수하기 위한 모니터를 제공합니다. 이 간편한 네트워크 구성 및 관리 프로세스를 통해 비즈니스 솔루션 개발 및 배치에 더 많은 시간과 노력을 기울일 수 있습니다.
{:shortdesc}

**HSBN vNext Beta** 네트워크는 네트워크 리소스(피어, 순서 지정, CA, 소스 코드, 원장)가 모두 **IBM Secure Service Container**(SSC)에 포함되어 있는 LinuxONE 기반의 보안 수준이 높은 환경에서 실행됩니다. 기능은 다음과 같습니다. 
* 피어 투 피어 통신을 위한 성능 최적화
* 확장성을 위한 프레임워크 및 고가용성 
* 하드웨어 암호화, 쉽게 조작할 수 없는 암호 키 및 안전하게 암호화된 가상 머신
* 부정 조작 방지 소프트웨어를 사용하는 안전한 부팅
* 루트 액세스 권한 없음
* FIPS 준수, 높은 수준의 EAL 보호, 감사가능성 및 암호 최적화

**HSNB vNext Beta** 플랜을 구독하면 다음 네트워크 리소스에 대한 지원이 제공됩니다. 

- 충돌 결함 허용 순서 지정 서비스
- 멤버당 2개 피어
- 최대 5명의 추가 네트워크 멤버
- 멤버당 5개의 인스턴스화된 체인코드
- 멤버 특정 인증 기관
- 최대 100개 채널
- 기본 통제 정책(모든 멤버는 관리자이며 네트워크 가입 초대장을 발행할 수 있음)

환경 보안 기능에 대한 세부사항은 [IBM Secure Service Container](etn_ssc.html) 섹션을 참조하십시오. 

## HSBN vNext Beta 플랜
{: #use_hsbn}

### 플랜 액세스

요청에 의해 IBM Blockchain on Bluemix **HSBN vNext Beta** 플랜이 제공됩니다. Bluemix 카탈로그에서 HSBN vNext Beta를 선택하고 서비스 인스턴스를 작성하면 최신 베타 릴리스에 대한 참여 요청이 IBM Blockchain 팀에 전송됩니다. 일단 승인이 되면, 플랜에 참여할 수 있는 이메일 초대장을 받습니다. 지시사항에 따라 HSBN vNext Beta 플랜 대시보드를 시작하십시오. 

HSBN vNext Beta 대시보드에서 다음 세 가지 옵션 중에 선택하십시오. 
1. **네트워크 빠른 시작**: HSBN vNext Beta 네트워크를 작성하고, 가입을 위해 다른 Bluemix 조직을 초대합니다. 
2. **네트워크 가입**: 다른 HSBN vNext Beta 네트워크에 대한 가입 초대장을 확인합니다. 
3. **네트워크 모니터**: 네트워크 리소스(피어, 채널 및 체인코드)를 관리합니다. 

<!-- to do - the rest of this page final edit -->

### 샘플 시나리오

여러분이 Marble 제조사이고 다른 벤더와 거래하는 데 IBM Blockchain 네트워크를 활용하려는 것으로 가정해 보겠습니다. 어떻게 작동할 수 있을까요? 모든 네트워크 멤버 및 공개적으로 사용 가능한 Marble 저장소의 현재 상태가 포함된 컨소시엄 채널을 작성할 수 있습니다. 이 채널에서 발생하는 모든 트랜잭션이 네트워크의 모든 멤버에게 표시되며 모든 트랜잭션을 조회할 수 있습니다. 그러나 개인정보 보호정책 및 기밀성 문제를 해결하기 위해 "서브 채널" 또는 독립형 채널을 작성할 수도 있습니다. 예를 들어, 특정 조건을 충족하는 경우 특정 벤더에게 더 좋은 가격을 제안합니다. 이 트랜잭션은 서브 채널에서 진행할 수 있으며 컨소시엄 채널에 업데이트되는 전체 Marble 공급에는 나중에 영향을 주게 됩니다. 또는 컨소시엄 채널에서 사용 가능하지 않은 특정 클래스의 Marble을 거래하려고 할 수 있습니다. 단순히 독립형 채널의 필수 당사자와 거래하고 컨소시엄 채널의 원장은 영향을 받지 않습니다. 채널은 모두 고유 원장을 보유하므로 개인정보 보호정책에 대한 강력한 메커니즘을 제공하며 채널에 가입하고 인증된 멤버만 원장과 상호작용할 수 있습니다.   

### 네트워크 작성
{: create_a_network}
네트워크는 다음 컴포넌트로 구성됩니다. 
* 트랜잭션을 인증하고 채널의 원장에 대한 블록에 순서를 지정하는 순서 지정 서비스
* 각 멤버의 네트워크 컴포넌트에 대한 ID 자료를 발행하는 멤버 특정 인증 기관(CA)
* 트랜잭션을 실행 및 커미트하고 채널 원장을 유지보수하는 멤버 특정 피어

블록체인 서비스의 대시보드에서 **네트워크 빠른 시작** 단추를 클릭하고 마법사를 따라 수행하십시오. 
1. **네트워크 이름 지정** 페이지에서 블록체인 네트워크 이름 및 멤버 ID를 나타내는 회사 이름을 입력한 후 **다음**을 클릭하십시오. 
2. 다음 **멤버 초대** 페이지에서 초대하려는 참가자의 관련 조직 정보를 지정하십시오. 네트워크에 가입 시 각각 피어 및 CA가 제공되며, 모든 네트워크 멤버는 가입한 모든 채널에 대한 원장을 유지보수합니다. <br>
   **참고:** 최대 5명의 멤버를 네트워크에 초대할 수 있습니다. 
3. **통제 규칙 정의** 페이지에 네트워크 정책 설정이 표시됩니다. 기본적으로, 네트워크의 모든 사용자는 새 채널을 작성하고 멤버를 초대할 수 있습니다.   
4. **인증서 생성** 페이지에서 **자동 생성됨** 옵션을 사용하여 조직의 네트워크 컴포넌트에 대한 인증서를 작성하십시오. 이러한 x509 인증서는 사용자에게 노출되지 않습니다.   
5. 마지막으로, **요약 검토** 페이지에서 네트워크에 대한 구성을 검토한 후 네트워크를 부트스트랩하려면 **완료**를 클릭하십시오. 

이 프로세스는 네트워크의 초기 설정을 완료합니다. 

### 네트워크 가입
{: invite_members}

네트워크가 초기화되고 나면 초대를 받은 사람들은 가입하도록 초대받은 네트워크 및 가입 지시사항이 포함된 이메일을 받게 됩니다. 초대된 사용자는 HSBN vNext 플랜 대시보드에서 사용 가능한 **보류 중인 초대** 단추를 보게 됩니다. 네트워크에 가입하려면 단추를 클릭하십시오. 

1. 목록에서 네트워크를 선택하고 **네트워크 가입**을 클릭하십시오. 
2. 다음 화면에서 통제 규칙을 검토하고 **다음**을 클릭하십시오. 
3. **인증서 생성** 페이지에서 조직 이름을 입력한 다음 **자동 생성됨** 옵션을 선택하십시오. 
4. **네트워크 요약 검토** 페이지에서 네트워크의 설정을 검토하고 **완료**를 클릭하십시오. 설정에는 네트워크에 가입하도록 초대를 받은 **초대된 참가자**도 표시됩니다. 

채널 작성 및 체인코드 설치/인스턴스화에 대한 지시사항은 [모니터](v10_dashboard.html)를 참조하십시오. 

<!-- I think all of this is adequately covered in the Monitor Section; and we already tell the story in the Sample Scenario topic above -->


<!-- From Jeff: Agreed. Commenting out all the rest sections on the page.


### Creating new channels
{: prepare_private_channels}

With the latest HSBN vNext plan, you can create a private channel, install a customized chaincode, complete the trade, and update the inventory number upon the other parties in the network make a query or propose a new transaction.

1. On the HSBN vNext plan dashboard, select **Enter Monitor**.
2. Select **Channels**, and click **New Channel**.
3. On the **Create a Channel** page, enter the channel name and choose the company that you want to make trade with by adding members. Then, click **Create** to create another private consortium channel.
4. Select **Chaincode** after you click the **Enter Monitor** button on the dashboard. You can view the chaincode that are already installed on your peer, or install a new chaincode to the peer.<br>
  **Note:** You can install at most 5 chaincode apps per peer.
5. Click **Install Chaincode** to install the smart contract to the peer. A smart contract, also known as chaincode, is the programmatic code installed and instantiated onto a channel’s peers by an appropriately authorized member. End users then invoke chaincode through a client-side application that interfaces with a network peer. Chaincode runs network transactions, which if validated, are appended to the shared ledger and modify world state. Chaincode can be developed for business contracts, asset definitions, and collectively-managed decentralized applications. You can download [this sample code](https://github.com/hyperledger/fabric/blob/master/examples/chaincode/go/marbles02/marbles_chaincode.go){: new_window} to your local environment for testing.

**Note:** After you install the chaincode onto the peer, you must instantiate the chaincode by providing the initial arguments. In the case of the Marbles sample chaincode, you can input `marble1, blue, 35` in a comma separated list to indicate that you have 35 blue marble1 for trade.


### Commencing transactions
{: commence_txs}

To make transactions within your network, the trading parties must:
* Join the same channel within the network.
* Install the same version of the chaincode onto the peer that represents each organization.


Each successful transaction results in a new block appended to the blockchain, and the ledger in the levelDB updated with the new state. Other members in the network can query the ledger or the transaction history to decide the next transaction.



### Monitoring your network
{: monitor_network}

You can perform the following tasks after you click the **Enter Monitor** button on the dashboard:
* Create new channels and invite other members to join your channels to trade privately.
* Install new chaincodes to your peer to initiate or participate into new trade.
* View the changes of blocks, transactions, chaincode invocations.
* View the log on your peer.
* View the information of resources that your organization owns.
* Export a JSON file containing the low-level networking information for each of your components (such as enrollID/enrollSecret for your CA).  

See the [HSBN vNext Beta dashboard](v10_dashboard.md) for more information about the usage of each panel on the dashboard. 


-->
