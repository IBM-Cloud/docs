---

copyright:
  years: 2015, 2016
lastupdated: "2017-02-24"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Manutenzione aggiornamenti VM
{: #maintenance_and_vm_updates}

## Strategia di manutenzione
{: #maintenance_strategy}

IBM WebSphere Application Server in Bluemix viene aggiornato regolarmente, garantendo che le nuove istanze del servizio vengano create con i fix pack e le patch correnti. Il cloud offre alla gestione middleware un provisioning facile e rapido
di nuove istanze del servizio. Si prevede che molti utilizzatori
eseguiranno un upgrade a una nuova istanza del servizio, quando vorranno applicare la manutenzione. Per gli utilizzatori che
vogliono mantenere istanze del servizio durature, sono disponibili dei repository di manutenzione
per guest operativo sottostante e middleware. Questi repository consentono agli utenti di gestire il loro ambiente proprio come farebbero se fosse installato in loco.

## Aggiornamenti VM

Le seguenti sezioni illustrano come applicare le modifiche di sistema della macchina virtuale.

Puoi aggiornare la tua VM come qualsiasi altro sistema RHEL. Utilizzando la gestione pacchetti Red Hat
"Yum", puoi installare, aggiornare, disinstallare ed effettuare altre operazioni di vario tipo con i tuoi
pacchetti.

Il tuo sistema è configurato per ricevere gli aggiornamenti dal server satellite Red Hat di IBM. Questo satellite
ti fornisce pacchetti sicuri appartenenti alla rete Red Hat, inviati dalla gestione pacchetti
Yum.

Il server satellite è gestito da IBM e non può essere modificato dal tuo sistema.

Per ulteriori informazioni, vedi [Applicazione di aggiornamenti dei pacchetti su Red Hat Enterprise Linux](https://access.redhat.com/articles/11258#rhel6){: new_window} e [Yum: la gestione pacchetti Red Hat](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Deployment_Guide/ch-yum.html){: new_window}.
