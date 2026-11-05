# Mappatura Nebrodi

Mappatura delle realtà produttive e delle risorse culturali nei 24 comuni del Parco dei Nebrodi, pensata per individuare possibili collaborazioni lungo la filiera della castagna: frutto, legno, buccia, riccio, foglie, corteccia, segatura e castagne non commerciabili.

- **261 realtà produttive**, divise in 10 macro-categorie.
- **58 risorse culturali** (macro-categoria 11): sagre, musei, monumenti, percorsi, tradizioni, associazioni e centri di educazione ambientale.

## Comuni mappati

**Messina:** Acquedolci, Alcara li Fusi, Capizzi, Caronia, Cesarò, Floresta, Galati Mamertino, Longi, Militello Rosmarino, Mistretta, Raccuja, Sant'Agata di Militello, Santa Domenica Vittoria, San Fratello, San Marco d'Alunzio, Santo Stefano di Camastra, San Teodoro, Tortorici, Ucria.

**Catania:** Bronte, Maniace, Randazzo.

**Enna:** Cerami, Troina.

## Contenuto del repository

| Percorso | Contenuto |
|---|---|
| `index.html` | L'applicativo: una scheda e un colore per ogni macro-categoria, legenda cliccabile, filtri per comune e disponibilità, campi da compilare, esportazione CSV e JSON |
| `data/produttive.json` | Le realtà produttive (macro-categorie 1–10) |
| `data/culturali.json` | Le risorse culturali (macro-categoria 11) |
| `download/mappatura_nebrodi.xlsx` | Excel completo: una scheda per macro-categoria, colori per categoria e legenda con i conteggi |
| `download/*.csv` | Gli stessi dati in CSV, con il punto e virgola come separatore |
| `.gitignore` | Esclude dal repository i file di sistema (`.DS_Store` del Mac e simili) |
| `.nojekyll` | Dice a GitHub Pages di pubblicare i file così come sono, senza elaborarli |

## Caricare su GitHub

**Dal terminale** (consigliato, carica anche i file nascosti):

```bash
cd mappatura-nebrodi-github
git init -b main
git add .
git commit -m "Mappatura Nebrodi: prima versione"
git remote add origin https://github.com/<utente>/<nome-repository>.git
git push -u origin main
```

**Dal sito di GitHub** (senza terminale): nel nuovo repository scegli **Add file → Upload files** e trascina il contenuto della cartella. Il Finder nasconde i file che iniziano con il punto: premi `Cmd + Shift + .` per vederli, così trascini anche `.gitignore` e `.nojekyll` e lasci fuori `.DS_Store`.

Prima di renderlo pubblico, tieni conto che i dati contengono nomi e numeri di telefono di ditte individuali. Sono presi da elenchi pubblici, ma se preferisci non ripubblicarli crea il repository come **Private** (GitHub Pages sui repository privati richiede un piano a pagamento).

## Pubblicare con GitHub Pages

1. Carica i file come descritto sopra.
2. Vai in **Settings → Pages**.
3. In **Source** scegli **Deploy from a branch**, poi il branch `main` e la cartella `/ (root)`, e salva.
4. Dopo un minuto circa la pagina è online all'indirizzo `https://<utente>.github.io/<nome-repository>/`.

Ogni macro-categoria ha un link diretto: per esempio `#m7` apre l'artigianato artistico e `#m11` le risorse culturali.

Aprendo `index.html` con doppio clic il browser blocca la lettura dei file JSON. Per provarlo sul computer avvia un piccolo server nella cartella, per esempio con `python3 -m http.server`, e apri `http://localhost:8000`.

## Dati in diretta dal Google Fogli

La pagina legge i dati direttamente dal Google Fogli condiviso, dalle schede 1–11 pubblicate sul web (File → Condividi → Pubblica sul web). Chi lavora nel foglio, o copia nel foglio una segnalazione arrivata dal modulo, la vede comparire sul sito dopo qualche minuto, senza toccare il repository. In alto nella pagina compare «Dati in diretta dal Google Fogli» con l'ora di lettura e il link «Modifica nel foglio».

In modalità diretta le colonne della pagina sono di sola lettura: si modifica solo nel foglio, così i dati restano in un posto solo.

