# C.O.D.E. Loop - Artifact Schema Rule

## Metadata

- Rule ID: CL-RULE-70
- Layer: Cross-layer schema
- Status: Active
- Applies To: All artifacts produced under C.O.D.E. Loop
- Version: 3.0

## Purpose

Definire la struttura minima comune che rende gli artifact leggibili, verificabili e propagabili tra layer anche quando il lavoro viene scomposto in rami parent-child.

In V3 lo schema distingue esplicitamente:

1. Artifact Tree Overview, cioe' la vista globale di tracking;
2. Artifact Detail File, cioe' il documento operativo che contiene la logica del singolo artifact.

## Scope

Questa rule si applica a Concept Artifact, Orchestration Artifact, Design Artifact, Execution Artifact, Validation Report, richieste di escalation e ogni artifact operativo prodotto sotto C.O.D.E. Loop.

## Allowed Inputs

1. output dei layer governati dalle rispettive rules;
2. metadata di versione e stato;
3. riferimenti espliciti a input upstream;
4. evidenze, mismatch e condizioni residue;
5. Artifact Tree Overview corrente;
6. relazioni parent-child approvate o proposte;
7. fatti, deduzioni, ipotesi e assunzioni dichiarate.

## Required Outputs

Ogni artifact deve dichiarare almeno:

1. Artifact ID;
2. Name;
3. Layer;
4. Status;
5. Version;
6. Source Inputs;
7. Validation State;
8. Open Issues;
9. Last Updated Context;
10. Parent Artifact ID, salvo root artifact senza parent;
11. Parent Layer, salvo root artifact senza parent;
12. Branch ID, quando rilevante;
13. Parent Scope Covered, quando rilevante;
14. Propagation Scope Status;
15. Sibling Dependencies, se presenti;
16. Rationale;
17. Inputs;
18. Outputs;
19. Constraints;
20. Acceptance Criteria;
21. Children, se presenti o previsti;
22. Facts, Deductions and Hypotheses, quando l'incertezza e' rilevante.

Convenzione minima raccomandata:

1. per root artifact senza parent usare valori espliciti come `Parent Artifact ID: N/A`, `Parent Layer: N/A`, `Branch ID: root`, `Parent Scope Covered: full scope`, `Propagation Scope Status: root`;
2. per child artifact attivi usare parent reale, branch ID stabile, scope coperto dichiarato e `Propagation Scope Status: active-child` o equivalente chiaro;
3. gli stati `deferred`, `not yet decomposed` e `out of scope` vanno resi leggibili soprattutto nella copertura del parent, non usati per lasciare ambiguo lo stato del child artifact;
4. ogni child artifact deve avere un solo parent diretto;
5. ogni informazione operativa deve vivere nel detail file, non solo nella overview o nella conversazione.

Ogni layer deve inoltre includere almeno il contenuto minimo seguente:

1. Concept: obiettivi, vincoli, assunzioni, criteri di successo, out of scope, known unknowns;
2. Orchestration: decomposizione, dipendenze, sequencing, rischi, copertura, child artifact candidates;
3. Design: contratti, modelli, edge cases, strategia di validazione, assunzioni tecniche;
4. Execution: evidenza implementativa, test, mismatch, deviazioni, stato del ramo;
5. Validation: criteri controllati, esito, condizioni residue, decisione di propagazione;
6. Escalation: tipo richiesta, evidenza, decisione richiesta, propagation status.

## Artifact Tree Overview

L'Artifact Tree Overview e' una vista globale di tracking.

Serve esclusivamente a:

1. visualizzare la gerarchia degli artifact;
2. monitorare stato e avanzamento;
3. navigare tra parent e child;
4. mostrare blocchi, nodi deferred e nodi pronti per validazione.

Non deve contenere logica operativa, razionale completo, contratti, decisioni implementative o criteri di accettazione dettagliati.

Formato minimo tabellare:

```text
ID       Name                      Parent   Layer           Status
A1       System Root               N/A      Concept         ACTIVE
A1.1     Component Design          A1       Orchestration   COMPLETED
A1.2     Architecture Definition   A1       Orchestration   READY_FOR_VALIDATION
A1.2.1   Contract Model            A1.2     Design          IN_PROGRESS
```

Formato minimo ad albero:

```text
A1 System Root [ACTIVE]
  A1.1 Component Design [COMPLETED]
  A1.2 Architecture Definition [READY_FOR_VALIDATION]
    A1.2.1 Contract Model [IN_PROGRESS]
```

La forma esatta puo' variare, ma deve restare human-readable e sufficiente per navigare il lavoro.

## Artifact Detail File

Ogni artifact operativo deve avere un dettaglio leggibile.

Schema standard raccomandato:

```yaml
id: A1.3.2
name: Execution Layer
layer: Execution
parent: A1.3
parent_layer: Design
branch_id: A1.3.execution
status: IN_PROGRESS
version: 1
source_inputs:
  - A1.3
validation_state: NOT_VALIDATED
last_updated_context: Short description of the current update.
parent_scope_covered: Defines the exact parent scope covered by this artifact.
propagation_scope_status: active-child
sibling_dependencies:
  - A1.3.1
description: >
  Describes responsibilities and behavior of the artifact.
rationale: >
  Explains why this artifact exists and why its boundaries are defined this way.
inputs:
  - upstream artifacts
  - structural definitions
outputs:
  - derived implementation artifacts
constraints:
  - Must not define strategic intent
  - Must follow parent artifact constraints
acceptance_criteria:
  - responsibilities clearly defined
  - outputs well specified
  - boundaries respected
facts_deductions_hypotheses:
  facts:
    - Verified information.
  deductions:
    - Reasonable inference from verified information.
  hypotheses:
    - Assumption that still needs confirmation.
open_issues:
  - Issue or none.
children:
  - A1.3.2.1
```

