# C.O.D.E. Loop - Rules Overview

## Scopo

Questa cartella contiene il rule system operativo di C.O.D.E. Loop.

Il sistema integra tre famiglie di vincoli:

1. guardrail operativi su accuratezza, ambiguita', truthfulness, preservazione dell'intent e semplicita';
2. formalizzazione esplicita degli artifact come albero di lavoro e come unica fonte operativa di verita';
3. controllo esplicito sul drift dei contratti architetturali, in particolare su identita', identificativi, relazioni dati, invarianti e contratti condivisi tra artifact.

Questo file introduce il sistema, ne chiarisce la logica generale e definisce l'ordine di lettura delle rules.

## Che Cos'e' C.O.D.E. Loop

C.O.D.E. Loop e' uno stile operativo per sviluppo AI-assisted.

L'idea centrale e' questa:

il codice non deve essere il primo atto decisionale, ma l'output finale di una catena di chiarimento, decomposizione, design, esecuzione e validazione.

In pratica il sistema cerca di ridurre:

1. drift di requirement;
2. reinterpretazioni implicite dell'obiettivo;
3. ottimizzazioni locali che cambiano il problema senza dirlo;
4. perdita del razionale mentre si produce codice;
5. conoscenza operativa non tracciata in artifact;
6. assunzioni, fonti o funzionalita' inventate per compensare lacune informative.

## Obiettivo Operativo

Lo scopo del sistema e' massimizzare qualita', affidabilita', profondita' tecnica e utilita' concreta dell'assistenza.

Il sistema deve privilegiare:

1. accuratezza rispetto alla velocita';
2. coerenza logica rispetto alla produzione immediata;
3. verificabilita' rispetto alla speculazione;
4. semplicita' rispetto alla complessita' non necessaria;
5. mantenimento dell'intent rispetto alle reinterpretazioni autonome;
6. evidenza artifact-driven rispetto alla memoria conversazionale.

L'obiettivo e' produrre risultati professionali, utilizzabili in contesti reali e sostenibili nel tempo.

## Architectural Contract Drift

Una richiesta localmente implementabile puo' cambiare il significato di un contratto gia' approvato.

Questo tipo di drift include cambiamenti a:

1. identita' di entita' o oggetti;
2. stabilita' degli identificativi;
3. relazioni dati;
4. ownership o collegamenti simili a foreign key;
5. invarianti;
6. contratti condivisi tra parent e sibling artifact;
7. criteri di validazione gia' approvati.

Quando emerge questo rischio, la richiesta non puo' essere trattata automaticamente come nuovo root indipendente o come normale dettaglio di execution.

La policy di gestione drift ha tre modi:

1. `Mitigate`: procedere solo con mitigazione documentata, condizioni esplicite e gate adeguato;
2. `Review`: fermarsi prima dell'implementazione e chiedere approvazione o re-validation del parent. Questo e' il default quando non esiste una policy locale esplicita;
3. `Strict`: bloccare l'execution fino a revisione upstream e re-validation.

## Come Va Letto Il Sistema

Il sistema e' organizzato in quattro layer principali piu' tre regole cross-layer:

1. Concept: chiarisce problema, obiettivi, vincoli, assunzioni e criteri di successo;
2. Orchestration: decompone il lavoro, esplicita dipendenze, sequencing, rischi e artifact figli;
3. Design: definisce contratti, modelli, edge case e strategia di validazione;
4. Execution: implementa codice, test ed evidenze senza alterare implicitamente il livello superiore;
5. Validation Gates: decide se un artifact puo' propagarsi o se un ramo puo' continuare;
6. Escalation: governa chiarimenti, change request, exception e re-validation;
7. Artifact Schema: impone forma minima, lineage, dettaglio operativo e overview dell'albero.

Il sistema introduce tre meccanismi strutturali:

1. checkpoint obbligatori tra tranche di lavoro significative;
2. artifact gerarchici con propagazione `1 -> N` tra layer adiacenti;
3. artifact tree overview come vista globale di tracking, distinta dagli artifact detail file.

Il bundle definisce il comportamento generale.

Se un progetto richiede vincoli locali, brief, esempi o istruzioni di avvio, questi vanno aggiunti fuori da questo bundle.

## Modello Artifact

Ogni elemento di lavoro esiste operativamente come artifact.

Gli artifact:

1. sono organizzati in una struttura ad albero;
2. hanno relazioni parent-child esplicite;
3. rappresentano la decomposizione progressiva dell'intent;
4. sono la fonte di verita' operativa del sistema;
5. contengono il contesto necessario per essere letti e validati senza memoria implicita.

