## Su questa repository e questi file

### Funzione della repository

Centralizzo in questa repository *specifications* per la web app PAGES/TAL/ThDS.


### File importanti

- Schema generale UML
    - [schema.png](schema.png)
    - [schema.uml](schema.uml)
- Specifici per le ricerche
    - [ricerche_testuali.md](ricerche_testuali.md)
    - [ricerche_mss.md](ricerche_mss.md)
- [README.md] centralizza tutte le altre informazioni di dettaglio
    - la sezione [Thread email e link per Paolo](#Thread email e link per Paolo) è solo per Paolo (fonti di informazione per la sintesi costituida da README.md)
    - per il resto, nel file le feature requests sono organizzate tematicamente (titolo 2 / titolo 3)
    - anche il file [vecchie_note.md](vecchie_note.md) è da ignorare, perché contiene note riportate altrove o non più importanti















## Lista autori-opere

### Come generare lista autori-opere (groupID → thesaurus?)

Il punto di partenza sono i groupID degli item, che contengono attualmente (ma vedi la modifica proposta sotto) stringhe libere del tipo "arus" (dato che Arusiano Messio ha solo un autore) che, per gli item di tipo text, identificano autore e opera in un'unica stringa (es.: "arus" per gli *Exempla* di Arusiano e "vel-orth" per l'ortografia di Velio).

Avevamo pensato ad una modifica ai modelli: far sì che il 'groupID' nei metadati di ogni item di tipo text non contenesse una stringa libera ma pescasse da un thesaurus. Cito dal paragrafo "Output" di [2022-03-07_bisettimanale.md]:

~~~
- In Cadmus, agganciare il 'group id' degli item al thes authors and works
    - obbligatorio solo per gli item testuali
    - ...o qualcosa del genere per generare la lista autori/opere in visualizzazione
~~~

Qualunque altra proposta è ben accetta comunque.

Origine di questa nota: [e2.md]

In un'email del 22.04.2022 (subj. "Quesiti su Cadmus") A. Consalvi (penso dopo averne parlato con Elena) ha ribadito la stessa richiesta:

> 1) Nella visualizzazione da che tipo di informazione del modello ricaverai la lista delle opere di tipo testuale presenti nella banca dati? Se, come abbiamo inteso correttamente, la ricavi dal group ID nella linguetta metadata di ciascun item abbiamo pensato che sarebbe utile (con una piccola modifica all'interfaccia dell'immissione dei dati) far sì che si possa agganciare alla classe group id un thesaurus (in questo modo per il group id non ci sarebbe nemmeno più bisogno di digitare manualmente l'abbreviazione, ma la si potrebbe selezionare da un menù a tendina). Tuttavia, tale opzione non deve essere obbligatoria, ma valere unicamente per gli item testuali (e non per i manoscritti). Se questo fosse possibile, faremmo una versione ridotta del thesaurus degli autori (che ovviamente comprende migliaia di opere che non saranno mai incluse nella banca dati).



### Livelli nella lista autori-opere

Riquadro TESTO_INDICE nello schema UML.

Cito da Elena, [e3.md], punto 5:

~~~
5) TESTO_INDICE. La localizzazione di ciascun item-text (indicata sia in Metadata > Title sia in base-text > citation) può comprendere uno, due o tre dati (considero un dato unico gli intervalli indicati con trattino-) separati da virgola e spazio. Ad esempio 

    - un dato: Ter. Maur. 2976-2981 (opera in versi, che citiamo solo con i numeri di verso) oppure Nom. Dub. Z1 (opera lessicografica con numerazione alfanumerica di lemmi);

    - due dati: Arus. 100, 10-12 (opera che citiamo con numero di pagina e rigo dell'edizione di riferimento, separati da virgola e spazio) oppure Ps. Palaem. reg. 6, 4 (opera che citiamo con numero di capitolo e di paragrafo, separati da virgola e spazio);

    - tre dati: Prisc. ars 18, 307, 1 (opera che citiamo con numero di libro, paragrafo e sottoparagrafo, separati da virgola e spazio).

Sarebbe possibile, almeno per i testi che citiamo con tre dati, strutturare l'elenco degli item che li costituiscono per libri (primo dato) che poi si espandono (secondo e terzo dato, con l'elenco dei singoli item)? Se non mi sono spiegata bene, il modello che ho in mente è quello del browse della LLT (ma anche in parte della digilibLT).
A parte questo non mi pare che servano altri filtri nel browse/indice degli item-texts.
~~~

