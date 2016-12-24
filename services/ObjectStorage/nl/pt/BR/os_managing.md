---

copyright:
  years: 2014, 2016
lastupdated: "2016-12-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Gerenciando objetos

É possível usar a CLI do Swift, a API ou a UI do Bluemix para gerenciar objetos e contêineres.
{: shortdesc}

Antes de poder gerenciar objetos, certifique-se de que você tenha autenticado sua instância de serviço, gerado credenciais de serviço e configurado a CLI do Swift.

É possível armazenar, fazer download e excluir objetos ao trabalhar com o serviço. Há algumas coisas para manter em mente ao gerenciar seus objetos.
  * Não há nenhum limite para a quantia de dados que podem ser armazenados, mas cada upload não pode conter mais do que 5 GB. Se for necessário fazer upload de arquivos maiores do que 5 GB, siga as etapas localizadas em [Armazenando objetos grandes](/docs/services/ObjectStorage/os_large_files.html).
  * O Swift não tem uma estrutura de diretório verdadeira, mas é possível incluir um [diretório existente](/docs/services/ObjectStorage/os_directories.html) em seus comandos.
  * Para evitar sobrescrever acidentalmente um arquivo, [configure a versão de objeto](/docs/services/ObjectStorage/os_versioning.html).
  * É possível [planejar um horário](/docs/services/ObjectStorage/os_deletion.html) para seus objetos serem excluídos.
