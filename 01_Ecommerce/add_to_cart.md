---
title: add_to_cart — Aggiunta al carrello
type: note
tags:
  - ecommerce
  - datalayer
  - ga4
  - add_to_cart
related:
  - _MOC_Ecommerce
  - _Glossario
  - view_item
  - remove_from_cart
  - view_cart
ga4_event: add_to_cart
categoria: ecommerce
piattaforme: [GA4, Google Ads, Meta CAPI, TikTok]
data_creazione: 2026-05-29
last_updated: 2026-05-29
source_verified_on: 2026-05-29
fonti:
  - https://developers.google.com/analytics/devguides/collection/ga4/reference/events#add_to_cart
status: stable
---

# add_to_cart — Aggiunta al carrello

Push eseguito quando l'utente aggiunge uno o più prodotti al carrello, da qualsiasi contesto:
PDP, pagina categoria (quick add), quickview, prodotti correlati, pagina carrello (modifica quantità).

> **Nota:** eseguire sempre `dataLayer.push({ ecommerce: null })` prima di questo push.

---

## Script

```javascript
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({ ecommerce: null }); // reset obbligatorio

window.dataLayer.push({
  event: 'add_to_cart',
  ecommerce: {
    currency: 'EUR',
    value:    89.90,  // prezzo unitario × quantità aggiunta
    items: [
      {
        item_id:        'SKU_001',
        item_name:      'Sneakers running',
        item_brand:     'Acme',
        item_category:  'Calzature',
        item_category2: 'Sport',
        item_variant:   'Nero / 42',
        price:          89.90,
        quantity:       1   // quantità aggiunta in questa sessione, non totale carrello
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
| `value` | Prezzo unitario × quantità aggiunta | numero | ✅ | `89.90` |
| `items[]` | Array prodotti aggiunti | array | ✅ | vedi sotto |

## Parametri — items[]

| Parametro | Descrizione | Tipo | Obbligatorio | Esempio |
|-----------|-------------|------|:------------:|---------|
| `item_id` | SKU univoco | stringa | ✅ | `"SKU_001"` |
| `item_name` | Nome prodotto | stringa | ✅ | `"Sneakers running"` |
| `item_brand` | Brand | stringa | ⬜ | `"Acme"` |
| `item_category` | Categoria L1 | stringa | ⬜ | `"Calzature"` |
| `item_variant` | Variante selezionata | stringa | ⬜ | `"Nero / 42"` |
| `price` | Prezzo unitario | numero | ✅ | `89.90` |
| `quantity` | Quantità aggiunta (non totale carrello) | numero | ✅ | `1` |

---

## Piattaforme

| Piattaforma | Tag GTM | Trigger | Note |
|-------------|---------|---------|------|
| GA4 | GA4 Event — add_to_cart | Custom Event: `add_to_cart` | Metrica Add to carts nel funnel |
| Google Ads | Dynamic Remarketing | Custom Event: `add_to_cart` | Audience "Abandoned cart" |
| Meta Pixel / CAPI | Meta AddToCart | Custom Event: `add_to_cart` | `value` + `currency` obbligatori |
| TikTok Pixel | TikTok AddToCart | Custom Event: `add_to_cart` | |

---

## Note GDPR

- Nessun campo PII
- Richiede `analytics_storage: granted` per GA4
- Richiede `ad_storage: granted` per remarketing

---

## Errori Comuni

| Errore | Conseguenza | Fix |
|--------|-------------|-----|
| `quantity` = quantità totale nel carrello invece di quella aggiunta | `add_to_cart` conta più unità del reale | Passare solo la quantità dell'aggiunta corrente |
| `value` = totale carrello invece di prezzo×quantità aggiunta | Revenue di add_to_cart gonfiata | `value` = `price * quantity` per questo push |
| Push mancante nel contesto quickview o categoria | Dati add_to_cart parziali | Verificare tutti i punti di ingresso al carrello nel sito |
| `item_variant` omesso | Impossibile analizzare add_to_cart per variante | Valorizzare con variante selezionata al momento dell'aggiunta |

---

## Riferimenti

- GA4 add_to_cart: https://developers.google.com/analytics/devguides/collection/ga4/reference/events#add_to_cart
