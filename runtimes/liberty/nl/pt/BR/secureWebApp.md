---

copyright:
  years: 2017
lastupdated: "2017-03-15"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Escrevendo aplicativos da web Java seguros
{: #secure_java_web_app}

Todos os aplicativos da web devem ser projetados e codificados visando segurança para evitar a introdução de vulnerabilidades severas de segurança.
{: shortdesc}

O {{site.data.keyword.Bluemix}} fornece um aplicativo iniciador seguro para ajudar a escrever código Java Liberty mais seguro e evitar a maioria dos problemas Cross-Site Scripting (XSS). É possível fazer download deste [aplicativo iniciador seguro](https://github.com/IBM-Bluemix/java-secure-app), construí-lo e implementá-lo localmente e no {{site.data.keyword.Bluemix_notm}}.

## Por que escrever apps da web seguros
{: #why}

Uma vulnerabilidade de segurança pode ser explorada por vários ataques de segurança. Um ataque pode roubar credenciais, causar perda de dados e função, interromper serviços, além de danificar a reputação e a renda de um negócio. O Cross-Site Scripting, XSS, é uma das vulnerabilidades de segurança comuns encontradas na maioria dos aplicativos da web que devem ser evitadas.

Em vez de aprender a teoria sobre ataques XSS e as técnicas reparatórias antes de iniciar o desenvolvimento de aplicativos da web, é possível usar este [aplicativo iniciador seguro](https://github.com/IBM-Bluemix/java-secure-app). O aplicativo iniciador seguro inclui exemplos de codificação de práticas de codificação seguras essenciais que evitam o XSS para que você possa iniciar o desenvolvimento enquanto aprende e aplica técnicas de prevenção do XSS.

## Como usar o app de amostra seguro
{: #how}

É possível usar o [aplicativo iniciador seguro](https://github.com/IBM-Bluemix/java-secure-app) como um ponto de início para o novo desenvolvimento de aplicativo Liberty. Comece aprendendo o código de contramedida XSS no app e, em seguida, aplique-o às operações da API do aplicativo. As contramedidas no aplicativo iniciador seguro ajudam a evitar que a entrada maliciosa do usuário danifique seu aplicativo tanto no servidor quanto no navegador, minimizando ou evitando ataques XSS.

Primeiramente, faça download desse aplicativo iniciador seguro e, em seguida, construa e implemente-o no Bluemix ou localmente, da mesma maneira feita com o aplicativo de amostra [getting-started-java](https://github.com/IBM-Bluemix/get-started-java). Acesse [Introdução ao Liberty no Bluemix](getting-started.html) para saber mais sobre a construção e implementação de aplicativos no Bluemix. Para iniciar, é possível usar essas etapas para clonar, construir e executar o app.

```
git clone https://github.com/IBM-Bluemix/java-secure-app
cd java-secure-app
mvn install liberty:run-server
```
Visualize o app em http://localhost:9080/GetStartedSecureJava/

## Mais informações
{: more}
O aplicativo iniciador seguro contém **BadServlet.java**. Esse aplicativo mostra um exemplo de código inseguro que os desenvolvedores poderão escrever se não tomarem cuidado.

O aplicativo iniciador seguro também contém **GoodServlet.java**, que inclui várias boas práticas de codificação segura, como validação de entrada, codificação de saída, configurações de cabeçalho de HTTP seguras, além de Política de segurança de conteúdo. Essas práticas são contramedidas importantes contra XSS. Aplicá-las também pode minimizar outras vulnerabilidades, como alguma injeção e passagem de diretório.

Consulte [Folha de dicas de prevenção de XSS ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.owasp.org/index.php/XSS){: new_window} para saber mais sobre XSS e suas contramedidas.
