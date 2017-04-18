{:new_window: target="_blank"}


# {{site.data.keyword.blockstorageshort}} 볼륨 준비 
{: #preparing-block-storage-volume}

마지막 업데이트 날짜: 2016년 7월 29일
{: .last-updated}

  볼륨을 작성하여 가상 서버에 연결한 후 볼륨을 사용할 수 있도록 마운트하고 준비해야 합니다. 
  
  **참고**: 관련 명령은 특정 운영 체제에 따라 다릅니다. 자세한 정보는 해당 운영 체제 문서를 참조하십시오. 다음 단계는 CentOS 가상 서버를 사용하여 테스트되었습니다. 
  
  볼륨을 준비하려면 다음 단계를 수행하십시오. 

1. 가상 서버에 로그인하십시오.   

   <pre><code>ssh -i security_key_name.pem ibmcloud@xxx.xx.xx.xx</pre></code>

   **참고:** 기본 사용자 ID, 보안 키 이름, 공인 IP 주소를 찾으려면 가상 서버의 개요 탭을 보십시오. 기본 사용자 ID는 *ibmcloud*입니다. SSH를 사용하여 가상 서버에 로그인하는 방법에 대한 정보는 [Linux 터미널에서 가상 서버 인스턴스에 로그인](../../virtualmachines/vm_manage_instances.html#vm_login)을 참조하십시오.  

2. 볼륨이 연결되었는지 확인하십시오.   

   <pre><code>sudo su -</pre></code>
   
   **참고:** *sudo su* 명령이 사용자 운영 체제에서 작동하지 않는 경우에는 각 명령 앞에 *sudo*를 사용하십시오. 예를 들면, *sudo fdisk -l*입니다. 
   
   <pre><code>fdisk -l</pre></code>

   볼륨 정보가 정보 텍스트의 아래쪽으로 나열됩니다. 예를 들면, *Disk /dev/vdb: 10.7 GB, 10737418240 bytes*입니다. 

3. 디스크를 파티션으로 나누십시오. 

   a. fdisk를 시작하여 새 파티션을 작성하십시오. 
    
     <pre><code>fdisk /dev/vdb</pre></code>

   b. 새 파티션을 작성하려면 **n**을 입력하십시오. 
   
   c. 기본 파티션을 지정하려면 **p**를 입력하십시오. 
   
   d. 하나의 파티션을 작성하려면 **1**을 입력하십시오. 
   
   e. 특정 요구사항이 없으면 나머지 프롬프트에서 기본값을 선택하고 Enter를 누르십시오. 

   f. 파티션에 쓰려면 **w**를 입력하십시오. 
   
   g. 새 디스크가 작성되었는지 확인하십시오. 
   
     <pre><code>fdisk -l</pre></code>

     **참고:** 새 디스크 이름은 일반적으로 디스크가 작성된 파티션의 이름에 증분 값(예: 1)을 더합니다. 예를 들면, *vdb1*입니다. 

4. 볼륨을 포맷하십시오.  

   정보를 저장하려면 볼륨을 포맷해야 합니다. 이 예에서는 ext4를 사용하지만 지원되는 모든 파일 시스템을 사용할 수 있습니다. 

   <pre><code>mkfs -t ext4 /dev/vdb1</pre></code>

    **참고:** 수퍼블록과 파일 시스템 계정 정보를 기록하는 단계를 완료하는 데 추가적인 시간이 소요될 수 있습니다. 프로세스가 완료되면 *done* 상태가 표시됩니다. 

5. 볼륨을 마운트하십시오.  

   a. 볼륨을 사용하려면 마운트해야 합니다. 

      <pre><code>mkdir -p /mnt/myvolume</pre></code>
      
      <pre><code>mount /dev/vdb1 /mnt/myvolume</pre></code>

      여기서 *myvolume*은 선택한 폴더 이름입니다. 

   b. 볼륨이 나열되고 준비되었는지 확인하십시오. 

      <pre><code>df -h</pre></code>

6. (선택사항) 볼륨을 영구적으로 마운트하십시오.  

   다시 부팅한 후 마운트를 반복할 필요가 없도록 볼륨을 영구적으로 마운트할 수 있습니다. 

   a. 볼륨의 UUID를 찾으십시오. 

      <pre><code>blkid</pre></code>

   b. 나열된 UUID를 복사하십시오. 

   c. 파일 시스템 테이블 정보를 편집하십시오. 

      <pre><code>nano /etc/fstab</pre></code>      

   d. 특정 UUID를 포함하여 다음 행을 파일의 맨 아래에 붙여 넣은 후 저장하십시오. 
   
      <pre><code>UUID=xxxxxx /mnt/myvolume ext4 defaults  0 2</pre></code>

   e. 볼륨이 영구적으로 마운트되었는지 테스트하려면 가상 서버를 다시 부팅하십시오. 

      <pre><code>reboot</pre></code>

  가상 서버가 다시 실행되면 가상 서버에 로그인하여 디렉토리를 작성한 새 폴더로 변경하십시오. 예를 들면, **cd /mnt/myvolume**으로 이동하십시오. 

  이제 볼륨을 사용할 수 있습니다. 