La vista globale dell'albero serve solo a:

1. visualizzare la gerarchia degli artifact;
2. monitorare lo stato di avanzamento;
3. navigare la struttura del progetto.

La vista globale non contiene logica operativa. La logica operativa vive nei singoli artifact detail file.

Esempio sintetico di tree overview:

```text
A1 System Root [ACTIVE]
  A1.1 Component Design [COMPLETED]
  A1.2 Architecture Definition [READY_FOR_VALIDATION]
  A1.4 Execution Flow [IN_PROGRESS]
    A1.4.1 Planner Definition [IN_PROGRESS]
    A1.4.2 Execution Layer [BLOCKED]
```

Esempio tabellare equivalente:

```text
ID       Artifact                 Parent   Status
A1       System Root              N/A      ACTIVE
A1.1     Component Design         A1       COMPLETED
A1.4.2   Execution Layer          A1.4     IN_PROGRESS
```

## Glossario Operativo Minimo

I termini seguenti hanno significato operativo stabile:

1. Artifact: unita' minima di verita' operativa, leggibile e validabile.
2. Artifact Tree Overview: vista globale di navigazione e tracking degli artifact.
3. Artifact Detail File: file operativo dedicato a un singolo artifact.
4. Parent Artifact: artifact del layer o livello immediatamente superiore da cui deriva il lavoro corrente.
5. Child Artifact: artifact del livello immediatamente inferiore che copre una porzione dichiarata del parent.
6. Branch: ramo di lavoro identificabile che collega parent e child lungo la propagazione.
7. Branch ID: identificativo stabile del ramo corrente, usato per collegare artifact, gate e richieste.
8. Parent Scope Covered: porzione esplicita del parent che il child sta decomponendo, progettando o implementando.
9. Checkpoint: controllo obbligatorio di riallineamento prima della tranche significativa successiva sul ramo corrente.
10. Branch Gate: gate applicato a un child artifact e al suo parent diretto quando il cambiamento resta locale al ramo.
11. Parent Gate: gate applicato quando il cambiamento altera copertura, contratti condivisi o coerenza complessiva del parent.
12. Layer Gate: gate applicato quando l'effetto del cambiamento non riguarda piu' un solo parent ma il layer nel suo insieme.
13. Architectural Contract Drift: cambiamento che altera identita', identificativi, relazioni dati, invarianti, criteri di validazione o contratti condivisi gia' approvati.
14. Drift Policy Mode: modo operativo che governa il drift architetturale; valori ammessi: `Mitigate`, `Review`, `Strict`.

## Default Minimo Per Task Piccoli

Se il task non richiede branching, il comportamento minimo corretto e' questo:

1. un Artifact Tree Overview minimale;
2. un Concept Artifact;
3. un Orchestration Artifact;
4. un Design Artifact;
5. un Execution Artifact.

Per gli artifact root senza parent diretto, i metadata di branching vanno comunque esplicitati in forma leggibile, usando valori coerenti come:

1. `Parent Artifact ID: N/A`;
2. `Parent Layer: N/A`;
3. `Branch ID: root`;
4. `Parent Scope Covered: full scope`;
5. `Propagation Scope Status: root`.

## Quando Aprire Un Nuovo Ramo

Un nuovo ramo va aperto quando almeno una di queste condizioni e' vera:

1. il parent copre responsabilita' o rischi materialmente distinti;
2. un singolo artifact downstream diventerebbe troppo ampio per essere validato in modo leggibile;
3. esistono contratti o decisioni che possono evolvere separatamente;
4. la validazione locale sarebbe piu' chiara se limitata a una porzione dichiarata del parent;
5. il tracking dello stato richiede distinguere nodi con avanzamento, blocchi o gate diversi.

Un nuovo ramo non va aperto solo per aumentare il numero di documenti.

## Modalita' d'Uso

Per usare il sistema in un progetto:

1. leggi prima questo `README.md`;
2. leggi poi le rules nell'ordine indicato sotto;
3. chiarisci se il task richiede un solo artifact per layer o una scomposizione in piu' rami;
4. crea o aggiorna l'Artifact Tree Overview prima di propagare lavoro significativo;
5. se apri un ramo, dichiara sempre parent artifact, branch ID e parent scope covered;
6. applica le regole al task corrente mantenendo separati i vincoli generali del sistema e il contesto locale del progetto;
7. esegui un checkpoint obbligatorio prima di ogni nuova tranche significativa di lavoro sul ramo attivo;
8. se un checkpoint fallisce, non continuare sul ramo corrente senza gate o risalita esplicita;
9. aggiungi brief, perimetro, esempi o istruzioni operative in file distinti dal bundle delle rules.

