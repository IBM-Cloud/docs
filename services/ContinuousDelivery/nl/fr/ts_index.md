---

copyright:
  years: 2015, 2017
lastupdated: "2017-2-9"

---
<!-- Common attributes used in the template are defined as follows: -->
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Traitement des incidents liés à {{site.data.keyword.contdelivery_short}}
{: #ts_cd}

Obtenez des réponses aux questions courantes liées au traitement des incidents relatifs à l'utilisation d'{{site.data.keyword.contdelivery_full}}.
{:shortdesc}


## Autorisation impossible auprès de GitHub
{: #cannot_authorize_github}

Vous n'êtes pas autorisé auprès de GitHub.
{:shortdesc}

Si vous n'avez pas autorisé {{site.data.keyword.Bluemix_notm}} à accéder à votre compte GitHub, l'un des problèmes suivants peut se produire :
{: tsSymptoms}

 * Lorsque vous tentez d'ajouter l'intégration d'outils GitHub à votre chaîne d'outils, l'ajout n'a pas lieu. 
 * Le pipeline ne s'exécute pas automatiquement lorsque vous envoyez des modifications par commande push à votre référentiel GitHub ou GitHub Enterprise. 

{{site.data.keyword.Bluemix_notm}} n'est pas autorisé à accéder à GitHub.  
{: tsCauses}
 
Si vous configurez l'intégration d'outils GitHub lors de la création de votre chaîne d'outils, procédez comme suit :
{: tsResolve}
 
  1. A la section Intégrations configurables, cliquez sur **GitHub**.  
  1. Si vous créez la chaîne d'outils sur {{site.data.keyword.Bluemix_notm}} public et si vous n'avez pas autorisé {{site.data.keyword.Bluemix_notm}} à accéder à GitHub, cliquez sur **Autorisation** pour accéder au site Web GitHub. 
  1. Si vous n'avez pas de session GitHub active, vous êtes invité à vous connecter. Cliquez sur **Authorize Application** pour autoriser {{site.data.keyword.Bluemix_notm}} à accéder à votre compte GitHub. Si vous disposez d'une session GitHub active mais n'avez pas saisi votre mot de passe récemment, vous êtes invité à entrer votre mot de passe GitHub pour confirmation.
  
Si vous disposez déjà d'une chaîne d'outils, mettez à jour la configuration de l'intégration d'outils GitHub :

 1. Dans le tableau de bord DevOps, dans la page **Chaînes d'outils**, cliquez sur la chaîne d'outils afin d'ouvrir sa page Vue
d'ensemble. Vous pouvez également, depuis la page de présentation de l'application, sur la carte Distribution continue, cliquer sur **Afficher la chaîne d'outils**, puis sur **Présentation**. 
 1. Sur la carte GitHub, cliquez sur le menu, puis sur **Configurer**.
 1. Mettez à jour les paramètres de configuration pour autoriser {{site.data.keyword.Bluemix_notm}} à accéder à GitHub. Cliquez sur **Autoriser** pour accéder au site Web GitHub. Si vous n'avez pas de session GitHub active, vous êtes invité à vous connecter. Cliquez sur **Authorize Application** pour autoriser {{site.data.keyword.Bluemix_notm}} à accéder à votre compte GitHub. Si vous disposez d'une session GitHub active mais n'avez pas saisi votre mot de passe récemment, vous êtes invité à entrer votre mot de passe GitHub pour confirmation.
 1. Lorsque vous avez terminé la mise à jour des paramètres, cliquez sur **Sauvegarder l'intégration**.


## L'intégration d'outils n'est pas configurée
{: #tool_integration_error}

Une fois que vous avez configuré une intégration d'outils pour votre chaîne d'outils, l'erreur `Echec de la configuration` s'affiche sur la carte de l'outil.
{:shortdesc}

Après avoir configuré une intégration d'outils, vous pouvez afficher sa carte d'outil sur la page de présentation de la chaîne d'outils et constater que la configuration a échoué.
{: tsSymptoms}

 ![Erreur Echec de la configuration](images/tool_setup_failed.png)
 
Lorsque vous ajoutez une intégration d'outils, la chaîne d'outils communique avec l'outil qui est représenté par l'intégration d'outils pour mettre à disposition les ressources nécessaires et les associer à la chaîne d'outils. Si une erreur se produit pendant le processus de configuration ou si la communication entre la chaîne d'outils et l'outil ne s'établit pas correctement, l'intégration d'outils passe à l'état d'erreur.
{: tsCauses}

Configurez à nouveau l'intégration d'outils :
{: tsResolve}

1. Sur sa carte d'outil, survolez le message `Echec de la configuration` et cliquez sur **Reconfigurer**.

 ![Bouton Reconfigurer](images/tool_reconfigure.png)
 
1. Assurez-vous que vous utilisez des paramètres de configuration valides. Si l'erreur est due à une configuration non valide, un message d'erreur s'affiche ; par exemple, `Impossible de configurer l'intégration. Vérifiez les paramètres puis réessayez. Motif : api_key:fakeKey non valide`. Mettez à jour les paramètres de l'intégration
d'outils et cliquez sur **Sauvegarder l'intégration**. 
1. Si l'erreur a été provoquée par un problème de communication, cliquez sur **Sauvegarder l'intégration** pour réessayer.
