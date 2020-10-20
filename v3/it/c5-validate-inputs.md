---

layout: col-document
tags: OWASP Top Ten Proactive Controls 2018, C5
document: OWASP Top Ten Proactive Controls 2018
order: 9

---

# C5: Validare tutti i dati in ingresso

## Descrizione
L' input validation è una tecnica a livello di programmazione che assicura che solo dati formattati correttamente
possano entrare in un determinato componente software.

### Validità sintattica e semantica
Un' applicazione dovrebbe controllare che i dati siano sia *sintatticamente* sia *semanticamente* validi (nel suddetto ordine) prima
 di farne qualsivoglia utilizzo (incluso mostrarlo all' utente).

**Validità sintattica** significa che i dati sono nel formato previsto. Ad esempio, un' applicazione potrebbe permettere che un
 utente selezioni un "account ID" di quattro cifre per eseguire una certa operazione. L' applicazione dovrebbe assumere che l'utente sta 
inserendo il payload di una SQL Injection, e dovrebbe controllare che i dati inseriti abbiano una lunghezza esattamente pari a quattro, 
e consista di soli numeri (oltre a utilizzare una parametrizzazione della query appropriata).

**Validità semantica** include l' accettare soltanto input che si trovi all' interno di un certo intervallo di valori per il dato contesto e 
funzionalità applicativa. Ad esempio, una "start date" dovrebbe precedere sempre una corrispondente "end date".

### Whitelisting vs Blacklisting
Ci sono due approcci generali all' esecuzione della validazione sintattica, comunemente conosciuti come blacklisting e whitelisting:

* **Blacklisting** o **blacklist validation*** mira a controlare che i dati non consistano di contenuto "known bad" ovvero notoriamente nocivo. 
Ad esempio, un' applicazione web potrebbe bloccare input contenente esattamente il testo ``<SCRIPT>`` al fine di prevenire XSS. 
Comunque, questa difesa potrebbe essere aggirata con un tag script scritto in minuscolo o un mix di minuscolo e maiuscolo.
* **Whitelisting** o **whitelist validation** mira a controllare che i dati in questione soddisfino delle "known good rules" ovvero regole che
 li facciano ritenere sicuramente inoffensivi. 
Per esempio una regola di "whitelist validation" per un dato che rappresenti uno stato USA, potrebbe essere imporre che il
 codice sia di due lettere e appartenga alla lista dei codici noti.

**Importante**
Nel costruire software sicuro, il whitelisting l'approccio minimo raccomandato. Blacklisting è maggiormente soggetto a errori e
può essere bypassato da svariate tecniche di elusione ed è pericoloso se usato come principale tecnica. Nonostante il blacklisting 
può spesso essere eluso è comunque spesso utile per prevenire gli attacchi più semplici. Quindi mentre il **whitelisting** aiuta a limitare 
 la superficie d' attacco assicurando che i dati siano sintatticamente e semanticamente validi, il **blacklisting** aiuta a identificare
  e potenzialmente prevenire attacchi scontati.

### Validazione lato Client e lato Server
La validazione dell' input deve essere sempre fatta lato serve per sicurezza. Seppure la validazione lato client può essere utile sia 
a scopi funzionali, sia per alcuni scopi di sicurezza, spesso può essere bypassata facilmente. Ciò rende la validazione lato server 
ancora più fondamentale per la sicurezza. Ad esempio, una validazione JavaScript può allertare l' utente che un particolare campo deve consistere
 di numeri ma il server deve validare che i dati inviati siano effettivamente solo numeri e nel giusto intervallo di valori per quella funzionalità. 

### Espressioni regolari
Le espressioni regolari offrono un modo di controllare se dei dati presentano un pattern specifico. Eccone un semplice esempio.

La seguente espressione regolare è usata per definire una regola di whitelisting per validare usernames.

    ^[a-z0-9_]{3,16}$

Questa espressione regolare accetta solo lettere in minuscolo, numeri e il carattere underscore. Il nome utente è anche limitato 
a una lunghezza da tre a sedici caratteri.

**Attenzione: Potenziale per attacco di Denial of Service**

Bisogna fare attenzione quando si creano espressioni regolari. Espressioni mal progettate possono aprire la strada a 
 condizioni favorevoli ad un Denial of Service (vedi: [ReDoS](https://www.owasp.org/index.php/Regular_expression_Denial_of_Service_-_ReDoS) ). 
 Esistono svariati tool per verificare che una data espressione regolare non sia suscettibile di ReDoS.

**Attenzione: Complessità**

Le espressioni regolari sono solo un modo di validare. Le espressioni regolari sono spesso difficili da mantenere o capire per alcuni sviluppatori. 
Altre alternative di validazione sono basate sulla scrittura di metodi di validazione programmatica che possono essere più facili per alcuni in termini
di manutenzione.


### Limitazioni della validazione dell' input

**La validazione dell' input non sempre rende i dati "sicuri" dal momento che alcune forme di input più complesse potrebbero essere "valide"ma comunque pericolose. 
Ad esempio un indirizzo email valido potrebbe contenere una SQL Injection o un URL valido potrebbe contenere un attacco di Cross-Site Scripting**. 
Difese aggiuntive oltre la validazione dell' input dovrebbero anche essere applicate ai dati, come ad esempio la query parameterization o l' escaping.

### La sfida di validare dati serializzati
Alcune forme di input sono talmente complesse che una validazione può proteggere un' applicazione solo in minima parte. 
Per esempio, è pericoloso deserializzare dati “untrusted” o dati che possono essere manipolati da un agente esterno. 
L'unico schema architetturale "sicuro" è non accettare oggetti serializzati da fonti non fidate oppure deserializzare solo 
in modo limitato per alcuni tipi di dati semplici. È preferibile evitare di elaborare formati dati serializzati ed usare invece formati 
più facili da difendere, come ad esempio JSON.

If that is not possible then consider a series of validation defenses when processing serialized data.
* Implement integrity checks or encryption of the serialized objects to prevent hostile object creation or data tampering.
* Enforce strict type constraints during deserialization before object creation; typically code is expecting a definable 
set of classes. Bypasses to this technique have been demonstrated.
* Isolate code that deserializes, such that it runs in very low privilege environments, such as temporary containers.
* Log security deserialization exceptions and failures, such as where the incoming type is not the expected type, or 
the deserialization throws exceptions.
* Restrict or monitor incoming and outgoing network connectivity from containers or servers that deserialize.
* Monitor deserialization, alerting if a user deserializes constantly.


### Input inaspettato dall' utente (Mass Assignment)
Alcuni framework supportano il "binding" automatico dei parametri delle richieste HTTP ad oggetti lato server usati dall' applicazione. 
Questa potenzialità di auto-binding può permettere ad un hacker di modificare oggetti sul server in modo che non dovrebbero essere permessi. 
Mediante questa funzionalità, un attacker potrebbe modificare il livello di controllo d' accesso o aggirare la logica dell' applicazione.

Questo attacco ha svariati nomi, tra cui: mass assignment, autobinding e object injection.

Per fare un semplice esempio, se un oggetto "User" ha un campo "privilege" che specifica il livello di privilege dell' utente nell' applicazione, 
un utente malintenzionato può cercare pagine dove i dati utente vengono modificati e aggiungere privilege=admin ai parametri HTTP inviati. 
Se l' auto-binding è attivato in modo insicuro, l' oggetto lato server che rappresenta l' utente verrà modificato automaticamente di conseguenza.

Per gestire questo, si possono usare due approcci:
* Evitare di usare l' auto-binding dell' input e usare invece dei Data Transfer Objects (DTOs).
* Abilitare l' auto-binding ma impostare delle regole di whitelisting per ciascuna pagina o feature definendo quali campi possono essere auto-bound.

Ulteriori esempi all' indirizzo: [OWASP Mass Assignment Cheat Sheet](https://www.owasp.org/index.php/Mass_Assignment_Cheat_Sheet).

### Validare e “sanificare” HTML
Consideriamo un' applicazione che debba accettare HTML dagli utenti (tramite un editor WYSIWYG che fa manipolare il contenuto come HTML o
 funzionalità che accettano direttamente HTML nell' input). in una tale situazione validazione o escaping non saranno d'aiuto.

* Le espressioni regolari non sono abbastanza espressive per "capire" la complessità di HTML5.
* Encoding o escaping dell'HTML non sono utili perché non farebbero rappresentare correttamente l'HTML stesso.

Perciò, è consigliato usare una libreria che può interpretare e pulire testo formattato come HTML. 
Per approfondire su HTML Sanitization: [XSS Prevention Cheat Sheet on HTML Sanitization](https://www.owasp.org/index.php/XSS_(Cross_Site_Scripting)_Prevention_Cheat_Sheet#RULE_.236_-_Sanitize_HTML_Markup_with_a_Library_Designed_for_the_Job) 

### Funzionalità di validazione in Librerie e Framework
Tutti i linguaggi e la maggior parte dei framework forniscono librerie di validazione o funzioni che dovrebbero essere sfruttate per validare i dati. 
Tipicamente le librerie di validazione coprono tipi di dati più comuni, requisiti di lunghezza, intervalli numerici, controlli "is null" etc. 
Molti librerie e framework di validazione consentono di definire espressioni regolari o logica per validazione "custom" 
in modo da permettere al programmatore di sfruttare la funzionalità nell' applicazione. Esempi di funzioni di validazione 
includono PHP [filter functions](https://secure.php.net/manual/en/filter.examples.validation.php) o
il [Hibernate Validator](http://hibernate.org/validator/) in Java. Esempi di HTML Sanitizers 
includono [Ruby on Rails sanitize method](http://edgeapi.rubyonrails.org/classes/ActionView/Helpers/SanitizeHelper.html), 
[OWASP Java HTML Sanitizer](https://www.owasp.org/index.php/OWASP_Java_HTML_Sanitizer_Project) o 
[DOMPurify](https://github.com/cure53/DOMPurify).

## Vulnerabilità prevenute
* La validazione dell' input riduce la superficie di attacco di un' applicazione e a volte rende un attacco molto più difficile.
* La validazione dell' input è una tecninca che fornisce sicurezza per alcune forme di dati, specifiche a certi attacchie non può essere applicata in modo generico come una regola generale di sicurezza.
* La validazione dell' input non dovrebbe essere pensata come il principale modo di prevenire [XSS](https://www.owasp.org/index.php/XSS_(Cross_Site_Scripting)_Prevention_Cheat_Sheet), [SQL Injection](https://www.owasp.org/index.php/SQL_Injection_Prevention_Cheat_Sheet) and other attacks.

## Riferimenti
* [OWASP Cheat Sheet: Input Validation](https://www.owasp.org/index.php/Input_Validation_Cheat_Sheet)
* [OWASP Cheat Sheet: iOS - Security Decisions via Untrusted Inputs](https://www.owasp.org/index.php/IOS_Developer_Cheat_Sheet#Security_Decisions_via_Untrusted_Inputs_.28M7.29)
* [OWASP Testing Guide: Testing for Input Validation](https://www.owasp.org/index.php/Testing_for_Input_Validation)

## Strumenti
* [OWASP Java HTML Sanitizer Project](https://www.owasp.org/index.php/OWASP_Java_HTML_Sanitizer)
* [Java JSR-303/JSR-349 Bean Validation](http://beanvalidation.org/)
* [Java Hibernate Validator](http://hibernate.org/validator/)
* [JEP-290 Filter Incoming Serialization Data](http://openjdk.java.net/jeps/290)
* [Apache Commons Validator](https://commons.apache.org/proper/commons-validator/)
* PHP [filter functions](https://secure.php.net/manual/en/book.filter.php)
