# Cahier des charges mybank.io

Benjamin LI
Alexis Lin
---

## Avant de commencer le projet

- Le projet est à réaliser par groupe de 1 ou 2
- La première étape du projet est de créer un dépot GitHub pour votre rendu et ajouter les droits en lecture à l'utilisateur github.com/lp1dev 
- Le rendu devra se faire sous forme de fichier docker-compose.yml et de conteneurs Docker fonctionnels

---

## Liste des tâches à réaliser

- Création d'un conteneur pour l'application basé sur alpine
- Intégration dans docker-compose
- Ajout de HTTPS via un reverse proxy NGINX
- Mise en place d'un pare-feu type fail2ban
- Audit des vulnérabilités de l'applicatif (manuel et automatisé)
- Reporting des vulnérabilités de l'application (cf section vulnérabilités)
- Fix des soucis de sécurité via NGINX et fail2ban

---

## Vulnérabilités

### Exemple

| Vulnérabilité | Injection SQL |
|:-----:|:------------:|
| Description | Le paramètre GET post_id de l'URL https://website.com/blog est utilisé par le back-end sans vérification de la preśence de caractères pouvant causer une injection SQL. | 
| Criticité | Critique |
| Exploitation | https://website.com/blog?id=1 UNION SELECT * FROM users |
| Remédiation | Ajouter une règle dans le pare-feu pour bloquer les requêtes contenant le mot clé UNION |


| Vulnérabilité | Injection SQL |
|:-----:|:------------:|
| Description | Utilisatiin du OR lors du login | 
| Criticité | Critique |
| Exploitation | Login: ' OR 1=1   Password: peu importe |
| Remédiation | Ajouter une règle dans le pare-feu pour bloquer les requêtes contenant le mot OR pour le formulaire du login |


| Vulnérabilité | Faille XSS|
|:-----:|:------------:|
| Description | ajout de js quand on ajoute une balise img dans l'url avec le onerror | 
| Criticité | Critique |
| Exploitation | http://localhost:3000/?view=login&error=%3Cimg%20src=%22abc%22%20onerror=%22alert(1)%22%20/%3E |
| Remédiation | Echapper les caractères HTML, CSS et Javascript, ajouter dans l'entete X-XSS-Protection qui filtre automatiquement certaines attaques XSS
, l’intégration d’un en-tête Content-Security-Policy dans les requêtes HTTP |


| Vulnérabilité | Faille SQL|
|:-----:|:------------:|
| Description | Transfert d'un nombre négatif | 
| Criticité | Critique |
| Exploitation | Transfert d'un nombre négatif |
| Remédiation | Empêcher de pour transférer un nombre négatif|