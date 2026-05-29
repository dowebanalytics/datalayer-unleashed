---
title: share — Condivisione contenuto
type: note
tags:
  - content
  - share
  - datalayer
  - ga4
related:
  - _Glossario
ga4_event: share
categoria: content
piattaforme: [GA4]
data_creazione: 2026-05-29
last_updated: 2026-05-29
status: draft
---

# share — Condivisione contenuto

> 🔲 **Stub** — da completare.

Push eseguito quando l'utente condivide un contenuto tramite social, email o copia link.

---

## Script

```javascript
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  event:        'share',
  method:       'twitter',    // twitter | facebook | whatsapp | email | copy_link
  content_type: 'article',
  item_id:      'post-123'
});
```

---

## Riferimenti

- GA4 share: https://developers.google.com/analytics/devguides/collection/ga4/reference/events#share
