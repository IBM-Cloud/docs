#Serviços
*Última atualização: 25/8/2015*

É possível localizar serviços disponíveis no **Catálogo** em **Serviços** na interface com o usuário do {{site.data.keyword.Bluemix}}.

Há serviços predefinidos disponíveis no {{site.data.keyword.Bluemix_notm}} para aplicativos móveis. O {{site.data.keyword.Bluemix_notm}} facilita
a implementação, hospedagem e escalação desses serviços móveis
para os apps móveis. O foco pode ser a lógica e o
design do aplicativo.

O {{site.data.keyword.Bluemix_notm}} hospeda e gerencia serviços de middleware para aplicativos da Web. Os desenvolvedores
de aplicativos podem especificar os serviços de middleware requeridos. O {{site.data.keyword.Bluemix_notm}} então
fornece automaticamente novas instâncias dos serviços de middleware
especificados e liga as instâncias de serviço ao aplicativo.

O {{site.data.keyword.Bluemix_notm}} exibe serviços de duas maneiras: por categoria de serviço e por tipo de suporte de serviço.

**Categoria**

Os serviços do {{site.data.keyword.Bluemix_notm}}
são organizados em diferentes categorias. Em cada categoria de serviço, os
serviços criados pela IBM são listados primeiro, seguidos pelos serviços de terceiros
e, em seguida, pelos serviços de comunidade.

**Suporte**

Vários níveis de suporte são fornecidos para serviços do {{site.data.keyword.Bluemix_notm}}. A tabela a seguir descreve as informações gerais de suporte para serviços do {{site.data.keyword.Bluemix_notm}}:

*Tabela 1. Informações de suporte de serviços do {{site.data.keyword.Bluemix_notm}}*

