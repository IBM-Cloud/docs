---

 

copyright:

  years: 2014, 2017

lastupdated: "2017-01-10" 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Segurança do {{site.data.keyword.Bluemix_notm}}
{: #security}

Projetada com práticas seguras de engenharia, a plataforma do {{site.data.keyword.Bluemix}} possui controles de segurança em camadas na rede e na infraestrutura. O {{site.data.keyword.Bluemix_notm}} fornece um grupo de serviços de segurança que podem ser usados por desenvolvedores de aplicativos para proteger seus apps móveis e da web. Esses elementos são combinados para fazer do {{site.data.keyword.Bluemix_notm}} uma plataforma com opções claras para desenvolvimento seguro do aplicativo.
{:shortdesc}

O {{site.data.keyword.Bluemix_notm}} garante disponibilidade de segurança ao seguir as políticas de segurança que são orientadas por melhores práticas na IBM para sistemas, rede e engenharia segura. Essas políticas incluem práticas, como varredura do código-fonte, varredura dinâmica, modelagem de ameaça e teste de penetração. O {{site.data.keyword.Bluemix_notm}} segue o processo IBM Product Security Incident Response Team (PSIRT) para gerenciamento de incidentes de segurança. Veja o site [IBM Security Vulnerability Management (PSIRT) ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](http://www-03.ibm.com/security/secure-engineering/process.html){: new_window} para obter detalhes.

O {{site.data.keyword.Bluemix_notm}} público e usar usa os serviços de nuvem de infraestrutura como serviço (IaaS) do {{site.data.keyword.BluSoftlayer}} e aproveita ao máximo sua arquitetura de segurança. O {{site.data.keyword.BluSoftlayer}} IaaS fornece várias camadas de sobreposição de proteção para seus aplicativos e dados. Para {{site.data.keyword.Bluemix_notm}} Local, você possui a segurança física e fornece a infraestrutura hospedando o {{site.data.keyword.Bluemix_notm}} Local em seu próprio datacenter sob um firewall da empresa. Além disso, o {{site.data.keyword.Bluemix_notm}} inclui recursos de segurança na camada Plataforma como serviço em diferentes categorias: plataforma, dados e aplicativo.

## Segurança da plataforma do {{site.data.keyword.Bluemix_notm}}
{: #platform-security}

O {{site.data.keyword.Bluemix_notm}} fornece segurança funcional, de infraestrutura, operacional e física (por meio do {{site.data.keyword.BluSoftlayer}}) para a plataforma principal. No entanto, o {{site.data.keyword.Bluemix_notm}} Local é exclusivo porque o cliente fornece a infraestrutura e o datacenter e possui segurança física.

O ambiente do {{site.data.keyword.Bluemix_notm}} no {{site.data.keyword.BluSoftlayer}} é compatível com as normas de segurança mais restritivas da tecnologia da informação (TI) da IBM, que atendem ou excedem os padrões de mercado. Esses padrões incluem o seguinte:
rede, criptografia de dados e controle de acesso
 * ACLs do aplicativo, permissões e teste de penetração
 * Identificação, autenticação e autorização
 * Informações e proteção de dados
 * Integridade de serviço e disponibilidade
 * Vulnerabilidade e gerenciamento de correção
 * Negação de serviço e detecção de ataques sistemáticos
 * Resposta a incidentes de segurança

![Visão geral de segurança da plataforma Bluemix](images/platform_sec.svg)

Figura 1. Visão geral de segurança de plataforma do {{site.data.keyword.Bluemix_notm}}

Com o {{site.data.keyword.Bluemix_notm}} Local, você hospeda o {{site.data.keyword.Bluemix_notm}} atrás do firewall de sua empresa e em seu datacenter. Portanto, você é responsável por determinados aspectos de segurança. A seguinte imagem detalha quais partes da segurança são de propriedade do cliente e quais partes de segurança são gerenciadas e mantidas pela IBM.

![Visão geral de segurança da plataforma Bluemix Local](images/security_local_platform.svg) {: #localplatformsecurity}

Figura 2. Visão geral de segurança da plataforma do {{site.data.keyword.Bluemix_notm}} Local

A IBM instala, monitora remotamente e gerencia o {{site.data.keyword.Bluemix_notm}} Local em seu datacenter por meio de Retransmissão, um recurso de entrega incluído com o {{site.data.keyword.Bluemix_notm}} Local. A Retransmissão se conecta com segurança a certificados específicos de cada instância do {{site.data.keyword.Bluemix_notm}} Local. Para obter mais informações sobre o {{site.data.keyword.Bluemix_notm}} Local e Retransmissão, consulte [Bluemix Local](/docs/local/index.html).

### Segurança funcional

O {{site.data.keyword.Bluemix_notm}} fornece vários recursos de segurança funcional, incluindo autenticação do usuário, autorização de acesso, auditoria de operações críticas e proteção de dados.

<dl>
<dt>Autenticação</dt>
<dd>Os desenvolvedores de aplicativos são autenticados no {{site.data.keyword.Bluemix_notm}} usando o IBM Web identity.

Para {{site.data.keyword.Bluemix_notm}} Dedicated e Local, a autenticação por meio de LDAP é suportada por padrão. Sob solicitação, a autenticação por meio do IBM Web identity pode ser configurada em vez de {{site.data.keyword.Bluemix_notm}}.
</dd>

<dt>Autorização</dt>
<dd>O {{site.data.keyword.Bluemix_notm}} usa os mecanismos do Cloud Foundry para assegurar que cada desenvolvedor de aplicativos tenha acesso somente aos aplicativos e instâncias de serviço que criaram. A autorização para serviços do {{site.data.keyword.Bluemix_notm}} baseia-se em OAuth. O acesso a todos os terminais internos da Plataforma do {{site.data.keyword.Bluemix_notm}} é restrito aos usuários externos.</dd>

<dt>Auditoria</dt>
<dd>São criados logs de auditoria para todas as tentativas de autenticação bem-sucedidas e malsucedidas dos desenvolvedores de aplicativos. Logs de auditoria são criados também para acesso privilegiado a sistemas Linux que hospedam os contêineres nos quais os aplicativos {{site.data.keyword.Bluemix_notm}} são executados.</dd>

<dt>Proteção de dados</dt>
<dd> Todo o tráfego do {{site.data.keyword.Bluemix_notm}} passa pelo IBM WebSphere® DataPower® SOA Appliances, que fornece funções de proxy reverso, rescisão de SSL e balanceamento de carga.
Os métodos de HTTP a seguir são permitidos:
<ul>
<li>DELETE</li>
<li>GET</li>
<li>HEAD</li>
<li>OPTIONS</li>
<li>POST</li>
<li>PUT</li>
<li>TRACE</li>
</ul>
 A inatividade de HTTP atinge o tempo limite em 2 minutos.</dd>
<dd>Os cabeçalhos a seguir são preenchidos pelo DataPower:
<dl>
<dt>$wsis</dt>
<dd>Configurado como true se a conexão do lado do cliente for segura (HTTPS) e como false, caso contrário.</dd>
<dt>$wssc</dt>
<dd>Configurado com um dos esquemas de conexão de cliente a seguir: https, http, ws ou wss.</dd>
<dt>$wssn</dt>
<dd>Configurado com o nome do host que é enviado pelo cliente.</dd>
<dt>$wssp</dt>
<dd>Configurado com a porta do servidor à qual o cliente se conecta.</dd>
<dt>x-client-ip</dt>
<dd>Configurado com o endereço IP do cliente.</dd>
<dt>x-forwarded-proto</dt>
<dd>Configurado com um dos esquemas de conexão de cliente a seguir: https, http, ws ou wss.</dd>
</dl>
</dd>

<dt>Práticas seguras de desenvolvimento</dt>
<dd> Para {{site.data.keyword.Bluemix_notm}} Public e Dedicated, varreduras de vulnerabilidade de segurança periódicas são executadas em vários componentes do {{site.data.keyword.Bluemix_notm}} usando o IBM Security AppScan® Dynamic Analyzer. A modelagem de ameaça e teste de penetração são executadas para detectar e tratar possíveis vulnerabilidades em todos os tipos de implementações do {{site.data.keyword.Bluemix_notm}}. Além disso, os desenvolvedores de aplicativos podem usar o serviço AppScan Dynamic Analyzer para proteger seus apps da web que são implementados no {{site.data.keyword.Bluemix_notm}}.</dd>
</dl>

### Segurança da infraestrutura

O {{site.data.keyword.Bluemix_notm}} baseia-se no Cloud Foundry para fornecer uma base robusta para executar seus aplicativos. Na arquitetura, vários componentes são fornecidos para segurança e isolamento. Além disso, gerenciamento de mudanças e procedimentos de recuperação e backup são implementados para assegurar integridade e disponibilidade.

<dl>
<dt>Segregação do ambiente</dt>
<dd> Para {{site.data.keyword.Bluemix_notm}} Public, os ambientes de desenvolvimento e de produção são segregados entre si para melhorar a estabilidade e a segurança do aplicativo.</dd>

<dt>Firewalls</dt>
<dd> Firewalls são adequados para restringir o acesso à rede do {{site.data.keyword.Bluemix_notm}}. Para {{site.data.keyword.Bluemix_notm}} Local, o firewall da sua empresa segrega o resto de sua rede de sua instância do {{site.data.keyword.Bluemix_notm}}.</dd>

<dt>Proteção contra intrusão</dt>
<dd>Os {{site.data.keyword.Bluemix_notm}} Public e Dedicated permitem proteção contra intrusão para descobrir ameaças, para que elas possam ser tratadas. As políticas de proteção contra intrusão são ativadas nos firewalls.</dd>

<dt>Gerenciamento de contêiner do aplicativo seguro</dt>
<dd>Cada aplicativo do {{site.data.keyword.Bluemix_notm}} é isolado e executado em seu próprio contêiner, que possui limites de recurso específicos para processador, memória e disco.</dd>

<dt>Reforço de segurança do sistema operacional</dt>
<dd>Os administradores IBM executam o reforço da rede e do sistema operacional regularmente, usando ferramentas tais como o IBM Endpoint Manager.</dd>
</dl>

### Segurança operacional

O {{site.data.keyword.Bluemix_notm}} fornece um ambiente de segurança operacional robusto com os controles a seguir.

<dl>
<dt>Varredura de vulnerabilidade</dt>
<dd>O {{site.data.keyword.Bluemix_notm}} usa a ferramenta de varredura de vulnerabilidade Tenable Network Security, Nessus, para detectar problemas com configurações da rede e do host, para que os problemas possam ser resolvidos.</dd>

<dt>Gerenciamento de correção automatizada</dt>
<dd>Os administradores do {{site.data.keyword.Bluemix_notm}} asseguram que as correções para sistemas operacionais sejam aplicadas em frequências apropriadas. As correções automatizadas são ativadas usando o IBM Endpoint Manager.</dd>

<dt>Consolidação e análise do log de auditoria</dt>
<dd>{{site.data.keyword.Bluemix_notm}} usa as ferramentas IBMSecurity QRadar® para consolidar logs do Linux para monitorar o acesso privilegiado em sistemas Linux. O {{site.data.keyword.Bluemix_notm}} também utiliza informações de segurança e gerenciamento de eventos (SIEM) do IBM QRadar para monitorar tentativas de login bem-sucedidas e malsucedidas dos desenvolvedores de aplicativos.</dd>

<dt>Gerenciamento de acesso do usuário</dt>
<dd>No {{site.data.keyword.Bluemix_notm}}, as diretrizes de separação de obrigações são seguidas para designar privilégios de acesso granular aos usuários e para assegurar que os usuários tenham somente o acesso que é necessário para executar suas tarefas de acordo com o princípio do menor privilégio.

Nos ambientes do {{site.data.keyword.Bluemix_notm}} Dedicated e Local, administradores designados podem gerenciar funções e permissões para os usuários do {{site.data.keyword.Bluemix_notm}} em suas organizações usando o Console administrativo. Veja [Gerenciando o {{site.data.keyword.Bluemix_notm}}](/docs/admin/adminpublic.html#mng) para obter detalhes.
</dd>
</dl>

### Segurança física

O {{site.data.keyword.Bluemix_notm}} Public e Dedicated dependem da topologia de rede dentro uma rede do {{site.data.keyword.BluSoftlayer}} para segurança de rede física. Essa arquitetura de rede dentro de uma rede assegura que os sistemas sejam totalmente acessíveis somente à equipe autorizada. Para {{site.data.keyword.Bluemix_notm}} Local, você possui a segurança física para a instância local. Seu datacenter está assegurado sob o firewall da sua empresa.

Na rede dentro uma rede do {{site.data.keyword.BluSoftlayer}}, a camada de rede pública manipula o tráfego público para websites hospedados ou recursos on-line. A camada de rede privada permite o gerenciamento fora da banda verdadeiro por meio de uma terceira operadora distinta sobre gateways SSL, PPTP ou IPSec VPN. A camada de rede de datacenter para datacenter fornece conectividade grátis e segura entre servidores que estão hospedados em instalações separadas do {{site.data.keyword.BluSoftlayer}}.

Cada datacenter do {{site.data.keyword.BluSoftlayer}} é totalmente protegido com controles que atendem requisitos reconhecidos pelo SSAE 16 e pelo segmento de mercado, sem exceções.

## Segurança de dados
{: #data-security}

Com o {{site.data.keyword.Bluemix_notm}}, proteger seus dados contra acesso não autorizado é um trabalho em conjunto entre o {{site.data.keyword.Bluemix_notm}} e você.

Os dados associados a um aplicativo em execução podem estar em um de três estados: dados em trânsito, dados em repouso e dados em uso.

<dl>
<dt>Dados em trânsito</dt>
<dd>Dados que estão sendo transferidos entre nós em uma rede.</dd>

<dt>Dados em repouso</dt>
<dd>Dados que estão armazenados.</dd>

<dt>Dados em uso</dt>
<dd>Dados que não estão armazenados atualmente e que estão sendo aplicados em um terminal.</dd>
</dl>

Cada tipo de dados precisa ser considerado quando você planeja segurança de dados.

A plataforma {{site.data.keyword.Bluemix_notm}} protege dados em trânsito assegurando o acesso do usuário final ao aplicativo usando SSL, por meio da rede, até que os dados atinjam o IBM DataPower Gateway no limite da rede interna do {{site.data.keyword.Bluemix_notm}}. O IBM DataPower Gateway age como um proxy reverso e fornece rescisão de SSL. De lá para o aplicativo, o IPSEC é usado para proteger os dados conforme eles viajam do IBM DataPower Gateway para o aplicativo.

A segurança para dados em uso e dados em repouso é sua responsabilidade ao desenvolver o aplicativo. É possível usufruir das vantagens de vários serviços relacionados aos dados, disponíveis no catálogo do {{site.data.keyword.Bluemix_notm}} para auxiliar nessas questões.

## Segurança de aplicativos do {{site.data.keyword.Bluemix_notm}}
{: #application-security}

Como desenvolvedor de aplicativos, deve-se ativar as configurações de segurança, incluindo proteção de dados do aplicativo, para os aplicativos executados no {{site.data.keyword.Bluemix_notm}}.

É possível usar recursos de segurança que são fornecidos por vários serviços do {{site.data.keyword.Bluemix_notm}} para assegurar seus aplicativos. Todos os serviços {{site.data.keyword.Bluemix_notm}} que são produzidos pela IBM seguem as práticas de desenvolvimento de engenharia segura da IBM.

**Observação:** alguns dos serviços descritos aqui podem não se aplicar às instâncias do {{site.data.keyword.Bluemix_notm}} Dedicated ou Local.

### Serviço de SSO

IBM Single Sign On for {{site.data.keyword.Bluemix_notm}} é um serviço de autenticação baseado em política que fornece uma maneira fácil de integrar o recurso de conexão única aos aplicativos Node.js ou Liberty for Java. Para que um desenvolvedor de aplicativos integre o recurso de conexão única a um aplicativo, o administrador cria instâncias de serviço e inclui fontes de identidade.

O serviço de Single Sign On suporta várias fontes de identidade em que as credenciais dos usuários são armazenadas:

<dl>
<dt>SAML corporativo</dt>
<dd>Um registro de usuário com uma troca de tokens SAML que conclui a autenticação.</dd>

<dt>Diretório de nuvem</dt>
<dd>Um registro de usuário que é hospedado no IBM Cloud.</dd>

<dt>Fontes de identidade sociais</dt>
<dd> Os registros de usuário que são mantidos pelo Google, Facebook e LinkedIn.</dd>
</dl>

Para obter mais informações, consulte [Introdução à conexão única](/docs/services/SingleSignOn/index.html).

### Segurança do aplicativo em nuvem

Esse serviço fornece uma análise de segurança de apps móveis e da web e permite varrer o código-fonte para vulnerabilidades de segurança. Para obter mais informações, consulte [Introdução à segurança do aplicativo na nuvem](/docs/services/ApplicationSecurityonCloud/index.html).

### Plug-in do IBM UrbanCode para teste de segurança do aplicativo

O plug-in do IBM Application Security Testing for {{site.data.keyword.Bluemix_notm}} permite executar varreduras de segurança nos apps da web ou Android que estão hospedados no {{site.data.keyword.Bluemix_notm}}. Esse plug-in é desenvolvido e suportado pela Comunidade do IBM UrbanCode™ Deploy na plataforma do IBM Bluemix DevOps Services.

Para obter mais informações, acesse [IBM Application Security Testing for Bluemix ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://developer.ibm.com/urbancode/plugindoc/ibmucd/ibm-application-security-testing-bluemix/1-0/){: new_window}. 

### dashDB

O serviço dashDB usa um servidor LDAP integrado para autenticação do usuário. A conexão entre os aplicativos e o banco de dados é protegida pelos certificados SSL. Esse serviço usa o recurso de criptografia nativa do DB2® para criptografar automaticamente seu banco de dados implementado e os backups de banco de dados. A rotação da chave mestra é automática e acontece a cada 90 dias.

Para obter mais informações, consulte [Introdução ao dashDB](/docs/services/dashDB/index.html).

### Secure Gateway

O serviço Secure Gateway permite que você conecte de forma segura apps {{site.data.keyword.Bluemix_notm}} em locais remotos, no local ou na nuvem. Ele fornece conectividade segura e estabelece um túnel entre a organização do {{site.data.keyword.Bluemix_notm}} e o local remoto ao qual você deseja se conectar. É possível configurar e criar um gateway seguro usando a interface com o usuário do {{site.data.keyword.Bluemix_notm}} ou um pacote de API.

Para obter mais informações, consulte [Introdução ao Secure Gateway](/docs/services/SecureGateway/secure_gateway.html).

### Security information and event management

É possível usar ferramentas do security information and event management (SIEM) para analisar alertas de segurança em logs de aplicativos. Uma dessas ferramentas é o IBM Security QRadar&reg; SIEM, que fornece inteligência de segurança em ambientes de nuvem. Para obter informações, veja [IBM QRadar Security Intelligence Platform ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](http://www-01.ibm.com/support/knowledgecenter/SS42VS/welcome?lang=en){: new_window}.
