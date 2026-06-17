# C.O.D.E. Loop - Design Layer Rule

## Metadata

- Rule ID: CL-RULE-30
- Layer: Design
- Status: Active
- Applies To: Contracts, interfaces, data models, edge cases, validation strategy
- Version: 3.0

## Purpose

Governare il layer Design in modo che la struttura operativa venga tradotta in una soluzione implementabile, coerente e verificabile.

In V3 il Design deve preservare truthfulness tecnica: non puo' inventare API, contratti, capacita' o garanzie non verificate.

## Scope

Questa rule si applica alle decisioni che fissano contratti, interfacce, modelli dati, invarianti, edge cases, dipendenze tra sibling e strategia di validazione.

## Allowed Inputs

1. Orchestration Artifact approvato;
2. vincoli Concept gia' propagati;
3. change o exception approvate che impattano il design;
4. Artifact Tree Overview corrente;
5. evidenze tecniche verificate o dichiarate come ipotesi.

## Required Outputs

Uno o piu' Design Artifact che, per ciascun ramo rilevante, dichiarino almeno:

1. contracts;
2. interfaces;
3. data model decisions;
4. invariants;
5. edge cases;
6. validation or test strategy;
7. parent scope covered e sibling dependencies, quando rilevanti;
8. verified technical facts;
9. design assumptions;
10. trade-off analysis, quando esistono alternative materiali;
11. Artifact Tree Overview status update, se il design cambia lo stato o la struttura dei rami.

## Mandatory Behaviors

1. tradurre ogni unita' orchestrativa rilevante in contratti o decisioni implementabili;
2. esplicitare invarianti e casi limite che l'Execution dovra' rispettare;
3. rendere verificabile la soluzione con una strategia di validazione leggibile;
4. mantenere leggibile il legame tra il ramo di design e il parent orchestrativo diretto;
5. rendere espliciti contratti condivisi o dipendenze tra sibling quando un ramo non e' isolato;
6. segnalare tradeoff o vincoli che cambiano il costo del downstream;
7. aprire escalation se il design rivela incoerenze non risolvibili localmente;
8. distinguere scelte tecniche verificate da ipotesi di design;
9. scegliere la soluzione piu' semplice che soddisfa completamente requisiti e vincoli;
10. definire input, output, constraints e acceptance criteria del ramo in modo consumabile dall'Execution.

## Forbidden Behaviors

1. ridefinire obiettivi o priorita' orchestrative senza richiesta upward;
2. demandare all'Execution contratti essenziali non definiti;
3. introdurre comportamento fuori scope in nome della convenienza tecnica;
4. lasciare edge cases materiali completamente impliciti;
5. lasciare implicito se un contratto vale solo per il ramo corrente o per piu' rami sibling;
6. inventare API, librerie, capacita' di piattaforma o garanzie non verificate;
7. introdurre astrazioni premature non giustificate dai requisiti;
8. nascondere un trade-off rilevante dietro una singola scelta presentata come inevitabile.

## Validation Requirements

Il Design Artifact e' valido solo se:

1. i contratti sono coerenti con intent e orchestrazione;
2. la soluzione e' testabile;
3. l'Execution puo' procedere sul ramo corrente senza dover inventare regole strutturali;
4. i rischi implementativi rilevanti sono stati nominati;
5. il parent scope covered e le dipendenze con sibling sono abbastanza chiari da sostenere il downstream;
6. le assunzioni tecniche critiche sono verificate o marcate come condizioni residue;
7. la complessita' introdotta e' proporzionata ai requisiti.

## Escalation Triggers

1. l'Orchestration non basta a definire un design coerente;
2. un contratto necessario collide con intent o scope approvati;
3. l'Execution segnala mismatch sostanziali non risolvibili localmente;
4. emerge un miglioramento architetturale che impatta il livello superiore;
5. due rami di design richiedono una ridefinizione del parent o di un contratto condiviso;
6. una decisione tecnica critica non puo' essere verificata con le informazioni disponibili;
7. la soluzione piu' semplice sufficiente richiede cambiare scope o criteri di successo.

## Rationale

Il Design e' il punto in cui il paradigma deve prevenire l'architectural drift prima che arrivi nel codice.

Questa rule rende l'Execution vincolata da un contratto verificabile, non da interpretazioni locali o da fiducia implicita in dettagli tecnici non controllati.
