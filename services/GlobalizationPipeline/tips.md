---

copyright:
  years: 2015, 2017
lastupdated: "2016-07-12"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Machine translation tips
{: #globalizationpipeline_tips}

Machine translation can be effective at providing an approximation of the source text's meaning. However, the quality and usefulness of machine translation varies greatly depending on the target language and the machine translation engine that you use. One of the key factors in the quality of machine translation is the quality of the source itself. Source text that is loaded with colloquialisms, incomplete sentences, incorrect punctuation, and ambiguous words and phrases might not be translated accurately.
{:shortdesc}

When you are creating your {{site.data.keyword.Bluemix_notm}} app UI, follow a few basic writing guidelines to improve not only your source language, but also the quality of the machine translation.

In addition, ask native language speakers to review and edit the machine translation. Also, gather feedback from your app users; they are perhaps the best judges of the usefulness and accuracy of the translation.

## Writing style tips
{: #writingstyletips}

* **Use short- to medium-length simple sentences (5 - 20 words):** Machine-translation engines often have difficulty translating compound and complex sentences, including sentences with semicolons. Convey one thought per sentence. If a sentence contains two active verbs to convey two thoughts, break the sentence down into two sentences. Machine-translation engines also have trouble parsing sentences that are too short to provide enough context.
* **Avoid phrases:** Use complete sentences whenever possible. Phrases are acceptable for headings and subheadings, but avoid telegraphic headline-style writing. Use complete sentences to introduce lists.
* **Avoid idioms, slang, and jargon:** Replace phrases for which literal translations make no sense. For example, replace "on the fly" with "dynamic," "on the other hand" with "alternatively," and "keep in mind" with "remember."
* **Avoid humor, sarcasm, colloquialisms, emoticons, and metaphors.**
* **Be succinct:** Remove unnecessary text and redundancies. For example, replace "It is useful to remember that large values increase the response time" with "Large values increase the response time."
* **Avoid sentences that are written completely in the upper-case:** Capitalization provides clues to the meaning of the word. For example, if you write "BILL", the machine-translation engine cannot determine if you meant the name "Bill" or the word "bill."
* **Avoid ambiguous words:** For example, do not use "once" in place of "after" or "when." Do not use "while" in place of "although" or "whereas." Do not use "may" when you mean "might" or "can."
* **Avoid pronouns:** Repeat nouns or noun phrases when possible. The pronoun "it" is particularly problematic.
* **Write in active voice when possible:** Active sentences are usually clearer than passive sentences. For example, write "The utility determines which path is most efficient" instead of "The most efficient path is determined."
* **Avoid culturally specific information.**
* **Be aware that machine translation engines might translate product names:** Many countries retain the original English product name, but machine translation engines might try to translate product names, especially if the names contain real words. Before you use a product name, test the translation of it. If you find problems, modify the text or translation accordingly.
* **Ensure that all information is written in one language:** Machine-translation engines might assume that all information is in a single language, even if the text includes one or two words in another language. For example, if the text includes "en route" (French), the machine translation engine still tries to translate those words as if they are English words.
* **Avoid marketing slogans:** Marketing slogans often rely on the audience's understanding of a particular culture. Avoid these kinds of slogans because machine translation engines are likely to have trouble translating them accurately.
* **Ensure that list items are complete and parallel:** For example, if one item begins with a verb, make sure that all items begin with a verb.
* **Avoid using please and thank you:** These words can seem out of place or even patronizing in some cultures.
* **Write dates in non numeric format:** Numeric date formats vary depending on country. Write out the month name, day, and year. For example use 1 September 2003 instead of 9/01/03, which might be interpreted as either 1 September 2003 or as 9 January 2003.

## Grammar tips
{: #grammartips}

* **Use proper punctuation:** Omitting periods and commas can cause a machine-translation engine to misinterpret the information.
* **Ensure that subjects agree with their verbs:** Ensure that plural subjects have plural verbs and singular subjects have singular verbs.
* **Use simple present tense verbs:** Many other languages do not have English verb qualities, such as voice and tense. Avoid future and past tenses whenever possible. For example, you can rewrite "If you run this program, DB2® will return an error message" as "If you run this program, DB2 returns an error message."
* **Ensure that pronouns agree with their antecedents:** For example, "A user should first determine their tasks" should be rewritten as "Users should first determine their tasks.".
* **Avoid dangling modifiers:** Place modifiers appropriately so that they modify the intended noun. For example, "While typing in commands, the program does not send any messages to you" can be rewritten as "While typing in commands, you do not receive any messages from the program."
* **Avoid double-negatives:** For example, "Do not omit the date" can be replaced with "Include the date."
* **Avoid the infinitive (to write), present participle (writing), and past participle (wrote) forms of verbs at the beginning of sentences:** These verb forms are often ambiguous and difficult to translate.
* **Avoid noun strings:** Limit compound noun phrases, such as "special filter factor estimate considerations," to no more than three words.
* **Avoid using words in multiple grammatical categories:** In English, many words, such as "default," can be a noun or a verb. This structure is not true of many other languages. Be consistent in how you use each word. For example, always use "default" as a noun.
* **Ensure that the elements of a sentence are parallel:** For example, use all nouns or all verbs in an in-sentence list; don't mix nouns and verbs.
* **Do not omit necessary words:** For example, instead of "The file names are displayed in uppercase characters and the file extensions in lowercase," use "The file names are displayed in uppercase characters and the file extensions are displayed in lowercase characters." Use the word "that" to provide clarification as necessary. For example, replace "If you determine the problem is a missing file" with "If you determine that the problem is a missing file."
* **Do not use a dash parenthetically:** For example, do not write "When you get to this point - the point when all data has been loaded - you need to test the system." Replace dashes with commas, or rewrite the sentence.
 
## Terminology tips
{: #terminologytips}

* **Use terminology consistently:** Avoid using multiple terms to refer to the same thing. Avoid using a single term to refer to more than one thing.
* **Include explanations for any specialized terms.**
* **Avoid terms that have different meanings in other environments and contexts:** These terms include "billion," "domestic," and "foreign."
* **Use consistent and standardized capitalization, hyphenation, and word formation:** For example, write "fix pack" instead of "Fix Pack".
* **Use lower-case unless the term is a proper noun.**
* **Avoid special symbols:** If you need to use the # symbol, do not refer to it as the pound sign. Instead, call it the number symbol (#).
* **Avoid abbreviations:** Machine-translation engines might recognize common abbreviations, such as IBM and DB2, but they do not recognize all abbreviations. Avoid abbreviations when possible. Do not use Latin abbreviations, such as "i.e.," and "etc."

## Punctuation tips
{: #punctuationtips}

* **Avoid using a slash to mean "and or":** Rewrite the sentence to indicate the exact meaning. For example, you can rewrite "You can view the draft copy and/or the review copy" as "You can view the draft copy, the review copy, or both."
* **Do not indicate plural by adding (s):** Either use the phrase "one or more" or use the plural form only.
* **Do not use an ampersand (&) to mean and.**
* **Use commas to separate items in an in-sentence list, and put a comma before the conjunction in the list:** For example, "Select your company, location, and profession."

## Spelling tips
{: #spellingtips}

* **Check spelling:** Misspelled words can cause translation errors. Always check for typos!
* **Use consistent spelling:** Ensure that terms, acronyms, and proper names are always spelled the same way, including the use of upper-case and lower-case letters.

## Visual presentation tips
{: #visualtips}

* **Avoid text in graphics.**
* **Avoid using formatting for emphasis.**

