---
title: add_to_wishlist — Aggiunta a wishlist
type: note
tags:
  - engagement
  - wishlist
  - datalayer
  - ga4
related:
  - _Glossario
  - add_to_cart
  - view_item
ga4_event: add_to_wishlist
categoria: engagement
piattaforme: [GA4, Meta CAPI, TikTok]
data_creazione: 2026-05-29
last_updated: 2026-05-29
source_verified_on: 2026-05-29
fonti:
  - https://developers.google.com/analytics/devguides/collection/ga4/reference/events
status: stable
---

# add_to_wishlist — Aggiunta a wishlist

Recommended event GA4 pushato quando l'utente aggiunge un prodotto alla wishlist
o lista dei desideri. Può avvenire dalla PDP, dalla pagina categoria o da qualsiasi contesto
che espone il pulsante wishlist.
Utile per costruire audience di interesse prodotto e analizzare l'intenzione d'acquisto.

---

## Script

```javascript
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({ ecommerce: null }); // reset obbligatorio (oggetto ecommerce presente)

window.dataLayer.push({
  event: 'add_to_wishlist',
  ecommerce: {
    currency: 'EUR',
    value:    89.90,  // prezzo unitario del prodotto aggiunto
    items: [
      {
        item_id:        'SKU_001',
        item_name:      'Sneakers running',
        item_brand:     'Acme',
        item_category:  'Calzature',
        item_category2: 'Sport',
        item_variant:   'Nero / 42',
        price:          89.90,
        quantity:       1
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
| `value` | Prezzo unitario del prodotto | numero | ✅ | `89.90` |
| `items[]` | Array con il singolo prodotto aggiunto | array | ✅ | vedi sotto |

## Parametri — items[]

| Parametro | Descrizione | Tipo | Obbligatorio | Esempio |
|-----------|-------------|------|:------------:|---------|
| `item_id` | SKU univoco | stringa | ✅ | `"SKU_001"` |
| `item_name` | Nome prodotto | stringa | ✅ | `"Sneakers running"` |
| `item_brand` | Brand | stringa | ⬜ | `"Acme"` |
| `item_category` | Categoria L1 | stringa | ⬜ | `"Calzature"` |
| `item_category2` | Categoria L2 | stringa | ⬜ | `"Sport"` |
| `item_variant` | Variante selezionata | stringa | ⬜ | `"Nero / 42"` |
| `price` | Prezzo unitario | numero | ✅ | `89.90` |
| `quantity` | Quantità (solitamente 1) | numero | ✅ | `1` |

---

## Piattaforme

| Piattaforma | Tag GTM | Trigger | Note |
|-------------|---------|---------|------|
| GA4 | GA4 Event — add_to_wishlist | Custom Event: `add_to_wishlist` | Audience "interessati ma non acquirenti" |
| Meta Pixel / CAPI | Meta AddToWishlist | Custom Event: `add_to_wishlist` | Standard event Meta, `value` + `currency` obbligatori |
| TikTok Pixel | TikTok AddToWishlist | Custom Event: `add_to_wishlist` | |

---

## Note GDPR

- Nessun campo PII
- Richiede `analytics_storage: granted` per GA4
- Richiede `ad_storage: granted` per Meta e TikTok (remarketing)

---

## Errori Comuni

| Errore | Conseguenza | Fix |
|--------|-------------|-----|
| Reset `ecommerce: null` omesso | Merge con dati di un evento ecommerce precedente | Push `{ ecommerce: null }` prima |
| `value` = 0 su prodotti in promozione | Valore audience degradato | Usare il prezzo effettivo, anche se scontato |
| Push non implementato sulla pagina wishlist (solo sulla PDP) | Dati parziali se l'utente aggiunge dalla lista | Implementare in tutti i punti di accesso al pulsante wishlist |

---

## Riferimenti

- GA4 Events Reference: https://developers.google.com/analytics/devguides/collection/ga4/reference/events
- Meta AddToWishlist: https://developers.facebook.com/docs/meta-pixel/reference#standard-events
