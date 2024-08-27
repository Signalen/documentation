---
icon: user-gear
---

# Gebruikersbeheer

Het advies is om gebruikers via Signalen aan te maken en daar ook de rollen toe te kennen aan deze gebruikers – om die reden zal het beheer hiervan niet worden omschreven in dit gedeelte van de handleiding, het is echter wel mogelijk.

·         Ga via het menu naar _Authenticatie en autorisatie › Gebruikers_ voor een weergavelijst van alle gebruikersaccounts. Specifieke accounts kunnen snel worden weergegeven door gebruik te maken van de zoekbalk: ![](<.gitbook/assets/image (82).png>)

·         De resultaten zijn te sorteren door de kolomnamen aan te klikken, of te filteren door rechts uit de \<FILTER> opties te selecteren. Zodra de sortering actief is zal er een pijl rechts naast de kolomnaam te zien zijn, indien er een volgorde van toepassing is ook een cijfer).

<figure><img src=".gitbook/assets/image (83).png" alt=""><figcaption></figcaption></figure>

·         Er kan een export van de lijstresultaten als \*.CSV bestand worden gemaakt door een selectie te maken van de gewenste accountgegevens. Om alle resultaten eenvoudig te selecteren vink je het vakje voor \<Gebruikersnaam> aan en kies vervolgens voor “alle xxx gebruikers selecteren”. Kies vervolgens in het veld \<Actie> voor \<Download CSV> en bevestig door de knop \<Uitvoeren> in te klikken. ![](<.gitbook/assets/image (84).png>)

&#x20;Het resultaat is een gebruikersrapport.csv met de kolommen \<Gebruikersnaam/E-mailadres/Voornaam/Achternaam/Groep/Staf/Superuser/Actief/Afdeling(en)> en is terug te vinden in de downloadmap.

## Gebruiker wijzigen

Ga via het menu naar _Authenticatie en autorisatie › Gebruikers_ en klik op de regel binnen de kolom \<Gebruikersnaam> die je wilt wijzigen om het dialoogvenster \<gebruiker wijzigen> te openen.

&#x20;De gebruikersaccounts worden door functioneel beheer aangemaakt in Signalen, maar het kan nodig zijn om specifiek informatie in te zien bijvoorbeeld over het tijdstip van laatste aanmelding.

&#x20;Tevens kan in dit dialoogvenster worden bepaald of een account kan inloggen op de Django-admin site (door ”stafstatus” aan te vinken), of een gebruiker de “Supergebruikerstatus” toekennen, indien nodig. Het gebruik van de “Supergebruikerstatus” is om security technische redenen niet aan te bevelen het verdient de voorkeur om alle rechten toe te kennen via roltoewijzingen.

## Groepen

Onder het menu _Authenticatie en autorisatie › Groepen_ zie je de rollen terug die eerder via Signalen zijn gedefinieerd. Door op een regel te klikken kunnen de eigenschappen van de geselecteerde rol worden bewerkt.

Het is gebruikelijk om via de frontend van Signalen een aantal rollen te definiëren en de rollen, waar nodig, via Django admin uit te bereiden. Deze rollen zijn herkenbaar aan de Engelstalige regels binnen de rechtenstructuur. Tevens is er een bekend probleem dat de in Django toegevoegde rechten komen te vervallen als dezelfde rol via de frontend van Signalen wordt bewerkt.

<figure><img src=".gitbook/assets/image (85).png" alt=""><figcaption></figcaption></figure>

&#x20;
