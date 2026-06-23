# Audit economico V2 - simulatore 2EMME Apartments 2026

## Obiettivo

Verificare la sostenibilita della nuova curva pricing introdotta in `index_v2.html`, con particolare attenzione a:

- sconto tiered ADR piu prudente;
- tassa soggiorno calcolata per numero ospiti;
- cap mensile applicato solo a soggiorni `30+` in modello `Guaranteed`;
- mantenimento del margine rispetto al floor prudente 60% occupancy.

## Assunzioni di calcolo

- Modello: `Guaranteed`
- Pagamento: settimanale, quindi senza ulteriore sconto pagamento
- Ospiti: 1
- Stagionalita: neutra, quindi ADR effettiva uguale ad ADR base
- Overuse e danni: 0
- Imposta forfettaria stimata: 6% del canone netto soggiorno
- La tassa di soggiorno non entra nel margine proprietario perche e una partita di giro
- Il servizio fisso e pari a 15 EUR
- Utenze, registro, pulizie e audit seguono le regole V2

## Curva sconti V2

| Fascia | Vecchia base | Nuova base | Cap V2 |
|---|---:|---:|---:|
| 14-29 notti | 15% x discountPower | 8% x discountPower | 10% |
| 30-60 notti | 35% x discountPower | 18% x discountPower | 22% |
| 61+ notti | 45% x discountPower | 25% x discountPower | 30% |

## Confronto sconto effettivo: vecchia logica vs V2

> Nota: la percentuale V2 e calcolata sul canone lordo e include l'effetto del cap mensile quando applicato.

| Alloggio | Notti | Vecchio sconto effettivo | Nuovo sconto effettivo V2 |
|---|---:|---:|---:|
| The NoLo Suite | 14 | 1.2% | 0.7% |
| The NoLo Suite | 30 | 10.5% | 5.6% |
| The NoLo Suite | 60 | 25.4% | 13.1% |
| The NoLo Suite | 90 | 34.2% | 18.3% |
| The NoLo Nest | 14 | 1.1% | 0.6% |
| The NoLo Nest | 30 | 9.2% | 11.8% |
| The NoLo Nest | 60 | 22.1% | 11.8% |
| The NoLo Nest | 90 | 29.7% | 16.0% |
| The NoLo Studio | 14 | 1.0% | 0.5% |
| The NoLo Studio | 30 | 8.7% | 16.7% |
| The NoLo Studio | 60 | 21.0% | 16.7% |
| The NoLo Studio | 90 | 28.2% | 16.7% |
| The NoLo Heritage | 14 | 0.8% | 0.4% |
| The NoLo Heritage | 30 | 6.4% | 3.4% |
| The NoLo Heritage | 60 | 15.5% | 8.0% |
| The NoLo Heritage | 90 | 20.8% | 11.2% |

## Scenari economici V2

| Alloggio | Notti | ADR base | Lordo | Netto soggiorno | Sconto eff. | Netto/gg dopo 6% | Floor | Delta vs floor | Margine netto stimato | Cap applicato |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---|
| The NoLo Suite | 14 | EUR 95 | EUR 1330.00 | EUR 1320.66 | 0.7% | EUR 88.71 | EUR 11.94 | EUR 76.77 | EUR 1080.92 | no |
| The NoLo Suite | 30 | EUR 95 | EUR 2850.00 | EUR 2690.50 | 5.6% | EUR 84.30 | EUR 11.94 | EUR 72.36 | EUR 2199.26 | no |
| The NoLo Suite | 60 | EUR 95 | EUR 5700.00 | EUR 4955.00 | 13.1% | EUR 77.56 | EUR 11.94 | EUR 65.62 | EUR 4128.50 | no |
| The NoLo Suite | 90 | EUR 95 | EUR 8550.00 | EUR 6982.50 | 18.3% | EUR 72.91 | EUR 11.94 | EUR 60.97 | EUR 6042.30 | no |
| The NoLo Nest | 14 | EUR 85 | EUR 1190.00 | EUR 1183.20 | 0.6% | EUR 79.44 | EUR 9.40 | EUR 70.04 | EUR 958.05 | no |
| The NoLo Nest | 30 | EUR 85 | EUR 2550.00 | EUR 2250.00 | 11.8% | EUR 70.50 | EUR 9.40 | EUR 61.10 | EUR 1794.00 | si |
| The NoLo Nest | 60 | EUR 85 | EUR 5100.00 | EUR 4500.00 | 11.8% | EUR 70.50 | EUR 9.40 | EUR 61.10 | EUR 3714.00 | si |
| The NoLo Nest | 90 | EUR 85 | EUR 7650.00 | EUR 6427.50 | 16.0% | EUR 67.15 | EUR 9.40 | EUR 57.75 | EUR 5523.64 | no |
| The NoLo Studio | 14 | EUR 90 | EUR 1260.00 | EUR 1253.16 | 0.5% | EUR 84.14 | EUR 8.25 | EUR 75.89 | EUR 1020.31 | no |
| The NoLo Studio | 30 | EUR 90 | EUR 2700.00 | EUR 2250.00 | 16.7% | EUR 70.50 | EUR 8.25 | EUR 62.25 | EUR 1794.00 | si |
| The NoLo Studio | 60 | EUR 90 | EUR 5400.00 | EUR 4500.00 | 16.7% | EUR 70.50 | EUR 8.25 | EUR 62.25 | EUR 3714.00 | si |
| The NoLo Studio | 90 | EUR 90 | EUR 8100.00 | EUR 6750.00 | 16.7% | EUR 70.50 | EUR 8.25 | EUR 62.25 | EUR 5825.00 | si |
| The NoLo Heritage | 14 | EUR 80 | EUR 1120.00 | EUR 1116.86 | 0.4% | EUR 74.90 | EUR 9.98 | EUR 64.92 | EUR 897.81 | no |
| The NoLo Heritage | 30 | EUR 80 | EUR 2400.00 | EUR 2318.67 | 3.4% | EUR 72.64 | EUR 9.98 | EUR 62.66 | EUR 1856.78 | no |
| The NoLo Heritage | 60 | EUR 80 | EUR 4800.00 | EUR 4415.82 | 8.0% | EUR 69.18 | EUR 9.98 | EUR 59.20 | EUR 3636.57 | no |
| The NoLo Heritage | 90 | EUR 80 | EUR 7200.00 | EUR 6398.58 | 11.2% | EUR 66.80 | EUR 9.98 | EUR 56.82 | EUR 5492.09 | no |

