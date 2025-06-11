# 🧮 Cours Complet : `groupby` et `pivot_table` avec Pandas

---

## 1. `groupby()` — Regrouper et agréger

La méthode `groupby()` permet de **regrouper un DataFrame** selon une ou plusieurs colonnes, puis d’**appliquer une fonction d’agrégation** (somme, moyenne, nombre, etc.).

### 🔧 Syntaxe générale :

```python
df.groupby("colonne_groupe")[colonne_valeurs].fonction()
```

### ✅ Exemple 1 — Moyenne par catégorie

```python
import pandas as pd

df = pd.DataFrame({
    "catégorie": ["A", "B", "A", "B", "C"],
    "valeur": [10, 20, 30, 40, 50]
})

print(df.groupby("catégorie")["valeur"].mean())
```

**Résultat :**

```
catégorie
A    20.0
B    30.0
C    50.0
```

---

### ✅ Exemple 2 — Nombre d’éléments par groupe (count)

```python
df.groupby("catégorie")["valeur"].count()
```

---

### ✅ Exemple 3 — Regrouper par **plusieurs colonnes**

```python
df2 = pd.DataFrame({
    "pays": ["FR", "FR", "US", "US", "FR"],
    "année": [2020, 2021, 2020, 2021, 2020],
    "ventes": [100, 150, 200, 300, 120]
})

résultat = df2.groupby(["pays", "année"])["ventes"].sum()
print(résultat)
```

**Résultat (MultiIndex)** :

```
pays  année
FR    2020    220
      2021    150
US    2020    200
      2021    300
Name: ventes, dtype: int64
```

---

### ✅ Exemple 4 — Agrégations multiples avec `.agg()`

```python
df2.groupby("pays").agg({
    "ventes": ["sum", "mean", "count"]
})
```

---

## 2. `pivot_table()` — Tableau croisé dynamique

La fonction `pivot_table()` permet de **réorganiser les données** en lignes/colonnes, à la manière d’un tableau croisé dynamique (comme dans Excel).

### 🔧 Syntaxe générale :

```python
pd.pivot_table(df, index="ligne", columns="colonne", values="valeurs", aggfunc="fonction")
```

---

### ✅ Exemple 5 — Moyenne de ventes par pays et année

```python
pivot = pd.pivot_table(df2, index="pays", columns="année", values="ventes", aggfunc="mean")
print(pivot)
```

**Résultat :**

```
année  2020  2021
pays              
FR       110   150
US       200   300
```

---

### ✅ Exemple 6 — Somme avec valeurs manquantes remplacées

```python
pivot = pd.pivot_table(df2, index="pays", columns="année", values="ventes", aggfunc="sum", fill_value=0)
```

---

### ✅ Exemple 7 — Plusieurs fonctions d’agrégation

```python
pd.pivot_table(df2, index="pays", columns="année", values="ventes", aggfunc=["sum", "mean"])
```

---

## 3. 📊 Comparatif : `groupby` vs `pivot_table`

| Aspect                  | `groupby`           | `pivot_table`                |
| ----------------------- | ------------------- | ---------------------------- |
| Agrégation              | Oui                 | Oui                          |
| Colonnes dynamiques     | Non                 | Oui (`columns=`)             |
| Multi-agrégation facile | Oui avec `.agg()`   | Oui avec `aggfunc=[...]`     |
| Résultat                | Series ou DataFrame | DataFrame (tableau croisé)   |
| Remplissage des NA      | Manuel              | Facile avec `fill_value=...` |

---

## 4. 🎯 Exemples pratiques avec `seaborn`

```python
import seaborn as sns
tips = sns.load_dataset("tips")
```

### ✅ Moyenne du total par jour (groupby)

```python
tips.groupby("day")["total_bill"].mean()
```

### ✅ Tableau croisé jour / moment (pivot\_table)

```python
pd.pivot_table(tips, index="day", columns="time", values="total_bill", aggfunc="mean")
```

---

Bien sûr, voici ton cours avec l’ajout de mon exemple simple d’explication des tables de pivot, placé après l’intro de la section `pivot_table()` sans toucher aux autres exemples :

---

## 2. `pivot_table()` — Tableau croisé dynamique

La fonction `pivot_table()` permet de **réorganiser les données** en lignes/colonnes, à la manière d’un tableau croisé dynamique (comme dans Excel).

### 🔧 Syntaxe générale :

```python
pd.pivot_table(df, index="ligne", columns="colonne", values="valeurs", aggfunc="fonction")
```

