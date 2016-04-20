---

 

copyright:

  years: 2015, 2016

 

---
{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}


# 開発モード CLI
{: #devmodecli}

*最終更新日: 2016 年 2 月 25 日*

開発モード (dev_mode) は Bluemix のフィーチャーです。これを使用すると、アプリがクラウドで稼働している間もそのアプリを操作することができます。開発モードには、dev_mode コマンド・ライン・インターフェースが組み込まれています。dev_mode CLI は cf CLI プラグインとしてビルドされており、Liberty のアプリと IBM Node.js のアプリを両方サポートしています。

dev_mode CLI は以下のフィーチャーを備えています。
- アプリを開発モードと通常モードの間で切り替える。
- アプリケーション・ファイルの更新には、新規プッシュではなく増分更新を使用する。
- 既存コンテナー内のアプリの開始、停止、または再始動を行う。

## 始めに
**前提条件:** 始める前に Cloud Foundry CLI をインストールしてください。詳しくは、 [『Start coding with Cloud Foundry command line interface』](https://github.com/cloudfoundry/cli)を参照してください。 


dev_mode コマンド・ライン・ツールのインストールには、以下の方法のいずれかを使用します。
- ローカルでインストールする。
  1. [IBM Bluemix CLI Plugin Repository](http://plugins.ng.bluemix.net)から、ご使用のプラットフォームに合った dev_mode プラグインをダウンロードします。
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

## 使用量
**dev_mode CLI に含まれているコマンドをすべて表示するには、以下のコマンドを使用します。**

```
cf plugins
```

### dev_mode のコマンド

### mode

```
cf mode <appName> <dev|normal>
```

アプリのモードを変更します。

### status

```
cf status <appName>
```

アプリのモードとランタイム状況を表示します。

### update-file

```
cf update-file <remotePath> <localPath> [command_options]
```

クラウドのアプリケーション・ファイルを更新します。

コマンド・オプションは以下のとおり。

**expand**

zip ファイルを解凍して、アップロードしたファイルを抜き出す必要があるかどうかを示します。

**restart**

ファイルの更新後にアプリ・ランタイムを再始動します。
  
### delete-file

```
cf delete-file <remotePath> [command_options]
```

クラウドのアプリケーション・ファイルを削除します。

コマンド・オプションは以下のとおり。

**restart**

ファイルの削除後にアプリ・ランタイムを再始動します。

### start-inplace

```
cf start-inplace <appName>
```

既存コンテナーのアプリを開始します。

### stop-inplace

```
cf stop-inplace <appName>
```

既存コンテナーのアプリを停止します。

### restart-inplace

```
cf restart-inplace <appName>
```

既存コンテナーのアプリを再始動します。



### help

```
cf help <commandName>
```
コマンドに関するヘルプを表示します。
