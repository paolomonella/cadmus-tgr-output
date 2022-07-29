---
Title: Test Cadmus
Author: Paolo Monella
Lang: it-IT
Date: 2022-07-29
Time: 15:00 CEST
Description: Stato avanzamento questioni poste da AC
Transformation: pandoc % -o %:r.pdf

---


## Test Cadmus



### Email A.C. 20.06.2022

1) aprire "quotation fr.", linguetta "general", cliccare sull'icona viola con il +, inserisco i campi "work*" e "location*" e selezio cf. dal menù a tendina "tag" (concludo cliccando prima su "accept changes" e poi su "save"). Una volta che riapro l'item, l'informazione relativa al tag non viene salvata. Suppongo possa trattarsi di un bug. In allegato ti ho inviato un video (questione_1) che rende sicuramente più chiaro il problema.

> DF: bug risolto. 

> Paolo: **OK** (ho verificato su cadmus v1.1.7 locale)



2) Per l'esperienza utente mia e di Elisa, i tooltip non sono particolarmente utili e rendono anche un po' macchinosa la digitazione quando compaiono perché, coprendo altri pulsanti sottostanti, rendono necessario girare attorno con l'icona del mouse affinché scompaiano. Personalmente tutti i pulsanti che hai ideato mi paiono già così intuitivi da non necessitare alcun tooltip (e.g. il tooltip "save data" per il pulsante "save").

> Paolo: **No action required**: a quanto capisco, i tooltip restano
> (in effetti però sarebbe meglio se il tooltip non impedisse all'utente di cliccare sull'elemento)



3) Dopo che si è lavorato in un "apparatus fr." e a distanza di tempo c'è necessità di aggiungere una nuova nota che è a cavallo tra due righe, Cadmus non consente di farlo. La soluzione (che ahimè ho sperimentato) è quella di eliminare tutti i tag esistenti e riaggiungerli uno ad uno - soluzione non molto pratica. Suppongo si tratti di un bug (video questione_3).

> Paolo: **OK**


4) all'interno dell'"apparatus fr." il limite di caratteri del campo "value" deve essere aumentato a 700 caratteri perché ho una nota di apparato che supera il limite attuale. Il limite di caratteri del campo "note" tanto sotto "witnesses" come "authors" deve essere aumentato a 200.
- DF: «Per 200 fatto. Per 700 non mi e’ chiaro: cioe’ quando inserisci una voce di apparato di tipo NOTA, il campo value non e’ neppure disponibile; c’e’ appunto il campo nota. Quello e’ limitato a 1000. Oppure non era questo che intendevi?»
- Andrea: «Errore mio che non ho specificato. Il limite di caratteri del campo "value" deve essere aumentato a 700 per "replacement", "addition after" e "addition before"».

> Paolo: **NO**.
> A me (Paolo) sembra che il limite sia attualmente (nella versione 1.1.7) di 100 caratteri (mentre dovrebbe essere 200)
> sia per apparatus fr. / witnesses / note 
> sia per apparatus fr. / authors / note 
> E mi sembra che sia attualmente intorno ai 300 caratteri (mentre dovrebbe essere 700)
> per apparatus fr. / witnesses / entry (type replacement) / value
> (per tutti i type, cioè 'replacement', 'addition after', 'addition before' e 'note').


5) la funzione copia e incolla che abbiamo aggiunto al "linguistic fr." funziona, ma suppongo ci sia probabilmente un altro bug. Quando si copia e poi si incolla, non si riesce a inserire subito anche il lemma, ma bisogna salvare, chiudere e riaprire l'item nuovamente (questione_5).

> DF: «Sembrerebbe che la mia versione non abbia questo errore, forse l'ho gia' eliminato con l'upgrade. Comunque se si ripresentasse ditemi e vediamo».
> Paolo: **Boh?** Non riesco a testarlo perché io non riesco (probabilmente per colpa mia) a salvare dopo aver inserito i tag linguistici. Lo farei testare direttamente a Andrea a questo punto.


