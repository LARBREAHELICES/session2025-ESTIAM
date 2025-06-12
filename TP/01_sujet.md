# 🧪 TP Pandas — Analyse de données sur les pourboires (`tips.csv`)

## 🛠️ Dépendances

```bash
pip install seaborn matplotlib scipy pandas
```

**Documentez votre code** et préparez-vous à expliquer certains passages dans un fichier `README.md`.

Lorsque cela est pertinent, vous pouvez illustrer votre travail avec des graphiques. Veillez cependant à bien choisir le type de graphique : il doit illustrer votre réponse de manière **cohérente** et **lisible**.

💡 Pensez à mettre votre travail dans Teams avec votre/vos nom(s).

Remarque pour télécharger les données à étudier 

```python

import seaborn as sns
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

# Chargement des données
tips = sns.load_dataset("tips")
```

---

## 💡 Recommandation

Vous pouvez utiliser la méthode `.to_numpy()` : elle permet de convertir une **série** ou un **DataFrame** Pandas en **tableau NumPy**, ce qui est utile pour des traitements vectorisés ou des algorithmes nécessitant ce format.


## 🎯 Objectif

Explorer, manipuler et analyser un jeu de données réels avec **Pandas**, **Matplotlib** et **seaborn**.

## 📁 Jeu de données

```python
import seaborn as sns
import pandas as pd

tips = sns.load_dataset("tips")
```

---

## 📋 Structure des données

* `total_bill` : montant total de l'addition
* `tip` : pourboire
* `sex` : sexe du serveur
* `smoker` : tabagisme (Yes/No)
* `day` : jour de la semaine
* `time` : déjeuner ou dîner
* `size` : nombre de personnes à table

---

## 🧠 Questions (notées sur 50 points)

---

### **1. Aperçu et types (2 pts)**

Affiche :

* les 5 premières lignes,
* les noms de colonnes,
* le type de chaque colonne.

---

### **2. Statistiques descriptives (3 pts)**

Affiche les statistiques de base pour `total_bill`, `tip`, et `size` :

* moyenne,
* écart-type,
* min/max,
* quartiles.

---

### **3. Valeurs manquantes (2 pts)**

Y a-t-il des valeurs manquantes ? Si oui, lesquelles et combien ?

Précisez votre démarche pour rechercher les données manquantes dans votre fichier `README.md`.

---

### **4. Histogrammes (3 pts)**

Trace les histogrammes de `total_bill` et `tip` (20 classes chacun). Interprète la distribution.

---

### **5. Moyennes groupées (3 pts)**

Affiche la moyenne des pourboires (`tip`) par :

* `sex`,
* `smoker`,
* `day`.

---

### **6. Pourboire moyen par nombre de personnes (2 pts)**

Quelle est la moyenne des pourboires en fonction de la taille de la table (`size`) ?

---

### **7. Table croisée (3 pts)**

Crée une table croisée (pivot table) des pourboires moyens par `day` et `time`.

---

### **8. Proportion des fumeurs (2 pts)**

Quel est le pourcentage de fumeurs dans l'échantillon ? Différence entre hommes et femmes ?

---

### **9. Boîte à moustaches (`boxplot`) (3 pts)**

Trace un `boxplot` de `tip` par `day`. Quels jours présentent une plus grande variabilité ?

---

### **10. Scatterplot (3 pts)**

Trace un nuage de points entre `total_bill` et `tip`. Quelle tendance observe-t-on ?

---

### **11. Corrélations linéaires (5 pts)**

Calcule la **corrélation de Pearson** entre :

* `total_bill` et `tip`,
* `size` et `tip`.

Donne la valeur du **coefficient** et du **p-value**. Interprète.

---

### **12. Corrélations catégorielles (4 pts)**

Calcule les corrélations entre les variables catégorielles (`sex`, `smoker`, `day`, `time`) et le montant du pourboire moyen. Tu peux t'aider de :

```python
tips.groupby("sex")["tip"].mean()
```

---

### **13. Différences (5 pts)**

Y a-t-il une différence significative entre les pourboires des **fumeurs** et **non-fumeurs** ?

---

### **14. Pourboire proportionnel à l'addition (3 pts)**

Crée une nouvelle colonne `tip_pct = tip / total_bill`. Calcule sa moyenne et son écart-type.

---

### **15. Qui donne les plus gros pourboires en proportion ? (4 pts)**

Compare `tip_pct` par :

* `sex`
* `smoker`
* `day`

---

### **16. Conversion en NumPy (2 pts)**

Convertis les colonnes `total_bill` et `tip` en un tableau NumPy 2D. Quelle est la forme du tableau ? Que représente chaque dimension ?

---

### **17. Calculs vectorisés (3 pts)**

Utilise **NumPy** pour calculer, sans boucle explicite :

* le pourboire moyen,
* le pourboire maximal,
* et la somme des pourboires pour les additions supérieures à 30 €.

---

### **18. Filtrage conditionnel avec NumPy (3 pts)**

À l’aide de **NumPy**, récupère tous les pourboires (colonne `tip`) associés à un nombre de personnes (`size`) supérieur ou égal à 4. Quelle est leur moyenne ?

---

### **19. Indexation booléenne avec Pandas (2 pts)**

Avec Pandas uniquement, sélectionne toutes les lignes où le pourboire représente plus de 20% de l’addition (`tip_pct > 0.2`). Combien de cas cela concerne-t-il ?

---

### **20. Application de fonctions personnalisées (3 pts)**

Crée une fonction Python qui catégorise les pourboires :

```python
def tip_level(tip):
    if tip < 2:
        return "faible"
    elif tip < 5:
        return "moyen"
    else:
        return "élevé"
```

Utilise `.apply()` pour créer une nouvelle colonne `tip_level`. Affiche la répartition des catégories.

---

### **21. Création de colonnes avec `np.where` (2 pts)**

Crée une colonne `"is_large_party"` valant `True` si `size >= 4`, sinon `False`, en utilisant `np.where`.

---

### **22. Tri avec NumPy (2 pts)**

Trie les `total_bill` avec **NumPy** et affiche les 10 plus grandes additions.

---

### **23. Groupes et écart-type (3 pts)**

Utilise Pandas pour grouper par `day` et afficher l’écart-type du `tip_pct`. Quel jour est le plus variable ?

---

### **24. Masquage NumPy avancé (3 pts)**

Crée un masque NumPy pour détecter les pourboires :

* supérieurs à 5 €,
* lors du dîner (`time == "Dinner"`),
* par des fumeurs (`smoker == "Yes"`).

Affiche combien de lignes respectent ces 3 conditions.

---

### **25. Jointure avec concaténation (2 pts)**

Sépare les données en deux DataFrames : un pour les hommes (`sex == "Male"`), un pour les femmes. Puis concatène-les verticalement et vérifie si l’index est bien conservé ou non.

---
