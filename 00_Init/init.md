---
title: init — Push di inizializzazione
type: note
tags:
  - init
  - datalayer
  - gtm
  - user-data
  - user-properties
  - consent-mode
related:
  - _Glossario
  - _MOC_User
  - login
ga4_event: null
categoria: init
piattaforme: [GA4, Google Ads, Meta CAPI, TikTok, Microsoft UET]
data_creazione: 2026-05-29
last_updated: 2026-05-29
source_verified_on: 2026-05-29
fonti:
  - https://support.google.com/analytics/answer/14078702
  - https://support.google.com/google-ads/answer/13262500
  - https://developers.facebook.com/docs/meta-pixel/advanced/advanced-matching/
status: stable
---

# init — Push di inizializzazione

Push **senza nome evento** da eseguire immediatamente prima dello snippet GTM in ogni pagina.
Popola il modello dati GTM con contesto pagina, stato autenticazione, dati utente e user properties.
Non attiva trigger: rende i valori disponibili come DLV su tutti gli eventi successivi.

---

## Quando eseguire

- **Ogni pageload** — prima dello snippet GTM
- **Ogni cambio route virtuale** nelle SPA (AngularJS, React, Vue.js) — aggiornare almeno `page_type`, `page_category`, `page_subcategory`
- Rieseguire con dati completi post-login se l'utente effettua il login nella stessa sessione

---

## Script — utente non loggato

```javascript
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({

  // Contesto pagina
  page_type:        'product',       // home | category | product | cart |
                                     // checkout | order_confirmation | account | other
  page_category:    'abbigliamento',
  page_subcategory: 'maglie',        // opzionale
  site_environment: 'production',    // production | staging | development
  site_language:    'it',            // ISO 639-1
  site_currency:    'EUR',           // ISO 4217

  // Stato sessione
  user_logged_in:   false

});
```

---

## Script — utente loggato

```javascript
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({

  // Contesto pagina
  page_type:        'product',
  page_category:    'abbigliamento',
  page_subcategory: 'maglie',
  site_environment: 'production',
  site_language:    'it',
  site_currency:    'EUR',

  // Stato sessione
  user_logged_in:   true,
  user_id:          '1234',         // ID interno — MAI email in chiaro
  user_type:        'registered',   // registered | guest | new_customer | returning

  // User Data — schema ufficiale Google UPD / Enhanced Conversions
  // Popolare SOLO se consenso ad_user_data: granted
  user_data: {
    email:        'mario.rossi@gmail.com',  // lowercase + trim
    phone_number: '+393331234567',           // formato E.164
    address: {
      first_name:  'mario',       // lowercase
      last_name:   'rossi',       // lowercase
      street:      'via manzoni 31',
      city:        'san benedetto del tronto',
      region:      'ap',
      postal_code: '63074',
      country:     'it'           // ISO 3166-1 alpha-2
    }
  },

  // User Properties — dimensioni utente GA4
  // snake_case, max 24 char nome, max 36 char valore, no PII
  user_properties: {
    customer_segment:    'loyal',        // new | returning | loyal | vip | at_risk
    subscription_plan:   'premium',      // free | premium | business
    total_orders_count:  '7',            // stringa
    customer_value_tier: 'high',         // low | medium | high
    registration_date:   '2023-05-14',   // ISO 8601
    acquisition_channel: 'google_ads',
    has_loyalty_card:    'true',         // 'true' | 'false'
    preferred_category:  'abbigliamento'
  }

});
```

---

## Parametri — Contesto pagina

| Parametro | Descrizione | Tipo | Obbligatorio | Esempio |
|-----------|-------------|------|:------------:|---------|
| `page_type` | Classificazione pagina | stringa | ✅ | `"product"` |
| `page_category` | Tassonomia L1 | stringa | ✅ | `"abbigliamento"` |
| `page_subcategory` | Tassonomia L2 | stringa | ⬜ | `"maglie"` |
| `site_environment` | Ambiente | stringa | ✅ | `"production"` |
| `site_language` | Lingua (ISO 639-1) | stringa | ✅ | `"it"` |
| `site_currency` | Valuta (ISO 4217) | stringa | ✅ | `"EUR"` |

## Parametri — Stato sessione

