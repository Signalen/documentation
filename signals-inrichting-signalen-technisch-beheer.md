---
icon: gear
---

# Signals (inrichting Signalen (technisch) beheer)

## Categories

Hier kun je subcategorieën toevoegen of op inactief zetten.

Dit is ook mogelijk (en eenvoudiger) in Signalen.

<table data-header-hidden><thead><tr><th width="40"></th><th></th></tr></thead><tbody><tr><td>!</td><td><mark style="background-color:green;">Het deactiveren van Subcategorieën heeft invloed op de werking van de Machine Learning waardoor dit niet zonder gevolgen uitgevoerd kan worden. Advies is om aanpassingen aan subcategorieën volgens een gecontroleerde wijzigingsprocedure uit te voeren.</mark></td></tr></tbody></table>

## Deleted signals

Meldingen die naar aanleiding van de periodic task delete\_signals\_in\_state\_for\_x\_days worden verwijderd komen hier in een lijst te staan. Klik op een regel om metadata te zien zoals aanmaakdatum, categorie en status.

## Departments

Hier kun je afdelingen/teams toevoegen of op inactief zetten.

Klik rechts bovenin op “Department toevoegen” om een afdeling toe te voegen:

<figure><img src=".gitbook/assets/image (92).png" alt=""><figcaption></figcaption></figure>

&#x20;

&#x20;

Je kunt dan een code (max 3 karakters) invullen en de afdeling een naam geven. Vervolgens kun je er categorieën aan toevoegen. Dit laatste is gemakkelijker vanuit Signalen.

<figure><img src=".gitbook/assets/image (93).png" alt=""><figcaption></figcaption></figure>

Open Signalen en controleer bij Instellingen > Afdelingen of je nieuwe afdeling erbij is gekomen

## ExpressionContexts

Instelling ten behoeve van automatische routering op basis van een geprikte locatie op de kaart.

## Expressions

Aan de hand van ‘expressions’ kun je een melding routeren naar een gewenste afdeling.

Een expression werkt met OR of AND

OR = OF en zet je tussen haakjes

AND = EN en hoeft niet tussen haakjes

### &#x20;_Voorbeeld 1:_

(location in areas."district"."Binnenstad" or location in areas."district"."Graafsepoort" or location in areas."district"."Muntel / Vliert" or location in areas."district"."Zuidoost") and AFV\_keuzemogelijkheden == "Illegale stort" and sub == "Vervuiling openbare ruimte"

&#x20;

Bovenstaand voorbeeld kun je lezen als:

Ligt de melding in locatie Binnenstad OF Graafsepoort OF Muntel/Vliert OF Zuidoost EN is het antwoord “Illegale stort” op de vraag “AFV\_keuzemogelijkheden” EN de subcategorie “Vervuiling openbare ruimte”

&#x20;

### _Voorbeeld 2:_

Dierenoverlast\_overig == "Hond" and (Dierenoverlast == "Loslopende hond, waar dat niet mag" or Dierenoverlast == "Bijtende hond. Wij werken samen met de politie. Wilt u s.v.p. ook aangifte doen bij de politie?") and sub == "Dierenoverlast overig"

&#x20;

Bovenstaand voorbeeld kun je lezen als:

Bij question Dierenoverlast\_overig moet het antwoord “Hond” gegevens zijn EN bij question Dierenoverlast moet het antwoord “Loslopende hond, waar dat niet mag” OF “Bijtende hond. Wij werken samen met de politie. Wilt u s.v.p. ook aangifte doen bij de politie?” EN de subcategorie “Dierenoverlast overig”

&#x20;

### _Voorbeeld 3:_

sub == "Speellocatie"

&#x20;

Dit is een makkelijke, de subcategorie moet op “Speellocatie” terecht gekomen zijn.

&#x20;

In theorie kun je alle ‘key’ velden in Django gebruiken om expressions te maken.

Let op! De routering werkt alleen als de betreffende vraag ook is ingevuld:

&#x20;

<figure><img src=".gitbook/assets/image (94).png" alt=""><figcaption></figcaption></figure>

## ExpressionsTypes

