---
icon: link
---

# Koppeling met externe systemen

## Signalen REST API

De volledige functionaliteit van Signalen is te gebruiken via de REST API. Deze API wordt gebruikt door de frontend, maar kan ook gebruikt worden door externe systemen om informatie uit Signalen te halen en acties uit te voeren. Denk bijvoorbeeld aan het veranderen van de status van een melding en het plaatsen van interne notities.

### Techniek

Een extern systeem authenticeert zich bij Signalen met een systeemgebruiker door middel van een JWT token. Dit token wordt meegestuurd in de Authorization header. Door middel van rechten en rollen kan ingesteld worden welke acties toegestaan zijn voor de systeemgebruiker.

&#x20;

De volledige API documentatie kan bekeken worden via de [OpenAPI specificatie](https://api.acc.meldingen.amsterdam.nl/signals/swagger/).

&#x20;

Voorbeeld: extern taakafhandelsysteem

Met behulp van de API is het onder andere mogelijk om een koppeling te realiseren met een extern taakafhandelsysteem. Meldingen die op een bepaalde categorie staan kunnen geautomatiseerd opgepakt worden door het externe systeem en het externe systeem kan na afhandeling de status terugkoppelen.

Het externe taakafhandelsysteem kan periodiek de Signalen API pollen op basis van de status Gemeld en eventueel een specifieke afdelingscode met:

&#x20;

```
GET /signals/v1/private/signals/?status=m&routing_department_code=<afdelingscode>
...
"results": [
    {
        "id": 1,
        ...
    }
]
```

Het externe systeem kan vervolgens voor iedere nog niet opgepakte melding een melding aanmaken in het eigen systeem en het meldingsnummer van Signalen opslaan bij de melding in het eigen systeem. Daarna koppelt het externe systeem de status "In afwachting van behandeling" terug naar Signalen met behulp van het volgende request:

```
PATCH /signals/v1/private/signals/{id}
{
    "status": {
        "state": "i",
        "text": "In behandeling via <naam externe applicatie>"
    }
}
```

Zodra de melding is afgehandeld in het externe systeem kan het externe systeem de status "Extern: verzoek tot afhandeling" terugkoppelen naar Signalen met behulp van het volgende request:

```
PATCH /signals/v1/private/signals/{id}
{
    "status": {
        "state": "closure requested",
        "text": "Afgehandeld via <naam externe applicatie>: <omschrijving>"
    }
}
```

De behandelaar in Signalen kan vervolgens de afhandeling beoordelen en de afhandeling verzorgen naar de melder door de melding op "Afgehandeld" te zetten.

&#x20;

#### Rekening houden met tussentijdse wijzigingen in Signalen

Eventueel kan het externe taakafhandelsysteem rekening houden met het feit dat meldingen - nadat ze verzonden zijn naar het externe systeem - aangepast worden in Signalen. Denk bijvoorbeeld aan het aanpassen van de categorie of een status.

Dit kan het externe taakafhandelsysteem doen door periodiek de API te pollen voor de lopende meldingen en meldingen af te sluiten in het eigen systeem op het moment dat de categorie gewijzigd wordt of de status aangepast wordt.

## Statussen

Signalen kent diverse statussen die uitgewisseld kunnen worden:\
\
&#x20; Gemeld = 'm',

&#x20; In Afwachting van behandeling = 'i',

&#x20; Behandeling = 'b',

&#x20; Afgehandeld = 'o',

&#x20; Ingepland = 'ingepland',

&#x20; Geannuleerd = 'a',

&#x20; Gesplitst = 's',

&#x20; VerzoekTotHeropenen = 'reopen requested',

&#x20; ReactieGevraagd = 'reaction requested',

&#x20; ReactieOntvangen = 'reaction received',

&#x20; Heropend = 'reopened',

&#x20; TeVerzenden = 'ready to send',

&#x20; Verzonden = 'sent',

&#x20; VerzendenMislukt = 'send failed',

&#x20; VerzoekTotAfhandeling = 'closure requested',

&#x20; DoorgezetNaarExtern = 'forward to external',

&#x20; AfgehandeldExtern = 'done external',



## Sigmax City Control

Deze koppeling is specifiek ontwikkeld voor Sigmax City Control en werkt op basis van STuF-ZKN. Met de juiste autorisatie kan de behandelaar in Signalen een melding doorzetten naar City Control door op het knopje "THOR" te klikken. Er wordt in Signalen een interne notitie aangemaakt en de melding wordt op de status "Extern: verzonden" gezet.

Als de melding in City Control is afgehandeld wordt de status vanuit City Control doorgestuurd naar Signalen. De afhandelstatus wordt opgeslagen in een interne notitie in Signalen en de melding wordt op de status "Extern: afgehandeld" gezet.

### Techniek

De koppeling is tweeweg en werkt op basis van STuF-ZKN 1.0. Er worden drie berichten gebruikt:

·         creeerZaak: Maakt een zaak aan vanuit Signalen in City Control

·         voegZaakdocumentToe: Voeg bijlagen toe vanuit Signalen aan de zaak in City Control

·         actualiseerZaakstatus: Koppel de status terug vanuit City Control aan Signalen

&#x20;

Signalen authenticeert op basis van Basic authentication bij City Control. City Control authenticeert op basis van een systeemgebruiker met een JWT token bij Signalen.

Signalen biedt daarnaast de mogelijkheid om op basis van tweezijdig TLS te authenticeren. Dit kan worden gebruikt als de gemeente ervoor kiest om een API gateway tussen het verkeer van Signalen en City Control te plaatsen.

### AVG en WPG

De meldingen in Signalen vallen onder de AVG wetgeving, niet onder WPG. De reden hiervoor is dat een MOR melding geen formele constatering is op basis waarvan een BOA kan handhaven. Een handhaver moet altijd zélf de constatering doen en dat doen ze in een handhaafapplicatie zoals CityControl.\
\
Voor de volledigheid: Bovenstaande informatie is getoetst bij privacy officers van diverse gemeenten, de FG van gemeente Amsterdam en de THOR product owner van gemeente Amsterdam.

## MOON koppeling

Een melding wordt door MOON opgehaald en in hun systeem gezet. Dit gebeurd in overleg met de gemeente. Vaak op basis van een combinatie van Status, Afdeling en Subcategorie. \
Daarnaast verzorgd MOON een WFS service waardoor er objecten op de kaart en in een lijstweergave getoond kunnen worden.\
\
In gebruik bij o.a. gemeenten Groningen, 's-Hertogenbosch en Enschede.

Onderstaande tabel is een voorbeeld. Alles is in samenwerking met MOON af te stemmen waaronder de tekst in Signalen en wanneer er een mail naar de melder moet worden verstuurd.

<table><thead><tr><th width="209">Status MOON</th><th width="74">Code</th><th width="140">Status Signalen</th><th width="222">Tekst Signalen</th><th>Mail naar melder</th></tr></thead><tbody><tr><td>// 0.0 Melding nog niet gehonoreerd</td><td>i</td><td>IN AFWACHTING VAN TOEWIJZING</td><td>Moon: Melding nog niet gehonoreerd</td><td>Nee</td></tr><tr><td>// 0.1 Locatie onbekend</td><td>i</td><td>IN AFWACHTING VAN TOEWIJZING</td><td>Moon: Locatie onbekend</td><td>Nee</td></tr><tr><td>// 0.2 Geen contractpartner toegekend</td><td>i</td><td>IN AFWACHTING VAN TOEWIJZING</td><td>Moon: Geen contractpartner toegekend</td><td>Nee</td></tr><tr><td>// 2.0 Aannemer</td><td>m</td><td>GEMELD</td><td>Uw melding is doorgezet naar onze aannemer.</td><td>Nee</td></tr><tr><td>// 2.1 Aannemer - afwachting van onderaannemer</td><td>o</td><td>AFGEHANDELD</td><td>Onze aannemer heeft vastgesteld dat het om een netwerkstoring gaat. De storing is doorgegeven aan de netwerkbeheerder. Een netwerkstoring kan wat langer duren dan het vervangen van een gewone defecte lamp. Wij werken met onze aannemer / Enexis inmiddels aan het herstel van deze storing. Wij hopen de verlichting zo spoedig mogelijk te herstellen en vragen hiervoor uw begrip. Om administratieve redenen geven wij nu de status ‘afgehandeld’ aan uw melding.</td><td>Ja</td></tr><tr><td>// 3.1 Monteur - storing in behandeling</td><td>i</td><td>IN AFWACHTING VAN TOEWIJZING</td><td>Moon: Aannemer - afwachting van onderaannemer</td><td>Nee</td></tr><tr><td>// 3.2 Aannemer - afwachting van netleverancier</td><td>i</td><td>IN AFWACHTING VAN TOEWIJZING</td><td>Moon: Monteur - storing in behandeling</td><td>Nee</td></tr><tr><td>// 3.2 Monteur - storing onvolledig / niet te verwerken</td><td>i</td><td>IN AFWACHTING VAN TOEWIJZING</td><td>Moon: Monteur - storing onvolledig / niet te verwerken</td><td>Nee</td></tr><tr><td>// 3.2 Monteur - materiaal in bestelling</td><td>ingepland</td><td>INGEPLAND</td><td>We hebben materiaal besteld om uw melding te kunnen behandelen. Wij hopen de verlichting zo spoedig mogelijk te herstellen en vragen hiervoor uw begrip.</td><td>Ja</td></tr><tr><td>// 3.3 Monteur - storing verwerkt</td><td>b</td><td>IN BEHANDELING</td><td>Moon: Monteur - storing verwerkt</td><td>Nee</td></tr><tr><td>// 3.4 Aannemer - storing goedgekeurd</td><td>b</td><td>IN BEHANDELING</td><td>Moon: Aannemer - storing goedgekeurd</td><td>Nee</td></tr><tr><td>// 4.0 Beheerder</td><td>i</td><td>IN AFWACHTING VAN TOEWIJZING</td><td>Moon: Beheerder</td><td>Nee</td></tr><tr><td>// 4.1 Beheerder - opdracht voor verwerking</td><td>i</td><td>IN AFWACHTING VAN TOEWIJZING</td><td>Moon: Beheerder - opdracht voor verwerking</td><td>Nee</td></tr><tr><td>// 4.2 Beheerder - afwachting van netleverancier</td><td>o</td><td>AFGEHANDELD</td><td>Onze aannemer heeft vastgesteld dat het om een netwerkstoring gaat. De storing is doorgegeven aan de netwerkbeheerder. Een netwerkstoring kan wat langer duren dan het vervangen van een gewone defecte lamp. Wij werken met onze aannemer / Enexis inmiddels aan het herstel van deze storing. Wij hopen de verlichting zo spoedig mogelijk te herstellen en vragen hiervoor uw begrip. Om administratieve redenen geven wij nu de status ‘afgehandeld’ aan uw melding.</td><td>Ja</td></tr><tr><td>// 4.3 Beheerder - verwerking afgekeurd</td><td>i</td><td>IN AFWACHTING VAN TOEWIJZING</td><td>Moon: Beheerder - verwerking afgekeurd</td><td>Nee</td></tr><tr><td>// 4.4 Beheerder - verwerking goedgekeurd</td><td>o</td><td>AFGEHANDELD</td><td>De verlichting is hersteld.</td><td>Ja</td></tr></tbody></table>



## Luminizer koppeling

Betreft openbare verlichting. Het koppelvlak is technisch gelijk aan dat van de gemeente Utrecht.

## Cityview koppeling

Betreft openbare verlichting. Gemeente Zaanstad is hiermee gekoppeld.

## Nobralux / Lightweb

Betreft openbare verlichting. Gaat in 2025 over naar Cityview. In gebruik bij gemeente Assen.

## TechView

Bij gemeente Helmond in gebruik. TechView haalt meldingen op uit Signalen en zet ze in de eigen applicatie. Statuswijzigingen in TechView worden ook naar Signalen verstuurd waardoor er een actuele status in beide systemen te zien is. Via de WFS service worden objecten op de kaart getoond en is voor de melder ook te zien wanneer een object al is gemeld. \
\
Storingen die direct in TechView worden gemaakt worden als anonieme melding naar Signalen gestuurd zodat daar ook een volledig overzicht is.

## BuitenBeterApp

Applicatie is gebouwd door Beheervisie/Progresity. Gratis te gebruiken voor melders. De melder kan de voortgang van de melding zien in de BuitenBeter app.&#x20;

Tegen betaling is een koppeling tussen de BuitenBeterApp en Signalen te realiseren. Meldingen die in de BuitenBeterApp worden gedaan komen dan netjes in Signalen terecht. De melder kan de voortgang van de melding in de BuitenBeterApp terug zien.

Wanneer je geen koppeling wilt kun je, indien gewenst, gebruik maken van de e-mails die Beheervisie/Progresity naar een algemeen mailadres van de gemeente stuurt. De e-mails hebben altijd hetzelfde format en kunnen met behulp van een servicegateway of broker worden opgepakt en in Signalen worden gezet. De melder kan de voortgang dan **niet** terug zien in de BuitenBeter app.

## Zo Gemeld

Applicatie is gebouwd door marktpartij Delta10. Gratis te gebruiken door gebruikers en gemeenten die Signalen gebruiken. Melder kan de voortgang van de melding zien in de Zo Gemeld app. Let op! Ook meldingen die anoniem zijn gedaan kan de melder terugzien en bekijken. Lijkt zeer op [#mijn-meldingenoverzicht](../../signalen-gebruikshandleidingen/schermen-paginas-in-signalen.md#mijn-meldingenoverzicht "mention"). \
\
Wanneer een melder een melding wil maken bij een gemeente die geen Signalen gebruikt dan krijgt de persoon een rode waarschuwing in beeld en kan de melder niet door met het aanmaken van een melding.\
\
Zo Gemeld is er voor inwoners die een melding willen doen. Het melden gaat in vier stappen:\
1\. Een beschrijving van de melding, eventueel met foto's\
2\. De locatie en relevante vragen over de melding\
3\. Contacgegevens\
4\. Controleren en versturen\
\
De app onthoudt de contactgegevens van de melder, zodat deze de volgende keer snel nog een melding kan doen.

## Zo Hersteld

Applicatie gebouwd door marktpartij Delta10. Met Zo Hersteld kunnen behandelaars eenvoudig op telefoon en tablet meldingen afhandelen. In de app kun je meldingen op de kaart bekijken en selecteren om aan een route toe te voegen. Deze route open je in de maps-app die je wilt gebruiken. Vervolgens ga je op je route met de meldingen aan de slag.\
\
In Zo Hersteld kun je meldingen sorteren en filteren op jouw voorkeur, zoals:\
\* Meest recente meldingen\
\* Op basis van de status van meldingen\
\* Meldingen die aan jou zijn toegewezen\
Het is eenvoudig om on-the-to notities en foto's te maken die je kunt toevoegen aan de melding.\
\
Aan het gebruik van Zo Hersteld zijn kosten verbonden. Voor meer informatie kun je contact opnemen met info@delta10.nl



## Djuma

Zaaksysteem. Er is nog geen gemeente gekoppeld met Djuma.

## OpenZaak

Zaaksysteem. Er is nog geen gemeente gekoppeld met OpenZaak.

## Xxllnc

Zaaksysteem. Gemeente Utrecht heeft een minimale koppeling met het oude zaaksysteem van Xxllnc. De koppeling in het oude zaaksysteem maakt een zaak aan met enkel het Signalen meldingsnummer, zodat het KCC bij het zoeken naar een zaak-/meldingsnummer kan herkennen dat het om een Signalen melding ging. \
\
Utrecht gaat over naar het nieuwe zaaksysteem van Xxllnc maar zullen de koppeling niet meenemen. Reden hiervoor is dat het KCC direct in Signalen werkt en niet meer in het zaaksysteem.

## MijnOmgeving

Onbekend.

## 21Qubz

Inzamelen en verwerken van afval- en grondstoffen. Gemeente Assen, Groningen en Amsterdam hebben een koppeling. Gemeente Utrecht heeft de koppeling afgenomen maar is nog niet actief. Samen met de gemeente Zaanstad zijn ze bezig met een doorontwikkeling van de koppeling omdat er diverse wensen zijn over de werking.

## Saver

Applicatie mbt afval. Gemeente Bergen op Zoom heeft hiermee een koppeling gerealiseerd. Saver pollt of er meldingen zijn en zet die in hun systeem. Meldingen die in Saver zijn afgehandeld worden ook in Signalen op Afgehandeld gezet.

## Rioned

Applicatie voor o.a. riolering. Gemeente Den Haag heeft hiermee een koppeling. Werkt nog niet goed ivm tonen vlakken, daar kan Signalen nog niet mee om gaan.

## KCM

Externe klanttevredenheidsonderzoek tool. Gemeente Utrecht maakt hier gebruik van. \
In de mail template "Send mail signal handled" wordt het stuk over KTO vervangen door een link naar de externe KTO tool. Deze externe KTO tool werkt niet via een API maar de variabelen zijn via een door de KTO-leverancier ingerichte URL te benaderen.

```
**Hoe tevreden bent u over de afhandeling van uw melding?**  
Laat het ons weten via de volgende link: [tevredenheidsonderzoek](https://link-naar-de-tool.nl?signal_id={{ signal_id }}&categorie={{ main_category_public_name }}&subcategorie={{ sub_category_public_name }}).
```

In bovenstaand voorbeeld wordt het meldingsnummer, hoofd- en subcategorie opgehaald via query parameters. Een compleet overzicht van alle beschikbare parameters vind je in Django bij de [e-mail-templates](../e-mail-templates/ "mention").

## Klantinfocus

Gemeente Hilversum maakt gebruik van deze externe KTO tool. Werkt hetzelfde als KCM, zie hierboven. Klantinfocus levert vijf smileys met vijf verschillende URLs aan die in de e-mail template "Send mail signal handled" gezet kan worden:

```
**Hoe tevreden bent u over de afhandeling van uw melding?**  
Laat het ons weten via de volgende link: [![Zeer ontevreden](https://websurveys2.govmetric.com/imgs/smileys/svg/standard/smiley-dark-red.svg)](https://link-naar-de-tool.nlQ_HC={{main_category_public_name}}&Q_SC={{sub_category_public_name}}&Q_createdate={{created_at}}&Q_source={{source}})[![Ontevreden](https://websurveys2.govmetric.com/imgs/smileys/svg/standard/smiley-light-red.svg)](https://link-naar-de-tool.nlQ_HC={{main_category_public_name}}&Q_SC={{sub_category_public_name}}&Q_createdate={{created_at}}&Q_source={{source}})[![Neutraal](https://websurveys2.govmetric.com/imgs/smileys/svg/standard/smiley-orange.svg)](https://link-naar-de-tool.nlQ_HC={{main_category_public_name}}&Q_SC={{sub_category_public_name}}&Q_createdate={{created_at}}&Q_source={{source}})[![Tevreden](https://websurveys2.govmetric.com/imgs/smileys/svg/standard/smiley-light-green.svg)](https://link-naar-de-tool.nlQ_HC={{main_category_public_name}}&Q_SC={{sub_category_public_name}}&Q_createdate={{created_at}}&Q_source={{source}})[![Zeer tevreden](https://websurveys2.govmetric.com/imgs/smileys/svg/standard/smiley-dark-green.svg)](https://link-naar-de-tool.nlQ_HC={{main_category_public_name}}&Q_SC={{sub_category_public_name}}&Q_createdate={{created_at}}&Q_source={{source}})  
```
