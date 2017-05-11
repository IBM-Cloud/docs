---

copyright:
  years: 2015, 2017
lastupdated: "2016-08-30"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# バンドルの操作
{: #globalizationpipeline_workingwithbundles}

作成した各バンドルには、リソース・ファイルから取得されたキー/値ペアと、生成されたすべての翻訳セットが含まれています。
{:shortdesc}

アップロードできるリソース・ファイルの形式は以下のとおりです。ファイルには、アプリの UI 文字列を表すキー/値ペアの形式の内容が含まれていなければなりません。


* ファイル・タイプ: *Java™ プロパティー・ファイル (.properties)*<br>
例:
```js
logout=Logout 
back=Back 
examples=Menu 
home=Home 
web=Web 
enterprise=Enterprise 
extra=Resources 
about=About 
settings=Settings 
help=Help 
support=Support 
topics=Topics 
appExitMsg=Are you sure you want to quit the application?
```
* ファイル・タイプ: *AMD I18N (.js)*<br>
例:
```js
define({
    "root": {
       logout: "Logout",
       back: "Back",
       examples: "Menu",
       home: "Home",
       web: "Web",
       enterprise: "Enterprise",
       extra: "Resources",
       about: "About",
       settings: "Settings",
       help: "Help",
       support: "Support",
       topics: "Topics",
       appExitMsg: "Are you sure you want to quit the application?"
    }
});
``` 
* ファイル・タイプ: *JSON (.json)*<br>
例:
```js
{
  "logout": "Logout",
  "back": "Back",
  "examples": "Menu",
  "home": "Home",
  "web": "Web",
  "enterprise": "Enterprise",
  "extra": "Resources",
  "about": "About",
  "settings": "Settings",
  "help": "Help",
  "support": "Support",
  "topics": "Topics",
  "appExitMsg": "Are you sure you want to quit the application?"
}
``` 

また、リソース・ファイルは以下のガイドラインに従っていなければなりません。
* キーの長さは最大 255 文字。
* 値の長さは最大 8191 文字。
* 1 つのバンドルに含めることができるキー/値ペアは最大 500 ペア。


## バンドルを翻訳する
{: #globalizationpipeline_translatingabundle}

アップロードしたリソース・ファイルのみが翻訳されます。[バンドルを作成する](index.html#globalizationpipeline_creatingbundles)ときや、[バンドルの詳細を変更する](bundles.html#globalizationpipeline_modifyingbundles)ときに、リソース・ファイルをアップロードできます。

リソース・ファイルをアップロードした後、その内容を、デフォルトの機械翻訳エンジンが提供しているどの言語にも翻訳できます。オプションで、[機械翻訳の構成](managing_translations.html#globalizationpipeline_service_to_service)のセクションの説明に従って、別の機械翻訳エンジンを選択することもできます。デフォルトのエンジンでは、以下のターゲット言語がサポートされています。

<table>
<thead>
<tr>
<th>ターゲット言語</th>
</tr>
</thead>
<tbody>
<tr>
<td>中国語 (簡体字)</td>
</tr>
<tr>
<td>中国語 (繁体字)</td>
</tr>
<tr>
<td>フランス語</td>
</tr>
<tr>
<td>ドイツ語</td>
</tr>
<tr>
<td>イタリア語</td>
</tr>
<tr>
<td>日本語</td>
</tr>
<tr>
<td>韓国語</td>
</tr>
<tr>
<td>ポルトガル語 (ブラジル)</td>
</tr>
<tr>
<td>スペイン語</td>
</tr>
</tbody>
</table>

**注:** {{site.data.keyword.GlobalizationPipeline_short}}のデフォルトの機械翻訳エンジンは、ソース言語として英語のサポートのみを提供します。ただし、{{site.data.keyword.GlobalizationPipeline_short}}内の構成で利用可能な別の機械翻訳エンジンは、英語以外の他のソース言語/言語ペアの翻訳をサポートします。

作成したバンドルは、**「バンドル」**タブに追加され、簡単にアクセスできるようになります。そこから、翻訳に対して追加の作業を実行できます。


## 操作するバンドルを選択する
{: #globalizationpipeline_selectingabundle}

1. **「バンドル」**タブをクリックして、作成したバンドルをすべて表示します。
2. リストから**「バンドル ID (Bundle ID)」**をクリックして、そのバンドルの詳細を表示します。
または、「アクション」の列にある**「バンドル詳細の表示 (View the bundles detail)」**アイコン ![バンドルを開いてその翻訳を操作する場合に、この「バンドル詳細の表示」アイコンを選択します](images/viewProjectDetailIcon.png)	をクリックします。

![「バンドル」タブで、使用可能なバンドルをすべて表示します。](images/translationBundles.png)

操作するバンドルを選択した後、その翻訳のステータスを表示したり、言語を追加/削除したり、翻訳を編集したり、リソース・ファイルを更新したりできます。

不要になったバンドルは、**「バンドル」**タブから削除できます。そのバンドルに関連する翻訳もすべて削除されます。

## バンドルの詳細を変更する
{: #globalizationpipeline_modifyingbundles}

バンドルを開くと、そのバンドルについての詳細がすべて表示されます。バンドルに含まれているターゲット言語がすべてリストされ、各言語の現在の翻訳ステータスが示されます。

![バンドルの詳細のページには、バンドルとその翻訳についての情報が表示されます。](images/bundleDetails.png)

バンドルに含まれている各言語のステータスは、進行中、失敗、翻訳済みのいずれかです。

| ステータス | 説明 |
|--------|-------------|
| 進行中 | 機械翻訳はまだ進行中です。 |
| 失敗 | リソース・ファイルをターゲット言語に翻訳中にエラーが発生しました。 |
| 翻訳済み | ターゲット言語への翻訳が完了しています。 |

バンドルで使用されているリソース・ファイルを更新したり、バンドルにターゲット言語を追加したり、バンドルからターゲット言語を削除したり、ターゲット言語用に生成された翻訳をダウンロードしたりできます。

### バンドルで使用されているリソース・ファイルを更新する

1. ソース言語の横の「アクション」列にある**「リソースのアップロード (Upload resources)」**アイコン ![このアイコンは新しいリソース・ファイルをアップロードする場合に選択します](images/uploadIcon.png) をクリックします。
2. **「参照」**をクリックし、アップロードする新しいリソース・ファイルを選択します。
3. アップロードするリソース・ファイルのタイプを選択します。
 * Java プロパティー・ファイル
 * AMD I18N
 * JSON
4. **「更新」**をクリックして、新しいリソース・ファイルをアップロードします。

新しいリソース・ファイルまたは更新されたリソース・ファイルに含まれているキー/値ペアと、既にアップロードされていた値が同期されます。新しいコンテンツまたは変更されたコンテンツのみが翻訳されます。

### バンドルにターゲット言語を追加する

1. **「言語の追加 (Add Language)」**ボタンをクリックします。
2. 使用可能なすべてのターゲット言語が表示されます。バンドルに追加する言語を選択します。

選択した言語の翻訳がすぐに開始されます。

### バンドルからターゲット言語を削除する

バンドルからターゲット言語を削除すると、ターゲット言語および関連するすべての翻訳がプロジェクトから削除されます。削除するターゲット言語の「アクション」列にある**「このターゲット言語を削除 (Remove this target language)」**アイコン ![「このターゲット言語を削除 (Remove this target language)」のごみ箱のアイコンを選択します](images/trashIcon.png) をクリックします。

### ターゲット言語用に生成された翻訳をダウンロードする

{{site.data.keyword.GlobalizationPipeline_short}}には、ターゲット言語用の翻訳をアプリケーションに取り込む手段がいくつか用意されています。翻訳をリソース・ファイルとしてダウンロードし、アプリケーション・ビルドに含めることができます。また、オープン・ソースの [SDK](https://github.com/IBM-Bluemix/gp-common) のいずれかを使用して、{{site.data.keyword.GlobalizationPipeline_short}}から動的に翻訳を参照することもできます。 

<!-- For information on {{site.data.keyword.GlobalizationPipeline_full}} SDKs, see <link>. -->

翻訳をリソース・ファイルとしてダウンロードするには、次のようにします。 

1. ダウンロードするターゲット言語またはソース言語の**「アクション」**列にある**「翻訳のダウンロード (Download the translations)」**アイコン ![ターゲット言語用のソース・キーまたは翻訳をダウンロードする場合に、このダウンロード・アイコンを選択します](images/downloadIcon.png) をクリックします。
2. ファイル・フォーマットを選択します。
3. **「ダウンロード」**をクリックします。