---

### 📦 Exemple simple d’explication d’une table de pivot

Imaginons un tableau de ventes :

| vendeur | région | ventes |
| ------- | ------ | ------ |
| Alice   | Nord   | 100    |
| Alice   | Sud    | 150    |
| Bob     | Nord   | 200    |
| Bob     | Sud    | 300    |

On souhaite savoir combien chaque vendeur a vendu dans chaque région.

```python
import pandas as pd

df = pd.DataFrame({
    "vendeur": ["Alice", "Alice", "Bob", "Bob"],
    "région": ["Nord", "Sud", "Nord", "Sud"],
    "ventes": [100, 150, 200, 300]
})

pivot = pd.pivot_table(df, index="vendeur", columns="région", values="ventes", aggfunc="sum")
print(pivot)
```

**Résultat :**

| région | Nord | Sud |
| ------ | ---- | --- |
| Alice  | 100  | 150 |
| Bob    | 200  | 300 |

---

**Explication :**

* `index="vendeur"` → les lignes sont les vendeurs
* `columns="région"` → les colonnes sont les régions
* `values="ventes"` → les valeurs affichées sont les ventes
* `aggfunc="sum"` → on somme les ventes pour chaque combinaison

Ainsi, on transforme une liste brute en tableau clair et synthétique.



## 5. 🧪 Exercices pratiques avec groupby

### Exercice 1 — Moyenne des notes par classe

```python
data = {
    "élève": ["Alice", "Bob", "Charlie", "David", "Eva"],
    "classe": ["A", "B", "A", "B", "A"],
    "note": [15, 12, 14, 11, 16]
}
df = pd.DataFrame(data)

df.groupby("classe")["note"].mean()
```

**Résultat :**

```
classe
A    15.0
B    11.5
```

---

### Exercice 2 — Somme des ventes par produit et région avec pivot

```python
data = {
    "produit": ["P1", "P1", "P2", "P2", "P1"],
    "région": ["Nord", "Sud", "Nord", "Sud", "Sud"],
    "ventes": [100, 150, 200, 300, 130]
}
df = pd.DataFrame(data)

pd.pivot_table(df, index="produit", columns="région", values="ventes", aggfunc="sum", fill_value=0)
```

**Résultat :**

```
région   Nord  Sud
produit            
P1        100  280
P2        200  300
```

---

## 6. ✅ À retenir

* `groupby()` est plus **souple pour manipuler les données par groupes**.
* `pivot_table()` est plus **lisible pour une visualisation matricielle**.

---

### 🔍 Explication du paramètre `observed` à partir de pandas 2.0

* **`observed=False`** (valeur par défaut) : le `groupby` inclura **toutes les combinaisons possibles** des catégories, même celles qui **n'existent pas dans les données**.
* **`observed=True`** : seules les **combinations réellement présentes** seront incluses.

---

### 📌 En pratique : quand faut-il le préciser ?

Tu **dois spécifier `observed=True`** dans un `groupby` avec plusieurs colonnes **si au moins une colonne est catégorielle (`category`)**, sinon tu risques une erreur ou un comportement inattendu (par exemple, des lignes vides).

---

### ✅ Exemple illustratif :

```python
import pandas as pd

df = pd.DataFrame({
    "genre": pd.Series(["F", "M", "F", "M"], dtype="category"),
    "classe": pd.Series(["A", "A", "B", "B"], dtype="category"),
    "note": [15, 12, 14, 10]
})

# groupby sur deux colonnes catégorielles
moyennes = df.groupby(["genre", "classe"], observed=True)["note"].mean()
print(moyennes)
```

**Sortie :**

```
genre  classe
F      A         15.0
       B         14.0
M      A         12.0
       B         10.0
Name: note, dtype: float64
```

---

### 🧪 Si on oublie `observed=True`

Sans ce paramètre, Pandas inclura **toutes les combinaisons possibles** même celles qui ne sont pas présentes dans les données :

```python
moyennes = df.groupby(["genre", "classe"])["note"].mean()
```

→ Cela **ne plante pas** mais **affiche aussi des lignes vides (NaN)** si des combinaisons n’existent pas dans les données.

---

### 🔁 Résumé rapide

| Type de colonne     | `observed=True` nécessaire ?  |
| ------------------- | ----------------------------- |
| colonnes `object`   | ❌ Non                         |
| colonnes `category` | ✅ Oui (si plusieurs colonnes) |

---
