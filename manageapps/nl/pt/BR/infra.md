---

 

copyright:

  years: 2016

 

---

{:shortdesc: .shortdesc}

#  Camadas de infraestrutura do Bluemix

*Última atualização: 15 de março de 2016*

O {{site.data.keyword.Bluemix_notm}} abstrai e oculta
camadas do sistema operacional e da infraestrutura, para que você não precise gerenciá-las. No entanto, às vezes
você pode desejar saber mais sobre o sistema operacional e o middleware para seu app.
{:shortdesc}

## Visualizando camadas de infraestrutura do Bluemix
{:viewinfra}

É possível executar o comando cf stacks para mostrar as pilhas disponíveis ou sistemas de arquivos raiz, em que seus apps devem ser implementados. É possível também especificar a pilha ao usar o comando cf push com a opção *-s* e o *stack_name*, em que stack_name é o sistema de arquivos raiz, como `lucid64` ou `cflinuxfs2`:
```
cf push appName -s stack_name
```
É possível usar o comando `cf buildpacks` para mostrar os componentes de middleware, como o perfil WebSphere Liberty e o SDK para Node.js, que estão disponíveis como tempos de execução para seu app ser executado. E você pode especificar o ambiente de tempo de execução para seu app usando o comando a seguir:
```
cf push appName -b buildpackname
```
