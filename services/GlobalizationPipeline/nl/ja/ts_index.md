---

copyright:
  years: 2015, 2017
lastupdated: "2016-08-30"

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# {{site.data.keyword.GlobalizationPipeline_short}}のトラブルシューティング
{: #globalizationpipelinets}

{{site.data.keyword.GlobalizationPipeline_short}}の使用に関する一般的な質問に対する答えをいくつか以下に示します。
{:shortdesc}


## アプリの名前が正しく翻訳されなかった
{: #problem1}

特定の文字列に対して生成された翻訳が、予期されたものではありませんでした。
{:shortdesc}

リソース・ファイルの翻訳時に、製品名などの固有名詞が含まれている文字列は、正しく翻訳されないことがあります。
{: tsSymptoms}

製品名や固有名詞は、他の言語に正しく翻訳されないことがよくあります。実際の物事を表す語が名前に含まれている場合は特にそうです。このようなタイプの語句やフレーズを翻訳すると、特定の言語でのその語句の意味に応じて、英語名とは異なる意味のテキストに翻訳されることがあります。
{: tsCauses}

製品名を使用する前に、製品名の翻訳をテストし、問題がある場合はテキストまたは訳語を修正してください。機械翻訳を使用する場合の文体のヒントを、[機械翻訳のヒント](./tips.html#globalizationpipeline_tips)で確認してください。
{: tsResolve}



## リソース・ファイルをアップロードできない
{: #problem2}

リソース・ファイルをアップロードしようとしましたが、受け入れられませんでした。
{:shortdesc}

リソース・ファイルを新しい翻訳バンドルに追加するときや、翻訳対象の既存のリソース・ファイルを更新するときに、エラーになります。
{: tsSymptoms}

{{site.data.keyword.GlobalizationPipeline_short}}で受け入れられるリソース・ファイルのタイプは、Java™ .properties、JSON、AMD I18N です。
{: tsCauses}

アップロードしようとしているリソース・ファイルが、以下のタイプのいずれかであることを確認してください。
{: tsResolve}
* Java .properties
* JSON
* AMD I18N



## リソース・ファイルが大きすぎてアップロードできない
{: #problem3}

リソース・ファイルをアップロードしようとしましたが、受け入れられませんでした。
{:shortdesc}

翻訳プロジェクトのリソース・ファイルを追加または更新するときに、ファイルのサイズが大きすぎるというエラーになります。
{: tsSymptoms}

{{site.data.keyword.GlobalizationPipeline_short}}では、特定のサイズ要件を満たすリソース・ファイルのみを受け入れます。
{: tsCauses}

リソース・ファイルが以下のガイドラインに従っていることを確認してください。
{: tsResolve}
* キー長さは最大 256 文字。
* 値の長さは最大 2048 文字。
* 1 つの翻訳プロジェクトに含めることができるキー/値ペアは最大 500 ペア。
* リソース・ファイルのサイズは 2 MB 以下。




## 文字列に含まれている変数の前後のスペースに一貫性がない
{: #problem5}

翻訳後の変数の前後に使用されているスペースの有無は、いつも同じではありません。
{:shortdesc}

文字列の中に含まれている変数の前後に使用されているスペースが翻訳後にどうなるかは、言語によって異なります。
{: tsSymptoms}

機械翻訳エンジンは自然言語を処理するように設計されているため、必ずしも、プログラミング言語で使用される特定の構文の処理方法を認識、把握していません。その結果、プレーン・テキストの中に混在している構文の処理に一貫性がない場合があります。
{: tsCauses}

現在のところ、{{site.data.keyword.GlobalizationPipeline_short}}は、"{}" というパターンが変数を表すためによく使用されることを認識しており、その内側に含まれている内容を元の書式のまま保持します。
{: tsResolve}
