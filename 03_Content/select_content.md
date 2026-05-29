---
title: select_content — Selezione contenuto
type: note
tags:
  - content
  - datalayer
  - ga4
  - select_content
related:
  - _Glossario
  - search
  - share
ga4_event: select_content
categoria: content
piattaforme: [GA4]
data_creazione: 2026-05-29
last_updated: 2026-05-29
source_verified_on: 2026-05-29
fonti:
  - https://developers.google.com/analytics/devguides/collection/ga4/reference/events#select_content
status: stable
---

# select_content — Selezione contenuto

Push eseguito quando l'utente seleziona (clicca su) un contenuto non-ecommerce:
articolo del blog, guida, video, banner editoriale, scheda FAQ, tab informativa.
Permette di misurare il CTR e il coinvolgimento su contenuti editoriali.

---

## Script

```javascript
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  event:        'select_content',
  content_type: 'article',   // article | guide | video | faq | banner | tab | category
  item_id:      'post-456'   // ID univoco del contenuto (slug, ID DB, ecc.)
});
```

---

## Parametri

| Parametro | Descrizione | Tipo | Obbligatorio | Esempio |
|-----------|-------------|------|:------------:|---------|
| `content_type` | Tipologia di contenuto | stringa | ✅ | `"article"` |
| `item_id` | Identificatore univoco del contenuto | stringa | ✅ | `"post-456"` |

### Valori consigliati per `content_type`

| Valore | Quando usarlo |
|--------|--------------|
| `article` | Click su articolo blog / news |
| `guide` | Click su guida o tutorial |
| `video` | Click su video editoriale (non prodotto) |
| `faq` | Apertura risposta FAQ (accordion) |
| `banner` | Click su banner promozionale o editoriale |
| `tab` | Cambio tab informativa su PDP (descrizione, specifiche, recensioni) |
| `category` | Click su categoria editoriale / tag |

---

## Piattaforme

| Piattaforma | Tag GTM | Trigger | Note |
|-------------|---------|---------|------|
| GA4 | GA4 Event — select_content | Custom Event: `select_content` | Popola report Events → engagement |

---

## Note GDPR

- Nessun campo PII
- Richiede `analytics_storage: granted`

---

## Errori Comuni

| Errore | Conseguenza | Fix |
|--------|-------------|-----|
| `content_type` non standardizzato (`"Article"`, `"ARTICLE"`, `"blog_post"`) | Frammentazione nei report | Definire vocabolario fisso lowercase e documentarlo nel tracking plan |
| `item_id` non univoco (es. stessa stringa per contenuti diversi) | Impossibile distinguere i contenuti | Usare ID DB o slug univoco per ogni contenuto |
| Confusione tra `select_content` e `select_item` | Dati ecommerce e contenuto mescolati | `select_item` solo per prodotti ecommerce, `select_content` per contenuti editoriali |

---

## Riferimenti

- GA4 select_content: https://developers.google.com/analytics/devguides/collection/ga4/reference/events#select_content
