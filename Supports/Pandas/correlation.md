## 📊 Qu’est-ce que la corrélation ?

La **corrélation** mesure **la relation entre deux variables**. Elle nous dit si deux choses évoluent ensemble, et comment :

* **Corrélation positive (+1)** : quand une variable augmente, l’autre augmente aussi (exemple : taille et poids).
* **Corrélation négative (-1)** : quand une variable augmente, l’autre diminue (exemple : nombre d’heures de jeu vidéo et notes scolaires).
* **Pas de corrélation (0)** : les variables n’ont pas de lien visible.

---

## 🔍 Comment l’interpréter ?

La corrélation est un nombre entre **-1 et +1**.

| Valeur | Signification              |
| ------ | -------------------------- |
| +1     | Relation positive parfaite |
| 0      | Pas de relation            |
| -1     | Relation négative parfaite |

---

## 🧮 Exemple simple

Imaginons :

| Heures d’étude | Note au contrôle |
| -------------- | ---------------- |
| 1              | 10               |
| 2              | 12               |
| 3              | 14               |
| 4              | 16               |

La corrélation est proche de +1 : plus on étudie, meilleure est la note.

---

## 📈 En Python avec Pandas

```python
import pandas as pd

data = {
    "heures_etude": [1, 2, 3, 4],
    "note": [10, 12, 14, 16]
}

df = pd.DataFrame(data)

corr = df["heures_etude"].corr(df["note"])
print(corr)
```

**Sortie :**

```
1.0
```

Cela montre une corrélation positive parfaite.

---

## ⚠️ Attention

La corrélation **ne signifie pas causalité** : deux variables peuvent évoluer ensemble sans qu’il y ait un lien de cause à effet.

## Comment rédiger une réponse sur la corrélation 


**La corrélation mesure la relation entre deux variables.**
Elle indique si elles évoluent ensemble et dans quel sens :

* Une corrélation **positive** (proche de +1) signifie que quand une variable augmente, l’autre augmente aussi.
* Une corrélation **négative** (proche de -1) signifie que quand une variable augmente, l’autre diminue.
* Une corrélation proche de **0** signifie qu’il n’y a pas de lien apparent entre les deux variables.

La corrélation est un nombre entre -1 et +1 qui exprime cette relation.

---

**Exemple simple :**
Si on regarde les heures d’étude et les notes d’un élève, on peut trouver une corrélation positive, car plus on étudie, plus la note tend à augmenter.

---

**Important :**
La corrélation ne prouve pas qu’une variable cause l’autre, elle montre juste qu’elles sont liées.

---

**En Python, on peut calculer la corrélation avec Pandas :**

```python
corr = df["heures_etude"].corr(df["note"])
print(corr)
```

---