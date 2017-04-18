{:new_window: target="_blank"}


# {{site.data.keyword.blockstorageshort}}-Datenträger vorbereiten 
{: #preparing-block-storage-volume}

Letzte Aktualisierung: 29. Juli 2016
{: .last-updated}

  Nachdem ein Datenträger erstellt und an einen virtuellen Server angehängt wurde, muss der Datenträger zur Verwendung vorbereitet werden. 
  
  **Hinweis:** Abhängig von Ihrem jeweiligen Betriebssystem können die relevanten Befehle variieren. Weitere Informationen finden Sie in der Dokumentation zu Ihrem Betriebssystem. Die folgenden Schritte wurden unter Verwendung eines virtuellen CentOS-Servers getestet. 
  
  Führen Sie zum Vorbereiten eines Datenträgers die folgenden Schritte aus: 

1. Melden Sie sich beim virtuellen Server an.   

   <pre><code>ssh -i sicherheitsschlüsselname.pem ibmcloud@xxx.xx.xx.xx</pre></code>

   **Hinweis:** Informationen zur Standard-Benutzer-ID, zum Namen des Sicherheitsschlüssels sowie zu Ihrer öffentlichen IP-Adresse finden Sie auf der Übersichtsregisterkarte des virtuellen Servers. Die  Standard-Benutzer-ID ist *ibmcloud*. Informationen zur Anmeldung beim virtuellen Server mithilfe von SSH finden Sie unter [Über ein Linux-Terminal bei einer Instanz eines virtuellen Servers anmelden](../../virtualmachines/vm_manage_instances.html#vm_login).  

2. Vergewissern Sie sich, dass der Datenträger angehängt ist.   

   <pre><code>sudo su -</pre></code>
   
   **Hinweis:** Falls der Befehl *sudo su* für Ihr Betriebssystem nicht funktioniert, verwenden Sie *sudo* vor jedem Befehl. Beispiel: *sudo fdisk -l*. 
   
   <pre><code>fdisk -l</pre></code>

   Die Datenträgerinformationen sind im unteren Teil des Informationstexts enthalten. Beispiel: *Disk /dev/vdb: 10.7 GB, 10737418240 bytes*. 

3. Partitionieren Sie die Festplatte. 

   a. Starten Sie 'fdisk' und erstellen Sie eine neue Partition. 
    
     <pre><code>fdisk /dev/vdb</pre></code>

   b. Geben Sie **n** ein, um eine neue Partition zu erstellen. 
   
   c. Geben Sie **p** ein, um die primäre Partition anzugeben. 
   
   d. Geben Sie zum Erstellen den Wert **1** ein. 
   
   e. Sofern Sie keine besonderen Anforderungen haben, wählen Sie bei den übrigen Aufforderungen Standardwerte aus und drücken die Eingabetaste. 

   f. Geben Sie **w** ein, um die Partition zu schreiben. 
   
   g. Überprüfen Sie, ob die neue Platte erstellt wurde. 
   
     <pre><code>fdisk -l</pre></code>

     **Hinweis:** Der neue Plattenname besteht in der Regel aus dem Name der Partition, auf der die Platte erstellt wurde, und einer inkrementell steigenden Nummer, wie zum Beispiel 1. Beispiel: *vdb1*. 

4. Formatieren Sie den Datenträger.  

   Sie müssen den Datenträger formatieren, um auf ihm Informationen speichern zu können. In diesem Beispiel wird 'ext4' verwendet. Sie können jedoch jedes beliebige unterstützte Dateisystem verwenden. 

   <pre><code>mkfs -t ext4 /dev/vdb1</pre></code>

    **Hinweis:** Die Ausführung des Schritts zum Schreiben von Superblöcken und Abrechnungsdaten für das Dateisystem kann zusätzliche Zeit in Anspruch nehmen. Wenn der Prozess abgeschlossen ist, wird als Status *done* (fertig) angezeigt. 

5. Führen Sie einen Mount für den Datenträger durch.  

   a. Sie müssen den Datenträger mit 'mount' bereitstellen, um ihn verwenden zu können. 

      <pre><code>mkdir -p /mnt/myvolume</pre></code>
      
      <pre><code>mount /dev/vdb1 /mnt/myvolume</pre></code>

      Dabei ist *myvolume* ein Ordnername Ihrer Wahl. 

   b. Überprüfen Sie, ob Ihr Datenträger aufgelistet wird und bereit ist. 

      <pre><code>df -h</pre></code>

6. (Optional) Stellen Sie den Datenträger mit 'mount' permanent bereit.  

   Sie möchten den Datenträger möglicherweise permanent bereitstellen, sodass Sie den Mount nicht nach jedem Neustart wiederholen müssen. 

   a. Ermitteln Sie die UUID für Ihren Datenträger. 

      <pre><code>blkid</pre></code>

   b. Kopieren Sie die UUID, die aufgelistet wird. 

   c. Bearbeiten Sie die Informationen der Dateisystemtabelle. 

      <pre><code>nano /etc/fstab</pre></code>      

   d. Fügen Sie die folgende Zeile mit Ihrer ermittelten UUID am Ende der Datei ein und speichern Sie die Datei. 
   
      <pre><code>UUID=xxxxxx /mnt/myvolume ext4 defaults  0 2</pre></code>

   e. Starten Sie den virtuellen Server erneut, um zu testen, ob der Datenträger permanent bereitgestellt wird. 

      <pre><code>reboot</pre></code>

  Wenn der virtuelle Server wieder aktiv ist, melden Sie sich am virtuellen Server an und ändern das Verzeichnis in den neuen Ordner, den Sie erstellt haben. Navigieren Sie zum Beispiel zum Ordner **cd /mnt/myvolume**. 

  Sie können den Datenträger jetzt verwenden. 