## Ordine di Lettura Consigliato

1. `README.md`;
2. `00-principles.md`;
3. `10-concept.md`;
4. `20-orchestration.md`;
5. `30-design.md`;
6. `40-execution.md`;
7. `50-validation-gates.md`;
8. `60-escalation.md`;
9. `70-artifact-schema.md`.

## Interpretazione Pratica Per Un Agente

Se stai iniziando un task da zero, il comportamento atteso non e' "scrivi subito il codice".

Il comportamento atteso e' piuttosto:

1. chiarire cosa si sta cercando di ottenere;
2. distinguere fatti verificati, deduzioni e ipotesi;
3. congelare il perimetro del task e i criteri di successo;
4. creare o aggiornare la mappa degli artifact;
5. decomporre il lavoro in rami tracciabili quando un artifact e' troppo ampio per essere governato bene come blocco unico;
6. definire parent, child e scope coperto prima di aprire un nuovo ramo downstream;
7. definire design e strategia di test prima delle scelte implementative principali;
8. implementare solo dopo che i layer superiori e il ramo corrente sono abbastanza chiari;
9. eseguire checkpoint obbligatori di riallineamento tra una tranche significativa e la successiva;
10. rendere visibili mismatch, conflitti, blocchi, deviazioni o incertezze;
11. validare prima di propagare al passo successivo o al ramo successivo.

## Selezione del Gate Corretto

Quando devi validare un cambiamento, usa il gate piu' piccolo che copre davvero il significato del cambiamento:

1. usa un Branch Gate se il cambiamento resta confinato a un child artifact e al suo parent diretto;
2. usa un Parent Gate se il cambiamento altera la copertura, i contratti condivisi o la coerenza tra sibling dello stesso parent;
3. usa un Layer Gate se l'effetto non e' piu' riconducibile a un solo parent o impatta il layer nel suo insieme.

Se il cambiamento altera identita', relazioni dati, invarianti o contratti condivisi, non usare un Branch Gate locale salvo policy `Mitigate` esplicita e condizioni tracciate. In assenza di policy locale, applica `Review`.

## Cosa Non Dare Per Scontato

Il sistema non autorizza a dare per scontato:

1. contesto implicito non documentato;
2. intent chiaro se non e' stato esplicitato;
3. autorizzazione a cambiare scope, contratto o criteri di successo;
4. equivalenza tra soluzione veloce e soluzione coerente con il sistema;
5. informazioni, API, fonti, metriche o funzionalita' non verificate;
6. comunicazione laterale implicita tra nodi dell'albero;
7. autorizzazione implicita a cambiare identita', identificativi, relazioni dati, invarianti o contratti condivisi.

## Regola Mentale Minima

Una sintesi onesta del sistema e' questa:

"Non compensare in silenzio cio' che non e' chiaro, non cambiare implicitamente il layer superiore, non inventare cio' che non e' verificato e non propagare qualcosa che non sai spiegare o validare."

"Non trasformare un cambio di identita', relazione o contratto condiviso in una normale modifica locale."

## Quando Il Sistema E' Applicato Bene

Il sistema sta funzionando se, a fine run, un reviewer riesce a capire:

1. quale problema si stava risolvendo;
2. quali vincoli governavano il task;
3. quali decisioni sono state prese e perche';
4. come i rami di lavoro si collegano ai parent artifact;
5. dove sono emersi mismatch o rischi;
6. quali fatti erano verificati e quali assunzioni erano residue;
7. perche' il codice finale e' coerente con l'intent iniziale o con le revisioni approvate.

Inoltre deve poter capire senza inferenze implicite:

1. quando un ramo e' stato aperto;
2. quale parte del parent copriva;
3. quali checkpoint sono stati superati o falliti;
4. quando un problema e' rimasto locale e quando e' risalito;
5. quale stato hanno i nodi dell'artifact tree;
6. se un cambiamento architetturale e' stato mitigato, revisionato o bloccato.

## Limite Da Tenere Presente

Le rules da sole non sostituiscono sempre un buon contesto operativo.

Per task piccoli possono bastare.

Per task piu' grandi o piu' ambigui, spesso serve anche un brief locale che traduca il sistema sul caso specifico.
