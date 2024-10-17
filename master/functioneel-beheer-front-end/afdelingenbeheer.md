---
icon: user-plus
---

# Afdelingenbeheer

1\)      Ga via de menuopties _Instellingen > Afdelingen_ naar de overzichtslijst van alle afdelingen en de subcategorie(ën) die aan een afdeling is toegewezen.

2\)      Klik op de regel van een afdeling waarna het scherm \<AFDELINGEN (Totaal aantal)> zal openen. Daar kun je de eigenschappen (verantwoordelijke categorie/toegang tot categorie) wijzigen.

3\)      Klik links onderin op “Opslaan” om de wijzigingen door te voeren

<table data-header-hidden><thead><tr><th width="40"></th><th></th></tr></thead><tbody><tr><td>!</td><td><mark style="background-color:green;">De registratie van afdelingen en de toewijzing van subcategorie(ën) worden door functioneel beheer gedaan via Django (Departments)</mark></td></tr></tbody></table>

Als de afdelingen in Django opgevoerd zijn, kun je Signalen gebruiken voor het vormgeven van de afdelingen/teams. Een afdeling kan gekoppeld worden aan één of meerdere categorieën. Er wordt onderscheid gemaakt tussen Toegang tot een categorie (leesrechten) en Verantwoordelijk voor een categorie. Wanneer een afdeling Verantwoordelijk is voor een bepaalde categorie dan kan een melding van die categorie op de afdeling worden gezet. Daarnaast kan de melding op naam van een gebruiker van die afdeling worden gezet.

Een gebruiker ziet alleen meldingen van de categorieën waar zijn/haar afdeling voor geautoriseerd is.

<table data-header-hidden><thead><tr><th width="40"></th><th></th></tr></thead><tbody><tr><td>!</td><td><mark style="background-color:green;">Zet de gebruiker een melding op een subcategorie waar zijn/haar afdeling geen Toegang toe heeft of niet Verantwoordelijk voor is, dan verdwijnt de melding uit het overzicht van de gebruiker. De gebruiker kan de melding dan niet meer inzien of terugvinden in Signalen.</mark></td></tr></tbody></table>
