# ROPF Demo

Démo fictionnelle d'un **Registre Ouvert des Personnes Français (ROPF)**

## Contenu

- `RFC-ROPF.md` : spécification technique
- `schema-ropf-v0.1.json` : schéma JSON de démonstration
- `exemples/citoyen.json` : exemple complet d'un dossier individuel
- `exemples/foyer.json` : exemple de foyer
- `exemples/compte_tiers.json` : exemple isolé d'un compte numérique tiers

## Important

Ce dépôt est une **fiction technique**.  
Tous les identifiants, numéros, mots de passe, codes, secrets et références sont **fictifs** et **non réutilisables**.

## Arborescence

```text
ropf_demo/
├── RFC-ROPF.md
├── schema-ropf-v0.1.json
└── exemples/
    ├── citoyen.json
    ├── foyer.json
    └── compte_tiers.json
```

## Description des fichiers

### `RFC-ROPF.md`
Spécification technique fictive du format ROPF.

Ce document joue le rôle d’une RFC (Request For Comments) :
- il définit la structure globale des données ;
- il décrit chaque bloc (`etat_civil`, `comptes_numeriques`, etc.) ;
- il fixe les conventions de nommage et les règles de format ;
- il fournit des exemples JSON réalistes.

C’est la référence principale pour comprendre et implémenter le format.

---

### `schema-ropf-v0.1.json`

[Schéma JSON du format ROPF.](schema-ropf-v0.1.json)

Schéma JSON (JSON Schema Draft 2020-12) du format.

Il permet de :
- valider automatiquement les fichiers ROPF ;
- vérifier la présence des champs obligatoires ;
- contrôler les types (string, array, object, etc.) ;
- faciliter l’intégration dans des outils ou pipelines.

C’est la base technique pour toute validation ou intégration automatisée.

---

### `exemples/citoyen.json`

[Exemple complet d’un dossier ROPF.](exemples/citoyen.json)

Exemple complet d’un dossier ROPF.

Il illustre :
- une fiche individuelle complète ;
- l’ensemble des blocs principaux (identité, coordonnées, adresses, comptes, administratif, etc.) ;
- la cohérence globale des données ;
- un cas réaliste de centralisation massive d’informations.

C’est le fichier de référence pour comprendre la structure globale.

---

### `exemples/foyer.json`

[Exemple de structure de foyer.](exemples/foyer.json)

Exemple de structure de foyer.

Il montre :
- la composition d’un ménage ;
- les relations entre individus ;
- les rattachements administratifs (CAF, impôts) ;
- une vue agrégée au niveau familial.

Utile pour modéliser les liens entre plusieurs dossiers individuels.

---

### `exemples/compte_tiers.json`

[Exemple détaillé d’un compte numérique dans un contexte de fuite massive.](exemples/compte_tiers.json)

Exemple détaillé d’un compte numérique dans un contexte de fuite massive.

Il contient :
- des identifiants de connexion fictifs ;
- des mots de passe volontairement bidon ;
- des historiques de connexion ;
- des données issues de plusieurs services (e-commerce, administratif, santé, etc.) ;
- des traces d’exposition à des fuites.

Ce fichier sert à illustrer concrètement l’impact d’une centralisation extrême des données numériques.

---

## Lecture recommandée

1. Commencer par `RFC-ROPF.md` pour comprendre le modèle
2. Consulter `exemples/citoyen.json` pour voir une implémentation complète
3. Explorer `exemples/compte_tiers.json` pour le détail des données numériques
4. Utiliser `schema-ropf-v0.1.json` pour valider les fichiers