# SKYNET WebServices
SKYNET WebServices - Integrazione con i gestionali .NET

## Caratteristiche
La libreria permette al software gestionale di utilizzare la piattaforma SKYNET per la veicolazione allo SdI dei documenti contabili, nonché per l'immediata loro messa a disposizione al proprio commercialista.

### Gestione del ciclo attivo (VENDITE)
- Invio dei documenti contabili al SdI (Sistema di interscambio) di tutte le tipologie di fattura elettronica (B2G, B2B e B2C)
- Controllo dello stato di invio e recupero delle notifiche dello SdI (ricevuta consegna, notifica esito, etc.)
- Recupero dell'elenco documenti contabili inviati

### Gestione del ciclo passivo (ACQUISTO)
- Recupero dell'elenco dei documenti ricevuti tramite il canale SdI
- Recupero dei dati del singolo documento ricevuto ivi incluse lle notifiche di ricezione
- Gestione dell'accettazione/rifiuto delle fatture

## Installazione
SKYNET web services è su NuGet.

Dalla Package Console, in Visual Studio:

```PM> Install-Package Skynet.WebServices```

Oppure usare il comando equivalente nella UI di Visual Studio.

## Documentazione
### Specifiche
La libreriaè compatabile con la versione 3.0 delle specifiche di integrazione disponibili al link seguente:
https://sdsdsadsadsads/d.sad.sa.das.
### Esempi