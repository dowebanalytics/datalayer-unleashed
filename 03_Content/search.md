---
title: search — Ricerca interna
type: note
tags:
  - content
  - search
  - datalayer
  - ga4
related:
  - _Glossario
ga4_event: search
categoria: content
piattaforme: [GA4]
data_creazione: 2026-05-29
last_updated: 2026-05-29
source_verified_on: 2026-05-29
fonti:
  - https://developers.google.com/analytics/devguides/collection/ga4/reference/events#search
status: stable
---

# search — Ricerca interna

Push eseguito quando l'utente esegue una ricerca interna al sito e vengono mostrati i risultati.

---

## Script

```javascript
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  event:          'search',
  search_term:    'sneakers nere',   // query inserita dall'utente
  search_results: 42                 // numero risultati (opzionale, custom param)
});
```

---

## Parametri

| Parametro | Descrizione | Tipo | Obbligatorio | Esempio |
|-----------|-------------|------|:------------:|---------|
| `search_term` | Query di ricerca | stringa | ✅ | `"sneakers nere"` |
| `search_results` | Numero risultati trovati | numero | ⬜ | `42` |

---

## Note GDPR

- Nessun campo PII
- Richiede `analytics_storage: granted`

---

## Riferimenti

- GA4 search event: https://developers.google.com/analytics/devguides/collection/ga4/reference/events#search
