---
title: login — Accesso utente
type: note
tags:
  - user
  - login
  - autenticazione
  - datalayer
  - ga4
related:
  - _MOC_User
  - init
  - sign_up
ga4_event: login
categoria: user
piattaforme: [GA4]
data_creazione: 2026-05-29
last_updated: 2026-05-29
source_verified_on: 2026-05-29
fonti:
  - https://developers.google.com/analytics/devguides/collection/ga4/reference/events#login
status: stable
---

# login — Accesso utente

Push eseguito quando l'utente completa il login con successo.
Dopo il push, re-pushare anche il contesto utente completo (user_data, user_properties, user_id)
se non già disponibili dal push init (es. login avvenuto nella stessa sessione di pageload anonimo).

---

## Script

```javascript
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  event:   'login',
  method:  'email',   // email | google | facebook | apple | phone

  // Aggiornamento contesto utente post-login
  user_logged_in: true,
  user_id:        '1234',
  user_type:      'registered',

  // User Data — solo se consenso ad_user_data: granted
  user_data: {
    email:        'mario.rossi@gmail.com',
    phone_number: '+393331234567',
    address: {
      first_name:  'mario',
      last_name:   'rossi',
      postal_code: '63074',
      country:     'it'
    }
  },

  // User Properties aggiornate
  user_properties: {
    customer_segment:   'loyal',
    total_orders_count: '7',
    customer_value_tier:'high'
  }
});
```

---

## Parametri

| Parametro | Descrizione | Tipo | Obbligatorio | Esempio |
|-----------|-------------|------|:------------:|---------|
| `method` | Metodo di login | stringa | ✅ | `"email"` |
| `user_logged_in` | Aggiorna stato sessione | booleano | ✅ | `true` |
| `user_id` | ID interno utente | stringa | ✅ | `"1234"` |
| `user_type` | Tipologia utente | stringa | ⬜ | `"registered"` |
| `user_data` | Dati utente (PII) | oggetto | se consenso | vedi [[init]] |
| `user_properties` | Attributi utente GA4 | oggetto | ⬜ | vedi [[init]] |

---

## Piattaforme

| Piattaforma | Tag GTM | Trigger |
|-------------|---------|---------|
| GA4 | GA4 Event — login | Custom Event: `login` |

---

## Note GDPR

- `user_data` contiene PII: pushare solo se `ad_user_data: granted`
- `user_id` non è PII se è un ID interno anonimizzato — non usare email

---

## Riferimenti

- GA4 login event: https://developers.google.com/analytics/devguides/collection/ga4/reference/events#login
