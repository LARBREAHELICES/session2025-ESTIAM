# Plan de la semaine

1. Révision Python - Numpy et Pandas

2. Présentation d'Airflow avec Docker pour définir un pipeline

3. Mini projet en équipe 

## Installation

## Commandes

```
docker build -t etl-jupyter-light .
docker run -it --rm -p 8887:8888 -v $(pwd):/app etl-jupyter-light
```

Pour ce connecter : http://127.0.0.1:8887lab?token=XXX