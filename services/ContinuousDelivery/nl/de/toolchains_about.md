---

copyright:
  years: 2015, 2017
lastupdated: "2017-3-31"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Informationen zu Toolchains    
{: #toolchains_about}  

Offene Toolchains stehen in den öffentlichen und den dedizierten Umgebungen von {{site.data.keyword.Bluemix}} (Public bzw. Dedicated) zur Verfügung. Sie können eine Toolchain auf zwei Arten erstellen: Entweder Sie verwenden eine Vorlage zum Erstellen einer Toolchain oder Sie erstellen eine Toolchain aus einer App. Als Ausgangspunkt können Sie eine Toolchain-Vorlage verwenden. Abhängig von der verwendeten Vorlage können Sie eine Toolchain erstellen, die eine bestimmte Gruppe von Toolintegrationen enthält, oder eine leere Toolchain, zu der Sie Toolintegrationen hinzufügen können.    
{:shortdesc}

Abhängig von der verwendeten Vorlage oder Toolchain umfasst die Toolchain in der öffentlichen {{site.data.keyword.Bluemix_notm}}-Umgebung (Bluemix Public) unter Umständen ein GitHub- oder Git-Repository, das den App-Startcode und eine vorkonfigurierte Delivery Pipeline enthält. Wenn Sie Änderungen per Push-Operation an das Repository der Toolchain übertragen, erstellt die Delivery Pipeline automatisch Builds der App und stellt die App in {{site.data.keyword.Bluemix_notm}} bereit.

Abhängig von der verwendeten Vorlage oder Toolchain umfasst die Toolchain in der öffentlichen {{site.data.keyword.Bluemix_notm}}-Umgebung (Bluemix Dedicated) unter Umständen ein GitHub- oder GitHub Enterprise-Repository, das App-Startcode und eine vorkonfigurierte Delivery Pipeline enthält. Wenn Sie Änderungen per Push-Operation an das GitHub- oder GitHub Enterprise-Repository der Toolchain übertragen, erstellt die Delivery Pipeline automatisch Builds der Apps und stellt die Apps in {{site.data.keyword.Bluemix_notm}} bereit.
