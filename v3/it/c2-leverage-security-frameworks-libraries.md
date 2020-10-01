---

layout: col-document
tags: OWASP Top Ten Proactive Controls 2018, C2
document: OWASP Top Ten Proactive Controls 2018
order: 6

---

# C2: Utilizzare librerie e framework di sicurezza

## Descrizione
Librerie di programmazione sicura (o secure coding) e framework software con sicurezza già integrata sono di grande aiuto per gli sviluppatori per 
prevenire difetti di sicurezza nella progettazione e nell' implementazione. A developer writing an application from scratch might not have sufficient knowledge, time, or budget to properly implement or maintain security features. Leveraging security frameworks helps accomplish security goals more efficiently and accurately.

## Linee guida per l' implementazione
Quando si includono librerie o framework di terze parti nel software, è importante considerare le seguenti “best practice”:

1. Usare librerie e framework da fonti fidate, soggette a manutenzione attiva ed ampiamente utilizzate nel settore.
2. Create e mantenere un inventario o catalogo di tutte le librerie di terze parti.
3. Mantenere proattivamente aggiornati tutti i componenti e le librerie. Utilizzare tool come 
[OWASP Dependency Check](https://www.owasp.org/index.php/OWASP_Dependency_Check) e [Retire.JS](https://retirejs.github.io/retire.js/) 
per identificare dipendenze del progetto e controllare che non ci siano vulnerabilità note e rese pubbliche.
4. Ridurre la superficie d' attacco incapsulando la libreria ed esponendo solo le funzionalità necessarie nel software.

## Vulnerabilità prevenute
Framework e librerie sicuri possono aiutare a prevenire un ampia gamma di vulnerabilità nelle applicazioni. 
È cruciale mantenere tali framework e librerie aggiornati come descritto in [using components 
with known vulnerabilities [Top Ten 2017 risks](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project).

## Strumenti
* [OWASP Dependency Check](https://www.owasp.org/index.php/OWASP_Dependency_Check) - identifica le dipendenze di un progetto e verifica che non abbiano vulnerabilità note
* [Retire.JS](http://retirejs.github.io/retire.js/) scanner per librerie JavaScript
