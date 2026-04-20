# RFC-DRAFT — Registre Ouvert des Personnes Français (ROPF)

- Statut : Draft fictif
- Version : 0.1.0
- Langue : fr-FR
- Format : JSON UTF-8
- Usage : démonstration dystopique / maquette narrative / test d’interopérabilité

---

## 1. Résumé

Le **Registre Ouvert des Personnes Français (ROPF)** définit un format JSON unifié permettant de représenter, agréger et échanger l’ensemble des données relatives à une personne physique dans un environnement où la séparation entre vie publique et vie privée n’existe plus.

Dans ce modèle, une fiche individuelle peut contenir :

- l’identité civile ;
- les coordonnées ;
- la situation familiale ;
- les adresses ;
- les rattachements administratifs ;
- les comptes numériques ;
- les traces de consommation ;
- les équipements utilisés ;
- les liens vers des pièces ;
- les accès applicatifs tiers.

---

## 2. Objectif

Le format ROPF a pour objectif de fournir :

1. un schéma interopérable entre administrations, opérateurs, plateformes et services ;
2. un modèle extensible pour centraliser les informations sur une personne ;
3. une structure lisible, versionnable et diffusable ;
4. un support technique de démonstration pour projets de fiction, prototypes, tests de parsing ou maquettes de systèmes totalisants.

---

## 3. Terminologie

Les mots-clés **DOIT**, **NE DOIT PAS**, **DEVRAIT**, **PEUT** sont à interpréter comme des exigences normatives.

### 3.1 Sujet
La personne physique décrite par l’objet JSON.

### 3.2 Dossier
L’enregistrement complet correspondant à un sujet.

### 3.3 Source
L’organisme, service, plateforme ou système ayant produit l’information.

### 3.4 Compte tiers
Un compte détenu par le sujet sur un service externe.

### 3.5 Secret fictif
Une valeur volontairement fausse, utilisée uniquement pour illustrer la disparition symbolique de la vie privée dans la fiction.

---

## 4. Contraintes générales

### 4.1 Encodage
Les documents ROPF DOIVENT être encodés en UTF-8.

### 4.2 Format
Les documents ROPF DOIVENT être valides en JSON.

### 4.3 Convention de nommage
Les noms de propriétés DOIVENT être en `snake_case`.

### 4.4 Horodatage
Les dates complètes DOIVENT utiliser ISO 8601.

Exemple :

```json
"date_mise_a_jour": "2026-04-20T13:45:00Z"
```

### 4.5 Extensibilité
Les champs non standard DOIVENT être placés dans `extensions`.

---

## 5. Structure générale d’un dossier ROPF

Un dossier ROPF DOIT être un objet JSON contenant au minimum les propriétés suivantes :

```json
{
  "schema": "urn:ropf:0.1",
  "version_schema": "0.1.0",
  "id_dossier": "uuid",
  "personne": {},
  "etat_civil": {},
  "coordonnees": {},
  "adresses": [],
  "foyer": {},
  "comptes_numeriques": [],
  "liens_administratifs": {},
  "documents": [],
  "historique": [],
  "audit": {},
  "extensions": {}
}
```

---

## 6. Description des blocs

### 6.1 `schema`
Identifiant canonique du schéma.

Type : `string`

Exemple :

```json
"schema": "urn:ropf:0.1"
```

### 6.2 `version_schema`
Version de la spécification appliquée.

Type : `string`

Exemple :

```json
"version_schema": "0.1.0"
```

### 6.3 `id_dossier`
Identifiant unique du dossier.

Type : `string`

Exemple :

```json
"id_dossier": "8f6c3f4c-4ee4-4c49-b2f3-f4e2d8a7e991"
```

### 6.4 `personne`
Bloc principal décrivant le sujet.

Type : `object`

Champs recommandés :

- `type_personne`
- `statut_existence`
- `langue_principale`
- `date_creation_dossier`

Exemple :

```json
"personne": {
  "type_personne": "personne_physique",
  "statut_existence": "vivant",
  "langue_principale": "fr",
  "date_creation_dossier": "2026-04-20T10:00:00Z"
}
```

---

## 7. Bloc `etat_civil`

Le bloc `etat_civil` DOIT contenir les informations d’identité civile.

Champs possibles :

- `prenom`
- `deuxieme_prenom`
- `nom`
- `nom_usage`
- `sexe_declare`
- `date_naissance`
- `commune_naissance`
- `departement_naissance`
- `pays_naissance`
- `nationalites`
- `surnoms`
- `identifiants_officiels`

Exemple :

