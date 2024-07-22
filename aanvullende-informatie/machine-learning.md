# Machine learning

## Architectuur van het model&#x20;

De tekst van de melding wordt opgedeeld in losse woorden. Van elk woord uit een melding wordt geanalyseerd hoe uniek het is voor die melding, afgezet tegen de de totale collectie woorden (‘TF-IDF’ of ‘term frequency-inverse document frequency’). Een woord als ‘de’ of ‘bedankt’ krijgt daardoor een laag gewicht en een woord als ‘vuilnis’ krijgt een hoger gewicht. Van die combinatie van woorden wordt vervolgens bepaald bij welke categorie de melding hoort en daarmee bij welke afdeling binnen de gemeente de melding het meest waarschijnlijk past.

## Automatische classificatie

Het classificatiemodel wordt getraind op basis van een Excel of CSV bestand met de volgende kolommen:

* Hoofdcategorie
* Subcategorie
* Meldingstekst

Na het trainen wordt er automatisch een rapport gegenereerd met een confusion matrix. In deze matrix is te zien in hoeverre de voorspelde categorieën (x-as) overeen komen met de werkelijke categorieën (y-as). Het is dus wenselijk dat de diagnonaal zo donker mogelijk van kleur is en de andere waarden zo licht mogelijk.

<figure><img src="../.gitbook/assets/image (250).png" alt=""><figcaption></figcaption></figure>

Ook komen er drie scores (precision, recall, accuracy) van 0 tot 1 uit, die de kwaliteit van het model bepalen. Hierbij is 1 de beste score.

<figure><img src="../.gitbook/assets/image (249).png" alt=""><figcaption></figcaption></figure>
