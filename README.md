# 🎯 Moteur de Recommandation avec Neo4j (Yelp Dataset)

> **Projet Universitaire 

---

## 💡 Le Concept
Ce projet explore la puissance des **Bases de Données Orientées Graphe** pour résoudre des problèmes que le SQL traditionnel peine à traiter : l'analyse de réseaux complexes et la recommandation sociale.

Nous avons utilisé le **Yelp Open Dataset** pour construire un moteur capable de recommander des commerces non pas seulement en fonction de leur note moyenne, mais en fonction de l'**influence réelle** des utilisateurs qui les fréquentent.

---

## 🚩 La Problématique
Dans une base de données classique (relationnelle), répondre à la question *"Quels sont les restaurants préférés des amis de mes amis ?"* nécessite des jointures coûteuses qui ralentissent le système.

**Notre objectif :**
1.  **Migrer** des données plates (fichiers JSON) vers un Graphe connecté.
2.  **Analyser** la structure du réseau (Qui est influent ? Qui suit qui ?).
3.  **Comparer** deux stratégies de recommandation : la quantité (Popularité) vs la qualité (PageRank).

---

## 🏗️ Architecture du Graphe
[cite_start]Nous avons modélisé les interactions sous forme de nœuds et de relations sémantiques [cite: 176-186] :

* **User** (Utilisateur)
* **Review** (Avis écrit)
* **Business** (Commerce noté)
* **Category** (Type de commerce)

> **Le flux de donnée :** `(Utilisateur) --[A ÉCRIT]--> (Avis) --[CONCERNE]--> (Commerce)`

---

## ⚙️ Méthodologie Technique

### 1. Ingestion et Nettoyage (ETL)
Nous avons utilisé la librairie **APOC** pour transformer des données brutes hétérogènes.
* **Challenge :** Gestion de la volumétrie (Millions d'utilisateurs).
* [cite_start]**Solution :** Échantillonnage intelligent et création de nœuds "à la volée" (Stub Nodes) pour préserver l'intégrité du graphe social même avec un jeu de données partiel [cite: 217-218].

### 2. Stratégies de Recommandation
Nous avons implémenté deux algorithmes pour comparer leurs résultats :

* **Approche A : La Popularité (Quantitative)**
    * *Méthode :* On compte simplement le nombre d'avis reçus.
    * *Résultat :* Met en avant les chaînes de fast-food et les lieux touristiques très fréquentés.
    * *Limite :* Biais de volume.

* **Approche B : L'Influence (Qualitative)**
    * *Méthode :* Algorithme **PageRank** (via *Graph Data Science Library*).
    * *Principe :* Un commerce est recommandé s'il est validé par des utilisateurs eux-mêmes influents dans le réseau.
    * *Résultat :* Met en avant des établissements de qualité, validés par la communauté experte.

---

## 🏆 Résultats et Conclusion
L'analyse comparative montre que l'approche **Graphe (PageRank)** est supérieure pour filtrer le "bruit".

| Méthode | Type de recommandation |
| :--- | :--- |
| **Popularité** | "Le McDo du centre-ville" (Beaucoup d'avis, qualité standard) |
| **PageRank** | "Le petit bistro local" (Moins d'avis, mais validé par des experts) |

[cite_start]**Conclusion :** Le graphe permet de passer d'une simple statistique de volume à une véritable **métrique de confiance** [cite: 366-368].

---

## 🛠️ Stack Technique
* **Base de Données :** Neo4j
* **Langage de requête :** Cypher
* **Bibliothèques :**
    * `APOC` (Pour l'ETL et le nettoyage)
    * `GDS` (Graph Data Science pour les algorithmes)
* **Données :** Yelp Open Dataset

---
*Projet réalisé le 15 Janvier 2026.*
