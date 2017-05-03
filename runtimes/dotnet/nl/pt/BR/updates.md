---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-30"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Atualizações mais recentes para o buildpack do ASP.NET Core
{: #latest_updates}


Uma lista das atualizações mais recentes no buildpack do aspnet.

## 29 de março de 2017: buildpack ASP.NET Core atualizado v1.0.13-20170330-1023

* Incluir suporte para o tempo de execução do .NET Core 1.0.4
* Incluir suporte para o tempo de execução do .NET Core 1.1.1
* Incluir suporte para o .NET Core SDK 1.0.1
* Atualizar versão do Nó para 6.10.0
* Remover suporte para o .NET Core SDK 1.0.0-preview2-003131
* Remover suporte para o .NET Core SDK 1.0.0-preview3-004056

## 31 de janeiro de 2017: buildpack ASP.NET Core atualizado v1.0.10-20170124-1145

* Incluir suporte para o .NET Core 1.0.3
* Incluir suporte para o conjunto de ferramentas .NET Core MSBuild
* Incluir suporte para projetos F#
* Remover suporte para o .NET Core SDK 1.0.0-preview2-003121

## 9 de dezembro de 2016: buildpack do ASP.NET Core atualizado v1.0.6-20161205-0912

* Incluir suporte para o .NET Core 1.1.0
* Remover suporte para o .NET Core 1.0.0 RC2
* Incluir uma opção para limpar o cache de pacotes NuGet

## 10 de outubro de 2016: buildpack do ASP.NET Core atualizado v1.0.1-20161005-1225

* Incluir suporte para .NET Core 1.0.1
* Corrija um problema intermitente que fez a implementação falhar ao armazenar em cache os
pacotes NuGet

## 31 de agosto de 2016: buildpack do ASP.NET Core atualizado v1.0-20160826-1345

* Inclua suporte para executar scripts de pré-compilação e pós-compilação usando
NPM e Bower para instalar javascript de front-end e bibliotecas css.
* Mova o buildpack do status Beta para o status GA

## 11 de julho de 2016: buildpack do ASP.NET Core atualizado v0.9-20160706-1603

Esta versão do buildpack inclui as mudanças a seguir:

* Esta versão do buildpack suporta a compilação do .NET CLI 1.0 Visualização 2 e o .NET Core 1.0 RTM
* O buildpack continua a suportar o .NET CLI 1.0 Visualização 1 e o .NET Core 1.0 RC2
* A versão padrão do .NET CLI a ser instalada agora é 1.0.0-preview2-003121

## 10 de junho de 2016: buildpack do ASP.NET Core atualizado v0.8.1-20160526-0957

Esta versão do buildpack inclui as mudanças a seguir:

* O nome do tempo de execução mudou de ASP.NET 5 para ASP.NET Core.
* O número da versão do buildpack foi incluído na saída do script de detecção.
* Essa versão do buildpack remove o suporte para aplicativos baseados em DNX que usam CoreCLR RC1 e inferior.
* Esta versão do buildpack suporta .NET CLI e .NET Core RC2.
* O buildpack detecta projetos com um arquivo project.json ou arquivos *.runtimeconfig.json da saída de publicação.

## 22 de outubro de 2015: Atualizado o buildpack do ASP.NET 5 v0.7-20151022-1257

* Esta versão do buildpack remove o Mono e, em seu lugar, suporta Beta 8 CoreCLR.

## 18 de setembro de 2015: buildpack do ASP.NET 5 v0.6-20150916-1220

* Esta versão do buildpack suporta mudanças Beta 7 DNX e pode executar aplicativos que dependem de liberações beta antigas
com o comando inicial customizado a seguir:

```
   dnx src/dotnetstarter kestrel --server.urls http://${VCAP_APP_HOST}:${PORT}
```
{: codeblock}

* O uso do servidor da web Nowin foi removido deste buildpack; em seu lugar, é usado o servidor da web [Kestrel]{https://github.com/aspnet/KestrelHttpServer}.

# rellinks
{: #rellinks notoc}
## geral
{: #general notoc}
* [tempo de execução Dotnet core](index.html)
