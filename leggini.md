step 2

libreia clsx è una libreria che ti consente di alternare facilmente i nomi delle classi. Ti consigliamo di dare un'occhiata alla documentazione per maggiori dettagli, ma ecco l'utilizzo di base

https://nextjs.org/learn/dashboard-app/css-styling
https://www.npmjs.com/package/clsx


step 3 
https://nextjs.org/learn/dashboard-app/optimizing-fonts-images

---- per i caratteri:
seleziona il carattere/i della tua applicazione nel file fonts.ts

https://fonts.google.com/

https://nextjs.org/docs/app/building-your-application/optimizing/fonts#using-multiple-fonts

https://nextjs.org/docs/app/api-reference/components/font#font-function-arguments

consulta questi link per impostare nel progetto il carattere desiderato

step 4
https://nextjs.org/learn/dashboard-app/creating-layouts-and-pages

in questo step si vedono le rotte create con le cartelle che all'interno hanno un file page.tsx. all'interno di una cartella e' possibile creare un file layout che permette di creare ulteriori rotte da quella cartella che e' possibile gestire dalla page.tsx di quella cartella che funge da home. per creare cioe' sezioni dell'applicazione con rotte, isolate dal resto. inoltre si e' parlato di render parziale, cioe il contenuto del layout e' statico, e il rendering interessa solo le pagine che sono chiamate nelle rotte. si migliorano le prestazioni.

step 5

ogni volta che <Link>i componenti appaiono nel viewport del browser, Next.js precarica automaticamente il codice per il percorso collegato in background. Nel momento in cui l'utente fa clic sul collegamento, il codice per la pagina di destinazione sarà già caricato in background, e questo è ciò che rende la transizione della pagina quasi istantanea!

step 6 connessione a database. 

creare repository ghithub
https://docs.github.com/en/get-started/quickstart/create-a-repo


https://nextjs.org/learn/dashboard-app/setting-up-your-database

bisogna mettere on line un progetto attravero il repositoy di github, poi collegare un database. il profilo hobbies di vercell permette un solo data base attivo alla volta

step 7 

https://nextjs.org/learn/dashboard-app/fetching-data

la gestione delle rotte per chiamate al data base e per recupero file dal client. sono server side perche vendgono eseguite dal server. possono essere fatte in ogni componente servere o anche organizzare le chiamte nella cartella api. in questo caso, cioe quando si costruisce una cartelle paer le rotte si usa il file route.ts. dove vengono indirizzare le chiamate da next. ogni route.ts riconosce i verbi delle crud. 

https://nextjs.org/docs/app/building-your-application/routing/route-handlers


usiamo vercel che fornisce la funzion sql. uno strumento che protegge la sintissi sql da iniezioni
https://vercel.com/docs/storage/vercel-postgres/sdk#sql

nell esempio il componete server importa le funzioni di recupero dati da fil da.ts. sono funzioni che vengono importate nel componente(deve essere async) e chiamate dove si usano per ricevere i dati.

interessante l'uso di Promise.all([]) che accetta un arrayi di promesse await che esegue in contemporanea. si noti che tali richieste non sono dipendenti tra loro.


step 8 

https://nextjs.org/learn/dashboard-app/static-and-dynamic-rendering

il rendering statico permette di costruire lato servere i componenti e il recupero dati. tutto cio viene memorizzato nella catch. il client al momento della chiamata interroga dunque la catch e prende da essa i dati.

se serve invece un recupero dei dati in tempo reale, con dati aggiornati in tempo reale bisogna passare ad un rendering dinamico.

il rendering dinamico invece avviene al momento della richiesta del client, la che in questo caso non interviene, idati sono presi direttamento dal DB aggiornati.

import { unstable_noStore as noStore } from 'next/cache';
 
export async function fetchRevenue() {
  // Add noStore() here to prevent the response from being cached.
  // This is equivalent to in fetch(..., {cache: 'no-store'}).
  noStore();
 
  // ...
}

altrimenti consultare anche:
https://nextjs.org/docs/app/api-reference/file-conventions/route-segment-config

bisogna tutttavia considerare che Con il rendering dinamico, la tua applicazione è veloce quanto il recupero dei dati più lento.

