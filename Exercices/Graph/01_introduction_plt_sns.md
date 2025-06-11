# 01 Exercice

1. Représentez graphiquement les données qui vous semble pertinentes

```python
# Charger un jeu de données fictif
data = {
    'product_id': [101, 102, 103, 104, 105, 106, 107, 108, 109, 110],
    'category': ['Electronics', 'Clothing', 'Electronics', 'Home', 'Clothing', 'Electronics', 'Home', 'Clothing', 'Electronics', 'Clothing'],
    'price': [150, 40, 200, 50, 30, 180, 60, 45, 220, 55],
    'quantity_sold': [30, 50, 25, 40, 60, 20, 35, 45, 15, 70],
    'date': pd.to_datetime(['2025-01-01', '2025-01-02', '2025-01-03', '2025-01-04', '2025-01-05', '2025-01-06', '2025-01-07', '2025-01-08', '2025-01-09', '2025-01-10']),
    'region': ['North', 'South', 'East', 'West', 'North', 'South', 'East', 'West', 'North', 'South']
}

# Convertir en DataFrame
df = pd.DataFrame(data)
```