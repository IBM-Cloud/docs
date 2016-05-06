---

copyright:
 years: 2015, 2016

---

# Inicializando os apps Push SDK for Android
{: #android_initialize}

Um local comum para colocar o código de inicialização está no método onCreate da atividade principal no aplicativo Android.

Clique no link **Opções móveis** no Painel do Aplicativo Bluemix
para obter a rota do aplicativo e o GUID do aplicativo. Use esses valores para a rota e o
GUID do App. Modifique o fragmento de código para usar os parâmetros appRoute e appGUID
do app Bluemix.


##Inicializar o SDK principal

```
// Inicialize o SDK for Java (Android) com o GUID do app IBM Bluemix e roteie
BMSClient.getInstance().initialize(getApplicationContext(), em que "applicationRoute","applicationGUID", bluemixRegion:"Local e seu app é hospedado");
```


**appRoute**

Especifica a rota que é designada ao aplicativo do servidor que você criou no Bluemix.

**AppGUID**

Especifica a chave exclusiva que é designada ao aplicativo que você criou no Bluemix. Esse valor faz
distinção entre maiúsculas e minúsculas.

**bluemixRegionSuffix**

Especifica o local em que o app está hospedado. Você pode usar um de três valores:

- BMSClient.REGION_US_SOUTH
- BMSClient.REGION_UK
- BMSClient.REGION_SYDNEY

##Inicializar o Push SDK do cliente

```
//Inicialize o Push SDK for Java do cliente
MFPPush push = MFPPush.getInstance();
push.initialize(getApplicationContext());
```
