# Objectif 

Dans ce TD, vous allez apprendre à collecter des données spatiales provenant de différentes sources. Elles seront utiles pour réaliser le diagnostic de l'environnement naturel autour de votre exploitation agricole (cf. UE "Analyse et Diagnostic d'un agroécosystème"). Nous allons rassembler différentes données au niveau de la petite région agricole (PRA) ainsi qu'au niveau de l'exploitation elle-même (EA).

Pour cet exercice, l'exploitation agricole de Borret (ancien domaine de l'ENSAT) sera utilisée comme exemple. 


# Créer un nouveau projet QGIS

Nous allons enregistrer toutes les données dans un nouveau projet QGIS qui aura pour extension .qgz (format depuis la version 3).
Sous QGIS : `Projet > Nouveau`.


Par défaut, le Système de Coordonnées de Référence (SRC) d'un projet QGIS est celui du système de référence mondial WGS-84 (celui du système GPS), nom de code *EPSG:4326*. Le système de référence du projet est toujours affiché en bas à droite de la fenêtre de QGIS. Vous devriez avoir le SRC suivant : 

![SCR actuel dans QGIS : EPSG:4326](figures/EPSG4326.png)

Les informations relatives à ce SRC sont accessibles depuis la barre d'état de QGIS ou dans le menu `Projet > Propriétés`.

Nous allons changer de SRC pour travailler dans le système de référence officiel de la France métropolitaine : la projection Lambert-93. Nom de code : *EPSG:2154*. Elle est liée au système géodésique RGF93. Les coordonnées sont définies en mètres. Si vous souhaitez en savoir plus sur la projection Lambert, reportez-vous à cette [page dédiée](https://fr.wikipedia.org/wiki/Projection_conique_conforme_de_Lambert).

- Dans l'onglet `SCR` de la fenêtre `Propriété du projet`, recherchez `2154` (code EPSG de la projection) via le filtre. Une fois la projection sélectionnée et le changement appliqué, vous pouvez vérifier qu'il est effectif dans la barre d'état du projet (en bas à droite de la fenêtre QGIS) :

![SCR actuel dans QGIS : EPSG:2154](figures/EPSG2154.png)

- Dans l'onglet `Général` de la fenêtre `Propriété du projet`, donnez un nom (ex. TD_dataCollect). Il apparaîtra à côté du nom de la fenêtre QGIS.

Sauvegardez à présent votre projet dans votre dossier de travail : `Projet > Enregistrer sous...`



# Localiser votre EA

Nous allons représenter le siège de l'EA de Borret sous forme d'un point en s'aidant du Geoportail de l'IGN.


**Méthode 1 : Export du lieu depuis le Geoportail**

L'IGN a conçu un portail de visualisation de nombreuses sources de données spatiales avec quelques fonctionnalités de localisation : [www.geoportail.gouv.fr/](https://www.geoportail.gouv.fr/)

Commencez par rechercher l'EA de Borret. Elle se trouve à Poucharramet en Haute Garonne. Choisissez les photographies aériennes comme fond de carte sur le Geoportail et repérez-vous par rapport à la photo ci-dessous.

![Recherche le siège de l'EA de Borret](figures/Borret.png){ width=50% }

Une fois que l'EA est localisée, sélectionnez l'onglet à droite de l'écran correspondant aux outils, puis `Annoter la carte` et placez votre point (siège de l'EA).

![Annoter la carte pour créer le point de votre exploitation](figures/geoportail_annoter.png)

![Placez votre point et exportez le résultat](figures/geoportail_ajoutpoint.png)

Votre point peut être exporté au format `kml` (depuis le menu `Annoter la carte`). Par défaut, le SRC associé aux objets est le WGS-84 (EPSG:4326). Après import sous QGIS, il faudra veiller à convertir le système pour être cohérent avec celui du projet (EPSG:2154). Nous le verrons par la suite.


**Méthode 2 : import des coordonnées depuis un csv**

Cette méthode ne requiert pas d'annoter la photographie aérienne sur le Geoportail. Elle consiste à lire les coordonnées du siège de l'EA et les enregistrer dans un fichier au format CSV (*comma-separated values*) qu'il sera possible d'importer sous QGIS. Le format CSV est très simple. Il correspond à un tableau décrit sous forme de texte : chaque ligne de texte correspond à une ligne du tableau et chaque virgule correspond au séparateur entre les colonnes. Vous pouvez le créer depuis un tableur (type Excel ou LibreOffice Calc) ou directement depuis un éditeur de texte (type notepad ou gedit). 

Pour obtenir les coordonnées X et Y de votre exploitation, vous pouvez utiliser soit le Géoportail soit Google Maps. Une autre façon de les obtenir serait d'aller sur place et d'utiliser un GPS (celui de votre smartphone par exemple).

Si vous faites dans Google Maps un clic droit sur l'endroit qui vous intéresse et que vous cliquez sur "Plus d'infos sur cet endroit", vous verrez alors apparaître les coordonnées dans l'ordre Y et X (et non X et Y - soit la latitude avant la longitude).

![Obtenir les coordonnées Y et X dans Google Maps](figures/chemin_borret_gmaps.png){height=50px}

Il ne vous reste plus qu'à les enregistrer dans votre tableur (Excel ou LibreOffice Calc) en faisant bien attention à ajouter le nom de chaque colonne :

![Ajouter dans un fichier texte les coordonnées](figures/tableur_csv.png){height=50px}

À noter, les coordonnées fournies par Google Maps utilisent le système de coordonnées géographique EPSG:4326.

Enregistrez maintenant votre fichier au format `csv`.



























