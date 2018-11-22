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
```PowerShell
PM> Install-Package Skynet.WebServices
```
Oppure usare il comando equivalente nella UI di Visual Studio.

## Documentazione
### Specifiche
La libreria è compatibile con [la versione 3.0 delle specifiche di integrazione disponibili di SKYNET](https://raw.githubusercontent.com/massivex/skynet-web-client-net/master/docs/20181115-SKYNET-API-30.pdf)

### Configurazione
Tutte le chiamate devono essere eseguito utilizzando la class `SkynetSso` come seguneche richiede in input l'indirizzo del server, la username e la password di accesso.
```cs
var skynetSso = new SkynetSso("https://sso.sediva.it", "gestionale@99999", "password");
```
In caso di errore i metodi ritornano un'eccezione di tipo `SkynetSsoException` che riporta il messaggio con la motivazione dell'errore (es. file XML non conforme alle spcifiche).

### Ciclo attivo
#### Invio di una fattura elettronica XML
```cs
var esitoCaricamento = skynetSso.InviaFatturaAttiva("c:\\temp\\IT00000000000_00000.xml");
// L'esito del caricamento ritorna l'id della fattura elettronica caricata
```

##### Recupero di una fattura attiva
```cs
var idFattura = "2d4ef"; // Codice alfanumerico della fattura attiva da recuperare
var notifiche = false;   // true per includere le notifiche nella risposta dal server
var fattturaAttiva = skynetSso.GetFatturaAttiva(new GetFatturaAttivaRequest { Id = idFattura, Notifiche = notifiche });
```

#### Elenco delle fatture attive
```cs
var year = 2018;    // Anno di filtro
var month = 5;      // Mese di filtro (da 1 a 12)
var elencoFattureAttive = skynetSso.ElencoFattureAttive(new ElencoFattureAttiveRequest { Year = year, Month = month });
```

### Ciclo passivo
#### Nuove fatture passive
Recupero dell'elenco delle fatture passive all'interno di un periodo di riferimento per le quali non è stato mai invocato il metodo di recupero.
```cs
var from = new DateTime(2018, 11, 1); // Data di inizio del periodo di filtro
var to = new DateTime(2018, 11, 30);  // Data di fine del periodo di filtro
var nuoveFatturePassive = skynetSso.NuoveFatturePassive(new FatturePassiveNuoveRequest { From = from, To = to });
```

#### Elenco fatture passive
Recupero dell'elenco delle fatture passive all'interno di un periodo di riferimento.
```cs
var from = new DateTime(2018, 11, 1); // Data di inizio del periodo di filtro
var to = new DateTime(2018, 11, 30);  // Data di fine del periodo di filtro
var elencoFatturePassive = skynetSso.ElencoFatturePassive(new ElencoFatturePassiveRequest { From = from, To = to });
```

#### Recupero fattura passiva
Recupero dei dati di dettaglio di una fattura passiva
```cs
var idFatturaPassiva = "13dw";
var getFatturaPassiva = skynetSso.GetFatturaPassiva(new GetFatturaPassivaRequest { Id = idFatturaPassiva });
```