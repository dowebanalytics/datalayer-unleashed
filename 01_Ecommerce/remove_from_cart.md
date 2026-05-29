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
  - add_to_cart
  - view_cart
ga4_event: remove_from_cart
categoria: ecommerce
piattaforme: [GA4]
data_creazione: 2026-05-29
last_updated: 2026-05-29
source_verified_on: 2026-05-29
fonti:
  - https://developers.google.com/analytics/devguides/collection/ga4/reference/events#remove_from_cart
status: stable
---

# remove_from_cart — Rimozione dal carrello

Push eseguito quando l'utente rimuove un prodotto dal carrello (click su "Rimuovi" o azzeramento
quantità). Se l'utente riduce la quantità (es. da 3 a 1), il push deve riportare la quantità
rimossa (2), non la quantità residua.

> **Nota:** eseguire sempre `dataLayer.push({ ecommerce: null })` prima di questo push.

---

## Script

```javascript
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({ ecommerce: null }); // reset obbligatorio

window.dataLayer.push({
  event: 'remove_from_cart',
  ecommerce: {
    currency: 'EUR',
    value:    89.90,  // prezzo unitario × quantità rimossa
    items: [
      {
        item_id:       'SKU_001',
        item_name:     'Sneakers running',
        item_brand:    'Acme',
        item_category: 'Calzature',
        item_variant:  'Nero / 42',
        price:         89.90,
        quantity:      1   // quantità rimossa (non quella residua nel carrello)
      }
    ]
  }
});
```

---

## Parametri — evento

| Parametro | Descrizione | Tipo | Obbligatorio | Esempio |
|-----------|-------------|------|:------------:|---------|
| `currency` | Valuta (ISO 4217 uppercase) | stringa | ✅ | `"EUR"` |
| `value` | Prezzo unitario × quantità rimossa | numero | ✅ | `89.90` |
| `items[]` | Array prodotti rimossi | array | ✅ | vedi sotto |

## Parametri — items[]

| Parametro | Descrizione | Tipo | Obbligatorio | Esempio |
|-----------|-------------|------|:------------:|---------|
| `item_id` | SKU univoco | stringa | ✅ | `"SKU_001"` |
| `item_name` | Nome prodotto | stringa | ✅ | `"Sneakers running"` |
| `item_brand` | Brand | stringa | ⬜ | `"Acme"` |
| `item_category` | Categoria L1 | stringa | ⬜ | `"Calzature"` |
| `item_variant` | Variante | stringa | ⬜ | `"Nero / 42"` |
| `price` | Prezzo unitario | numero | ✅ | `89.90` |
| `quantity` | Quantità rimossa | numero | ✅ | `1` |

---

## Piattaforme

| Piattaforma | Tag GTM | Trigger | Note |
|-------------|---------|---------|------|
| GA4 | GA4 Event — remove_from_cart | Custom Event: `remove_from_cart` | Analisi abbandono carrello |

---

## Note GDPR

- Nessun campo PII
- Richiede `analytics_storage: granted`

---

## Errori Comuni

| Errore | Conseguenza | Fix |
|--------|-------------|-----|
| `quantity` = quantità residua nel carrello invece di quella rimossa | Dati distorti | Calcolare la differenza prima/dopo la rimozione |
| Push non implementato per riduzione quantità (solo per rimozione totale) | Dati incompleti | Gestire sia il caso "Rimuovi" che il caso "quantità → 0" |

---

## Riferimenti

- GA4 remove_from_cart: https://developers.google.com/analytics/devguides/collection/ga4/reference/events#remove_from_cart
