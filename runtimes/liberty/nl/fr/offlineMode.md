---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Mode Hors ligne pour Liberty
{: #offline_mode}

Quand une application Liberty est envoyée par push vers {{site.data.keyword.Bluemix}}, le pack de construction Liberty peut accéder à des sites externes à Bluemix
pour acquérir les artefacts requis par l'application. Les sites externes accessibles au pack de construction Liberty sont répertoriés ci-dessous. Dans les environnements [Bluemix dédié](/docs/dedicated/index.html#dedicated) et
[Bluemix local](/docs/local/index.html#local), ces sites peuvent avoir besoin d'être mis en *liste blanche*.

* https://download.run.pivotal.io et https://java-buildpack.cloudfoundry.org sont utilisés pour accéder aux composants pour :
  * [l'agent AppDynamics ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://www.appdynamics.com/)
  * [le pilote JDBC MariaDB ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://mariadb.com/)
  * [l'agent New Relic](newRelic.html)
  * [OpenJDK](customizingJRE.html#OpenJDK)
  * [le pilote JDBC PostgreSQL ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://www.postgresql.org)
* https://dl.zeroturnaround.com/jrebel/ est utilisé pour accéder aux composants pour [JRebel ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://zeroturnaround.com/software/jrebel/).
* https://download.ruxit.com/agent/paas/cloudfoundry/java est utilisé pour accéder aux composants pour l'[agent Dynatrace Ruxit](dynatrace.html).
* http://downloads.dynatracesaas.com/cloudfoundry/buildpack/java/ est utilisé pour accéder à l'[agent Dynatrace](dynatrace.html).

## Utilisation d'un proxy
{: #working_with_proxy}

Dans certains environnements, comme [Bluemix Dedicated](/docs/dedicated/index.html#dedicated) et
[Bluemix Local](/docs/local/index.html#local), un proxy peut être configuré. Voir
[Utilisation d'un proxy](/docs/manageapps/workingWithProxy.html) pour plus de détails.

# rellinks
{: #rellinks notoc}
## general
{: #general notoc}
* [Environnement d'exécution Liberty](index.html)
* [Présentation de Liberty Profile](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
