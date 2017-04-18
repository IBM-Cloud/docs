{:new_window: target="_blank"}


# Preparando volumes do {{site.data.keyword.blockstorageshort}} 
{: #preparing-block-storage-volume}

Última atualização: 29 de julho de 2016
{: .last-updated}

  Depois de criar o volume e anexá-lo a um servidor virtual, deve-se montar e preparar o volume para ser usado.
  
  **Nota**: comandos relevantes podem variar, dependendo do sistema operacional específico. Para obter mais informações, consulte a documentação
do seu sistema operacional. As etapas a seguir foram testadas usando um servidor virtual CentOS.
  
  Para preparar um volume, siga estas etapas:

1. Efetue login no servidor virtual.  

   <pre><code>ssh -i security_key_name.pem ibmcloud@xxx.xx.xx.xx</pre></code>

   **Nota:** para localizar o ID de usuário padrão, o nome da chave de segurança e o endereço IP público, visualize a guia de visão geral do servidor virtual. O ID de usuário padrão é *ibmcloud*. Para obter informações sobre como efetuar login no servidor virtual usando SSH, consulte [Efetuando login em uma instância de servidor virtual a partir de um terminal Linux](../../virtualmachines/vm_manage_instances.html#vm_login). 

2. Verifique se o seu volume está anexado.  

   <pre><code>sudo su -</pre></code>
   
   **Nota:** se o comando *sudo su* não funcionar para seu sistema operacional, use *sudo* antes de cada comando. Por exemplo, *sudo fdisk -l*.
   
   <pre><code>fdisk -l</pre></code>

   As informações sobre o volume são listadas em direção à parte inferior do texto informativo. Por exemplo, *Disk /dev/vdb: 10.7 GB, 10737418240 bytes*.

3. Particione o disco.

   a. Inicie fdisk e crie uma nova partição.
    
     <pre><code>fdisk /dev/vdb</pre></code>

   b. Insira **n** para criar uma nova partição.
   
   c. Insira **p** para especificar a partição primária.
   
   d. Para criar uma partição, insira **1**.
   
   e. A menos que você tenha requisitos específicos, selecione valores padrão nos prompts restantes e pressione Enter.

   f. Insira **w** para gravar a partição.
   
   g. Verifique se o novo disco foi criado.
   
     <pre><code>fdisk -l</pre></code>

     **Nota:** o nome do novo disco é geralmente o nome da partição na qual ela foi criada mais um número incremental, como 1. Por exemplo, *vdb1*.

4. Formate o volume. 

   Deve-se formatar o volume para que ele armazene informações. Esse exemplo usa ext4, no entanto, é possível usar qualquer sistema de arquivos que seja suportado.

   <pre><code>mkfs -t ext4 /dev/vdb1</pre></code>

    **Nota:** a etapa para gravar superblocos e informações de contabilidade do sistema de arquivos pode demorar um tempo extra para ser concluída. Quando o processo estiver concluído, você verá *done* listado como o status.

5. Monte o volume. 

   a. Deve-se montar o volume para usá-lo.

      <pre><code>mkdir -p /mnt/myvolume</pre></code>
      
      <pre><code>mount /dev/vdb1 /mnt/myvolume</pre></code>

      em que *myvolume* é um nome de pasta à sua escolha.

   b. Verifique se seu volume está listado e pronto.

      <pre><code>df -h</pre></code>

6. (Opcional) Monte o volume permanentemente. 

   Talvez você queira montar o volume permanentemente, para que não precise repetir a montagem após uma reinicialização.

   a. Localize o UUID do volume.

      <pre><code>blkid</pre></code>

   b. Copie o UUID listado.

   c. Edite as informações da tabela de sistema de arquivos.

      <pre><code>nano /etc/fstab</pre></code>      

   d. Cole a linha a seguir, incluindo seu UUID específico, na parte inferior do arquivo e salve.
   
      <pre><code>UUID=xxxxxx /mnt/myvolume ext4 defaults  0 2</pre></code>

   e. Para testar se o volume está montado permanentemente, reinicialize o servidor virtual.

      <pre><code>reboot</pre></code>

  Quando o servidor virtual estiver em execução novamente, efetue login no servidor virtual e mude os diretórios para a nova pasta criada. Por exemplo, navegue para **cd /mnt/myvolume**.

  Agora é possível usar o volume.
