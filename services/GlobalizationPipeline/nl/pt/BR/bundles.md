---

copyright:
  years: 2015, 2017
lastupdated: "2016-08-30"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Trabalhando com pacotes configuráveis
{: #globalizationpipeline_workingwithbundles}


Cada pacote configurável que você cria contém os pares de valores de chave de seu arquivo de recursos e o conjunto completo de traduções que foram geradas.
{:shortdesc}

Os arquivos de recursos que você faz upload podem ser de qualquer um dos formatos a seguir e devem ter conteúdo na forma de pares de chave/valor que representem as sequências da IU do seu app.


* Tipo de arquivo: *Arquivos de propriedade Java™ (.properties)*<br>
Exemplo:
```js
logout=Logout
back=Back
examples=Menu
home=Home
web=Web
enterprise=Enterprise
extra=Resources
about=About
settings=Settings
help=Help
support=Support
topics=Topics
appExitMsg=Tem certeza de que deseja sair do aplicativo?
```
* Tipo de arquivo: *AMD I18N (.js)*<br>
Exemplo:
```js
define({
    "root": {
       logout: "Efetuar logout",
       back: "Voltar",
       examples: "Menu",
       home: "Início",
       web: "Web",
       enterprise: "Corporativo",
       extra: "Recursos",
       about: "Sobre",
       settings: "Configurações",
       help: "Ajuda",
       support: "Suporte",
       topics: "Tópicos",
       appExitMsg: "Tem certeza de que deseja sair do aplicativo?"
    }
});
``` 
* Tipo de arquivo: *JSON (.json)*<br>
Exemplo:
```js
{
  "logout": "Efetuar logout",
  "back": "Voltar",
  "examples": "Menu",
  "home": "Início",
  "web": "Web",
  "enterprise": "Corporativo",
  "extra": "Recursos",
  "about": "Sobre",
  "settings": "Configurações",
  "help": "Ajuda",
  "support": "Suporte",
  "topics": "Tópicos",
  "appExitMsg": "Tem certeza de que deseja sair do aplicativo?"
}
``` 

Além disso, um arquivo de recursos também deve seguir estas diretrizes:
* Cada chave pode ter no máximo 255 caracteres.
* Cada valor pode ter no máximo 8191 caracteres.
* Cada pacote configurável pode ter no máximo 500 pares de chave/valor.


## Traduzindo um pacote configurável
{: #globalizationpipeline_translatingabundle}

Somente arquivos de recursos transferidos por upload serão traduzidos. É possível fazer upload de um arquivo de recursos ao [criar um pacote configurável](index.html#globalizationpipeline_creatingbundles) ou [modificar com detalhes do pacote configurável](bundles.html#globalizationpipeline_modifyingbundles).

Depois de fazer upload de um arquivo de recursos, é possível traduzir seu conteúdo
em qualquer idioma fornecido pelo mecanismo de tradução de máquina padrão. Como
opção, é possível escolher um mecanismo de tradução de máquina alternativo, conforme
descrito na seção
[Configuração
de tradução de máquina](managing_translations.html#globalizationpipeline_service_to_service). O mecanismo padrão suporta os idiomas de destino a seguir

<table>
<thead>
<tr>
<th>Idiomas de destino</th>
</tr>
</thead>
<tbody>
<tr>
<td>Chinês (Simplificado)</td>
</tr>
<tr>
<td>Chinês (Tradicional)</td>
</tr>
<tr>
<td>French</td>
</tr>
<tr>
<td>Alemanha</td>
</tr>
<tr>
<td>Italiano</td>
</tr>
<tr>
<td>japonês</td>
</tr>
<tr>
<td>Korean</td>
</tr>
<tr>
<td>Português do Brasil</td>
</tr>
<tr>
<td>Espanhol</td>
</tr>
</tbody>
</table>

**Nota:** o mecanismo de tradução de máquina padrão do {{site.data.keyword.GlobalizationPipeline_short}} só fornece suporte para inglês como um idioma de origem. Entretanto,
mecanismos de tradução de máquina alternativos disponíveis para configuração no {{site.data.keyword.GlobalizationPipeline_short}} suportam a tradução de outros idiomas de origem/pares de
idiomas não inglês.

À medida que você cria pacotes configuráveis, eles são incluídos na guia
**Pacotes configuráveis** para torná-los facilmente acessíveis. De lá,
tarefas adicionais podem ser executadas em suas traduções.


## Selecionando um pacote configurável com o qual trabalhar
{: #globalizationpipeline_selectingabundle}

1. Clique na guia **Pacotes configuráveis** para visualizar todos os pacotes configuráveis que você criou.
2. Clique em um **ID de pacote configurável** na lista para ver mais detalhes sobre esse pacote configurável ou clique no ícone **Visualizar os detalhes dos pacotes configuráveis** ![Selecione o ícone Visualizar os detalhes dos pacotes configuráveis para abrir um pacote configurável e trabalhar com suas traduções](images/viewProjectDetailIcon.png) na coluna Ações.

![Visualize todos os pacotes configuráveis disponíveis na guia Pacotes configuráveis.](images/translationBundles.png)

Depois de selecionar um pacote configurável com o qual trabalhar, será possível visualizar o status de suas traduções, incluir ou remover idiomas, editar as traduções ou fornecer atualizações para o arquivo de recursos.

Se você não precisar mais de um pacote configurável, será possível excluí-lo na
guia **Pacotes configuráveis**. Todas as traduções associadas ao
pacote configurável também são excluídas.

## Modificando detalhes do pacote configurável
{: #globalizationpipeline_modifyingbundles}

Ao abrir um pacote configurável, é possível visualizar todos os detalhes sobre ele. Todos os idiomas de destino que estiverem no pacote configurável serão listados, com o status de tradução atual de cada um.

![A página de detalhes do pacote configurável mostra informações sobre um pacote configurável e suas traduções.](images/bundleDetails.png)

O status de cada idioma no pacote configurável pode ser Em andamento, Com falha ou Traduzido:

| Barra de Status | Descri‡Æo |
|--------|-------------|
| Em Progresso | A tradução de máquina ainda está em andamento. |
| Reprovado | Ocorreu um erro enquanto o arquivo de recursos estava sendo traduzido para o idioma de destino. |
| Translated | A tradução para o idioma de destino está concluída. |

É possível atualizar o arquivo de recursos que o pacote configurável usa, incluir
um idioma de destino em um pacote configurável, excluir um idioma de destino de um pacote
configurável e fazer download das traduções geradas para um idioma de destino.

### Atualizando o arquivo de recursos usado pelo pacote configurável

1. Ao lado do idioma de origem, clique no ícone **Fazer upload de recursos** ![Selecione este ícone para fazer upload de um novo arquivo de recursos](images/uploadIcon.png) na coluna Ações.
2. Clique em **Procurar** e selecione o novo arquivo de recursos a ser transferido por upload.
3. Selecione o tipo de arquivo de recursos que você está fazendo upload
 * Arquivo de propriedades Java
 * AMD I18N
 * JSON
4. Clique em **Atualizar** para fazer upload do novo arquivo de recursos.

Os pares de chave/valor que estão no arquivo de recursos novo ou atualizado são
sincronizados com os valores que já foram transferidos por upload. Somente o conteúdo
novo ou mudado será traduzido.

### Incluindo um idioma de destino em um pacote configurável

1. Clique no botão **Incluir idioma**.
2. Todos os idiomas de destino disponíveis são mostrados. Selecione os idiomas a serem incluídos no pacote configurável.

A tradução para os idiomas selecionados será iniciada imediatamente.

### Excluindo um idioma de destino de um pacote configurável

Ao excluir um idioma de destino de um pacote configurável, você remove o idioma de
destino e todas as traduções associadas do projeto. Na coluna Ações do idioma de destino
a ser removido, clique no ícone **Remover este idioma de destino**
![Selecione o ícone de lixeira Remover este idioma de
destino](images/trashIcon.png).

### Fazendo download das traduções geradas para um idioma de destino

O {{site.data.keyword.GlobalizationPipeline_short}} fornece diversas
maneiras de incorporar a tradução para um idioma de destino em seu aplicativo. É possível
fazer download da tradução como arquivo de recursos e incluí-la na construção do seu
aplicativo. É possível também referenciar a tradução dinamicamente a partir do
{{site.data.keyword.GlobalizationPipeline_short}} usando um dos
[SDKs](https://github.com/IBM-Bluemix/gp-common) de software livre. 

<!-- For information on {{site.data.keyword.GlobalizationPipeline_full}} SDKs, see <link>. -->

Para fazer download da tradução como arquivo de recursos: 

1. Na coluna **Ações** do idioma de destino ou de origem a ser transferido por download, clique no ícone **Fazer download das traduções** ![Selecione o ícone de download para fazer download das chaves ou traduções de origem para um idioma de destino](images/downloadIcon.png).
2. Selecione um formato de arquivo.
3. Clique em **Fazer o Download**.
