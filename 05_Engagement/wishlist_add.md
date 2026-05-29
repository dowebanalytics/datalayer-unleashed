---
title: wishlist_add — Aggiunta a wishlist
type: note
tags:
  - engagement
  - wishlist
  - datalayer
  - ga4
related:
  - _Glossario
  - add_to_cart
ga4_event: null
categoria: engagement
piattaforme: [GA4, Meta CAPI]
data_creazione: 2026-05-29
last_updated: 2026-05-29
status: draft
---

# wishlist_add — Aggiunta a wishlist

> 🔲 **Stub** — da completare.

Evento custom pushato quando l'utente aggiunge un prodotto alla wishlist.

---

## Script

```javascript
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  event: 'wishlist_add',
  ecommerce: {
    currency: 'EUR',
    value:    89.90,
    items: [{
      item_id:   'SKU_001',
      item_name: 'Sneakers running',
      price:     89.90,
      quantity:  1
    }]
  }
});
```
