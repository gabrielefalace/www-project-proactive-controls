---

layout: col-document
tags: OWASP Top Ten Proactive Controls 2018, C1
document: OWASP Top Ten Proactive Controls 2018
order: 5

---

# C1: Definire dei requisiti di sicurezza

## Descrizione

Un requisito di sicurezza (Security Requirements) è uno _statement_ riguardo a una funzionalità di sicurezza necessaria che garantisce che una delle 
svariate proprietà di sicurezza del software sia soddisfatta. I requisiti di sicurezza sono derivati da standard industriali, 
normative rilevanti e la storia di vulnerabilità pregresse. I requisiti di sicurezza definiscono nuove features o 
estensioni di attuali feature per risolvere uno specifico problema di sicurezza o eliminare una potenziale vulnerabilità.

I requisiti di sicurezza forniscono un fondamento di funzionalità di sicurezza verificate per un' applicazione. 
Tali _Security Requirements_ standard permettono agli sviluppatori di riutilizzare la definizione dei controlli e 
le "best practices" anziché creare una approccio alla sicurezza "personalizzato" per ogni applicazione. 
Questi stessi requisiti verificati forniscono la soluzione a problemi di sicurezza già noti, in quanto successi nel passato. 
I requisiti esistono proprio per prevenire il ripetersi di problemi di sicurezza già successi in precedenza.

### Lo standard OWASP ASVS
[The OWASP Application Security Verification Standard (ASVS)](https://www.owasp.org/index.php/Category:OWASP_Application_Security_Verification_Standard_Project) 
è un catalogo di requisiti di sicurezza disponibili e criteri di verifica. OWASP ASVS può essere una fonte 
di requisiti di sicurezza dettagliati per i team di sviluppo.

I Security requirements sono categorizzati in diversi blocchi sulla base di una funzione più generale di sicurezza. 
Ad esempio, lo standard ASVS contiene categorie come _authentication_, _access control_, _error handling_ / _logging_, 
e _web services_. Ciascuna categoria contiene un insieme di requisiti basati sulle relative _best practices_ 
sotto forma di affermazioni (statements) verificabili.

### Estendere i requisiti con User Stories e Misuse Cases

I requisiti ASVS sono statement basilari e verificabili che possono essere estesi con User Stories e  
cosiddetti “Misuse Cases”. Il vantaggio di una user story o misuse case è che lega l' applicazione in modo preciso 
a cosa l' utente o l' attacker fa al sistema, piuttosto che descrivere ciò che il sistema offre all' utente. 

Di seguito è un esempio di estensione del requisito ASVS 3.0.1. Dalla sezione "Authentication Verification Requirements" 
del ASVS 3.0.1, il requisito 2.19 si concentra sulle password di default.

> 2.19 Verificare che non ci siano password di default in uso per il framework applicativo o qualsiasi componente 
> usato dall' applicazione (ad es. "admin/password").

Questo requisito contiene sia l' azione di verificare che non ci siano password di default, e porta con se anche
la raccomandazione che nessuna password di default dovrebbe essere utilizzata nell' applicazione.

Una user story si focalizza sul punto di vista dell utente, amministratore, o attacker del sistema, 
e descrive funzionalità sulla base di ciò che l' utente vuole che il sistema faccia. 
Una user story prende la forma di "As a user, I can do x, y, and z".

    In qualità di Utente, posso inserire username e password per accedere all' applicazione.
    In qualità di Utente, posso inserire una password lunga 1023 caratteri.

Quando la storia si focalizza su un attacker e le sue azioni, viene detta "misuse case".

    In qualità di attacker, posso inserire username e password di dafault per accedere.

Questa storia contiene lo stesso messaggio del tradizionale requisito da ASVS, con dettagli aggiuntivi 
sull' utente o l' attacker che aiutano a renderla più testabile.

## Implementazione
Un uso efficace di questi requisiti richiede 4 passi: scoperta / selezione, 
documentazione, implementazione e infine la verifica della corretta realizzazione delle nuove features di 
sicurezza e funzionalità nell' applicazione. 

### Scoperta e selezione
Il processo comincia con la scoperta e la selezione dei requisiti di sicurezza. In questa fase, lo sviluppatore 
 comprende i requisiti di sicurezza da una fonte standard come il ASVS e sceglie quali requisiti 
includere per un determinato rilascio dell' applicazione. Il punto della scoperta e selezione è di scegliere un numero 
 gestibile di requisiti di sicurezza per questo rilascio o sprint, e poi continuare ad iterare per ogni sprint, 
 aggiungendo via via più funzioni di sicurezza nel tempo.

### Investigazione e documentazione
Nella fase d' investigazione e documentazione, lo sviluppatore revisiona l' applicazione esistente, confrontandola con i 
nuovi requisiti di sicurezza per determinare se essa attualmente soddisfa il requisito oppure è necessario sviluppare. 
L' investigazione culmina con la documentazione dei risultati della revisione.

### Implementazione e test
Una volta determinata la necessità di sviluppare, lo sviluppatore deve ora modificare l'applicazione in 
qualche modo per aggiungere nuove funzionalità o eliminare le opzioni insicure. In questa fase lo sviluppatore 
prima determmina il design necessario per implementare il requisito, e dopo completa i necessari cambiamenti nel codice. 
Bisognerebbe aggiungere opportuni test per confermare la messa in opera della nuova funzionalità or 
dimostrare la rimozione dell' opzione insicura individuata precedentemente.

## Vulnerabilità prevenute
I security requirements definiscono i requisiti di funzionalità di un' applicazione. Una sicurezza migliore, incorporata 
 sin dall' inizio del ciclo di vita di un' applicazione risulta nella prevenzione di intere categorie di vulnerabilità. 

## References
* [OWASP Application Security Verification Standard (ASVS)](https://www.owasp.org/index.php/Category:OWASP_Application_Security_Verification_Standard_Project)
* [OWASP Mobile Application Security Verification Standard (MASVS)](https://github.com/OWASP/owasp-masvs)
* [OWASP Top Ten](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project)
