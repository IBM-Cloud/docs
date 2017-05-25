---

copyright:
  years: 2015, 2016
lastupdated: "2017-02-24"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Maintenance et mise à jour des machines virtuelles
{: #maintenance_and_vm_updates}

## Stratégie de maintenance
{: #maintenance_strategy}

IBM WebSphere Application Server in Bluemix est mis à jour régulièrement de sorte à garantir que les nouvelles instances de service soient créées avec les groupes de correctifs et les correctifs les plus récents. Le cloud met à la disposition des équipes de gestion du middleware de nouvelles instances de service facilement et rapidement. En général, de nombreux consommateurs procèdent à la mise à niveau vers une nouvelle instance de service lorsqu'ils veulent assurer la maintenance. Pour les consommateurs qui veulent conserver des instances de service à longue durée de vie, des référentiels de maintenance sont disponibles pour le middleware et l'invité du système d'exploitation sous-jacent. Ceux-ci permettent aux utilisateurs d'assurer la maintenance de leur environnement comme ils le feraient sur site.

## Mises à jour des machines virtuelles

La section ci-après décrit comment appliquer des modifications système aux machines virtuelles.

Vous pouvez mettre à jour votre machine virtuelle de la même façon que n'importe quel système RHEL normal. Avec le gestionnaire de packages Red Hat "Yum", vous pouvez installer, mettre à jour et désinstaller vos packages, entre autres opérations.

Votre système est configuré pour recevoir ces mises à jour depuis le serveur Red Hat Satellite d'IBM. Ce satellite fournit des packages sécurisés et fiables depuis Red Hat Network par le biais du gestionnaire de packages Yum.

Le serveur satellite est géré par IBM et ne peut pas être modifié depuis votre système.

Pour plus d'informations, voir [Applying package updates on Red Hat Enterprise Linux](https://access.redhat.com/articles/11258#rhel6){: new_window} et [Yum, the Red Hat package manager](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Deployment_Guide/ch-yum.html){: new_window}.
