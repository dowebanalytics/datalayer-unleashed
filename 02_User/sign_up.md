---
title: sign_up — Registrazione utente
type: note
tags:
  - user
  - registrazione
  - datalayer
  - ga4
related:
  - _MOC_User
  - init
  - login
ga4_event: sign_up
categoria: user
piattaforme: [GA4, Google Ads]
data_creazione: 2026-05-29
last_updated: 2026-05-29
source_verified_on: 2026-05-29
fonti:
  - https://developers.google.com/analytics/devguides/collection/ga4/reference/events#sign_up
status: stable
---

# sign_up — Registrazione utente

Push eseguito quando l'utente completa la registrazione con successo.
Primo evento con user_id valido per questo utente.

---

## Script

```javascript
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  event:  'sign_up',
  method: 'email',   // email | google | facebook | apple

  user_logged_in: true,
  user_id:        '1234',
  user_type:      'new_customer',

  user_data: {
    email:        'mario.rossi@gmail.com',
    phone_number: '+393331234567',
    address: {
      first_name: 'mario',
      last_name:  'rossi',
      country:    'it'
    }
  },

  user_properties: {
    customer_segment:    'new',
    total_orders_count:  '0',
    registration_date:   '2026-05-29',
    acquisition_channel: 'google_ads'
  }
});
```

---

## Parametri

| Parametro | Descrizione | Tipo | Obbligatorio | Esempio |
|-----------|-------------|------|:------------:|---------|
| `method` | Metodo di registrazione | stringa | ✅ | `"email"` |
| `user_logged_in` | Aggiorna stato sessione | booleano | ✅ | `true` |
| `user_id` | ID interno nuovo utente | stringa | ✅ | `"1234"` |
| `user_data` | Dati utente (PII) | oggetto | se consenso | vedi [[init]] |
| `user_properties` | Attributi utente GA4 | oggetto | ⬜ | vedi [[init]] |

---

## Note GDPR

- Stesso principio di [[login]] per `user_data`
- `registration_date` in `user_properties` non è PII

---

## Riferimenti

- GA4 sign_up event: https://developers.google.com/analytics/devguides/collection/ga4/reference/events#sign_up
