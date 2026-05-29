---
title: dataLayer Unleashed — Vault Index
type: index
tags:
  - meta
  - vault
  - stato
data_creazione: 2026-05-29
last_updated: 2026-05-29
status: stable
---

# _Vault Index — dataLayer Unleashed

Stato del vault. Aggiornare ad ogni sessione di lavoro significativa.
Ultima modifica: **29 maggio 2026** (v1.1 — completamento 01_Ecommerce)

---

## Path Vault

```
/Users/guidobarbacci/Library/Mobile Documents/com~apple~CloudDocs/00_DO_WEB_ANALYTICS/dataLayer Unleashed/
```

## Repository GitHub

```
https://github.com/dowebanalytics/datalayer-unleashed
```

---

## Struttura

```
dataLayer Unleashed/
├── README.md
├── 00_Index.md
├── _vault_index.md
├── _Glossario.md
├── _MOC_Ecommerce.md
├── _MOC_User.md
│
├── 00_Init/
│   └── init.md
│
├── 01_Ecommerce/
│   ├── view_item_list.md
│   ├── select_item.md
│   ├── view_item.md
│   ├── add_to_cart.md
│   ├── remove_from_cart.md
│   ├── view_cart.md
│   ├── begin_checkout.md
│   ├── add_shipping_info.md
│   ├── add_payment_info.md
│   ├── purchase.md
│   └── refund.md
│
├── 02_User/
│   ├── login.md
│   ├── sign_up.md
│   └── account_update.md
│
├── 03_Content/
│   ├── search.md
│   ├── select_content.md
│   └── share.md
│
├── 04_Lead/
│   └── generate_lead.md
│
├── 05_Engagement/
│   ├── newsletter_subscribe.md
│   ├── wishlist_add.md
│   └── coupon_apply.md
│
└── 09_Templates/
    └── _evento_template.md
```

---

## Convenzioni File (v1)

### Frontmatter YAML obbligatorio

```yaml
---
title: ...
type: note                      # note | index | moc | glossary | template
tags: [...]
related: [...]
ga4_event: nome_evento          # nome ufficiale GA4
categoria: ecommerce            # ecommerce | user | content | lead | engagement | init
piattaforme: [GA4, Meta, GAds]  # piattaforme che leggono il push
data_creazione: 2026-05-29
last_updated: 2026-05-29
source_verified_on: 2026-05-29
fonti:
  - https://...
status: stable                  # stable | draft | review | deprecated
---
```

### Struttura nota standard

1. Frontmatter YAML
2. `# Titolo H1`
3. Intro 1-2 righe — quando si fa il push e perché
4. `## Script` — codice JavaScript pronto all'uso
5. `## Parametri` — tabella con Parametro | Descrizione | Tipo | Obbligatorio | Esempio
6. `## Piattaforme` — quali tag leggono questo push in GTM
7. `## Note GDPR` — consenso richiesto, PII coinvolti, condizioni di firing
8. `## Errori Comuni` — tabella Errore | Conseguenza | Fix
9. `## Riferimenti` — link ufficiali Google, Meta, TikTok

### Naming file

- Note evento: `nome_evento.md` (snake_case, nome GA4 esatto)
- MOC: `_MOC_NomeArea.md`
- Glossario: `_Glossario.md`
- Template: `_evento_template.md`
- Index: `00_Index.md`

---

## File (23 totali)

| Sezione | Count | Status |
|---------|-------|--------|
| Root (index, moc, glossario) | 5 | ✅ stable |
| 00_Init | 1 | ✅ stable |
| 01_Ecommerce | 11 | ✅ stable |
| 02_User | 3 | 🔲 stub |
| 03_Content | 3 | 🔲 stub |
| 04_Lead | 1 | 🔲 stub |
| 05_Engagement | 3 | 🔲 stub |
| 09_Templates | 1 | ✅ stable |

---

## Salute Vault (inizializzazione: 29 maggio 2026)

| Check | Stato |
|---|---|
| Wikilink rotti | ✅ 0 |
| Errori YAML | ✅ 0 |
| 00_Index.md aggiornato | ✅ |

---

## TODO / Prossimi passi

- [x] Completare note stub 01_Ecommerce (11 eventi)
- [ ] Completare note stub 02_User, 03_Content, 04_Lead, 05_Engagement
- [ ] Validare push su implementazione reale (Shopify o Magento)
- [ ] Integrare con Tracking Masterpiece come sezione operativa
