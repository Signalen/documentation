# Knoppen Delen, THOR, Extern en PDF

<div align="left">

<figure><img src=".gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

</div>

## Delen

Voorwaarden:\
\- Feature flag staat aan\
\- Gebruiker heeft het recht "Splitsen van een melding"\
\- Optioneel: Instellen van de juiste filters

Het komt regelmatig voor dat een melding meerdere acties bevat. Bijvoorbeeld wanneer er durgsafval is gevonden. In zo'n situatie moet handhaving eerst onderzoek plegen en kan daarna het afval worden opgeruimd.\
\
Door een melding te delen ontstaat er een Hoofdmelding met een of meerdere Deelmeldingen. Op deze manier kunnen verschillende afdelingen aan dezelfde melding werken.&#x20;

<table data-header-hidden><thead><tr><th width="40"></th><th></th></tr></thead><tbody><tr><td><strong>!</strong></td><td><mark style="background-color:green;">De originele melding wordt de Hoofdmelding. Er kan <strong>alleen</strong> vanuit de Hoofdmelding gecommuniceerd worden naar de melder. De aan de hoofdmelding gekoppeld afdeling is verantwoordelijk voor de afhandeling van de Hoofdmelding en de communicatie naar de melder toe. Dit noemen we de regiehouder.</mark><br><br><mark style="background-color:green;">Bij het wijzigen van een Deelmelding krijg je als behandelaar een waarschuwing dat je NIET met een melding kunt communiceren en dat je toelichting alleen voor intern gebruik is:</mark><br><img src=".gitbook/assets/image (257).png" alt=""></td></tr></tbody></table>

Klik op de knop _Delen_ om een Standaardmelding te delen en er een Hoofd- en Deelmelding(en) van te maken.\
\
Je krijgt dan eerst de optie om een notitie bij de Hoofdmelding te maken. Tevens zie je het meldingsnummer, de status en de subcategorie van de hoofdmelding.

<figure><img src=".gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

Daaronder staat het scherm om een eerste deelmelding toe te voegen:

<figure><img src=".gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

Kies de subcategorie van de deelmelding en typ een omschrijving die duidelijk maakt wat er van de afdeling wordt verwacht. Op die manier kan er snel gehandeld worden. Pas eventueel de Urgentie en het Type melding aan.\
\
Klik op "Extra deelmelding toevoegen" om meerdere deelmeldingen aan te maken.\
\
Klik op "Opslaan" om de Hoofd- en Deelmelding(en) op te slaan.\
\
Stel eventueel de bijbehorende filters in:

<div align="left">

<figure><img src=".gitbook/assets/image (252).png" alt=""><figcaption></figcaption></figure>

</div>

### Filter: Soort

Met het filter op "Soort" kun je een een selectie maken op Standaard meldingen, Hoofdmeldingen en/of Deelmeldingen.

<div align="left">

<figure><img src=".gitbook/assets/image (152).png" alt=""><figcaption></figcaption></figure>

</div>

### Filter: Verantwoordelijke afdeling

De filter "Verantwoordelijke afdeling" gebruik je in combinatie met een Afdeling. Zo krijg je alle (Hoofd)meldingen te zien waarbij de verantwoordelijke afdeling Afdeling x is. In onderstaand voorbeeld is dat afdeling "B\&P west wijkteam":

<figure><img src=".gitbook/assets/image (254).png" alt=""><figcaption></figcaption></figure>

### Filter: Hoofdmelding MET wijziging in deelmelding

Filter "Hoofdmelding met wijziging in deelmelding" laat een lijst zien van Hoofdmeldingen waarbij er in de onderliggende Deelmelding een wijziging is geweest. De verantwoordelijke afdeling kan aan de hand van de actie in de Deelmelding bepalen of er een bericht naar de melder moet of dat de Hoofdmelding kan worden afgehandeld:\


<figure><img src=".gitbook/assets/image (255).png" alt=""><figcaption></figcaption></figure>

In de Hoofdmelding zie je alle Deelmeldingen terug. Bij de deelmelding waar wat is gewijzigd zie je in de Geschiedenis wat er is gebeurd, zoals een statuswijziging.\
\
Als verantwoordelijke afdeling heb je de keuze om bijv. een bericht naar de melder toe te sturen. Je kunt ook klikken op de knop "Geen actie nodig". Dan verdwijnt de wijziging in de Deelmelding bij de Hoofdmelding en komt deze Hoofdmelding niet meer in het filter "Hoofdmelding MET wijziging in deelmelding" terug. Pas als de Deelmelding opnieuw wordt gewijzigd zal de Hoofdmelding weer in het filter terugkomen.

<figure><img src=".gitbook/assets/image (256).png" alt=""><figcaption></figcaption></figure>

### Filter: Hoofdmelding ZONDER wijziging in deelmelding

Het filter "Hoofdmelding ZONDER wijziging in deelmelding" toont alle Hoofdmeldingen waarbij er géén wijziging in de Deelmelding is geweest.&#x20;

## THOR

Voorwaarden:\
\- Feature flag staat aan\
\- Gebruiker heeft het recht "Doorsturen van een melding (THOR)"\
\- Gemeente maakt gebruik van CityControl en de zaakmodule\
\- Koppeling is gerealiseerd\
\- Optioneel: Instellen van de juiste filters\
\
Deze knop is speciaal gemaakt voor de koppeling tussen Signalen en CityControl, een handhavingsapplicatie van de leverancier Sigmax. De knop kan niet voor andere leveranciers of applicaties worden gebruikt.