Voordat je aan de slag kunt met routeerregels, maak je een expressietype "routing" aan door in de Django Admin naar ExpressionTypes te gaan en daar een nieuwe ExpressionType toe te voegen met de volgende instellingen:

·         Naam: routing

·         Description: routing type

Sla deze vervolgens op.

## Gebieden

Hier staan de gebieden van de gemeente gedefinieerd, voorzien van een unieke code en gegroepeerd onder district, buurt, of wijk. Ieder stadsdeel en wijk heeft een eigen gebied.

Door shapefiles aan te leveren kunnen nieuwe gebieden worden toegevoegd door de technisch applicatiebeheerder.

<figure><img src=".gitbook/assets/image (95).png" alt=""><figcaption></figcaption></figure>

## Questions

De question onder _Signals > Questions_, bestaan uit de volgende onderdelen:

_Key_: Dit is naam van de vraag/het item. Let op! bij het toevoegen van een nieuwe vraag mag er géén spatie in de “Key” staan.

_Field type_: Het type vraag dat aangemaakt is. Hier kan gekozen worden uit de volgende opties:

_PlainText_: Dit is gewoonlijk de keuze als er een tekst getoond dient te worden en een vraag niet noodzakelijk is. Je kunt in de META waarden de "type":"\<waarde>" : “citation”, “caution” of “alert” toevoegen. Iedere waarde wijzigt de opmaak van de tekst. Verder kan het formulier ongeldig worden gemaakt als binnen dit veld type een platte tekst met de validator isBlocking wordt weergegeven.

_TextInput_: Een tekstveld voor één regel tekst.

_MultiTextInput_: Een tekstveld voor meerdere regels tekst

_CheckboxInput_: Een selectievakje waarmee de melder één of meerdere opties aan kan vinken.

_RadioInput_: Toont ronde aanklikveldjes, zogenaamde radio buttons, waarmee de bezoeker één waarde kan kiezen uit een vaste reeks opties.

_SelectInput_: Toont een keuzelijst waarmee de melder één waarde kan kiezen uit een vaste reeks opties.

_TextareaInput_: Een groter tekstveld voor meerdere regels tekst.

_AssetSelect_: Toont objecten op een kaart en laat de bezoeker één of meerdere objecten selecteren.

_LocationSelect_: Toont locaties op een kaart en laat de bezoeker één locatie selecteren.

&#x20;

_Meta_: De inhoud van het object, in JSON (zie volgende alinea JSON-notatie voorbeelden voor mogelijke input). Dit veld kan worden gebruikt om de inhoud/eigenschappen van het formulier nader te specificeren.

_Required_: Geeft aan of het onderdeel/formulier veld verplicht ingevuld dient te worden of niet. Indien deze opties is aangevinkt, is de bezoeker verplicht de vraag te beantwoorden. Anders is de vraag optioneel. PlainText - Alerts zijn nooit verplicht.

_Category_: Geeft aan onder welke (sub)categorie de vraag getoond zal worden. Meerdere waarden zijn mogelijk. Standaard worden de hoofdcategorieën niet gebruikt voor het toewijzen van content.

_Order_: Geeft aan op welke volgorde van de eerder ingestelde categorie de vraag getoond zal worden. Meerdere waarden zijn mogelijk. Standaard worden de hoofdcategorieën niet gebruikt voor het toewijzen van content.

De objecten/formulier velden die onder dit menu ingericht kunnen worden zijn aanvullende vragen,  drop-down menu’s of getoonde (alert)tekst op basis van hoofd- en/of subcategorie. Tevens ins het mogelijk om binnen de Signalen frontend GUI de knop \<volgende> uit te zetten, door deze als voorwaarde te blokkeren; hierbij wordt gebruik gemaakt van zogenaamde Validators.

&#x20;

### **Locatie vragen**

Alle aanvullende vragen worden voorafgegaan door locatievragen, zodat de melder een locatie op de kaart kan aangeven. Deze locatie kaarten bevatten een link naar WFS lagen indien zij een object op de kaart moeten tonen. Voor gebruikersgemak is een featureflag ontwikkeld, om deze objecten in een lijst te tonen. Indien deze featureflag (showSelectorV2removeafterfinishepic5440) aan staat, kan de lijst geactiveerd worden door de onderstaande code toe te voegen aan de locatievraag.

