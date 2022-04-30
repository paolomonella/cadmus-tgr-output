# Mapping criteri di ricerca: ricerche testuali




## TokenTextPart

### Posizione nel mio schema UML

origine_dati → TokenTextPart

### Modello

Da <https://github.com/vedph/cadmus_doc/blob/master/web/help/general-parts.md#token-text>

### Proprietà utili per la ricerca

- Nessuna proprietà
- L'utente dovrebbe poter fare una ricerca per autore/opera (ad es. cerca questa parola solo nell'Ars di Prisciano). Ma come impostare questi filtri? Non abbiamo una tabella degli autori/opere grammaticali effettivamente presenti in Cadmus TGR. Attualmente gli item testuali hanno, in `metadata/group ID`, una stringa (testo a inserimento libero) come ad es. "ps-palaem-reg" per le *Regulae* dello Pseudo-Palemone. Esistono poi, in Cadmus, alcuni thesauri che potrebbero tornare utili, ma soprattutto c'è l'index di autori (e opere) grammaticali antichi (in file Word) curato da Michela e Elena.

### Ricerca "bruta" per testo: indicizzare

- Il testo base








## NotePart_traduzione

### Posizione nel mio schema UML

origine_dati → NotePart_traduzione

### Modello

Da <https://github.com/vedph/cadmus_doc/blob/master/web/help/general-parts.md#note>

