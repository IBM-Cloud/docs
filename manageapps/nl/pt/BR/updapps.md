---

copyright:
  years: 2015, 2016

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

#Atualizando apps
{: #updatingapps}

*Última atualização: 9 de maio de 2016*


É possível usar o comando cf push ou o {{site.data.keyword.Bluemix}} DevOps Services para atualizar os aplicativos no {{site.data.keyword.Bluemix_notm}}. Em muitos casos, mesmo para os buildpacks integrados, como o Node.js, deve-se também fornecer um parâmetro -c para especificar qual comando será usado para iniciar seu aplicativo.
{:shortdesc}

##Criando e usando um domínio customizado
{: #domain}

É possível usar um domínio customizado na URL de seu aplicativo, em vez do domínio de sistema padrão do {{site.data.keyword.Bluemix_notm}}, que é mybluemix.net.

Os domínios fornecem a rota da URL que é alocada para sua organização no {{site.data.keyword.Bluemix_notm}}. Para usar um domínio customizado, deve-se registrar o domínio customizado em um servidor DNS público, configurar o domínio customizado no {{site.data.keyword.Bluemix_notm}} e, em seguida, mapear o domínio customizado para o domínio do sistema do {{site.data.keyword.Bluemix_notm}} no servidor DNS público. Depois que seu domínio customizado estiver mapeado para o domínio do sistema do
{{site.data.keyword.Bluemix_notm}}, as
solicitações de seu domínio customizado serão roteadas para seu aplicativo no
{{site.data.keyword.Bluemix_notm}}.

É possível criar e usar um domínio customizado no {{site.data.keyword.Bluemix_notm}} usando a interface com o usuário do
{{site.data.keyword.Bluemix_notm}} ou a interface de linha de comandos cf.

* Utilize a interface com o usuário do
{{site.data.keyword.Bluemix_notm}}:

  1. Crie um domínio customizado para sua organização.
    
	1. Na barra de menus do **PAINEL** do {{site.data.keyword.Bluemix_notm}}, clique em **GERENCIAR ORGANIZAÇÕES**.
	
	2. Na guia **DOMÍNIOS**, clique em **INCLUIR DOMÍNIO**, insira o nome do domínio customizado e clique em **SALVAR**.
    	
  2. Inclua a rota com o domínio customizado para um aplicativo.
  
    1. Na barra de menus do **PAINEL** do {{site.data.keyword.Bluemix_notm}}, clique no quadrado do aplicativo no qual você deseja incluir a rota. A página
**Visão geral** é exibida.
	
	2. No menu do aplicativo na página **Visão geral**, clique em **Editar rotas e acesso a app**.
	
	3. Clique em **Incluir rota** e especifique a rota que você deseja
usar para o aplicativo.
	
* Use a interface de linha de comandos cf:
  
  1. Crie um domínio customizado para sua organização, inserindo o comando a seguir:
    
    ```
    cf create-domain <your org name> mydomain
    ```
    
    *organization_name*
  
        O nome de sua organização.
	  
    *mydomain*
    
        O nome de domínio customizado que você deseja usar.
	  
  2. Inclua a rota com o domínio customizado em um aplicativo, inserindo o comando a
seguir:
    
    ```
    cf map-route myapp mydomain -n host_name
    ```
    
    *myapp*
      
    	O nome do aplicativo.
  	
    *mydomain*
      
    	O nome de seu domínio customizado.
	
    *host_name*
    
        O nome do host na rota que você deseja usar para seu aplicativo.
	
Após configurar o domínio customizado no {{site.data.keyword.Bluemix_notm}}, deve-se mapear o domínio customizado para o domínio do sistema do {{site.data.keyword.Bluemix_notm}} em seu servidor DNS registrado:

  1. Configure um registro 'CNAME' para o nome de domínio customizado em seu servidor DNS.
  2. Mapeie o nome do domínio customizado para o terminal seguro para a região do {{site.data.keyword.Bluemix_notm}} em que seu aplicativo está em execução. Use os terminais da região a seguir para fornecer a rota da URL alocada para a sua organização no {{site.data.keyword.Bluemix_notm}}:
  
    * US-SOUTH: `secure.us-south.bluemix.net`
    * EU-GB: `secure.eu-gb.bluemix.net`
    * AU-SYD: `secure.au-syd.bluemix.net`
  
Em um navegador ou uma interface de linha de comandos, insira a URL a seguir para acessar o aplicativo myapp:

```
http://host_name.mydomain
```

**Nota:** para remover uma rota órfã, use o comando a seguir:

```
cf delete-route domain -n hostname -f
```

*domain* é o nome de seu domínio e *hostname* é o nome do host da rota de seu aplicativo. Para obter mais informações sobre o comando
**cf delete-route**, digite `cf
delete-route -h`.

##Implementações azul/verde
{: #blue_green}

O {{site.data.keyword.Bluemix_notm}}
suporta a técnica de implementação azul/verde para permitir entrega contínua e minimizar
eventos de tempo de inatividade.

*Implementação azul/verde* é uma técnica de implementação com
tempo de inatividade zero que consiste em dois ambientes de produção quase idênticos,
chamados Azul e Verde. Eles diferem pelos artefatos que o desenvolvedor
alterou intencionalmente, em geral pela versão do aplicativo. Em um determinado momento
qualquer, pelo menos um dos ambientes está ativo. Com o uso da técnica de
implementação azul/verde, é possível perceber os benefícios a seguir:

* Execute o software rapidamente do estágio final do teste até a produção em tempo real.
* Implemente uma nova versão de um aplicativo sem interromper o tráfego para o aplicativo.
* Retroceda rapidamente. Se houver algo errado com um dos seus ambientes, será possível
alternar rapidamente para o outro ambiente.

Se você já tiver implementado um
aplicativo no
{{site.data.keyword.Bluemix_notm}} e desejar
atualizar o aplicativo para uma nova versão, poderá usar qualquer uma das duas abordagens
a seguir para assegurar a implementação azul/verde.

###Exemplo: usando o comando cf rename

Neste exemplo, o nome do aplicativo é Blue. O exemplo
demonstra como atualizar a versão de *Blue* usando o comando **cf
rename** sem interromper o tráfego para o aplicativo. Como opção, agora a
versão antiga de *Blue* pode ser excluída quando a versão atualizada
estiver em vigor.

1. Envie por push o app *Blue* para o {{site.data.keyword.Bluemix_notm}}.
  
  ```
  cf push Blue
  ```
  
  **Resultado:** o app *Blue* está em execução e respondendo à URL `Blue.mybluemix.net`.
  
2. Use o comando **cf rename** para renomear o app *Blue* para *Green*:
  
  ```
  cf rename Blue Green
  ```
  
  Liste os aplicativos no espaço atual, usando o comando **cf apps**:
  
  ```
  ...
  name             requested state   instances   memory   disk   urls
  Green            started           1/1         1G       1G	 Blue.mybluemix.net
  ...
  ```
  
  **Resultado:** o app *Green* está em execução e respondendo à URL `Blue.mybluemix.net`.

3. Faça as mudanças necessárias e tenha a versão atualizada de *Blue*
pronta. Envie por push o app *Blue* atualizado para o {{site.data.keyword.Bluemix_notm}}:
  
  ```
  cf push Blue
  ```
  
  Liste os aplicativos no espaço atual, usando o comando **cf apps**:
  
  ```
  ...
  name             requested state   instances   memory   disk   urls
  Green            started           1/1         1G       1G	 Blue.mybluemix.net
  Blue             started           1/1         1G       1G	 Blue.mybluemix.net
  ...
  ```
  
  **Resultados:**
    * Duas instâncias do aplicativo são implementadas, *Blue* e *Green*.
	* O app *Green* está em execução e respondendo à URL `Blue.mybluemix.net`.
	
4. Opcional: se desejar excluir a versão antiga (*Green*) do app, use o comando **cf delete**.
  
  ```
  cf delete Green -f
  ```
  
  Liste as rotas em seu espaço, usando o comando **cf route**:
  
  ```
  ...
  host             domain           apps
  Blue             mybluemix.net    Blue
  ...
  ```
  
  **Resultado:** o app *Blue* está respondendo à URL `Blue.mybluemix.net`.
  
###Exemplo: usando o comando cf map-route

Neste exemplo, *Blue* é o aplicativo implementado
anteriormente e *Green* é a versão atualizada. Esse exemplo demonstra
como atualizar a versão de *Blue* usando o comando **cf
map-route** sem interromper o tráfego para o aplicativo. Como opção, agora a
versão antiga de *Blue* pode ser excluída quando a versão atualizada
estiver em vigor.

1. Envie por push o app *Blue* para o {{site.data.keyword.Bluemix_notm}}.
  
  ```
  cf push Blue
  ```
  
  **Resultado:** o app *Blue* está em execução e respondendo à URL `Blue.mybluemix.net`.
  
2. Faça as mudanças necessárias e tenha a versão de *Green* pronta. Envie por push o app *Green* para o {{site.data.keyword.Bluemix_notm}}:
  
  ```
  cf push Green
  ```
  
  Liste os aplicativos no espaço atual, usando o comando **cf route**:
  
  ```
  ...
  host             domain           apps
  Blue             mybluemix.net    Blue
  Green            mybluemix.net    Green
  ...
  ```
  
  **Resultados:**
  
    * Duas instâncias do app são implementadas, *Blue* e *Green*.
	* O app *Blue* está respondendo à URL `Blue.mybluemix.net`. E o app *Green* está respondendo à URL `Green.mybluemix.net`.
	
3. Mapeie o app *Blue* para o app *Green* para que todo o tráfego para `Blue.mybluemix.net` seja roteado para o app *Blue* e o app *Green*.
  
  ```
  cf map-route Green mybluemix.net -n Blue
  ```
  
  Liste as rotas em seu espaço, usando o comando cf routes:
  
  ```
  ...
  host             domain           apps
  Blue             mybluemix.net    Blue, Green
  Green            mybluemix.net    Green
  ...
  ```
  
  **Resultado:**

    * O Roteador CF agora envia o tráfego para Blue.mybluemix.net. para o app Blue e o app Green.
	* O Roteador CF continua a enviar o tráfego para Green.mybluemix.net. para o app Green.
	
4. Ao verificar que *Green* está sendo executado conforme o esperado, remova a rota `Blue.mybluemix.net` do app *Blue*:
  
  ```
  cf unmap-route Blue mybluemix.net -n Blue
  ```
  
  Liste as rotas em seu espaço, usando o comando cf routes:
  
  ```
  ...
  host             domain           apps
  Blue             mybluemix.net    Green
  Green            mybluemix.net    Green
  ...
  ```
  
  **Resultado:** O Roteador CF para de enviar o tráfego para o app *Blue*. O app *Green* está respondendo a ambas as URLs: `Green.mybluemix.net` e `Blue.mybluemix.net`.
  
5. Remova a rota `Green.mybluemix.net` para o app *Green*.
  
  ```
  cf unmap-route Green mybluemix.net -n Green
  ```
  
  **Resultado:** O Roteador CF para de enviar o tráfego para o app *Blue*. O app *Green* está respondendo à URL `Blue.mybluemix.net`.
  
6. Opcional: se desejar excluir a versão antiga (*Blue*) do aplicativo, use o comando `cf delete`.
  
  ```
  cf delete Blue -f
  ```
  
  Liste as rotas em seu espaço, usando o comando cf route:
  
  ```
  ...
  host             domain           apps
  Blue             mybluemix.net    Green
  ...
  ```
  
  **Resultado:** o app *Green* está respondendo à URL `Blue.mybluemix.net`.


# Links Relacionados
{: #rellinks}

## Links Relacionados
{: #general}

* [Implementações azul/verde](http://martinfowler.com/bliki/BlueGreenDeployment.html){:new_window}
* [IBM{{site.data.keyword.Bluemix_notm}} DevOps
Services](https://hub.jazz.net/){:new_window}
