---

copyright:
  years: 2016, 2017
lastupdated: "2017-05-19"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Integración con Jenkins Pipeline

Después de añadir {{site.data.keyword.DRA_full}} a una cadena de herramientas abierta y de definir las políticas que supervisa, puede integrarla con un proyecto Jenkins Pipeline. Los conductos se definen en la interfaz web de Jenkins o en un *Jenkinsfile* que se almacena en su repositorio de control de origen. Puede ver y administrar proyectos Jenkins Pipeline desde la interfaz web de Jenkins. 

El plugin IBM Cloud DevOps para Jenkins integra proyectos Jenkins con cadenas de herramientas. Una *cadena de herramientas* es un conjunto de integraciones de herramientas que dan soporte a tareas de desarrollo, despliegue, y operaciones. El poder colectivo de una cadena de herramientas es mayor que la suma de sus integraciones de herramientas individuales. Las cadenas de herramientas abiertas son parte del servicio {{site.data.keyword.contdelivery_full}}. Para obtener más información sobre el servicio {{site.data.keyword.contdelivery_short}}, consulte [su documentación](https://console.ng.bluemix.net/docs/services/ContinuousDelivery/cd_about.html). 

Después de instalar el plugin IBM Cloud DevOps, puede configurar su proyecto Jenkins para publicar resultados de pruebas en {{site.data.keyword.DRA_short}}, evaluar la calidad de la compilación automáticamente en las puertas y realizar un seguimiento del riesgo de su despliegue. También puede enviar notificaciones de trabajos a otras herramientas en su cadena de herramientas como, por ejemplo, Slack y PagerDuty. Para ayudarle en el seguimiento de despliegues, la cadena de herramientas puede añadir mensajes de despliegue a confirmaciones Git y los correspondientes problemas Git o JIRA relacionados. También puede ver los despliegues en la página Conexiones de la cadena de herramientas. 

El plugin proporciona una interfaz de línea de mandatos y las acciones posteriores a la compilación para dar soporte a la integración. {{site.data.keyword.DRA_short}} agrega y analiza los resultados de pruebas de unidad, pruebas funcionales, herramientas de cobertura de código, exploraciones de código de seguridad estático y exploraciones de código de seguridad dinámico para determinar si el código cumple las políticas predefinidas en las puertas especificadas del proceso de despliegue. Si el código no cumple o supera una política, el despliegue se detiene para impedir que se liberen cambios arriesgados. Puede utilizar {{site.data.keyword.DRA_short}} como red de seguridad para su entorno de entrega continua, como método para implementar y mejorar con el tiempo los estándares de calidad y como una herramienta de visualización de datos para ayudarle a comprender el estado de salud de su proyecto.

Si está familiarizado con Jenkins Pipeline, siga leyendo. De lo contrario, [consulte la documentación de Jenkins Pipeline](https://jenkins.io/doc/book/pipeline/) antes de continuar. 

## Requisitos previos
{: #jenkins_prerequisites}

Debe tener acceso a un servidor que ejecute un proyecto Jenkins Pipeline. 

## Creación de una cadena de herramientas
{: #jenkins_create}

Antes de poder integrar {{site.data.keyword.DRA_short}} con un proyecto Jenkins, debe crear una cadena de herramientas. 

1. Para crear una cadena de herramientas, vaya a la página [Crear una cadena de herramientas](https://console.ng.bluemix.net/devops/create) y siga las instrucciones en dicha página. 

2. Después de crear la cadena de herramientas, añada {{site.data.keyword.DRA_short}} a la misma. Consulte la [documentación de {{site.data.keyword.DRA_short}}](https://console.ng.bluemix.net/docs/services/DevOpsInsights/index.html) para obtener más información. 

## Instalación del plugin
{: #jenkins_install}

Instale el plugin en el servidor Jenkins abriendo la interfaz del servidor y siguiendo estos pasos:

1. Pulse **Gestionar Jenkins**.
2. Pulse **Gestionar plugins**. 
3. Pulse el separador **Disponible**.
4. Filtre por `IBM Cloud DevOps`. 
5. Seleccione **IBM Cloud DevOps**.
6. Pulse **Descargar ahora e instalar al reiniciar**. 

El plugin está disponible tras reiniciar el servidor.  

## Creación de un conducto
{: #jenkinsfile_create}

Los conductos se definen en el menú de configuración de los proyectos Jenkins o en un Jenkinsfile en su repositorio. Para continuar, cree o abra un script o un Jenkinsfile para utilizar con {{site.data.keyword.DRA_short}}. Puede seguir los formatos [declarativos](https://jenkins.io/doc/book/pipeline/syntax/#declarative-pipeline) o [de scripts](https://jenkins.io/doc/book/pipeline/syntax/#scripted-pipeline).

## Exposición de variables de entorno necesarias

Abra la definición del conducto.  

En la definición, añada las siguientes variables de entorno. Estas variables son necesarios para la integración del conducto con {{site.data.keyword.DRA_short}}.

| Variable de entorno        | Definición    |
| ----------------------------|---------------|
| `IBM_CLOUD_DEVOPS_CREDS`    | Credenciales de Bluemix que se definen en Jenkins con el mandato `credentials`. Por ejemplo, `IBM_CLOUD_DEVOPS_CREDS = credentials('BM_CRED')`. Al establecer la variable con este mandato, establece dos variables de entorno más de forma automática: `IBM_CLOUD_DEVOPS_CREDS_USR` e `IBM_CLOUD_DEVOPS_CREDS_PSW` para el nombre de usuario y la contraseña.  |
| `IBM_CLOUD_DEVOPS_ORG`      | Organización de Bluemix a la que pertenece su cadena de herramientas.     |
| `IBM_CLOUD_DEVOPS_APP_NAME` | Nombre de la aplicación que despliega su cadena de herramientas.   |
| `IBM_CLOUD_DEVOPS_TOOCLHAIN_ID` | Identificador de su cadena de herramientas. Abra la Visión general de la cadena de herramientas y consulte el URL para determinar el ID. El formato del URL de la cadena de herramientas es `https://console.ng.bluemix.net/devops/toolchains/[SU_ID_CADENA_HERRAMIENTAS]`.   |
| `IBM_CLOUD_DEVOPS_WEBHOOKURL` | Webhook que proporcionó al añadir Jenkins a su cadena de herramientas.   |

Para obtener más información sobre el mandato `credentials`, consulte la [documentación de Jenkins Pipeline](https://jenkins.io/doc/pipeline/tour/environment/#credentials-in-the-environment).
{: tip}

Si está utilizando el formato de conducto de script, establezca sus credenciales con `withCredentials` y su entorno con `withEnv` en lugar de hacerlo con `credentials` y `environment` que se utilizan en el siguiente ejemplo. Para obtener más información sobre `withCredentials`, consulte la [documentación de Jenkins](https://jenkins.io/doc/pipeline/steps/credentials-binding/).
{: tip} 

Estas credenciales y variables de entorno las utiliza el plugin IBM Cloud DevOps para interactuar con DevOps Insights. En este ejemplo, se establecen en el formato de conducto declarativo. 

```
environment {
        IBM_CLOUD_DEVOPS_CREDS = credentials('BM_CRED')
        IBM_CLOUD_DEVOPS_ORG = 'dlatest'
        IBM_CLOUD_DEVOPS_APP_NAME = 'Weather-App'
        IBM_CLOUD_DEVOPS_TOOLCHAIN_ID = '1111111-aaaa-2222-bbbb-333333333'
        IBM_CLOUD_DEVOPS_WEBHOOK_URL = 'https://jenkins:5a55555a-a555-5555-5555-a555aa55a555:55555555-5555-5555-5555-555555555555@devops-api.ng.bluemix.net/v1/toolint/messaging/webhook/publish'
    }
```


## Adición de pasos de Cloud DevOps
El plugin Cloud DevOps añade cuatro pasos a los conductos Jenkins. Utilice estos pasos en sus conductos para interactuar con DevOps Insights. 

* `publishBuildRecord`, que publica información de compilación para DevOps Insights
* `publishTestResult`, que publica los resultados de las pruebas para DevOps Insights
* `publishDeployRecord`, que publica registros de despliegue para DevOps Insights
* `evaluateGate`, que impone las políticas de DevOps Insights 

Añada estos pasos a su definición de conducto siempre que necesite ejecutarlo. Por ejemplo, podría cargar los resultados de una prueba después de ejecutarla y, a continuación, evaluar dichos resultados en una puerta después de haberlos cargado. 

### Publicación de registros de compilación

Publique los registros de compilación con el paso `publishBuildRecord`. Este paso requiere cuatro parámetros.

| Parámetro        | Definición    |
| ----------------------------|---------------|
| `gitBranch`    | Nombre de la rama Git que utiliza la compilación.  |
| `gitCommit`      | ID de confirmación que utiliza la compilación.    |
| `gitRepo` | URL del repositorio Git.   |
| `result` | Resultado de la etapa de compilación. El valor es `SUCCESS` o `FAIL`.   |

Este ejemplo muestra estos parámetros en un mandato:

```
publishBuildRecord gitBranch: "${GIT_MASTER}", gitCommit: "${GIT_COMMIT}", gitRepo: "https://github.com/username/reponame", result:"SUCCESS"
```

Jenkins Pipeline no expone la información de Git como variables de entorno. Utilice el mandato `sh(returnStdout: true, script: 'git rev-parse HEAD').trim()` para obtener el ID de confirmación Git.
{: tip}

### Publicación de resultados de prueba
Publique los resultados de la prueba con el paso `publishTestResult`. Este paso requiere dos parámetros.

| Parámetro        | Definición    |
| ----------------------------|---------------|
| `type`    | Tipo de resultado de prueba. El valor debe ser `unittest` para pruebas de unidad, `fvt` para pruebas de verificación funcional o `code` para pruebas de cobertura de código.  |
| `fileLocation`      | Ubicación del archivo de resultados de la prueba.    |

El siguiente ejemplo muestra estos parámetros en mandatos. El primer mandato publica los resultados de la prueba de unidad Mocha. El segundo mandato publica los resultados de la prueba de cobertura de código. 

```
publishTestResult type:'unittest', fileLocation: './mochatest.json'
publishTestResult type:'code', fileLocation: './tests/coverage/reports/coverage-summary.json'
```

### Publicación de registros de despliegue

Publique los registros de despliegue con el paso `publishDeployRecord`. Este paso requiere dos parámetros. También puede aceptar un parámetro opcional. 

| Parámetro        | Definición    |
| ----------------------------|---------------|
| `environment`    | Entorno en el que se desplegó la app. Para que DevOps Insights funcione correctamente, debe identificar un entorno como `STAGING` y otro entorno como `PRODUCTION`. |
| `result`      | Resultado de la etapa de compilación. El valor debe ser `SUCCESS` o `FAIL`.    |
| `appUrl`      | *Opcional*: URL que se utiliza para acceder a su aplicación.    |

El siguiente ejemplo muestra estos parámetros en mandatos. El primer mandato publica los registros de despliegue para un entorno de transferencia. El segundo mandato publica el registro de despliegue para un entorno de producción.

```
publishDeployRecord environment: "STAGING", appUrl: "http://staging-Weather-App.mybluemix.net", result:"SUCCESS"
publishDeployRecord environment: "PRODUCTION", appUrl: "http://Weather-App.mybluemix.net", result:"SUCCESS"
```

### Adición de puertas

Utilice el mandato `evaluateGate` para añadir puertas a su conducto. Las puertas imponen las políticas de DevOps Insights, que establecen requisitos para las pruebas para la promoción de la compilación. 

Este paso requiere un parámetro. También puede aceptar un parámetro opcional. 

| Parámetro        | Definición    |
| ----------------------------|---------------|
| `policy`    | Nombre de la política que la puerta implementa. El nombre de la política se define en DevOps Insights. |
| `forceDecision`      | *Opcional*: Indica si debe detenerse el conducto según la decisión que tome la puerta. Establezca este parámetro en `true` para detener la ejecución del conducto si la puerta falla. Establézcalo en `false` para permitir que el conducto continúe después de que se produzca una anomalía en la puerta. De forma predeterminada, el valor es `false`.     |

El siguiente ejemplo muestra estos parámetros en un mandato. En este mandato, el conducto continúa ejecutándose independientemente de la decisión de la puerta.  

```
evaluateGate policy: 'Weather App Policy', forceDecision: 'true'
```

### Comunicación con cadenas de herramientas

Envíe el estado del conducto a las cadenas de herramientas de Bluemix utilizando el mandato `notifyOTC`. Para obtener más información sobre la integración de Jenkins con cadenas de herramientas, [consulte la documentación](https://console.ng.bluemix.net/docs/services/ContinuousDelivery/toolchains_integrations.html#jenkins). Puede omitir los pasos 6d a 6f, puesto que sólo se aplican a proyectos Jenkins de formato libre.

Este paso requiere dos parámetros y también puede utilizarse otro opcional. 

| Parámetro        | Definición    |
| ----------------------------|---------------|
| `stageName`    | Nombre de la etapa de conducto actual. |
| `status`    | Estado de la etapa de conducto actual. Con `SUCCESS`, `FAILURE` o `ABORTED` activará de forma automática el resaltado de color en Slack.  |
| `webhookUrl`      | *Opcional*: URL de webhook que se muestra en su mosaico Jenkins de la cadena de herramientas. Si incluye este parámetro, su valor prevalece sobre la variable de entorno `IBM_CLOUD_DEVOPS_WEBHOOKURL`.   |

Los siguientes ejemplos muestran cómo utilizar el paso `notifyOTC` tanto en definiciones de conductos de scripts como en definiciones de conductos declarativos.

#### Conducto declarativo
```
stage('Deploy') {
    steps {
      ...
    }

    post {
        success {
            notifyOTC stageName: "Deploy", status: "SUCCESS"
        }
        failure {
            notifyOTC stageName: "Deploy", status: "FAILURE", webhookUrl: "https://different-webhook-url@devops-api.ng.bluemix.net/v1/toolint/messaging/webhook/publish"
        }
    }
}
```

#### Conducto de script
```
stage('Deploy') {
  try {
      ... (deploy steps)

      notifyOTC stageName: "Deploy", status: "SUCCESS"
  }
  catch (Exception e) {
      notifyOTC stageName: "Deploy", status: "FAILURE", webhookUrl: "https://different-webhook-url@devops-api.ng.bluemix.net/v1/toolint/messaging/webhook/publish"
  }
}
```

En ambos ejemplos, el URL de webhook de la cadena de herramientas únicamente se modifica en caso de una anomalía. 

## Cómo asegurar la trazabilidad a lo largo de las integraciones de la cadena

Configure su entorno de Jenkins para integrar con su cadena de herramientas de Bluemix siguiendo las instrucciones en [la documentación de Bluemix](https://console.ng.bluemix.net/docs/services/ContinuousDelivery/toolchains_integrations.html#jenkins). Puede omitir los pasos 6d a 6f, puesto que sólo se aplican a proyectos Jenkins de formato libre.

La integración con una cadena de herramientas le ofrece trazabilidad de principio a fin y correlación de despliegues. Después de seguir las instrucciones de integración, añada el mandato `cf icd --create-connection $IBM_CLOUD_DEVOPS_WEBHOOK_URL $CF_APP_NAME` después de los pasos de despliegue. Este mandato conecta a su integración de Jenkins para una app que se está ejecutando en Bluemix. 

Este ejemplo muestra un paso de despliegue en su totalidad. El último mandato es `cf icd --create-connection`. 

<pre>
sh '''
    echo "CF Login..."
    cf api https://api.ng.bluemix.net
    cf login -u $IBM_CLOUD_DEVOPS_CREDS_USR -p $IBM_CLOUD_DEVOPS_CREDS_PSW -o $IBM_CLOUD_DEVOPS_ORG -s staging
    echo "Deploying...."
    export CF_APP_NAME="staging-$IBM_CLOUD_DEVOPS_APP_NAME"
    cf delete $CF_APP_NAME -f
    cf push $CF_APP_NAME -n $CF_APP_NAME -m 64M -i 1
    <b>cf icd --create-connection $IBM_CLOUD_DEVOPS_WEBHOOK_URL $CF_APP_NAME</b>
'''
</pre>

Tal como se describe en la documentación de integración de Jenkins, los plugins CloudFoundry CLI y CloudFoundry ICD deben estar instalados en su servidor Jenkins. También puede necesitar iniciar una sesión en Bluemix desde el servidor para conectarse.

## Ejemplo de un conducto declarativo

Este ejemplo muestra un conducto completo que está definido como un Jenkinsfile declarativo. 

```
#!groovy
/*
    Ejemplo de un archivo Jenkins de ejemplo para Weather App, una aplicación node.js con una prueba de unidad, pruebas
    de cobertura de código y de verificación funcional, despliegue a un entorno de transferencia y producción y
    utilización de una puerta IBM Cloud DevOps.
    Se utiliza como un ejemplo para utilizar nuestro plugin en Jenkinsfile.
    Básicamente necesitará especificar 4 variables de entorno y después podrá utilizar los 4 métodos diferentes
    para la etapa de compilación/prueba/despliegue y la puerta.
 */
pipeline {
    agent any
    environment {
        // Primero necesita especificar 4 variables de entorno necesarias, que
        // se van a utilizar para los siguientes pasos de IBM Cloud DevOps
        IBM_CLOUD_DEVOPS_CREDS = credentials('BM_CRED')
        IBM_CLOUD_DEVOPS_ORG = 'dlatest'
        IBM_CLOUD_DEVOPS_APP_NAME = 'Weather-V1'
        IBM_CLOUD_DEVOPS_TOOLCHAIN_ID = '1320cec1-daaa-4b63-bf06-7001364865d2'
        IBM_CLOUD_DEVOPS_WEBHOOK_URL = 'WEBHOOK_URL_PLACEHOLDER'
    }
    tools {
        nodejs 'recent'
    }
    stages {
        stage('Build') {
            environment {
                // obtener la confirmación git desde Jenkins
                GIT_COMMIT = sh(returnStdout: true, script: 'git rev-parse HEAD').trim()
                GIT_BRANCH = 'master'
                GIT_REPO = 'GIT_REPO_URL_PLACEHOLDER'
            }
            steps {
                checkout scm
                sh 'npm --version'
                sh 'npm install'
                sh 'grunt dev-setup --no-color'
            }
            // sección posterior a la compilación para utilizar el método
            // "publishBuildRecord" para publicar el registro de compilación
            post {
                success {
                    publishBuildRecord gitBranch: "${GIT_BRANCH}", gitCommit: "${GIT_COMMIT}", gitRepo: "${GIT_REPO}", result:"SUCCESS"
                }
                failure {
                    publishBuildRecord gitBranch: "${GIT_BRANCH}", gitCommit: "${GIT_COMMIT}", gitRepo: "${GIT_REPO}", result:"FAIL"
                }
            }
        }
        stage('Unit Test and Code Coverage') {
            steps {
                sh 'grunt dev-test-cov --no-color -f'
            }
            // sección posterior a la compilación para utilizar el método
            // "publishTestResult" para publicar los resultados de la prueba
            post {
                always {
                    publishTestResult type:'unittest', fileLocation: './mochatest.json'
                    publishTestResult type:'code', fileLocation: './tests/coverage/reports/coverage-summary.json'
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                // Hacer push a Weather App para Bluemix, almacenamiento intermedio
                sh '''
                        echo "CF Login..."
                        cf api https://api.ng.bluemix.net
                        cf login -u $IBM_CLOUD_DEVOPS_CREDS_USR -p $IBM_CLOUD_DEVOPS_CREDS_PSW -o $IBM_CLOUD_DEVOPS_ORG -s staging

                        echo "Deploying...."
                        export CF_APP_NAME="staging-$IBM_CLOUD_DEVOPS_APP_NAME"
                        cf delete $CF_APP_NAME -f
                        cf push $CF_APP_NAME -n $CF_APP_NAME -m 64M -i 1

                        # utilizar "cf icd --create-connection" para habilitar la trazabilidad
                        cf icd --create-connection $IBM_CLOUD_DEVOPS_WEBHOOK_URL $CF_APP_NAME

                        export APP_URL=http://$(cf app $CF_APP_NAME | grep urls: | awk '{print $2}')
                    '''
            }
            // sección posterior a la compilación para utilizar el método
            // "publishDeployRecord" para publicar el registro de despliegue
            // y notificar a OTC del estado de la etapa
            post {
                success {
                    publishDeployRecord environment: "STAGING", appUrl: "http://staging-${IBM_CLOUD_DEVOPS_APP_NAME}.mybluemix.net", result:"SUCCESS"
                    // utilizar el método "notifyOTC" para notificar a otc del estado de la etapa
                    notifyOTC stageName: "Deploy to Staging", status: "SUCCESS"
                }
                failure {
                    publishDeployRecord environment: "STAGING", appUrl: "http://staging-${IBM_CLOUD_DEVOPS_APP_NAME}.mybluemix.net", result:"FAIL"
                    // utilizar el método "notifyOTC" para notificar a otc del estado de una etapa
                    notifyOTC stageName: "Deploy to Staging", status: "FAILURE"
                }
            }
        }
        stage('FVT') {
            // establecer el APP_URL como la variable de entorno para fvt
            environment {
                APP_URL = "http://staging-${IBM_CLOUD_DEVOPS_APP_NAME}.mybluemix.net"
            }
            steps {
                sh 'grunt fvt-test --no-color -f'
            }
            // sección posterior a la compilación para utilizar el método
            // "publishTestResult" para publicar los resultados de la prueba
            post {
                always {
                    publishTestResult type:'fvt', fileLocation: './mochafvt.json', environment: 'STAGING'
                }
            }
        }
        stage('Gate') {
            steps {
                // utilizar "evaluateGate" para soportar la puerta IBM Cloud DevOps
                evaluateGate policy: 'Weather App Policy', forceDecision: 'true'
            }
        }
        stage('Deploy to Prod') {
            steps {
                // Hacer push a Weather App para Bluemix, almacenamiento de producción
                sh '''
                        echo "CF Login..."
                        cf api https://api.ng.bluemix.net
                        cf login -u $IBM_CLOUD_DEVOPS_CREDS_USR -p $IBM_CLOUD_DEVOPS_CREDS_PSW -o $IBM_CLOUD_DEVOPS_ORG -s production

                        echo "Deploying...."
                        export CF_APP_NAME="prod-$IBM_CLOUD_DEVOPS_APP_NAME"
                        cf delete $CF_APP_NAME -f
                        cf push $CF_APP_NAME -n $CF_APP_NAME -m 64M -i 1

                        # utilizar "cf icd --create-connection" para habilitar la trazabilidad
                        cf icd --create-connection $IBM_CLOUD_DEVOPS_WEBHOOK_URL $CF_APP_NAME
                        
                        export APP_URL=http://$(cf app $CF_APP_NAME | grep urls: | awk '{print $2}')
                    '''
            }
            // sección posterior a la compilación para utilizar el método
            // "publishDeployRecord" para publicar el registro de despliegue
            // y notificar a OTC del estado de la etapa
            post {
                success {
                    publishDeployRecord environment: "PRODUCTION", appUrl: "http://prod-${IBM_CLOUD_DEVOPS_APP_NAME}.mybluemix.net", result:"SUCCESS"
                    // utilizar el método "notifyOTC" para notificar a otc del estado de la etapa
                    notifyOTC stageName: "Deploy to Prod", status: "SUCCESS"
                }
                failure {
                    publishDeployRecord environment: "PRODUCTION", appUrl: "http://prod-${IBM_CLOUD_DEVOPS_APP_NAME}.mybluemix.net", result:"FAIL"
                    // utilizar el método "notifyOTC" para notificar a otc del estado de la etapa
                    notifyOTC stageName: "Deploy to Prod", status: "FAILURE"
                }
            }
        }
    }
}
``` 










