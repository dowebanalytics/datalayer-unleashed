---
title: MOC — Ecommerce
type: moc
tags:
  - moc
  - ecommerce
  - ga4
  - funnel
data_creazione: 2026-05-29
last_updated: 2026-05-29
status: stable
---

# MOC — Ecommerce

Mappa degli 11 eventi ecommerce standard GA4 in ordine di funnel.

## Funnel completo

```
Listing pagina
  └── [[view_item_list]]     → impression prodotti in lista

Click prodotto
  └── [[select_item]]        → click su card prodotto

Scheda prodotto (PDP)
  └── [[view_item]]          → apertura PDP

Carrello
  ├── [[add_to_cart]]        → aggiunta al carrello
  ├── [[remove_from_cart]]   → rimozione dal carrello
  └── [[view_cart]]          → visualizzazione carrello

Checkout
  ├── [[begin_checkout]]     → inizio processo checkout
  ├── [[add_shipping_info]]  → selezione metodo spedizione
  └── [[add_payment_info]]   → selezione metodo pagamento

Conversione
  ├── [[purchase]]           → ordine completato
  └── [[add_to_wishlist]]    → aggiunta a wishlist

Post-vendita
  └── [[refund]]             → rimborso totale o parziale
```

## Regola ecommerce: null

**Prima di ogni evento ecommerce pushare sempre:**

```javascript
window.dataLayer.push({ ecommerce: null });
```

Questo azzera l'oggetto ecommerce nel modello GTM ed evita il merge con dati del push precedente.
Critico nelle SPA e in qualsiasi pagina dove più eventi ecommerce si susseguono senza reload.

## Note comuni

- `currency` è obbligatorio in tutti gli eventi con `value`. GA4 ignora `value` senza `currency`.
- `currency` deve essere in uppercase (ISO 4217): `EUR`, `USD`, non `eur`, `usd`.
- `items[]` è obbligatorio in tutti gli eventi ecommerce.
- `transaction_id` deve essere univoco per ogni `purchase`. GA4 deduplica su stesso ID nella stessa giornata.
- `value` = totale ordine. `tax` e `shipping` vanno separati.
