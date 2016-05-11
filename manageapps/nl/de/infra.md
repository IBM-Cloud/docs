---

 

copyright:

  years: 2016

 

---

{:shortdesc: .shortdesc}

#  Bluemix-Infrastrukturebenen

*Letzte Aktualisierung: 15. März 2016*

{{site.data.keyword.Bluemix_notm}} abstrahiert und verdeckt Betriebssystem- und Infrastrukturebenen, damit diese von Ihnen nicht verwaltet werden müssen. Manchmal kann es jedoch wünschenswert sein, mehr über das Betriebssystem und die Middleware für Ihre App zu wissen.
{:shortdesc}

## Bluemix-Infrastrukturebenen anzeigen
{:viewinfra}

Sie können den Befehl 'cf stacks' ausführen, um die verfügbaren Stacks bzw. Rootdateisysteme anzuzeigen, auf denen Ihre Apps bereitgestellt werden sollen. Sie können bei der Verwendung des Befehls 'cf push' mit der Option *-s* und dem Stacknamen in *stack_name* auch den Stack angeben; dabei ist der 'stack_name' das Stammdateisystem, zum Beispiel `lucid64` oder `cflinuxfs2`:
```
cf push appName -s stack_name
```
Mithilfe des Befehls `cf buildpacks` können Sie die Middlewarekomponenten anzeigen, z. B. WebSphere Liberty Profile und SDK for Node.js; diese sind als Laufzeiten für die Ausführung Ihrer App verfügbar. Des Weiteren können Sie mithilfe des folgenden Befehls
die Laufzeitumgebung für Ihre App angeben:
```
cf push appName -b buildpackname
```
