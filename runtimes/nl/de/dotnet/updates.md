---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Neueste Aktualisierungen für das Buildpack 'ASP.NET Core'
{: #latest_updates}

*Letzte Aktualisierung: 10. Juni 2016*

Eine Liste mit den neuesten Aktualisierungen im aspnet-Buildpack.

## 10. Juni 2016: Buildpack 'ASP.NET Core' v0.8.1-20160526-0957 aktualisiert

Diese Version des Buildpacks enthält die folgenden Änderungen:

* Der Name der Laufzeit wird von ASP.NET 5 in ASP.NET Core geändert.
* Die Buildpackversionsnummer ist in der Ausgabe des Erkennungsscripts enthalten.
* Diese Version des Buildpacks entfernt die Unterstützung von DNX-basierten Anwendungen, die CoreCLR RC1 und niedriger verwenden.
* Diese Version des Buildpacks unterstützt .NET CLI und .NET Core RC2.
* Das Buildpack erkennt Projekte mit einer Datei project.json oder Dateien *.runtimeconfig.json in der Veröffentlichungsausgabe (publish).

## 22. Oktober 2015: Buildpack 'ASP.NET 5' v0.7-20151022-1257 aktualisiert

* Diese Version des Buildpacks entfernt Mono und unterstützt dafür die Beta-8-CoreCLR.

## 18. September 2015: Buildpack 'ASP.NET 5' v0.6-20150916-1220 aktualisiert

* Diese Version des Buildpacks unterstützt Beta-7-DNX-Änderungen und kann mithilfe des folgenden angepassten Startbefehls Anwendungen ausführen, die von älteren Betaversionen abhängig sind:

```
   dnx src/dotnetstarter kestrel --server.urls http://${VCAP_APP_HOST}:${PORT}
```
{: codeblock}

* Die Verwendung des Nowin-Web-Servers wurde in diesem Buildpack entfernt. Dafür wird der [Kestrel]{https://github.com/aspnet/KestrelHttpServer}-Web-Server verwendet.

# Zugehörige Links
{: #rellinks}
## Allgemein
{: #general}
* [Dotnet Core-Laufzeit](index.html)
