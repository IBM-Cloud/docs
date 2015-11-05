{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

#{{site.data.keyword.Bluemix_notm}} Local
{: #local}
*Última atualização: 20 de outubro de 2015* 

{{site.data.keyword.Bluemix}} Local traz a eficiência e agilidade da plataforma baseada em nuvem do {{site.data.keyword.Bluemix_notm}} para seu datacenter. Com o
{{site.data.keyword.Bluemix_notm}} Local, é possível proteger
suas cargas de trabalho mais sensíveis no firewall de sua empresa,
enquanto permanece estavelmente conectado e em sincronia
com o {{site.data.keyword.Bluemix_notm}} Public.
{:shortdesc}

A IBM® utiliza operações em nuvem como um serviço para
monitorar e manter seu ambiente, para que você possa se concentrar na construção de apps e serviços que são executados no topo do ambiente. A IBM também manipula atualizações de plataforma, para que você possa se concentrar nos negócios.

{{site.data.keyword.Bluemix_notm}} Local inclui um
catálogo privado, organizado, que exibe os serviços locais que estão
disponíveis exclusivamente para você. Ele também inclui serviços adicionais
que são organizados e estão disponíveis para uso a partir do {{site.data.keyword.Bluemix_notm}} Public.

{{site.data.keyword.Bluemix_notm}} Local fica em uma
máquina virtual que está atrás do firewall de sua empresa, para que
você tenha o maior desempenho e a infraestrutura de nuvem mais
segura disponíveis para você. A IBM instala, monitora remotamente e
gerencia o {{site.data.keyword.Bluemix_notm}} Local em seu
datacenter por meio da tecnologia de retransmissão da IBM.

Retransmissão é um recurso de entrega incluído com o
{{site.data.keyword.Bluemix_notm}} Local que permite que a
IBM forneça automática e consistentemente atualizações
para todas as implementações locais, de modo que você sempre tenha um
sistema atualizado, estável e seguro. A retransmissão obtém
conectividade segura por meio de uma saída, SSL de saída e um túnel
VPN que se origina da máquina virtual de concepção que utiliza
certificados que são específicos a cada instância do
{{site.data.keyword.Bluemix_notm}} Local. O tráfego neste
túnel é a automação Urban Code Deployer para serviço e
manutenção da plataforma, recursos de computação e serviços para sua instância.

![{{site.data.keyword.Bluemix_notm}} Visão geral do Local](images/bluemixlocalarchitecture.png "Visão
geral do Bluemix
Local")

*Figura 1. {{site.data.keyword.Bluemix_notm}}
Visão geral detalhada do Local*

Os ambientes do {{site.data.keyword.Bluemix_notm}}
Local possuem os mesmos padrões de segurança do
{{site.data.keyword.Bluemix_notm}} público em termos de
segurança operacional. Você fornece o hardware e a infraestrutura,
que fornece controle sobre a segurança da infraestrutura e física. O
acesso do desenvolvedor ao {{site.data.keyword.Bluemix_notm}}
local é controlado por suas políticas LDAP, que podem ser
configuradas pela equipe do
{{site.data.keyword.Bluemix_notm}} quando seu ambiente foi
configurado. Dentro do ambiente local, utilizando o Console administrativo, é possível gerenciar funções e permissões do usuário.

O {{site.data.keyword.Bluemix_notm}} Local vem com
todos os tempos de execução do
{{site.data.keyword.Bluemix_notm}} incluídos e 64 GB de
memória de computação.

Além disso, há um conjunto de serviços disponíveis para
o {{site.data.keyword.Bluemix_notm}} Local.

| **Tipo** | **Nome** | **Descrição** |    
|----------|----------|-----------------|
|Incluído | {{site.data.keyword.Bluemix_notm}} Runtimes | Use
tempos de execução para que seu app fique funcionando
rapidamente, sem necessidade de configurar e gerenciar VMs e
sistemas operacionais. Todos os tempos de execução do
{{site.data.keyword.Bluemix_notm}} estão disponíveis
para uso em sua instância do {{site.data.keyword.Bluemix_notm}} Local.|
|Incluído | {{site.data.keyword.autoscaling}}| Aumentar ou diminuir dinamicamente a capacidade de
cálculo do aplicativo com base em políticas. Com esse serviço, você
tem uso ilimitado em seu ambiente do {{site.data.keyword.Bluemix}} Local.|
|Opcional |{{site.data.keyword.datacshort}}| Esse serviço fornece uma grade de dados da memória
que suporta cenários de armazenamento em cache distribuído para seus apps. Inclui
 50 GB de cache na memória. |
|Opcional | {{site.data.keyword.APIM}} | Use o serviço {{site.data.keyword.APIMfull}} para compor, gerenciar e socializar APIs. É
possível importar APIs com recursos usando uma URL de proxy ou montando dados a partir de origens de dados HTTP. O
benefício do uso do serviço {{site.data.keyword.APIM}}
é que é possível gerenciar como suas APIs são usadas. |

*Tabela 1. Serviços locais*

##Configurando a instância do {{site.data.keyword.Bluemix_notm}}
Local
{: #setuplocal}

O {{site.data.keyword.Bluemix_notm}} Local foi projetado
para fornecer uma versão privada da oferta do
{{site.data.keyword.Bluemix_notm}} Public que está
hospedada em seu próprio hardware, gerenciada por você. É possível
usar serviços e tempos de execução do
{{site.data.keyword.Bluemix_notm}} para suportar suas
necessidades de computação em um ambiente em nuvem seguro,
hospedado pelo cliente e gerenciado.

A IBM fornece acesso ao
{{site.data.keyword.Bluemix_notm}} Local usando um login
protegido por senha. É possível acessar os serviços, os tempos de execução
e os recursos associados e implementar e remover apps do {{site.data.keyword.Bluemix_notm}}. Revise
as etapas a seguir para trabalhar com seu representante IBM
para configurar sua instância local do
{{site.data.keyword.Bluemix_notm}}.

Para configurar sua versão privada do {{site.data.keyword.Bluemix_notm}}:

<ol>
<li>Revise os
<a href="index.html#localinfra">requisitos
da infraestrutura do {{site.data.keyword.Bluemix_notm}}
Local</a> para configurar sua instância local.</li>
<li>Entre em contato com o representante de conta da IBM ou entre em
contato com o
<a href="https://console.ng.bluemix.net/?direct=classic/#/contactUs/cloudOEPaneId=contactUs" target="_blank">{{site.data.keyword.Bluemix_notm}}</a>
para começar.</li>
<li>Estabeleça seu contrato do {{site.data.keyword.Bluemix_notm}}
Local com a IBM que inclui datas do acontecimento para entrega.
<ol type="a">
	<li>Trabalhe com a IBM com relação à taxa para sua instância do
{{site.data.keyword.Bluemix_notm}} Local. A taxa de
recorrência mensal baseia-se nos serviços locais que você deseja
usar, mais uma assinatura para todos os
serviços públicos do {{site.data.keyword.Bluemix_notm}}. Em seguida, você receberá uma fatura para tudo o que usar além
desse contrato de assinatura.</li>
	<li>Identifique os prazos finais de cada fase de configuração da
instância do {{site.data.keyword.Bluemix_notm}} Local.</li>
	</ol>
	</li>
<li>Depois que sua plataforma e conta forem criadas,
identifique as pessoas em sua organização para as funções
que são necessárias para que sua instância local esteja ativa e
executando. Para cada função, há um representante IBM correspondente.<br />
<p>Funções do cliente:</p>
<dl>
<dt>**Focal em compras**</dt>
<dd>Trabalha com o representante IBM no estabelecimento de seu
ambiente do {{site.data.keyword.Bluemix_notm}} Local,
incluindo a identificação da pessoa certa em sua organização para
trabalhar em qualquer aspecto do projeto. Essa função supervisiona a seleção padrão, acordos comerciais e a disposição de acesso aos recursos do cliente. O
focal em compras é o contato geral para configurar a instância local.</dd>
<dt>**Executivo de conformidade**</dt>
<dd>Trabalha com o representante IBM para selecionar uma opção de topologia e de implementação que atenda aos requisitos de segurança. Essa
função trabalha com o consultor de conformidade IBM para determinar
quais padrões de implementação alcançam as metas de conformidade e
objetivos.</dd>
<dt>**Especialista em rede**</dt>
<dd>Trabalha com o representante IBM nos planos de rede para a
implementação do {{site.data.keyword.Bluemix_notm}}. Essa função fornece os requisitos para o representante IBM e trabalha junto em um plano de implementação. No
final da fase de instalação e verificação, esta função será "sign
off", quando a configuração da rede está em conformidade com os
padrões corporativos.</dd>
<dt>**DevOps focal**</dt>
<dd>Trabalha com o representante IBM para planejar e aplicar as
atualizações de manutenção que são necessárias para a plataforma,
serviços e tempos de execução do
{{site.data.keyword.Bluemix_notm}}. Essa função também trabalha com o representante IBM na configuração da instância do {{site.data.keyword.Bluemix_notm}} Local.</dd>
</dl>
<p>Funções IBM:</p>
<dl>
<dt>**Gerenciador de fornecimento IBM**</dt>
<dd>Trabalha com o focal de compra do cliente para estabelecer o
ambiente
de cliente. </dd>
<dt>**Consultor de conformidade IBM**</dt>
<dd>Trabalha com o executivo de conformidade do cliente para selecionar
uma opção de topologia e implementação que atenda aos requisitos de segurança.</dd>
<dt>**Especialista em rede IBM**</dt>
<dd>Trabalha com o especialista da rede do cliente para estabelecer os planos de rede para a implementação. Essa função trabalha com o cliente para coletar requisitos e criar um plano de implementação. Essa função também executa testes automatizados para verificar o resultado físico do plano de implementação.</dd>	
<dt>**Focal IBM DevOps**</dt>
<dd>Trabalha com o focal DevOps do cliente na instalação e
manutenção contínua do topologia de implementação. Essa função trabalha com o cliente para planejar e executar as atualizações necessárias para a plataforma e serviços.</dd>
</dl>
</li>
<li>Você fornece o hardware e a IBM ajuda a definir e estabelecer
conectividade de rede entre a rede corporativa e a
instância do {{site.data.keyword.Bluemix_notm}} Local. Para
obter mais informações sobre os requisitos de infraestrutura,
consulte
<a href="index.html#localinfra">requisitos de
infraestrutura do {{site.data.keyword.Bluemix_notm}}
Local</a>. <ol type="a">
	<li>A IBM configura o acesso à rede e LDAP baseado no que foi
fornecido. É fornecido
acesso administrativo aos contatos designados. Deve-se também
designar um contato para suporte e faturamento.</li>
	<li>A IBM configura um catálogo organizado em seu ambiente local
para mostrar os serviços locais e vários dos serviços públicos do
{{site.data.keyword.Bluemix_notm}}.</li>
	<li>Você valida a configuração de rede e de firewall,
do terminal LDAP, e acessa.</li>
	</ol>
</li>
</ol>
	
##Requisitos da infraestrutura local do {{site.data.keyword.Bluemix_notm}}
{: #localinfra}

Para {{site.data.keyword.Bluemix_notm}} Local, você possui a segurança física e a infraestrutura para hospedar a instância local. A
IBM configura os requisitos a seguir para configurar o {{site.data.keyword.Bluemix_notm}} Local.
###Hardware
Embora existam requisitos para o tipo e o tamanho do hardware disponível, é possível escolher qualquer combinação
para atender os requisitos totais do recurso.
<dl>
<dt>**Hardware do VMware ESXi**</dt>
<dd>
ESXi é uma camada de virtualização que é executada em servidores físicos e que abstrai o processador,
a memória, o armazenamento e os recursos em múltiplas máquinas virtuais. Escolha qualquer combinação que atenda aos
totais de recurso a seguir, sob a condição de que a contagem núcleo física mínima por ESXi é oito. As
seguintes especificações são apenas para o tempo de execução
principal do {{site.data.keyword.Bluemix_notm}}.
<ul>
<li>48 núcleos físicos a 2.0 GHz ou mais cada</li>
<li>756 GB de RAM física </li>
</li>Tamanho total de armazenamento de dados de 7.5 TB <ul>
<li>Armazenamento de dados de 7 TB para manter
{{site.data.keyword.Bluemix_notm}} </li>
<li>500 GB de armazenamento de dados para suspender a máquina virtual de concepção</li>
</ul>
</ul>
<p><strong>Nota:</strong> Se você usar diversos armazenamentos de
dados, use o mesmo prefixo para cada um.</p>
</dd>
<dt>**Alta disponibilidade**</dt>
<dd>
Para suportar uma única falha de nó, deve-se ter n+1 ESXi. Por exemplo, se forem usados dois ESXis, significando 16x núcleos cada, então será necessário um terceiro.
<p><strong>Nota:</strong> O administrador VMware do cliente pode decidir impingir o failover de alta disponibilidade rigorosa no cluster para garantir os recursos.</p>
</dd>
<dt>**Rede**</dt>
<dd>
Os requisitos recomendados incluem um grupo da porta acessível de cliente com 10 endereços IP de rede do cliente
que tenham acesso à Internet de saída. Em seguida, defina uma segunda VLAN privada entre somente os
ESXis sendo usados para {{site.data.keyword.Bluemix_notm}} Local. Essa VLAN é mostrada como um grupo da porta em VMware. O {{site.data.keyword.Bluemix_notm}} Local usa isso para sub-rede privada,
que é mais segura e pode ajudar a evitar problemas de roteamento.
</dd>
</dl>

###Configuração do servidor vCenter
Revise os requisitos a seguir de versão,
de datacenter, de conjunto de recursos e de armazenamento de dados.
<dl>
<dt>**Versões suportadas de VMware**</dt>
<dd>vCenter e ESXi 5.1 e 5.5</dd>
<dt>**Datacenter**</dt>
<dd>Crie um datacenter, se não existir um.</dd>
<dt>**Pasta do Datacenter**</dt>
<dd>Crie uma pasta de MV com o mesmo nome que o cluster, se não planeja conceder acesso de Administrador que seja propagado do datacenter.</dd>
<dt>**Cluster**</dt>
<dd>Crie um cluster especialmente para uso do {{site.data.keyword.Bluemix_notm}} Local. Um exemplo para o nome do cluster é
`bluemix`.</dd>
<dt>**Conjunto de recursos**</dt>
<dd>Crie um conjunto de recursos sob o cluster do {{site.data.keyword.Bluemix_notm}} Local. Um exemplo para o nome do conjunto de
recursos é `local`.</dd>
</dt>**Armazenamento de dados**</dt>
<dd>Requer 7.5 TB para a implementação inicial de
{{site.data.keyword.Bluemix_notm}}. <br />
<br />
**Nota**: Ao usar mais de um armazenamento de
dados, assegure-se de que cada um deles comece com o mesmo prefixo. Os exemplos de múltiplos nomes de
armazenamento de dados com o mesmo prefixo são `bluemix_datastore_01` e
`bluemix_datastore_02`.</dd>
</dl>

###Largura da banda da rede
O rendimento recomendado é 5 Mbps para cima e 5 Mbps
para baixo e é possível esperar um uso de dados mensal de 10 GB. A IBM estabelece janelas acordadas quando
grandes pacotes configuráveis de dados são entregues, que podem
ter no máximo 3 GB.
###Permissões de VMware
Configure as funções e as permissões a seguir. A propagação é
configurada para cada permissão. Se a permissão for propagada, a permissão será aprovada na hierarquia de objeto. No
entanto, as permissões para um objeto-filho sempre substituem as permissões que são propagadas de um objeto pai.
<dl>
<dt>**v Center Server**</dt>
<dd>Configure a função como somente leitura e não propagada.<br />
<br />
**Nota**: Essa função é necessária para recuperar o status de
tarefa para operações de disco específicas.</dd>
<dt>**Datacenter**</dt>
<dd>Crie a função "{{site.data.keyword.Bluemix_notm}}" e
conceda permissões para o **Datastore**, incluindo
**Operações de arquivo de nível baixo** e
**Atualizar arquivos da máquina virtual**.<br />
<br />
**Nota**: Esta função é necessária para suportar
posts de arquivos para os armazenamentos de dados.</dd>
<dt>**Cluster**</dt>
<dd>Configure a função como administrador e propagado.</dd>
<dt>**Armazenamento de dados**</dt>
<dd>Configure o administrador de função e propagado para cada armazenamento de dados do {{site.data.keyword.Bluemix_notm}}.</dd>
<dt>**Rede**</dt>
<dd>Configure grupos da porta pública e privada com a função de administrador, não propagados.</dd>
</dl>

###Conjunto do Droplet Execution Agent (DEA)
Cada DEA é configurado com:
- 16 - 32 GB de RAM
- 2x - 4x vCPU
- 150 - 300 GB de armazenamento

Por exemplo, se o tamanho do host ESXi for 256 GB
de memória com 16x núcleos, então serão incluídos oito DEAs. Se o tamanho do host ESXi for 64 GB de memória com
8x núcleos, dois ESXis e quatro DEAs precisarão ser incluídos. É necessário um adicional de 1,5 TB de armazenamento
para cada um dos quatro DEAs. Esse exemplo é baseado em um DEA configurado com 32 GB de RAM, 4x vCPU e 300 GB de armazenamento.

##Mantendo sua instância local
{: #maintainlocal}

A IBM mantém e instala atualizações e correções conforme
julga adequado para a plataforma, tempos de execução e serviços do
Bluemix Local. Os serviços podem não estar disponíveis durante
as janelas de manutenção.

**Importante**: A IBM se reserva o direito de interromper os serviços para aplicar manutenção emergencial, conforme necessário. A
IBM pode mudar os horários de manutenção planejados, mas o notifica sobre quaisquer mudanças, bem como quaisquer informações de manutenção emergencial.

Os tipos de manutenção a seguir são necessários para o {{site.data.keyword.Bluemix_notm}} Local:
<dl>
<dt>**Janelas de manutenção padrão**</dt>
<dd>Os serviços utilizam janelas de manutenção predefinidas padrão,
o que pode fazer com que os serviços fiquem indisponíveis. A IBM não requer aprovação do cliente para executar manutenção, mas tenta minimizar o impacto em seus serviços.<br />
<br />
A IBM envia mensagens transmitidas das mudanças que estão planejadas para cada janela de manutenção, por meio de email, telefone ou outros métodos.<br />
<br />
**Importante**: Algum serviço pode não ficar
disponível durante o período de manutenção.</dd>

<dt>**Janela de mudança mensal**</dt>
<dd>A janela de manutenção mensal é aplicada com base na coordenação
entre você e a IBM em uma janela de 21 dias. É possível fornecer à
IBM datas ou horas específicas dentro da janela de 21 dias, o que
pode não funcionar para você. A IBM tenta planejar atualizações
nesses momentos. Com base nas solicitações, a IBM
comunica a janela de manutenção planejada para você. Não
espera-se que Janelas de mudança mensal causem impacto no ambiente do
Bluemix Local em execução.<br />
<br />
**Nota**: Se você não solicita um tempo específico para a atualização, a manutenção é aplicada automaticamente no final da janela.<br />
<br />
Acesse **ADMINISTRAÇÃO > INFORMAÇÕES DO SISTEMA**
para visualizar atualizações pendentes, configurar datas
indisponíveis e aprovar atualizações. Para obter mais informações
sobre notificações e planejamento de atualizações pendentes,
consulte <a href="../admin/index.html#oc_system">Visualizando
informações do sistema</a>.</dd>

<dt>**Outro**</dt>
<dd>A IBM pretende limitar toda a manutenção que possa afetar seus
serviços, especialmente a disponibilidade do ambiente, tempos de
execução e serviços do Bluemix Local, para as janelas padrão e mensal. Outras janelas de mudança podem ser usadas, excepcionalmente, para gerenciamento
do ambiente. A IBM fará esforços razoáveis para minimizar o impacto
durante essas janelas de mudanças e notificará você com antecedência.</dd>
</dl>

Para configurar a manutenção de sua instância local, trabalhe
com seu representante de conta designado da IBM para identificar uma janela acordada para a
manutenção padrão.
   
