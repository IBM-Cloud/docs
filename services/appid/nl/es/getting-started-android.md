---

copyright:
  years: 2017
lastupdated: "2017-03-30"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:pre: .pre}

# Configuración del SDK de Android
{: #android-sdk}

Cree las apps de Android con el SDK del cliente de {{site.data.keyword.appid_short}}, inicialice el SDK, autentique usuarios, y realice solicitudes a recursos protegidos o no protegidos.
{:shortdesc}


## Antes de empezar
{: #before-you-begin}

Necesita la siguiente información:
  * Una instancia del servicio de {{site.data.keyword.appid_short_notm}}.
  * Su ID de arrendatario.
    * En el separador **Credenciales de servicio** del panel de control de servicio, pulse **Ver credenciales**. Su ID de arrendatario se muestra en el campo **tenantID**. Este valor se utiliza para inicializar la app.
  * Su región de {{site.data.keyword.Bluemix}}. Puede encontrar su región consultando en la IU. El valor se utiliza para inicializar la app.
    <table> <caption> Tabla 1. Regiones de {{site.data.keyword.Bluemix_notm}} y sus correspondientes valores de SDK </caption>
    <tr>
      <th> Región Bluemix </th>
      <th> Valor de SDK </th>
    </tr>
    <tr>
      <td> Sur de EE.UU. </td>
      <td> AppID.REGION_US_SOUTH </td>
    </tr>
    <tr>
      <td> Sídney </td>
      <td> AppID.REGION_SYDNEY </td>
    </tr>
    <tr>
      <td> Reino Unido </td>
      <td> AppID.REGION_UK </td>
    </tr>
  </table>

  * Un proyecto de Android Studio, configurado para funcionar con Gradle.
    * Para obtener más información sobre la configuración del entorno de desarrollo de Android, consulte los <a href="https://developers.google.com/web/tools/setup/" target="_blank">documentos de las Herramientas del desarrollador de Google <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>.

## Instalación del SDK del cliente
{: #install-appid-sdk}

1. Cree un proyecto de Android Studio o abra uno ya existente.
2.  Añada el repositorio de JitPack a su archivo `build.gradle` raíz.

  ```gradle
    allprojects {
	    repositories {
		    ...
		    maven { url 'https://jitpack.io' }
	    }
    }
  ```
  {:pre}

3. Abra el archivo `build.gradle` para su aplicación.

    **Nota**: Asegúrese de abrir el archivo para su app, no el archivo `build.gradle` del proyecto.
4. Busque la sección de dependencias del archivo y añada una dependencia de compilación para el SDK del cliente de {{site.data.keyword.appid_short_notm}}:

  ```gradle
   dependencies {
       compile group: 'com.github.ibm-cloud-security:appid-clientsdk-android:1.+'
   }
  ```
  {:pre}

5. Busque la sección defaultConfig y añada las siguientes líneas de código:

  ```gradle
  defaultConfig {
  ...
  manifestPlaceholders = ['appIdRedirectScheme': android.defaultConfig.applicationId]
  }
  ```
  {:pre}

6. Sincronice el proyecto con Gradle. Pulse **Tools** > **Android** > **Sync Project with Gradle Files**.

## Inicialización del SDK del cliente
{: #initialize-client-sdk}

Inicialice el SDK del cliente pasando los parámetros context, tenant ID y region al método initialize. Un lugar habitual, pero no obligatorio, donde poner el código de inicialización es en el método onCreate de la actividad principal de la aplicación de Android.

  ```java
  AppID.getInstance().initialize(getApplicationContext(), <tenantId>, AppID.REGION_UK);
  ```
  {:pre}

1. Sustituya "tenantId" por el tenantId del servicio de {{site.data.keyword.appid_short_notm}}.
2. Sustituya el AppID.REGION_UK por la región de {{site.data.keyword.Bluemix_notm}}.


## Autenticar los usuarios utilizando el widget de inicio de sesión
{: #authenticate-login-widget}

La configuración predeterminada del widget de inicio de sesión requiere el uso de Facebook y de Google para la autenticación. Si sólo configura uno de ellos, el widget de inicio de sesión no se iniciará y se redirigirá al usuario a la pantalla de autenticación de IDP configurada.

Después de inicializar el SDK del cliente de {{site.data.keyword.appid_short_notm}}, puede autenticar los usuarios ejecutando el widget de inicio de sesión.

  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
  loginWidget.launch(this, new AuthorizationListener() {
        @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
          //Se ha producido una excepción
        }

        @Override
        public void onAuthorizationCanceled () {
          //Autenticación cancelada por el usuario
        }

        @Override
        public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
          //Usuario autenticado
        }
      });
  ```
  {:pre}


## Acceso a los atributos de usuario
{: #accessing}

Cuando obtenga una señal de acceso, es posible obtener acceso al punto final de los atributos protegidos del usuario. Puede obtener acceso utilizando los siguientes métodos de la API:

  ```java
  void setAttribute(@NonNull String name, @NonNull String value, UserAttributeResponseListener listener);
  void setAttribute(@NonNull String name, @NonNull String value, @NonNull AccessToken accessToken, UserAttributeResponseListener listener);

  void getAttribute(@NonNull String name, UserAttributeResponseListener listener);
  void getAttribute(@NonNull String name, @NonNull AccessToken accessToken, UserAttributeResponseListener listener);

  void deleteAttribute(@NonNull String name, UserAttributeResponseListener listener);
  void deleteAttribute(@NonNull String name, @NonNull AccessToken accessToken, UserAttributeResponseListener listener);

  void getAllAttributes(@NonNull UserAttributeResponseListener listener);
  void getAllAttributes(@NonNull AccessToken accessToken, @NonNull UserAttributeResponseListener listener);
  ```
  {:pre}

Cuando no se haya aprobado explícitamente una señal de acceso, {{site.data.keyword.appid_short_notm}} utilizará la última señal recibida.

Por ejemplo, puede invocar este código para establecer un atributo nuevo, o para alterar temporalmente uno existente:

  ```java
  appId.getUserAttributeManager().setAttribute(name, value, useThisToken,new UserAttributeResponseListener() {
		@Override
		public void onSuccess(JSONObject attributes) {
			//atributos recibidos en formato JSON con una respuesta satisfactoria
		}

		@Override
		public void onFailure(UserAttributesException e) {
			//Se ha producido una excepción
		}
	});
  ```
  {:pre}

### Inicio de sesión anónimo
{: #anonymous notoc}

Con {{site.data.keyword.appid_short_notm}} puede iniciar sesión de forma anónima, consulte [usuario anónimo](/docs/services/appid/user-profile.html#anonymous).

  ```java
  appId.loginAnonymously(getApplicationContext(), new AuthorizationListener() {
		@Override
		public void onAuthorizationFailure(AuthorizationException exception) {
			//Se ha producido una excepción
		}

		@Override
		public void onAuthorizationCanceled() {
			//Autenticación cancelada por el usuario
		}

		@Override
		public void onAuthorizationSuccess(AccessToken accessToken, IdentityToken identityToken) {
			//Usuario autenticado
		}
	});
  ```
  {:pre}

### Autenticación progresiva
{: #progressive notoc}

Cuando el usuario contiene una señal de acceso anónimo, puede ser identificado pasándola al método `loginWidget.launch`.

  ```java
  void launch (@NonNull final Activity activity, @NonNull final AuthorizationListener authorizationListener, String accessTokenString);
  ```
  {:pre}

Tras un inicio de sesión anónimo, se producirá la autenticación progresiva, aunque se invoque el widget de inicio de sesión sin pasar una señal de acceso porque el servicio ha utilizado la última señal recibida. Si desea borrar las señales almacenadas, ejecute el siguiente mandato:

  ```java
  	appIDAuthorizationManager = new AppIDAuthorizationManager(this.appId);
  appIDAuthorizationManager.clearAuthorizationData();
  ```
  {:pre}


## Pasos siguientes
{: #next-steps}

{{site.data.keyword.appid_short_notm}} proporciona una configuración predeterminada cuando se configuran inicialmente los proveedores de identidad. Puede utilizar la configuración predeterminada sólo en modalidad de desarrollo. Antes de publicar la aplicación, actualice la configuración predeterminada de [Facebook](/docs/services/appid/identity-providers.html#facebook) y [Google](/docs/services/appid/identity-providers.html#google) a sus propias credenciales.
