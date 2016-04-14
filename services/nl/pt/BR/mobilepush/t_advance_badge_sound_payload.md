---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}
# Configurar badge, som, carga útil e badge iOS

{: #badge-sound-payload}

Configure um badge iOS, som e carga útil JSON adicional.

1. No painel Notificações push, vá para a guia
                        **Notificações**.
2. Vá para a seção **Campos opcionais**
para configurar os seguintes recursos de notificação push. badge ios, som e carga útil adicional.

	a. **Badge iOS** - Para dispositivos iOS, o número a ser
exibido como badge do ícone de app. Se essa propriedade
estiver ausente, o badge não será mudado. Para remover o badge,
configure o valor dessa propriedade para 0.

	b. **Arquivo de som** - Insira uma sequência para apontar
para o arquivo de som em seu app móvel. Na carga útil, especifique o nome da sequência do
arquivo de som a ser usado.


	Android

	```
	"settings": {
	     "gcm" : {
	     "sound":"tt.wav",
	  }
	 }  
	```

	iOS

	```
	"settings": {
	     "apns" : {
	      "badge": 10,
	      "sound": "tt.wav",
	  }
	}
	``` 		
**Carga útil adicional** - essa carga útil pode ser qualquer
par de valores de chave e deve ser um objeto JSON que você queira enviar com a
notificação push.

	```
	{"key":"value", "key2":"value2"}
	```
