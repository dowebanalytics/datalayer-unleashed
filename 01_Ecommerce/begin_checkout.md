---
title: begin_checkout — Inizio checkout
type: note
tags:
  - ecommerce
  - datalayer
  - ga4
  - begin_checkout
  - checkout
related:
  - _MOC_Ecommerce
  - _Glossario
  - view_cart
  - add_shipping_info
  - add_payment_info
  - purchase
ga4_event: begin_checkout
categoria: ecommerce
piattaforme: [GA4, Meta CAPI, TikTok]
data_creazione: 2026-05-29
last_updated: 2026-05-29
source_verified_on: 2026-05-29
fonti:
  - https://developers.google.com/analytics/devguides/collection/ga4/reference/events#begin_checkout
status: stable
---

# begin_checkout — Inizio checkout

Push eseguito quando l'utente avvia il processo di checkout: click su "Procedi all'ordine"
dalla pagina carrello, o apertura della prima pagina/step del checkout.
Deve includere tutti i prodotti presenti nel carrello al momento dell'avvio.

> **Nota:** eseguire sempre `dataLayer.push({ ecommerce: null })` prima di questo push.

---

## Script

```javascript
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({ ecommerce: null }); // reset obbligatorio

window.dataLayer.push({
  event: 'begin_checkout',
  ecommerce: {
    currency: 'EUR',
    value:    104.80,       // totale prodotti (escluso tax e shipping)
    coupon:   'WELCOME10',  // coupon applicato al carrello (omettere se assente)
    items: [
      {
        item_id:       'SKU_001',
        item_name:     'Sneakers running',
        item_brand:    'Acme',
        item_category: 'Calzature',
        item_variant:  'Nero / 42',
        price:         89.90,
        quantity:      1,
        coupon:        'WELCOME10',  // coupon a livello item (omettere se assente)
        discount:      9.00
      },
      {
        item_id:       'SKU_002',
        item_name:     'Calzini sport',
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
| `coupon` | Coupon a livello ordine | stringa | ⬜ | `"WELCOME10"` |
| `items[]` | Tutti i prodotti nel carrello | array | ✅ | vedi sotto |

## Parametri — items[]

| Parametro | Descrizione | Tipo | Obbligatorio | Esempio |
|-----------|-------------|------|:------------:|---------|
| `item_id` | SKU univoco | stringa | ✅ | `"SKU_001"` |
| `item_name` | Nome prodotto | stringa | ✅ | `"Sneakers running"` |
| `item_brand` | Brand | stringa | ⬜ | `"Acme"` |
| `item_category` | Categoria L1 | stringa | ⬜ | `"Calzature"` |
| `item_variant` | Variante | stringa | ⬜ | `"Nero / 42"` |
| `price` | Prezzo unitario (post-sconto) | numero | ✅ | `89.90` |
| `quantity` | Quantità | numero | ✅ | `1` |
| `coupon` | Coupon a livello item | stringa | ⬜ | `"WELCOME10"` |
| `discount` | Valore sconto applicato all'item | numero | ⬜ | `9.00` |

---

## Piattaforme

| Piattaforma | Tag GTM | Trigger | Note |
|-------------|---------|---------|------|
| GA4 | GA4 Event — begin_checkout | Custom Event: `begin_checkout` | Step 1 funnel checkout |
| Meta Pixel / CAPI | Meta InitiateCheckout | Custom Event: `begin_checkout` | |
| TikTok Pixel | TikTok InitiateCheckout | Custom Event: `begin_checkout` | |

---

## Note GDPR

- Nessun campo PII
- Richiede `analytics_storage: granted` per GA4
- Richiede `ad_storage: granted` per Meta e TikTok

---

## Errori Comuni

| Errore | Conseguenza | Fix |
|--------|-------------|-----|
| Push eseguito al pageload della pagina checkout invece che al click | `begin_checkout` doppio su reload | Triggerare su click "Procedi" o navigazione verso il primo step, non su pageview |
| `items[]` non aggiornato rispetto all'ultimo stato del carrello | Dati checkout disallineati dal carrello | Leggere il carrello aggiornato dal backend prima del push |

---

## Riferimenti

- GA4 begin_checkout: https://developers.google.com/analytics/devguides/collection/ga4/reference/events#begin_checkout