```json
"etat_civil": {
  "prenom": "Jean",
  "deuxieme_prenom": "Michel",
  "nom": "Dupont",
  "nom_usage": "Dupont",
  "sexe_declare": "masculin",
  "date_naissance": "1987-04-12",
  "commune_naissance": "Nancy",
  "departement_naissance": "54",
  "pays_naissance": "FR",
  "nationalites": ["FR"],
  "surnoms": ["JMD"],
  "identifiants_officiels": [
    {
      "type_identifiant": "nir",
      "valeur": "1 87 04 54 123 *** **",
      "source": "assurance_maladie",
      "verifie": true
    }
  ]
}
```

---

## 8. Bloc `coordonnees`

Le bloc `coordonnees` regroupe les moyens de contact.

Exemple :

```json
"coordonnees": {
  "emails": [
    {
      "adresse": "jean.dupont@example.fr",
      "type": "personnel",
      "principal": true,
      "verifie": true
    }
  ],
  "telephones": [
    {
      "numero": "+33601020304",
      "type": "mobile",
      "principal": true,
      "verifie": true
    }
  ],
  "sites_web": [
    "https://jeandupont.example.fr"
  ]
}
```

---

## 9. Bloc `adresses`

Le bloc `adresses` DOIT être un tableau d’objets.

Types d’adresse suggérés :

- `residence_principale`
- `residence_secondaire`
- `ancienne_adresse`
- `adresse_professionnelle`
- `adresse_facturation`

Exemple :

```json
"adresses": [
  {
    "type_adresse": "residence_principale",
    "ligne_1": "12 rue des Lilas",
    "ligne_2": "",
    "code_postal": "57000",
    "commune": "Metz",
    "departement": "57",
    "pays": "FR",
    "coordonnees_gps": {
      "latitude": 49.1193,
      "longitude": 6.1757
    },
    "date_debut": "2021-09-01"
  }
]
```

---

## 10. Bloc `foyer`

Le bloc `foyer` décrit la composition du ménage.

Exemple :

```json
"foyer": {
  "id_foyer": "foyer-57-0001",
  "type_foyer": "couple_avec_enfants",
  "nombre_adultes": 2,
  "nombre_enfants": 2,
  "membres": [
    {
      "id_personne_reference": "personne:conjoint-001",
      "role": "conjoint"
    },
    {
      "id_personne_reference": "personne:enfant-001",
      "role": "enfant"
    }
  ]
}
```

---

## 11. Bloc `parcours_professionnel`

Ce bloc PEUT être utilisé pour décrire les situations professionnelles successives.

Exemple :

```json
"parcours_professionnel": [
  {
    "employeur": "SAS Exemple",
    "poste": "Développeur web",
    "type_contrat": "cdi",
    "date_debut": "2020-01-15",
    "email_professionnel": "j.dupont@sas-exemple.fr",
    "revenu_annuel_net_estime": 42000
  }
]
```

---

## 12. Bloc `liens_administratifs`

Ce bloc centralise les rattachements à des portails ou services publics français.

Exemple :

```json
"liens_administratifs": {
  "franceconnect": {
    "identifiant_connexion": "jean.dupont.fc@example.fr",
    "statut": "actif"
  },
  "impots_gouv": {
    "numero_fiscal": "273849102938",
    "reference_avis": "26AX93847",
    "statut": "actif"
  },
  "ameli": {
    "numero_assure_suffixe": "78",
    "cpam_rattachement": "Moselle",
    "statut": "actif"
  },
  "caf": {
    "numero_allocataire": "5482910X",
    "caisse_rattachement": "CAF Moselle",
    "statut": "actif"
  },
  "ants": {
    "identifiant_portail": "jd_ants_57",
    "statut": "actif"
  },
  "mon_compte_formation": {
    "identifiant_portail": "jean.dupont@example.fr",
    "statut": "actif"
  }
}
```

---

## 13. Bloc `comptes_numeriques`

Le bloc `comptes_numeriques` DOIT être un tableau de comptes tiers.

Chaque entrée PEUT contenir :

- `id_compte`
- `service`
- `categorie_service`
- `identifiant_connexion`
- `mot_de_passe_fictif`
- `methode_authentification`
- `double_facteur_active`
- `email_recuperation`
- `telephone_recuperation`
- `questions_recuperation`
- `date_derniere_connexion_connue`
- `statut_compte`

### Exemple

```json
"comptes_numeriques": [
  {
    "id_compte": "cmp-google-001",
    "service": "google",
    "categorie_service": "identite_numerique",
    "identifiant_connexion": "jean.dupont@gmail.com",
    "mot_de_passe_fictif": "motdepasse_bidonnnn_2026",
    "methode_authentification": [
      "mot_de_passe",
      "totp"
    ],
    "double_facteur_active": true,
    "email_recuperation": "secours.dupont@example.fr",
    "telephone_recuperation": "+33600000000",
    "questions_recuperation": [
      {
        "question": "nom de votre premier chat",
        "reponse_fictive": "chaussette-factice"
      }
    ],
    "date_derniere_connexion_connue": "2026-04-19T21:11:00Z",
    "statut_compte": "actif"
  }
]
```

