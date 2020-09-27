# Objectif 

Dans ce TD, vous allez apprendre à collecter des données spatiales provenant de différentes sources. Elles seront utiles pour réaliser le diagnostic de l'environnement naturel autour de votre exploitation agricole (cf. UE "Analyse et Diagnostic d'un agroécosystème"). Nous allons rassembler différentes données au niveau de la petite région agricole (PRA) ainsi qu'au niveau de l'exploitation elle-même (EA).

Pour cet exercice, l'exploitation agricole de Borret (ancien domaine de l'ENSAT) sera utilisée comme exemple. 


# Créer un nouveau projet QGIS

Nous allons enregistrer toutes les données dans un nouveau projet QGIS qui aura pour extension .qgz (format depuis la version 3).
Sous QGIS : `Projet > Nouveau`.


Par défaut, le Système de Coordonnées de Référence (SRC) d'un projet QGIS est celui du système de référence mondial WGS-84 (celui du système GPS), nom de code EPSG:4326. Le système de référence du projet est toujours affiché en bas à droite de la fenêtre de QGIS. Vous devriez avoir le SRC suivant : 

![SCR actuel dans QGIS : EPSG:4326](figures/EPSG4326.png)

Les informations relatives à ce SRC sont accessibles depuis la barre d'état de QGIS ou dans le menu `Projet > Propriétés`.

