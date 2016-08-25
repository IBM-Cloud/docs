---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Administrando o Driving Behavior Analysis
{: #1stanchor}
Última atualização: 19 de junho de 2016
{: .last-updated}

Administre a instância de serviço {{site.data.keyword.iotdriverinsights_full}} usando o console de administração no painel do {{site.data.keyword.Bluemix_notm}}. No console de administração, é possível configurar parâmetros para o {{site.data.keyword.iotdriverinsights_short}} e gerenciar os dados armazenados no serviço. Também é possível visualizar as informações do locatário e reconfigurar a senha do locatário.

{:shortdesc}

## Iniciando o console de administração
{: #start-admin-console}

Para acessar o console de administração do serviço {{site.data.keyword.iotdriverinsights_short}}:

1. No painel do {{site.data.keyword.Bluemix_notm}}, clique no quadro do serviço {{site.data.keyword.iotdriverinsights_short}}.
2. Selecione a visualização **Gerenciar** de sua instância de serviço.
Anote as credenciais de *Nome do usuário* e *Senha*. Para acessar o console de administração, seu ID IBM será necessário, que pode não ser o mesmo de suas credenciais do {{site.data.keyword.Bluemix_notm}}.
3. Clique em **Ativar** e, quando solicitado, insira suas credenciais de ID IBM.
4. Clique em **EFETUAR LOGIN**. O **Console do administrador** é aberto em uma nova janela.

## Gerenciando informações do locatário
{: #viewtenantinfo}

Para visualizar as informações do locatário, clique em **Informações do locatário**.

### Reconfigurando a senha do locatário
{: #resettenantpassword}

Para reconfigurar a senha do locatário:

1. Na janela **Informações do locatário**, clique em **RECONFIGURAR**.
2. Na caixa de diálogo de confirmação, clique em **OK**.
Uma nova senha é gerada e exibida na visualização **Informações do locatário**.
**Importante:** certifique-se de atualizar a senha em todos os aplicativos que acessam a API do {{site.data.keyword.iotdriverinsights_short}}.

## Configurando os parâmetros de serviço
{: #configureparameters}

Os parâmetros de serviço controlam o modo de análise dos dados da viagem. Para modificar os parâmetros de serviço:

1. Abra a visualização **Parâmetros** e ajuste os parâmetros de serviço a seguir, conforme necessário:
  - Clique na guia **Comportamento** e atualize os [parâmetros de comportamento de condução](#behavior_parameters) para se adequarem a seus requisitos.
  - Clique na guia **Contexto** e atualize os [parâmetros de mapeamento de contexto](#context_parameters) para se adequarem a seus requisitos.
2. Clique em **SALVAR**.
3. Clique em **OK**.

Os valores de parâmetro atualizados serão aplicados à próxima tarefa que for enviada.

### Parâmetros de comportamento de condução
{: #behavior_parameters}

As tabelas a seguir descrevem os parâmetros de comportamento de condução das categorias que podem ser configuradas na guia **Comportamento**.

#### Configurações de limite de velocidade

É possível especificar o limite de velocidade em km/h para cada tipo de estrada. Se a velocidade exceder o valor limite de velocidade especificado para o tipo de estrada, o excesso de velocidade será detectado.

|Nome do parâmetro|Description|Valor padrão (km/h)|
|:--------|:--------|:-------|
|Pista Expressa|Limite de velocidade para um tipo de estrada pista expressa|120|
|Rodovia Urbana|Limite de velocidade para um tipo de estrada rodovia urbana|90|
|Principal Urbana|Limite de velocidade para um tipo de estrada principal urbana|60|
|Estrada Urbana|Limite de velocidade para um tipo de estrada urbana|40|
|Outros|Limite de velocidade para um tipo de estrada classificado como 'Outros'|30|
|Descon.|Limite de velocidade para tipos de estrada desconhecidos|120|

#### Configurações de curvas

|Nome do parâmetro|Description|Valor Padrão|
|:--------|:--------|:-------|
|Velocidade Angular (Mín. \- Máx., graus/s)|Valor da velocidade angular normal de uma curva. O valor Min é usado como um limite para identificar o segmento de curva. O valor
Max é usado para detectar o comportamento de curva acentuada.|10 \- 25|
|Velocidade Média (km/h)|Velocidade normal durante uma curva. Esse valor é usado para identificar comportamentos em um segmento de curva que possui valores de velocidade angulares.|60|

#### Configurações de condução com fadiga

|Nome do parâmetro|Description|Valor Padrão|
|:--------|:--------|:-------|
|Tempo de Condução(ões) Contínua(s)|A extensão máxima de condução contínua permitida.|10800|


### Parâmetros de mapeamento de contexto
{: #context_parameters}

As tabelas a seguir descrevem os parâmetros de mapeamento de contexto das categorias que podem ser configuradas na guia **Contexto**.

#### Configurações de fuso horário e de intervalo de tempo

Especifique o fuso horário e as horas de cada período.

|Nome do parâmetro|Description|Valor Padrão|
|:--------|:--------|:-------|
|Fuso horário da análise|Fuso horário aplicado para análise. |+00:00|
|Horário do Dia|Intervalo de tempo do horário do dia.|1030 \- 1730|
|À Noite|Intervalo de tempo à noite.|2030 \- 0700|
|Pico da Manhã|Intervalo de tempo do horário de pico da manhã.|0700 \- 1030|
|Pico da Tarde|Intervalo de tempo do horário de pico da tarde.|1730 \- 2030|

#### Tipos de estrada

Os parâmetros de tipos de estrada são usados para mapear os valores de tipo de estrada de seus dados de entrada para as classificações de tipo de estrada do {{site.data.keyword.iot4auto_short}}. Se você não tiver um valor de tipo de estrada, será possível recuperá-lo usando a API REST "getLinkInformation", que é fornecida pelo "{{site.data.keyword.iotmapinsights_short}}".

 O valor de tipo de estrada é armazenado em "propriedades > tipo" na resposta. Para obter um exemplo que mostra a posição de "tipo" na resposta, consulte [Resposta JSON de amostra para `getLinkInformation`](#sampleJson).

 |Nome do parâmetro|Description|Valor Padrão|
 |:--------|:--------|:-------|
|Pista Expressa|Valor de tipo de estrada que é mapeado para Pista expressa.|1|
|Rodovia Urbana|Valor de tipo de estrada que é mapeado para Rodovia urbana.|2|
|Principal Urbana|Valor de tipo de estrada que é mapeado para Principal urbana.|3|
|Estrada Urbana|Valor de tipo de estrada que é mapeado para Estrada urbana.|4|
|Outros|Valor de tipo de estrada que é mapeado para Outros.|5|

#### Limite de velocidade

Os parâmetros de limite de velocidade definem o intervalo de velocidade média para cada tipo de estrada em km/h. O intervalo de velocidade média é o intervalo entre os valores mais baixos e mais altos especificados.

|Nome do parâmetro|Description|Valor Padrão|
|:--------|:--------|:-------|
|Pista Expressa|Intervalo de velocidade média para o tipo de estrada Pista expressa.|55 \- 85|
|Rodovia Urbana|Intervalo de velocidade média para o tipo de estrada Rodovia urbana.|35 \- 65|
|Principal Urbana|Intervalo de velocidade média para o tipo de estrada Principal urbana.|20 \- 40|
|Estrada Urbana|Intervalo de velocidade média para o tipo de estrada Estrada urbana.|15 \- 35|
|Outros|Intervalo de velocidade média para o tipo de estrada Outros.|10 \- 20|
|Descon.|Intervalo de velocidade média para o tipo de estrada Desconhecido.|20 \- 60|

### Resposta do JSON de Amostra da API REST "getLinkInformation"
{: #sampleJson}

```
{
	"links": [{
		"internal_link_id": "32088220365736308",
		"external_link_id": "3846419005",
		...
		"properties": {
			"type": "5",
			...
		},
		...
	}]
}
```
{: screen}


## Gerenciando dados armazenados no serviço
{: #managedata}

Os dados de análise do carro, os dados de contexto e os resultados da análise são armazenados no serviço até que sejam excluídos.

Para excluir os dados armazenados no serviço:

1. Clique em **Gerenciamento de dados** para visualizar os dados de análise do carro e os dados de resultado da análise.
2. Selecione um registro e, em seguida, no registro, clique em **EXCLUIR**.