- [note part](https://github.com/vedph/cadmus_doc/blob/master/web/help/general-parts.md#note) for translation, with `role`=`transl` and `tag`=language (`NotePart`).

### Proprietà utili per la ricerca

- Nessuna proprietà
- Ma l'utente dovrebbe poter fare una ricerca per autore/opera: vd. sopra per TokenTextPart

### Ricerca "bruta" per testo: indicizzare

- Ricerca libera sul testo della traduzione

*Nota*: Online ora ci c'è solo la traduzione inglese, per Prisciano (la cui traduzione italiana andrà solo a stampa), ma in futuro avremo anche traduzioni italiane di altre opere grammaticali online.








## apparatus_layer

### Posizione nel mio schema UML

origine_dati → apparatus_layer

### Modello

Da <https://github.com/vedph/cadmus_doc/blob/master/web/help/philology-parts.md#apparatus>:

Apparatus Model

- `tag`: an optional arbitrary string representing a categorization of some sort for that fragment, e.g. "margin", "interlinear", etc. This can be overridden by variants `tag`.

- `entries`: 1 or more variants/notes, each with these properties:

  - `type`: an enumerated constant to be chosen among replacement (0), addition before (1), addition after (2), note (3).
  - `value`: the variant's value. May be zero (empty or null) for deletions. Is optional (because not used) when `type` is note.
  - `tag`: an optional arbitrary string representing a categorization of some sort for that fragment, e.g. "margin", "interlinear", etc. It overrides the fragment's `tag`.
  - `normValue`: an optional normalized form derived from `value`. Normalization details are up to each single project, and the model makes no assumptions about it.
  - `note`: an optional annotation. When `type` is _note_, `value` has no meaning, and this property contains the note's text. Otherwise, this can be an additional note, side to side with the variant's value.
  - `witnesses`: optional array of annotated witnesses. Each has a `value` (e.g. `O`) and an optional note (e.g. `manus altera`).
  - `authors`: optional array of annotated authors. Each has a `value` (e.g. `Verg.` or `Wilamowitz`) and optional `tag` (e.g. `ancient` or `modern`), `location` (e.g. `Kleine Schriften p.12` or `Aen. 1.23`), and `note` (e.g. `exempli gratia`).
  - `isAccepted`: boolean, true if the variant represents the accepted text (=lemma).
  - `groupId`: an optional arbitrary ID to be used for grouping fragments in the layer together.

### Proprietà utili per la ricerca

- `entries`: 1 or more variants/notes, each with these properties:
  - `witnesses` / `value` (not the optional note, e.g. `manus altera`)
  - `authors` / `value` (not `tag` or `location` or `note`)

*Nota filter out*: nel gruppo PAGES c'è stata una discussione in cui io chiedevo di inserire `entries / witnesses / value`, e gli altri erano molto titubanti. Abbiamo trovato questo compromesso (dimmi tu quanto è realizzabile; ma se non è realizzabile, temo che dovremo togliere la ricerca per `witnesses` / `authors`): quando l'utente vede la nota di apparato per un passo, dovrebbe vedere *tutte* le varianti di *tutti* i MSS. Dovrebbe essergli però possibile "to gray out" (andare eliminando) i MSS che non gli interessano. Quindi se ci sono delle spunte da mettere in quadratini per filtrare le lezioni da vedere, l'apparato non dev'essere all'inizio vuoto, e l'utente va aggiungendo manoscritto; ma dev'essere all'inizio 'pieno' (con tutti i MSS) e l'utente va de-selezionando MSS per eliminarne le lezioni. Lo stesso dovrebbe valere per gli `authors`. Ma mentre lo scrivo, mi rendo conto però che questo si applica a una sorta di 'browse' e visualizzazione statica dell'apparato, non alla ricerca di cui stiamo parlando ora. Se è così, temo che dovremo escludere `witnesses` e `authors`, perché il grupppo PAGES non vuole che l'utente cerchi tutte le varianti del manoscritto X e veda tra i risultati solo quelle.

### Ricerca "bruta" per testo: indicizzare

Ricerca libera sul testo della variante, cioè su

- `entries`: 1 or more variants/notes, each with these properties:
  - `value`: the variant's value. May be zero (empty or null) for deletions. Is optional (because not used) when `type` is note.
  - `note`: an optional annotation. When `type` is _note_, `value` has no meaning, and this property contains the note's text. Otherwise, this can be an additional note, side to side with the variant's value.










## quotations_layer

### Posizione nel mio schema UML

origine_dati → quotations_layer

### Modello

Da <https://github.com/vedph/cadmus_tgr_doc/blob/master/models.md>:

VarQuotationsLayerFragment

- `quotations` (`VarQuotation[]`): quotations with variants:
  - `tag` (`string`, thesaurus: `quotation-tags`)
  - `authority`\* (`string`, thesaurus: `quotation-authorities`): the authority type (grammatical/linguistic)
  - `work`\* (`string`, hierarchical thesaurus: `author-works`): author and work.
  - `location`\* (`string`): location in the work (book, chapter, etc.)
  - `parallels` (`QuotationParallel[]`): further occurrences of the same quotation in other grammatical works:
    - `tag` (`string`, thesaurus: `quotation-tags`)
    - `work`\* (`string`, thesaurus: `author-works`): author and work.
    - `location`\* (`string`): location in the work (book, chapter, etc.)
  - `variants` (`QuotationVariant[]`): variant readings:
    - `lemma`\* (`string`): the lemma
    - `type`\* (`string`, enumerated type equal to that of the apparatus entry type)
    - `value`\* (`string`): the value (zero for deletions)
    - `witnesses` (`AnnotatedValue[]`):
      - `value`\* (`string`): e.g. "O"
      - `note` (`string`): e.g. "manus altera"
    - `authors` (`LocAnnotatedValue[]`):
      - `tag` (`string`): any optional classification for the author (e.g. ancient vs modern).
      - `value`\* (`string`): e.g. "Wilamowitz" or "Serv.Aen.": either freely typed, or picked from a thesaurus (`author-works`).
      - `location` (`string`): e.g. "Kleine Schriften, p.12" or "12, 587"
      - `note` (`string`): e.g. "exempli gratia"

### Proprietà utili per la ricerca

- `quotations` (`VarQuotation[]`): quotations with variants:
  - `work`\* (`string`, hierarchical thesaurus: `author-works`): author and work.
  - `authority`\* (`string`, thesaurus: `quotation-authorities`): the authority type (grammatical/linguistic)

*Nota*: Elena aveva scritto: "... + flag (facoltativo) per il tipo di autorità in virtù della quale è citata", facendo riferimento a `authority`. Non ho chiaro cosa intendesse per "facoltativo", ma io direi di introdurre comunque anche questo criterio di ricerca.


### Ricerca "bruta" per testo: indicizzare

L'utente può fare una ricerca libera sul testo citato. Quindi se Prisciano cita "Arma virumque cano" e noi tagghiamo che è del `work` "aen", l'utente può fare una ricerca incrociando, ad esempio:

- "virum" come ricerca bruta per testo
- `work` = l.v.verg.aen









## int_layer_paleogr_transcr

### Posizione nel mio schema UML

origine_dati → int_layer_paleogr_transcr

### Modello

Interpolations and transcriptions.
`role`="paleo"

- `interpolations` (`Interpolation[]`):
  - `type`\* (string, enumeration equal to that of the apparatus entry type)
  - `role`\* (`string`, thesaurus: `interpolation-roles`): "paleographic transcription", "gloss", "paratext".
  - `tag` (`string`, thesaurus: `interpolation-tags`)
  - `languages`\* (`string[]`, [ISO 639-3](https://en.wikipedia.org/wiki/ISO_639-3), thesaurus: `interpolation-languages`)
  - `value`\* (`string`)
  - `groupId` (`string`)
  - `note` (`string`)
  - `sources` (`ReadingSource[]`)
    - `witness`\* (`string`, thesaurus: `apparatus-witnesses`)
    - `handId` (`string`)
  - `quotations` (`VarQuotation[]`)

### Proprietà utili per la ricerca

- `interpolations` (`Interpolation[]`):
  - `sources` (`ReadingSource[]`)
    - `witness`\* (`string`, thesaurus: `apparatus-witnesses`)

*Nota*: anche qui, per `sources/witness`, vale la *Nota filter out* di sopra. Il gruppo PAGES non voleva che si potesse filtrare/cercare per testimone. Ma possiamo farlo se riesci a realizzare una sorta di approccio 'filter out'.

*Nota*: Per ora non ho inserito `interpolations/groupID` perché non so a cosa serva. Ho chiesto al gruppo PAGES se lo usano o pensano di usarlo. Mi ha risposto Elena:

> Sì, avevamo previsto la class groupID anche nell'Interpolations Layer (che appunto non è concepito solo per le interpolazioni) per poterla eventualmente utilizzare per raggruppare serie di glosse o interpolazioni che ricorrono identiche o molto simili in più witnesses. 

Le sto chiedendo a mia volta se pensi che sia il caso di creare una ricerca (strutturata o di 'testo libero') su questo campo, nonché se pensino di ancorare mai questo campo a un thesaurus. Al momento penso però di non includerlo nelle ricerche.


### Ricerca "bruta" per testo: indicizzare

- `interpolations` (`Interpolation[]`):
  - `value`\* (`string`)








## int_layer_glosses

### Posizione nel mio schema UML

origine_dati → int_layer_glosses

### Modello

Lo stesso di [#int_layer_paleogr_transcr].
`role`="gloss"

### Proprietà utili per la ricerca

- `interpolations` (`Interpolation[]`):
  - `sources` (`ReadingSource[]`)
    - `witness`\* (`string`, thesaurus: `apparatus-witnesses`)

*Nota*: anche qui, per `sources/witness`, vale la *Nota filter out* di sopra.

*Nota*: Per ora non ho inserito `interpolations/groupID` perché non so a cosa serva. Ho chiesto al gruppo PAGES se lo usano o pensano di usarlo.

### Ricerca "bruta" per testo: indicizzare

- `interpolations` (`Interpolation[]`):
  - `value`\* (`string`)








## int_layer_hum_interp

### Posizione nel mio schema UML

origine_dati → int_layer_hum_interp

### Modello

Lo stesso di [#int_layer_paleogr_transcr].
`role`="interp"

### Proprietà utili per la ricerca

- `interpolations` (`Interpolation[]`):
  - `sources` (`ReadingSource[]`)
    - `witness`\* (`string`, thesaurus: `apparatus-witnesses`)
  - `quotations` (`VarQuotation[]`)

*Nota*: anche qui, per `sources/witness`, vale la *Nota filter out* di sopra.

*Nota*: Per ora non ho inserito `interpolations/groupID` perché non so a cosa serva. Ho chiesto al gruppo PAGES se lo usano o pensano di usarlo.

### Ricerca "bruta" per testo: indicizzare

- `interpolations` (`Interpolation[]`):
  - `value`\* (`string`)








## linguistic_tags

### Posizione nel mio schema UML

origine_dati → linguistic_tags

### Modello

Da <https://github.com/vedph/cadmus_tgr_doc/blob/master/models.md>:

LingTagsLayerFragment

Tag: `fr.it.vedph.tgr.ling-tags`.

- `forms` (`LingTaggedForm[]`):
  - `lemmata` (`string[]`: optional normalized text forms
  - `dubious` (`boolean` (Thesaurus dubii sermonis)
  - `note` (`string`)
  - `tags` (`AnnotatedTag[]`):
    - `value`\* (`string`)
    - `notes` (`TaggedNote[]`):
      - `tag`\* (`string`)
      - `note`\* (`string`)

### Proprietà utili per la ricerca

- `forms` (`LingTaggedForm[]`):
  - `lemmata` (`string[]`: optional normalized text forms
  - `dubious` (`boolean` (Thesaurus dubii sermonis)
  - `tags` (`AnnotatedTag[]`):
    - `value`\* (`string`)

*Nota*: Elena mi aveva indicato di mettere un "flag (facoltativo) per le forme/categorie trattate come ‘dubbie’ dai grammatici antichi" (corrispondenti alla proprietà `dubious`) solo in combinazione con `forms/tags`. Non aveva dato questa indicazione anche per `forms/lemmata`. Forse però potremmo creare quella combinazione anche per `lemmata` (`dubious` + `forms/lemmata`): probabilmente viene anche più semplice.

### Ricerca "bruta" per testo: indicizzare

Nessuna: qui c'è solo ricerca strutturata. Ad es. l'utente riceve una lista di tutti i passaggi che parlano di
`a.lit.c.ancepslittera: consonans: anceps/liquida` (tratto dal thesaurus `ling-tags@en`)