Nous allons changer de SRC pour travailler dans le système de référence officiel de la France métropolitaine : la projection Lambert-93. Nom de code : EPSG:2154. Elle est liée au système géodésique RGF93. Les coordonnées sont définies en mètres. Si vous souhaitez en savoir plus sur la projection Lambert, reportez-vous à cette [page dédiée](https://fr.wikipedia.org/wiki/Projection_conique_conforme_de_Lambert).

- Dans l'onglet `SCR` de la fenêtre `Propriété du projet`, recherchez `2154` (code EPSG de la projection) via le filtre. Une fois la projection sélectionnée et le changement appliqué, vous pouvez vérifier qu'il est effectif dans la barre d'état du projet (en bas à droite de la fenêtre QGIS) :

![SCR actuel dans QGIS : EPSG:2154](figures/EPSG2154.png)

- Dans l'onglet `Général` de la fenêtre `Propriété du projet`, donnez un nom (ex. TD_dataCollect). Il apparaîtra à côté du nom de la fenêtre QGIS.

Sauvegardez à présent votre projet dans votre dossier de travail : `Projet > Enregistrer sous...`



# Localiser votre EA

Nous allons représenter le siège de l'EA de Borret sous forme d'un point en s'aidant du Geoportail de l'IGN.


## Méthode 1 : Export du lieu depuis le Geoportail

L'IGN a conçu un portail de visualisation de nombreuses sources de données spatiales avec quelques fonctionnalités de localisation : [www.geoportail.gouv.fr/](https://www.geoportail.gouv.fr/)

Commencez par rechercher l'EA de Borret. Elle se trouve à Poucharramet en Haute Garonne. Choisissez les photographies aériennes comme fond de carte sur le Geoportail et repérez-vous par rapport à la photo ci-dessous.

![Recherche le siège de l'EA de Borret](figures/Borret.png){ width=50% }

Une fois que l'EA est localisée, sélectionnez l'onglet à droite de l'écran correspondant aux outils, puis `Annoter la carte` et placez votre point (siège de l'EA).

![Annoter la carte pour créer le point de votre exploitation](figures/geoportail_annoter.png)

![Placez votre point et exportez le résultat](figures/geoportail_ajoutpoint.png)

Votre point peut être exporté au format `kml` (depuis le menu `Annoter la carte`). Par défaut, le SRC associé aux objets est le WGS-84 (EPSG:4326). Après import sous QGIS, il faudra veiller à convertir le système pour être cohérent avec celui du projet (EPSG:2154). Nous le verrons par la suite.



## Méthode 2 : import des coordonnées depuis un csv

Cette méthode ne requiert pas d'annoter la photographie aérienne sur le Geoportail. Elle consiste à lire les coordonnées du siège de l'EA et les enregistrer dans un fichier au format CSV (*comma-separated values*) qu'il sera possible d'importer sous QGIS. Le format CSV est très simple. Il correspond à un tableau décrit sous forme de texte : chaque ligne de texte correspond à une ligne du tableau et chaque virgule correspond au séparateur entre les colonnes. Vous pouvez le créer depuis un tableur (type Excel ou LibreOffice Calc) ou directement depuis un éditeur de texte (type notepad ou gedit). 

Pour obtenir les coordonnées X et Y du siège de l'EA, vous pouvez utiliser le Géoportail (onglet `outils > Afficher les cooronnées`). Plusieurs SRC sont proposés ce qui est intéressant. Cette source est très fiable. Une alternative est de passer par Google Maps. C'est ce que nous allons choisir ici pour l'exemple. 

Après avoir identifé l'EA sur Google Maps, cliquez (bouton droit) sur le lieu d'intérêt en sélectionnant ensuite l'option `Plus d'infos sur cet endroit` dans la fenêtre. Les coordonnées géographiques apparaissent en dégrés décimaux (EPSG:4326), dans l'ordre Y (latitude) et X (longitude). :warning: Cet ordre est une **source d'erreurs fréquentes** dans les imports...

![Obtenir les coordonnées Y et X dans Google Maps](figures/chemin_borret_gmaps.png){height=50px}

Enregistrez à présent les coordonnées via un tableur ou directement dans un éditeur de texte au format `csv`:

![Ajouter dans un fichier texte les coordonnées](figures/fichier_csv.png){height=50px}



## Charger la localisation de l'EA sous QGIS

Pour importer un fichier, il faut passer par le `Gestionnaire des sources de données` :

![Charger une couche dans QGIS](figures/QGIS_charger.png){height=150px}

- Si vous avez opté pour la méthode 1, sélectionnez l'onglet `Vecteur` depuis le gestionnaire des couches et recherchez votre fichier `kml` comme source à importer (NB : le "glisser/déposer" peut aussi se pratiquer). 

- Si vous avez opté pour la méthode 2, sélectionnez l'onglet `Texte Délimité` et recherchez votre fichier `csv` comme nom à importer. 
:warning: Pensez à bien préciser la géométrie souhaitée. Il s'agit ici de créer un object ponctuel à partir des coordonnées (X,Y) enregistrées. Ainsi, il faut apparier vos colonnes du fichier avec les champs X et Y en choisissant une géométrie `point`. 
:warning: Ne pas oublier de préciser également dans quel SRC sont enregistrées vos coordonnées. Ici, le `SRC de la géométrie` a pour code EPSG:4326.

Une nouvelle couche contenant votre point est ajoutée au projet. Vous pouvez prendre connaissance de ses propriétés pour les contrôler (clic droit sur le nom de la couche > `Propriétés`). Dans l'onglet `Information`, vérifiez le SRC : `EPSG:4326`. Fermez ensuite la fenêtre. 



## Rendre cohérent le SRC de la couche avec celui du projet

Vérifiez le SRC de votre projet. A-t-il changé ? Il est probable qu'il soit repassé en WGS-84 (EPSG:4326) alors que nous l'avions défini en Lambert-93 (EPSG:2154)... Pourquoi ? Allez dans le menu `Préférences > Options` et sélectionnez l'onglet `SRC`. Par défaut, le SRC peut être (re)défini automatiquement lors de l'ajout de la première couche. Pour éviter cela, vous pouvez choisir le Lambert-93 comme SRC par défaut puis, fermer la fenêtre. Il faut ensuite redéfinir le SRC de votre projet (EPSG:2154).

![Changer les options de SRC pour les projets](figures/src.png){height=50px}

Ce n'est pas encore fini ! Le point importé est en WGS-84 alors que nous souhaitons travailler en Lambert-93 (SRC du projet). Le point est quand même visible malgré ses coordonnées car QGIS procède par défaut à une reprojection "à la volée" ce qui rend l'incohérence entre les SRC couche/projet transparente pour l'utilisateur (c'est bien dommage). Il faut donc procéder à une "reprojection" de la couche contenant l'EA pour la basculer dans le bon système de référence. Pour cela, allez dans le menu `Traitement > Boîte à outils` et recherchez l'algorithme `Reprojeter une couche`. NB : si le menu `Traitement` n'est pas accessible, allez dans `Extensions > Installer / Gérer les extensions` et activez l'extension `Processing`.

Le SCR cible de la nouvelle couche projetée doit être `EPSG:2154` comme celui de votre projet. Cette couche est à enregistrer dans le format [GeoPackage](https://www.geopackage.org/) (extension `gpkg`). Il s'agit d'un format récent, ouvert, et non propriétaire, implémenté sous forme d'une base de données SQLite. Une fois enregistrée, votre couche sera ajoutée dans QGIS. Vous pouvez alors supprimer les précédentes couches en WGS-84.

![Enregistrez votre nouvelle couche au format gpkg](figures/QGIS_gpkg.png){height=100px}



## Ajouter le nom de votre exploitation

Si vous n'avez pas le nom de votre exploitation dans votre fichier vectoriel, il va falloir le modifier. Cliquez (bouton droit) sur la couche et sélectionnez `Ouvrir la table d'attributs`. Par défaut vous ne pouvez pas modifier le contenu des champs (le fichier est en mode *lecture*). Pour permettre l'édition (mode *écriture*), il faut activer le crayon en haut à gauche de la fenêtre. Vous pouvez alors reneigner le nom de votre exploitation agricole dans la colonne `Nom` (ex. Borret). Une fois l'édition terminée, désactivez le crayon. 


## Modifier l'affichage de votre exploitation

### Changer le type d'icône

Dans les `Propriétés` de la couche, l'onglet `Symbologie` vous permet de changer tout ce qui a trait à la représentation de vos données. Sélectionnez `Symbole Simple` et changez le type de symbole en `Symbole SVG`. De nombreux symboles sont disponibles. Il est aussi possible d'importer des fichiers SVG. C'est l'option que nous allons choisir en important un symbole depuis l'URL suivante : [https://www.svgrepo.com/show/228574/silo.svg](https://www.svgrepo.com/show/228574/silo.svg). Modifiez à présent la taille du symbole avec l et h = 10 mm.

![Nouveau symbole SVG importé depuis une URL](figures/symbole.png)

### Afficher le nom de l'EA (étiquette)

En restant dans les `Propriétés` de la couche, sélectionnez l'onglet `Étiquettes`. Choisissez `Étiquettes simples` avec comme valeur celle du champ `Nom`. En adoptant une position `cartographique`, appliquez une `distance de décalage` pour cette étiquette `à partir de l'emprise du symbole`. Le nom de l'exploitation doit désormais apparaître sur la carte après application. 


# Ajouter un fond cartographique

Quand on dispose d'un fond cartographique (ex. photographie aérienne, carte topographique) sur son disque dure local, il suffit de l'importer dans le projet QGIS. Une alternative est d'avoir recours à des fonds cartographiques enregistrés sur des serveurs distants. Ceux-ci sont alors disponibles via des *services Web*. Ces services sont accessibles via une URL (adresse qui pointe vers le serveur) renseignée dans l'application cliente (ici QGIS). Plusieurs types de services existent : (1) le WMS (*Web Map Service*) qui renvoie des données en mode image, (2) le WFS (*Web Feature Service*) qui retourne des données en mode vecteur, et (3) le WCS (*Web Coverage Service*) qui renvoie des données raster avec des fonctions d'interrogation plus avancées que le WMS.

## Visualiser un fond OpenStreetMap ou Google Maps via un flux

Par défaut QGIS n'intègre pas des fournisseurs de tuiles (Google Maps, Bing, OpenStreetMap). Deux solutions pour y accéder :

1. Installer un *plug-in* dédié. Pour cela, dans le menu `Extensions > Installer`, recherchez le *plug-in* `QuickMapServices` et installez-le. Vérifiez ensuite l'installation et les données disponibles par défaut dans le menu `Internet > QuickMapServices`. Le *plug-in* donne accès à certaines sources mais pas à Google Maps ou Bings par défaut. Pour cela, il faut récupérer les autres contributions via le menu `settings` du *plug-in* et l'onglet `More services`.

2. Se conncecter à un service de tuile XYZ. Pour cela, sélectionnez `XYZ Tiles` dans le panneau `Explorateur` de QGIS. Ensuite, créez une `nouvelle connexion` (clic bouton droit) avec pour nom "Google Maps" et pour URL `https://mt1.google.com/vt/lyrs=m&x=%7Bx%7D&y=%7By%7D&z=%7Bz%7D`. Le flux est maintenant disponible et vous pouvez l'exploiter. Pour importer une liste prédéfinie de flux utiles, vous pouvez exécuter un script python dans la console QGIS (`Ctrl+Alt+P`) en copiant-collant les lignes du fichier suivant : [**https://git.io/fjMJq**](https://raw.githubusercontent.com/klakar/QGIS_resources/master/collections/Geosupportsystem/python/qgis_basemaps.py). C'est beau la technique... ;-)

![Flux de fonds de carte gratuits](figures/connexionXYZ.png)

> **A noter** : les données accessibles sont définies dans un système de projection dit pseudo-Mercator (EPSG:3857). Il est différent du SRC de votre projet. QGIS applique donc une reprojection à la volée pour que tout se passe bien. 

Dans le panneau `Explorateur`, vous aurez désormais accès à des dizaines de fournisseurs de tuiles dans la partie `XYZ Tiles`. Double-cliquez sur `Google Satellite` pour avoir uniquement une image en fond.


## Visualiser un fond issu du Geoportail de l'IGN via un flux

L'IGN a également mis en place une liste de *Geoservices*. On peut ainsi accéder à une partie des données du Geoportail via les URL suivantes :

- `https://wxs.ign.fr/choisirgeoportail/geoportail/wmts?SERVICE=WMTS&REQUEST=GetCapabilities` (pour les ressources images)
- `https://wxs.ign.fr/choisirgeoportail/geoportail/wfs?SERVICE=WFS&REQUEST=GetCapabilities` (pour les ressources vecteur)

Le WMTS est un [service d'images tuilées](https://geoservices.ign.fr/documentation/geoservices/wmts.html) (Web Map Tile Service). Il contient dans son adresse une clé (= "choisirgeoportail"), définie par l'IGN. Cette clé ne nécessite pas la création d'un compte au préalable. Elle donne directement accès à certaines ressources comme les photographies aériennes, pour un test. Reportez-vous à la [documentation](https://geoservices.ign.fr/documentation/services-acces.html) des *Geoservices* de l'IGN pour davantage de détail.

Pour configurer ce service sous QGIS, sélectionnez `WMS/WMTS` dans le panneau `Explorateur` et créez (clic bouton droit) une nouvelle connexion "Geoportail" en reportant l'URL mentionnée ci-dessus. Vous devriez obtenir les flux suivants :

![Flux WMTS du Geoportail](figures/wmts_ign.png)

Pour les ressources vecteur (parcelles cadastrales issues de la BDParcellaire, bâtiments issus de la BDTopo), c'est la même démarche mais depuis l'option `WFS` du panneau `Explorateur`. Une illustration après ajout et changement de symbologie est présentée ci-dessous.

![Exploitation agricole avec bâtiments et parcelles cadastrales](figures/EA_parcellaireCad.png)


# Rechercher des données relatives à l'environnement de l'EA

## Les limites communales (site IGN)

Nous allons d'abord télécharger les communes de Haute-Garonne à partir de la base de données ADMIN EXPRESS (qui remplace la base GEOFLA). Cette base contient notamment des couches de régions, départements et communes au format vecteur. Elle est accessible sur la page du [site de l'IGN](https://geoservices.ign.fr/documentation/diffusion/telechargement-donnees-libres.html#admin-express) qui regroupe les données libres.

Télécharger ([lien ftp](ftp://Admin_Express_ext:Dahnoh0eigheeFok@ftp3.ign.fr/ADMIN-EXPRESS_2-4__SHP__FRA_L93_2020-09-15.7z)) l'édition 2020 par territoire. Décompressez ensuite l'archive .7z et recherchez la couche COMMUNE au format .shp (projection Lambert-93). Importez-là sous QGIS. Prenez connaissance de la représentation cartographique et du contenu de la table attributaire (clic droit sur la couche > `Ouvrir la table d'attributs`)

Pour réduire la taille du fichier, nous allons appliquer un filtre pour ne sélectionner que les communes de la Haute-Garonne (31). Pour cela, depuis la table attributaire, dans la barre d'outils, cliquez sur l'icône `Sélectionner les entités en utilisant une expression`. Appliquez ensuite la procédure suivante :

- Cliquez sur `Champs et valeurs` (colonne du milieu) pour voir la liste des champs de la table (i.e. les attributs)
- Double-cliquez sur le champ INSEE_DEP ; apparition dans la case `Expression` à gauche de la fenêtre (notez les guillemets doubles)
- Cliquez sur l'opérateur =
- Rajouter le numéro de département 31 
- Lancer la requête en cliquant sur le bouton `Sélectionner des entités` en bas de la fenêtre

![Requête SQL pour conserver les communes de Haute-Garonne](figures/requete_sql31.png)

Fermez à présent la table attributaire. Cliquez ensuite (bouton droit) sur la couche COMMUNE > `Exporter` > `Sauvegarder les entités sélectionnées sous...` Choisissez comme `Nom de fichier` votre fichier au format gpkg déjà créé précédemment (point relatif au siège de l'EA). Ce format peut contenir plusieurs couches. Précisez "Communes" pour le `Nom de la couche` et vérifiez que l'option `N'enregistrer que les entités sélectionnées` est bien cochée. Une fois la sauvegarde réalisée, vous pouvez ne conserver que la nouvelle couche des communes du département 31. Au passage, vous pouvez constater dans le panneau `Explorateur` que votre base de données gpkg (GeoPackage) contient bien deux couches.


![Couche des communes (31) au format gpkg](figures/geoPackage_dpt.png)


## Les Petites Régions Agricoles (site agreste)

Les Régions Agricoles (RA) constituent un zonage d'agriculture homogène composé d'un ensemble de communes. Le croisement avec les limites départementales conduit aux Petites Régions Agricole (PRA). Ce découpage a été initialisé en 1946 et actualisé par la suite. La liste des PRA est [accessible sur le site](https://agreste.agriculture.gouv.fr/agreste-web/methodon/Z.1/!searchurl/listeTypeMethodon/) du service statistique ministériel de l'agriculture (agreste). Le référentiel date de 2017. Il s'agit d'un fichier .xls à télécharger.

Sous cette forme, il n'est pas possible de spatialiser les PRA. Pour y parvenir, on va réaliser une *jointure* attributaire avec le fichier des communes.

































