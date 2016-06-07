---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Administrando o {{site.data.keyword.iotdriverinsights_short}}
{: #1stanchor}
*Última atualização: 6 de maio de 2016*


A administração do {{site.data.keyword.iotdriverinsights_full}} inclui visualizar
informações do locatário e reconfigurar a senha do locatário, configurar os parâmetros para o serviço e gerenciar dados armazenados no serviço.
{:shortdesc}

É possível executar tarefas de administração usando o {{site.data.keyword.iotdriverinsights_full}} Administration Console (Console Administrativo).

Para acessar o Console Administrativo:

1. Acesse a visualização **Gerenciar** de sua instância de serviço.
2. Clique em **Ativar**. O **Console Administrativo** é aberto como uma nova janela.
3. Insira o *nome do usuário* e a *senha* conforme mostrado
na visualização **Gerenciar**, em seguida, clique em **LOGIN**.

## Visualizando informações do locatário
{: #viewtenantinfo}

Após fazer login no **Console Administrativo**, é possível ver a
visualização **Informações do Locatário** e as informações do locatário.

## Reconfigurando a senha do locatário
{: #resettenantpassword}

Na visualização **Informações do Locatário**, 

1. Clique em **RECONFIGURAR**.
2. No diálogo de confirmação, clique em **OK**.
Em seguida, a nova senha será mostrada na visualização **Informações do Locatário**

## Configurando parâmetros para o serviço
{: #configureparameters}

Clique em **Parâmetros** na área de janela de navegação. A visualização **Parâmetros** e os parâmetros são exibidos.

É possível editar os parâmetros para modificar os resultados da análise.

A tabela a seguir descreve os parâmetros de comportamento:

|Category|Nome do Parâmetro|Description|Valor
Padrão|
|:-------:|:--------:|:--------|:-------:|
|Limite de Velocidade (km/h)|\-|Limite de velocidade para tipo de estrada. Se a velocidade do veículo exceder este valor na estrada de cada tipo, o serviço o identifica como em excesso de velocidade.|\-|
|Limite de Velocidade (km/h)|Pista Expressa|Limite de velocidade para Pista Expressa|120|
|Limite de Velocidade (km/h)|Rodovia Urbana|Limite de velocidade para Rodovia Urbana|90|
|Limite de Velocidade (km/h)|Principal Urbana|Limite de velocidade para Principal Urbana|60|
|Limite de Velocidade (km/h)|Estrada Urbana|Limite de velocidade para Estrada Urbana|40|
|Limite de Velocidade (km/h)|Outros|Limite de velocidade para Outros|30|
|Limite de Velocidade (km/h)|Descon.|Limite de velocidade para Desconhecido|120|
|Curva|Velocidade Angular (Mín. \- Máx., graus/s)|Valor da velocidade angular normal em curva. O valor mín. é usado como limite para identificar o segmento de curva. O valor máx. é usado para detectar o comportamento de curva acentuada.|10 \- 25|
|Curva|Velocidade Média (km/h)|Velocidade normal durante a curva. Este valor é usado para identificar comportamentos no segmento de curva em conjunto com valores de Velocidade Angular.|60|
|Condução com Fadiga|Tempo de Condução(ões) Contínua(s)|Se um veículo for conduzido continuamente além deste valor, o serviço o identificará como "Condução com Fatiga".|10800|

A tabela a seguir descreve os parâmetros de contexto:

|Category|Nome do Parâmetro|Description|Valor
Padrão|
|:-------:|:--------:|:--------|:-------:|
|Fuso Horário da Análise|\-|Fuso horário aplicado para análise |+00:00|
|Intervalo de horas|\-|Este valor define o tipo de período de tempo.|\-|
|Intervalo de horas|Horário do Dia|Intervalo de horas do horário do dia|1030 \- 1730|
|Intervalo de horas|À Noite|Intervalo de horas do horário noturno|2030 \- 0700|
|Intervalo de horas|Pico da Manhã|Intervalo de horas do horário de pico da manhã|0700 \- 1030|
|Intervalo de horas|Pico da Tarde|Intervalo de horas do horário de pico da tarde|1730 \- 2030|
|Tipo de Estrada|\-|Estes valores são usados para mapear o valor de tipo de estrada do usuário
para classificações de tipo de estrada exclusivas do {{site.data.keyword.iotdriverinsights_short}}. Se você não tiver um valor de Tipo de Estrada, será possível recuperar o valor de Tipo de Estrada usando a API REST `getLinkInformation`, que é fornecida pelo **{{site.data.keyword.iotmapinsights_short}}**. O valor de tipo de estrada é armazenado em **propriedades > tipo** na resposta. [JSON de amostra](#sampleJson) representa a posição do `tipo` na resposta.|\-|
|Tipo de Estrada|Pista Expressa|Mapa de valores do tipo de estrada para Pista Expressa|1|
|Tipo de Estrada|Rodovia Urbana|Mapa de valores do tipo de estrada para Rodovia Urbana|2|
|Tipo de Estrada|Principal Urbana|Mapa de valores do tipo de estrada para Principal Urbana|3|
|Tipo de Estrada|Estrada Urbana|Mapa de valores do tipo de estrada para Estrada Urbana|4|
|Tipo de Estrada|Outros|Mapa de valores do tipo de estrada para Outros|5|
|Limite de Velocidade (Baixa \- Alta, km/h)|\-|Este valor define o intervalo de velocidade média para cada tipo de estrada.|\-|
|Limite de Velocidade (Baixa \- Alta, km/h)|Pista Expressa|Intervalo de velocidade média para Pista Expressa|55 \- 85|
|Limite de Velocidade (Baixa \- Alta, km/h)|Rodovia Urbana|Intervalo de velocidade média para Rodovia Urbana|35 \- 65|
|Limite de Velocidade (Baixa \- Alta, km/h)|Principal Urbana|Intervalo de velocidade média para Principal Urbana|20 \- 40|
|Limite de Velocidade (Baixa \- Alta, km/h)|Estrada Urbana|Intervalo de velocidade média para Estrada Urbana|15 \- 35|
|Limite de Velocidade (Baixa \- Alta, km/h)|Outros|Intervalo de velocidade média para Outros|10 \- 20|
|Limite de Velocidade (Baixa \- Alta, km/h)|Descon.|Intervalo de velocidade média para Desconhecido|20 \- 60|


Para aplicar mudanças nos parâmetros:

1. Clique em **SALVAR**. 
2. No diálogo de confirmação, clique em **OK**.

Em seguida, novos parâmetros são aplicados e tornam-se efetivos para a próxima tarefa enviada.

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

- Clique em **Gerenciamento de dados** na área de janela de navegação. É possível ver a visualização **Gerenciamento de dados** e os dados de análise do carro e de resultado da análise.
- É possível excluir dados ao clicar em **EXCLUIR** em um registro.
