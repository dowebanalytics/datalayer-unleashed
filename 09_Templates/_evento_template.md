---
title: NOME_EVENTO — Descrizione breve
type: note
tags:
  - CATEGORIA
  - datalayer
  - ga4
  - NOME_EVENTO
related:
  - _Glossario
ga4_event: NOME_EVENTO          # null se evento custom
categoria: CATEGORIA            # ecommerce | user | content | lead | engagement | init
piattaforme: [GA4]              # aggiungere: Google Ads, Meta CAPI, TikTok, Microsoft UET
data_creazione: YYYY-MM-DD
last_updated: YYYY-MM-DD
source_verified_on: YYYY-MM-DD
fonti:
  - https://developers.google.com/analytics/devguides/collection/ga4/reference/events#NOME_EVENTO
status: draft                   # draft | stable | review | deprecated
---

# NOME_EVENTO — Descrizione breve

Spiegazione in 1-2 righe: quando si esegue il push e perché.

> **Nota:** se evento ecommerce, aggiungere: eseguire sempre `dataLayer.push({ ecommerce: null })` prima di questo push.

---

## Script

```javascript
window.dataLayer = window.dataLayer || [];
// Se ecommerce: window.dataLayer.push({ ecommerce: null });

window.dataLayer.push({
  event: 'NOME_EVENTO',  // omettere se push senza evento
  // parametri...
});
```

---

## Parametri

| Parametro | Descrizione | Tipo | Obbligatorio | Esempio |
|-----------|-------------|------|:------------:|---------|
| `param1` | Descrizione | stringa | ✅ | `"valore"` |
| `param2` | Descrizione | numero | ⬜ | `99.90` |

---

## Piattaforme

| Piattaforma | Tag GTM | Trigger |
|-------------|---------|---------|
| GA4 | GA4 Event — NOME_EVENTO | Custom Event: `NOME_EVENTO` |

---

## Note GDPR

- Consenso richiesto: `analytics_storage` / `ad_storage` / `ad_user_data`
- PII coinvolti: nessuno / specificare

---

## Errori Comuni

| Errore | Conseguenza | Fix |
|--------|-------------|-----|
| ... | ... | ... |

---

## Riferimenti

- GA4 Event Reference: https://developers.google.com/analytics/devguides/collection/ga4/reference/events#NOME_EVENTO