De werking is zeer eenvoudig: Je drukt op de knop THOR en de melding wordt vanuit Signalen naar de zaakmodule van CityControl gestuurd. \
\
De melding krijgt in Signalen eerst de status "Extern: te verzenden". De melding wordt nu verzonden.\
![](<.gitbook/assets/image (153).png>)\
\
Zodra de melding succesvol in CityControl is aangekomen wijzigt de status naar "Extern: verzonden"\
![](<.gitbook/assets/image (154).png>)\
In de Geschiedenis van Signalen is het zaaknummer in CityControl terug te zien:\
![](<.gitbook/assets/image (155).png>)\
\
De 'zaak' wordt in CityControl behandeld. Tussentijdse statuswijzigingen of notities worden NIET naar Signalen gestuurd. Het KCC kan de huidige stand van zaken dus niet in Signalen zien.\
\
Wanneer de 'zaak' in CityControl is afgehandeld komt het resultaat in Signalen te staan en wijzigt de status naar "Extern: afgehandeld":\
![](<.gitbook/assets/image (157).png>)\
In de Geschiedenis van Signalen is te zien wat er met de 'zaak' in CityControl is gedaan:\
![](<.gitbook/assets/image (156).png>)

Voor de werking aan de kant van CityControl [koppeling-signalen-citycontrol.md](koppeling-met-externe-systemen/koppeling-signalen-citycontrol.md "mention")

## Extern

Bij sommige meldingen wil je graag dat een externe partij een actie uitvoert of informatie verstrekt. Hier is de functionaliteit "Doorzetten naar externe partij" ontwikkeld, met de bijbehorende knop "Extern".\
\
Klik op de knop "Extern" om een actie uit te zetten naar een externe partij. Vul het e-mailadres in en typ de informatievraag of de actie in het toelichtingenveld:

<div align="left">

<figure><img src=".gitbook/assets/image (158).png" alt=""><figcaption></figcaption></figure>

</div>

Je krijgt een e-mail preview (voorbeeld) te zien van de volledige e-mail die verstuurd zal worden naar de externe partij. Controleer de e-mail en klik op Verstuur.

![](<.gitbook/assets/image (161).png>)\
\
Let op! De link is 14 dagen geldig. Na deze termijn is de link niet meer geldig en kan de externe partij niet meer bij de meldingsinformatie, of de actie voorzien van een reactie.

De status van de melding wijzigt naar "Doorgezet naar extern"\
![](<.gitbook/assets/image (160).png>)

De externe partij kan nu op het linkje klikken in de e-mail. Er wordt dan meer informatie getoond over de melding. Zoals je ziet krijgt de externe partij de meldingstekst van de melder NIET te zien. Hier is bewust voor gekozen omdat een melder soms contactgegevens achter laat of een heel verhaalt typt terwijl maar een klein deel van belang is voor de externe partij.

<div align="left">

<figure><img src=".gitbook/assets/image (162).png" alt=""><figcaption></figcaption></figure>

</div>

Wanneer de externe partij de actie heeft uitgevoerd kan er een reactie worden teruggestuurd. Daarvoor moet de externe opnieuw op de link in de bijlage klikken en kan een toelichting geven en eventueel foto's toevoegen. Klik op "Verstuur" om de actie af te sluiten. De link is daarna ongeldig en kan niet meer worden gebruikt.\
\
De externe partij krijgt een bevestigingsmail zodra de actie is afgerond.

<div align="left">

<figure><img src=".gitbook/assets/image (163).png" alt=""><figcaption></figcaption></figure>

</div>

De melding in Signalen komt op "Extern: Verzoek tot afhandeling" te staan\
![](<.gitbook/assets/image (164).png>)\
In de Geschiedenis van de melding, onder "Toelichting ontvangen" lees je terug wat de externe partij met de melding heeft gedaan. Foto's zijn ook zichtbaar in de melding.

<figure><img src=".gitbook/assets/image (165).png" alt=""><figcaption></figcaption></figure>

De melding komt altijd op de status "Extern: Verzoek tot afhandeling" te staan. Ook als de externe partij niets met de melding heeft gedaan. Dit zie je ook terug in de Geschiedenis. De behandelaar kan opnieuw een actie uitzetten bij de externe partij, de melding verder behandelen of afsluiten.

<table data-header-hidden><thead><tr><th width="40"></th><th></th></tr></thead><tbody><tr><td><strong>!</strong></td><td><mark style="background-color:green;">Deze functionaliteit kun je ook intern gebruiken. Bijvoorbeeld om een collega een vraag te stellen die geen gebruik maakt van Signalen. Je typt dan het e-mailadres in van je collega en die kan de vraag beantwoorden. Op die manier blijven alle acties en informatie in Signalen bij elkaar staan.</mark></td></tr></tbody></table>

\


## PDF

Met de knop PDF wordt een export gemaakt van de melding inclusief meldingstekst, locatie, foto's en geschiedenis. Ook de contactgegevens van de melder, mits je daarvoor geautoriseerd bent, worden in het PDF bestand gezet. Ben je niet geautoriseerd om meldergegevens te zien, dan zullen er sterren staan op de plaats van het telefoonnummer en/of e-mailadres.
