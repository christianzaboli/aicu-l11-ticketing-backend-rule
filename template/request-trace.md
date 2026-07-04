# Request Trace - L11

## Feature Studenti

```txt
priority + sourceChannel -> urgencyLabel
```

## Trace

| Step | Cosa entra | Cosa decide il server | Errore possibile | Evidenza attesa |
| --- | --- | --- | --- | --- |
| request | body JSON: title, description, priority, sourceChannel | - | 400 se malformato | body ricevuto |
| validation | title, priority, sourceChannel | campi obbligatori, enum priority (alta/normale/bassa), enum sourceChannel (telefono/email/chat) | 400 fieldErrors | errori restituiti al client |
| auth/session | token JWT / cookie sessione | estrae operatore autenticato | 401 se non autenticato | operatore estratto |
| rule | priority, sourceChannel | calcola urgencyLabel via mapping (già validati) | nessuno (già filtrato da validation) | urgencyLabel assegnata |
| Prisma | dati ticket completi (title, description, priority, sourceChannel, urgencyLabel, createdByOperatorId, status) | scrive record in DB | nessuno (rollback se fallisce) | ticket salvato su DB |
| response | ticket creato | - | - | 201 + JSON del ticket |

## Caso Valido

```txt
priority=alta
sourceChannel=telefono
expected urgencyLabel=intervento rapido
```

## Caso Invalido

```txt
field=priority
value=immediata
expected error=400 fieldErrors.priority
```

## File Candidati

| Area | File candidato | Perche' |
| --- | --- | --- |
| UI payload | form ticket | campi priority e sourceChannel |
| API route | route POST ticket | endpoint createTicket |
| validation | validatore ticket | validazione enum e obbligatorietà |
| rule | libreria mapping | computeUrgencyLabel() |
| Prisma/schema | schema.prisma | modello Ticket |
| lista/card | component lista ticket | visualizzazione urgencyLabel |

## Fuori Scope

- Implementazione
- Test automatici
- Timezone / SLA
- Dashboard / assegnazioni
- Autenticazione (già esistente)
- Notifiche (email / SMS al cliente)
- Allegati / upload file
- Audit log / storico modifiche
- Rate limiting
