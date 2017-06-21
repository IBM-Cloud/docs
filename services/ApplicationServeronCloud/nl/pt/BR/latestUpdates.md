---

copyright:
  years: 2015, 2016
lastupdated: "2017-04-07"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Atualizações mais recentes
{: #latest_updates}

Uma lista das atualizações mais recentes para o serviço.

## 15 de março de 2017: WebSphere Application Server no {{site.data.keyword.Bluemix_notm}} atualizado

* Integrada a manutenção de serviços diversos.
* Binários do WebSphere Application Server no {{site.data.keyword.Bluemix_notm}} submetidos a upgrade, de modo que o fix pack
8.5.5.11 ou 9.0.0.3 esteja instalado com novas instâncias do Traditional WebSphere Application Server.
* [Várias vulnerabilidades de segurança](https://www-01.ibm.com/support/docview.wss?uid=swg22000587){: new_window}
abordadas no WebSphere Application Server no {{site.data.keyword.Bluemix_notm}} incluindo:
  * Uma vulnerabilidade não especificada relacionada ao componente Bibliotecas que não possui impacto de confidencialidade, alto impacto de integridade e nenhum impacto de disponibilidade.
  * Uma vulnerabilidade não especificada relacionada ao componente Bibliotecas que poderia permitir que um invasor remoto obtivesse
informações confidenciais resultando em um alto impacto de confidencialidade usando vetores de ataque desconhecidos.
  * Uma vulnerabilidade não especificada relacionada ao componente Bibliotecas que poderia permitir que um invasor remoto causasse uma negação de serviço resultando em um baixo impacto de disponibilidade usando vetores de ataque desconhecidos.
  * Uma vulnerabilidade no OpenSSL que poderia permitir que um invasor remoto obtivesse informações confidenciais, causada por um erro na cifra DES/3DES, usada como parte do protocolo SSL/TLS.
  * Uma vulnerabilidade que permite que os usuários integrem o código JavaScript arbitrário na IU da web, alterando a funcionalidade desejada, levando potencialmente à divulgação de credenciais dentro de uma sessão confiável.
  * Uma vulnerabilidade em ataques de divisão de resposta Apache HTTPD para HTTP, causada por validação imprópria da entrada fornecida pelo usuário.
  * Uma vulnerabilidade no Samba que poderia permitir que um invasor autenticado remoto obtivesse privilégios elevados no sistema, causada pela falha de manipulação da soma de verificação PAC.
  * Uma vulnerabilidade no Samba que poderia permitir que um invasor autenticado remoto obtivesse privilégios elevados no sistema,
causada pelo encaminhamento de um Chamado de concessão de chamado (TGT) a outro serviço ao usar a autenticação do Kerberos.
  * Uma vulnerabilidade no Samba para um estouro de buffer baseado em heap, causada por uma falha de quebra de número inteiro na função ndr_pull_dnsp_name().


## 10 de fevereiro de 2017: WebSphere Application Server no {{site.data.keyword.Bluemix_notm}} atualizado

* Integrada a manutenção de serviços diversos.
* Binários do WebSphere Application Server no {{site.data.keyword.Bluemix_notm}} submetidos a upgrade de modo que o fix pack
8.5.5.11 ou 9.0.0.2 esteja instalado com novas instâncias do Traditional WebSphere Application Server.
* Binários do WebSphere Application Server no {{site.data.keyword.Bluemix_notm}} submetidos a upgrade de modo que o fix pack 16.0.0.4 esteja instalado com novas instâncias do WebSphere Application Server Liberty (Planos Core e ND).
* [Várias vulnerabilidades de segurança](https://www-01.ibm.com/support/docview.wss?uid=swg21997657){: new_window} abordadas no WebSphere Application Server no {{site.data.keyword.Bluemix_notm}} incluindo:
  * Uma vulnerabilidade de negação de serviço, causada permitindo que objetos serializados de fontes não confiáveis executem e causem o consumo de recursos.
  * O uso de solicitações SOAP malformadas que poderia permitir que um invasor remoto obtivesse informações confidenciais.


## 16 de dezembro de 2016: WebSphere Application Server no {{site.data.keyword.Bluemix_notm}} atualizado

* Integrada a manutenção de serviços diversos.
* [Várias vulnerabilidades de segurança](https://www-01.ibm.com/support/docview.wss?uid=swg21995995){: new_window}
abordadas no IBM SDK Java Technology Edition que afetam o WebSphere Application Server no {{site.data.keyword.Bluemix_notm}}
incluindo:
  * Uma vulnerabilidade não especificada no Oracle Java SE e no Java SE Embedded relacionada ao componente Hotspot que possui alto impacto de confidencialidade, alto impacto de integridade e alto impacto de disponibilidade.
  * Uma vulnerabilidade não especificada no Oracle Java SE e no Java SE Embedded relacionada ao componente Networking que poderia
permitir que um invasor remoto obtivesse informações confidenciais resultando em um alto impacto de confidencialidade usando vetores de
ataque desconhecidos.
  *  Uma vulnerabilidade cross-site scripting no IBM WebSphere Application Server que permite que os usuários integrem código JavaScript arbitrário na IU da web, alterando a funcionalidade desejada, levando potencialmente à divulgação de credenciais dentro de uma sessão confiável.


## 8 de novembro de 2016: WebSphere Application Server no {{site.data.keyword.Bluemix_notm}} atualizado

* Capacidade incluída para que os clientes solicitem um endereço [IP público](networkEnvironment.html#networkEnvironment) para sua VM do WebSphere Application Server no {{site.data.keyword.Bluemix_notm}}
* [Várias vulnerabilidades de segurança](http://www-01.ibm.com/support/docview.wss?uid=swg21993842){: new_window} abordadas que afetam o WebSphere Application Server no {{site.data.keyword.Bluemix_notm}} incluindo:
  * Uma vulnerabilidade no IBM WebSphere Application Server que poderia permitir que invasores remotos executassem código Java arbitrário com um objeto serializado de fontes não confiáveis.
  * Uma vulnerabilidade de negação de serviço causada por uma leitura fora dos limites na função TS_OBJ_print_bio. Um invasor remoto poderia explorar essa vulnerabilidade usando um
arquivo de registro de data e hora criado especialmente para fazer com que o aplicativo travasse.
  * Uma potencial vulnerabilidade no OpenSSL que poderia permitir que um invasor remoto obtivesse informações confidenciais, causada por um erro no Padrão de Criptografia de Dados triplo na
cifra de bloco de 64 bits, usada como uma parte do protocolo SSL/TLS. Ao capturar grandes quantias de tráfego criptografado entre o servidor
SSL/TLS e o cliente, um invasor remoto capaz de realizar um ataque man-in-the-middle poderia explorar essa vulnerabilidade para recuperar os dados de texto simples e obter informações confidenciais. Essa vulnerabilidade é conhecida como o ataque SWEET32 Birthday.
  * O OpenSSL é vulnerável a uma negação de serviço. Ao solicitar repetidamente uma renegociação, um invasor remoto autenticado poderia enviar uma extensão da Solicitação de Status do OCSP
excessivamente grande para consumir todos os recursos de memória disponíveis.
  * O OpenSSL é vulnerável a uma negação de serviço, causada por um estouro de número inteiro na função MDC2_Update. Ao usar vetores de ataque desconhecidos, um invasor remoto poderia
explorar essa vulnerabilidade para acionar uma gravação fora dos limites e fazer com que o aplicativo travasse.
  * Uma potencial vulnerabilidade no OpenSSL que permite que um invasor remoto obtenha informações confidenciais, causada por um erro na implementação de DSA que permite seguir um caminho
de código de horário não constante para determinadas operações. Um invasor poderia explorar essa vulnerabilidade usando um ataque cache-timing para recuperar a chave DSA privada.
  * O OpenSSL é vulnerável a uma negação de serviço, causada por verificações de comprimento de mensagem ausente ao fazer a análise sintática de certificados. Um invasor remoto
autenticado poderia explorar essa vulnerabilidade para acionar uma leitura fora de limites e causar uma negação de serviço.

## 19 de setembro de 2016: WebSphere Application Server no {{site.data.keyword.Bluemix_notm}} atualizado

* Binários do WebSphere Application Server no {{site.data.keyword.Bluemix_notm}} submetidos a upgrade para que novas instâncias do WebSphere Application Server Liberty (Planos Core e ND) tenham o fix pack 16.0.0.3 instalado.
* [Várias vulnerabilidades de segurança](http://www-01.ibm.com/support/docview.wss?uid=swg21990236){: new_window} abordadas que afetam o WebSphere Application Server no {{site.data.keyword.Bluemix_notm}} incluindo:
  * Uma vulnerabilidade no IBM WebSphere Application Server Liberty que poderia permitir que um invasor remoto realizasse ataques de phishing.
  * Uma vulnerabilidade no IBM WebSphere Application Server Liberty para cross-site scripting em clientes OpenID Connect.
  * Uma potencial vulnerabilidade no IBM WebSphere Application Server Liberty que poderia permitir que um invasor remoto obtivesse informações confidenciais, causada pela manipulação
inadequada de exceções quando não existe uma página de erro padrão.
  * Uma vulnerabilidade no Apache Tomcat para uma negação de serviço, causada por um erro no componente Apache Commons FileUpload.
  * Uma vulnerabilidade no IBM WebSphere Application Server e no IBM WebSphere Application Server Liberty que poderia permitir que um invasor remoto obtivesse informações confidenciais, causada pela manipulação inadequada de respostas sob determinadas condições.
  * Uma vulnerabilidade não especificada relacionada ao componente Networking que não tem impacto de confidencialidade, com baixo impacto de integridade e nenhuma disponibilidade.

## 17 de agosto de 2016: WebSphere Application Server no {{site.data.keyword.Bluemix_notm}} atualizado

* Binários do WebSphere Application Server no Bluemix submetidos a upgrade de 8.5.5.9 a 8.5.5.10
* [Várias vulnerabilidades de segurança](http://www-01.ibm.com/support/docview.wss?uid=swg21988710){: new_window} abordadas que afetam o WebSphere Application Server no {{site.data.keyword.Bluemix_notm}} incluindo:
  * As vulnerabilidades do Apache Struts que afetam o WebSphere Application Server e o console de administração do WebSphere Application Server Hypervisor Edition.
  * Uma potencial negação de vulnerabilidade de serviço com o IBM WebSphere Application Server ao usar serviços de SIP.
  * Várias vulnerabilidades que podem afetar o IBM HTTP Server usado pelo WebSphere Application Server.
  * Uma vulnerabilidade que permite o redirecionamento do tráfego HTTP com aplicativos CGI que pode afetar o IBM HTTP Server (IHS). Essa vulnerabilidade é conhecida como "HTTPOXY".
  * Uma vulnerabilidade de divulgação de informações no IBM WebSphere Application Server.
  * Uma potencial vulnerabilidade de restrição de segurança ao efetuar bypass no IBM WebSphere Application Server que ocorre apenas em ambientes que têm ativada a propriedade customizada HttpSessionIdReuse do contêiner de web.


## 24 de junho de 2016: WebSphere Application Server no {{site.data.keyword.Bluemix_notm}} atualizado

* Incluída a capacidade para os clientes escolherem entre a V8.5 e a V9.0 quando você cria uma nova instância do *Traditional ND* ou do *Traditional WebSphere*.
* Binários do WebSphere Application Server no {{site.data.keyword.Bluemix_notm}} submetidos a upgrade de modo que novas
instâncias do WebSphere Application Server Liberty (Planos Core e ND) tenham o fix pack 16.0.0.2 instalado. 16.0.0.2 é o próximo fix pack depois de 8.5.5.9. A partir de 16.0.0.2, todos os recursos opcionais autorizados do Liberty suportados para esses planos são instalados por padrão.
* [Várias vulnerabilidades de segurança](http://www-01.ibm.com/support/docview.wss?uid=swg21984977){: new_window} abordadas que afetam o WebSphere Application Server no {{site.data.keyword.Bluemix_notm}} incluindo:
  * Uma vulnerabilidade XML External Entity Injection (XXE) no Apache Standard Taglibs que afeta o IBM WebSphere Application Server.
  * Um potencial para segurança menor que a esperada ao usar o recurso Descoberta de API do perfil Liberty do WebSphere Application Server e os documentos do Swagger.
  * Uma vulnerabilidade potencial de divulgação de informações no Admin Center do IBM WebSphere Application Server Liberty.
  * Uma vulnerabilidade potencial de divisão de resposta HTTP no IBM WebSphere Application Server.
  * Vulnerabilidades do OpenSSL divulgadas em 3 de maio de 2016 pelo Projeto OpenSSL.

## 13 de junho de 2016: WebSphere Application Server no {{site.data.keyword.Bluemix_notm}} atualizado

* Capacidade incluída para que os clientes construam, provisionem, gerenciem e excluam instâncias de máquina virtual por meio da criação de
um aplicativo ou script que use APIs RESTful do WebSphere Application Server no Bluemix.
* Incluída função que permite que um cliente tenha um número fixo de instâncias INTERROMPIDAS com não mais de 10 endereços IP ou 64 GB de memória. Agora os clientes são cobrados por instâncias acumuladas no estado INTERROMPIDO a uma taxa reduzida de 5%.

## 26 de abril de 2016: WebSphere Application Server no {{site.data.keyword.Bluemix_notm}} atualizado

* [Vulnerabilidades de segurança em potencial](http://www-01.ibm.com/support/docview.wss?uid=swg21982128){: new_window} abordadas no WebSphere Application Server no {{site.data.keyword.Bluemix_notm}} se o FIPS 140-2
estiver ativado e múltiplas vulnerabilidades no Samba - incluindo Badlock.
* Integrada a manutenção de serviços diversos.

## 15 de abril de 2016: WebSphere Application Server no {{site.data.keyword.Bluemix_notm}} atualizado

* Binários do WebSphere Application Server no {{site.data.keyword.Bluemix_notm}} submetidos a upgrade de 8.5.5.8 a 8.5.5.9
* Tratada uma vulnerabilidade [Cross-site scripting](http://www-01.ibm.com/support/docview.wss?uid=swg21981221){: new_window} no Liberty for Java para IBM {{site.data.keyword.Bluemix_notm}} que afeta consumidores que usam o cliente OpenID Connect (OIDC).
* Integrada a manutenção de serviços diversos.

## 19 de fevereiro de 2016: WebSphere Application Server no {{site.data.keyword.Bluemix_notm}} atualizado
* Incluída uma opção para clientes com aplicativos de uso intensivo de memória para "dimensionar corretamente" seu ambiente com máquinas virtuais maiores. Os clientes podem selecionar o tamanho do recurso específico de um determinado componente do WebSphere Application Server ou de um único sistema com máquinas virtuais de até 32 GB de RAM.
* Binários do WebSphere Application Server no {{site.data.keyword.Bluemix_notm}} submetidos a upgrade de 8.5.5.7 a 8.5.5.8
* Várias vulnerabilidades abordadas no IBM SDK Java Technology Edition que afetam o WebSphere Application Server no {{site.data.keyword.Bluemix_notm}} que são referenciadas comumente como [SLOTH](http://www-01.ibm.com/support/docview.wss?uid=swg21977244){: new_window}.
* Tratada uma vulnerabilidade [Cross-site scripting](http://www-01.ibm.com/support/docview.wss?uid=swg21976337){: new_window} que afeta consumidores da saída do provedor OAuth.
* Integrada a manutenção de serviços diversos.

## 11 de dezembro de 2015: WebSphere Application Server no {{site.data.keyword.Bluemix_notm}} atualizado
* Nome de produto oficial mudado de IBM Application Server on Cloud no {{site.data.keyword.Bluemix_notm}} para IBM WebSphere Application Server no {{site.data.keyword.Bluemix_notm}}
* Novas capacidades incluídas no plano do WebSphere Application Server no {{site.data.keyword.Bluemix_notm}} Network Deployment. O plano consiste em um ambiente de célula do WebSphere Application Server Network Deployment com duas ou mais máquinas virtuais. Esses novos recursos permitem que os
usuários configurem um ambiente em cluster para alta disponibilidade, failover e escalabilidade.
* Novas capacidades incluídas no plano WebSphere Application Server no {{site.data.keyword.Bluemix_notm}} Liberty Core. O plano inclui
o uso de um Liberty Collective, que é um domínio administrativo para um grupo de perfis Liberty
(servidores) e consiste em duas ou mais máquinas virtuais
* Binários do WebSphere Application Server no {{site.data.keyword.Bluemix_notm}} submetidos a upgrade de 8.5.5.6 a 8.5.5.7
* Tratada uma [vulnerabilidade do Apache Commons Collections](https://www.us-cert.gov/ncas/current-activity/2015/11/13/Apache-Commons-Collections-Java-Library-Vulnerability){: new_window} para manipular a desserialização
do objeto Java.
* Tratada uma vulnerabilidade que poderia permitir um [ataque
de divisão de resposta HTTP](http://www-01.ibm.com/support/docview.wss?uid=swg21972254){: new_window}.
* Integrada a manutenção de serviços diversos.

## 15 de outubro de 2015: Atualizado o Application Server on Cloud
* Incluídos os dois novos planos a seguir:
  * [WebSphere Application Server Traditional V9 Beta](https://www-01.ibm.com/marketing/iwm/iwmdocs/web/cc/earlyprograms/websphere.shtml){: new_window}
  * WebSphere Application Server ND
* Manutenção de serviços diversos
