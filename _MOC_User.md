---
title: MOC — User
type: moc
tags:
  - moc
  - user
  - login
  - registrazione
data_creazione: 2026-05-29
last_updated: 2026-05-29
status: stable
---

# MOC — User

Mappa degli eventi relativi all'autenticazione e gestione utente.

## Eventi

| Evento | Quando | Note |
|--------|--------|------|
| [[login]] | Utente completa il login | Aggiornare user_data e user_properties post-login |
| [[sign_up]] | Utente completa la registrazione | Primo push con user_id |
| [[account_update]] | Utente aggiorna i propri dati | Re-pushare user_data aggiornato |

## Relazione con il push init

Il push `init` (senza evento) popola il contesto utente ad ogni pageload.
Gli eventi `login` e `sign_up` completano il profilo utente con:
- Nuovo `user_id` (appena ottenuto dal backend)
- `user_data` aggiornato (email, telefono, indirizzo)
- `user_properties` aggiornate (segment, order_count, ecc.)

In un'architettura SPA, dopo il login è necessario re-pushare `user_logged_in: true`
e `user_id` perché il push init originale li aveva valorizzati a `false` / omessi.
