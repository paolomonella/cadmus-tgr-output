# Mapping criteri di ricerca: ricerche su manoscritti

# A. Indicazioni generali

## Ricerca "bruta" per testo

Bisognerebbe indicizzare tutti i campi testuali degli item MSS: l'utente può fare una ricerca di testo libero che 'pesca' in tutte le parts che compongono gli items-manuscripts (e contengono testo).

## In generale sulle ricerche strutturate

Cito da Elena, [e3.md](e3.md), punto 2:

~~~
I risultati della ricerca dovrebbero apparire sempre come lista ordinata alfabeticamente sulla base della segnatura dei manoscritti (orig. dati: Metadata > Title). La ricerca dovrebbe poter funzionare sia che il campo libero di ricerca sia utilizzato sia che non lo sia (cioè se lo si lascia vuoto e si usano solo i filtri).
~~~

## Parti senza ricerche strutturate

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
