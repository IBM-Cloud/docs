---

copyright:
  years: 2015, 2017
lastupdated: "2017-4-11"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:screen:.screen}
{:codeblock:.codeblock}

# Trabalhando com o Git Repos and Issue Tracking (Experimental)
{: #git_working}

Colabore com a sua equipe e gerencie seu código-fonte com um repositório (repo) Git e um rastreador de problemas que seja hospedado pela IBM e construído no [GitLab Community Edition ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://about.gitlab.com/){:new_window}.
{: shortdesc}

A integração de ferramenta Git Repos and Issue Tracking suporta que as equipes gerenciem código e colaborem de várias maneiras:
   * Gerenciar repositórios Git por meio de controles de acesso de baixa granularidade que mantém o código seguro
   * Revisar o código e aprimorar a colaboração por meio de solicitações de mesclagem
   * Rastrear problemas e compartilhar ideias por meio do rastreador de problemas
   * Documentar projetos no sistema de wikis

**Nota:** como essa integração de ferramenta é construída no GitLab Community Edition e hospedada pela IBM no Bluemix, algumas opções do GitLab não estão disponíveis. Por exemplo, o Delivery Pipeline fornece integração contínua e entrega contínua para o Bluemix, portanto, os recursos de integração contínua no GitLab não são suportados. Além disso, as funções de administração não estão disponíveis porque são gerenciadas pela IBM.

## Limites de tamanho do arquivo e do repositório
{: #git_limits}

Os arquivos são estritamente limitados a 100 MB. O limite de tamanho sugerido do repositório é 1 GB. Se o seu repositório excede 1 GB, talvez você receba um e-mail com uma solicitação para reduzir o tamanho do repositório.

## Criando um token de acesso pessoal ou chave SSH para autenticação    
{: #git_authentication}

Para concluir operações Git remotas, como `clonar` ou `enviar por push` no repositório Git local, deve-se usar um token de acesso pessoal ou uma chave SSH para se autenticar no GitLab.

* Para configurar um token de acesso pessoal, veja [Tokens de acesso pessoal![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://git.ng.bluemix.net/help/api/README.html#personal-access-tokens){:new_window}.
* Para configurar uma chave SSH, veja [SSH ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://git.ng.bluemix.net/help/ssh/README){:new_window} ou [Como criar suas chaves SSH ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://git.ng.bluemix.net/help/gitlab-basics/create-your-ssh-keys){:new_window}. O acesso aos repositórios com autenticação SSH pode requerer configuração adicional para proxies e firewalls.

**Nota:** para usar um token de acesso pessoal ou chave SSH para autenticação, deve-se configurar o Git localmente. Para obter instruções, veja [Iniciar o uso do Git na linha de comandos ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://git.ng.bluemix.net/help/gitlab-basics/start-using-git){:new_window}.
