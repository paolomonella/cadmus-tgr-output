---
Description: Scaricato da https://raw.githubusercontent.com/vedph/cadmus_itinera_doc/master/models.md il 24.04 2022
---

# Cadmus Itinera Models

- [Cadmus Itinera Models](#cadmus-itinera-models)
  - [Common Models](#common-models)
    - [Attachment](#attachment)
    - [Chronotope](#chronotope)
    - [CitedPerson](#citedperson)
    - [DecoratedCount](#decoratedcount)
    - [DecoratedId](#decoratedid)
    - [DocReference](#docreference)
    - [MsLocation](#mslocation)
    - [MsLocationRange](#mslocationrange)
    - [PersonName](#personname)
    - [PhysicalDimension](#physicaldimension)
    - [PhysicalSize](#physicalsize)
  - [Letter Item](#letter-item)
  - [Correspondent Item](#correspondent-item)
  - [Poetic Text Item](#poetic-text-item)
  - [Manuscript Item](#manuscript-item)
  - [Parts](#parts)
    - [AttachmentsPart](#attachmentspart)
    - [ChronotopicsPart](#chronotopicspart)
    - [CitedPersonsPart](#citedpersonspart)
    - [LitDedicationsPart](#litdedicationspart)
    - [CorrExchangesPart](#correxchangespart)
    - [DocReferencesPart](#docreferencespart)
    - [ExtBibliographyPart](#extbibliographypart)
    - [SerialTextInfoPart](#serialtextinfopart)
    - [MsBindingPart](#msbindingpart)
    - [MsCatchwordsPart](#mscatchwordspart)
    - [MsCompositionPart](#mscompositionpart)
    - [MsContentLociPart](#mscontentlocipart)
    - [MsContentsPart](#mscontentspart)
    - [MsDecorationsPart](#msdecorationspart)
    - [MsHandsPart](#mshandspart)
    - [MsHistoryPart](#mshistorypart)
    - [MsLayoutsPart](#mslayoutspart)
    - [MsMaterialDscPart](#msmaterialdscpart)
    - [MsNumberingsPart](#msnumberingspart)
    - [MsPlacePart](#msplacepart)
    - [MsPoemRangesPart](#mspoemrangespart)
    - [MsQuiresPart](#msquirespart)
    - [MsSignaturesPart](#mssignaturespart)
    - [MsWatermarksPart](#mswatermarkspart)
    - [PersonEventsPart](#personeventspart)
    - [PersonPart](#personpart)

In what follows I adopt these conventions:

- each type name is followed by its type in parentheses; if the type is drawn from a taxonomy, the word "thesaurus" is added (this is the internal name of a taxonomy in Cadmus).
- the type name marked by asterisk means that it requires a value.
- data types followed by `[]` mean an array, i.e. a list of such data. For instance, `string[]` = a list of `string`'s. For strings, `MD` means Markdown, i.e. a lightweight markup system providing essential formatting; this practically means that you can add formatting to the text, like e.g. italic or bold.
- custom types are defined with a name (e.g. `HistoricalDate`), and described only the first time they are introduced in the document; if they are types already present in the Cadmus "stock" models, there is no description but a link to the documentation.

In general, this architecture is targeted to modular content creation. The usual flow is creating highly structured and modular data using Cadmus, and then automatically build a relational DB from them, optimized for the search types we're going to support, plus LOD "extractions" for connecting the relevant parts of our data to the semantic web.

There are 4 items in the Cadmus DB:

- _letters_: data about letters (not their text);
- _correspondents_ of the letters;
- _poetic texts_ related to the letters;
- _manuscripts_.

About 30 part types are variously assigned to those items.

## Common Models

Some commonly reused (sub-part) models are listed here.

### Attachment

- `Attachment`:
  - `id` (`string`): an arbitrary ID.
  - `externalIds` (`string[]`)
  - `type`\* (`string`; thesaurus `epist-attachment-types`: manuscript, work)
  - `name`\* (`string`; if work, use thesaurus of works): not specified if unindentified.
  - `portion` (`string`): the specification of the portion of the attachment. For instance, if the attachment is a work, this specifies the work's location (e.g. Aen. 1.13-2.26).
  - `isLost` (`boolean`)
  - `isUnknown` (`boolean`)
  - `note`: you can use this when the object is not identified to provide an informal description.

### Chronotope

- `Chronotope`:
  - `tag`\* (`string`)
  - `place` (`string`)
  - `isPlaceDubious` (`boolean`)
  - `date`\* (`HistoricalDate`)
  - `textDate` (`string`): the attested text form of the date. It might also be different from the reconstructed one.
  - `sources` (`DocReference[]`)

Note that here and in other parts the _place just corresponds to a conventional name_ (e.g. `Napoli`). This is not a full-fledged geographic model, but just a name; including data like coordinates here would not be an option, because this would imply duplicating (i.e. re-entering and re-storing) them wherever the same name occurs. Rather, coordinates will be later automatically deduced from the name using a geolocation service like Google. We must thus ensure that the place name can be located without issues (eventually by enriching our geolocation request with restrictions, e.g. "in Italy" or the like).

### CitedPerson

- `CitedPerson`: a person cited in a literary source:
  - `name` (`PersonName`)
  - `rank` (`short`)
  - `ids` (`DecoratedId[]`)
  - `sources` (`DocReference[]`)

### DecoratedCount

- `DecoratedCount`:
  - `id` (`string`)
  - `value` (`int`)
  - `note` (`string`)

### DecoratedId

- `DecoratedId`:
  - `id` (`string`)
  - `rank`: a numeric rank to sort identifications in their order of probability. For a single identification, just leave the rank value equal (to 0). Otherwise, use 1=highest probability, 2=lower than 1, and so on.
  - `tag` (`string`)
  - `sources` (`DocReference[]`)

### DocReference

- `DocReference`: a literary citation:
  - `tag` (`string`; thesaurus `doc-reference-tags`)
  - `author`\* (`string`)
  - `work`\* (`string`)
  - `location` (`string`; e.g. "2.34")
  - `note` (`string`, 500)

### MsLocation

- `MsLocation`: a location in a manuscript:
  - `n`\* (`int`): sheet number.
  - `r` (`bool`): true if Roman number.
  - `s` (`string`): the suffix, with 0-2 lowercase letters (e.g. `r`=recto, `v`=verso, `rv`=both).
  - `l` (`int`): line number.

### MsLocationRange

- `MsLocationRange`: a range of manuscript's locations:
  - `start`: `MsLocation`
  - `end`: `MsLocation`

### PersonName

- `PersonName`: a personal name:
  - `language`\* (`string` = code from [ISO 639-3](https://en.wikipedia.org/wiki/ISO_639-3), thesaurus `person-name-languages`)
  - `tag` (`string`, thesaurus `person-name-tags`): optional tag used to group names, typically used when a person has several names.
  - `parts`\* (`PersonNamePart[]`):
    - `type`\* (`string`, thesaurus `person-name-types`): e.g. first name, last name, etc. Types are not unique in a name: for instance, you might have a person with 2 first names.
    - `value`\* (`string`)

### PhysicalDimension

This and the following sub-models come from the general Cadmus parts.

- `PhysicalDimension`:
  - `tag` (`string`)
  - `value`\* (`number`, decimal)
  - `unit`\* (`string`, thesaurus `physical-size-units`)

### PhysicalSize

- `PhysicalSize`:
  - `tag` (`string`)
  - `w` (`PhysicalDimension`)
  - `h` (`PhysicalDimension`)
  - `d` (`PhysicalDimension`)
  - `note` (`string`)

At least 1 among `w`/`h`/`d` should be specified.

## Letter Item

The letter item has 7 part types:

- `AttachmentsPart`: letter's attachments (`it.vedph.itinera.attachments`).
- `ChronotopicsPart`: date and place (`it.vedph.itinera.chronotopics`).
- `CitedPersonsPart`: persons cited in the letter (`it.vedph.itinera.cited-persons`).
- `DocReferencesPart`: references to documents (`it.vedph.itinera.doc-references`).
- `ExtBibliographyPart`: bibliography (`it.vedph.ext-bibliography`).
- `NotePart`: general purpose note (`it.vedph.note`).
- `SerialTextInfoPart`\*: essential metadata about a letter (`it.vedph.itinera.letter-info`).

## Correspondent Item

The correspondent item has 9 part types:

- `CorrExchangesPart`: exchanges of works, manuscripts or other objects involving the correspondent (`it.vedph.itinera.corr-exchanges`).
- `DocReferencesPart`: references made by author or references made by correspondent. A role distinguishes the two usages (`it.vedph.itinera.doc-references` with roles `auth` and `corr`).
- `ExtBibliographyPart`: bibliography (`it.vedph.ext-bibliography`).
- `LitDedicationsPart`: literary dedications (`it.vedph.itinera.lit-dedications`).
- `NotePart`: general purpose note (`it.vedph.note`).
- `PersonEventsPart`: events in a person's life (`it.vedph.itinera.person-events`).
- `PersonPart`\*: biographic data (`it.vedph.itinera.person`).
- `PersonWorksPart`: works (`it.vedph.itinera.person-works`).

Note about _correspondents of correspondents_: given that their model is equal to or a subset of the author's correspondents, it makes more sense to just treat them as author's correspondents. That is, instead of having a _nested_ list of correspondents of correspondents inside each correspondent (thus building a recursive nesting), we would just keep a plain, _flat_ list of correspondents. Some of them would be correspondents of the reference author (here Petrarch); others would be correspondents of the correspondent X.

We can then just use these models, adding a _group ID_ to the correspondent item, with a value equal to their reference correspondent ID.

Each item in Cadmus can have a group ID for general purpose grouping, e.g. grouping a set of texts belonging to the same work (fragmented to be more manageable); a set of lemmata under the same letter in a dictionary; etc. In this case, we would e.g. have the correspondent with `id`=`barbato`, and all his correspondents would be stored just like any other correspondent. The only difference is that their group ID would be `barbato`. We can thus keep a much simpler "flat" list of correspondents, each with a reference correspondent, arbitrarily chosen according to the project's purposes. In this case, the default correspondent is Petrarch, with no group ID; correspondents of correspondents have the group ID of their reference correspondent. The advantages are:

- avoid repeating parts of the correspondents model inside itself, with a redundant and potentially recursive structure.
- keep the data architecture flat, as a single list of correspondents, thus easing indexing and searching.
- allow the full data model of correspondents also for correspondents of correspondents, even though usually they will just use a subset of them. This allows for future or occasional expansions where required, without having to change the nested model.

## Poetic Text Item

The poetic text item has 6 parts:

- `AttachmentsPart`: letter's attachments (`it.vedph.itinera.attachments`).
- `ChronotopicsPart`: date and place (`it.vedph.itinera.chronotopics`).
- `CitedPersonsPart`: persons cited in the text (`it.vedph.itinera.cited-persons`).
- `ExtBibliographyPart`: bibliography (`it.vedph.ext-bibliography`).
- `NotePart`: general purpose note (`it.vedph.note`).
- `SerialTextInfoPart`\*: essential metadata about a text.

## Manuscript Item

The manuscript item has 20 parts:

- `ExtBibliographyPart`: bibliography (`it.vedph.ext-bibliography`).
- `HistoricalDatePart`: datatation (`it.vedph.historical-date`).
- `MsBindingPart`: binding (`it.vedph.itinera.ms-binding`).
- `MsCatchwordsPart`: catchwords (`it.vedph.itinera.ms-catchwords`).
- `MsCompositionPart`: composition (`it.vedph.itinera.ms-composition`).
- `MsContentLociPart`: "loci critici" (`it.vedph.itinera.ms-content-loci`).
- `MsContentsPart`: contents (`it.vedph.itinera.ms-contents`).
- `MsDecorationsPart`: decorations (`it.vedph.itinera.ms-decorations`).
- `MsHandsPart`: hands (`it.vedph.itinera.ms-hands`).
- `MsHistoryPart`: history of the MS (`it.vedph.itinera.ms-history`).
- `MsLayoutsPart`: layouts (`it.vedph.itinera.ms-layouts`).
- `MsMaterialDscPart`: material description (`it.vedph.itinera.ms-material-dsc`).
- `MsNumberingsPart`: numberings (`it.vedph.itinera.ms-numberings`).
- `MsPlacePart`: place of origin (`it.vedph.itinera.ms-place`).
- `MsPoemRangesPart`: poem's ranges in a manuscript (`it.vedph.itinera.ms-poem-ranges`).
- `MsQuiresPart`: quires (`it.vedph.itinera.ms-quires`).
- `MsSignaturesPart`: signature(s) (`it.vedph.itinera.ms-signatures`).
- `MsWatermarksPart`: watermarks (`it.vedph.itinera.ms-watermarks`).
- `NotePart`: general purpose note (`it.vedph.note`).

## Parts

### AttachmentsPart

Attachments linked to a letter or poetic text.

- `attachments` (`Attachment[]`)

Thesauri: `epist-attachment-types`.

### ChronotopicsPart

Spatial and temporal coordinates for a letter or a related poetic text.

- chronotopes (`Chronotope[]`)

Thesauri: `chronotope-tags`, `doc-reference-tags`.

### CitedPersonsPart

- `persons` (`CitedPerson[]`):
  - `name` (`PersonName`)
  - `ids` (`DecoratedId[]`)
  - `sources` (`DocReference[]`)

Thesauri: `person-name-languages`, `person-name-tags`, `person-name-types`, `person-id-tags`.

### LitDedicationsPart

Literary dedications.

- `dedications` (`LitDedication[]`):
  - `title`\* (`string`)
  - `date` (`HistoricalDate`)
  - `dateSent` (`HistoricalDate`)
  - `participants` (`DecoratedId[]`): the subjects partecipating in the dedication (e.g. dedicator, dedicatee, etc.).
  - `sources` (`DocReference[]`)

Thesauri: `doc-reference-tags`.

### CorrExchangesPart

Exchanges from the reference author to the correspondent, or vice-versa.

- `exchanges` (`CorrExchange[]`) of works/manuscripts with author:
  - `isDubious` (`boolean`)
  - `isIndirect` (`boolean`)
  - `isFromParticipant` (`boolean`): the "direction" of the exchange: true when the attachment is coming from 1 or more of the participants; false when it is coming from the correspondent (represented by the container item) to the participants.
  - `chronotopes`\* (`Chronotope[]`): from, to, and other chronotopic indications.
  - `participants` (`DecoratedId[]`):
    - `id` (`string`): the participant ID. This should refer to a person part.
    - `tag` (`string`, thesaurus): the role of the participant (e.g. destinatario, latore...).
  - `sources` (`DocReference[]`)
  - `attachments` (`Attachment[]`)

Thesauri: `doc-reference-tags`, `chronotope-tags`, `epist-attachment-types`.

### DocReferencesPart

A list of document references (literary citations, short bibliographic references, etc.).

- `references` (`DocReference[]`):
  - `tag`: any classification tag meaningful in the data context.
  - `author`: the author ID (e.g. `Hom.`). For archive documents, it can be a constant reserved ID. For bibliographic references, it's the modern author ID.
  - `work`: the work ID (e.g. `Il.`). For archive documents, it can be the archive name. For bibliographic references, it's the modern work's title ID.
  - `location`: the work's location (e.g. `12.34`). For archive documents, it can be their location in the archive (e.g. a signature). For bibliographic references, it's usually a page number or other means of locating some passage.
  - `note`: a generic annotation.

Thesauri: `doc-reference-tags`.

### ExtBibliographyPart

External bibliography. This part establishes a link between its item and an external, read/write bibliographic repository.

- `entries` (`ExtBibEntry[]`):
  - `id` (`string`): the identifier for this entry. This is a GUID.
  - `label` (`string`): a human-friendly label for this entry.
  - `payload` (`string`): an optional payload, whose content depends on the external repository. In our case, this is internally used to distinguish between works and containers.
  - `tag` (`string`): an optional tag assigned to this entry. Typically this is related to the reason for including this entry.
  - `note` (`string`): an optional note about this entry.

Thesauri: `ext-biblio-author-roles`, `ext-biblio-languages`, `ext-biblio-work-tags`.

### SerialTextInfoPart

A text being part of a series of exchanges, like e.g. a letter.

- `textId`\* (`string`)
- `language`\* (`string` = code from [ISO 639-3](https://en.wikipedia.org/wiki/ISO_639-3), thesaurus)
- `subject`\* (`string`, MD, 500)
- `genre` (`string`, thesaurus `serial-text-genres`)
- `verse` (`string`, thesaurus `serial-text-verses`)
- `rhyme` (`string`): rhyme scheme.
- `authors`\* (`CitedPerson[]`): the rank for person is used here to express the fact that the attribution of the text to the identified person has a certain level of confidence.
- `headings` (`string[]`): zero or more headings found in the manuscript text or its variants.
- `recipients`\* (`DecoratedId[]`): recipient(s), at least 1.
- `replyingTo` (`DecoratedId[]`)
- `related` (`DocReference[]`)
- `isReceived` (`boolean`)
- `note` (`string`, MD, max 1000): a general-purpose free text note to hold "varia".

Thesauri: `serial-text-languages`, `doc-reference-tags`, `serial-text-genres`, `serial-text-verses`, `person-name-tags`, `person-name-types`, `person-id-tags`.

### MsBindingPart

- `century`\* (`number`)
- `description`\* (`string`, MD, 5000)
- `coverMaterial`\* (`string`, thesaurus `ms-binding-materials`)
- `supportMaterial`\* (`string`, thesaurus `ms-binding-support-materials`)
- `size` (`PhysicalSize`)

Thesauri: `ms-binding-materials`, `ms-binding-support-materials`, `physical-size-tags`, `physical-dimension-tags`, `physical-size-units` (required).

### MsCatchwordsPart

- `catchwords` (`MsCatchword[]`):
  - `position`\* (`string`, thesaurus `ms-catchword-positions`)
  - `isVertical` (`boolean`)
  - `decoration` (`string`)
  - `register` (`string`): numerazioni/segnature a registro
  - `note` (`string`)

Thesauri: `ms-catchword-positions`.

### MsCompositionPart

- `sheetCount`\* (`number`)
- `guardSheetCount` (`number`)
- `guardSheets` (`MsGuardSheet[]`):
  - `isBack` (`boolean`)
  - `material` (`string`, thesaurus `ms-materials`)
  - `location` (`MsLocation`)
  - `date` (`HistoricalDate`)
  - `note` (`string`)
- `sections` (`MsSection[]`):
  - `tag` (`string`): any arbitrarily chosen ID used to group sections together.
  - `label`\* (`string`)
  - `start`\* (`MsLocation`)
  - `end`\* (`MsLocation`)
  - `date` (`HistoricalDate`)

Thesauri: `ms-materials`.

### MsContentLociPart

Loci critici.

- `loci` (`MsContentLocus[]`)
  - `citation`\* (`string`)
  - `text`\* (`string`)
  - `refSheet` (`MsLocation`)
  - `imageId` (`string`)

Thesauri: none.

### MsContentsPart

- `contents` (`MsContent[]`):
  - `author` (`string`)
  - `claimedAuthor` (`string`)
  - `work`\* (`string`)
  - `ranges` (`MsLocationRange[]`)
  - `state` (`string`, thesaurus `ms-content-states`)
  - `title` (`string`)
  - `incipit` (string)
  - `explicit` (string)
  - `note` (`string`)
  - `units` (`MsContentUnit[]`):
    - `label`\* (`string`)
    - `start`\* (`MsLocation`)
    - `end`\* (`MsLocation`)
    - `incipit` (`string`)
    - `explicit` (`string`)

Thesauri: `ms-content-states`.

### MsDecorationsPart

- `decorations` (`MsDecoration[]`):
- `id`\* (`string`): inner ID
- `name`\* (`string`)
- `flags` (`string[]`; 0-N picks from thesaurus `ms-decoration-flags`, like original, unitary, complete, etc.)
- `date` (`HistoricalDate`)
- `place` (`string`): geographic place.
- `artist` (`MsDecorationArtist`):
  - `type`\* (`string`, thesaurus `ms-decoration-artist-types`)
  - `id`\* (`string`)
  - `name`\* (`string`)
  - `note` (`string`)
  - `sources` (`DocReference[]`)
- `note` (`string`)
- `references` (`DocReference[]`)
- `elements` (`MsDecorationElement[]`):
  - `key` (`string`): the key used for this element when it represents also a parent of other elements. Its scope is limited to the part.
  - `parentKey` (`string`): used to group sub-elements under an element, it is the `key` of the parent element. Its scope is limited to the part.
  - `type`\* (`string`, thesaurus `ms-decoration-elem-types`): the element's type.
  - `flags`\* (`string[]`; 0-N picks from thesaurus `ms-decoration-elem-flags`: original, unitary, complete, has tips, etc.)
  - `ranges`\* (`MsLocationRange[]`)
  - `typologies` (`string[]`; 0-N picks from thesaurus `ms-decoration-elem-typologies`); as typologies vary too much according to type, organize them into sub-sets, and let the UI automatically pick the one corresponding to the type.
  - `subject` (`string`): the decoration subject when applicable. For letters, it might be the letter itself.
  - `colors` (`string[]`; 0-N picks from thesaurus `ms-decoration-elem-colors`)
  - `gilding` (`string`, thesaurus `ms-decoration-elem-gildings`): gilding type.
  - `technique` (`string`, thesaurus `ms-decoration-elem-techniques`)
  - `tool` (`string`, thesaurus `ms-decoration-elem-tools`)
  - `position` (`string`, thesaurus `ms-decoration-elem-positions`): relative to the page.
  - `lineHeight` (`number`): height measured in lines.
  - `textRelation` (`string`): relationship with text.
  - `description` (`string`, MD, 1000)
  - `imageId` (`string`): this is an ID representing the prefix for all the images representing the decoration; e.g. if it is `ae`, we would expect any number of image resources named after it plus a conventional numbering, like `ae00001`, `ae00002`, etc.
  - `note` (`string`).

Thesauri: `ms-decoration-elem-types` (required), `ms-decoration-artist-types`, `ms-decoration-elem-flags`,
`ms-decoration-elem-colors`, `ms-decoration-elem-gildings`,
`ms-decoration-elem-techniques`, `ms-decoration-elem-positions`,
`ms-decoration-elem-tools`, `ms-decoration-elem-typologies`,
`ms-decoration-type-hidden`.

For reference, this was the old `MsDecoration` model:

- `type`\* (`string`, thesaurus)
- `subject` (`string`)
- `colors`\* (`string[]`; 0-N picks from a thesaurus)
- `tool` (`string`, thesaurus)
- `start` (`MsLocation`)
- `end` (`MsLocation`)
- `position` (`string`, thesaurus)
- `size` (`PhysicalSize`)
- `description` (`string`, MD, 1000)
- `textRelation` (`string`, 1000)
- `guideLetters` (`MsGuideLetter[]`):
  - `position`\* (`string`, thesaurus)
  - `morphology` (`string`)
- `imageId` (`string`): this is an ID representing the prefix for all the images representing the decoration; e.g. if it is `ae`, we would expect any number of image resources named after it plus a conventional numbering, like `ae00001`, `ae00002`, etc.
- `artist` (`MsDecorationArtist`):
  - `type`\* (`string`, thesaurus)
  - `id`\* (`string`): inner ID
  - `name`\* (`string`)
  - `note` (`string`)
  - `sources` (`DocReference[]`)
- `note` (`string`)

### MsHandsPart

- `hands` (`MsHand[]`):
  - `id`\* (`string`)
  - `types`\* (`string[]`, thesaurus `ms-hand-types`)
  - `personId` (`string`)
  - `description`\* (`string`, MD, 2000)
  - `initials` (`string`)
  - `corrections` (`string`)
  - `punctuation` (`string`)
  - `abbreviations` (`string`, MD, 1000)
  - `idReason`\* (`string`, thesaurus `ms-hand-id-reasons`)
  - `ranges`\* (`MsLocationRange[]`):
    - `start` (`MsLocation`)
    - `end` (`MsLocation`)
  - `extentNote` (`string`)
  - `rubrications` (`MsRubrication[]`):
    - `ranges` (`MsLocationRange[]`)
    - `type`\* (`string`, thesaurus `ms-rubrication-types`)
    - `description` (`string`)
    - `issues` (`string`)
  - `subscriptions` (`MsSubscription[]`):
    - `ranges` (`MsLocationRange[]`)
    - `language`\* (`string` = code from [ISO 639-3](https://en.wikipedia.org/wiki/ISO_639-3), thesaurus `ms-languages`)
    - `text` (`string`)
  - `signs` (`MsHandSign`[]): description of any relevant graphical sign, whether it's a letter or not (the type is specified in `type`):
    - `id`\* (`string`): this must be a unique, arbitrarily chosen string for this sign
    - `type`\* (`string`, thesaurus `ms-hand-sign-types`)
    - `description` (`string`, MD, 1000)
    - `imageId` (`string`): this is an ID representing the prefix for all the images representing that sign; e.g. if it is `ae`, we would expect any number of image resources named after it plus a conventional numbering, like `ae00001`, `ae00002`, etc.
  - `imageIds` (`string[]`)

Thesauri: `ms-hand-id-reasons`, `ms-hand-types`, `ms-hand-sign-types`,
`ms-rubrication-types`, `ms-languages`.

### MsHistoryPart

- `provenances`\* (`GeoAddress[]`, at least 1; in chronological order):
  - `area`\* (`string`, thesaurus `ms-provenance-areas`)
  - `address` (`string`)
- `history`\* (`string`, MD, 5000)
- `persons` (`MsHistoryPerson[]`):
  - `id` (`string`)
  - `role` (`string`, thesaurus `ms-history-person-roles`)
  - `name`\* (`PersonName`)
  - `date` (`HistoricalDate`)
  - `note` (`string`, 1000)
  - `externalIds` (`string[]`)
  - `sources` (`DocReference[]`)
- `annotations` (`MsAnnotation[]`):
  - `language`\* (`string` = code from [ISO 639-3](https://en.wikipedia.org/wiki/ISO_639-3), thesaurus `ms-history-languages`)
  - `type`\* (`string`, thesaurus `ms-annotation-types`)
  - `text`\* (`string`, 1000)
  - `ranges` (`MsLocationRange[]`)
  - `personId` (`string`)
  - `sources` (`DocReference[]`)
- `restorations` (`MsRestoration[]`):
  - `type`\* (`string`, thesaurus `ms-restoration-types`)
  - `place` (`string`)
  - `date` (`HistoricalDate`)
  - `note` (`string`)
  - `personId` (`string`)
  - `sources` (`DocReference[]`)

Thesauri: `ms-provenance-areas`, `ms-history-person-roles`,
`ms-history-languages`, `ms-annotation-types`, `ms-restoration-types`,
`person-name-types`, `person-name-tags`, `doc-reference-tags`.

### MsLayoutsPart

Formerly `MsDimensionsPart`.

- `layouts` (`MsLayout[]`):
  - `sample`\* (`MsLocation`): the sheet used as the sample for taking measurements and counts.
  - `dimensions` (`PhysicalDimension[]`): any number of measurements taken for any kind of measurable thing in the manuscript. TODO: use formula for entering.
  - `columnCount`\* (`int`)
  - `rulingTechnique` (`string`, thesaurus `ms-ruling-techniques`)
  - `derolez` (`string`; not a thesaurus)
  - `priking` (`string`)
  - `counts` (`DecoratedCount[]`): any number of counts (thesaurus `ms-counts`). This allows entering any number of counts with different levels of precision. For instance, you might have `rowMinCount`, `rowMaxCount`, `lineCount`, `approxLineCount`, `lineMinCount`, `lineMaxCount`, `prickCount`, etc. It also allows descriptions for properties like columns, direction, blanks, ruling, execution, etc., eventually with a count (which might represent an average, or the most frequent value, etc.).

Thesauri: `physical-size-units` (required), `ms-dimensions`, `ms-counts`, `ms-ruling-techniques`.

In the web editor, we can use a formula to quickly enter a set of dimensions. The formula has these parts:

- whitespaces are ignored, so all the regular expressions below assume that no whitespace exists (they are removed before parsing).
- syntax: `N x N = <height> x <width>`: in the following scheme, - vs + mark portions which are alternative (where `-` stands for empty, and `+` for written).

```txt
240 × 150 = 30 / 5 [5 / 170 / 5] 5 / 40 × 15 / 5 [5 / 50 / 5* (20) 5* / 40 / 5] 5 / 15
               ----++++    +++++----         ----++++       -  ||   -      ++++----
hhh   www   hhhhhhhhhhhhhhhhhhhhhhhhhhh   wwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwwww
                                             1111111111111111  ||  22222222222222
h     w     mt he  hw   ah fw    fe  mb   ml cle clw  cw   crX cg  clX  cw crw cre  mr

height:

[mt   ]
[he/hw]
[ah   ]
[fe/fw]
[mb   ]

width:
     col1                   col2
[ml] [cle/clw][cw][cre/crw] [cg][cle/clw][cw][cre/crw]... [mr]
```

Examples:

- `240 × 150 = 30 / 5 [170 / 5] 40 × 15 [5 / 50 / 5* (20) 5* / 40] 5 / 15`
- `200 x 160 = 30 [130] 40 x 15 [5 / 50 / 5 (10) 5 / 50 / 5] 15`
- `200 x 160 = 30 [130] 40 x 15 [5 / 50 / 5* (10) 5* / 50 / 5] 15`
- `200 x 150 = 30 [130] 40 x 30 [5 / 95] 20`
- `200 x 150 = 30 [130] 40 x 30 [5 / 90 / 5] 20`
- `210 x 150 = 30 [5 / 130 / 5] 40 x 20 [50 (10) 50] 20`
- `250 x 150 = 30 / 5 [170 / 5] 40 x 30 [5 / 90] 5 / 20`

### MsMaterialDscPart

- `material`\* (`string`, thesaurus `ms-materials`)
- `state`\* (`string`, thesaurus `ms-states`)
- `format` (`string`, thesaurus `ms-formats`)
- `stateNote` (`string`, 500)
- `palimpsests` (`MsPalimpsest[]`):
  - `location`\* (`MsLocation`)
  - `date` (`HistoricalDate`)
  - `note` (`string`)

Thesauri: `ms-materials`, `ms-formats`, `ms-states`.

### MsNumberingsPart

- `numberings` (`MsNumbering[]`):
  - `isMain` (`boolean`)
  - `isPagination` (`boolean`): cartulazione vs. paginazione.
  - `era`\* (`string`, thesaurus `ms-numbering-eras`: one from "coeva", "antica", "moderna", "recente")
  - `system`\* (`string`, thesaurus `ms-numbering-systems`)
  - `technique`\* (`string`, thesaurus `ms-numbering-techniques`)
  - `century`\* (`number`)
  - `position` (`string`, thesaurus `ms-numbering-positions`)
  - `issues` (`string`)

Thesauri: `ms-numbering-eras`, `ms-numbering-systems`, `ms-numbering-techniques`, `ms-numbering-positions`.

### MsPlacePart

Place of origin (provenance is in `MsHistoryPart`).

- `area`\* (`string`, thesaurus `ms-place-areas`)
- `address` (`string`): this contains any number of components separated by comma, like in geocoding addresses, whereas the area is the top level component.
- `city` (`string`)
- `site` (`string`): e.g. "St. Paul monastry".
- `subscriber` (`string`): subscriber ID (human-readable, arbitrary string)
- `subscriptionLoc` (`MsLocation`)
- `sources` (`DocReference[]`): modern bibliography references.

Thesauri: `ms-place-areas`, `doc-reference-tags`.

### MsPoemRangesPart

This part defines the sequence of poems or other types of numbered compositions in a manuscript. This is used to compare the sequence of poems in different mss of Petrarch's RVF.

- `tag` (`string` thesaurus `ms-poem-ranges-tags`)
- `ranges`\* (`AlnumRange[]`):
  - `a`\* (`string`): the start "number".
  - `b` (`string`): the end number unless equal to the start "number".
- `note` (`string`)

In ranges, values for `a` and `b` are strings representing "alphanumerics", i.e. either numbers (a string with only digits), or at least 1 digit followed by any combination of digit or non-digit characters. These alphanumerics are sorted according to the following criteria:

- an alphanumeric with only digits (e.g. `12`) is sorted by its numeric value.
- an alphanumeric with non-digit characters (e.g. `12a`, `12b1`, etc.) is sorted first by its numeric value, and then alphabetically by its string suffix.

Ranges can be expressed only for alphanumerics with digits only, as they would be ambiguous in other cases: e.g. `12-15` means `12`, `13`, `14`, `15`; but `12-15a` could be interpreted in a number of different ways, as we have no predefined convention for the non-digits part. For instance, a valid range could be `1-13, 15-19, 20a, 21-36, 38, 50-67`.

Thesauri: `ms-poem-ranges-tags`.

### MsQuiresPart

- `types` (`string[]`, thesaurus: `ms-quire-types`): the prevalent types (binione, ternione, etc.)
- `quires` (`MsQuire[]`):
  - `tag` (`string`, thesaurus)
  - `startNr`\* (`number`)
  - `endNr`\* (`number`)
  - `sheetCount`\* (`number`)
  - `sheetDelta` (`number`, negative or positive)
  - `note` (`string`)

Thesauri: none.

Note: allow users to enter collations using formulas like `1-3^4-1`. In this syntax we have any number of tokens separated by whitespace. Each token has the syntax `N-N^N±N {note}` where `-N` and `±N` are optional:

- `N` or `N-N` is the gatherings range (=`startNr` and `endNr`; when only `N` is specified, both are assumed to be equal);
- `^` introduces the sheets count (`sheetCount`);
- `±N` adds an exceptionally missing or additional sheet count (`sheetDelta`).
- `note` is an optional short note. It should not include braces.

### MsSignaturesPart

- signatures (`MsSignature[]`):
  - `tag` (`string`, thesaurus `ms-signature-tags`)
  - `city`\* (`string`)
  - `library`\* (`string`)
  - `fund` (`string`)
  - `location`\* (`string`)

At least 1 must be present. The signature with empty tag is the default (current) signature. Other signatures may be added for historical reasons, and should have a tag.

Thesauri: `ms-signature-tags`.

### MsWatermarksPart

- `watermarks` (`MsWatermark[]`):
  - `subject`\* (`string`, thesaurus `ms-watermark-subjects`)
  - `similarityRank` (`number`): a rank for the similarity of the watermark described here to the paradigmatic watermark model; the higher the number, the less similar is the watermark.
  - `description` (`string`): a text description for this watermark instance.
  - `place` (`string`)
  - `date` (`HistoricalDate`)
  - `externalIds` (`string[]`)

Thesauri: `ms-watermark-subjects`.

### PersonEventsPart

Any event relevant for the biography of a person, including his works.

- `events` (`BioEvent[]`):
  - `type`\* (`string`; thesaurus `bio-event-types`)
  - `date` (`HistoricalDate`)
  - `places` (`string[]`)
  - `description` (`string`, MD, 1000)
  - `sources`\* (`DocReference[]`)
  - `participants` (`DecoratedId[]`)
  - `work` (`string`)
  - `rank` (`number`)
  - `isWorkLost` (`boolean`)
  - `externalIds` (`string[]`)

Thesauri: `bio-event-types`, `event-participant-tags`, `doc-reference-tags`.

### PersonPart

This contains the ID and biographic data of any person (the part role ID makes the distinction among different groups explicit). It can also represent any other generic actor, e.g. a group of persons ("Celestini").

- `personId`\* (`string`, eventually from thesaurus): this is an internal human-readable ID for the correspondent, e.g. `barbato`, `flavio-2`, etc. It can used as a facility for referring to the correspondent across parts, without recurring to the machine-related item ID. Thus, it must be unique in the database.
- `externalIds` (`string[]`): optional IDs in external resources which can be mapped to this correspondent.
- `names`\* (`PersonName[]`): at least 1 name.
- `sex` (`string`: `m`, `f`, or null if unknown)
- `chronotopes` (`Chronotope[]`): chronotopic indications, usually for birth and/or death.
- `bio` (`string`, MD, 6000)

Thesauri: `person-name-languages`, `doc-reference-tags`, `person-name-types`, `chronotope-tags`, `person-name-tags`.
