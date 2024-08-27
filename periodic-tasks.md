---
icon: diagram-subtask
---

# Periodic tasks

Clocked, intervals en solar events worden niet tot zelden gebruikt. In de praktijk worden vooral Crontab-schema’s gebruikt voor het inplannen van taken. Crontab-schema's helpen bij het beslissen wanneer een taak wordt uitgevoerd, bijvoorbeeld een bepaald tijdstip of een dag van de week, of zelfs een maand van het jaar. Het advies is om een crontab toe te voegen in timezone “Europe/Amsterdam” zodat je niet hoeft om te rekenen met UTC tijd:

<figure><img src=".gitbook/assets/image (90).png" alt=""><figcaption></figcaption></figure>

De taken, gedefinieerd onder _Periodic tasks > Periodic tasks_ zullen door de Celery module volgens schema worden uitgevoerd en als log terug te zien zijn onder _CELERY RESULTS > Task results._ Het resultaat wordt 24 uur bewaard.

Klik op een taak om te zien wanneer die voor het laatst gelopen heeft:

<figure><img src=".gitbook/assets/image (91).png" alt=""><figcaption></figcaption></figure>

## Overzicht van taken

### De volgende taken zijn standaard geconfigureerd:

**clean\_up\_reaction\_request\_task**: zet meldingen die langer dan 5 dagen in de status "reactie gevraagd" staan naar de status "reactie ontvangen".

**save\_and\_zip\_csv\_files\_endpoint**: zet dagelijks een CSV export klaar voor het datawarehouse(zorgt voor de datadump voor de rapportages).

**backend\_cleanup**: ruimt de resultaten van achtergrondtaken ouder dan 24 uur op.

**refresh\_materialized\_view\_public\_signals\_geography\_feature\_collection**: ververst de publieke kaart elk half uur.

&#x20;

### De functioneel beheerder kan de volgende aanvullende taken configureren:

**delete\_expired\_tokens**: ruimt verlopen tokens op die gebruikt worden voor de "mijn meldingen" functionaliteit.

**clean\_up\_forward\_to\_external\_task**: zet meldingen die langer dan 14 dagen in de status "doorgezet naar extern" staan naar de status "verzoek tot afhandeling".

**task\_clean\_datawarehouse\_disk**: ruimt datawarehouse exports die ouder zijn dan 30 dagen op.

**anonymize\_reporters**: verwijderd contactgegevens (e-mailadres en telefoonnummer) van de melder voor meldingen die ouder zijn dan 365 dagen en in de status "afgehandeld", "geannuleerd", "gesplitst" of "verzoek tot afhandeling". De termijn kan handmatig ingesteld worden door onder Arguments > Positional arguments een andere waarde in te vullen, bijvoorbeeld \[730] voor twee jaar.

**update\_status\_children\_based\_on\_parent**: zet de status van deelmeldingen automatisch op "geannuleerd" als de status van de hoofdmelding "afgehandeld" is.

**delete\_signals\_in\_state\_for\_x\_days**: verwijdert meldingen die ouder zijn dan x- dagen in de status "afgehandeld", "geannuleerd" of "gesplitst". Deze taak dient dus twee of driemaal te worden ingepland. De termijn en status dient handmatig ingesteld worden door onder Arguments > Positional arguments een waarde in te vullen. Bijvoorbeeld \["a",365] betekend dat meldingen met de status Geannuleerd na 365 dagen worden verwijderd en \["o",1825] betekend dat meldingen met de status Geannuleerd na 1825 dagen worden verwijderd.

<table data-header-hidden><thead><tr><th width="40"></th><th></th></tr></thead><tbody><tr><td>!</td><td><mark style="background-color:green;">De taak delete_signals_in_state_for_x_days kijkt NIET naar datum binnenkomst maar naar de laatste wijzigingsdatum in de melding. De bewaartermijn verloopt wanneer de datum van de laatste wijziging is verstreken.</mark></td></tr></tbody></table>
