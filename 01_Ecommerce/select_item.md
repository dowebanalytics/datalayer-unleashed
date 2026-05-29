---
title: select_item — Click su prodotto in lista
type: note
tags:
  - ecommerce
  - datalayer
  - ga4
  - select_item
related:
  - _MOC_Ecommerce
  - _Glossario
  - view_item_list
  - view_item
ga4_event: select_item
categoria: ecommerce
piattaforme: [GA4]
data_creazione: 2026-05-29
last_updated: 2026-05-29
source_verified_on: 2026-05-29
fonti:
  - https://developers.google.com/analytics/devguides/collection/ga4/reference/events#select_item
status: stable
---

# select_item — Click su prodotto in lista

Push eseguito quando l'utente clicca su un prodotto all'interno di una lista (categoria, ricerca,
prodotti correlati, slider). Precede sempre `view_item` nel funnel.
Permette di misurare il CTR di ogni prodotto per posizione nella lista.

> **Nota:** eseguire sempre `dataLayer.push({ ecommerce: null })` prima di questo push.

---

## Script

```javascript
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({ ecommerce: null }); // reset obbligatorio

window.dataLayer.push({
  event: 'select_item',
  ecommerce: {
    item_list_id:   'category_abbigliamento',
    item_list_name: 'Abbigliamento',
    items: [
      {
        item_id:        'SKU_001',
        item_name:      'Sneakers running',
        item_brand:     'Acme',
        item_category:  'Calzature',
        item_category2: 'Sport',
        item_list_id:   'category_abbigliamento',
        item_list_name: 'Abbigliamento',
        index:          0,     // posizione del prodotto nella lista (0-based)
        price:          89.90,
        quantity:       1
      }
    ]
  }
});
```

> `items[]` contiene **un solo prodotto** — quello su cui l'utente ha cliccato.

---

## Parametri — evento

| Parametro | Descrizione | Tipo | Obbligatorio | Esempio |
|-----------|-------------|------|:------------:|---------|
| `item_list_id` | ID slug della lista di provenienza | stringa | ⬜ | `"category_abbigliamento"` |
| `item_list_name` | Nome lista di provenienza | stringa | ⬜ | `"Abbigliamento"` |
| `items[]` | Array con il singolo prodotto cliccato | array | ✅ | vedi sotto |

## Parametri — items[] (singolo prodotto)

| Parametro | Descrizione | Tipo | Obbligatorio | Esempio |
|-----------|-------------|------|:------------:|---------|
| `item_id` | SKU univoco | stringa | ✅ | `"SKU_001"` |
| `item_name` | Nome prodotto | stringa | ✅ | `"Sneakers running"` |
| `item_brand` | Brand | stringa | ⬜ | `"Acme"` |
| `item_category` | Categoria L1 | stringa | ⬜ | `"Calzature"` |
| `item_list_id` | ID lista (ripetuto a livello item) | stringa | ⬜ | `"category_abbigliamento"` |
| `item_list_name` | Nome lista (ripetuto a livello item) | stringa | ⬜ | `"Abbigliamento"` |
| `index` | Posizione nella lista (0-based) | numero | ⬜ | `0` |
| `price` | Prezzo unitario | numero | ⬜ | `89.90` |
| `quantity` | Quantità | numero | ⬜ | `1` |

---

## Piattaforme

| Piattaforma | Tag GTM | Trigger | Note |
|-------------|---------|---------|------|
| GA4 | GA4 Event — select_item | Custom Event: `select_item` | Abilita CTR analysis per posizione |

---

## Note GDPR

- Nessun campo PII
- Richiede `analytics_storage: granted`

---

## Errori Comuni

| Errore | Conseguenza | Fix |
|--------|-------------|-----|
| `items[]` con più prodotti | GA4 registra click multipli | Un solo item — quello cliccato |
| `index` omesso | Impossibile analizzare performance per posizione | Sempre valorizzare con posizione 0-based |
| `item_list_id` diverso da quello usato in `view_item_list` | Rottura del funnel lista→click | Usare lo stesso ID slug in entrambi gli eventi |

---

## Riferimenti

- GA4 select_item: https://developers.google.com/analytics/devguides/collection/ga4/reference/events#select_item
