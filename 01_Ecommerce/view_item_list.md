---
title: view_item_list — Visualizzazione lista prodotti
type: note
tags:
  - ecommerce
  - datalayer
  - ga4
  - view_item_list
  - listing
related:
  - _MOC_Ecommerce
  - _Glossario
  - select_item
  - view_item
ga4_event: view_item_list
categoria: ecommerce
piattaforme: [GA4, Meta CAPI, TikTok]
data_creazione: 2026-05-29
last_updated: 2026-05-29
source_verified_on: 2026-05-29
fonti:
  - https://developers.google.com/analytics/devguides/collection/ga4/reference/events#view_item_list
status: stable
---

# view_item_list — Visualizzazione lista prodotti

Push eseguito quando l'utente visualizza una pagina che contiene una lista di prodotti:
pagina categoria, risultati di ricerca, widget prodotti correlati, slider homepage.
Ogni prodotto visibile nella lista deve essere incluso nell'array `items[]`.

> **Nota:** eseguire sempre `dataLayer.push({ ecommerce: null })` prima di questo push.

---

## Script

```javascript
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({ ecommerce: null }); // reset obbligatorio

window.dataLayer.push({
  event: 'view_item_list',
  ecommerce: {
    item_list_id:   'category_abbigliamento',   // ID slug della lista
    item_list_name: 'Abbigliamento',             // nome leggibile della lista
    items: [
      {
        item_id:        'SKU_001',
        item_name:      'Sneakers running',
        item_brand:     'Acme',
        item_category:  'Calzature',
        item_category2: 'Sport',
        item_list_id:   'category_abbigliamento', // ripetere a livello item
        item_list_name: 'Abbigliamento',
        index:          0,              // posizione 0-based nella lista
        price:          89.90,
        quantity:       1
      },
      {
        item_id:        'SKU_002',
        item_name:      'Calzini sport',
        item_brand:     'Acme',
        item_category:  'Abbigliamento',
        item_list_id:   'category_abbigliamento',
        item_list_name: 'Abbigliamento',
        index:          1,
        price:          14.90,
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
| `item_list_id` | ID slug della lista | stringa | ⬜ | `"category_abbigliamento"` |
| `item_list_name` | Nome leggibile della lista | stringa | ⬜ | `"Abbigliamento"` |
| `items[]` | Array prodotti visibili | array | ✅ | vedi sotto |

## Parametri — items[]

| Parametro | Descrizione | Tipo | Obbligatorio | Esempio |
|-----------|-------------|------|:------------:|---------|
| `item_id` | SKU univoco | stringa | ✅ | `"SKU_001"` |
| `item_name` | Nome prodotto | stringa | ✅ | `"Sneakers running"` |
| `item_brand` | Brand | stringa | ⬜ | `"Acme"` |
| `item_category` | Categoria L1 | stringa | ⬜ | `"Calzature"` |
| `item_category2` | Categoria L2 | stringa | ⬜ | `"Sport"` |
| `item_list_id` | ID lista (ripetuto a livello item) | stringa | ⬜ | `"category_abbigliamento"` |
| `item_list_name` | Nome lista (ripetuto a livello item) | stringa | ⬜ | `"Abbigliamento"` |
| `index` | Posizione nella lista (0-based) | numero | ⬜ | `0` |
| `price` | Prezzo unitario | numero | ⬜ | `89.90` |
| `quantity` | Quantità | numero | ⬜ | `1` |

---

## Piattaforme

| Piattaforma | Tag GTM | Trigger | Note |
|-------------|---------|---------|------|
| GA4 | GA4 Event — view_item_list | Custom Event: `view_item_list` | Popola report Item list performance |
| Meta Pixel / CAPI | Meta ViewCategory | Custom Event: `view_item_list` | |
| TikTok Pixel | TikTok ViewContent | Custom Event: `view_item_list` | |

---

## Note GDPR

- Nessun campo PII
- Richiede `analytics_storage: granted` per GA4
- Richiede `ad_storage: granted` per Meta e TikTok

---

## Errori Comuni

| Errore | Conseguenza | Fix |
|--------|-------------|-----|
| `items[]` con soli prodotti above the fold | Dati incompleti di impression | Includere tutti i prodotti nel DOM, anche se non visibili senza scroll |
| `index` omesso | Impossibile analizzare position performance | Sempre includere `index` 0-based |
| `item_list_id` / `item_list_name` omessi | Impossibile distinguere liste nei report GA4 | Valorizzare con slug coerente (es. `category_slug`, `search_results`, `related_products`) |
| Reset `ecommerce: null` omesso | Merge con dati della lista precedente in SPA | Push `{ ecommerce: null }` prima di ogni evento |

---

## Riferimenti

- GA4 view_item_list: https://developers.google.com/analytics/devguides/collection/ga4/reference/events#view_item_list
