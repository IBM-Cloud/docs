---

 

copyright:

  years: 2015，2016

 

---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 開発モード CLI
{: #devmodecli}

*最終更新日: 2016 年 4 月 11 日*

Bluemix 開発モード・コマンド・ライン・インターフェース (dev_mode CLI) を使用すると、クラウドでアプリを実行中にそのアプリを更新できます。dev_mode CLI は cf CLI プラグインとしてビルドされており、Liberty のアプリと IBM Node.js のアプリを両方サポートしています。
{: shortdesc}
 

開発モード CLI では以下のタスクを実行できます。
- アプリを開発モードと通常モードの間で切り替える。
- アプリケーション・ファイルの更新には、新規プッシュではなく増分更新を使用する。
- 既存コンテナー内のアプリの開始、停止、または再始動を行う。

## dev_mode プラグインのインストール
**前提条件:** 始める前に Cloud Foundry CLI をインストールしてください。詳しくは、 [『Start coding with Cloud Foundry command line interface』](https://github.com/cloudfoundry/cli)を参照してください。 


dev_mode コマンド・ライン・ツールのインストールには、以下の方法のいずれかを使用します。
- ローカルでインストールする。
  1. [IBM Bluemix CLI Plugin Repository](http://plugins.{DomainName})から、ご使用のプラットフォームに合った dev_mode プラグインをダウンロードします。
  2. cf install-plugin コマンドを使用して dev_mode プラグインをインストールします。
  
        ```
        cf install-plugin dev_mode-linux_amd64
        ```

- Bluemix CLI リポジトリーからインストールする。
  1. 以下のコマンドを使用して、Cloud Foundry CLI リポジトリー群に bluemix-repo リポジトリーを追加します。
  
        ```
        cf add-plugin-repo bluemix-repo http://plugins.ng.bluemix.net
        ```

  2. cf repo-plugins を入力します。bluemix-repo リポジトリーに dev_mode プラグインが表示されます。
		
		```
        cf repo-plugins
        ```
  
  3. 以下のコマンドを使用して、Cloud Foundry CLI プラグイン群に dev_mode プラグインをインストールします。
  
        ```
        cf install-plugin dev_mode -r bluemix-repo
        ```

## dev_mode コマンドの表示
**dev_mode CLI に含まれているコマンドをすべて表示するには、以下のコマンドを使用します。**

```
cf plugins
```

## dev_mode CLI コマンドの索引
{: #dev_mode_cmds_index}

以下の表の索引を使用して、使用頻度の高い dev_mode CLI コマンドを参照してください。

<table summary="dev_mode コマンドの索引">
 <thead>
 <th colspan="4">dev_mode のコマンド</th>
 </thead>
 <tbody> 
 <tr> 
 <td>[help](#help)</td> 
 <td>[mode](#mode)</td> 
 <td>[status](#status)</td>
 <td>[update-file](#update_file)</td>
 </tr> 
 <tr> 
 <td>[delete-file](#delete_file)</td>
 <td>[start-inplace](#start_inplace)</td>
 <td>[stop-inplace](#stop_inplace)</td>
 <td>[restart-inplace](#restart_inplace)</td>
 </tr>
  </tbody> 
 </table> 
*表 1. dev_mode コマンド*



## help
{: #help}

コマンドに関するヘルプを表示します。

```
cf help <commandName>
```


## mode
{: #mode}

アプリのモードを変更します。

```
cf mode <appName> <dev|normal>
```
<strong>コマンド・オプション</strong>:<dl>
   <dt>dev</dt>
   <dd>開発モード。</dd>
   <dt>normal</dt>
   <dd>実動モード。</dd>
   </dl>


## status
{: #status}

アプリのモードとランタイム状況を表示します。```
cf status <appName>
```



## update-file
{: #update_file}

クラウドのアプリケーション・ファイルを更新します。

```
cf update-file <remotePath> <localPath> [command_options]
```


<strong>コマンド・オプション</strong>:<dl>
   <dt>expand</dt>
   <dd>zip ファイルを解凍して、アップロードしたファイルを抜き出す必要があるかどうかを示します。</dd>
   <dt>restart</dt>
   <dd>ファイルの更新後にアプリ・ランタイムを再始動します。</dd>
   </dl>


  
## delete-file
{: #delete_file}

クラウドのアプリケーション・ファイルを削除します。

```
cf delete-file <remotePath> [command_options]
```


<strong>コマンド・オプション</strong>:<dl>
   <dt>restart</dt>
   <dd>ファイルの更新後にアプリ・ランタイムを再始動します。</dd>
  </dl>


## start-inplace
{: #start_inplace}
既存コンテナーのアプリを開始します。

```
cf start-inplace <appName>
```



## stop-inplace
{: #stop_inplace}
既存コンテナーのアプリを停止します。

```
cf stop-inplace <appName>
```



## restart-inplace
{: #restart_inplace}

既存コンテナーのアプリを再始動します。

```
cf restart-inplace <appName>
```



# 関連リンク
{: #rellinks}

## 関連リンク
{: #general}

<!-- Include a link to your full product documentation, pricing sheet, IBM Bluemix prerequisites -->


* [CLI と開発ツール](../../index.html#cli){:new_window}


