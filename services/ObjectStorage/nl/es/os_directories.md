---

copyright:
  years: 2014, 2017
lastupdated: "2017-02-10"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Trabajo con directorios

Swift no tiene una auténtica estructura de directorios, sino que utiliza la denominación para representar un diseño de directorios. Si especifica un nombre de directorio, se adjunta a todos los nombres de archivo como parte de la vía de acceso relativa.
{: shortdesc}

## Cómo añadir un directorio a un contenedor con la CLI de Swift

Para añadir un directorio a un contenedor, debe tener la estructura de directorios colocada en el dispositivo local.

1. Localmente, cree un directorio y guarde el archivo.
2. Ejecute el siguiente mandato para cargar un directorio al contenedor.

    ```
    swift upload <nombre_contenedor> <nombre_directorio>
    ```
    {: pre}

## Descarga de un directorio con la CLI
Para descargar una estructura de directorios, utilice el parámetro `-prefix` para indicar el directorio o la estructura de directorios que desea descargar.

1. Ejecute el siguiente mandato para descargar un directorio.

    ```
    swift download <nombre_contenedor> --prefix <directorio>
    ```
    {: pre}
