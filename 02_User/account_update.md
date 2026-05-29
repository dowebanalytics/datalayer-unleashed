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
  - _Glossario
  - init
  - login
ga4_event: null
categoria: user
piattaforme: [GA4, Google Ads, Meta CAPI, TikTok, Microsoft UET]
data_creazione: 2026-05-29
last_updated: 2026-05-29
source_verified_on: 2026-05-29
fonti:
  - https://support.google.com/analytics/answer/14078702
  - https://support.google.com/google-ads/answer/13262500
status: stable
---

# account_update — Aggiornamento dati account

Evento custom (non recommended GA4) pushato quando l'utente salva modifiche al proprio profilo:
email, numero di telefono, indirizzo di spedizione o dati anagrafici.
Lo scopo principale è aggiornare `user_data` e `user_properties` nella sessione corrente
affinché Enhanced Conversions, Meta CAPI e TikTok ricevano i dati aggiornati sugli eventi successivi.

---

## Script

```javascript
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  event: 'account_update',

  // Campi aggiornati — includere solo quelli effettivamente modificati
  // oppure l'oggetto completo se il backend restituisce il profilo intero
  update_fields: 'email,phone',  // elenco campi modificati (custom param opzionale)

  // User Data aggiornato — solo se consenso ad_user_data: granted
  user_data: {
    email:        'nuova.email@gmail.com',  // lowercase + trim
    phone_number: '+393339876543',           // formato E.164
    address: {
      first_name:  'mario',
      last_name:   'rossi',
      street:      'via nuova 10',
      city:        'roma',
      region:      'rm',
      postal_code: '00100',
      country:     'it'
    }
  },

  // User Properties aggiornate (se cambiate dall'update)
  user_properties: {
    subscription_plan:  'premium',  // se l'utente ha cambiato piano
    preferred_category: 'sport'     // se aggiornata nelle preferenze
  }
});
```

---

## Parametri

| Parametro | Descrizione | Tipo | Obbligatorio | Esempio |
|-----------|-------------|------|:------------:|---------|
| `update_fields` | Elenco campi modificati (CSV) | stringa | ⬜ | `"email,phone"` |
| `user_data` | Dati utente aggiornati (PII) | oggetto | se dati aggiornati + consenso | vedi [[init]] |
| `user_data.email` | Nuova email. Lowercase + trim | stringa | ⬜ | `"nuova.email@gmail.com"` |
| `user_data.phone_number` | Nuovo telefono. Formato E.164 | stringa | ⬜ | `"+393339876543"` |
| `user_data.address.*` | Nuovo indirizzo | oggetto | ⬜ | vedi [[init]] |
| `user_properties` | Attributi utente GA4 aggiornati | oggetto | ⬜ | vedi [[init]] |

---

## Piattaforme

| Piattaforma | Tag GTM | Trigger | Note |
|-------------|---------|---------|------|
| GA4 | GA4 Event — account_update | Custom Event: `account_update` | Registra l'evento aggiornamento |
| Google Ads EC | User-Provided Data variable | Custom Event: `account_update` | Aggiorna user_data per EC sessione corrente |
| Meta Pixel / CAPI | Meta Custom Event | Custom Event: `account_update` | Aggiorna Advanced Matching |
| TikTok Pixel | TikTok Custom Event | Custom Event: `account_update` | Aggiorna Advanced Matching |
| Microsoft UET | UET Custom Event | Custom Event: `account_update` | |

---

## Note GDPR

- `user_data` contiene PII: pushare **solo se `ad_user_data: granted`**
- Se il consenso non è granted, eseguire il push con il solo campo `event` e `update_fields` (senza `user_data`)
- Il push aggiorna il modello GTM per la sessione corrente: gli eventi successivi (es. `purchase`) troveranno i dati aggiornati nelle DLV

---

## Errori Comuni

| Errore | Conseguenza | Fix |
|--------|-------------|-----|
| `user_data` pushato anche senza consenso | Violazione GDPR | Condizionare il push a `ad_user_data: granted` |
| `email` non normalizzata (uppercase, spazi) | Match rate SHA-256 degradato | `email.toLowerCase().trim()` lato backend prima del push |
| Push eseguito prima del salvataggio server | `user_data` non ancora validato | Triggerare solo su risposta HTTP 200 dal backend |
| `user_properties` non aggiornate dopo cambio piano | GA4 registra ancora il vecchio piano | Includere nel push tutti i campi `user_properties` modificati |

---

## Riferimenti

- Google Analytics UPD: https://support.google.com/analytics/answer/14078702
- Google Ads Enhanced Conversions: https://support.google.com/google-ads/answer/13262500
