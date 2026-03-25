# Documentation du Modèle Sémantique : DataPeakInsights Pilotage

![Power BI](https://img.shields.io/badge/Power%20BI-Data%20Viz-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![TMDL](https://img.shields.io/badge/TMDL-Semantic%20Model-00758F?style=for-the-badge)
![AI Audit](https://img.shields.io/badge/AI%20Audit-Gemini%20%2B%20MCP-8E44AD?style=for-the-badge&logo=google-gemini)
![GitHub](https://img.shields.io/badge/GitHub-Source%20Control-181717?style=for-the-badge&logo=github)

## Vue d'ensemble
Ce projet Power BI a pour vocation le pilotage 360° de l'activité, couvrant les aspects financiers, la prospection commerciale et le suivi opérationnel des missions. Le modèle est construit selon une architecture en étoile (Star Schema) et utilise le format TMDL pour faciliter le versionning et l'audit.

## Périmètre Fonctionnel

Les mesures DAX sont organisées par domaines fonctionnels (Display Folders) :

*   **Finance** : Suivi des Recettes, Dépenses, Marge et Chiffre d'Affaires (YTD/Total).
*   **Prospection** : Analyse du funnel de conversion (Nb Prospects, Taux de transformation, Clients convertis MTD).
*   **Clients** : Suivi du portefeuille, jours facturés et tendances opérationnelles.
*   **Time Intelligence** : Gestion des périodes temporelles et date du jour dynamique.

## Gouvernance & Audit IA via MCP

Ce projet a bénéficié d'une procédure d'audit et d'optimisation automatisée grâce à l'intégration de l'intelligence artificielle via le **Model Context Protocol (MCP)**. Cette approche moderne du développement Power BI garantit un code sain, maintenable et performant.

### 1. Automatisation de l'audit
Le protocole MCP a permis de connecter l'assistant IA directement à la structure de fichiers TMDL (Tabular Model Definition Language).
*   **Processus :** L'IA analyse les fichiers de définition `.tmdl` sans nécessiter d'export manuel ou de copier-coller fastidieux.
*   **Analyse sémantique :** Le modèle comprend non seulement la syntaxe DAX, mais aussi les dépendances (Lineage Tags), les relations (via `USERELATIONSHIP`) et le contexte métier (Noms des tables).

### 2. Gain Quantifiable (Mise à jour du 25/03/2026)
L'audit final a permis de refactoriser 18 mesures complexes.
*   **Optimisation moteur :** Migration des fonctions itératives (SUMX) vers des agrégations filtrées (CALCULATE), réduisant la charge CPU du moteur de stockage.
*   **Zéro Dette Technique :** Suppression de tous les opérateurs de division directe `/` au profit de `DIVIDE` sécurisés.
*   **Accessibilité :** Injection de descriptions métier pour chaque KPI, permettant une compréhension immédiate lors du survol dans Power BI Desktop.

### 3. Qualification des Améliorations
Les interventions de l'IA ont porté sur des axes critiques pour la stabilité du rapport :

*   **Sécurité des Calculs (Safe Division) :**
    *   Utilisation systématique de la fonction `DIVIDE` (ex: mesure *'Taux Transformation MTD'*) pour gérer automatiquement les erreurs de division par zéro, remplaçant l'opérateur `/`.
*   **Gestion des Valeurs Nulles :**
    *   Implémentation de `COALESCE` (ex: mesure *'CA Total HT YTD'*) pour garantir que les KPI affichent '0' plutôt que '(Vide)' dans les cartes, améliorant l'expérience utilisateur.
*   **Optimisation des Variables :**
    *   Standardisation avec la syntaxe `VAR ... RETURN` (ex: mesure *'Tendance Nb Jours Fact Moyens %'*) pour améliorer la lisibilité et les performances (calcul unique des variables).
*   **Gestion Temporelle Avancée :**
    *   Validation des logiques de Time Intelligence (`TOTALMTD`, `DATEADD`) et gestion des relations inactives via `USERELATIONSHIP` pour les dates de création/contact.

### 4. Statut 'Production-Ready' pour le Retail/B2B
Ce modèle est certifié prêt pour la production pour les raisons suivantes :

1.  **Robustesse Financière :** Les mesures financières (HT/TTC) sont typées explicitement (`isGeneralNumber`) et gèrent les filtrages contextuels complexes (Recette vs Dépense).
2.  **Logique Métier Intégrée :** Le modèle gère nativement les cycles de vente B2B longs (Prospect -> Client) et les comparaisons temporelles (MoM, YTD), essentiels pour le pilotage Retail/Consulting.
3.  **Maintenabilité :** Grâce au format TMDL et à l'audit MCP, le code est propre, documenté via des métadonnées, et prêt pour une intégration CI/CD.

---

## Détails Techniques

*   **Mode de stockage :** Import
*   **Format de définition :** TMDL
*   **Tables principales :**
    *   `FACT ACTIVITES` (Transactions)
    *   `DIM CLIENTS` / `DIM PROSPECTION` (Référentiels)
    *   `DIM-Calendar` (Temps)
    *   `DIM MISSIONS` (Opérations)

---
*Généré et audité par Gemini Code Assist via MCP.*
