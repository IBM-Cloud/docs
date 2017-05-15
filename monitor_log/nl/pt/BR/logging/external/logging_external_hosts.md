---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Configurando hosts de logs externos
{: #thirdparty_logging}

O {{site.data.keyword.Bluemix_notm}} mantém
uma quantia limitada de informação de log na memória. Quando as informações são
registradas, as informações antigas são substituídas pelas informações mais novas. Para manter todas as
informações de log, é possível salvar seus logs do aplicativo Cloud Foundry em um host de log externo, como um
serviço de gerenciamento de log de terceiro ou outro host.
{:shortdesc}

Para mover logs de seu app CF e do sistema para um host de log externo, conclua as etapas a seguir:

  1. Determine o terminal de criação de log.

	 É possível enviar logs a um agregador de log de terceiro, como Papertrail, Splunk ou Sumologic. Também é possível enviar logs a um host de syslog, um host de syslog criptografado com TLS (Segurança da camada de transporte) ou um terminal HTTPS POST. Os métodos para obter terminais de criação de log variam para diferentes hosts de logs.

  2. Crie uma instância de serviço fornecida pelo usuário.

	 Use o comando `cf create-user-provided-service` (ou `cups`, uma versão curta do comando) para criar uma instância de serviço fornecido pelo
usuário:
	 ```
	 cf create-user-provided-service <service_name> -l <logging_endpoint>
	 ```
	 &lt;service_name&gt;

	 O nome da instância de serviço fornecida pelo usuário.

	 &lt;logging_endpoint&gt;

	 O terminal de criação de log para o qual o {{site.data.keyword.Bluemix_notm}} envia logs. Consulte a tabela a seguir para substituir *logging_endpoint* por seu valor:

	 <table>
	 <caption>Tabela 1. Valores do terminal de criação de log</caption>
     <thead>
     <tr>
     <th>Terminal de criação de log</th>
     <th>Comando:</th>
	 <th>Notas</th>
     </tr>
     </thead>
     <tbody>
     <tr>
     <td>host syslog</td>
     <td>`cf cups my-logs -l syslog://HOST:PORT`</td>
	 <td>Por exemplo, para ativar a criação de log para Papertrail, digite `cf cups my-logs -l syslog://<papertrail-url>`. Substitua `<papertrail-url>` pela URL de seu terminal de criação de log a partir do Papertrail.</td>
     </tr>
	 <tr>
     <td>host syslog-tls</td>
     <td>`cf cups my-logs -l syslog-tls://HOST:PORT`</td>
	 <td>O certificado deve ser confiável por uma autoridade de certificação. Não use certificados autoassinados.</td>
     </tr>
	 <tr>
     <td>HTTPS POST</td>
     <td>`cf cups my-logs -l https://HOST:PORT`</td>
	 <td>Esse terminal deve estar na Internet pública e acessível pelo {{site.data.keyword.Bluemix_notm}}</td>
     </tr>
     </tbody>
     </table>
  3. Ligue a instância de serviço ao seu app.

	 Use o comando a seguir para ligar a instância de serviço a seu app:

	 ```
	 cf bind-service <appname> <service_name>
	 ```
	 &lt;appname&gt;

	 O nome do seu app.

	 &lt;service_name&gt;

	 O nome da instância de serviço fornecida pelo usuário.

  4. Remonte o app.
     Digite `cf restage appname` para que as mudanças entrem em vigor.

