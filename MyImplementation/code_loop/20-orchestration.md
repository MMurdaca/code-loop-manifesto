# C.O.D.E. Loop - Orchestration Layer Rule

## Metadata

- Rule ID: CL-RULE-20
- Layer: Orchestration
- Status: Active
- Applies To: Work decomposition, dependency planning, responsibility mapping

## Purpose

Governare il layer Orchestration in modo che l'intent venga tradotto in struttura operativa senza essere riscritto.

L'Orchestration deve anche espandere o aggiornare l'artifact tree, rendendo ogni ramo tracciabile come decomposizione del parent, e impedire che una richiesta che cambia un contratto gia' approvato venga trattata come nuovo root scollegato.

## Scope

Questa rule si applica alla decomposizione di lavoro, alla definizione di dipendenze, sequencing, rischi, responsabilita' e struttura parent-child degli artifact.

## Allowed Inputs

1. Concept Artifact approvato;
2. change o clarification response approvate dal layer superiore;
3. vincoli gia' noti che impattano sequencing e dipendenze;
4. Artifact Tree Overview corrente;
5. known unknowns e assunzioni critiche dichiarate dal Concept;
6. assunzioni su identita', relazioni e invarianti dichiarate dal Concept.

## Required Outputs

Uno o piu' Orchestration Artifact che, per ciascun ramo rilevante, dichiarino almeno:

1. decomposition units;
2. dependency map;
3. sequencing rationale;
4. responsibility boundaries;
5. risk list;
6. coverage statement rispetto al Concept;
7. parent scope covered, quando il Concept viene propagato in piu' rami;
8. child artifact candidates;
9. Artifact Tree Overview update;
10. deferred, blocked or not-yet-decomposed scope;
11. drift impact assessment quando la decomposizione tocca identita', relazioni dati, invarianti o contratti condivisi.

## Mandatory Behaviors

1. coprire esplicitamente ogni punto rilevante del Concept Artifact;
2. rendere visibili dipendenze, rischi e blocchi;
3. mantenere tracciabile il legame tra intent e struttura operativa;
4. rendere espliciti i rami di propagazione quando il Concept e' troppo ampio per una sola decomposizione leggibile;
5. dichiarare per ogni ramo quale porzione del parent copre e quale porzione resta deferred o non ancora decomposta;
6. evidenziare lacune o conflitti anziche' compensarli nel sequencing;
7. proporre change request upward quando l'intent risulta non eseguibile o migliorabile in modo rilevante;
8. aggiornare l'artifact tree quando vengono creati, bloccati, completati o rimappati rami;
9. mantenere la vista globale come tracking, non come luogo di logica operativa;
10. impedire comunicazioni laterali implicite tra sibling: le dipendenze tra sibling devono essere esplicite;
11. collegare ogni richiesta di cambio identita', relazione o contratto condiviso al parent e ai sibling impattati invece di aprirla automaticamente come root indipendente;
12. applicare default `Review` quando la decomposizione rivela architectural contract drift e non esiste policy locale esplicita.

## Forbidden Behaviors

1. cambiare obiettivi o criteri di successo del Concept;
2. introdurre scope implicito non approvato;
3. trasformare il layer in un design tecnico dettagliato;
4. nascondere uncoverage o rischi per far apparire il piano piu' lineare;
5. lasciare implicita la sovrapposizione o il conflitto tra rami sibling;
6. usare l'Artifact Tree Overview per sostituire gli artifact detail file;
7. creare decomposition unit senza parent, status o coverage leggibili;
8. trattare un nodo bloccato come se fosse semplicemente deferred;
9. creare un nuovo root per aggirare la re-validation di un parent o sibling gia' impattato.

## Validation Requirements

L'Orchestration Artifact e' valido solo se:

1. mostra copertura rispetto al Concept;
2. esplicita dipendenze e sequencing in modo eseguibile;
3. delimita responsabilita' e rischi principali;
4. rende leggibile il parent scope covered del ramo corrente o del set di rami;
5. non contiene override impliciti dell'intent;
6. la mappa dei child artifact e' coerente con l'Artifact Tree Overview;
7. gli stati dei rami sono distinguibili e non richiedono inferenze dalla conversazione;
8. i potenziali drift architetturali sono associati al parent corretto e non nascosti come nuovo scope indipendente.

## Escalation Triggers

1. il Concept non permette una decomposizione affidabile;
2. una dipendenza critica cambia priorita' o scope del lavoro;
3. emerge un miglioramento strutturale che richiede revisione dell'intent;
4. il Design segnala che la struttura operativa e' insufficiente o incoerente;
5. due rami orchestrativi risultano in conflitto o non coprono piu' correttamente il parent;
6. l'artifact tree e gli artifact detail file descrivono strutture divergenti;
7. un ramo richiede informazioni critiche non presenti nel Concept;
8. una nuova richiesta modifica identita', relazioni dati, invarianti o contratti condivisi gia' coperti da un parent approvato.

## Rationale

L'Orchestration e' il layer che impedisce il salto diretto da idea a implementazione.

Questa rule riduce context drift, sequencing implicito, perdita di responsabilita' e tracking parallelo non governato.