6) la funzione copia e incolla andrebbe aggiunta anche al "witnesses fr."

> Paolo: **OK**, funziona

7) abbiamo notato che nell'"apparatus fr.", Cadmus è in grado di contare le parole (8.9-9.6 nell'immagine questione_7). Qualora ci fossero due o più note che insistono su porzioni di testo tra loro sovrapposte, la numerazione (nell'esempio riportato) andrebbe da 1 a 8 e nel campo "subrange" non abbiamo mai indicato le righe. Quindi qualora la nota d'apparato riguardasse "Quot praepositiones? Unam, 'ab'." indicheremmo "subrange"=1-4. Confermi che non ci sono problemi di interferenza tra i due sistemi di numerazione?
A seconda della risposta si potrebbe riflettere se sia possibile aiutare in qualche modo chi deve inserire i dati ed evitare che debba contare manualmente le singole parole (evitando così anche banali errori - specialmente nel caso di porzioni di testo più estese).

> DF: «Si le numerazioni di subrange sono totalmente distinte dalle altre e non si basano su “coordinate” Y (linea) e X (parola grafica), ma solo su X (parola grafica); 1=prima parola, 2=seconda, etc. Per ora il controllo e’ semplicemente una casella di testo perche’ e’ di uso molto raro (l’unico progetto che ne fa uso e’ il vostro)».

> Paolo: **No action required**. Ne deduco che non c'è niente da fare




### Email A.C. 23.06.2022

1) Come vedrai ci sono due item all'interno di "codicological units part" e quando si apre un item e si passa dalla linguetta "unit" a quella "units" e si clicca sul secondo dei due item, Cadmus apre nuovamente il primo. Il problema non si presenta se si clicca sulla X rossa a fondo pagina di ciascun item, ma te lo segnalo perché penso sia abbastanza pratico che anche la linguetta "units" funzioni correttamente.

> Paolo: **NO**. Il problema segnalato da AC persiste ancora




### Email A.C. 22.07.2022

1) All'interno del quotations fragment avremmo bisogno di aggiungere un campo note tanto accanto a location quanto accanto a tag (in questo secondo caso quando si aggiunge un parallel). In allegato ti ho inviato uno screenshot esplicativo (Questione_1).

![Questione 1](img/Questione_1.png)

> Paolo: **NO**. Ora c'è un campo `note` accanto a `work` e `location`. Ma se clicco su `add parallel` ho solo `work`, `location` e `tag`, mentre credo che AC volesse che venisse aggiunto anche un secondo campo `note` accanto a `tag` (vd. la sua screenshot qui sopra)



2) (2A) Sempre all'interno del quotations fragment, sotto la sezione variants, value deve essere opzionale e non obbligatorio (qualunque sia il type).

> Daniele: «mi confermi che il modello va cambiato in modo che value non sia obbligatorio? Ora il modello e’:

```
export interface QuotationVariant {
  lemma: string;
  type: ApparatusEntryType;
  value: string;
  witnesses?: AnnotatedValue[];
  authors?: LocAnnotatedValue[];
}
```

> (dove ? indica opzionale). Vorreste quindi che value divenisse opzionale. Corretto? Ve lo chiedo perche’ in astratto pare strano, cioe’ che senso ha inserire una variante senza il suo valore? Ma sicuramente mi sfugge qualcosa. Mi potete pero’ confermare, cosi’ sono certo delle modifiche? Grazie!»

> Andrea:  «confermo».

> Paolo: **OK**, 'value' è ora opzionale



2) (2B) In merito ai manoscritti, andando sotto ms units - sezione general - il campo sheet count non ammette numeri superiori a 100 e servirebbe che questo limite fosse tolto.

> Paolo: **OK**, ora il limite pare essere a 1000. Ma non penso ci siano in giro MSS con più di 1000 fogli.



3) Sempre sotto ms units, ma sotto leaf sizes e area sizes - bisogna invertire in entrambi i casi l'ordine di width e height.

> Paolo: **OK**. Nella versione online (vers. precedent) era width/height/depth; nella nuova versione è height/width/depth