&#x20;

<mark style="background-color:yellow;">"label": "Selecteer de straatverlichting waar het om gaat",</mark>

<mark style="background-color:yellow;">"endpoint": "</mark>[<mark style="background-color:yellow;">\[URL\]</mark>](https://geoserver.luminizer.nl/geoserver/luminizer\_317/ows?service=WFS\&version=1.0.0\&request=GetFeature\&typeName=luminizer\_317:mast\&outputFormat=application/json\&srsName=%7bsrsName%7d\&bbox=%7bwest%7d,%7bsouth%7d,%7beast%7d,%7bnorth%7d)<mark style="background-color:yellow;">",</mark>

<mark style="background-color:yellow;">"language": {</mark>

<mark style="background-color:yellow;">"title": "Kies de straatverlichting",</mark>

<mark style="background-color:yellow;">"submitPlural": "Meld deze straatverlichting",</mark>

<mark style="background-color:yellow;">"unregistered": "De straatverlichting staat niet op de kaart",</mark>

<mark style="background-color:yellow;">"submitSingular": "Meld deze straatverlichting",</mark>

<mark style="background-color:yellow;">"unregisteredId": "Wat is het nummer van de straatverlichting?",</mark>

<mark style="background-color:yellow;">"objectTypeSingular": "lichtpunt",</mark>

<mark style="background-color:yellow;">"objectTypePlural": "lichtpunten"</mark>

<mark style="background-color:yellow;">},</mark>

<mark style="background-color:yellow;">"shortLabel": "Straatverlichting",</mark>

<mark style="background-color:yellow;">"featureTypes": \[</mark>

<mark style="background-color:yellow;">{</mark>

<mark style="background-color:yellow;">"icon": {</mark>

<mark style="background-color:yellow;">"iconUrl": "/assets/images/openbare\_verlichting/overig.svg"</mark>

<mark style="background-color:yellow;">},</mark>

<mark style="background-color:yellow;">"label": "Straatverlichting",</mark>

<mark style="background-color:yellow;">"idField": "LumiId",</mark>

<mark style="background-color:yellow;">"description": "Lichtpuntnummer \{{ MastCode \}} "</mark>

<mark style="background-color:yellow;">}</mark>

<mark style="background-color:yellow;">],</mark>

<mark style="background-color:yellow;">"maxNumberOfAssets": 1</mark>

<mark style="background-color:yellow;">}</mark>

### **JSON-notatie voorbeelden**

