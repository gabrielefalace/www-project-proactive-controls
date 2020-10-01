---

layout: col-document
tags: OWASP Top Ten Proactive Controls 2018, C2
document: OWASP Top Ten Proactive Controls 2018
order: 7

---

# C3: Accesso sicuro al database

## Descrizione
This section describes secure access to all data stores, including both relational databases and NoSQL databases. Some areas to consider:

1. Secure queries
2. Secure configuration
3. Secure authentication
4. Secure communication

### Interrogazioni (query) sicure
La cosiddetta SQL Injection avviene quando un input dell' utente considerato untrusted (ovvero: la cui attendibilità non può essere verificata)
 è dinamicamente aggiunto ad una query SQL in modo non sicuro, spesso tramite una semplice concatenazione di stringhe.
 La SQL Injection è uno dei rischi peggiori per la sicurezza delle applicazioni. 
 La SQL Injection è facile da sfruttare e può portare al furto, la dstruzione o la modifica di un intero database. 
 L' applicazione può perfino essere usata per eseguire comandi pericolosi sul sistema operativo su cui gira il database, 
 dando così a un attacker una via d' ingresso nella rete.

Per mitigare il rischio di SQL Injection, bisogna impedire che ogni input considerato untrusted venga interpretato come parte di un comando SQL. 
Il miglior modo di fare ciò è mediante la tecnica di programmazione detta 'Query Parameterization'. 
Questa difesa dovrebbe essere applicata a SQL, OQL, così come anche alla costruzione di Stored Procedure.

Una buona lista di esempi di Query Parameterization in ASP, ColdFusion, C#, Delphi, .NET, Go, Java, Perl, PHP, PL/SQL, PostgreSQL, Python, 
R, Ruby and Scheme può essere trovata su [http://bobby-tables.com](http://bobby-tables.com/) 
e in [OWASP Cheat Sheet on Query Parameterization](https://www.owasp.org/index.php/Query_Parameterization_Cheat_Sheet).

**Attenzione riguardo alla Query Parameterization**

Alcune parti di una query non sono parametrizzabili. Queste parti differiscono da un database vendo all' altro. 
Bisogna accertarsi di di fare una validazione exact-match accurata o escaping manuale quando si ha a che fare con parametri 
di query che non si possono parametrizzare. Inoltre, mentre l' uso di query parametrizzate ha un effetto massicciamente positivo sulle performance,
 alcune query parametrizzate in specifici database potrebbero impattare le performance negativamente. 
 Occorrerebbe testare sempre le performance delle query; In special modo query complesse con abbondante uso di clausole 'like' o ricerca testuale.

### Configurazione sicura
Purtroppo, i DBMS (DataBase Management System) non sono sempre pre-configurati in modo sicuro. 
Bisogna fare attenzione ad assicurare che i controlli di sicurezza messi a disposizione dal DBMS e dalle piattaforme di hosting 
siano attivi e configurati appropriatamente. Ci sono standard, guide, e benchmark disponibili per i DBMS più comuni. 

Una guida veloce su come mettere a punto una configurazione sicura è disponibile su 
[Database Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Database_Security_Cheat_Sheet.html#database-configuration-and-hardening).

### Autenticazione sicura
Tutti gli accessi al DB devono essere autenticati appropriatamente. 
L' autenticazione sul DBMS dovrebbe avvenire in sicurezza, tramite un canale sicuro. 
Le credenziali devono essere appropriatamente messe in sicurezza e disponibili per l' uso.

Una guida veloce su come mettere a punto un processo di autenticazione sicuro può essere trovato su 
[Database Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Database_Security_Cheat_Sheet.html#authentication).

### Comunicazione sicura
La maggior parte dei DBMS supporta una serie di metodi di comunicazione (services, APIs, ecc) - sicuri (autenticati, cifrati) 
e insicuri (non autenticati o in chiaro). È una buona pratica usare solo le opzioni di comunicazione sicure così come 
 spiegato nella sezione *Proteggere i dati ovunque*.

Una veloce guida su come mettere a punto un processo di comunicazione sicuro può essere trovato nel 
[Database Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Database_Security_Cheat_Sheet.html#connecting-to-the-database).

## Vulnerabilità Prevenute
* [OWASP Top 10 2017- A1: Injection](https://www.owasp.org/index.php/Top_10-2017_A1-Injection)
* [OWASP Mobile Top 10 2014-M1 Weak Server Side Controls](https://www.owasp.org/index.php/Mobile_Top_10_2014-M1)

## Riferimenti
* [OWASP Cheat Sheet: Query Parameterization](https://www.owasp.org/index.php/Query_Parameterization_Cheat_Sheet)
* [OWASP Cheat Sheet: Database Security](https://cheatsheetseries.owasp.org/cheatsheets/Database_Security_Cheat_Sheet.html)
* [Bobby Tables: A guide to preventing SQL injection](http://bobby-tables.com/)
* [CIS Database Hardening Standards](https://www.cisecurity.org/cis-benchmarks/)
