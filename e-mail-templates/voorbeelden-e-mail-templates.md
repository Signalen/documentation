---
icon: envelope-open
---

# Voorbeelden e-mail templates

### Send mail signal created

```
Titel:
Uw melding {{ formatted_signal_id }}: melding ontvangen

Bericht:
Geachte melder,

Dank voor uw melding. Fijn dat u zich betrokken voelt bij de stad.

**Uw melding**  
{{ text }}
 
Nummer: {{ formatted_signal_id }}  
Gemeld op: {{ created_at|date:"j F Y, H.i" }} uur  
Plaats: {% raw %}
{% if address %}{{ address|format_address:"O hlT, P W" }}{% else %}Locatie is gepind op de kaart{% endif %}

**Wat doen we met uw melding?**  
{{ handling_message }}

**Meer weten?**  
Voor vragen over uw melding kunt u bellen met telefoonnummer, maandag tot en met vrijdag van 08.00 tot 18.00. Geef dan ook het nummer van uw melding door: {{ formatted_signal_id }}.

Met vriendelijke groet,

{{ ORGANIZATION_NAME }}  

*Dit bericht is automatisch gemaakt met de informatie uit uw melding.*  

____________________________________________________________________________________________________

#### U gaf ook nog deze informatie

**Vragen**  
{% for label, answers in extra_properties.items %}{{ label }}   
*{% for answer in answers %}{{ answer}}{% if not forloop.last %}, {% endif %}{% endfor %}*   
{% endfor %}  
 
**Uw contactgegevens**   
Om uw privacy te beschermen hebben wij uw gegevens onherkenbaar gemaakt voor anderen.
{% if reporter_phone %}
Wat is uw telefoonnummer?   
{{ reporter_phone}}
{% endif %}{% if reporter_email %}
Wat is uw e-mailadres?  
{{ reporter_email}}  
{% endif %}  

**Melding doorsturen**  
{% if reporter_sharing_allowed %}  Ja, ik geef de gemeente toestemming om mijn melding door te sturen naar andere organisaties als de melding niet voor de gemeente is bestemd.
{% else %}
Nee, ik geef de gemeente geen toestemming om mijn melding door te sturen naar andere organisaties als de melding niet voor de gemeente is bestemd.
{% endif %}
{% endraw %}
```

### Send mail signal handled

<pre><code>Titel:
Uw melding {{ formatted_signal_id }} : antwoord op uw melding

Bericht:
Geachte melder,

Op {{ created_at|date:"j F Y" }} om {{ created_at|date:"H.i" }} uur hebt u een melding gedaan bij de gemeente. In deze mail vertellen wij u wat wij hebben kunnen doen.   

**U liet ons het volgende weten**  
{{ text }}

**Wat hebben wij kunnen doen?**  
{{ status_text }}

**Bent u tevreden met de afhandeling van uw melding?**

