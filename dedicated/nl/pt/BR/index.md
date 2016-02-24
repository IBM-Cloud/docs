{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

#{{site.data.keyword.Bluemix_notm}} Dedicated
{: #dedicated}

*Última atualização: 18 de janeiro de 2016*

{{site.data.keyword.Bluemix}} é
uma plataforma de padrão aberto, baseada em nuvem para construir, executar e
gerenciar aplicativos. Com o {{site.data.keyword.Bluemix_notm}} Dedicated, você obtém o poder e a simplicidade do {{site.data.keyword.Bluemix_notm}}&mdash; em seu próprio ambiente dedicado do SoftLayer que está firmemente conectado ao ambiente do {{site.data.keyword.Bluemix_notm}} Public e à sua própria rede.
{:shortdesc}

O {{site.data.keyword.Bluemix_notm}} Dedicated
inclui um catálogo particular que exibe os serviços dedicados que
estão disponíveis exclusivamente para você. Ele também inclui serviços adicionais
que são organizados e estão disponíveis para uso a partir do {{site.data.keyword.Bluemix_notm}} Public.

O {{site.data.keyword.Bluemix_notm}} Dedicated é
desenvolvido em SoftLayer para que você tenha o maior desempenho da
infraestrutura de nuvem disponível. Cada datacenter possui segurança de 24 horas, 7 dias por semana e
controles rigorosos. Você e a IBM acessam a instância do
{{site.data.keyword.Bluemix_notm}} Dedicated usando um
túnel VPN e uma VLAN privada.

![{{site.data.keyword.Bluemix_notm}} Dedicated](images/detaileddedicated.png "{{site.data.keyword.Bluemix_notm}} Dedicated")

*Figura 1. Diagrama detalhado do
{{site.data.keyword.Bluemix_notm}}
Dedicated*

Ambientes do {{site.data.keyword.Bluemix_notm}} Dedicated
possuem as mesmas normas de segurança que as do {{site.data.keyword.Bluemix_notm}} público em termos de segurança de infraestrutura, operacional e física. No entanto,
o acesso do desenvolvedor ao {{site.data.keyword.Bluemix_notm}} dedicado é
controlado por suas políticas de LDAP, que podem ser configuradas pela equipe do {{site.data.keyword.Bluemix_notm}}
quando configuram seu ambiente. No ambiente dedicado,
é possível gerenciar funções e permissões do usuário. Consulte
[Gerenciando
usuários e permissões](../admin/index.html#oc_useradmin) para obter detalhes.

O {{site.data.keyword.Bluemix_notm}} Dedicated
vem com todos os tempos de execução do {{site.data.keyword.Bluemix_notm}} incluídos
e 128 GB de memória do aplicativo.

Além disso, há um conjunto de serviços incluídos por padrão e opcionais que você pode escolher para a sua instância dedicada.

| **Tipo**        | **Nome**            | **Descrição** |      
|-----------------|-------------------|-------------------|
| Incluído | {{site.data.keyword.autoscaling}} | Aumentar ou diminuir dinamicamente a capacidade de
cálculo do aplicativo com base em políticas. Com esse serviço,
você possui uso ilimitado no ambiente do {{site.data.keyword.Bluemix_notm}}
Dedicated. |
| Incluído | {{site.data.keyword.datacshort}} | Esse serviço fornece uma grade de dados da memória
que suporta cenários de armazenamento em cache distribuído para seus apps. Inclui
50 GB de cache na memória. |
| Opcional | {{site.data.keyword.mql}} | O {{site.data.keyword.mqlfull}} for {{site.data.keyword.Bluemix_notm}} é um serviço de sistema de mensagens baseado em nuvem que fornece sistema de mensagens flexível e fácil de usar para apps {{site.data.keyword.Bluemix_notm}}. O
{{site.data.keyword.mql}} fornece uma solução fácil de administrar para sistema de mensagens. É
possível usar o {{site.data.keyword.mql}} para tornar os seus apps mais responsivos e escaláveis e compartilhar e transferir trabalho entre apps com uma API única e poderosa. |
| Opcional | {{site.data.keyword.dashdbshort}} | Use dashDB para armazenar dados relacionais, incluindo tipos especiais como dados geoespaciais. Depois, analise esses dados com SQL ou análise integrada avançada como análise preditiva e mineração de dados, análise com R e análise geo-espacial. |
|Opcional | {{site.data.keyword.APIM}} | Use o serviço {{site.data.keyword.APIMfull}} para compor, gerenciar e socializar APIs. É
possível importar APIs com recursos usando uma URL de proxy ou montando dados a partir de origens de dados HTTP. O
benefício do uso do serviço {{site.data.keyword.APIM}}
é que é possível gerenciar como suas APIs são usadas. |
|Opcional | {{site.data.keyword.SecureGateway}} | O serviço {{site.data.keyword.SecureGateway}} fornece uma maneira segura de conectar aplicativos {{site.data.keyword.Bluemix_notm}} a locais remotos no local ou na nuvem.   |

*Tabela 1. Serviços dedicados*


##Configurando o {{site.data.keyword.Bluemix_notm}} Dedicated
{: #setupdedicated}

O {{site.data.keyword.Bluemix_notm}} Dedicated
foi projetado para fornecer uma versão privada da oferta {{site.data.keyword.Bluemix_notm}}
Public. É possível usar os serviços e tempos de execução do
{{site.data.keyword.Bluemix_notm}} para suportar suas
necessidades computacionais em uma conta do SoftLayer hospedada pela IBM.

A IBM fornece acesso ao
{{site.data.keyword.Bluemix_notm}} Dedicated usando um login
protegido por senha. É possível acessar os serviços, os tempos de execução
e os recursos associados e implementar e remover apps do {{site.data.keyword.Bluemix_notm}}. A
IBM usufrui das vantagens de vários locais do SoftLayer para entregar o {{site.data.keyword.Bluemix_notm}} Dedicated, para que você tenha sua versão privada em um local perto.

Para configurar sua versão privada do {{site.data.keyword.Bluemix_notm}}:

<ol>
<li>Entre em contato com o representante de conta designado da IBM ou <a href="https://console.ng.bluemix.net/?direct=classic/#/contactUs/cloudOEPaneId=contactUs" target="_blank">entre em contato com o {{site.data.keyword.Bluemix_notm}}</a> para começar.</li>
<li>Trabalhe com a IBM com relação à taxa de sua instância do {{site.data.keyword.Bluemix_notm}} Dedicated. A taxa de recorrência mensal baseia-se nos serviços
dedicados que você desejar usar, mais uma assinatura de todos os serviços públicos do
{{site.data.keyword.Bluemix_notm}}. Em seguida, você receberá uma fatura para tudo o que usar além
desse contrato de assinatura.</li>
<li>Identifique os prazos finais de cada fase de configuração
da instância do {{site.data.keyword.Bluemix_notm}} Dedicated. Para obter informações sobre cada fase e as tarefas envolvidas, veja <a href="index.html#rolesresponsibilities" target="_blank">Funções e responsabilidades do {{site.data.keyword.Bluemix_notm}} Dedicated</a>.</li>
<li>Selecione o <a href="http://www.softlayer.com/data-centers" target="_blank">local do datacenter do SoftLayer</a> para a instância dedicada. Em seguida, sua plataforma e conta dedicadas
são criadas. Para a conta, identifique as pessoas de sua organização
para as funções que são necessárias para tornar a instância dedicada
operacional. Para obter informações sobre as funções designadas, veja <a href="index.html#rolesresponsibilities" target="_blank">Funções e responsabilidades do {{site.data.keyword.Bluemix_notm}} Dedicated</a>.
</li>
<li>Defina e estabeleça conectividade de rede entre a
rede corporativa e a instância do {{site.data.keyword.Bluemix_notm}}
Dedicated.
	<ol type="a">
	<li>A IBM instala a infraestrutura de
monitoramento e segurança da instância dedicada.</li>
	<li>A IBM instala os serviços dedicados de único locatário selecionados.</li>
	<li>Você fornece configuração de rede e terminais para
coisas como endereços IP ou firewalls e acesso ao LDAP para
integração ao {{site.data.keyword.Bluemix_notm}}.</li>
	</ol>
</li>
<li>Identifique e designe funções para sua equipe administrativa para o ambiente.
	<ol type="a">
	<li>A IBM configura o acesso à rede e LDAP baseado no que foi
fornecido. É fornecido
acesso administrativo aos contatos designados. Deve-se também
designar um contato para suporte e faturamento.</li>
	<li>A IBM configura um catálogo organizado em seu ambiente dedicado para mostrar os serviços dedicados. O catálogo organizado inclui serviços adicionais que são organizados e estão disponíveis para uso a partir do {{site.data.keyword.Bluemix_notm}} Public. Você tem a opção de decidir quais serviços públicos atendem aos requisitos para seus negócios com base em sua privacidade de dados e critérios de segurança.</li>
	<li>Você valida a configuração de rede e de firewall,
do terminal LDAP, e acessa.</li>
	</ol>
</li>
</ol>

É possível esperar um processo semelhante à lista a seguir para a implementação e a configuração iniciais do seu ambiente. Para obter detalhes sobre quem é responsável por cada uma das tarefas, veja [Funções e responsabilidades](../dedicated/index.html#rolesresponsibilities).

<ol>
<li>Selecione qual datacenter usar para hospedar sua instância dedicada. Para obter informações sobre opções do datacenter, veja <a href="http://www.softlayer.com/data-centers" target="_blank">Local do datacenter do SoftLayer</a>.</li>
<li>Especifique os nomes de domínio para a implementação e os IDs que deseja usar. Obtenha três domínios ao configurar sua instância do {{site.data.keyword.Bluemix_notm}}. Selecione o prefixo para a <code>*mycompany*.*region*.bluemix.net</code> e  <code>*mycompany*.*region*.mybluemix.net</code>. E, escolha o nome completo do terceiro domínio.<br />
<p>É possível escolher quantos domínios customizados desejar. No entanto, você é responsável pelos certificados dos domínios customizados. Para obter informações sobre como criar seu domínio customizado, veja <a href="../manageapps/updapps.html#domain">Criando e usando um domínio customizado</a>.</p></li>
<li>Identifique um proprietário para a conta pública que é usada para representar sua empresa no {{site.data.keyword.Bluemix_notm}} Public. A IBM usa essa conta para rastrear o uso de serviços organizados.</li>
<li>Selecione o tipo de conexão segura para seu datacenter. É possível selecionar dentre SoftLayer VPN, SoftLayer Direct Link e AT&T Net Bond.</li>
<li>Decida se haverá qualquer acesso ao seu ambiente dedicado a partir da Internet pública.</li>
<li>Selecione o tipo de autenticação que será usada. É possível selecionar a partir do ID IBM ou Active Directory. Para obter informações sobre como usar e registrar um ID IBM, veja a página <a href="https://www.ibm.com/account/profile/us?page=regfaqhelp#4">Ajuda e perguntas mais frequentes</a>.
</li>
<li>Identifique e designe funções à sua equipe administrativa para o ambiente. Para obter informações sobre as funções que você deve designar, veja <a href="index.html#rolesresponsibilities" target="_blank">Funções e responsabilidades do {{site.data.keyword.Bluemix_notm}} Dedicated</a>.</li>
<li>A IBM implementa a plataforma principal que inclui os tempos de execução elásticos, o console, o recurso de administração e o monitoramento.</li>
<li>A IBM configura o acesso administrativo para o ambiente.</li>
<li>É possível começar a usar sua instância dedicada que é monitorada pela equipe de operações da IBM para responder aos alertas. </li>
</ol>

Depois que a instância do {{site.data.keyword.Bluemix_notm}} estiver configurada, será possível monitorar e gerenciar sua instância do {{site.data.keyword.Bluemix_notm}} usando a página Administração. Para obter mais informações, veja [Gerenciando o {{site.data.keyword.Bluemix_notm}} Local e Dedicated](../administer/index.html#mng). Para obter informações sobre upgrades e manutenção, veja [Mantendo sua instância dedicada](index.html#maintaindedicated).

##Funções e responsabilidades
{: #rolesresponsibilities}

Se você configurar uma conta do {{site.data.keyword.Bluemix_notm}} Dedicated, identificará as pessoas em sua organização para as funções necessárias para que sua instância funcione.

###Funções

A lista a seguir mostra as funções e as responsabilidades designadas ao cliente:

<dl>
<dt>**Focal em compras**</dt>
<dd>Trabalha com o representante IBM no estabelecimento do
ambiente do {{site.data.keyword.Bluemix_notm}} Dedicated, incluindo a identificação das pessoas certas em sua organização para trabalhar em qualquer aspecto do projeto. A pessoa designada a essa função recebe uma função de gerenciamento de projeto e supervisiona a seleção padrão, acordos comerciais e a disposição de acesso aos recursos do cliente. O focal em compras é o contato geral para configurar a instância dedicada e rastrear o processo da implementação.</dd>
<dt>**Executivo de conformidade**</dt>
<dd>Trabalha com o representante IBM para selecionar uma opção de topologia e de implementação que atenda aos requisitos de segurança. A pessoa designada a essa função trabalha com o consultor de conformidade IBM para determinar quais padrões de implementação alcançam os objetivos de conformidade.</dd>
<dt>**Especialista em rede**</dt>
<dd>Trabalha com o representante IBM nos planos de rede para a
implementação do {{site.data.keyword.Bluemix_notm}}. A pessoa designada a essa função revisa as especificações de rede necessárias para a IBM e trabalha junto com a IBM em um plano de implementação. No término da fase de instalação e verificação, a pessoa designada a essa função aprovará que a configuração de rede está em conformidade com os padrões corporativos.</dd>
<dt>**DevOps focal**</dt>
<dd>Trabalha com o representante IBM para planejar e aplicar as
atualizações de manutenção que são necessárias para a plataforma,
serviços e tempos de execução do
{{site.data.keyword.Bluemix_notm}}. A pessoa designada a essa função também trabalha com o representante IBM na configuração da instância do {{site.data.keyword.Bluemix_notm}} Dedicated.</dd>
</dl>

Seus representantes de serviços trabalham com seu defensor dedicado e outros especialistas IBM, que trabalham juntos para assegurar que você sempre tenha o suporte necessário. Seu Defensor dedicado é seu único ponto de contato dentro da equipe de suporte de desenvolvimento do {{site.data.keyword.Bluemix_notm}} que conclui as tarefas a seguir:

<ul>
<li>Ativa a adoção rápida do ambiente do {{site.data.keyword.Bluemix_notm}} Dedicated.</li>
<li>Entrega educação de valor e materiais de ativação para melhorar sua autossuficiência.</li>
<li>Cultiva um relacionamento de longo prazo entre você e o desenvolvimento, o suporte e serviços do {{site.data.keyword.Bluemix_notm}} que você usa.</li>
</ul>

O suporte e a equipe de operações do {{site.data.keyword.Bluemix_notm}} que trabalham com você em sua instância do {{site.data.keyword.Bluemix_notm}} podem acessar seu ambiente local, mas faz isso apenas pelos motivos a seguir.

<ul>
<li>Para responder a alertas e executar manutenção operacional</li>
<li>Para tentar reproduzir um problema relatado em um chamado de suporte</li>
</ul>

###Responsabilidades

Da configuração de seu ambiente até a manutenção contínua, deve-se concluir uma variedade de tarefas. A tabela a seguir descreve as tarefas necessárias e o proprietário para concluir a tarefa durante as fases de concepção, progressão e conclusão.

A fase de concepção é usada para estabelecer o ambiente do {{site.data.keyword.Bluemix_notm}} Dedicated. Os objetivos principais dessa fase incluem os itens a seguir:

- Revisar o contrato financeiro e estabelecer as datas do acontecimento para entrega.
- Criar a plataforma {{site.data.keyword.Bluemix_notm}} e fornecer acesso aos tempos de execução e serviços.
- Definir e estabelecer conectividade de rede entre a rede corporativa e as operações do {{site.data.keyword.Bluemix_notm}}.
- Identificar e designar funções para sua equipe administrativa.

*Tabela 1. Tarefas da fase de concepção*

| **Tarefa** | **Detalhes da tarefa** | **Parte responsável** |
|----------|------------------|-----------------------|
|Configurar padrões de conformidade | Identificar padrões corporativos do governo, da indústria e proprietários que são necessários para o ambiente. | Cliente |
|Criar plano de integração de segurança e conformidade | Criar plano de segurança e integração que inclui custos, planejamento e recursos que são necessários para atingir conformidade de segurança. | IBM |
|Aprovação do plano de conformidade | Aprovar o plano de conformidade. | Cliente |
|Criar dimensionamento para o ambiente |  	Criar dimensionamento de ambiente com base nas opções predefinidas que consideram a alta disponibilidade e os objetivos de recuperação de desastre, bem como o DEA inicial e o fornecimento de serviço que são necessários para suportar os apps criados com a plataforma. Você e a IBM trabalham juntos para definir, por exemplo, quais bancos de dados são necessários, quais serviços são oferecidos no catálogo organizado do cliente e muito mais. | A IBM e o cliente compartilham a responsabilidade |
|Selecionar arquitetura | Selecione a arquitetura com base nas opções predefinidas que consideram a alta disponibilidade e os requisitos de recuperação de desastre. | IBM |
|Definir objetivos de recuperação de desastre | Definir os requisitos de recuperação de desastre para o ambiente. | Cliente |
|Criar plano de recuperação de desastres | Consultar e definir o plano de recuperação de desastres. A IBM cria um modelo de recuperação de desastre e consulta você sobre fornecimento de feedback e aprovação do plano. | A IBM e o cliente compartilham a responsabilidade |
|Criar plano de backup e recuperação | Criar um plano de backup e recuperação que defina a frequência e os requisitos para distribuição ocasional do backup pelo site. A IBM faz backup de componentes de malha, serviços IBM, metadados de serviço, incluindo funções de usuário e muito mais. Você faz backup de todos os dados específicos do aplicativo pelos quais é responsável. | A IBM e o cliente compartilham a responsabilidade |
|Identificar ferramentas para detecção de eventos e determinação de problemas | Identificar ferramentas da IBM e de terceiros usadas para detecção de eventos e determinação de problemas no nível da plataforma {{site.data.keyword.Bluemix_notm}}. | IBM |
|Definir plano de escalada | Definir o plano de escalada para fazer triagem e resolver eventos detectados a partir dos componentes de monitoramento. | IBM |
|Assinar contratos de infraestrutura, de plataforma e de suporte | Assinar o contrato de assinatura, incluindo os termos financeiros e as condições para o ambiente. Assinar contrato de monitoramento de rede e segurança. Assinar assinatura de suporte. | Cliente |
|Comprar ambiente | Comprar recursos de cálculo, rede e armazenamento, incluindo VLAN principal e de serviços para hospedar o {{site.data.keyword.Bluemix_notm}}, serviços bare metal para hospedar o Data Power e o SoftLayer Firewall. Fornecer infraestrutura para permitir túnel VPN. | Cliente |
|Instalar componentes de malha, de aplicativo e de monitoramento e gerenciamento | Instalar, configurar e verificar componentes de malha, como BOSH Director, Cloud Controller, Health Manager, sistema de mensagens, roteadores, DEAs e provedores de serviço, além dos componentes de monitoramento definidos no plano de escalada e de detecção de problema. | IBM |
|Instalar e configurar componentes de segurança | Instalar e configurar componentes de segurança que são ligados ao plano de monitoramento e escalada, incluindo IBM QRadar, área segura de credenciais, sistema de prevenção de intrusão, IBM BigFix e IBM Security Privileged Identity Management. | IBM |
|Instalar e configurar componentes customizados |  	Instalar e configurar componentes customizados que residem fora do escopo do produto e serviços {{site.data.keyword.Bluemix_notm}}. | Cliente |
|Estabelecer configuração de rede inicial | Estabelecer configuração de rede inicial, incluindo firewalls, DataPower, Fortigate e DNS. | IBM |
|Conectar pipeline do {{site.data.keyword.Bluemix_notm}} | Conectar pipeline de integração contínua e de entrega contínua do {{site.data.keyword.Bluemix_notm}} com repositórios da IBM. | IBM |
|Customizar componentes de solução externa | Customizar balanceadores de carga para cenários de recuperação de desastre. | Cliente |
|Instalar solução de VPN | Instalar solução de VPN bidirecional. | IBM |
|Configurar servidor de login | Configurar o servidor de login para uso com o LDAP corporativo. | IBM |
|Rastrear status para controles de segurança, de conformidade e de auditoria  | Rastrear status até o ponto em que todas as ferramentas e processos estiverem adequados para atingir a conformidade identificada. | Cliente |
|Revisar a infraestrutura física | Revisar instalações físicas que hospedam os componentes da solução para ameaças e revisão de controles de segurança para proteger o datacenter. | Cliente |
|Inspecionar software de monitoramento | Inspecionar componentes de monitoramento e gerenciamento, conforme definido no plano de escalada e de determinação de problema. | Cliente |
|Inspecionar sistema operacional | Inspecionar para assegurar-se de que a imagem do sistema operacional atenda aos padrões de conformidade. A IBM fornece acesso à imagem do sistema operacional. | A IBM e o cliente compartilham a responsabilidade |

A fase seguinte é a de progressão. A fase de progressão descreve o relacionamento colaborativo em andamento, entre você e o IBM Cloud. Os objetivos principais dessa fase incluem os itens a seguir:

- Revisar a capacidade e coordenar os ajustes necessários.
- Revisar as melhorias de manutenção e plataforma.
- Coordenar as atividades para resolução de problemas e análise de causa raiz.

*Tabela 2. Tarefas da fase de progressão*

| **Tarefa** | **Detalhes da tarefa** | **Parte responsável** |
|----------|------------------|-----------------------|
|Revisar relatórios de capacidade semanal | Revisar os relatórios de capacidade semanal e executar a ação corretiva, se necessário. | Cliente |
|Criar projeções mês a mês | Coletar informações e criar uma projeção mês a mês da capacidade e do consumo. | A IBM e o cliente compartilham a responsabilidade |
|Revisar projeções de capacidade | Revisar as projeções de capacidade, visto que estão relacionadas a eventos externos que podem causar impacto na capacidade, bem como novas implementações previstas de apps. Trabalhe com a IBM para revisar as projeções e planejar adequadamente. | A IBM e o cliente compartilham a responsabilidade |
|Revisar projeções | Revisar as projeções de capacidade, visto que estão relacionadas a eventos externos que podem causar impacto na capacidade. | Cliente |
|Ajustar a capacidade |  Incluir ou remover capacidade conforme suas necessidades mudarem. | IBM |
|Publicar atualizações e manutenção futuras | Criar documentação para a manutenção necessária de componentes da IBM. | IBM |
|Executar manutenção | Trabalhe com a IBM para planejar a manutenção necessária dentro de uma janela de 30 dias. É possível fornecer datas que podem não funcionar para você na janela de 30 dias e a IBM trabalhará para planejar a manutenção adequadamente. | A IBM e o cliente compartilham a responsabilidade |
|Tratar de falhas de fornecimento | Corrigir falhas de fornecimento, se ocorrerem, para serviços criados pelo cliente que estejam implementados no Catálogo. | IBM |
|Executar varreduras de rede e de IP | Executar varreduras diárias e mensais de rede e de IP. | A IBM e o cliente compartilham a responsabilidade |
|Fornecer acesso aos logs de auditoria | Fornecer acesso a todos os logs de auditoria de segurança e administrativos.   | A IBM e o cliente compartilham a responsabilidade |
|Conduzir teste | Conduzir teste periódico de Controles de chave sobre operações e teste de penetração de terceiros. | A IBM e o cliente compartilham a responsabilidade |
|Relato de status, coordenação de auditoria e reuniões de conformidade  | Concluir relato de status, coordenação de auditoria externa e representação em reuniões de status de revisão de conformidade. | IBM |
|Verificação de emprego e de necessidade de negócios | Verificação completa do emprego trimestralmente e verificação da necessidade contínua de negócios para representantes IBM que possuem acesso ao ambiente do cliente. | IBM |
|Resolução de vulnerabilidades de segurança | Resolver vulnerabilidades de segurança relatadas na plataforma. | IBM |

O estágio final da conclusão representa o término do relacionamento entre você e a IBM {{site.data.keyword.Bluemix_notm}}. As tarefas principais dessa fase incluem os itens a seguir:

* Término do contrato financeiro
* Remoção de todas as conexões de rede
* Infraestrutura de reciclagem

*Tabela 3. Tarefas da fase de conclusão*

| **Tarefa** | **Detalhes da tarefa** | **Parte responsável** |
|----------|------------------|-----------------------|
|Terminar o contrato financeiro | Discutir e concordar com um término para o contrato financeiro. | A IBM e o cliente compartilham a responsabilidade |
|Ambiente de desatribuição | Encerrar o acesso e as credenciais para o ambiente. | A IBM e o cliente compartilham a responsabilidade |
|Remover conexões de rede do cliente | Remover conexões de rede entre a IBM e o ambiente do cliente. | A IBM e o cliente compartilham a responsabilidade |
|Reciclar a infraestrutura | Seu ambiente é reciclado com base nos processos definidos pelo SoftLayer. | IBM |

##Mantendo sua instância dedicada
{: #maintaindedicated}

A IBM mantém e instala atualizações e correções conforme
julga adequado para a plataforma, tempos de execução e serviços do {{site.data.keyword.Bluemix_notm}} Dedicated.

**Importante**: A IBM se reserva o direito de interromper os serviços para aplicar manutenção emergencial, conforme necessário. A IBM pode mudar os horários de manutenção planejados, mas o notificará sobre essas mudanças, bem como sobre quaisquer informações de manutenção emergencial.

Os tipos de
manutenção a seguir são necessários para o {{site.data.keyword.Bluemix_notm}} Dedicated:
<dl>
<dt>**Janelas de manutenção padrão**</dt>
<dd>Os serviços utilizam janelas de manutenção predefinidas padrão,
o que pode fazer com que os serviços fiquem indisponíveis. A IBM não requer aprovação do cliente para executar manutenção, mas tenta minimizar o impacto em seus serviços.<br />
<br />
A IBM envia mensagens transmitidas das mudanças que estão planejadas para cada janela de manutenção, por meio de e-mail, telefone ou outros métodos.<br />
<br />
**Importante**: Algum serviço pode não ficar
disponível durante o período de manutenção.</dd>

<dt>**Janela de mudança mensal**</dt>
<dd>A janela de manutenção mensal é aplicada com base na coordenação
entre você e a IBM em uma janela de 21 dias. É possível fornecer à
IBM datas ou horas específicas dentro da janela de 21 dias, o que
pode não funcionar para você. A IBM tenta planejar atualizações
nesses momentos. Com base nas solicitações, a IBM
comunica a janela de manutenção planejada para você. Não se espera que as janelas de
mudança mensal causem impacto no ambiente do Bluemix Dedicated em
execução.<br />
<br />
**Nota:** Se você não solicita um momento específico
para a atualização, a manutenção é aplicada automaticamente no final
da janela.<br />
<br />
Acesse **ADMINISTRAÇÃO > INFORMAÇÕES DO SISTEMA**
para visualizar atualizações pendentes, configurar datas
indisponíveis e aprovar atualizações. Para obter mais informações
sobre notificações e planejamento de atualizações pendentes,
consulte <a href="../admin/index.html#oc_system">Visualizando
informações do sistema</a>.</dd>

<dt>**Outro**</dt>
<dd>A IBM pretende limitar toda a manutenção que possa afetar seus
serviços, especialmente a disponibilidade de seu
ambiente, tempos de execução
e serviços do {{site.data.keyword.Bluemix_notm}}
Dedicated para as atualizações padrão e mensal. Outras janelas de mudança podem ser usadas, excepcionalmente, para gerenciamento
do ambiente. A IBM fará esforços razoáveis para minimizar o impacto a você durante essas janelas de mudança e você será notificado com antecedência.</dd>
</dl>

Para configurar a manutenção de sua instância dedicada, trabalhe com seu representante de conta designado pela IBM para identificar uma janela acordada para a manutenção padrão.

Se houver um problema relatado após uma atualização de manutenção, você acordará com seu representante IBM se for de seu melhor interesse permitir que a IBM reverta a atualização. Em concordância, a IBM reverterá a atualização para restaurar o ambiente para o estado anterior.

## Recuperação de desastre
{: #dr}

O {{site.data.keyword.Bluemix_short}} Public fornece uma plataforma continuamente disponível para inovação. Várias medidas de segurança asseguram que suas organizações, espaços e apps estejam sempre disponíveis. Implementar apps em várias regiões geográficas permite disponibilidade contínua que protege contra perda simultânea não planejada de vários componentes de hardware ou software, ou a perda de um datacenter inteiro, para que, mesmo no caso de um desastre natural em uma localização geográfica, as instâncias de app distribuídas do {{site.data.keyword.Bluemix_notm}} Public em localizações geográficas alternativas fiquem disponíveis.
{: shortdesc}

A recuperação de desastre do {{site.data.keyword.Bluemix_short}} Dedicated torna-se possível por meio de disponibilidade contínua para seus apps, da alta disponibilidade inerente da plataforma e da capacidade de restaurar sua instância no caso de uma falha. Você é responsável por ativar a disponibilidade contínua de seus apps implementando em várias regiões. A alta disponibilidade é construída no nível de plataforma por meio de tecnologias incluídas no Cloud Foundry e de outros componentes. Além disso, é possível trabalhar junto com a IBM para assegurar que seus dados sejam corretamente submetidos a backup no caso de você precisar restaurar sua instância a qualquer momento.

### Ativando a disponibilidade contínua para o {{site.data.keyword.Bluemix_notm}} Dedicated
{: #enabling}

Por padrão, o {{site.data.keyword.Bluemix_notm}} Public é implementado em várias localizações geográficas. No entanto, deve-se fazer o seguinte para ativar instâncias do {{site.data.keyword.Bluemix_notm}} Dedicated distribuídas globalmente:

* Assegure-se de que os desenvolvedores estejam implementando apps em mais de uma região, por meio de um processo manual ou automatizado. As regiões devem ter uma separação de mais de 200 km umas das outras para assegurar que um desastre natural não possa afetar ambas as localizações geográficas.
* Configure um balanceador de carga global, como Akamai ou Dyn, para apontar para apps em pelo menos duas regiões diferentes.

**Nota**: nem todos os serviços do {{site.data.keyword.Bluemix_notm}} suportam distribuição regional. Ao construir um aplicativo, para atingir a distribuição geográfica, deve-se também certificar-se de que os serviços usados por esse aplicativo tenham a sincronização de dados como um recurso-chave.

#### Implementando apps do {{site.data.keyword.Bluemix_notm}} Dedicated em várias localizações geográficas
{: #deploying}

Para implementar em um segundo local ou em vários locais, deve-se seguir um processo semelhante ao usado para ativar sua localização geográfica primária:

1. Ative um novo ambiente dedicado para hospedar instâncias adicionais de seus aplicativos. Para criar um novo ambiente, entre em contato com a equipe de vendas da IBM para iniciar o processo. Para obter mais informações sobre a configuração de uma instância dedicada, consulte [Configurando o {{site.data.keyword.Bluemix_notm}} Dedicated](../dedicated/index.html#setupdedicated). Deve-se efetuar login separadamente para acessar cada ambiente. Cada local físico dos ambientes hospedados deve ter uma separação mínima de 200 km do local original para assegurar disponibilidade.
2. Obtenha o nome de domínio exclusivo no qual seu novo app implementado será hospedado.  Por exemplo, se seu domínio original for *mycompany.east.bluemix.net*, será possível criar um novo ambiente local com um novo domínio, como *mycompany.west.bluemix.net* e implementar no novo domínio.
3. Sempre que você implementar seu app original, implemente também no novo local. Para obter mais informações sobre implementação, consulte [Fazendo upload de seu app](../starters/upload_app.html).


#### Ativando um balanceador de carga global para o {{site.data.keyword.Bluemix_notm}} Dedicated
{: #glb}

Um balanceador de carga global não apenas assegura disponibilidade contínua e é necessário para recuperação de desastre, como também possui diversos benefícios adicionais:

* Roteia usuários para a região mais próxima do {{site.data.keyword.Bluemix_notm}}, por padrão
* Roteia com base no desempenho
* Direciona seletivamente uma porcentagem de tráfego para uma nova versão do aplicativo
* Fornece failover do site com base na verificação de funcionamento da região
* Fornece failover do site com base na verificação de funcionamento do aplicativo
* Usa roteamento ponderado entre os terminais

É possível escolher um balanceador de carga global, como Akamai ou Dyn. Para obter mais informações sobre como usar Akamai como um balanceador de carga global, consulte [Gerenciamento de tráfego global](https://www.akamai.com/us/en/solutions/products/web-performance/global-traffic-management.jsp){: new_window}. Para obter mais informações sobre como usar Dyn como um balanceador de carga global, consulte [Quatro motivos pelos quais as empresas estão levando o balanceamento de carga global para a nuvem](http://dyn.com/blog/4-reasons-businesses-are-taking-global-load-balancing-to-the-cloud/){: new_window}.

### Alta disponibilidade
{: #ha}

Além de ativar a disponibilidade contínua, o {{site.data.keyword.Bluemix_notm}} também fornece alta disponibilidade na plataforma usando tecnologias construídas no Cloud Foundry, no Docker e em outros componentes.

Essas tecnologias incluem os itens a seguir:

<dl>
<dt>Escalabilidade no Cloud Foundry</dt>
<dd>Um <a href="https://docs.cloudfoundry.org/concepts/architecture/execution-agent.html" target="_blank">Droplet Execution Agent (DEA)</a> do Cloud Foundry executa verificações de funcionamento nos apps nele executados. Se houver um problema com o app ou com o próprio DEA, ele implementará instâncias adicionais do app em um DEA alternativo para tratar do problema. Para obter mais informações, consulte <a href="https://docs.cloudfoundry.org/concepts/high-availability.html" target="_blank">Configurando o CF para alta disponibilidade com redundância</a>.
</dd>
<dt>Redundância do SoftLayer</dt>
<dd>Com o SoftLayer em ambientes dedicados, dados em cada cluster de armazenamento em nuvem são gravados várias vezes e os clusters de armazenamento são configurados com recursos de recuperação automática em caso de falha da unidade. Se houver algum problema com uma máquina virtual, o SoftLayer tentará reiniciar a máquina virtual em outro host.</dd>
<dt>Backup de metadados</dt>
<dd>Os metadados são submetidos a backup usando o SoftLayer EVault Backup em um local que tenha uma distância de no mínimo 200 km.</dd>
</dl>

##Restaurando sua instância dedicada
{: #restorededicated}

É feito backup regularmente de definições, metadados e configurações do {{site.data.keyword.Bluemix_notm}} Dedicated para se preparar para indisponibilidades não planejadas no ambiente. Os dados por cujo backup você é responsável incluem dados do aplicativo, dados de serviços do banco de dados em nuvem e armazenamentos de objeto.

Como parte do backup de dados, que inclui metadados e configurações do sistema, a IBM conclui as tarefas a seguir:

<ul>
<li>Criptografa todas as cópias de backup e gerencia chaves de criptografia</li>
<li>Monitora e gerencia a atividade de backup</li>
<li>Fornece os arquivos de backup criptografados</li>
<li>Restaura os dados solicitados</li>
<li>Gerencia conflitos de planejamento entre as operações de gerenciamento de backup e correção</li>
</ul>

Como a proteção de dados privados é crítica, a IBM precisa da sua colaboração ao lidar com o gerenciamento de arquivo de backup, de modo que os arquivos não sejam movidos para fora dos datacenters. Especificamente, a IBM solicita que você conclua as tarefas a seguir:

<ul>
<li>Mova uma cópia dos dados de backup criptografados externos, exatamente como faria para quaisquer outros dados de backup gerenciados.</li>
<li>Forneça os arquivos de backup para o operador da IBM no caso de qualquer necessidade de restauração.</li>
</ul>

# rellinks
## general
* [Descobrir: {{site.data.keyword.Bluemix_notm}} Dedicated](http://www.ibm.com/cloud-computing/bluemix/hybrid/dedicated/)
* [Gerenciando o {{site.data.keyword.Bluemix_notm}} Local e o {{site.data.keyword.Bluemix_notm}} Dedicated](../admin/index.html#mng)
* [Entrando em contato com o suporte](../troubleshoot/getting_customer_support.html#bluemix_support)
