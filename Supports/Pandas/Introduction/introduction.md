# 🐼 1. Qu’est-ce que Pandas ?

Pandas (Panel Data) est une bibliothèque Python pour :

* manipuler des **données tabulaires** (colonnes, lignes),
* importer/exporter des fichiers (CSV, Excel, JSON…),
* faire du **nettoyage, du tri, du filtrage, des agrégations**,
* être compatible avec NumPy et Matplotlib.

---

## ⚙️ 2. Installation

```bash
pip install pandas
```

---

## 📋 3. Structures principales

### 📄 `Series` : vecteur 1D (comme une colonne)

```python
import pandas as pd

s = pd.Series([10, 20, 30], index=["a", "b", "c"])
print(s["b"])  # 20
```

### 📊 `DataFrame` : tableau 2D (équivalent Excel)

```python
df = pd.DataFrame({
    "name": ["Alice", "Bob", "Charlie"],
    "age": [25, 30, 35]
})
print(df["name"])      # Colonne
print(df.loc[1])       # Ligne par label
print(df.iloc[0])      # Ligne par index
```

---

## 📥 4. Import de données

```python
df = pd.read_csv("data.csv")
df = pd.read_excel("fichier.xlsx")
df = pd.read_json("data.json")
```

> 🔄 Pour exporter : `df.to_csv("out.csv")`, `df.to_excel(...)`

---

## 🔍 5. Exploration rapide

```python
df.head()          # 5 premières lignes
df.tail(3)         # 3 dernières lignes
df.shape           # (nb_lignes, nb_colonnes)
df.columns         # liste des colonnes
df.info()          # types et nulls
df.describe()      # stats numériques
```

---

## 🔁 6. Sélection et filtrage

```python
df["age"]                # Une colonne
df[["name", "age"]]      # Plusieurs colonnes
df.loc[0]                # Ligne par étiquette
df.iloc[2]               # Ligne par index

# Filtrage conditionnel
df[df["age"] > 30]
df[df["name"].str.startswith("A")]
```

---

## 🔄 7. Modification

```python
df["age"] = df["age"] + 1         # Ajout ou modification
df["is_adult"] = df["age"] >= 18  # Nouvelle colonne booléenne
df["name_upper"] = df["name"].str.upper()
```

---

## 🧹 8. Nettoyage

```python
df.drop(columns=["colonne1"])         # Supprimer colonne
df.drop(index=[0, 2])                 # Supprimer lignes
df = df.dropna()                      # Supprime lignes avec NaN
df = df.fillna(0)                     # Remplace NaN par 0
df.rename(columns={"name": "prenom"}) # Renommer
```

---

## 🧮 9. Groupes et agrégation

```python
df.groupby("sexe")["age"].mean()
df.groupby("classe").agg({
    "math": "mean",
    "anglais": "sum"
})
```

---

## 🔢 10. Tri et index

```python
df.sort_values("age")              # Tri croissant
df.sort_values("age", ascending=False)  # Tri décroissant
df.set_index("id", inplace=True)   # Changer l'index
```

---

## 🧠 Exemple pratique

### Moyenne des notes par élève

```python
df = pd.DataFrame({
    "nom": ["Alice", "Bob", "Alice", "Bob"],
    "matière": ["math", "math", "fr", "fr"],
    "note": [15, 12, 17, 14]
})

df.groupby("nom")["note"].mean()
```

→ Résultat : moyenne par élève

---

## 🧠 Récapitulatif des méthodes clés

| Objectif           | Méthode                    |
| ------------------ | -------------------------- |
| Lire un fichier    | `read_csv`, `read_excel`   |
| Aperçu rapide      | `head`, `info`, `describe` |
| Filtrer            | `df[cond]`, `loc`, `iloc`  |
| Créer / modifier   | `df["col"] = ...`          |
| Nettoyer           | `drop`, `fillna`, `dropna` |
| Grouper et agréger | `groupby`, `agg`           |
| Trier              | `sort_values()`            |

---

### 🎭 Qu’est-ce qu’un masque ?

```python
df = pd.DataFrame({
    "name": ["Alice", "Bob", "Charlie"],
    "age": [25, np.nan, 35]
})
```

Un **masque** est une **`Series` ou `array` de booléens** (`True`/`False`) utilisée pour **sélectionner des lignes ou des colonnes** dans un `DataFrame`.

---

### 🧱 Masques pour **lignes**

✔️ Masque aligné sur **l’index** (lignes)
👉 `df[mask]` ou `df.loc[mask]`

```python
mask = df["age"] > 30
df[mask]         # sélectionne les lignes où l'âge > 30
```

---

### 🧱 Masques pour **colonnes**

✔️ Masque aligné sur **les colonnes**
👉 `df.loc[:, mask]`

```python
mask = df.isna().any(axis=0)  # Series booléenne sur les colonnes
df.loc[:, ~mask]              # garde les colonnes sans NaN

df.T[~df.T.isna().any(axis=1)].T # moins lisible
```

---

### ⚠️ Erreurs classiques

```python
df[mask_cols]  # ❌ fonctionne SEULEMENT si mask_cols est aligné sur l’index
```

---

### ✅ Rappel synthétique

| Objectif             | Masque aligné sur… | Syntaxe                      |
| -------------------- | ------------------ | ---------------------------- |
| Filtrer des lignes   | `df.index`         | `df[mask]` ou `df.loc[mask]` |
| Filtrer des colonnes | `df.columns`       | `df.loc[:, mask]`            |

---

Si tu veux une fiche mémo ou un visuel, je peux aussi te le générer.