Lo schema puo' essere espresso in Markdown, YAML-like text o tabella, purche' i campi siano leggibili e stabili.

## Artifact Rules

### Identity Rule

Ogni artifact deve avere:

1. ID univoco;
2. parent esplicito o valore root;
3. stato definito;
4. versione leggibile;
5. layer dichiarato.

### Lineage Rule

Ogni artifact:

1. puo' generare uno o piu' figli;
2. eredita vincoli dal padre;
3. non puo' modificare intenzioni superiori, solo specializzarle;
4. deve dichiarare quale scope del parent copre.

### Isolation Rule

Ogni artifact e' autonomo:

1. contiene tutto il contesto necessario per la propria funzione;
2. non dipende da conoscenza implicita esterna;
3. puo' essere validato senza recuperare razionale dalla conversazione.

### Propagation Rule

La conoscenza fluisce attraverso:

```text
Parent Artifact -> Child Artifact
```

Non sono ammessi canali laterali impliciti tra nodi.

Le dipendenze tra sibling sono ammesse solo se dichiarate come sibling dependencies.

## Status Model

Gli stati possono essere adattati al progetto, ma devono restare leggibili.

Stati raccomandati:

1. `DRAFT`;
2. `ACTIVE`;
3. `IN_PROGRESS`;
4. `READY_FOR_VALIDATION`;
5. `PASS_WITH_CONDITIONS`;
6. `COMPLETED`;
7. `BLOCKED`;
8. `DEFERRED`;
9. `REJECTED`;
10. `SUPERSEDED`.

Lo stato di un nodo nell'overview deve corrispondere allo stato operativo dichiarato nel detail file o a una sintesi esplicitamente derivata da esso.

## Mandatory Behaviors

1. mantenere uno schema stabile tra artifact dello stesso tipo;
2. dichiarare sempre lo stato dell'artifact;
3. collegare ogni artifact ai suoi input upstream;
4. usare parent metadata espliciti per ogni child artifact e valori `N/A` o equivalenti solo per root artifact senza parent;
5. usare un solo parent diretto per ogni child artifact;
6. rendere espliciti problemi aperti, condizioni residue e stato di copertura del ramo;
7. evitare artifact che dipendono dalla sola memoria conversazionale;
8. tenere separata la vista di tracking dalla logica operativa;
9. aggiornare tree overview e detail file in modo coerente;
10. dichiarare facts, deductions e hypotheses quando influenzano decisioni o validazione.

## Forbidden Behaviors

1. produrre artifact senza identificativo o versione;
2. omettere gli input upstream che giustificano il contenuto;
3. nascondere condizioni aperte dentro testo non strutturato;
4. trattare un artifact ambiguo come se fosse pronto al downstream;
5. produrre child artifact senza parent diretto, scope coperto o propagation scope status leggibili;
6. collegare implicitamente un child artifact a piu' parent diretti;
7. usare l'Artifact Tree Overview come sostituto del detail file;
8. conservare decisioni operative solo in note conversazionali;
9. creare livelli concettuali intermedi non rappresentati da artifact quando contengono lavoro operativo;
10. lasciare che sibling comunichino tramite assunzioni non dichiarate.

## Validation Requirements

Uno schema artifact e' valido solo se:

1. contiene metadata minimi leggibili;
2. rende possibile il confronto con la versione precedente;
3. permette al downstream di capire cosa consumare e con quale stato;
4. rende leggibile il legame tra child artifact, parent diretto e ramo corrente;
5. rende leggibile se l'artifact e' root oppure child e con quale convenzione e' dichiarato;
6. rispetta il minimo di contenuto richiesto dal layer di appartenenza;
7. e' coerente con l'Artifact Tree Overview;
8. non richiede conoscenza implicita per ricostruire lineage, stato o decisioni;
9. dichiara le assunzioni che influenzano propagazione o validazione.

## Escalation Triggers

1. manca lo schema minimo necessario per il downstream;
2. un artifact non e' abbastanza leggibile da essere validato;
3. i metadata non permettono di capire quale versione sia attiva;
4. il layer corrente non puo' completare lo schema senza chiarimenti upstream;
5. la mappa parent-child o la copertura del parent non sono piu' leggibili;
6. overview e detail file divergono su parent, stato o scope;
7. un sibling dependency non dichiarato diventa necessario per proseguire;
8. un dettaglio operativo esiste solo fuori dagli artifact.

## Rationale

Se gli artifact non hanno una forma minima stabile, il sistema perde tracciabilita' e la propagazione torna a dipendere dal contesto implicito.

Questa rule rende gli artifact consumabili sia da umani sia da agenti.

La V3 formalizza l'albero degli artifact come vista di tracking, ma mantiene la logica operativa dentro i detail file per evitare canali paralleli e ambigui.
