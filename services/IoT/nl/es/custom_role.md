---

copyright:
  years: 2016, 2017
lastupdated: "2016-11-10"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Acerca de los roles personalizados
{: #custom_roles}

Además de los roles predefinidos que se detallan en la [documentación sobre usuario, aplicación y rol de pasarela](roles_index.html), los usuarios pueden crear roles personalizados que tengan una combinación exclusiva de permisos. Los roles representan el acceso a operaciones específicas, y, mediante la creación de un rol personalizado, puede combinar cualquiera de los permisos que están disponibles para los roles predefinidos.
{:shortdesc}

Para obtener más información sobre las operaciones de API disponibles para los roles de usuario, consulte la [documentación sobre usuario, aplicación y rol de pasarela](roles_index.html).

## Creación de un rol personalizado
{: #custom-role-create}

Para crear un rol personalizado:

1. En el panel de control de {{site.data.keyword.iot_short_notm}}, abra el panel **Miembros** desde la barra de navegación.
2. Seleccione el separador **Roles** y pulse **Nuevo rol**.
3. Escriba un nombre para el rol personalizado.
4. Opcional: escriba una descripción para el rol personalizado.
5. Opcional: los roles personalizados pueden utilizar un rol existente como plantilla. Para basar el rol personalizado en un rol de usuario existente, seleccione el rol en la lista.
6. Pulse **Siguiente**.
7. En la lista de permisos, expanda las categorías de permisos y seleccione las operaciones que debe incluir el rol personalizado.
8. Pulse **Añadir rol**.

El rol personalizado se incluye en la lista de roles disponibles.

## Edición o supresión de un rol personalizado
{: #custom-role-edit}

Para editar o suprimir un rol personalizado:

1. En el panel de control de {{site.data.keyword.iot_short_notm}}, abra el panel **Miembros** desde la barra de navegación.
2. Seleccione el separador **Roles**.
3. Localice la columna correspondiente al rol personalizado que desea editar.
3. Pulse el icono de edición correspondiente al nombre del rol personalizado.
4. Realice los cambios necesarios en la descripción del rol y en los permisos.
5. Para suprimir el rol, desplácese hasta la parte inferior de la lista categorías de permisos y pulse **Suprimir rol**.
5. Si ha realizado cambios, pulse **Guardar** para actualizar el rol.

El rol se actualiza.
