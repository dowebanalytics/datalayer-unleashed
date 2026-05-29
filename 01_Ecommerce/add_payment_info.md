---
title: add_payment_info — Selezione metodo di pagamento
type: note
tags:
  - ecommerce
  - datalayer
  - ga4
  - add_payment_info
  - checkout
related:
  - _MOC_Ecommerce
  - _Glossario
  - add_shipping_info
  - purchase
ga4_event: add_payment_info
categoria: ecommerce
piattaforme: [GA4]
data_creazione: 2026-05-29
last_updated: 2026-05-29
source_verified_on: 2026-05-29
fonti:
  - https://developers.google.com/analytics/devguides/collection/ga4/reference/events#add_payment_info
status: stable
---

# add_payment_info — Selezione metodo di pagamento

Push eseguito quando l'utente seleziona o conferma il metodo di pagamento durante il checkout.
Corrisponde al completamento dello step pagamento nel funnel, subito prima del `purchase`.

> **Nota:** eseguire sempre `dataLayer.push({ ecommerce: null })` prima di questo push.

---

## Script

```javascript
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({ ecommerce: null }); // reset obbligatorio

window.dataLayer.push({
  event: 'add_payment_info',
  ecommerce: {
    currency:     'EUR',
    value:        104.80,       // totale prodotti (escluso tax e shipping)
    payment_type: 'credit_card', // metodo: credit_card | paypal | bank_transfer | klarna | cash_on_delivery
    coupon:       'WELCOME10',  // omettere se assente
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
| `payment_type` | Metodo di pagamento selezionato | stringa | ✅ | `"credit_card"` |
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
| GA4 | GA4 Event — add_payment_info | Custom Event: `add_payment_info` | Step 3 funnel checkout (ultimo prima di purchase) |

---

## Note GDPR

- Nessun campo PII — il metodo di pagamento non è dato sensibile
- Richiede `analytics_storage: granted`
- **Non includere** dati della carta, IBAN o credenziali: non sono necessari e violerebbero PCI-DSS e GDPR

---

## Errori Comuni

| Errore | Conseguenza | Fix |
|--------|-------------|-----|
| `payment_type` con nomi inconsistenti (`"Carta"`, `"credit_card"`, `"CC"`) | Frammentazione nei report | Definire vocabolario fisso lowercase e documentarlo |
| Push troppo anticipato (al caricamento dello step) | Dati duplicati | Triggerare su conferma metodo, non su visualizzazione dello step |

---

## Riferimenti

- GA4 add_payment_info: https://developers.google.com/analytics/devguides/collection/ga4/reference/events#add_payment_info
