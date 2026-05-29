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
  - select_content
ga4_event: share
categoria: content
piattaforme: [GA4]
data_creazione: 2026-05-29
last_updated: 2026-05-29
source_verified_on: 2026-05-29
fonti:
  - https://developers.google.com/analytics/devguides/collection/ga4/reference/events#share
status: stable
---

# share — Condivisione contenuto

Push eseguito quando l'utente condivide un contenuto tramite i pulsanti di condivisione social,
email, WhatsApp o copia link. Misura il tasso di condivisione per canale e tipo di contenuto.

---

## Script

```javascript
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  event:        'share',
  method:       'whatsapp',  // canale di condivisione (vedi tabella sotto)
  content_type: 'article',   // article | product | guide | video
  item_id:      'post-456'   // ID univoco del contenuto condiviso
});
```

---

## Parametri

| Parametro | Descrizione | Tipo | Obbligatorio | Esempio |
|-----------|-------------|------|:------------:|---------|
| `method` | Canale di condivisione | stringa | ✅ | `"whatsapp"` |
| `content_type` | Tipologia di contenuto condiviso | stringa | ✅ | `"article"` |
| `item_id` | ID univoco del contenuto | stringa | ✅ | `"post-456"` |

### Valori consigliati per `method`

| Valore | Canale |
|--------|--------|
| `facebook` | Pulsante condivisione Facebook |
| `twitter` | Pulsante condivisione X / Twitter |
| `whatsapp` | Pulsante condivisione WhatsApp |
| `linkedin` | Pulsante condivisione LinkedIn |
| `pinterest` | Pulsante condivisione Pinterest |
| `email` | Condivisione via email |
| `copy_link` | Copia URL negli appunti |
| `native` | Share nativo del browser/OS (Web Share API) |

---

## Piattaforme

| Piattaforma | Tag GTM | Trigger | Note |
|-------------|---------|---------|------|
| GA4 | GA4 Event — share | Custom Event: `share` | Analisi viralità contenuti |

---

## Note GDPR

- Nessun campo PII
- Richiede `analytics_storage: granted`

---

## Errori Comuni

| Errore | Conseguenza | Fix |
|--------|-------------|-----|
| `method` con nome del canale non standardizzato (`"FB"`, `"Facebook"`, `"facebook"`) | Frammentazione | Vocabolario fisso lowercase |
| Push mancante per condivisione via Web Share API (mobile) | Dati share mobile incompleti | Ascoltare l'evento `navigator.share()` e pushare con `method: 'native'` |
| `item_id` omesso | Impossibile risalire al contenuto condiviso | Sempre valorizzare con slug o ID del contenuto |

---

## Riferimenti

- GA4 share: https://developers.google.com/analytics/devguides/collection/ga4/reference/events#share
