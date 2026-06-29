# 2EMME Guest Portal

Modulo guest-facing per 2EMME Apartments.

## Scopo

Questo modulo unifica in un unico flusso:

- dati prenotazione;
- dati ospite;
- allergie e preferenze;
- selezione pack italiani;
- calcolo crediti benefit e upgrade;
- generazione contratto medium stay;
- caricamento documento ospite con compilazione assistita;
- salvataggio/caricamento bozza locale;
- stampa/PDF.

## Stato

MVP statico, pensato per GitHub Pages o Netlify.

Non richiede backend obbligatorio.
Non salva documenti ospite su GitHub.
I dati restano nel browser tramite localStorage, salvo esportazione/stampa manuale.

## File

```text
/guest-portal/index.html     MVP applicativo autosufficiente
/guest-portal/README.md      note operative
```

## Scelte progettuali

- `contriattoHospitality/index.html`: preventivatore ufficiale ospite.
- `contriattoHospitality/index_v3_revenue.html`: dashboard interna revenue.
- `contriattoHospitality/guest-portal/index.html`: portale ospite evoluto con pack, contratto e documento.
- `Cleaningapp`: resta separata per housekeeping, turni e sync prenotazioni.

## Privacy

Il caricamento documento nel MVP non deve essere inteso come archiviazione. L'immagine/testo devono essere verificati manualmente dall'operatore prima di qualsiasi uso amministrativo.

Per un uso produttivo con OCR cloud, firma digitale o pagamento, serve una fase successiva con backend, privacy policy aggiornata, retention e controllo accessi.
