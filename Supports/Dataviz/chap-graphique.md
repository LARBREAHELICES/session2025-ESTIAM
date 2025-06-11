### **Introduction à Pandas et la visualisation de données**

Avec Pandas, vous pouvez effectuer des opérations de nettoyage, de transformation, d'agrégation, et de visualisation sur vos données.

### **Installation des bibliothèques nécessaires**
Avant de commencer, assurez-vous que vous avez installé les bibliothèques suivantes :
```bash
pip install pandas matplotlib seaborn
```

### **Chargement des données**

```python
import pandas as pd

# Charger les données dans un DataFrame (exemple fictif)
data = {'event': ['view', 'addtocart', 'view', 'transaction', 'view', 'addtocart', 'transaction']}
events = pd.DataFrame(data)

```

### **Visualisation avec Matplotlib et Seaborn**

#### **1. Compter les occurrences de chaque événement**
Dans l'exemple suivant, nous allons afficher le nombre d'occurrences de chaque type d'événement dans le DataFrame. Cela nous aide à voir la répartition des différents événements comme "view", "addtocart" et "transaction".

```python
import matplotlib.pyplot as plt
import seaborn as sns

# Affichage des valeurs de chaque type d'événement
event_counts = events['event'].value_counts()
print(event_counts)
```

#### **2. Graphique en barres pour la répartition des événements**
Nous pouvons créer un graphique en barres pour afficher la distribution de chaque type d'événement dans notre DataFrame.

```python
# Visualisation des événements sous forme de graphique en barres
sns.countplot(x='event', data=events)
plt.title("Répartition des événements")
plt.xlabel("Type d'événement")
plt.ylabel("Nombre d'événements")
plt.show()
```

**Explication du code :**
- **`sns.countplot()`** : Cette fonction crée un graphique en barres en comptant les occurrences de chaque valeur dans la colonne spécifiée (ici `event`).
- **`plt.title()`** : Ajoute un titre au graphique.
- **`plt.xlabel()` et `plt.ylabel()`** : Ajoutent des labels aux axes x et y pour clarifier les données.
- **`plt.show()`** : Affiche le graphique.

#### **3. Graphique circulaire (camembert) pour la répartition des événements**
Un graphique circulaire peut être plus adapté pour visualiser la proportion de chaque événement par rapport aux autres. Nous allons utiliser `plt.pie()` pour créer un graphique en camembert.

```python
# Calcul des valeurs de 'event' pour créer un graphique circulaire
event_counts = events['event'].value_counts()
labels = event_counts.index
sizes = event_counts.values

# Explosion de la deuxième et troisième tranche pour mettre en évidence
explode = (0, 0.15, 0.15)  # Explose les tranches pour mettre en évidence

# Création d'une figure pour le graphique en camembert
plt.figure(figsize=(8, 8))
plt.pie(sizes, explode=explode, labels=labels, autopct='%1.1f%%', shadow=True, startangle=90)

# Assurer un aspect circulaire
plt.axis('equal')

# Affichage du graphique
plt.title("Répartition des événements (Camembert)")
plt.show()
```

**Explication du code :**
- **`plt.pie()`** : Crée un graphique circulaire.
  - **`sizes`** : Les tailles des tranches (les valeurs de chaque type d'événement).
  - **`explode`** : Permet d'exploser certaines tranches pour les mettre en évidence. Par exemple, on peut augmenter l'explosion de la tranche pour le type d'événement le plus fréquent.
  - **`autopct='%1.1f%%'`** : Affiche les pourcentages sur chaque tranche.
  - **`plt.axis('equal')`** : Cette commande assure que le graphique est bien circulaire.
  