# Mapping criteri di ricerca: ricerche su manoscritti

```
TEMPLATE

## [titolo ricerca]

### Modello

Da <https://github.com/vedph/cadmus_tgr_doc/blob/master/models.md>:

### Proprietà utili per la ricerca
```





# Appunti vari per me


## Dallo schemone


    + filtri/ricerca avanzata \n sui dati di ogni MS, ad es.: \n dataz. da HistoricalDate, \n orig. da MsPlacesPart/MsPlace, \n scrittura \n da MsScriptsPart/MsScript/type \n [thesarus ms-script-types], \n mani da MsScriptsPart/MsHand/id, \n opere contenute \n da MsContentsPart/MsContent/ \n work [thesaurus \n author-work o note]
    + (quando nessun filtro \n è attivo, l'utente vede \n la lista con tutti i MSS)

## Da riunione 15 nov.

- Ricerche per
    - Localizzazione
    - Cronologia
    - Contenuto
    - Palinsesti 
    - Anche testo libero magari

Origine di questa nota: [2021-11-25_riunione_umanisti_visualizzaz_cadmus.md], par. "Manoscritti"




## Da e3 (lascio intatto qui)

(ho tolto a, che era ricerca libera, e l'ho editato e incollato sotto)

    b) filtri per ricerca avanzata:

        I) datazione (orig. dati: HistoricalDate) [fatto]

        II) origine geografica (orig. dati: MsPlacesPart > MsPlace) [fatto]

        III) scrittura (orig. dati: MsScriptsPart > MsScript > type = thesarus ms-script-types) [fatto]

        IV) mani (orig. dati: MsScriptsPart > MsHand > id) [fatto]

        IV) contenuti testuali (orig. dati: MsContentsPart > MsContent > work =
        thesaurus author-work o manually written string) → [fatto]

I risultati della ricerca dovrebbero apparire sempre come lista ordinata alfabeticamente sulla base della segnatura dei manoscritti (orig. dati: Metadata > Title). La ricerca dovrebbe poter funzionare sia che il campo libero di ricerca sia utilizzato sia che non lo sia (cioè se lo si lascia vuoto e si usano solo i filtri).

Origine di questa nota: [e3.md], punto 2




# A. Indicazioni generali

## Ricerca "bruta" per testo

Bisognerebbe indicizzare tutti i campi testuali degli item MSS: l'utente può fare una ricerca di testo libero che 'pesca' in tutte le parts che compongono gli items-manuscripts (e contengono testo).


## Ordine parts nel nostro model

- MsSignaturesPart [nessuna, ok]
- MsPlacesPart
- MsContentsPart
- MsUnitsPart
- MsScriptsPart
- MsFormalFeaturesPart [nessuna, ok]
- MsOrnamentsPart [nessuna, ok]
- MsHistoryPart

## Nessuna ricerca strutturata

Per le seguenti parti non è prevista nessuna rierca 'strutturata', ma solo ricerca libera sui campi testuali:

- MsSignaturesPart
- MsFormalFeaturesPart
- MsOrnamentsPart
- MsHistoryPart











# B. Ricerche strutturate








## MsPlacesPart

### Modello

Da <https://github.com/vedph/cadmus_tgr_doc/blob/master/models.md>:

- `places` (`MsPlace[]`):
  - `area`\* (`string`, thesaurus)
  - `address` (`string`)
  - `city` (`string`)
  - `site` (`string`)
  - `rank` (`number`): 0 if not used, else a rank to define the level of probability of this hypothesis (e.g. 1=most probable, 2=less probable, etc.).
  - `sources` (`DocReference[]`)

### Proprietà utili per la ricerca

- `places` (`MsPlace[]`):
  - `area`\* (`string`, thesaurus)
  - `city` (`string`)

*Nota*: Sto chiedendo a Elena e agli altri se vogliono includere anche `site`, ma per ora non lo includo. Una annotazione generale: non hanno ancora (per lo più) riempito le parts negli item dei MSS in Cadmus, quindi quando chiedo loro se una proprietà *sarà* popolata e utile in futuro, parlo appunto per lo più di quel che intendono fare poi, non di pratiche che hanno già in atto.






## MsContentsPart

### Modello

Da <https://github.com/vedph/cadmus_tgr_doc/blob/master/models.md>:

- `contents` (`MsContent[]`):
  - `start`\* (`MsLocation`)
  - `end`\* (`MsLocation`)
  - `work` (`string`, hierarchical thesaurus: `author-works`): author and work; this can be picked from a thesaurus, or manually written.
  - `location` (`string`)
  - `title` (`string`)
  - `incipit`\* (`string`)
  - `explicit`\* (`string`)
  - `editions` (`DocReference[]`): references to modern editions.
  - `note` (`string`)


### Proprietà utili per la ricerca

- `contents` (`MsContent[]`):
  - `work` (`string`, hierarchical thesaurus: `author-works`)
















## MsUnitsPart

### Modello

Da <https://github.com/vedph/cadmus_tgr_doc/blob/master/models.md>:

Codicological description. [...]


### Proprietà utili per la ricerca

- `units`: `MsUnit[]+` (codicological units):
  - `date` (`HistoricalDate`)
  - `palimpsests` (`MsPalimpsest[]`): the sheet(s) which are palimpsests inside this unit:
    - `date` (`HistoricalDate`)

*Nota*: Quel che ci interessa qui è la `HistoricalDate`. La ricerca a rigore non restituirà un MS, ma una unità codicologica di un MS, oppure (dato che c'è un altro `HistoricalDate` dentro `palimpsests`) di uno o più fogli riscritti dentro un MS. Il riferimento all'intero manoscritto andrà comunque mostrato.








## MsScriptsPart

### Modello

Da <https://github.com/vedph/cadmus_tgr_doc/blob/master/models.md>:

- `scripts` (`MsScript[]`):
  - `role`\* (`string`, thesaurus: `ms-script-roles`); e.g. mano principale, secondaria, scriptio superior, scriptio inferior...
  - `languages`\* (`string[]` [ISO 639-3](https://en.wikipedia.org/wiki/ISO_639-3), thesaurus: `ms-languages`): 1 or more languages.
  - `type` (`string`, hierarchical thesaurus: `ms-script-types`)
  - `hands` (`MsHand[]`+):
    - `id`\* (`string`)
    - `date` (`HistoricalDate`)
    - `start`\* (`MsLocation`)
    - `end`\* (`MsLocation`)
    - `description`\* (`string`)
    - `letters` (`MsHandLetter[]`):
      - `letter`\* (`string`)
      - `description` (`string`)
      - `imageId` (`string`)
    - `abbreviations` (`string`, MD)

### Proprietà utili per la ricerca

- `scripts` (`MsScript[]`):
  - `type` (`string`, hierarchical thesaurus: `ms-script-types`)
  - `hands` (`MsHand[]`+):
    - `id`\* (`string`)







