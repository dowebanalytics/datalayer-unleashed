# dataLayer Unleashed

Template operativi dei push dataLayer da utilizzare durante la redazione dei **documenti di implementazione** per sviluppatori.

Ogni nota contiene: descrizione dell'evento, script JavaScript pronto all'uso, tabella parametri con tipo e esempio, note GDPR/Consent Mode, piattaforme che leggono il push.

## Struttura del vault

| Cartella | Contenuto |
|----------|-----------|
| `00_Init` | Push di inizializzazione pagina (contesto pagina, utente, user_data, user_properties) |
| `01_Ecommerce` | Tutti gli 11 eventi standard GA4 ecommerce (view_item_list → refund) |
| `02_User` | Login, registrazione, aggiornamento account |
| `03_Content` | Ricerca, selezione contenuto, condivisione |
| `04_Lead` | Lead generation, form submission |
| `05_Engagement` | Newsletter, wishlist, coupon, chat |
| `09_Templates` | Template base per nuovi eventi |

## Convenzioni

- Ogni push è documentato con: descrizione, script, tabella parametri, piattaforme, note GDPR
- I valori `user_data` seguono lo schema ufficiale Google (UPD / Enhanced Conversions)
- Le `user_properties` seguono le convenzioni GA4 (snake_case, max 24 char nome, max 36 char valore)
- L'ecommerce segue la specifica GA4 recommended events ufficiale
- Il push `ecommerce: null` è sempre documentato dove obbligatorio

## Utilizzo

1. Identifica l'evento nella cartella corrispondente
2. Copia lo script nella documentazione tecnica per il dev
3. Adatta i valori di esempio ai dati reali del sito
4. Verifica la sezione GDPR per le condizioni di firing

## Integrazione futura

Questo vault è pensato per essere integrato come sezione operativa in **Tracking Masterpiece**
una volta completato e validato su implementazioni reali.

## Vault correlati

- **Tracking Unleashed** — metodologia GTM, GA4, Consent Mode, server-side
- **BOT Unleashed** — rilevamento e mitigazione traffico bot/IVT
