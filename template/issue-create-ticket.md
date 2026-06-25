# Issue: Create ticket with validation

## Request

```txt
Serve creare ticket dal supporto.
```

## Fatti (Facts)

- Siamo in un applicazione SPA in React con JavaScript dedicata alla gestione di ticket
- L'applicazione contiene ticket e ne consente la creazione da parte di utenti generici
- NON hai ancora accesso all'applicazione: siamo in una fase precedente di analisi
- La struttura base del ticket (titolo e descrizione) è identica per tutti i ruoli
- I campi obbligatori di un ticket sono titolo e descrizione 

## Assunzioni (Assumptions)

- Un ticket creato dal supporto sarà contrassegnato da un'etichetta (come il ruolo dell'autore, ossia "Supporto") per distinguerlo da quello di un utente generico

## Domande Aperte (Questions)

- Un utente riconosciuto col ruolo di "Suppporto" avrà una sezione riservata per la creazione di ticket?
- Il campo "Autore" del ticket viene autocompilato dal sistema con il ruolo o l'operatore deve poterlo selezionare manualmente?
- Che forma ha il feedback di successo?
- Esistono limiti di lunghezza minima o massima per i campi titolo e descrizione?

## Decisione (Decision)

Per questo slice, "creare ticket" significa:

```txt
Permettere a un utente con ruolo Supporto di compilare e inviare il form di creazione ticket, salvandolo nel sistema con l'attributo del ruolo tracciato correttamente.
```

## Fuori Scope / Non-Obiettivi (Non-Goals)

- allegati
- menzioni
- gestione dell'accesso al form da parte di utenti con ruolo diverso da Supporto (autorizzazione/redirect)

## Criteri Di Accettazione (Acceptance Criteria)

1. Un utente identificato come "Supporto" può accedere al form di creazione, inserire i dati obbligatori (titolo e descrizione) ed effettuare l'invio
2. Il sistema convalida che i campi di testo non siano vuoti (nemmeno di soli spazi vuoti tramite trim)
3. Al salvataggio del ticket, il client invia la richiesta includendo il ruolo 'Supporto'. L'interfaccia mostra un feedback di successo e il nuovo ticket appare nella lista con l'etichetta autore 'Supporto'

## Piano Di Verifica Manuale (Manual Test Plan)

- Accedi come utente Supporto, compila i campi del ticket con testo valido e premi invio. 
    - Risultato atteso: Il ticket viene creato, l'interfaccia mostra il successo e il ticket salvato presenta il flag/ruolo "Supporto"
- Accedi come utente Supporto, inserisci solo spazi vuoti nei campi obbligatori e premi invio. 
    - Risultato atteso: Il form blocca l'invio, mostra un messaggio di errore testuale chiaramente visibile in corrispondenza dei campi non validi e non crea nessun ticket vuoto nel sistema
- Compila solo il titolo (lascia la descrizione con spazi vuoti)
    - Risultato atteso: Il form blocca l'invio e mostra un messaggio di errore testuale chiaramente visibile in corrispondenza del campo non valido

## Note Per L06

- [quale payload andra' chiarito]
- [quale errore andra' chiarito]
- [quale campo dati andra' deciso]
