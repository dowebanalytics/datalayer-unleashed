---
title: coupon_apply — Applicazione coupon
type: note
tags:
  - engagement
  - coupon
  - datalayer
  - ga4
related:
  - _Glossario
  - begin_checkout
ga4_event: null
categoria: engagement
piattaforme: [GA4]
data_creazione: 2026-05-29
last_updated: 2026-05-29
status: draft
---

# coupon_apply — Applicazione coupon

> 🔲 **Stub** — da completare.

Evento custom pushato quando l'utente applica un codice coupon con successo.

---

## Script

```javascript
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  event:        'coupon_apply',
  coupon_code:  'WELCOME10',
  coupon_value: 9.00,      // valore sconto applicato
  coupon_type:  'percent'  // percent | fixed
});
```
