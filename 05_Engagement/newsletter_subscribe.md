---
title: newsletter_subscribe — Iscrizione newsletter
type: note
tags:
  - engagement
  - newsletter
  - datalayer
  - ga4
related:
  - _Glossario
  - generate_lead
ga4_event: null
categoria: engagement
piattaforme: [GA4, Meta CAPI, Klaviyo]
data_creazione: 2026-05-29
last_updated: 2026-05-29
status: stable
---

# newsletter_subscribe — Iscrizione newsletter

Evento custom (non recommended GA4) pushato quando l'utente completa l'iscrizione alla newsletter.

---

## Script

```javascript
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  event:              'newsletter_subscribe',
  newsletter_source:  'footer_form',  // footer_form | popup | checkout | account
  newsletter_topic:   'general'       // general | promo | product_updates (se presente)
});
```

---

## Parametri

| Parametro | Descrizione | Tipo | Obbligatorio | Esempio |
|-----------|-------------|------|:------------:|---------|
| `newsletter_source` | Punto di raccolta iscrizione | stringa | ✅ | `"footer_form"` |
| `newsletter_topic` | Tipologia newsletter | stringa | ⬜ | `"general"` |

---

## Note GDPR

- L'email dell'utente è gestita dal form sottostante, non va nel push
- Nessun campo PII nel push
