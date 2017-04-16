{:new_window: target="_blank"}


# Preparación de {{site.data.keyword.blockstorageshort}} 
{: #preparing-block-storage-volume}

Última actualización: 29 de julio de 2016
{: .last-updated}

  Una vez que haya creado su volumen y lo adjunte a un servidor virtual, deberá montar y preparar el volumen que va a utilizar. 
  
  **Nota**: Los mandatos relevantes pueden variar en función de su sistema operativo específico. Para obtener más información, consulte la documentación de su sistema operativo. Los pasos siguientes fueron probados utilizando el servidor virtual de CentOS.
  
  Para preparar un volumen, siga estos pasos:

1. Inicie sesión en el servidor virtual.  

   <pre><code>ssh -i security_key_name.pem ibmcloud@xxx.xx.xx.xx</pre></code>

   **Nota:** Para encontrar el ID de usuario predeterminado, el nombre de la clave de seguridad y su dirección IP pública, vea el separador de visión general del servidor virtual. El ID de usuario predeterminado es *ibmcloud*.Para obtener más información sobre cómo iniciar sesión en el servidor virtual mediante SSH, consulte [Inicio de sesión en una instancia se servidor virtual desde un terminal de Linux](../../virtualmachines/vm_manage_instances.html#vm_login). 

2. Verifique que dicho volumen esté adjunto.   

   <pre><code>sudo su -</pre></code>
   
   **Nota:** Si el mandato *sudo su* no funciona en su sistema operativo, utilice *sudo* antes de cada mandato. Por ejemplo, *sudo fdisk -l*.
   
   <pre><code>fdisk -l</pre></code>

   La información de volumen se lista en el final del texto de información. Por ejemplo, *Disk /dev/vdb: 10.7 GB, 10737418240 bytes*.

3. Partición del disco.

   a. Inicie fdisk y cree una partición nueva. 
    
     <pre><code>fdisk /dev/vdb</pre></code>

   b. Especifique **n** para crear una partición nueva.
   
   c. Especifique **p** para especificar la partición primaria.
   
   d. Para crear una partición, especifique **1**.
   
   e. Salvo que haya requisitos específicos, seleccione los valores predeterminados en las solicitudes restantes y pulse Intro.

   f. Especifique **w** para escribir una partición. 
   
   g. Verifique que el disco nuevo se haya creado.
   
     <pre><code>fdisk -l</pre></code>

     **Nota:** El nombre del disco nuevo habitualmente tiene el nombre de la partición en la que se ha creado, además de un número incremental, como por ejemplo 1. Por ejemplo, *vdb1*.

4. Dé formato al volumen.  

   Deberá dar formato al volumen para almacenar información. En este ejemplo se utiliza ext4; sin embargo, puede utilizar cualquier sistema de archivos que esté soportado. 

   <pre><code>mkfs -t ext4 /dev/vdb1</pre></code>

    **Nota:** El paso para escribir superbloques y la información de contabilidad del sistema de archivos puede tomar tiempo extra para completarlo. Cuando el proceso haya terminado, el estado será *done*.

5. Monte el volumen.  

   a. Debe montar el volumen para utilizarlo.

      <pre><code>mkdir -p /mnt/myvolume</pre></code>
      
      <pre><code>mount /dev/vdb1 /mnt/myvolume</pre></code>

      donde *myvolume* es el nombre de la carpeta que elija. 

   b. Compruebe que su volumen aparece en la lista y está preparado. 

      <pre><code>df -h</pre></code>

6. (Opcional) Monte el volumen permanentemente.  

   Puede montar el volumen permanentemente, de modo que no necesite volver a montarlo después de rearrancar el sistema. 

   a. Ubique el UUID de su volumen

      <pre><code>blkid</pre></code>

   b. Copie el UUID que aparece. 

   c. Edite la información de la tabla de los sistemas de archivos. 

      <pre><code>nano /etc/fstab</pre></code>      

   d. Pegue la línea siguiente, incluyendo su UUID específico, en la parte inferior del archivo y guárdelo.
   
      <pre><code>UUID=xxxxxx /mnt/myvolume ext4 defaults  0 2</pre></code>

   e. Para probar que el volumen se haya montado permanentemente, rearranque el servidor virtual. 

      <pre><code>reboot</pre></code>

  Cuando el servidor virtual esté ejecutándose de nuevo, inicie sesión en el servidor virtual y vaya al directorio de la nueva carpeta que ha creado. Por ejemplo, navegue a **cd /mnt/myvolume**.

  Ahora puede utilizar el volumen. 
