---
icon: brain-circuit
---

# Machine learning

## Architectuur van het model&#x20;

De tekst van de melding wordt opgedeeld in losse woorden. Van elk woord uit een melding wordt geanalyseerd hoe uniek het is voor die melding, afgezet tegen de de totale collectie woorden (‘TF-IDF’ of ‘term frequency-inverse document frequency’). Een woord als ‘de’ of ‘bedankt’ krijgt daardoor een laag gewicht en een woord als ‘vuilnis’ krijgt een hoger gewicht. Van die combinatie van woorden wordt vervolgens bepaald bij welke categorie de melding hoort en daarmee bij welke afdeling binnen de gemeente de melding het meest waarschijnlijk past.

## Automatische classificatie

Het classificatiemodel wordt getraind op basis van CSV bestand met de volgende kolommen:

| Text            | Main                              | Middle            | Sub             |
| --------------- | --------------------------------- | ----------------- | --------------- |
| Meldingstekst 1 | Wel invullen, wordt niet gebruikt | \[Hoofdcategorie] | \[Subcategorie] |
| Meldingstekst 2 | Nvt                               | \[Hoofdcategorie] | \[Subcategorie] |
| Meldingstekst 3 | Nvt                               | \[Hoofdcategorie] | \[Subcategorie] |

De kolom **Text** bevat de meldingstekst van de melder en kan over alles gaan.\
De kolom **Main** is nodig om de machine learning te laten werken maar doet feitelijk niets. Vul een dummy-waarde in zoals Nvt of Test\
De kolom **Middle** bevat de hoofdcategorie\
De kolom **Sub** bevat de subcategorie

<mark style="background-color:green;">Tip! Maak de koppeling via kolomnaam ID (signals.csv) en \_signal\_id (categories.csv). Ontdubbel op basis van “updated\_at” datum in (categories.csv)​. Doe dit niet in Excel maar in een krachtigere tool zoals PowerBI of Cognos. Maak er eventueel een standaard rapportage voor een volgende keer​.</mark>

Een melding komt op een categorie te staan als machine learning daar ≥ 41% zeker van is. Is de machine learning dat niet? Dan komt de melding op “Overig \[Hoofdcategorie]” te staan. \
Is de machine learning niet >= 41% zeker van de hoofdcategorie? Dan komt de melding op Hoofd- en Subcategorie “Overig” te staan.​

### Hoe leert het model?

Voorbeeld:​

* Je hebt een trainingsbestand van 1.000 regels​
* 800 regels worden gebruikt om van te leren​
* 200 regels worden bewaard en daarmee toetst het algoritme hoe goed het werkt. Uit deze toetsing komen de scores en confusion matrix​
* Waarde per woord​

Hij leert dus ook van typfouten zoals graffiti, grafiti, grafity, graffitti

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
\* Correctheid = Staat de melding op de juiste categorie?​

Tekstueel overlappende categorieën samenvoegen​\
\* Confusion matrix bekijken​ (zie tabel hierboven)\
\* Gebruik niet alleen categorieën, maar ook aanvullende vragen om te routeren

\
