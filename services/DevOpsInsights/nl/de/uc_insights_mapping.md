---

copyright:
  years: 2017
lastupdated: "2017-03-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Umgebungen zu Berichten zuordnen
{: #uc_insights_mapping}

Die Informationen, die in Delivery Insights angezeigt werden, sind nach *logischen Umgebungen* gruppiert, bei denen es sich um eine Gruppe von IBM UrbanCode Deploy-Umgebungen (auch als *physische Umgebungen* bezeichnet) handelt. Sie können Ihre Umgebungen in einer Art und Weise in logische Umgebungen gruppieren, die für Ihre Organisation Sinn macht.
{:shortdesc}

## Logische Umgebungen

Delivery Insights gruppiert die IBM UrbanCode Deploy-Umgebungen in eine oder mehrere logische Umgebungen. So können Sie Umgebungen in Gruppen zusammenfassen, die für Ihre Anforderungen und Ihre Organisation geeignet sind. Wenn Sie beispielsweise mehrere Produktionsumgebungen für mehrere Anwendungen haben, können Sie alle diese Umgebungen in einer einzelnen logischen Umgebung gruppieren und Metriken für alle diese Umgebungen in einem einzelnen Produktionsumgebungs-Dashboard kombinieren. Die Zuordnung erfolgt nach Zeichenfolge, sodass Sie Umgebungen in einer Art und Weise gruppieren können, die für die IBM UrbanCode Deploy-Server Sinn macht.

## Logische Standardumgebungen

Standardmäßig umfassen Ihre Berichte logische Umgebungen, die IBM UrbanCode Deploy-Umgebungen anhand von Zeichenfolgen zugeordnet werden können. Beispielsweise werden alle Umgebungen mit "dev" im Namen zur logischen Entwicklungsumgebung (development = Entwicklung) und alle Umgebungen mit "prod" im Namen zur logischen Produktionsumgebung zugeordnet.

![Die logischen Standardumgebungen](images/uc_insights_mapping.gif)

## Umgebungen zu logischen Umgebungen zuordnen

Sie können physische Umgebungen manuell zu logischen Umgebungen zuordnen oder physische Umgebungen mithilfe von Mustern dynamisch mit logischen Umgebungen verknüpfen.

Führen Sie die folgenden Schritte durch, um physische Umgebungen mithilfe eines Musters zu logischen Umgebungen zuzuordnen:

1. Klicken Sie in {{site.data.keyword.DRA_short}} auf **Delivery Insights > Umgebungen zuordnen**.
1. Klicken Sie auf eine vorhandene logische Umgebung oder auf **Logische Umgebung hinzufügen**.
1. Klicken Sie in den Einstellungen für die logische Umgebung unter **Muster** auf **Muster hinzufügen**.
1. Geben Sie ein Muster für Umgebungsnamen an. Sie können dabei den Stern (*) als Platzhalter verwenden. Das Muster `env` entspricht beispielsweise den Umgebungen `env1`, `env2` und `env`.
1. Prüfen Sie, ob die logische Umgebung die von Ihnen gewünschten Umgebungen enthält.

Um Umgebungen manuell zu logischen Umgebungen zuzuordnen, klicken Sie auf **Manuell hinzufügen** und wählen Sie die Umgebungen aus, die hinzugefügt oder entfernt werden sollen.

![Integration in DevOps Connect einrichten](images/uc_insights_mapping_manually.gif)

Da Sie nun Umgebungen zu logischen Umgebungen zugeordnet haben, können Sie jetzt Berichtsinformationen zusammengefasst nach diesen logischen Gruppen anzeigen.
