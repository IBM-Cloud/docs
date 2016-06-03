---

copyright:
  2015, 2016

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

#Sécurisation des applications
{: #securingapps}

*Dernière mise à jour : 9 mai 2016*

Vous pouvez sécuriser vos applications en téléchargeant des certificats SSL et en limitant l'accès aux applications.
{:shortdesc}

##Création de demandes de signature de certificat
{: #ssl_csr}

Pour pouvoir télécharger les certificats SSL pour lesquels vous disposez d'une habilitation dans {{site.data.keyword.Bluemix}}, vous devez créer une demande de signature
de certificat sur votre serveur.

Une demande de signature de certificat est un message qui est envoyé à une autorité de certification afin de demander la signature d'une clé
publique et des informations associées. En général, les demandes de signature de certificat sont au format PKCS #10. Une demande de signature de
certificat inclut une clé publique ainsi qu'un nom usuel, une organisation, une ville, un état, un pays et une adresse électronique. Les demandes de
certificat SSL ne sont acceptées qu'avec une longueur de clé de demande de signature de certificat de 2048 bits.

Pour que la demande de signature de certificat soit valide, les informations suivantes doivent être indiquées lors de sa génération :

**Nom du pays **
  
  Code à deux chiffres qui représente le pays ou la région. Par exemple, "US" représente les Etats-Unis. Pour les autres pays ou régions, reportez-vous
à la [liste des codes de pays ISO](https://www.iso.org/obp/ui/#search){:new_window} avant de créer la demande de
signature de certificat.
  
**Etat ou province **

  Nom entier non abrégé de l'état ou de la province.

**Localité **

  Nom entier de la ville.
  
**Organisation**

  Nom entier de l'entreprise ou de la société tel qu'enregistré juridiquement auprès de votre localité, ou votre nom. Pour les sociétés, veillez à inclure le suffixe d'enregistrement, par exemple SARL, EURL ou SCI.
  
**Unité organisationnelle **

  Nom de la branche de votre société qui commande le certificat, par exemple Comptabilité ou Marketing.
  
**Nom usuel**

  Nom de domaine complet pour lequel vous demandez le certificat SSL.
  
Les méthodes de création d'une demande de signature de certificat (CSR) varient selon le système d'exploitation. L'exemple suivant montre comment
créer une demande de signature de certificat avec l'[outil de ligne de commande OpenSSL](http://www.openssl.org/){:new_window} :

```
openssl req -out CSR.csr -new -newkey rsa:2048 -nodes -keyout
    privatekey.key
```

**Remarque :** l'implémentation d'OpenSSL SHA-512 dépend du support de compilateur pour le type entier 64 bits. Vous pouvez utiliser
l'option SHA-1 pour les applications qui présentent des problèmes de compatibilité avec le certificat SHA-256.

Un certificat est émis par un organisme de certification et il est signé numériquement par cet organisme. Après avoir créé la demande de signature de certificat, vous pouvez générer votre certificat SSL auprès d'une autorité de certification publique. 

##Téléchargement de certificats SSL
{: #ssl_certificate}

Vous pouvez appliquer un protocole de sécurité pour garantir la confidentialité des communications avec votre
application et empêcher les écoutes clandestines, les altérations et les falsifications de messages

Dans {{site.data.keyword.Bluemix_notm}}, pour chaque organisation dont le propriétaire de compte bénéficie
d'un plan Paiement à la carte ou Abonnement, vous avez droit à quatre téléchargements de certificat gratuits. Pour chaque organisation dont le propriétaire de compte bénéficie d'un compte d'essai gratuit, vous avez droit à un téléchargement de certificat gratuit.

Pour
pouvoir télécharger des certificats, vous devez créer une demande de signature de certificat. Voir [Création de demandes de signature de certificat](#ssl_csr).

Lorsque vous utilisez un domaine personnalisé, pour servir le certificat SSL, utilisez les noeuds finaux de région suivants afin de fournir la route
d'URL allouée à votre organisation dans Bluemix :


  * Sur des Etats-Unis : secure.us-south.bluemix.net 
  * Europe-Royaume-Uni : secure.eu-gb.bluemix.net
  * Australie-Sydney : secure.au-syd.bluemix.net 


Pour télécharger un certificat pour votre application, procédez comme suit :

1. Créez une route ou modifiez une route existante en sélectionnant **Editer les routes et l'accès à l'application** dans le menu de l'application.

2. Dans la boîte de dialogue Editer les routes et l'accès à l'application, cliquez sur **Gestion des domaines**.

3. Pour votre domaine personnalisé, cliquez sur **Télécharger le certificat**.

4. Recherchez et téléchargez un certificat, une clé privée et, éventuellement, un certificat intermédiaire. Vous pouvez également cocher la case pour
autoriser les demandes de certificat client. Si vous sélectionnez cette option, vous devez télécharger un fichier de clés certifiées de certificat
client définissant les accès utilisateur autorisés à votre domaine personnalisé.

  **Certificat**
    
    Document numérique qui associe une clé publique à l'identité du propriétaire
du certificat, permettant ainsi l'authentification du propriétaire du certificat. Un certificat est émis par un organisme de certification et il est signé numériquement par cet organisme.
    
    En général, un certificat est émis et signé par une autorité de certification. Toutefois, pour le test et le développement, vous pouvez
utiliser un certificat autosigné. 
    
    Les types de certificat suivants sont pris en charge dans
{{site.data.keyword.Bluemix_notm}}:

	* PEM (pem, .crt, .cer et .cert)
	* DER (.der ou .cer )
	* PKCS #7 (p7b, p7r, spc)
	  
  **Clé privée**
  
    Canevas algorithmique servant à chiffrer des messages que seule la clé publique correspondante pourra déchiffrer. La clé privée sert également à déchiffrer les messages encodés par la clé publique correspondante. Elle est conservée sur le système de l'utilisateur et protégée par un mot de passe.
    
    Les types de clé privée suivants sont pris en charge dans {{site.data.keyword.Bluemix_notm}}:
    
    * PEM (pem, .key)
    * PKCS #8 (p8, pk8)
    
    **Limitation :** les clés privées protégées par une phrase passe ne peuvent pas être téléchargées.
    
  **Certificat intermédiaire**
  
    Certificat subordonné émis par l'autorité de certification racine accréditée spécifiquement pour émettre
des certificats serveur d'entité de
fin. Le
résultat est une chaîne de certificats qui débute à l'autorité de certification racine accréditée, continue avec le certificat intermédiaire et se finit par
le
certificat SSL émis pour l'organisation.
    
    Il est recommandé d'utiliser un certificat intermédiaire pour vérifier l'authenticité du certificat principal. Les certificats intermédiaires sont généralement obtenus auprès d'un tiers digne de confiance. Vous n'aurez peut-être pas besoin de certificat intermédiaire si vous testez votre application avant de la déployer en production.
  
  **Activer la demande de certificat client**
  
    Si vous activez cette option, un utilisateur qui tente d'accéder à un domaine protégé par SSL doit fournir un certificat côté client. Par exemple, dans un navigateur Web, lorsqu'un utilisateur tente d'accéder à un domaine protégé par SSL, le navigateur Web invite l'utilisateur à fournir
un certificat client pour le domaine. Utilisez l'option de téléchargement de fichier **Magasin de clés de confiance pour les certificats client**
pour définir les certificats client auxquels vous permettez d'accéder à votre domaine personnalisé.
  
  **Remarque :** la fonction de certificat personnalisé dans la gestion des domaines {{site.data.keyword.Bluemix_notm}}
dépend de l'extension SNI (Server
Name Indication) du protocole TLS (Transport Layer Security). Par conséquent, le code client qui accède aux applications
{{site.data.keyword.Bluemix_notm}} protégées par des certificats personnalisés doit prendre en charge
l'extension SNI dans l'implémentation TLS. Pour plus d'informations, voir la
[section 7.4.2 de RFC
4346](http://tools.ietf.org/html/rfc4346#section-7.4.2){:new_window}.

  **Magasin de clés de confiance pour les certificats client**
  
  Ce magasin est un fichier contenant les certificats client pour les utilisateurs que vous désirez autoriser à accéder à votre application. Si vous activez
l'option de demande de certificat client, téléchargez un fichier de magasin de clés de confiance pour les certificats client. 
  
   Les types de certificat suivants sont pris en charge dans
{{site.data.keyword.Bluemix_notm}}:
    
      * PEM (pem, .crt, .cer et .cert)
	  * DER (.der ou .cer )
      * PKCS #7 (p7b, p7r, spc)

Pour supprimer un certificat ou remplacer un certificat existant par un nouveau, accédez à **Gérer les organisations** > **Domaines** > **Afficher le certificat** afin de gérer vos certificats.
