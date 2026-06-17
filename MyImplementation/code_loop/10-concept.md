# C.O.D.E. Loop - Concept Layer Rule

## Metadata

- Rule ID: CL-RULE-10
- Layer: Concept
- Status: Active
- Applies To: Intent definition and intent revisions
- Version: 3.0

## Purpose

Governare il layer Concept in modo che l'intenzione venga formalizzata prima di ogni decomposizione strutturale o decisione implementativa.

In V3 il Concept deve anche rendere espliciti ambiguita', assunzioni, fatti verificati, ipotesi e criteri di qualita' che governeranno il downstream.

## Scope

Questa rule si applica a ogni definizione iniziale di intent e a ogni revisione significativa di obiettivi, vincoli, assunzioni e criteri di successo.

## Allowed Inputs

1. problema o opportunita' da affrontare;
2. obiettivi di business, prodotto o sistema;
3. vincoli tecnici, organizzativi o temporali;
4. assunzioni dichiarate;
5. richieste upward approvate che impattano l'intent;
6. evidenze, fonti o contesto verificato;
7. incertezze o informazioni mancanti emerse prima della decomposizione.

## Required Outputs

Un Concept Artifact che dichiari almeno:

1. problem statement;
2. objective set;
3. constraints;
4. assumptions;
5. success criteria;
6. out of scope;
7. known unknowns;
8. facts, deductions and hypotheses;
9. quality bar e priorita' operative;
10. candidate child scope, se il Concept e' troppo ampio per un solo ramo downstream.

## Mandatory Behaviors

1. definire cosa il sistema deve ottenere prima di decidere come costruirlo;
2. distinguere esplicitamente in-scope e out-of-scope;
3. dichiarare vincoli e assunzioni in modo leggibile;
4. formulare criteri di successo verificabili;
5. rendere visibili eventuali conflitti o ambiguita' invece di nasconderli;
6. rendere leggibile quando l'intent e' abbastanza ampio da richiedere una futura scomposizione in piu' rami di Orchestration;
7. distinguere fatti verificati, deduzioni e ipotesi prima che il downstream le trasformi in decisioni operative;
8. chiedere chiarimenti quando un'ambiguita' cambia obiettivi, vincoli, priorita' o criteri di successo;
9. preservare l'intent anche quando un'alternativa locale sembra piu' semplice o piu' veloce;
10. definire il minimo livello di qualita' atteso in termini di affidabilita', utilita' concreta e verificabilita'.

## Forbidden Behaviors

1. decomporre task o dipendenze operative come sostituto dell'intent;
2. imporre dettagli di design o execution non necessari al livello Concept;
3. trattare assunzioni implicite come decisioni gia' approvate;
4. lasciare indeterminati gli obiettivi principali quando il downstream dipende da essi;
5. presentare ipotesi, stime o deduzioni come fatti verificati;
6. permettere che l'Orchestration inventi intent mancante invece di richiedere chiarimento;
7. allargare lo scope per migliorare localmente la soluzione senza approvazione upward.

## Validation Requirements

Il Concept Artifact e' valido solo se:

1. contiene tutti i campi minimi richiesti;
2. non mostra conflitti interni evidenti non dichiarati;
3. i criteri di successo sono comprensibili e verificabili;
4. il downstream puo' iniziare l'orchestrazione senza dover inventare l'intent;
5. la futura scomposizione in rami non richiede di reinterpretare il Concept;
6. le assunzioni critiche sono approvate o esplicitamente bloccanti;
7. il quality bar non contraddice vincoli, tempi o priorita' dichiarate.

## Escalation Triggers

1. due obiettivi principali risultano incompatibili;
2. i vincoli disponibili non bastano a delimitare il problema;
3. emerge una revisione sostanziale dell'intent;
4. il downstream segnala che il Concept e' insufficiente o ambiguo;
5. non e' possibile distinguere fatti verificati da ipotesi su elementi critici;
6. una richiesta tenta di sostituire il Concept con una soluzione implementativa gia' decisa.

## Rationale

Il Concept deve governare, non seguire le ottimizzazioni locali.

Questa rule protegge il sistema dal requirement drift, dalle ridefinizioni implicite del problema e dalla trasformazione di incertezza non verificata in lavoro operativo.
