---

layout: col-document
tags: OWASP Top Ten Proactive Controls 2018, Intro
document: OWASP Top Ten Proactive Controls 2018
order: 4

---

# Introduzione
La OWASP Top Ten Proactive Controls 2018 è una lista di tecniche di sicurezza che dovrebbe essere 
considerata per qualsiasi progetto di sviluppo software.
Questo documento è scritto per assistere gli sviluppatori nuovi allo sviluppo di software sicuro.

Uno dei principali obiettivi di questo documento è di fornire una guida pratica e concreta che 
aiuti gli sviluppatori a costruire software sicuro. Queste tecniche dovrebbero essere applicate 
proattivamente nelle fasi iniziali dello sviluppo software per assicurare la massima efficacia.

## La Top 10 Proactive Controls
La lista è in ordine decrescente d' importanza, con il 1 come più importante:
* C1: Definire dei requisiti di sicurezza
* C2: Utilizzare librerie e framework di sicurezza 
* C3: Accesso sicuro al database
* C4: Effettuare l' encoding e l' escaping dei dati
* C5: Validare tutti i dati in ingresso
* C6: Implementare correttamente l' identità digitale
* C7: Imporre controlli d' accesso
* C8: Proteggere i dati ovunque
* C9: Implementare logging e monitoring di sicurezza
* C10: Gestire tutti gli errori ed eccezioni

## Come è stata creata questa lista

Questa lista è inizialmente stata creata dagli attuali leader del progetto con contribuzioni di molti volontari. 
Il documento è stato poi condiviso globalmente in modo da considerare anche contributi anonimi. 
Centinaia di contributi sono stati accettati da questo processo di “community”.

## Pubblico destinatario
Questo docmento è stato scritto principalmente per sviluppatori. A ogni modo, development managers, product owners, 
Q/A professionals, program managers and chiunque coinvolto nella produzione di software può anche beneficiare da questo documento. 

## Come usare questo documento
Lo scopo di questo documento è di fornire una prima sensibilizzazione sulla produzione di software sicuro. 
Questo documento fornisce anche un buon fondamento di argomenti per incentivare ulteriori training sullo sviluppo di software sicuro. 
Questi controlli dovrebbero essere usati consistentemente e accuratamente in tutte le applicazioni. 
Comunque, questo documento dovrebbe essere visto come un punto di partenza piuttosto che un insieme esaustivo di tecniche e prassi. 
Un vero e proprio “secure development process” dovrebbe includere requisiti completi da uno standard come il OWASP ASVS 
in aggiunta ad una serie di attività di sviluppo software descritte nei cosiddetti Maturity Models
[OWASP SAMM](https://www.owasp.org/index.php/OWASP_SAMM_Project) and [BSIMM](https://www.bsimm.com/).

## Link al progetto OWASP Top 10 Project
Il progetto OWASP Top 10 Proactive Controls è simile a
[OWASP Top 10](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project)
ma si concentra maggiormente su tecniche difensive e controlli piuttosto che sui rischi. 
Ciascuna tecnica o controllo in questo documento corrisponde ad uno o più elementi del OWASP Top 10 (che è *risk based*). 
Queste corrispondenze sono incluse alla fine di ciascuna descrizione del controllo.
