# Comandos bl

*Última atualização:* 13 de novembro de 2015

Se você estiver construindo um aplicativo Node.js, será possível usar o Bluemix™ Live Sync para atualizar rapidamente a instância do aplicativo em execução no Bluemix e desenvolver como se você estivesse na área de trabalho sem reimplementar. Ao fazer uma mudança, é possível ver essa mudança no seu aplicativo Bluemix em execução imediatamente. A interface
da linha de comandos Bluemix Live Sync é denominada *bl*.

É possível usar os comandos da interface de linha de comandos **bl** para concluir as tarefas a seguir:

* Inicie e pare um aplicativo que está sendo executado no Bluemix.
* Crie um novo projeto baseado em nuvem a partir de sua área de trabalho.
* Sincronize as mudanças de sua área de trabalho com a área de trabalho do projeto baseado em nuvem e com o aplicativo em execução no Bluemix.
* Consulte a lista de projetos disponíveis para sincronização.
* Consulte o status dos aplicativos em execução.

Para obter informações adicionais sobre download e uso do comando bl, veja [Bluemix Live Sync](https://www.ng.bluemix.net/docs/manageapps/bluemixlive.html#bluemixlive).

## Comandos bl

A linha de comandos do Bluemix Live Sync, **bl**, tem a sintaxe a seguir:

``` bl command [arguments][options] [--help]```

### Comandos
<dl>
<dt>login, l</dt>
<dd>Efetue login no Bluemix.</dd>
<dt>logout, lo</dt>
<dd>Efetue logout do usuário.</dd>
<dt>sync, s</dt>
<dd>Inicie o processo de sincronização entre a área de trabalho e o servidor.</dd>
<dt>create, c</dt>
<dd>Crie um projeto privado, vincule-o ao repositório Git nesse diretório e implemente o conteúdo no Bluemix.</dd>
<dt>projects, p</dt>
<dd>Liste todos os projetos que estão disponíveis para sincronização.</dd>
<dt>start, st</dt>
<dd>Inicie a instância do aplicativo no Bluemix.</dd>
<dt>stop, sp</dt>
<dd>Pare a instância do aplicativo no Bluemix.</dd>
<dt>status, ss</dt>
<dd>Liste o status da instância de aplicativo em execução no Bluemix.</dd>
</dl>

### Argumentos
<dl>
<dd>Argumentos para o comando.</dd>
</dl>

### Opções
<dl>
<dd>Opções para o comando.</dd>
</dl>

### Opções globais
<dl>
<dt>--help</dt>
<dd>Exiba a página de ajuda para o comando especificado</dd>
<dt>--verbose</dt>
<dd>Ative a criação de log detalhado.</dd>
</dl>

**Nota:** Se qualquer um de seus argumentos ou opções contiver um espaço, coloque o valor entre aspas duplas.