Cito da Elena, [e5_2022-02-27_22.29_da_elena.md]:

~~~
Non abbiamo bisogno (e sarebbe contrario alle convenzioni del ThlL e del nostro stesso Index delle opere grammaticali latine) di esplicitare se i varî livelli siano libri/capitoli/paragrafi/sottoparagrafi/versi ecc. Questo sarà, semmai, spiegato nella risorsa statica dell'Index delle opere grammaticali (come avviene nell'Index del ThlL).
~~~






## Browse testo


### Quanti item per schermata in browse

Ogni schermata contiene 10 item testuali.

(Per ora iniziamo così: se poi vediamo che vengono schermate troppo grandi o troppo piccole, cambiamo)

Origine di questa nota: [note.md], punto 0


### Visualizzaz. layer annotaz. linguistica

Quando l'utente è in 'browse', cioè sta semplicemente leggendo il testo, se sceglie di vedere la colonna di un layer, quel layer viene *normalmente* popolato subito (non appena si apre un item testuale) con tutte le annotazioni (ad es. con tutte le note di apparato su quell'item).

Con una sola eccezione, il layer delle *annotazioni linguistiche*, che si comporta invece così:

Quando l'utente carica un item testuale nella colonna di sinistra e sceglie/ha scelto di vedere il layer linguistico in una delle colonne di destra, tale colonna è all'inizio vuota (altrimenti sarebbe troppo affollata), e solo quando l'utente clicca (nella colonna testo base) su una pericope annotata, allora a destra compare l'annotazione linguistica.

- L'utente può selezionare tag 'superiori' (ad es. sintassi dei casi)
    - oppure tag 'inferiori' (sottocategorie, ad es. sintassi di un caso specifico)

Origine di questa nota: [e2.md] e [2021-11-25_riunione_umanisti_visualizzaz_cadmus.md]


### Progetto e curatore

Indicare per ogni item visualizzato

1. il progetto a cui appartiene (PRIN, ERC o Thesaurus Dubii Sermonis). Riporto dall'[email di Elena](e3.md):
2. il curatore dell'item (Andrea Consalvi, Elisa Merisio etc.)

```
0) Nei metadati di ciascun item (Metadata > Description) abbiamo indicato l'acronimo del progetto di ricerca grazie al quale l'item è stato prodotto: questo dato, così come il nome dello studioso che ha curato la digitalizzazione di ciascun testo / manoscritto nella banca dati, dovrebbe apparire da qualche parte nella visualizzazione sia dei testi sia dei manoscritti: magari in un riquadro (comprimibile dall'utente) in un angolo della schermata quando si consulta un item?
```

Origine di questa nota: [e3.md], punto 0


### [DONE] Creazione nuovo layer witnesses

Da [e2.md] (vd. anche lo scambio di email con subj. "Quesiti su Cadmus" di aprile 2022):

> Quando aggiungiamo al modello il neonato "witness fragment" (quello che indica quali MSS tramandano un certo item testuale), bisognerà visualizzarlo, possibilmente in un angolino dei layer testuali.


Da un'email di Elena del 30.04.2022:

> 5. Sono riuscita (faticosamente perché da quando è stato aggiornato il sito si carica molto lentamente e funziona in generale male, cioè si blocca a ogni pagina e va ricaricato in continuazione) ad accedere a Cadmus e ho visto che con l’aggiornamento è stata inserita per gli items-texts una Witnesses part, mentre a noi servirebbe un Witnesses layer, come avevo scritto a Daniele. Ci servirebbe cioè, all'interno del singolo item, di poter evidenziare porzioni di testo anche inferiori a quello dell'intero item e indicare per quelle quali mss. sono disponibili. Se abbiamo, invece, com'è adesso, una Witnesses part, possiamo elencare solo i mss. disponibili per l'intero item.

