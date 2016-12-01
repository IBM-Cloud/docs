
---

copyright:
years: 2015, 2016

---

{:new_window: target="_blank"}
# Configuración de credenciales para el navegador web Safari
{: #configure-credential-for-safari}
Última actualización: 15 de noviembre de 2016
{: .last-updated}

El servicio IBM {{site.data.keyword.mobilepushshort}} amplía sus funciones para enviar notificaciones al navegador Safari.  

Asegúrese de disponer de una cuenta de desarrollador de Apple. Tiene que registrar un Push ID del sitio web y generar un certificado para configurar Safari para que reciba notificaciones. Comience siguiendo estos pasos. 

1. En el centro Apple Developer Member, pulse **Certificados, ID y Perfiles**. 
2. Pulse **Identificadores** y luego **ID Push del sitio web**.
3. Elija crear una nueva entrada seleccionando el icono del signo más.
![Panel de control de Push](images/safari_1.jpg)

4. En el panel Registrar ID Push del sitio web, especifique una descripción adecuada del ID Push del sitio web y un ID identificador. Se recomienda que esté en formato de nombre de dominio invertido, comenzando por 'web'. Por ejemplo: web.com.example.dailyweatherreports.
5. Registre el ID Push del sitio web. 
6. Seleccione **Editar** para actualizar el ID Push del sitio web. 
7. En la ventana Asistente de certificados para la información sobre certificados, especifique su ID de correo electrónico y un nombre común. Deje en blanco la dirección de correo electrónico de la entidad emisora de certificados. 
8. Pulse **Guardar en disco** y seleccione **Continuar**.
9. Guarde el certificado en una carpeta adecuada. 

 
