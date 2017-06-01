---

copyright:
  years: 2015, 2016
lastupdated: "2017-02-24"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Manutenção e atualizações da VM (máquina virtual)
{: #maintenance_and_vm_updates}

## Estratégia de Manutenção
{: #maintenance_strategy}

O IBM WebSphere Application Server no Bluemix é atualizado regularmente, assegurando que novas instâncias de serviço sejam criadas com fix packs e correções atuais. A
nuvem traz fornecimento fácil e rápido de novas instâncias de serviço para o gerenciamento de middleware. Espera-se
que muitos consumidores façam upgrade para uma nova instância de serviço quando desejarem aplicar a manutenção. Para os consumidores que desejam reter instâncias de serviço de longa duração, os repositórios de manutenção ficam
disponíveis para o middleware e o convidado operacional subjacente. Esses repositórios permitem que os usuários
mantenham seus ambientes assim como fariam no local.

## Atualizações de MV

A seção a seguir explica como aplicar mudanças no sistema de máquina virtual.

É possível atualizar sua MV como qualquer outro sistema RHEL normal. Ao usar o gerenciador de pacote
Red Hat "Yum", é possível instalar, atualizar, desinstalar e executar várias outras coisas com seus pacotes.

Seu sistema é configurado para receber essas atualizações do Servidor de Satélite Red Hat da IBM. Esse satélite
fornece pacotes seguros da Rede Red Hat pelo gerenciador de pacote Yum.

O Servidor de satélite é gerenciado pela IBM e não pode ser modificado de seu sistema.

Para obter mais informações, consulte [Aplicando atualizações de pacote no Red Hat Enterprise Linux](https://access.redhat.com/articles/11258#rhel6){: new_window} e [Yum, o gerenciador de pacote do Red Hat](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Deployment_Guide/ch-yum.html){: new_window}.