| Parametro | Descrizione | Tipo | Obbligatorio | Esempio |
|-----------|-------------|------|:------------:|---------|
| `user_logged_in` | Utente loggato | booleano | ✅ | `true` |
| `user_id` | ID interno utente | stringa | se loggato | `"1234"` |
| `user_type` | Tipologia utente | stringa | ⬜ | `"registered"` |

## Parametri — user_data

| Parametro | Descrizione | Tipo | Obbligatorio | Esempio |
|-----------|-------------|------|:------------:|---------|
| `email` | Email. Lowercase + trim | stringa | ✅ se loggato | `"mario.rossi@gmail.com"` |
| `phone_number` | Telefono. Formato E.164 | stringa | ⬜ | `"+393331234567"` |
| `address.first_name` | Nome. Lowercase | stringa | ⬜ | `"mario"` |
| `address.last_name` | Cognome. Lowercase | stringa | ⬜ | `"rossi"` |
| `address.street` | Via | stringa | ⬜ | `"via manzoni 31"` |
| `address.city` | Città | stringa | ⬜ | `"san benedetto del tronto"` |
| `address.region` | Provincia / regione | stringa | ⬜ | `"ap"` |
| `address.postal_code` | CAP | stringa | se address | `"63074"` |
| `address.country` | Paese (ISO 3166-1 alpha-2) | stringa | se address | `"it"` |

## Parametri — user_properties

| Parametro | Descrizione | Tipo | Esempio |
|-----------|-------------|------|---------|
| `customer_segment` | Segmento cliente | stringa | `"loyal"` |
| `subscription_plan` | Piano abbonamento | stringa | `"premium"` |
| `total_orders_count` | Ordini totali lifetime | stringa | `"7"` |
| `customer_value_tier` | Fascia CLV | stringa | `"high"` |
| `registration_date` | Data registrazione (ISO 8601) | stringa | `"2023-05-14"` |
| `acquisition_channel` | Canale acquisizione | stringa | `"google_ads"` |
| `has_loyalty_card` | Possiede loyalty card | stringa | `"true"` |
| `preferred_category` | Categoria preferita | stringa | `"abbigliamento"` |

---

## Piattaforme

| Piattaforma | Legge | Campo |
|-------------|-------|-------|
| GA4 | `page_type`, `page_category`, `user_id`, `user_properties` | DLV → GA4 Config tag |
| Google Ads EC | `user_data` | User-Provided Data variable → Enhanced Conversions |
| Meta Pixel / CAPI | `user_data` | Advanced Matching / Customer Information Parameters |
| TikTok Pixel | `user_data` | Advanced Matching |
| Microsoft UET | `user_data` | Enhanced Conversions |

---

## Note GDPR / Consent Mode v2

- `user_data` contiene PII → pushare **solo se `ad_user_data: granted`**
- `user_properties` non sono PII ma richiedono `analytics_storage: granted` per essere associate a un profilo persistente
- Se il consenso non è disponibile al pageload (primo accesso), omettere `user_data` e re-pusharlo post-consenso o al prossimo pageload
- Il blocco `user_data` deve essere omesso completamente per utenti anonimi, non valorizzato con stringhe vuote

---

## Errori Comuni

| Errore | Conseguenza | Fix |
|--------|-------------|-----|
| Push eseguito dopo lo snippet GTM | DLV non valorizzate al momento di gtm.js | Spostare il push prima dello snippet |
| `email` non normalizzata (uppercase, spazi) | Match rate SHA-256 degradato | `email.toLowerCase().trim()` lato backend |
| `user_data` pushato senza consenso | Violazione GDPR | Check `ad_user_data` prima del push |
| `first_name` / `last_name` al root invece che in `address` | Enhanced Conversions non riceve i dati | Struttura corretta: `address.first_name` |
| `user_properties` con valori numerici | Incompatibilità GA4 (accetta solo string) | Convertire in stringa: `'7'` non `7` |
| `page_type` con vocabolario non standardizzato | Conditional triggers rotti | Definire vocabolario fisso e documentarlo |

---

## Riferimenti

- Google Analytics UPD: https://support.google.com/analytics/answer/14078702
- Google Ads Enhanced Conversions: https://support.google.com/google-ads/answer/13262500
- Meta Advanced Matching: https://developers.facebook.com/docs/meta-pixel/advanced/advanced-matching/
- TikTok Advanced Matching: https://business-api.tiktok.com/portal/docs?id=1701890972946433
