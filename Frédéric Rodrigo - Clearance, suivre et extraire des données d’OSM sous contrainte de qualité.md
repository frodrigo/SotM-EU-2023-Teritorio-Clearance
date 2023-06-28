---
title: 2023 - Clearance, suivre et extraire des données d’OSM sous contrainte de qualité
css: 'style.css'
---

# Clearance
## Suivre et extraire des données d’OSM sous contrainte de qualité

## SotM FR 2023

Frédéric Rodrigo - Teritorio

frederic@teritorio.fr

---

## Contexte

Besoin
- Exposer et diffuser des données OSM
  - site web, carte papier
- Qualité et responsabilité contenu
  - par ex. DAE

Souhait
- Contribuer à OSM
- Collaborer
- Mettre à jour les données

---

# Qualité

----

### Qualité - À priori

Validateur dans les éditeurs

- Règles variables
- Validation et respect des règles facultatives
- Besoin en validation différente suivant la thématique

----

### Qualité - À posteriori

Détection d’anomalies

- Keep Right
- OSM Inspector
- Osmose-QA

Itération sur la qualité


---

## Mise à jour

- Diff entrant
- Rétro action de correction

![](include/04-OSM-diff-update.png)

La qualité des mises à jour n’est jamais assurée

---

## Contrôle externe des changements

Contrôle des changements dans OSM

- OSMCha
- Osm-analytic-tracker

![](include/09-osmcha.png)


---

## Filtre des mises à jour

![](include/05-OSM-diff-update-filter.png)

----

### Filtre simple

- [LeBonTag](https://www.lebontag.fr/) (libre)
- Teritorio (pseudo libre)

![](include/11-ideomap.png)

----

### LoCha

MaRS / Daylight de Meta (Facebook)

- Cohérence locale des changements
- Mise à jour partielles

![](include/12-mars.png)

---

## Problème

- MaRS : outil privé
- Daylight : règles et fréquence non maîtrisées
- LeBonTag : non collaboratif, sortie SIG, validation par objet

---

## Le besoin

Extrait OSM à qualité maîtrisée

- Flux de mise à jour, à la minute
- Filtrage automatique
  - maîtrise des règles
  - faible charge de travail humain
- Collaboratif
  - validation humain
  - projet par territoires et thématiques
- Cohérence locale des validations
- Format I/O : PBF OSM + diff

---

# Clearance

----

## Projet Clearance

1 instance Clearance, plusieurs projets.

Un projet. Une communauté.
- Une zone : Extract OSM + Diff
- Une thématique
- Règles de validation

Par ex : le tourisme, les stations ferroviaires, la randonné…

----

## Moteur Clearance

- Base de donnes, import
  - Extract OSM
  - Diff, sans les appliquer
- Moteur de règles pour valider les LoCha
  - OK ⇒ LoCha appliqué
  - Pas OK ⇒ LoCha en rétention
    - Si Σ changement V+1 OK ⇒ application
    - Sinon application LoCha manuelle
- Export d'un Extract OSM + Diff

Invariant : la qualité ne fait qu'augmenter*.

----

## Règles de validation

Analyse
- metadata
- tags
- geom

----

## Règles de validation

Annotations indépendante ou en groupe

geom, tag par tag...

- Acceptable
- Doutable / sans avis
- Rejeté

Entre dernière version intégré et LoCha en rétention

----

## Ex de règles

- Rejet du changement
  - déplacement geom > 10m
  - changement par un contributeur débutant
  - balck list des tags
- Validation de l'état final
  - une boulangerie doit avoir un nom
  - pas de boulangerie en doublon

---

## Clearance Beta

- ✅ Import / Export + diff
- ⌛ Jeux de règle de validation
- ⏳ Interface de contrôle et validation manuelle
- 🯀 Validation par LoCha

[Demo beta](https://clearance-dev.teritorio.xyz/landes_tourism_poi/changes_logs/)


---

# Conclusion

Clearance : Extrait OSM à qualité maîtrisée

- Prototype encore en cours
- Vous voulez tester ?
- https://github.com/teritorio/clearance
- https://github.com/teritorio/clearance-frontend
