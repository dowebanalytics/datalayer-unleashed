---
title: coupon_apply — Applicazione coupon
type: note
tags:
  - engagement
  - coupon
  - sconto
  - datalayer
  - ga4
related:
  - _Glossario
  - begin_checkout
  - purchase
ga4_event: null
categoria: engagement
piattaforme: [GA4]
data_creazione: 2026-05-29
last_updated: 2026-05-29
source_verified_on: 2026-05-29
fonti:
  - https://developers.google.com/analytics/devguides/collection/ga4/reference/events
status: stable
---

# coupon_apply — Applicazione coupon

Evento custom pushato quando l'utente inserisce e applica con successo un codice coupon/sconto.
Permette di misurare il tasso di utilizzo dei coupon, i codici più usati e il loro impatto
sul funnel di conversione.

Il push deve avvenire **solo su applicazione valida**: se il coupon non è valido o scaduto,
non pushare (o pushare un evento separato `coupon_error`).

---

## Script — applicazione valida

```javascript
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  event:        'coupon_apply',
  coupon_code:  'WELCOME10',    // codice inserito dall'utente (uppercase consigliato)
  coupon_value: 9.00,           // valore sconto applicato in valuta
  coupon_type:  'percent',      // percent | fixed | free_shipping | gift
  coupon_scope: 'order'         // order | item | shipping
});
```

## Script — coupon non valido (opzionale)

```javascript
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  event:         'coupon_error',
  coupon_code:   'CODICESBAGLIATO',
  coupon_error:  'invalid'   // invalid | expired | already_used | minimum_not_met
});
```

---

## Parametri — coupon_apply

| Parametro | Descrizione | Tipo | Obbligatorio | Esempio |
|-----------|-------------|------|:------------:|---------|
| `coupon_code` | Codice coupon applicato | stringa | ✅ | `"WELCOME10"` |
| `coupon_value` | Valore sconto in valuta | numero | ✅ | `9.00` |
| `coupon_type` | Tipologia di sconto | stringa | ✅ | `"percent"` |
| `coupon_scope` | Ambito applicazione sconto | stringa | ⬜ | `"order"` |

### Valori per `coupon_type`

| Valore | Descrizione |
|--------|-------------|
| `percent` | Sconto percentuale (es. 10%) |
| `fixed` | Sconto fisso in valuta (es. €10) |
| `free_shipping` | Spedizione gratuita |
| `gift` | Prodotto omaggio |

### Valori per `coupon_scope`

| Valore | Descrizione |
|--------|-------------|
| `order` | Sconto applicato all'intero ordine |
| `item` | Sconto applicato a specifici prodotti |
| `shipping` | Sconto applicato alla spedizione |

## Parametri — coupon_error (opzionale)

| Parametro | Descrizione | Tipo | Obbligatorio | Esempio |
|-----------|-------------|------|:------------:|---------|
| `coupon_code` | Codice inserito dall'utente | stringa | ✅ | `"CODICESBAGLIATO"` |
| `coupon_error` | Motivo dell'errore | stringa | ✅ | `"expired"` |

---

## Piattaforme

| Piattaforma | Tag GTM | Trigger | Note |
|-------------|---------|---------|------|
| GA4 | GA4 Event — coupon_apply | Custom Event: `coupon_apply` | Analisi coupon adoption e impact sul funnel |
| GA4 | GA4 Event — coupon_error | Custom Event: `coupon_error` | Analisi coupon rejection rate (opzionale) |

---

## Note GDPR

- Nessun campo PII
- Richiede `analytics_storage: granted`
- `coupon_code` non è PII, ma se i codici sono nominali (es. `MARIO_VIP`) considerare l'anonimizzazione

---

## Errori Comuni

| Errore | Conseguenza | Fix |
|--------|-------------|-----|
| Push su tentativo non valido | Dati coupon gonfiati | Pushare `coupon_apply` solo su risposta di successo dal backend |
| `coupon_code` in lowercase/uppercase misto | Frammentazione nei report | Normalizzare sempre in uppercase sul push |
| `coupon_value` calcolato lato client prima della risposta server | Valore sconto potenzialmente errato | Usare il valore restituito dal backend dopo la validazione |
| `coupon_apply` non pushato se il coupon è già nel carrello al pageload | Dati parziali su sessioni con coupon pre-applicato | Pushare anche all'apertura del carrello se il coupon risulta già attivo |

---

## Riferimenti

- GA4 Events Reference: https://developers.google.com/analytics/devguides/collection/ga4/reference/events
