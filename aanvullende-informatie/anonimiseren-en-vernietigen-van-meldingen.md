# Anonimiseren en vernietigen van meldingen

## Anonimiseren

Het anonimiseren van contactgegevens van melders kan ingesteld worden middels de taak anonymize\_reporters. Je kunt hem zo inplannen dat de taak dagelijks anonimiseert.\
\
Het telefoonnummer en/of e-mailadres van een melder worden dan weggepoetst. Deze gegevens zijn écht weg en kunnen niet worden teruggehaald.

Ga in Django naar "Periodic tasks" om de taak in te plannen:

<figure><img src="../.gitbook/assets/image (130).png" alt=""><figcaption></figcaption></figure>

Zodra de gegevens van een melder zijn geanonimiseerd komt dit in de Geschiedenis van de melding te staan:

<figure><img src="../.gitbook/assets/image (133).png" alt=""><figcaption></figcaption></figure>

## Vernietigen van meldingen

<table data-header-hidden><thead><tr><th width="40"></th><th></th></tr></thead><tbody><tr><td><strong>!</strong></td><td><mark style="background-color:green;">Feature flag DELETE_SIGNALS_IN_STATE_X_AFTER_PERIOD_Y_ENABLED moet aan staan.</mark></td></tr></tbody></table>

Het verwijderen van afgesloten meldingen kan middels de taak delete\_signals\_in\_state\_for\_x\_days. Je kunt hem inplannen of eenmalig laten draaien.

<figure><img src="../.gitbook/assets/image (119).png" alt=""><figcaption></figcaption></figure>

In dit geval is de taak eenmalig ingepland. Zet het vinkje uit om structureel in te plannen:

<figure><img src="../.gitbook/assets/image (120).png" alt=""><figcaption></figcaption></figure>

Bij Argumenten vul je de status en het aantal dagen in:

delete\_signals\_in\_state\_for\_x\_days met parameters **\["o", 1825]**

delete\_signals\_in\_state\_for\_x\_days met parameters **\["a", 365]**

delete\_signals\_in\_state\_for\_x\_days met parameters **\["s", 1825]**

&#x20;

o = Afgehandeld

a = Geannuleerd

s = Gesplitst

&#x20;

1825 = 5 jaar

365 = 1 jaar

<figure><img src="../.gitbook/assets/image (121).png" alt=""><figcaption></figcaption></figure>

Klik rechts onderin op Opslaan om de taak in te plannen.

<mark style="background-color:red;">**Let op! De taak kijkt naar de datum van de STATUSWIJZIGING, dus wanneer de melding op Afgehandeld of Geannuleerd is gezet.**</mark>

<mark style="background-color:red;">**NIET naar de aanmaakdatum!**</mark>

### **Voorbeeld uitvoering**

#### **Voorbeeld 1**

In dit voorbeeld is gekozen voor de status a van geannuleerd en voor een periode van 990 dagen.

Daarmee zou testmelding 1 verwijderd moeten worden.

Die is aangemaakt op 26-01-2021 en de laatste wijziging heeft op 25-02-2021 plaatsgevonden.

<figure><img src="../.gitbook/assets/image (122).png" alt=""><figcaption></figcaption></figure>

De taak staat ingepland:

<figure><img src="../.gitbook/assets/image (123).png" alt=""><figcaption></figcaption></figure>

Onder “Task result” vind je vervolgens de taak terug. Het resultaat (SUCCESS of FAILED) is ook terug te zien:

<figure><img src="../.gitbook/assets/image (124).png" alt=""><figcaption></figcaption></figure>

In dit geval is de taak succesvol uitgevoerd.



Als je de taak opent kun je terugzien welk meldingsnummer is verwijderd.

In dit geval is het meldingsnummer 1:\
![](<../.gitbook/assets/image (126).png>)

Oude situatie met 699 meldingen:\
![](<../.gitbook/assets/image (127).png>)

Nieuwe situatie met drie meldingen minder, 696 meldingen totaal:\
![](<../.gitbook/assets/image (128).png>)

#### Voorbeeld 2

Dit is een recent voorbeeld. De onderstaande melding heeft de status "Geannuleerd" gekregen op 04-05-2023 en heeft een vernietigingsperiode van 365 dagen. De laatste wijziging in de Geschiedenis is op 03-05-2024, dat is het anonimiseren van de melding 1 jaar na datum indiening.

<figure><img src="../.gitbook/assets/image (263).png" alt=""><figcaption></figcaption></figure>

Voor het vernietigen van de melding wordt het anonimiseren negeert en wordt er gekeken naar het moment waarop de melding op de status "Geannuleerd" is gezet, in dit geval op 04-05-2023. De melding is precies 1 jaar later verwijderd.

<div align="left" data-full-width="false">

<figure><img src="../.gitbook/assets/image (264).png" alt="" width="350"><figcaption></figcaption></figure>

</div>

### Deleted Signals overzicht

In het totaal zijn er 3 meldingen verwijderd.

Die kun je terugvinden in het “Deleted Signals” overzicht:

<figure><img src="../.gitbook/assets/image (129).png" alt=""><figcaption></figcaption></figure>

Dit overzicht is (nog) niet te exporteren.

Deze functionaliteit wordt ontwikkeld.