Ho girato questa richiesta il 30.04.2022 a Daniele.

A. Consalvi aggiunge (dopo l'aggiornamento Cadmus) in un'email del 05.05.2022 dice che la modifica è ancora da fare:

> La part witnesses era già presente in Cadmus, bisogna aggiungere il layer witnesses di cui abbiamo parlato nelle e-mail dal 22/04 al 24/04 anche con Daniele.

Daniele scrive il 08/05/22, 17:25:

> Per witnesses, credo si debba aggiornare il profilo nel database, altrimenti non vede il nuovo layer. Ora riguardo e ti mando query.

e poi vd. le query che Daniele ha scritto nella sua email del 08/05/22, 17:50.

Ho dato le due query il 19.05.2022, cioè:

```{#query1905a}
db.facets.update({"_id":"text"}, { $push: {  partDefinitions: { "typeId": "it.vedph.token-text-layer", "roleId": "fr.it.vedph.tgr.available-witnesses", "name": "witnesses", "description": "Available witnesses layer.", "colorKey": "FFF194", "groupKey": "text", "sortKey": "witnesses-layer" } } });
```

E:

```{#query1905b}
db.thesauri.update({"_id":"model-types@en"}, {$push: { entries: { "id": "fr.it.vedph.tgr.available-witnesses", "value": "witnesses fr." } }});
```

e sembra aver funzionato tutto.

...Invece no: si è 'rotto' Cadmus online (19.05.2022 18:10)

Il giorno dopo (20.05.2022) su consiglio di Daniele ho cancellato l'intero thesaurus `model-types@en` da Robo 3T e l'ho ricreato a mano dalla UI Cadmus. Ho trovato anche qual era l'errore: nella [prima query](#query1905a) avevo scritto `id` invece di `_id`, cioè
`"id" : "fr.it.vedph.tgr.available-witnesses"`
invece di
`"_id" : "fr.it.vedph.tgr.available-witnesses"`
col seguente risultato nel JSON:

```
        {
            "id" : "fr.it.vedph.tgr.available-witnesses", 
            "value" : "witnesses fr."
        }
```

invece di `_id` etc.

Oggi 20.05.2020 09:50 il problema è completamente risolto, e il nuovo layer witnesses funziona come desiderato.



### [DONE] Correzione tgr/itinera ms-signatures


In Robo 3T oggi 19.05.2022 ho dato:

```
db.getCollection('thesauri').find({"_id":"model-types@en"})
```

e nel JSON del thesaurus che trova, ho editato a mano:

```
    {
        "_id" : "it.vedph.itinera.ms-signatures",
        "value" : "ms signatures"
    },
```

in: 

```
 {
        "_id" : "it.vedph.tgr.ms-signatures",
        "value" : "ms signatures"
    },
```

cioè "itinera" → "tgr".

Poi, sempre in Robo 3T, in

```
db.getCollection('facets').find({})
```

nell'entry con `_id` : `manuscript`

in

```
        {
            "typeId" : "it.vedph.itinera.ms-signatures",
            "roleId" : null,
            "name" : "ms signatures",
            "description" : "Manuscript's signatures.",
            "isRequired" : true,
            "colorKey" : "D7D5DB",
            "groupKey" : "manuscript",
            "sortKey" : "ms-signatures"
        }, 
```

ho editato a mano

```
            "typeId" : "it.vedph.itinera.ms-signatures",
```

in

```
            "typeId" : "it.vedph.tgr.ms-signatures",
```

...ma i problemi di Cadmus 'rotto' ci sono ancora.




### Visualizzazione nuovo layer witnesses

Da un'email di Elena del 27.04.2022:

> dovrebbe essere un riquadrino a comparsa, magari che appare solo quando si visualizza l'Apparatus layer e che comunque l'utente può far sparire se non gli interessa



### Numeri di riga

Niente numeri di riga.

Origine di questa nota: [2021-11-25_riunione_umanisti_visualizzaz_cadmus.md], par. "Testo: tipi di visualizzazione"


### Per evitare sovrapposiz. evidenziature

- Il testo latino base (della colonna di sinistra) si evidenzia solo quando l'utente clicca in una delle due colonne di destra
    - così evitiamo il problema della sovrapposizione di evidenziature

Origine di questa nota: [2022-03-07_bisettimanale.md]






## Manoscritti

### Visualizzazione di ciascuna scheda MS

Riquadro MS_SCHEDA nello schema UML.

Cito da Elena, [e3.md], punto 3:

~~~
3) MS_SCHEDA. Credo che la visualizzazione di ciascuna scheda (cioè di ciascun item-manuscript) possa consistere nell'elenco delle parts che la compongono, che l'utente dovrebbe poter cliccare per espanderle e poi ricomprimere.
Nella visualizzazione della parte dei contenuti di ogni manoscritto bisognerebbe che le opere di cui abbiamo l'edizione tra gli item-texts della nostra banca dati siano linkate al browse del testo (poiché per marcare i contenuti testuali dei manoscritti usiamo un thesaurus, suppongo che anche questa operazione sia semplice).
~~~





