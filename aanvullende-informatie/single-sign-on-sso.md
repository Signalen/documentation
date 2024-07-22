---
description: >-
  Gebruikers kunnen inloggen op de Signalen backoffice via Single Sign On (SSO).
  Signalen implementeert hiervoor het OpenID Connect protocol en heeft daarom
  een vertrouwensrelatie met de Identity Provid
---

# Single Sign On (SSO)

## Met Entra ID

1.  Zoek in het Azure Portaal naar “Microsoft Entra ID” en klik op de service.\


    <div align="left">

    <figure><img src="https://docs.delta10.nl/assets/signalen/single-sign-on/1-search-sso.png" alt=""><figcaption></figcaption></figure>

    </div>
2. Klik op “App-registraties” in het linkermenu.
3. Klik op “+ Nieuwe registratie”.
4. Geef als naam de naam van de applicatie op, bijvoorbeeld “Signalen”.
5. Laat “Alleen accounts in deze organisatiemap” aangevinkt.
6. Laat Omleidings-URI voor nu nog leeg, we vullen deze later.
7. Klik op “Registreren”.
8.  Kopieer de waarde “Toepassings-id (client-id)” en bewaar deze tijdelijk.\


    <div align="left">

    <figure><img src="https://docs.delta10.nl/assets/signalen/single-sign-on/2-application-id.png" alt=""><figcaption></figcaption></figure>

    </div>
9.  Klik op “Eindpunten” en kopieer de waarde van “OpenID Connect-document met metagegevens” en bewaar deze tijdelijk.\


    <div align="left">

    <figure><img src="https://docs.delta10.nl/assets/signalen/single-sign-on/3-endpoints.png" alt=""><figcaption></figcaption></figure>

    </div>
10. Klik op “Een omleidings-URI toevoegen”.\


    <div align="left">

    <figure><img src="https://docs.delta10.nl/assets/signalen/single-sign-on/4-redirect-uri.png" alt=""><figcaption></figcaption></figure>

    </div>
11. Klik op “+ Een platform toevoegen”. kies voor “Web” en vul de eerste omleidings-URI in en klik op “Configureren”.
12. Als er meerdere omleidings-URI’s gegeven zijn, voeg deze ook toe door op “URI toevoegen” te klikken.
13. Klik op het knopje “Opslaan”.
14. Ga nu naar “Certificaten en geheimen”.\


    <div align="left">

    <figure><img src="https://docs.delta10.nl/assets/signalen/single-sign-on/5-certificates-and-secrets.png" alt=""><figcaption></figcaption></figure>

    </div>
15. Klik op “+ Nieuw clientgeheim”
16. Kies als beschrijving “Geheim voor applicatie” en kies voor een verloopdatum van 24 maanden. Klik op “Toevoegen”.
17. Kopieer de waarde uit de kolom “Waarde” met het knopje naast de waarde en bewaar deze tijdelijk.\


    <div align="left">

    <figure><img src="https://docs.delta10.nl/assets/signalen/single-sign-on/6-secret-value.png" alt=""><figcaption></figcaption></figure>

    </div>
18. Mocht er “admin consent” nodig zijn voor een applicatie, geef dan tenant-wide admin consent op de applicatie met behulp van [deze instructie](https://learn.microsoft.com/en-us/azure/active-directory/manage-apps/grant-admin-consent). Autorisatie vindt plaats binnen de applicatie.
19. Stuur de tijdelijk bewaarde gegevens op via een beveiligd kanaal:\
    \
    \- De link van het OpenID Connect-document met metagegevens\
    \- Het toepassings-id (client-id)\
    \- De waarde van het clientgeheim

## Externe autoriseren via AzureAD

<mark style="background-color:green;">Deze instructie is relatief oud en moet geüpdate worden.</mark>\ <mark style="background-color:green;">Omdat het een indicatie geeft van wat er moet gebeuren heb ik deze instructie toch toegevoegd.</mark>\
\
Login op [https://portal.azure.com](https://portal.azure.com)

Ga naar Azure Active Directory

<div align="left">

<figure><img src="../.gitbook/assets/image (175).png" alt="" width="189"><figcaption></figcaption></figure>

</div>

Ga naar App registrations\
<img src="../.gitbook/assets/image (176).png" alt="" data-size="original">

&#x20;

New registration

Vul redirect URL in en klik op register

&#x20;![](<../.gitbook/assets/image (177).png>)

&#x20;

Redirect url’s zijn veranderd, de juiste zijn:

* Acceptatie: https://dex.s-hertogenbosch.signalen.dev/callback
* Productie: https://dex.meldingen.s-hertogenbosch.nl/callback

&#x20;&#x20;

Kies Certificates & Secrets\
![](<../.gitbook/assets/image (178).png>)

&#x20;

Client Secrets > New client secret

<figure><img src="../.gitbook/assets/image (179).png" alt=""><figcaption></figcaption></figure>

Geef een naam en selecteer de duur van het secret

<div align="left">

<figure><img src="../.gitbook/assets/image (180).png" alt="" width="232"><figcaption></figcaption></figure>

</div>

<figure><img src="../.gitbook/assets/image (181).png" alt=""><figcaption></figcaption></figure>

**Secret meteen kopiëren (je kunt niet meer terug om het te kopiëren)**

Ga naar Overview\
![](<../.gitbook/assets/image (183).png>)

Application ID nodig\
![](<../.gitbook/assets/image (184).png>)

Selecteer Branding\
![](<../.gitbook/assets/image (185).png>)

Hier kun je logo importeren en de url van de pagina invullen

&#x20;

Ga naar Overview

Selecteer Endpoints\
![](<../.gitbook/assets/image (186).png>)

Kopieer hier de regel die staat onder: ![](<../.gitbook/assets/image (187).png>)

Ga naar Enterprise applications\
![](<../.gitbook/assets/image (188).png>)

Zoek de app die net is geregistreerd

Openen > Overview

Assign Users aan de app\
![](<../.gitbook/assets/image (189).png>)

Informatie die verstuurd moet worden via een beveiligd kanaal:

* Application (client) ID
* Client secret
* OpenID Connect-document met metagegevens.