## Lettura dei risultati

### 1. Sostenibilita generale

Tutti gli scenari testati restano sopra il floor prudente 60% occupancy. La V2 non mette in crisi la sostenibilita economica dei soggiorni 14, 30, 60 e 90 notti.

### 2. Cap mensile

Il cap mensile interviene soprattutto su Nest e Studio, dove l'ADR base e relativamente alto rispetto al cap impostato:

- Nest: cap applicato a 30 e 60 notti.
- Studio: cap applicato a 30, 60 e 90 notti.
- Suite: cap non applicato negli scenari testati.
- Heritage: cap non applicato negli scenari testati.

Questo significa che per Nest e Studio il vero limite commerciale non e solo la curva sconto, ma anche il `monthlyCap`.

### 3. Sconto tier

La vecchia curva era troppo aggressiva soprattutto per la fascia 61+ notti, perche moltiplicava fino al 45% per il `discountPower`.
La V2 mantiene una progressivita commerciale ma evita sconti superiori al 30% di fascia.

### 4. Pagamento anticipato

La V2 riduce anche lo sconto pagamento:

- mensile anticipato: 3%
- totale anticipato: 6%

La vecchia logica usava 5% e 10%, che sommati allo sconto tier potevano abbassare troppo il canone netto.

## Raccomandazioni operative

### Suite

ADR base 95 EUR sostenibile.
Per soggiorni lunghi la Suite resta sopra floor anche senza cap applicato. Consiglio di non abbassare l'ADR base sotto 90 EUR in bassa stagione e di usare rialzi stagionali nei mesi estivi.

### Nest

ADR base 85 EUR sostenibile, ma il cap mensile da 2.250 EUR e molto influente.
Se vuoi proteggere il margine su 30-60 notti, valuta cap mensile 2.350-2.450 EUR oppure mantieni 2.250 EUR come leva commerciale.

### Studio

ADR base 90 EUR sostenibile, ma cap mensile 2.250 EUR applicato su 30/60/90 notti.
Per lo Studio, che ha posizionamento luxury 6 piano, il cap potrebbe essere troppo basso. Consiglio test a 2.400-2.500 EUR.

### Heritage

ADR base 80 EUR sostenibile e curva molto prudente grazie a `discountPower` 0.70.
Qui non serve ridurre ulteriormente gli sconti. Si puo valutare ADR 85 EUR nei periodi di domanda alta.

## Decisione consigliata

La V2 e economicamente piu equilibrata della versione originale.
Prima di sostituire `index.html`, si consiglia di validare manualmente questi casi:

1. 2 ospiti per 14 notti;
2. 2 ospiti per 30 notti;
3. Studio 60 notti con cap 2.250 vs 2.450;
4. Nest 60 notti con cap 2.250 vs 2.400;
5. Suite 90 notti in alta stagione.

## Prossimi step tecnici

- Usare `index_v2.html` come ambiente di validazione.
- Dopo conferma commerciale, sostituire `index.html` con la V2.
- Eventualmente separare configurazione prezzi e regole in `pricing-config.js`.