### Collegamento sigla-schede MSS

Riquadro TESTO_LETTURA nello schema UML.

Cito da Elena, [e3.md], punto 6 (ma Elena ne aveva parlato anche in [2021-11-25_riunione_umanisti_visualizzaz_cadmus.md], par. "Collegamento testo-MSS"):

~~~
6) TESTO_LETTURA. Nella visualizzazione dell'apparatus layer e dei vari interpolations layer bisognerà che si possa cliccare sul siglum di un manoscritto ed essere linkati al corrispondente item-manuscript (con apertura dell'item-manuscript, cioè di MS_SCHEDA, in una nuova scheda del browser). A questo scopo Daniele mi ha fatto tenere una lista delle corrispondenze tra le segnature dei manoscritti e i sigla ad essi associati nelle edizioni delle varie opere che abbiamo via via digitalizzato. Occorrerebbe dunque creare un link tra le segnature dei manoscritti e le varie entries dei thesauri di sigla che usiamo per gli item-texts.
~~~

La "lista delle corrispondenze" qui citata è un file di word che ha Elena.


### Mappa dinamica MSS

1. Linea del tempo

Il gruppo chiede di creare una mappa con una barra "linea del tempo" in basso.

*Descrizione del caso d'uso*: All'inizio la barra è, mettiamo, al 5. sec. d.C., e la mappa è vuota (perché non ci sono MSS del 5. secolo).  L'utente sposta la barra verso destra e passa all'8. secolo, e sulla mappa spuntano pallini in corrispondenza dell'area di provenienza dei MSS di 8. secolo (o precedenti). L'utente sposta la barra ancora più avanti fino al 9. secolo, e spuntano i pallini dei MSS di tutti i secoli fino al nono.

2. Solo i codici di un ramo dello stemma

- *Desideratum:* L'utente può scegliere di visualizzare sulla mappa solo i codici di un certo ramo (ad es.del ramo theta):
    - Bellissimo se avessimo a sinistra lo stemma
        - L'utente clicca su MS o subarchetipo
        - E a destra la mappa si modifica dinamicamente

