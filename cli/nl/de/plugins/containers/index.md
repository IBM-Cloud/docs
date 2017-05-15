---



copyright:

  years: 2015, 2017

lastupdated: "2017-01-12"


---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# IBM Containers CLI
{: #containercli}

*Version:* 1.0.0

IBM Containers CLI ist ein {{site.data.keyword.Bluemix_notm}}-CLI-Plug-in zur Verwaltung von Containern und Containergruppen unter Bluemix.
{: shortdesc}

**Hinweis:** Unter *Voraussetzungen* wird aufgelistet, welche Aktionen vor der Verwendung des Befehls ausgeführt werden müssen. Für Befehle, für die keine Voraussetzungen erfüllt sein müssen, ist **Keine** angegeben. Andernfalls kann mindestens eine der folgenden Aktionen eine Voraussetzung sein:
<dl>
<dt>Endpunkt</dt>
<dd>Vor dem Verwenden des Befehls muss ein API-Endpunkt durch Absetzen des Befehls <code>bluemix api</code> definiert werden.</dd>
<dt>Anmeldung</dt>
<dd>Vor der Verwendung des Befehls ist die Anmeldung über den Befehl <code>bluemix login</code> erforderlich. Verwenden Sie beim Anmelden mit einer eingebundenen ID die Option '--sso' für die Anmeldung mit einmaligem Kenncode.</dd>
<dt>Ziel</dt>
<dd>Vor dem Verwenden des Befehls muss der Befehl <code>bluemix target</code> zum Definieren einer Organisation und eines Bereichs ausgeführt werden.</dd>
<dt>Docker</dt>
<dd>Docker CLI (docker) ist erforderlich, um Befehle im IBM Containers CLI-Plug-in auszuführen.</dd>
</dl>

<table summary="Bluemix-Befehle zur Verwaltung von Containern in Bluemix">
<caption>Tabelle 1. Befehle zur Verwaltung von Containern in Bluemix</caption>
 <thead>
 <th colspan="5">Befehle zur Verwaltung von Containern in Bluemix</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix ic attach](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_attach)</td>
 <td>[bluemix ic build](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_build)</td>
 <td>[bluemix ic cp](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_cp)</td>
 <td>[bluemix ic cpi](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_cpi)</td>
 <td>[bluemix ic exec](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_exec)</td>
 </tr>
 <tr>
 <td>[bluemix ic group-create](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_group_create)</td>
 <td>[bluemix ic group-inspect](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_group_inspect)</td>
 <td>[bluemix ic group-instances](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_group_instances)</td>
 <td>[bluemix ic group-remove](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_group_remove)</td>
 <td>[bluemix ic group-update](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_group_update)</td>
 </tr>
 <tr>
  <td>[bluemix ic groups](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_groups)</td>
  <td>[bluemix ic info](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_info)</td>
  <td>[bluemix ic init](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_init)</td>
  <td>[bluemix ic images](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_images)</td>
  <td>[bluemix ic inspect](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_inspect)</td>
 </tr>
 <tr>
 <td>[bluemix ic ip-bind](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_ip_bind)</td>
 <td>[bluemix ic ip-release](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_ip_release)</td>
 <td>[bluemix ic ip-request](/docs/cli/reference/bluemix_cli/index.html#ip_request)</td>
 <td>[bluemix ic ip-unbind](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_ip_unbind)</td>
 <td>[bluemix ic ips](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_ips)</td>
 </tr>
 <tr>
 <td>[bluemix ic kill](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_kill)</td>
 <td>[bluemix ic logs](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_logs)</td>
 <td>[bluemix ic namespace-get](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_namespace_get)</td>
 <td>[bluemix ic namespace-set](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_namespace_set)</td>
 <td>[bluemix ic pause](/docs/cli/reference/bluemix_cli/index.html#pause)</td>
 </tr>
 <tr>
 <td>[bluemix ic port](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_port)</td>
 <td>[bluemix ic ps](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_ps)</td>
 <td>[bluemix ic rename](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_rename)</td>
 <td>[bluemix ic reprovision](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_reprovision)</td>
 <td>[bluemix ic restart](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_restart)</td>
 </tr>
 <tr>
 <td>[bluemix ic rm](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_rm)</td>
 <td>[bluemix ic rmi](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_rmi)</td>
 <td>[bluemix ic route-map](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_route_map)</td>
 <td>[bluemix ic route-unmap](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_route_unmap)</td>
 <td>[bluemix ic run](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_run)</td>
 </tr>
 <tr>
 <td>[bluemix ic service-bind](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_service_bind)</td>
 <td>[bluemix ic service-unbind](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_service_unbind)</td>
 <td>[bluemix ic start](/docs/cli/reference/bluemix_cli/index.html#ic_start)</td>
 <td>[bluemix ic stats](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_stats)</td>
 <td>[bluemix ic stop](/docs/cli/reference/bluemix_cli/index.html#ic_stop)</td>
 </tr>
 <tr>
 <td>[bluemix ic top](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_top)</td>
 <td>[bluemix ic unpause](/docs/cli/reference/bluemix_cli/index.html#unpause)</td>
 <td>[bluemix ic unprovision](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_unprovision)</td>
 <td>[bluemix ic volume-inspect](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_inspect)</td>
 <td>[bluemix ic volume-create](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_create)</td>
 </tr>
 <tr>
 <td>[bluemix ic volume-fs](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_fs)</td>
 <td>[bluemix ic volume-fs-create](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_fs_create)</td>
 <td>[bluemix ic volume-fs-remove](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_fs_remove)</td>
 <td>[bluemix ic volume-fs-inspect](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_fs_inspect)</td>
 <td>[bluemix ic volume-fs-flavors](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_fs_flavors)</td>
 </tr>
 <tr>
 <td>[bluemix ic volume-remove](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_remove)</td>
 <td>[bluemix ic volumes](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volumes)</td>
 <td>[bluemix ic wait](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_wait)</td>
 <td>[bluemix ic wait-status](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_wait_status)</td>
 <td>[bluemix ic version](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_version)</td>
 </tr>
  </tbody>
 </table>


## bluemix ic attach
{: #bluemix_ic_attach}

Dient zum Steuern eines aktiven Containers oder zum Anzeigen der Ausgabe des Containers. Verwenden Sie die Tastenkombination `STRG+C`, um die Verarbeitung zu beenden und den Container zu stoppen. Dieser Befehl ruft die Docker-CLI auf. Weitere Informationen finden Sie unter dem Befehl [attach ![Symbol für externen Link](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/attach/){: new_window} in der Docker-Hilfe.

```
bluemix ic attach [--no-stdin] [--sig-proxy] CONTAINER
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung, Ziel, Docker

<strong>Befehlsoptionen</strong>:

   <dl>
   <dt>--no-stdin (optional)</dt>
   <dd>Standardeingabe nicht einschließen.</dd>
   <dt>--sig-proxy (optional)</dt>
   <dd>Alle empfangenen Signale an den Prozess weiterleiten. Der Standardwert ist <i>true</i>.</dd>
   <dt><i>CONTAINER</i> (erforderlich)</dt>
   <dd>Der Name oder die ID des Containers.</dd>
    </dl>

<strong>Beispiele</strong>:

Das folgende Beispiel zeigt eine Anforderung für die Zuordnung zum Container `my_container`:
```
bluemix ic attach my_container
```



## bluemix ic build
{: #bluemix_ic_build}

Ruft den Build-Service für IBM Containers auf, um ein Docker-Image lokal oder in Ihrem privaten {{site.data.keyword.Bluemix_notm}}-Repository zu erstellen. Dieser Befehl ruft die Docker-CLI auf. Weitere Informationen finden Sie unter dem Befehl [build ![Symbol für externen Link](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/build/){: new_window} in der Docker-Hilfe.

```
bluemix ic build -t TAG|--tag TAG [--no-cache] [-p|--pull] [-q|--quiet] DOCKERFILE_LOCATION
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung, Ziel, Docker

<strong>Befehlsoptionen</strong>:
   <dl>
   <dt>-t <i>TAG</i>|--tag <i>TAG</i> (erforderlich)</dt>
   <dd>Der Repository-Name, der auf das erstellte Image anzuwenden ist.</dd>
   <dt>--no-cache (optional)</dt>
   <dd>Den Cache nicht verwenden, wenn das Image erstellt wird. Der Standardwert ist <i>false</i>.</dd>
   <dt>--pull (optional)</dt>
   <dd>Versuchen, das Basisimage mit Pull-Operation aus der Registry zu extrahieren, auch wenn es im Cache gespeichert ist.</dd>
   <dt>-q|--quiet (optional)</dt>
   <dd>Die von den Containern generierte ausführliche Ausgabe unterdrücken. Der Standardwert ist <i>false</i>.</dd>
   <dt><i>DOCKERFILE_LOCATION</i> (erforderlich)</dt>
   <dd>Der Pfad zur Dockerfile und zum Kontext auf dem lokalen Host.</dd>
    </dl>

<strong>Beispiele</strong>:

Das folgende Beispiel zeigt eine Anforderung zum Erstellen eines Image mit dem Namen *myimage*. Die Dockerfile und andere im Build zu verwendende Artefakte befinden sich in dem Verzeichnis, in dem der Befehl ausgeführt wird. Da die Registry und der Namensbereich im Imagenamen enthalten sind, wird das Image im privaten {{site.data.keyword.Bluemix_notm}}-Repository Ihrer Organisation erstellt.
```
bluemix ic build -t registry.ng.bluemix.net/mynamespace/myimage .
```


## bluemix ic cp
{: #bluemix_ic_cp}
Kopiert Dateien oder Ordner zwischen einem Container und dem lokalen Dateisystem. Dieser Befehl ruft die Docker-CLI auf. Weitere Informationen finden Sie unter dem Befehl [cp ![Symbol für externen Link](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/cp/){: new_window} in der Docker-Hilfe.


## bluemix ic cpi
{: #bluemix_ic_cpi}

Greift auf ein Docker Hub-Image oder auf ein Image in Ihrer lokalen Registry zu und kopiert das Image in Ihr privates {{site.data.keyword.Bluemix_notm}}-Repository.

```
bluemix ic cpi SOURCE_IMAGE DESTINATION_IMAGE
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung, Ziel

<strong>Befehlsoptionen</strong>:
   <dl>
   <dt><i>SOURCE_IMAGE</i> (erforderlich)</dt>
   <dd>Der Name des Quellenrepositorys und des Quellenimage.</dd>
   <dt><i>DESTINATION_IMAGE</i> (erforderlich)</dt>
   <dd>Die URL des privaten {{site.data.keyword.Bluemix_notm}}-Repositorys, die den Namensbereich und den Namen des Zielimage einschließt. Ein Tag für das Image ist optional.</dd>
   </dl>

<strong>Beispiele</strong>:

Image aus dem Quellenrepository in Ihr privates Repository kopieren und einen Tag für das Image hinzufügen:

```
bluemix ic cpi source_repository/source_image_name private_registry_URL/destination_image_name:tag
```

Das Image `sinatra` aus dem Repository `training` in Ihr privates Repository `registry.ng.bluemix.net/mynamespace` kopieren und das Image mit dem Namen `mysinatra` benennen. Den Tag `v1` für das Image `mysinatra` hinzufügen.

```
bluemix ic cpi training/sinatra registry.ng.bluemix.net/mynamespace/mysinatra:v1
```


## bluemix ic exec
{: #bluemix_ic_exec}

Führt einen Befehl in einem Container aus. Weitere Informationen finden Sie unter dem Befehl [exec ![Symbol für externen Link](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/exec/){: new_window} in der Docker-Hilfe.

```
bluemix ic exec [-d|--detach] [-it] [-u USER|--user USER] CONTAINER [CMD]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung, Ziel, Docker

<strong>Befehlsoptionen</strong>:

   <dl>
   <dt>-d|--detach (optional)</dt>
   <dd>Angegebenen Befehl im Hintergrund ausführen.</dd>
   <dt>-it (optional)</dt>
   <dd>Interaktiver Modus. Anzeige der Standardeingabe beibehalten. Geben Sie <i>exit</i> zum Beenden ein.</dd>
   <dt>-u <i>USER</i>|--user <i>USER</i> (optional)</dt>
   <dd>Der Benutzername.</dd>
   <dt><i>CONTAINER</i> (erforderlich)</dt>
   <dd>Der Name oder die ID des Containers.</dd>
   <dt><i>CMD</i> (optional)</dt>
   <dd>Der in dem angegebenen Container bzw. den angegebenen Containern auszuführende Befehl.</dd>
   </dl>

<strong>Beispiele</strong>:

Befehl `bash` im Container `my_container` im interaktiven Modus ausführen:

```
bluemix ic exec -it my_container bash
```

Befehl `date` im Container `my_container` ausführen:

```
bluemix ic exec my_container date
```


## bluemix ic group-create
{: #bluemix_ic_group_create}

Erstellt eine skalierbare Containergruppe.

```
bluemix ic group-create [--publish,-p PORT] --name GROUP_NAME [--memory,-m MEMORY_SIZE] [-n,--hostname HOSTNAME] [-d,--domain DOMAIN] [--env,-e ENV_KEY=ENV_VAL] [--env-file ENVIRO

NMENT_VARIABLE_FILE] [-P false|true] [--volume] [--min MIN_INSTANCE_COUNT] [--max MAX_INSTANCE_COUNT] [--desired DESIRED_INSTANCE_COUNT] [--anti false|true] [--auto false|true] IMAGE_NAME [CMD [CMD ...]]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung, Ziel

<strong>Befehlsoptionen</strong>:
   <dl>
    <dt><i>IMAGE_NAME</i> (erforderlich)</dt>
   <dd>Das Image, das in jede Containerinstanz in der Containergruppe eingeschlossen werden soll. Sie können Befehle nach dem Image auflisten, fügen Sie jedoch keine Optionen nach dem Image ein. Fügen Sie alle Optionen ein, bevor Sie ein Image angeben. <br><br>Wenn Sie ein Image im privaten {{site.data.keyword.Bluemix_notm}}-Repository Ihrer Organisation verwenden, geben Sie das Image im folgenden Format an: <i>registry.ng.bluemix.net/NAMENSBEREICH/IMAGE</i>. <br><br>Wenn Sie ein Image verwenden, das durch IBM Containers bereitgestellt wird, geben Sie nicht den Namensbereich Ihrer Organisation an. Geben Sie das Image im folgenden Format an: <i>registry.ng.bluemix.net/IMAGE</i>. </dd>
   <dt>--name <i>GROUP_NAME</i> (erforderlich)</dt>
   <dd>Der Gruppe einen Namen zuweisen. <i>-n</i> ist veraltet.<br>
   <strong>Tipp:</strong> Der Containername muss mit einem Buchstaben beginnen. Der Name kann Großbuchstaben, Kleinbuchstaben, Ziffern, Punkte (.), Unterstreichungszeichen (_) oder Bindestriche (-) enthalten.</dd>
   <dt>-m <i>MEMORY_SIZE</i>|--memory <i>MEMORY_SIZE</i> (optional)</dt>
   <dd>Der Gruppe eine Speicherbegrenzung in MB zuweisen. Wenn Sie eine Containergruppe über die CLI erstellen, ist der Standardwert für jede Containerinstanz <i>64</i> MB. Wenn Sie eine Containergruppe über das {{site.data.keyword.Bluemix_notm}}-Dashboard erstellen, ist der Standardwert für jede Containerinstanz <i>256</i> MB. Gültige Werte: <i>64</i>, <i>256</i>, <i>512</i>, <i>1024</i> und <i>2048</i>. Nach der Zuweisung einer Speicherbegrenzung kann der Wert nicht mehr geändert werden.</dd>
   <dt>-n <i>HOSTNAME</i>|--hostname <i>HOSTNAME</i> (optional)</dt>
   <dd>Der Hostname (z. B. <i>mycontainerhost</i>). Der Hostname und der Domänenname werden zum vollständigen Wert der öffentlichen Routen-URL kombiniert. Beispiel: <i>http://mycontainerhost.mybluemix.net</i>. Wenn Sie die Details einer Containergruppe mit dem Befehl <i>bluemix ic group-inspect</i> untersuchen, werden der Host und die Domäne zusammen als Route aufgeführt.</dd>
   <dt>-d <i>DOMAIN</i>|--domain <i>DOMAIN</i> (optional)</dt>
   <dd>Die Domäne lautet in der Regel <i>.mybluemix.net</i>. Der Hostname und der Domänenname werden zum vollständigen Wert der öffentlichen Routen-URL kombiniert. Beispiel: <i>http://mycontainerhost.mybluemix.net</i>. Wenn Sie die Details einer Containergruppe mit dem Befehl <i>bluemix ic group-inspect</i> untersuchen, werden der Host und die Domäne zusammen als Route aufgeführt.</dd>
   <dt>-e <i>ENV_KEY=ENV_VAL</i>|--env <i>ENV_KEY=ENV_VAL</i> (optional)</dt>
   <dd>Legen Sie die Umgebungsvariable fest. Geben Sie mehrere Schlüssel separat an. Wenn Anführungszeichen angegeben werden, geben Sie sie so an, dass der Name und der Wert der Umgebungsvariablen eingeschlossen werden. Beispiel: `-e "schlüssel1=wert1" -e "schlüssel2=wert2" -e "schlüssel3=wert3"`.  In der folgenden Tabelle sind einige häufig verwendete Umgebungsvariablen aufgeführt, die Sie angeben können:</dd>
    </dl>


|  Umgebungsvariable                              |     Beschreibung                            |
| :----------------------------- | :------------------------------ |
| CCS_BIND_APP=*&lt;appname&gt;*       | Bindet einen Service an einen Container. Mit der Umgebungsvariablen `CCS_BIND_APP` können Sie eine App an den Container binden. Die App wird an den Zielservice gebunden und fungiert als Bridge, über die {{site.data.keyword.Bluemix_notm}} die Informationen aus der Umgebungsvariablen `VCAP_SERVICES` Ihrer Bridge-App in die aktive Containerinstanz übertragen kann. Weitere Informationen zur Erstellung einer Bridge-App finden Sie unter [Service an einen Container binden](../../../containers/container_integrations_binding.html){: new_window}. |
| CCS_BIND_SRV=*&lt;service_instanzname1&gt;*,*&lt;service_instanzname2&gt;* | Um einen Bluemix-Service ohne Zuhilfenahme einer Bridge-App direkt an einen Container zu binden, verwenden Sie CCS_BIND_SRV. Diese Bindung ermöglicht Bluemix das Einfügen von VCAP_SERVICES-Informationen in die aktive Containerinstanz. Zum Auflisten mehrerer Bluemix-Services schließen Sie diese als Teil derselben Umgebungsvariablen ein. |
| LOG_LOCATIONS=*&lt;dateipfad&gt;* | Fügt eine Protokolldatei für die Überwachung im Container hinzu. Fügen Sie die Umgebungsvariable `LOG_LOCATIONS` mit einem Pfad zu der Protokolldatei ein. |
{: caption="Tabelle 2. Häufig verwendete Umgebungsvariablen" caption-side="top"}

 <dl>
   <dt>--env-file <i>ENVIRONMENT_VARIABLE_FILE</i> (optional)</dt>
   <dd> Importiert Umgebungsvariablen aus einer Datei. Dabei ist ENVFILE der Pfad zu der Datei im lokalen Verzeichnis. Jede Zeile in der Datei stellt ein Schlüssel=Wert-Paar dar. </dd>
   <dt>--volume <i>VOLUME</i>:<i>CONTAINER_PATH</i>[:ro] (optional)</dt>
   <dd>Datenträger einem Container durch Angabe der Details im Format <i>VolumeId:ContainerPath[:ro]</i> zuordnen.
   <ul>
   <li><i>VOLUME</i>: Die ID oder der Name des Datenträgers.</li>
   <li><i>CONTAINER_PATH</i>: Der absolute Pfad zum Datenträger im Container.</li>
   <li>ro: Optional. Die Angabe <i>ro</i> aktiviert den Schreibschutz des Datenträgers anstelle des standardmäßigen Lese-/Schreibzugriffs.</li></ul>
   </dd>
   <dt>-p <i>PORT</i>|--publish <i>PORT</i> (optional)</dt>
   <dd>Macht den Port für den HTTP-Datenverkehr verfügbar. Container in Ihrer Gruppe müssen über den HTTP-Port empfangsbereit sein. HTTPS-Anforderungen sind nicht möglich. Für Containergruppen können Sie nicht mehrere Ports einschließen. <br><br>Wenn Sie einen Port angeben, machen Sie die App für {{site.data.keyword.Bluemix_notm}} Load Balancer oder Container verfügbar. Anschließend können Bluemix Load Balancer oder die Container den Port verwenden, um den Host und die App in demselben {{site.data.keyword.Bluemix_notm}}-Bereich zu erreichen. Anschließend können die {{site.data.keyword.Bluemix_notm}}-Lastausgleichsfunktion oder -Container den Port verwenden, um den Host und die App im selben {{site.data.keyword.Bluemix_notm}}-Bereich zu erreichen. Wenn ein Port in der Dockerfile für das Image, das Sie verwenden, angegeben ist, schließen Sie diesen Port ein. <br>
   <strong>Tipps</strong>: <ul>
   <li>Für das von IBM zertifizierte Liberty Server-Image oder für eine modifizierte Version dieses Image geben Sie Port 9080 ein.</li>
   <li>Für das von IBM zertifizierte Node.js-Image oder für eine modifizierte Version dieses Image geben Sie Port 8000 ein.</li>
   </ul>
   </dd>
   <dt>-P (optional)</dt>
   <dd>Alle Ports veröffentlichen.</dd>
   <dt>--min <i>MIN_INSTANCE_COUNT</i> (optional)</dt>
   <dd>Die minimale Anzahl von Instanzen. Der Standardwert ist 1. Wenn Sie eine minimale Anzahl von Instanzen festlegen, kann der Wert nach der Erstellung der Containergruppe nicht mehr geändert werden.</dd>
   <dt>--max <i>MAX_INSTANCE_COUNT</i> (optional)</dt>
   <dd>Die maximale Anzahl von Instanzen. Der Standardwert ist 2. Wenn Sie eine maximale Anzahl von Instanzen festlegen, kann der Wert nach der Erstellung der Containergruppe nicht mehr geändert werden.</dd>
   <dt>--desired <i>DESIRED_INSTANCE_COUNT</i> (optional)</dt>
   <dd>Die Anzahl der von Ihnen benötigten Instanzen. Der Standardwert ist 2.</dd>
   <dt>--auto (optional)</dt>
   <dd>Wenn die Containergruppe erstellt wurde und die automatische Wiederherstellung aktiviert ist, überprüft IBM Containers den Status jeder Instanz mit einer HTTP-Anforderung an den Port, der zugewiesen wurde.<br>
   Wenn in zwei aufeinander folgenden Intervallen von 90 Sekunden keine Antwort von einer Containerinstanz empfangen wird, wird die Instanz entfernt und durch eine neue Instanz ersetzt. Wenn der Container antwortet, wird keine Aktion ausgeführt. Dieser Prozess wird kontinuierlich wiederholt. Wenn die Gesamtzahl verschiedener Container, die Mitglieder der Gruppe sind, während eines 30-Minuten-Fensters drei Mal oder mehrmals die maximale Größe der Gruppe überschreitet, wird die automatische Wiederherstellung für die Containergruppe permanent inaktiviert. Zur erneuten Aktivierung der automatischen Wiederherstellung müssen Sie die Containergruppe neu erstellen.</dd>
  <dt>--anti (optional)</dt>
  <dd> Mit anti-affinity kann die Hochverfügbarkeit der Containergruppe optimiert werden. Bei Verwendung der Option --anti werden die einzelnen Containerinstanzen in einer Gruppe auf separate physische Rechenknoten gestellt, was die Wahrscheinlichkeit minimiert, dass alle Container in der Gruppe aufgrund eines Hardwarefehlers ausfallen. Diese Option kann bei größeren Gruppen möglicherweise nicht verwendet werden, da für jede Bluemix-Region und -Organisation nur eine begrenzte Anzahl von Rechenknoten bereitgestellt werden kann. Wenn die Bereitstellung nicht erfolgreich ist, müssen Sie die Anzahl der Containerinstanzen in der Gruppe entweder reduzieren oder die Option --anti entfernen. </dd>
   <dt><i>CMD</i> (optional)</dt>
   <dd>Der Befehl und die Argumente, die an die Containergruppe zur Ausführung übergeben werden. Dieser Befehl muss ein Befehl mit langer Laufzeit sein. Verwenden Sie keinen Befehl mit kurzer Laufzeit, beispielsweise <i>/bin/date</i>, da ein Befehl mit kurzer Laufzeit dazu führen kann, dass der Container abstürzt.  <br> <strong>Hinweise:</strong> <ul>
   <li>Der Befehl und seine Argumente müssen am Ende der Befehlszeile von <i>bluemix ic run</i> kommen.</li>
   <li>Wenn die Befehlsargumente einen Bindestrich (-) enthalten, wie in <i>-c</i> im vorherigen Beispielbefehl, müssen dem Befehl zwei Bindestriche (--) vorangestellt werden.</li>
   </ul></dd>
   </dl>


<strong>Beispiele</strong>:

Containergruppe `my_container_group` unter Verwendung des Image `registry.ng.bluemix.net/ibmnode`, das von IBM Containers bereitgestellt wird, erstellen und anschließend den Befehl `ping localhost` mit langer Laufzeit für diese Containergruppe ausführen:

```
bluemix ic group-create --name my_container_group registry.ng.bluemix.net/ibmnode ping localhost
```

Containergruppe `my_container_group` unter Verwendung des Image `registry.ng.bluemix.net/ibmnode`, das von IBM Containers bereitgestellt wird, erstellen und anschließend den Befehl `tail -f /dev/null` mit langer Laufzeit für diese Containergruppe ausführen:

```
bluemix ic group-create --name my_container_group registry.ng.bluemix.net/ibmnode -- tail -f /dev/null
```

Skalierbare Gruppe `mygroup` mit aktivierter automatischer Wiederherstellung unter Verwendung des Image `registry.ng.bluemix.net/ibmliberty` erstellen. Der Port ist `9080`, der Hostname ist `mycontainerhost` und der Domänenname ist `mybluemix.net`.
```
bluemix ic group-create -p 9080 --auto -n mycontainerhost -d mybluemix.net --name mygroup registry.ng.bluemix.net/ibmliberty
```


## bluemix ic group-inspect
{: #bluemix_ic_group_inspect}

Zeigt detaillierte Informationen an, wie zum Beispiel Umgebungsvariablen, Ports oder Speicher, die für eine Containergruppe bei der Erstellung angegeben wurden.

```
bluemix ic group-inspect CONTAINER_GROUP
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung, Ziel

<strong>Befehlsoptionen</strong>:

   <dl>
   <dt><i>CONTAINER_GROUP</i> (erforderlich)</dt>
   <dd>Die ID oder der Name der Containergruppe.</dd>
   </dl>

<strong>Beispiele</strong>:

Das folgende Beispiel zeigt eine Anforderung zum Überprüfen der Containergruppe `my_group`:
```
bluemix ic group-inspect my_group
```


## bluemix ic group-instances
{: #bluemix_ic_group_instances}

Listet Instanzen einer angegebenen Containergruppe auf.

```
bluemix ic group-instances CONTAINER_GROUP
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung, Ziel

<strong>Befehlsoptionen</strong>:

   <dl>
   <dt><i>CONTAINER_GROUP</i> (erforderlich)</dt>
   <dd>Die ID oder der Name der Containergruppe.</dd>
   </dl>

<strong>Beispiele</strong>:

Alle Instanzen der Containergruppe `my_group` auflisten:
```
bluemix ic group-instances my_group
```


## bluemix ic group-remove
{: #bluemix_ic_group_remove}

Entfernen Sie eine Containergruppe aus einem Bereich.

```
bluemix ic group-remove [-f|--force] GROUP_NAME [GROUP_NAME2 [...]]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung, Ziel

<strong>Befehlsoptionen</strong>:

   <dl>
   <dt>-f|--force (optional)</dt>
   <dd>Erzwingt das Entfernen eines aktiven oder fehlerhaften Containers.</dd>
   <dt><i>GROUP_NAME</i> (erforderlich)</dt>
   <dd>Die ID oder der Name der Containergruppe.</dd>
   </dl>


<strong>Beispiele</strong>:

Das folgende Beispiel ist eine Anforderung zum Entfernen einer Containergruppe, wobei `my_group` der Name der Containergruppe ist.
```
bluemix ic group-remove my_group
```


## bluemix ic group-update
{: #bluemix_ic_group_update}

Aktualisiert eine Containergruppe.


```
bluemix ic group-update [--anti] [--desired DESIRED_INSTANCE_COUNT] [-e ENV_KEY=ENV_VAL] GROUP_NAME
```

**Tipp:** Verwenden Sie zum Aktualisieren des Hostnamens oder der Domäne für eine Containergruppe den Befehl `bluemix ic route-map [-n HOST][-d DOMAIN] CONTAINER_GROUP`.

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung, Ziel

<strong>Befehlsoptionen</strong>:
 <dl>
   <dt>--anti (optional)</dt>
   <dd>Mit anti-affinity kann die Hochverfügbarkeit der Containergruppe optimiert werden. Bei Verwendung der Option --anti werden die einzelnen Containerinstanzen in Ihrer Gruppe auf separate physische Rechenknoten gestellt, was die Wahrscheinlichkeit minimiert, dass bei einem Hardwarefehler alle Container in der Gruppe ausfallen. Diese Option kann bei größeren Gruppen möglicherweise nicht verwendet werden, da für jede Bluemix-Region und -Organisation nur eine begrenzte Anzahl von Rechenknoten bereitgestellt werden kann. Wenn die Bereitstellung nicht erfolgreich ist, müssen Sie die Anzahl der Containerinstanzen in der Gruppe entweder reduzieren oder die Option --anti entfernen.</dd>
   <dt>--desired <i>DESIRED_INSTANCE_COUNT</i> (optional)</dt>
   <dd>Die Anzahl der von Ihnen benötigten Instanzen. Der Standardwert ist <i>2</i>.</dd>
   <dt>-e <i>ENV_KEY=ENV_VAL</i>(optional)</dt>
   <dd>Legen Sie die Umgebungsvariable fest. Geben Sie mehrere Schlüssel separat an. Wenn Anführungszeichen angegeben werden, geben Sie sie so an, dass der Name und der Wert der Umgebungsvariablen eingeschlossen werden. Beispiel: `-e "schlüssel1=wert1" -e "schlüssel2=wert2" -e "schlüssel3=wert3"`.</dd>
   <dt><i>GROUP_NAME</i> (erforderlich)</dt>
   <dd>Die ID oder der Name der Containergruppe.</dd>
   </dl>

<strong>Beispiele</strong>:

Das folgende Beispiel zeigt eine Anforderung zum Aktualisieren der Containergruppe `my_group`:
```
bluemix ic group-update --desired 5 my_group
```


## bluemix ic groups
{: #bluemix_ic_groups}

Listet Containergruppen im privaten {{site.data.keyword.Bluemix_notm}}-Repository der Organisation auf.

```
bluemix ic groups [-q]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung, Ziel

<strong>Befehlsoptionen</strong>:
	<dl>
	<dt>-q (optional)</dt>
   	<dd>Nur Gruppen-IDs anzeigen.</dd>
	</dl>


## bluemix ic images
{: #bluemix_ic_images}

Zeigt eine Liste aller verfügbaren Images im privaten {{site.data.keyword.Bluemix_notm}}-Repository der Organisation an. Weitere Informationen finden Sie unter dem Befehl [images ![Symbol für externen Link](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/images){: new_window} in der Docker-Hilfe. Die Liste umfasst die Image-ID, das Erstellungsdatum und den Imagenamen.

```
bluemix ic images [-a|--all] [-f CONDITION] [--no-trunc] [-q|--quiet]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung, Ziel, Docker

<strong>Befehlsoptionen</strong>:

   <dl>
   <dt>-a|--all (optional)</dt>
   <dd>Alle Image-Layer für jedes Image im Repository Ihrer Organisation einschließen, nicht nur den neuesten Layer.</dd>
   <dt>-f (optional)</dt>
   <dd>Die Liste der Images nach der angegebenen Bedingung filtern.</dd>
   <dt>--no-trunc (optional)</dt>
   <dd>Ausgabe nicht abschneiden.</dd>
   <dt>-q|--quiet (optional)</dt>
   <dd>Nur die numerischen IDs anzeigen.</dd>
   </dl>

<strong>Beispiele</strong>:

Das folgende Beispiel zeigt eine Anforderung zum Empfangen einer Liste der verfügbaren Images für die Organisation:
```
bluemix ic images
```


## bluemix ic info
{: #bluemix_ic_info}

Zeigt eine Gruppe von Informationen an, die den Status der Instanz des Container-Cloud-Service beschreiben. Die Informationen umfassen die Containerbegrenzung, die Containernutzung, die aktiven Container, die Speicherbegrenzung, Speicherbelegung, die variabel verknüpfte IP-Begrenzung, die variabel verknüpfte IP-Nutzung, die CCS-Host-URL, die Registry-Host-URL und den Status des Debugmodus.

```
bluemix ic info
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung, Ziel


## bluemix ic init
{: #bluemix_ic_init}

Initialisiert die Containerumgebung auf Ihrer lokalen Maschine, um den vollen Funktionsumfang des IBM Containers-Service verwenden zu können.

```
bluemix ic init
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung, Ziel

**Hinweis:** Stellen Sie vor der Initialisierung sicher, dass die Docker-CLI (docker) installiert und in Ihrer Umgebungsvariablen PATH konfiguriert ist. Wenn Sie zu einer anderen Region wechseln wollen, verwenden Sie den Befehl `bluemix region-set`.

<strong>Beispiele</strong>:

Wechselt zur Region `us-south`:

```
bluemix region-set us-south
```


## bluemix ic inspect
{: #bluemix_ic_inspect}

Zeigt die Informationen zu einem Container an. Weitere Informationen finden Sie unter dem Befehl [inspect ![Symbol für externen Link](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/inspect){: new_window} in der Docker-Hilfe.

```
bluemix ic inspect [IMAGE|images|CONTAINER]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung, Ziel, Docker

<strong>Befehlsoptionen</strong>:

   <dl>
   <dt><i>IMAGE</i> (erforderlich)</dt>
   <dd>Detaillierte Informationen zu einem bestimmten Image durch Angabe des Namens oder der ID des Image anzeigen.</dd>
   <dt>images (erforderlich)</dt>
   <dd>Detaillierte Informationen zu allen Images in Ihrem Repository anzeigen.</dd>
   <dt><i>CONTAINER</i> (erforderlich)</dt>
   <dd>Detaillierte Informationen zu einem bestimmten Container durch Angabe des Namens oder der ID des Containers anzeigen.</dd>
   </dl>

**Tipp:** Es kann nur jeweils eine der Optionen *IMAGE*, *images* oder *CONTAINER* angegeben werden.

<strong>Beispiele</strong>:

Das folgende Beispiel zeigt eine Anforderung zum Überprüfen eines Containers mit dem Namen `proxy`:
```
bluemix ic inspect proxy
```


## bluemix ic ip-bind
{: #bluemix_ic_ip_bind}

Bindet eine verfügbare, variabel verknüpfte IP-Adresse an einen Container.

```
bluemix ic ip-bind IP_ADDRESS CONTAINER
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung, Ziel

<strong>Befehlsoptionen</strong>:

   <dl>
   <dt><i>IP_ADDRESS</i> (erforderlich)</dt>
   <dd>Die zu bindende IP-Adresse.</dd>
   <dt><i>CONTAINER</i> (erforderlich)</dt>
   <dd>Die ID oder der Name des zu bindenden Containers.</dd>
   </dl>

<strong>Beispiele</strong>:

Das folgende Beispiel zeigt eine Anforderung zum Binden der IP-Adresse `192.123.12.12` an den Container `proxy`:
```
bluemix ic ip-bind 192.123.12.12 proxy
```


## bluemix ic ip-release
{: #bluemix_ic_ip_release}

Gibt eine variabel verknüpfte IP-Adresse von der Instanz des Container-Cloud-Service frei.

```
bluemix ic ip-release IP_ADDRESS [IP_ADDRESS2 [...]]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung, Ziel

<strong>Befehlsoptionen</strong>:

   <dl>
   <dt><i>IP_ADDRESS</i> (erforderlich)</dt>
   <dd>Die freizugebende IP-Adresse.</dd>
   </dl>


## bluemix ic ip-request
{: #ip_request}
Fordert eine neue variabel verknüpfte IP-Adresse an.

```
bluemix ic ip-request [-q]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung, Ziel

<strong>Befehlsoptionen</strong>:

   <dl>
   <dt>-q (optional)</dt>
   <dd>Listet nur die IP-Adressen (ohne IDs) für die Container auf, die an diese IP-Adressen gebunden sind.</dd>
   </dl>


## bluemix ic ip-unbind
{: #bluemix_ic_ip_unbind}

Hebt die Bindung einer variabel verknüpften IP-Adresse an ihren Container auf.

Öffentliche IP-Adressen sind eine begrenzte Ressource in IBM Containers. Daher werden öffentliche IP-Adressen, die einem Bereich zugeordnet und nicht an einen Container gebunden sind, in regelmäßigen, d. h. ungefähr wöchentlichen, Intervallen von freien Testbenutzern zurückgefordert. Nicht gebundene öffentliche IP-Adressen werden nie von Kunden mit nutzungsabhängiger Zahlung oder von Abonnementbenutzern zurückgefordert.

```
bluemix ic ip-unbind IP_ADDRESS CONTAINER
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung, Ziel

<strong>Befehlsoptionen</strong>:

   <dl>
   <dt><i>IP_ADDRESS</i> (erforderlich)</dt>
   <dd>Die IP-Adresse, deren Bindung aufzuheben ist.</dd>
   <dt><i>CONTAINER</i> (erforderlich)</dt>
   <dd>Die ID oder der Name des Containers, dessen Bindung aufzuheben ist.</dd>
   </dl>

<strong>Beispiele</strong>:

Das folgende Beispiel zeigt eine Anforderung zum Aufheben der Bindung der IP-Adresse `192.123.12.12` an den Container `proxy`:
```
bluemix ic ip-unbind 192.123.12.12 proxy
```


## bluemix ic ips
{: #bluemix_ic_ips}

Listet die verfügbaren, variabel verknüpften IP-Adressen für den angemeldeten Benutzer auf. Die Liste umfasst IP-Adressen und die Container-ID, mit der die IP-Adressen verbunden sind. Wenn die IP-Adresse nicht im Gebrauch ist, wird keine Container-ID angezeigt.

```
bluemix ic ips [-q]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung, Ziel

<strong>Befehlsoptionen</strong>:

   <dl>
   <dt>-q (optional)</dt>
   <dd>Listet nur die IP-Adressen (ohne IDs) für die Container auf, die an diese IP-Adressen gebunden sind.</dd>
   </dl>


<strong>Beispiele</strong>:

Das folgende Beispiel zeigt eine Anforderung zum Empfangen einer Liste aller IP-Adressen für die Organisation.
```
bluemix ic ips -q
```


## bluemix ic kill
{: #bluemix_ic_kill}

Stoppt einen aktiven Prozess in einem Container, ohne den Container zu stoppen. Weitere Informationen finden Sie unter dem Befehl [kill ![Symbol für externen Link](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/kill/){: new_window} in der Docker-Hilfe.

```
bluemix ic kill [-s CMD|--signal CMD] CONTAINER
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung, Ziel, Docker

<strong>Befehlsoptionen</strong>:

   <dl>
   <dt>-s <i>CMD</i>|--signal <i>CMD</i> (optional)</dt>
   <dd>Befehl an den Prozess senden, der im Container ausgeführt wird.</dd>
   <dt><i>CONTAINER</i> (erforderlich)</dt>
   <dd>Die ID oder der Name des Containers.</dd>
   </dl>


<strong>Beispiele</strong>:

Das folgende Beispiel zeigt eine Anforderung zum Beenden des Prozesses in einem Container mit dem Namen `proxy`:
```
bluemix ic kill proxy
```


## bluemix ic logs
{: #bluemix_ic_logs}

Zeigt die Ausgabe- oder Fehlerprotokolle für einen aktiven Container an. Weitere Informationen finden Sie unter dem Befehl [logs ![Symbol für externen Link](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/logs/){: new_window} in der Docker-Hilfe.
```
bluemix ic logs [OPTIONS] CONTAINER
```


## bluemix ic namespace-get
{: #bluemix_ic_namespace_get}

Zeigt den Namen des privaten {{site.data.keyword.Bluemix_notm}}-Image-Repositorys für die Organisation an, bei der Sie angemeldet sind.

```
bluemix ic namespace-get
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung, Ziel


## bluemix ic namespace-set
{: #bluemix_ic_namespace_set}

Legt den Namen des privaten {{site.data.keyword.Bluemix_notm}}-Image-Repositorys für die Organisation fest, bei der Sie angemeldet sind.

*Einschränkung:* Im Namen des Namensbereichs Ihres Repositorys kann kein Bindestrich (`-`) verwendet werden.

```
bluemix ic namespace-set NAME
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung, Ziel

<strong>Befehlsoptionen</strong>:

   <dl>
   <dt><i>NAME</i> (erforderlich)</dt>
   <dd>Eine nur einmal ausführbare Funktion zum Festlegen des Repository-Namensbereichs für Ihre Organisation, sofern dieser nicht bereits festgelegt ist. Reinitialisieren Sie IBM Containers nach dem Festlegen des Namensbereichs mit dem Befehl `bluemix ic init`, bevor Sie fortfahren.</dd>
   </dl>


## bluemix ic pause
{: #pause}

Hält alle Prozesse innerhalb eines aktiven Containers an. Weitere Informationen finden Sie unter dem Befehl [pause ![Symbol für externen Link](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/pause/){: new_window} in der Docker-Hilfe. Informationen zum Aufheben des Anhaltens eines Containers finden Sie unter dem Befehl [bluemix ic unpause](#unpause).

```
bluemix ic pause CONTAINER
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung, Ziel, Docker

<strong>Befehlsoptionen</strong>:
   <dl>
   <dt><i>CONTAINER</i> (erforderlich)</dt>
   <dd>Der Name oder die ID des Containers.</dd>
   </dl>

<strong>Antworten:</strong>

- Paused container successfully (Container erfolgreich angehalten)

- Command failed with container cloud service (Befehl für Container-Cloud-Service fehlgeschlagen)

 `{message}`

 Dabei ist `{message}` der zugehörige Fehler.

- Command failed - Could not connect to container cloud service (Befehl fehlgeschlagen - Verbindung zu Container-Cloud-Service konnte nicht hergestellt werden)

<strong>Beispiele</strong>:

Das folgende Beispiel zeigt eine Anforderung zum Anhalten eines Containers mit dem Namen `proxy`:
```
bluemix ic pause proxy
```


## bluemix ic port
{: #bluemix_ic_port}

Listet Portzuordnungen oder eine bestimmte Zuordnung für den Container auf. Dieser Befehl schließt den Befehl `docker port` ein. Weitere Informationen finden Sie unter dem Befehl [port ![Symbol für externen Link](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/port/){: new_window} in der Docker-Hilfe.


## bluemix ic ps
{: #bluemix_ic_ps}
Zeigt eine Liste der Container an, die im Namensbereich des angemeldeten Benutzers aktiv sind. Standardmäßig zeigt dieser Befehl nur Container an, die aktiv sind. Weitere Informationen finden Sie unter dem Befehl [ps ![Symbol für externen Link](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/ps/){: new_window} in der Docker-Hilfe.

```
bluemix ic ps [-a|--all] [--filter env=SEARCH_CRITERIA] [-s|--size] [-l NUM|--limit NUM] [-q|--quiet]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung, Ziel, Docker

<strong>Befehlsoptionen</strong>:

   <dl>
   <dt>-a|--all (optional)</dt>
   <dd>Alle Container anzeigen, d. h. aktive und gestoppte Container.</dd>
   <dt>--filter env=<i>SEARCH_CRITERIA</i> (optional)</dt>
   <dd>Suchcontainer mit einem bestimmten Wert für die Umgebungsvariable. Sie können Ihre Container nach jedem Umgebungsvariablen-Schlüssel oder -Wert filtern, der im Abschnitt 'Env' Ihrer CLI-Antwort aufgelistet wird, wenn Sie einen Container untersuchen. Ersetzen Sie SEARCH_CRITERIA durch den Schlüssel oder Wert, den Sie suchen. Ihre Suchkriterien müssen keine exakten Übereinstimmungen darstellen. </dd>
   <dt>-s|--size (optional)</dt>
   <dd>Die Größen der Container auflisten.</dd>
   <dt>-l <i>NUM</i>|--limit <i>NUM</i> (optional)</dt>
   <dd>Die kürzlich erstellten Container auflisten, wobei <i>NUM</i> die Anzahl der kürzlich erstellten Container ist, die zurückgegeben werden sollen. <br><br> Beispiel: Wenn Sie nacheinander die Container <i>node1</i> bis <i>node5</i>erstellt haben, gibt der Befehl <i>bluemix ic ps --limit 2</i> die Container 'node4' und 'node5' zurück, da diese die beiden zuletzt erstellten Container sind. </dd>
   <dt>-q|--quiet (optional)</dt>
   <dd>Nur Container-IDs anzeigen.</dd>
   </dl>


<strong>Beispiele</strong>:

Das folgende Beispiel zeigt eine Anforderung zum Anzeigen aller aktiven und gestoppten Container:
```
bluemix ic ps -a
```


## bluemix ic rename
{: #bluemix_ic_rename}
Ordnet einem Container einen neuen Namen zu. Weitere Informationen finden Sie unter dem Befehl [rename ![Symbol für externen Link](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/rename/){: new_window} in der Docker-Hilfe.

```
bluemix ic rename OLD_NAME NEW_NAME
```
<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung, Ziel, Docker

<strong>Befehlsoptionen</strong>:

<dl>
   <dt><i>OLD_NAME</i> (erforderlich)</dt>
   <dd>Der alte Name des Containers.</dd>
   <dt><i>NEW_NAME</i> (erforderlich)</dt>
   <dd>Der neue Name des Containers.</dd>
   </dl>


## bluemix ic reprovision
{: #bluemix_ic_reprovision}

Erstellt den IBM Containers-Service erneut in dem Bluemix-Bereich, an dem Sie angemeldet sind. Das ursprüngliche Kontingent für den Bereich wird beibehalten.

<strong>Wichtig</strong>: Bei Ausführung dieses Befehls wird keine(r) Ihrer einzelnen Container und Gruppen in diesem Bereich auf den neu bereitgestellten Bereich migriert, sondern während des Migrationsprozesses entfernt.

```
bluemix ic reprovision [--force|-f] [AVAILABILITY_ZONE]
```
<strong>Befehlsoptionen</strong>:

<dl>
   <dt>--force|-f (optional)</dt>
   <dd>Erzwingt die erneute Erstellung des IBM Containers-Service im Bluemix-Bereich.</dd>
   <dt><i>AVAILABILITY_ZONE</i> (optional)</dt>
   <dd>Der Name der IBM Containers-Verfügbarkeitszone, in der Ihre Container bereitgestellt werden. Wenn keine Verfügbarkeitszone angegeben ist, wird die für die Region definierte Standard-Verfügbarkeitszone verwendet.</dd>
   </dl>


## bluemix ic restart
{: #bluemix_ic_restart}

Startet einen Container erneut. Weitere Informationen finden Sie unter dem Befehl [restart ![Symbol für externen Link](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/restart/){: new_window} in der Docker-Hilfe.

```
bluemix ic restart CONTAINER [-t SECS|--time SECS]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung, Ziel, Docker

<strong>Befehlsoptionen</strong>:

   <dl>
   <dt><i>CONTAINER</i> (erforderlich)</dt>
   <dd>Der Name oder die ID des Containers.</dd>
   <dt>-t <i>SECS</i>|--time <i>SECS</i> (optional)</dt>
   <dd>Die Anzahl Sekunden, die vor dem Neustart des Containers abgewartet werden soll.</dd>
   </dl>


<strong>Antworten:</strong>

- Restarted container successfully (Container erfolgreich erneut gestartet)

- Command failed with container cloud service (Befehl für Container-Cloud-Service fehlgeschlagen)

 `{message}`

 Dabei ist `{message}` der zugehörige Fehler.

- Command failed - Could not connect to container cloud service (Befehl fehlgeschlagen - Verbindung zu Container-Cloud-Service konnte nicht hergestellt werden)

<strong>Beispiele</strong>:

Das folgende Beispiel zeigt eine Anforderung zum erneuten Starten eines Containers mit dem Namen `proxy`:
```
bluemix ic restart proxy
```


## bluemix ic rm
{: #bluemix_ic_rm}

Entfernt einen Container. Weitere Informationen finden Sie unter dem Befehl [rm ![Symbol für externen Link](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/rm/){: new_window} in der Docker-Hilfe.

```
bluemix ic rm [-f|--force] CONTAINER
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung, Ziel, Docker

<strong>Befehlsoptionen</strong>:

   <dl>
   <dt>-f|--force (optional)</dt>
   <dd>Erzwingt das Entfernen eines aktiven oder fehlerhaften Containers.</dd>
   <dt><i>CONTAINER</i> (erforderlich)</dt>
   <dd>Der Name oder die ID des Containers.</dd>
   </dl>

<strong>Antworten:</strong>

- Removed container successfully (Container erfolgreich entfernt)

- Command failed with container cloud service (Befehl für Container-Cloud-Service fehlgeschlagen)

 `{message}`

 Dabei ist `{message}` der zugehörige Fehler.

- Command failed - Could not connect to container cloud service (Befehl fehlgeschlagen - Verbindung zu Container-Cloud-Service konnte nicht hergestellt werden)

<strong>Beispiele</strong>:

Das folgende Beispiel zeigt eine Anforderung zum Entfernen eines Containers mit dem Namen `proxy`:
```
bluemix ic rm proxy
```


## bluemix ic rmi
{: #bluemix_ic_rmi}

Entfernt ein Image aus dem Namensbereich des angemeldeten Benutzers. Weitere Informationen finden Sie unter dem Befehl [rmi ![Symbol für externen Link](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/rmi/){: new_window} in der Docker-Hilfe.

```
bluemix ic rmi [-R REGISTRY|--registry REGISTRY] IMAGE
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung, Ziel, Docker

<strong>Befehlsoptionen</strong>:

   <dl>
   <dt>-R <i>REGISTRY</i>|--registry <i>REGISTRY</i> (optional)</dt>
   <dd>Ändern des Registry-Hosts. Standardmäßig wird die Registry verwendet, die im Befehl <i>bluemix ic init</i> angegeben wird.</dd>
   <dt><i>IMAGE</i> (erforderlich)</dt>
   <dd>Der Name des Image, das entfernt werden soll. Wenn der Imagename nicht mit Tags versehen wird, wird standardmäßig das Image mit dem Tag <i>latest</i> entfernt.</dd>
   </dl>

<strong>Antworten:</strong>

- Removed: `{IMAGE}` (Entfernt: IMAGE)

 Dabei ist `{IMAGE}` der Name des entfernten Image.

- Error! No registry host specified. (Fehler! Es wurde kein Registry-Host angegeben.)

- Image remove failed - Could not connect to container cloud registry (Entfernen des Image fehlgeschlagen - Verbindung zu Container-Cloud-Registry konnte nicht hergestellt werden)

- Command failed with container cloud service (Befehl für Container-Cloud-Service fehlgeschlagen)

 `{message}`

 Dabei ist `{message}` der zugehörige Fehler.

<strong>Beispiele</strong>:

Das folgende Beispiel zeigt eine Anforderung zum Entfernen des Image `mynamespace/myimage:latest`:
```
bluemix ic rmi registry.ng.bluemix.net/mynamespace/myimage:latest
```


## bluemix ic route-map
{: #bluemix_ic_route_map}

Legt die Route für den Internetdatenverkehr fest, die für den Zugriff auf die Containergruppe verwendet werden soll. Mit diesem Befehl können Sie eine neue Route festlegen oder eine vorhandene Route aktualisieren.

```
bluemix ic route-map [-n HOST|--hostname HOST] [-d DOMAIN|--domain DOMAIN] CONTAINER_GROUP
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung, Ziel

<strong>Befehlsoptionen</strong>:

   <dl>
   <dt>-n <i>HOST</i>|--hostname <i>HOST</i> (optional)</dt>
   <dd>Der Hostname für die Route. Der Hostname ist der erste Teil der vollständigen öffentlichen Routen-URL, wie z. B. <i>mycontainerhost</i> in der URL <i>mycontainerhost.mybluemix.net</i>.</dd>
   <dt>-d <i>DOMAIN</i>|--domain <i>DOMAIN</i> (optional)</dt>
   <dd>Der Domänenname für die Route, der den zweiten Teil der vollständigen öffentlichen Routen-URL darstellt. In den meisten Fällen ist die Domäne <i>mybluemix.net</i>. Sie können mit diesem Parameter auch eine private Domäne angeben.</dd>
   <dt><i>CONTAINER_GROUP</i> (erforderlich)</dt>
   <dd>Die ID oder der Name der Containergruppe.</dd>
   </dl>

<strong>Beispiele</strong>:

Das folgende Beispiel zeigt eine Anforderung zum Zuordnen der Route für die Gruppe mit dem Namen `GROUP1`. Dabei ist `my_host` der Hostname und `mybluemix.net` die Domäne.
```
bluemix ic route-map -n my_host -d mybluemix.net GROUP1
```


## bluemix ic route-unmap
{: #bluemix_ic_route_unmap}

Legt die Route für den Internetdatenverkehr fest, die für den Zugriff auf die Containergruppe verwendet werden soll. Mit diesem Befehl können Sie eine neue Route festlegen oder eine vorhandene Route aktualisieren.

```
bluemix ic route-unmap [-n HOST|--hostname HOST] [-d DOMAIN|--domain DOMAIN] CONTAINER_GROUP
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung, Ziel

<strong>Befehlsoptionen</strong>:

   <dl>
   <dt>-n <i>HOST</i>|--hostname <i>HOST</i> (optional)</dt>
   <dd>Der Hostname für die Route.</dd>
   <dt>-d <i>DOMAIN</i>|--domain <i>DOMAIN</i> (optional)</dt>
   <dd>Der Domänenname für die Route.</dd>
   <dt><i>CONTAINER_GROUP</i> (erforderlich)</dt>
   <dd>Die ID oder der Name der Containergruppe.</dd>
   </dl>

<strong>Beispiele</strong>:

Das folgende Beispiel zeigt eine Anforderung zum Aufheben der Zuordnung der Route für die Gruppe mit dem Namen `GROUP1`. Dabei ist `my_host` der Hostname und `organization.com` die Domäne.
```
bluemix ic route-unmap -n my_host -d organization.com GROUP1
```


## bluemix ic run
{: #bluemix_ic_run}

Startet einen neuen Container im Container-Cloud-Service über einen Imagenamen. Weitere Informationen finden Sie unter dem Befehl [run ![Symbol für externen Link](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/run/){: new_window} in der Docker-Hilfe.


```
bluemix ic run [-p PORT|--publish PORT] [-P] [-m MEMORY|--memory MEMORY] [-e ENV|--env ENV] [--volume VOLUME:CONTAINER_PATH] -n NAME|--name NAME [--link NAME:ALIAS] [-it] IMAGE [CMD [CMD ...]]
```
**Hinweis:** Stellen Sie sicher, dass das Cloud Foundry-Befehlstool installiert ist und dass Sie über ein Cloud Foundry-Token verfügen. Durch eine erfolgreiche Anmeldung mit den Befehle `bluemix login` und `bluemix ic init` werden das erforderliche Token und die erforderlichen Zertifikate generiert.


<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung, Ziel, Docker

<strong>Befehlsoptionen</strong>:

   <dl>
   <dt>-p <i>PORT</i>|--publish <i>PORT</i>  (optional)</dt>
   <dd>Macht den Port für den HTTP-Datenverkehr verfügbar. Schließen Sie die Ports ein, die in der Dockerfile für das Image, das Sie verwenden, angegeben sind. Sie können mehrere Ports mit mehreren Optionen <i>-p</i> einschließen. Durch das Verfügbarmachen eines Ports wird automatisch eine öffentliche IP-Adresse an den Container gebunden, wenn eine öffentliche IP-Adresse verfügbar ist. <br><br>Wenn Sie eine bestehende IP-Adresse im Bereich haben, die Sie an den Container binden wollen, können Sie die IP-Adresse angeben, anstatt Sie später zu binden. Die IP-Adresse muss im folgenden Format angegeben werden: &lt;ip-adresse&gt;:&lt;container-port&gt;:&lt;container-port&gt; <br><br>Weitere Informationen zum Anfordern von IP-Adressen für einen Bereich finden Sie unter dem Befehl <a href="index.html#ip_request" target="_blank">bluemix ic ip-request</a>. <br><br>Wenn Sie einen Port angeben, machen Sie die App für {{site.data.keyword.Bluemix_notm}} Load Balancer oder Container in demselben {{site.data.keyword.Bluemix_notm}}-Bereich verfügbar. Anschließend können Bluemix Load Balancer oder die Container den Port verwenden, um den Host zu erreichen. Wenn ein Port in der Dockerfile für das Image, das Sie verwenden, angegeben ist, schließen Sie diesen Port ein. <br><br><strong>Tipps</strong>:<ul><li>Für das von IBM zertifizierte Liberty Server-Image oder für eine modifizierte Version dieses Image geben Sie Port 9080 ein.</li><li>Für das von IBM zertifizierte Node.js-Image oder für eine modifizierte Version dieses Image geben Sie Port 8000 ein.</li></ul></dd>
   <dt>-P (optional)</dt>
   <dd>Die in der Dockerfile für das Image angegebenen Ports automatisch für den HTTP-Datenverkehr verfügbar machen.</dd>
   <dt>-m <i>MEMORY</i>|--memory <i>MEMORY</i> (optional)</dt>
   <dd>Der Gruppe eine Speicherbegrenzung in MB zuweisen. Wenn Sie eine Containergruppe über die CLI erstellen, ist der Standardwert für jede Containerinstanz 64 MB.  Wenn Sie eine Containergruppe über das {{site.data.keyword.Bluemix_notm}}-Dashboard erstellen, ist der Standardwert für jede Instanz 256 MB. Gültige Werte: 64, 256, 512, 1024 und 2048. Nach der Zuweisung einer Speicherbegrenzung kann der Wert nicht mehr geändert werden.</dd>
   <dt>-e <i>ENV</i>|--env <i>ENV</i> (optional)</dt>
   <dd>Die Umgebungsvariable festlegen, wobei <i>ENV</i> ein Schlüssel=Wert-Paar ist. Geben Sie mehrere Schlüssel separat an. Wenn Sie Anführungszeichen angeben, geben Sie sie so an, dass der Name und der Wert der Umgebungsvariablen eingeschlossen werden. Beispiel: -e "schlüssel1=wert1" -e "schlüssel2=wert2" -e "schlüssel3=wert3". In der folgenden Tabelle sind einige häufig verwendete Umgebungsvariablen aufgeführt, die Sie angeben können:</dd>
   </dl>


|      Umgebungsvariable                          |   Beschreibung                              |
| :----------------------------- | :------------------------------ |
| CCS_BIND_APP=*&lt;appname&gt;*       | Bindet einen Service an einen Container. Mit der Umgebungsvariablen `CCS_BIND_APP` können Sie eine App an den Container binden. Die App wird an den Zielservice gebunden und fungiert als Bridge, über die {{site.data.keyword.Bluemix_notm}} die Informationen aus der Umgebungsvariablen `VCAP_SERVICES` Ihrer Bridge-App in die aktive Containerinstanz übertragen kann. Weitere Informationen zur Erstellung einer Bridge-App finden Sie unter [Service an einen Container binden](../../../containers/container_integrations_binding.html){: new_window}. |
| CCS_BIND_SRV=*&lt;service_instanzname1&gt;*,*&lt;service_instanzname2&gt;* | Um einen Bluemix-Service ohne Zuhilfenahme einer Bridge-App direkt an einen Container zu binden, verwenden Sie CCS_BIND_SRV. Diese Bindung ermöglicht Bluemix das Einfügen von VCAP_SERVICES-Informationen in die aktive Containerinstanz. Zum Auflisten mehrerer Bluemix-Services schließen Sie diese als Teil derselben Umgebungsvariablen ein. |
| LOG_LOCATIONS=*&lt;dateipfad&gt;* | Fügt eine Protokolldatei für die Überwachung im Container hinzu. Fügen Sie die Umgebungsvariable `LOG_LOCATIONS` mit einem Pfad zu der Protokolldatei ein. |
{: caption="Tabelle 3. Häufig verwendete Umgebungsvariablen" caption-side="top"}


   <dl>
   <dt>--volume <i>VOLUME</i>:<i>CONTAINER_PATH</i>[:ro] (optional)</dt>
   <dd>Datenträger einem Container durch Angabe der Details im Format <i>VolumeId:ContainerPath[:ro]</i> zuordnen.
   <ul>
   <li><i>VOLUME</i>: Die ID oder der Name des Datenträgers.</li>
   <li><i>CONTAINER_PATH</i>: Der absolute Pfad zum Datenträger im Container.</li>
   <li>ro: Optional. Die Angabe <i>ro</i> aktiviert den Schreibschutz des Datenträgers anstelle des standardmäßigen Lese-/Schreibzugriffs.</li></ul>
   </dd>
   <dt>-n <i>NAME</i>|--name <i>NAME</i> (erforderlich)</dt>
   <dd>Dem Container einen Namen zuweisen. <br> <strong>Tipp:</strong> Der Containername muss mit einem Buchstaben beginnen. Der Name kann Großbuchstaben, Kleinbuchstaben, Ziffern, Punkte (.), Unterstreichungszeichen (_) oder Bindestriche (-) enthalten.</dd>
   <dt>--link <i>NAME</i>:<i>ALIAS</i> (optional)</dt>
   <dd>Wenn ein Container mit einem anderen Container, der aktiv ist, kommunizieren soll, können Sie ihn durch einen Alias für den Hostnamen adressieren.</dd>
   <dt>-it (optional)</dt>
   <dd>Container im interaktiven Modus ausführen. Nach dem Erstellen des Containers die Anzeige der Standardeingabe beibehalten. Geben Sie <i>exit</i> zum Beenden ein.</dd>
   <dt><i>IMAGE</i> (erforderlich)</dt>
   <dd>Das Image, das in den Container eingeschlossen werden soll. Sie können Befehle nach dem Image auflisten, fügen Sie jedoch keine Optionen nach dem Image ein. Fügen Sie alle Optionen vor der Angabe eines Image ein. Fügen Sie alle Optionen ein, bevor Sie ein Image angeben. <br><br>Wenn Sie ein Image im privaten {{site.data.keyword.Bluemix_notm}}-Repository Ihrer Organisation verwenden, geben Sie das Image im folgenden Format an: <i>registry.ng.bluemix.net/NAMENSBEREICH/IMAGE</i>. <br><br>Wenn Sie ein Image verwenden, das durch IBM Containers bereitgestellt wird, geben Sie das Image im folgenden Format an: <i>registry.ng.bluemix.net/IMAGE</i>. </dd>
   <dt><i>CMD</i> (optional)</dt>
   <dd>Der Befehl und die Argumente, die an die Containergruppe zur Ausführung übergeben werden. Dieser Befehl muss ein Befehl mit langer Laufzeit sein. Verwenden Sie keinen Befehl mit kurzer Laufzeit, beispielsweise <i>/bin/date</i>, da ein Befehl mit kurzer Laufzeit dazu führen kann, dass der Container abstürzt.</dd>
   </dl>


<strong>Beispiele</strong>:

Den Befehl `sh -c "while true; do date; sleep 20; done"` mit langer Laufzeit für den Container `my_container` ausführen, der auf dem Image `registry.ng.bluemix.net/ibmnode` erstellt wurde.
```
bluemix ic run --name my_container registry.ng.bluemix.net/ibmnode -- sh -c "while true; do date; sleep 20; done"
```


Container `proxy` unter Verwendung des Image `my_namespace/nginx` erstellen und anschließend mit einer Speicherbegrenzung von `1024` MB starten, wobei `my_namespace` der Namensbereich ist, der den angemeldeten Benutzern zugeordnet ist.
```
bluemix ic run -n proxy -m 1024 registry.ng.bluemix.net/my_namespace/nginx
```

Container mit dem Image `my_namespace/blog` erstellen und starten und die Berechtigungsnachweise als Umgebungsvariablen übergeben. `my_namespace` ist der Namensbereich, der den angemeldeten Benutzern zugeordnet ist.
```
bluemix ic run -n my_container -e USER=johnsmith -e PASS=password registry.ng.bluemix.net/my_namespace/blog
```

Datenträger einem Container unter Verwendung des Image `my_namespace/blog` hinzufügen, wobei `my_namespace` der Namensbereich ist, der den angemeldeten Benutzern zugeordnet ist.
```
bluemix ic run -n my_container -v VolId1:/first/path -v VolId2:/second/path registry.ng.bluemix.net/my_namespace/blog
```


## bluemix ic service-bind
{: #bluemix_ic_service-bind}

Fügt einen Service zu einer aktiven Containergruppe hinzu. Dieser Befehl ist nur für Containergruppen verfügbar. Einzelne Container müssen einen Service im Rahmen des Befehls 'bluemix ic run' binden.

```
bluemix ic service-bind GROUP_NAME SERVICE_INSTANCE
```
<strong>Befehlsoptionen</strong>:

   <dl>
   <dt><i>GROUP_NAME</i> (erforderlich)</dt>
   <dd>Die ID oder der Name der Gruppe.</dd>
   <dt><i>SERVICE_INSTANCE</i> (erforderlich)</dt>
   <dd>Der Name der Serviceinstanz, die zur Containergruppe hinzugefügt werden soll.</dd>
   </dl>


## bluemix ic service-unbind
{: #bluemix_ic_service-unbind}

Entfernt einen Service aus einer aktiven Containergruppe. Dieser Befehl ist nur für Containergruppen verfügbar. Einzelne Container müssen den Container entfernen und einen neuen Container ohne den Service erstellen.

```
bluemix ic service-unbind GROUP_NAME SERVICE_INSTANCE
```
<strong>Befehlsoptionen</strong>:

   <dl>
   <dt><i>GROUP_NAME</i> (erforderlich)</dt>
   <dd>Die ID oder der Name der Gruppe.</dd>
   <dt><i>SERVICE_INSTANCE</i> (erforderlich)</dt>
   <dd>Der Name der Serviceinstanz, die zur Containergruppe hinzugefügt werden soll.</dd>
   </dl>


## bluemix ic start
{: #ic_start}
Startet einen gestoppten Container. Weitere Informationen finden Sie unter dem Befehl [start ![Symbol für externen Link](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/start/){: new_window} in der Docker-Hilfe. Informationen zum Stoppen eines Containers finden Sie unter dem Befehl [bluemix ic stop](#ic_stop).

```
bluemix ic start CONTAINER
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung, Ziel, Docker

<strong>Befehlsoptionen</strong>:

   <dl>
   <dt><i>CONTAINER</i> (erforderlich)</dt>
   <dd>Der Name oder die ID des Containers.</dd>
   </dl>


<strong>Antworten:</strong>

- Started container successfully (Container erfolgreich gestartet)

- Command failed with container cloud service (Befehl für Container-Cloud-Service fehlgeschlagen)

 `{message}`

 Dabei ist `{message}` der zugehörige Fehler.

- Command failed - Could not connect to container cloud service (Befehl fehlgeschlagen - Verbindung zu Container-Cloud-Service konnte nicht hergestellt werden)

<strong>Beispiele</strong>:

Das folgende Beispiel zeigt eine Anforderung zum Starten eines Containers mit dem Namen `proxy`.
```
bluemix ic start proxy
```


## bluemix ic stats
{: #bluemix_ic_stats}

Zeigt Live-Nutzungsstatistiken für einen oder mehrere Container an. Verwenden Sie die Tastenkombination `STRG+C` zum Beenden. Weitere Informationen finden Sie unter dem Befehl [stats ![Symbol für externen Link](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/stats/){: new_window} in der Docker-Hilfe.

```
bluemix ic stats [--no-stream] CONTAINER [CONTAINER]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung, Ziel, Docker

<strong>Befehlsoptionen</strong>:

   <dl>
   <dt><i>CONTAINER</i> (erforderlich)</dt>
   <dd>Der Name oder die ID des Containers.</dd>
   <dt>--no-stream (optional)</dt>
   <dd>Nur das letzte Ergebnis anzeigen und keine vorherigen Informationen einschließen.</dd>
   </dl>

<strong>Beispiele</strong>:

Das folgende Beispiel zeigt eine Anforderung zum Anzeigen der jüngsten Statistiken zu einem Container:
```
bluemix ic stats --no-stream my_container
```


## bluemix ic stop
{: #ic_stop}
Stoppt einen aktiven Container. Weitere Informationen finden Sie unter dem Befehl [stop ![Symbol für externen Link](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/stop/){: new_window} in der Docker-Hilfe. Informationen zum Starten eines Containers finden Sie unter dem Befehl [bluemix ic start](#ic_start).

```
bluemix ic stop CONTAINER [-t SECS|--time SECS]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung, Ziel, Docker

<strong>Befehlsoptionen</strong>:

   <dl>
   <dt><i>CONTAINER</i> (erforderlich)</dt>
   <dd>Der Name oder die ID des Containers.</dd>
   <dt>-t <i>SECS</i>|--time <i>SECS</i> (optional)</dt>
   <dd>Die Anzahl Sekunden, die vor dem Stoppen des Containers abgewartet werden soll.</dd>
   </dl>

<strong>Antworten:</strong>

- Stopped container successfully (Container erfolgreich gestoppt)

- Command failed with container cloud service (Befehl für Container-Cloud-Service fehlgeschlagen)

 `{message}`

 Dabei ist `{message}` der zugehörige Fehler.

- Command failed - Could not connect to container cloud service (Befehl fehlgeschlagen - Verbindung zu Container-Cloud-Service konnte nicht hergestellt werden)

<strong>Beispiele</strong>:

Das folgende Beispiel zeigt eine Anforderung zum Stoppen eines Containers mit dem Namen `proxy`.
```
bluemix ic stop proxy
```


## bluemix ic top
{: #bluemix_ic_top}

Zeigt die Prozesse an, die im Container ausgeführt werden. Weitere Informationen finden Sie unter dem Befehl [top ![Symbol für externen Link](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/top/){: new_window} in der Docker-Hilfe.

```
bluemix ic top CONTAINER [CONTAINER]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung, Ziel, Docker

<strong>Befehlsoptionen</strong>:

   <dl>
   <dt><i>CONTAINER</i> (erforderlich)</dt>
   <dd>Der Name oder die ID des Containers.</dd>
   </dl>

<strong>Beispiele</strong>:

Das folgende Beispiel zeigt eine Anforderung zum Anzeigen der Prozesse in einem Container mit dem Namen `my_container`.
```
bluemix ic top my_container
```


## bluemix ic unpause
{: #unpause}

Hebt das Anhalten aller Prozesse innerhalb eines aktiven Containers auf. Weitere Informationen finden Sie unter dem Befehl [unpause ![Symbol für externen Link](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/unpause/){: new_window} in der Docker-Hilfe. Informationen zum Anhalten eines Containers finden Sie unter dem Befehl [bluemix ic pause](#pause).

```
bluemix ic unpause CONTAINER
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung, Ziel, Docker

<strong>Befehlsoptionen</strong>:

   <dl>
   <dt><i>CONTAINER</i> (erforderlich)</dt>
   <dd>Der Name oder die ID des Containers.</dd>
   </dl>

<strong>Antworten:</strong>

- Unpaused container successfully (Anhalten des Containers erfolgreich aufgehoben)

- Command failed with container cloud service (Befehl für Container-Cloud-Service fehlgeschlagen)

 `{message}`

 Dabei ist `{message}` der zugehörige Fehler.

- Command failed - Could not connect to container cloud service (Befehl fehlgeschlagen - Verbindung zu Container-Cloud-Service konnte nicht hergestellt werden)

<strong>Beispiele</strong>:

Das folgende Beispiel zeigt eine Anforderung zum Aufheben des Anhaltens eines Containers mit dem Namen `proxy`:
```
bluemix ic unpause proxy
```


## bluemix ic unprovision
{: #bluemix_ic_unprovision}

Löscht den IBM Containers-Service aus dem Bluemix-Bereich, an dem Sie angemeldet sind.

<strong>Achtung</strong>: Bei Ausführung dieses Befehls gehen alle einzelnen Container und Containergruppen verloren. Ihr Bereich steht in Bluemix weiterhin zur Verfügung. Zur erneuten Verwendung von IBM Containers müssen Sie `bluemix ic reprovision` ausführen, um den IBM Containers-Service erneut bereitzustellen.

```
bluemix ic reprovision [--force|-f]
```
<strong>Befehlsoptionen</strong>:

<dl>
   <dt>--force|-f (optional)</dt>
   <dd>Erzwingt die Löschung von Bluemix aus dem Bluemix-Bereich.</dd>
 </dl>


## bluemix ic version
{: #bluemix_ic_version}

Zeigt die Version von Docker und der IBM Containers-API an.

```
bluemix ic version
```

<strong>Voraussetzungen</strong>: Docker

Zum Anzeigen der Version von IBM Containers führen Sie den Befehl `bluemix ic info` aus. Weitere Informationen finden Sie unter dem Befehl [version ![Symbol für externen Link](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/version/){: new_window} in der Docker-Hilfe.


## bluemix ic volume-create
{: #bluemix_ic_volume_create}

Erstellt einen Datenträger.

```
bluemix ic volume-create VOLUME_NAME FS_NAME
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung, Ziel

<strong>Befehlsoptionen</strong>:

   <dl>
   <dt><i>FS_NAME</i> (optional)</dt>
   <dd>Der Name der Dateifreigabe. Wenn keine Datei verfügbar oder benannt ist, wird der Datenträger auf der Standard-Dateifreigabe des Bereichs aufgebaut.</dd>
   <dt><i>VOLUME_NAME</i> (erforderlich)</dt>
   <dd>Der Name des Datenträgers. Der Name kann Kleinbuchstaben, Ziffern, Unterstreichungszeichen (_) und Bindestriche (-) enthalten.</dd>
   </dl>


<strong>Beispiele</strong>:

Das folgende Beispiel zeigt eine Anforderung zum Erstellen eines Datenträgers.
```
bluemix ic volume-create volume_name fileshare_name
```


## bluemix ic volume-fs
{: #bluemix_ic_volume_fs}

Auflistung der Dateifreigaben.

```
bluemix ic volume-fs
```


## bluemix ic volume-fs-create
{: #bluemix_ic_volume_fs_create}

Erstellen Sie eine Dateifreigabe.

```
bluemix ic volume-fs-create FILE_SHARE_NAME
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung, Ziel

<strong>Befehlsoptionen</strong>:

   <dl>
   <dt><i>FILE_SHARE_NAME</i> (erforderlich)</dt>
   <dd>Der Name der Dateifreigabe. Der Name kann Kleinbuchstaben, Ziffern, Unterstreichungszeichen (_) und Bindestriche (-) enthalten.</dd>
   </dl>

<strong>Beispiele</strong>:

Das folgende Beispiel zeigt eine Anforderung zum Erstellen einer Dateifreigabe.
```
bluemix ic volume-fs-create my_file_share
```


## bluemix ic volume-fs-flavors
{: #bluemix_ic_volume_fs_flavors}

Alle Versionen der Dateifreigaben auflisten.

```
bluemix ic volume-fs-flavors
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung, Ziel


## bluemix ic volume-fs-inspect
{: #bluemix_ic_volume_fs_inspect}

Eine Dateifreigabe überprüfen.

```
bluemix ic volume-fs-inspect FILE_SHARE_NAME
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung, Ziel

<strong>Befehlsoptionen</strong>:

  <dl>
  <dt><i>FILE_SHARE_NAME</i> (erforderlich)</dt>
   <dd>Der Name der Dateifreigabe.</dd>
   </dl>

<strong>Beispiele</strong>:

Das folgende Beispiel zeigt eine Anforderung zum Überprüfen einer Dateifreigabe. Dabei ist `my_file_share` der Name der Dateifreigabe.
```
bluemix ic volume-fs-inspect my_file_share
```


## bluemix ic volume-fs-remove
{: #bluemix_ic_volume_fs_remove}

Entfernen Sie eine Dateifreigabe.

```
bluemix ic volume-fs-remove FILE_SHARE_NAME
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung, Ziel

<strong>Befehlsoptionen</strong>:

   <dl>
   <dt><i>FILE_SHARE_NAME</i> (erforderlich)</dt>
   <dd>Der Name der Dateifreigabe.</dd>
   </dl>

<strong>Beispiele</strong>:

Das folgende Beispiel zeigt eine Anforderung zum Entfernen einer Dateifreigabe. Dabei ist `my_file_share` der Name der Dateifreigabe.
```
bluemix ic volume-fs-remove my_file_share
```


## bluemix ic volume-inspect
{: #bluemix_ic_volume_inspect}

Überprüft einen Datenträger.

```
bluemix ic volume-inspect VOLUME_NAME
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung, Ziel

<strong>Befehlsoptionen</strong>:

   <dl>
   <dt><i>VOLUME_NAME</i> (erforderlich)</dt>
   <dd>Der Name des Datenträgers.</dd>
   </dl>

<strong>Beispiele</strong>:

Das folgende Beispiel zeigt eine Anforderung zum Überprüfen des Datenträgers. Dabei ist `volume_name` der Name des Datenträgers.
```
bluemix ic volume-inspect volume_name
```


## bluemix ic volume-remove
{: #bluemix_ic_volume_remove}

Entfernt einen Datenträger.

```
bluemix ic volume-remove VOLUME_NAME
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung, Ziel

<strong>Befehlsoptionen</strong>:

   <dl>
   <dt><i>VOLUME_NAME</i> (erforderlich)</dt>
   <dd>Der Name des Datenträgers.</dd>
    </dl>

<strong>Beispiele</strong>:

Das folgende Beispiel zeigt eine Anforderung zum Entfernen eines Datenträgers. Dabei ist `volume_name` der Name des Datenträgers.
```
bluemix ic volume-remove volume_name
```


## bluemix ic volumes
{: #bluemix_ic_volumes}

Listet Datenträger auf.

```
bluemix ic volumes
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung, Ziel


## bluemix ic wait
{: #bluemix_ic_wait}

Beendet einen Container und zeigt den Beendigungscode als Bestätigung an. Weitere Informationen finden Sie unter dem Befehl [wait ![Symbol für externen Link](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/wait/){: new_window} in der Docker-Hilfe.

```
bluemix ic wait CONTAINER [CONTAINER]
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung, Ziel, Docker

<strong>Befehlsoptionen</strong>:

   <dl>
   <dt><i>CONTAINER</i> (erforderlich)</dt>
   <dd>Der Name oder die ID des Containers.</dd>
   </dl>

<strong>Beispiele</strong>:

Das folgende Beispiel zeigt eine Anforderung zum Beenden eines Containers mit dem Namen `my_container`:
```
bluemix ic wait my_container
```


## bluemix ic wait-status
{: #bluemix_ic_wait_status}

Wartet, bis ein einzelner Container oder eine Containergruppe in einen nicht-transienten Status wechselt. In dieser Zeit gibt die Befehlszeile keine Daten zurück und Sie können keine Befehle eingeben. Sobald der Container in einen nicht-transienten Status wechselt, wird eine Bestätigungsnachricht angezeigt. Bei einzelnen Containern lauten die nicht-transienten Status 'Running' (Aktiv), 'Shutdown' (Heruntergefahren), 'Crashed' (Ausgefallen), 'Paused' (Angehalten) und 'Suspended' (Ausgesetzt). Bei Containergruppen lauten die nicht-transienten Status CREATE_COMPLETE, UPDATE_COMPLETE und FAILED.

```
bluemix ic wait-status CONTAINER
```

<strong>Voraussetzungen</strong>: Endpunkt, Anmeldung, Ziel, Docker

<strong>Befehlsoptionen</strong>:

   <dl>
   <dt><i>CONTAINER</i> (erforderlich)</dt>
   <dd>Der Name oder die ID des Containers.</dd>
   </dl>

<strong>Beispiele</strong>:

Das folgende Beispiel zeigt eine Anforderung zum Beenden eines Containers mit dem Namen `my_container`:
```
bluemix ic wait my_container
```
