---

copyright:
  years: 2015,2016

---

{:shortdesc: .shortdesc}

# Criando regras e respondendo a alertas {: #rules}

Use as regras de análise para configurar alertas e notificações para os dispositivos. Por exemplo, é possível criar uma regra que inclui um alerta para o painel do dispositivo e envia um e-mail para um administrador se o sensor de temperatura do dispositivo registrar uma temperatura anormalmente alta.
{: shortdesc}

É possível usar regras que incluem condições que comparam pontos de dados ou parâmetros de contexto, como mapeamentos de ativos com valores estáticos, outros pontos de dados parâmetros de contexto. 

>**Nota:** ao usar instâncias de plano grátis do {{site.data.keyword.iotrtinsights_short}}, todas as regras são desativadas automaticamente após uma hora. É possível reativar manualmente as regras. Para obter cobertura contínua de regras, é possível fazer upgrade para um plano pago.

Para criar uma regra para um dispositivo: 
1. No console do {{site.data.keyword.iotrtinsights_short}}, acesse **Análise > Regras**.
2. Clique em **Incluir nova regra**, forneça um nome para a regra, forneça uma descrição e selecione um esquema de mensagem para a regra e, em seguida, clique em **Avançar**.  
3. Clique em **OK** para criar a nova regra. 
3. **Opcional:** Selecione uma prioridade de alerta para a regra.
A prioridade é usada para classificar os alertas que são exibidos no painel de alertas. A prioridade padrão é Baixa. 
3. Para configurar a lógica de regra, inclua uma ou mais condições IF que são usadas como acionadores para a regra.
É possível incluir condições em linhas paralelas para aplicá-las como condições OR ou incluir condições em colunas sequenciais para aplicá-las como condições AND.
**Dica:** para conferir os valores típicos retornados por seus dispositivos, acesse **Dispositivos > Procurar dispositivos** e clique em seu dispositivo para ver os dados exibidos em tempo real. **Importante:** para acionar uma condição que compara dois pontos de dados ou para acionar duas ou mais condições de pontos de dados que são combinadas sequencialmente, os dados de acionamento devem ser incluídos na mesma mensagem. Se os dados forem recebidos em mais de uma mensagem, a condição ou condições sequenciais não serão acionadas.  
> **Exemplos:**   
Uma regra simples poderá acionar um alerta se um valor de parâmetro for maior do que um valor especificado.   
Por exemplo: Condição = `ax>5`  
Uma regra mais complexa poderá acionar um alerta se um valor de parâmetro para um dispositivo que estiver mapeado para um ativo específico exceder um valor específico.   
Por exemplo: Condição = `ax>5 AND asset.assetnum==5001`   
Para etapas detalhadas, veja [Exemplo: Criando uma regra complexa usando condições de esquema de mensagem e de parâmetro de contexto](#complex "Exemplo: Criando uma regra complexa usando condições de esquema de mensagem e de parâmetro de contexto").   
4. Configure os requisitos de acionador condicional para a sua regra.
Para controlar o número de alertas que são acionadas para uma regra durante um período de tempo, é possível configurar os requisitos de acionador condicional para a sua regra.
**Importante:** o acionamento condicional age em qualquer condição na regra. Por exemplo, se uma regra tiver 5 condições paralelas diferentes (OR) configuradas, cada condição que for verdadeira será considerada na contagem de acionadores condicionais.
Para configurar o acionamento condicional para uma regra: 
 1. No editor de regras, clique no link **Acionar cada vez que as condições forem atendidas** para abrir o diálogo de condição. 
 2. Selecione e configure o acionador condicional que você deseja usar com a regra. 
 <ul>
 <li>Acionar cada vez que as condições forem atendidas</li>
 <li>Acionar se a condições forem atendidas N vezes em *Unidade de tempo* M</li>
 </ul>  
 Para obter uma descrição mais detalhada dos acionadores condicionais, veja [Acionamento condicional](#conditional "Visão geral de acionamento condicional").
5. Crie ou selecione uma ou mais ações que ocorrem se as condições da regra forem atendidas.
Para obter mais informações sobre ações, veja [Criar ações](actions.html#shared "Criar ações").   
 > Por exemplo: uma ação pode ser para enviar um e-mail. Para obter informações sobre os diferentes tipos de ação, veja [Tipos de ação](actions.html "Tipos de ação").
6. Quando estiver satisfeito com sua regra, clique em **Salvar**. 
7. Na página Regras, clique em ![ícone Configurar](images/gear.png "ícone Configurar") e selecione **Ativar** para ativar a regra.

Sua regra está ativa. Se as condições da regra forem atendidas, um alerta será incluído no painel **Painéis > Visão geral** e qualquer ação de regra será executada. 

## Acionamento condicional {: #conditional}

Para controlar o número de alertas que são acionadas para uma regra durante um período de tempo, é possível configurar os requisitos de acionador condicional para a sua regra. 

Dependendo da frequência de mensagens e das condições da regra, uma regra poderá ser acionada um grande número de vezes quando uma condição acionadora for atendida. Por exemplo, se a condição for `temp >= 90` e a temperatura aumentar e estabilizar em 91, a regra agora será acionada com cada mensagem recebida. Dependendo da frequência das mensagens do dispositivo e das ações que a regra está configurada para executar, isso pode, por exemplo, preencher rapidamente sua caixa de entrada de e-mail ou sobrecarregar um feed do Twitter com mensagens que não fornecem nenhum valor adicional além da primeira mensagem. 

**Importante:** o acionamento condicional age em qualquer condição na regra. Por exemplo, se uma regra tiver 5 condições paralelas diferentes (OR) configuradas, cada condição que for verdadeira será considerada na contagem de acionadores condicionais. 

Condição | descrição
------------- | -------------
Acionar cada vez que as condições forem atendidas | A regra é acionada cada vez que as condições da regra são atendidas.
Acionar se as condições forem atendidas N vezes em M *dias/horas/minutos/customizado* | A regra é acionada quando as condições tiverem sido atendidas M vezes no intervalo de tempo selecionado e não é acionada novamente até que o período configurado tenha passado. </br>Exemplo: requisito de acionador condicional =`Acionar somente uma vez se as condições forem atendidas 4 vezes em 30 minutos`. O dispositivo envia uma nova mensagem a cada cinco minutos. Ao meio-dia, a temperatura excede inicialmente 90 graus, que atende à condição. O contador de acionadores condicionais é iniciado, mas a regra ainda não é acionada. Após 15 minutos e o recebimento de mais três mensagens que indicam que `temp > 90`, a regra é acionada. A regra não é acionada por outros 15 minutos, não importa qual seja a temperatura.

## Exemplo: Criando uma regra complexa usando condições de esquema de mensagem e de parâmetro de contexto {: #complex}
Para criar uma regra mais complexa que cria um alerta no Painel de alertas quando o parâmetro ax excede um valor de cinco para qualquer dispositivo IoT Phone que estiver mapeado para o número de ativo 5001, execute as etapas a seguir: 
1. Acesse **Dispositivos > Gerenciar mapeamentos de ativos** e mapeie pelo menos um dispositivo IoT Phone para um ativo com o número de ativo 5001. Para etapas detalhadas, veja [Gerenciando ativos](assets.html "Gerenciando ativos"). 
2. Acesse **Análise** e clique em **Incluir nova regra**.
3. Forneça um nome descritivo e uma descrição para a regra e especifique o tipo de dispositivo ao qual a regra se aplica, selecionando o esquema de mensagem criado para o seu tipo de dispositivo IoT Phone. 
4. Clique em **OK** para criar a nova regra. 
<!-- 5. Click ![Add icon.](images/rules_plus.png "Add icon") to add an initial condition. -->
6. Clique no novo tile de condição e edite a condição inicial. 
 1. Selecione **Ponto de dados** como o operando para comparação. 
 2. Selecione o ponto de dados **ax**. 
 3. Selecione o operador **>** para que a condição seja verdadeira se o valor do primeiro operando for maior do que valor do segundo operando.
 3. Selecione **Valor estático** como o operando para comparação. 
 4. Insira o valor `5` para comparação com o ponto de dados ax. 
 5.  Clique em **OK** para incluir a condição.
5. Para incluir a condição AND, clique em ![ícone Incluir](images/rules_plus.png "ícone Incluir") que está à direita da primeira condição. 
6. Clique no novo tile de condição e edite a condição. 
  1. Selecione **contexto** como o operando para comparação. 
  2. No menu de parâmetro de contexto, clique no triângulo na frente do esquema de contexto **ativos** para expandir a lista de parâmetros de contexto do ativo. 
  3. Selecione o parâmetro de esquema de contexto **ASSETNUM**.
  3. Selecione o operador **==** para que a condição seja verdadeira se os valores do primeiro e segundo operandos forem iguais. 
  3. Selecione **Valor estático** como o operando para comparação. 
  4. Insira `5001` como o valor para comparação com o parâmetro de esquema de contexto **ASSETNUM**. 
  5.  Clique em **OK** para criar a condição. 
7. Use o acionador condicional padrão `Acionar cada vez que as condições forem atendidas`.
7. Crie ou selecione uma ou mais ações. 
7. Salve a nova regra.
7. Na página Regras, no novo tile de regra, clique em ![ícone Configurar](images/gear.png "ícone Configurar") e selecione **Ativar** para ativar a regra.

## Exemplo: Criando regras baseadas em ativos {: #asset_rules}

Depois de ter mapeado seus dispositivos para ativos com sucesso, é possível criar regras que usam os detalhes do ativo. O mapeamento de dispositivos para ativos e a criação de regras que incorporam pontos de dados e informações de ativos são uma ferramenta poderosa.

Nos exemplos a seguir, estamos usando os ativos para controlar nossos telefones celulares corporativos. Dois ativos foram criados e mapeados para telefones celulares. O ativo 5001 é mapeado para telefones com PURCHASEPRICE < 100 e o ativo 5002 para telefones com PURCHASEPRICE >=100. A condição acionadora de dados do dispositivo para cada exemplo é `d.ax>5`, que neste exemplo simplificado corresponde a uma aceleração súbita do telefone, por exemplo, se ele for eliminado. 

Agora é possível configurar duas regras simples que dizem-nos quando um telefone que está mapeado para o ativo 5001 foi eliminado. Também é igualmente fácil configurar uma regra que controla quando um telefone que não está mapeado para 5001 é eliminado. Isso pode ser qualquer telefone em 5002 ou qualquer telefone que não esteja mapeado para um ativo. 

Por exemplo: | Regra
------------- | -------------
Acionar regra somente se o dispositivo fizer parte do ativo 5001 | IF `d.ax>5` AND  `asset.assetnum==5001` THEN ...
Acionar regra somente se o dispositivo NÃO fizer parte do ativo 5001 | IF `d.ax>5` AND  `asset.assetnum!=5001` THEN ...

Também é possível configurar regras que são acionadas para telefones com um determinado PURCHASEPRICE.   

Por exemplo: | Regra
------------- | -------------
Acionar regra somente se o telefone custar menos que 100 | IF `d.ax>5` AND  `asset.purchaseprice<100` THEN ...
Acionar regra somente se o telefone custar mais que 100 | IF `d.ax>5` AND  `asset.purchaseprice>=100` THEN ...

E, por fim, é possível combinar estas regras para comportamento mais complexo. 

Por exemplo: | Regra
------------- | -------------
Acionar regra somente se o telefone fizer parte do ativo 5001 (custa menos que 100), mas custa mais que 75 | IF `d.ax>5` AND `asset.assetnum==5001` AND  `asset.purchaseprice>75` THEN ...
Acionar regra somente se o telefone fizer parte do ativo 5002 (custa mais que 100), mas custa menos que 75 | IF `d.ax>5`  AND `asset.assetnum==5002` AND  `asset.purchaseprice<200` THEN ...
