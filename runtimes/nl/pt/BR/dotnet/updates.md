---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Atualizações mais recentes para o buildpack do ASP.NET Core
{: #latest_updates}

*Última atualização: 10 de junho de 2016*

Uma lista das atualizações mais recentes no buildpack do aspnet.

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
{: #rellinks}
## geral
{: #general}
* [tempo de execução Dotnet core](index.html)
