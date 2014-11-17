---
layout: post
title: "Retour sur la velocity Barcelone - day 1"
description: ""
author:
  name:           M6Web
  avatar:
  email:
  twitter:  techM6Web
  facebook:
  github:
category:
tags: []
image:
  feature:
  credit:
  creditlink:
comments: true
---

http://velocityconf.com/velocityeu2014/public/schedule/proceedings


Baptiste, François et Olivier ont eu la chance de participer à la Vélocity Conférence Europe 2014 qui avait lieu cette année à Barcelone. 

Voici le compte rendu des conférences et des moments qui les ont marqués.


# Morning Keynotes

Les keynotes du matin semblaient être scénarisées sur différents points que les organisateurs de la conférence voulaient mettre en avant.

## Life after human error - Steven Shorrock (EUROCONTROL)

Steven Shorrock n’est pas un homme de l’IT, mais travaille autour de la sécurité aérienne. Il se définit comme un ergonomiste des systèmes. Il a présenté comment, autour des erreurs humaines, “les mots créaient le monde” et entrainaient immédiatement un jugement social (“négligence" est évidement plus connoté que “erreur d’attention”). Il peut y avoir des erreurs dans la définition d’une erreur. Qualifier une erreur demandait une définition précise de standard et de contextes.   
Il a également conseillé d’étudier les cas de fonctionnement normaux ; ne pas faire seulement des *post-mortem* mais des *pre* et des *no* mortem.

![hal](/images/posts/velocity2014/hal.jpg)


Une présentation intéressante sur l’incident et l’erreur.

## Maximize the Return of Your Digital Investments Aaron Rudger (Keynote Systems)

Une présentation sponsorisée bien faite, montrant les difficultés de communication entre deux populations (IT et biz en l’occurence) et comment un outil performant et agréable peut aider à combler ce gap.  
Chez M6Web nous utilisons grafana, et il est vrai que cet outil pourrait largement sortir du périmètre de l’IT. 


## Always Keep an Eye on Your Website Performance - PerfBar Khalid Lafi (WireFilter)

Une rapide démonstration d’un outil en javascript à installer sur les postes de vos développeurs et permettant d'afficher des alertes si un site en production (ou ailleurs) dépasse un certain seuil. 

A découvrir : [PerfBar](http://lafikl.github.io/perfBar/) 

## The Impatience Economy, Where Velocity Creates Value Monica Pal (Aerospike Inc.)

Il y a une génération on attendait 10 jours un échange de courrier postal, aujourd’hui un adolescent vérifie son téléphone toutes les 10 secondes ! Nous sommes moins attentifs, plus impatients.  
De ce constat Monica Pal explique comment les backend webs doivent s’adapter et servir de plus en plus d’informations contextualisées : *search, sort, recommand, personalize*.

## Recruiting for Diversity in Tech Laine Campbell (Pythian)

Un thème récurrent de la velocity de cette année. Laine explique comment l’ascenseur *méritocratique* est cassé et que seul une démarche volontaire permettra d’augementer la diversité dans les entreprises. 

## Better Performance Through Better Design Mark Zeman (SpeedCurve)

La dernière keynote était vraiment excellente. Mark Zeman, venue de Nouvelle Zélande, a expliqué comment le processus créatif pouvait aider à améliorer la performance. Pour cela il faut *redesign the design process*. Pour cela il a proposé, entre autre de : 
- se fixer certains principes/objectifs de performance dès le départ 
- d’ajouter les designers dans la *feature team* et d’itérer via des prototypes
- de partager le savoir sous forme d’informations visuelles


![better_perf_with_better_design1](/images/posts/velocity2014/better_perf_with_better_design1.jpg)

![better_perf_with_better_design2](/images/posts/velocity2014/better_perf_with_better_design2.jpg)

# IT Janitor - How to Tidy Up Mark Barnes (Financial Times)

Ce manager au Financial Times a expliqué comment le journal a été touché de plein fouet par la révolution du web mobile et a dû s’adapter très rapidement. 

![transfo_mobile_FT](/images/posts/velocity2014/transfo_mobile_FT.jpg)

Il a expliqué quelle stratégie il a adopté pour tuer ou refaire les vieux systèmes et comment, en premier lieu, il a vendu le projet à ses supérieurs.  
Il a tout d’abord présenté le TCO de ce qu’il a appelé la version *”classic”* de ft.com (la carotte) puis a appuyé sur la peur de l’incident et les pbs de sécurités (le baton) ; le journal ayant été la cible de hackers israéliens. 

Après une analyse fine du traffic il a ensuite appliqué ces stratégies : 
- tuer directement une application inutile (il y en avait), quitte à la rallumer si quelqu’un finalement en à l’usage :) (et couper un serveur Solaris avec 1833 jours d’uptime !)
- reécrire l’application et la redéployer sur le nouveau système
- tuer une application et écrire plusieurs autres (découpage en micro services)

Son crédo était *”try to make the right thing easier.”* Ainsi les projets basés sur la nouvelle stack disposait *out of the box* de fonctionnalité de monitoring et de log. Cela a motivé pas mal les équipes de développements. 

Au final la purge du legacy a apporter : 
- un gain de 30% de performance 
- un meilleur TTM
- de substantiel retours sur investissement

# Mansplaining 101: Cisadmin Edition Marni Cohen (Puppet Labs)

La conférence la plus geek de la journée. La conférencière a ouvert un terminal et à tapé 

```bash
brew install feminism
```

![marni1](/images/posts/velocity2014/marni1.jpg)




La conférence était très sincère et didactique sur comment mieux intégrer les femmes dans l’IT. 


Voici les scripts et les ressources qu’elle a présenté : [https://gitlab.com/marni/mansplaining](https://gitlab.com/marni/mansplaining)



## Building the FirefoxOS Homescreen

![Firefox OS](http://zef.me/wp-content/uploads/2013/05/FirefoxOS-logo_610x385.png)

Conférence de présentation de l'OS pour smartphone de Firefox.

Lors de cette présentation, Kevin Grandon Ingénieur chez Mozilla nous a présenté le nouvel OS, et nous a initié la programmation sur ce dernier.
Ce nouvel OS est donc basé sur un langue simple : HTML / CSS / Javascript. 

Le développement est donc assez facile à prendre en main, le débugage aussi car on peux monitorer tous ce qu’il se passe sur le device de test via un firebug dédié.

http://slidedeck.io/KevinGrandon/slides-fxos-home-screen-velocity-2014 

https://github.com/KevinGrandon/slides-fxos-home-screen-velocity-2014

## Don’t Kill Yourself : Mobile Web Performance Tricks that Aren’t Worth it - and Somme that Are

Optimisations pour le web mobile.

Lyza Gardner nous a présenté sa vision de l’optimisation sur web mobile. Elle nous a tout d’abord fait un compte rendu sur son expérience personnelle. Liza a chercher via différentes analyses (speedIndex…) à trouver une relation entre temps de chargement , nombres d’assets etc… Et la conclusion qu’elle mettais en avant, c’est qu’il n’y avais pas de recette magique. 
Elle a ensuite fait la parallèle entre le web lors de ces débuts qui était limité par le débit de nos connexions de l’époque, et le web mobile tel qu’il est actuellement. Ainsi certaines optimisation de l’époque sont adaptable, et même toujours valables, à nos problématiques actuelles.
Selon elle, il ne faut pas optimiser un site pour le mobile, mais l’optimiser tout cours. Elle propose de se fixer des objectifs, par exemple se fixer une limite de nombre d’appel asset. Mais surtout d’optimiser / limiter les images puisque 62% du trafic d’un site correspond a ces dernières.


## What are the Third-party Components Doing to Your Site’s Performance?

 Nous utilisons tous des « Third-Party » sur nos sites, mais est-ce une bonne idée ?

Un Third-Party est un script que nous chargeons depuis un autre site. Par exemple : Google Analitycs. Il existe différents type de Third-Party : la publicité, les analyseurs de trafic … La problématique est que nous ne pouvons pas controller ces outils. Nous n’avons pas la main sur le temps de chargement, la disponibilité de l’outils, et cela peux influer sur l’expérience utilisateur et la qualité de nos services.

Pour conclure, il faut trouver le bon compromis entre ce que nous apporte le Third-Party et ce qu’il peux nous couter ...


## Guide to Survive a World Wide Event

Retour d’expérience de Movistar TV, une chaine payante multi-support qui a diffuser la coupe du monde en Espagne, au Brésil et en Argentine. 

Cette société c’est confronté à une problématique de traffic avec des pics de connexions important en peu de temps. La société devais diffuser la coupe du monde FIFA 2014 dans plusieurs pays et sur plusieurs devices différents. Après des tests en condition réels avant le début de la compétition, ils se sont aperçus qu’ils ne pouvais pas gérer le pic de connexion qui arrivais entre 5 minutes avant le coup d’envoie et 5 minutes après, ainsi qu’a la reprise du match et début de deuxième mit-temps.  
Il a donc fallu tout refaire à plusieurs niveaux : 
* Création d’un CDN en interne
* Refonte globale du système de connexion pour pouvoir supporté les pics. 
* Mise en place de monitoring via Graphite
* Mise en place de Tests

Mais en jouant avance beaucoup de problématiques : 
* Multi plateforme
* Déploiement sur plusieurs continent (Amérique du Sud, Europe)
* Rassembler 11 outils de monitoring en un seul.







