# Introdução à amostra de HelloWorld
{: #gettingstarted-cordova}

Se desejar iniciar com um novo aplicativo Cordova, é possível usar o app HelloWorld. Esse app demonstra como se conectar ao backend do Bluemix a partir de um app móvel sem autenticação. O app já possui o SDK instalado. Quando você estiver pronto, poderá obter as bibliotecas específicas que deseja usar em seu app.

1. Crie seu backend móvel no Bluemix.
<ol>
	<li>Na seção Textos padrão do catálogo do Bluemix, clique em MobileFirst Services Starter.</li>
    	<li>Insira um nome e um host para seu app e clique em **Criar**.</li>
    	<li>Clique em **Concluir**. </li>
</ol>
2. Obtenha o projeto a partir do GitHub. Opcionalmente, é possível usar o comando git clone para obter o projeto. Em seu
computador, abra o terminal e, em seguida, insira o comando a seguir:
```
git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-Cordova-helloworld.git
```
Antes de iniciar, faça download do arquivo Gradle.zip e instale o Gradle extraindo o arquivo compactado transferido por download no diretório de sua escolha. O Android Studio pode perguntar por um GRADLE HOME quando você importar a amostra pela primeira vez. Configure esse caminho com o diretório bin que está localizado no arquivo Gradle.zip extraído. O arquivo build.gradle constrói automaticamente seu projeto enviando por pull as dependências necessárias.

3. Inicialize o projeto.
Para inicializar o SDK, substitua &lt;APPLICATION_ROUTE&gt; e &lt;APPLICATION_ID&gt; pela rota e pelo GUID do aplicativo no bloco try na função BMSClient.getInstance().initialize():
```
// inicializar o SDK com o ID e a rota do aplicativo IBM Bluemix
BMSClient.getInstance().initialize(this, "<APPLICATION_ROUTE>", "<APPLICATION_ID>");
```
4. Execute a amostra em seu ambiente de desenvolvimento.
Na barra de ferramentas do Android Studio, clique no botão executar e selecione um
simulador.
No simulador, clique em **Executar ping no Bluemix**. O app de amostra envia uma solicitação Get para um recurso protegido no tempo de execução de Node.js no Bluemix. Se a
solicitação for bem-sucedida, a conexão será verificada e o texto no
simulador será atualizado.
Nota: o código de tempo de execução de Node.js é fornecido no texto padrão do MobileFirst Services Starter. Se o aplicativo backend não tiver sido criado com o texto padrão do MobileFirst Services Starter, o aplicativo não será conectado com êxito.


![Aplicativo Hello World conectado com êxito ao Bluemix](images/yayconnected.jpg "Figura 1. Aplicativo Hello World conectado com êxito ao Bluemix")

Quando você se conectar com êxito ao Bluemix a partir do app móvel no Android Studio, uma mensagem que diz "Oba! você está conectado" será exibida.
5. Resolva quaisquer problemas.

![Aplicativo Hello World não conectado ao Bluemix](images/bummer_android.jpg "Figura 2. Aplicativo Hello World não conectado ao Bluemix")

Quando a conexão falha, uma mensagem "Puxa, algo deu errado" é exibida. Mais informações sobre o erro são incluídas.
Verifique os itens a seguir:
 * Verifique se você colou corretamente os valores de
rota e GUID.
 * Também é possível verificar o log de depuração para obter mais informações.

## Próximas etapas:
{: #next}
Para obter informações sobre como obter o SDK e o integrar ao app móvel, consulte Configurando o cliente SDK do Android.
