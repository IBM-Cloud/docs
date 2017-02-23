---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-23"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Criando e conectando um simulador de dispositivo Node-RED
Use o Node-RED para criar um simulador de dispositivo e enviar dados do dispositivo simulado para sua organização do {{site.data.keyword.iot_full}}.  
{:shortdesc}

Node-RED é uma ferramenta para conexão de dispositivos de hardware, APIs e serviços on-line de maneiras novas e interessantes. Para obter mais informações, consulte o website [Node-RED](http://nodered.org/).  

É possível executar sua instância do Node-RED em seu próprio ambiente ou utilizá-la como um aplicativo do {{site.data.keyword.Bluemix_notm}}. O processo a seguir inclui as instruções para o {{site.data.keyword.Bluemix_notm}}.

Para criar e conectar o simulador de dispositivo Node-RED:

1. Crie o simulador de dispositivo Node-RED
   Use o simulador de dispositivo para enviar mensagens do dispositivo MQTT para o {{site.data.keyword.iot_short_notm}}. O simulador de dispositivo simulou o envio de dados de um contêiner de carga para um broker MQTT, como o {{site.data.keyword.iot_short_notm}}.
    1. Efetue login no {{site.data.keyword.Bluemix_notm}} em: https://console.ng.bluemix.net
    2. Selecione a guia **Catálogo**.
    3. Localize a seção Modelos do catálogo de serviços e clique em **Comunidade Node-RED Starter BETA**. **Dica:** clique [aqui](https://console.ng.bluemix.net/catalog/starters/node-red-starter/) para ir diretamente para a página do Node-RED Starter.
    4. Na página do Node-RED Starter, selecione o espaço no qual deseja implementar o Node-RED, verifique as seleções de Criar um aplicativo e clique em **Criar** para incluir o Node-RED em sua organização do Bluemix.  
    Por
exemplo:  
     - Espaço: dev
     - Nome: myDevice
     - Host: myDevice

    Deixe o resto das opções em seus valores padrão. Após o aplicativo ser implementado, você será levado à página Iniciar codificação com o Node-RED.  
    **Nota:** o processo de preparação pode levar alguns minutos.

    3. Clique no link Rotas para abrir o Node-RED.  
    Exemplo: `http://simulatedDevice.mybluemix.net`
    4. Clique em **Acessar o seu editor de fluxo do Node-RED** para abrir o editor.
    5. Copie os dados de fluxo do Node-RED localizados na seção [Dados de fluxo do nó do Node-RED](#flow_data) deste documento.
    5. No editor de fluxo do Node-RED, clique no menu no canto superior direito e selecione **Importar > Área de transferência**.  
    6. Cole a área de transferência no campo de entrada de importação de nós e clique em **Ok**.
    O fluxo do simulador de dispositivo é importado para o editor de fluxo.

2. Registre seu dispositivo com o {{site.data.keyword.iot_short_notm}}  
Siga estas etapas para conectar o dispositivo de amostra do Node-RED:
 1. No {{site.data.keyword.Bluemix_notm}}, acesse Painel
 2. Selecione o espaço no qual você implementou o {{site.data.keyword.iot_short_notm}}.
 3. Clique no quadro **{{site.data.keyword.iot_short_notm}}**.
 4. Clique em **Ativar painel** para abrir o painel do {{site.data.keyword.iot_short_notm}}.
 5. Selecione **Dispositivos**
 6. Clique em **Incluir dispositivo**
 7. Clique em **Criar tipo de dispositivo**.
 9. Insira um nome descritivo e uma descrição para o tipo de dispositivo, como `sample_device`.
 10. Opcional: insira os atributos de tipo de dispositivo.
 11. Opcional: insira os metadados de tipo de dispositivo.
 12. Clique em **Criar** para incluir o novo tipo de dispositivo.
 13. Clique em **Avançar** para incluir seu dispositivo.
 14. Insira um ID de dispositivo como `Device001`.
 15. Opcional: insira os metadados de dispositivo.
 16. Clique em **Avançar** para incluir uma conexão de dispositivo com um token de autenticação gerado automaticamente.
 17. Verifique se as informações de resumo estão corretas e, em seguida, clique em **Incluir** para incluir a conexão.
 18. Na página de informações sobre o dispositivo que é aberta, copie e salve as informações sobre o dispositivo:  
  <ul>
  <li> ID de Organização
  <li> Tipo do Dispositivo
  <li> ID do dispositivo
  <li> Método de Autenticação
  <li> Token de Autenticação
  </ul>
  **Dica:** você precisará do ID da organização, Token de autenticação, Tipo de dispositivo e ID do dispositivo nas próximas etapas para finalizar a configuração do aplicativo Node-RED para concluir a conexão.

2. Conecte seu dispositivo ao {{site.data.keyword.iot_short_notm}}  
 1. Abra o editor de fluxo do Node-RED.
 2. Clique duas vezes no nó Publicar em IoT.
 3. Verifique se a entrada do tópico é: `iot-2/evt/event_name/fmt/json` **Dica:** a parte /event_name do tópico configura o nome do evento para os eventos publicados.
 4. Clique no ícone de edição ao lado do campo Servidor.
 5. Atualize o nome do servidor para corresponder à sua organização do {{site.data.keyword.iot_short_notm}}.  
 ```
 {organization_ID}.messaging.internetofthings.ibmcloud.com
 ```  
 Em que {organization_ID} é o *ID da organização* anteriormente salvo.
 6. Atualize o identificador de cliente com seu ID da organização, tipo de dispositivo e ID do dispositivo:
 ```
 d:{organization_ID}:{device_type}:{device_ID}
   ```  
   Em que {organization_ID}, {device_type} e {device_ID} são os valores anteriormente salvos.
 7. Clique na guia **Segurança**.
 8. Verifique se o campo Nome do usuário tem o valor `use-token-auth`.
 9. Atualize o campo Senha com o *Token de autenticação* anteriormente salvo.
 10. Clique em **Atualizar** e, em seguida, em **OK**.
 12. No canto superior direito do editor de fluxo do Node-RED, clique em **Implementar**.
 13. Verifique se o status de conexão do nó Publicar em IoT exibe *conectado*.  **Dica:** se a conexão não for feita, verifique novamente as configurações inseridas. Até mesmo um pequeno erro de recortar e colar causará falha na conexão.

4. Valide a conexão de dispositivo
 1. Em outra guia do navegador ou janela, abra o painel {{site.data.keyword.iot_short_notm}}.
 2. Selecione **Dispositivos** e clique em **Device001** ou no nome do dispositivo incluído, se for diferente.  
 A página de informações sobre o dispositivo é aberta. Esta visualização permite ver o status da conexão para o seu dispositivo. O dispositivo deve aparecer como desconectado neste estágio.   
 3. De volta ao editor de fluxo do Node-RED, clique no botão no nó Injetar para gerar uma carga útil do ativo.  
 A carga útil contém os pontos de dados a seguir:  
 ```
 {"d":
  { "name":"My Device",
    "location":
    {
      "longitude":-87.90,
      "latitude":43.03
    },
    "velocity":13,
    "type":"GPS"
  }
 }
 ```
  {:codeblock}  

 3. Na guia de depuração da área de janela direita, verifique se as mensagens são criadas.  
 4. De volta à página de informações do dispositivo do {{site.data.keyword.iot_short_notm}}, agora o dispositivo deve estar conectado. Verifique se você vê os mesmos pontos de dados recebidos do dispositivo.  
 ```
 Event	Datapoint	 Value	Time Received
 event_name	d.name	My Device	May 16, 2016 2:22:18 PM
 event_name	d.location.longitude	-87.90	May 16, 2016 2:22:18 PM
 event_name	d.location.latitude	43.03	May 16, 2016 2:22:18 PM
 event_name	d.velocity	13	May 16, 2016 2:22:18 PM
 event_name	d.type	GPS	May 16, 2016 2:22:18 PM
 ```  
  {:codeblock}  

 Agora você conectou seu dispositivo IoT de amostra ao {{site.data.keyword.iot_short_notm}} e pode ver os dados do dispositivo.

## Dados de fluxo do nó do Node-RED
{: #flow_data}  
Copie o texto a seguir para sua área de transferência e, em seguida, cole-o na área de transferência de importação ao importar nós no editor de fluxo do Node-RED.   
**Importante:** certifique-se de que você copie todo o texto, incluindo os colchetes inicial e final.  

```
[{"id":"e658d1b6.c187e8","type":"mqtt-broker","z":"965c3822.02c558","broker":"organization_ID.messaging.internetofthings.ibmcloud.com","port":"1883","clientid":"d:organization_ID:device_type:device_ID","usetls":false,"verifyservercert":true,"compatmode":true,"keepalive":"60","cleansession":true,"willTopic":"","willQos":"0","willRetain":"false","willPayload":"","birthTopic":"","birthQos":"0","birthRetain":"false","birthPayload":""},{"id":"23f82ce8.126dc4","type":"mqtt out","z":"965c3822.02c558","name":"Publish to IoT","topic":"iot-2/evt/event_name/fmt/json","qos":"","retain":"","broker":"e658d1b6.c187e8","x":480,"y":273,"wires":[]},{"id":"92e2f51f.5126","type":"inject","z":"965c3822.02c558","name":"Send data","topic":"","payload":"","payloadType":"num","repeat":"","crontab":"","once":false,"x":92,"y":265,"wires":[["832b025d.2d24c"]]},{"id":"832b025d.2d24c","type":"function","z":"965c3822.02c558","name":"Device payload","func":"var name1 = \"My Device\";\nvar type1 = \"GPS\";\nvar longitude1 = [-98.49,-97.74,-96.79,-94.20,-90.19,-94.57,-87.62,-87.90,-93.26,-95.99];\nvar latitude1 = [29.42,30.26,32.77,36.37,38.62,39.09,41.87,43.03,44.97,41.25];\nvar velocity1 = context.get('velocity1')||0;\n\n\n\nvelocity1 = velocity1+1;\nif(velocity1 > 20) velocity1=0;\ncontext.set('velocity1',velocity1);\n\nvar counter1 = context.get('counter1')||0;\ncounter1 = counter1+1;\nif(counter1 > 9) counter1 = 0;\ncontext.set('counter1',counter1);\n\nmsg = {\n \tpayload: JSON.stringify(\n \t { d:{\n \"name\" : name1,\n \"location\" : \n {\n \"longitude\" : longitude1[counter1],\n \t \"latitude\" : latitude1[counter1]\n },\n \"velocity\" : velocity1,\n \t \"type\" : type1\n \t }\n \t }\n )\n}\n\nreturn msg;","outputs":1,"noerr":0,"x":270,"y":108,"wires":[["f04ddebd.f55298","23f82ce8.126dc4"]]},{"id":"f04ddebd.f55298","type":"debug","z":"965c3822.02c558","name":"","active":true,"console":"false","complete":"false","x":250,"y":384,"wires":[]},{"id":"d606058f.d3422","type":"comment","z":"965c3822.02c558","name":"Configure Publish to IoT for your environment","info":"1. Double click the node.\n2. Click the edit icon next to the Server field.\n3. Update the Server name to correspond to your Watson IoT Platform organization.\n `organization_ID.messaging.internetofthings.ibmcloud.com`\n\n4. Update the Client ID with your orgainzaiton ID, device type, and device ID:\n `d:organization_ID:device_type:device_ID`\n\n5. Click the Security tab.\n6. Verify that the Username field has the value use-auth-token.\n7. Update the Password field with the Authentication Token that you saved earlier.\n8. Click Update and then OK.\n9. In the upper right corner of the Node-RED flow editor, click Deploy. ","x":570,"y":241,"wires":[]},{"id":"b997cfe2.ebfd7","type":"comment","z":"965c3822.02c558","name":"Function Node","info":"The Function node allows you to pass each message though a JavaScript function.\n\nThe Javascript function creates the message payload that is sent to your Watson IoT Platform organization.","x":271,"y":77,"wires":[]},{"id":"1ce4e378.c5a565","type":"comment","z":"965c3822.02c558","name":"Debug Node","info":"The Debug node causes any message to be displayed in the Debug sidebar. By default, it just displays the payload of the message, but it is possible to display the entire message object.","x":250,"y":414,"wires":[]},{"id":"ba916f5e.695db8","type":"comment","z":"965c3822.02c558","name":"Inject Node","info":"The Inject node allows you to inject messages into a flow, either by clicking the button on the node, or setting a time interval between injects.","x":75,"y":236,"wires":[]}]
```
{:codeblock}
