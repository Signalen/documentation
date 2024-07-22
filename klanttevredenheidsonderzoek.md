# Klanttevredenheidsonderzoek

Voorwaarden:\
\- Feature flag staat aan\
\- E-mailtemplate “Send mail signal feedback received” en “Send mail signal negative KTO contact” zijn ingericht\
\- URL naar klanttevredenheidsonderzoek zit in afhandelmail (Send mail signal handled)\
\- Melder heeft een e-mailadres achtergelaten\
\- Optioneel: Bij negatieve feedback komt de melding op status “Verzoek tot heropenen” te staan\
\- Optioneel: Feature flag “Meldingen van deze melder” staat aan

## Afhandelmail met klanttevredenheidsonderzoek

Nadat een melding de status Afgehandeld heeft gekregen, wordt er een e-mail naar de melder verstuurd. In deze e-mail zit een link naar het klanttevredenheidsonderzoek.

<div align="left">

<figure><img src=".gitbook/assets/image (221).png" alt=""><figcaption></figcaption></figure>

</div>

De melder klikt op één van de twee smileys of linkjes en komt in een scherm met verschillende opties terecht.

### Tevreden

<figure><img src=".gitbook/assets/image (224).png" alt=""><figcaption></figcaption></figure>

De melder kan aangeven waarom hij/zij tevreden is over de afhandeling van de melding.\
Daarnaast is er nog een vrij tekstveld wat gebruikt kan worden.\
Nadat de melder op “Verstuur” heeft geklikt dan is de link niet meer geldig. Tevens is het niet meer mogelijk om contact op te nemen met de melder.

### Ontevreden

<figure><img src=".gitbook/assets/image (225).png" alt=""><figcaption></figcaption></figure>

De melder kan aangeven waarom hij/zij tevreden is over de afhandeling van de melding. Daarnaast kunnen er foto’s worden toegevoegd en is er een vrij tekstveld die gebruikt kan worden. Als laatste kan de melder ervoor kiezen om geen contact meer te willen. In dat geval is het niet meer mogelijk om berichten vanuit Signalen naar de melder te sturen.

## Verzoek tot Heropenen

Afhankelijk van het gekozen antwoord bij een ontevreden reactie, komt de melding in Signalen op de status “Verzoek tot heropenen” te staan.\
![](<.gitbook/assets/image (226).png>)\
\
De behandelaar kan kiezen om de melding te Heropenen en opnieuw te behandelen óf om de melding alsnog af te sluiten.\
\
Verzoek tot heropenen > Heropend > (optioneel: In behandeling) > Afgehandeld met mail naar melder\
_Of_\
Verzoek tot heropenen > Afgehandeld zonder mail naar de melder

### Heropend

De behandelaar kiest ervoor om de status te wijzigen van “Verzoek tot heropenen” naar “Heropend”. Er wordt altijd een bericht naar de melder verstuurd.\
\
Nadat de melding is behandeld kan de status worden gewijzigd naar “Afgehandeld”. De melder krijgt opnieuw een afhandelmail met een klanttevredenheidsonderzoek erin.

Indien de melder ontevreden is kan de melding opnieuw op de status “Verzoek tot heropenen” komen.

### Afgehandeld

De behandelaar kan ervoor kiezen om niets met de melding te doen. De status van de melding kan gewijzigd worden naar “Afgehandeld”. Er wordt geen bericht verstuurd aan de melder.

<div align="left">

<figure><img src=".gitbook/assets/image (198).png" alt=""><figcaption></figcaption></figure>

</div>

## Contact met melder

Bij een ontevreden reactie kan de melder ervoor kiezen om geen contact meer te willen over de melding of reactie. Afhankelijk van het gekozen antwoord komt de melding op de status “Verzoek tot heropenen” te staan. Echter zal bij het Heropenen of Afhandelen van een melding geen bericht meer naar de melder worden verstuurd.\
\
Let op! Toelichting is verplicht.

<div align="left">

<figure><img src=".gitbook/assets/image (199).png" alt=""><figcaption></figcaption></figure>

</div>

## Optioneel: KTO terug zien in de melding

De terugkoppeling van een melder kan in Signalen, in het detailscherm van de melding, worden bekeken. Voorwaarde hiervoor is dat de feature flag aan staat.

Open het detailscherm van de melding en kijk naar “Meldingen van deze melder”. Het aantal meldingen is gebaseerd op het e-mailadres.

<div align="left">

<figure><img src=".gitbook/assets/image (200).png" alt="" width="563"><figcaption></figcaption></figure>

</div>

Het aantal niet tevreden en openstaande klanttevredenheidsonderzoeken zijn direct zichtbaar. Klik op het totaal aantal meldingen van deze melder om details te zien over de klanttevredenheid.

<figure><img src=".gitbook/assets/image (202).png" alt=""><figcaption></figcaption></figure>

Je ziet nu de meldingen met een tevreden of ontevreden respons maar ook meldingen waar (nog) geen klanttevredenheidsonderzoek is ingevuld.

De url om de klanttevredenheid in te vullen is 5 dagen geldig (instelbaar).
