---
title: select_content — Selezione contenuto
type: note
tags:
  - content
  - datalayer
  - ga4
related:
  - _Glossario
ga4_event: select_content
categoria: content
piattaforme: [GA4]
data_creazione: 2026-05-29
last_updated: 2026-05-29
status: draft
---

# select_content — Selezione contenuto

> 🔲 **Stub** — da completare.

Push eseguito quando l'utente seleziona un contenuto editoriale (articolo, video, scheda informativa).

---

## Script

```javascript
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  event:        'select_content',
  content_type: 'article',    // article | video | product | banner
  item_id:      'post-123'    // ID univoco del contenuto
});
```

---

## Riferimenti

- GA4 select_content: https://developers.google.com/analytics/devguides/collection/ga4/reference/events#select_content
