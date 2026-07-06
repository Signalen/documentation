---
icon: envelope-open
---

# E-mail templates

In Django kun je via _E-mail integrations > E-mail_ templates de verschillende e-mail opmaken aanpassen. De code die hiervoor gebruikt wordt is markdown language (Zie [https://commonmark.org/help/](https://commonmark.org/help/) voor een korte tutorial en opmaak).

De key in Django refereert naar een onderliggend script, een key is nodig om de juiste email in de juiste situatie te versturen. Dit houdt dus in dat je alleen maar templates kan maken als deze verbonden zijn aan een key. Zomaar een nieuw template bedenken voor een andere functie of handeling kan dus niet zomaar vanuit Django.\
\
Wanneer je een e-mail template aanmaakt of wijzigt vind je onderaan de beschikbare variabelen. Zo zijn er algemene variabelen die in iedere template te gebruiken zijn en specifieke variabelen voor een bepaalde e-mail template:

<div align="left"><figure><img src="../../../.gitbook/assets/image (1).png" alt=""><figcaption><p>Algemene variabelen</p></figcaption></figure></div>

<div align="left"><figure><img src="../../../.gitbook/assets/image (2).png" alt=""><figcaption><p>Deel van template-specifieke variabelen</p></figcaption></figure></div>

**Er zijn verschillende e-mail types die verstuurd kunnen worden. Per e-mailtype staat benoemd wanneer de e-mail wordt verstuurd en naar wie de e-mail wordt verstuurd.**

**1. Send mail to verify the email address of a reporter:** wordt verstuurd naar het nieuwe e-mailadres van de melder wanneer een wijziging van contactgegevens wordt aangevraagd en dit e-mailadres geverifieerd moet worden.

**2. Sent mail to current reporter that a change of contact information is requested:** wordt verstuurd naar het huidige e-mailadres van de melder wanneer een wijziging van contactgegevens wordt aangevraagd.

**3. Send mail to new reporter stating that contact information was successfully updated:** wordt verstuurd naar de nieuwe melder nadat het nieuwe e-mailadres is geverifieerd en de contactgegevens succesvol zijn bijgewerkt.

**4. Send mail when a My Signals token has been requested:** wordt verstuurd aan de melder wanneer een inlog voor de "mijn meldingen" omgeving is aangevraagd. Ontvangt daarna een link waarmee ingelogd kan worden op "mijn meldingen".

**5. Send mail signal assigned:** wordt verstuurd aan een behandelaar wanneer een melding wordt toegewezen aan een behandelaar of afdeling. Bij toewijzing aan een afdeling ontvangen alleen actieve behandelaren met afdelingsnotificaties deze e-mail. Bij toewijzing aan een behandelaar wordt de e-mail alleen verstuurd als gebruikersnotificaties voor deze behandelaar aan staan.

**6. Send mail signal created:** wordt verstuurd aan de melder wanneer een melding succesvol is aangemaakt met status “Gemeld”.

**7. Send mail signal forwarded to external:** wordt verstuurd aan een externe partij wanneer een melding wordt doorgezet naar een externe partij. De e-mail gaat naar het opgegeven externe e-mailadres.

**8. Send mail forwarded to external reaction received:** wordt verstuurd aan een externe partij wanneer een externe partij een reactie heeft gegeven op een naar hun doorgestuurde melding.

**9. Send mail signal handled:** wordt verstuurd aan de melder wanneer een melding de status “Afgehandeld” krijgt, behalve wanneer de vorige status “Verzoek tot heropenen” was.

**10. Send mail signal reopened:** wordt verstuurd aan de melder wanneer een melding de status “Heropend” krijgt.

**11. Send mail signal scheduled:** wordt verstuurd aan de melder wanneer een melding de status “Ingepland” krijgt en is aangegeven dat hierover een e-mail verstuurd moet worden.

**12. Send mail optional:** wordt verstuurd aan de melder wanneer optioneel een status update naar de melder wordt gestuurd bij de statussen “Gemeld”, “In afwachting van behandeling”, “In behandeling”, “Extern: verzoek tot afhandeling”, “Geannuleerd” of “Ingepland”.

**13. Send mail signal reaction requested:** wordt verstuurd aan de melder wanneer een melding de status “Reactie gevraagd” krijgt.

**14. Send mail signal reaction requested received:** wordt verstuurd aan de melder wanneer zijn reactie op het formulier voor status "Reactie gevraagd" ontvangen is.

**15. Send mail signal negative KTO contact:** wordt verstuurd aan een melder wanneer een melding de status “Afgehandeld” krijgt nadat de vorige status “Verzoek tot heropenen” was, en de laatste feedback contact toestaat. Deze mail wordt alleen verstuurd als de FEATURE FLAG `REPORTER_MAIL_HANDLED_NEGATIVE_CONTACT_ENABLED` aanstaat, deze staat standaard uit.

**16. Send mail signal feedback received:** wordt verstuurd aan een melder nadat de melder feedback heeft ingestuurd, als contact met de melder is toegestaan. Deze mail wordt alleen verstuurd als de FEATURE FLAG `SYSTEM_MAIL_FEEDBACK_RECEIVED_ENABLED` aanstaat, deze staat standaard uit.

<mark style="background-color:red;">**Let op! De e-mail wordt uiteraard alleen verstuurd als de melder een e-mailadres heeft ingevuld.**</mark>
