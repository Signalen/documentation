---
icon: brain-circuit
---

# Machine learning

## Architectuur van het model

De tekst van de melding wordt opgedeeld in losse woorden. Van elk woord uit een melding wordt geanalyseerd hoe uniek het is voor die melding, afgezet tegen de de totale collectie woorden (‘TF-IDF’ of ‘term frequency-inverse document frequency’). Een woord als ‘de’ of ‘bedankt’ krijgt daardoor een laag gewicht en een woord als ‘vuilnis’ krijgt een hoger gewicht. Van die combinatie van woorden wordt vervolgens bepaald bij welke categorie de melding hoort en daarmee bij welke afdeling binnen de gemeente de melding het meest waarschijnlijk past.

## Automatische classificatie

Het classificatiemodel wordt getraind op basis van CSV bestand met de volgende kolommen:

| Main              | Sub             | Text            |
| ----------------- | --------------- | --------------- |
| \[Hoofdcategorie] | \[Subcategorie] | Meldingstekst 1 |
| \[Hoofdcategorie] | \[Subcategorie] | Meldingstekst 2 |
| \[Hoofdcategorie] | \[Subcategorie] | Meldingstekst 3 |

De kolom **Main** bevat de hoofdcategorie\
De kolom **Sub** bevat de subcategorie De kolom **Text** bevat de meldingstekst van de melder en kan over alles gaan.<br>

<mark style="background-color:green;">Tip! Maak de koppeling via kolomnaam ID (signals.csv) en \_signal\_id (categories.csv). Ontdubbel op basis van “updated\_at” datum in (categories.csv)​. Doe dit niet in Excel maar in een krachtigere tool zoals PowerBI of Cognos. Maak er eventueel een standaard rapportage voor een volgende keer​.</mark>

Een melding komt op een categorie te staan als machine learning daar ≥ 41% zeker van is. Is de machine learning dat niet? Dan komt de melding op “Overig \[Hoofdcategorie]” te staan.\
Is de machine learning niet >= 41% zeker van de hoofdcategorie? Dan komt de melding op Hoofd- en Subcategorie “Overig” te staan.​

### Hoe leert het model?

Voorbeeld:​

* Je hebt een trainingsbestand van 1.000 regels​
* 800 regels worden gebruikt om van te leren​
* 200 regels worden bewaard en daarmee toetst het algoritme hoe goed het werkt. Uit deze toetsing komen de scores en confusion matrix​
* Waarde per woord​

Hij leert dus ook van typfouten zoals graffiti, grafiti, grafity, graffitti

### Hoe update je zelf je Machine Learning?

Wanneer je een trainingset heb gemaakt kun je zelf je Machine Learning trainen. Volg hiervoor onderstaande stappen:

1. Ga naar Django > Classificatie management > Training sets&#x20;
2. Klik op “Training set toevoegen”&#x20;
3. Geef een naam en kies het .xlsx bestand; klik op Opslaan&#x20;
4.  Vink de regel aan en selecteer de actie “Train model met geselecteerde dataset”&#x20;

    * Neem meldingen uit Signalen mee = Nee&#x20;

    Klik op “Uitvoeren”&#x20;
5. Wacht tot je een groene bevestigingsregel ziet of een rode foutmelding krijgt&#x20;
   * Groen? Ga naar Classifiers&#x20;
   * Rood? Los eerst het probleem in je .xsls bestand op&#x20;
6. Open de regel onder Classifiers en controleer de status van de taak&#x20;
   * Running > ML is nog bezig&#x20;
   * Failed > Controleer de foutmelding en los op&#x20;
   * Completed > ML is gereed&#x20;
7. Klaar? Vink de regel aan, selecteer de actie “Maak deze classifier actief” en klik op uitvoeren&#x20;

**Bekende foutmeldingen**\
&#xNAN;_&#x56;alueError: This solver needs samples of at least 2 classes in the data, but the data contains only one class: 'test' --> de kolom MAIN moet minimaal twee verschillende waardes bevatten_&#x20;

### Onder de motorkap kijken

Je kunt het model aan het werk zien met F12 (rechtermuisknop > inspecteren)​.\
Tabblad "Netwerk"\
Typ de tekst in en kijk bij prediction > tabblad Response/Reactie

<figure><img src="../../.gitbook/assets/image (268).png" alt=""><figcaption></figcaption></figure>

In bovenstaand voorbeeld is de machine learning niet zeker van de subcategorie (37%) maar wel van de hoofdcategorie (92%). Daarom komt deze melding op "Overig \[hoofdcategorie]" te staan.

### Scores van het model

**Precision**: accuraatheid van de voorspelling (true positives / true positives + false positives)\
**Recall**: compleetheid van de voorspelling (true positives / true positives + false negatives)\
**Accuracy**: hoe vaak heeft het model gelijk? (correcte voorspellingen / alle voorspellingen)\
\
Hoe hoger, hoe beter. Maximale score is 1.

<figure><img src="../../.gitbook/assets/image (269).png" alt=""><figcaption></figcaption></figure>

Na het trainen wordt er automatisch een rapport gegenereerd met een confusion matrix. In deze matrix is te zien in hoeverre de voorspelde categorieën (x-as) overeen komen met de werkelijke categorieën (y-as). Het is dus wenselijk dat de diagnonaal zo donker mogelijk van kleur is en de andere waarden zo licht mogelijk.

<figure><img src="../../.gitbook/assets/image (250).png" alt=""><figcaption></figcaption></figure>

### Hoe krijg je het model beter?

Meer maar vooral betere trainingsdata invoeren​. Controleer op correctheid, liefst vooraf​.\
\* Correctheid = staat de melding op de juiste categorie?\
\* Minimaal 50 meldingen per subcategorie\
\* Verwijder testmeldingen, geannuleerde meldingen, meldingen van BuitenBeter en meldingen uit de 'overig'-categorieën uit je dataset

Tekstueel overlappende categorieën samenvoegen​.\
\* Confusion matrix bekijken​ (zie tabel hierboven)\
\* Gebruik niet alleen categorieën, maar ook aanvullende vragen om te routeren

<br>
