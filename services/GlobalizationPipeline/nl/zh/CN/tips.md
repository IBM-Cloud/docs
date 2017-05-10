---

copyright:
  years: 2015, 2017
lastupdated: "2016-07-12"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# 机器翻译提示
{: #globalizationpipeline_tips}


机器翻译可以有效地提供源文本的大概意思。但是，机器翻译的质量和有效性却因目标语言和所使用的机器翻译引擎而有很大的不同。机器翻译质量好坏的其中一个重要因素是源本身的质量。源文本中如果有俗语、不完整的句子、不正确的标点和模棱两可的字词都可能导致翻译不够准确。
{:shortdesc}

当您创建 {{site.data.keyword.Bluemix_notm}} 应用程序 UI 时，请遵循一些基本的书写准则，不仅改进源语言质量，也改进机器翻译的质量。

此外，要求说母语的人复查和编辑机器翻译。同时，从您的应用程序用户收集反馈；他们也许是翻译有用性和准确性最好的评判者。

## 书写样式提示
{: #writingstyletips}

* **使用简短到中等长度的简单句子（5 - 20 个字）：**机器翻译引擎通常很难翻译复合且复杂的句子，包括含有分号的句子。一个句子表达一种意思。如果句子包含两个主动动词来表达两种意思，请将该句分成两句。机器翻译引擎在解析太短而无法提供足够上下文的句子时也会有问题。
* **避免使用短语：**尽可能使用完整的句子。标题和副标题可以使用短语，但是应避免电报标题样式的书写。请使用完整的句子来引入列表。
* **避免使用习语、俚语和术语：**替换字面翻译没意义的短语。例如，将“on the fly”替换为“dynamic”、“on the other hand”替换为“alternatively”，以及将“keep in mind”替换为“remember”。
* **避免使用诙谐、讽刺、俗语、表情和隐喻。**
* **简明扼要：**移除不必要和冗余的文本。例如，将“It is useful to remember that large values increase the response time”替换为“Large values increase the response time”。
* **避免使用完全以大写字母书写的句子：**大写提供隐含的单词意思。例如，如果您书写“BILL”，那么机器翻译引擎无法确定您的意思是“Bill”这个人名，还是单词“bill”。
* **避免使用能够引起歧义的单词：**例如，不要使用“once”替代“after”或“when”。不要使用“while”替代“although”或“whereas”。当您的意思是“might”或“can”时，不要使用“may”。
* **避免使用代词：**尽可能重复名词或名词短语。代词“it”问题尤其大。
* **尽可能以主动语态书写：**主动句通常比被动句更加清晰明了。例如，书写“The utility determines which path ismost efficient”而不是“The most efficient path is determined”。
* **避免使用文化特定信息。**
* **请注意，机器翻译引擎可能会翻译产品名称：**许多国家或地区会保留原始英文产品名称，但是机器翻译引擎可能会尝试翻译产品名称，尤其是名称包含实际单词的情况下更是如此。在您使用产品名称之前，请先测试其翻译。如果发现问题，请相应地修改文本或翻译。
* **确保所有信息以一种语言书写：**机器翻译引擎可能会假设所有信息以一种语言书写，即使文本包含其他语言的一两个字词也是如此。例如，如果文本包含“en route”（法语），那么机器翻译引擎仍会尝试把它们当做英文单词来翻译。
* **避免营销口号：**营销口号通常依赖于受众对特定文化的了解。因为机器翻译引擎可能无法准确地翻译这些类型的口号，因此应避免使用。
* **确保列表项完整且类似：**例如，如果一个项目以动词开头，那么请确保所有项目都以动词开头。
* **避免使用 please 和 thank you：**这些单词可能会显得不合时宜，甚至在某些文化中会显得自以为是。
* **以非数字格式书写日期：**国家或地区不同，数字日期格式也会不同。写出月份名称、日和年。例如，使用 1 September 2003，而不是 9/01/03，这可能会解释为 2003 年 9 月 1 日或 2003 年 1 月 9 日。

## 语法提示
{: #grammartips}

* **使用适当的标点：**省略句号和逗号可能会导致机器翻译引擎错误地解读信息。
* **确保主语与谓语动词一致：**确保复数主语具有复数谓语动词，而单数主语具有单数谓语动词。
* **使用一般现在时动词：**许多其他语言没有英文的动词性质，如语态和时态。尽可能避免使用将来和过去时态。例如，您可以将“If you run this program, DB2® will return an error message”重写为“If you run this program, DB2 returns an error message”。
* **确保代词与其先行词一致：**例如，“A user should first determine their tasks”应该重写为“Users should first determine their tasks”。
* **避免悬垂修饰语：**适当地放置修饰语，以便它们修饰预期的名词。例如，“While typing in commands, the program does not send any messages to you”可以重写为“While typing in commands, you do not receive any messages from the program”。
* **避免双重否定：**例如，“Do not omit the date”可以替换为“Include the date”。
* **避免在句子开头使用动词的不定式 (to write)、现在分词 (writing) 和过去分词 (wrote)：**这些动词形式通常会引起歧义，很难翻译。
* **避免名词连缀：**将复合名词短语（如“special filter factor estimate considerations”）限制为不超过三个单词。
* **避免在多个语法类别中使用单词：**英文中许多单词（如“default”）既可以做名词，也可以做动词。许多其他语言却并不使用这种结构。请在使用每一个单词的方式上保持一致。例如，始终将“default”用作名称。
* **确保句子的成分是类似的：**例如，使用句子列表中的所有名词或所有动词；不混合名词和动词。
* **不省略必要的单词：**例如，使用“The file names are displayed in uppercase characters and the file extensions are displayed in lowercase characters”，而不是“The file names are displayed in uppercase characters and the file extensions in lowercase”。必要时使用单词“that”以使句子清晰明了。例如，将“If you determine the problem is a missing file”替换为“If you determine that the problem is a missing file”。
* **不要使用破折号作为插入语：**例如，不要写“When you get to this point - the point when all data has been loaded - you need to test the system”。将破折号替换为逗号，或者重写该句子。
 
## 术语提示
{: #terminologytips}

* **使用术语要一致：**避免使用多个术语来指相同的事情。避免使用单一术语来指多个事情。
* **包含任何特殊术语的解释。**
* **避免使用在其他环境和上下文中具有不同意思的术语：**这些术语包括“billion”、“domestic”和“foreign”。
* **使用一致和标准化的大小写、断字和构词：**例如，写“fix pack”而不是“fixpack”。
* **除非术语是专有名称，否则使用小写字母。**
* **避免使用特殊符号：**如果您需要使用 # 符号，请不要指英镑符号，而是指数字符号 (#)。
* **避免使用缩写：**机器翻译引擎可能会识别常见缩写（如 IBM 和 DB2），但是它们无法识别所有缩写。尽可能避免使用缩写。不要使用拉丁文缩写，如“i.e.”和“etc”。

## 标点提示
{: #punctuationtips}

* **避免使用斜杠来表示“and or”：**重写句子以指示确切的意思。例如，您可以将“You can view the draft copy and/or the review copy”重写为“You can view the draft copy, the review copy, or both”。
* **不要通过添加 (s) 来指示复数：**使用短语“one or more”或仅使用复数形式。
* **不要使用“@”符号 (&) 来表示 and。**
* **使用逗号分隔句子列表中的项目，在列表中的连接位置之前放置逗号：**例如，“Select your company, location, and profession”。

## 拼写提示
{: #spellingtips}

* **检查拼写：**拼写错误的单词可能会导致翻译错误。始终检查是否存在拼写错误！
* **使用一致的拼写：**确保术语、首字母缩略词和专有名称始终以相同的方式拼写，包括大小写字母的使用。

## 视觉呈现提示
{: #visualtips}

* **避免在图形中使用文本。**
* **避免使用格式设置来进行强调。**

