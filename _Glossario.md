---
title: Glossario — dataLayer Unleashed
type: glossary
tags:
  - glossario
  - datalayer
  - ga4
  - gtm
data_creazione: 2026-05-29
last_updated: 2026-05-29
status: stable
---

# Glossario — dataLayer Unleashed

| Termine | Definizione |
|---------|-------------|
| **dataLayer** | Array JavaScript globale (`window.dataLayer`) usato da GTM per ricevere dati dalla pagina. Ogni elemento è un oggetto con parametri e/o un campo `event`. |
| **push** | Operazione `dataLayer.push({...})` che aggiunge un oggetto all'array e notifica GTM. |
| **message** | Termine interno GTM per ogni oggetto pushato nel dataLayer. Se l'oggetto ha un campo `event`, diventa un trigger attivabile. |
| **push senza evento** | Push che non contiene il campo `event`. Popola il modello dati GTM ma non attiva trigger. Usato per dati di contesto pagina/utente. |
| **DLV** | Data Layer Variable — tipo di variabile GTM che legge un valore dal dataLayer tramite dot-notation (es. `ecommerce.value`). |
| **ecommerce: null** | Push di reset obbligatorio prima di ogni evento ecommerce. Evita che dati del push precedente contaminino quello successivo. |
| **user_data** | Oggetto contenente PII utente (email, telefono, indirizzo) nel formato ufficiale Google per Enhanced Conversions e User-Provided Data (UPD). |
| **user_properties** | Oggetto con attributi utente non identificativi (segmento, piano, CLV tier) da mappare come GA4 User Properties. |
| **UPD** | User-Provided Data — funzionalità Google che raccoglie, hasha e invia dati utente per Enhanced Conversions e GA4. |
| **Enhanced Conversions** | Funzionalità Google Ads che invia dati utente hashati SHA-256 per migliorare l'attribuzione delle conversioni. |
| **SHA-256** | Algoritmo di hashing one-way usato da Google per anonimizzare email, telefono e nome prima dell'invio. GTM e sGTM lo applicano automaticamente se si usa la variabile User-Provided Data. |
| **E.164** | Formato internazionale per numeri di telefono: prefisso paese + numero, senza spazi o trattini (es. `+393331234567`). |
| **items[]** | Array GA4 obbligatorio in tutti gli eventi ecommerce. Contiene uno o più oggetti prodotto con `item_id`, `item_name`, `price`, `quantity`. |
| **recommended events** | Categoria GA4 di eventi con nome e parametri standardizzati da Google. Da preferire sempre ai custom events. |
| **Consent Mode v2** | Framework Google per la gestione del consenso. I segnali rilevanti per il dataLayer sono `analytics_storage`, `ad_storage`, `ad_user_data`, `ad_personalization`. |
| **ad_user_data** | Segnale Consent Mode v2 specifico per l'invio di dati utente a piattaforme Google. Deve essere `granted` per inviare `user_data`. |
| **PII** | Personally Identifiable Information — dati che identificano direttamente un individuo (email, telefono, nome, indirizzo). |
| **sGTM** | Server-side Google Tag Manager — container GTM che gira su infrastruttura server anziché nel browser. Legge gli stessi push del container web. |
| **item_id** | Identificatore univoco del prodotto (SKU). Obbligatorio in tutti gli eventi ecommerce. |
| **transaction_id** | Identificatore univoco dell'ordine. Obbligatorio nell'evento `purchase`. GA4 usa questo campo per deduplicare ordini duplicati. |
