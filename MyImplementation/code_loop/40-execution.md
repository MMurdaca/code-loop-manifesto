# C.O.D.E. Loop - Execution Layer Rule

## Metadata

- Rule ID: CL-RULE-40
- Layer: Execution
- Status: Active
- Applies To: Implementation, refactoring, testing, integration
- Version: 3.0

## Purpose

Governare il layer Execution in modo che l'implementazione resti allineata al Design Artifact e produca evidenza verificabile invece di deviazioni implicite.

In V3 l'Execution deve anche rispettare esplicitamente quality policy, truthfulness tecnica e aggiornamento dello stato degli artifact.

## Scope

Questa rule si applica alla generazione del codice, ai refactoring, ai test, all'integrazione, alla segnalazione di mismatch o miglioramenti rilevanti e all'aggiornamento dello stato del ramo implementato.

## Allowed Inputs

1. Design Artifact approvato;
2. eventuali exception o re-validation request approvate;
3. criteri di validazione definiti upstream;
4. Artifact Tree Overview corrente;
5. contratti, assunzioni e condizioni residue dichiarate nel Design Artifact.

## Required Outputs

Uno o piu' Execution Artifact che, per ciascun ramo rilevante, dichiarino almeno:

1. implemented scope;
2. test and validation evidence;
3. detected mismatches;
4. unresolved issues;
5. deviation notes;
6. integration impact;
7. checkpoint outcome sul ramo corrente;
8. files, modules or components touched;
9. verification commands or manual evidence;
10. Artifact Tree Overview status update;
11. assumptions confirmed or invalidated during execution.

## Mandatory Behaviors

1. implementare rispetto all'ultima baseline di design validata;
2. eseguire un checkpoint obbligatorio prima di ogni nuova tranche significativa di lavoro sul ramo corrente;
3. produrre evidenza di test o validazione invece di lasciare il comportamento implicito;
4. registrare mismatch, deviazioni e limiti noti distinguendo quelli locali al ramo da quelli che impattano il parent;
5. aprire richieste upward quando un problema impatta contratti, scope o intent;
6. trattare i miglioramenti rilevanti come change request e non come override locali;
7. verificare l'esistenza e il comportamento di API, librerie o file prima di basarci decisioni critiche;
8. mantenere codice leggibile, manutenibile e coerente con i contratti approvati;
9. preferire soluzioni semplici, robuste e sufficienti ai requisiti;
10. aggiornare lo stato del ramo implementato quando passa a `IN_PROGRESS`, `READY_FOR_VALIDATION`, `COMPLETED`, `BLOCKED` o stato equivalente.

## Forbidden Behaviors

1. ridefinire contratti o intent direttamente nel codice;
2. compensare in silenzio incoerenze del design;
3. nascondere fallimenti di validazione o mismatch materiali;
4. trattare l'ottimizzazione locale come autorita' sufficiente per cambiare il sistema;
5. continuare il lavoro su un ramo dopo un checkpoint fallito senza gate o risalita esplicita;
6. inventare risultati di test, output, metriche o comportamento non verificato;
7. introdurre complessita' non richiesta per rendere la soluzione piu' sofisticata;
8. lasciare che il codice diventi l'unica documentazione del razionale operativo.

## Validation Requirements

L'Execution Artifact e' valido solo se:

1. esplicita cosa e' stato implementato;
2. include evidenza di validazione sufficiente;
3. rende visibili mismatch, deviazioni e problemi aperti;
4. permette di confrontare l'implementazione con il Design Artifact;
5. rende leggibile a quale parent e a quale scope di design appartiene il ramo implementato;
6. distingue test eseguiti, test non eseguiti e verifiche non disponibili;
7. aggiorna o propone l'aggiornamento dello stato dell'artifact tree;
8. non richiede di dedurre dalla conversazione cosa e' stato fatto.

## Escalation Triggers

1. un test o una verifica contraddice il Design Artifact;
2. l'implementazione richiede un cambiamento di contratto o scope;
3. emerge un miglioramento progettuale che impatta il layer superiore;
4. manca una baseline di design abbastanza chiara per procedere;
5. un checkpoint obbligatorio mostra che il ramo non puo' continuare senza reinterpretare il parent o un contratto condiviso;
6. una dipendenza tecnica non si comporta come assunto dal Design;
7. la soluzione semplice sufficiente non e' possibile senza cambiare un vincolo upstream.

## Rationale

L'Execution e' il punto in cui i sistemi generativi tendono piu' facilmente a ottimizzare localmente.

Questa rule serve a impedire che il codice prenda il controllo del paradigma e a rendere verificabile cio' che e' stato davvero implementato.
