---

copyright:
  years: 2012, 2017
  
lastupdated: "2017-01-25"  

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}
{:codeblock: .codeblock} 



# Identification et résolution des problèmes pour {{site.data.keyword.mqa}} 
{: #tsmqa}
Voici les réponses à plusieurs questions fréquentes concernant l'utilisation
de {{site.data.keyword.mqa}}.
{:shortdesc}

## La génération hybride JavaScript échoue
{: #ts_js_build_fail}

La génération de votre application hybride JavaScript {{site.data.keyword.mqa}} échoue, même si le composant SDK hybride JavaScript&tm; pour IBM MobileFirst Platform Foundation se trouve dans l'application et que le code requis est ajouté.


Lorsque vous tentez d'exécuter la génération de votre application
{{site.data.keyword.mqa}}, celle-ci échoue. 
{: tsSymptoms notoc} 


1. Les composants SDK hybrides propres aux plateformes Android et iOS ne sont pas installés dans le projet.
2. Les composants SDK hybrides propres aux plateformes Android et iOS qui sont installés ne sont pas compatibles avec le composant SDK JavaScript installé.
3. Le logiciel SDK Android natif, le logiciel SDK iOS natif, ou les deux, sont installés, mais les composants SDK hybrides propres aux
plateformes Android et iOS ne sont pas installés.
{: tsCauses notoc} 
 

Voici quelques suggestions de résolution du problème :
{: tsResolve notoc}
  1.  Assurez-vous d'avoir installé tous les composants SDK hybrides propres aux plateformes Android et iOS requis et tous les logiciels SDK
Android ou iOS natifs requis pour les plateformes que votre application prend en charge. 
  2. Assurez-vous que le numéro de version de vos composants SDK hybrides propres aux plateformes Android et iOS est identique ou supérieur à celui du composant JavaScript, jusqu'à la version suivante. Le tableau suivant contient des exemples :
  
| Version de composant JavaScript | Version de composant propre à la plateforme | Compatible ? |
|---------: |------------: |------------: |
| 1.2.3 | 1.2.3 | Oui |
| 1.2.3 | 1.2.1 | Non |
| 1.2.3 | 1.3.2 | Oui |
| 1.2.3 | 2.0.0 | Non |

  3. Assurez-vous d'avoir installé les composants SDK hybrides propres aux plateformes Android et iOS. Alors que le logiciel SDK Android natif et que le
logiciel SDK iOS natif sont requis si votre application s'exécute sur ces plateformes, pour les applications hybrides, les composants SDK hybrides
propres aux plateformes Android et iOS doivent également être installés pour chaque plateforme.

  
## Impossible d'ouvrir une analyse des sentiments ou de distribuer des applications de test
{: #ts_sent_fail}

Vous ne pouvez pas ouvrir une analyse des sentiments ou distribuer votre application de test.

Vous ne pouvez pas ouvrir une analyse des sentiments ou distribuer votre
application de test car votre navigateur bloque les fenêtres en incrustation.
{: tsSymptoms notoc} 

Mobile Quality Assurance utilise des fenêtres en incrustation et des cookies pour communiquer avec le serveur Mobile Quality Assurance.
{: tsCauses notoc}


Pour établir la communication entre Mobile Quality Assurance et le serveur Mobile Quality Assurance, il peut être nécessaire de configurer les paramètres du navigateur afin d'autoriser les fenêtres en incrustation et les cookies. Par exemple, lorsque vous
cliquez sur une option dans l'interface utilisateur, comme Score de sentiment, Mobile Quality Assurance peut être empêché de communiquer avec le serveur. L'analyse des sentiments ne peut pas être affichée si les fenêtres en incrustation et les cookies sont bloqués. Pour plus d'informations sur la configuration des paramètres de votre navigateur, consultez la documentation relative à votre navigateur. 
{: tsResolve notoc}


## Impossible d'exécuter une application arrivée à expiration
{: #ts_app_expired}

Vous ne pouvez pas exécuter votre application Mobile Quality Assurance.

Lorsque vous tentez d'exécuter votre application Mobile Quality Assurance, le message suivant, qui indique que votre application est arrivée à expiration et qu'elle ne peut pas être exécutée, apparaît : Your application has expired and cannot be run at this time.
{: tsSymptoms notoc} 

Votre application est signalée comme désactivée dans la page Builds de Mobile Quality Assurance.
{: tsCauses notoc}


Vérifiez la page Builds de Mobile Quality Assurance pour vous assurer qu'aucune des applications n'est signalée comme désactivée. En général, les applications sont signalées comme désactivées pour indiquer aux testeurs (par le biais de l'application elle-même) qu'ils ne doivent pas utiliser une version spécifique de la génération. Pour plus d'informations sur les paramètres qui figurent dans la page Builds de Mobile Quality Assurance, voir Managing builds dans l'IBM Knowledge Center.
{: tsResolve notoc}

