---
title: refund — Rimborso ordine
type: note
tags:
  - ecommerce
  - datalayer
  - ga4
  - refund
related:
  - _MOC_Ecommerce
  - _Glossario
  - purchase
ga4_event: refund
categoria: ecommerce
piattaforme: [GA4]
data_creazione: 2026-05-29
last_updated: 2026-05-29
source_verified_on: 2026-05-29
fonti:
  - https://developers.google.com/analytics/devguides/collection/ga4/reference/events#refund
status: stable
---

# refund — Rimborso ordine

Push eseguito quando un ordine o parte di esso viene rimborsato.
GA4 sottrae automaticamente il valore dal report Monetization.
Tipicamente inviato via Measurement Protocol server-side dal gestionale ordini.

> **Nota:** eseguire sempre `dataLayer.push({ ecommerce: null })` prima di questo push.

---

## Script — rimborso totale

```javascript
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({ ecommerce: null });

window.dataLayer.push({
  event: 'refund',
  ecommerce: {
    transaction_id: 'ORD-2026-00012345',
    currency:       'EUR',
    value:          119.80
    // items[] omesso = rimborso totale dell'ordine
  }
});
```

## Script — rimborso parziale

```javascript
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({ ecommerce: null });

window.dataLayer.push({
  event: 'refund',
  ecommerce: {
    transaction_id: 'ORD-2026-00012345',
    currency:       'EUR',
    value:          14.90,              // valore degli item rimborsati
    items: [
      {
        item_id:  'SKU_002',
        item_name:'Calzini sport',
        price:    14.90,
        quantity: 1                     // quantità rimborsata (non totale ordine)
      }
    ]
  }
});
```

---

## Parametri

| Parametro | Descrizione | Tipo | Obbligatorio | Esempio |
|-----------|-------------|------|:------------:|---------|
| `transaction_id` | ID ordine originale | stringa | ✅ | `"ORD-2026-00012345"` |
| `currency` | Valuta (ISO 4217 uppercase) | stringa | ✅ | `"EUR"` |
| `value` | Importo rimborsato | numero | ✅ | `14.90` |
| `items[]` | Prodotti rimborsati (solo rimborso parziale) | array | ⬜ | vedi sopra |

---

## Piattaforme

| Piattaforma | Note |
|-------------|------|
| GA4 | Sottrae `value` dalla revenue nei report Monetization |
| Google Ads | Non supporta refund event direttamente — gestire via Conversion Adjustments API |
| Meta / TikTok | Non hanno un evento refund standard — gestire lato CRM |

---

## Note GDPR

- Nessun campo PII
- Richiede `analytics_storage: granted`
- Consigliato inviare via Measurement Protocol server-side per garantire la ricezione (il cliente potrebbe non tornare sul sito)

---

## Riferimenti

- GA4 refund event: https://developers.google.com/analytics/devguides/collection/ga4/reference/events#refund
