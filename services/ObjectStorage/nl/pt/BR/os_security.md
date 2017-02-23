---

copyright:
  years: 2014, 2017
lastupdated: "2017-02-10"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}



# Gerenciando acesso

As Listas de Controle de Acesso podem ser usadas para gerenciar o acesso ao serviço. Os [Usuários administrativos](/docs/services/ObjectStorage/os_access_types.html) podem conceder e remover os acessos de leitura e gravação.
{: shortdesc}

Antes de gerenciar o acesso usando a UI ou a CLI do Swift, assegure-se de ter configurado o serviço e começado o armazenamento de objetos.

Quando estiver trabalhando com listas de controle de acesso, mantenha os seguintes pontos em mente:
  * Quando um usuário cria um contêiner, os privilégios de administrador são concedidos automaticamente a ele para esse contêiner.
  * As listas de controle de acesso não estão disponíveis para a instância de serviço, para a
conta de armazenamento ou no nível de projeto. O acesso pode ser gerenciado somente no nível do contêiner ou do objeto.
  * Certifique-se de verificar se o acesso a um contêiner foi [removido](/docs/services/ObjectStorage/os_remove_access.html).
