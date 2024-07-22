# Data warehouse - koppelmogelijkheden

## CSV export <a href="#toc154666882" id="toc154666882"></a>

Het Signalen systeem kan periodiek een CSV export maken van alle data in de database (zie [csv-export.md](csv-export.md "mention")). Deze CSV export kan vervolgens direct van de object store of via de REST API opgehaald worden. De CSV bestanden bieden toegang tot een deel van de data die in Signalen opgeslagen wordt.

## PostgreSQL database replica <a href="#toc154666883" id="toc154666883"></a>

Daarnaast is het mogelijk om de data op te halen replica van de database. Deze replica biedt near-realtime toegang tot de data. Toegang tot deze replica is alleen-lezen en biedt in principe toegang tot alle data die er in Signalen opgeslagen wordt.

## Data warehouse - Datamodel <a href="#toc154666884" id="toc154666884"></a>

Voorbeelden

Delta 10 heeft  [een repository gemaakt met voorbeeldqueries](https://github.com/delta10/signalen-bi) die gebruikt kunnen worden als startpunt.

&#x20;

### Belangrijke tabellen

Het datamodel bestaat uit verschillende tabellen. We bespreken hier de belangrijkste tabellen:

&#x20;

Melding

De tabel _signals\_signal_ bevat alle meldingen. De velden _category\_assignment_, _location_, _reporter_, _status, priority, routing\_assignment, user\_assignment_ en _type\_assignment_ bevatten de huidige waarde van het veld. Wanneer een veld in de geschiedenis meerdere waarden heeft gehad, kunnen alle historische waarden opgehaald worden via de specifieke tabel.

&#x20;

Het veld _extra\_properties_ bevat de antwoorden op additionele vragen die gesteld worden voor specifieke categorieën, en kan bijvoorbeeld een lantaarnpaalnummer bevatten voor een melding over een kapotte lantaarnpaal.

&#x20;

Locatie

De tabel _signals\_location_ bevat de actuele en historische locatie van de melding. In het veld geometrie is de geolocatie terug te vinden. Het veld _address_ bevat een adres op het moment dat een melding in de buurt van een adres is.

Het veld _area\_code_ en _area\_type\_code_ bevat het gebied waarbinnen de melding valt voor het gebiedstype dat als standaard is ingesteld in de backend.

&#x20;

Bijlage

De tabel _signals\_attachment_ kan een verwijzing naar één of meerdere bijlagen van de melding bevatten, bijvoorbeeld de foto's die door de melder zijn meegestuurd. Het veld file verwijst naar het pad op de bestandsopslag van Signalen.

&#x20;

Bron

De tabel _signals\_source_ bevat de verschillende mogelijke bronnen die instelbaar zijn per gemeente. Meldingen via de frontoffice krijgen altijd de bron "online" mee. De medewerker in de backoffice kan bij het aanmaken kiezen tussen de aangeboden opties, maar kan geen melding met de bron "online" maken.

&#x20;

Status

De tabel _signals\_status_ bevat de huidige en historische statuswijzigingen van een melding. Een statuswijziging kan een tekst bevatten voor interne doeleinden of terugkoppeling naar de melder.

Het statusveld kan de volgende statussen bevatten:

·         m: Gemeld

·         i: In afwachting van behandeling

·         b: In behandeling

·         h: On hold

·         o: Afgehandeld

·         a: Geannuleerd

·         reopened: Heropend

·         closure requested: Verzoek tot afhandeling

·         ingepland: Ingepland

·         reopen requested: Verzoek tot heropenen

·         reaction requested: Reactie gevraagd (van melder, voor meer informatie)

·         reaction received: Reactie ontvangen (van melder)

·         forward to external: Doorgezet naar extern systeem

En een aantal statussen specifiek voor koppelingen met externe systemen:

·         ready to send: Klaar om te verzenden

·         sent: Verzonden

·         send failed: Verzenden mislukt

·         done external: Extern afgehandeld

&#x20;

Melder

De tabel _signals\_reporter_ bevat het e-mailadres en/of telefoonnummer van de melder. Het is ook mogelijk om anoniem te melden. Meldingen kunnen na een bepaalde periode geanonimiseerd worden. In dat geval wordt het veld e-mailadres en telefoonnummer leeggemaakt en wordt _email\_anonymized en phone\_anonymized_ op waar gezet. De melder kan aangeven of de contactgegevens met derden gedeeld mogen worden in het veld _sharing\_allowed_.

&#x20;

Afdeling

De tabel _signals\_department_ bevat de verschillende afdelingen van de gemeente met hun eigen interne code. Via de tabel _signals\_categorydepartment_ wordt een afdeling gekoppeld aan een of meerdere categorieën en wordt bepaald of de afdeling alleen recht heeft om meldingen uit de categorie te bekijken (_can\_view)_ of dat de afdeling ook verantwoordelijk is voor de categorie (_is\_responsible_).

Een gebruiker kan lid zijn van één of meerdere afdelingen en krijgt op deze manier toegang tot de meldingen.

&#x20;

Behandelende afdeling

De tabel _signals\_signaldepartments_ bevat alle historische behandelende afdelingen van een melding. Via de tabel _signals\_signaldepartments\_departments_ worden de behandelende afdelingen gekoppeld aan de melding.

&#x20;

Categorieën

De tabel _signals\_category_ bevat de verschillende categorieën meldingen die aanwezig zijn. Iedere gemeente kan een eigen categorieindeling kiezen. Elke categorie kan een servicedoel in dagen hebben, dat opgeslagen zit in de tabel _signals\_servicelevelobjective_. Dit servicedoel kan berekend worden in werkdagen of totaal aantal dagen.

&#x20;

Categorietoewijzing

De tabel _signals\_category\_assignment_ bevat alle historische categorietoewijzingen van een melding. Bij het plaatsen van een melding in een categorie wordt op basis van het serviceniveau van de categorie automatisch het veld _deadline_ en _deadline\_factor\_3_ berekend. Dit is de datum waarop de melding volgens het service doel opgelost moet zijn.

&#x20;

Gebieden

In de tabellen _signals\_area en signals\_areatype_ kunnen verschillende gebieden en gebiedstypes ingeladen worden per gemeente.

In de database worden toewijzingen van meldingen aan bepaalde gebieden alleen opgeslagen voor het standaard gebiedstype. Met behulp van een geo-query kan een overzicht gemaakt worden van meldingen voor een gebiedstype dat niet standaard is.

&#x20;

Additionele vragen

In de tabel _signals\_question_ en _signals\_categoryquestion_ is de configuratie voor additionele vragen terug te vinden. Wanneer een melding geclassificeerd wordt in een bepaalde categorie kan aan de melder een additionele vraag gesteld worden.

Bijvoorbeeld bij kapotte verlichting kan gevraagd worden aan de melder om de verlichting op de kaart aan te klikken, of bij afval kan gevraagd worden of het om een boven- of ondergrondse container gaat. De functioneel beheerder van de gemeente kan deze vragen zelf instellen.

&#x20;

### Formaat van velden

Signalen kent de volgende veldformaten:

·         Integer: een numeriek veld

·         String: een textueel veld

·         Geo: in alle gevallen een punt met een X,Y coordinaat, opgeslagen in EPSG:4326 projectie

·         Datum/tijd: een datum + tijd paar, opgeslagen in UTC

·         JSON veld: complex veld met verschillende (key, value) paren. Bijvoorbeeld het veld _extra\_properties_

#### Visuele weergave (belangrijkste velden)

<figure><img src=".gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

#### **Visuele weergave (volledige database mrt-2024)**

<figure><img src=".gitbook/assets/Signalen datamodel.png" alt=""><figcaption></figcaption></figure>
