---

copyright:
  years: 2015, 2016
lastupdated: "2017-02-24"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Wartung und VM-Aktualisierungen
{: #maintenance_and_vm_updates}

## Wartungsstrategie
{: #maintenance_strategy}

IBM WebSphere Application Server in Bluemix wird regelmäßig aktualisiert, sodass sichergestellt ist, dass die neuen Serviceinstanzen mit aktuellen Fixpacks und Patches erstellt werden. Die Cloud bietet eine einfache und schnelle Bereitstellung neuer Serviceinstanzen für das Middleware-Management. Es wird erwartet, dass viele Nutzer ein Upgrade auf eine neue Serviceinstanz durchführen, wenn sie eine Wartung durchführen möchten. Für Nutzer, die langfristigere Serviceinstanzen beibehalten möchten, stehen Wartungsrepositorys für die Middleware und die zugrunde liegende Betriebsgastmaschine zur Verfügung. Mit diesen Repositorys können Benutzer ihre Umgebung so warten, wie sie es lokal tun würden.

## VM-Aktualisierungen

Im folgenden Abschnitt wird die Vorgehensweise beim Anwenden von VM-Systemänderungen erläutert.

Sie können Ihre VM wie jedes andere normale RHEL-System aktualisieren. Mithilfe des Red Hat-Paketmanagers Yum können Sie Pakete unter anderem installieren, aktualisieren und deinstallieren.

Ihr System ist so eingerichtet, dass diese Aktualisierungen über den IBM Red Hat Satellite-Server empfangen werden. Dank diesem Satelliten erhalten Sie über den Paketmanager Yum sichere Pakete von Red Hat Network.

Der Satellite-Server wird von IBM verwaltet und kann nicht von Ihrem System aus geändert werden.

Weitere Informationen finden Sie unter [Applying package updates on Red Hat Enterprise Linux](https://access.redhat.com/articles/11258#rhel6){: new_window} und unter [Yum, the Red Hat package manager](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Deployment_Guide/ch-yum.html){: new_window}.
