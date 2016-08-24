---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Administrando o {{site.data.keyword.iot4auto_short}}
{: #1stanchor}
Última atualização: 29 de julho de 2016
{: .last-updated}

Administre sua instância de serviço do {{site.data.keyword.iot4auto_full}} usando o console de administração no painel do {{site.data.keyword.Bluemix_notm}}. No console de administração, é possível configurar parâmetros para o {{site.data.keyword.iot4auto_short}} e gerenciar os dados que são armazenados no serviço. Também é possível visualizar as informações do locatário e reconfigurar a senha do locatário.

{:shortdesc}

## Iniciando o console de administração
{: #start_admin_console}

Para acessar o console de administração do serviço do {{site.data.keyword.iot4auto_short}}:

1. No painel do {{site.data.keyword.Bluemix_notm}}, clique no título do serviço do {{site.data.keyword.iot4auto_short}}.
2. Selecione a visualização **Gerenciar** de sua instância de serviço.
Como eles serão necessários mais tarde, anote o nome do usuário e as credenciais de senha. Para acessar o console de administração, é necessário o seu ID IBM, que pode não ser o mesmo que suas credenciais do {{site.data.keyword.Bluemix_notm}}.
3. Clique em **Ativar** e, quando solicitado, insira suas credenciais do ID IBM.
4. Clique eme **EFETUAR LOGIN**. A janela do **Console administrativo** será aberta.

## Gerenciando informações do locatário
{: #view_tenant_info}

Para visualizar informações do locatário, clique em **Informações do locatário**.

### Reconfigurando a senha do locatário
{: #reset_tenant_password}

Para reconfigurar a senha do locatário:

1. Na janela **Informações do locatário**, clique em **RECONFIGURAR**.
2. Na caixa de diálogo, clique em **OK**.
Uma nova senha é gerada e exibida na visualização **Informações do locatário**.  
**Importante:** certifique-se de atualizar a senha em todos os seus aplicativos que acessam a API do {{site.data.keyword.iot4auto_short}}.

## Configurando os parâmetros de serviço
{: #configure_parameters}

Os parâmetros de serviço controlam como os dados da viagem são analisados. Para modificar os parâmetros de serviço:

1. Abra a visualização **Parâmetros** e ajuste os parâmetros de serviço a seguir:
  - Clique na guia **Comportamento** e atualize os [parâmetros de comportamento de direção](#behavior_parameters) para atender aos seus requisitos.
  - Clique na guia **Contexto** e atualize os [parâmetros de mapeamento de contexto](#context_parameters) para atender aos seus requisitos.
2. Clique em **SALVAR**.
3. Clique em **OK**.

Os valores de parâmetro atualizados são aplicados na próxima tarefa que é enviada.

### Parâmetros de comportamento de direção
{: #behavior_parameters}


As tabelas a seguir descrevem os parâmetros de comportamento de direção para as categorias que podem ser configuradas na guia **Comportamento**.

#### Configurações de alta velocidade

É possível especificar o limite de velocidade em km/h para cada tipo de estrada. Se a velocidade exceder o valor limite de velocidade especificado para o tipo de estrada, o excesso de velocidade será detectado.

|Nome de Parâmetro|Descrição|Valor padrão (km/h)|
|:--------|:--------|:-------|
|Pista Expressa|Limite de velocidade para um tipo de estrada de pista expressa|120|
|Rodovia Urbana|Limite de velocidade para um tipo de estrada de rodovia urbana|90|
|Principal Urbana|Limite de velocidade para um tipo de estrada de rodovia principal urbana|60|
|Estrada Urbana|Limite de velocidade para um tipo de estrada urbana|40|
|Outros|Limite de velocidade para um tipo de estrada que é classificado como 'Outros'|30|
|Descon.|Limite de velocidade para tipos de estrada desconhecidos|120|
*Tabela 1. Parâmetros de configuração de limite de velocidade*
#### Configurações de curva

|Nome de Parâmetro|Descrição|Valor-padrão|
|:--------|:--------|:-------|
|Velocidade Angular (Mín. \- Máx., graus/s)|Valor da velocidade angular normal de uma curva. O valor Min é usado como um limite para identificar o segmento de curva. O valor
Max é usado para detectar um comportamento de curva acentuada.|10 \- 25|
|Velocidade Média (km/h)|Velocidade normal durante uma curva. Este valor é usado para identificar comportamentos em um segmento de curva que possui valores de velocidade angular.|60|
*Tabela 2. Parâmetros de configuração de curva do veículo*

#### Configurações de condução em fadiga

|Nome de Parâmetro|Descrição|Valor-padrão|
|:--------|:--------|:-------|
|Tempo de Condução(ões) Contínua(s)|O comprimento máximo de condução contínua que é permitido.|10800|
*Tabela 3. Parâmetros de configuração de detecção de condução em fadiga*
### Parâmetros de mapeamento de contexto
{: #context_parameters}

As tabelas a seguir descrevem os parâmetros de mapeamento de contexto para as categorias que podem ser configuradas na guia **Contexto**.

#### Configurações de fuso horário e intervalo de tempo

Especifique o fuso horário e as horas para cada período.

|Nome de Parâmetro|Descrição|Valor-padrão|
|:--------|:--------|:-------|
|Fuso horário da análise|Fuso horário aplicado para a análise. |+00:00|
|Horário do Dia|Intervalo de tempo do horário diurno.|1030 \- 1730|
|À Noite|Intervalo de tempo do horário noturno.|2030 \- 0700|
|Pico da Manhã|Intervalo de tempo do horário de pico da manhã.|0700 \- 1030|
|Pico da Tarde|Intervalo de tempo do horário de pico da noite.|1730 \- 2030|
*Tabela 4. Parâmetros de configuração de fuso horário e intervalo de tempo*
#### Tipos de estradas

Os parâmetros de tipos de estradas são usados para mapear os valores de tipo de estrada de seus dados de entrada para as classificações de tipo de estrada do {{site.data.keyword.iot4auto_short}}. Se você não tiver um valor de tipo de estrada, será possível recuperar o valor de tipo de estrada usando o comando de API REST `getLinkInformation` que é fornecido pelo serviço do {{site.data.keyword.iotmapinsights_short}}.

O valor de tipo de estrada é retornado e armazenado na seção de propriedades da resposta JSON `getLinkInformation` e é definido como `type`, conforme descrito na [resposta JSON de amostra para `getLinkInformation`](#sampleJson).


|Nome de Parâmetro|Descrição|Valor-padrão|
|:--------|:--------|:-------|
|Pista Expressa|Valor de tipo de estrada que é mapeado para Pista Expressa.|1|
|Rodovia Urbana|Valor de tipo de estrada que é mapeado para Rodovia Urbana.|2|
|Principal Urbana|Valor de tipo de estrada que é mapeado para Principal Urbana.|3|
|Estrada Urbana|Valor de tipo de estrada que é mapeado para Estrada Urbana.|4|
|Outros|Valor de tipo de estrada que é mapeado para Outros.|5|
*Tabela 5. Parâmetros de configuração de tipo de estrada*

#### Limite de velocidade

Os parâmetros de limite de velocidade definem o intervalo de velocidade média para cada tipo de estrada em km/h. O intervalo de velocidade média é o intervalo entre os valores mínimo e máximo que são especificados.

|Nome de Parâmetro|Descrição|Valor-padrão|
|:--------|:--------|:-------|
|Pista Expressa|Intervalo de velocidade média para o tipo de estrada de Pista Expressa.|55 \- 85|
|Rodovia Urbana|Intervalo de velocidade média para o tipo de estrada de Rodovia Urbana.|35 \- 65|
|Principal Urbana|Intervalo de velocidade média para o tipo de estrada de Principal Urbana.|20 \- 40|
|Estrada Urbana|Intervalo de velocidade média para o tipo de estrada de Estrada Urbana.|15 \- 35|
|Outros|Intervalo de velocidade média para o tipo de estrada Outros.|10 \- 20|
|Descon.|Intervalo de velocidade média para o tipo de estrada Desconhecido.|20 \- 60|
*Tabela 6. Parâmetros de configuração de limite de velocidade*


### Resposta JSON de amostra para `getLinkInformation`
{: #sampleJson}

A amostra de código a seguir fornece um exemplo de uma resposta JSON para o comando de API REST `getLinkInformation`:

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

## Excluindo dados que estão armazenados no serviço
{: #managedata}

Os dados de análise do veículo, os dados de contexto e os resultados da análise são armazenados no serviço até que sejam excluídos.

Para excluir os dados que estão armazenados no serviço:

1. Para visualizar os dados de análise do veículo e de resultado da análise, clique em **Gerenciamento de dados**.
2. Selecione um registro e, em seguida, clique em **EXCLUIR**.
