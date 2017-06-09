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

# 將環境對映至報告
{: #uc_insights_mapping}

您在 Delivery Insights 中看到的資訊會依*邏輯環境* 分組，邏輯環境是 IBM UrbanCode Deploy 環境（亦稱為*實體環境*）的集合。您可以用對組織有意義的任何方式，將您的環境分組成邏輯環境。
{:shortdesc}

## 邏輯環境

Delivery Insights 會將您的 IBM UrbanCode Deploy 環境分組成一個以上的邏輯環境。如此，您就可以將環境收集至對您和組織有意義的群組中。例如，如果您有用於多個應用程式的多個正式作業環境，您可以將所有這些環境分組在單一邏輯環境中，並將所有這些環境的度量值結合在單一正式作業環境儀表板中。對映是透過搜尋字串來進行，因此您可以用對 IBM UrbanCode Deploy 伺服器有意義的任何方式來對環境進行分組。

## 預設邏輯環境

依預設，您的報告包括使用字串來比對 IBM UrbanCode Deploy 環境的邏輯環境。例如，名稱中有 "dev" 的所有環境都會對映至 DEV 邏輯環境，而名稱中有 "prod" 的所有環境都會對映至 PROD 邏輯環境。

![預設邏輯環境](images/uc_insights_mapping.gif)

## 將環境對映至邏輯環境

您可以手動將實體環境對映至邏輯環境，或者您可以使用型樣，以動態方式建立實體環境與邏輯環境的關聯。

若要使用型樣將實體環境對映至邏輯環境，請遵循下列步驟：

1. 在 {{site.data.keyword.DRA_short}} 中，按一下 **Delivery Insights > 對映環境**。
1. 按一下現有邏輯環境，或按一下**新增邏輯環境**。
1. 在邏輯環境的設定中，按一下**型樣**下的**新增型樣**。
1. 指定環境名稱的型樣。您可以使用星號 (*) 作為萬用字元。例如，型樣 `env*` 符合環境 `env1`、`env2` 及 `env`。
1. 確認邏輯環境包含您想要的環境。

若要手動將環境對映至邏輯環境，請按一下**手動新增**，然後選取要新增或移除的環境。

![在 DevOps Connect 中設定整合](images/uc_insights_mapping_manually.gif)

現在您已經將環境對映至邏輯環境，您可以看到那些邏輯環境所聚集的報告資訊。
