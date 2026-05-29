---
title: view_cart — Visualizzazione carrello
type: note
tags:
  - ecommerce
  - datalayer
  - ga4
  - view_cart
related:
  - _MOC_Ecommerce
  - _Glossario
  - add_to_cart
  - begin_checkout
ga4_event: view_cart
categoria: ecommerce
piattaforme: [GA4]
data_creazione: 2026-05-29
last_updated: 2026-05-29
source_verified_on: 2026-05-29
fonti:
  - https://developers.google.com/analytics/devguides/collection/ga4/reference/events#view_cart
status: stable
---

# view_cart — Visualizzazione carrello

Push eseguito quando l'utente apre la pagina carrello o un drawer/mini-cart laterale.
Deve includere **tutti i prodotti presenti nel carrello** al momento della visualizzazione,
non solo quelli aggiunti nell'ultima sessione.

> **Nota:** eseguire sempre `dataLayer.push({ ecommerce: null })` prima di questo push.

---

## Script

```javascript
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({ ecommerce: null }); // reset obbligatorio

window.dataLayer.push({
  event: 'view_cart',
  ecommerce: {
    currency: 'EUR',
    value:    104.80,  // valore totale dei prodotti nel carrello (escluso tax e shipping)
    items: [
      {
        item_id:       'SKU_001',
        item_name:     'Sneakers running',
        item_brand:    'Acme',
        item_category: 'Calzature',
        item_variant:  'Nero / 42',
        price:         89.90,
        quantity:      1
      },
      {
        item_id:       'SKU_002',
        item_name:     'Calzini sport',
        item_brand:    'Acme',
        item_category: 'Abbigliamento',
        price:         14.90,
        quantity:      1
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
| `value` | Totale prodotti nel carrello | numero | ✅ | `104.80` |
| `items[]` | Tutti i prodotti nel carrello | array | ✅ | vedi sotto |

## Parametri — items[]

| Parametro | Descrizione | Tipo | Obbligatorio | Esempio |
|-----------|-------------|------|:------------:|---------|
| `item_id` | SKU univoco | stringa | ✅ | `"SKU_001"` |
| `item_name` | Nome prodotto | stringa | ✅ | `"Sneakers running"` |
| `item_brand` | Brand | stringa | ⬜ | `"Acme"` |
| `item_category` | Categoria L1 | stringa | ⬜ | `"Calzature"` |
| `item_variant` | Variante | stringa | ⬜ | `"Nero / 42"` |
| `price` | Prezzo unitario | numero | ✅ | `89.90` |
| `quantity` | Quantità nel carrello | numero | ✅ | `1` |

---

## Piattaforme

| Piattaforma | Tag GTM | Trigger | Note |
|-------------|---------|---------|------|
| GA4 | GA4 Event — view_cart | Custom Event: `view_cart` | Abilita analisi abbandono carrello |

---

## Note GDPR

- Nessun campo PII
- Richiede `analytics_storage: granted`

---

## Errori Comuni

| Errore | Conseguenza | Fix |
|--------|-------------|-----|
| `items[]` con solo ultimo prodotto aggiunto | Snapshot carrello incompleto | Includere tutti i prodotti presenti nel carrello |
| `value` non allineato alla somma degli item | Dati incoerenti | `value` = somma di `price × quantity` per ogni item |
| Push non implementato per drawer/mini-cart | Dati view_cart parziali | Implementare su tutti i punti di accesso al carrello |

---

## Riferimenti

- GA4 view_cart: https://developers.google.com/analytics/devguides/collection/ga4/reference/events#view_cart
