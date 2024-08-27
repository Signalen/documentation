---
icon: envelope-open
---

# Uitgaande e-mail met Office 365 API

Signalen verstuurt transactionele mail naar melders en behandelaren om ze te informeren over de status van een melding. Hiervoor koppelen we met de e-mailservers van de gemeente. In deze handleiding staat uitgelegd hoe de Signalen geautoriseerd kan worden om mail te versturen via Office 365 API op basis van de permissie "Mail.Send" op de Entra ID Applicatie.

### Basisconfiguratie <a href="#basisconfiguratie" id="basisconfiguratie"></a>

1.  Zoek in het Azure Portaal naar “Microsoft Entra ID” en klik op de service.\


    <div align="left">

    <figure><img src="https://docs.delta10.nl/assets/signalen/single-sign-on/1-search-sso.png" alt=""><figcaption></figcaption></figure>

    </div>
2. Klik op “App registrations" in het linkermenu.
3. Klik op de aangemaakte app registratie voor Signalen.
4. Klik op "API permissions".
5. Klik op "Add a permission".
6. Kies voor "Microsoft Graph".
7. Kies voor "Application permissions".
8.  Zoek op de permissie "Mail.Send".\


    <div align="left">

    <figure><img src="https://docs.delta10.nl/assets/signalen/outgoing-e-mail/1-select-permission.png" alt=""><figcaption></figcaption></figure>

    </div>
9. Klik op "Add permissions" om de permissie toe te voegen aan de applicatie.
10. Klik op de knop "Grant admin consent for ...." om de permissies toe te kennen aan de applicatie. Er staat nu een groen vinkje achter de applicatie.

### Mailbox voor uitgaande mail <a href="#mailbox-voor-uitgaande-mail" id="mailbox-voor-uitgaande-mail"></a>

Het is alleen mogelijk om mail te versturen namens een bestaand e-mailadres dat gekoppeld is aan een mailbox. Dit mag een gedeelde mailbox zijn.

In [dit artikel](https://www.codetwo.com/admins-blog/no-reply-mailbox-in-microsoft-365/) staat uitgelegd hoe je specifiek een noreply mailbox kunt aanmaken waarbij binnenkomende mail geweigerd wordt.
