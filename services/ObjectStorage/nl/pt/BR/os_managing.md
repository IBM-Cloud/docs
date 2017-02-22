---

copyright:
  years: 2014, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Gerenciando objetos

É possível usar a CLI do Swift, a API ou a UI do Bluemix para gerenciar objetos e contêineres.
{: shortdesc}

Antes de gerenciar objetos, assegure-se de ter [autenticado](/docs/services/ObjectStorage/os_authenticate.html) sua instância de serviço, [gerado](/docs/services/ObjectStorage/os_credentials.html)
as credenciais de serviço e [configurado](/docs/services/ObjectStorage/os_configuring.html) a CLI do Swift.

Mantenha os seguintes pontos em mente quando estiver gerenciando objetos:
  * Não há nenhum limite para a quantia de dados que podem ser armazenados, mas cada upload não pode conter mais do que 5 GB. Se for necessário fazer upload de arquivos maiores que 5 GB, siga as etapas localizadas em [armazenando objetos grandes](/docs/services/ObjectStorage/os_large_files.html).
  * O Swift não tem uma estrutura de diretório verdadeira, mas é possível incluir um [diretório existente](/docs/services/ObjectStorage/os_directories.html) em seus comandos.
  * Para evitar sobrescrever acidentalmente um arquivo, [configure a versão de objeto](/docs/services/ObjectStorage/os_versioning.html).
  * É possível [planejar um horário](/docs/services/ObjectStorage/os_deletion.html) para seus objetos serem excluídos.
