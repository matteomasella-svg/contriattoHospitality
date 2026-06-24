## 2EMME Apartments – Documentazione Ufficiale 2026

Interfaccia HTML interattiva per la gestione commerciale e informativa dei soggiorni 2EMME Apartments.

Il file consente di simulare costi, benefit, penali di recesso, calendario pulizie, tutela economica e principali condizioni contrattuali dei modelli di soggiorno 2026.

## Funzionalità principali

- simulatore soggiorno con:
  - check-in / check-out
  - numero notti
  - stagionalità
  - alloggio
  - modello contrattuale
  - modalità di pagamento
  - parcheggio / benefit mobilità
- calcolo automatico di:
  - soggiorno lordo
  - sconti tiered ADR
  - sconti per modalità pagamento
  - utenze / surcharge / forfait
  - imposta registro / bolli
  - pulizie intermedie
  - audit tecnico
  - pulizia finale
  - tassa soggiorno + servizio
- gestione logica 2026 di:
  - recesso anticipato
  - penali fisse per fascia durata
  - soglie 50% e 83%
  - planner operativo soggiorno
  - benefit maturati
  - timeline penale / recesso
- sezioni informative a fisarmonica su:
  - costi e garanzie
  - recesso anticipato
  - pulizie e audit
  - fair use / overuse
  - regole della casa
  - benefit
  - privacy / GDPR
  - contratto sintetico CAV

## Struttura del progetto

```bash
.
├── index.html
├── logo_correct.png
└── README.md
```

## Note di revisione pricing

La revisione del codice ha evidenziato tre punti da correggere prima di usare il simulatore come preventivatore definitivo:

1. **Tassa di soggiorno**: attualmente il calcolo considera 1 solo ospite. Va aggiunto un campo `Numero ospiti` e la formula deve diventare `9.5 * ospiti * min(notti, 14)`.
2. **Sconto tiered ADR**: la curva attuale può diventare troppo aggressiva perché applica `15% / 35% / 45%` moltiplicati per `discountPower`. Su Suite, ad esempio, la fascia 61+ può superare il 50% di sconto prima dei cap. La curva consigliata è più prudente: `8% / 18% / 25%` con cap rispettivi `10% / 22% / 30%`.
3. **Cap mensile proporzionale**: attualmente viene applicato anche ai soggiorni brevi. Va limitato ai soggiorni `30+` e solo al modello `Guaranteed`, altrimenti crea uno sconto nascosto anche su 1-13 notti.

## Patch consigliata per la logica sconti

```js
function getTierDiscountRate(tierName, discountPower) {
  const rawRates = {
    long: 0.08 * discountPower,
    extra: 0.18 * discountPower,
    smart: 0.25 * discountPower
  };
  const caps = {
    long: 0.10,
    extra: 0.22,
    smart: 0.30
  };
  return Math.min(rawRates[tierName] || 0, caps[tierName] || 0);
}
```

Formula tassa soggiorno consigliata:

```js
const guestCount = Math.max(1, parseInt(document.getElementById('guest-count').value || '1', 10) || 1);
const tax = 9.5 * guestCount * Math.min(nights, 14);
```

Applicazione corretta del cap mensile:

```js
const proportionalMonthlyCap = (config.monthlyCap / 30) * nights;
if (contractMode !== 'flex' && nights >= 30 && tieredNet > proportionalMonthlyCap) {
  tieredNet = proportionalMonthlyCap;
}
```
