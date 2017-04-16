{:new_window: target="_blank"}


# Préparation des volumes {{site.data.keyword.blockstorageshort}} 
{: #preparing-block-storage-volume}

Dernière mise à jour : 29 juillet 2016
{: .last-updated}

  Après avoir créé votre volume et l'avoir connecté à un serveur virtuel, vous devez le monter et le préparer à être utilisé. 
  
  **Remarque** : Les commandes appropriées peuvent varier en fonction de votre système d'exploitation. Pour plus d'informations, voir la documentation de votre système d'exploitation. Les étapes suivantes ont été testées à l'aide d'un serveur virtuel CentOS. 
  
  Pour préparer un volume, procédez comme suit :

1. Connectez-vous au serveur virtuel.   

   <pre><code>ssh -i security_key_name.pem ibmcloud@xxx.xx.xx.xx</pre></code>

   **Remarque :** Pour trouver l'ID utilisateur par défaut, le nom de clé de sécurité et votre adresse IP publique, ouvrez l'onglet Présentation du serveur virtuel. L'ID utilisateur par défaut est *ibmcloud*. Pour plus d'informations sur la connexion au serveur virtuel à l'aide de SSH, voir [Connexion à une instance de serveur virtuel à partir d'un terminal Linux](../../virtualmachines/vm_manage_instances.html#vm_login). 

2. Vérifiez que le volume est connecté.   

   <pre><code>sudo su -</pre></code>
   
   **Remarque :** Si la commande *sudo su* ne fonctionne pas sur votre système d'exploitation, utilisez *sudo* avant chaque commande. Par exemple, *sudo fdisk -l*.
   
   <pre><code>fdisk -l</pre></code>

   Les informations de volume se trouvent à la fin du texte informatif. Par exemple, *Disk /dev/vdb: 10.7 GB, 10737418240 bytes*.

3. Partitionnez le disque. 

   a. Lancez fdisk et créez une nouvelle partition.
    
     <pre><code>fdisk /dev/vdb</pre></code>

   b. Entrez **n** pour créer une nouvelle partition.
   
   c. Entrez **p** pour spécifier la partition principale. 
   
   d. Pour créer une partition, entrez **1**.
   
   e. Sauf en cas d'exigences spécifiques, sélectionnez les valeurs par défaut pour les autres invites et appuyez sur Entrée. 

   f. Entrez **w** pour écrire la partition.
   
   g. Vérifiez que le nouveau disque est créé. 
   
     <pre><code>fdisk -l</pre></code>

     **Remarque :** Le nom du nouveau disque correspond généralement au nom de la partition sur laquelle il a été créé, plus un numéro incrémentiel, tel que 1. Par exemple, *vdb1*.

4. Formatez le volume. 

   Vous devez formater le volume de telle sorte qu'il puisse stocker des informations. Cet exemple utilise ext4, mais vous pouvez utiliser n'importe quel système de fichiers pris en charge.

   <pre><code>mkfs -t ext4 /dev/vdb1</pre></code>

    **Remarque :** L'étape d'écriture des superblocks et des informations de comptabilité de système de fichiers peut prendre un peu plus de temps. Lorsque le processus est terminé, l'état *Terminé* s'affiche. 

5. Montez le volume.  

   a. Vous devez monter le volume pour l'utiliser. 

      <pre><code>mkdir -p /mnt/myvolume</pre></code>
      
      <pre><code>mount /dev/vdb1 /mnt/myvolume</pre></code>

      où *myvolume* est un nom de dossier de votre choix. 

   b. Assurez-vous que votre volume est répertorié et qu'il est prêt. 

      <pre><code>df -h</pre></code>

6. (Facultatif) Montez le volume de façon permanente.  

   Vous souhaiterez peut-être monter le volume de façon permanente de manière à ne pas avoir à répéter l'opération de montage après un redémarrage. 

   a. Localisez l'identificateur unique universel pour votre volume.

      <pre><code>blkid</pre></code>

   b. Copiez l'identificateur unique universel indiqué. 

   c. Editez les informations de table de systèmes de fichiers. 

      <pre><code>nano /etc/fstab</pre></code>      

   d. Collez la ligne suivante, y compris votre identificateur unique universel, au bas du fichier, puis enregistrez ce dernier :
   
      <pre><code>UUID=xxxxxx /mnt/myvolume ext4 defaults  0 2</pre></code>

   e. Pour vérifier que le volume a été monté de façon permanente, redémarrez le serveur virtuel. 

      <pre><code>reboot</pre></code>

  Lorsque le serveur virtuel est de nouveau actif, connectez-vous à ce dernier et accédez au nouveau dossier que vous avez créé. Par exemple, exécutez la commande **cd /mnt/myvolume**.

  Vous pouvez à présent utiliser le volume.
