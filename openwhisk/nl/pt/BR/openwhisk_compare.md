---

copyright:
  years: 2016, 2017
lastupdated: 2017-04-26

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Função como Serviço comparado
{: #openwhisk_faas_compared}

Uma arquitetura sem servidor não é uma panaceia para todos os problemas de computação, mas resolve
alguns. Há [muitos casos de usos](./openwhisk_use_cases.html) em que um design sem servidor
pode ser uma boa escolha. Aqui vamos comparar as seguintes arquiteturas:

1. **Função como Serviço (FaaS)** - OpenWhisk gerenciado. Atualmente, a IBM é o
único fornecedor que oferece [OpenWhisk no Bluemix](https://console.ng.bluemix.net/openwhisk) gerenciado.

2. **Infraestrutura como Serviço (IaaS)** com o OpenWhisk Roll Your Own (RYO). Os
usuários finais podem fazer download do OpenWhisk no Apache Incubation Project e instalá-lo e executá-lo no [Bluemix IaaS](https://console.ng.bluemix.net/catalog/?category=devices) ou em outra [nuvem IaaS](https://en.wikipedia.org/wiki/Cloud_computing#Infrastructure_as_a_service_.28IaaS.29).

3. **Plataforma como Serviço (PaaS)** - tempo de execução de aplicativo gerenciado. Um bom exemplo é o tempo
de execução do [Liberty
for Java](https://console.ng.bluemix.net/catalog/starters/liberty-for-java) gerenciado pela implementação do IBM Bluemix CloudFoundry.

4. **Contêiner como Serviço (CaaS)** - ambiente de contêiner gerenciado. Um bom
exemplo é [Contêineres no
Bluemix](https://console.ng.bluemix.net/catalog/?category=containerImages) da IBM.

5. **Infraestrutura como Serviço (IaaS)** com o tempo de execução Java EE. Um bom exemplo é o
[WebSphere
Application Server VM no Bluemix](https://console.ng.bluemix.net/catalog/services/websphere-application-server) da IBM.

Aqui está um resumo dos prós e contras de cada opção de arquitetura na **perspectiva de um
usuário final** que desenvolve e opera aplicativos nestes tempos de execução diferentes:


| Tópico | (1) FaaS do OpenWhisk | (2) RYI do OpenWhisk | (3) PaaS | (4) CaaS | (5) IaaS+Java EE |
| --- | --- | --- | --- | --- | --- |
|	Unidade do aplicativo	|	Função única (geralmente um pequeno bloco de código em contêiner JavaScript, Swift ou
Docker) - pode ser menor ou maior que 1 Kb. Normalmente não mais que alguns Kbs.	|	Igual à coluna (1)	|	Dependendo do tempo de execução utilizado - pode ser um arquivo EAR ou WAR ou outro pacote configurável de
aplicativo específico do idioma, geralmente e relativamente grande em tamanho - Kb ou até mesmo Mb com muitos
serviços em um pacote configurável, mas pode ser tão pequeno quanto um único serviço	|	Contêiner do Docker é a
unidade de implementação.	|	MV com o App Server com o arquivo EAR ou WAR e outras
dependências - geralmente dimensionada em Gb.	|
|	Área de cobertura de recurso	|	O usuário final não paga nem se preocupa com memória, CPU ou outros recursos. Enquanto a ação tem alguma área de cobertura, o usuário não precisa se preocupar com isso	|	Alta. O usuário
final deve primeiro fornecer o ambiente IaaS e, somente então, instalar e configurar o OpenWhisk sobre ele.	|	Pequeno. O usuário final paga pela memória e CPU para executar apps, mas não paga por apps que não estiverem executando	|	Pequeno para Médio	|	Alta. O usuário final precisa pagar pelo armazenamento em disco, memória, CPUs e
possivelmente por outros componentes quando o app está em execução. Quando ele é interrompido, somente os custos de armazenamento incorrem	|
|	Instalação e Configuração	|	Nenhum necessário	|	Difícil - tudo é feito pelo usuário final	|	Nenhum necessário	|	Moderado - ferramentas de gerenciamento de hardware, rede, S.O. e contêiner enviadas pelo fornecedor, imagens, conectividade e instâncias do CaaS pelo usuário final	|	Difícil - hardware, rede, S.O. e instalação inicial do Java EE enviados pelo fornecedor, além de configuração adicional, armazenamento em cluster e ajuste de escala pelo usuário final	|
|	Tempo de fornecimento	|	Milissegundos	|	Consulte as colunas (4) e (5)	|	Minutos	|	Minutos	|	Horas	|
|	Administração contínua	|	Nenhuma	|	Fixo	|	Nenhuma	|	Moderado	|	Fixo	|
|	Ajuste de escala elástica	|	Cada ação é sempre instantaneamente e inerentemente escalada, dependendo da carga. Não há necessidade de fornecer MVs ou outros recursos antecipadamente	|	Não fornecido - o usuário final deve fornecer capacidade de cálculo no IaaS e gerenciar o ajuste de escala de MVs. Depois que as MVs forem escaladas, o OpenWhisk escalará a ação automaticamente, mas os recursos já deverão ter sido fornecidos
antecipadamente	|	Automático, mas com ajuste de escala lento. No início de um pico de vários
minutos, os usuários podem estar aguardando uma ação de ajuste de escala ser concluída. O ajuste de escala
automático requer cuidado	|	Automático, mas com ajuste de escala lento. No início de um pico de vários
minutos, os usuários podem estar aguardando uma ação de ajuste de escala ser concluída. O ajuste de escala
automático requer cuidado	|	Não Fornecido	|
|	Planejamento de capacidade	|	Não necessário. O FaaS fornecerá automaticamente o máximo de capacidade
necessário	|	É necessário fornecer capacidade suficiente antecipadamente ou planejá-la	|	Um planejamento de
capacidade é necessário, mas algum aumento de capacidade automático é fornecido	|	Um planejamento de
capacidade é necessário, mas algum aumento de capacidade automático é fornecido	|	É necessário provisionar estaticamente capacidade suficiente para manipular a carga de trabalho de pico	|
|	Conexões e estado persistentes	|	Muito limitado - não pode manter uma conexão persistente, exceto em casos
de armazenamento em cache do contêiner. Geralmente, o estado deve ser mantido no recurso externo	|	Igual à coluna (1)	|	Suportado - pode manter um soquete ou uma conexão aberta durante longos períodos e pode armazenar
o estado na memória entre as chamadas	|	Suportado - pode manter um soquete ou uma conexão aberta durante longos períodos e pode armazenar
o estado na memória entre as chamadas	|	Suportado - pode manter um soquete ou uma conexão aberta durante longos períodos e pode armazenar
o estado na memória entre as chamadas	|
|	Manutenção	|	Não necessário - toda a pilha é gerenciada pela IBM	|	Significativo - dependendo do ambiente de
destino, o usuário deve fornecer instalação e manutenção de hardware, rede, S.O., armazenamento, BD, OpenWhisk,
etc.	|	Não necessário - toda a pilha é gerenciada pelo fornecedor	|	Significativo - o usuário deve criar e manter imagens customizadas, implementar e gerenciar contêineres, conexões entre contêineres, etc.	|	Significativo - o usuário deve alocar MVs e gerenciar e escalar servidores Java EE individualmente	|
|	Alta Disponibilidade (HA) e Recuperação de Desastre (DR)	|	Inerente/sem custos extras	|	Roll Your Own (RYO) 	|	Disponível com custo extra	|	Contêineres com falha podem ser reiniciados automaticamente	|	Disponível com custo
extra, semiautomático. MVs podem efetuar failover automaticamente	|
|	Security	|	Enviado pelo fornecedor	|	Roll Your Own (RYO)	|	Combinação de RYO e enviado pelo fornecedor	|	Combinação de RYO e enviado pelo fornecedor	|	Roll Your Own (RYO)	|
|	Velocidade do desenvolvedor	|	Mais alta	|	Mais alta	|	Mais alta	|	Média	|	Lento	|
|	Utilização de recurso (recursos inativos que ainda precisam ser pagos)	|	Os recursos nunca estão inativos porque eles são chamados somente quando há uma solicitação. Quando não há carga de trabalho, não há alocação de
recursos nem custos	|	Por que essa opção está usando IaaS ou CaaS - considerações semelhantes se aplicam como
nas colunas (4) e (5)	|	Alguns recursos podem estar inativos. O ajuste de escala automático para cima e para
baixo ajuda a eliminar recursos inativos, mas um número de instâncias em execução deve estar sempre
presente e ser usado com menos de 50% da sua capacidade. Instâncias interrompidas não incorrem em nenhum custo	|	Semelhante à coluna (3)	|	Alguns recursos podem estar inativos. O Auto-scaling não é
suportado. Um número de instâncias em execução deve estar sempre presente e ser usado com menos
de 50% da sua capacidade. Instâncias interrompidas podem incorrer em custos de armazenamento	|
|	Vencimento	|	Maturidade precoce	|	Maturidade precoce	|	Maturidade precoce	|	Maturidade moderada	|	Muito
maturo	|
|	Limites de recursos	|	[Alguns limites
existem](./openwhisk_reference.html#openwhisk_syslimits)	|	Depende de recursos alocados	|	Não	|	Não	|	Não	|
|	Latência para serviços raramente utilizados	|	Solicitações raras podem inicialmente observar tempo de resposta
de vários segundos, mas estará em intervalo de milissegundo para solicitações subsequentes	|	Depende	|	Muito baixo	|	Muito baixo	|	Muito baixo - supondo que o sistema possui recursos suficientes	|
|	Tipo de ponto sensacional de aplicativo	|	Processamento de eventos, Internet das Coisas (IoT), backend móvel,
microsserviços. Definitivamente inadequado para aplicativos monolíticos. Consulte
[casos de uso](./openwhisk_use_cases.html)	|	Igual à coluna (1), mas quando o usuário deseja
executar em nuvem não IBM ou executar no local.	|	Aplicativos da web com carga de trabalho 24x7 e serviços
stateful que precisam manter a conexão aberta por longos períodos de tempo. Pode ser usado para executar
microsserviços ou aplicativos monolíticos	|	Bem adequado para aplicativos de microsserviço.	|	Aplicativos
corporativos tradicionais migrados do local para a nuvem. Melhor adequado para aplicativos monolíticos	|
|	Carregando granularidade e faturamento	|	[Por blocos de 100 milissegundos](https://console.ng.bluemix.net/openwhisk/learn/pricing)	|	Depende da implementação - se estiver usando IaaS ou CaaS, então, considerações semelhantes se aplicarão -
consulte as colunas (4) e (5)	|	Normalmente cobrado por hora (raramente por minuto) para pacote configurável
de recursos (CPU + memória + algum espaço em disco)	|	Semelhante à coluna (3)	|	Semelhante à coluna (3)	|
|	Custo Total de Propriedade (TCO)	|	Para aplicativos de ponto ideal, o custo deverá ser menor que as alternativas. Como os recursos são escalados automaticamente, nunca ocorre um problema de fornecimento	|	Para
implementações de nuvem, poderá será mais caro que o FaaS do OpenWhisk, mas, para
implementação no local, poderá ser mais barato que as arquiteturas tradicionais	|	Relativamente baixo -
o usuário não precisa fornecer ou gerenciar recursos, somente precisa se preocupar com seu aplicativo,
no entanto, há algum nível de superfornecimento comparado com sem servidor	|	Moderado - o usuário
precisa provisionar e gerenciar contêineres e aplicativo, mas há algum nível de superfornecimento comparado
com sem servidor e comparado com o PaaS	|	Relativamente alto, mas, considerando que a migração de aplicativos
legados para o modelo nativo em nuvem pode ser muito cara, isso poderá ser uma opção viável e econômica para esses
apps	|