step 9 lo streaming
Diamo un'occhiata a come migliorare l'esperienza dell'utente in caso di richieste di dati lente.
https://nextjs.org/learn/dashboard-app/streaming

Lo streaming è una tecnica di trasferimento dati che consente di suddividere un percorso in "pezzi" più piccoli e di trasmetterli progressivamente dal server al client non appena sono pronti.
Esistono due modi per implementare lo streaming in Next.js:

A livello di pagina, con il loading.tsxfile.
Per componenti specifici, con <Suspense>.
1. loading.tsx è uno speciale file Next.js costruito su Suspense, che ti consente di creare un'interfaccia utente di fallback da mostrare in sostituzione durante il caricamento del contenuto della pagina. inoltre visto che la nav bar della pagina e' statica, essa e' visibile da subito e quindi anche durante lo striming, puo essere azionata per direzionare in altre pagine ... si chaima navigazione interrompibile.

i gruppi di percorso 
https://nextjs.org/docs/app/building-your-application/routing/route-groups

I gruppi di percorsi consentono di organizzare i file in gruppi logici senza influenzare la struttura del percorso dell'URL. Quando crei una nuova cartella utilizzando le parentesi (), il nome non verrà incluso nel percorso dell'URL. Quindi /dashboard/(overview)/page.tsx diventa /dashboard.

In questo caso stai utilizzando un gruppo di percorsi per assicurarti che loading.tsxsi applichi solo alla pagina di panoramica della dashboard. 

lo streaming di un componente
https://nextjs.org/learn/dashboard-app/streaming#streaming-a-component

La sospensione ti consente di rinviare il rendering di parti della tua applicazione fino a quando non vengono soddisfatte alcune condizioni (ad esempio, i dati vengono caricati). Puoi avvolgere i tuoi componenti dinamici in Suspense. Quindi, passagli un componente di fallback da mostrare durante il caricamento del componente dinamico.

Il luogo in cui collochi i confini della suspense varierà a seconda dell'applicazione. In generale, è buona norma spostare i recuperi dei dati nei componenti che ne hanno bisogno, quindi avvolgere tali componenti in Suspense. Ma non c'è niente di sbagliato nello streaming delle sezioni o dell'intera pagina se è ciò di cui ha bisogno la tua applicazione.
Spostando il recupero dei dati ai componenti che ne hanno bisogno, puoi creare confini di Suspense più granulari. Ciò consente di eseguire lo streaming di componenti specifici e impedire il blocco dell'interfaccia utente.

step 10 (facoltatico) il prerendering parziale

si tratta di una funzionalita sperimentale di next.js in pratica combina il rendering dinamico e quello parziale.

siccome  se chiami una funzione dinamica all'interno del tuo percorso (ad esempio noStore(), cookies(), ecc.), l'intero percorso diventa dinamico, si puo imperdire questa assolutizzazione e chrere dei buchi (hole) in un componente statico dove si inseriscono i componenti dinamici, come recupero dati, ecc.
https://nextjs.org/learn/dashboard-app/partial-prerendering

step 11

Learn how to use the Next.js APIs: searchParams, usePathname, and useRouter.
https://nextjs.org/learn/dashboard-app/adding-search-and-pagination

uso di useSearchParams
bisogna importare l'hook, creare una variabie con useSearchParams nel componente e creare un nuovo UrlSerachParams con la variabile creata
https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams

si usa usePatname e useRouter

uso combinato tra i due, in praca si ottine la path attuale con usePatname e di usa useRouter con metodo Replace (di useRouter) per andare in altra pagina

Best practice: Debouncing

Il debouncing è una pratica di programmazione che limita la velocità con cui una funzione può attivarsi. 
Evento trigger : quando si verifica un evento che dovrebbe essere rimbalzato (come la pressione di un tasto nella casella di ricerca), viene avviato un timer.
Attendi : se si verifica un nuovo evento prima della scadenza del timer, il timer viene reimpostato.
Esecuzione : Se il timer raggiunge la fine del conto alla rovescia, viene eseguita la funzione antirimbalzo.
Puoi implementare il antirimbalzo in diversi modi, inclusa la creazione manuale della tua funzione antirimbalzo. Per semplificare le cose, utilizzeremo una libreria chiamatause-debounce


step 12 Mutating Data
https://nextjs.org/learn/dashboard-app/mutating-data