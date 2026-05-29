---
title: remove_from_cart — Rimozione dal carrello
type: note
tags:
  - ecommerce
  - datalayer
  - ga4
  - remove_from_cart
related:
  - _MOC_Ecommerce
  - _Glossario
ga4_event: remove_from_cart
categoria: ecommerce
piattaforme: [GA4, Google Ads, Meta CAPI, TikTok]
data_creazione: 2026-05-29
last_updated: 2026-05-29
source_verified_on: 2026-05-29
fonti:
  - https://developers.google.com/analytics/devguides/collection/ga4/reference/events#remove_from_cart
status: draft
---

# remove_from_cart — Rimozione dal carrello

Push quando l'utente rimuove un prodotto dal carrello o azzera la quantità.

> **Nota:** eseguire sempre `dataLayer.push({ ecommerce: null })` prima di questo push.
> Vedere [[_MOC_Ecommerce]] per le regole comuni a tutti gli eventi ecommerce.

---

## Script

```javascript
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({ ecommerce: null }); // reset obbligatorio

window.dataLayer.push({
  event: 'remove_from_cart',
  ecommerce: {
    // Parametri chiave: currency, value, items[]
  }
});
```

---

## Parametri

> 🔲 **Stub** — da completare nella prossima sessione di lavoro.

| Parametro | Descrizione | Tipo | Obbligatorio | Esempio |
|-----------|-------------|------|:------------:|---------|
| `currency` | Valuta ISO 4217 | stringa | ✅ | `"EUR"` |
| `value` | Valore totale | numero | ✅ | `89.90` |
| `items[]` | Array prodotti | array | ✅ | vedi sotto |
| `items[].item_id` | SKU prodotto | stringa | ✅ | `"SKU_001"` |
| `items[].item_name` | Nome prodotto | stringa | ✅ | `"Sneakers running"` |
| `items[].price` | Prezzo unitario | numero | ✅ | `89.90` |
| `items[].quantity` | Quantità | numero | ✅ | `1` |

---

## Piattaforme

| Piattaforma | Tag GTM | Trigger |
|-------------|---------|---------|
| GA4 | GA4 Event — remove_from_cart | Custom Event: `remove_from_cart` |
| Google Ads | Conversion Tracking | Custom Event: `remove_from_cart` |
| Meta Pixel / CAPI | Meta Pixel / CAPI tag | Custom Event: `remove_from_cart` |

---

## Note GDPR

- Richiede `analytics_storage: granted` per GA4
- Richiede `ad_storage: granted` per Google Ads e Meta
- Nessun campo PII diretto

---

## Riferimenti

- GA4 Event Reference: https://developers.google.com/analytics/devguides/collection/ga4/reference/events#remove_from_cart
