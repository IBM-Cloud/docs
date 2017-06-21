---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-15"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Configurando as Políticas de Segurança
{: #set_up_policies.md}

Quando um advanced security plan (ASP) é usado para uma organização, um analista de segurança pode configurar políticas de segurança de conexão e listas de bloqueio ou listas de desbloqueio. Quando um plano padrão é usado, o analista pode configurar políticas de conexão com menos opções e não pode configurar listas de bloqueio ou desbloqueio.

## Configurando políticas de conexão para segurança avançada
{: #config_connect}

É possível configurar o nível de segurança padrão que é aplicado a todos os dispositivos. É possível, então, incluir configurações de segurança customizadas para dispositivos específicos.

1. Na página **Polícias** de segurança, clique em **Configurar** ao lado de **Segurança de conexão**.
2. Em **Segurança de conexão padrão**, selecione o nível de segurança de conexão padrão na lista suspensa. O valor que você seleciona aqui é aplicado a todos os dispositivos, exceto aos dispositivos que tenham configurações de conexão customizadas. Essas políticas afetam como os dispositivos se conectam ao servidor -- eles não mudam nenhuma configuração no dispositivo real nem enviam nenhuma mensagem para o dispositivo. É possível selecionar um dos níveis de segurança a seguir como o padrão:
    - TLS opcional
    - TLS com Autenticação do Token
    - TLS com Autenticação por Certificado de Cliente
    - TLS com Autenticação do Token e Autenticação por Certificado de Cliente
    - TLS com Certificado de cliente ou Token
3. Se necessário, clique em **Incluir conexão customizada** e selecione os tipos de dispositivo e os níveis de segurança customizados. 
3. Clique em **Atualizar conformidade**. Com base no nível de segurança selecionado, a tabela atualizada mostra o número de dispositivos que são impactados e o nível previsto de conformidade no nível de segurança configurado.
4. Clique em **Salvar**.  

**Nota:**
também é possível acessar as configurações de segurança de conexão da página **Geral** em **Configurações**. Clique em **Abrir política de segurança de conexão**.

## Configurando políticas de conexão para segurança padrão
{: #config_connect}

Para organizações que usam a segurança padrão, você muda as configurações de segurança na página **Geral** em **Configurações**. É possível configurar o nível de segurança padrão que é aplicado a todos os dispositivos.

1. Em **Configurações**, selecione **Geral**.
2. Em **Segurança de conexão**, selecione o nível de segurança de conexão padrão na lista suspensa. O valor selecionado aqui é aplicado a todos os dispositivos. Essas políticas afetam como os dispositivos se conectam ao servidor -- eles não mudam nenhuma configuração no dispositivo real nem enviam nenhuma mensagem para o dispositivo. É possível selecionar um dos níveis de segurança a seguir como o padrão:
    - TLS opcional
    - TLS com Autenticação do Token
    - TLS com Autenticação do Token e Autenticação por Certificado de Cliente
4. Clique em **Salvar**.  

## Configurando listas de bloqueio e listas de desbloqueio
{: #config_black_white}

As organizações que usavam a segurança avançada podem restringir o acesso ao servidor de determinados dispositivos usando uma lista de bloqueio ou podem usar uma lista de desbloqueio para conceder acesso ao servidor a dispositivos específicos. Você pode usar uma lista de bloqueio ou uma lista de desbloqueio -- elas não podem ser usadas juntas.

### Configurar uma lista de bloqueio
{: #config_blacklist}

1. Na página **Políticas** de segurança, na seção **Lista de bloqueio**, clique em **Configurar**.
2. Na página **Lista de Bloqueio**, clique em **Incluir na Lista de Bloqueio**.
3. Na janela **Incluir na Lista de Bloqueio**, execute uma das ações a seguir:
    - Na guia **Endereço IP/Intervalo**, insira os dispositivos de endereços IP que você deseja bloquear ou os intervalos de endereços IP para vários dispositivos consecutivos.
    - Na guia **CIDR**, insira um bloco indicado Classless Inter-Domain Routing (CIDR).
    - Na guia **País**, insira ou selecione países dos quais você deseja bloquear todos os dispositivos
4. Na janela **Incluir na Lista de Bloqueio**, clique em **Salvar**.
5. Revise a lista de dispositivos bloqueados. Todos os dispositivos que fazem parte da lista, com base no endereço IP, no CIDR ou no país, não podem se conectar ao servidor {{site.data.keyword.iot_short_notm}}.
6. Clique em **Salvar**.
7. Ative a lista de bloqueio. Se você tem uma lista de desbloqueio ativada, ela se torna desativada.

### Configure uma lista de desbloqueio
{: #config_whitelist}

1. Na página **Políticas** de segurança, clique em **Configurar** ao lado de **Lista de desbloqueio**.
2. Na página **Lista de Desbloqueio**, clique em **Incluir na Lista de Desbloqueio**.
3. Na janela **Incluir na Lista de Desbloqueio**, execute uma das ações a seguir:
    - Na guia **Endereço IP/Intervalo**, insira os dispositivos de endereços IP aos quais você deseja permitir o acesso ou os intervalos de endereços IP para vários dispositivos consecutivos.
    - Na guia **CIDR**, insira um bloco indicado Classless Inter-Domain Routing (CIDR).
    - Na guia **País**, insira ou selecione países dos quais você deseja bloquear o acesso para todos os dispositivos.
4. Na janela **Incluir na Lista de Desbloqueio**, clique em **Salvar**.
5. Revise a lista de dispositivos permitidos. Todos os dispositivos que fazem parte da lista, com base no endereço IP, no CIDR ou no país, podem se conectar ao servidor {{site.data.keyword.iot_short_notm}}.
6. Clique em **Salvar**.
7. Ative a lista de desbloqueio. Se você tem uma lista de bloqueio ativada, ela se torna desativada.
