---
title : Le projet "Vaccination COVID-19"
language: fr
author: Romain Tavenard
rights: Creative Commons CC BY-NC-SA
---

# Organisation

* Groupes de 2 ou 3 étudiants du même groupe de TD.
* Déclaration des groupes :
  * au plus tard le jeudi 18/11/2021, par dépôt sur CURSUS d'un fichier contenant le nom des membres du groupe
  * si pas inscrit dans un groupe à cette date : note de 0 au projet
* Rendu final : au plus tard le vendredi 10/12/2021, 23h59

# Contenu du projet

Dans ce projet, vous serez amenés à manipuler des données  concernant les centres de vaccination contre la COVID-19.
Le but principal de ce projet est de lister les centres situés à Rennes et qui proposent des rendez-vous pour une première dose de vaccin.
La section "Bonus" ci-dessous vous propose également des objectifs secondaires qui vous permettront d'embellir votre projet si ce but principal est déjà rempli.

# But principal

Dans le cadre de la vaccination contre la COVID-19, une grande partie des prises de rendez-vous se font en ligne, via des plateformes (dont doctolib).
Pour permettre à des applications tierces (telle que ViteMaDose, par exemple) d'accéder aux informations de rendez-vous disponibles, ces plateformes publient les données relatives aux centres de vaccination et aux rendez-vous qu'ils proposent.

Votre but principal, dans le cadre de ce projet, sera de **lister les centres de vaccination situés à Rennes qui proposent des premières injections de vaccin anti-COVID-19 (sans se soucier de savoir si des créneaux sont disponibles)**.

Pour cela, vous vous appuierez sur des données disponibles librement, présentées plus en détail dans la section "Données" ci-dessous.


# Données

Le site <https://data.gouv.fr> met régulièrement à jour une liste des centres de vaccination situés en France. Les informations permettant de récupérer ces données sont disponibles sur [cette page](https://www.data.gouv.fr/fr/datasets/lieux-de-vaccination-contre-la-covid-19/).

Vous devrez vous baser sur ces données pour repérer les centres de vaccinations situés à Rennes (le code postal de la ville de Rennes est 35000).
Il vous est demandé d'accéder à ces données via l'API REST (et non pas en enregistrant le fichier de données sur votre ordinateur). De cette manière, à chaque fois que votre script s'exécutera, vous travaillerez sur la dernière version disponible de la liste des centres de vaccination.

Dans ces données, une URL est associée à chaque centre de vaccination, il s'agit de l'adresse à entrer dans un navigateur web pour atteindre l'interface de prise de rendez-vous pour le centre en question.
Dans ce projet, nous ne nous intéresserons qu'aux centres pour lesquels l'interface de réservation est la plateforme doctolib.

Voici un exemple d'URL associée à un centre de vaccination :
<https://partners.doctolib.fr/centre-de-sante/ile-et-vilaine/centre-de-vaccination-covid-19-vaccimobile-35-ars-communes-ile-et-vilaine?pid=practice-178662&enable_cookies_consent=1>

La partie qui nous intéresse dans cette URL est située entre le dernier `/` et le point d'interrogation `?` :

`centre-de-vaccination-covid-19-vaccimobile-35-ars-communes-ile-et-vilaine`

Dans la suite, nous appellerons cette sous-partie de l'URL le **nom de code** du centre de vaccination.

Les données relatives à un centre de vaccination sont disponibles via l'API REST de doctolib, à l'URL suivante :

<https://partners.doctolib.fr/booking/NOM_DE_CODE.json>

où `NOM_DE_CODE` doit être remplacé par le nom de code du centre en question.
Attention, doctolib impose, pour l'accès à son API REST, qu'un `User-Agent` soit renseigné lors de la requête HTTP.

Dans les données fournies pour chaque centre, on trouve notamment une liste de `visit_motives`, et dans le cadre de ce projet, on vous demande de lister, pour chaque centre rennais, les `visit_motives` correspondant à des rendez-vous pour première injection.

# Bonus

Outre le but principal énoncé plus haut, vous êtes libres de proposer un certain nombre de bonus qui vous rapporteront des points supplémentaires s'ils sont correctement implémentés (un projet qui n'implémenterait que le but principal ne pourrait pas viser la note de 20).

Nous vous proposons ci-dessous quelques bonus possibles, et vous êtes libres d'en choisir parmi cette liste et/ou d'en implémenter d'autres à votre convenance :

* Afficher les horaires d'ouverture mises en forme pour chaque centre de vaccination (accessible à toutes et tous)
* Générer une sortie HTML contenant une carte indiquant la localisation des différents centres de vaccination et les informations les concernant (requiert de découvrir une nouvelle librairie : [`folium`](https://python-visualization.github.io/folium/quickstart.html), par exemple en lisant [ce tutoriel](https://deparkes.co.uk/2016/06/03/plot-lines-in-folium/))
* Trouver les `visit_motives` pour lesquelles il existe des rendez-vous disponibles (nécessite un goût prononcé pour les enquêtes approfondies, sachant que les créneaux disponibles sont accessibles via une URL du type : <https://partners.doctolib.fr/availabilities.json?start_date=DATE_DEBUT&visit_motive_ids=VISIT_MOTIVE_ID&agenda_ids=LISTE_AGENDA_IDS&practice_ids=LISTE_PRACTICE_IDS&destroy_temporary=true&limit=10> où les listes sont des séries d'identifiants séparés par des tirets `-`)

Enfin, si vous ne l'avez pas déjà fait, utilisez votre programme pour vous renseigner sur le centre de vaccination le plus proche de chez vous et prendre rendez-vous. Cela n'offre pas de point bonus, mais peut sauver des vies :)

# Évaluation

Pour l'évaluation, il sera porté une attention particulière à ce que votre code soit lisible (commentaires : ni trop ni trop peu, nom de variables / fonctions pertinents, etc.) et bien découpé en blocs comme vous avez pu le voir lors du TD "Analyse et décomposition de problèmes".

De plus, les éléments notés "Bonus" plus haut n'en sont pas vraiment : il n’est pas envisageable d'obtenir la note maximale en se contentant d'implémenter le "but principal".
Typiquement, sur les 20 points de la note finale, 6 seront dédiés à la qualité et l'originalité des bonus proposés.