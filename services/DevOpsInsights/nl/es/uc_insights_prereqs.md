---

copyright:
  years: 2017
lastupdated: "2017-03-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Requisitos previos para Delivery Insights
{: #prereqs}

Para ver información sobre los servidores IBM UrbanCode Deploy en {{site.data.keyword.DRA_short}}, debe alojar una instancia de DevOps Connect en un sistema que se pueda conectar a sus servidores IBM UrbanCode Deploy. Este sistema puede ser un sistema físico o una máquina virtual.
{:shortdesc}

El sistema que aloja DevOps Connect debe tener los siguientes requisitos previos: 
- El sistema debe tener un JRE (Java Runtime Environment) versión 8 o posterior.
- La variable `PATH` del sistema debe incluir la ubicación del JRE. 
- El sistema debe permitir que DevOps Connect cree conexiones salientes a IBM Bluemix.

Para instalar DevOps Connect para utilizarlo con Delivery Insights, abra el servicio DevOps Insights y pulse **Valores > Configuración de Delivery Insights**. 