Se il foglio non risponde, o non è più pubblicato, la pagina usa la copia in `data/` e lo segnala con «Copia salvata nel repository». Per aggiornare quella copia di riserva ogni tanto: apri la pagina, premi **Esporta dati (JSON)** e sostituisci i due file in `data/`.

Le impostazioni sono in cima allo script di `index.html`: `SHEET_PUB` è l'indirizzo del foglio pubblicato (lascialo vuoto, `""`, per usare solo `data/`), `SHEET_TABS` collega ogni macro-categoria al numero `gid` della sua scheda. Se aggiungi, rinomini o ricrei una scheda nel foglio, il nome non conta, ma il `gid` (il numero dopo `#gid=` nell'indirizzo della scheda) deve corrispondere, e la scheda deve essere tra quelle pubblicate.

La scheda «Risposte dal modulo» non è pubblicata e non compare sul sito: le segnalazioni vanno controllate e poi copiate nella scheda giusta.

## Compilare e aggiornare i dati (senza il foglio)

Le colonne con la matita (Lavorazione, Materia prima, Possibile collaborazione, Disponibilità, Note e, nella scheda 11, Possibile collegamento) si compilano direttamente nella pagina. Le modifiche restano **solo nel browser di chi le fa**: GitHub Pages ospita pagine statiche e non ha un database.

Per renderle definitive e condividerle con il gruppo:

1. Nella pagina premi **Esporta dati (JSON)**: scarica `produttive.json` e `culturali.json` con le modifiche incluse.
2. Sostituisci i file nella cartella `data/` del repository e fai un commit.
3. Chi apre la pagina vede i dati aggiornati. **Ripristina dati originali** cancella le modifiche locali e ricarica i file del repository.

Ogni record ha un `id` stabile: aggiungendo nuove righe a mano, usa un `id` nuovo e lo stesso schema degli altri record.

## Importare dati

Il pulsante **Importa dati** carica uno o più file insieme e riconosce da solo il formato:

| File | Da dove viene |
|---|---|
| `produttive.json`, `culturali.json` | **Esporta dati (JSON)** di questa pagina, anche da un altro computer |
| CSV della pagina | **Scarica CSV** di questa pagina |
| CSV di una scheda del Google Fogli | Nel foglio condiviso: apri la scheda, poi **File → Scarica → Valori separati da virgola (.csv)** |
| CSV delle risposte del modulo | Scheda **Risposte dal modulo**, scaricata allo stesso modo |

Una riga con lo stesso `id`, oppure con lo stesso nome e comune di una scheda esistente, aggiorna quella scheda; le altre diventano schede nuove. Nei CSV le celle vuote non cancellano i dati già presenti, tranne nelle colonne da compilare (Lavorazione, Materia prima, Possibile collaborazione, Disponibilità, Note, Possibile collegamento). Le righe senza nome o senza area vengono saltate. Le segnalazioni del modulo finiscono nella categoria «Segnalati con il modulo» della loro scheda.

Come le modifiche, i dati importati restano nel browser finché non premi **Esporta dati (JSON)** e carichi i due file nella cartella `data/` del repository.

## Fonti e limiti

- **Realtà produttive:** ricerche su Pagine Gialle per sottocategoria su ciascun comune, del 5 novembre 2026. Sono state tenute solo le attività con sede nei 24 comuni ed è stato scartato ciò che non era pertinente (negozi, imprese edili, sindacati e simili).
- **Risorse culturali:** schede dei comuni, centri visita e itinerari del sito del [Parco dei Nebrodi](https://www.parcodeinebrodi.it), più ricerche web. Ogni riga ha il link alla sua fonte.
- **Contatti e date:** sono quelli pubblicati online e vanno verificati prima di contattare le attività. Dove la fonte non indicava un dato (ad esempio l'organizzatore di una sagra) il campo dice "Da verificare".
- **Lacune note:** laboratori tessili, cosmetici e di biomateriali, aziende con castagneti, apicoltori, pro loco e fattorie didattiche sono poco presenti online e vanno integrati con altre fonti (Parco, GAL, consorzi, UNPLI).
