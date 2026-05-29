---
title: add_shipping_info — Selezione metodo di spedizione
type: note
tags:
  - ecommerce
  - datalayer
  - ga4
  - add_shipping_info
  - checkout
related:
  - _MOC_Ecommerce
  - _Glossario
  - begin_checkout
  - add_payment_info
ga4_event: add_shipping_info
categoria: ecommerce
piattaforme: [GA4]
data_creazione: 2026-05-29
last_updated: 2026-05-29
source_verified_on: 2026-05-29
fonti:
  - https://developers.google.com/analytics/devguides/collection/ga4/reference/events#add_shipping_info
status: stable
---

# add_shipping_info — Selezione metodo di spedizione

Push eseguito quando l'utente seleziona o conferma il metodo di spedizione durante il checkout.
Corrisponde al completamento dello step spedizione nel funnel.

> **Nota:** eseguire sempre `dataLayer.push({ ecommerce: null })` prima di questo push.

---

## Script

```javascript
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({ ecommerce: null }); // reset obbligatorio

window.dataLayer.push({
  event: 'add_shipping_info',
  ecommerce: {
    currency:      'EUR',
    value:         104.80,      // totale prodotti (escluso tax e shipping)
    shipping_tier: 'standard',  // metodo scelto: standard | express | pickup | free
    coupon:        'WELCOME10', // omettere se assente
    items: [
      {
        item_id:       'SKU_001',
        item_name:     'Sneakers running',
        item_category: 'Calzature',
        item_variant:  'Nero / 42',
        price:         89.90,
        quantity:      1
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
| `value` | Totale prodotti | numero | ✅ | `104.80` |
| `shipping_tier` | Metodo di spedizione selezionato | stringa | ✅ | `"standard"` |
| `coupon` | Coupon a livello ordine | stringa | ⬜ | `"WELCOME10"` |
| `items[]` | Prodotti nel carrello | array | ✅ | vedi sotto |

## Parametri — items[]

| Parametro | Descrizione | Tipo | Obbligatorio | Esempio |
|-----------|-------------|------|:------------:|---------|
| `item_id` | SKU univoco | stringa | ✅ | `"SKU_001"` |
| `item_name` | Nome prodotto | stringa | ✅ | `"Sneakers running"` |
| `item_category` | Categoria L1 | stringa | ⬜ | `"Calzature"` |
| `item_variant` | Variante | stringa | ⬜ | `"Nero / 42"` |
| `price` | Prezzo unitario | numero | ✅ | `89.90` |
| `quantity` | Quantità | numero | ✅ | `1` |

---

## Piattaforme

| Piattaforma | Tag GTM | Trigger | Note |
|-------------|---------|---------|------|
| GA4 | GA4 Event — add_shipping_info | Custom Event: `add_shipping_info` | Step 2 funnel checkout |

---

## Note GDPR

- Nessun campo PII
- Richiede `analytics_storage: granted`

---

## Errori Comuni

| Errore | Conseguenza | Fix |
|--------|-------------|-----|
| `shipping_tier` con valori inconsistenti (`"Standard"`, `"standard"`, `"STANDARD"`) | Frammentazione nei report GA4 | Definire vocabolario fisso lowercase e documentarlo |
| Push eseguito al caricamento dello step invece che alla conferma | Dati duplicati su reload | Triggerare su click "Continua" o cambio step nel checkout |

---

## Riferimenti

- GA4 add_shipping_info: https://developers.google.com/analytics/devguides/collection/ga4/reference/events#add_shipping_info
