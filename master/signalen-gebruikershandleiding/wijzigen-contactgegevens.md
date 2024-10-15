---
icon: address-card
---

# Wijzigen contactgegevens

**Voorwaarden**:\
\- Gebruiker moet Schrijfrechten hebben\
\- E-mail templates moeten zijn ingericht (zie [e-mail-templates](../../e-mail-templates/ "mention") en voor voorbeelden [#aanpassen-contactgegevens](../../e-mail-templates/voorbeelden-e-mail-templates.md#aanpassen-contactgegevens "mention")):

* Send mail to new reporter stating that contact information was successfully updated
* Send mail to current reporter that a change of contact information is requested
* Send mail to verify the email address of a reporter



Achter de contactgegevens van de melder staat een potloodje waarmee een telefoonnummer en e-mailadres toegevoegd of gewijzigd kunnen worden.

<figure><img src="../../.gitbook/assets/image (134).png" alt=""><figcaption></figcaption></figure>

Klik op het potloodje om de gegevens toe te voegen of te wijzigen:

<figure><img src="../../.gitbook/assets/image (135).png" alt=""><figcaption></figcaption></figure>

<table data-header-hidden><thead><tr><th width="40"></th><th></th></tr></thead><tbody><tr><td><strong>!</strong></td><td><mark style="background-color:green;">Bij meldingen die zijn aangemaakt <strong>vóór</strong> de installatie van <strong>versie FE 2.14.9 en BE 2.32.1 [4.11.1]</strong> krijg je een foutmelding bij het wijzigen van contactgegevens:</mark><br><img src="../../.gitbook/assets/image (136).png" alt=""><br>Toen bestond deze functionaliteit nog niet en kan de actie niet worden uitgevoerd.</td></tr></tbody></table>

### Telefoonnummer toevoegen

Bij een anonieme melding is het _niet_ mogelijk om alleen een telefoonnummer toe te voegen. Verificatie via het e-mailadres is verplicht.

### Telefoonnummer wijzigen

Alleen het telefoonnummer wijzigen is zonder verificatie mogelijk.\
Is er ook een e-mailadres ingevuld? Dan krijgt de melder per e-mail een bevestiging van de gewijzigde contactgegevens:\


<figure><img src="../../.gitbook/assets/image (137).png" alt=""><figcaption></figcaption></figure>

### E-mailadres toevoegen

Voeg je het e-mailadres toe, dan ontvangt de melder een e-mail met het verzoek om het nieuwe e-mailadres te bevestigen.

<figure><img src="../../.gitbook/assets/image (139).png" alt=""><figcaption></figcaption></figure>

In Signalen staat dat de verificatiecode is verzonden:

<figure><img src="../../.gitbook/assets/image (138).png" alt=""><figcaption></figcaption></figure>

De melder krijgt, na het aanklikken van de URL, een bevestiging te zien. Tevens komt er een bevestiging per mail.

<figure><img src="../../.gitbook/assets/image (140).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (142).png" alt=""><figcaption></figcaption></figure>

### E-mailadres wijzigen

Dit is vrijwel identiek als het toevoegen van een e-mailadres. \
De melder ontvangt een bericht op het oude e-mailadres dat er een wijziging van het e-mailadres is aangevraagd:

<figure><img src="../../.gitbook/assets/image (143).png" alt=""><figcaption></figcaption></figure>

En op het nieuwe e-mailadres de URL om het nieuwe e-mailadres te bevestigen:

<figure><img src="../../.gitbook/assets/image (144).png" alt=""><figcaption></figcaption></figure>

In Signalen is te zien dat er aan het nieuwe e-mailadres een verificatiemail is verzonden:

<figure><img src="../../.gitbook/assets/image (145).png" alt=""><figcaption></figcaption></figure>

Zodra de melding is geaccepteerd blijft alleen het nieuwe e-mailadres zichtbaar.\
\
Het is daarnaast mogelijk om de verificatie te annuleren. Er wordt dan gevraagd naar de reden van annuleren:

<div align="left">

<figure><img src="../../.gitbook/assets/image (259).png" alt="" width="398"><figcaption></figcaption></figure>

</div>

De reden wordt meegenomen in de logging:\


<figure><img src="../../.gitbook/assets/image (260).png" alt=""><figcaption></figcaption></figure>
