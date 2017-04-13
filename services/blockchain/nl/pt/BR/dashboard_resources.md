---

copyright:
  years: 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Recursos
{: #dashboard_resources}
Última atualização: 16 de março de 2017
{: .last-updated}

Esta tela contém detalhes importantes da rede e informações de status em tempo real para seus componentes de blockchain. Esses
componentes incluem o peer, a CA e o nó de ordenação. Cada componente possui quatro cabeçalhos
distintos - **Nome**, **URL**, **Status** e **Ações**.
{:shortdesc}

A **Figura 1** mostra a tela do painel inicial exibindo seus componentes de rede:

![Rede de Blockchain](images/myresources.png "Meus Recursos")
*Figura 1. Meus Recursos*

#### Nome

O cabeçalho "Nome" exibe o nome formal no nível do sistema para seu componente. Vemos que nossos componentes são
denominados `order01`, `peer01` e `ca01`.  

#### URL

O cabeçalho "URL" exibe o terminal de API para cada componente. Esses terminais são necessários para
atingir componentes de rede específicos de um aplicativo do lado do cliente e suas definições geralmente
existirão em um arquivo de configuração modelado pelo JSON que acompanha o app. Se você estiver customizando um aplicativo
que requer aprovação de peers que não fazem parte de sua Organização, será necessário recuperar esses
endereços de IP dos administradores relevantes em uma operação fora da banda. Os clientes devem ser capazes de se conectar
a quaisquer peers dos quais eles precisam de uma resposta.

#### Status

O cabeçalho "Status" exibe o estado da rede atual de cada componente (por exemplo, Em Execução ou Interrompido).

#### Ações

O cabeçalho "Ações" fornece botões para iniciar ou parar seus componentes. Ele também contém uma caixa
suspensa que se vincula aos logs de seu componente. Os logs expõem as chamadas de procedimento remoto que ocorrem
entre os vários componentes de rede e se mostram úteis para depuração e resolução de problemas. Experimente
parar um peer e tentar atingi-lo com uma transação; você verá erros de conectividade gRPC. Agora reinicie o peer e tente a transação novamente; você verá uma conexão bem-sucedida. Também
é possível deixar um peer inativo por um longo período de tempo pois seus canais continuam a transacionar. Quando o
peer for trazido de volta, você perceberá uma sincronização do livro razão por meio do protocolo gossip. Quando
o peer tiver sincronizado totalmente o livro razão, você poderá executar chamadas e consultas normais.  

#### Credenciais de Serviço

Na parte superior direita desta tela, você observará uma guia Credenciais de Serviço. Clique nessa guia para expor um
arquivo JSON que contém as informações de rede de nível inferior para cada um de seus componentes
(por exemplo, enrollID/enrollSecret para sua CA). Esta é a totalidade das informações de configuração que você
precisará para um aplicativo. Observe, no entanto, que esse arquivo contém apenas o IP do peer. Se precisar atingir
peers adicionais, será necessário obter esses terminais.   
