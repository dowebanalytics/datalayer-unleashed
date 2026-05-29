---
title: generate_lead — Lead generato
type: note
tags:
  - lead
  - form
  - datalayer
  - ga4
related:
  - _Glossario
ga4_event: generate_lead
categoria: lead
piattaforme: [GA4, Google Ads, Meta CAPI, TikTok, Microsoft UET]
data_creazione: 2026-05-29
last_updated: 2026-05-29
source_verified_on: 2026-05-29
fonti:
  - https://developers.google.com/analytics/devguides/collection/ga4/reference/events#generate_lead
status: stable
---

# generate_lead — Lead generato

Push eseguito quando l'utente completa un form di contatto, richiesta informazioni, richiesta preventivo
o qualsiasi azione che genera un lead qualificato.

---

## Script

```javascript
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  event:     'generate_lead',
  value:     0,             // valore stimato del lead (opzionale, utile per Smart Bidding)
  currency:  'EUR',         // obbligatorio se si passa value
  lead_type: 'contact_form' // contact_form | quote_request | callback | newsletter_optin

  // Opzionale: dati utente per Enhanced Conversions lead
  // Solo se consenso ad_user_data: granted
  // user_data: { email: '...', phone_number: '...' }
});
```

---

## Parametri

| Parametro | Descrizione | Tipo | Obbligatorio | Esempio |
|-----------|-------------|------|:------------:|---------|
| `value` | Valore stimato del lead | numero | ⬜ | `50.00` |
| `currency` | Valuta (se value presente) | stringa | se value | `"EUR"` |
| `lead_type` | Tipologia di lead | stringa | ⬜ | `"contact_form"` |

---

## Piattaforme

| Piattaforma | Tag GTM | Trigger |
|-------------|---------|---------|
| GA4 | GA4 Event — generate_lead | Custom Event: `generate_lead` |
| Google Ads | Conversion — Lead | Custom Event: `generate_lead` |
| Meta CAPI | Meta Lead | Custom Event: `generate_lead` |
| TikTok | TikTok SubmitForm | Custom Event: `generate_lead` |
| Microsoft UET | UET Goal | Custom Event: `generate_lead` |

---

## Note GDPR

- Se si raccolgono dati utente dal form, aggiungerli come `user_data` (solo con `ad_user_data: granted`)
- Richiede `analytics_storage: granted` e `ad_storage: granted`

---

## Riferimenti

- GA4 generate_lead: https://developers.google.com/analytics/devguides/collection/ga4/reference/events#generate_lead
