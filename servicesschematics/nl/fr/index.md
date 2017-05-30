---

copyright:
  years: 2017
lastupdated: "2017-05-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Initiation à {{site.data.keyword.bpfull_notm}} (bêta)
{: #gettingstarted}

{{site.data.keyword.bplong}} est un outil d'automatisation que vous pouvez
utiliser pour définir et déployer votre infrastructure de cloud en tant qu'unité simple, et qui permet de réutiliser ces définitions de ressource de cloud dans d'autres
environnements.
{:shortdesc}

{{site.data.keyword.bpshort}} utilise Terraform, développé par HashiCorp, pour codifier l'infrastructure. Les composants de votre infrastructure sont répartis en ressources individuelles (par exemple, matériel physique, comptes utilisateur, etc...). En dissociant les ressources de niveau supérieur et de niveau inférieur, vous pouvez traiter votre infrastructure de la même façon que vous traitez vos logiciels, c'est-à-dire sous forme de code.  

Lorsque vous utilisez {{site.data.keyword.bpshort}}, vous écrivez des configurations pour votre environnement avec une syntaxe déclarative. Vous
décrivez l'apparence que doit avoir votre environnement ; par exemple, vous pouvez
indiquer qu'il doit comporter 10 serveurs
virtuels en production. Le service compare votre configuration à celle créée précédemment par Terraform et ajoute ou retire des ressources si nécessaire. 

{{site.data.keyword.bpshort}} est un outil DevOps collaboratif qui fournit une source unique de données de référence. Vous pouvez stocker des configurations d'environnement dans le contrôle des sources pour permettre à votre équipe d'effectuer des révisions du code, de versionner son infrastructure, d'effectuer le suivi des modifications via l'historique de validation et d'annuler des modifications plus facilement. 

{{site.data.keyword.bpshort}} est mis automatiquement à la disposition de tous les utilisateurs sur votre compte {{site.data.keyword.Bluemix_notm}}. 


## Création d'une configuration
{: #configuration}

Lorsque vous créez une configuration, vous codifiez les ressources de cloud qui composent votre environnement.
{:shortdesc}


Si vous voulez tester un exemple de configuration avec {{site.data.keyword.bpshort}}, procédez comme suit. Dans l'exemple, vous pouvez mettre à disposition une clé SSH à utiliser dans {{site.data.keyword.BluSoftlayer}}. 

**Remarque :** l'exemple de configuration requiert un compte {{site.data.keyword.BluSoftlayer}}. Voir la [documentation relative à la liaison de vos comptes {{site.data.keyword.Bluemix_notm}} et SoftLayer](../../pricing/linking_accounts.html#unifyingaccounts) si vous possédez un compte, ou [créez un compte](https://console.ng.bluemix.net/docs/pricing/index.html#pay-accounts).

1. Générez une paire de clés SSH localement. 
  ```
  ssh-keygen -t rsa
  ```
  {:codeblock}

2. Déviez l'exemple de configuration dans <a href="https://github.com/IBM-Bluemix/tf-bluemix-ssh-key" target="_blank">GitHub <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>. 

  Les exemples ci-dessous présentent des types différents de blocs figurant dans l'exemple de configuration. Vous pouvez afficher la configuration entière dans le fichier `main.tf` du référentiel GitHub. 
  
  * Le bloc provider configure le fournisseur de cloud {{site.data.keyword.IBM_notm}} et les données d'identification de connexion. 

    ```
    provider "ibmcloud" {
      ibmid                    = "${var.ibmid}"
      ibmid_password           = "${var.ibmidpw}"
      softlayer_account_number = "${var.slaccountnum}"
    }
    ```
    {:screen}
  
  * Le bloc resource définit un composant de votre infrastructure, qui dans cet exemple est une clé SSH. 
  
    ```
    resource "ibmcloud_infra_ssh_key" "ssh_key" {
      label = "${var.key_label}"
      notes = "${var.key_note}"
      public_key = "${var.public_key}"
    }
    ```
    {:screen}
  
  * Le bloc variable définit vos variables, que vous pouvez entrer dans l'interface graphique de {{site.data.keyword.bpshort}} pour cet exemple. 
  
    ```
    variable ibmid {
      type = "string"
      description = "Your IBM-ID."
    }
    ```
    {:screen}
  
  * Le bloc output définit les éléments affichés dans la sortie Terraform une fois que vous avez utilisé la configuration pour créer votre environnement et que la ressource (clé SSH) est créée. 
  
    ```
    output "ssh_key_id" {
      value = "${ibmcloud_infra_ssh_key.ssh_key.id}"
    }
    ```
    {:screen}
  
A présent, vous pouvez créer un environnement à partir de votre configuration.  

{:codeblock}

## Création d'un environnement 
{: #environment}

Lorsque vous créez un environnement, vous faites pointer le service vers votre configuration pour qu'il puisse extraire les dernières modifications de code que vous avez apportées.
{:shortdesc}

Avec l'exemple de configuration, procédez comme suit pour créer un environnement. 

1. Dans le menu, sélectionnez **Services**, puis **{{site.data.keyword.bpshort}}**. Le tableau de bord {{site.data.keyword.bpshort}} s'ouvre. 

2. Dans le menu de navigation de gauche, sélectionnez **Environments** et cliquez sur **Create Environment** pour décrire les propriétés relatives à votre configuration. La création d'un environnement définit la façon dont {{site.data.keyword.bpshort}} met à disposition et à jour des ressources de cloud, mais ne crée pas les ressources. 

3. Entrez les détails de votre environnement. L'exemple de configuration requiert les valeurs qui sont répertoriées dans le tableau ci-après. 

  <table summary="Valeurs requises pour que vous puissiez utiliser l'exemple de configuration comme source de votre environnement.">
  <caption>Tableau 1. Valeurs requises pour que vous puissiez utiliser l'exemple de configuration comme source de votre environnement.
  </caption>
  <thead>
  <th colspan="1">Paramètre </th>
  <th colspan="1">Description</th>
  </thead>
  <tbody>
  <tr>
  <td>Source control URL</td>
  <td>Entrez l'adresse URL de GitHub à laquelle vous avez dévié l'exemple de configuration. </td>
  </tr>
  <tr>
  <td>Name</td>
  <td>Entrez un nom unique à affecter à votre environnement. </td>
  </tr>
  <td>Terraform version</td>
  <td>Entrez la version de Terraform pour garantir qu'une version compatible de Terraform est exécutée dans votre environnement. Pour l'exemple de configuration, utilisez la version <code>0.9.1</code>.</td>
  </tr>
  <tr>
  <td>Variables</td>
  <td>Vous pouvez définir des variables dans le service ou remplacer les variables d'environnement qui figurent dans vos fichiers <code>.tf</code>. Vous pouvez masquer les variables sensibles en cliquant sur l'icône de verrouillage. Le masquage des variables empêche les autres utilisateurs d'afficher les valeurs masquées dans la page des détails de l'environnement.
<p>
  <p>Ajoutez les variables et les valeurs suivantes pour pouvoir utiliser l'exemple de configuration :

<ul>
  <li><code>ibmid</code> - Entrez votre {{site.data.keyword.ibmid}} complet comme valeur. </li>
  <li><code>ibmidpw</code> - Entrez le mot de passe associé à votre {{site.data.keyword.ibmid}} et cliquez sur l'icône de verrouillage pour masquer la valeur. </li>
  <li><code>slaccountnum</code> - Entrez votre numéro de compte {{site.data.keyword.BluSoftlayer}}.
   <li><code>datacenter</code> - Entrez le centre de données dans lequel déployer la ressource de clé SSH. Voir le <a href="https://github.com/IBM-Bluemix/tf-bluemix-ssh-key/blob/master/README.md" target="_blank">fichier Readme <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> pour la liste complète des valeurs disponibles. </li> 
   <li><code>public_key</code> - Entrez la clé SSH publique. Pour copier la clé publique dans votre presse-papiers, vous pouvez exécuter la commande <code>pbcopy < ~/.ssh/id_rsa.pub</code>.
   <li><code>key_label</code> - Identifiez la clé avec un nom unique.
   <li><code>key_note</code> - Facultatif : ajoutez une description de la clé SSH. </ul></td>
   </tr></tbody></table>

4. Une fois que vous avez terminé d'indiquer les détails de l'environnement, cliquez sur **Create**. L'environnement créé est affiché.  
5. Pour afficher un aperçu des ressources qui seront mises à disposition ou retirées lorsque vous déploierez votre environnement, cliquez sur **Plan**. 
6. Affichez le journal de plan pour rechercher d'éventuelles erreurs dans la sortie.  
7. Lorsque vous êtes prêt à déployer votre environnement, cliquez sur **Apply**. Vous pouvez surveiller le journal d'application pour déterminer si le déploiement de la clé a abouti. Si le déploiement a réussi, la ligne suivante apparaît vers la fin de la sortie :

  ```
  Apply complete! Resources: 1 added, 0 changed, 0 destroyed.
  ```
  {: screen}

  Vous pouvez aussi afficher la clé SSH
sur
la
page [{{site.data.keyword.slportal}}](https://control.bluemix.net/devices/sshkeys).
8. Facultatif : pour supprimer une clé SSH et l'environnement dans {{site.data.keyword.Bluemix_notm}}, sélectionnez **Destroy resources** dans le menu des actions.

### Etapes suivantes
{: #next}

* Pour en savoir plus sur le déploiement de vos environnements à l'aide d'un programme, [consultez les instructions relatives à l'interface de ligne de commande ou à l'API](schematics_deploying.html).
* Pour créer vos propres configurations à partir de rien, prenez connaissance des <a href="https://ibm-bluemix.github.io/tf-ibm-docs/">ressources de cloud {{site.data.keyword.IBM_notm}} <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>. Les ressources de cloud {{site.data.keyword.IBM_notm}} sont disponibles sous la forme d'un fournisseur de plug-in Terraform. 
