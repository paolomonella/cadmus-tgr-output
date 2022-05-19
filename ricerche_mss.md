# Mapping criteri di ricerca: ricerche su manoscritti

# A. Indicazioni generali

## Ricerca "bruta" libera per testo

Bisognerebbe indicizzare tutti i campi testuali degli item MSS: l'utente può fare una ricerca di testo libero che 'pesca' in tutte le parts che compongono gli items-manuscripts (e contengono testo).

## In generale sulle ricerche strutturate

Cito da Elena, [e3.md](e3.md), punto 2:

~~~
I risultati della ricerca dovrebbero apparire sempre come lista ordinata alfabeticamente sulla base della segnatura dei manoscritti (orig. dati: Metadata > Title). La ricerca dovrebbe poter funzionare sia che il campo libero di ricerca sia utilizzato sia che non lo sia (cioè se lo si lascia vuoto e si usano solo i filtri).
~~~

## Parti senza ricerche strutturate

Per le seguenti parti non è prevista nessuna rierca 'strutturata', ma solo ricerca libera su tutti i campi testuali:

- MsFormalFeaturesPart
- MsOrnamentsPart
- MsHistoryPart










# B. Ricerche strutturate





## MsSignaturesPart

### Modello

See [Itinera](https://github.com/vedph/cadmus_itinera_doc/blob/master/models.md#mssignaturespart).

- signatures (`MsSignature[]`):
  - `tag` (`string`, thesaurus `ms-signature-tags`)
  - `city`\* (`string`)
  - `library`\* (`string`)
  - `fund` (`string`)
  - `location`\* (`string`)

### Proprietà utili per la ricerca

- signatures (`MsSignature[]`):
  - `city`\* (`string`)
  - `library`\* (`string`)
  - `fund` (`string`)

*Nota*: in un'email del 01/05/22, 10:11 Elena elena scrive:

> forse non sarebbe male poter consultare la lista delle signatures di mss compresi nella banca dati filtrando progressivamente city, library, fund e poi o facendo una ricerca libera sul solo campo location oppure visualizzando l'elenco delle segnature per i city - library - fund selezionati (es. tutti i Vat. lat., cfr. https://bvmm.irht.cnrs.fr/recherche/rechercheParVille.php ).




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
  - `site` (`string`)

*Nota*: in [README.md], paragrafo "Nuovi thesauri MsPlacesPart e MsSignature" chiediamo che `area`, `city` e `site` siano ora agganciati a dei thesauri (che dobbiamo ancora creare) di luoghi medievali di origine dei manoscritti.





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
