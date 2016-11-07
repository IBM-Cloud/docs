---

copyright:
  years: 2016
lastupdated: "2016-10-18"

---
{:new_window: target="_blank"}

# O que há de novo no painel Móvel
{: #what_is_new}

Última atualização: 18 de outubro de 2016
{: .last-updated}

A atualização de outubro do painel do {{site.data.keyword.Bluemix}} Mobile introduziu as mudanças a seguir:

   * Agora é possível incluir os recursos de Notificações push e Analítica em seu projeto diretamente do painel.
   * [Iniciadores de código](starters.html#Code_Starter) agora estão disponíveis.
   * Swift agora é suportado.


### Analytics
{: #analytics}

   * O modo demo é ativado por padrão quando você inclui o recurso de Analítica. É possível desativar o modo demo para visualizar a analítica depois de executar o app.


### UI Builder
{: #ui_builder}

   * O recurso **Notificações push** agora é acessado a partir do projeto.
   * A guia **Configurações do projeto** foi renomeada para a guia **Configurações**.
   * A guia **Autenticação** foi renomeada para a guia **Acesso do usuário**.


### Código
{: #code}

   * O código gerado Objective-C e Swift para iOS agora usa CocoaPods para gerenciar dependências. Isso significa que você precisa instalar o CocoaPods. Para instalá-lo, execute `sudo gem install cocoapods`. Após a instalação do CocoaPods, execute `pod setup` para configurá-lo (se não estiver ainda). Por último, execute `pod install` para fazer download e instalar as dependências necessárias do projeto antes de abrir o arquivo `.xcworkspace` no Xcode. Detalhes adicionais estão disponíveis no arquivo `README.md` no archive de código transferido por download. Leia sobre [Ferramentas de pré-requisito do desenvolvedor](get_code.html#prereq-dev-tools) para obter mais informações.

Verifique novamente várias vezes para se manter em dia com novas atualizações.


# Links relacionados
{: #rellinks}

<!-- links to internal services don't work
## {{site.data.keyword.Bluemix_notm}} Mobile services
{: #general}
* [Mobile Analytics (Beta)](../services/mobileanalytics/index.html){: new_window}
* [Mobile Client Access](../services/mobileaccess/index.html){: new_window}
* [Mobile Foundation](../services/mobilefoundation/index.html){: new_window}
* [Mobile Quality Assurance)](../services/MobileQualityAssurance/index.html){: new_window}
* [Push Notifications](../services/mobilepush/index.html){: new_window}
-->

## Postagens do blog
{: #general}
* [Postagem do blog: Introducing the Bluemix Mobile
dashboard](https://developer.ibm.com/bluemix/2016/07/08/new-bluemix-mobile-dashboard/){: new_window}
* [Postagem do blog: Introducing the next generation of the Bluemix Mobile dashboard](https://ibm.com/blogs/bluemix/2016/10/introducing-the-next-generation-of-the-bluemix-mobile-dashboard/){: new_window}
* [Postagem do blog: Introducing Bluemix Mobile Code Starters](https://www.ibm.com/blogs/bluemix/2016/10/rapid-dev-with-mobile-code-starters/){: new_window}
* [Postagem do blog: Bluemix
Mobile, Part 1: Creating a Store Catalog application](https://developer.ibm.com/bluemix/2016/07/13/bluemix-mobile-creating-store-catalog-app-part1/){: new_window}
* [Postagem do blog: Bluemix
Mobile, Part 2: Integrating custom Bluemix backend into the Store Catalog app](https://developer.ibm.com/bluemix/2016/07/14/bluemix-mobile-integrating-custom-backend-part2/){: new_window}

## Tutoriais e amostras
{: #samples}
* [Backend móvel para Bluemix](https://github.com/ibm-bluemix-mobile-services/mobiledashboard-storecatalog-backend){: new_window}