---

## 14. Bloc `documents`

Le bloc `documents` référence des pièces ou supports.

Exemple :

```json
"documents": [
  {
    "id_document": "doc-cni-001",
    "type_document": "carte_nationale_identite",
    "numero_document": "IDFR-FAUX-123456",
    "date_expiration": "2031-05-12",
    "fichier_reference": "objets/documents/cni-jean-dupont.pdf",
    "empreinte_sha256": "3c7f0f7a8b2d-demo-factice"
  }
]
```

---

## 15. Bloc `historique`

Le bloc `historique` est un journal événementiel.

Exemple :

```json
"historique": [
  {
    "id_evenement": "evt-001",
    "type_evenement": "changement_adresse",
    "date_evenement": "2021-09-01T10:00:00Z",
    "description": "Installation à Metz"
  },
  {
    "id_evenement": "evt-002",
    "type_evenement": "ouverture_compte",
    "date_evenement": "2018-03-12T09:12:00Z",
    "description": "Création d’un compte sur une plateforme de commerce"
  }
]
```

---

## 16. Bloc `audit`

Le bloc `audit` DOIT contenir les métadonnées de production du dossier.

Exemple :

```json
"audit": {
  "date_creation": "2026-04-20T10:00:00Z",
  "date_mise_a_jour": "2026-04-20T13:45:00Z",
  "sources": [
    {
      "nom_source": "registre_central_demo",
      "date_import": "2026-04-20T10:00:00Z"
    },
    {
      "nom_source": "agregateur_services_demo",
      "date_import": "2026-04-20T10:15:00Z"
    }
  ],
  "niveau_confiance_global": 0.92
}
```

---

## 17. Bloc `extensions`

Les données non prévues par le schéma standard DOIVENT être placées dans `extensions`.

Exemple :

```json
"extensions": {
  "x_consommation": {
    "enseignes_habituelles": ["Carrefour", "Amazon", "Leroy Merlin"]
  },
  "x_equipements": {
    "appareils": [
      {
        "type": "telephone",
        "marque": "Samsung",
        "modele": "Galaxy S24",
        "imei_fictif": "IMEI-DEMO-0001"
      }
    ]
  }
}
```

---

## 18. Nomenclature recommandée

### 18.1 Suffixes recommandés

- `_id` : identifiant interne
- `_date` : date simple
- `_datetime` : date et heure
- `_ref` : référence externe
- `_fictif` : valeur volontairement bidon
- `_principal` : booléen de primauté
- `_actif` : booléen de statut
- `_source` : origine de la donnée

### 18.2 Préfixes recommandés

- `x_` : extension hors standard
- `id_` : identifiant
- `date_` : date
- `nombre_` : comptage
- `type_` : catégorie
- `nom_` : libellé

---

## 19. Exemple minimal conforme

```json
{
  "schema": "urn:ropf:0.1",
  "version_schema": "0.1.0",
  "id_dossier": "8f6c3f4c-4ee4-4c49-b2f3-f4e2d8a7e991",
  "personne": {
    "type_personne": "personne_physique",
    "statut_existence": "vivant",
    "langue_principale": "fr",
    "date_creation_dossier": "2026-04-20T10:00:00Z"
  },
  "etat_civil": {
    "prenom": "Jean",
    "nom": "Dupont",
    "date_naissance": "1987-04-12",
    "nationalites": ["FR"]
  },
  "coordonnees": {
    "emails": [
      {
        "adresse": "jean.dupont@example.fr",
        "principal": true,
        "verifie": true
      }
    ]
  },
  "adresses": [
    {
      "type_adresse": "residence_principale",
      "ligne_1": "12 rue des Lilas",
      "code_postal": "57000",
      "commune": "Metz",
      "pays": "FR"
    }
  ],
  "comptes_numeriques": [
    {
      "id_compte": "cmp-google-001",
      "service": "google",
      "identifiant_connexion": "jean.dupont@gmail.com",
      "mot_de_passe_fictif": "motdepasse_bidonnnn_2026",
      "double_facteur_active": true,
      "statut_compte": "actif"
    }
  ],
  "audit": {
    "date_creation": "2026-04-20T10:00:00Z",
    "date_mise_a_jour": "2026-04-20T13:45:00Z"
  },
  "extensions": {}
}
```
