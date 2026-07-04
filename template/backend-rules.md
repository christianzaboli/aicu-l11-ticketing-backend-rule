# Backend Rules - L11

## Valori Validi

### Priority

-

### Source Channel

-

## Mapping

| Priority | Source Channel | Urgency Label |
| --- | --- | --- |
| alta | telefono | intervento rapido |
| alta | email | prioritario |
| normale | chat | standard |
| bassa | qualunque | monitorare |

## Dati Decisi Dal Server

- `urgencyLabel`:
- `createdByOperatorId`:
- eventuali default:

## Dati Inviati Dal Client

- `title`:
- `description`:
- `priority`:
- `sourceChannel`:

## Fuori Scope

-

## Regola In Forma Di Funzione

```txt
computeUrgencyLabel(priority, sourceChannel) -> urgencyLabel
```

Non duplicare questa regola nel client.