<strong>- [![Tevreden](https://meldingen.[gemeentenaam].nl/assets/images/happy.png) Ja, ik ben tevreden]({{ positive_feedback_url }})   
</strong>- [![Niet tevreden](https://meldingen.s-hertogenbosch.nl/assets/images/unhappy.png) Nee, ik ben niet tevreden]({{ negative_feedback_url }}) 

**Gegevens van uw melding**  
Nummer: {{ formatted_signal_id }}  
Gemeld op: {{ created_at|date:"j F Y, H.i" }} uur  
Plaats: {% if address %}{{ address|format_address:"O hlT, P W" }}{% else %}Locatie is gepind op de kaart{% endif %}

**Meer weten?**  
Voor vragen over uw melding kunt u bellen met telefoonnummer, maandag tot en met vrijdag van 08.00 tot 18.00. Geef dan ook het nummer van uw melding door: {{ formatted_signal_id }}.

Met vriendelijke groet,

{{ ORGANIZATION_NAME }}
</code></pre>

### Send mail signal scheduled

```
Titel:
Uw melding {{ formatted_signal_id }} meer informatie voor u

Bericht:
Geachte melder,

Op {{ created_at|date:"j F Y" }} om {{ created_at|date:"H.i" }} uur hebt u een melding gedaan bij de gemeente. In deze e-mail leest u meer over wat wij aan het doen zijn.

**U liet ons het volgende weten**  
{{ text }}

**Meer informatie**    
{{ status_text }}

**Gegevens van uw melding**  
Nummer: {{ formatted_signal_id }}  
Gemeld op: {{ created_at|date:"j F Y, H.i" }} uur  
Plaats: {% raw %}
{% if address %}{{ address|format_address:"O hlT, P W" }}{% else %}Locatie is gepind op de kaart{% endif %}
{% endraw %}  

**Meer weten?**  
Voor vragen over uw melding kunt u bellen met telefoonnummer, maandag tot en met vrijdag van 08.00 tot 18.00. Geef dan ook het nummer van uw melding door: {{ formatted_signal_id }}.

Met vriendelijke groet,

{{ ORGANIZATION_NAME }}
```

### Send mail signal reopened

```
Titel:
Uw melding {{ formatted_signal_id }}

Bericht:
Geachte melder,

U bent niet tevreden over wat wij met uw melding hebben gedaan. Dat spijt ons. Wij gaan opnieuw aan het werk.

**Wat wij nu gaan doen**  
{{ status_text }}

**U liet ons het volgende weten**  
Bent u tevreden met de afhandeling van uw melding?  
{% raw %}
{% if feedback_is_satisfied %} *Ja, ik ben tevreden met de afhandeling van mijn melding* {% else%} *Nee, Ik ben niet tevreden met de afhandeling van mijn melding* {% endif %}  

{% if feedback_is_satisfied %}**Waarom bent u tevreden?**{% else %}**Waarom bent u niet tevreden?** {% endif %}  {% if feedback_text %}  *{{ feedback_text }}*  
{% else %}
{% for f_text in feedback_text_list %}  *{{ f_text }}*  
{% endfor %}
{%endif %}

{% if feedback_text_extra %}
**Wilt u ons verder nog iets laten weten?**  
*{{ feedback_text_extra }}*
{% endif %}

**Gegevens van uw melding**  
Nummer: {{ formatted_signal_id }}  
Gemeld op: {{ created_at|date:"j F Y, H.i" }} uur  
Plaats: {% if address %}{{ address|format_address:"O hlT, P W" }}{% else %}Locatie is gepind op de kaart{% endif %}
{% endraw %} 

**Meer weten?**  
Voor vragen over uw melding kunt u bellen met telefoonnummer, maandag tot en met vrijdag van 08.00 tot 18.00. Geef dan ook het nummer van uw melding door: {{ formatted_signal_id }}.

Met vriendelijke groet,

{{ ORGANIZATION_NAME }}
```

### Send mail optional

```
Titel:
Uw melding {{ formatted_signal_id }}

Bericht:
Geachte melder,

Op {{ created_at|date:"j F Y" }} om {{ created_at|date:"H.i" }} uur hebt u een melding gedaan bij de gemeente. In deze e-mail leest u de stand van zaken van uw melding.

**U liet ons het volgende weten**  
{{ text }}

**Stand van zaken**  
{{ status_text }}

**Gegevens van uw melding**  
Nummer: {{ formatted_signal_id }}  
Gemeld op: {{ created_at|date:"j F Y, H.i" }} uur  
Plaats: {% raw %}
{% if address %}{{ address|format_address:"O hlT, P W" }}{% else %}Locatie is gepind op de kaart{% endif %}
{% endraw %}  

**Meer weten?**  
Voor vragen over uw melding kunt u bellen met telefoonnummer, maandag tot en met vrijdag van 08:00 tot 18:00. Geef dan ook het nummer van uw melding door: {{ formatted_signal_id }}.

Met vriendelijke groet,

{{ ORGANIZATION_NAME }}
```

### Send mail signal reaction requested

```
Titel:
Uw melding {{ formatted_signal_id }}

Bericht:
Geachte melder,

Op {{ created_at|date:"j F Y" }} om {{ created_at|date:"H.i" }} uur hebt u een melding gedaan bij de gemeente. In deze e-mail leest u de stand van zaken van uw melding.

**U liet ons het volgende weten**  
{{ text }}

**Stand van zaken**  
{{ status_text }}

**Gegevens van uw melding**  
Nummer: {{ formatted_signal_id }}  
Gemeld op: {{ created_at|date:"j F Y, H.i" }} uur  
Plaats: {% raw %}
{% if address %}{{ address|format_address:"O hlT, P W" }}{% else %}Locatie is gepind op de kaart{% endif %}
{% endraw %}  

**Meer weten?**  
Voor vragen over uw melding kunt u bellen met telefoonnummer, maandag tot en met vrijdag van 08:00 tot 18:00. Geef dan ook het nummer van uw melding door: {{ formatted_signal_id }}.

Met vriendelijke groet,

{{ ORGANIZATION_NAME }}
```

### Send mail signal reaction requested received

```
Titel:
Uw melding {{ formatted_signal_id }} uw reactie ontvangen

Bericht:
Geachte melder,

Bedankt voor uw reactie. U hoort binnen 3 werkdagen weer bericht van ons.  

**Bent u tevreden met de afhandeling van uw melding?**  
{% raw %}
{% if feedback_is_satisfied %} Ja, ik ben tevreden met de afhandeling van mijn melding {% else%} Nee, Ik ben niet tevreden met de afhandeling van mijn melding {% endif %}  

{% if feedback_is_satisfied %}**Waarom bent u tevreden?** {% else %} **Waarom bent u niet tevreden?** {% endif %}  
{% if feedback_text %} {{ feedback_text }}{% else %}{% for f_text in feedback_text_list %}{{ f_text }}{% endfor %}
{%endif %}

{% if feedback_text_extra %}
**Wilt u ons verder nog iets laten weten?**  
{{ feedback_text_extra }}
{% endif %}

**Contact**  
{% if feedback_allows_contact %} Ja, bel of e-mail mij over deze melding of over mijn reactie. {% else %} Nee, bel of e-mail mij niet meer over deze melding of over mijn reactie. {% endif %}

**Gegevens van uw melding**  
Nummer: {{ formatted_signal_id }}  
Gemeld op: {{ created_at|date:"j F Y, H.i" }} uur  
Plaats: {% if address %}{{ address|format_address:"O hlT, P W" }}{% else %}Locatie is gepind op de kaart{% endif %}
{% endraw %}  

**Meer weten?**  
Voor vragen over uw melding kunt u bellen met telefoonnummer, maandag tot en met vrijdag van 08.00 tot 18.00. Geef dan ook het nummer van uw melding door: {{ formatted_signal_id }}.

Met vriendelijke groet,

{{ ORGANIZATION_NAME }}
```

## Aanpassen contactgegevens

### Send mail to verify the email address of a reporter

```
Titel:
Uw melding {{ formatted_signal_id }}

Bericht:
Geachte melder,

Er is een wijziging van uw e-mailadres aangevraagd. Graag willen wij u vragen om onderstaande url te gebruiken om uw nieuwe e-mailadres te bevestigen.

[{{ verification_url }}]({{ verification_url }})

Alvast bedankt!

Met vriendelijke groet,

{{ ORGANIZATION_NAME }}
```

### Send mail to current reporter that a change of contact information is requested

```
Titel:
Uw melding {{ formatted_signal_id }}

Bericht:
Geachte melder,

Er is een wijziging van uw e-mailadres aangevraagd voor melding {{ formatted_signal_id }}. Op het nieuwe e-mailadres ontvangt u een e-mail om het nieuwe adres te bevestigen. Bevestig uw nieuwe e-mailadres alstublieft binnen 24 uur.

Met vriendelijke groet,

{{ ORGANIZATION_NAME }}
```

### Send mail to new reporter stating that configuration information was successfully updated

```
Titel:
Uw melding {{ formatted_signal_id }}

Bericht:
Geachte melder,

Bij deze bevestigen wij dat uw verzoek om uw contact gegevens te wijzigen succesvol is uitgevoerd.

Met vriendelijke groet,

{{ ORGANIZATION_NAME }}
```

## Mijn meldingen

### Send mail when a My Signals token has been requested

```
Titel:
Inloggen op uw meldingenoverzicht

Bericht:
Geachte melder,

[Bevestig uw e-mailadres]({{ my_signals_url }}) om in te loggen op uw meldingenoverzicht. In uw meldingenoverzicht vindt u al uw meldingen van de afgelopen 12 maanden terug. En u ziet status updates.

**Meer weten?**  
Voor vragen over uw melding kunt u bellen met telefoonnummer, maandag tot en met vrijdag van 08:00 tot 18:00.


Met vriendelijke groet,

{{ ORGANIZATION_NAME }}
```

## Klanttevredenheid <a href="#klanttevredenheid" id="klanttevredenheid"></a>

### Send mail signal feedback received

```
Titel:
Uw melding {{ formatted_signal_id }} uw reactie ontvangen

Bericht:
Geachte melder,

Bedankt voor uw reactie. U hoort binnen 3 werkdagen weer bericht van ons.  

**Bent u tevreden met de afhandeling van uw melding?**  
{% raw %}
{% if feedback_is_satisfied %} Ja, ik ben tevreden met de afhandeling van mijn melding {% else%} Nee, Ik ben niet tevreden met de afhandeling van mijn melding {% endif %}  

{% if feedback_is_satisfied %}**Waarom bent u tevreden?** {% else %} **Waarom bent u niet tevreden?** {% endif %}  
{% if feedback_text %} {{ feedback_text }}{% else %}{% for f_text in feedback_text_list %}{{ f_text }}{% endfor %}
{%endif %}

{% if feedback_text_extra %}
**Wilt u ons verder nog iets laten weten?**  
{{ feedback_text_extra }}
{% endif %}

**Contact**  
{% if feedback_allows_contact %} Ja, bel of e-mail mij over deze melding of over mijn reactie. {% else %} Nee, bel of e-mail mij niet meer over deze melding of over mijn reactie. {% endif %}

**Gegevens van uw melding**  
Nummer: {{ formatted_signal_id }}  
Gemeld op: {{ created_at|date:"j F Y, H.i" }} uur  
Plaats: {% if address %}{{ address|format_address:"O hlT, P W" }}{% else %}Locatie is gepind op de kaart{% endif %}
{% endraw %}  

**Meer weten?**  
Voor vragen over uw melding kunt u bellen met telefoonnummer, maandag tot en met vrijdag van 08.00 tot 18.00. Geef dan ook het nummer van uw melding door: {{ formatted_signal_id }}.

Met vriendelijke groet,

{{ ORGANIZATION_NAME }}
```

### Send mail negative KTO contact

```
Titel:
Uw melding {{ formatted_signal_id }}

Bericht:
Geachte melder,
U bent niet tevreden over wat wij met uw melding hebben gedaan. Dat spijt ons. Wij willen u graag wat meer informatie geven.

**Wat wij u nog meer willen laten weten**    
{{ status_text }}

**U liet ons het volgende weten**  
Bent u tevreden met de afhandeling van uw melding?  
{% raw %}
{% if feedback_is_satisfied %} Ja, ik ben tevreden met de afhandeling van mijn melding {% else %} Nee, ik ben niet tevreden met de afhandeling van mijn melding {% endif %}


**Waarom bent u niet tevreden?**  
{% if feedback_text %}{{ feedback_text }}  
{% else %}
{% for f_text in feedback_text_list %}{{ f_text }}  {% endfor %}
{%endif %}
{{ feedback_text_extra }}  


**Gegevens van uw melding**  
Nummer: {{ formatted_signal_id }}  
Gemeld op: {{ created_at|date:"j F Y, H.i" }} uur  
Plaats: {% if address %}{{ address|format_address:"O hlT, P W" }}{% else %}Locatie is gepind op de kaart{% endif %}
{% endraw %}

**Meer weten?**  
Voor vragen over uw melding kunt u bellen met telefoonnummer, maandag tot en met vrijdag van 08:00 tot 18:00. Geef dan ook het nummer van uw melding door: {{ formatted_signal_id }}.

Met vriendelijke groet,

{{ ORGANIZATION_NAME }}
```

## Interne behandelaar <a href="#interne-behandelaar" id="interne-behandelaar"></a>

### Send mail signal assigned

```
Titel:
Melding {{ formatted_signal_id }} is toegewezen aan {% raw %}
{% if assigned_to_user %}jou{% else %}{{ assigned_to_department }}{% endif %}

Bericht:
Beste {{ recipient_full_name }},

De volgende melding is aan {% if assigned_to_user %}jou{% else %}{{ assigned_to_department }}{% endif %}
{% endraw %} toegewezen:

- Nummer: {{ formatted_signal_id }}
- Subcategorie: {{ sub_category_public_name }}
- Gemeld op: {{ created_at|date:"DATETIME_FORMAT" }}

{{ signal_url }}

Met vriendelijke groet,

{{ ORGANIZATION_NAME }}
```

## Externe behandelaar <a href="#externe-behandelaar" id="externe-behandelaar"></a>

### Send mail signal forwarded to external

```
Titel:
Verzoek tot behandeling van Signalen melding {{formatted_signal_id}}

Bericht:
Geachte behandelaar,

Er is een melding binnengekomen bij de Gemeente. Kunnen jullie hier naar kijken en ons laten weten of jullie deze kunnen afhandelen.

Wat kunt u doen?
U kunt de melding gelijk inzien en oppakken. Als de melding verwerkt, ontvangen wij graag een bericht.

[Bekijk de actie]({{ reaction_url }})

Nummer: {{ formatted_signal_id }}


Met vriendelijke groet,  

{{ ORGANIZATION_NAME }}
```

### Send mail forwarded to external reaction received

```
Titel:
Melding {{formatted_signal_id}}: reactie ontvangen

Bericht:
Geachte behandelaar,

Bedankt voor het invullen van het actieformulier. Uw informatie helpt ons bij het verwerken van de melding.

U liet ons het volgende weten:  
{{ reaction_text }}

Gegevens van de melding
- Nummer: {{ formatted_signal_id }}
- Gemeld op: {{ created_at|date:"DATETIME_FORMAT" }}
- Plaats: {% raw %}
{% if location %}{{ location|format_address:"O hlT, P W" }}{% endif %}
{% endraw %}


Met vriendelijke groet,

{{ ORGANIZATION_NAME }}
```
