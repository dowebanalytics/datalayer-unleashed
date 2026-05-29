---
title: view_item — Visualizzazione scheda prodotto (PDP)
type: note
tags:
  - ecommerce
  - datalayer
  - ga4
  - view_item
  - pdp
related:
  - _MOC_Ecommerce
  - _Glossario
  - select_item
  - add_to_cart
ga4_event: view_item
categoria: ecommerce
piattaforme: [GA4, Google Ads, Meta CAPI, TikTok]
data_creazione: 2026-05-29
last_updated: 2026-05-29
source_verified_on: 2026-05-29
fonti:
  - https://developers.google.com/analytics/devguides/collection/ga4/reference/events#view_item
status: stable
---

# view_item — Visualizzazione scheda prodotto (PDP)

Push eseguito quando l'utente apre la pagina prodotto (PDP — Product Detail Page).
Deve includere la variante selezionata di default (o quella selezionata dall'utente se la variante
cambia senza reload della pagina).

> **Nota:** eseguire sempre `dataLayer.push({ ecommerce: null })` prima di questo push.
> In caso di cambio variante via AJAX (senza reload), eseguire un nuovo push con `ecommerce: null` + `view_item` aggiornato.

---

## Script

```javascript
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({ ecommerce: null }); // reset obbligatorio

window.dataLayer.push({
  event: 'view_item',
  ecommerce: {
    currency: 'EUR',
    value:    89.90,  // prezzo della variante visualizzata
    items: [
      {
        item_id:        'SKU_001',
        item_name:      'Sneakers running',
        item_brand:     'Acme',
        item_category:  'Calzature',
        item_category2: 'Sport',
        item_variant:   'Nero / 42',   // variante selezionata (taglia, colore, ecc.)
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
| `value` | Prezzo prodotto (variante visualizzata) | numero | ✅ | `89.90` |
| `items[]` | Array con il singolo prodotto | array | ✅ | vedi sotto |

## Parametri — items[]

| Parametro | Descrizione | Tipo | Obbligatorio | Esempio |
|-----------|-------------|------|:------------:|---------|
| `item_id` | SKU univoco della variante | stringa | ✅ | `"SKU_001"` |
| `item_name` | Nome prodotto | stringa | ✅ | `"Sneakers running"` |
| `item_brand` | Brand | stringa | ⬜ | `"Acme"` |
| `item_category` | Categoria L1 | stringa | ⬜ | `"Calzature"` |
| `item_category2` | Categoria L2 | stringa | ⬜ | `"Sport"` |
| `item_variant` | Variante selezionata (taglia/colore) | stringa | ⬜ | `"Nero / 42"` |
| `price` | Prezzo unitario variante | numero | ✅ | `89.90` |
| `quantity` | Quantità (default: 1) | numero | ⬜ | `1` |

---

## Piattaforme

| Piattaforma | Tag GTM | Trigger | Note |
|-------------|---------|---------|------|
| GA4 | GA4 Event — view_item | Custom Event: `view_item` | Popola report Product detail views |
| Google Ads | Dynamic Remarketing | Custom Event: `view_item` | `ecommerce.items[0].item_id` → `id` |
| Meta Pixel / CAPI | Meta ViewContent | Custom Event: `view_item` | `value` + `currency` obbligatori per Meta |
| TikTok Pixel | TikTok ViewContent | Custom Event: `view_item` | |

---

## Note GDPR

- Nessun campo PII
- Richiede `analytics_storage: granted` per GA4
- Richiede `ad_storage: granted` per Google Ads e Meta (remarketing)

---

## Errori Comuni

| Errore | Conseguenza | Fix |
|--------|-------------|-----|
| `currency` mancante | GA4 ignora `value` | Sempre includere `currency` se si passa `value` |
| `item_variant` omesso su PDP con varianti | Impossibile analizzare performance per variante | Valorizzare con combinazione taglia/colore della variante visualizzata |
| Push non aggiornato al cambio variante AJAX | `view_item` registra solo la variante default | Ascoltare evento JS di cambio variante e re-pushare con `ecommerce: null` |
| `value` = 0 su prodotti in promozione | Revenue distorta nei report | Usare il prezzo scontato effettivo, non il prezzo base |

---

## Riferimenti

- GA4 view_item: https://developers.google.com/analytics/devguides/collection/ga4/reference/events#view_item
