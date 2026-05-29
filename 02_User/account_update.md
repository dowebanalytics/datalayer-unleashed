---
title: account_update — Aggiornamento dati account
type: note
tags:
  - user
  - account
  - datalayer
  - ga4
related:
  - _MOC_User
  - init
  - login
ga4_event: null
categoria: user
piattaforme: [GA4, Google Ads, Meta CAPI]
data_creazione: 2026-05-29
last_updated: 2026-05-29
status: draft
---

# account_update — Aggiornamento dati account

> 🔲 **Stub** — evento custom (non recommended GA4). Da completare.

Push eseguito quando l'utente aggiorna i propri dati (email, telefono, indirizzo).
Serve principalmente per aggiornare `user_data` e rialimentare Enhanced Conversions con i nuovi valori.

---

## Script

```javascript
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  event: 'account_update',

  // Ri-pushare user_data aggiornato — solo se consenso ad_user_data: granted
  user_data: {
    email:        'nuova.email@gmail.com',
    phone_number: '+393339876543',
    address: {
      first_name:  'mario',
      last_name:   'rossi',
      postal_code: '00100',
      country:     'it'
    }
  }
});
```

---

## Note GDPR

- Pushare `user_data` aggiornato solo se `ad_user_data: granted`
- Questo push aggiorna il dato anche per le Enhanced Conversions future nella stessa sessione
