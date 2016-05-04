---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Limites de memória e o buildpack do Liberty
{: #memory_limits}

*Última atualização: 23 de março de 2016*

Um limite de memória deve ser especificado ao implementar um aplicativo com o buildpack do Liberty.

**Evite problemas**

* Um servlet "Hello World" que é implementado com o buildpack do Liberty com um
limite de memória de 256 MB pode não ser implementado e executado corretamente. Se
for implementado, ele será executado próximo do limite de 256 M. Considere especificar um mínimo de 512 M como
Limite de memória até para aplicativos simples.

## Limites de memória e o buildpack do Liberty
{: #memory_limits_and_liberty}


Ao implementar um aplicativo com o
buildpack do Liberty, um "Limite de memória" será solicitado a você.

Para determinar qual Limite de memória especificar,
é importante entender que você não está especificando o tamanho do heap de aplicativo Java. Você
está especificando a quantia de memória que o processo inteiro consegue usar. Esta quantia inclui a memória
que é usada pelos componentes a seguir:

* a memória que é usada pelo contêiner warden.
* a memória que é usada para mapear as extensões kernel e bibliotecas do sistema no processo.
* a memória que é usada para os executáveis jvm, heap de trabalho jvm, espaço jit e referências compactadas.
* a memória que é usada para classes (aplicativo e servidor de aplicativos), pilhas de encadeamento e buffers io diretos.
* A memória que é usada pelo heap de aplicativo Java.

Mais informações sobre o uso de memória JVM podem ser localizadas no artigo do developerWorks [Obrigado pela memória](http://www.ibm.com/developerworks/library/j-nativememory-linux/)

Ao implementar
um aplicativo, o uso de memória do processo inteiro é monitorado. Se o uso de memória exceder o limite de memória
que você especificou quando o aplicativo foi implementado, o kernel irá parar o processo. Esta ação acontece sem aviso e pode ser manifestada nas seguintes formas:

* se o Limite de memória for excedido durante a implementação do aplicativo, você receberá uma mensagem de que ocorreu uma falha. Talvez
veja que o aplicativo está oscilando. Você pode ver que o aplicativo tentou ser iniciado várias vezes, sempre sem êxito. Ou
pode receber uma mensagem indicando que a implementação do aplicativo falhou.
* Se o Limite de memória for excedido enquanto o aplicativo estiver em serviço, o processo será interrompido. O
Cloud Foundry tentará reiniciar o aplicativo. É possível que o aplicativo seja reiniciado, mas ficará indisponível por algum tempo.

# rellinks
## geral
* [Tempo de execução do Liberty](index.html)
* [Visão geral do perfil do Liberty](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
