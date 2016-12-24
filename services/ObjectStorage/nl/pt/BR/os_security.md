---

copyright:
  years: 2014, 2016
lastupdated: "2016-12-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}



# Gerenciando acesso

As Listas de Controle de Acesso podem ser usadas para gerenciar o acesso ao serviço. Os [usuários administrativos](/docs/services/ObjectStorage/os_access_types.html) podem conceder acesso de leitura e gravação, bem como remover o acesso ao gerenciar sua instância de serviço.
{: shortdesc}


As Listas de Controle de Acesso podem ser gerenciadas usando a CLI do Swift ou a UI do Bluemix. Antes de gerenciar o acesso, assegure-se de que você tenha configurado o serviço e começado a armazenar objetos. Há algumas coisas para manter em mente ao gerenciar o acesso.
  * Quando um usuário cria um contêiner, os privilégios de administrador são concedidos automaticamente a ele para esse contêiner.
  * As listas de controle de acesso não estão disponíveis para a instância de serviço, para a
conta de armazenamento ou no nível de projeto. O acesso pode ser gerenciado somente no nível de contêiner.
  * Certifique-se de verificar se o acesso a um contêiner foi [removido](/docs/services/ObjectStorage/os_remove_access.html).
