---

copyright:
  years: 2014, 2017
lastupdated: "2017-01-25"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Instrumentando o MQA com um app Android (descontinuado)
{: #instrumentAnd}


Para usar o {{site.data.keyword.mqafull}} com seu app Android, deve-se fazer download do SDK e instrumentá-lo fazendo algumas mudanças usando o ambiente de desenvolvimento do Android Studio.
{: shortdesc}

Para poder instrumentar um app com o {{site.data.keyword.mqa}}, deve-se ter uma conta do {{site.data.keyword.Bluemix}} e a versão corretamente instalada do ambiente de desenvolvimento para as plataformas do app que você está instrumentando.

Para instrumentar o {{site.data.keyword.mqa}} para funcionar com seu app Android, conclua as tarefas a seguir:

1. Inclua as permissões requeridas e o SDK transferido por download no seu projeto do Android.

	1. Abra seu projeto no Android Studio.
	
	2. Selecione **Arquivo** > **Novo** > **Novo módulo**.
	
	3. No assistente *Criar novo módulo*, em *Mais módulos*, selecione **Importar pacote .JAR ou .AAR** e, em seguida, clique em **Avançar**.
	
	4. No campo Nome do arquivo, insira o nome do arquivo .aar do SDK do {{site.data.keyword.mqa}} que você transferiu por download e clique em **Concluir**.
	
	5. Comece a incluir o {{site.data.keyword.mqa}} em seu app móvel no projeto do Android Studio selecionando **Arquivo** > **Estrutura do projeto**.
	
	6. Selecione o módulo para seu app na janela Estrutura do projeto e selecione a guia *Dependências*.
	
	7. Selecione **+** e, em seguida, selecione **Dependência do módulo**.
	
	8. Na janela Escolher módulos, selecione o módulo do Android do {{site.data.keyword.mqa}} que você importou e, em seguida, clique em **OK**.
	
	9. Selecione **OK** para fechar a janela Estrutura do projeto.
	
	10. Atualize o arquivo manifest do Android, assegurando-se de que as atividades a seguir estejam incluídas em uma entrada `< application>`:
	    
		```
		<activity android:name="com.ibm.mqa.ui.ProblemActivity" />
		<activity android:name="com.ibm.mqa.ui.FeedbackActivity" />
		<activity android:name="com.ibm.mqa.ui.ScreenshotEditorActivity" />
		```
		{: codeblock}
	   
	11. Assegure-se de que as seguintes permissões necessárias estejam listadas no arquivo manifest:
	
		```
		<uses-permission android:name="android.permission.INTERNET" /> 
		<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
		<uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW" />
		```
		{: codeblock}
   
	O código a seguir mostra uma possível amostra de seu arquivo `AndroidManifest.xml`:

		```
		<?xml version="1.0" encoding="utf-8"?>
        <manifest xmlns:android=
		  "http://schemas.android.com/apk/res/android"
        package="com.applause.android"
        android:versionCode="6"
        android:versionName="2.3" >

        <uses-sdk android:minSdkVersion="8" />

        <!-- Required permission -->
        <uses-permission android:name="android.permission.INTERNET" /> 
        <uses-permission android:name=
		  "android.permission.READ_EXTERNAL_STORAGE" />
        <uses-permission android:name=
		  "android.permission.SYSTEM_ALERT_WINDOW" /> 

        <!-- Optional permissions -->
  
        <uses-permission android:name=
		  "android.permission.ACCESS_WIFI_STATE" />
        <uses-permission android:name=
		  "android.permission.ACCESS_NETWORK_STATE" />
        <uses-permission android:name=
		  "android.permission.READ_PHONE_STATE" />
        <uses-permission android:name=
		  "android.permission.ACCESS_COARSE_LOCATION" />
        <uses-permission android:name=
		  "android.permission.ACCESS_FINE_LOCATION" />
        <uses-permission android:name=
		  "android.permission.BLUETOOTH" />
        <!-- ... rest of your application's 
		  permissions, if any -->

        <application
        android:icon="@drawable/ic_launcher"
        android:label="@string/app_name"
        android:theme="@style/AppTheme"
        android:name=".MyApplication' >

        <!-- ... rest of your application's components -->

        <!-- Quality assurance application activities -->
        <activity android:name=
		  "com.ibm.mqa.ui.ProblemActivity" />
        <activity android:name=
		  "com.ibm.mqa.ui.FeedbackActivity" />
        <activity android:name=
		  "com.ibm.mqa.ui.ScreenshotEditorActivity" /> 
        </application>

        </manifest>
		```
	    {: codeblock}

2. Configure uma nova sessão para ser iniciada com cada login.

	1. Inclua o fragmento de código a seguir na classe `MainActivity` de seu app, que está no arquivo `MainActivity.java`. Ele usa sua chave do aplicativo para enviar dados ao {{site.data.keyword.mqa}}.
		 
		```
		public static final String APP_KEY = "Your_Application_Key_Goes_Here";
		```
		{: codeblock}
		
		Substitua *Your_Application_Key_Goes_Here* pela chave do aplicativo na página Configurações do app do {{site.data.keyword.mqa}}.
	
	2. Para usar o construtor de configuração do {{site.data.keyword.mqa}}, primeiro importe os itens a seguir incluindo-os no arquivo `MainActivity.java` de seu app: 
		
		```
		import com.ibm.mqa.MQA;
		import com.ibm.mqa.MQA.Mode;
		import com.ibm.mqa.config.Configuration;
		```
		{: codeblock}
		
	3. Crie um objeto de configuração no evento onCreate de sua classe MainActivity. Esse objeto fornece diversos métodos que é possível usar para especificar itens de configuração. Na conclusão da configuração do objeto, você chama um método build() para finalizar o objeto. Veja a seguir um exemplo de configuração completa:
	
		```
		Configuration configuration = new Configuration.Builder(this)
		.withAPIKey(APP_KEY) //Provides the quality assurance application APP_KEY
		.withMode(Mode.QA) //Selects the quality assurance application mode
		.build();
		```
		{: codeblock}
	
	4. Na classe de aplicativo do seu app, inclua o código para configurar e iniciar as sessões do {{site.data.keyword.mqa}} chamando o método `MQA.startNewSession()` no evento `onCreate` da sua classe de aplicativo.
	
	    Por Exemplo: 
		   
		```
		MQA.startNewSession(this, configuration);
		```
		{: codeblock}

        Exemplo estendido:

		<pre><code>
		// import Android class
        import android.app.Application;

        // Make sure that you import the quality assurance
		  application
        import com.ibm.mqa.MQA;
        import com.ibm.mqa.MQA.Mode;
        import com.ibm.mqa.config.Configuration;

        // Optionally import the quality assurance 
		  application's logging functions
        import com.ibm.mqa.Log;

        public class MyApplication extends Application {
 
	    public static final String APP_KEY = 
		  "Your_Application_Key_Goes_Here";
 
	    @Override
	    public void onCreate() {
		super.onCreate();
		 
		Configuration configuration = new 
		  Configuration.Builder(this)
		.withAPIKey(APP_KEY) //Provides the quality assurance 
		  application APP_KEY
		.withMode(Mode.QA) //Selects the quality assurance 
		  production mode.  This example is for preproduction mode, 
		//Use .withMode(Mode.MARKET) for production mode. 
		.build();
 
		MQA.startNewSession(this, configuration);
	       }
             }
		</code></pre>
		{: codeblock}

3. Continue com as etapas na página [Introdução ao {{site.data.keyword.mqa}}](index.html).


# Links relacionados
{: #rellinks notoc}

## Links relacionados
{: #general notoc}
* [Introdução ao {{site.data.keyword.mqa}}](index.html){:new_window}