*Origine dati*: I dati sull'area d'origine dei MSS dovrebbero venire, se non sbaglio, da [questo punto dei modelli Cadmus TGR](https://github.com/vedph/cadmus_tgr_doc/blob/master/models.md#MsPlacesPart):

- `places` (`MsPlace[]`):
  - `area`\* (`string`, thesaurus)

...e/o da `places/city`.

Origine di questa nota: [2021-11-25_riunione_umanisti_visualizzaz_cadmus.md], par. "Manoscritti"




### Nuovi thesauri MsPlacesPart e MsSignature

Michela e Elena hanno deciso di creare dei nuovi thesauri per

- `area`, `city`, `site` di `MsPlacesPart`
    - (fonte: un'email di Elena del 01/05/22, 10:11, punto 7bis)
- `city`, `library` e `fund` di `MsSignaturesPart`
    - (fonte: un'email di Elena del 01/05/22, 10:29)

Quindi bisognerebbe cambiare il modello di `MsPlacesPart` (da <https://github.com/vedph/cadmus_tgr_doc/blob/master/models.md>) e di `MsSignaturesPart` (da [Itinera](https://github.com/vedph/cadmus_itinera_doc/blob/master/models.md#mssignaturespart)) in modo da agganciare queste proprietà ai nuovi thesauri (che al 19.05.2022 sono ancora da creare).

Per quanto riguarda `area`, `city` e `site` di `MsPlace`, allo stato attuale del DB (30.04.2022), pochissimi (meno di una decina) di item MS hanno tali campi popolati, quindi si possono anche cancellare 'a mano' segnandosi altrove il contenuto, per poi reinserirlo quando i thesauri saranno creati.

I thesauri saranno piuttosto lunghi, quindi sarà necessario che i collaboratori Cadmus possano (nell'interfaccia/app Cadmus) cercare al loro interno, come già si fa per il thesaurus authors/works e dei tag linguistici.







### Codices disiecti

- Codices disiecti: visualizzazione
    - Dire che
         - la parte che sta a Parigi è la n. 1
         - quella che sta a S. Pietroburgo è la n. 2
         - e quella a Orléans è la n. 3
    - Circa una 50ina di MSS sono disiecti
        - su Centinaia di MSS in tutto in Cadmus
- Codices disiecti: modifica da fare al modello Cadmus
    - "group id" dovrebbe attingere
        - a un thesaurus (thesaurus da modificare spesso, ahinoi) di codici ricostruiti

Scrive Elena in [e5_2022-02-27_22.29_da_elena.md]:

~~~
Non abbiamo ancora creato quel thesaurus perché la compilazione delle schede dei mss è ancora perlopiù da fare (gli items sono stati creati ma le loro parts vanno ancora create e compilate). Quando lo creeremo, il thesaurus dei group id dei codices disiecti sarà comunque utilizzato per riempire la stringa di un campo già presente nella Units Part degli item-manuscripts. La visualizzazione di questa specifica stringa dovrebbe consistere in un link alla visualizzazione della/e Units Part(s) dell'altro/degli altri manoscritti contenenti parti del codex disiectus identificato dal group id che peschiamo dal thesaurus.
~~~

Origine di questa nota: l'elenco puntato viene da [2021-11-25_riunione_umanisti_visualizzaz_cadmus.md], par. "Codices disiecti"; i paragrafo successivo da [e5_2022-02-27_22.29_da_elena.md]












## Indice citazioni

Dato che ci sono le citazioni, gli indici 'tradizionali' servono meno, ma si è comunque pensato di crearne uno, che comprenda le citazioni presenti

1. nel testo dei grammatici
2. (per la sola *Ars* di Prisciano) anche nelle interpolazioni umanistiche (cioè `interpolations` con `role`="interp")



### Origine dei dati

1. Origine dei dati per le citazioni nel testo dei grammatici (punto 1 sopra):

- `quotations` (`VarQuotation[]`): quotations with variants:
   - `work`\* (`string`, hierarchical thesaurus: `author-works`): author and work.
   - `authority`\* (`string`, thesaurus: `quotation-authorities`): the authority type (grammatical/linguistic)

2. Origine dei dati per le citazioni all'interno delle interpolazioni umanistiche (punto 2 sopra):

- `interpolations` (`Interpolation[]`):
   - `quotations` (`VarQuotation[]`)

### Ordinamento e visualizzazione

Da un'email di Elena del 30.04.2022:

- Si potrebbe trattare invero di un unico indice 
    - al quale sia possibile aggiungere (*scil.* alle citazioni nel testo dei grammatici, punto 1 sopra) con un flag anche le citazioni presenti nell’Interpolations Layer (*scil.* le interpolazioni umanistiche, punto 2 sopra)
- L’indice dovrebbe poter essere consultato
    - per autori **citati**
        - elenco degli autori **citati** e dei passi di ciascun autore secondo l'ordine del testo **citato** con indicazione accanto o link ai passi dei testi citanti, cioè dei grammatici, in cui le citazioni occorrono
    - e per autori **citanti**
        - elenco degli autori e opere grammaticali comprese nelle banca dati e, all'interno di ciascuna di queste, elenco degli esempi letterari che contengono, ordinati alfabeticamente di nuovo per autore **citato** e ordine del testo **citato**). 
- Dovrebbe inoltre esser possibile [...] distinguere (con un flag?) autorità grammaticali e linguistiche
    - Origine dei dati per questo: `quotations` / `authority`











## Altre questioni


### Contesto snippet risultati ricerca

Quando l'utente vede i risultati della ricerca, gli 'snippet' dovrebbero coincidere con l'intero item testuale (al gruppo PAGES interessa che l'utente non si faccia un'idea frettolosa sulla base di poco contesto). Dentro l'item, la pericope cercata (o annotata, se si cerca per tag linguistici) va evidenziata.
Se l'utente clicca sulla snippet, si apre il testo continuo (in modalità 'browse').

Origine di questa nota: [2021-11-25_riunione_umanisti_visualizzaz_cadmus.md], par. "Testo: snippet risultati del search"



### Terza linguetta per index statico

HOME. Nel menù di navigazione oltre a Texts e Manuscripts dobbiamo prevedere una terza linguetta Index/List of the Latin grammatical works, with abbreviations and standard editions. Si tratta del nostro Index dei testi grammaticali, con abbreviazioni in parte difformi da quelle del ThlL e l'indicazione delle più recenti edizioni critiche di riferimento, non sempre già acquisite nell'Index del ThlL); esiste per ora solo come risorsa statica (una tabella del tutto simile a quella di https://www.thesaurus.badw.de/tll-digital/index.html, ma naturalmente molto più breve) ma dovrebbe essere completata (suppongo sia operazione banale) con i link al browse di ciascun testo nella nostra banca dati (limitatamente ai testi grammaticali compresi nella nostra banca dati, che per ora non sono certo tutti quelli della lista).

Origine di questa nota: [e3.md], punto 1


### Dubius sermo (modifica al modello)

- In Cadmus, nei linguistic tags, 
    -  metti un tag "dubius sermo" sì/no

Origine di questa nota: il paragrafo "Output" di [~/travaglio/pages/riunioni/2022-03-07_bisettimanale.md] 

### Testo: manuale utente

- Spiegare bene la differenza
     - tra un 'browse' avanzato
     - E search (che comprende ricerche complesse)

Origine di questa nota: [2022-02-21_riunione_visualizzaz_cadmus.md]

### LOD e TEI

Questi due dossier restano aperti. Michela vuole portare avanti questi output solo se non ci rallentano troppo, dato che non ci servono per la rendicontazione

Origine di questa nota: [e2.md], [2022-02-21_riunione_visualizzaz_cadmus.md] e gli scambi di email


### [SOLVED] Breaking change per aggiornamento Cadmus

- Vd. il breaking change descritto in [questo file](2021-11-26_riunione_io_e_daniele_visualizzaz_cadmus.md)
    - ho scritto a Daniele il 21.03.2022 chiedendogli se sia ancora da fare
    - sì, è da fare, e al 23.04.2022 diventa urgente perché bisogna fare alcune modifiche a Cadmus
- Aggiornamento fine aprile 2022
    - abbiamo fatto l'aggiornamento il 23.04.2022, e si è 'rotto' Cadmus sul server IS (e nelle installazioni locali sul computer di Paolo); funziona invece sulle VM locali di Daniele. Stiamo provando a debuggare
- Abbiamo debuggato a inizio maggio 2022

### [DONE] Copiare-incollare tag linguistici

In un'email del 22.04.2022 (subj. "Quesiti su Cadmus") A. Consalvi (penso dopo averne parlato con Elena) ha chiesto questa modifica a Cadmus:

> 3) Ti chiedo inoltre se sia possibile aggiungere una funzione per quanto concerne l'apparato critico: capita sovente che ad esempio in un trattato di morfologia seguano più esempi che hanno tutti gli stessi tag linguistici, ma diverso lemma. Sarebbe possibile creare una funzione che consenta di copiare e incollare unicamente i tag linguistici? Sarebbe estremamente utile per velocizzare il processo di immissione dati.

Il 18.05.20022 A. Consalvi mi scrive che Daniele ha aggiunto la funzione... e funziona.


## Thread email e link per Paolo

### Fonti di informazione per questo file

Ho creato questo file a fine aprile 2022 riportando qui le questioni ancora aperte sulla visualizzazione. Vi sono confluite annotazioni tratte da:

- [2021-11-25_riunione_umanisti_visualizzaz_cadmus.md](2021-11-25_riunione_umanisti_visualizzaz_cadmus.md)
- [2021-11-26_riunione_io_e_daniele_visualizzaz_cadmus.md](2021-11-26_riunione_io_e_daniele_visualizzaz_cadmus.md) 
- [2022-02-21_riunione_visualizzaz_cadmus.md](2022-02-21_riunione_visualizzaz_cadmus.md) 
- [2022-03-07_bisettimanale.md](2022-03-07_bisettimanale.md)
- [e1.md](e1.md)
- [e2.md](e2.md)
- [e3.md](e3.md)
- [e4_2022-02-27_18.10_da_paolo.md](e4_2022-02-27_18.10_da_paolo.md)
- [e5_2022-02-27_22.29_da_elena.md](e5_2022-02-27_22.29_da_elena.md)
- [e6_2022-02-28_09.17_da_michela.md](e6_2022-02-28_09.17_da_michela.md)
- [e7_2022-02-28_12.26_da_paolo.md](e7_2022-02-28_12.26_da_paolo.md)
- [e8_2022-03-01_13.45_da_paolo.md](e8_2022-03-01_13.45_da_paolo.md)
- [e9_2022-03-05_19.41_da_elena.md](e9_2022-03-05_19.41_da_elena.md)
- [e_2022-03-07_1227_da_daniele.md](e_2022-03-07_1227_da_daniele.md)
- [e_2022-03-07_1413_da_daniele.md](e_2022-03-07_1413_da_daniele.md)

(questi file non sono visibili nella repository GitHub per questioni di riservatezza, ma li ho sul mio computer)


### Thread email importanti

- Attualmente sono marcati in thunderbird con tag 'PAGES' (celeste)
- sono tre:

1. subj. "RE: PAGES"
    - 1a email 28.11.2021, ma era una risposta di D a una mia con subj. "Gigliozzi, AIUCD e PAGES"
    - tra me e D, con [e1.md] e [e2.md] e altre email minori
    - per discutere la visualizzazione (poi ho aperto a margine anche il tema LOD/API)
2. subj. "Re: LOD PAGES"
    - 1a email 08.12.2021
    - tra me e D per discutere specificamente LOD/API
        - spin-off del thread n. 1
3. subj. "RE: LOD / API"
    - 1a email 08.12.2021
    - D scrive agli umanisti PAGES
        - per discutere il possibile ouput LOD/API
4. subj. "Nuovo link schema"
    - sullo schema grande UML per la visualizzazione, tra me, Elena, Andrea C., Claudio, Elisa M., Michela
    - poi cambia subj. in "Conferme su ricerche testuali e indici [era: Re: Nuovo link schema]"


### Appunti di riunioni

- Nel mio computer, sono nella cartella `pages/riunioni` (quelle con Websoup hanno 'websoup' nel nome file)



### Link utili

- [Documentazione Cadmus](https://github.com/vedph/cadmus_tgr_doc)
- [Schema grafico](https://github.com/vedph/cadmus_tgr_doc/blob/master/overview.md)
- [Schema testuale](https://github.com/vedph/cadmus_tgr_doc/blob/master/models.md)
- [Sito che ilaria M. mi ha mandato questo come esempio (MSS)](https://elmss.nuigalway.ie/catalogue)
