---
icon: sitemap
---

# Technische architectuur

![Overzicht van technische architectuur](https://docs.delta10.nl/assets/signalen/technische-architectuur/overzicht.png)

### Frontend, backend en classification <a href="#frontend-backend-en-classification" id="frontend-backend-en-classification"></a>

Signalen is opgebouwd volgens de Common Ground [informatiearchitectuur](https://componentencatalogus.commonground.nl/20190130\_-\_Common\_Ground\_-\_Informatiearchitectuurprincipes.pdf)- en [realisatieprincipes](https://componentencatalogus.commonground.nl/20190130\_-\_Common\_Ground\_-\_Realisatieprincipes.pdf) en is opgebouwd uit componenten, waarbij data, services en interactie gescheiden zijn. Signalen kent de volgende componenten:

* Frontend (interactielaag): Javascript applicatie voor melders + backoffice medewerkers die communiceert met de backend.
* Backend (servicelaag): Python service die een REST API aanbiedt voor de functionaliteit in Signalen, waaronder het melden en afhandelen van meldingen. Naast de frontend koppelen ook andere externe taakafhandelsystemen via deze REST API.
* Classification (servicelaag): Python service die een REST API aanbiedt. Deze service classificeert meldingen met behulp van een machine learning model op basis van de meldtekst en plaatst deze in de juiste categorie.

De componenten draaien op een Kubernetes omgeving en worden geïnstalleerd en up-to-date gehouden met behulp van [Helm charts](https://github.com/signalen/helm-charts).

### Opslag <a href="#opslag" id="opslag"></a>

Signalen maakt gebruik van twee typen opslag en zet hiervoor de volgende Azure PaaS diensten in:

* PostgreSQL database (Azure Database for PostgreSQL): voor de opslag van alle relationele data, zoals
* Blob store (Azure Storage Account): voor de opslag van bijlagen zoals foto's, CSV exports voor het datawarehouse en het machine learning model.

### Afhankelijkheden <a href="#afhankelijkheden" id="afhankelijkheden"></a>

De Signalen backend maakt - naast PostgreSQL - gebruik van de volgende externe componenten:

* [Elasticsearch](https://www.elastic.co/): voor het bijhouden van een secundaire index voor _full-text search_. Deze secundaire index kan ten alle tijden opnieuw opgebouwd worden op basis van de informatie uit PostgreSQL.
* [RabbitMQ](https://www.rabbitmq.com/): een message queue waarin achtergrondtaken worden opgeslagen die asynchroon uitgevoerd worden door de backend. Achtergrondtaken zijn onder andere het updaten van de Elasticsearch index en het versturen van een e-mail.

Deze componenten draaien ook op Kubernetes.
