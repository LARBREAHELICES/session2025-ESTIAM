
```python
average_score = round(
    sum(student['score'] for student in students) / len(students), 2
)
```

### Explication :

1. **`students`**
   → C’est une **liste de dictionnaires**, où chaque dictionnaire représente un élève avec au moins une clé `'score'` contenant sa note.
   Exemple :

   ```python
   students = [
       {"name": "Alice", "score": 15},
       {"name": "Bob", "score": 18},
       {"name": "Charlie", "score": 12}
   ]
   ```

2. **`student['score'] for student in students`**
   → C’est une **compréhension de générateur** qui extrait uniquement les scores de chaque élève dans la liste.

3. **`sum(...)`**
   → Calcule la **somme de tous les scores** extraits par la ligne précédente.

4. **`len(students)`**
   → Donne le **nombre total d'élèves**, pour pouvoir faire la moyenne.

5. **`sum(...) / len(students)`**
   → Fait la **moyenne des scores**.

6. **`round(..., 2)`**
   → Arrondit le résultat de la moyenne à **2 chiffres après la virgule**.

7. **`average_score = ...`**
   → Stocke le résultat dans la variable `average_score`.

### Exemple complet :

```python
students = [
    {"name": "Alice", "score": 15},
    {"name": "Bob", "score": 18},
    {"name": "Charlie", "score": 12}
]

average_score = round(sum(student['score'] for student in students) / len(students), 2)

print(average_score)  # Affiche : 15.0
```

👉 Ce code calcule donc **la moyenne des notes** des élèves et l'arrondit à 2 chiffres après la virgule.
