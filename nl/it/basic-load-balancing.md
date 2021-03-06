---

copyright:
  years: 2017
lastupdated: "2017-08-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Bilanciamento del carico di base
Il servizio IBM Bluemix load balancer distribuisce il traffico tra più istanze server (server virtuale e bare metal) che risiedono localmente, nello stesso data center. 

## Programma di bilanciamento del carico pubblico 
Viene assegnato un nome dominio completo e accessibile pubblicamente alla tua istanza del servizio del programma di bilanciamento del carico. Puoi utilizzare questo nome dominio per accedere alle tue applicazioni ospitate dietro il servizio del programma di bilanciamento del carico. Le istanze di calcolo di backend che ospitano la tua applicazione devono essere su una rete privata cloud IBM. 

**NOTA:** ti raccomandiamo di eseguire il provisioning dei tuoi server di backend come ‘solo privato’, a meno che non richiedano la connettività pubblica diretta. Questa procedura ti aiuta ad avere una migliore protezione e a conservare il tuo indirizzo IP pubblico. Le applicazioni ospitate in questi server di backend sono ancora accessibili sulla rete pubblica utilizzando il programma di bilanciamento del carico.  

## Protocolli/Porte applicazione di backend e frontend
Puoi definire fino a 10 porte (protocolli) dell'applicazione di frontend e associarle alle rispettive porte (protocolli) nei server dell'applicazione di backend. Il nome dominio completo assegnato alla tua istanza del servizio del programma di bilanciamento del carico e le porte dell'applicazione di frontend sono esposti con il mondo esterno. Le richieste utente in entrata vengono ricevute su queste porte. 

D'altra parte, le porte di backend sono conosciute solo internamente. Queste porte di backend potrebbero non essere le stesse delle porte di frontend. Ad esempio, il programma di bilanciamento del carico può essere configurato per ricevere il traffico web/HTTP in entrata su nella porta di frontend 80, mentre i server di backend sono in ascolto sulla porta personalizzata 81. 

Le porte/protocolli di frontend supportate sono HTTP, HTTPS e TCP. Le porte/protocolli di backend supportate sono HTTP e TCP. Il traffico HTTPS in entrata deve essere terminata nel programma di bilanciamento del carico per consentire la comunicazione HTTP di testo semplice con il server di backend. 

**NOTE:**

* Durante la configurazione iniziale, puoi possibile definire solo fino a due porte di frontend. Quando un programma di bilanciamento del carico viene creato, puoi modificare la configurazione della porta per definire ulteriori porte, fino al massimo di dieci porte.
* Tutte le dieci porte di frontend devono essere associate alla stessa serie di istanze del server di backend.
* Il numero massimo di istanze del server che possono essere posizionate dietro a un programma di bilanciamento del carico è 50.
* L'intervallo di porte compreso tra 56500 e 56520 è riservato per scopi di gestione e non può essere utilizzato come porte virtuali di frontend. 

## Metodi di bilanciamento del carico
I seguenti tre metodi di bilanciamento del carico sono disponibili per la distribuzione del traffico tra i server dell'applicazione di backend:

* **Round Robin:** Round Robin è il metodo di bilanciamento del carico predefinito. Con questo metodo, il programma di bilanciamento del carico inoltra le connessioni client in entrata in modalità round robin ai server di backend. Di conseguenza, tutti i server di backend ricevono all'incirca un numero uguale di connessioni client.

* **Round Robin ponderato:** con questo metodo, il programma di bilanciamento del carico inoltra le connessioni client in entrata ai server di backend in base al peso assegnato a tali server. Ad ogni server viene assegnato un peso predefinito di 50, che può essere personalizzato con qualsiasi valore compreso tra 0 e 100. 

	Ad esempio, se ci sono tre applicazioni server A, B e C, e i loro pesi sono personalizzati con 60, 60 e 30 rispettivamente, i server A e B riceveranno lo stesso numero di connessioni, mentre il server C ne riceverà la metà. 

	**NOTE:** 

	* Reimpostare il peso su ‘0’ significa che nessuna nuova connessione sarà inoltrata a tale server, ma tutto il traffico esistente continuerà a fluire finché rimane attivo. L'utilizzo di un peso di ‘0’ può aiutare a terminare un server correttamente e a rimuoverlo dalla rotazione del servizio. 
	* Il valori del peso del server sono applicabili solo con il metodo 'round robin ponderato'. Vengono ignorati con i metodi di bilanciamento del carico 'round robin' e 'numero minimo di connessioni'. 

* **Numero minimo di connessioni:** con questo metodo, l'istanza del server che inoltra il numero minimo di connessioni a un ora specificata riceve la successiva connessione client. 
