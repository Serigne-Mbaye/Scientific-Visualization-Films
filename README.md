# Visualizzazione scientifica
### *Approfondimento sul cinema*
<hr />

## Autori
984605 Pomayay Gabonal Angello Fernando  
01553A Mbaye Serigne Darou
<hr />

## Acquisizione dati
### kaggle
IL primo dataset sui fil utilizzato lo abbiamo trovato su un sito nel quale è possibile recuperare
diversi tipi di dataset: kaggle. 
https://www.kaggle.com/datasets/kianindeed/imdb-movie-dataset-dec-2023?resource=download  
Contiene 1950 tuple, il dataset è aggiornato al 15 dicembre 2023

Il secondo dataset utilizzato lo abbiamo trovato sempre su kaggle, questo dataset contiene i guadagni
di tutti i film usciti divisi per anno ordinati per rank in base al guadagno più alto al botteghino.
I dati su questo dataset vanno dal 1977 al 2024, il dataset viene aggiornato mensilmente.
https://www.kaggle.com/datasets/jonbown/worldwide-box-office-rankings-1977?resource=download&select=ranking_summary_2024.csv

### Wikidata
Il terzo dataset è quello contenente i dati di tutti gli attori di tutto il mondo. Visto che
l'argomento era il cinema ci è venuta l'idea di create una Choropleth Map in cui mostrare i paesi
nei quali sono nati più attori. Non abbiamo trovato in giro nessun dataset con questi dati ma
grazie a Wikidata Query Service abbiamo raccolto, tramite una query SPARQL, il nome, data di
nascita e stato di nascita di tutti gli attori presenti nel loro database.  
```
SELECT ?actorLabel ?birthDate ?birthCountryLabel
  WHERE
  {
    ?actor wdt:P106 wd:Q33999;  # Filtrare per professione: attore/attrice
         wdt:P569 ?birthDate;  # Data di nascita
         wdt:P19 ?birthPlace.  # Luogo di nascita
    ?birthPlace wdt:P17 ?birthCountry. # Stato di nascita
  
    FILTER(YEAR(?birthDate) >= 1920 && YEAR(?birthDate) < 1930)

    SERVICE wikibase:label { bd:serviceParam wikibase:language"en".}
  }
```
Abbiamo raccolto i dati con query che filtrano con un range di 10 anni perchè per ogni query perchè
Wikidata non permette di fare query con output troppo lunghi. Successivamente abbiamo unito tutti i
csv ottenuti in un unico csv per un totale di 155.489 tuple.

### Google Trends
Il quarto e ultimo dataset contiene i dati sulla popolarità tra Cinema e Serie TV.  
Abbiamo usato Google Trends, i dati presi sono relativi al periodo 2004-2024.

## Descrizione progetto
Il nostro progetto di visualizzazione scientifica, sviluppato utilizzando Jupyter in Python, 
si propone di offrire un'esperienza di visualizzazione avanzata e dinamica dei dati. Abbiamo 
adottato la potente libreria Plotly per la creazione dei grafici, poiché offre una vasta gamma 
di funzionalità interattive e una maggiore flessibilità rispetto a molte altre librerie di 
visualizzazione.

Una delle caratteristiche principali del nostro progetto è l'utilizzo di un approccio dinamico 
per la visualizzazione dei dati. Piuttosto che generare molteplici immagini statiche dello stesso
grafico utilizzando matplotlib, abbiamo scelto di implementare un codice dinamico che permette di 
mostrare più dati su un solo grafico. Questo non solo rende più efficiente il processo di 
visualizzazione, ma consente anche agli utenti di interagire direttamente con il grafico, 
esplorando i dati in modo più intuitivo e approfondito. In più, la nostra soluzione basata su Plotly 
offre un supporto nativo per la visualizzazione in 3D, consentendo agli utenti di esplorare dati 
multidimensionali in modo ancora più dettagliato e coinvolgente.

Inoltre, per garantire una fruizione ottimale dei risultati della nostra analisi durante la 
presentazione, abbiamo adottato una strategia di esportazione dei grafici in formato HTML. Questo 
ci consente di conservare l'interattività e la completezza dei grafici generati con Plotly, 
consentendo agli utenti di visualizzarli facilmente attraverso un browser web. Tutti i grafici 
sono organizzati in una cartella dedicata, facilitando l'accesso e la gestione durante la 
preparazione e la condivisione delle presentazioni.

Tuttavia, un'eccezione è "guadagni_per_anno.ipynb" grafico particolarmente dinamico che utilizza la 
libreria Dash di Plotly. Questo grafico è stato implementato tramite un server interno che offre
un'interfaccia interattiva accessibile attraverso un link nel browser. In questo modo, gli utenti 
possono esplorare i dati sui film dal 1977 fino al gennaio 2024 in tempo reale.

Complessivamente, il nostro progetto di visualizzazione scientifica si distingue per la sua
combinazione di potenza analitica, flessibilità e interattività, offrendo agli utenti una 
presentazione completa per esplorare e comprendere i dati scientifici in modo più efficace
e coinvolgente.
