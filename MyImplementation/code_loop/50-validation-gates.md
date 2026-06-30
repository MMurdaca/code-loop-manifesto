# C.O.D.E. Loop - Validation Gates Rule

## Metadata

- Rule ID: CL-RULE-50
- Layer: Cross-layer validation
- Status: Active
- Applies To: All artifact validations and propagation decisions

## Purpose

Definire le regole minime con cui ogni artifact viene validato prima di propagarsi al layer successivo o di continuare sul ramo corrente.

Il gate valida lineage, truthfulness, coerenza dell'artifact tree, stato delle assunzioni, rispetto del principio di semplicita' sufficiente e architectural contract drift, impedendo che venga propagato come normale cambio locale.

## Scope

Questa rule si applica a Concept Gate, Orchestration Gate, Design Gate, Execution Gate, Branch Gate, Parent Gate e Layer Gate.

## Allowed Inputs

1. artifact in stato Ready for Validation;
2. criteria di gate del layer corrente;
3. artifact upstream rilevanti gia' validati;
4. eventuali condizioni residue aperte;
5. parent artifact e scope coperto, quando il gate valuta un ramo;
6. Artifact Tree Overview corrente;
7. evidenze di test, verifica, fonti o assunzioni dichiarate;
8. drift impact assessment e drift policy mode, quando rilevanti.

## Required Outputs

Un Validation Report che dichiari almeno:

1. artifact valutato;
2. gate applicato;
3. esito del gate;
4. criteri controllati;
5. condizioni residue o motivi di fail;
6. next action;
7. parent artifact e branch scope, quando rilevanti;
8. lineage and tree consistency result;
9. truthfulness and assumption check;
10. propagation decision;
11. status update richiesto sull'artifact tree;
12. architectural drift assessment, quando rilevante;
13. drift policy mode applicata e relativa decisione.

## Mandatory Behaviors

1. validare ogni artifact prima della propagazione significativa;
2. eseguire un checkpoint obbligatorio prima di ogni nuova tranche significativa di lavoro sul ramo attivo;
3. distinguere esplicitamente tra Branch Gate, Parent Gate e Layer Gate quando il lavoro e' decomposto in rami;
4. scegliere il gate piu' piccolo che copre correttamente il significato del cambiamento senza nasconderne l'impatto reale;
5. usare solo tre esiti principali: Pass, Pass with Conditions, Fail;
6. bloccare la propagazione su Fail;
7. usare Pass with Conditions solo se il downstream puo' lavorare senza reinterpretare il layer superiore o il parent diretto;
8. chiedere re-validation quando l'artifact cambia in modo sostanziale;
9. controllare che parent, child, scope coperto e stato siano coerenti tra detail file e tree overview;
10. verificare che fatti, deduzioni e ipotesi siano distinguibili quando influenzano il gate;
11. respingere output che dipendono da risultati, fonti o API inventate;
12. controllare che la complessita' introdotta sia giustificata dai requisiti;
13. controllare se il cambiamento altera identita', identificativi, relazioni dati, invarianti o contratti condivisi;
14. applicare `Review` come default se il drift impact e' reale e non esiste policy locale;
15. usare almeno Parent Gate quando il drift impatta un parent o sibling; usare Layer Gate quando il contratto e' condiviso nel layer;
16. marcare come Fail un artifact che implementa drift non dichiarato o non approvato.

## Forbidden Behaviors

1. propagare artifact senza stato di gate noto;
2. usare Pass with Conditions per coprire contraddizioni strutturali;
3. validare contro baseline non approvate;
4. trattare il self-check del produttore come sostituto del gate;
5. usare un Branch Gate quando il problema richiede chiaramente una rivalidazione del parent o del layer;
6. ignorare divergenze tra artifact tree e artifact detail file;
7. considerare validata un'assunzione critica solo perche' il downstream l'ha usata;
8. accettare evidence non riproducibile senza dichiararne il limite;
9. validare come Pass un cambio che altera contratti architetturali senza drift assessment;
10. usare Pass with Conditions per permettere Execution in modalita' `Review` o `Strict` prima della decisione richiesta.

## Validation Requirements

Un gate e' valido solo se il report rende espliciti:

1. la versione dell'artifact valutato;
2. il tipo di gate applicato;
3. i criteri controllati;
4. l'esito finale;
5. le condizioni residue o il motivo del blocco;
6. la decisione sulla propagazione;
7. il parent artifact e il branch scope, quando il gate non e' di layer intero;
8. la coerenza tra tree overview e detail file;
9. lo stato delle assunzioni critiche;
10. gli eventuali test o controlli non eseguiti;
11. architectural drift impact e drift policy mode, quando il cambiamento tocca contratti architetturali.

## Escalation Triggers

1. il gate non puo' essere eseguito per mancanza di artifact upstream validi;
2. due artifact validi risultano in conflitto;
3. le condizioni residue superano l'autorita' del gate corrente;
4. un checkpoint obbligatorio mostra che il ramo non puo' continuare sulla baseline valida attuale;
5. il validator rileva un mismatch che richiede revisione upstream;
6. lineage, parent scope o artifact status non sono ricostruibili;
7. un'informazione critica e' non verificata ma necessaria alla propagazione;
8. il gate rileva architectural contract drift non dichiarato dall'artifact valutato;
9. la drift policy mode richiesta non e' compatibile con l'esito proposto.

## Rationale

Senza gate espliciti il loop si riduce a una sequenza di documenti senza controllo reale.

Questa rule rende la propagazione un atto condizionato, non implicito.

Il gate corretto non e' sempre quello piu' piccolo possibile.

E' quello piu' piccolo che resta ancora semanticamente sufficiente a governare il cambiamento reale.
