# 📊 Documentation du Modèle Sémantique : DataPeakInsights Pilotage

![Power BI](https://img.shields.io/badge/Power%20BI-Data%20Viz-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![TMDL](https://img.shields.io/badge/TMDL-Semantic%20Model-00758F?style=for-the-badge)
![AI Audit](https://img.shields.io/badge/AI%20Audit-Gemini%20%2B%20MCP-8E44AD?style=for-the-badge&logo=google-gemini)
![GitHub](https://img.shields.io/badge/GitHub-Source%20Control-181717?style=for-the-badge&logo=github)
![Status](https://img.shields.io/badge/Status-Production%20%26%20WIP-orange?style=for-the-badge)

## 🎯 Vue d'ensemble
Ce projet Power BI assure le pilotage 360° de l'activité DataPeakInsights, couvrant la santé financière, la prospection commerciale et le suivi opérationnel des missions[cite: 3]. Le modèle est conçu selon une architecture en étoile (Star Schema) et exploite le format moderne **TMDL (Tabular Model Definition Language)** pour optimiser le versionnement et la gouvernance par l'IA.

---

## 🚧 Roadmap & Scalabilité (Work In Progress)

Dans une démarche d'amélioration continue, la couche de données évolue actuellement vers une architecture multi-sources automatisée :

* **Nouvelles Sources d'Ingestion :** Connexion et synchronisation via les API REST de **Ceasy** et **Medius Expense** (gestion opérationnelle et notes de frais).
* **Refonte de la Modélisation CRM :** Remodélisation du MCD Airtable pour supporter la montée en charge du volume de prospects et clients.
* **Automatisation du Pipeline :** Pipeline d'actualisation hybride garantissant l'intégrité du modèle sémantique lors des requêtes multi-APIs.

---

## 📌 Périmètre Fonctionnel

Les mesures DAX sont organisées de manière rigoureuse au sein de dossiers d'affichage (*Display Folders*) :

* **Finance :** Suivi des Recettes, Dépenses, Marge opérationnelle et Chiffre d'Affaires (YTD/Total).
* **Prospection :** Analyse fine du funnel de conversion (Volume de prospects, Taux de transformation, Clients convertis MTD).
* **Clients :** Suivi du portefeuille client, calcul des jours facturés et tendances d'activité.
* **Time Intelligence :** Calculs temporels dynamiques et gestion des décalages calendaires (MoM, YTD, Date du jour).

---

## 🤖 Gouvernance & Audit IA via MCP

Ce projet intègre un workflow de gouvernance automatisé grâce au **Model Context Protocol (MCP)** couplé à l'IA (Gemini Code Assist), garantissant un code propre, performant et exempt de dette technique.

### 1. Automatisation du Code Audit
Le protocole MCP permet la connexion directe de l'assistant IA à la structure TMDL :
* **Analyse native :** Traitement fluide des fichiers `.tmdl` sans export manuel.
* **Compréhension contextuelle :** Contrôle précis des dépendances (*Lineage Tags*), des relations inactives (`USERELATIONSHIP`) et des métadonnées métier.

### 2. Gains & Refactorisation DAX
Une passe d'audit sur 18 mesures clés a permis d'atteindre les standards d'ingénierie suivants :
* **Sécurité des calculs (*Safe Division*) :** Remplacement systématique des opérateurs `/` par la fonction `DIVIDE` pour prévenir toute erreur de division par zéro.
* **Expérience utilisateur (UX) :** Implémentation de `COALESCE` sur les cartes de KPI pour afficher `0` au lieu de `(Vide)`.
* **Optimisation des performances :** Migration des fonctions itératives (`SUMX`) vers `CALCULATE` et généralisation du pattern `VAR ... RETURN` pour soulager le moteur de stockage (*VertiPaq*).
* **Documentation embarquée :** Injection de descriptions sémantiques pour chaque KPI, visibles au survol dans Power BI Desktop.

---

## 🛠️ Détails Techniques

* **Mode de stockage :** Import (VertiPaq)
* **Format de définition :** TMDL (Tabular Model Definition Language)
* **Architecture :** Modèle en étoile (*Star Schema*)
* **Tables Principales :**
  * `FACT ACTIVITES` *(Table de faits - Transactions)*
  * `DIM CLIENTS` / `DIM PROSPECTION` *(Référentiels métier)*
  * `DIM MISSIONS` *(Suivi opérationnel)*
  * `DIM-Calendar` *(Dimension temporelle personnalisée)*

---
*Généré et maintenu avec l'appui de Gemini Code Assist via MCP.*
