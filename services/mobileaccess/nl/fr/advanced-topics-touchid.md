---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-27" 

---

# Autorisation d'accès avec Touch ID
{: #before-you-begin}

Touch ID est une fonctionnalité de reconnaissance d'empreinte digitale pour les appareils iOS. Vous pouvez l'utiliser avec le service {{site.data.keyword.amafull}} pour sécuriser automatiquement les informations d'autorisation pour les accès à venir. 

**Remarque :** Touch ID n'est disponible que dans le SDK {{site.data.keyword.amashort}} Objective-C.

Pour configurer la force de la sécurité, définissez l'une des règles de persistance suivantes avec la méthode
`IMFAuthorizationManager.setAuthorizationPersistencePolicy()`.

* **IMFAuthorizationPersistencePolicyNever** (la plus sécurisée) : Ne jamais conserver les informations d'autorisation sur cet appareil. L'en-tête d'autorisation n'est valide qu'au cours d'une seule session d'application. Les informations d'autorisation sont conservées dans la chaîne de certificats iOS.

* **IMFAuthorizationPersistencePolicyAlways** (la moins sécurisée) : Toujours conserver les informations d'autorisation sur cet appareil, que la technologie Touch ID soit ou non présente, prise en charge ou activée. L'authentification par Touch ID et code d'accès à l'appareil n'est jamais requise.

* **IMFAuthorizationPersistencePolicyWithTouchBiometrics** : Utiliser Touch ID pour extraire les informations d'autorisation de la chaîne de certificats iOS. Cette option est un bon compromis entre sécurité et facilité d'utilisation. Les informations d'autorisation sont conservées uniquement si la
technologie Touch ID est présente, prise en charge et activée. L'authentification par Touch ID ou par le mot de passe de l'appareil est requise pour accéder, une fois par session d'application, aux informations d'autorisation conservées. Une fois cette règle définie, mais si l'accès à Touch ID n'existe pas, par exemple, dans le cas où le matériel nécessaire n'est pas présent ou a été
désactivé, la règle de secours est **IMFAuthorizationPersistancePolicyNever**.
