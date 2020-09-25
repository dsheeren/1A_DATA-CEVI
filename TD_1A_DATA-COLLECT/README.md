# Objectifs

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