|Tipo	|Descrição	|Detalhes do suporte|
|:------|:--------------|:--------------|
|IBM	|Um serviço que é fornecido pela IBM e que está geralmente disponível.	|Problemas determinados como um defeito
em um serviço fornecido pela IBM que geralmente está disponível são suportados. O suporte será fornecido com base na severidade configurada. Para obter informações sobre severidade de chamados, veja [Entrando em contato com o suporte do {{site.data.keyword.Bluemix_notm}}](https://www.ng.bluemix.net/docs/troubleshoot/getting_customer_support.html#bluemix_support).|
|Terceiros	|Um serviço fornecido por uma empresa que não seja a IBM.	|O suporte para serviços de terceiros é fornecido
perlo provedor de serviços. Se um problema for investigado pela IBM e ficar determinado ser um defeito em um serviço de terceiro, a IBM não será obrigada a fornecer uma correção. A IBM compartilhará a análise com o provedor de serviços de terceiro, se necessário.|
|Comunidade	|Um serviço que é fornecido por uma comunidade de software
livre.	|O suporte para serviços de comunidade é fornecido pela
[Comunidade](https://developer.ibm.com/bluemix/) de Desenvolvedores do {{site.data.keyword.Bluemix_notm}}
por meio do [Fórum](https://developer.ibm.com/answers/smartspace/bluemix/) da Comunidade de Desenvolvedores do {{site.data.keyword.Bluemix_notm}}. Se um problema for investigado pela IBM e ficar determinado ser um defeito em serviço de comunidade, a IBM não será obrigada a fornecer uma correção.|
|Beta	|Um serviço que não está pronto para produção e está
em um estágio de avaliação de desenvolvimento. Um serviço Beta pode ajudar as equipes de desenvolvimento
e marketing a avaliar o valor dos serviços antes de tornarem o
serviço geralmente disponível.	|Problemas que são determinados como sendo um defeito
em um serviço beta fornecido pela IBM são suportados mas a IBM não é obrigada a
fornecer uma correção. Além disso,
o chamado de problema será designado como severidade 3 ou 4 onde aplicável. Para obter informações sobre severidade de chamados, veja [Entrando em contato com o suporte do {{site.data.keyword.Bluemix_notm}}](https://www.ng.bluemix.net/docs/troubleshoot/getting_customer_support.html#bluemix_support).|

O {{site.data.keyword.Bluemix_notm}} também tem serviços experimentais que você pode tentar. Para visualizar todos os serviços experimentais, textos padrão e tempos de execução disponíveis, efetue login no {{site.data.keyword.Bluemix_notm}}, role para a parte inferior do Catálogo e, em seguida, clique em **{{site.data.keyword.Bluemix_notm}} Lab Catalog**.

Serviços experimentais podem não ser estáveis e podem mudar de maneiras que não sejam compatíveis com versões anteriores. Esses serviços não são recomendados para uso em ambientes de produção. O suporte para serviços experimentais é fornecido por meio
do [fórum](https://developer.ibm.com/answers/smartspace/bluemix/) da Comunidade de desenvolvedores do
{{site.data.keyword.Bluemix_notm}}. Se um problema for investigado pela IBM
e for determinado que é um defeito em um serviço experimental,
a IBM não será obrigada a fornecer uma correção.

Para usar um serviço na interface com o usuário do {{site.data.keyword.Bluemix_notm}}, interface de linha de comandos cf, IBM {{site.data.keyword.Bluemix_notm}} DevOps Services ou quaisquer ferramentas suportadas, execute as etapas a seguir:

1. Crie uma instância do serviço. Na maioria dos casos,
a instância de serviço pode ser criada durante a criação do aplicativo.

2. Identifique o aplicativo que usa a nova instância de serviço. Para aplicativos da web, é possível especificar mais de um aplicativo
para usar a mesma instância de serviço, geralmente para compartilhamento de dados.

3. Escreva seu próprio código no aplicativo para interagir com
o serviço.

##Serviços por região

Nem todos os serviços estão disponíveis em toda região do {{site.data.keyword.Bluemix_notm}}. A tabela a seguir mostra os serviços que são fornecidos pela IBM.

*Tabela 2. Disponibilidade do serviço*

|Serviço	|Disponível na região sul dos EUA	|Disponível na região do Reino Unido na Europa|
|:----------|:------------------------------|:------------------|
|App Sec Manager	|Sim	|Não|
|AppScan® Dynamic Analyzer	|Sim	|Não|
|AppScan Mobile Analyzer	|Sim	|Não|
|Advanced Mobile Access	|Sim	|Sim|
|Analytics for Apache Hadoop	|Sim	|Não|
|API Management	|Sim	|Sim|
|Auto-Scaling	|Sim	|Sim|
|BigInsights®	|Sim	|Não|
|Business Rules	|Sim	|Sim|
|Cloud Integration	|Sim	|Sim|
|Cloudant® NoSQL DB	|Sim	|Sim|
|Concept Expansion	|Sim	|Sim|
|dashDB™	|Sim	|Sim|
|Data Cache	|Sim	|Sim|
|Delivery Pipeline	|Sim	|Sim|
|Embeddable Reporting	|Sim	|Não|
|Gamification	|Sim	|Sim|
|Geospatial Analytics	|Sim	|Sim|
|Globalização	|Sim	|Não|
|IBM DataWorks	|Sim	|Sim|
|Insights for Twitter	|Sim	|Sim|
|Teste de Integração	|Sim	|Sim|
|Internet of Things Foundation	|Sim	|Não|
|Message Hub	|Sim	|Não|
|Message Resonance	|Sim	|Sim|
|Mobile Analyzer for iOS	|Sim	|Não|
|Mobile Application Security	|Sim	|Sim|
|Mobile Data	|Sim	|Sim|
|Monitoring and Analytics	|Sim	|Sim|
|Mobile Quality Assurance	|Sim	|Sim|
|MQ Light	|Sim	|Sim|
|Armazenamento de objeto	|Sim	|Não|
|Push	|Sim	|Sim|
|Push for iOS 8	|Sim	|Sim|
|Perguntas e Respostas	|Sim	|Sim|
|Rapid Apps	|Sim	|Sim|
|Relationship Extraction	|Sim	|Sim|
|Secure Gateway	|Sim	|Sim|
|Cache de sessão	|Sim	|Sim|
|Single Sign On	|Sim	|Não|
|SQL Database	|Sim	|Sim|
|Static Analyzer	|Sim	|Sim|
|Streaming Analytics	|Sim	|Não|
|Time Series Database	|Sim	|Sim|
|Track & Plan	|Sim	|Sim|
|Visualization Rendering	|Sim	|Sim|
|Fluxo de Trabalho	|Sim	|Sim|
|Workload Scheduler	|Sim	|Sim|
|XPages NoSQL Database	|Sim	|Sim|


##Incluindo um serviço em seu aplicativo
*Última atualização: 25/08/2015*

O {{site.data.keyword.Bluemix}} possui
uma lista de serviços e gerencia-os em nome dos desenvolvedores. Para incluir um serviço para o
seu aplicativo, deve-se solicitar uma instância desse serviço e configurar o aplicativo para
interagir com o serviço.

É possível ver todos os serviços que estão disponíveis no {{site.data.keyword.Bluemix_notm}} das maneiras a seguir:

* A partir da interface com o usuário do {{site.data.keyword.Bluemix_notm}}. Visualize o Catálogo do {{site.data.keyword.Bluemix_notm}}.
* A partir da interface da linha de comandos cf. Use o comando **cf marketplace**.
* A partir de seu próprio aplicativo. Use a [API de Serviços GET /v2/services](http://apidocs.cloudfoundry.org/197/services/list_all_services.html).

É possível selecionar o serviço necessário ao desenvolver
aplicativos. Na seleção, o
{{site.data.keyword.Bluemix_notm}} interage com o serviço e
executa as etapas necessárias para fornecer os recursos do serviço. O processo de fornecimento pode ser diferente para diferentes
tipos de serviços. Por exemplo, um serviço de banco de dados cria um banco de dados
e um serviço de notificação push para aplicativos móveis gera
informações de configuração.

O {{site.data.keyword.Bluemix_notm}} fornece os recursos de um
serviço para o aplicativo usando uma instância de serviço. Uma instância de serviço pode ser compartilhada entre os aplicativos da web.

É possível também usar serviços que são hospedados em outras regiões, se esses serviços estiverem disponíveis
nessas regiões. Esses
serviços devem ser acessíveis pela internet e possuírem terminais de API. Deve-se
codificar manualmente o aplicativo para usar esses serviços da mesma maneira que você
codifica aplicativos externos ou ferramentas de terceiros para usar os serviços
{{site.data.keyword.Bluemix_notm}}. Para obter informações adicionais, veja [Permitindo que aplicativos externos e ferramentas de terceiros usem os serviços do {{site.data.keyword.Bluemix_notm}}](https://www.ng.bluemix.net/docs/services/reqnsi.html#accser_external).

Se você desejar incluir um serviço no catálogo de serviços do {{site.data.keyword.Bluemix_notm}} para os aplicativos {{site.data.keyword.Bluemix_notm}} usar, será possível construir
seu próprio serviço e integrá-lo com o {{site.data.keyword.Bluemix_notm}}. Para obter mais informações, veja [Integrando um serviço ao {{site.data.keyword.Bluemix_notm}}](https://www.stage1.ng.bluemix.net/docs/services/v2api.html).

###Solicitando uma nova instância de serviço

Para solicitar uma nova instância de serviço, deve-se usar a interface com o usuário do {{site.data.keyword.Bluemix_notm}} ou a interface de
linha de comandos cf.

**Nota:** Ao especificar o nome do serviço, evite usar caracteres que não sejam caracteres alfabéticos ou numéricos, pois os resultados poderão ser imprevisíveis.

Se você usar a interface com o usuário do {{site.data.keyword.Bluemix_notm}} para solicitar uma instância de serviço, conclua as etapas a seguir:

1. No **Catálogo** do {{site.data.keyword.Bluemix_notm}}, clique no ladrilho para o serviço que você deseja incluir. A página de detalhes do serviço é aberta.

2. Na área de janela Incluir serviço, selecione um aplicativo que você deseja ligar a essa instância de serviço a partir da lista **App**.

3. Digite um nome no campo **Nome do serviço**. Um nome de serviço padrão é fornecido. É possível alterar o nome no campo ou
mantê-lo inalterado.

4. Preencha os campos ou seleções adicionais e, em seguida, clique em **CREATE**.

Se estiver usando a interface de linha de comandos cf para solicitar uma instância de serviço, conclua as seguintes etapas:

1. Use o comando **cf marketplace** para localizar o nome e o plano do serviço
que você requer.

2. Use o comando a seguir para criar uma instância de serviço, em que service_name é o nome do serviço, service_plan é o plano do serviço e service_instance é o nome que você deseja usar para essa instância de serviço.

    ```
    cf create-service service_name service_plan service_instance
    ```

3. Use o comando a seguir para ligar a instância de serviço a um aplicativo, em que appname é o nome do aplicativo e service_instance é o nome da instância de serviço.

    ```
    cf bind-service appname service_instance
    ```

**Nota:** Uma instância de serviço é específica para um espaço em que a instância de serviço é criada. Não é possível mover uma instância de serviço para
outro espaço ou organização. Em vez disso, deve-se solicitar uma nova instância de
serviço para cada espaço em que você deseja utilizá-la.

### <a id='config'></a> Configurando seu aplicativo para interagir com um serviço ###

Depois de ligar uma instância de serviço ao aplicativo, deve-se
configurar o aplicativo para interagir com o serviço.

Cada serviço pode requer um mecanismo diferente
de comunicação com os aplicativos. Esses mecanismos são
documentados como parte da definição de serviço para suas informações
ao desenvolver aplicativos. Para consistência, os
mecanismos são necessários para que seu aplicativo interaja
com o serviço.

* Para interagir com os serviços de banco de dados, use as informações que o {{site.data.keyword.Bluemix_notm}} fornece como o ID do usuário, senha
e o URI de acesso para o aplicativo.
* Para interagir com os serviços de backend móveis, use as informações que o {{site.data.keyword.Bluemix_notm}} fornece, como a identidade
do aplicativo (ID do app), informações de segurança que são específicas para o cliente e o URI de acesso para
o aplicativo. Os serviços móveis geralmente funcionam em contexto entre si para que as informações de
contexto, como o nome do desenvolvedor de aplicativos e o usuário que usa o aplicativo,
possam ser compartilhadas em todo o conjunto de serviços.
* Para interagir com os aplicativos da Web ou código do lado do servidor para aplicativos móveis, use as
informações que o {{site.data.keyword.Bluemix_notm}} fornece como
as credenciais de tempo de execução no ambiente *VCAP_SERVICES* do
aplicativo. O valor da variável de ambiente *VCAP_SERVICES*
é a serialização de um objeto JSON. A
variável contém os dados de tempo de execução que são necessários
para interagir com os serviços aos quais o aplicativo está ligado. O
formato dos dados é diferente para serviços diferentes. Talvez seja necessário ler a documentação do serviço sobre
o que deve-se esperar e como interpretar cada parte de informação.

Se um serviço ligado a um aplicativo ficar paralisado, o aplicativo pode ter parado de executar ou conter erros. O {{site.data.keyword.Bluemix_notm}}
não reinicia automaticamente o aplicativo para recuperar desses problemas. Considere codificar o aplicativo para identificar e recuperar de indisponibilidades,
exceções e falhas de conexão. Consulte o tópico de resolução de problemas [Os apps não serão reiniciados automaticamente](https://www.ng.bluemix.net/docs/troubleshoot/managingapps.html#tr_appnotautorestarted) para obter informações adicionais.

###Permitindo que apps externos usem serviços do {{site.data.keyword.Bluemix_notm}}

Pode haver aplicativos que foram criados e executados fora
do {{site.data.keyword.Bluemix_notm}}
ou é possível usar ferramentas de terceiros. Se os serviços do
{{site.data.keyword.Bluemix_notm}} fornecerem
terminais acessíveis pela internet, será possível  usar esses serviços com apps locais ou
ferramentas de terceiros.

Para ativar um app externo ou ferramenta de terceiro para usar um serviço do {{site.data.keyword.Bluemix_notm}}, conclua as etapas a seguir:

1. Solicite uma instância do serviço.
    1. No Painel na interface com o usuário do {{site.data.keyword.Bluemix_notm}}, clique em **Usar serviços ou APIs**. O Catálogo é exibido.
    2. No Catálogo, selecione o serviço desejado clicando no ladrilho do serviço. A página de detalhes do serviço é aberta.
    3. Na janela Incluir serviço, mantenha a seleção da lista **App**: como **Deixar desvinculado**. Essa seleção significa que o serviço não será conectado a um app do {{site.data.keyword.Bluemix_notm}}.
    4. Faça qualquer outra seleção conforme necessário. Em seguida, clique em **CRIAR**. Uma instância de serviço é criada e o Painel de serviço é exibido.
2. Na área de janela de navegação à esquerda do Painel de serviço, é possível selecionar **Credenciais do serviço ** para visualizar ou incluir credenciais no formato JSON. Use a chave de API que é exibida como as credenciais para se conectar à instância de serviço.

Seu aplicativo que é executado fora do
{{site.data.keyword.Bluemix_notm}} agora poderá
acessar o serviço do {{site.data.keyword.Bluemix_notm}}.

**Nota:** Se desejar excluir instâncias de serviço ou verificar as informações de faturamento, deve-se voltar para o Painel na interface com o usuário para gerenciar as instâncias de serviço.

###Criando uma instância de serviço fornecida pelo usuário

É possível ter recursos que sejam gerenciados fora do {{site.data.keyword.Bluemix_notm}}. Se você tiver credenciais para acessar esses recursos externos a partir da Internet, é possível criar instâncias de serviço fornecido pelo usuário do {{site.data.keyword.Bluemix_notm}} para representar e se comunicar com os seus recursos externos.

Para criar uma instância de serviço fornecida pelo usuário e ligá-la a um aplicativo, conclua as etapas a seguir:

1. Crie uma instância de serviço fornecida pelo usuário usando o comando **cf create-user-provided-service** ou **cf
cups**:
    * Para criar uma instância de serviço fornecida pelo usuário, use a opção **-p** e separe os nomes de parâmetro com vírgulas. A interface da linha de comandos cf, então, solicita cada parâmetro por vez. Por exemplo:
        ```
        cf cups testups1 -p "host, port, dbname, username, password"
        host> pubsub01.example.com
        port> 1234
        dbname> sampledb01
        username> pubsubuser
        password> p@$$w0rd
        Creating user provided service testups1 in org my-org / space dev as user@sample.com...
        OK
        ```

    * Para criar uma instância de serviço que drene informações para um software de gerenciamento de log de terceiro, use a opção **-l** e especifique o destino que o software de gerenciamento de log de terceiro fornece. Por
exemplo:

        ```
        cf cups testups2 -l syslog://example.com
        Creating user provided service testups2 in org my-org / space dev as user@sample.com...
        OK
        ```

    Se você desejar atualizar um ou mais parâmetros da instância de serviço fornecida pelo usuário, use o comando **cf update-user-provided-service** ou **cf uups**.

    * Para atualizar uma instância de serviço geral fornecida pelo usuário, use a opção **-p**
e especifique as chaves e valores de parâmetro em um objeto json. Por
exemplo:

        ```
        cf uups testups1 -p "{\"username\":\"pubsubuser2\",\"password\":\"p@$$w0rd2\"}"
        Updating user provided service testups1 in org my-org / space dev as user@sample.com...
        OK
        ```

    * Para criar uma instância de serviço que drene informações para um software de gerenciamento de log de terceiro, use a opção -l. Por
exemplo:

        ```
        cf uups testups2 -l syslog://example2.com
        Updating user provided service testups2 in org my-org / space dev as user@sample.com...
        OK
        ```

2. Ligar a instância de serviço ao seu aplicativo usando o comando cf bind-service. Por
exemplo:

	```
	cf bind-service myapp testups1
	Binding service testups1 to app myapp in org my-org / space dev as user@sample.com...
	OK
	```

Agora é possível configurar o seu aplicativo para usar os recursos externos. Para obter informações sobre como configurar seu aplicativo para interagir com um serviço, veja [Configurando seu aplicativo para interagir com um serviço](#config).

###Usando serviços em uma outra região

Se você tiver uma instância de serviço criada e ligada
a apps em uma região, poderá usar esta instância de serviço em uma outra
região criando um serviço fornecido pelo usuário.

Suponha que você esteja iniciando na região em que
deseja usar a instância de serviço. Para usar uma instância de serviço existente
em uma outra região, conclua as etapas a seguir:

1. Alterne para a região em que a instância de serviço existe. Na barra de menus superior do {{site.data.keyword.Bluemix_notm}},
expanda **Região** ou clique no ícone **Região** e,
em seguida, selecione a região em que a instância de serviço existe.

2. Recupere as credenciais e os parâmetros de conexão da variável de ambiente VCAP_SERVICES da instância de serviço na região na qual o serviço existe. Conclua
as etapas a seguir:

	1. No Painel do {{site.data.keyword.Bluemix_notm}}, clique no tile do aplicativo. A página Visão geral é exibida.
	2. Na área de janela de navegação à esquerda, clique em **Variáveis de ambiente**. Os detalhes da variável de ambiente *VCAP_SERVICES*
são exibidos na área de janela direita. Registre o conteúdo JSON para a
instância de serviço.

3. Alterne para a região em que você deseja usar a instância de
serviço. Na barra de menus superior do {{site.data.keyword.Bluemix_notm}}, expanda **Região** ou clique no ícone **Região** e, em seguida, selecione a região em que você deseja usar a instância de serviço.

4. Crie uma instância de serviço fornecida pelo usuário usando as credenciais
e os parâmetros de conexão que você registrou a partir da variável de ambiente
*VCAP_SERVICES*. Para obter informações sobre como criar
uma instância de serviço fornecida pelo usuário, consulte [Criando uma
instância de serviço fornecida pelo usuário](creating-a-user-provided-service-instance).

5. Ligue a instância de serviço fornecida pelo usuário ao seu app
usando o comando a seguir:

	```
	cf bind-service myapp user-provided_service_instance
	```

# rellinks
## general 
* [Ligando um serviço usando a interface com o usuário do {{site.data.keyword.Bluemix_notm}}](https://www.ng.bluemix.net/docs/starters/ee.html#ee_bindui)
* [Recuperando VCAP_SERVICES](https://www.ng.bluemix.net/docs/cli/retrieving.html)


