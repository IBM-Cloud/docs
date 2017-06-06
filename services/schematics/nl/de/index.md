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

# Einführung in {{site.data.keyword.bpfull_notm}} (Beta)
{: #gettingstarted}

{{site.data.keyword.bplong}} ist ein Automatisierungstool, das Sie verwenden können, um die Cloudinfrastruktur als eine einzige Einheit definieren und bereitstellen und die Cloudressourcendefinitionen für eine beliebige Anzahl von Umgebungen wiederverwenden zu können.{:shortdesc}

{{site.data.keyword.bpshort}} verwendet Terraform von HashiCorp, um die Infrastruktur zu codifizieren. Die Komponenten Ihrer Infrastruktur werden in einzelne Ressourcen heruntergebrochen, bei denen es sich um verschiedenste Ressourcen handeln kann, von physischer Hardware bis hin zu Benutzerkonten. Durch Abstrahieren übergeordneter und untergeordneter Ressourcen können Sie Ihre Infrastruktur wie Ihre eigene Software als Code behandeln. 

Wenn Sie mit {{site.data.keyword.bpshort}} arbeiten, schreiben Sie Konfigurationen für Ihre Umgebung in deklarativer Syntax. Sie können angeben, wie Ihre Umgebung aussehen soll, z. B. mit 10 {{site.data.keyword.virtualmachinesshort}} in der Produktion. Der Service vergleicht Ihre Konfiguration mit der, die Terraform zuvor erstellt hat, und fügt Ressourcen nach Bedarf hinzu oder entfernt sie.

{{site.data.keyword.bpshort}} ist ein interaktives DevOps-Tool, das einen Single Source of Truth für die Infrastruktur bereitstellt. Sie können Umgebungskonfigurationen in der Quellcodeverwaltung speichern, wodurch Ihr Team die Möglichkeit erhält, Codeprüfungen durchzuführen, die eigene Infrastruktur zu versionieren, Änderungen mittels Festschreibungsverlauf zu verfolgen und Änderungen einfacher zurückzusetzen.

{{site.data.keyword.bpshort}} ist automatisch für alle Benutzer in Ihrem {{site.data.keyword.Bluemix_notm}}-Konto verfügbar.


## Konfiguration erstellen
{: #configuration}

Wenn Sie eine Konfiguration erstellen, codifizieren Sie die Cloudressourcen, aus denen sich Ihre Umgebung zusammensetzt.{:shortdesc}


Wenn Sie eine Beispielkonfiguration mit {{site.data.keyword.bpshort}} ausprobieren möchten, führen Sie die folgenden Schritte aus. In dem Beispiel können Sie einen SSH-Schlüssel bereitstellen, der in {{site.data.keyword.BluSoftlayer}} verwendet werden soll. 

**Hinweis: ** Die Beispielkonfiguration erfordert ein {{site.data.keyword.BluSoftlayer}}-Konto. Siehe dazu das Dokument [{{site.data.keyword.Bluemix_notm}}- und SoftLayer-Konten verknüpfen](../../pricing/linking_accounts.html#unifyingaccounts), wenn Sie über ein bestehendes Konto verfügen, oder Sie können sich [für ein Konto anmelden](https://console.ng.bluemix.net/docs/pricing/index.html#pay-accounts).

1. Generieren Sie ein SSH-Schlüsselpaar lokal.
  ```
  ssh-keygen -t rsa
  ```
  {:codeblock}

2. Verzweigen Sie die Beispielkonfiguration in <a href="https://github.com/IBM-Bluemix/tf-bluemix-ssh-key" target="_blank">GitHub <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>. 

  Die folgenden Beispiele zeigen verschiedene Arten von Blöcken, die in der Beispielkonfiguration vorhanden sind. Die vollständige Konfiguration wird in der `main.tf`-Datei des GitHub-Repositorys angezeigt.
  
  * Der Provider-Block richtet die {{site.data.keyword.IBM_notm}} Cloud-Provider und Anmeldeberechtigungsnachweise ein.

    ```
    provider "ibmcloud" {
      ibmid                    = "${var.ibmid}"
      ibmid_password           = "${var.ibmidpw}"
      softlayer_account_number = "${var.slaccountnum}"
    }
    ```
    {:screen}
  
  * Der Ressourcenblock definiert eine Komponente Ihrer Infrastruktur, die in diesem Beispiel ein SSH-Schlüssel ist.
  
    ```
    resource "ibmcloud_infra_ssh_key" "ssh_key" {
      label = "${var.key_label}"
      notes = "${var.key_note}"
      public_key = "${var.public_key}"
    }
    ```
    {:screen}
  
  * Der Variablenblock definiert Ihre Variablen, die Sie in der {{site.data.keyword.bpshort}}-GUI für dieses Beispiel eingeben können.
  
    ```
    variable ibmid {
      type = "string"
      description = "Your IBM-ID."
    }
    ```
    {:screen}
  
  * Der Ausgabeblock definiert, was in der Terraform-Ausgabe angezeigt wird, nachdem die Konfiguration zur Erstellung Ihrer Umgebung verwendet und die Ressource (SSH-Schlüssel) erstellt wurde.
  
    ```
    output "ssh_key_id" {
      value = "${ibmcloud_infra_ssh_key.ssh_key.id}"
    }
    ```
    {:screen}
  
Sie können jetzt eine Umgebung aus Ihrer Konfiguration erstellen. 

{:codeblock}

## Umgebung erstellen
{: #environment}

Wenn Sie eine Umgebung erstellen, verweisen Sie den Service auf Ihre Konfiguration, sodass der Service Ihre neuesten Codeänderungen extrahieren kann.{:shortdesc}

Führen Sie anhand der Beispielkonfiguration die folgenden Schritte durch, um eine Umgebung zu erstellen.

1. Wählen Sie im Menü die Option **Services** und anschließend **{{site.data.keyword.bpshort}}** aus. Sie werden an das {{site.data.keyword.bpshort}}-Dashboard weitergeleitet.

2. Wählen Sie im linken Navigationsmenü die Option **Umgebungen** aus und klicken Sie auf **Umgebung erstellen**, um Eigenschaften Ihrer Konfiguration zu beschreiben. Mit dem Erstellen einer Umgebung wird definiert, wie {{site.data.keyword.bpshort}} Cloudressourcen bereitstellt und aktualisiert, aber es werden noch keine Ressourcen erstellt.

3. Geben Sie Informationen zu Ihrer Umgebung ein. Die Beispielkonfiguration erfordert die Werte, die in der folgenden Tabelle aufgelistet sind.

  <table summary="Die Werte, die erforderlich sind, um die Beispielkonfiguration als Quelle für Ihre Umgebung zu verwenden.">
  <caption>Tabelle 1. Die Werte, die erforderlich sind, damit Sie die Beispielkonfiguration als Quelle für Ihre Umgebung verwenden können.</caption>
  <thead>
  <th colspan="1">Einstellung</th>
  <th colspan="1">Beschreibung</th>
  </thead>
  <tbody>
  <tr>
  <td>URL für die Quellcodeverwaltung</td>
  <td>Geben Sie die GitHub-URL ein, in der Sie die Beispielkonfiguration verzweigt haben.</td>
  </tr>
  <tr>
  <td>Name</td>
  <td>Geben Sie einen eindeutigen Namen ein, der Ihrer Umgebung zugeordnet werden soll.</td>
  </tr>
  <td>Terraform-Version</td>
  <td>Geben Sie die Version von Terraform ein, um sicherzustellen, dass eine kompatible Version von Terraform für Ihre Umgebung ausgeführt wird. Für die Beispielkonfiguration verwenden Sie die Version <code>0.9.1</code>.</td>
  </tr>
  <tr>
  <td>Variablen</td>
  <td>Sie können Variablen im Service definieren oder Umgebungsvariablen überschreiben, die sich in Ihren <code>.tf </code>-Dateien befinden. Sie können sensible Variablen maskieren, wenn Sie auf das Sperrsymbol klicken. Durch das Maskieren einer Variablen wird verhindert, dass andere Benutzer die ausgeblendeten Werte auf der Seite für Umgebungsdetails sehen.<p>
  <p>Fügen Sie die folgenden Variablen und Werte hinzu, um mit der Beispielkonfiguration zu arbeiten:
  <ul>
  <li><code>ibmid</code> - Geben Sie Ihre vollständige {{site.data.keyword.ibmid}} als Wert ein.</li>
  <li><code>ibmidpw</code> - Geben Sie das Kennwort ein, das Ihrer {{site.data.keyword.ibmid}} zugeordnet ist, und klicken Sie auf das Sperrsymbol, um den Wert zu maskieren.</li>
  <li><code>slaccountnum</code> - Geben Sie die Nummer Ihres {{site.data.keyword.BluSoftlayer}}-Kontos ein.
   <li><code>datacenter</code> - Geben Sie das Rechenzentrum ein, auf dem Sie die SSH-Schlüssel-Ressource bereitstellen möchten. In der <a href="https://github.com/IBM-Bluemix/tf-bluemix-ssh-key/blob/master/README.md" target="_blank">Readme-Datei <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> finden Sie eine vollständige Liste der verfügbaren Werte.</li> 
   <li><code>public_key</code> - Geben Sie den öffentlichen SSH-Schlüssel ein. Um den öffentlichen Schlüssel in die Zwischenablage zu kopieren, können Sie den Befehl <code>pbcopy < ~/.ssh/id_rsa.pub</code> ausführen.<li><code>key_label</code> - Geben Sie den Schlüssel mit einem eindeutigen Namen an.<li><code>key_note</code> - Optional: Fügen Sie einen beschreibenden Text über den SSH-Schlüssel hinzu.</ul></td>
   </tr></tbody></table>

4. Wenn Sie die Details zur Umgebung ausgefüllt haben, klicken Sie auf **Erstellen**. Die neu erstellte Umgebung wird angezeigt. 
5. Um eine Vorschau anzuzeigen, welche Ressourcen bereitgestellt oder entfernt werden, wenn Sie Ihre Umgebung bereitstellen, klicken Sie auf **Plan**. 
6. Sie können das Planprotokoll anzeigen, um die Ausgabe auf Fehler zu untersuchen. 
7. Wenn Sie bereit sind, Ihre Umgebung bereitzustellen, klicken Sie auf **Anwenden**. Sie können das Anwendungsprotokoll überwachen, um zu sehen, ob der Schlüssel erfolgreich bereitgestellt wurde. Eine erfolgreiche Bereitstellung zeigt die folgende Zeile am Ende der Ausgabe an: 

  ```
  Apply complete! Resources: 1 added, 0 changed, 0 destroyed.
  ```
  {: screen}

  Sie können den SSH-Schlüssel auch in der [{{site.data.keyword.slportal}}](https://control.bluemix.net/devices/sshkeys) anzeigen.
8. Optional: Um den SSH-Schlüssel und die Umgebung aus {{site.data.keyword.Bluemix_notm}} zu entfernen, wählen Sie im Menü "Aktionen" die Option **Ressourcen vernichten** aus.

### Weitere Schritte
{: #next}

* Um mehr über die programmgestützte Bereitstellung Ihrer Umgebungen herauszufinden, [prüfen Sie die CLI oder die API](schematics_deploying.html).
* Um Ihre eigenen Konfigurationen von Grund auf neu zu erstellen, lesen Sie die <a href="https://ibm-bluemix.github.io/tf-ibm-docs/">{{site.data.keyword.IBM_notm}} Cloudressourcen in <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>.{{site.data.keyword.IBM_notm}} Cloudressourcen stehen als Terraform-Plug-in-Provider zur Verfügung. 
