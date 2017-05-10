---

copyright:
  years: 2015, 2017
lastupdated: "2016-10-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Gerenciando traduções
{: #globalizationpipeline_managingtranslations}


Uma vez criados os pacotes configuráveis e iniciada a geração de traduções para seu aplicativo, o conteúdo gerado pela máquina poderá ser usado como está ou modificado posteriormente. Você também tem a opção de usar uma tradução de máquina diferente do padrão. Esta seção descreve como mudar o mecanismo de tradução de máquina que executa as traduções de seus pacotes configuráveis, como executar edição humana pós-tradução e também como designar funções de usuário e restrições de acesso às pessoas que precisarão acessar as traduções.
{:shortdesc}

## Configuração da tradução de máquina
{: #globalizationpipeline_service_to_service}

O {{site.data.keyword.GlobalizationPipeline_full}} suporta a capacidade de integrar serviços de tradução de máquina alternativos para executar a tradução de máquina de seus pacotes configuráveis. A inclusão de um serviço alternativo poderá ser benéfica se o mecanismo padrão utilizado pelo {{site.data.keyword.GlobalizationPipeline_short}} não oferecer um idioma específico que você precisa ou se você preferir as traduções de máquina que são geradas por um mecanismo diferente. O uso ou os encargos de serviços alternativos são cobertos sob os termos desses serviços.

Para incluir e configurar um serviço de tradução de máquina alternativo para o {{site.data.keyword.GlobalizationPipeline_short}}, selecione a guia **Configuração de tradução de máquina** no painel do {{site.data.keyword.GlobalizationPipeline_short}}.

* Para incluir um serviço de tradução de máquina que esteja no catálogo do {{site.data.keyword.Bluemix_notm}}, (**Watson Language Translator**), o serviço deve
primeiro ser incluído em seu espaço do {{site.data.keyword.Bluemix_notm}}.

* Para incluir um serviço de terceiros, selecione o botão desse serviço na guia **Configuração de tradução de máquina** e forneça as credenciais de usuário requeridas para acessar o serviço.

Após um serviço de tradução de máquina ter sido incluído no {{site.data.keyword.GlobalizationPipeline_short}}, conclua as etapas restantes para concluir a integração desse serviço.

1. Clique em **Ativar** para ativar a integração com esse serviço.

2. Clique em **Atualizar idiomas** para visualizar uma lista atualizada de idiomas de destino suportados.

3. Na lista de idiomas de destino, selecione o mecanismo de tradução de máquina que deverá executar a tradução.

4. Clique em **Salvar** para retornar à guia **Configuração de tradução de máquina**.

Depois que um serviço alternativo tiver sido configurado com o {{site.data.keyword.GlobalizationPipeline_short}}, todos os idiomas de destino que tiverem sido designados a esse mecanismo começarão a ser gerados usando esse mecanismo. 

Para parar de usar um mecanismo de tradução de máquina alternativo:

1. Na guia **Configuração de tradução de máquina**, clique no
botão **Desativar** para o serviço que você deseja parar de usar.

Depois que um serviço de tradução de máquina alternativo for desativado, todas as traduções que foram geradas pelo serviço permanecerão nos pacotes configuráveis. Entretanto, a tradução em um determinado idioma de destino poderá não estar disponível para atualizações futuras se o idioma de destino não for mais suportado pelo mecanismo de tradução de máquina atualmente ativado.

<!-- Review comment: When you disable an engine, do you need to go back and reconfigure the languages?? Does it go back to the default engine? What happens? -->

## Visualizando e editando traduções
{: #globalizationpipeline_translations}

O serviço {{site.data.keyword.GlobalizationPipeline_short}} fornece recursos
de edição humana pós-tradução. Um tradutor profissional ou alguém conhecedor de qualquer
um dos idiomas de destino pode fazer edições nas traduções geradas. É possível editar
para melhorar a qualidade ou a consistência da tradução ou substituir palavras
preferenciais. Por exemplo, talvez você queira sobrescrever a tradução do nome de um
produto.

Para visualizar e editar as traduções de um idioma de destino:

1. Na página **Detalhes do pacote configurável**, selecione um idioma de destino ou clique no ícone **Visualizar as traduções** ![Selecione o ícone Visualizar traduções para visualizar as traduções de um idioma de destino](images/viewProjectDetailIcon.png) na coluna Ações.
2. As traduções são apresentadas em uma tabela que mostra informações de chave, origem e tradução.
 * **Chave:** representa um atributo no arquivo de recursos que tem um valor associado.
 * **Origem:** representa uma sequência traduzível que foi incluída no arquivo de recursos transferido por upload.
 * **Tradução:** representa a versão traduzida de um valor de origem.
3. Na coluna Ações, clique no ícone **Modificar a tradução** ![Selecione o ícone Modificar a tradução para editar as traduções de um determinado par de chave/valor.](images/editIcon.png) para editar um valor traduzido pela máquina.
4. Edite a tradução e clique em **Atualizar** para atualizar o valor traduzido original com sua edição.

![A janela da caixa de diálogo Modificar tradução fornece uma maneira simples de editar as traduções.](images/editTranslation.png) 

***Dica:*** quando você trabalha com pacotes configuráveis grandes que incluem muitas chaves traduzíveis, a descoberta de um valor específico pode ser difícil. Na página de tradução do idioma de destino, é possível procurar rapidamente entre todas as chaves, origens e traduções usando a caixa **Procurar...**.

![Use a caixa de procura que é fornecida na página de tradução do idioma de destino para procurar as chaves, origens, traduções ou as três em um idioma de destino.](images/search.png) 


## Incluindo usuários da API
{: #globalizationpipeline_users}

À medida que gerencia suas traduções, você poderá desejar conceder acesso a usuários da API adicionais com base nas tarefas que eles precisam executar. Por exemplo, talvez você queira permitir que um tradutor edite a tradução, mas não possa modificar as informações do pacote configurável.

| Tipo de função | Visualizar traduções? | Editar traduções? | Modificar informações do pacote configurável? |
|-----------|--------------------|--------------------|----------------------------|
| Reader | Sim | NÃO | NÃO |
| Translator | Sim | Sim | NÃO |
| Administrador | Sim | Sim | Sim |

Se você criar mais usuários da API, será possível restringir o acesso deles a um ou mais pacotes configuráveis específicos, ou conceder a eles acesso a todos os pacotes configuráveis disponíveis.

Para conceder a um usuário da API acesso a pacotes configuráveis em uma instância
de serviço do {{site.data.keyword.GlobalizationPipeline_short}}:

1. No painel do {{site.data.keyword.GlobalizationPipeline_short}}, clique na guia **Usuários da API**.
2. Clique em **Novo usuário da API**.
3. Digite um **nome de exibição** e **comentário** para descrever o novo usuário da API.
4. Escolha um **tipo** para o novo usuário da API.
5. Escolha conceder ao usuário da API acesso a todos os pacotes configuráveis ou somente pacotes configuráveis selecionados.
6. Clique em **Salvar**.

![Conclua o fórum para criar um novo usuário da API.](images/newUser.png)

Um ID e uma senha do usuário da API são gerados e exibidos. Copie e salve essas credenciais; depois de fechar a janela, não será possível acessá-las novamente. As credenciais podem ser usadas para serviço RESTful via [SDKs](https://github.com/IBM-Bluemix/gp-common). 

Para reconfigurar a senha de usuário da API:

1. No painel do {{site.data.keyword.GlobalizationPipeline_short}}, clique na guia **Usuários da API**.
2. Clique no ícone **Reconfigurar senha** ![Selecione este ícone para reconfigurar a senha dos usuários da API](images/resetPW.png) para reconfigurar a senha de um ID de usuário específico. 
3. Clique
em **Sim**. 