De JSON notatie kan per veld type aangepast worden en voorzien van eigenschappen, voor een gedetailleerde opmaak. Voor meer/uitgebreide informatie over dit onderwerp en de verschillende mogelijkheden: [https://github.com/Signalen/frontend/blob/develop/docs/additional-questions.md](https://github.com/Signalen/frontend/blob/develop/docs/additional-questions.md)

&#x20;

_Label_ = de hoofdtekst, veelal de vraag die je stelt. De waarde wordt dikgedrukt weergegeven. \* url/linkjes werken alleen als waarden onder bij value en niet onder label.

_Subtitle_ = extra informatie die je kunt toevoegen. De waarde wordt in het Lichtgrijs gedrukt weergegeven.  \* werkt niet bij het Field type – PlainText.

_Shortlabel_ = informatie over het antwoord die alleen in de backoffice te zien is. Wordt op dit moment niet gebruikt.

_Value_ = Is letterlijk de waarde van het object – de Tekst die getoond wordt bij het Field type - \<PlainText> o Onder Field type – \<Radio Input> is dit de inhoud van de aanvullende vragen. Deze wordt niet dikgedrukt weergegeven.

_Placeholder_ = te gebruiken bij TextInput en TextareaInput. Laat een voorbeeld waarde zien in het tekstveld zoals hieronder 123456.

<figure><img src=".gitbook/assets/image (96).png" alt=""><figcaption></figcaption></figure>

Hieronder vind je de ‘standaard’ JSON input die je in het veld \<META> kunt gebruiken voor het inrichten van de objecten onder _Signals > Questions:_



Meta Standaard vragen (RadioInput)

&#x20;{"label": "Is er sprake van een onveilige situatie>", "values": {"1": "Nee", "2": "Ja,"}

{"label": "Gebeurt het vaker?", "values": {"1": "Nee", "2": "Ja, het gebeurt vaker"}, "ifOneOf": {"personen\_type\_overlast\_6": \["1","2","3","4","5","6","7","8","9","10"]\}}

&#x20;{"label": "Wanneer gebeurt het?", "placeholder": "Omschrijving hoe vaak en tijdstippen", "ifOneOf": {"personen\_frequentie\_overlast\_10": "2"\}}

&#x20;

#### Weergave Alert Teksten (Type = alert, citation, of caution)

&#x20;

Citation:

<div align="left">

<figure><img src=".gitbook/assets/image (98).png" alt="" width="563"><figcaption></figcaption></figure>

</div>

&#x20;Caution:

<div align="left">

<figure><img src=".gitbook/assets/image (99).png" alt="" width="258"><figcaption></figcaption></figure>

</div>

Alert:

<div align="left">

<figure><img src=".gitbook/assets/image (100).png" alt="" width="563"><figcaption></figcaption></figure>

</div>

#### Validators

Het validators attribuut op de metawaarde is mogelijk op alle invoertypen, waarbij wordt gespecificeerd welke validatie op de invoerwaarde moet worden uitgevoerd.\
\
Met behulp van een validator kan een **harde stop** worden ingesteld. De harde stop zit in de Signalen frontend GUI en schakelt in feite de knop \<volgende> voor sommige aanvullende vragen uit. Dit kan middels een Validator worden ingesteld bij subcategorieën die niet door de gemeente kunnen worden behandeld. Bijvoorbeeld meldingen voor de dierenambulance of milieuklachtencentrale.&#x20;

&#x20;{"type": "alert", "value": "Neem contact op met Dierenambulance (24 uur per dag bereikbaar), via telefoonnummer 000 - 00 00 00 of via de website. U kunt dit formulier niet meer verder invullen.", "ifOneOf": {"Voorbeeld\_RadioInput": \["3"]}, <mark style="background-color:yellow;">"validators": \["isBlocking"]</mark>}\


<table data-header-hidden><thead><tr><th width="233"></th><th></th></tr></thead><tbody><tr><td><strong>Field type</strong></td><td><strong>Omschrijving</strong></td></tr><tr><td><em>PlainText</em></td><td>Mogelijke waarde:isBlocking. Het formulier wordt ongeldig wanneer een platte tekst met validator isBlocking wordt weergegeven.</td></tr><tr><td><em>Others except PlainText</em></td><td>Mogelijke waarden:required.</td></tr><tr><td><em>TextInput</em></td><td>Mogelijke waarden:email, max, maxLength, min, minLength, pattern, required,requiredTrue.</td></tr><tr><td><em>TextareaInput</em></td><td>Mogelijke waarden:email, max, maxLength, min, minLength, pattern, required,requiredTrue.</td></tr></tbody></table>

&#x20;

#### ifOneOf

Deze eigenschap toont voorwaardelijk veld waardes, als aan 1 van de opgegeven voorwaarden (gespecificeerd na de “ifOneOf”: notatie) is voldaan.  Als een waarde wordt geselecteerd, laat dan deze question zien. Bijvoorbeeld:

&#x20;

{"label": "Is de stroom in uw huis ook uit?", "values": {"1": "Ja, de stroom is uit in mijn huis", "2": "Nee, mijn huis heeft stroom"}, "ifOneOf": {"Straatverlichting\_type\_melding\_3": "2"\}}

&#x20;

Bijvoorbeeld als je “antwoord 4 kiest/aanvinkt van de vragen Dode\_dieren _**of**_ Overlast\_parkeren _**of**_ antwoord 9 van AFV\_keuzemogelijkheden” krijgt je vervolgens een vrij tekstveld te zien.

&#x20;

<mark style="background-color:yellow;">{</mark>

&#x20;  <mark style="background-color:yellow;">"ifOneOf":{</mark>

&#x20;     <mark style="background-color:yellow;">"Dode\_dieren":"4",</mark>

&#x20;     <mark style="background-color:yellow;">"Overlast\_parkeren":"4",</mark>

&#x20;     <mark style="background-color:yellow;">"AFV\_keuzemogelijkheden":"9"</mark>

&#x20;  <mark style="background-color:yellow;">},</mark>

&#x20;  <mark style="background-color:yellow;">"placeholder":"vrij tekstveld"</mark>

<mark style="background-color:yellow;">}</mark>

<figure><img src=".gitbook/assets/image (101).png" alt=""><figcaption></figcaption></figure>

#### ifAllOf

Werkt hetzelfde als alsifOneOf hierboven uitgelegd, behalve dat dit veld alleen wordt weergegeven als aan alle voorwaarden is voldaan. Zowel ifOneOf als ifAllOf kunnen worden genest en gemengd.

&#x20;

## Routing expressions

Hier kun je de routering inrichten.

Je kiest voor “Routing expression toevoegen” aan de rechterkant.

Vervolgens kies je een Expression en een Department waar de melding aan toegewezen moet worden:

<figure><img src=".gitbook/assets/image (102).png" alt=""><figcaption></figcaption></figure>

&#x20;

Belangrijk!

1\.      Vergeet niet het vinkje “Is active” aan te zetten, anders werkt het niet

2\.      De volgorde is zeer belangrijk (Order)

Op basis van de order worden de routing expressions gelezen. Zodra een expressie voldoet, dan wordt er niet meer naar de rest gekeken.

### **Routeerregels**

Met behulp van routeerregels kunnen meldingen op basis van vooringestelde regels gerouteerd worden naar een specifieke afdeling en eventueel gebruiker. Deze routeeregels kunnen door de functioneel beheerder ingesteld worden in de Django admin.

De routeerregels draaien voor een specifieke melding op het moment dat een melding wordt aangemaakt, de status of categorie van een melding wordt aangepast. Signalen loopt, in de ingestelde volgorde, alle routeerregels af. De eerste routeerregel die "waar" is, zal worden uitgevoerd. De melding wordt vervolgens toegewezen aan de afdeling en eventueel gebruiker die bij deze routeerregel is ingericht.

### **Routeerregels opstellen**

Onder het kopje "Expressions" kun je nieuwe routeerregels opstellen. Klik op "Toevoegen" om een nieuwe regel te maken. Geef de routeerregel een beschrijvende naam en kies voor het type "routing". Onder code kun je vervolgens de routeerregel zelf in programmeertaal opstellen.

Hieronder volgen een aantal voorbeelden van logica die je kunt gebruiken:

&#x20;

_Melding in specifieke subcategorie_

Controleer of een melding in de subcategorie "Putten" staat met:

sub == "Putten"

&#x20;

_Melding in een van de subcategorieën_

Controleer of een melding in de subcategorieën "Putten" of "Verf" staat met:

sub == "Putten" or sub == "Verf"

&#x20;

_Melding in specifieke subcategorie en binnen een specifiek gebied_

Controleer of een melding binnen de subcategorie "Verf" en binnen het gebied met de code "Heusden" valt en gebiedstype "district" met:

sub == "Verf" and location in areas."district"."Heusden"

&#x20;

_Gebruik van haakjes_

Het is mogelijk om and en or te combineren met behulp van haakjes. De volgende expressie kijkt of de subcategorie "Putten" of "Verf" is én of de melding binnen het gebied met de code "Heusden" valt:

(sub == "Putten" or sub == "Verf") and location in areas."district"."Heusden"

&#x20;

_Variabelen_

Binnen een routeerregel zijn de volgende variabelen beschikbaar:

·         **sub**: De naam van de subcategorie

·         **main**: De naam van de hoofdcategorie

·         **location**: De locatie van de melding

·         **time**: Het tijdstip van de melding (in uren, minuten en seconden)

·         **day**: De dag van de melding (Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday)

·         **areas**: Alle gebieden die zijn geconfigureerd op de omgeving, gegroepeerd per gebiedstype

&#x20;

_Antwoorden op aanvullende vragen_

Binnen de variabelen is ook het antwoord op een aanvullende vraag beschikbaar onder de key van de aanvullende vraag. Neem als voorbeeld een aanvullende vraag met de volgende instellingen:

·         Key: Verlichting

·         Field type: RadioInput

En deze meta:

<mark style="background-color:yellow;">{</mark>

&#x20; <mark style="background-color:yellow;">"label": "Wat is het probleem?",</mark>

&#x20; <mark style="background-color:yellow;">"values": {</mark>

&#x20;   <mark style="background-color:yellow;">"1": "Lamp doet het niet",</mark>

&#x20;   <mark style="background-color:yellow;">"2": "Een hele rij lampen doet het niet",</mark>

&#x20;   <mark style="background-color:yellow;">"3": "Lamp geeft lichthinder (schijnt bijvoorbeeld in slaapkamer)",</mark>

&#x20;   <mark style="background-color:yellow;">"4": "Lamp of lantaarnpaal is beschadigd of niet compleet",</mark>

&#x20;   <mark style="background-color:yellow;">"5": "Anders"</mark>

&#x20; <mark style="background-color:yellow;">}</mark>

<mark style="background-color:yellow;">}</mark>

Dan kan met behulp van de volgende expressie gekeken worden of het antwoord "Lamp doet het niet" of "Anders" is:

Verlichting == "Lamp doet het niet" or Verlichting == "Anders"

### **Routeerregels toepassen**

Nadat een routeerregel is aangemaakt, kan deze toegepast worden voor een specifieke afdeling en persoon. Dit kan door een "Routing expression" aan te maken. Bij het aanmaken van een "Routing expression" kies je:

·         De routeerregel die van toepassing is (expression)

·         De afdeling waar de routeerregel naartoe routeert als deze "waar" is (department)

·         De (eventuele) persoon waar de routeerregel naartoe routeert als deze "waar" is (user)

·         De volgorde van de routeerregel ten opzichte van de andere routeerregels (order)

·         Of de routeerregel actief is (is active).

Nadat de "Routing expression" is aangemaakt, is de regel actief. Nieuwe meldingen en bestaande meldingen waarvan de locatie of de subcategorie wordt aangepast, zullen gerouteerd worden volgens de "routing expression".

## Signals

Toont een lijst met het meldingsnummer, datum binnenkomst, datum gewijzigd, status en de categorie.

## Sources

Hier kun je bronnen toevoegen die, vanuit de backoffice van Signalen, gekozen kunnen worden bij het aanmaken van een nieuwe melding. Zo kan bijvoorbeeld worden aangegeven of een melding telefonisch, of via e-mail is binnengekomen.

&#x20;

<figure><img src=".gitbook/assets/image (103).png" alt=""><figcaption></figcaption></figure>

<table data-header-hidden><thead><tr><th width="40"></th><th></th></tr></thead><tbody><tr><td>!</td><td><p><mark style="background-color:green;">Er is een feature flag waarmee je meldingen, die binnenkomen met een gemeente-mailadres, direct op de bron “Interne melding” kunt laten komen:</mark><br><mark style="background-color:green;">apiTransformSourceBasedOnReporter: true</mark></p><p><mark style="background-color:green;">apiTransformSourceBasedOnReporterSource: "Interne melding"</mark></p><p><mark style="background-color:green;">apiTransformSourceBasedOnReporterDomainExtensions: "@s-hertogenbosch.nl"</mark></p></td></tr></tbody></table>

## Standaard afmeldteksten

Standaard afmeldteksten worden voor het gemak beheert vanuit Signalen, maar kunnen ook in Django worden aangepast.

In dit scherm zie je de titel maar ook de subcategorie en op welke volgorde de teksten worden getoond. Je kunt in hier een standaard tekst toevoegen die bij een bepaalde status gekozen kan worden (hoeft niet afmelden te zijn). Er kunnen meerdere standaard teksten per subcategorie en status worden aangemaakt.

## Standaardteksten

Standaard afmeldteksten worden voor het gemak beheert vanuit Signalen, maar kunnen ook in Django worden aangepast.

In dit scherm zie je alleen de titel van de standaard tekst. Hier kun je ook de tekst aanpassen.

## Feature flags

De algehele functionaliteit van de Signalen applicatie wordt vormgegeven door de zogenaamde feature flags, waarmee de inrichting bepaald kan worden door deze uit of aan te zetten. Je kunt (deels) zien welke Feature flags aan staan op de startpagina van Django [menu-structuur-1.md](menu-structuur-1.md "mention")

| <p> </p><p>Features </p><p> </p>                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1. Meldingen in de backoffice kunnen toewijzen aan een afdeling (assignSignalToDepartment)                                                                                                                                                                                                                                                                                                                                                                                                  |
| 2. Meldingen in de backoffice kunnen toewijzen aan een persoon (assignSignalToEmployee)                                                                                                                                                                                                                                                                                                                                                                                                     |
| 3. CSV export maken vanuit de frontend (enableCsvExport)                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| 4. Melder een overzicht geven van "mijn meldingen" (enableMyIncidents / MY\_SIGNALS\_ENABLED)                                                                                                                                                                                                                                                                                                                                                                                               |
| 5. Publieke kaart met meldingen tonen (enablePublicIncidentsMap)                                                                                                                                                                                                                                                                                                                                                                                                                            |
| <p>6. Stuur een melder een e-mail nadat de melder negatieve feedback feedback heeft gegeven en daarna toch besloten is om de melding niet meer op te pakken. (reporterMailHandledNegativeContactEnabled / REPORTER_MAIL_HANDLED_NEGATIVE_CONTACT_ENABLED). <br>Stuur een melder een ontvangstbevestiging van feedback (SYSTEM_MAIL_FEEDBACK_RECEIVED_ENABLED)<br>Melder heeft aangegeven dat er contact opgenomen mag worden<br>(REPORTER_MAIL_CONTACT_FEEDBACK_ALLOWS_CONTACT_ENABLED)</p> |
| 7. Mogelijkheid om meldingen (via e-mail) door te sturen naar een externe behandelaar (enableForwardIncidentToExternal)                                                                                                                                                                                                                                                                                                                                                                     |
| 8. Hernoem het meldingstype "Groot onderhoud" naar "Projecten" (useProjectenSignalType)                                                                                                                                                                                                                                                                                                                                                                                                     |
| 9. Activeer knop om melding door te zetten naar handhaving (showThorButton)                                                                                                                                                                                                                                                                                                                                                                                                                 |
| 10. Draai routeerregels opnieuw bij het wijzigen van de locatie of subcategorie van een melding (DSL\_RUN\_ROUTING\_EXPRESSIONS\_ON\_UPDATES)                                                                                                                                                                                                                                                                                                                                               |
| 11. Pas de bron van de melding automatisch aan naar "interne melding" voor melders met een bepaald e-mailadres (bijvoorbeeld \*@gemeente.nl) (API\_TRANSFORM\_SOURCE\_BASED\_ON\_REPORTER, API\_TRANSFORM\_SOURCE\_BASED\_ON\_REPORTER\_DOMAIN\_EXTENSIONS, API\_TRANSFORM\_SOURCE\_BASED\_ON\_REPORTER\_SOURCE)                                                                                                                                                                            |
| 12. Maak het mogelijk om meldingen na een periode te verwijderen (DELETE\_SIGNALS\_IN\_STATE\_X\_AFTER\_PERIOD\_Y\_ENABLED)                                                                                                                                                                                                                                                                                                                                                                 |
| 13.Onbekend (API\_USE\_QUESTIONNAIRES\_APP\_FOR\_FEEDBACK)                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| 14.Voor Amsterdam: Maak automatisch een deelmelding aan per gekozen eikenprocessierups boom (AUTOMATICALLY\_CREATE\_CHILD\_SIGNALS\_PER\_EIKENPROCESSIERUPS\_TREE)                                                                                                                                                                                                                                                                                                                          |
| 15.Voor Amsterdam: Maak automatisch een deelmelding aan per container (AUTOMATICALLY\_CREATE\_CHILD\_SIGNALS\_PER\_CONTAINER)                                                                                                                                                                                                                                                                                                                                                               |
| 16.Bepaal automatisch het Stadsdeel (API\_DETERMINE\_STADSDEEL\_ENABLED)                                                                                                                                                                                                                                                                                                                                                                                                                    |

