---
layout: post
title: "A consommer sans modération"
description: "TODO"
author:
  name: Team Cytron
  avatar: cytron.png
  email:
  twitter: techM6Web
  facebook:
  github:
category:
tags: [api, cytron]
image:
  feature: 
  credit: 
  creditlink: 
comments: true
permalink: a-consommer-sans-moderation.html
---

Après avoir travaillé pendant plusieurs mois sur la création de nos API avec Symfony, arrive le moment de leur publication !

Or, les clients de nos API sont multiples : il peut s'agir d'applications mobiles, de sites web mais aussi d’un BO interne. Chacun de ces clients peut nécessiter des “vues” différentes de l’API.

Effectivement, alors que le BO devra pouvoir accéder à la totalité des ressources disponibles, l'application mobile ne devra avoir accès qu’aux ressources publiées. De la même manière, la gestion du cache ainsi que la disponibilité des routes doit pouvoir facilement s’adapter au client qui consomme l’API.

Nous avons opté pour l’utilisation d’un sous-domaine par client afin de l’identifier et ainsi de lui appliquer des configurations particulières. Ex :
* http://bo.api.m6web.fr pour le BO,
* http://mobile.api.m6web.fr pour l'application mobile.


#### Authentification

Nous utilisons le composant sécurité de Symfony, qui permet de créer un utilisateur authentifié à la volée et de charger la configuration spécifique à celui-ci.

Nous avons tout d’abord besoin de créer une classe `User` implémentant `Symfony\Component\Security\Core\User\UserInterface`, et contentant les informations de configuration spécifique.

Les différents `Users` sont ensuite créés à l’aide d’un fournisseurs d'utilisateurs implémentant `Symfony\Component\Security\Core\User\UserProviderInterface`.
Dans notre cas, chaque utilisateur possède son propre fichier de configuration yml. Le fournisseur d’utilisateur vérifie donc que l’utilisateur demandé possède un fichier de configuration et instancie un objet `User` avec cette configuration. Ce UserProvider est défini comme service dans notre bundle et configuré dans `security.yml`.

Il faut ensuite créer notre propre fournisseur d’authentification pour avoir une authentification par nom de domaine. Pour cela nous avons suivi et adapté le [cookbook de Symfony](http://symfony.com/doc/current/cookbook/security/custom_authentication_provider.html). Cette authentification s’articule autour de 2 classes : un FirewallListener et un AuthenticationProvider. Pour que notre FirewallListener puisse facilement récupérer le client associé, nous avons ajouté un paramètre au routing Symfony :

```yaml
host: {client}.api.m6web.fr
```

Le FirewallListener utilise donc ce paramètre du routing comme nom d’utilisateur et le transmet à notre AuthenticationProvider. Celui-ci récupère le `User` grâce au `UserProvider` et profite de cette phase pour vérifier que l’adresse IP du client est bien autorisée dans sa configuration grâce au [FirewallBundle](https://github.com/M6Web/FirewallBundle).

Effectivement, nous avons ajouté un filtrage initial (mais optionnel) sur les IPs pour chaque client, dans le fichiers `app/config/users/{username}.yml` :

```yaml
firewall:
    user_access:
        default_state: false
        lists:
            m6_prod: true
            m6_preprod: true
            m6_dev: true
            m6_lan: true
            m6_local: true
            m6_public: true
```

Pour plus de précisions, voir la [documentation du FirewallBundle](https://github.com/M6Web/FirewallBundle#firewall-bundle-).

#### Autorisation

Pour gérer les autorisations d’accès des utilisateurs aux différentes routes, nous avons créé un EventListener qui écoute `kernel.request` et qui décide de laisser passer la requête ou non en fonction de la configuration de l’utilisateur.

```yaml
allow:
    default: true
    methods:
        delete: false
    resources:
        exam: false
    routes:
        get_articles: false
```

Dans cet exemple l’utilisateur a accès par défaut à toutes les routes sauf les méthodes `DELETE`, les routes concernant les exams et la route spécifique `get_articles`.

#### Durée de cache

Les temps de cache sont différents en fonction de l’utilisation des données. Les données du backoffice ne seront pas cachées, tandis que les données de l’application mobile auront un temps de cache de 300s.
Nous avons là-aussi créé un EventListener qui écoute cette fois kernel.response et qui modifie les headers de cache de la réponse en fonction de la configuration utilisateur qui peut contenir une durée par défaut de cache et des durées de cache par route. 


#### Filtrage automatique avec Doctrine

Nous pouvons offrir une "vue" différente de nos données à chaque client en définissant des critères de filtrages (ex: date de publication, ressource activé, etc.) dans les fichiers de configuration des clients.

```yaml
entities:
    article:
        active: true
        publication: false
```

Afin de ne pas modifier le comportement par défaut de Doctrine, nous avons ajoutés une méthode [`findWithContext`](https://gist.github.com/oziks/8180382) qui reprends les mêmes paramètres que la méthode `findBy` de Doctrine avec le `SecurityContext` en plus.

Il est donc très simple de récupérer les ressources en fonctions des paramètres d'un client grâce à la méthode `findWithContext` :

```php
$article = $this
    ->get('m6_contents.article.manager')
    ->getRepository()
    ->findWithContext($this->container->get('security.context'), ['id' => $id]);
```

#### Personnalisation avancée

Grâce à l'utilisation du Bundle Security de Symfony, toute la configuration spécifique à un sous-domaine est stockée dans l’utilisateur courant. Et dans Symfony, l’utilisateur courant est facilement récupérable à partir du service `security_context`. Il est ainsi possible de personnaliser n’importe quelle brique du service en y injectant la dépendance sur ce service.
