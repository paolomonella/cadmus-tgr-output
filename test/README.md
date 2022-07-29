## Collaudo Cadmus

1) aprire "quotation fr.", linguetta "general", cliccare sull'icona viola con il +, inserisco i campi "work*" e "location*" e selezio cf. dal menù a tendina "tag" (concludo cliccando prima su "accept changes" e poi su "save"). Una volta che riapro l'item, l'informazione relativa al tag non viene salvata. Suppongo possa trattarsi di un bug. In allegato ti ho inviato un video (questione_1) che rende sicuramente più chiaro il problema.

> Daniele: bug risolto. Paolo ha verificato su cadmus v1.1.7 locale

2) Per l'esperienza utente mia e di Elisa, i tooltip non sono particolarmente utili e rendono anche un po' macchinosa la digitazione quando compaiono perché, coprendo altri pulsanti sottostanti, rendono necessario girare attorno con l'icona del mouse affinché scompaiano. Personalmente tutti i pulsanti che hai ideato mi paiono già così intuitivi da non necessitare alcun tooltip (e.g. il tooltip "save data" per il pulsante "save").

> no action required: i tooltip restano
> (in effetti però sarebbe meglio se il tooltip non impedisse all'utente di cliccare sull'elemento)

3) Dopo che si è lavorato in un "apparatus fr." e a distanza di tempo c'è necessità di aggiungere una nuova nota che è a cavallo tra due righe, Cadmus non consente di farlo. La soluzione (che ahimè ho sperimentato) è quella di eliminare tutti i tag esistenti e riaggiungerli uno ad uno - soluzione non molto pratica. Suppongo si tratti di un bug (video questione_3).

> Paolo ha provato su cadmus locale ed è tutto OK

4) all'interno dell'"apparatus fr." il limite di caratteri del campo "value" deve essere aumentato a 700 caratteri perché ho una nota di apparato che supera il limite attuale. Il limite di caratteri del campo "note" tanto sotto "witnesses" come "authors" deve essere aumentato a 200.
- Daniele: «Per 200 fatto. Per 700 non mi e’ chiaro: cioe’ quando inserisci una voce di apparato di tipo NOTA, il campo value non e’ neppure disponibile; c’e’ appunto il campo nota. Quello e’ limitato a 1000. Oppure non era questo che intendevi?»
- Andrea: «Errore mio che non ho specificato. Il limite di caratteri del campo "value" deve essere aumentato a 700 per "replacement", "addition after" e "addition before"».

> A me (Paolo) sembra che il limite sia di 100 caratteri (dovrebbe essere 200)
> sia per apparatus fr. / witnesses / note 
> sia per apparatus fr. / authors / note 
> E mi sembra che sia intorno ai 300 caratteri (dovrebbe essere 700)
> per apparatus fr. / witnesses / entry (type replacement) / value
> (per tutti i type, cioè 'replacement', 'addition after', 'addition before' e 'note').


5) la funzione copia e incolla che abbiamo aggiunto al "linguistic fr." funziona, ma suppongo ci sia probabilmente un altro bug. Quando si copia e poi si incolla, non si riesce a inserire subito anche il lemma, ma bisogna salvare, chiudere e riaprire l'item nuovamente (questione_5).

> Daniele: «Sembrerebbe che la mia versione non abbia questo errore, forse l'ho gia' eliminato con l'upgrade. Comunque se si ripresentasse ditemi e vediamo».
> Paolo: non riesco a testarlo perché io non riesco (probabilmente per colpa mia) a salvare dopo aver inserito i tag linguistici. Lo farei testare direttamente a Andrea a questo punto.

6) la funzione copia e incolla andrebbe aggiunta anche al "witnesses fr."

> Paolo: OK, funziona

7) abbiamo notato che nell'"apparatus fr.", Cadmus è in grado di contare le parole (8.9-9.6 nell'immagine questione_7). Qualora ci fossero due o più note che insistono su porzioni di testo tra loro sovrapposte, la numerazione (nell'esempio riportato) andrebbe da 1 a 8 e nel campo "subrange" non abbiamo mai indicato le righe. Quindi qualora la nota d'apparato riguardasse "Quot praepositiones? Unam, 'ab'." indicheremmo "subrange"=1-4. Confermi che non ci sono problemi di interferenza tra i due sistemi di numerazione?
A seconda della risposta si potrebbe riflettere se sia possibile aiutare in qualche modo chi deve inserire i dati ed evitare che debba contare manualmente le singole parole (evitando così anche banali errori - specialmente nel caso di porzioni di testo più estese).

> Daniele: «Si le numerazioni di subrange sono totalmente distinte dalle altre e non si basano su “coordinate” Y (linea) e X (parola grafica), ma solo su X (parola grafica); 1=prima parola, 2=seconda, etc. Per ora il controllo e’ semplicemente una casella di testo perche’ e’ di uso molto raro (l’unico progetto che ne fa uso e’ il vostro)».

8) in poi...

> Ci sono altre richieste che Andrea ha fatto in email successive, ma oggi non posso più lavorarci. Ci lavoro domani, sempre scrivendo le mie considerazioni in questo file.
