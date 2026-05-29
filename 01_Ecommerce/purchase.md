---
title: purchase — Ordine completato
type: note
tags:
  - ecommerce
  - datalayer
  - ga4
  - purchase
  - conversione
related:
  - _MOC_Ecommerce
  - _Glossario
  - begin_checkout
  - refund
ga4_event: purchase
categoria: ecommerce
piattaforme: [GA4, Google Ads, Meta CAPI, TikTok, Microsoft UET]
data_creazione: 2026-05-29
last_updated: 2026-05-29
source_verified_on: 2026-05-29
fonti:
  - https://developers.google.com/analytics/devguides/collection/ga4/reference/events#purchase
status: stable
---

# purchase — Ordine completato

Push eseguito sulla pagina di conferma ordine (thank you page) al completamento dell'acquisto.
È l'evento di conversione principale: GA4 lo marca automaticamente come Key Event.

> **Nota:** eseguire sempre `dataLayer.push({ ecommerce: null })` prima di questo push.

---

## Script

```javascript
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({ ecommerce: null }); // reset obbligatorio

window.dataLayer.push({
  event: 'purchase',
  ecommerce: {
    transaction_id: 'ORD-2026-00012345', // univoco per ogni ordine
    currency:       'EUR',               // ISO 4217 uppercase
    value:          119.80,              // totale ordine (incluso sconto, escluso tax e shipping)
    tax:            21.60,               // IVA
    shipping:       5.00,                // costo spedizione
    coupon:         'WELCOME10',         // coupon a livello ordine (omettere se assente)
    items: [
      {
        item_id:       'SKU_001',
        item_name:     'Sneakers running',
        item_brand:    'Acme',
        item_category: 'Calzature',
        item_category2:'Sport',
        item_variant:  'Nero / 42',
        price:         89.90,
        quantity:      1,
        coupon:        'WELCOME10',      // coupon a livello item (omettere se assente)
        discount:      9.00              // valore sconto applicato all'item
      },
      {
        item_id:   'SKU_002',
        item_name: 'Calzini sport',
        price:     14.90,
        quantity:  2
      }
    ]
  }
});
```

---

## Parametri — evento

| Parametro | Descrizione | Tipo | Obbligatorio | Esempio |
|-----------|-------------|------|:------------:|---------|
| `transaction_id` | ID ordine univoco. Usato da GA4 per deduplicare | stringa | ✅ | `"ORD-2026-00012345"` |
| `currency` | Valuta (ISO 4217 uppercase) | stringa | ✅ | `"EUR"` |
| `value` | Totale ordine (netto di sconti, senza tax/shipping) | numero | ✅ | `119.80` |
| `tax` | Importo IVA | numero | ⬜ | `21.60` |
| `shipping` | Costo spedizione | numero | ⬜ | `5.00` |
| `coupon` | Codice coupon a livello ordine | stringa | ⬜ | `"WELCOME10"` |
| `items[]` | Array prodotti acquistati | array | ✅ | vedi sotto |

## Parametri — items[]

| Parametro | Descrizione | Tipo | Obbligatorio | Esempio |
|-----------|-------------|------|:------------:|---------|
| `item_id` | SKU univoco | stringa | ✅ | `"SKU_001"` |
| `item_name` | Nome prodotto | stringa | ✅ | `"Sneakers running"` |
| `item_brand` | Brand | stringa | ⬜ | `"Acme"` |
| `item_category` | Categoria L1 | stringa | ⬜ | `"Calzature"` |
| `item_category2` | Categoria L2 | stringa | ⬜ | `"Sport"` |
| `item_variant` | Variante (taglia/colore) | stringa | ⬜ | `"Nero / 42"` |
| `price` | Prezzo unitario | numero | ✅ | `89.90` |
| `quantity` | Quantità | numero | ✅ | `1` |
| `coupon` | Coupon a livello item | stringa | ⬜ | `"WELCOME10"` |
| `discount` | Sconto applicato all'item | numero | ⬜ | `9.00` |

---

## Piattaforme

| Piattaforma | Tag GTM | Trigger | Note |
|-------------|---------|---------|------|
| GA4 | GA4 Event — purchase | Custom Event: `purchase` | Key Event automatico |
| Google Ads | Conversion Tracking | Custom Event: `purchase` | `value` → conversion value |
| Meta Pixel / CAPI | Meta Purchase | Custom Event: `purchase` | `value` + `currency` obbligatori |
| TikTok Pixel | TikTok CompletePayment | Custom Event: `purchase` | |
| Microsoft UET | UET Goal | Custom Event: `purchase` | |

---

## Note GDPR

- Richiede `analytics_storage: granted` per GA4
- Richiede `ad_storage: granted` per Google Ads e Meta
- In un setup sGTM, il `purchase` può essere inviato server-side post-pagamento per eliminare la perdita da ad blocker
- Se disponibile, aggiungere `user_data` nel push per alimentare Enhanced Conversions (verificare consenso `ad_user_data: granted`)

---

## Errori Comuni

| Errore | Conseguenza | Fix |
|--------|-------------|-----|
| `transaction_id` non univoco (generato lato client, duplicato al refresh) | Revenue duplicata in GA4 | Generare ID server-side, passarlo alla thank you page |
| `value` include tax e shipping | Revenue gonfiata | `value` = totale prodotti, `tax` e `shipping` separati |
| `currency` lowercase o mancante | Evento scartato da GA4 | Sempre `"EUR"` uppercase |
| `items[]` vuoto o assente | Report Monetization parziali | Sempre includere array completo |
| Push eseguito più volte per reload thank you page | Conversioni duplicate | Usare flag session o cookie post-purchase per prevenire re-push |
| Reset `ecommerce: null` omesso | Merge con dati del push precedente | Pushare `{ ecommerce: null }` prima di ogni evento ecommerce |

---

## Riferimenti

- GA4 purchase event: https://developers.google.com/analytics/devguides/collection/ga4/reference/events#purchase
- Ecommerce tracking guide: https://developers.google.com/analytics/devguides/collection/ga4/ecommerce
