---

copyright:
  years: 2016, 2017
lastupdated: "2016-02-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Usando o pacote GitHub
{: #openwhisk_catalog_github}

O pacote `/whisk.system/github` oferece uma maneira conveniente de usar as [APIs do GitHub](https://developer.github.com/).

O pacote inclui o feed a seguir:

| Entidade | Tipo | Parâmetros | Descrição |
| --- | --- | --- | --- |
| `/whisk.system/github` | pacote | username, repository, accessToken | Interagir com a API do GitHub |
| `/whisk.system/github/webhook` | alimentação | events, username, repository, accessToken | Disparar eventos acionadores na atividade do GitHub |

É sugerido criar uma ligação de pacote com os valores `username`,
`repository` e `accessToken`.  Com a ligação, não será necessário especificar os valores toda vez que usar o feed no pacote.

## Disparando um evento acionador com atividade do GitHub

O feed `/whisk.system/github/webhook` configura um serviço para disparar um acionador quando houver atividade em um repositório do GitHub especificado. Os parâmetros são como segue:

- `username`: o nome do usuário do repositório GitHub.
- `repository`: o repositório do GitHub.
- `accessToken`: seu token de acesso pessoal do GitHub. Ao [criar seu token](https://github.com/settings/tokens), certifique-se de que sejam selecionados os escopos repo:status epublic_repo. Além
disso, certifique-se de que não tenha nenhum webhook já definido para seu repositório.
- `events`: o [tipo de evento do GitHub](https://developer.github.com/v3/activity/events/types/) de interesse.

A seguir está um exemplo de criação de um acionador que será disparado toda vez que houver uma nova confirmação em um repositório do GitHub.

1. Gere um [token de acesso pessoal](https://github.com/settings/tokens) do GitHub.
  
  O token de acesso será usado na próxima etapa.
  
2. Crie uma ligação de pacote configurada para seu repositório GitHub e com o token de acesso.
  
  ```
  wsk package bind /whisk.system/github myGit \
    --param username myGitUser \
    --param repository myGitRepo \
    --param accessToken aaaaa1111a1a1a1a1a111111aaaaaa1111aa1a1a
  ```
  {: pre}
  
3. Crie um acionador para o tipo de evento `push` do GitHub usando seu feed `myGit/webhook`.
  
  ```
  wsk trigger create myGitTrigger --feed myGit/webhook --param events push
  ```
  {: pre}
  
  Uma confirmação para o repositório GitHub usando um `git push` faz
com que o acionador seja disparado pelo webhook. Se houver uma regra que corresponda ao acionador, então, a
ação associada será chamada.
  A ação recebe a carga útil de webhook do GitHub como um parâmetro de entrada. Cada evento
de webhook do GitHub tem um esquema JSON semelhante, mas é um objeto de carga útil
exclusivo que é determinado por seu tipo de evento.
  Para obter mais informações sobre o
conteúdo da carga útil, consulte a documentação da API de
[Eventos e carga útil
do GitHub](https://developer.github.com/v3/activity/events/types/).
  
