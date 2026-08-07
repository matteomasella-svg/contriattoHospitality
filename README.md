# 2EMME Apartments — Documentazione Ufficiale 2026

Repository canonico per la documentazione commerciale e contrattuale dei soggiorni **2EMME Apartments**.

## Documento contrattuale corrente

Il **Master contrattuale vigente** è:

`MASTER/Accordo_di_Soggiorno_2EMME_Apartments_v1.0.md`

- Versione: **1.0**
- Stato: **APPROVED / CANONICAL MASTER**
- Data di consolidamento: **7 agosto 2026**
- Ambito: strutture esercitate come Case e Appartamenti per Vacanze (CAV) in forma imprenditoriale.

Il Master disciplina il rapporto generale di ospitalità temporanea. Non costituisce contratto di locazione abitativa.

### Regola di prevalenza

Per ogni singolo soggiorno, la versione dell'Accordo effettivamente sottoscritta dall'Ospite e archiviata digitalmente insieme al Riepilogo della Prenotazione, agli allegati applicabili e alle evidenze di firma costituisce **l'unica versione contrattuale valida per quel soggiorno**.

La homepage `index.html` è l'implementazione operativa/interattiva del sistema 2026 e **non sostituisce il Master testuale**.

## Gerarchia documentale ufficiale

```text
contriattoHospitality/
├── MASTER/
│   └── Accordo_di_Soggiorno_2EMME_Apartments_v1.0.md
├── ALLEGATI/
│   └── README.md
├── TEMPLATE_FIRMABILE/
│   └── README.md
├── ARCHIVE/
│   └── README.md
├── index.html
├── index_v2.html
├── index_v3_revenue.html
├── backup_index_old.html
├── logo_correct.png
└── README.md
```

### Funzione delle cartelle

**MASTER/**  
Contiene il testo contrattuale canonico vigente. Qualunque revisione sostanziale deve produrre una nuova versione numerata.

**ALLEGATI/**  
Contiene o indicizza Informativa Privacy, Fair Use Policy, Regole della Casa, Carta dell'Ospitalità Consapevole, Green Policy e Schede delle Strutture.

**TEMPLATE_FIRMABILE/**  
Definisce la composizione del pacchetto che viene presentato all'Ospite: Riepilogo Prenotazione, accordo sintetico, documentazione richiamata e log di firma.

**ARCHIVE/**  
Contiene esclusivamente versioni superate. Nessun file archiviato deve essere utilizzato per nuove prenotazioni.

## Stato delle versioni HTML

- `index.html` — **homepage operativa ufficiale**, derivata dalla V2 e promossa a homepage il 24 giugno 2026.
- `index_v2.html` — sorgente/versione V2 conservata per tracciabilità.
- `index_v3_revenue.html` — dashboard interna e strumenti revenue; non è il master contrattuale.
- `backup_index_old.html` — versione precedente archiviata; non utilizzare come riferimento corrente.

## Flusso contrattuale 2EMME Apartments

1. Creazione del **Riepilogo della Prenotazione** con dati dell'Ospite, struttura, periodo, modello di soggiorno e condizioni economiche.
2. Identificazione dell'Ospite.
3. Messa a disposizione del **Master/Condizioni Generali** e degli allegati applicabili.
4. Presentazione dell'**Accordo di Soggiorno sintetico firmabile**.
5. Accettazione e firma mediante procedura digitale/OTP o altra modalità adottata dal Gestore.
6. Registrazione di versione Master, versioni allegati, data, ora, identificativo pratica e log di accettazione.
7. Archiviazione del pacchetto sottoscritto come versione valida del singolo soggiorno.

## Funzionalità dell'interfaccia operativa

L'interfaccia HTML consente di simulare e gestire:

- check-in / check-out;
- numero notti;
- stagionalità;
- alloggio;
- modello contrattuale;
- modalità di pagamento;
- parcheggio / benefit mobilità;
- soggiorno lordo;
- sconti tiered ADR;
- sconti per modalità pagamento;
- utenze / surcharge / forfait;
- imposta registro / bolli;
- pulizie intermedie;
- audit tecnico;
- pulizia finale;
- tassa soggiorno + servizio;
- recesso anticipato;
- garanzie;
- Fair Use / Overuse;
- Regole della Casa;
- benefit;
- privacy / GDPR;
- contratto sintetico CAV.

## Note di revisione pricing

La revisione del codice ha evidenziato tre punti da correggere prima di usare il simulatore come preventivatore definitivo:

1. **Tassa di soggiorno**: il calcolo deve considerare il numero effettivo degli ospiti e le regole vigenti applicabili.
2. **Sconto tiered ADR**: la curva deve essere mantenuta entro cap prudenziali per evitare sconti eccessivi.
3. **Cap mensile proporzionale**: deve essere applicato solo quando coerente con durata e modello contrattuale.

### Patch consigliata per la logica sconti

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

### Controllo delle modifiche contrattuali

Ogni modifica sostanziale al Master deve:

1. incrementare il numero di versione;
2. indicare la data di efficacia;
3. aggiornare questo README;
4. spostare la versione precedente in `ARCHIVE/` senza eliminarla;
5. verificare la coerenza di `index.html`, template firmabile e allegati;
6. evitare modifiche retroattive ai pacchetti già sottoscritti.

---

**Canonical Contract Master:** `MASTER/Accordo_di_Soggiorno_2EMME_Apartments_v1.0.md`