---

layout: col-document
tags: OWASP Top Ten Proactive Controls 2018, C4
document: OWASP Top Ten Proactive Controls 2018
order: 8

---

# C4: Effettuare l' encoding e l' escaping dei dati

## Description

**Encoding** ed escaping sono tecniche di difesa aventi lo scopo di prevenire attacchi di tipo “injection”. 
Encoding (noto come "Output Encoding") consiste nel tradurre caratteri speciali in un formato diverso 
ma equivalente che non può essere pericoloso nell' interprete target, ad esempio 
trasformando il carattere ``<`` nella stringa ``&lt;`` quando la si renderizza in una pagina HTML. 
**Escaping** consiste invece nell' aggiungere un carattere speciale prima del carattere/stringa per evitare che venga interpretato erroneamente, 
Ad esempio, aggiungere un carattere ``\`` prima del carattere ``"``  in modo che sia interpretato come testo e non come la 
terminazione di una stringa.

Il miglior momento per applicare l'output encoding è **appena prima** che il contenuto venga passato all' interprete. 
Se questa difesa è attivata troppo presto nell' elaborazione di una richiesta, allora l' encoding / escaping 
potrebbe interferire con l'uso del contenuto in altre parti del programma. Se, Ad esempio, si facesse escaping di contenuto 
HTML prima di persisterlo nel database e in seguito l' interfaccia utente rifacesse l' escape
 il contenuto non verrà visualizzato correttamente a causa del doppio escaping.

### Encoding contestuale dell' output

L' encoding contestuale dell' output è una tecnica cruciale per fermare gli attacchi XSS. 
Questo tipo di difesa di applica all' output, quando si sta costruendo l' interfaccia utente, all' ultimo momento 
prima che dati "untrusted" siano aggiunti dinamicamente all' HTML. Il tipo di encoding dipenderà dalla locazione 
(o contesto) nel documento dove i dati verranno renderizzati o immagazzinati. I diversi tipi di encoding 
che possono essere usati per costruire interfacce sicure includono "HTML Entity Encoding", "HTML Attribute Encoding", 
"JavaScript Encoding" e "URL Encoding".

#### Esempi di Java Encoding
Per esempi dell' OWASP Java Encoder che fornisce l' output encoding contestuale si veda: 
[OWASP Java Encoder Project Examples](https://www.owasp.org/index.php/OWASP_Java_Encoder_Project#tab=Use_the_Java_Encoder_Project).


#### Esempi di encoding .NET
A partire da .NET 4.5, la libreria Anti-Cross Site Scripting è parte del framework, ma non abilitata per default. 
Si può specificare di usare AntiXssEncoder dalla suddetta libreria come encoder di default per l' intera applicazione 
usando i setting in web.conf. A questo punto è importante effettivamente dare l' encoding - cioè
 usare la giusta funzione dalla libreria AntiXSSEncoder per la giusta location dei dati nel documento.

#### Esempi di encoding PHP
**Zend Framework 2**

Nel Zend Framework 2 (ZF2), ``Zend\Escaper`` può essere usato per l'output encoding. Per encoding contestuale 
vedi [Context-specific escaping with zend-escaper](https://framework.zend.com/blog/2017-05-16-zend-escaper.html).

### Altri tipi di encoding e difese contro le Injection
Encoding/Escaping possono essere usate per neutralizzare contenuto verso altre forme d' injection. Per esempio, 
è possibile neutralizzare alcuni meta-caratteri speciali quando si aggiunge input ad un comando del sistema operativo. 
Questo viene detto "OS command escaping", "shell escaping", o in modi simili. 
Questa difesa può essere usata in generale per eliminare vulnerabilità di tipo "Command Injection".

Ci sono altre forme di escaping che possono essere usate per impedire le injection come ad esempio XML attribute escaping 
per la prevenzione di XML e "XML path" injection, così come l' LDAP distinguished name escaping che può essere usato
 per fermare varie forme di LDAP injection.

### Encoding dei caratteri e Canonicalizzazione
L' Encoding Unicode è un metodo per salvare i caratteri con più byte. Ovunque siano ammessi dati di input, 
i dati possono essere immessi tramite Unicode [Unicode](https://www.owasp.org/index.php/Unicode_Encoding) 
per camuffare codice nocivo e permettere tutta una serie di attacchi. [RFC 2279](https://tools.ietf.org/html/rfc2279) 
riporta molti modi in cui un testo può essere “encoded”.

La canonicalizzazione è un metodo in cui i sistemi convertono i dati in una forma semplice o standard.  
Le applicazioni web solitamente usano la canonicalizzazione per assicurare che tutto il contenuto
all content usi lo stesso tipo di carattere quando memorizzato oppure mostrato a schermo.

Per essere al sicuro contro attacchi che sfruttano la canonicalizzazione stessa un' applicazione dovrebbe essere gestire in modo safe
 l' eventuale immissione di caratteri malformati (Unicode o altri tipi).


## Vulnerabilità Prevenute
* [OWASP Top 10 2017 - A1: Injection](https://www.owasp.org/index.php/Top_10-2017_A1-Injection)
* [OWASP Top 10 2017 - A7: Cross Site Scripting (XSS)](https://www.owasp.org/index.php/Top_10-2017_A7-Cross-Site_Scripting_(XSS))
* [OWASP Mobile_Top_10_2014-M7 Client Side Injection](https://www.owasp.org/index.php/Mobile_Top_10_2014-M7)

## Riferimenti
* [XSS](https://www.owasp.org/index.php/Cross-site_Scripting_(XSS)) - Informazioni generali
* [OWASP Cheat Sheet: XSS Prevention](https://www.owasp.org/index.php/XSS_(Cross_Site_Scripting)_Prevention_Cheat_Sheet) - Prevenire XSS nelle applicazioni (EN)
* [OWASP Cheat Sheet: DOM based XSS Prevention](https://www.owasp.org/index.php/DOM_based_XSS_Prevention_Cheat_Sheet)
* [OWASP Cheat Sheet: Injection Prevention](https://www.owasp.org/index.php/Injection_Prevention_Cheat_Sheet)

## Strumenti
* [OWASP Java Encoder Project](https://www.owasp.org/index.php/OWASP_Java_Encoder_Project)
* [AntiXSSEncoder](https://docs.microsoft.com/en-us/dotnet/api/system.web.security.antixss.antixssencoder?redirectedfrom=MSDN&view=netframework-4.7.2)
* [Zend\Escaper](https://framework.zend.com/blog/2017-05-16-zend-escaper.html) - esempi di encoding contestuale (EN)
