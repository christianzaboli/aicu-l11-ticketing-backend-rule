# Backend Rules - L11

## Valori Validi

### Priority

- `alta`
- `normale`
- `bassa`

### Source Channel

- `telefono`
- `email`
- `chat`

## Mapping

| Priority | Source Channel | Urgency Label |
| --- | --- | --- |
| alta | telefono | intervento rapido |
| alta | email | prioritario |
| normale | chat | standard |
| bassa | qualunque | monitorare |

## Dati Decisi Dal Server

- `urgencyLabel`: calcolato dal server via mapping priority + sourceChannel
- `createdByOperatorId`: estratto dalla sessione dell'operatore autenticato
- eventuali default: `status` = `"aperto"`

## Dati Inviati Dal Client

- `title` (string, obbligatorio)
- `description` (string, opzionale)
- `priority` (string, valori: alta, normale, bassa)
- `sourceChannel` (string, valori: telefono, email, chat)

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

## Regola In Forma Di Funzione

```txt
computeUrgencyLabel(priority, sourceChannel) -> urgencyLabel
```

Non duplicare questa regola nel client.
